---
title: Erkunden eines Beispielszenarios
titleSuffix: Azure Digital Twins
description: Hier wird das ADT Explorer-Beispiel verwendet, um ein vorgefertigtes Szenario zu visualisieren und zu erkunden.
author: baanders
ms.author: baanders
ms.date: 8/12/2020
ms.topic: quickstart
ms.service: digital-twins
ms.openlocfilehash: b199a50443445b983011d755c3ffacaa71131faf
ms.sourcegitcommit: c6b9a46404120ae44c9f3468df14403bcd6686c1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88893909"
---
# <a name="explore-a-sample-azure-digital-twins-scenario-using-adt-explorer"></a>Erkunden eines Azure Digital Twins-Beispielszenarios mit ADT Explorer

Mit Azure Digital Twins können Sie Livemodelle Ihrer realen Umgebungen erstellen und mit ihnen interagieren. Hierzu werden einzelne Elemente als **digitale Zwillinge** modelliert und in einem **Graphen** miteinander verknüpft, der auf Liveereignisse reagieren kann und aus dem Informationen abgefragt werden können.

In dieser Schnellstartanleitung erkunden Sie einen vorgefertigten Azure Digital Twins-Graphen unter Verwendung einer Beispielanwendung namens [**ADT Explorer**](https://docs.microsoft.com/samples/azure-samples/digital-twins-explorer/digital-twins-explorer/) (Azure Digital Twins). Mit ADT Explorer können Sie ein Szenario hochladen, visuelle Darstellungen Ihrer Zwillinge und Ihres Graphen anzeigen und andere Verwaltungsaktivitäten in einer browserbasierten, visuellen Umgebung durchführen.

Diese Schnellstartanleitung umfasst folgende Hauptschritte:

1. Einrichten von Azure Digital Twins und ADT Explorer
1. Hochladen vorgefertigter Modelle und Graphdaten zum Erstellen des Beispielszenarios
1. Erkunden des erstellten Szenariographen
1. Ändern des Graphen

## <a name="prerequisites"></a>Voraussetzungen

Für diese Schnellstartanleitung ist ein Azure-Abonnement erforderlich. Bei Bedarf können Sie **[jetzt kostenlos ein Abonnement erstellen](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)** .

Bevor Sie mit der Schnellstartanleitung beginnen, müssen zwei Beispiele heruntergeladen werden:
* Die Beispielanwendung **ADT Explorer**. Dieses Beispiel enthält die Haupt-App, die im Rahmen der Schnellstartanleitung verwendet wird, um ein Azure Digital Twins-Szenario zu laden und zu erkunden. Die App finden Sie hier: [ADT Explorer (Azure Digital Twins)](https://docs.microsoft.com/samples/azure-samples/digital-twins-explorer/digital-twins-explorer/). Klicken Sie auf die Schaltfläche *Download ZIP* (ZIP herunterladen), um eine *ZIP-Datei* des Beispielcodes als _**ADT_Explorer.zip**_ auf Ihren Computer herunterzuladen.
* Das **Azure Digital Twins-Beispielszenario**. Es enthält einen vorgefertigten Azure Digital Twins-Graphen, der zur Verwendung in ADT Explorer geladen wird. Das Szenario finden Sie hier: [Azure Digital Twins (Beispiele)](https://docs.microsoft.com/samples/azure-samples/digital-twins-samples/digital-twins-samples). Klicken Sie auf die Schaltfläche *Download ZIP* (ZIP herunterladen), um eine *ZIP-Datei* des Beispielcodes als _**Azure_Digital_Twins_samples.zip**_ auf Ihren Computer herunterzuladen.

## <a name="set-up-azure-digital-twins-and-adt-explorer"></a>Einrichten von Azure Digital Twins und ADT Explorer

Für die Verwendung von Azure Digital Twins muss zunächst eine **Azure Digital Twins-Instanz** eingerichtet werden. Die erstellte Instanz des Diensts kann dann im weiteren Verlauf der Schnellstartanleitung mit den Beispieldaten aufgefüllt werden.

Darüber hinaus müssen Berechtigungen für ADT Explorer eingerichtet werden, damit die Anwendung auf Ihrem Computer ausgeführt werden und auf Ihre Azure Digital Twins-Instanz zugreifen kann. Dadurch können Sie mithilfe der Beispiel-App Ihre Instanz und die zugehörigen Daten erkunden.

### <a name="set-up-azure-digital-twins-instance"></a>Einrichten einer Azure Digital Twins-Instanz

Eine Instanz und die erforderliche Authentifizierung können Sie am einfachsten einrichten, indem Sie ein Beispielskript für die automatisierte Bereitstellung ausführen. Führen Sie die Anweisungen unter [ *Einrichten einer Instanz und der Authentifizierung (per Skript)* ](how-to-set-up-instance-scripted.md). Die Anleitung enthält auch Schritte zur Überprüfung, ob Sie jeden Schritt erfolgreich abgeschlossen haben und für die Nutzung Ihrer neuen Instanz bereit sind.

In dieser Schnellstartanleitung benötigen Sie die folgenden Werte, die Sie bei der Instanzeinrichtung verwendet haben. Wenn Sie diese Werte erneut abrufen müssen, verwenden Sie die unten aufgeführten Links zu den entsprechenden Abschnitten im Artikel zur Einrichtung, um sie im [Azure-Portal](https://portal.azure.com) zu ermitteln.
* Azure Digital Twins-Instanz: **_Hostname_** ([im Portal suchen](how-to-set-up-instance-portal.md#verify-success-and-collect-important-values))
* Azure AD-App-Registrierung: **_Anwendungs-ID (Client)_** ([im Portal suchen](how-to-set-up-instance-portal.md#collect-important-values))
* Azure AD-App-Registrierung: **_Verzeichnis-ID (Client)_** ([im Portal suchen](how-to-set-up-instance-portal.md#collect-important-values))

### <a name="set-adt-explorer-permissions"></a>Festlegen von Berechtigungen für ADT Explorer

Bereiten Sie als Nächstes die von Ihnen erstellte Azure Digital Twins-Instanz für die Arbeit mit ADT Explorer (einer lokal gehosteten Webanwendung) vor. Navigieren Sie im Azure-Portal zur Seite [App-Registrierungen](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps), und wählen Sie in der Liste den Namen Ihrer App-Registrierung aus.

Wählen Sie im Menü der Registrierung die Option *Authentifizierung* aus, und klicken Sie anschließend auf *+ Plattform hinzufügen*.

:::image type="content" source="media/quickstart-adt-explorer/authentication-pre.png" alt-text="Seite mit den Authentifizierungsdetails für eine App-Registrierung im Azure-Portal. Die Schaltfläche „Plattform hinzufügen“ ist hervorgehoben." lightbox="media/quickstart-adt-explorer/authentication-pre.png":::

Wählen Sie auf der Seite *Plattformen konfigurieren* die Option *Web* aus.
Geben Sie folgende Konfigurationsdetails an:
* **Umleitungs-URIs**: Fügen Sie *http://localhost:3000* als Umleitungs-URI hinzu.
* **Implizite Gewährung**: Aktivieren Sie das Kontrollkästchen *Zugriffstoken*.

:::row:::
    :::column:::
        :::image type="content" source="media/quickstart-adt-explorer/authentication-configure-web.png" alt-text="Seite „Plattformen konfigurieren“ mit Hervorhebung der oben beschriebenen Informationen":::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

Klicken Sie auf *Konfigurieren*, um den Vorgang abzuschließen.

Sie verfügen nun über eine Webkonfiguration für ADT Explorer. Dies sollte im Azure-Portal auf der Registerkarte „Authentifizierung“ zu sehen sein.

:::image type="content" source="media/quickstart-adt-explorer/authentication-post.png" alt-text="Seite mit den Authentifizierungsdetails für eine App-Registrierung im Azure-Portal. Der Webplattformabschnitt mit dem Umleitungs-URI http://localhost:3000 und die für Zugriffstoken aktivierte implizite Gewährung sind hervorgehoben.":::

### <a name="run-and-configure-adt-explorer"></a>Ausführen und Konfigurieren von ADT Explorer

Führen Sie als Nächstes die ADT Explorer-Anwendung aus, und konfigurieren Sie sie für Ihre Azure Digital Twins-Instanz.

Navigieren Sie zur heruntergeladenen Datei _**ADT_Explorer.zip**_, und entpacken Sie sie. Öffnen Sie eine Eingabeaufforderung am Speicherort *ADT_explorer/client/src*.

Führen Sie `npm install` aus, um alle erforderlichen Abhängigkeiten herunterzuladen.

Führen Sie dann `npm run start` aus, um die App zu starten.

Nach einigen Sekunden wird ein Browserfenster geöffnet, und die App wird im Browser angezeigt.

:::image type="content" source="media/quickstart-adt-explorer/explorer-blank.png" alt-text="Browserfenster mit einer unter „localhost:3000“ ausgeführten App. Die App heißt ADT Explorer und enthält Felder für einen Abfrage-Explorer, eine Modellansicht, eine Graphansicht und einen Eigenschaften-Explorer. Es sind noch keine Daten vorhanden." lightbox="media/quickstart-adt-explorer/explorer-blank.png":::

Klicken Sie im oberen Bereich des Fensters auf die Schaltfläche *Sign in* (Anmelden), um ADT Explorer für die Verwendung der von Ihnen eingerichteten Instanz zu konfigurieren. 

:::image type="content" source="media/quickstart-adt-explorer/sign-in.png" alt-text="ADT Explorer mit hervorgehobenem Anmeldesymbol im oberen Bereich des Fensters. Bei dem Symbol handelt es sich um eine einfache Silhouette einer Person mit der Silhouette eines Schlüssels im Vordergrund." lightbox="media/quickstart-adt-explorer/sign-in.png":::

Geben Sie die relevanten Informationen ein, die Sie zuvor im Abschnitt [Voraussetzungen](#prerequisites) gesammelt haben:
* Anwendungs-ID (Client)
* Verzeichnis-ID (Mandant)
* ADT-URL im Format *https://<instance host name>*

>[!NOTE]
> Sie können jederzeit zu diesen Informationen zurückkehren und sie bearbeiten. Wählen Sie dazu das gleiche Symbol aus, um das Anmeldefeld aufzurufen. Die von Ihnen übergebenen Werte werden gespeichert.

Sollte von Microsoft ein Popupfenster vom Typ *Angeforderte Berechtigungen* angezeigt werden, erteilen Sie Ihre Einwilligung für diese Anwendung, und akzeptieren Sie die Konfiguration, um fortzufahren.

## <a name="add-the-sample-data"></a>Hinzufügen der Beispieldaten

Importieren Sie als Nächstes das Beispielszenario und den Graphen in ADT Explorer.

Das Beispielszenario befindet sich in der heruntergeladenen Datei _**Azure_Digital_Twins_samples.zip**_. Navigieren Sie zu dieser Datei, und entzippen Sie sie.

### <a name="models"></a>Modelle

Der erste Schritt bei einer Azure Digital Twins-Lösung besteht darin, das Vokabular für Ihre Umgebung zu definieren. Hierzu werden benutzerdefinierte [**Modelle**](concepts-models.md) zur Beschreibung der in Ihrer Umgebung vorhandenen Entitätstypen erstellt. 

Die Modelle werden in einer JSON-LD-ähnlichen Sprache namens **Digital Twins Definition Language (DTDL)** geschrieben und beschreiben jeweils die *Eigenschaften*, *Telemetriedaten*, *Beziehungen* und *Komponenten* eines einzelnen Entitätstyps. Diese Modelle werden später als Grundlage für digitale Zwillinge verwendet, die bestimmte Instanzen dieser Typen darstellen.

Die Modellerstellung umfasst in der Regel drei Schritte:
1. Schreiben der Modelldefinition (in der Beispiellösung dieser Schnellstartanleitung bereits erledigt)
2. Überprüfen der Korrektheit der Syntax (in der Beispiellösung dieser Schnellstartanleitung bereits erledigt)
3. Hochladen in Ihre Azure Digital Twins-Instanz
 
Für diese Schnellstartanleitung wurden die Modelldateien bereits geschrieben und überprüft und in die heruntergeladene Lösung integriert. In diesem Abschnitt werden zwei vorgefertigte Modelle in Ihre Instanz hochgeladen, um die folgenden Komponenten einer Gebäudeumgebung zu definieren:
* Etage
* Raum

#### <a name="upload-models"></a>Hochladen von Modellen

Klicken Sie im Feld *MODEL VIEW* (MODELLANSICHT) auf das Symbol *Upload a Model* (Modell hochladen).

:::image type="content" source="media/quickstart-adt-explorer/upload-model.png" alt-text="Modellansichtsfeld mit hervorgehobenem mittlerem Symbol. Es zeigt einen auf eine Wolke gerichteten Pfeil." lightbox="media/quickstart-adt-explorer/upload-model.png":::
 
1. Navigieren Sie im daraufhin angezeigten Dateiauswahlfeld zum Ordner *Azure_Digital_Twins_samples/AdtSampleApp/SampleClientApp/models* des heruntergeladenen Repositorys.
2. Wählen Sie *Room.json* und *Floor.json* aus, und klicken Sie auf „OK“. (Sie können auch die anderen Modelle hochladen, diese werden in der Schnellstartanleitung jedoch nicht verwendet.)
3. Folgen Sie den Anweisungen in dem Popupdialogfeld, in dem Sie zur Anmeldung bei Ihrem Azure-Konto aufgefordert werden.

>[!NOTE]
>Wenn Sie die folgende Fehlermeldung erhalten: :::image type="content" source="media/quickstart-adt-explorer/error-models-popup.png" alt-text="Popupfenster mit dem Text „Error: Error fetching models: ClientAuthError: Error opening popup window. This can happen if you are using IE or if popups are blocked in the browser.“ (Fehler: Fehler beim Abrufen von Modellen: ClientAuthError: Fehler beim Öffnen des Popupfensters. Dieses Problem kann auftreten, wenn Sie Internet Explorer verwenden oder Popups im Browser blockiert sind.) und der Schaltfläche „Close“ (Schließen) im unteren Bereich." border="false"::: 
> Deaktivieren Sie Ihren Popupblocker, oder verwenden Sie einen anderen Browser.

Die Modelldateien werden von ADT Explorer in Ihre Azure Digital Twins-Instanz hochgeladen. Sie sollten im Feld *MODEL VIEW* (MODELLANSICHT) mit Anzeigename und vollständiger Modell-ID angezeigt werden. Sie können auf das Informationssymbol *View Model* (Modell anzeigen) klicken, um den zugrunde liegenden DTDL-Code anzuzeigen.

:::row:::
    :::column:::
        :::image type="content" source="media/quickstart-adt-explorer/model-info.png" alt-text="Feld „Model View“ (Modellansicht) mit zwei Modelldefinitionen: „Floor (dtmi:example:Floor;1)“ und „Room (dtmi:example:Room;1)“. Für die Modelle ist jeweils das Symbol „View Model“ (Modell anzeigen) hervorgehoben, das den Buchstaben „i“ in einem Kreis zeigt." lightbox="media/quickstart-adt-explorer/model-info.png":::
    :::column-end:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

### <a name="twins-and-the-twin-graph"></a>Zwillinge und der Zwillingsgraph

Nachdem Sie nun Modelle in Ihre Azure Digital Twins-Instanz hochgeladen haben, können Sie [**digitale Zwillinge**](concepts-twins-graph.md) hinzufügen, die den Modelldefinitionen entsprechen. 

Digitale Zwillinge stellen die tatsächlichen Entitäten in Ihrer Geschäftsumgebung dar – also etwa Sensoren eines landwirtschaftlichen Betriebs, die Beleuchtung eines Fahrzeugs oder (wie in dieser Schnellstartanleitung) Räume auf einer Etage eines Gebäudes. Sie können zahlreiche Zwillinge eines beliebigen Modelltyps erstellen (beispielsweise mehrere Räume, für die jeweils das Modell *Room* (Raum) verwendet wird) und sie mithilfe von Beziehungen in einem **Zwillingsgraphen**, der die gesamte Umgebung darstellt, miteinander verknüpfen.

In diesem Abschnitt werden vorab erstellte Zwillinge hochgeladen, die in einem vorab erstellten Graphen miteinander verknüpft sind. Der Graph enthält zwei Etagen und zwei Räume mit folgendem Layout:
* *Floor0* (Etage0)
    - enthält *Room0* (Raum0)
* *Floor1* (Etage1)
    - enthält *Room1* (Raum1)

#### <a name="import-the-graph"></a>Importieren des Graphen

Klicken Sie im Feld *GRAPH VIEW* (GRAPHANSICHT) auf das Symbol *Import Graph* (Graph importieren).

:::image type="content" source="media/quickstart-adt-explorer/import-graph.png" alt-text="Feld „Graph View“ (Graphansicht) mit einem hervorgehobenen Symbol. Es zeigt einen auf eine Wolke gerichteten Pfeil." lightbox="media/quickstart-adt-explorer/import-graph.png":::

Navigieren Sie in der Feldauswahl erneut zum Ordner *client/examples*, und wählen Sie die Tabellendatei _**buildingScenario.xlsx**_ aus. Diese Datei enthält eine Beschreibung des Beispielgraphen. Klicken Sie auf „OK“.

Nach wenigen Sekunden wird von ADT Explorer eine Importansicht mit einer Vorschau des zu ladenden Graphen angezeigt.

Klicken Sie zum Bestätigen des Graphuploads rechts oben in *GRAPH VIEW* (GRAPHANSICHT) auf das Symbol *Speichern*:

:::row:::
    :::column:::
        :::image type="content" source="media/quickstart-adt-explorer/graph-preview-save.png" alt-text="Hervorgehobenes Speichersymbol im Bereich mit der Graphvorschau" lightbox="media/quickstart-adt-explorer/graph-preview-save.png":::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

Von ADT Explorer werden nun unter Verwendung der hochgeladenen Datei die angeforderten Zwillinge und Beziehungen zwischen ihnen erstellt. Anschließend wird ein Dialogfeld mit dem Hinweis angezeigt, dass der Vorgang abgeschlossen ist. Klicken Sie auf *Close* (Schließen).

:::row:::
    :::column:::
        :::image type="content" source="media/quickstart-adt-explorer/import-success.png" alt-text="Dialogfeld mit der Information, dass der Graph erfolgreich importiert wurde. Der Text lautet: „Import successful. 49 twins imported. 50 relationships imported.“ (Import erfolgreich. 49 Zwillinge importiert. 50 Beziehungen importiert.)" lightbox="media/quickstart-adt-explorer/import-success.png":::
    :::column-end:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

Der Graph ist nun in ADT Explorer hochgeladen. Klicken Sie im oberen Bereich des Fensters von ADT Explorer im Feld *GRAPH EXPLORER* (GRAPH-EXPLORER) auf die Schaltfläche *Run Query* (Abfrage ausführen), um den Graphen anzuzeigen. 

:::image type="content" source="media/quickstart-adt-explorer/run-query.png" alt-text="Hervorgehobene Schaltfläche „Run Query“ (Abfrage ausführen) im oberen Bereich des Fensters" lightbox="media/quickstart-adt-explorer/run-query.png":::

Dadurch wird die Standardabfrage zum Auswählen und Anzeigen aller digitalen Zwillinge ausgeführt. ADT Explorer ruft alle Zwillinge und Beziehungen aus dem Dienst ab und zeichnet den durch sie definierten Graphen im Feld *GRAPH VIEW* (GRAPHANSICHT).

## <a name="explore-the-graph"></a>Erkunden des Graphen

Nun können Sie sich den hochgeladenen Graphen des Beispielszenarios ansehen:

:::image type="content" source="media/quickstart-adt-explorer/graph-view-full.png" alt-text="Ansicht des Felds „Graph View“ (Graphansicht) mit enthaltenem Zwillingsgraphen. Ein mit „floor1“ (Etage1) beschrifteter Kreis ist durch einen Pfeil mit der Beschriftung „contains“ (enthält) mit einem Kreis mit der Beschriftung „room1“ (Raum1) verbunden, und ein mit „floor0“ (Etage0) beschrifteter Kreis ist durch einen Pfeil mit der Beschriftung „contains“ (enthält) mit einem Kreis mit der Beschriftung „room0“ (Raum0) verbunden.":::

Die Kreise (Graphknoten) stellen digitale Zwillinge dar. Bei den Linien handelt es sich um Beziehungen. Wie Sie sehen, ist *Room0* (Raum0) im Zwilling *Floor0* (Etage0) und *Room1* (Raum1) im Zwilling *Floor1* (Etage1) enthalten.

Mit einer Maus können Sie auf Teile des Graphen klicken und sie durch Ziehen verschieben.

### <a name="view-twin-properties"></a>Anzeigen von Zwillingseigenschaften 

Sie können einen Zwilling auswählen, um eine Liste der zugehörigen Eigenschaften sowie deren Werte im Feld *PROPERTY EXPLORER* (EIGENSCHAFTEN-EXPLORER) anzuzeigen. 

Hier sehen Sie die Eigenschaften von *Room0* (Raum0):

:::row:::
    :::column:::
        :::image type="content" source="media/quickstart-adt-explorer/properties-room0.png" alt-text="Hervorhebung des Felds „Property Explorer“ (Eigenschaften-Explorer) mit Eigenschaften für „Room0“ (Raum0) – einschließlich des Felds „$dtId“ mit dem Wert „Room0“, eines Temperaturfelds mit dem Wert „70“ und eines Luftfeuchtigkeitsfelds mit dem Wert „30“." lightbox="media/quickstart-adt-explorer/properties-room0.png":::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

Beachten Sie, dass *Room0* (Raum0) eine Temperatur von **70** hat.

Hier sehen Sie die Eigenschaften von *Room1* (Raum1):

:::row:::
    :::column:::
        :::image type="content" source="media/quickstart-adt-explorer/properties-room1.png" alt-text="Hervorhebung des Felds „Property Explorer“ (Eigenschaften-Explorer) mit Eigenschaften für „Room1“ (Raum1) – einschließlich des Felds „$dtId“ mit dem Wert „Room1“, eines Temperaturfelds mit dem Wert „80“ und eines Luftfeuchtigkeitsfelds mit dem Wert „60“." lightbox="media/quickstart-adt-explorer/properties-room1.png":::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

Beachten Sie, dass *Room1* (Raum1) eine Temperatur von **80** hat.

### <a name="query-the-graph"></a>Abfragen des Diagramms

Eine Hauptfunktion von Azure Digital Twins ist das einfache [Abfragen](concepts-query-language.md) des Zwillingsgraphen und das effiziente Beantworten von Fragen zur Umgebung. 

Zum Abfragen der Zwillinge in Ihrem Graphen können unter anderem deren *Eigenschaften* verwendet werden. Mit eigenschaftenbasierten Abfragen lässt sich eine Vielzahl von Fragen beantworten. Dazu zählt auch das Auffinden von Ausreißern in Ihrer Umgebung, die möglicherweise Ihre Aufmerksamkeit erfordern.

In diesem Abschnitt wird eine Abfrage ausgeführt, um folgende Frage zu beantworten: _**Bei welchen Zwillingen in meiner Umgebung liegt die Temperatur über 75?**_

Führen Sie zur Beantwortung dieser Frage im Feld *QUERY EXPLORER* (ABFRAGE-EXPLORER) die folgende Abfrage aus:

```SQL
SELECT * FROM DigitalTwins T WHERE T.Temperature > 75
```

Wie Sie weiter oben bei der Betrachtung der Zwillingseigenschaften gesehen haben, hat *Room0* (Raum0) eine Temperatur von **70** und *Room1* (Raum1) eine Temperatur von **80**. Folglich wird in den Ergebnissen nur _**Room1**_ (Raum1) angezeigt.
    
:::image type="content" source="media/quickstart-adt-explorer/result-query-property-before.png" alt-text="Ergebnisse der Eigenschaftenabfrage, in denen nur „Room1“ (Raum1) angezeigt wird" lightbox="media/quickstart-adt-explorer/result-query-property-before.png":::

>[!TIP]
> In der obigen Abfrage werden auch andere Vergleichsoperatoren ( *<* , *>* , *=* oder *!=* ) unterstützt. Sie können in der Abfrage mit diesen Operatoren sowie mit anderen Werten und Zwillingseigenschaften experimentieren, um andere Fragen zu beantworten.

## <a name="edit-data-in-the-graph"></a>Bearbeiten von Daten im Graphen

Sie können ADT Explorer verwenden, um die Eigenschaften der im Graphen dargestellten Zwillinge zu bearbeiten. In diesem Abschnitt **_erhöhen Sie die Temperatur_ von „Room0“ (Raum0) auf 76**.

Wählen Sie dazu *Room0* (Raum0) aus, um die zugehörige Eigenschaftenliste im Feld *PROPERTY EXPLORER* (EIGENSCHAFTEN-EXPLORER) anzuzeigen.

Die Eigenschaften in dieser Liste können bearbeitet werden. Wählen Sie den Temperaturwert **70** aus, um die Eingabe eines neuen Werts zu ermöglichen. Geben Sie **76** ein, und klicken Sie auf das Symbol *Save* (Speichern), um die Temperatur auf **76** zu aktualisieren.

:::row:::
    :::column:::
        :::image type="content" source="media/quickstart-adt-explorer/new-properties-room0.png" alt-text="Das Feld „Property Explorer“ (Eigenschaften-Explorer) mit Eigenschaften für „Room0“ (Raum0). Der Temperaturwert ist ein bearbeitbares Feld, das den Wert „76“ enthält. Außerdem ist das Speichersymbol hervorgehoben." lightbox="media/quickstart-adt-explorer/new-properties-room0.png":::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

Nach dem Speichern wird das Fenster *Patch Information* (Patchinformationen) mit dem Patchcode angezeigt, der im Hintergrund für die [APIs](how-to-use-apis-sdks.md) von Azure Digital Twins verwendet wurde, um die Aktualisierung durchzuführen. Klicken Sie auf *Close* (Schließen).

### <a name="query-to-see-the-result"></a>Ausführen der Abfrage, um die Ergebnisse anzuzeigen

Vergewissern Sie sich, dass die Aktualisierung der Temperatur für *Room0* (Room0) vom Graphen registriert wurde. Führen Sie dazu erneut die Abfrage von weiter oben aus, **um alle Zwillinge in der Umgebung abzurufen, bei denen die Temperatur über 75 liegt**:

```SQL
SELECT * FROM DigitalTwins T WHERE T.Temperature > 75
```

Nachdem die Temperatur von *Room0* (Raum0) von **70** in **76** geändert wurde, sollten im Ergebnis beide Zwillinge angezeigt werden.

:::image type="content" source="media/quickstart-adt-explorer/result-query-property-after.png" alt-text="Ergebnisse der Eigenschaftenabfrage, in denen „Room0“ (Room0) und „Room1“ (Raum1) angezeigt werden" lightbox="media/quickstart-adt-explorer/result-query-property-after.png":::

## <a name="review-and-contextualize-learnings"></a>Überprüfen und Kontextualisieren der Erkenntnisse

In dieser Schnellstartanleitung haben Sie eine Azure Digital Twins-Instanz erstellt, eine Verbindung mit ADT Explorer hergestellt und die Instanz mit einem Beispielszenario aufgefüllt. 

Anschließend haben Sie folgende Aktionen für den Graphen ausgeführt:
1. Sie haben eine Abfrage zur Beantwortung einer szenariobezogenen Frage ausgeführt.
2. Sie haben eine Eigenschaft eines digitalen Zwillings bearbeitet.
    * Sie haben die Abfrage erneut ausgeführt, um zu sehen, wie sich die Antwort nach Ihrer Aktualisierung geändert hat.

Diese Übung veranschaulicht, wie Sie den Azure Digital Twins-Graphen verwenden können, um Fragen zu einer Umgebung zu beantworten, auch wenn sich diese verändert. 

In dieser Schnellstartanleitung wurde die Temperatur zwar manuell geändert, in Azure Digital Twins werden digitale Zwillinge jedoch häufig mit echten IoT-Geräten verbunden, um automatische, auf Telemetriedaten basierende Aktualisierungen zu erhalten. Dadurch können Sie einen Livegraphen erstellen, der immer den tatsächlichen Zustand Ihrer Umgebung widerspiegelt, und Abfragen verwenden, um Echtzeitinformationen zu den Vorgängen in Ihrer Umgebung zu erhalten.

## <a name="clean-up-resources"></a>Bereinigen von Ressourcen

Beenden Sie zum Abschließen dieser Schnellstartanleitung zunächst die ausgeführte Konsolen-App. Dadurch wird die Verbindung mit der ADT Explorer-App im Browser getrennt, und es können keine Livedaten mehr im Browser angezeigt werden. Sie können den Browsertab schließen.

Falls Sie mit den Tutorials für Azure Digital Twins fortfahren möchten, können Sie die in dieser Schnellstartanleitung verwendete Instanz in den entsprechenden Artikeln wiederverwenden und müssen sie nicht entfernen.
 
[!INCLUDE [digital-twins-cleanup-basic.md](../../includes/digital-twins-cleanup-basic.md)]

Löschen Sie abschließend die Dateien des Beispielprojekts, die Sie auf Ihren lokalen Computer heruntergeladen haben (_**ADT_Explorer.zip**_ und _**Azure_Digital_Twins_samples.zip**_).

## <a name="next-steps"></a>Nächste Schritte 

Fahren Sie mit den Tutorials für Azure Digital Twins fort, um Ihr eigenes Azure Digital Twins-Szenario und Ihre eigenen Interaktionstools zu erstellen.

> [!div class="nextstepaction"]
> [*Tutorial: Codieren einer Client-App*](tutorial-code.md)