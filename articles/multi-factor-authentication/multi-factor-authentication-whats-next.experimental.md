---
title: Azure MFA aaaConfigure | Documenti Microsoft
description: "Si tratta hello Azure multi-factor authentication pagina che descrive quale toodo successivamente con autenticazione a più fattori.  Sono inclusi i report, gli avvisi di illecito, il bypass monouso, i messaggi vocali personalizzati, la memorizzazione nella cache, gli indirizzi IP attendibili e le password dell'app."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 75af734e-4b12-40de-aba4-b68d91064ae8
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: kgremban
ms.openlocfilehash: db7d87d95b73fed78d3ce599fd03da9692851663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-settings"></a>Configurare le impostazioni di Azure Multi-Factor Authentication
Le informazioni in questo articolo sono utili per gestire Azure Multi-Factor Authentication ora che si è operativi.  Vengono illustrate vari argomenti che consentono di hello tooget meglio Azure multi-Factor Authentication.  Non tutte queste funzionalità sono disponibili in ogni versione di Azure Multi-Factor Authentication.

| Funzionalità | Descrizione | 
|:--- |:--- |
| [Avviso di illecito](#fraud-alert) |Avviso di illecito può essere configurato e impostare in modo che gli utenti possono segnalare tentativi fraudolenti tooaccess le proprie risorse. |
| [Bypass monouso](#one-time-bypass) |Un bypass monouso consente tooauthenticate un utente di una sola volta "ignorando" multi-factor authentication. |
| [Messaggi vocali personalizzati](#custom-voice-messages) |I messaggi vocali personalizzati consentono di toouse registrazioni o personali greetings con multi-factor authentication. |
| [Memorizzazione nella cache](#caching-in-azure-multi-factor-authentication) |La memorizzazione nella cache consente tooset un periodo di tempo specifico in modo che i tentativi di autenticazione successivi esito positivo automaticamente. |
| [Indirizzi IP attendibili](#trusted-ips) |Gli amministratori di un tenant gestito o federato possono utilizzare gli indirizzi IP attendibili toobypass la verifica per gli utenti che accedono dalla rete intranet locale della società hello. |
| [Password dell'app](#app-passwords) |Una password di app consente a un'applicazione che non è compatibile con autenticazione a più fattori toobypass l'autenticazione a più fattori e continua a lavorare. |
| [Memorizzare Multi-Factor Authentication per dispositivi e browser memorizzati](#remember-multi-factor-authentication-for-devices-that-users-trust) |Consente di dispositivi tooremember per un numero prefissato di giorni dopo che un utente ha effettuato l'accesso con autenticazione a più fattori. |
| [Metodi di verifica selezionabili](#selectable-verification-methods) |Consente di metodi di autenticazione hello toochoose disponibili per gli utenti toouse. |

## <a name="access-hello-azure-mfa-management-portal"></a>Accedere hello portale di gestione di Azure MFA

funzionalità Hello trattate in questo articolo vengono configurate nel portale di gestione di Azure multi-Factor Authentication hello. Esistono due modi tooaccess hello portale di gestione di autenticazione a più fattori tramite hello portale di Azure classico. Hello viene innanzitutto mediante la gestione di un Provider multi-Factor Authentication. in secondo luogo, Hello è tramite le impostazioni del servizio di autenticazione a più fattori hello. 

### <a name="use-an-authentication-provider"></a>Usare un provider di autenticazione

Se si utilizza un Provider multi-Factor Authentication per MFA in base al consumo, tramite il portale di gestione di metodo tooaccess hello.

tooaccess hello portale di gestione di autenticazione a più fattori tramite un Provider di Azure multi-Factor Authentication, accedere a hello portale di Azure classico come amministratore e opzione di hello selezionare Active Directory. Fare clic su hello **provider multi-Factor Authentication** scheda, quindi selezionare la directory e fare clic su hello **Gestisci** pulsante nella parte inferiore di hello.

### <a name="use-hello-mfa-service-settings-page"></a>Pagina Impostazioni servizio di autenticazione a più fattori hello 

Se si dispone di uno dei seguenti licenze hello, è possibile utilizzare una pagina di impostazioni di servizio di autenticazione a più fattori hello:
- Azure MFA
- Azure AD Premium 
- Enterprise Mobility + Security

tooaccess hello portale di gestione di autenticazione a più fattori tramite la pagina di impostazioni di servizio di autenticazione a più fattori, accedere al portale di Azure classico come amministratore hello hello e selezionare l'opzione di hello Active Directory. Fare clic sul nome della directory e quindi fare clic su hello **configura** scheda. Hello multi-factor authentication, selezionare nella sezione **Gestisci impostazioni servizio**. Nella parte inferiore di hello della pagina di impostazioni di servizio di autenticazione a più fattori hello, fare clic su hello **Go toohello portale** collegamento.


## <a name="fraud-alert"></a>Avviso di illecito
Avviso di illecito può essere configurato e impostare in modo che gli utenti possono segnalare tentativi fraudolenti tooaccess le proprie risorse.  Gli utenti possono segnalare gli illeciti con l'app per dispositivi mobili hello o tramite telefono.

### <a name="set-up-fraud-alert"></a>Configurare un avviso di illecito
1. Passare toohello il portale di gestione di autenticazione a più fattori per le istruzioni di hello nella parte superiore di hello di questa pagina.
2. Nel portale di gestione di Azure multi-Factor Authentication hello, fare clic su **impostazioni** nella sezione Configurazione hello.
3. Nella sezione avviso illecito della pagina Impostazioni hello hello, controllare hello **consentire agli utenti avvisi di illeciti toosubmit** casella di controllo.
4. Selezionare **salvare** tooapply le modifiche. 

### <a name="configuration-options"></a>Opzioni di configurazione

- **Blocca utente se viene segnalato un illecito**: se un utente segnala un illecito, il relativo account viene bloccato.
- **Codice illecito durante il messaggio introduttivo iniziale tooReport** -gli utenti in genere premono verifica di # tooconfirm in due passaggi. Se tooreport illecito, immette un codice prima di premere #. Il codice predefinito è **0**, ma è possibile personalizzarlo.

> [!NOTE]
> I messaggi vocali predefinita di Microsoft, indicare agli utenti toopress # 0 toosubmit un avviso di illecito. Se si desidera toouse un codice diverso da 0, è necessario registrare e caricare i propri messaggi vocali personalizzati con le istruzioni appropriate.

![Screenshot delle opzioni di Avviso di illecito](./media/multi-factor-authentication-whats-next/fraud.png)

### <a name="how-users-report-fraud"></a>Segnalazione di illeciti da parte degli utenti 
Gli avvisi di illecito possono essere segnalati in due modi:  Tramite l'app per dispositivi mobili hello o tramite telefono hello.  

#### <a name="report-fraud-with-hello-mobile-app"></a>Segnalazione di frodi con hello app per dispositivi mobili
1. Telefono tooyour viene inviata una verifica, selezionare la tooopen hello Microsoft Authenticator app.
2. Selezionare **Deny** notifica hello. 
3. Selezionare **Segnala illecito**.
4. Chiudi hello app.

#### <a name="report-fraud-with-a-phone"></a>Segnalare un illecito tramite il telefono
1. Quando una chiamata di verifica tooyour telefono, è necessario rispondere.  
2. tooreport illecito, immettere codice illecito hello (valore predefinito è 0) e quindi hello simbolo #. Viene quindi segnalato che è stato inviato un avviso di illecito.
3. Terminare la chiamata hello.

### <a name="view-fraud-reports"></a>Visualizzare le segnalazioni di illeciti
1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Hello sinistra, selezionare Active Directory.
3. Nella parte superiore di hello, selezionare **provider multi-Factor Authentication** tooshow un elenco dei provider multi-Factor Authentication.
4. Selezionare il Provider di multi-Factor Authentication e fare clic su **Gestisci** nella parte inferiore di hello della pagina hello. verrà visualizzata la finestra di Hello portale di gestione di Azure multi-Factor Authentication.
5. Hello Azure multi-Factor Authentication portale di gestione, in visualizzazione Report, scegliere **avviso illecito**.
6. Specificare l'intervallo di date hello che si desidera tooview nel report hello. È anche possibile specificare i nomi utente, i numeri di telefono e hello lo stato utente.
7. Fare clic su **eseguire** tooshow un report degli avvisi di illecito. Fare clic su **esportare tooCSV** se si desidera tooexport hello report.

## <a name="one-time-bypass"></a>Bypass monouso
Un bypass monouso consente una sola volta tooauthenticate un utente senza eseguire una verifica in due passaggi. Hello bypass è temporaneo e scade dopo un numero di secondi specificato. In situazioni in cui app per dispositivi mobili hello o il telefono non riceve una notifica o una chiamata telefonica, è possibile attivare un bypass monouso pertanto utente hello può accedere a risorse hello desiderato.

### <a name="create-a-one-time-bypass"></a>Creare un bypass monouso
1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Passare toohello il portale di gestione di autenticazione a più fattori per le istruzioni di hello nella parte superiore di hello di questa pagina.
3. Se viene visualizzato il nome di hello del Provider di autenticazione a più fattori di Azure in hello sinistra con un  **+**  tooit Avanti, fare clic su hello  **+** . Vengono visualizzati i gruppi di replica diversi Server di autenticazione a più fattori e il gruppo di Azure predefinito hello. Selezionare il gruppo appropriato di hello.
4. In Amministrazione utenti selezionare **Bypass monouso**.
5. Nella pagina Bypass monouso hello, fare clic su **nuovo Bypass monouso**.

  ![Cloud](./media/multi-factor-authentication-whats-next/create1.png)

6. Immettere nome utente di hello, durata hello del bypass hello e motivo hello hello bypass. quindi fare clic su **Bypass**.
7. Hello limite di tempo diventa effettiva immediatamente, in questo caso utente hello toosign esigenze in prima hello monouso bypass scade. 

### <a name="view-hello-one-time-bypass-report"></a>Hello vista monouso bypass del report
1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Hello sinistra, selezionare Active Directory.
3. Nella parte superiore di hello, selezionare **provider multi-Factor Authentication** tooshow un elenco dei provider multi-Factor Authentication.
4. Selezionare il Provider di multi-Factor Authentication e fare clic su **Gestisci** nella parte inferiore di hello della pagina hello. verrà visualizzata la finestra di Hello portale di gestione di Azure multi-Factor Authentication.
5. Nel portale di gestione di Azure multi-Factor Authentication, di hello sul lato sinistro di hello, in visualizzazione Report, fare clic su **Bypass monouso**.
6. Specificare l'intervallo di date hello che si desidera tooview nel report hello. È anche possibile specificare i nomi utente, i numeri di telefono e hello lo stato utente.
7. Fare clic su **eseguire** tooshow un report di bypass. Fare clic su **esportare tooCSV** se si desidera tooexport hello report.

## <a name="custom-voice-messages"></a>Messaggi vocali personalizzati
I messaggi vocali personalizzati consentono di toouse registrazioni o personali greetings per la verifica in due passaggi. È possibile utilizzare i messaggi vocali personalizzati nei record di addizione tooor tooreplace hello Microsoft.

Prima di iniziare, tenere presente quanto segue:

* formati di file Hello supportato sono. wav e. mp3.
* limite delle dimensioni file Hello è 5 MB.
* I messaggi di autenticazione devono avere una durata inferiore a 20 secondi. I messaggi che sono più di 20 secondi non consentono agli utenti di hello toorespond abbastanza tempo prima che il tempo di verifica hello è scaduto.

### <a name="set-up-a-custom-message"></a>Configurare un messaggio personalizzato

Esistono due parti toocreating il messaggio personalizzato. Innanzitutto, si carica il messaggio hello e attivarla per gli utenti.

tooupload il messaggio personalizzato:

1. Creare un messaggio vocale personalizzato utilizzando uno dei formati di file hello è supportato.
2. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
3. Passare toohello il portale di gestione di autenticazione a più fattori per le istruzioni di hello nella parte superiore di hello di questa pagina.
4. Nel portale di gestione di Azure multi-Factor Authentication hello, fare clic su **messaggi vocali** nella sezione Configurazione hello.
5. In Configura hello: pagina messaggi vocali, fare clic su **nuovo messaggio vocale**.
   ![Cloud](./media/multi-factor-authentication-whats-next/custom1.png)
6. In Configura hello: pagina nuovi messaggi vocali, fare clic su **Gestisci file audio**.
   ![Cloud](./media/multi-factor-authentication-whats-next/custom2.png)
7. In Configura hello: file audio, fare clic su **carica File audio**.
   ![Cloud](./media/multi-factor-authentication-whats-next/custom3.png)
8. In Configura hello: carica File audio, fare clic su **Sfoglia** e passare messaggio vocale tooyour, fare clic su **aprire**.
9. Aggiungere una descrizione e fare clic su **Carica**.
10. Dopo aver caricato messaggio vocale, un messaggio di conferma che è stato caricato correttamente il file hello.

tooturn messaggio hello per gli utenti:

1. A sinistra di hello, fare clic su **messaggi vocali**.
2. In hello sezione messaggi vocali, fare clic su **nuovo messaggio vocale**.
3. Dall'elenco a discesa lingua hello, selezionare una lingua.
4. Se questo messaggio è per un'applicazione specifica, specificarlo nella casella applicazione hello.
5. Dall'elenco a discesa tipo di messaggio hello, selezionare toobe tipo di messaggio hello viene sottoposto a override con il nuovo messaggio personalizzato.
6. Nella prima parte hello hello elenco a discesa File audio, selezionare i file audio hello caricato.
7. Fare clic su **Crea**. Viene visualizzato un messaggio per confermare che è stato creato un messaggio vocale.
    ![Cloud](./media/multi-factor-authentication-whats-next/custom5.png)</center>

## <a name="caching-in-azure-multi-factor-authentication"></a>Memorizzazione nella cache in Azure Multi-Factor Authentication
La memorizzazione nella cache consente tooset un periodo di tempo specifico in modo che i tentativi di autenticazione successivi entro tale periodo di tempo esito positivo automaticamente. La memorizzazione nella cache viene utilizzato quando i sistemi locali, ad esempio VPN inviano numerose richieste di verifica mentre prima richiesta hello è ancora in corso. Consentendo hello richieste successive toosucceed automaticamente dopo che l'utente hello ha esito positivo verifica prima di hello in corso. 

La memorizzazione nella cache non è previsto toobe utilizzato per accessi tooAzure Active Directory.

### <a name="set-up-caching"></a>Configurare la memorizzazione nella cache 
1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Passare toohello il portale di gestione di autenticazione a più fattori per le istruzioni di hello nella parte superiore di hello di questa pagina.
3. Nel portale di gestione di Azure multi-Factor Authentication hello, fare clic su **la memorizzazione nella cache** nella sezione Configurazione hello.
4. Fare clic su **nuova Cache** nella pagina di memorizzazione nella cache di hello configurazione.
5. Selezionare il tipo di Cache di hello e i secondi cache di hello. Fare clic su **Crea**.

<center>![Cloud](./media/multi-factor-authentication-whats-next/cache.png)</center>

## <a name="trusted-ips"></a>IP attendibili
Indirizzi IP attendibili è una funzionalità di Azure MFA che gli amministratori di un tenant gestito o federato possono utilizzare toobypass la verifica. Il metodo utilizzato per gli utenti che accedono dalla rete intranet locale della società hello. Questa funzionalità è disponibile con una versione completa di hello di Azure multi-Factor Authentication, non hello versione gratuita per gli amministratori. Per informazioni dettagliate su come tooget hello versione completa di Azure multi-Factor Authentication, vedere [Azure multi-Factor Authentication](multi-factor-authentication.md).

| Tipo di tenant di Azure AD | Opzioni disponibili per gli indirizzi IP attendibili |
|:--- |:--- |
| Gestito |<li>Intervalli di indirizzi IP specifici: gli amministratori possono specificare un intervallo di indirizzi IP che è possano ignorare la verifica in due passaggi per gli utenti che accedono dalla rete intranet della società hello.</li> |
| Federato |<li>Tutti gli utenti federati - tutti gli utenti accedono federati in all'interno di hello organizzazione possono ignorare la verifica in due passaggi usando un'attestazione rilasciata da ADFS.</li><br><li>Intervalli di indirizzi IP specifici: gli amministratori possono specificare un intervallo di indirizzi IP che è possano ignorare la verifica in due passaggi per gli utenti che accedono dalla rete intranet della società hello. |

Questo bypass può essere usato solo all'interno della rete Intranet di un'azienda. 

**Esperienza dell'utente finale all'interno della rete aziendale:**

Quando la funzionalità Indirizzi IP attendibili è disabilitata, è necessario usare la verifica in due passaggi per i flussi del browser e le password dell'app per le applicazioni rich client meno recenti. 

Se la funzionalità Indirizzi IP attendibili è abilitata, la verifica in due passaggi *non* è necessaria per i flussi dei browser. Le password di app *non* necessari per le app rich client meno recenti, purché hello utente non è stato già creato una password di app. Se si inizia a usare una password dell'app, questa rimane obbligatoria. 

**Esperienza dell'utente finale all'esterno della rete aziendale:**

Sia che la funzionalità Indirizzi IP attendibili sia abilitata o meno, è necessario usare la verifica in due passaggi per i flussi del browser e le password dell'app per le applicazioni rich client meno recenti. 

### <a name="tooenable-trusted-ips"></a>tooenable gli indirizzi IP attendibili
1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Passare toohello pagina di impostazioni di servizio di autenticazione a più fattori per le istruzioni di hello all'inizio di hello di questo articolo.
3. Nella pagina Impostazioni servizio hello in indirizzi IP attendibili, sono disponibili due opzioni:
   
   * **Per le richieste degli utenti federati originate dalla intranet dell'utente** : casella di controllo hello. Federati tutti gli utenti che accedono dalla verifica in due passaggi bypass rete aziendale hello usando un'attestazione rilasciata da ADFS.
   * **Per le richieste da un determinato intervallo di indirizzi IP pubblici** : immettere gli indirizzi IP hello nella casella di testo hello fornita utilizzando la notazione CIDR. Ad esempio: xxx.xxx.xxx.0/24 per gli indirizzi IP hello intervallo xxx.xxx.xxx.1 – xxx.xxx.xxx.254 oppure xxx.xxx.xxx.xxx/32 per un singolo indirizzo IP. È possibile immettere fino too50 intervalli di indirizzi IP. Gli utenti che accedono da tali indirizzi IP possono ignorare la verifica in due passaggi.
4. Fare clic su **Salva**.
5. Una volta applicati gli aggiornamenti di hello, fare clic su **Chiudi**.

![IP attendibili](./media/multi-factor-authentication-whats-next/trustedips3.png)

## <a name="app-passwords"></a>Password dell'app
Alcune applicazioni, come Office 2010 o le versioni meno recenti di Apple Mail, non supportano la verifica in due passaggi Non sono configurati tooaccept una verifica di secondo. toouse queste App, è necessario toouse "password dell'app" al posto della password tradizionali. password dell'app Hello consente toobypass applicazione hello verifica in due passaggi e continuare a lavorare.

> [!NOTE]
> Autenticazione moderna per hello client di Office 2013
> 
> Client di Office 2013 (inclusi Outlook) e i protocolli di autenticazione moderna di supporto più recenti e può essere abilitato toowork con verifica in due passaggi. Dopo aver abilitato la verifica in due passaggi, non è più necessario usare le password dell'app per questi client.  Per altre informazioni, vedere l'[annuncio dell'anteprima pubblica dell'autenticazione moderna di Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).

### <a name="important-things-tooknow-about-app-passwords"></a>Aspetti importanti tooknow sulle password di app
Di seguito è riportato un elenco delle informazioni importanti da conoscere sulle password delle app.

* Le password dell'App devono essere immesso nella casella di input hello una volta per ogni app. Gli utenti non sono a tenerne traccia tookeep e immetterle ogni volta.
* la password effettiva Hello viene generata automaticamente e non viene fornita dall'utente hello. password generata automaticamente Hello è più difficile per un utente malintenzionato tooguess ed è più sicura.
* Il limite è di 40 password per utente. 
* App che memorizza nella cache le password e l'utilizzo in scenari locali potrà non si avviano in quanto la password di app hello non è noto di fuori di id organizzativo hello. Un esempio è posta elettronica di Exchange in locale, ma è posta hello archiviato nel cloud hello. Hello stessa password non funziona.
* Quando viene avviata l'autenticazione a più fattori, è possibile usare la password con alcuni client non basati su browser. Non è possibile usare le password delle app per attività amministrative. Assicurarsi di creare un account di servizio con gli script di PowerShell toorun una password complessa e non abilitare tale account per la verifica in due passaggi.

> [!WARNING]
> Le password di app non funzionano in ambienti ibridi dove i client comunicano con endpoint di individuazione automatica sia locali che nel cloud. Le password del dominio sono necessari tooauthenticate locale e le password di app sono necessari tooauthenticate cloud hello.

### <a name="naming-guidance-for-app-passwords"></a>Indicazioni per la denominazione delle password dell'app
I nomi delle password di App deve riflettere dispositivo hello in cui vengono utilizzati. Ad esempio, se si usa un portatile con app non basate su browser, creare una sola password dell'app denominata Portatile e usare tale password. Quindi, creare un'altra password di app denominata Desktop per hello stesse applicazioni nel computer desktop. 

È consigliabile creare una password dell'app per ogni dispositivo, anziché una password dell'app per ogni applicazione.

### <a name="federated-sso-app-passwords"></a>Password dell'app federate (SSO)
Azure AD supporta la federazione (Single Sign-On) con Active Directory Domain Services (AD DS) di Windows Server in locale. Se l'organizzazione è federata con Azure AD e si sta toobe tramite Azure multi-Factor Authentication, le password di app di informazioni hello sono importante. In questa sezione si applica solo ai clienti toofederated (SSO).

* Le password dell'app vengono verificate da Azure AD e di conseguenza ignorano la federazione. La federazione viene usata attivamente solo durante l'impostazione delle password dell'app.
* Per gli utenti federati (SSO), non passiamo mai toohello il Provider di identità (IdP), a differenza del flusso passivo hello. Hello password sono archiviate nell'id organizzativo hello. Se l'utente hello lascia la società hello, tali informazioni sono tooflow tooorganizational id utilizzando DirSync in tempo reale. Disabilitazione o eliminazione di account potrebbe richiedere toothree ore toosync, ritardando disabilitazione o eliminazione della Password di App in Azure AD.
* Le impostazioni locali di Controllo dell'accesso Client non vengono rispettate dalla password dell'app.
* Per la password dell'app non è disponibile alcuna funzionalità di registrazione o controllo dell'autenticazione in locale.
* Alcune architetture avanzate possono richiedere una combinazione di nome utente e password dell'organizzazione e password delle app quando si usa la verifica in due passaggi con i client. Ciò dipende dalla posizione in cui viene eseguita l'autenticazione. Per i client che eseguono l'autenticazione con un'infrastruttura locale, verranno usati un nome utente e una password dell'organizzazione. Per i client che eseguono l'autenticazione con Azure AD, utilizzare una password di app hello.

  Si supponga ad esempio di avere un'architettura costituita dalle istanze seguenti:

  * Si sta eseguendo la federazione dell'istanza locale di Active Directory con Azure AD
  * Si usa Exchange Online
  * Si usa Lync, specificamente in locale
  * Si usa Azure Multi-Factor Authentication

  ![Verifica](./media/multi-factor-authentication-whats-next/federated.png)

  In questi casi, è necessario seguire questa procedura:

  * Quando si firma-in tooLync, utilizzare il nome utente e password di azienda.
  * Quando si tenta di rubrica hello tooaccess, tramite un client di Outlook che si connette tooExchange online, è possibile utilizzare una password di app.

### <a name="allow-app-password-creation"></a>Consentire la creazione di password dell'app
Per impostazione predefinita, gli utenti non è possibile creare password di app, ma è possibile abilitare funzionalità hello manualmente. gli utenti tooallow hello le password di app toocreate possibilità, usare hello seguente procedura:

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Passare toohello pagina di impostazioni di servizio di autenticazione a più fattori per le istruzioni di hello all'inizio di hello di questo articolo.
3. Selezionare il pulsante di opzione hello troppo Avanti**consentono agli utenti toocreate app password toosign in App non basate su browser**.

![Creazione di password dell'app](./media/multi-factor-authentication-whats-next/trustedips3.png)

### <a name="create-app-passwords"></a>Creare password dell'app
Gli utenti possono creare password dell'app durante la registrazione iniziale. Essi viene fornite un'opzione alla fine di hello hello del processo di registrazione che consenta loro toocreate le password dell'app.

Gli utenti possono creare password delle app anche dopo la registrazione. Possono creare hello le password di app modificando le impostazioni nel portale di Office 365 portal o hello Azure hello. Per altre informazioni e procedure dettagliate per gli utenti, vedere [Che cosa sono le password per le app in Azure Multi-Factor Authentication](./end-user/multi-factor-authentication-end-user-app-passwords.md).

## <a name="remember-multi-factor-authentication-for-devices-that-users-trust"></a>Memorizza Multi-Factor Authentication per i dispositivi considerati attendibili dagli utenti
La memorizzazione di Multi-Factor Authentication per i dispositivi e i browser che gli utenti considerano attendibili è una funzionalità disponibile gratuitamente per tutti gli utenti di MFA. Multi-factor authentication consente passa tooby-gli utenti autenticazione a più fattori per un numero prefissato di giorni dopo l'accesso. Questa funzionalità migliora l'usabilità, riducendo il numero di hello di volte in cui un utente può eseguire la verifica nel hello stesso dispositivo.

Tuttavia, se un dispositivo o un account viene compromesso, la memorizzazione di MFA per i dispositivi attendibili può influire sulla sicurezza. Se viene compromesso un account aziendale o un dispositivo attendibile viene smarrito o rubato, è necessario troppo[ripristinare multi-Factor Authentication su tutti i dispositivi](multi-factor-authentication-manage-users-and-devices.md#restore-mfa-on-all-remembered-devices-for-a-user). L'azione revoca stato hello attendibile da tutti i dispositivi e utente di hello è di nuovo la verifica in due passaggi tooperform obbligatorio. È anche possibile indicare il toorestore utenti autenticazione a più fattori con i propri dispositivi con le istruzioni di hello in [gestire le impostazioni per la verifica in due passaggi](./end-user/multi-factor-authentication-end-user-manage-settings.md#require-two-step-verification-again-on-a-device-youve-marked-as-trusted)

### <a name="how-it-works"></a>Funzionamento

Memorizzazione di multi-Factor Authentication funziona impostando un cookie permanente nel browser hello quando un utente archivia hello "non chiedere più per **X** giorni" casella al momento dell'accesso. Hello utente non richiesto per l'autenticazione a più fattori nuovamente da tale browser fino alla scadenza del cookie hello. Se l'utente di hello apre un browser diverso in hello stesso dispositivo o Cancella i cookie, vengono richieste tooverify di nuovo. 

Hello "non chiedere più per **X** giorni" non è visualizzata la casella di controllo per le app non basate su browser, supportano l'autenticazione moderna o meno. Queste app usano token di aggiornamento che forniscono nuovi token di accesso ogni ora. Quando un token di aggiornamento viene convalidato, Azure AD verifica è stata eseguita la verifica di hello ultimo tempo entro il numero di hello configurato di giorni. 

In conclusione, ricordare di autenticazione a più fattori nei dispositivi attendibili riduce il numero di hello di autenticazioni per le app web (che richiedono in genere ogni ora). Ma aumenta anche il numero di hello di autenticazione per i client di autenticazione moderna (che richiedono in genere ogni 90 giorni).

> [!NOTE]
>Questa funzionalità non è compatibile con hello "Mantieni l'accesso" funzionalità di ADFS quando gli utenti eseguono la verifica in due passaggi per ADFS tramite hello Azure MFA Server o una soluzione di autenticazione a più fattori di terze parti. Se gli utenti selezionare "Mantieni l'accesso" in AD FS e inoltre contrassegnare il dispositivo come attendibile per l'autenticazione a più fattori, non sarà in grado di tooverify hello numero "Ricordare autenticazione a più fattori" di giorni alla scadenza. Azure AD richiede una verifica di nuovo in due passaggi, ma AD FS restituisce un token con attestazione di autenticazione a più fattori originale hello e data invece di eseguire di nuovo la verifica in due passaggi. Questo processo attiva un ciclo di verifica tra Azure AD e AD FS. 

### <a name="enable-remember-multi-factor-authentication"></a>Abilitare la funzionalità Memorizza Multi-Factor Authentication
1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Passare toohello pagina di impostazioni di servizio di autenticazione a più fattori per le istruzioni di hello all'inizio di hello di questo articolo.
3. Nella pagina Impostazioni servizio hello Gestisci impostazioni utente del dispositivo, verificare hello **consentire agli utenti l'autenticazione a più fattori tooremember nei dispositivi attendibili** casella.
   ![Memorizzare dispositivi](./media/multi-factor-authentication-whats-next/remember.png)
4. Impostare il numero di hello di giorni che si desidera eseguire la verifica in due passaggi tooallow hello attendibile dispositivi toobypass. valore predefinito di Hello è 14 giorni.
5. Fare clic su **Salva**.
6. Fare clic su **Close**.

### <a name="mark-a-device-as-trusted"></a>Contrassegnare un dispositivo come attendibile

Dopo aver abilitato questa funzionalità, gli utenti possono contrassegnare un dispositivo come attendibile al momento dell'accesso, selezionando l'opzione **Non chiedere più**.

![Screenshot di Non chiedere più](./media/multi-factor-authentication-whats-next/trusted.png)

## <a name="selectable-verification-methods"></a>Metodi di verifica selezionabili
È possibile scegliere quali metodi di verifica mettere a disposizione degli utenti. Hello nella tabella seguente fornisce una breve panoramica di ogni metodo.

Quando gli utenti registrano i propri account per l'autenticazione a più fattori, sceglieranno il metodo di verifica preferita fuori opzioni hello è abilitata. materiale sussidiario Hello per il processo di registrazione è trattata nella [Imposta account per la verifica in due passaggi](multi-factor-authentication-end-user-first-time.md)

| Metodo | Descrizione |
|:--- |:--- |
| Chiamare toophone |Invia una chiamata vocale automatizzata. Hello utente risposte hello chiamata e preme # hello phone tastierino tooauthenticate. Il numero di telefono non è sincronizzate tooon locale di Active Directory. |
| Testo messaggio toophone |Invia un messaggio di testo contenente un codice di verifica. utente Hello è testo toohello tooeither richiesta risposta messaggio con il codice di verifica hello o codice di verifica tooenter hello hello sign nell'interfaccia. |
| Notifica tramite app per dispositivi mobili |Invia un telefono tooyour di notifica push o al dispositivo registrato. Visualizza una notifica di hello Hello utente e seleziona **verificare** toocomplete verifica. <br>è disponibile per app di Microsoft Authenticator Hello [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), e [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |
| Codice di verifica dall'app per dispositivi mobili |app Microsoft Authenticator Hello genera un nuovo codice di verifica OATH ogni 30 secondi. Hello utente immette il codice di verifica hello nell'interfaccia accesso.<br>è disponibile per app di Microsoft Authenticator Hello [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), e [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |

### <a name="how-tooenabledisable-authentication-methods"></a>Come tooenable o disabilitare i metodi di autenticazione
1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Passare toohello pagina di impostazioni di servizio di autenticazione a più fattori per le istruzioni di hello all'inizio di hello di questo articolo.
3. Nella pagina Impostazioni servizio hello in Opzioni di verifica, selezionare/deselezionare le opzioni di hello desiderato toouse.
   ![Opzioni di verifica](./media/multi-factor-authentication-whats-next/authmethods.png)
4. Fare clic su **Save**.
5. Fare clic su **Close**.
