---
title: Details zu unterstützten Datenformaten | Microsoft Azure Maps
description: Hier erfahren Sie, wie durch Trennzeichen getrennte räumliche Daten im räumlichen E/A-Modul analysiert werden.
author: anastasia-ms
ms.author: v-stharr
ms.date: 03/03/2020
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: philmea
ms.openlocfilehash: 4b7c82e4650c7680709e809d9f563d79f068601f
ms.sourcegitcommit: 0e8a4671aa3f5a9a54231fea48bcfb432a1e528c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/24/2020
ms.locfileid: "87127926"
---
# <a name="supported-data-format-details"></a>Details zu unterstützten Datenformaten

Dieser Artikel enthält Einzelheiten zur Lese- und Schreibunterstützung für alle XML-Tags und Well-Known-Text-Geometrietypen. Außerdem erfahren Sie, wie durch Trennzeichen getrennte räumliche Daten im räumlichen E/A-Modul analysiert werden.

## <a name="supported-xml-namespaces"></a>Unterstützte XML-Namespaces

Das räumliche E/A-Modul unterstützt XML-Tags aus den folgenden Namespaces:

| Namespacepräfix | Namespace-URI   | Notizen                                                                    |
|:------------------|:-----------------|:----------------------------------------|
| `atom`           | `http://www.w3.org/2005/Atom`   |                                         |
| `geo`            | `http://www.w3.org/2003/01/geo/wgs84_pos#`  | Schreibgeschützte Unterstützung in GeoRSS-Dateien.           |
| `georss`         | `http://www.georss.org/georss`  |                                                |
| `geourl`         | `http://geourl.org/rss/module/` | Schreibgeschützte Unterstützung in GeoRSS-Dateien.                       |
| `gml`            | `http://www.opengis.net/gml`    |                                                        |
| `gpx`            | `http://www.topografix.com/GPX/1/1` |                                                   |
| `gpxx`           | `http://www.garmin.com/xmlschemas/GpxExtensions/v3` | Schreibgeschützte Unterstützung in GPX-Dateien. Analysiert und verwendet „DisplayColor“. Alle anderen Eigenschaften werden den Formmetadaten hinzugefügt. |
| `gpx_style`      | `http://www.topografix.com/GPX/gpx_style/0/2`      | Unterstützt in GPX-Dateien. Verwendet Linienfarbe. |
| `gx`             | `http://www.google.com/kml/ext/2.2` |                                                      |
| `kml`            | `http://www.opengis.net/kml/2.2`    |                                                      |
| `rss`            |                                 | Schreibgeschützt. Für GeoRSS-Schreibvorgänge wird das Atom-Format verwendet.              |

## <a name="supported-xml-elements"></a>Unterstützte XML-Elemente

Das räumliche E/A-Modul unterstützt die folgenden XML-Elemente. Alle nicht unterstützten XML-Tags werden in ein JSON-Objekt konvertiert. Anschließend wird jedes Tag als Eigenschaft im Feld `properties` der übergeordneten Form oder Ebene hinzugefügt.

### <a name="kml-elements"></a>KML-Elemente

Das räumliche E/A-Modul unterstützt die folgenden KML-Elemente:

