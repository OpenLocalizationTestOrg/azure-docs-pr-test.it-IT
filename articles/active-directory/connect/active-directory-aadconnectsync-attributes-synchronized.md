---
title: Attributi sincronizzati da Azure AD Connect | Documentazione Microsoft
description: Elenca gli attributi di hello che sono sincronizzati tooAzure Active Directory.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c2bb36e0-5205-454c-b9b6-f4990bcedf51
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 2fe5b944a7fc832f245631416c265fb82eedeb15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-attributes-synchronized-tooazure-active-directory"></a>Sincronizzazione di Azure AD Connect: attributi sincronizzati tooAzure Active Directory
In questo argomento sono elencati gli attributi di hello che vengono sincronizzati tramite la sincronizzazione di Azure AD Connect.  
Hello attributi vengono raggruppati in base hello correlato app di Azure AD.

## <a name="attributes-toosynchronize"></a>Attributi toosynchronize
È una domanda comune *hello elenco di attributi minimi toosynchronize*. valore predefinito di Hello e approccio consigliato è tookeep gli attributi predefiniti di hello in modo da un elenco indirizzi globale completo (elenco indirizzi globale) può essere costruito hello cloud e tooget tutte le funzionalità nei carichi di lavoro di Office 365. In alcuni casi, esistono alcuni attributi che l'organizzazione non desidera cloud sincronizzati toohello poiché questi attributi contengono riservati o informazioni personali (informazioni personali), come in questo esempio:  
![attributi non validi](./media/active-directory-aadconnectsync-attributes-synchronized/badextensionattribute.png)

In questo caso, iniziare con elenco hello di attributi in questo argomento e identificare gli attributi che contengono dati sensibili o informazioni personali e non possono essere sincronizzati. Deselezionare questi attributi durante l'installazione tramite [Filtro attributi e app di Azure AD](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering).

> [!WARNING]
> Quando la deselezione di attributi, si deve prestare attenzione e deselezionare solo tali toosynchronize assolutamente non possibili attributi. Deselezionando altri attributi si potrebbe influire negativamente sulle funzionalità.
>
>

## <a name="office-365-proplus"></a>Office 365 ProPlus
| Nome attributo | Utente | Commento |
| --- |:---:| --- |
| accountEnabled |X |Definisce se un account è abilitato. |
| cn |X | |
| displayName |X | |
| objectSID |X |Proprietà meccanica. Identificatore utente di Active Directory utilizzato toomaintain sincronizzazione tra Azure Active Directory e Active Directory. |
| pwdLastSet |X |Proprietà meccanica. Tooknow usato quando tooinvalidate già i token rilasciati. Usata sia dal servizio di sincronizzazione delle password che dalla federazione. |
| sourceAnchor |X |Proprietà meccanica. Relazione di toomaintain identificatore non modificabile compreso tra ADDS e Azure AD. |
| usageLocation |X |Proprietà meccanica. paese dell'utente Hello. Usato per l'assegnazione delle licenze. |
| userPrincipalName |X |Nome UPN è hello ID di accesso per utente hello. Hello spesso corrisponde al valore [posta elettronica]. |

