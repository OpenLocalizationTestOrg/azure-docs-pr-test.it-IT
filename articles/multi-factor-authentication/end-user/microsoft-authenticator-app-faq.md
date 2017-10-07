---
title: app Authenticator aaaMicrosoft Guida e supporto tecnico | Documenti Microsoft
description: Fornisce un elenco di domande e risposte app Microsoft Authentication toohello correlati e Azure multi-Factor Authentication.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f04d5bce-e99e-4f75-82d1-ef6369be3402
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: afba9b59ccaac60d022e8516fcf573dcfbf68af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-authenticator-app-faq"></a>Domande frequenti sull'app Microsoft Authenticator

In questo articolo risposte a domande comuni che è stata ricevuta su app Microsoft Authenticator hello. Se non viene visualizzata una domanda tooyour risposta, visitare toohello [forum app Microsoft Authenticator](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp). È necessario anche un altro domande frequenti su una funzionalità specifica sull'app hello, [l'accesso con le domande frequenti su telefono](microsoft-authenticator-app-phone-signin-faq.md).

app Microsoft Authenticator Hello sostituito app Azure Authenticator hello e hello consiglia app quando si usa Azure multi-Factor Authentication. è disponibile per app di Microsoft Authenticator Hello [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), e [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).

## <a name="frequently-asked-questions"></a>Domande frequenti

### <a name="what-are-hello-codes-in-hello-app-for-why-does-hello-number-keep-counting-down"></a>Quali sono i codici di hello in app hello per? Perché numero hello mantenere rovescia?

Quando si apre l'app Microsoft Authenticator hello, vengono visualizzati gli account di hello aggiunti e un numero di sei o otto cifre da ciascuno di essi. Può essere presente anche un timer di trenta secondi che procede a ritroso.

Questi codici vengono utilizzati quando si accede tooyour account. Dopo avere immesso nome utente e password, potrebbe essere richiesto tooenter un codice di verifica. Aprire hello Microsoft Authenticator app e copiare hello codice attualmente visualizzato. Immettere il codice in hello toofinish di pagina di accesso.

motivo di Hello hello codici modifica ogni 30 secondi in modo che non viene mai utilizzato hello stesso codice due volte. Non è ad esempio una password che si sta deve tooremember. l'idea Hello è che solo un utente con phone tooyour di accesso sa che il codice di verifica.

codici di Hello non richiedono internet o dati, non vi è tooworry che toosign servizio telefonico. Quando si chiude l'applicazione hello, che non mantenere in esecuzione in background hello e non Svuota la batteria. È possibile chiudere l'applicazione hello e Ignora finché hello successivo che si accede.  

### <a name="i-only-get-notifications-when-i-have-hello-app-open-if-hello-app-isnt-open-i-dont-get-any-notifications"></a>Le notifiche viene visualizzata solo quando si dispone di app hello aprire. Se l'applicazione hello non è aperta, non viene visualizzato di tutte le notifiche.

Se ricevere le notifiche, ma non apportare rumore o vibrare nonostante la suoneria si trova su, controllare innanzi tutto le impostazioni dell'app hello. Abilita audio di hello app toouse o vibrare con le notifiche.

Se si non ricevere le notifiche del tutto, verificare hello seguenti casi:

- Il telefono è in modalità non disturbare o non interattiva? Tale modalità può impedire l'invio di notifiche da parte delle app.
- Si ricevono notifiche da altre app? In caso contrario, potrebbe esserci un problema con le connessioni di rete hello dal proprio telefono, o canale notifiche hello da Android o Apple. È possibile risolvere prima opzione hello nelle impostazioni del telefono, ma potrebbe essere necessario tootalk tooyour provider di servizi per informazioni su come seconda opzione hello.
- È possibile ricevere notifiche per alcuni account su app hello, ma non altri? In caso affermativo, rimuovere l'account problematico hello dall'app e aggiungerlo di nuovo le notifiche push tooenable. 

Se i problemi persistono anche dopo aver provato questi suggerimenti, inviare i log per la diagnostica. Passare le impostazioni dell'app toohello, quindi selezionare **Guida e commenti e suggerimenti** e **inviare i log**. Quindi, passare toohello [forum app Microsoft Authenticator](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp) e indicare quali problemi vengono visualizzati e le procedure da sperimentate finora. 

