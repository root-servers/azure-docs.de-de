---
title: Standardbenutzerberechtigungen – Azure Active Directory | Microsoft-Dokumentation
description: Erfahren Sie, welche verschiedenen Benutzerberechtigungen in Azure Active Directory verfügbar sind.
services: active-directory
author: ajburnle
manager: daveba
ms.service: active-directory
ms.subservice: fundamentals
ms.workload: identity
ms.topic: conceptual
ms.date: 08/17/2020
ms.author: ajburnle
ms.reviewer: vincesm
ms.custom: it-pro, seodec18, contperfq1
ms.collection: M365-identity-device-management
ms.openlocfilehash: f96d307f8cc5aa248ffe3bc7c6b0d569ac0910ea
ms.sourcegitcommit: 5ed504a9ddfbd69d4f2d256ec431e634eb38813e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/02/2020
ms.locfileid: "89320833"
---
# <a name="what-are-the-default-user-permissions-in-azure-active-directory"></a>Welche Standardbenutzerberechtigungen gibt es in Azure Active Directory?
In Azure Active Directory (Azure AD) wird allen Benutzern ein Satz mit Standardberechtigungen gewährt. Der Zugriffsumfang eines Benutzers basiert auf dem Benutzertyp, den [Rollenzuweisungen](active-directory-users-assign-role-azure-portal.md) und dem Besitz einzelner Objekte. In diesem Artikel werden diese Standardberechtigungen beschrieben, und es werden die Standardberechtigungen für Mitglieder und Gastbenutzer miteinander verglichen. Die Standardberechtigungen für Benutzer können nur in den Benutzereinstellungen in Azure AD geändert werden.

## <a name="member-and-guest-users"></a>Mitglieder und Gastbenutzer
Der gewährte Satz an Standardberechtigungen richtet sich danach, ob der Benutzer ein natives Mitglied des Mandanten ist (Mitgliedsbenutzer), oder ob der Benutzer als Gast im Rahmen der B2B-Zusammenarbeit (Gastbenutzer) aus einem anderen Verzeichnis übernommen wurde. Weitere Informationen zum Hinzufügen von Gastbenutzern finden Sie unter [Was ist die Azure AD B2B-Zusammenarbeit?](../external-identities/what-is-b2b.md).
* Mitgliedsbenutzer können Anwendungen registrieren, ihr eigenes Profilfoto und ihre Mobiltelefonnummer verwalten, das eigene Kennwort verwalten und B2B-Gäste einladen. Zusätzlich können die Benutzer (mit einigen Ausnahmen) alle Verzeichnisinformationen lesen. 
* Gastbenutzer erhalten eingeschränkte Verzeichnisberechtigungen. Sie können ihr eigenes Profil verwalten, ihr eigenes Kennwort ändern und einige Informationen über andere Benutzer, Gruppen und Apps abrufen, jedoch nicht alle Verzeichnisinformationen lesen. Gastbenutzer können beispielsweise Benutzer, Gruppen und andere Verzeichnisobjekte nicht auflisten. Gäste können zu Administratorrollen hinzugefügt werden, wodurch ihnen alle in der Rolle enthaltenen Lese- und Schreibberechtigungen gewährt werden. Gäste können auch andere Gäste einladen.

## <a name="compare-member-and-guest-default-permissions"></a>Vergleich der Standardberechtigungen für Mitglieds- und Gastbenutzer