## <a name="exchange-online"></a>Exchange Online
| Nome attributo | Utente | Contatto | Gruppo | Commento |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Definisce se un account è abilitato. |
| assistant |X |X | | |
| altRecipient |X | | |Richiede la build 1.1.552.0 o successiva di Azure AD Connect. |
| authOrig |X |X |X | |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| countryCode |X |X | | |
| department |X |X | | |
| description |X |X |X | |
| displayName |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| homePhone |X |X | | |
| info |X |X |X |Questo attributo non viene attualmente utilizzato per i gruppi. |
| Initials |X |X | | |
| l |X |X | | |
| legacyExchangeDN |X |X |X | |
| mailNickname |X |X |X | |
| mangedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| mobile |X |X | | |
| msDS-HABSeniorityIndex |X |X |X | |
| msDS-PhoneticDisplayName |X |X |X | |
| msExchArchiveGUID |X | | | |
| msExchArchiveName |X | | | |
| msExchAssistantName |X |X | | |
| msExchAuditAdmin |X | | | |
| msExchAuditDelegate |X | | | |
| msExchAuditDelegateAdmin |X | | | |
| msExchAuditOwner |X | | | |
| msExchBlockedSendersHash |X |X | | |
| msExchBypassAudit |X | | | |
| msExchBypassModerationLink | | |X |Disponibile in Azure AD Connect versione 1.1.524.0 |
| msExchCoManagedByLink | | |X | |
| msExchDelegateListLink |X | | | |
| msExchELCExpirySuspensionEnd |X | | | |
| msExchELCExpirySuspensionStart |X | | | |
| msExchELCMailboxFlags |X | | | |
| msExchEnableModeration |X | |X | |
| msExchExtensionCustomAttribute1 |X |X |X |Questo attributo non viene attualmente utilizzato da Exchange Online. |
| msExchExtensionCustomAttribute2 |X |X |X |Questo attributo non viene attualmente utilizzato da Exchange Online. |
| msExchExtensionCustomAttribute3 |X |X |X |Questo attributo non viene attualmente utilizzato da Exchange Online. |
| msExchExtensionCustomAttribute4 |X |X |X |Questo attributo non viene attualmente utilizzato da Exchange Online. |
| msExchExtensionCustomAttribute5 |X |X |X |Questo attributo non viene attualmente utilizzato da Exchange Online. |
| msExchHideFromAddressLists |X |X |X | |
| msExchImmutableID |X | | | |
| msExchLitigationHoldDate |X |X |X | |
| msExchLitigationHoldOwner |X |X |X | |
| msExchMailboxAuditEnable |X | | | |
| msExchMailboxAuditLogAgeLimit |X | | | |
| msExchMailboxGuid |X | | | |
| msExchModeratedByLink |X |X |X | |
| msExchModerationFlags |X |X |X | |
| msExchRecipientDisplayType |X |X |X | |
| msExchRecipientTypeDetails |X |X |X | |
| msExchRemoteRecipientType |X | | | |
| msExchRequireAuthToSendTo |X |X |X | |
| msExchResourceCapacity |X | | | |
| msExchResourceDisplay |X | | | |
| msExchResourceMetaData |X | | | |
| msExchResourceSearchProperties |X | | | |
| msExchRetentionComment |X |X |X | |
| msExchRetentionURL |X |X |X | |
| msExchSafeRecipientsHash |X |X | | |
| msExchSafeSendersHash |X |X | | |
| msExchSenderHintTranslations |X |X |X | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| msExchUserHoldPolicies |X | | | |
| msOrg-IsOrganizational | | |X | |
| objectSID |X | |X |Proprietà meccanica. Identificatore utente di Active Directory utilizzato toomaintain sincronizzazione tra Azure Active Directory e Active Directory. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherTelephone |X |X | | |
| pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| proxyAddresses |X |X |X | |
| publicDelegates |X |X |X | |
| pwdLastSet |X | | |Proprietà meccanica. Tooknow usato quando tooinvalidate già i token rilasciati. Usata sia dal servizio di sincronizzazione delle password che dalla federazione. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityEnabled | | |X |Derivato da groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |Proprietà meccanica. Relazione di toomaintain identificatore non modificabile compreso tra ADDS e Azure AD. |
| st |X |X | | |
| streetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| title |X |X | | |
| unauthOrig |X |X |X | |
| usageLocation |X | | |Proprietà meccanica. paese dell'utente Hello. Usato per l'assegnazione delle licenze. |
| userCertificate |X |X | | |
| userPrincipalName |X | | |Nome UPN è hello ID di accesso per utente hello. Hello spesso corrisponde al valore [posta elettronica]. |
| userSMIMECertificates |X |X | | |
| wWWHomePage |X |X | | |

## <a name="sharepoint-online"></a>SharePoint Online
| Nome attributo | Utente | Contatto | Gruppo | Commento |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Definisce se un account è abilitato. |
| authOrig |X |X |X | |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| countryCode |X |X | | |
| department |X |X | | |
| description |X |X |X | |
| displayName |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| hideDLMembership | | |X | |
| homePhone |X |X | | |
| info |X |X |X | |
| Initials |X |X | | |
| ipPhone |X |X | | |
| l |X |X | | |
| mail |X |X |X | |
| mailNickname |X |X |X | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| middleName |X |X | | |
| mobile |X |X | | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointLinkedBy |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| objectSID |X | |X |Proprietà meccanica. Identificatore utente di Active Directory utilizzato toomaintain sincronizzazione tra Azure Active Directory e Active Directory. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherIpPhone |X |X | | |
| otherMobile |X |X | | |
| otherPager |X |X | | |
| otherTelephone |X |X | | |
| pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| postOfficeBox |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |Proprietà meccanica. Tooknow usato quando tooinvalidate già i token rilasciati. Usata sia dal servizio di sincronizzazione delle password che dalla federazione. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityEnabled | | |X |Derivato da groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |Proprietà meccanica. Relazione di toomaintain identificatore non modificabile compreso tra ADDS e Azure AD. |
| st |X |X | | |
| streetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| title |X |X | | |
| unauthOrig |X |X |X | |
| URL |X |X | | |
| usageLocation |X | | |Proprietà meccanica. paese dell'utente Hello. Usato per l'assegnazione delle licenze. |
| userPrincipalName |X | | |Nome UPN è hello ID di accesso per utente hello. Hello spesso corrisponde al valore [posta elettronica]. |
| wWWHomePage |X |X | | |

