---
title: accesso aaaConditional nel portale di Azure classico hello | Documenti Microsoft
description: Utilizzare il controllo di accesso condizionale in hello Azure toocheck portale classico per condizioni specifiche per l'autenticazione per accesso tooapplications.
services: active-directory
keywords: accesso condizionale tooapps, l'accesso condizionale con Azure AD, proteggere l'accesso alle risorse toocompany, criteri di accesso condizionale
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: da3f0a44-1399-4e0b-aefb-03a826ae4ead
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.custom: oldportal
ms.openlocfilehash: 049bd3f6ec9e35479319ee7608b007b9a1e16647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-hello-azure-classic-portal"></a>Accesso condizionale in hello portale di Azure classico

Questo argomento vengono illustrati l'accesso condizionale in hello portale di Azure classico. Per informazioni più recenti di hello sull'accesso condizionale in hello Azure Active Directory, vedere [accesso condizionale in Azure Active Directory](active-directory-conditional-access-azure-portal.md).


funzionalità di controllo di accesso condizionale di Azure Active Directory (Azure AD) di Hello offrono un modo semplice toohelp risorse protette nel cloud hello e in locale. Criteri di accesso condizionale come autenticazione a più fattori offrono protezione contro il rischio di hello di furto e phished credenziali. Altri criteri di accesso condizionale garantiscono la sicurezza dei dati dell'organizzazione. Ad esempio, inoltre toorequiring credenziali, potrebbe essere un criterio che solo i dispositivi che sono registrati in un sistema di gestione di dispositivi mobili, ad esempio Microsoft Intune può accedere ai servizi sensibili dell'organizzazione.

