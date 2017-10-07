---
title: configurare password single sign-on per un'applicazione Azure AD raccolta aaaProblem | Documenti Microsoft
description: "Comprendere faccia persone problemi comuni di hello quando si configura Password Single Sign-on per le applicazioni che sono già elencati in hello raccolta di applicazioni Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 78c37c52453c375bf7ccbca6df5c9008be4ce642
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Problema nella configurazione dell'accesso Single Sign-On basato su password per un'applicazione nella raccolta di Azure AD

Questo articolo è utile faccia di persone di toounderstand hello comuni problemi quando si configura **Password Single Sign-on** con un'applicazione di raccolta di Azure AD.

## <a name="credentials-are-filled-in-but-hello-extension-does-not-submit-them"></a>Le credenziali vengono compilate, ma non inviare estensione hello

Ciò in genere si verifica se l'accesso è stato modificato da fornitore dell'applicazione hello recente pagina tooadd un campo, modificare un identificatore sottostante è utilizzato i campi nome utente e password hello toodetect o come accesso hello l'esperienza per l'applicazione. Fortunatamente, in molti casi, Microsoft può rivolgersi applicazione fornitori toorapidly risolvere questi problemi.

Microsoft ha tooautomatically tecnologie rilevare quando interrompere le integrazioni, ma in alcuni casi non è in grado di toofind questi problemi destro stoccaggio oppure richiederà un certo tempo toofix. In caso di hello quando uno di questi integrazioni non funziona correttamente, Gradiremmo se è stato aperto un caso di supporto in modo è possibile risolvere più rapidamente possibile.

In aggiunta toothis, **in contatto con il fornitore dell'applicazione, se si** **inviarli ritenuti utili** in modo da poter usare tali toonatively integrare le applicazioni con Azure Active Directory. È possibile inviare hello fornitore toohello [elenco l'applicazione nella raccolta di applicazioni per Azure Active Directory hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget li avviati.

## <a name="credentials-are-filled-in-and-submitted-but-hello-page-indicates-hello-credentials-are-incorrect"></a>Le credenziali vengono compilate e inviate, ma la pagina hello indica hello credenziali non sono corrette

tooresolve questo problema, prima seguente hello di controllo:

-   Hanno utente hello innanzitutto provare troppo**accedere direttamente nel sito Web di applicazione toohello** con hello credenziali archiviate per loro.

  * Se questa impostazione, è quindi necessario utente hello fare clic su hello **aggiornare le credenziali** pulsante hello **riquadro dell'applicazione** in hello **app** sezione di hello [applicazione Accedere al pannello](https://myapps.microsoft.com/) tooupdate li toohello più recente noto utilizza nome utente e password.

   * Se è o un altro assegnato hello credenziali per l'utente, utente hello o assegnazione di applicazioni del gruppo passando toohello **utenti e gruppi** scheda dell'applicazione hello, selezionando l'assegnazione di hello e Fare clic su hello **credenziali di aggiornamento** pulsante.

-   Se le proprie credenziali utente hello assegnata dispone hello utente **controllare toobe assicurarsi che la password è scaduto in un'applicazione hello** e in tal caso, **aggiornare la password scaduta** accedendo toohello applicazione direttamente.

   * Dopo aver aggiornata la password di hello in un'applicazione hello, richiedere hello di hello utente tooclick **aggiornare le credenziali** pulsante hello **riquadro dell'applicazione** in hello **app** sezione di hello [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) tooupdate li toohello più recente noto utilizza nome utente e password.

   * Se è o un altro assegnato hello credenziali per l'utente, utente hello o assegnazione di applicazioni del gruppo passando toohello **utenti e gruppi** scheda dell'applicazione hello, selezionando l'assegnazione di hello e Fare clic su hello **credenziali di aggiornamento** pulsante.

