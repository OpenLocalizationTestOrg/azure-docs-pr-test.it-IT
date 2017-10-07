---
title: criteri dei dispositivi aaaAzure Active Directory l'accesso condizionale per servizi di Office 365 | Documenti Microsoft
description: "Informazioni su come tooprovision accesso condizionale dispositivo criteri toohelp rendere le risorse aziendali più sicura, mantenendo tooservices di conformità e l'accesso utente."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8664c0bb-bba1-4012-b321-e9c8363080a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 38229a8d9766efbf0e6b17875b3018011c6b4ea3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="active-directory-conditional-access-device-policies-for-office-365-services"></a>Criteri di accesso condizionale dei dispositivi di Active Directory per i servizi di Office 365

Accesso condizionale richiede più parti toowork. tra cui un utente con autenticazione a più fattori, un dispositivo autenticato e un dispositivo conforme. In questo articolo, focalizzata principalmente sulle condizioni basate sul dispositivo che l'organizzazione può utilizzare toohelp controllare servizi di accesso tooOffice 365. 

Gli utenti aziendali desiderano tooaccess Office 365 servizi come Exchange e SharePoint Online o dall'istituto dai loro dispositivi personali. Si desidera hello toobe di accesso protetto. È possibile fornire l'accesso condizionale dispositivo criteri toohelp apportare alle risorse aziendali più sicure, durante la concessione dell'accesso tooservices per gli utenti che utilizzano i dispositivi conformi. È possibile impostare i criteri di accesso condizionale tooOffice 365 nel portale di accesso condizionale di Microsoft Intune hello.

Azure Active Directory (Azure AD) consente di applicare l'accesso condizionale criteri toohelp accesso sicuro tooOffice 365 i servizi. È possibile creare criteri di accesso condizionale che impediscano a un utente che usa un dispositivo non conforme di accedere a un servizio di Office 365. utente Hello deve essere conformi a criteri per i dispositivi della società toohello prima di concessa l'accesso toohello servizio. In alternativa, è possibile creare un criterio che richiede agli utenti tooenroll tooan di accesso loro toogain dispositivi servizio Office 365. I criteri possono essere applicati tooall utenti in un'organizzazione o limitato tooa alcuni gruppi di destinazione. È possibile aggiungere ulteriori criteri tooa gruppi di destinazione nel tempo.

Un prerequisito per l'applicazione di criteri per i dispositivi è che gli utenti devono registrare i propri dispositivi con il servizio Registrazione dispositivi di hello Azure AD. È possibile scegliere tooturn su multi-factor authentication per i dispositivi che registrati con il servizio Registrazione dispositivi di Azure AD hello. Multi-factor authentication è consigliato per hello servizio Registrazione dispositivi di Azure Active Directory. Quando è attivata l'autenticazione a più fattori, vengono considerati come utenti di registrare i propri dispositivi con hello servizio Registrazione dispositivi di Azure AD per l'autenticazione a due fattori.

## <a name="how-does-a-conditional-access-policy-work"></a>Come funzionano i criteri di accesso condizionale

Quando un utente richiede l'accesso tooan servizio Office 365 da una piattaforma supportata, Azure AD autentica l'utente hello e dispositivo hello. Concede l'accesso toohello servizio di Azure AD solo se l'utente hello conforme toohello set dei criteri per il servizio di hello. Gli utenti di dispositivi che non sono registrati vengono forniti istruzioni su come tooenroll e diventare conforme tooaccess aziendali servizi di Office 365. Gli utenti di dispositivi iOS e Android sono necessari tooenroll i propri dispositivi tramite un'applicazione hello portale aziendale di Intune. Quando un utente registra un dispositivo, hello dispositivo è registrato con Azure AD e viene registrato per la conformità e gestione dei dispositivi. È necessario utilizzare il servizio Registrazione dispositivi di hello Azure AD con Microsoft Intune per la gestione di dispositivi mobili per i servizi di Office 365. Registrazione del dispositivo è necessaria per gli utenti tooaccess servizi di Office 365 quando sono applicati i criteri del dispositivo.

Quando un utente registra correttamente un dispositivo, il dispositivo hello diventa attendibile. Azure AD offre hello autenticato utente l'accesso single sign-on toocompany applicazioni. Azure AD applica un accesso condizionale criteri toogrant tooa servizio di accesso non solo hello hello utente richiede l'accesso, ma ogni utente hello ora rinnova una richiesta di accesso. Hello utente viene negato l'accesso tooservices quando vengono modificate le credenziali di accesso, dispositivo hello viene smarrito o rubato o hello del criterio hello condizioni non sono in fase di hello della richiesta di rinnovo.

## <a name="deployment-considerations"></a>Considerazioni sulla distribuzione

È necessario utilizzare i dispositivi di tooregister servizio registrazione dispositivo Azure AD hello.

Quando gli utenti locali stanno toobe autenticato, Active Directory Federation Services (ADFS) (versione 1.0 e versioni successive) è obbligatorio. Autenticazione a più fattori per l'area di lavoro ha esito negativo quando il provider di identità hello non è in grado di multi-factor authentication. Ad esempio, non è possibile usare l'autenticazione a più fattori con AD FS 2.0. Verificare che hello locale AD FS funziona con l'autenticazione a più fattori e che un metodo di autenticazione a più fattori valido sia attiva prima di attivare l'autenticazione a più fattori per il servizio Registrazione dispositivi di hello Azure AD. Ad esempio, AD FS in Windows Server 2012 R2 offre funzionalità per l'autenticazione a più fattori. È inoltre necessario impostare un metodo di autenticazione valido aggiuntive (multi-factor authentication) nel server AD FS hello prima di attivare l'autenticazione a più fattori per il servizio Registrazione dispositivi di hello Azure AD. Per altre informazioni sui metodi di autenticazione a più fattori supportati in AD FS, vedere [Configurare altri metodi di autenticazione per AD FS](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs).

## <a name="next-steps"></a>Passaggi successivi

*   Per domande toocommon risposte, vedere [accesso condizionale di Azure Active Directory FAQ](active-directory-conditional-faqs.md).