| Elementname         | Lesen    | Schreiben   | Notizen                                                                                                                      |
|----------------------|---------|---------|----------------------------------------------------------------------------------------------------------------------------|
| `address`            | Teilweise | ja     | Das Objekt wird analysiert, aber nicht zum Positionieren der Form verwendet.                                                                    |
| `AddressDetails`     | Teilweise | nein      | Das Objekt wird analysiert, aber nicht zum Positionieren der Form verwendet.                                                                    |
| `atom:author`        | ja     | ja     |                                                                                                                            |
| `atom:link`          | ja     | ja     |                                                                                                                            |
| `atom:name`          | ja     | ja     |                                                                                                                            |
| `BalloonStyle`       | Teilweise | Teilweise | `displayMode` wird nicht unterstützt. Wird in `PopupTemplate` konvertiert. Fügen Sie zum Schreiben eine Eigenschaft vom Typ `popupTemplate` als Eigenschaft des Features hinzu, für das der Schreibvorgang ausgeführt werden soll. |
| `begin`              | ja     | ja     |                                                                                                                            |
| `color`              | ja     | ja     | Beinhaltet `#AABBGGRR` und `#BBGGRR`. Wird analysiert, um eine CSS-Farbzeichenfolge zu erhalten.                                                           |
| `colorMode`          | ja     | nein      |                                                                                                                            |
| `coordinates`        | ja     | ja     |                                                                                                                            |
| `Data`               | ja     | ja     |                                                                                                                            |
| `description`        | ja     | ja     |                                                                                                                            |
| `displayName`        | ja     | ja     |                                                                                                                            |
| `Document`           | ja     | ja     |                                                                                                                            |
| `drawOrder`          | Teilweise | nein      | Wird für Bodenüberlagerungen gelesen und zum Sortieren dieser Überlagerungen verwendet. 
| `east`               | ja     | ja     |                                                                                                                            |
| `end`                | ja     | ja     |                                                                                                                            |
| `ExtendedData`       | ja     | ja     | Unterstützt nicht typisierte Elemente vom Typ `Data`, `SimpleData` und `Schema` sowie Entitätsersetzungen im Format `$[dataName]`.                      |
| `extrude`            | Teilweise | Teilweise | Wird nur für Polygone unterstützt. MultiGeometry-Objekte mit Polygonen verschiedener Höhe werden in einzelne Features unterteilt. Linienformate werden nicht unterstützt. Polygone mit der Höhe „0“ werden als flaches Polygon gerendert. Beim Lesen wird die Höhe der ersten Koordinate im äußeren Ring als Höheneigenschaft des Polygons hinzugefügt. Anschließend wird die Höhe der ersten Koordinate verwendet, um das Polygon auf der Karte zu rendern. |
| `fill`               | ja     | ja     |                                                                                                                            |
| `Folder`             | ja     | ja     |                                                                                                                            |
| `GroundOverlay`      | ja     | ja     | `color` wird nicht unterstützt.                                                                                                   |
| `heading`            | Teilweise | nein      | Wird analysiert, aber nicht von `SimpleDataLayer` gerendert. Ein Schreibvorgang wird nur ausgeführt, wenn Daten in der Eigenschaft der Form gespeichert werden.                 |
| `hotSpot`            | ja     | Teilweise | Ein Schreibvorgang wird nur ausgeführt, wenn Daten in der Eigenschaft der Form gespeichert werden. Einheiten werden nur als Pixel ausgegeben.                         |
| `href`               | ja     | ja     |                                                                                                                            |
| `Icon`               | Teilweise | Teilweise | Wird analysiert, aber nicht von `SimpleDataLayer` gerendert. Die Symboleigenschaft der Form wird nur geschrieben, wenn sie URI-Daten enthält. Nur `href` wird unterstützt. |
| `IconStyle`          | Teilweise | Teilweise | Werte vom Typ `icon`, `heading`, `colorMode` und `hotspots` werden analysiert, aber nicht von `SimpleDataLayer` gerendert.         |
| `innerBoundaryIs`    | ja     | ja     |                                                                                                                            |
| `kml`                | ja     | ja     |                                                                                                                            |
| `LabelStyle`         | nein      | nein      |                                                                                                                            |
| `LatLonBox`          | ja     | ja     |                                                                                                                            |
| `gx:LatLonQuad`      | ja     | ja     |                                                                                                                            |
| `LinearRing`         | ja     | ja     |                                                                                                                            |
| `LineString`         | ja     | ja     |                                                                                                                            |
| `LineStyle`          | ja     | ja     | `colorMode` wird nicht unterstützt.                                                                                         |
| `Link`               | ja     | nein      | Für Netzwerkverbindungen wird nur die Eigenschaft `href` unterstützt.                                                                   |
| `MultiGeometry`      | Teilweise | Teilweise | Wird beim Lesen ggf. in einzelne Features unterteilt.                                                                     |
| `name`               | ja     | ja     |                                                                                                                            |
| `NetworkLink`        | ja     | nein      | Links müssen sich in der gleichen Domäne befinden wie das Dokument.                                                                  |
| `NetworkLinkControl` | nein      | nein      |                                                                                                                            |
| `north`              | ja     | ja     |                                                                                                                            |
| `open`               | ja     | ja     |                                                                                                                            |
| `outerBoundaryIs`    | ja     | ja     |                                                                                                                            |
| `outline`            | ja     | ja     |                                                                                                                            |
| `overlayXY`          | nein      | nein      |                                                                                                                            |
| `Pair`               | Teilweise | nein      | Es wird nur der Stil `normal` in einem Element vom Typ `StyleMap` unterstützt. `highlight` wird nicht unterstützt.                                   |
| `phoneNumber`        | ja     | ja     |                                                                                                                            |
| `PhotoOverlay`       | nein      | nein      |                                                                                                                            |
| `Placemark`          | ja     | ja     |                                                                                                                            |
| `Point`              | ja     | ja     |                                                                                                                            |
| `Polygon`            | ja     | ja     |                                                                                                                            |
| `PolyStyle`          | ja     | ja     |                                                                                                                            |
| `Region`             | Teilweise | Teilweise | `LatLongBox` wird auf der Dokumentebene unterstützt.                                                                      |
| `rotation`           | nein      | nein      |                                                                                                                            |
| `rotationXY`         | nein      | nein      |                                                                                                                            |
| `scale`              | nein      | nein      |                                                                                                                            |
| `Schema`             | ja     | ja     |                                                                                                                            |
| `SchemaData`         | ja     | ja     |                                                                                                                            |
| `schemaUrl`          | Teilweise | ja     | Das Laden von Stilen aus externen Dokumenten, die in keiner KMZ-Datei enthalten sind, wird nicht unterstützt.                             |
| `ScreenOverlay`      | nein      | nein      |                                                                                                                            |
| `screenXY`           | nein      | nein      |                                                                                                                            |
| `SimpleData`         | ja     | ja     |                                                                                                                            |
| `SimpleField`        | ja     | ja     |                                                                                                                            |
| `size`               | nein      | nein      |                                                                                                                            |
| `Snippet`            | Teilweise | Teilweise | Das Attribut `maxLines` wird ignoriert.                                                                                  |
| `south`              | ja     | ja     |                                                                                                                            |
| `Style`              | ja     | ja     |                                                                                                                            |
| `StyleMap`           | Teilweise | nein      | Nur der normale Stil in einem Element vom Typ `StyleMap` wird unterstützt.                                                                        |
| `styleUrl`           | Teilweise | ja     | URLs für externe Stile werden nicht unterstützt.                                                                         |
| `text`               | ja     | ja     | Das Ersetzen von `$[geDirections]` wird nicht unterstützt.                                                                          |
| `textColor`          | ja     | ja     |                                                                                                                            |
| `TimeSpan`           | ja     | ja     |                                                                                                                            |
| `TimeStamp`          | ja     | ja     |                                                                                                                            |
| `value`              | ja     | ja     |                                                                                                                            |
| `viewRefreshMode`    | Teilweise | nein      |  Wenn auf einen WMS-Dienst verwiesen wird, wird für Bodenüberlagerungen nur `onStop` unterstützt. `BBOX=[bboxWest],[bboxSouth],[bboxEast],[bboxNorth]` wird an die URL angefügt und aktualisiert, wenn die Karte verschoben wird.  |
| `visibility`         | ja     | ja     |                                                                                                                            |
| `west`               | ja     | ja     |                                                                                                                            |
| `when`               | ja     | ja     |                                                                                                                            |
| `width`              | ja     | ja     |                                                                                                                            |

