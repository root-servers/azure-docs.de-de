---
title: Azure Security Control – Datenschutz
description: Azure Security Control – Datenschutz
author: msmbaldwin
ms.service: security
ms.topic: conceptual
ms.date: 04/14/2020
ms.author: mbaldwin
ms.custom: security-benchmark
ms.openlocfilehash: d89320807c6322120490db85100453edf593aded
ms.sourcegitcommit: e132633b9c3a53b3ead101ea2711570e60d67b83
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/07/2020
ms.locfileid: "86045534"
---
# <a name="security-control-data-protection"></a>Sicherheitskontrolle: Datenschutz

Die Empfehlungen zum Datenschutz konzentrieren sich auf die Behandlung von Problemen im Zusammenhang mit Verschlüsselung, Zugriffssteuerungslisten, identitätsbasierter Zugriffskontrolle und Überwachungsprotokollen für den Datenzugriff.

## <a name="41-maintain-an-inventory-of-sensitive-information"></a>4.1: Verwalten eines Bestands an vertraulichen Informationen

| Azure-ID | CIS-IDs | Verantwortlichkeit |
|--|--|--|
| 4,1 | Version 13.1 | Kunde |

Verwenden Sie Tags für die Nachverfolgung von Azure-Ressourcen, die vertrauliche Informationen speichern oder verarbeiten.

- [Erstellen und Verwenden von Tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)

## <a name="42-isolate-systems-storing-or-processing-sensitive-information"></a>4.2: Isolieren von Systemen, die vertrauliche Informationen speichern oder verarbeiten

| Azure-ID | CIS-IDs | Verantwortlichkeit |
|--|--|--|
| 4,2 | 13.2, 2.10 | Kunde |

Implementieren Sie eine Isolation mit separaten Abonnements und Verwaltungsgruppen für einzelne Sicherheitsdomänen, z. B. Umgebungstyp und Datenvertraulichkeitsstufe. Sie können die Zugriffsebene auf diejenigen Ihrer Azure-Ressourcen beschränken, die von Ihren Anwendungen und Unternehmensumgebungen gefordert werden. Sie können den Zugriff auf Azure-Ressourcen über die rollenbasierte Azure-Zugriffssteuerung (Azure RBAC) steuern. 

