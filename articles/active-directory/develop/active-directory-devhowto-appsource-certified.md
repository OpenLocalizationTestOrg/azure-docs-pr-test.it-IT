---
title: aaaHow tooget AppSource certificate per Azure Active Directory | Documenti Microsoft
description: Informazioni dettagliate su come tooget applicazione AppSource certificate per Azure Active Directory.
services: active-directory
documentationcenter: 
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 21206407-49f8-4c0b-84d1-c25e17cd4183
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/03/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: e9f07e9220afcba1120b987122fe770fe5225eed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-appsource-certified-for-azure-active-directory"></a>Come tooget AppSource certificate per Azure Active Directory
[Microsoft AppSource](https://appsource.microsoft.com/) è una destinazione per toodiscover agli utenti di business, provare e gestire le applicazioni line-of-business SaaS (autonomo SaaS e componente aggiuntivo tooexisting SaaS Microsoft prodotti).

toolist un'applicazione SaaS in AppSource autonoma, è necessario accettare l'applicazione single sign-on dall'account aziendale da qualsiasi società o organizzazione con Azure Active Directory. processo di accesso Hello deve utilizzare hello [OpenID Connect](./active-directory-protocols-openid-connect-code.md) o [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocolli. L'integrazione SAML non è accettata per la certificazione AppSource.

## <a name="guides-and-code-samples"></a>Guide ed esempi di codice
Se si desidera toolearn sulla modalità di connessione dell'applicazione con Azure Active Directory tramite Openid di toointegrate, seguire le guide e scrivere il codice negli esempi di hello [Guida per gli sviluppatori di Azure Active Directory](./active-directory-developers-guide.md#get-started "introduzione Azure AD per gli sviluppatori").

## <a name="multi-tenant-applications"></a>Applicazioni multi-tenant

Un'applicazione che accetta l'accesso degli utenti da qualsiasi società o organizzazione con Azure Active Directory senza richiedere un'istanza, una configurazione o una distribuzione separata è nota come *applicazione multi-tenant*. AppSource consiglia che le applicazioni implementano hello multi-tenancy tooenable *con clic singolo* esperienza di valutazione gratuita.

In ordine tooenable multi-tenancy sull'applicazione:
- Impostare `Multi-Tenanted` proprietà troppo`Yes` sulle informazioni della registrazione applicazione in hello [portale Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (per impostazione predefinita, le applicazioni create in hello portale di Azure sono configurate come *single-tenant*)
- Aggiornare il toohello le richieste di codice toosend '`common`' endpoint (aggiornare l'endpoint di hello da *https://login.microsoftonline.com/ {yourtenant}* troppo*https://login.microsoftonline.com/common*)
- Per alcune piattaforme, ad esempio ASP.NET, è necessario anche tooupdate tooaccept il codice più emittenti

Per ulteriori informazioni su multi-tenancy, vedere: [come toosign in qualsiasi utente di Azure Active Directory (AD) usando hello modello di applicazione multi-tenant](./active-directory-devhowto-multi-tenant-overview.md).

### <a name="single-tenant-applications"></a>Applicazioni a tenant singolo
Le applicazioni che accettano solo l'accesso degli utenti di un'istanza di Azure Active Directory definita sono note come *applicazioni a tenant singolo*. Gli utenti esterni, inclusi gli account aziendale o dell'istituto di istruzione da altre organizzazioni o account personale, possono accedere in applicazione single-tenant tooa dopo l'aggiunta di ogni utente come *account guest* istanza toohello Azure Active Directory un'applicazione Hello è registrata. È possibile aggiungere utenti come guest tooan di account Azure Active Directory tramite hello [ *collaborazione B2B di Azure AD* ](../active-directory-b2b-what-is-azure-ad-b2b.md) - e può essere eseguita [a livello di programmazione](../active-directory-b2b-code-samples.md). Quando si aggiunge un utente come tooan account guest Azure Active Directory, un messaggio di posta elettronica di invito viene inviato toohello utente, con invito hello tooaccept facendo clic sul collegamento hello nel messaggio di posta elettronica di invito hello. Inviti inviati tooan utente in un'organizzazione invitando che sia anche membro dell'organizzazione partner hello sono tooaccept non è necessario un invito toosign in.

Le applicazioni single-tenant possono abilitare hello *Contact Me* esperienza, ma se si desidera tooenable hello con clic singolo / libero valutazione AppSource consigliato, abilitare multi-tenancy all'applicazione.


## <a name="appsource-trial-experiences"></a>Esperienze di valutazione di AppSource

### <a name="free-trial-customer-led-trial-experience"></a>Versione di valutazione gratuita (esperienza di valutazione gestita dal cliente) 
Hello *lock-versione di valutazione* esperienza hello AppSource consigliato, poiché offre un'applicazione tooyour accesso con clic singolo. Di seguito è illustrata questa esperienza:<br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li>L'utente trova l'applicazione nel sito Web AppSource</li><li>Seleziona l'opzione "Versione di valutazione gratuita"</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li>AppSource reindirizza l'utente tooa URL del sito web</li><li>Il sito web avvia hello <i>single sign-on</i> processo automaticamente (al caricamento della pagina)</li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li>Utente viene reindirizzato tooMicrosoft Accedi pagina</li><li>Utente fornisce credenziali toosign in</li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li>L'utente dà il consenso per l'applicazione</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>Accedi completa e l'utente viene reindirizzato tooyour indietro sito</li><li>Utente avvia versione di valutazione gratuita di hello</li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a>Desidero essere contattato (esperienza di valutazione gestita dal partner)
Hello *partner valutazione* può essere utilizzata quando un manuale o un'operazione a lungo termine deve utente di hello tooprovision toohappen /Company: ad esempio, l'applicazione deve tooprovision le macchine virtuali, istanze di database, o operazioni che richiedono toocomplete molto tempo. In questo caso, dopo l'utente seleziona hello *'Richiesta versione di valutazione'* pulsante e compila un modulo, AppSource invia hello informazioni di contatto dell'utente. Dopo aver ricevuto queste informazioni, quindi eseguire il provisioning di ambiente hello e invia all'utente di toohello hello istruzioni su come tooaccess hello esperienza di valutazione:<br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li>L'utente trova l'applicazione nel sito Web AppSource</li><li>Seleziona l'opzione "Desidero essere contattato"</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li>Compila un modulo con le informazioni di contatto</li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td>Le informazioni dell'utente vengono ricevute</td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td>L'ambiente viene configurato</td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td>L'utente viene contattato con le informazioni sulla versione di valutazione</td>
        </tr>
        </table><br/><br/>
        <ul><li>Le informazioni dell'utente vengono ricevute e viene configurata l'istanza di valutazione</li><li>Si invia hello collegamento ipertestuale tooaccess utenti toohello dell'applicazione</li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li>Utente accede l'applicazione e il processo single sign-on di hello completo</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li>L'utente dà il consenso per l'applicazione</li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>Accedi completa e l'utente viene reindirizzato tooyour indietro sito</li><li>Utente avvia versione di valutazione gratuita di hello</li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a>Altre informazioni
Per ulteriori informazioni sull'esperienza di valutazione AppSource hello, vedere [questo video](https://aka.ms/trialexperienceforwebapps). 
 
## <a name="next-steps"></a>Passaggi successivi

- Per altre informazioni sulla creazione di applicazioni che supportano gli accessi di Azure Active Directory, vedere [Scenari di autenticazione per Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios) 

- Per informazioni su come toolist applicazione SaaS in AppSource, Vai vedere [AppSource informazioni per i Partner](https://appsource.microsoft.com/partners)


## <a name="get-support"></a>Ottenere supporto
Per l'integrazione di Azure Active Directory, utilizziamo [Overflow dello Stack](http://stackoverflow.com/questions/tagged/azure-active-directory) con supporto di tooprovide hello della community. 

Si consiglia di è possibile porre domande su Stack Overflow prima e individuare toosee problemi esistenti se un utente ha richiesto la domanda prima. Assicurarsi di aggiungere alle domande o ai commenti il tag `[azure-active-directory]`.

Utilizzare hello seguendo i commenti e suggerimenti tooprovide di sezione commenti e consentono di ridefinire e definire il contenuto.

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->