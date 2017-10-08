---
title: aaaSet una verifica in due passaggi per l'account aziendale o dell'istituto di istruzione | Documenti Microsoft
description: "Quando la società Configura Azure multi-Factor Authentication, sarà richiesta toosign per verifica in due passaggi. Informazioni su come tooset, configurarlo. "
services: multi-factor-authentication
keywords: come toouse azure, active directory nel cloud hello, esercitazione di active directory
documentationcenter: 
author: kgremban
manager: femila
editor: pblachar
ms.assetid: 46f83a6a-dbdd-4375-8dc4-e7ea77c16357
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 2d0348081eefa42c23de2047044688879dcb5966
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-my-account-for-two-step-verification"></a>Configurare l'account per la verifica in due passaggi
Verifica in due passaggi è un passaggio di protezione aggiuntiva che consente di proteggere il tuo account, rendendo più difficile per toobreak altri utenti in. Se si sta leggendo questo articolo, probabilmente è stato ricevuto un messaggio di posta elettronica su Multi-Factor Authentication inviato dall'amministratore dell'azienda o dell'istituto di istruzione. O forse si tentato toosign in e ha ricevuto un messaggio che chiede tooset una verifica aggiuntiva di sicurezza. Se è questo caso di hello, **non è possibile accedere fino a completare il processo di autoregistrazione hello**.

Questo articolo consente di configurare l'**account aziendale o dell'istituto di istruzione**. Si verifica in due passaggi tooenable, un account Microsoft personale, vedere [sulla verifica in due passaggi](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).

## <a name="set-up-your-account"></a>Configurare l'account

Quando il reparto IT richiede toostart utilizzando la verifica in due passaggi, una dicitura schermata **l'amministratore ha richiesto di impostare questo account per la verifica aggiuntiva di sicurezza** viene visualizzato:

![Configurazione](./media/multi-factor-authentication-end-user-first-time/first.png)

tooget avviato, selezionare **configurarlo adesso.**

Se non viene visualizzata una schermata simile alla seguente quando si accede, seguire le direzioni di hello in [gestire le impostazioni per la verifica in due passaggi](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page) pagina Impostazioni di hello toofind in cui è possibile gestire le opzioni di verifica. 

## <a name="decide-how-you-want-tooverify-your-sign-ins"></a>Decidere come tooverify i controllo accessi

prima domanda di Hello nel processo di registrazione hello è quello desiderato ci toocontact è. Esaminare le opzioni di hello nella tabella hello e utilizzare i passaggi di installazione di hello collegamenti toogo toohello per ogni metodo.