### <a name="im-already-using-hello-microsoft-authenticator-application-for-verification-codes-how-do-i-switch-tooone-click-push-notifications"></a>Si sta già utilizzando hello applicazione Authenticator di Microsoft per i codici di verifica. Come passare le notifiche push tooone-fare clic su?
L'approvazione dell'accesso tramite notifica push è disponibile solo per account Microsoft personali o account Microsoft aziendali o dell'istituto di istruzione, non per account di terze parti come Google o Facebook. Se si dispone di un lavoro o scuola account Microsoft, l'organizzazione può scegliere toodisable questa opzione.

Se si utilizza un account Microsoft per l'account personale e si desidera tooswitch sulla toopush notifiche, è necessario tooadd account nuovamente. Registrare nuovamente il dispositivo hello con l'account e impostare le notifiche push.  

Se si utilizza Microsoft Authenticator per l'account aziendale o dell'istituto di istruzione, quindi si decide se le notifiche di tooallow un solo clic.

### <a name="do-one-click-push-notifications-work-for-non-microsoft-accounts"></a>Le notifiche push con un clic funzionano con gli account non Microsoft?
No, le notifiche push funzionano solo con gli account Microsoft e gli account Azure Active Directory. Se l'azienda o l'istituto di istruzione usa account di Azure AD, è possibile che disabilitino questa funzionalità.  

### <a name="i-restored-my-device-from-a-backup-and-my-account-codes-are-missing-or-not-working-what-happened"></a>Ho ripristinato il mio dispositivo da una copia di backup e i codici del mio account mancano o non funzionano. Che cosa è successo?
A scopo di sicurezza, gli account non vengono ripristinati dalle copie di backup dell'app.  Dopo aver ripristinato l'applicazione hello, eliminare gli account e aggiungerli nuovamente.

### <a name="i-got-a-new-device-how-do-i-remove-hello-microsoft-authenticator-app-from-my-old-device-and-move-toohello-new-one"></a>Ho un nuovo dispositivo. Come rimuovere app Microsoft Authenticator hello dal mio dispositivo precedente e spostare toohello uno nuovo?
Aggiunta hello Microsoft Authenticator app tooa nuova periferica non automaticamente rimuoverlo da tutti gli altri dispositivi. toomanage quali dispositivi sono configurati per l'account, visitare hello stesso sito Web, utilizzare verifica in due passaggi toomanage e scegliere tooremove App precedente.