## <a name="prerequisites"></a>Prerequisiti
L'accesso condizionale di Azure AD è una funzionalità di [Azure Active Directory Premium](http://www.microsoft.com/identity). Ogni utente che accede a un'applicazione a cui sono applicati i criteri di accesso condizionale deve avere una licenza di Azure AD Premium. Per altre informazioni sui requisiti relativi alle licenza, vedere [Report Utilizzo senza licenza](https://aka.ms/utc5ix).

## <a name="how-is-conditional-access-control-enforced"></a>Applicazione del controllo di accesso condizionale
Con il controllo accesso condizionale, Azure AD verifica per condizioni specifiche hello impostata per un utente tooaccess un'applicazione. Dopo che siano soddisfatti i requisiti di accesso, utente hello viene autenticato e può accedere a un'applicazione hello.  

![Panoramica dell'accesso condizionale](./media/active-directory-conditional-access/conditionalaccess-overview.png)

## <a name="conditions"></a>Condizioni
Di seguito sono riportate condizioni che è possibile includere in un criterio di accesso condizionale:

* **Appartenenza a un gruppo**. Controllare che un utente acceda sulla base dell'appartenenza a un gruppo.
* **Località**. Utilizzare il percorso di hello di hello utente tootrigger multi-factor authentication e utilizzare i controlli di blocco quando un utente non è presente in una rete attendibile.
* **Piattaforma del dispositivo**. Utilizzare piattaforma del dispositivo hello, ad esempio iOS, Android, Windows Mobile o Windows, come condizione per l'applicazione dei criteri.
* **Dispositivo abilitato**. Lo stato di abilitazione o disabilitazione del dispositivo viene convalidato durante la valutazione dei criteri del dispositivo. Se si disattiva un dispositivo perso o rubato nella directory di hello, sia non è più possibile soddisfare i requisiti dei criteri.
* **Accesso e rischi per l'utente**. È possibile usare [Azure AD Identity Protection](active-directory-identityprotection.md) per i criteri di rischio dell'accesso condizionale. Tali criteri assicurano all'organizzazione una protezione avanzata in base a eventi di rischio e attività di accesso anomale.

## <a name="controls"></a>Controlli
Si tratta di controlli che è possibile utilizzare tooenforce un criterio di accesso condizionale:

* **Multi-Factor Authentication**. È possibile richiedere l'autenticazione avanzata tramite l'autenticazione a più fattori. È possibile usare l'autenticazione a più fattori con Azure Multi-Factor Authentication o mediante un provider di autenticazione a più fattori, in combinazione con AD FS (Active Directory Federation Services). Tramite multi-factor authentication consente di proteggere le risorse da cui si accede da un utente non autorizzato potrebbe avere avuto accesso toohello le credenziali di un utente valido.
* **Blocco**. È possibile applicare le condizioni, ad esempio l'accesso utente percorso tooblock utente. È ad esempio possibile bloccare l'accesso quando un utente non si trova in una rete attendibile.
* **Dispositivi conformi**. È possibile impostare i criteri di accesso condizionale a livello di dispositivo hello. È possibile impostare un criterio in base al quale possono accedere alle risorse dell'organizzazione soltanto i computer aggiunti a un dominio o registrati in un sistema di gestione di dispositivi mobili. Ad esempio, possibile usare Intune toocheck conformità del dispositivo e quindi segnalarlo tooAzure Active Directory per l'applicazione quando l'utente hello tenta tooaccess un'applicazione. Per istruzioni dettagliate sul funzionamento toouse Intune tooprotect App e dati, vedere [proteggere App e dati con Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/protect-apps-and-data-with-microsoft-intune). È inoltre possibile utilizzare la protezione dei dati tooenforce Intune per dispositivi smarriti o rubati. Per altre informazioni, vedere [Proteggere i dati con la cancellazione completa o selettiva tramite Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).

## <a name="applications"></a>Applicazioni
È possibile applicare un criterio di accesso condizionale a livello di applicazione hello. Livelli di accesso set per le applicazioni e servizi in cloud hello o locale. criteri di Hello sono applicato direttamente il sito Web toohello o un servizio. Per accedere toohello browser e tooapplications che accedono a hello servizio vengono applicati i criteri di Hello.

## <a name="device-based-conditional-access"></a>Accesso condizionale basato su dispositivo
È possibile limitare l'accesso tooapplications dai dispositivi registrati con Azure AD, e che soddisfano condizioni specifiche. Accesso condizionale basato su dispositivo protegge le risorse dell'organizzazione da utenti che tentano di risorse hello tooaccess da:

* Dispositivi sconosciuti o non gestiti.
* I dispositivi che non soddisfano i criteri di sicurezza hello per l'organizzazione impostato.

I criteri possono essere impostati in base ai requisiti seguenti:

* **Dispositivi aggiunti a un dominio**. Impostare un toodevices accesso toorestrict criteri che sono tooan aggiunti a un dominio di Active Directory locale, e anche registrati con Azure AD. Questi criteri si applicano tooWindows desktop, portatili e Tablet enterprise.
  Per ulteriori informazioni su come tooset di registrazione automatica dei dispositivi appartenenti a un dominio con Azure AD, vedere [configurare la registrazione automatica dei dispositivi appartenenti a un dominio di Windows con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).
* **Dispositivi conformi**. Impostare un toodevices accesso toorestrict di criteri che sono contrassegnati **conformi** nella directory di sistema di gestione hello. Con questo criterio, l'accesso viene limitato ai soli dispositivi conformi ai criteri di sicurezza, ad esempio l'applicazione della crittografia dei file. È possibile utilizzare questo accesso toorestrict criteri da hello seguenti dispositivi:
  
  * **Dispositivi Windows aggiunti a un dominio**. Gestito da System Center Configuration Manager (nel hello current branch) distribuiti in una configurazione ibrida.
  * **Dispositivi Windows 10 mobili o personali**. Dispositivi gestiti da Intune o da un sistema di gestione di dispositivi mobili di terze parti supportato.
  * **Dispositivi iOS e Android**. Dispositivi gestiti da Intune.

Gli utenti che accedono alle applicazioni che sono protetti da un dispositivo basato su un, i criteri Autorità di certificazione devono accedere un'applicazione hello da un dispositivo che soddisfa i requisiti di questo criterio. Se si tenta di accedere da un dispositivo che non soddisfa i requisiti del criterio, l'accesso viene negato.

Per informazioni su come tooconfigure un dispositivo basata su criteri di autorità di certificazione in Azure AD, vedere [impostare criteri di accesso condizionale basato su dispositivo per applicazioni connesse a Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md).

## <a name="resources"></a>Risorse
Vedere hello seguenti delle risorse categorie e gli articoli delle toolearn a ulteriori informazioni sull'impostazione di accesso condizionale per l'organizzazione.

### <a name="multi-factor-authentication-and-location-policies"></a>Criteri basati sull'autenticazione a più fattori e la località
* [Introduzione alle App connessa AD tooAzure di accesso condizionale in base a criteri di autenticazione a più fattori, il percorso e gruppo](active-directory-conditional-access-azuread-connected-apps.md)
* [Applicazioni e browser supportati](active-directory-conditional-access-supported-apps.md)

### <a name="device-based-conditional-access"></a>Accesso condizionale basato su dispositivo
* [Impostare criteri di accesso condizionale basato su dispositivo per l'accesso di applicazioni connesse a Active Directory tooAzure di controllo](active-directory-conditional-access-policy-connected-applications.md)
* [Come configurare la registrazione automatica dei dispositivi Windows con Azure Active Directory aggiunti a un dominio](active-directory-conditional-access-automatic-device-registration-setup.md)
* [Risoluzione dei problemi di accesso di Azure Active Directory](active-directory-conditional-access-device-remediation.md)
* [Proteggere i dati con la cancellazione selettiva o completa tramite Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune)

### <a name="protect-resources-based-on-sign-in-risk"></a>Protezione delle risorse in base ai rischi di accesso
* [Azure AD identity protection](active-directory-identityprotection.md)

### <a name="next-steps"></a>Passaggi successivi
* [Domande frequenti sull'accesso condizionale](active-directory-conditional-faqs.md)
* [Riferimento tecnico](active-directory-conditional-access-technical-reference.md)

