---
title: Verbessern der Resilienz
titleSuffix: Azure Machine Learning
description: Hier erfahren Sie, wie Sie die Resilienz Ihrer Azure Machine Learning-Ressourcen gegenüber Ausfällen mithilfe einer Hochverfügbarkeitskonfiguration verbessern.
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: conceptual
ms.author: jhirono
author: jhirono
ms.reviewer: larryfr
ms.date: 07/16/2020
ms.openlocfilehash: 9b298e10d3eb95bcb0ef525eb973259a3ab1dbbb
ms.sourcegitcommit: b33c9ad17598d7e4d66fe11d511daa78b4b8b330
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88852546"
---
# <a name="increase-azure-machine-learning-resiliency"></a>Verbessern der Resilienz von Azure Machine Learning

[!INCLUDE [aml-applies-to-basic-enterprise-sku](../../includes/aml-applies-to-basic-enterprise-sku.md)]

In diesem Artikel erfahren Sie, wie Sie die Resilienz Ihrer Microsoft Azure Machine Learning-Ressourcen mithilfe einer Hochverfügbarkeitskonfiguration verbessern. Sie können die Azure-Dienste, von denen Azure Machine Learning abhängig ist, für Hochverfügbarkeit konfigurieren. Dieser Artikel zeigt die Dienste auf, die Sie für Hochverfügbarkeit konfigurieren können, sowie Links zu weiteren Informationen zur Konfiguration dieser Ressourcen.

> [!NOTE]
> Azure Machine Learning selbst bietet keine Notfallwiederherstellung.

## <a name="understand-azure-services-for-azure-machine-learning"></a>Grundlegendes zu Azure-Diensten für Azure Machine Learning

Azure Machine Learning ist von mehreren Azure-Diensten abhängig und verfügt über mehrere Ebenen. Einige dieser Dienste werden in Ihrem Abonnement (Kundenabonnement) bereitgestellt. Sie sind für die Hochverfügbarkeitskonfiguration dieser Dienste verantwortlich. Andere Dienste werden in einem Microsoft-Abonnement erstellt und von Microsoft verwaltet. 

Die Azure-Dienste umfassen Folgendes:

* **Azure Machine Learning-Infrastruktur**: Eine von Microsoft verwaltete Umgebung für den Azure Machine Learning-Arbeitsbereich.

* **Zugeordnete Ressourcen**: Ressourcen, die während der Erstellung des Azure Machine Learning-Arbeitsbereichs in Ihrem Abonnement bereitgestellt werden. Zu diesen Ressourcen zählen Azure Storage, Azure Key Vault, Azure Container Registry (ACR) und Application Insights. Sie sind für das Konfigurieren von Hochverfügbarkeitseinstellungen für diese Ressourcen verantwortlich.
  * Standardspeicher enthält Daten wie etwa Modelle, Trainingsprotokolldaten und Datasets.
  * Key Vault enthält Anmeldeinformationen für Azure Storage, Container Registry und Datenspeicher.
  * Container Registry enthält ein Docker-Image für die Trainings- und Rückschlussumgebungen.
  * Application Insights dient zum Überwachen von Azure Machine Learning.

* **Computeressourcen**: Ressourcen, die Sie nach der Bereitstellung des Arbeitsbereichs erstellen. Beispielsweise können Sie eine Compute-Instanz oder einen Computecluster erstellen, um ein Machine Learning-Modell zu trainieren.
  * Compute-Instanz und Computecluster: Von Microsoft verwaltete Umgebungen für die Modellentwicklung.
  * Weitere Ressourcen: Microsoft Computeressourcen, die an Azure Machine Learning angefügt werden können, z. B. Azure Kubernetes Service (AKS), Azure Databricks, Azure Container Instances und Azure HDInsight. Sie sind für das Konfigurieren von Hochverfügbarkeitseinstellungen für diese Ressourcen verantwortlich.

* **Zusätzliche Datenspeicher**: Azure Machine Learning kann für Trainingsdaten zusätzliche Datenspeicher einbinden, z. B. Azure Storage, Azure Data Lake Storage und Azure SQL-Datenbank.  Diese Datenspeicher werden in Ihrem Abonnement bereitgestellt. Sie sind für das Konfigurieren ihrer Hochverfügbarkeitseinstellungen verantwortlich.

Die folgende Tabelle zeigt, von wem die Azure-Dienste verwaltet werden (von Microsoft oder Ihnen) und welche Dienste standardmäßig hochverfügbar sind.

| Dienst | Verwaltet von | Hochverfügbarkeit standardmäßig |
| ----- | ----- | ----- |
| **Azure Machine Learning-Infrastruktur** | Microsoft | |
| **Zugeordnete Ressourcen** |
| Azure Storage | Sie | |
| Key Vault | Sie | ✓ |
| Container Registry | Sie | |
| Application Insights | Sie | Nicht verfügbar |
| **Computeressourcen** |
| Compute-Instanz | Microsoft |  |
| Computecluster | Microsoft |  |
| Andere Computeressourcen, z. B. AKS, <br>Azure Databricks, Container Instances, HDInsight | Sie |  |
| **Zusätzliche Datenspeicher** wie Azure Storage, SQL-Datenbank,<br> Azure Database for PostgreSQL und Azure Database for MySQL und <br>Azure Databricks File System | Sie | |

Im weiteren Verlauf dieses Artikels werden die Aktionen beschrieben, die Sie durchführen müssen, damit die einzelnen Dienste hochverfügbar werden.