## <a name="lync-online"></a>Lync Online
| Nome attributo | Utente | Contatto | Gruppo | Commento |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Definisce se un account è abilitato. |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| department |X |X | | |
| description |X |X |X | |
| displayName |X |X |X | |
| facsimiletelephonenumber |X |X |X | |
| givenName |X |X | | |
| homePhone |X |X | | |
| ipPhone |X |X | | |
| l |X |X | | |
| mail |X |X |X | |
| mailNickname |X |X |X | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| mobile |X |X | | |
| msExchHideFromAddressLists |X |X |X | |
| msRTCSIP-ApplicationOptions |X | | | |
| msRTCSIP-DeploymentLocator |X |X | | |
| msRTCSIP-Line |X |X | | |
| msRTCSIP-OptionFlags |X |X | | |
| msRTCSIP-OwnerUrn |X | | | |
| msRTCSIP-PrimaryUserAddress |X |X | | |
| msRTCSIP-UserEnabled |X |X | | |
| objectSID |X | |X |Proprietà meccanica. Identificatore utente di Active Directory utilizzato toomaintain sincronizzazione tra Azure Active Directory e Active Directory. |
| otherTelephone |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |Proprietà meccanica. Tooknow usato quando tooinvalidate già i token rilasciati. Usata sia dal servizio di sincronizzazione delle password che dalla federazione. |
| securityEnabled | | |X |Derivato da groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |Proprietà meccanica. Relazione di toomaintain identificatore non modificabile compreso tra ADDS e Azure AD. |
| st |X |X | | |
| streetAddress |X |X | | |
| telephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| title |X |X | | |
| usageLocation |X | | |Proprietà meccanica. paese dell'utente Hello. Usato per l'assegnazione delle licenze. |
| userPrincipalName |X | | |Nome UPN è hello ID di accesso per utente hello. Hello spesso corrisponde al valore [posta elettronica]. |
| wWWHomePage |X |X | | |

## <a name="azure-rms"></a>Azure RMS
| Nome attributo | Utente | Contatto | Gruppo | Commento |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Definisce se un account è abilitato. |
| cn |X | |X |Nome comune o alias. In genere prefisso di hello del valore [posta elettronica]. |
| displayName |X |X |X |Stringa che rappresenta il nome di hello spesso visualizzato come nome descrittivo di hello (nome, cognome). |
| mail |X |X |X |Indirizzo di posta elettronica completo. |
| member | | |X | |
| objectSID |X | |X |Proprietà meccanica. Identificatore utente di Active Directory utilizzato toomaintain sincronizzazione tra Azure Active Directory e Active Directory. |
| proxyAddresses |X |X |X |Proprietà meccanica. Usata da Azure AD. Contiene tutti gli indirizzi di posta elettronica secondari per l'utente hello. |
| pwdLastSet |X | | |Proprietà meccanica. Tooknow usato quando tooinvalidate già i token rilasciati. |
| securityEnabled | | |X |Derivato da groupType. |
| sourceAnchor |X |X |X |Proprietà meccanica. Relazione di toomaintain identificatore non modificabile compreso tra ADDS e Azure AD. |
| usageLocation |X | | |Proprietà meccanica. paese dell'utente Hello. Usato per l'assegnazione delle licenze. |
| userPrincipalName |X | | |Questo nome UPN è hello ID di accesso per utente hello. Hello spesso corrisponde al valore [posta elettronica]. |

## <a name="intune"></a>Intune
| Nome attributo | Utente | Contatto | Gruppo | Commento |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Definisce se un account è abilitato. |
| c |X |X | | |
| cn |X | |X | |
| description |X |X |X | |
| displayName |X |X |X | |
| mail |X |X |X | |
| mailNickname |X |X |X | |
| member | | |X | |
| objectSID |X | |X |Proprietà meccanica. Identificatore utente di Active Directory utilizzato toomaintain sincronizzazione tra Azure Active Directory e Active Directory. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |Proprietà meccanica. Tooknow usato quando tooinvalidate già i token rilasciati. Usata sia dal servizio di sincronizzazione delle password che dalla federazione. |
| securityEnabled | | |X |Derivato da groupType |
| sourceAnchor |X |X |X |Proprietà meccanica. Relazione di toomaintain identificatore non modificabile compreso tra ADDS e Azure AD. |
| usageLocation |X | | |Proprietà meccanica. paese dell'utente Hello. Usato per l'assegnazione delle licenze. |
| userPrincipalName |X | | |Nome UPN è hello ID di accesso per utente hello. Hello spesso corrisponde al valore [posta elettronica]. |