**Bereich** | **Berechtigungen für Mitgliedsbenutzer** | **Standardberechtigungen für Gastbenutzer** | **Eingeschränkte Berechtigungen für Gastbenutzer (Vorschau)**
------------ | --------- | ---------- | ----------
Benutzer und Kontakte | <ul><li>Alle öffentlichen Eigenschaften von Benutzern und Kontakten lesen</li><li>Gäste einladen<li>Eigenes Kennwort ändern<li>Eigene Mobiltelefonnummer verwalten<li>Eigenes Foto verwalten<li>Eigene Aktualisierungstoken für ungültig erklären</li></ul> | <ul><li>Eigene Eigenschaften lesen<li>Eigenschaften für Anzeigename, E-Mail-Adresse, Anmeldename, Foto, Benutzerprinzipalname und Benutzertyp anderer Benutzer und Kontakte lesen<li>Eigenes Kennwort ändern<li>Nach einem anderen Benutzer nach Anzeigename, Benutzerprinzipalname oder objectId (falls zulässig) suchen<li>Manager- und direkte Berichtsinformationen anderer Benutzer lesen</li></ul> | <ul><li>Eigene Eigenschaften lesen<li>Eigenes Kennwort ändern</li></ul>
Gruppen | <ul><li>Sicherheitsgruppen erstellen<li>Office 365-Gruppen erstellen<li>Alle Eigenschaften von Gruppen lesen<li>Nicht ausgeblendete Gruppenmitgliedschaften lesen<li>Ausgeblendete Office 365-Gruppenmitgliedschaften für eingebundene Gruppe lesen<li>Eigenschaften, Besitz und Mitgliedschaft von Gruppen im Besitz des Benutzers verwalten<li>Gäste zu Gruppen im Besitz des Benutzers hinzufügen<li>Einstellungen für dynamische Mitgliedschaften verwalten<li>Gruppen im Besitz des Benutzers löschen<li>Office 365-Gruppen im Besitz des Benutzers wiederherstellen</li></ul> | <ul><li>Eigenschaften aller nicht ausgeblendeten Gruppen lesen, einschließlich Mitgliedschaft und Besitz (auch nicht eingebundene Gruppen)<li>Ausgeblendete Office 365-Gruppenmitgliedschaften für eingebundene Gruppen lesen<li>Gruppen nach Anzeigename oder objectId (falls zulässig) suchen</li></ul> | Keine Berechtigungen
Anwendungen | <ul><li>Neue Anwendung registrieren (erstellen)<li>Eigenschaften für registrierte Anwendungen und Unternehmensanwendungen lesen<li>Anwendungseigenschaften, Zuweisungen und Anmeldeinformationen für Anwendungen im Besitz des Benutzers verwalten<li>Anwendungskennwort für Benutzer erstellen oder löschen<li>Anwendungen im Besitz des Benutzers löschen<li>Anwendungen im Besitz des Benutzers wiederherstellen</li></ul> | <ul><li>Eigenschaften für registrierte Anwendungen und Unternehmensanwendungen lesen</li></ul> | <ul><li>Eigenschaften für registrierte Anwendungen und Unternehmensanwendungen lesen
Geräte</li></ul> | <ul><li>Alle Eigenschaften von Geräten lesen<li>Alle Eigenschaften von Geräten im Besitz des Benutzers verwalten</li></ul> | Keine Berechtigungen | Keine Berechtigungen
Verzeichnis | <ul><li>Alle Unternehmensinformationen lesen<li>Alle Domänen lesen<li>Alle Partnerverträge lesen</li></ul> | <ul><li>Anzeigenamen und überprüfte Domänen lesen</li></ul> | <ul><li>Anzeigenamen und überprüfte Domänen lesen</li></ul>
Rollen und Bereiche | <ul><li>Alle administrativen Rollen und Mitgliedschaften lesen<li>Alle Eigenschaften und Mitgliedschaften von administrativen Einheiten lesen</li></ul> | Keine Berechtigungen | Keine Berechtigungen
Abonnements | <ul><li>Alle Abonnements lesen<li>Mitglied für Diensttarif aktivieren</li></ul> | Keine Berechtigungen | Keine Berechtigungen
Richtlinien | <ul><li>Alle Eigenschaften von Richtlinien lesen<li>Alle Eigenschaften von Richtlinien im Besitz des Benutzers verwalten</li></ul> | Keine Berechtigungen | Keine Berechtigungen

