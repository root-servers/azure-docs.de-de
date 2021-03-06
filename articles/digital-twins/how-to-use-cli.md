---
title: Verwenden der Azure Digital Twins-Befehlszeilenschnittstelle
titleSuffix: Azure Digital Twins
description: Informieren Sie sich über die ersten Schritte mit der Azure Digital Twins-Befehlszeilenschnittstelle und deren Verwendung.
author: baanders
ms.author: baanders
ms.date: 05/25/2020
ms.topic: how-to
ms.service: digital-twins
ms.openlocfilehash: 2c642b2441d1f30c31e707a237732e028f548ac5
ms.sourcegitcommit: 58d3b3314df4ba3cabd4d4a6016b22fa5264f05a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/02/2020
ms.locfileid: "89298180"
---
# <a name="use-the-azure-digital-twins-cli"></a>Verwenden der Azure Digital Twins-Befehlszeilenschnittstelle

Zusätzlich zur Verwaltung Ihrer Azure Digital Twins-Instanz im Azure-Portal verfügt Azure Digital Twins über eine **Befehlszeilenschnittstelle (Command-Line Interface, CLI)** , über die Sie die meisten wichtigen Aktionen mit dem Dienst ausführen können, einschließlich:
* Verwalten einer Azure Digital Twins-Instanz
* Verwalten von Modellen
* Verwalten von digitalen Zwillingen
* Verwalten von Zwillingsbeziehungen
* Konfigurieren von Endpunkten
* Verwalten von [Routen](concepts-route-events.md)
* Konfigurieren der [Sicherheit](concepts-security.md) über die rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC)

[!INCLUDE [digital-twins-known-issue-cloud-shell](../../includes/digital-twins-known-issue-cloud-shell.md)]

## <a name="uses-deploy-and-validate"></a>Verwendungen (bereitstellen und validieren)

Zusätzlich zur allgemeinen Verwaltung Ihrer Instanz ist die CLI auch ein nützliches Tool für die Bereitstellung und Validierung.
* Mithilfe der Befehle auf Steuerungsebene kann die Bereitstellung einer neuen Instanz wiederholbar oder automatisiert werden.
* Mit den Befehlen auf Datenebene können Sie schnell Werte in Ihrer Instanz und den erwartungsgemäßen Abschluss von Vorgängen überprüfen.

## <a name="get-the-extension"></a>Erhalten der Erweiterung

Die Azure Digital Twins-Befehle sind Teil der [Azure IoT-Erweiterung für Azure CLI](https://github.com/Azure/azure-iot-cli-extension). Sie können die Referenzdokumentation für diese Befehle als Teil des `az iot`-Befehlssatzes anzeigen: [az dt](https://docs.microsoft.com/cli/azure/ext/azure-iot/dt?view=azure-cli-latest).

Mit diesen Schritten können Sie sicherstellen, dass Sie über die neueste Version der Erweiterung verfügen. Sie können diese Befehle in [Azure Cloud Shell](../cloud-shell/overview.md) oder einer [lokalen Azure-Befehlszeilenschnittstelle](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) ausführen.

[!INCLUDE [digital-twins-cloud-shell-extensions.md](../../includes/digital-twins-cloud-shell-extensions.md)]

## <a name="next-steps"></a>Nächste Schritte

Um eine Alternative zu CLI-Befehlen kennenzulernen, informieren Sie sich über die Verwaltung einer Azure Digital Twins-Instanz mit APIs und SDKs:
* [*Verwenden der Azure Digital Twins-APIs und SDKs*](how-to-use-apis-sdks.md)
