---
title: Erstellen eines Azure-Dienstprinzipals
services: cognitive-services
author: PatrickFarley
manager: nitinme
ms.service: cognitive-services
ms.topic: include
ms.date: 09/01/2020
ms.author: pafarley
ms.openlocfilehash: 5cff103d17138608f4932e36444847437f6da236
ms.sourcegitcommit: 5ed504a9ddfbd69d4f2d256ec431e634eb38813e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/02/2020
ms.locfileid: "89321651"
---
## <a name="create-an-azure-service-principal"></a>Erstellen eines Azure-Dienstprinzipals

Damit Ihre Anwendung mit Ihrem Azure-Konto interagieren kann, benötigen Sie einen Azure-Dienstprinzipal zum Verwalten der Berechtigungen. Folgen Sie den Anweisungen unter [Erstellen eines Azure-Dienstprinzipals](https://docs.microsoft.com/powershell/azure/create-azure-service-principal-azureps?view=azps-4.4.0&viewFallbackFrom=azps-3.3.0).

Wenn Sie einen Dienstprinzipal erstellen, sehen Sie, dass dieser einen Geheimniswert, eine ID und eine Anwendungs-ID aufweist. Speichern Sie die Anwendungs-ID und das Geheimnis für spätere Schritte an einem temporären Speicherort.