## <a name="to-restrict-the-default-permissions-for-member-users"></a>Einschränken der Standardberechtigungen für Mitgliedsbenutzer

Die Standardberechtigungen für Mitgliedsbenutzer können auf folgende Weise eingeschränkt werden:

Berechtigung | Erläuterung der Einstellung
---------- | ------------
Benutzer können Anwendungen registrieren | Durch das Festlegen dieser Einstellung auf „Nein“ werden Benutzer daran gehindert, Anwendungsregistrierungen zu erstellen. Die Fähigkeit kann anschließend bestimmten Personen wieder gewährt werden, indem diese der Rolle „Anwendungsentwickler“ hinzugefügt werden.
Benutzern die Verbindungsherstellung mit LinkedIn über ihr Geschäfts-, Schul- oder Unikonto erlauben | Durch das Festlegen dieser Einstellung auf „Nein“ werden Benutzer daran gehindert, ihr Geschäfts-, Schul- oder Unikonto mit ihrem LinkedIn-Konto zu verbinden. Weitere Informationen finden Sie unter [Datenfreigabe und Benutzereinwilligung bei LinkedIn-Kontoverbindungen](../users-groups-roles/linkedin-user-consent.md).
Fähigkeit zum Erstellen von Sicherheitsgruppen | Durch das Festlegen dieser Einstellung auf „Nein“ werden Benutzer daran gehindert, Sicherheitsgruppen zu erstellen. Globale Administratoren und Benutzeradministratoren können weiterhin Sicherheitsgruppen erstellen. Informationen zur Vorgehensweise finden Sie unter [Azure Active Directory-Cmdlets zum Konfigurieren von Gruppeneinstellungen](../users-groups-roles/groups-settings-cmdlets.md).
Fähigkeit zum Erstellen von Office 365-Gruppen | Durch das Festlegen dieser Einstellung auf „Nein“ werden Benutzer daran gehindert, Office 365-Gruppen zu erstellen. Durch das Festlegen dieser Option auf „Einige“ wird einem ausgewählten Benutzersatz das Erstellen von Office 365-Gruppen ermöglicht. Globale Administratoren und Benutzeradministratoren können weiterhin Office 365-Gruppen erstellen. Informationen zur Vorgehensweise finden Sie unter [Azure Active Directory-Cmdlets zum Konfigurieren von Gruppeneinstellungen](../users-groups-roles/groups-settings-cmdlets.md).
Zugriff auf Azure AD-Verwaltungsportal einschränken | Wenn Sie diese Option auf „Nein“ festlegen, können Nichtadministratoren das Azure AD-Verwaltungsportal zum Lesen und Verwalten von Ressourcen verwenden. Mit der Einstellung „Ja“ wird der Zugriff auf Azure AD-Daten im Verwaltungsportal für Nichtadministratoren eingeschränkt.<p>**Hinweis**: Durch diese Einstellung wird der Zugriff auf Azure AD-Daten mithilfe von PowerShell oder anderen Clients wie Visual Studio nicht eingeschränkt. Wenn diese Einstellung auf „Ja“ festgelegt ist, kann einem bestimmten Benutzer, der kein Administrator ist, die Fähigkeit erteilt werden, das Azure AD-Verwaltungsportal zu verwenden, indem ihm eine beliebige Administratorrolle zugewiesen wird, z. B. die Rolle „Verzeichnisleseberechtigte“.<p>Diese Rolle ermöglicht das Lesen grundlegender Verzeichnisinformationen und ist den Mitgliedsbenutzern (nicht aber Gästen und Dienstprinzipalen) standardmäßig zugewiesen.
Fähigkeit zum Lesen anderer Benutzer | Diese Einstellung ist nur in PowerShell verfügbar. Das Festlegen dieses Flags auf „$false“ verhindert, dass Nicht-Administratoren Benutzerinformationen aus dem Verzeichnis lesen können. Durch dieses Flag wird jedoch nicht verhindert, dass Benutzerinformationen in anderen Microsoft-Diensten wie z. B. Exchange Online gelesen werden können. Diese Einstellung ist für besondere Umstände bestimmt – die Festlegung dieses Flags auf „$false“ wird nicht empfohlen.


