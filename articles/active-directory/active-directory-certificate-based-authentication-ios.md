---
title: autenticazione basata su certificati aaaAzure Active Directory in iOS | Documenti Microsoft
description: Informazioni sugli scenari di hello supportata e requisiti di hello per la configurazione dell'autenticazione basata su certificato nelle soluzioni con i dispositivi iOS
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
ms.openlocfilehash: 4486ff5239c2897b3bc187053f31d74807430301
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a>Autenticazione basata su certificati di Azure Active Directory in iOS

L'autenticazione basata su certificato (CBA) consente toobe autenticato da Azure Active Directory con un certificato client in un dispositivo Windows, Android o iOS, quando ci si connette l'account di Exchange online a: 

* Applicazioni Office per dispositivi mobili, come Microsoft Outlook e Microsoft Word   
* Client Exchange ActiveSync (EAS) 

Configurazione di questa funzionalità Elimina hello necessità tooenter un nome utente e la combinazione di password in determinate posta elettronica e le applicazioni di Microsoft Office sul tuo dispositivo mobile. 

In questo argomento vengono fornite hello requisiti e degli scenari di hello è supportato per la configurazione CBA in un dispositivo iOS(Android) per gli utenti del tenant Office 365 Enterprise, Business, formazione, governo, Cina, e piani Germania.

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

Hello versione sistema operativo del dispositivo deve essere iOS 9 e versioni successive 

È necessario configurare un server federativo.  

Per le applicazioni Office in iOS è richiesto Microsoft Authenticator.  

Per un certificato client toorevoke di Azure Active Directory, token ADFS hello deve avere hello seguenti attestazioni:  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  (hello numero di serie del certificato client hello) 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  (stringa hello per emittente hello del certificato client hello) 

Azure Active Directory aggiunge queste attestazioni toohello il token di aggiornamento se sono disponibili nel token ADFS hello (o qualsiasi altro token SAML). Quando il token di aggiornamento hello deve toobe convalidato, queste informazioni sono utilizzate toocheck hello revoca. 

Come procedura consigliata, è necessario aggiornare le pagine di errore hello ADFS con seguenti hello:

* requisito di Hello per l'installazione di Microsoft Authenticator hello in iOS
* Istruzioni su come tooget un certificato utente. 

Per ulteriori informazioni, vedere [personalizzazione delle pagine di hello AD FS Sign-in](https://technet.microsoft.com/library/dn280950.aspx).

Alcune applicazioni di Office (con l'autenticazione moderna abilitata) inviare '*prompt = account di accesso*' tooAzure AD nella richiesta. Per impostazione predefinita, Azure AD Converte l'oggetto in hello richiesta tooADFS troppo '*wauth = usernamepassworduri*' (richiede l'autenticazione ADFS toodo U/P) e '*wfresh = 0*' (richiede lo stato SSO tooignore ad FS ed eseguire una ripetizione dell'autenticazione) . Se si desidera tooenable basata sui certificati di autenticazione per queste App, è necessario un comportamento toomodify hello predefinito AD Azure. Solo il set di hello '*PromptLoginBehavior*' nelle impostazioni del dominio federato troppo '*disabilitato*'. È possibile utilizzare hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) tooperform cmdlet questa attività:

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a>Supporto dei client Exchange ActiveSync
Nelle versioni iOS 9 o versione successiva, client di posta elettronica iOS native hello è supportato. Per tutte le altre applicazioni di Exchange ActiveSync, toodetermine se questa funzionalità è supportata, contattare lo sviluppatore dell'applicazione.  


## <a name="next-steps"></a>Passaggi successivi

Se si desidera l'autenticazione basata su certificato tooconfigure nell'ambiente in uso, vedere [Introduzione all'autenticazione basata sui certificati in Android](active-directory-certificate-based-authentication-get-started.md) per le istruzioni.


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
