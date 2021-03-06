---
title: 'Schnellstart: Erstellen Ihrer ersten statischen Web-App mit Azure Static Web Apps und dem Azure-Portal'
description: Hier wird beschrieben, wie Sie mit dem Azure-Portal eine Instanz von Azure Static Web Apps erstellen.
services: static-web-apps
author: craigshoemaker
ms.service: static-web-apps
ms.topic: quickstart
ms.date: 08/13/2020
ms.author: cshoe
ms.openlocfilehash: e0b78c5e053c5668fbebd8ebaac91a90aa2b364f
ms.sourcegitcommit: 62717591c3ab871365a783b7221851758f4ec9a4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/22/2020
ms.locfileid: "88752822"
---
# <a name="quickstart-building-your-first-static-web-app-in-the-azure-portal"></a>Schnellstart: Erstellen Ihrer ersten statischen Web-App im Azure-Portal

Azure Static Web Apps veröffentlicht eine Website in einer Produktionsumgebung, indem Apps aus einem GitHub-Repository erstellt werden. In dieser Schnellstartanleitung stellen Sie über das Azure-Portal eine Web-Anwendung in Azure Static Web Apps bereit.

Falls Sie noch nicht über ein Azure-Abonnement verfügen, können Sie ein [kostenloses Testkonto](https://azure.microsoft.com/free) erstellen.

## <a name="prerequisites"></a>Voraussetzungen

- [GitHub](https://github.com) -Konto
- [Azure](https://portal.azure.com)-Konto

[!INCLUDE [create repository from template](../../includes/static-web-apps-get-started-create-repo.md)]

## <a name="create-a-static-web-app"></a>Erstellen einer statischen Web-App

Nachdem das Repository nun erstellt wurde, können Sie im Azure-Portal eine statische Web-App erstellen.

1. Navigieren Sie zum [Azure-Portal](https://portal.azure.com).
1. Wählen Sie **Ressource erstellen** aus.
1. Suchen Sie nach **Static Web Apps**.
1. Wählen Sie **Static Web Apps (Vorschau)** aus.
1. Klicken Sie auf **Erstellen**

Konfigurieren Sie auf der Registerkarte _Grundlagen_ zunächst Ihre neue App, und verknüpfen Sie sie mit einem GitHub-Repository.

:::image type="content" source="media/getting-started-portal/basics-tab.png" alt-text="Registerkarte „Grundlagen“":::

1. Wählen Sie Ihr _Azure-Abonnement_ aus.
1. Wählen Sie eine neue _Ressourcengruppe_ aus, oder erstellen Sie sie.
1. Geben Sie der App den Namen **my-first-static-web-app**.
      1. Gültige Zeichen sind `a-z` (Groß-/Kleinschreibung nicht beachtet), `0-9` und `-`.
1. Wählen Sie eine _Region_ aus, die in Ihrer Nähe liegt.
1. Wählen Sie für _SKU_ die Option **Free** aus.
1. Wählen Sie die Schaltfläche **Mit GitHub anmelden** aus, und führen Sie die Authentifizierung mit GitHub durch.

Geben Sie nach der Anmeldung mit GitHub die Informationen zum Repository ein.

:::image type="content" source="media/getting-started-portal/repository-details.png" alt-text="Details zum Repository":::

1. Wählen Sie Ihre bevorzugte _Organisation_ aus.
1. Wählen Sie in der Dropdownliste _Repository_ den Eintrag **my-first-web-static-app** aus.
1. Wählen Sie in der Dropdownliste _Branch_ den Eintrag **master** aus.
1. Wählen Sie unten auf der Seite die Schaltfläche **Next: Erstellen >** , um die Buildkonfiguration zu bearbeiten.

:::image type="content" source="media/getting-started-portal/next-build-button.png" alt-text="Schaltfläche „Weiter: Erstellen“":::

> [!NOTE]
> Wenn Sie keine Repositorys sehen, müssen Sie möglicherweise den Azure Static Web Apps in GitHub autorisieren. Navigieren Sie zu Ihrem GitHub-Repository, und wechseln Sie zu **Einstellungen > Anwendungen > Autorisierte OAuth-Apps**, wählen Sie **Azure Static Web Apps** und dann **Erteilen** aus. Bei Organisationsrepositorys müssen Sie Besitzer der Organisation sein, um die Berechtigungen erteilen zu können.

1. Fügen Sie auf der Registerkarte _Erstellen_ die für Ihr bevorzugtes Front-End-Framework spezifischen Konfigurationsdetails hinzu.

    # <a name="no-framework"></a>[Kein Framework](#tab/vanilla-javascript)

    - Löschen Sie den Standardwert aus dem Feld _App-Speicherort_.
    - Löschen Sie den Standardwert aus dem Feld _App-Speicherort_.
    - Löschen Sie den Standardwert aus dem Feld _Speicherort für App-Artefakte_.

    # <a name="angular"></a>[Angular](#tab/angular)

    - Löschen Sie den Standardwert aus dem Feld _App-Speicherort_.
    - Löschen Sie den Standardwert aus dem Feld _App-Speicherort_.
    - Geben Sie im Feld _Speicherort für App-Artefakte_ den Speicherort **dist/angular-basic** ein.

    # <a name="react"></a>[React](#tab/react)

    - Löschen Sie den Standardwert aus dem Feld _App-Speicherort_.
    - Löschen Sie den Standardwert aus dem Feld _App-Speicherort_.
    - Geben Sie im Feld _Speicherort für App-Artefakte_ den Speicherort **build** ein.

    # <a name="vue"></a>[Vue](#tab/vue)

    - Löschen Sie den Standardwert aus dem Feld _App-Speicherort_.
    - Löschen Sie den Standardwert aus dem Feld _App-Speicherort_.
    - Geben Sie im Feld _Speicherort für App-Artefakte_ den Speicherort **dist** ein.

    ---

1. Klicken Sie auf **Überprüfen + erstellen**.

    :::image type="content" source="media/getting-started-portal/review-create.png" alt-text="Schaltfläche „Bewerten + erstellen“":::

    > [!NOTE]
    > Sie können die [Workflowdatei](github-actions-workflow.md) bearbeiten, um diese Werte nach der Erstellung der App zu ändern.

1. Klicken Sie auf **Erstellen**.

    :::image type="content" source="media/getting-started-portal/create-button.png" alt-text="Schaltfläche „Erstellen“":::

1. Wählen Sie **Zu Ressource wechseln** aus.

    :::image type="content" source="media/getting-started-portal/resource-button.png" alt-text="Schaltfläche „Zu Ressource wechseln“":::

[!INCLUDE [view website](../../includes/static-web-apps-get-started-view-website.md)]

## <a name="clean-up-resources"></a>Bereinigen von Ressourcen

Falls Sie diese Anwendung nicht weiter nutzen möchten, können Sie die Azure Static Web Apps-Instanz mit den folgenden Schritten löschen:

1. Öffnen Sie das [Azure-Portal](https://portal.azure.com).
1. Suchen Sie in der oberen Suchleiste nach **my-first-web-static-app**.
1. Wählen Sie den App-Namen aus.
1. Wählen Sie die Schaltfläche **Löschen** aus.
1. Wählen Sie zum Bestätigen des Löschvorgangs **Ja** aus.

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [Hinzufügen einer API zu Azure Static Web Apps (Vorschauversion) mit Azure Functions](add-api.md)