## <a name="associated-resources"></a>Zugeordnete Ressourcen

> [!IMPORTANT]
> Azure Machine Learning unterstützt kein Failover des Standardspeicherkontos mit georedundantem Speicher (GRS), geozonenredundantem Speicher (GZRS), georedundantem Speicher mit Lesezugriff (RA-GRS) oder geozonenredundantem Speicher mit Lesezugriff (RA-GZRS).

Stellen Sie sicher, dass Sie die Einstellungen für Hochverfügbarkeit der einzelnen Ressourcen konfigurieren, indem Sie die folgende Dokumentation zu Rate ziehen:

* **Azure Storage**: Informationen zum Konfigurieren der Hochverfügbarkeitseinstellungen finden Sie unter [Azure Storage-Redundanz](https://docs.microsoft.com/azure/storage/common/storage-redundancy).
* **Key Vault:** Key Vault bietet standardmäßig Hochverfügbarkeit und erfordert keine Benutzeraktion.  Weitere Informationen finden Sie unter [Azure Key Vault: Verfügbarkeit und Redundanz](https://docs.microsoft.com/azure/key-vault/general/disaster-recovery-guidance).
* **Containerregistrierung**: Wählen Sie die Registrierungsoption „Premium“ für Georeplikation aus. Weitere Informationen finden Sie unter [Georeplikation in Azure Container Registry](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication).
* **Application Insights**: Application Insights bietet keine Einstellungen für Hochverfügbarkeit. Wenn Sie den Aufbewahrungszeitraum der Daten und Details anpassen möchten, lesen Sie [Datenerfassung, -aufbewahrung und -speicherung in Application Insights](https://docs.microsoft.com/azure/azure-monitor/app/data-retention-privacy#how-long-is-the-data-kept).

## <a name="compute-resources"></a>Computeressourcen

Stellen Sie sicher, dass Sie die Einstellungen für Hochverfügbarkeit der einzelnen Ressourcen konfigurieren, indem Sie die folgende Dokumentation zu Rate ziehen:

* **Azure Kubernetes Service:** Siehe [Best Practices für Geschäftskontinuität und Notfallwiederherstellung in Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/operator-best-practices-multi-region) und [Erstellen eines Azure Kubernetes Service-Clusters (AKS), der Verfügbarkeitszonen verwendet](https://docs.microsoft.com/azure/aks/availability-zones). Wenn der AKS-Cluster mit Azure Machine Learning Studio, dem SDK oder der CLI erstellt wurde, wird regionsübergreifende Hochverfügbarkeit nicht unterstützt.
* **Azure Databricks**: Siehe [Regionale Notfallwiederherstellung für Azure Databricks-Cluster](https://docs.microsoft.com/azure/azure-databricks/howto-regional-disaster-recovery).
* **Container Instances**: Ein ACI-Orchestrator ist für Failover verantwortlich. Siehe [Azure Container Instances und Containerorchestratoren](https://docs.microsoft.com/azure/container-instances/container-instances-orchestrator-relationship).
* **HDInsight**: Siehe [Von Azure HDInsight unterstützte Hochverfügbarkeitsdienste](https://docs.microsoft.com/azure/hdinsight/hdinsight-high-availability-components).

## <a name="additional-data-stores"></a>Zusätzliche Datenspeicher

Stellen Sie sicher, dass Sie die Einstellungen für Hochverfügbarkeit der einzelnen Ressourcen konfigurieren, indem Sie die folgende Dokumentation zu Rate ziehen:

* **Azure-Blobcontainer/Azure Files/Data Lake Storage Gen2**: Gleiche Vorgehensweise wie bei Standardspeicher.
* **Data Lake Storage Gen1:** Weitere Informationen finden Sie im [Leitfaden zu Hochverfügbarkeit und Notfallwiederherstellung für Data Lake Storage Gen1](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-disaster-recovery-guidance).
* **SQL-Datenbank:** Weitere Informationen finden Sie unter[Hochverfügbarkeit für Azure SQL-Datenbank und SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-high-availability).
* **Azure Database for PostgreSQL**: Siehe [Hochverfügbarkeitskonzepte von Azure Database for PostgreSQL – Einzelserver](https://docs.microsoft.com/azure/postgresql/concepts-high-availability).
* **Azure Database for MySQL**: Siehe [Informationen zur Geschäftskontinuität in Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/concepts-business-continuity).
* **Azure Databricks File System**: Siehe [Regionale Notfallwiederherstellung für Azure Databricks-Cluster](https://docs.microsoft.com/azure/azure-databricks/howto-regional-disaster-recovery).

## <a name="azure-cosmos-db"></a>Azure Cosmos DB

Wenn Sie Ihren eigenen kundenseitig verwalteten Schlüssel zum Bereitstellen des Azure Machine Learning-Arbeitsbereichs angeben, wird Azure Cosmos DB ebenfalls in Ihrem Abonnement bereitgestellt. In diesem Fall sind Sie für das Konfigurieren der Hochverfügbarkeitseinstellungen verantwortlich. Siehe [Hochverfügbarkeit mit Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/high-availability).

## <a name="next-steps"></a>Nächste Schritte

Verwenden Sie eine [Azure Resource Manager-Vorlage](https://github.com/Azure/azure-quickstart-templates/tree/master/201-machine-learning-advanced), um Azure Machine Learning mit zugeordneten Ressourcen mit Ihren Hochverfügbarkeitseinstellungen bereitzustellen.
