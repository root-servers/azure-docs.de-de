---
title: 'Auszahlungsrichtliniendetails: Azure Marketplace'
description: Details zu Auszahlungsrichtlinien, einschließlich Zeitplänen und Entschädigung.
ms.service: marketplace
ms.subservice: partnercenter-marketplace-publisher
ms.topic: conceptual
author: mingshen-ms
ms.author: mingshen
ms.date: 04/24/2020
ms.openlocfilehash: 801d3ca383ebde75d6590558638df6820e538249
ms.sourcegitcommit: 3d56d25d9cf9d3d42600db3e9364a5730e80fa4a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87529942"
---
# <a name="payout-policy-details"></a>Auszahlungsrichtliniendetails

In diesem Artikel werden der Auszahlungsprozess von Microsoft, der Auszahlungszeitplan und die Entschädigungsrichtlinie erläutert, und Sie erfahren, wo Sie den Status einer Auszahlung finden.

## <a name="where-to-find-upcoming-payouts"></a>Ort für bevorstehende Auszahlungen

Wählen Sie in Partner Center die Option **Auszahlung** in der rechten oberen Ecke des Bildschirms aus:

![Auszahlungssymbol rechts oben im Partner Center-Portal](./media/payout-overview.png)

> [!TIP]
> Nicht alle Kontorollen haben Zugriff auf Auszahlungsinformationen. Ausführliche Informationen zu Rollen und Berechtigungen für den Zugriff auf den Auszahlungsbericht finden Sie [hier](./payout-summary-overview.md#roles-and-permissions).

## <a name="payment-schedules"></a>Zahlungspläne

In den folgenden Abschnitten wird der Prozess für Auszahlungen beschrieben.

### <a name="enterprise-agreement-transactions-after-may-1-2020"></a>Enterprise Agreement-Transaktionen nach dem 1. Mai 2020

#### <a name="update-to-our-commercial-marketplace-publisher-payout-model"></a>Aktualisierung unseres Auszahlungsmodells für Herausgeber im kommerziellen Marketplace

Ab dem 1. Mai 2020 aktualisieren wir unsere Auszahlungsrichtlinie für Produkte, die von Kunden mit einem Microsoft Enterprise Agreement im Azure Marketplace oder in AppSource erworben werden. Wenn ein Kunde ein Produkt im Azure Marketplace oder in AppSource erwirbt und dabei sein vorhandenes Microsoft Enterprise Agreement verwendet, werden Auszahlungen für Transaktionen nach dem 1. Mai 2020 im nächsten Auszahlungszyklus 30 Tage nach der Kundenrechnung geleistet. Für Transaktionen, bei denen der Kunde eine Kreditkarte verwendet, gilt unverändert ein Einbehaltungszeitraum von 30 Tagen vor der Auszahlung. Die folgende Tabelle enthält Details zum Auszahlungszeitplan.

> [!NOTE]
> Unter [Prozess bei Nichtzahlung des Kunden](#process-for-customer-non-payment) erfahren Sie, welche Maßnahmen wir ergreifen, wenn der Kunde nicht bezahlt und wir bereits eine Auszahlung an Sie geleistet haben.

| Ereignis  | Datum (UTC) | Partnersichtbarkeit: Partner Center-Auszahlungsbericht  |  Partnersichtbarkeit: Partner Center-Analysen\* |
| --- | --- | --- | --- |
| Transaktion oder Nutzungsmonat | 01.08.2020–31.08.2020 | – | **Nutzungsbericht**: Anzeige des neuen Verbrauchs (wird alle vier Stunden aktualisiert)<br>**Auftragsbericht**: – |
| Laufzeitende (Monat) | 31.08.2020 | – | **Nutzungsbericht**: Anzeige des Verbrauchs am Monatsende<br>**Auftragsbericht**: – |
| Auftragsgenerierung | 03.09.2020–07.09.2020 | – | **Nutzungsbericht**: Anzeige des Verbrauchs mit Auftrags-ID/Auftragspositions-ID (OrderID/OrderLineItemID)<br>**Auftragsbericht**: Anzeige AKTIVER Kundenaufträge |
| Berechnung der erzielten Auszahlung | 04.09.2020–10.09.2020 | Kennzeichnung als **Nicht verarbeitet** im Transaktionsverlauf des Auszahlungsdashboards | **Nutzungsbericht**: Anzeige des Verbrauchs mit Auftrags-ID/Auftragspositions-ID (OrderID/OrderLineItemID)<br>**Auftragsbericht**: Anzeige AKTIVER Kundenaufträge |
| Monatliche Auszahlung | 10.05.2020 | Kennzeichnung als **Anstehend** im Transaktionsverlauf des Auszahlungsdashboards | **Nutzungsbericht**: Anzeige des Verbrauchs mit Auftrags-ID/Auftragspositions-ID (OrderID/OrderLineItemID)<br>**Auftragsbericht**: Anzeige AKTIVER Kundenaufträge |
| Auszahlungsdatum\** | 15.10.2020 | Kennzeichnung als **Gesendet** im Transaktionsverlauf und im Auszahlungsabschnitt des Auszahlungsdashboards | **Nutzungsbericht**: Anzeige des Verbrauchs mit Auftrags-ID/Auftragspositions-ID (OrderID/OrderLineItemID)<br>**Auftragsbericht**: Anzeige AKTIVER Kundenaufträge |
| Begleichung der Kundenrechnung | 01.12.2020 | Kennzeichnung als **Gesendet** im Transaktionsverlauf und im Auszahlungsabschnitt des Auszahlungsdashboards | **Nutzungsbericht**: Anzeige des Verbrauchs mit Auftrags-ID/Auftragspositions-ID (OrderID/OrderLineItemID)<br>**Auftragsbericht**: Anzeige AKTIVER Kundenaufträge  |
|  |  |  |  |

\* Auf Nutzungs- und Auftragsberichte kann im Analyseabschnitt in Partner Center zugegriffen werden.</br>\** Das Auszahlungsdatum ist in Pacific Standard Time (PST) angegeben.

### <a name="customers-who-pay-using-credit-card-or-invoice"></a>Kunden mit Kreditkarten- oder Rechnungszahlung

Für alle Käufe mit Kreditkarte oder monatlicher Rechnung gilt ein Einbehaltungszeitraum von 30 Tagen, um sicherzustellen, dass die Zahlung tatsächlich erfolgt und es zu keinen Rückbuchungen oder möglichen Betrugsfällen kommt.

| Ereignis  | Datum (UTC) | Partnersichtbarkeit: Partner Center-Auszahlungsbericht  |  Partnersichtbarkeit: Partner Center-Analysen\*  |
| --- | --- | --- | --- |
| Transaktion oder Nutzungsmonat | 01.08.2019–31.08.2019 | – | **Nutzungsbericht**: Anzeige des neuen Verbrauchs (wird alle vier Stunden aktualisiert)<br>**Auftragsbericht**: – |
| Laufzeitende (Monat) | 31.08.2019 | – | **Nutzungsbericht**: Anzeige des Verbrauchs am Monatsende<br>**Auftragsbericht**: – |
| Auftragsgenerierung | 03.09.2019–07.09.2019 | – | **Nutzungsbericht**: Anzeige des Verbrauchs mit Auftrags-ID/Auftragspositions-ID (OrderID/OrderLineItemID)<br>**Auftragsbericht**: Anzeige AKTIVER Kundenaufträge |
| Begleichung der Kundenrechnung | 07.09.2019–10.09.2019 | – | **Nutzungsbericht**: Anzeige des Verbrauchs mit Auftrags-ID/Auftragspositions-ID (OrderID/OrderLineItemID)<br>**Auftragsbericht**: Anzeige AKTIVER Kundenaufträge |
| Berechnung der Auszahlung | 08.09.2019–12.09.2019 | Kennzeichnung als **Nicht verarbeitet** im Transaktionsverlauf des Auszahlungsdashboards | **Nutzungsbericht**: Anzeige des Verbrauchs mit Auftrags-ID/Auftragspositions-ID (OrderID/OrderLineItemID)<br>**Auftragsbericht**: Anzeige AKTIVER Kundenaufträge |
| Monatliche Auszahlung | 05.11.2019\* | Kennzeichnung als **Anstehend** im Transaktionsverlauf des Auszahlungsdashboards | **Nutzungsbericht**: Anzeige des Verbrauchs mit Auftrags-ID/Auftragspositions-ID (OrderID/OrderLineItemID)<br>**Auftragsbericht**: Anzeige AKTIVER Kundenaufträge |
| Auszahlungsdatum\** | 15.11.2019 | Kennzeichnung als **Gesendet** im Transaktionsverlauf und im Auszahlungsabschnitt des Auszahlungsdashboards | **Nutzungsbericht**: Anzeige des Verbrauchs mit Auftrags-ID/Auftragspositions-ID (OrderID/OrderLineItemID)<br>**Auftragsbericht**: Anzeige AKTIVER Kundenaufträge |
|  |  |  |  |

\* Auf Nutzungs- und Auftragsberichte kann im Analyseabschnitt in Partner Center zugegriffen werden.</br>\** Das Auszahlungsdatum ist in Pacific Standard Time (PST) angegeben.

### <a name="enterprise-agreement-transactions-prior-to-may-1-2020"></a>Enterprise Agreement-Transaktionen vor dem 1. Mai 2020

Alle Käufe vor diesem Datum werden gemäß dem folgenden Zeitplan verarbeitet und bezahlt, nachdem Microsoft die Zahlung von Kunden erhalten und die Marketplace-Gebühr verarbeitet hat.

| Ereignis  | Datum (UTC)  | Partnersichtbarkeit: Partner Center-Auszahlungsbericht  |  Partnersichtbarkeit: Partner Center-Analysen\*  |
| --- | --- | --- | --- |
| Transaktion oder Nutzungsmonat | 01.08.2019–31.08.2019 | – | **Nutzungsbericht**: Anzeige des neuen Verbrauchs (wird alle vier Stunden aktualisiert)<br>**Auftragsbericht**: – |
| Laufzeitende (Monat) | 31.08.2019 | – | **Nutzungsbericht**: Anzeige des Verbrauchs am Monatsende<br>**Auftragsbericht**: – |
| Auftragsgenerierung | 03.09.2019–07.09.2019 | – | **Nutzungsbericht**: Anzeige des Verbrauchs mit Auftrags-ID/Auftragspositions-ID (OrderID/OrderLineItemID)<br>**Auftragsbericht**: Anzeige AKTIVER Kundenaufträge |
| Begleichung der Kundenrechnung | 01.12.2019 | – | **Nutzungsbericht**: Anzeige des Verbrauchs mit Auftrags-ID/Auftragspositions-ID (OrderID/OrderLineItemID)<br>**Auftragsbericht**: Anzeige AKTIVER Kundenaufträge |
| Berechnung der Auszahlung | 05.12.2019–07.12.2019 | Kennzeichnung als **Nicht verarbeitet** im Transaktionsverlauf des Auszahlungsdashboards | **Nutzungsbericht**: Anzeige des Verbrauchs mit Auftrags-ID/Auftragspositions-ID (OrderID/OrderLineItemID)<br>**Auftragsbericht**: Anzeige AKTIVER Kundenaufträge |
| Monatliche Auszahlung | 05.01.2019 | Kennzeichnung als **Anstehend** im Transaktionsverlauf des Auszahlungsdashboards | **Nutzungsbericht**: Anzeige des Verbrauchs mit Auftrags-ID/Auftragspositions-ID (OrderID/OrderLineItemID)<br>**Auftragsbericht**: Anzeige AKTIVER Kundenaufträge |
| Auszahlungsdatum\** | 15.01.2019 | Kennzeichnung als **Gesendet** im Transaktionsverlauf und im Auszahlungsabschnitt des Auszahlungsdashboards | **Nutzungsbericht**: Anzeige des Verbrauchs mit Auftrags-ID/Auftragspositions-ID (OrderID/OrderLineItemID)<br>**Auftragsbericht**: Anzeige AKTIVER Kundenaufträge |
|  |  |  |  |

\* Auf Nutzungs- und Auftragsberichte kann im Analyseabschnitt in Partner Center zugegriffen werden.</br>\** Das Auszahlungsdatum ist in Pacific Standard Time (PST) angegeben.

## <a name="process-for-customer-non-payment"></a>Prozess bei Nichtzahlung des Kunden

In seltenen Fällen gelingt es Microsoft nicht, Kundenzahlungen für Käufe im kommerziellen Marketplace einzuziehen. Sollte ein Kunde seiner Zahlungsverpflichtung gegenüber Microsoft nicht gemäß dem entsprechenden Abrechnungszeitplan nachkommen, beginnt der Inkassoprozess. Dieser dauert ungefähr vier Monate und beinhaltet eine beharrliche Kommunikation durch Microsoft. Sollte die Zahlung bis zum Ende dieses Prozesses nicht eingehen, schreibt Microsoft den Betrag als uneinbringlich ab.

Aufgrund des hier beschriebenen Auszahlungsprozesses wurden von Microsoft unter Umständen bereits Zahlungen an Herausgeber (Sie) geleistet, die letztendlich uneinbringlich sind. Für Beträge dieser Art gibt es daher einen Ausgleichsprozess. Wenn der Inkassoprozess für einen Kunden gestartet wurde und die Käufe voraussichtlich abgeschrieben werden müssen, erhalten Sie eine entsprechende Benachrichtigung, um Sie darüber zu informieren, dass Ihre (bereits erhaltene) Zahlung unter Umständen ausgeglichen werden muss.

Microsoft verwendet eine der folgenden Methoden, um bereits an Sie geleistete Zahlungen zurückzuerhalten: (1) Microsoft kann die unbezahlten Beträge mit zukünftigen Auszahlungen verrechnen. Wenn also beispielsweise Auszahlungen in Höhe von 1.000 USD als uneinbringlich eingestuft und abgeschrieben werden, werden Ihre zukünftigen Auszahlungen so lange zurückgehalten, bis die 1.000 USD ausgeglichen sind. (2) Alternativ kann Microsoft von Herausgebern eine Rückerstattung für nicht geleistete Zahlungen verlangen oder ihnen den entsprechenden Betrag in Rechnung stellen.

Im Anschluss finden Sie einen Beispielzeitplan:

| Ereignis | Ungefähres Datum | Partnersichtbarkeit |
| --- | --- | --- |
| Exemplarisches Auszahlungsdatum | 15.10.2020 | Kennzeichnung als **Gesendet** im Transaktionsverlauf und im Auszahlungsabschnitt des Auszahlungsdashboards |
| <font color="red">Ausbleibende Kundenzahlung an Microsoft</font> | 02.12.2020–05.12.2020 | Keine Änderung, wie oben |
| Kunde erhält erste E-Mail wegen Zahlungsverzug | 06.12.2020 | Keine |
| Kunde erhält regelmäßig E-Mails mit zunehmender Dringlichkeit | 07.12.2020–31.01.2021 | Keine |
| Herausgeber wird über voraussichtliche Abschreibung informiert | 07.01.2021 | Herausgeber erhält eine E-Mail-Benachrichtigung mit der Information, dass der Kunde noch nicht bezahlt hat. Transaktions-ID und Dollarbetrag sind angegeben. |
| Kunde erhält Kündigungsbenachrichtigung | 01.02.2021 | Keine |
| Inkassoprozess endet/Betrag wird abgeschrieben | 15.02.2021 | Herausgeber erhält eine E-Mail-Benachrichtigung mit der Information, dass der Betrag abgeschrieben wurde. Transaktions-ID und Dollarbetrag sind angegeben. |
| Auszahlung wird abgezogen | 01.03.2021 | Partner Center-Auszahlungsauszug des Herausgebers enthält negative Transaktion |
| Auszahlung wird einbehalten | 15.03.2021 | Partner Center-Auszahlungsauszug enthält zukünftige Auszahlungen. Zahlungen an den Herausgeber werden erst wieder geleistet, wenn der Saldo nicht mehr negativ ist.  |
|||

## <a name="number-of-days-for-payments-to-reach-a-payout-account"></a>Anzahl der Tage bis zum Eingang von Zahlungen auf einem Auszahlungskonto

In der Regel senden wir die in einem Monat fälligen Zahlungen am 15. des Monats, es dauert jedoch einige Zeit, bis die Zahlung auf Ihrem Konto eingeht. Die Anzahl der Tage hängt von der Zahlungsmethode ab, die wir für Ihr Konto verwenden (siehe weiter unten).

> [!NOTE]
> Die unten gezeigten Tage sind ungefähre Angaben. Es kann länger oder kürzer dauern, bis eine Auszahlung auf Ihrem Konto eingeht.

| Payment Method     | Anzahl der Tage bis zum Eingang auf dem Auszahlungskonto     |
|--------------------|--------------------------------------------|
| PayPal             | 1 Werktag                             |
| ACH/SEPA-Überweisungen           | 2-3 Werktage                          |
| Telegrafische Geldüberweisung      | 7-10 Werktage                         |

## <a name="next-step"></a>Nächster Schritt

- [Steuerliche Aspekte für kommerzielle Marketplace-Herausgeber](./tax-details-paid-transactions.md)
