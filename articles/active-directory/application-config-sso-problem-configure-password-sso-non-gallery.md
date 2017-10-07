---
title: configurazione delle password single sign-on per un'applicazione non raccolta aaaProblem | Documenti Microsoft
description: Comprendere faccia persone problemi comuni di hello quando si configura Password Single Sign-on per le applicazioni non raccolta personalizzate che non sono elencate in hello raccolta di applicazioni Azure AD
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
ms.openlocfilehash: 3aee0a4c525bb3da338da2da0882ec572cf0e5e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a>Problema nella configurazione dell'accesso Single Sign-On basato su password per un'applicazione non inclusa nella raccolta

Questo articolo è utile faccia di persone di toounderstand hello comuni problemi quando si configura **Password single sign-on** con un'applicazione non raccolta.

## <a name="how-toocapture-sign-in-fields-for-an-application"></a>Accedi toocapture come campi di un'applicazione

L'acquisizione dei campi di accesso è supportata solo per le pagine di accesso basate su HTML e **non è supportata per le pagine di accesso non standard**, ad esempio le pagine che usano Flash o altre tecnologie non basate su HTML.

Esistono due modi per acquisire i campi di accesso per le applicazioni personalizzate:

-   Acquisizione automatica dei campi di accesso

-   Acquisizione manuale dei campi di accesso

**Acquisizione di campo accesso automatico** funziona correttamente con la maggior parte delle abilitato HTML delle pagine di accesso, se si utilizza **ID DIV noti hello username e password di input** campo. Hello pratica è da scraping hello HTML nella pagina di hello toofind ID DIV che corrispondono a determinati criteri e salvando quindi che i metadati per questa applicazione, pertanto è possibile riprodurre tooit le password in un secondo momento.

**Acquisizione manuale Accedi campo** può essere usata in caso di hello che hello applicazione **fornitore non etichetta** hello input campi utilizzati per l'accesso. Acquisizione manuale Accedi campo può essere usata anche in caso di hello quando hello **fornitore esegue il rendering di più campi** che non può essere rilevata automaticamente. Azure AD possono archiviare i dati per come firma un numero di campi si trovano in hello nella pagina, purché si informazioni in tali campi sono nella pagina hello.

In generale, **se acquisizione campo accesso automatico non funziona, è sempre consigliabile opzione manuale di hello durante il tentativo.**

### <a name="how-tooautomatically-capture-sign-in-fields-for-an-application"></a>Come tooautomatically acquisire i campi di accesso per un'applicazione

tooconfigure **basato su Password Single Sign-on** per un'applicazione mediante **acquisizione automatica Accedi campo**, attenersi alla procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

  * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello tooconfigure single sign-on.

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Modalità di selezione hello **basato su Password Sign-on.**

9.  Immettere hello **Sign-on URL**. Si tratta hello URL in cui gli utenti immettono il nome utente e password toosign in a. **Verificare che i campi di accesso hello siano visibili nell'URL hello è fornire**.

10. Fare clic su hello **salvare** pulsante.

11. Una volta tale scopo, si verrà automaticamente cercare come URL per un nome utente e password casella di input e consentono di toouse AD Azure toosecurely trasmettere applicazione toothat le password utilizzando l'estensione browser del Pannello di accesso hello.

## <a name="how-toomanually-capture-sign-in-fields-for-an-application"></a>Come toomanually acquisire i campi di accesso per un'applicazione

