---
title: Versionshinweise zu Azure Stack Edge und Azure Data Box Gateway in Release 2007 | Microsoft-Dokumentation
description: In diesem Artikel werden offene Probleme und Lösungen für Azure Stack Edge und Data Box Gateway in Release 2007 beschrieben.
services: databox
author: twooley
ms.service: databox
ms.subservice: gateway
ms.topic: article
ms.date: 07/14/2020
ms.author: twooley
ms.openlocfilehash: f9a08cda1466dbe284a0ac3c0e34b109be236883
ms.sourcegitcommit: 9c3cfbe2bee467d0e6966c2bfdeddbe039cad029
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/24/2020
ms.locfileid: "88783925"
---
# <a name="azure-stack-edge-and-azure-data-box-gateway-2007-release-notes"></a>Versionshinweise zu Azure Stack Edge und Azure Data Box Gateway in Release 2007

In den folgenden Versionshinweisen werden die schwerwiegenden offenen und die gelösten Probleme für das Release 2007 von Azure Stack Edge und Data Box Gateway beschrieben.

Die Versionshinweise werden fortlaufend aktualisiert, und wenn schwerwiegende Probleme festgestellt werden, die eine Problemumgehung erfordern, werden sie hinzugefügt. Lesen Sie vor der Bereitstellung von Azure Stack Edge bzw. Data Box Gateway die Informationen in den Anmerkungen zu dieser Version sorgfältig durch.

Dieses Release entspricht den folgenden Softwareversionen:

- **Azure Stack Edge 2007 (1.6.1280.1667)**  – KB 4566549
- **Data Box Gateway 2007 (1.6.1280.1667)**  – KB 4566550

> [!NOTE]
> Update 2007 kann nur auf die Geräte angewendet werden, auf denen die allgemein verfügbaren Versionen (oder höhere Versionen) der Software ausgeführt werden.

## <a name="whats-new"></a>Neues

Dieses Release enthält die folgenden Fehlerbehebungen:

- **Uploadproblem:** Dieses Release behebt ein Uploadproblem, bei dem der Upload aufgrund von Fehlern neu gestartet wird, was den Abschluss von Uploads insgesamt verzögern kann. Dieses Problem kann auftreten, wenn ein Dataset hochgeladen wird, das hauptsächlich aus Dateien besteht, die im Verhältnis zur verfügbaren Bandbreite sehr groß sind, insbesondere, aber nicht ausschließlich dann, wenn die Bandbreiteneinschränkung aktiviert ist. Diese Änderung sorgt dafür, dass dem Abschluss von Uploads genügend Zeit eingeräumt wird, bevor der Upload für eine bestimmte Datei neu gestartet wird.

Dieses Release enthält auch die folgenden Updates:

- Das Basisimage für die virtuelle Windows-Festplatte wurde aktualisiert.
- Alle kumulativen Windows-Updates und .NET Framework-Updates sind dabei eingeschlossen, die bis Mai 2020 veröffentlicht wurden.
- Dieses Release unterstützt IoT Edge 1.0.9.3 auf Azure Stack Edge-Geräten.

## <a name="known-issues-in-this-release"></a>Bekannte Probleme in dieser Version

Für dieses Release werden keine neuen Probleme aufgeführt. Alle in den Versionshinweisen enthaltenen Probleme wurden aus früheren Releases übernommen. Um eine Liste der bekannten Probleme anzuzeigen, wechseln Sie zu [Bekannte Probleme in der Version für die allgemeine Verfügbarkeit](data-box-gateway-release-notes.md#known-issues-in-ga-release).

## <a name="next-steps"></a>Nächste Schritte

- [Vorbereiten der Bereitstellung von Azure Stack Edge](data-box-edge-deploy-prep.md)
- [Vorbereiten der Bereitstellung von Azure Data Box Gateway](data-box-gateway-deploy-prep.md)