## <a name="dynamics-crm"></a>Dynamics CRM
| Nome attributo | Utente | Contatto | Gruppo | Commento |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Definisce se un account è abilitato. |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| countryCode |X |X | | |
| description |X |X |X | |
| displayName |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| l |X |X | | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| mobile |X |X | | |
| objectSID |X | |X |Proprietà meccanica. Identificatore utente di Active Directory utilizzato toomaintain sincronizzazione tra Azure Active Directory e Active Directory. |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| preferredLanguage |X | | | |
| pwdLastSet |X | | |Proprietà meccanica. Tooknow usato quando tooinvalidate già i token rilasciati. Usata sia dal servizio di sincronizzazione delle password che dalla federazione. |
| securityEnabled | | |X |Derivato da groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |Proprietà meccanica. Relazione di toomaintain identificatore non modificabile compreso tra ADDS e Azure AD. |
| st |X |X | | |
| streetAddress |X |X | | |
| telephoneNumber |X |X | | |
| title |X |X | | |
| usageLocation |X | | |Proprietà meccanica. paese dell'utente Hello. Usato per l'assegnazione delle licenze. |
| userPrincipalName |X | | |Nome UPN è hello ID di accesso per utente hello. Hello spesso corrisponde al valore [posta elettronica]. |

## <a name="3rd-party-applications"></a>Applicazioni di terze parti
Questo gruppo è un set di attributi utilizzati come hello attributi minimi necessari per un'applicazione o il carico di lavoro generico. Può essere usato per un carico di lavoro non elencato in un'altra sezione o per un'app non Microsoft. Viene utilizzata in modo esplicito per seguenti hello:

