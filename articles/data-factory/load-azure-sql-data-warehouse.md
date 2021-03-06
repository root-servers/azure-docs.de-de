---
title: Laden von Daten in Azure Synapse Analytics
description: Verwenden von Azure Data Factory zum Kopieren von Daten in Azure Synapse Analytics
services: data-factory
ms.author: jingwang
author: linda33wj
manager: shwang
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.topic: conceptual
ms.custom: seo-lt-2019
ms.date: 06/08/2020
ms.openlocfilehash: 8891c65707822abeb2bcca52280d9b56dc725e4f
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85251997"
---
# <a name="load-data-into-azure-synapse-analytics-by-using-azure-data-factory"></a>Laden von Daten in Azure Synapse Analytics mithilfe von Azure Data Factory

[!INCLUDE[appliesto-adf-asa-md](includes/appliesto-adf-asa-md.md)]

[Azure Synapse Analytics](../synapse-analytics/sql-data-warehouse/sql-data-warehouse-overview-what-is.md) (früher SQL Data Warehouse) ist eine cloudbasierte Datenbank für die horizontale Skalierung, mit der sehr große Datenvolumen verarbeitet werden können, und zwar sowohl relational als auch nicht relational. Azure Synapse Analytics basiert auf der MPP-Architektur (Massively Parallel Processing), die für Data-Warehouse-Workloads auf Unternehmensniveau optimiert ist. Es bietet Cloudelastizität mit der Flexibilität, Speicher zu skalieren und unabhängig zu berechnen.

Die ersten Schritte mit Azure Synapse Analytics sind jetzt mithilfe von Azure Data Factory einfacher als je zuvor. Azure Data Factory ist ein vollständig verwalteter, cloudbasierter Datenintegrationsdienst. Mithilfe dieses Diensts können Sie eine Azure Synapse Analytics-Instanz mit Daten aus dem vorhandenen System auffüllen und so Zeit beim Erstellen von Analyselösungen sparen.

Azure Data Factory bietet die folgenden Vorteile beim Laden von Daten in Azure Synapse Analytics:

* **Mühelose Einrichtung**: Intuitiver Assistent mit 5 Schritten. Keine Skripterstellung erforderlich.
* **Unterstützung für umfangreiche Datenspeicher**: Integrierte Unterstützung für umfangreiche lokale und cloudbasierte Datenspeicher. Eine ausführliche Liste finden Sie in der Tabelle [Unterstützte Datenspeicher](copy-activity-overview.md#supported-data-stores-and-formats).
* **Sicher und kompatibel**: Daten werden über HTTPS oder ExpressRoute übertragen. Globale Dienste stellen sicher, dass Ihre Daten nie die geografische Grenze verlassen.
* **Beispiellose Leistung mithilfe von PolyBase**: PolyBase ist die effizienteste Methode zum Verschieben von Daten in Azure Synapse Analytics. Mit der Funktion „Stagingblob“ werden schnelle Ladezeiten für alle Arten von Datenspeicher erreicht. Dies gilt auch für Azure Blob Storage und Data Lake Store. (Azure Blob Storage und Azure Data Lake Store werden standardmäßig von Polybase unterstützt.) Weitere Informationen finden Sie unter [Leistung der Kopieraktivität](copy-activity-performance.md).

In diesem Artikel erfahren Sie, wie Sie das Tool zum Kopieren von Daten in Data Factory zum _Laden von Daten aus Azure SQL-Datenbank in Azure Synapse Analytics_ verwenden. Sie können ähnliche Schritte zum Kopieren von Daten aus anderen Typen von Datenspeichern ausführen.

> [!NOTE]
> Weitere Informationen finden Sie unter [Kopieren von Daten nach und aus Azure Synapse Analytics mithilfe von Azure Data Factory](connector-azure-sql-data-warehouse.md).

## <a name="prerequisites"></a>Voraussetzungen

* Azure-Abonnement: Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/) erstellen, bevor Sie beginnen.
* Azure Synapse Analytics: Dieses Data Warehouse enthält die Daten, die aus der SQL-Datenbank kopiert werden. Wenn Sie keine Azure Synapse Analytics-Instanz besitzen, finden Sie unter [Erstellen einer Azure Synapse Analytics-Instanz](../sql-data-warehouse/sql-data-warehouse-get-started-tutorial.md) die entsprechenden Anweisungen.
* Azure SQL-Datenbank: In diesem Tutorial werden Daten aus einem Beispieldataset von Adventure Works LT nach Azure SQL-Datenbank kopiert. Sie können diese Beispieldatenbank in SQL-Datenbank erstellen, indem Sie den Anweisungen unter [Schnellstart: Erstellen einer Azure SQL-Einzeldatenbank](../azure-sql/database/single-database-create-quickstart.md) folgen.
* Azure-Speicherkonto: Azure Storage wird im Massenkopiervorgang als _Staging_blob verwendet. Falls Sie noch nicht über ein Azure-Speicherkonto verfügen, finden Sie Anweisungen dazu unter [Erstellen eines Speicherkontos](../storage/common/storage-account-create.md).