### <a name="georss-elements"></a>GeoRSS-Elemente

Das räumliche E/A-Modul unterstützt die folgenden GeoRSS-Elemente:

| Elementname             | Lesen    | Schreiben | Notizen                                                                                          |
|--------------------------|---------|-------|------------------------------------------------------------------------------------------------|
| `atom:author`            | ja     | ja   |                                                                                                |
| `atom:category`          | ja     | ja   |                                                                                                |
| `atom:content`           | ja     | ja   |                                                                                                |
| `atom:contributor`       | ja     | ja   |                                                                                                |
| `atom:email`             | ja     | ja   |                                                                                                |
| `atom:entry`             | ja     | ja   |                                                                                                |
| `atom:feed`              | ja     | ja   |                                                                                                |
| `atom:icon`              | ja     | ja   |                                                                                                |
| `atom:id`                | ja     | ja   |                                                                                                |
| `atom:link`              | ja     | ja   |                                                                                                |
| `atom:logo`              | ja     | ja   |                                                                                                |
| `atom:name`              | ja     | ja   |                                                                                                |
| `atom:published`         | ja     | ja   |                                                                                                |
| `atom:rights`            | ja     | ja   |                                                                                                |
| `atom:source`            | ja     | ja   |                                                                                                |
| `atom:subtitle`          | ja     | ja   |                                                                                                |
| `atom:summary`           | ja     | ja   |                                                                                                |
| `atom:title`             | ja     | ja   |                                                                                                |
| `atom:updated`           | ja     | ja   |                                                                                                |
| `atom:uri`               | ja     | ja   |                                                                                                |
| `geo:lat`                | ja     | nein    | Wird als `georss:point` geschrieben.                                                                   |
| `geo:lon`                | ja     | nein    | Wird als `georss:point` geschrieben.                                                                   |
| `geo:long`               | ja     | nein    | Wird als `georss:point` geschrieben.                                                                   |
| `georss:box`             | ja     | nein    | Wird als Polygon gelesen und mit der `subType`-Eigenschaft „Rectangle“ (Rechteck) versehen.                                |
| `georss:circle`          | ja     | ja   |                                                                                                |
| `georss:elev`            | ja     | ja   |                                                                                                |
| `georss:featurename`     | ja     | ja   |                                                                                                |
| `georss:featuretypetag`  | ja     | ja   |                                                                                                |
| `georss:floor`           | ja     | ja   |                                                                                                |
| `georss:line`            | ja     | ja   |                                                                                                |
| `georss:point`           | ja     | ja   |                                                                                                |
| `georss:polygon`         | ja     | ja   |                                                                                                |
| `georss:radius`          | ja     | ja   |                                                                                                |
| `georss:relationshiptag` | ja     | ja   |                                                                                                |
| `georss:where`           | ja     | ja   |                                                                                                |
| `geourl:latitude`        | ja     | nein    | Wird als `georss:point` geschrieben.                                                                   |
| `geourl:longitude`       | ja     | nein    | Wird als `georss:point` geschrieben.                                                                   |
| `position`               | ja     | nein    | Bei manchen XML-Feeds wird GML mit einem Positionstag (anstelle eines `georss:where`-Tags) umschlossen. Dieses Tag wird zwar gelesen, beim Schreiben wird jedoch ein `georss:where`-Tag verwendet. |
| `rss`                    | ja     | nein    | GeoRSS (im ATOM-Format geschrieben).                                                                 |
| `rss:author`             | ja     | Teilweise | Wird als `atom:author` geschrieben.                                                                 |
| `rss:category`           | ja     | Teilweise | Wird als `atom:category` geschrieben.                                                               |
| `rss:channel`            | ja     | nein    |                                                                                                |
| `rss:cloud`              | ja     | nein    |                                                                                                |
| `rss:comments`           | ja     | nein    |                                                                                                |
| `rss:copyright`          | ja     | Teilweise | Wird als `atom:rights` geschrieben, wenn die Form noch nicht über eine Eigenschaft vom Typ `rights` `properties` verfügt.       |
| `rss:description`        | ja     | Teilweise | Wird als `atom:content` geschrieben, wenn die Form noch nicht über eine Eigenschaft vom Typ `content` `properties` verfügt.      |
| `rss:docs`               | ja     | nein    |                                                                                                |
| `rss:enclosure`          | ja     | nein    |                                                                                                |
| `rss:generator`          | ja     | nein    |                                                                                                |
| `rss:guid`               | ja     | Teilweise | Wird als `atom:id` geschrieben, wenn die Form noch nicht über eine Eigenschaft vom Typ `id` `properties` verfügt.         |
| `rss:image`              | ja     | Teilweise | Wird als `atom:logo` geschrieben, wenn die Form noch nicht über eine Eigenschaft vom Typ `logo` `properties` verfügt.      |
| `rss:item`               | ja     | Teilweise | Wird als `atom:entry` geschrieben.                                                                  |
| `rss:language`           | ja     | nein    |                                                                                                |
| `rss:lastBuildDate`      | ja     | Teilweise | Wird als `atom:updated` geschrieben, wenn die Form noch nicht über eine Eigenschaft vom Typ `updated` `properties` verfügt.     |
| `rss:link`               | ja     | Teilweise | Wird als `atom:link` geschrieben.                                                                   |
| `rss:managingEditor`     | ja     | Teilweise | Wird als `atom:contributor` geschrieben.                                                            |
| `rss:pubDate`            | ja     | Teilweise | Wird als `atom:published` geschrieben, wenn die Form noch nicht über eine Eigenschaft vom Typ `published` `properties` verfügt.  |
| `rss:rating`             | ja     | nein    |                                                                                                |
| `rss:skipDays`           | ja     | nein    |                                                                                                |
| `rss:skipHours`          | ja     | nein    |                                                                                                |
| `rss:source`             | ja     | Teilweise | Wird als `atom:source` geschrieben mit `atom:link` geschrieben.                                       |
| `rss:textInput`          | ja     | nein    |                                                                                                |
| `rss:title`              | ja     | Teilweise | Wird als `atom:title` geschrieben.                                                                  |
| `rss:ttl`                | ja     | nein    |                                                                                                |
| `rss:webMaster`          | ja     | nein    |                                                                                                |

