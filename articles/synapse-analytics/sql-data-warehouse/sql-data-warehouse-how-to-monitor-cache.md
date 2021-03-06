---
title: Optimieren des Gen2-Cache
description: Erfahren Sie, wie Sie den Gen2-Cache im Azure-Portal überwachen.
services: synapse-analytics
author: kevinvngo
manager: craigg
ms.service: synapse-analytics
ms.subservice: sql-dw
ms.topic: conceptual
ms.date: 09/06/2018
ms.author: kevin
ms.reviewer: igorstan
ms.custom: azure-synapse
ms.openlocfilehash: 4d66a1174b1b4adc94b24c6aecd55b2b8679f2f7
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85211883"
---
# <a name="how-to-monitor-the-gen2-cache"></a>Überwachen des Gen2-Cache

In diesem Artikel wird beschrieben, wie eine langsame Abfrageleistung überwacht und behoben wird, indem bestimmt wird, ob die Workload den Gen2-Cache optimal nutzt.

In der Gen2-Speicherarchitektur werden die am häufigsten abgefragten Columnstore-Segmente automatisch in einem Cache eingeordnet, der sich auf NVMe-basierten SSDs befindet, die für Gen2-Data Warehouses entwickelt wurden. Es wird eine bessere Leistung erreicht, wenn bei Ihren Abfragen Segmente abgerufen werden, die sich im Cache befinden.
 
## <a name="troubleshoot-using-the-azure-portal"></a>Behandeln von Problemen über das Azure-Portal

Mithilfe von Azure Monitor können Sie Metriken des Gen2-Cache anzeigen, um Probleme mit der Abfrageleistung zu beheben. Wechseln Sie zunächst zum Azure-Portal, und klicken Sie auf **Monitor**, **Metriken** und **+ Bereich auswählen**:

![Azure Monitor](./media/sql-data-warehouse-how-to-monitor-cache/cache-0.png)

Verwenden Sie die Such- und Dropdownleisten zum Suchen nach Ihrem Data Warehouse. Wählen Sie dann „Übernehmen“ aus.

![Azure Monitor](./media/sql-data-warehouse-how-to-monitor-cache/cache-1.png)

Die wesentlichen Metriken für die Problembehandlung des Gen2-Cache sind **Prozentsatz der Cachetreffer** und **Cacheverwendung in Prozent**. Wählen Sie **Prozentsatz der Cachetreffer** aus, und klicken Sie auf die Schaltfläche **Metrik hinzufügen**, um **Cacheverwendung in Prozent** hinzuzufügen. 

![Cachemetriken](./media/sql-data-warehouse-how-to-monitor-cache/cache-2.png)

## <a name="cache-hit-and-used-percentage"></a>Prozentsatz der Cachetreffer und Cacheverwendung in Prozent

In der folgenden Matrix sind Szenarien basierend auf den Werten der Cachemetriken beschrieben:

|                                | **Hoher Prozentsatz der Cachetreffer** | **Niedriger Prozentsatz der Cachetreffer** |
| :----------------------------: | :---------------------------: | :--------------------------: |
| **Hohe Cacheverwendung in Prozent** |          Szenario 1           |          Szenario 2          |
| **Geringe Cacheverwendung in Prozent**  |          Szenario 3           |          Szenario 4          |

**Szenario 1:** Sie verwenden den Cache auf optimale Weise. [Behandeln Sie Probleme](sql-data-warehouse-manage-monitor.md) in anderen Bereichen, die möglicherweise zu einer Verlangsamung Ihrer Abfragen führen.

**Szenario 2:** Das aktuelle Arbeitsdataset passt nicht in den Cache, sodass aufgrund der physischen Lesevorgänge ein niedriger Prozentsatz an Cachetreffern anfällt. Sie können die Leistungsebene zentral hochskalieren und die Workload erneut ausführen, um den Cache zu füllen.

**Szenario 3:** Die Abfragen werden wahrscheinlich unabhängig von Problemen mit dem Cache langsam ausgeführt. [Behandeln Sie Probleme](sql-data-warehouse-manage-monitor.md) in anderen Bereichen, die möglicherweise zu einer Verlangsamung Ihrer Abfragen führen. Sie können zudem [Ihre Instanz zentral herunterskalieren](sql-data-warehouse-manage-monitor.md), um die Cachegröße zu reduzieren und so Kosten zu sparen. 

**Szenario 4:** Die Abfragen wurden möglicherweise aufgrund eines „kalten“ Cache langsam ausgeführt. Sie können Ihre Abfragen erneut ausführen, da das Arbeitsdataset sich nun im Cache befinden sollte. 

> [!IMPORTANT]
> Wenn der Prozentsatz der Cachetreffer oder die Cacheverwendung in Prozent nach der erneuten Ausführung der Workload nicht aktualisiert wird, befindet sich Ihr Arbeitssatz möglicherweise bereits im Arbeitsspeicher. Nur gruppierte Columnstore-Tabellen werden zwischengespeichert.

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zur allgemeinen Optimierung der Abfrageleistung finden Sie unter [Überwachen der Abfrageausführung](sql-data-warehouse-manage-monitor.md#monitor-query-execution).