## <a name="create-a-data-factory"></a>Erstellen einer Data Factory

1. Wählen Sie im Menü auf der linken Seite **Ressource erstellen** > **Daten + Analysen** > **Data Factory** aus:

2. Geben Sie auf der Seite **Neue Data Factory** Werte für folgende Elemente an:

    * **Name**: Geben Sie als Namen *LoadSQLDWDemo* ein. Der Name der Data Factory muss global eindeutig sein. Wenn die Fehlermeldung „Data Factory mit dem Namen ‚LoadSQLDWDemo‘ ist nicht verfügbar“ angezeigt wird, geben Sie einen anderen Namen für die Data Factory ein. Sie können beispielsweise den Namen _**IhrName**_**ADFTutorialDataFactory** verwenden. Versuchen Sie erneut, die Data Factory zu erstellen. Benennungsregeln für Data Factory-Artefakte finden Sie im Thema [Data Factory – Benennungsregeln](naming-rules.md).
    * **Abonnement**: Wählen Sie Ihr Azure-Abonnement aus, in dem die Data Factory erstellt werden soll. 
    * **Ressourcengruppe**: Wählen Sie eine vorhandene Ressourcengruppe aus der Dropdownliste aus, oder wählen Sie die Option **Neu erstellen** aus, und geben Sie dann den Namen einer Ressourcengruppe ein. Weitere Informationen über Ressourcengruppen finden Sie unter [Verwenden von Ressourcengruppen zum Verwalten von Azure-Ressourcen](../azure-resource-manager/management/overview.md).  
    * **Version**: Wählen Sie **V2** aus.
    * **Standort**: Wählen Sie den Standort für die Data Factory aus. In der Dropdownliste werden nur unterstützte Standorte angezeigt. Die von der Data Factory verwendeten Datenspeicher können sich an anderen Standorten bzw. in anderen Regionen befinden. Diese Datenspeicher umfassen Azure Data Lake Store, Azure Storage, Azure SQL-Datenbank usw.

3. Klicken Sie auf **Erstellen**.
4. Nach Abschluss der Erstellung navigieren Sie zu Ihrer Data Factory. Die Startseite **Data Factory** wird wie in der folgenden Abbildung dargestellt angezeigt:

   ![Data Factory-Startseite](./media/doc-common-process/data-factory-home-page.png)

   Wählen Sie die Kachel **Erstellen und überwachen** aus, um die Datenintegrationsanwendung auf einer separaten Registerkarte zu starten.

## <a name="load-data-into-azure-synapse-analytics"></a>Laden von Daten in Azure Synapse Analytics

1. Wählen Sie auf der Seite **Erste Schritte** die Kachel **Daten kopieren** aus, um das Tool Daten kopieren zu starten.

1. Geben Sie auf der Seite **Eigenschaften** im Feld **Aufgabenname** den Namen **CopyFromSQLToSQLDW** ein, und wählen Sie dann **Weiter** aus.

    ![Eigenschaftenseite](./media/load-azure-sql-data-warehouse/copy-data-tool-properties-page.png)