### <a name="gml-elements"></a>GML-Elemente

Das räumliche E/A-Modul unterstützt die folgenden GML-Elemente: 

| Elementname            | Lesen | Schreiben | Notizen                                                                                  |
|-------------------------|------|-------|----------------------------------------------------------------------------------------|
| `gml:coordinates`       | ja  | nein    | Wird als `gml:posList` geschrieben.                                                              |
| `gml:curveMember`       | ja  | nein    |                                                                                        |
| `gml:curveMembers`      | ja  | nein    |                                                                                        |
| `gml:Box`               | ja  | nein    | Wird als `gml:Envelope` geschrieben.                                                             |
| `gml:description`       | ja  | ja   |                                                                                        |
| `gml:Envelope`          | ja  | ja   |                                                                                        |
| `gml:exterior`          | ja  | ja   |                                                                                        |
| `gml:Feature`           | ja  | nein    | Wird als Form geschrieben.                                                                    |
| `gml:FeatureCollection` | ja  | nein    | Wird als Geometrieauflistung geschrieben.                                                      |
| `gml:featureMember`     | ja  | nein    | Wird als Geometrieauflistung geschrieben.                                                      |
| `gml:geometry`          | ja  | nein    | Wird als Form geschrieben.                                                                    |
| `gml:geometryMember`    | ja  | ja   |                                                                                        |
| `gml:geometryMembers`   | ja  | ja   |                                                                                        |
| `gml:identifier`        | ja  | ja   |                                                                                        |
| `gml:innerBoundaryIs`   | ja  | nein    | Wird mithilfe von `gml.interior` geschrieben.                                                          |
| `gml:interior`          | ja  | ja   |                                                                                        |
| `gml:LinearRing`        | ja  | ja   |                                                                                        |
| `gml:LineString`        | ja  | ja   |                                                                                        |
| `gml:lineStringMember`  | ja  | ja   |                                                                                        |
| `gml:lineStringMembers` | ja  | nein    |                                                                                        |
| `gml:MultiCurve`        | ja  | nein    | Liest nur Member vom Typ `gml:LineString`. Wird als `gml.MultiLineString` geschrieben.                  |
| `gml:MultiGeometry`     | Teilweise  | Teilweise   | Wird nur als FeatureCollection-Element gelesen.                                              |
| `gml:MultiLineString`   | ja  | ja   |                                                                                        |
| `gml:MultiPoint`        | ja  | ja   |                                                                                        |
| `gml:MultiPolygon`      | ja  | ja   |                                                                                        |
| `gml:MultiSurface`      | ja  | nein    | Liest nur Member vom Typ `gml:Polygon`. Wird als `gml.MultiPolygon` geschrieben.                        |
| `gml:name`              | ja  | ja   |                                                                                        |
| `gml:outerBoundaryIs`   | ja  | nein    | Wird mithilfe von `gml.exterior` geschrieben.                                                          |
| `gml:Point`             | ja  | ja   |                                                                                        |
| `gml:pointMember`       | ja  | ja   |                                                                                        |
| `gml:pointMembers`      | ja  | nein    |                                                                                        |
| `gml:Polygon`           | ja  | ja   |                                                                                        |
| `gml:polygonMember`     | ja  | ja   |                                                                                        |
| `gml:polygonMembers`    | ja  | nein    |                                                                                        |
| `gml:pos`               | ja  | ja   |                                                                                        |
| `gml:posList`           | ja  | ja   |                                                                                        |
| `gml:surfaceMember`     | ja  | ja   |                                                                                        |