-   Hanno estensione browser hello utente aggiornamento hello accesso pannello seguendo procedure hello seguito hello [come tooinstall hello estensione Browser Pannello di accesso](#how-to-install-the-access-panel-browser-extension) sezione.

-   Verificare che l'estensione browser del Pannello di accesso hello sia in esecuzione e attivati nel browser dell'utente.

-   Verificare che gli utenti non siano cercando toosign nell'applicazione toohello dal Pannello di accesso hello durante in **modalità privata, inPrivate o incognito**. estensione del Pannello di accesso Hello non è supportata in queste modalità.

Nel caso in cui il problema persiste, potrebbe essere case hello che è stata modificata sul lato applicazione hello che è temporaneamente interrotta l'integrazione dell'applicazione hello con Azure AD. Ad esempio, ciò può verificarsi quando il fornitore dell'applicazione hello introduce uno script nella pagina che si comporta in modo diverso per vs manuale automatico di input, causando automatizzata integrazione, ad esempio nostro, toobreak. Fortunatamente, in molti casi, Microsoft può rivolgersi applicazione fornitori toorapidly risolvere questi problemi.

Microsoft ha tooautomatically tecnologie rilevare quando interrompere le integrazioni, ma in alcuni casi non è in grado di toofind questi problemi destro stoccaggio oppure richiederà un certo tempo toofix. In caso di hello quando uno di questi integrazioni non funziona correttamente, Gradiremmo se è stato aperto un caso di supporto in modo è possibile risolvere più rapidamente possibile.

In aggiunta toothis, **in contatto con il fornitore dell'applicazione, se si** **inviarli ritenuti utili** in modo da poter usare tali toonatively integrare le applicazioni con Azure Active Directory. È possibile inviare hello fornitore toohello [elenco l'applicazione nella raccolta di applicazioni per Azure Active Directory hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget li avviati.

## <a name="hello-extension-works-in-chrome-and-firefox-but-not-in-internet-explorer"></a>Hello estensione può essere utilizzata in Chrome e Firefox, ma non in Internet Explorer

Esistono due cause principali toothis problema:

-   A seconda delle impostazioni di sicurezza hello abilitate in Internet Explorer, se il sito Web di hello non è parte di un **attendibili**, in alcuni casi lo script venga impedito l'esecuzione di un'applicazione hello.

  *  tooresolve, indicare utente hello troppo**Aggiungi sito Web dell'applicazione hello** toohello **siti attendibili** elenco all'interno di loro **le impostazioni di sicurezza di Internet Explorer**. È possibile inviare il toohello utenti [come tooadd toomy un sito attendibile siti elenco](https://answers.microsoft.com/en-us/ie/forum/ie9-windows_7/how-do-i-add-a-site-to-my-trusted-sites-list/98cc77c8-b364-e011-8dfc-68b599b31bf5) articolo per informazioni dettagliate.

-   In rare circostanze, la convalida di sicurezza di Internet Explorer può talvolta causare tooload pagina hello più lento rispetto a esecuzione hello dello script.

   * Sfortunatamente, questa situazione può variare a seconda versione del browser hello, velocità del computer o al sito visitato. In questo caso, si consiglia di contattare il supporto in modo è possibile risolvere l'errore integrazione hello per questa applicazione specifica.

In aggiunta toothis, **in contatto con il fornitore dell'applicazione, se si** **inviarli ritenuti utili** in modo da poter usare tali toonatively integrare le applicazioni con Azure Active Directory. È possibile inviare hello fornitore toohello [elenco l'applicazione nella raccolta di applicazioni per Azure Active Directory hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget li avviati.

## <a name="check-if-hello-applications-login-page-has-changed-recently-or-requires-an-additional-field"></a>Controllare se hello pagina di accesso dell'applicazione è stato modificato di recente o richiede un campo aggiuntivo

Se la pagina di accesso dell'applicazione hello è cambiata drasticamente, talvolta in questo modo il nostro toobreak integrazioni. Un esempio è quando un fornitore dell'applicazione aggiunge un segno di campo, un captcha, o si verifica nel tootheir multi-factor authentication. Fortunatamente, in molti casi, Microsoft può rivolgersi applicazione fornitori toorapidly risolvere questi problemi.

Mentre Microsoft include le tecnologie tooautomatically rilevare quando interrompere le integrazioni, ma in alcuni casi non è in grado di toofind questi problemi sin da subito. In caso contrario hanno alcune toofix ora. In caso di hello quando uno di questi integrazioni non funziona correttamente, Gradiremmo apertura di un caso di supporto in modo è possibile risolvere più rapidamente possibile.

In aggiunta toothis, **in contatto con il fornitore dell'applicazione, se si** **inviarli ritenuti utili** in modo da poter usare tali toonatively integrare le applicazioni con Azure Active Directory. È possibile inviare hello fornitore toohello [elenco l'applicazione nella raccolta di applicazioni per Azure Active Directory hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget li avviati.

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Come tooinstall hello estensione Browser Pannello di accesso

hello tooinstall estensione Browser Pannello di accesso, le operazioni di hello seguenti:

1.  Aprire hello [Pannello di accesso](https://myapps.microsoft.com) in uno dei browser supportato hello e accedere come un **utente** in Azure AD.

2.  Fare clic su un **applicazione password SSO** in hello Pannello di accesso.

3.  Hello prompt dei comandi in cui viene chiesto tooinstall hello selezionare software **installa**.

4.  Basata sul browser è il collegamento di download toohello diretto. **Aggiungere** browser tooyour di estensione hello.

5.  Se il browser viene richiesto, selezionare tooeither **abilitare** o **Consenti** hello estensione.

6.  Al termine dell'installazione, **riavviare** la sessione del browser.

7.  Accedere in hello Pannello di accesso e di vedere se è possibile **avviare** applicazioni password SSO

È anche possibile scaricare l'estensione hello per Chrome e Firefox dai collegamenti diretti hello riportato di seguito:

-   [Estensione Pannello di accesso per Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Estensione Pannello di accesso per Firefox](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="next-steps"></a>Passaggi successivi
[Fornire le applicazioni single sign-on tooyour con Proxy dell'applicazione](active-directory-application-proxy-sso-using-kcd.md)