1. Führen Sie auf der Seite **Quelldatenspeicher** die folgenden Schritte aus:
    >[!TIP]
    >In diesem Tutorial verwenden Sie die *SQL-Authentifizierung* als Authentifizierungstyp für Ihren Quelldatenspeicher, Sie können bei Bedarf aber auch andere unterstützte Authentifizierungsmethoden auswählen: *Dienstprinzipal* oder *Verwaltete Identität*. Ausführlichere Informationen finden Sie in den entsprechenden Abschnitten [dieses Artikels](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#linked-service-properties).
    >Zum sicheren Speichern von Geheimnissen für Datenspeicher empfiehlt sich darüber hinaus die Verwendung einer Azure Key Vault-Instanz. Eine ausführliche Erläuterung finden Sie in [diesem Artikel](https://docs.microsoft.com/azure/data-factory/store-credentials-in-key-vault).

    a. Klicken Sie auf **+ Neue Verbindung erstellen**.

    b. Wählen Sie im Katalog **Azure SQL-Datenbank** und dann **Weiter** aus. Sie können in das Suchfeld zum Filtern der Connectors „SQL“ eingeben.

    ![Auswählen der Azure SQL-Datenbank](./media/load-azure-sql-data-warehouse/select-azure-sql-db-source.png)

    c. Wählen Sie auf der Seite **New Linked Service** (Neuer verknüpfter Dienst) in der Dropdownliste Ihren Server- und Datenbanknamen aus, und geben Sie den Benutzernamen und das Kennwort an. Klicken Sie auf **Verbindung testen**, um die Einstellungen zu überprüfen, und wählen Sie dann **Erstellen** aus.

    ![Konfigurieren von Azure SQL-Datenbank](./media/load-azure-sql-data-warehouse/configure-azure-sql-db.png)

    d. Wählen Sie den neu erstellten verknüpften Dienst als Quelle aus, und klicken Sie auf **Weiter**.

1. Geben Sie auf der Seite **Tabellen auswählen, aus denen die Daten kopiert werden sollen, oder eine benutzerdefinierte Abfrage verwenden** die Zeichenfolge **SalesLT** ein, um die Tabellen zu filtern. Aktivieren Sie das Kontrollkästchen **(Alles auswählen)** , um alle Tabellen für den Kopiervorgang zu verwenden, und wählen Sie dann **Weiter** aus.

    ![Auswählen von Quelltabellen](./media/load-azure-sql-data-warehouse/select-source-tables.png)

1. Geben Sie auf der Seite **Filter anwenden** die Einstellungen an, oder wählen Sie **Weiter** aus.

1. Führen Sie auf der Seite **Zieldatenspeicher** die folgenden Schritte aus:
    >[!TIP]
    >In diesem Tutorial verwenden Sie die *SQL-Authentifizierung* als Authentifizierungstyp für Ihren Zieldatenspeicher, Sie können bei Bedarf aber auch andere unterstützte Authentifizierungsmethoden auswählen: *Dienstprinzipal* oder *Verwaltete Identität*. Ausführlichere Informationen finden Sie in den entsprechenden Abschnitten [dieses Artikels](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-data-warehouse#linked-service-properties).
    >Zum sicheren Speichern von Geheimnissen für Datenspeicher empfiehlt sich darüber hinaus die Verwendung einer Azure Key Vault-Instanz. Eine ausführliche Erläuterung finden Sie in [diesem Artikel](https://docs.microsoft.com/azure/data-factory/store-credentials-in-key-vault).

    a. Klicken Sie auf **+ Neue Verbindung erstellen**, um eine Verbindung hinzuzufügen.

    b. Wählen Sie im Katalog **Azure Synapse Analytics (früher SQL DW)** und dann **Weiter** aus. Sie können in das Suchfeld zum Filtern der Connectors „SQL“ eingeben.

    ![Auswählen von Azure SQL DW](./media/load-azure-sql-data-warehouse/select-azure-sql-dw-sink.png)

    c. Wählen Sie auf der Seite **New Linked Service** (Neuer verknüpfter Dienst) in der Dropdownliste Ihren Server- und Datenbanknamen aus, und geben Sie den Benutzernamen und das Kennwort an. Klicken Sie auf **Verbindung testen**, um die Einstellungen zu überprüfen, und wählen Sie dann **Erstellen** aus.

    ![Konfigurieren von Azure SQL DW](./media/load-azure-sql-data-warehouse/configure-azure-sql-dw.png)

    d. Wählen Sie den neu erstellten verknüpften Dienst als Senke aus, und klicken Sie auf **Weiter**.

1. Überprüfen Sie den Inhalt der Seite **Tabellenmapping**, und klicken Sie dann auf **Weiter**. Eine intelligente Tabellenzuordnung wird angezeigt. Die Quelltabellen werden den Zieltabellen auf Grundlage der Tabellennamen zugeordnet. Wenn eine Quelltabelle im Ziel nicht vorhanden ist, wird von Azure Data Factory standardmäßig eine Zieltabelle mit dem gleichen Namen erstellt. Sie können eine Quelltabelle auch einer vorhandenen Zieltabelle zuordnen.

   > [!NOTE]
   > Das automatische Erstellen der Tabelle für die Azure Synapse Analytics-Senke tritt auf, wenn SQL Server oder Azure SQL-Datenbank als Quelle verwendet werden. Wenn Sie Daten aus einem anderen Quelldatenspeicher kopieren, müssen Sie das Schema vorab in der Azure Synapse Analytics-Senke erstellen, bevor Sie den Datenkopiervorgang ausführen.

   ![Seite „Tabellenmapping“](./media/load-azure-sql-data-warehouse/table-mapping.png)

1. Überprüfen Sie den Inhalt der Seite **Spaltenzuordnung**, und wählen Sie dann **Weiter** aus. Die intelligente Tabellenzuordnung basiert auf dem Spaltennamen. Wenn Sie Data Factory die Tabellen automatisch erstellen lassen, kann eine Datentypkonvertierung erfolgen, wenn zwischen den Quell- und Zielspeichern Inkompatibilitäten vorliegen. Wenn es eine nicht unterstützte Datentypkonvertierung zwischen der Quell- und Zielspalte gibt, wird eine Fehlermeldung neben der entsprechenden Tabelle angezeigt.

    ![Seite „Spaltenzuordnung“](./media/load-azure-sql-data-warehouse/schema-mapping.png)

1. Führen Sie auf der Seite **Einstellungen** die folgenden Schritte aus:

    a. Klicken Sie im Abschnitt **Stagingeinstellungen** auf **+ Neu**, um einen neuen Stagingspeicher zu erstellen. Der Speicher wird für das Staging der Daten verwendet, bevor diese mit PolyBase in Azure Synapse Analytics geladen werden. Nach Abschluss des Kopiervorgangs werden die vorläufigen Daten in Azure Blob Storage automatisch bereinigt.

    b. Wählen Sie auf der Seite **Neuer verknüpfter Dienst** Ihr Speicherkonto und dann **Erstellen** aus, um den verknüpften Dienst bereitzustellen.

    c. Deaktivieren Sie im Abschnitt **Erweiterte Einstellungen** die Option **Use type default** (Typstandard verwenden), und wählen Sie dann **Weiter** aus.

    ![Konfigurieren von PolyBase](./media/load-azure-sql-data-warehouse/configure-polybase.png)

1. Überprüfen Sie auf der Seite **Zusammenfassung** die Einstellungen, und klicken Sie dann auf **Weiter**.

    ![Seite „Zusammenfassung“](./media/load-azure-sql-data-warehouse/summary-page.png)

1. Klicken Sie auf der Seite **Bereitstellung** auf **Überwachen**, um die Pipeline (Task) zu überwachen. 
 
1. Beachten Sie, dass die Registerkarte **Überwachen** auf der linken Seite automatisch ausgewählt ist. Wenn die Pipelineausführung erfolgreich abgeschlossen wurde, wählen Sie den Link **CopyFromSQLToSQLDW** unter der Spalte **PIPELINENAME** aus, um Details zur Aktivitätsausführung anzuzeigen oder die Pipeline erneut auszuführen.

    [![Überwachen der Pipelineausführungen](./media/load-azure-sql-data-warehouse/pipeline-monitoring.png)](./media/load-azure-sql-data-warehouse/pipeline-monitoring.png#lightbox)

1. Wählen Sie oben den Link **Alle Pipelineausführungen** aus, um zurück zur Ansicht mit den Pipelineausführungen zu wechseln. Klicken Sie zum Aktualisieren der Liste auf **Aktualisieren**.

    ![Überwachung der Aktivitätsausführungen](./media/load-azure-sql-data-warehouse/activity-monitoring.png)

1. Zum Überwachen der Ausführungsdetails jeder Kopieraktivität wählen Sie in der Ansicht der Aktivitätsausführungen unter **AKTIVITÄTSNAME** den Link **Details** (Brillensymbol) aus. Sie können Details wie die Menge der Daten, die aus der Quelle in die Senke kopiert wurden, den Datendurchsatz, die Ausführungsschritte mit entsprechender Dauer sowie die verwendeten Konfigurationen überwachen.
    ![Überwachen von Details zur Aktivitätsausführung](./media/load-azure-sql-data-warehouse/monitor-activity-run-details-1.png)

    ![Überwachen der Details zur Aktivitätsausführung](./media/load-azure-sql-data-warehouse/monitor-activity-run-details-2.png)

## <a name="next-steps"></a>Nächste Schritte

Lesen Sie den folgenden Artikel, um mehr über die Unterstützung von Azure Synapse Analytics zu erfahren:

> [!div class="nextstepaction"]
>[Azure Synapse Analytics-Connector](connector-azure-sql-data-warehouse.md)
