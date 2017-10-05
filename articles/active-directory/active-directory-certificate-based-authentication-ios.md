---
title: Autenticazione basata su certificati di Azure Active Directory in iOS | Documentazione Microsoft
description: Informazioni sugli scenari supportati e i requisiti per configurare l'autenticazione basata su certificati nelle soluzioni con i dispositivi iOS
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: 26a6fc54-0153-44fb-b970-9b432c99e9f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: c781f3f054fad5c5092fed5058c932fd4e97cf35
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a>Autenticazione basata su certificati di Azure Active Directory in iOS

L'autenticazione basata su certificati (CBA) consente di essere autenticati da Azure Active Directory con un certificato client su un dispositivo Windows, Android o iOS quando si connette il proprio account Exchange online a: 

* Applicazioni Office per dispositivi mobili, come Microsoft Outlook e Microsoft Word   
* Client Exchange ActiveSync (EAS) 

La configurazione di questa funzionalità elimina la necessità di immettere una combinazione di nome utente e password in determinate applicazioni di posta e applicazioni Microsoft Office sul dispositivo mobile. 

Questo argomento indica i requisiti e gli scenari supportati per la configurazione dell'autenticazione basata su certificati su un dispositivo iOS (Android) per gli utenti dei tenant nei piani di Office 365 Enterprise, Business, Education, US Government, China e Germany.

Questa funzionalità è disponibile in anteprima nei piani di Office 365 US Government Defense e Federal.




## <a name="office-mobile-applications-support"></a>Supporto delle applicazioni Office per dispositivi mobili

| App | Supporto |
| --- | --- |
| App Azure Information Protection |![Controllo][1] |
| Microsoft Teams |![Controllo][1] |
| OneNote |![Controllo][1] |
| OneDrive |![Controllo][1] |
| Outlook |![Controllo][1] |
| App per dispositivi mobili di Power BI |![Controllo][1] |
| Skype for Business Online |![Controllo][1] |
| Word / Excel / PowerPoint |![Controllo][1] |
| Yammer |![Controllo][1] |


## <a name="requirements"></a>Requisiti 

La versione del sistema operativo del dispositivo deve essere iOS 9 o successiva 

È necessario configurare un server federativo.  

Per le applicazioni Office in iOS è richiesto Microsoft Authenticator.  

Perché Azure Active Directory possa revocare un certificato client, il token ADFS deve avere le attestazioni seguenti:  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  (Il numero di serie del certificato client) 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  (La stringa per l'autorità emittente del certificato client) 

Azure Active Directory aggiunge queste attestazioni per il token di aggiornamento se sono disponibili nel token ADFS (o in qualsiasi altro token SAML). Quando il token di aggiornamento deve essere convalidato, queste informazioni vengono usate per controllare la revoca. 

Come procedura consigliata, è necessario aggiornare le pagine di errore di ADFS con le operazioni seguenti:

* Il requisito dell'installazione di Microsoft Authenticator in iOS
* Istruzioni su come ottenere un certificato utente. 

Per altre informazioni, vedere [Personalizzazione delle pagine di accesso ad AD FS](https://technet.microsoft.com/library/dn280950.aspx).

Alcune app di Office, in cui non è abilitata l'autenticazione moderna, inviano "*prompt=login*" ad Azure AD nella richiesta. Per impostazione predefinita, Azure AD lo traduce in una richiesta ad AD FS di eseguire l'autorizzazione di nome utente e password, ovvero "*wauth=usernamepassworduri*", e di ignorare lo stato SSO ed eseguire una nuova autenticazione, ovvero "*wfresh=0*". Per abilitare l'autenticazione basata su certificati per queste applicazioni, è necessario modificare il comportamento predefinito di Azure AD. È sufficiente impostare "*PromptLoginBehavior*" tra le impostazioni del dominio federato su "*Disabled*" (Disabilitato). Per eseguire questa operazione è possibile usare il cmdlet [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0):

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a>Supporto dei client Exchange ActiveSync
In iOS 9 o versioni successive è supportato il client di posta iOS nativo. Per tutte le altre applicazioni Exchange ActiveSync, contattare lo sviluppatore dell'applicazione per determinare se questa funzionalità è supportata.  


## <a name="next-steps"></a>Passaggi successivi

Se si desidera configurare l'autenticazione basata su certificati nel proprio ambiente, vedere [Introduzione all'autenticazione basata su certificati in Android](active-directory-certificate-based-authentication-get-started.md) per le istruzioni.


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