Per gli account Microsoft personali, il sito Web è la pagina della [sicurezza dell'account](https://account.microsoft.com/security). Per gli account Microsoft aziendali o dell'istituto di istruzione, il sito Web può essere [Mie app](https://myapps.microsoft.com) o un portale personalizzato configurato dall'organizzazione.

### <a name="how-do-i-remove-an-account-from-hello-app"></a>Come si rimuove un account dall'app hello?
* iOS: dalla schermata principale hello, Scorri rapidamente verso sinistra in un riquadro dell'account. Selezionare **Elimina**.
* Windows Phone: Dalla schermata principale hello, selezionare il pulsante di menu hello, quindi **modificare gli account**. Toccare hello **X** nome di account toohello successivo.
* Android: Dalla schermata principale hello, selezionare il pulsante di menu hello, quindi **modificare gli account**. Toccare hello **X** nome di account toohello successivo.

Se si dispone di un dispositivo è registrato con l'organizzazione, potrebbe essere necessario toocomplete tooremove un passaggio aggiuntivo all'account. In questi dispositivi, app di Microsoft Authenticator hello viene registrato automaticamente come amministratore del dispositivo. Se si desidera toocompletely Disinstalla hello app, è necessario toofirst app hello nelle impostazioni dell'app hello di annullare la registrazione.

### <a name="why-does-hello-app-request-so-many-permissions"></a>Perché richiedere autorizzazioni così tante app hello?
Ecco un elenco completo delle autorizzazioni che può essere richiesta, e come vengono usati in app hello. autorizzazioni specifiche di Hello visualizzati dipendono dal tipo di hello del telefono, che si dispone.

* **Fotocamera**: utilizziamo un codice QR tooscan fotocamera quando si aggiunge un lavoro, dell'istituto di istruzione o l'account non Microsoft.
* **Contatti e phone**: quando si accede con l'account Microsoft personale, si tenta di processo hello toosimplify mediante la ricerca di account in uso sul telefono.
* **SMS**: quando si accede con l'account Microsoft personale per hello prima volta, è necessario assicurarsi che le corrispondenze di numeri di telefono hello uno presente nel record toomake. Si invia un telefono toohello messaggio di testo in cui è stato scaricato app hello. messaggio contiene un codice di verifica cifra 6-8. Invece chiesto toofind questo codice, immetterlo nell'app hello è trovata automaticamente nel messaggio di testo hello.
* **Disegnare su altre app**: quando si riceve una notifica tooverify la tua identità, viene visualizzata la notifica su qualsiasi altra applicazione che potrebbe essere in esecuzione.
* **Ricevere i dati da hello internet**: questa autorizzazione è necessaria per l'invio di notifiche.
* **Impedire la sospensione del telefono**: se si registra il dispositivo con l'organizzazione, è possibile modificare questo criterio sul telefono.
* **Controllo vibrazione**: È possibile scegliere se si desidera una vibrazione ogni volta che si riceve una notifica tooverify la tua identità.
* **Uso dell'hardware per la lettura delle impronte digitali**: alcuni account aziendali e dell'istituto di istruzione richiedono un PIN aggiuntivo al momento della verifica dell'identità. toomake hello processo più semplice, si consente toouse l'impronta digitale anziché immettere hello PIN.
* **Visualizzare le connessioni di rete**: quando si aggiunge un account Microsoft, hello app richiede la connessione di rete o internet.
* **Leggere il contenuto di hello dello spazio di archiviazione**: questa autorizzazione viene utilizzata solo quando si segnala un problema tecnico tramite le impostazioni dell'app hello. Alcuni raccolti dall'archivio problema hello toodiagnose.
* **Accesso di rete completo**: questa autorizzazione è necessaria per l'invio di notifiche tooverify la tua identità.
* **Eseguire all'avvio**: se si riavvia il telefono, questa autorizzazione garantisce di continuare si riceve notifiche tooverify la tua identità.

### <a name="why-does-hello-microsoft-authenticator-app-allow-you-tooapprove-a-request-without-unlocking-hello-device"></a>Perché hello App Authenticator Microsoft consente tooapprove una richiesta senza lo sblocco dispositivo hello?

Non è necessario toounlock che la verifica di tooapprove dispositivo le richieste in quanto è sufficiente tooprove è che sia il telefono con l'utente. La verifica in due passaggi richiede di dimostrare di conoscere una determinata informazione e di essere in possesso di qualcosa, cosa Hello che si conosce è la password. cosa Hello è telefono (impostato con l'app Microsoft Authenticator hello e registrato come un'autenticazione a più fattori di prova). Pertanto, con phone hello e approvazione richiesta di hello soddisfa hello criteri per il secondo fattore di autenticazione di hello. 

### <a name="what-does-hello-lock-icon-in-hello-account-list-mean"></a>Icona di blocco hello nell'elenco di account hello cosa?

icona del lucchetto Hello indica che il dispositivo hello viene registrato in Azure AD e registrate toohello account. La registrazione del dispositivo per iOS avviene durante l'enrollment di Microsoft Intune.

## <a name="next-steps"></a>Passaggi successivi

### <a name="contact-us"></a>Contatti
Se la domanda non è stato risposto qui, è opportuno toohear da parte dell'utente. Passare toohello [forum app Microsoft Authenticator](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp) toopost la domanda e get Guida dalla community di hello o lasciare un commento in questa pagina.


### <a name="related-topics"></a>Argomenti correlati
* [Informazioni sulla verifica in due passaggi](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification) per l'account Microsoft
* [Problemi con la verifica in due passaggi](multi-factor-authentication-end-user-troubleshoot.md) per un account aziendale o dell'istituto di istruzione
* [Utilizzare toosign Microsoft Authenticator di hello dal telefono](microsoft-authenticator-app-phone-signin-faq.md)