* Yammer (viene usato solo Utente)
* [Scenari di collaborazione tra organizzazioni Business-to-Business (B2B) ibridi offerti da risorse come SharePoint](http://go.microsoft.com/fwlink/?LinkId=747036)

Questo gruppo è un set di attributi che possono essere utilizzati se hello Azure Active directory non è utilizzato toosupport Office 365, Dynamics o Intune. Contiene un piccolo set di attributi principali.

| Nome attributo | Utente | Contatto | Gruppo | Commento |
| --- |:---:|:---:|:---:| --- |
| accountEnabled |X | | |Definisce se un account è abilitato. |
| cn |X | |X | |
| displayName |X |X |X | |
| givenName |X |X | | |
| mail |X | |X | |
| managedBy | | |X | |
| mailNickname |X |X |X | |
| member | | |X | |
| objectSID |X | | |Proprietà meccanica. Identificatore utente di Active Directory utilizzato toomaintain sincronizzazione tra Azure Active Directory e Active Directory. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |Proprietà meccanica. Tooknow usato quando tooinvalidate già i token rilasciati. Usata sia dal servizio di sincronizzazione delle password che dalla federazione. |
| sn |X |X | | |
| sourceAnchor |X |X |X |Proprietà meccanica. Relazione di toomaintain identificatore non modificabile compreso tra ADDS e Azure AD. |
| usageLocation |X | | |Proprietà meccanica. paese dell'utente Hello. Usato per l'assegnazione delle licenze. |
| userPrincipalName |X | | |Nome UPN è hello ID di accesso per utente hello. Hello spesso corrisponde al valore [posta elettronica]. |

## <a name="windows-10"></a>Windows 10
Un computer(device) appartenenti a un dominio Windows 10 consente di sincronizzare alcuni tooAzure attributi Active Directory. Per ulteriori informazioni sugli scenari di hello, vedere [connessione tooAzure dispositivi appartenenti a un dominio Active Directory per Windows 10 esperienze](../active-directory-azureadjoin-devices-group-policy.md). Questi attributi verranno sempre sincronizzati e Windows 10 non appare come app che è possibile deselezionare. Un computer di dominio di Windows 10 viene identificato con hello attributo userCertificate popolato.

| Nome attributo | Dispositivo | Commento |
| --- |:---:| --- |
| accountEnabled |X | |
| deviceTrustType |X |Valore hardcoded per i computer di dominio. |
| displayName |X | |
| ms-DS-CreatorSID |X |Chiamato anche registeredOwnerReference. |
| objectGUID |X |Chiamato anche deviceID. |
| objectSID |X |Chiamato anche onPremisesSecurityIdentifier. |
| operatingSystem |X |Chiamato anche deviceOSType. |
| operatingSystemVersion |X |Anche chiamato deviceOSVersion. |
| userCertificate |X | |

Questi attributi per **utente** sono inoltre toohello altre App è stata selezionata.  

| Nome attributo | Utente | Commento |
| --- |:---:| --- |
| domainFQDN |X |Anche chiamato dnsDomainName. Ad esempio, contoso.com. |
| domainNetBios |X |Anche chiamato netBiosName. Ad esempio, CONTOSO. |

## <a name="exchange-hybrid-writeback"></a>Writeback della distribuzione ibrida Exchange
Questi attributi vengono scritti nuovamente da Azure AD Active Directory locale tooon quando si seleziona tooenable **ibrida di Exchange**. A seconda della versione di Exchange in uso, potrebbe essere sincronizzato un numero minore di attributi.

| Nome attributo | Utente | Contatto | Gruppo | Commento |
| --- |:---:|:---:|:---:| --- |
| msDS-ExternalDirectoryObjectID |X | | |Derivato da cloudAnchor in Azure AD. Si tratta di un nuovo attributo di Exchange 2016 e Windows Server 2016 AD. |
| msExchArchiveStatus |X | | |Archivio online: Consente di posta elettronica tooarchive clienti. |
| msExchBlockedSendersHash |X | | |Filtro: esegue il writeback del filtro locale e dei dati dei mittenti attendibili e bloccati dai client. |
| msExchSafeRecipientsHash |X | | |Filtro: esegue il writeback del filtro locale e dei dati dei mittenti attendibili e bloccati dai client. |
| msExchSafeSendersHash |X | | |Filtro: esegue il writeback del filtro locale e dei dati dei mittenti attendibili e bloccati dai client. |
| msExchUCVoiceMailSettings |X | | |Abilitare la messaggistica unificata (UM) - vocale Online: utilizzata da Microsoft Lync Server integrazione tooindicate tooLync Server locale, tale utente hello è posta vocale nei servizi online. |
| msExchUserHoldPolicies |X | | |Attesa di controversia legale: Consente toodetermine di servizi cloud che gli utenti sono in contenere controversia legale. |
| proxyAddresses |X |X |X |Viene inserito solo indirizzo di hello x500 da Exchange Online. |
| publicDelegates |X | | |Consente che un toobe cassetta postale di Exchange Online concesso SendOnBehalfTo diritti toousers con cassetta postale di Exchange locale. Richiede la build 1.1.552.0 o successiva di Azure AD Connect. |

## <a name="exchange-mail-public-folder"></a>Cartelle pubbliche della posta di Exchange
Questi attributi vengono sincronizzati da tooAzure di Active Directory locale AD quando si seleziona tooenable **cartella pubblica di posta elettronica di Exchange**.

| Nome attributo | Cartella pubblica | Commento |
| --- | :---:| --- |
| displayName | X |  |
| mail | X |  |
| msExchRecipientTypeDetails | X |  |
| objectGUID | X |  |
| proxyAddresses | X |  |
| targetAddress | X |  |

## <a name="device-writeback"></a>Writeback dispositivi
Gli oggetti dispositivo vengono creati in Active Directory. Questi oggetti possono essere dispositivi associati AD tooAzure o i computer Windows 10 appartenenti a un dominio.

| Nome attributo | Dispositivo | Commento |
| --- |:---:| --- |
| altSecurityIdentities |X | |
| displayName |X | |
| dn |X | |
| msDS-CloudAnchor |X | |
| msDS-DeviceID |X | |
| msDS-DeviceObjectVersion |X | |
| msDS-DeviceOSType |X | |
| msDS-DeviceOSVersion |X | |
| msDS-DevicePhysicalIDs |X | |
| msDS-KeyCredentialLink |X |Solo con lo schema di AD Windows Server 2016 |
| msDS-IsCompliant |X | |
| msDS-IsEnabled |X | |
| msDS-IsManaged |X | |
| msDS-RegisteredOwner |X | |

## <a name="notes"></a>Note
* Quando si usa un ID alternativo hello locale attributo userPrincipalName è sincronizzato con onPremisesUserPrincipalName di attributo hello Azure AD. Hello attributo ID alternativo, ad esempio posta elettronica, vengono sincronizzati con hello Azure AD attributo userPrincipalName.
* Negli elenchi di hello precedenti, il tipo di oggetto di hello **utente** si applica anche il tipo di oggetto toohello **iNetOrgPerson**.

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su hello [sincronizzazione di Azure AD Connect](active-directory-aadconnectsync-whatis.md) configurazione.

Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