- [Erstellen zusätzlicher Azure-Abonnements](https://docs.microsoft.com/azure/billing/billing-create-subscription)

- [Erstellen von Verwaltungsgruppen](https://docs.microsoft.com/azure/governance/management-groups/create)

- [Erstellen und Verwenden von Tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)

## <a name="43-monitor-and-block-unauthorized-transfer-of-sensitive-information"></a>4.3: Überwachen und Blockieren einer nicht autorisierten Übertragung vertraulicher Informationen

| Azure-ID | CIS-IDs | Verantwortlichkeit |
|--|--|--|
| 4.3 | 13.3 | Shared |

Nutzen Sie eine Drittanbieterlösung von Azure Marketplace an Netzwerkperimetern, die die nicht autorisierte Übertragung von vertraulichen Informationen überwacht, derartige Übertragungen blockiert und gleichzeitig die Informationssicherheitsexperten benachrichtigt.

Bei der zugrundeliegenden Plattform, die von Microsoft verwaltet wird, behandelt Microsoft alle Kundeninhalte als vertraulich und schützt Kundendaten vor Verlust und Gefährdung. Um die Sicherheit von Kundendaten innerhalb von Azure zu gewährleisten, hat Microsoft eine Reihe von robusten Datenschutzkontrollen und -funktionen implementiert und kümmert sich um deren Verwaltung.

- [Grundlegendes zum Schutz von Kundendaten in Azure](https://docs.microsoft.com/azure/security/fundamentals/protection-customer-data)

## <a name="44-encrypt-all-sensitive-information-in-transit"></a>4.4: Verschlüsseln aller vertraulichen Informationen während der Übertragung

| Azure-ID | CIS-IDs | Verantwortlichkeit |
|--|--|--|
| 4.4 | 14.4 | Shared |

Verschlüsseln Sie alle vertraulichen Informationen während der Übertragung. Stellen Sie sicher, dass alle Clients, die sich mit Ihren Azure-Ressourcen verbinden, TLS 1.2 oder höher aushandeln können.

Befolgen Sie ggf. die Empfehlungen von Azure Security Center zur Verschlüsselung ruhender Daten und zur Verschlüsselung während der Übertragung.

- [Grundlegendes zur Verschlüsselung während der Übertragung mit Azure](https://docs.microsoft.com/azure/security/fundamentals/encryption-overview#encryption-of-data-in-transit)

## <a name="45-use-an-active-discovery-tool-to-identify-sensitive-data"></a>4.5: Verwenden eines aktiven Ermittlungstools zur Bestimmung vertraulicher Daten

| Azure-ID | CIS-IDs | Verantwortlichkeit |
|--|--|--|
| 4,5 | 14.5 | Shared |

Wenn für Ihren spezifischen Dienst in Azure keine Funktion verfügbar ist, verwenden Sie ein aktives Ermittlungstools eines Drittanbieters, um alle vertraulichen Informationen zu bestimmen, die von den Technologiesystemen des Unternehmens gespeichert, verarbeitet oder übertragen werden, einschließlich der Systeme, die sich vor Ort oder bei einem Remotedienstanbieter befinden, und um den Bestand an vertraulichen Informationen des Unternehmens zu aktualisieren.

Verwenden Sie Azure Information Protection, um vertrauliche Informationen in Office 365-Dokumenten zu bestimmen.

Verwenden Sie Azure SQL Information Protection, um die Klassifizierung und Bezeichnung von Informationen zu unterstützen, die in Azure SQL-Datenbank gespeichert sind.

- [Implementieren von Azure SQL Data Discovery](https://docs.microsoft.com/azure/sql-database/sql-database-data-discovery-and-classification)

- [Implementieren von Azure Information Protection](https://docs.microsoft.com/azure/information-protection/deployment-roadmap)

- [Grundlegendes zum Schutz von Kundendaten in Azure](https://docs.microsoft.com/azure/security/fundamentals/protection-customer-data)

## <a name="46-use-role-based-access-control-to-control-access-to-resources"></a>4.6: Verwenden der rollenbasierten Zugriffssteuerung zum Steuern des Zugriffs auf Ressourcen

| Azure-ID | CIS-IDs | Verantwortlichkeit |
|--|--|--|
| 4.6 | 14.6 | Kunde |

Verwenden Sie Azure AD-RBAC, um den Zugriff auf Daten und Ressourcen zu steuern, und verwenden Sie andernfalls dienstspezifische Zugriffssteuerungsmethoden.

- [Konfigurieren von RBAC in Azure](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal)

## <a name="47-use-host-based-data-loss-prevention-to-enforce-access-control"></a>4.7: Verwenden der hostbasierten Verhinderung von Datenverlusten zum Erzwingen der Zugriffssteuerung

| Azure-ID | CIS-IDs | Verantwortlichkeit |
|--|--|--|
| 4,7 | 14.7 | Shared |

Wenn aus Compliancegründen für Computeressourcen erforderlich, implementieren Sie ein Drittanbietertool, z. B. eine automatisierte Lösung für die hostbasierte Verhinderung von Datenverlust, um Zugriffssteuerungen für Daten auch dann zu erzwingen, wenn Daten von einem System kopiert werden.

Für die zugrundeliegende Plattform, die von Microsoft verwaltet wird, behandelt Microsoft alle Kundeninhalte als vertraulich und unternimmt große Anstrengungen, um Kundendaten vor Verlust und Gefährdung zu schützen. Um die Sicherheit von Kundendaten innerhalb von Azure zu gewährleisten, hat Microsoft eine Reihe von robusten Datenschutzkontrollen und -funktionen implementiert und kümmert sich um deren Verwaltung.

- [Grundlegendes zum Schutz von Kundendaten in Azure](https://docs.microsoft.com/azure/security/fundamentals/protection-customer-data)

## <a name="48-encrypt-sensitive-information-at-rest"></a>4.8: Verschlüsseln vertraulicher, ruhender Informationen

| Azure-ID | CIS-IDs | Verantwortlichkeit |
|--|--|--|
| 4.8 | 14.8 | Kunde |

Verwenden Sie die Verschlüsselung ruhender Daten für alle Azure-Ressourcen. Microsoft empfiehlt, Azure die Verwaltung Ihrer Verschlüsselungsschlüssel zu erlauben. Es gibt jedoch in einigen Fällen die Möglichkeit, ihre eigenen Schlüssel zu verwalten. 

- [Grundlegendes zur Verschlüsselung ruhender Daten in Azure](https://docs.microsoft.com/azure/security/fundamentals/encryption-atrest)

- [Konfigurieren der von Kunden verwalteten Verschlüsselungsschlüssel](https://docs.microsoft.com/azure/storage/common/storage-encryption-keys-portal)

## <a name="49-log-and-alert-on-changes-to-critical-azure-resources"></a>4.9: Protokollieren und Warnen bei Änderungen an wichtigen Azure-Ressourcen

| Azure-ID | CIS-IDs | Verantwortlichkeit |
|--|--|--|
| 4,9 | 14.9 | Kunde |

Verwenden Sie Azure Monitor mit dem Azure-Aktivitätsprotokoll, um Warnungen zu erstellen, die bei Änderungen an wichtigen Azure-Ressourcen ausgegeben werden.

- [Erstellen von Warnungen für Ereignisse des Azure-Aktivitätsprotokolls](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-activity-log)


## <a name="next-steps"></a>Nächste Schritte

- Weitere Informationen finden Sie in der nächsten Sicherheitskontrolle:  [Verwaltung von Sicherheitsrisiken](security-control-vulnerability-management.md)