#### <a name="additional-notes"></a>Weitere Hinweise

- Member-Elemente werden nach einer Geometrie durchsucht, die sich möglicherweise in untergeordneten Elementen befindet. Dieser Suchvorgang ist erforderlich, da viele auf GML-basierende XML-Formate möglicherweise keine Geometrie als direkt untergeordnetes Element eines Member-Elements platzieren.
- `srsName` wird für WGS84-Koordinaten und die folgenden Codes teilweise unterstützt: [EPSG:4326](https://epsg.io/4326) und Web Mercator ([EPSG:3857](https://epsg.io/3857)) oder einer der alternativen Codes. Alle anderen Koordinatensysteme werden unverändert als WGS84 analysiert.
- Sofern beim Lesen eines XML-Feeds nicht angegeben, wird die Achsenreihenfolge auf der Grundlage von Hinweisen im XML-Feed ermittelt. Die Achsenreihenfolge „Breitengrad, Längengrad“ wird bevorzugt.
- Ist beim Schreiben in eine GML-Datei kein benutzerdefinierter GML-Namespace für die Eigenschaften angegeben, werden keine zusätzlichen Eigenschaftsinformationen hinzugefügt.

### <a name="gpx-elements"></a>GPX-Elemente

Das räumliche E/A-Modul unterstützt die folgenden GPX-Elemente:

| Elementname             | Lesen    | Schreiben   | Notizen                                                                                       |
|--------------------------|---------|---------|---------------------------------------------------------------------------------------------|
| `gpx:ageofdgpsdata`      | ja     | ja     |                                                                                             |
| `gpx:author`             | ja     | ja     |                                                                                             |
| `gpx:bounds`             | ja     | ja     | Wird beim Lesen in ein LocationRect-Element konvertiert.                                                    |
| `gpx:cmt`                | ja     | ja     |                                                                                             |
| `gpx:copyright`          | ja     | ja     |                                                                                             |
| `gpx:desc`               | ja     | ja     | Wird zur Abstimmung auf andere XML-Formate beim Lesen in eine Beschreibungseigenschaft kopiert.               |
| `gpx:dgpsid`             | ja     | ja     |                                                                                             |
| `gpx:ele`                | ja     | ja     |                                                                                             |
| `gpx:extensions`         | Teilweise | Teilweise | Beim Lesen werden Stilinformationen extrahiert. Alle anderen Erweiterungen werden in einem einfachen JSON-Objekt zusammengefasst. Nur Informationen zum Formstil werden geschrieben. |
| `gpx:geoidheight`        | ja     | ja     |                                                                                             |
| `gpx:gpx`                | ja     | ja     |                                                                                             |
| `gpx:hdop`               | ja     | ja     |                                                                                             |
| `gpx:link`               | ja     | ja     |                                                                                             |
| `gpx:magvar`             | ja     | ja     |                                                                                             |
| `gpx:metadata`           | ja     | ja     |                                                                                             |
| `gpx:name`               | ja     | ja     |                                                                                             |
| `gpx:pdop`               | ja     | ja     |                                                                                             |
| `gpx:rte`                | ja     | ja     |                                                                                             |
| `gpx:rtept`              | ja     | ja     |                                                                                             |
| `gpx:sat`                | ja     | ja     |                                                                                             |
| `gpx:src`                | ja     | ja     |                                                                                             |
| `gpx:sym`                | ja     | ja     | Der Wert wird erfasst, aber nicht zum Ändern des Reißzweckensymbols verwendet.                               |
| `gpx:text`               | ja     | ja     |                                                                                             |
| `gpx:time`               | ja     | ja     |                                                                                             |
| `gpx:trk`                | ja     | ja     |                                                                                             |
| `gpx:trkpt`              | ja     | ja     |                                                                                             |
| `gpx:trkseg`             | ja     | ja     |                                                                                             |
| `gpx:type`               | ja     | ja     |                                                                                             |
| `gpx:vdop`               | ja     | ja     |                                                                                             |
| `gpx:wpt`                | ja     | ja     |                                                                                             |
| `gpx_style:color`        | ja     | ja     |                                                                                             |
| `gpx_style:line`         | Teilweise | Teilweise | `color`, `opacity`, `width` und `lineCap` werden unterstützt.                                           |
| `gpx_style:opacity`      | ja     | ja     |                                                                                             |
| `gpx_style:width`        | ja     | ja     |                                                                                             |
| `gpxx:DisplayColor`      | ja     | nein      | Dient zum Angeben der Farbe einer Form. Beim Schreiben wird stattdessen die Farbe `gpx_style:line` verwendet.  |
| `gpxx:RouteExtension`    | Teilweise | nein      | Alle Eigenschaften werden in `properties` eingelesen. Nur `DisplayColor` wird verwendet.                     |
| `gpxx:TrackExtension`    | Teilweise | nein      | Alle Eigenschaften werden in `properties` eingelesen. Nur `DisplayColor` wird verwendet.                     |
| `gpxx:WaypointExtension` | Teilweise | nein      | Alle Eigenschaften werden in `properties` eingelesen. Nur `DisplayColor` wird verwendet.                     |
| `gpx:keywords`           | ja     | ja     |                                                                                             |
| `gpx:fix`                | ja     | ja     |                                                                                             |

#### <a name="additional-notes"></a>Weitere Hinweise

Beim Schreiben gilt Folgendes:

- MultiPoint-Elemente werden in einzelne Wegpunkte unterteilt.
- Polygon- und MultiPolygon-Elemente werden als Strecken geschrieben. 
  
## <a name="supported-well-known-text-geometry-types"></a>Unterstützte Well-Known-Text-Geometrietypen

| Geometrietyp | Lesen | Schreiben |
|--------------|:----:|:-----:|
| POINT | x | x |
| POINT Z | x | x | 
| POINT M | x | x<sup>[2]</sup> |
| POINT ZM | x<sup>[1]</sup><sup>[2]</sup> | | 
| LINESTRING | x | x |
| LINESTRING Z | x | x | 
| LINESTRING M | x | x<sup>[2]</sup> |
| LINESTRING ZM | x<sup>[1]</sup><sup>[2]</sup> | | 
| POLYGON | x | x |
| POLYGON Z | x | x |
| POLYGON M | x | x<sup>[2]</sup> |
| POLYGON ZM | x<sup>[1]</sup><sup>[2]</sup> | | 
| MULTIPOINT | x | x |
| MULTIPOINT Z | x | x | 
| MULTIPOINT M | x | x<sup>[2]</sup> |
| POMULTIPOINTINT ZM | x<sup>[1]</sup><sup>[2]</sup> | | 
| MULTILINESTRING | x | x |
| MULTILINESTRING Z | x | x | 
| MULTILINESTRING M | x | x<sup>[2]</sup> |
| MULTILINESTRING ZM | x<sup>[1]</sup><sup>[2]</sup> | | 
| MULTIPOLYGON | x | x |
| MULTIPOLYGON Z | x | x | 
| MULTIPOLYGON M | x | x<sup>[2]</sup> |
| MULTIPOLYGON ZM | x<sup>[1]</sup><sup>[2]</sup> | | 
| GEOMETRYCOLLECTION | x | x |
| GEOMETRYCOLLECTION Z | x | x | 
| GEOMETRYCOLLECTION M | x | x<sup>[2]</sup> | 
| GEOMETRYCOLLECTION ZM | x<sup>[1]</sup><sup>[2]</sup> | x | 

\[1\] Nur der Z-Parameter wird erfasst und als dritter Wert in den Positionswert eingefügt.

\[2\] Der M-Parameter wird nicht erfasst.

## <a name="delimited-spatial-data-support"></a>Unterstützung von durch Trennzeichen getrennten räumlichen Daten

Durch Trennzeichen getrennte räumliche Daten (beispielsweise CSV-Dateien) enthalten häufig Spalten mit räumlichen Daten. Dabei kann es sich beispielsweise um Spalten mit Breiten- und Längengradinformationen handeln. Im Well-Known-Text-Format kann eine Spalte mit räumlichen Geometriedaten enthalten sein.

### <a name="spatial-data-column-detection"></a>Erkennung von Spalten mit räumlichen Daten

Beim Lesen einer durch Trennzeichen getrennten Datei mit räumlichen Daten wird durch Analysieren der Kopfzeile ermittelt, welche Spalten Positionsfelder enthalten. Wenn die Kopfzeile Typinformationen enthält, werden diese verwendet, um die Zellwerte in den entsprechenden Typ umzuwandeln. Ist keine Kopfzeile angegeben, wird die erste Zeile analysiert und zum Generieren einer Kopfzeile verwendet. Bei der Analyse der ersten Zeile werden Spaltennamen ohne Berücksichtigung der Groß-/Kleinschreibung mit den folgenden Namen abgeglichen. Die Reihenfolge der Namen entspricht der Priorität für den Fall, dass in einer Datei mehrere Namen vorhanden sind.

#### <a name="latitude"></a>Breitengrad

- `latitude`
- `lat`
- `latdd`
- `lat_dd`
- `latitude83`
- `latdecdeg`
- `y`
- `ycenter`
- `point-y`

#### <a name="longitude"></a>Längengrad

- `longitude`
- `lon`
- `lng`
- `long`
- `longdd`
- `long_dd`
- `longitude83`
- `longdecdeg`
- `x`
- `xcenter`
- `point-x`

#### <a name="elevation"></a>Elevation

- `elevation`
- `elv`
- `altitude`
- `alt`
- `z`

#### <a name="geography"></a>Gebiet

Die erste Datenzeile wird nach Zeichenfolgen im Well-Known-Text-Format durchsucht. 

### <a name="delimited-data-column-types"></a>Spaltentypen für durch Trennzeichen getrennte Daten

Bei der Überprüfung der Kopfzeile werden im Spaltennamen enthaltene Typinformationen extrahiert und zur Umwandlung der Zellen in dieser Spalte verwendet. Das folgende Beispiel zeigt einen Spaltennamen mit einem Typwert: „ColumnName (typeName)“. Die folgenden Namen werden unterstützt (ohne Berücksichtigung der Groß-/Kleinschreibung):

#### <a name="numbers"></a>Zahlen

- edm.int64
- INT
- long
- edm.double
- float
- double
- number

#### <a name="booleans"></a>Boolesche Werte

- edm.boolean
- bool
- boolean

#### <a name="dates"></a>Datumsangaben

- edm.datetime
- date
- datetime

#### <a name="geography"></a>Gebiet

- edm.geography
- geography

#### <a name="strings"></a>Zeichenfolgen

- edm.string
- varchar
- text
- Zeichenfolge

Falls keine Typinformationen aus der Kopfzeile extrahiert werden können und beim Lesen die Option für die dynamische Typzuweisung aktiviert ist, wird jede Zelle einzeln analysiert, um zu bestimmen, welcher Datentyp am besten für die Umwandlung geeignet ist.

## <a name="next-steps"></a>Nächste Schritte

In den folgenden Artikeln finden Sie weitere Codebeispiele, die Sie Ihren Karten hinzufügen können:

> [!div class="nextstepaction"]
> [Lesen und Schreiben von räumlichen Daten](spatial-io-read-write-spatial-data.md)