toomanually acquisizione i campi di accesso, è necessario aver installato estensione Browser Pannello di accesso di hello e **non sia in esecuzione in modalità inPrivate, incognito o private.** estensione del browser di hello tooinstall, seguire la procedura seguente hello in hello [come tooinstall hello estensione Browser Pannello di accesso](#i-cannot-manually-detect-sign-in-fields-for-my-application) sezione.

tooconfigure **basato su Password Single Sign-on** per un'applicazione mediante **acquisizione manuale Accedi campo**, attenersi alla procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

   * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello tooconfigure single sign-on.

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Modalità di selezione hello **basato su Password Sign-on.**

9.  Immettere hello **Sign-on URL**. Si tratta hello URL in cui gli utenti immettono il nome utente e password toosign in a. **Verificare che i campi di accesso hello siano visibili nell'URL hello è fornire**.

10. Fare clic su hello **salvare** pulsante.

11. Una volta tale scopo, si verrà automaticamente cercare come URL per un nome utente e password casella di input e consentono di toouse AD Azure toosecurely trasmettere applicazione toothat le password utilizzando l'estensione browser del Pannello di accesso hello. In caso di hello che l'operazione non riesce, è possibile **hello Accedi modalità toouse manuale Accedi campo acquisizione delle modifiche** continuando toostep 12.

12. Fare clic su **Configura impostazioni Password Single Sign-On per &lt;nomeapp&gt;**.

13. Seleziona hello **rilevare manualmente Accedi campi** opzione di configurazione.

14. Fare clic su **OK**.

15. Fare clic su **Salva**.

16. Seguire hello schermata istruzioni toouse hello Pannello di accesso.

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a>Errore "Non sono stati trovati campi di accesso nell'URL specificato"

Questo errore viene visualizzato quando il rilevamento automatico dei campi di accesso ha esito negativo. Questo problema, provare manuale Accedi campo rilevamento da hello seguendo i passaggi in hello tooresolve [come toomanually acquisire i campi di accesso per un'applicazione](#how-to-manually-capture-sign-in-fields-for-an-application) sezione.

## <a name="i-see-an-unable-toosave-single-sign-on-configuration-error"></a>Viene visualizzato un errore di "configurazione Single Sign-on non è possibile toosave"

In alcuni casi rari, l'aggiornamento della configurazione hello single sign-on può avere esito negativo. tooresolve questo provare a salvare hello configurazione single sign-on nuovamente.

Se il problema persiste toofail in modo coerente, assistenza al supporto tecnico e fornire informazioni di hello raccolte in hello [come dettagli di hello toosee di una notifica tramite il portale](#i-cannot-manually-detect-sign-in-fields-for-my-application) e [come la Guida mediante l'invio di notifiche dettagli tooa tooget il supporto tecnico](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sezioni.

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a>Non è possibile rilevare manualmente i campi di accesso per l'applicazione

Alcuni dei comportamenti hello che si potrebbero verificare quando il rilevamento manuale non funziona:

-   il processo di acquisizione manuale di Hello sembrava toowork, ma i campi di hello acquisiti non sono corretti

-   Hello destra campi non vengono evidenziati quando si esegue il processo di acquisizione hello

-   il processo di acquisizione Hello viene visualizzata la pagina di accesso dell'applicazione toohello come previsto, ma non accade nulla

-   Acquisizione manuale visualizzata toowork SSO non verificarsi quando gli utenti visitano toohello applicazione hello Pannello di accesso.

Se si verifica uno di questi problemi, verificare i seguenti di hello:

-   Verificare di disporre di più recente dell'estensione del browser del Pannello di accesso hello hello **installato** e **abilitato** seguendo procedure hello hello [come tooinstall hello Browser Pannello di accesso estensione](#how-to-install-the-access-panel-browser-extension) sezione.

-   Verificare che non si stia tentando il processo di acquisizione hello durante il browser **modalità privata, inPrivate o incognito**. estensione del Pannello di accesso Hello non è supportata in queste modalità.

-   Verificare che gli utenti non siano cercando toosign nell'applicazione toohello dal Pannello di accesso hello durante in **modalità privata, inPrivate o incognito**. estensione del Pannello di accesso Hello non è supportata in queste modalità.

-   Riprovare il processo di acquisizione manuale di hello, verifica i marcatori di hello rosso sono campi corretti hello.

-   Se il processo di acquisizione manuale di hello sembra toohang, o pagina di accesso hello non esegue alcuna operazione (caso 3 sopra), riprovare il processo di acquisizione manuale di hello. Ma questa volta dopo aver completato il processo di hello, premere hello **F12** pulsante tooopen console per sviluppatori del browser. Una volta, aprire hello **console** e tipo **window.location= "&lt;immettere hello sign in url specificato quando si configura l'applicazione hello&gt;"** e quindi premere  **Immettere**. Questa forza una pagina di reindirizzamento cui terminare il processo di acquisizione hello e archiviare hello campi che sono stati acquisiti.

Se nessuno di questi approcci risolve il problema, rivolgersi al supporto Microsoft. Assistenza al supporto tecnico con i dettagli di hello di ciò che si è tentato, nonché informazioni hello raccolte in hello [come dettagli di hello toosee di una notifica tramite il portale](#i-cannot-manually-detect-sign-in-fields-for-my-application) e [informazioni tooget inviando i dettagli sulla notifica tooa supporto tecnico](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sezioni (se applicabile).

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Come tooinstall hello estensione Browser Pannello di accesso

hello tooinstall estensione Browser Pannello di accesso, le operazioni di hello seguenti:

1.  Aprire hello [Pannello di accesso](https://myapps.microsoft.com) in uno dei browser supportato hello e accedere come un **utente** in Azure AD.

2.  Fare clic su un **applicazione password SSO** in hello Pannello di accesso.

3.  Hello prompt dei comandi in cui viene chiesto tooinstall hello selezionare software **installa**.

4.  Basata sul browser è il collegamento di download toohello diretto. **Aggiungere** browser tooyour di estensione hello.

5.  Se il browser viene richiesto, selezionare tooeither **abilitare** o **Consenti** hello estensione.

6.  Al termine dell'installazione, **riavviare** la sessione del browser.

7.  Accedere in hello Pannello di accesso e di vedere se è possibile **avviare** applicazioni password SSO.

È anche possibile scaricare l'estensione hello per Chrome e Firefox dai collegamenti diretti hello riportato di seguito:

-   [Estensione Pannello di accesso per Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Estensione Pannello di accesso per Firefox](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-toosee-hello-details-of-a-portal-notification"></a>Modalità dettagli hello toosee di una notifica del portale

È possibile visualizzare i dettagli di hello di qualsiasi notifica tramite il portale seguendo i passaggi di hello riportati di seguito:

1.  Fare clic su hello **notifiche** icona (campana hello) in alto a destra hello di hello portale di Azure

2.  Selezionare qualsiasi notifica in un **errore** stato (quelli con un toothem Avanti rosso (!)).

  >!NOTA] Non è possibile fare clic sulle notifiche in uno stato di **Operazione completata** o **In corso**.
  >
  >

3.  Questo hello aprire **i dettagli sulla notifica** blade.

4.  Utilizzare queste informazioni manualmente toounderstand ulteriori dettagli sul problema hello.

5.  Se è ancora necessario della Guida, è possibile condividere queste informazioni con il problema con un supporto tecnico o hello gruppo tooget Guida del prodotto.

6.  Fare clic su hello **copia** **icona** toohello diritto di hello **copiare errore** toocopy textbox tutti hello tooshare dettagli di notifica con un ingegnere del supporto o il prodotto gruppo.

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a>Informazioni tooget inviando al supporto tecnico tooa dettagli di notifica

È molto importante che si condivide **tutti hello dettagli riportati di seguito** con un supporto tecnico per assistenza, in modo che tali eventi consentono rapidamente. Tale scopo, **acquisire uno screenshot,** o facendo clic su hello **sull'icona di errore di copia**, trovato toohello destra di hello **copiare errore** casella di testo.

## <a name="notification-details-explained"></a>Spiegazione dei dettagli della notifica

Hello seguente illustra più quali tutti gli elementi hello notifica significa e fornisce esempi di ognuno di essi.

### <a name="essential-notification-items"></a>Elementi essenziali della notifica

-   **Titolo** : hello titolo descrittivo della notifica hello

    -   Esempio: **Impostazioni proxy di applicazione**

-   **Descrizione** : hello descrizione di ciò che si è verificato in seguito a operazione hello

    -   Esempio: **L'URL interno immesso è già usato da un'altra applicazione**

-   **Id di notifica** : id univoco di hello della notifica hello

    -   Esempio: **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**

-   **Id richiesta client** : id richiesta specifico hello apportate dal browser

    -   Esempio: **302fd775-3329-4670-a9f3-bea37004f0bc**

-   **Ora UTC timbro** : hello timestamp durante il quale la notifica hello si è verificato, in formato UTC

    -   Esempio: **2017-03-23T19:50:43.7583681Z**

-   **Id della transazione interna** : hello ID interno, è possibile utilizzare l'errore hello toolook nei nostri sistemi

    -   Esempio: **71a2f329-ca29-402f-aa72-bc00a7aca603**

-   **UPN** – utente hello che ha eseguito l'operazione di hello

    -   Esempio: **tperkins@f128.info**

-   **Id tenant** : hello ID univoco del tenant hello che hello utente che ha eseguito l'operazione di hello è un membro di

    -   Esempio: **7918d4b5-0442-4a97-be2d-36f9f9962ece**

-   **L'Id di oggetto utente** : hello ID univoco dell'utente di hello che ha eseguito l'operazione di hello

    -   Esempio: **17f84be4-51f8-483a-b533-383791227a99**

### <a name="detailed-notification-items"></a>Elementi della notifica dettagliati

-   **Nome visualizzato** – **(può essere vuoto)** un nome di visualizzazione più dettagliato per correggere l'errore hello

    -   Esempio*: **impostazioni del proxy di applicazione**

-   **Stato** : hello specifico stato di notifica di hello

    -   Esempio*: **Operazione non riuscita**

-   **Id di oggetto** – **(può essere vuoto)** hello ID di oggetto su cui hello è stata eseguita l'operazione

    -   Esempio: **8e08161d-f2fd-40ad-a34a-a9632d6bb599**

-   **Dettagli** : hello descrizione dettagliata dell'accaduto come risultato di operazione hello

    -   Esempio: **L'URL interno "http://bing.com/" non è valido perché è già in uso**

-   **Copiare l'errore** – fare clic su hello **sull'icona Copia** toohello diritto di hello **copiare errore** toocopy textbox tutti hello tooshare dettagli di notifica con un ingegnere del supporto o il prodotto gruppo

    -   Esempio: ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```

## <a name="next-steps"></a>Passaggi successivi
[Fornire le applicazioni single sign-on tooyour con Proxy dell'applicazione](active-directory-application-proxy-sso-using-kcd.md)