## <a name="to-restrict-the-default-permissions-for-guest-users"></a>Einschränken der Standardberechtigungen für Gastbenutzer

Die Standardberechtigungen für Gastbenutzer können auf folgende Weise eingeschränkt werden:

>[!NOTE] 
>Die Einstellung **Berechtigungen für Gastbenutzer sind eingeschränkt** wurde durch die Einstellung für Zugriffseinschränkungen für Gastbenutzer ersetzt. Anleitungen zur Verwendung dieser Funktion finden Sie unter [Einschränken von Gastzugriffsberechtigungen (Vorschau) in Azure Active Directory](../users-groups-roles/users-restrict-guest-permissions.md).

Berechtigung | Erläuterung der Einstellung
---------- | ------------
Zugriffseinschränkungen für Gastbenutzer (Vorschau) | Wenn diese Option auf „Gastbenutzer haben denselben Zugriff wie Mitglieder“ festgelegt wird, werden Gastbenutzern standardmäßig alle Benutzerberechtigungen von Mitgliedern gewährt.<p>Wird diese Option auf „Der Gastbenutzerzugriff ist auf Eigenschaften und Mitgliedschaften eigener Verzeichnisobjekte beschränkt“ festgelegt, ist der Gastzugriff standardmäßig auf das eigene Benutzerprofil beschränkt. Der Zugriff auf andere Benutzer ist auch bei der Suche nach Benutzerprinzipalname oder objectId nicht mehr zulässig. Der Zugriff auf Gruppen einschließlich Gruppenmitgliedschaften ist ebenfalls nicht mehr zulässig. Diese Einstellung verhindert nicht den Zugriff auf Gruppen in anderen Microsoft-Diensten wie z. B. Microsoft Teams. Weitere Informationen finden Sie unter [Gastzugriff auf Microsoft Teams]().<p>Gastbenutzer können unabhängig von diesen Berechtigungseinstellungen weiterhin Administratorrollen hinzugefügt werden.
Gäste können einladen | Wenn Sie diese Option auf „Ja“ festlegen, können Gäste andere Gäste einladen. Weitere Informationen finden Sie unter [Delegieren von Einladungen zur B2B-Zusammenarbeit](../external-identities/delegate-invitations.md#configure-b2b-external-collaboration-settings).
Mitglieder können einladen | Wenn Sie diese Option auf „Ja“ festlegen, können Mitglieder in Ihrem Verzeichnis, die keine Administratoren sind, Gäste einladen. Weitere Informationen finden Sie unter [Delegieren von Einladungen zur B2B-Zusammenarbeit](../external-identities/delegate-invitations.md#configure-b2b-external-collaboration-settings).
Administratoren und Benutzer mit der Rolle „Gasteinladender“ können einladen | Wenn Sie diese Option auf „Ja“ festlegen, können Administratoren und Benutzer, die der Rolle „Gasteinladender“ zugewiesen sind, Gäste einladen. Ist diese Option auf „Ja“ festgelegt, können Benutzer, die der Rolle „Gasteinladender“ zugewiesen sind, Gäste auch unabhängig davon einladen, was für die Einstellung „Mitglieder können einladen“ festgelegt ist. Weitere Informationen finden Sie unter [Delegieren von Einladungen zur B2B-Zusammenarbeit](../external-identities/delegate-invitations.md#assign-the-guest-inviter-role-to-a-user).

## <a name="object-ownership"></a>Objektbesitz

### <a name="application-registration-owner-permissions"></a>Berechtigungen als Anwendungsregistrierungsbesitzer
Wenn ein Benutzer eine Anwendung registriert, wird er automatisch als Besitzer für die Anwendung hinzugefügt. Als Besitzer kann der Benutzer die Metadaten der Anwendung verwalten, beispielsweise den Namen und Berechtigungen, die von der App anfordert werden. Darüber hinaus kann der Benutzer auch die mandantenspezifische Konfiguration der Anwendung verwalten, z.B. die SSO-Konfiguration und Benutzerzuweisungen. Ein Besitzer kann außerdem andere Besitzer hinzufügen oder entfernen. Im Gegensatz zu globalen Administratoren können Besitzer nur Anwendungen verwalten, deren Besitzer sie sind.

### <a name="enterprise-application-owner-permissions"></a>Besitzerberechtigungen für Unternehmensanwendungen
Wenn ein Benutzer eine neue Unternehmensanwendung hinzufügt, wird er automatisch als Besitzer hinzugefügt. Als Besitzer kann er die mandantenspezifische Konfiguration der Anwendung verwalten, z. B. die SSO-Konfiguration, die Bereitstellung und Benutzerzuweisungen. Ein Besitzer kann außerdem andere Besitzer hinzufügen oder entfernen. Im Gegensatz zu globalen Administratoren können Besitzer nur die Anwendungen verwalten, deren Besitzer sie sind.

### <a name="group-owner-permissions"></a>Berechtigungen als Gruppenbesitzer
Wenn ein Benutzer eine Gruppe erstellt, wird er automatisch als Besitzer für diese Gruppe hinzugefügt. Als Besitzer kann der Benutzer die Eigenschaften der Gruppe verwalten, beispielsweise den Namen und die Gruppenmitgliedschaft. Ein Besitzer kann außerdem andere Besitzer hinzufügen oder entfernen. Im Gegensatz zu globalen Administratoren und Benutzerdministratoren können Besitzer nur Gruppen verwalten, deren Besitzer sie sind. Informationen zum Zuweisen eines Gruppenbesitzers finden Sie unter [Verwalten von Besitzern für eine Gruppe](active-directory-accessmanagement-managing-group-owners.md).

### <a name="ownership-permissions"></a>Besitzerberechtigungen
In den folgenden Tabellen werden die spezifischen Berechtigungen in Azure Active Directory beschrieben, über die Mitgliedsbenutzer für Objekte in ihrem Besitz verfügen. Der Benutzer verfügt über diese Berechtigungen nur für Objekte, deren Besitzer er ist.

#### <a name="owned-application-registrations"></a>Anwendungsregistrierungen im Besitz des Benutzers
Benutzer können die folgenden Aktionen für Anwendungsregistrierungen ausführen, deren Besitzer sie sind.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/applications/audience/update | Aktualisieren der applications.audience-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/authentication/update | Aktualisieren der applications.authentication-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/basic/update | Aktualisieren der Basiseigenschaften für Anwendungen in Azure Active Directory |
| microsoft.directory/applications/credentials/update | Aktualisieren der applications.credentials-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/delete | Löschen von Anwendungen in Azure Active Directory |
| microsoft.directory/applications/owners/update | Aktualisieren der applications.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/permissions/update | Aktualisieren der applications.permissions-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/policies/update | Aktualisieren der applications.policies-Eigenschaft in Azure Active Directory |
| microsoft.directory/applications/restore | Wiederherstellen von Anwendungen in Azure Active Directory |

#### <a name="owned-enterprise-applications"></a>Unternehmensanwendungen im Besitz des Benutzers
Benutzer können die folgenden Aktionen für Unternehmensanwendungen ausführen, deren Besitzer sie sind. Eine Unternehmensanwendung besteht aus dem Dienstprinzipal, einer oder mehrerer Anwendungsrichtlinien und manchmal einem Anwendungsobjekt im gleichen Mandanten wie der Dienstprinzipal.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/auditLogs/allProperties/read | Lesen aller Eigenschaften (einschließlich der privilegierten Eigenschaften) für Überwachungsprotokolle (auditLogs) in Azure Active Directory |
| microsoft.directory/policies/basic/update | Aktualisieren der Basiseigenschaften für Richtlinien in Azure Active Directory |
| microsoft.directory/policies/delete | Löschen von Richtlinien in Azure Active Directory |
| microsoft.directory/policies/owners/update | Aktualisieren der policies.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/appRoleAssignedTo/update | Aktualisieren der servicePrincipals.appRoleAssignedTo-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/appRoleAssignments/update | Aktualisieren der users.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/audience/update | Aktualisieren der servicePrincipals.audience-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/authentication/update | Aktualisieren der servicePrincipals.authentication-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/basic/update | Aktualisieren der Basiseigenschaften für servicePrincipals in Azure Active Directory |
| microsoft.directory/servicePrincipals/credentials/update | Aktualisieren der servicePrincipals.credentials-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/delete | Löschen von servicePrincipals in Azure Active Directory |
| microsoft.directory/servicePrincipals/owners/update | Aktualisieren der servicePrincipals.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/permissions/update | Aktualisieren der servicePrincipals.permissions-Eigenschaft in Azure Active Directory |
| microsoft.directory/servicePrincipals/policies/update | Aktualisieren der servicePrincipals.policies-Eigenschaft in Azure Active Directory |
| microsoft.directory/signInReports/allProperties/read | Lesen aller Eigenschaften (einschließlich der privilegierten Eigenschaften) für Anmeldeberichte (signInReports) in Azure Active Directory |

#### <a name="owned-devices"></a>Geräte im Besitz des Benutzers
Benutzer können die folgenden Aktionen für Geräte ausführen, deren Besitzer sie sind.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/devices/bitLockerRecoveryKeys/read | Lesen der devices.bitLockerRecoveryKeys-Eigenschaft in Azure Active Directory |
| microsoft.directory/devices/disable | Deaktivieren von Geräten in Azure Active Directory |

#### <a name="owned-groups"></a>Gruppen im Besitz des Benutzers
Benutzer können die folgenden Aktionen für Gruppen ausführen, deren Besitzer sie sind.

| **Aktionen** | **Beschreibung** |
| --- | --- |
| microsoft.directory/groups/appRoleAssignments/update | Aktualisieren der groups.appRoleAssignments-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/basic/update | Aktualisieren der Basiseigenschaften für Gruppen in Azure Active Directory |
| microsoft.directory/groups/delete | Löschen von Gruppen in Azure Active Directory |
| microsoft.directory/groups/dynamicMembershipRule/update | Aktualisieren der groups.dynamicMembershipRule-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/members/update | Aktualisieren der groups.members-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/owners/update | Aktualisieren der groups.owners-Eigenschaft in Azure Active Directory |
| microsoft.directory/groups/restore | Wiederherstellen von Gruppen in Azure Active Directory |
| microsoft.directory/groups/settings/update | Aktualisieren der groups.settings-Eigenschaft in Azure Active Directory |

## <a name="next-steps"></a>Nächste Schritte

* Weitere Informationen zur Einstellung für Zugriffseinschränkungen für Gastbenutzer finden Sie unter [Einschränken von Gastzugriffsberechtigungen (Vorschau) in Azure Active Directory](../users-groups-roles/users-restrict-guest-permissions.md).
* Weitere Informationen zum Zuweisen von Azure AD-Administratorrollen finden Sie unter [Zuweisen eines Benutzers zu Administratorrollen in Azure Active Directory](active-directory-users-assign-role-azure-portal.md).
* Informationen dazu, wie der Zugriff auf Ressourcen in Microsoft Azure gesteuert wird, finden Sie unter [Grundlegendes zum Zugriff auf Ressourcen in Azure](../../role-based-access-control/rbac-and-directory-admin-roles.md)
* Weitere Informationen zur Beziehung zwischen Azure Active Directory und Ihrem Azure-Abonnement finden Sie unter [Beziehung zwischen Azure-Abonnements und Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)
* [Verwalten von Benutzern](add-users-azure-active-directory.md)