| Metodo di contatto | Description |
| --- | --- |
| [App per dispositivi mobili](#use-a-mobile-app-as-the-contact-method) |- **Ricevi notifiche per la verifica.** Questa opzione inserisce un'app autenticatore di notifica toohello sul tablet o smartphone. Visualizzare la notifica di hello e, se legittima, selezionare **Authenticate** nell'app hello. L'azienda o dell'istituto di istruzione potrebbe richiedere di immettere un PIN prima eseguire l'autenticazione.<br>- **Usare il codice di verifica.** In questa modalità l'app autenticatore hello genera un codice di verifica che aggiorna ogni 30 secondi. Immettere il codice di verifica più recente hello in hello nell'interfaccia accesso.<br>è disponibile per app di Microsoft Authenticator Hello [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), e [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |
| [Chiamata o SMS sul telefono cellulare](#use-your-mobile-phone-as-the-contact-method) |- **Telefonata** inserisce un numero di telefono del toohello chiamata vocale automatizzata fornito. Risposta chiamata hello e premere # in hello phone tastierino tooauthenticate.<br>- **SMS** invia un SNS contenente un codice di verifica. In seguito hello prompt dei comandi in testo hello, toohello testo del messaggio di risposta o immettere il codice di verifica hello fornito hello sign nell'interfaccia. |
| [Chiamata telefonica dell'ufficio](#use-your-office-phone-as-the-contact-method) |Inserisce un numero di telefono del toohello chiamata vocale automatizzata fornito. Hello risposta chiamata e preme # hello phone tastierino tooauthenticate. |

## <a name="use-a-mobile-app-as-hello-contact-method"></a>Usare un'app per dispositivi mobili come metodo di contatto hello
L'uso di questo metodo richiede l'installazione di un'app di autenticazione sul telefono o sul tablet. Hello procedure in questo articolo sono basate sulle app Authenticator Microsoft hello, che è possibile [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), e [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).

1. Selezionare **app per dispositivi mobili** dall'elenco a discesa hello.
2. Selezionare l'opzione **Ricevi notifiche per la verifica** o **Use verification code** (Usa codice di verifica), quindi selezionare **Configura**.

   ![Schermata della verifica aggiuntiva di sicurezza](./media/multi-factor-authentication-end-user-first-time/mobileapp.png)

3. Nel telefono o tablet, aprire l'applicazione hello e selezionare  **+**  tooadd un account. (Nei dispositivi Android, selezionare hello tre punti, quindi **aggiungere account**.)
4. Specificare che si desidera tooadd un account aziendale o dell'istituto di istruzione. verrà visualizzata la finestra di scanner di codici a matrice Hello sul telefono. Se la fotocamera non funziona correttamente, è possibile selezionare tooenter le informazioni della società manualmente. Per ulteriori informazioni, vedere l'articolo su come [aggiungere manualmente un account](#add-an-account-manually).  
5. Immagine di codice a matrice hello che venivano visualizzate con la schermata Ciao per la configurazione delle app per dispositivi mobili hello di analisi.  Selezionare **eseguita** schermata di codice a matrice hello tooclose.  

   ![Schermata di codice QR](./media/multi-factor-authentication-end-user-first-time/scan2.png)

6. Al termine di attivazione sul telefono hello, selezionare **Contact me**.  Questo passaggio invia una notifica o un telefono tooyour codice di verifica. Selezionare **Verifica**.  
7. Se richiesto dall'azienda, immettere il PIN per approvare la verifica di accesso.

   ![Casella per l'immissione di un PIN](./media/multi-factor-authentication-end-user-first-time/scan3.png)

8. Al termine dell'immissione del PIN, selezionare **Chiudi**. A questo punto, la verifica avrà esito positivo.
9. È consigliabile immettere il numero di telefono cellulare in caso si perda l'accesso tooyour app per dispositivi mobili. Specificare il paese dall'elenco a discesa hello e immettere il numero di telefono cellulare in hello casella Avanti toohello nome del paese. Selezionare **Avanti**.
10. A questo punto, verrà richiesta tooset backup delle password di app per le app non basate su browser come Outlook 2010 o versioni precedenti, o app di posta elettronica native hello nei dispositivi di Apple. Questa azione avviene perché alcune app non supportano la verifica in due passaggi. Se non si utilizzano queste App, fare clic su **eseguita** e ignorare il resto di hello di questi passaggi.
11. Se si utilizza queste App, copia password di app hello fornito e incollarlo nell'applicazione anziché la password regolare. È possibile utilizzare hello stessa password di app per più applicazioni. Per altre informazioni, vedere [Guida alle password per le app].
12. Fare clic su **Done**.

### <a name="add-an-account-manually"></a>aggiungere manualmente un account
Se si desidera che un'app per dispositivi mobili toohello account tooadd manualmente, anziché utilizzando un lettore di hello QR, seguire questi passaggi.

1. Seleziona hello **immettere manualmente l'account** pulsante.  
2. Immettere il codice hello e l'URL di hello che vengono fornite in hello stessa pagina in cui viene hello codice a barre. Queste info va inserito nella hello **codice** e **URL** caselle hello app per dispositivi mobili.

    ![Configurazione](./media/multi-factor-authentication-end-user-first-time/barcode2.png)
3. Al termine dell'attivazione di hello, selezionare **Contact me**. Questo passaggio invia una notifica o un telefono tooyour codice di verifica. Selezionare **Verifica**.

## <a name="use-your-mobile-phone-as-hello-contact-method"></a>Utilizzo del cellulare come metodo di contatto hello
1. Selezionare **telefono per l'autenticazione** dall'elenco a discesa hello.  

    ![Configurazione](./media/multi-factor-authentication-end-user-first-time/phone.png)  
2. Scegliere il paese dall'elenco a discesa hello e immettere il numero di telefono cellulare.
3. Selezionare il metodo hello si preferisce toouse con il cellulare - SMS o telefonata.
4. Selezionare **Contact me** tooverify il numero di telefono. A seconda della modalità di hello selezionata, è inviarti un testo o chiamata. Seguire le istruzioni di hello fornite nella schermata di hello, quindi selezionare **verificare**.
5. A questo punto, verrà richiesta tooset backup delle password di app per le app non basate su browser come Outlook 2010 o versioni precedenti, o app di posta elettronica native hello nei dispositivi di Apple. Questa azione avviene perché alcune app non supportano la verifica in due passaggi. Se non si utilizzano queste App, fare clic su **eseguita** e ignorare hello passaggi restanti di hello.
6. Se si utilizza queste App, copia password di app hello fornito e incollarlo nell'applicazione anziché la password regolare. È possibile utilizzare hello stessa password di app per più applicazioni. Per altre informazioni, vedere [Guida alle password per le app].
7. Fare clic su **Done**.

## <a name="use-your-office-phone-as-hello-contact-method"></a>Usare il telefono dell'ufficio come metodo di contatto hello
1. Selezionare **telefono ufficio** dall'elenco a discesa hello  

    ![Configurazione](./media/multi-factor-authentication-end-user-first-time/office.png)  
2. casella numero di telefono Hello viene compilato automaticamente con le informazioni di contatto società. Se il numero di hello è errato o mancante, chiedere all'amministratore toomake modifiche.
3. Selezionare **Contact me** tooverify il numero di telefono e si chiamerà il numero. Seguire le istruzioni di hello fornite nella schermata di hello, quindi selezionare **verificare**.
4. A questo punto, verrà richiesta tooset backup delle password di app per le app non basate su browser come Outlook 2010 o versioni precedenti, o app di posta elettronica native hello nei dispositivi di Apple. Questa azione avviene perché alcune app non supportano la verifica in due passaggi. Se non si utilizzano queste App, fare clic su **eseguita** e ignorare hello passaggi restanti di hello.
5. Se si utilizza queste App, copia password di app hello fornito e incollarlo nell'applicazione anziché la password regolare. È possibile utilizzare hello stessa password di app per più applicazioni. Per altre informazioni, vedere [Che cosa sono le password per le app?](multi-factor-authentication-end-user-app-passwords.md).
6. Fare clic su **Done**.

## <a name="next-steps"></a>Passaggi successivi
* Modificare le opzioni desiderate e [gestire le impostazioni per la verifica in due passaggi](multi-factor-authentication-end-user-manage-settings.md)
* Impostare [password di app](multi-factor-authentication-end-user-app-passwords.md) per tutte le app di dispositivo native che non supportano la verifica in due passaggi.
* Estrarre hello [app Authenticator Microsoft](microsoft-authenticator-app-how-to.md) per fast, autenticazione sicura anche quando non è disponibile il servizio di cella.

