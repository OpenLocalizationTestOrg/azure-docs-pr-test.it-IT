---
title: integrazione di Gateway Desktop con l'estensione dei criteri di rete di Azure MFA aaaRemote | Documenti Microsoft
description: "Questo articolo viene illustrato come integrare l'infrastruttura di Gateway Desktop remoto con autenticazione a più fattori Azure utilizzando l'estensione dei criteri di rete Server () hello per Microsoft Azure."
services: active-directory
keywords: Azure MFA, integrare Gateway Desktop remoto, Azure Active Directory, estensione NPS (Network Policy Server)
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: ae5f6864416582bd82b787005ca787988d23a813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
#  <a name="integrate-your-remote-desktop-gateway-infrastructure-using-hello-network-policy-server-nps-extension-and-azure-ad"></a>Integrare l'infrastruttura di Gateway Desktop remoto utilizzando l'estensione di hello Server dei criteri di rete (NPS) e Azure AD

Questo articolo fornisce informazioni dettagliate per l'integrazione dell'infrastruttura di Gateway Desktop remoto con Azure multi-Factor Authentication (MFA) tramite l'estensione dei criteri di rete Server () hello per Microsoft Azure. 

Hello estensione dei criteri di rete del servizio () per Azure consente l'autenticazione client RADIUS Remote Authentication Dial-In utente Service () toosafeguard clienti mediante Azure's basato su cloud [multi-Factor Authentication (MFA)](multi-factor-authentication.md). Questa soluzione offre la verifica in due passaggi per l'aggiunta di un secondo livello di sicurezza toouser accessi e le transazioni.

In questo articolo vengono fornite istruzioni dettagliate per l'integrazione dell'infrastruttura Criteri di rete hello con autenticazione a più fattori di Azure utilizzando l'estensione dei criteri di rete hello per Azure. In questo modo la verifica sicura per gli utenti che tentano di toolog su tooa Gateway Desktop remoto. 

le organizzazioni di offre servizi di accesso (NPS) e criteri di rete Hello hello seguenti di hello toodo possibilità:
* Definire le posizioni centrale per la gestione di hello e controllo delle richieste di rete specificando chi può connettersi, le ore del giorno sono consentite le connessioni, hello la durata delle connessioni e hello livello di sicurezza che i client devono utilizzare tooconnect e così via. Invece che specificare questi criteri in ogni VPN o server Gateway Desktop remoto, è possibile specificarli una sola volta in una posizione centrale. il protocollo RADIUS Hello fornisce hello centralizzato di autenticazione, autorizzazione e Accounting (AAA). 
* Stabilire e applicare criteri di integrità client Protezione accesso rete (NAP) che determinano se i dispositivi vengono concesse le risorse toonetwork di accesso con restrizioni o senza restrizioni.
* Forniscono un mezzo tooenforce autenticazione e autorizzazione per accedere ai punti di accesso wireless che supportano too802.1x e commutatori Ethernet.    

In genere, le organizzazioni utilizzare criteri di rete (RADIUS) toosimplify e centralizzare la gestione di hello di VPN criteri. Tuttavia, molte organizzazioni inoltre utilizzano toosimplify dei criteri di rete e centralizzare la gestione di hello dei criteri di autorizzazione connessioni Desktop desktop remoto (criteri di autorizzazione del desktop remoto). 

Le organizzazioni possono anche l'integrazione di criteri di rete con Azure MFA tooenhance protezione e fornire un elevato livello di conformità. Ciò garantisce che gli utenti stabilire toolog verifica in due fasi in toohello Gateway Desktop remoto. Per gli utenti toobe consentito l'accesso, è necessario specificare la combinazione di nome utente/password con le informazioni utente hello dispone dei relativi controlli. Queste informazioni devono essere attendibili e non facilmente duplicabili, ad esempio un numero di telefono cellulare, un numero di rete fissa, un'applicazione in un dispositivo mobile e così via.

Toohello precedente la disponibilità di hello estensione dei criteri di rete per Azure, i clienti che desideravano tooimplement di verifica in due passaggi per integrato dei criteri di rete e gli ambienti Azure MFA era tooconfigure e gestiscono un Server separato di autenticazione a più fattori nell'ambiente locale hello come documentati in [Gateway Desktop remoto e il Server Azure multi-Factor Authentication tramite RADIUS](multi-factor-authentication-get-started-server-rdg.md).

disponibilità Hello hello estensione di criteri di rete per Azure offre ora organizzazioni hello scelta toodeploy una soluzione di autenticazione a più fattori in locale o un basato su cloud MFA soluzione toosecure client l'autenticazione RADIUS.

## <a name="authentication-flow"></a>Flusso di autenticazione

Per gli utenti toobe concesse toonetwork di accedere alle risorse tramite un Gateway Desktop remoto, che è necessario soddisfare condizioni hello specificate in un criterio autorizzazione di connessione desktop remoto (autorizzazione connessioni desktop remoto) e un criterio di autorizzazione desktop remoto risorse (criterio di autorizzazione risorse Desktop remoto). Estremità di desktop remoto specificare chi è autorizzato tooconnect tooRD gateway. Criteri di autorizzazione risorse Desktop remoto specificare le risorse di rete hello, ad esempio Desktop remoto o le applicazioni remote, tale utente hello è consentito tooconnect toothrough hello Gateway Desktop remoto. 

Un Gateway Desktop remoto può essere configurato toouse archivio criteri centrali per i criteri di autorizzazione del desktop remoto. Criteri di autorizzazione risorse Desktop remoto non è possibile utilizzare un criterio centrale, man mano che vengono elaborati in hello Gateway Desktop remoto. Un esempio di un toouse Gateway Desktop remoto configurato archivio criteri centrali per i criteri di autorizzazione del desktop remoto è un server RADIUS client tooanother dei criteri di rete che funge da archivio centrale di hello.

Quando l'estensione dei criteri di rete per Azure hello è integrato con hello dei criteri di rete e Gateway Desktop remoto, il flusso di autenticazione ha esito positivo di hello è il seguente:

1. server Gateway Desktop remoto Hello riceve una richiesta di autenticazione da una risorsa di tooa tooconnect utente desktop remoto, ad esempio una sessione Desktop remoto. Funge da client RADIUS, server Gateway Desktop remoto hello converte messaggio di richiesta di accesso RADIUS tooa richiesta hello e invia i server RADIUS (NPS) toohello di messaggi hello in cui è installato l'estensione dei criteri di rete hello. 
2. Hello nome utente e la combinazione di password viene verificata in Active Directory e hello utente viene autenticato.
3. Se tutti hello condizioni come specificato in hello richiesta di connessione dei criteri di rete e che siano soddisfatti i criteri di rete hello (ad esempio, ora del giorno o gruppo di restrizioni di appartenenza), hello estensione dei criteri di rete attiva una richiesta per l'autenticazione secondaria con Azure MFA. 
4. Azure MFA comunica con Azure AD, recupera i dettagli dell'utente hello ed esegue l'autenticazione secondaria hello utilizzando il metodo hello configurato dall'utente hello (messaggio di testo, app per dispositivi mobili e così via). 
5. Al completamento dell'operazione di richiesta di autenticazione a più fattori hello Azure MFA comunica l'estensione dei criteri di rete di hello risultato toohello.
6. server dei criteri di rete Hello in cui è installato l'estensione hello invia un messaggio di autorizzazione di accesso RADIUS per server Gateway Desktop remoto toohello dei criteri di autorizzazione connessioni desktop remoto hello.
7. è concesso l'accesso utente Hello toohello richiesto risorsa di rete tramite hello Gateway Desktop remoto.

## <a name="prerequisites"></a>Prerequisiti
Questa sezione descrive i prerequisiti di hello necessari prima dell'integrazione di Azure MFA con hello Gateway Desktop remoto. Prima di iniziare, è necessario disporre di hello seguenti prerequisiti soddisfatti.  

* Infrastruttura Servizi Desktop remoto
* Licenza di Azure MFA
* Software Windows Server
* Ruolo Servizi di accesso e criteri di rete
* Azure AD con sincronizzazione con AD in locale 
* ID GUID di Azure Active Directory

### <a name="remote-desktop-services-rds-infrastructure"></a>Infrastruttura Servizi Desktop remoto
Deve essere presente un'infrastruttura Servizi Desktop remoto funzionante. In caso contrario, è possibile creare rapidamente questa infrastruttura in Azure con i seguenti hello avvio rapido modello: [distribuzione crea insiemi di sessioni Desktop remoto](https://github.com/Azure/azure-quickstart-templates/tree/ad20c78b36d8e1246f96bb0e7a8741db481f957f/rds-deployment). 

Se si desidera toomanually creare un'infrastruttura di servizi desktop remoto locale rapidamente a scopo di test, seguire hello passaggi toodeploy uno. 
**Altre informazioni**: [Deploy RDS with Azure quick start](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-in-azure) (Avvio rapido per la distribuzione di Servizi Desktop remoto con Azure) e [Basic RDS infrastructure deployment](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-deploy-infrastructure) (Distribuzione di un'infrastruttura Servizi Desktop remoto di base). 

### <a name="licenses"></a>Licenze
È richiesta una licenza per Azure MFA, disponibile tramite una sottoscrizione di Azure AD Premium, Enterprise Mobility + Security (EMS) o MFA. Per ulteriori informazioni, vedere [come tooget Azure multi-Factor Authentication](multi-factor-authentication-versions-plans.md). A scopo di test, è possibile usare una sottoscrizione della versione di valutazione gratuita.

### <a name="software"></a>Software
Hello estensione dei criteri di rete richiede Windows Server 2008 R2 SP1 o versione successiva con installato il servizio ruolo dei criteri di rete hello. Tutti i passaggi di hello in questa sezione sono stati eseguiti usando Windows Server 2016.

### <a name="network-policy-and-access-services-nps-role"></a>Ruolo Servizi di accesso e criteri di rete
Hello servizio ruolo dei criteri di rete fornisce client e server RADIUS hello funzionalità, nonché il servizio di integrità criteri di accesso di rete. Questo ruolo deve essere installato in almeno due computer nell'infrastruttura: hello Gateway Desktop remoto e un altro server membro o controller di dominio. Per impostazione predefinita, il ruolo di hello è già presente nel computer hello configurato come hello Gateway Desktop remoto.  È anche necessario installare ruolo dei criteri di rete hello in almeno in un altro computer, ad esempio un controller di dominio o server membro.

Per informazioni sull'installazione di ruoli di hello dei criteri di rete servizio Windows Server 2012 o versioni precedenti, vedere [installare un Server dei criteri di integrità Protezione accesso alla rete](https://technet.microsoft.com/library/dd296890.aspx). Per una descrizione di procedure consigliate per i criteri di rete, tra cui hello raccomandazione tooinstall dei criteri di rete in un controller di dominio, vedere [procedure consigliate per i criteri di rete](https://technet.microsoft.com/library/cc771746).

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a>Azure Active Directory con sincronizzazione con Active Directory locale 
hello toouse estensione dei criteri di rete, in locale gli utenti devono essere sincronizzati con Azure AD e abilitati per l'autenticazione a più fattori. Questa sezione presuppone che gli utenti locali siano sincronizzati con Azure AD tramite AD Connect. Per informazioni su Azure AD Connect, vedere [Integrare le directory locali con Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md). 

### <a name="azure-active-directory-guid-id"></a>ID GUID di Azure Active Directory
tooinstall dei criteri di rete, è necessario tooknow hello GUID di hello Azure AD. Di seguito vengono fornite istruzioni per la ricerca di hello GUID di hello Azure AD.

## <a name="configure-multi-factor-authentication"></a>Configurare Multi-Factor Authentication 
In questa sezione vengono fornite istruzioni per l'integrazione di Azure MFA con hello Gateway Desktop remoto. Come amministratore, è necessario configurare il servizio di Azure MFA hello prima che gli utenti self-è possono registrare i dispositivi a più fattori o applicazioni.

Seguire i passaggi di hello in [Introduzione ad Azure multi-Factor Authentication nel cloud hello](multi-factor-authentication-get-started-cloud.md) tooenable autenticazione a più fattori per gli utenti di Azure AD. 

### <a name="configure-accounts-for-two-step-verification"></a>Configurare gli account per la verifica in due passaggi
Una volta che un account è stato abilitato per l'autenticazione a più fattori, non è possibile accedere tooresources disciplinato hello criteri di autenticazione a più fattori fino a quando non è stato configurato un toouse dispositivo attendibile per il secondo fattore di autenticazione hello sono autenticati utilizzando la verifica in due passaggi.

Seguire i passaggi di hello in [cosa Azure multi-Factor Authentication alle mie esigenze?](./end-user/multi-factor-authentication-end-user.md) toounderstand e configurare correttamente i dispositivi per l'autenticazione a più fattori con l'account utente.

## <a name="install-and-configure-nps-extension"></a>Installare e configurare l'estensione NPS
In questa sezione vengono fornite istruzioni per la configurazione dell'infrastruttura di servizi desktop remoto toouse Azure MFA per l'autenticazione client con hello Gateway Desktop remoto.

### <a name="acquire-azure-active-directory-guid-id"></a>Acquisire l'ID GUID di Azure Active Directory

Come parte della configurazione di hello di hello estensione dei criteri di rete, è necessario toosupply credenziali di amministratore e l'ID di Azure AD hello per tenant di Azure AD. Hello alla procedura seguente viene illustrato come tooget hello ID del tenant.

1. Accedi toohello [portale di Azure](https://portal.azure.com) come amministratore globale di hello di hello Azure tenant.
2. Nel riquadro di spostamento sinistro di hello, selezionare hello **Azure Active Directory** icona.
3. Selezionare **Proprietà**.
4. Nel pannello Proprietà hello, accanto a hello ID di Directory, fare clic su hello **copia** icona, come illustrato di seguito, toocopy hello ID tooclipboard.

 ![Proprietà](./media/nps-extension-remote-desktop-gateway/image1.png)

### <a name="install-hello-nps-extension"></a>Installare l'estensione dei criteri di rete hello
Installare l'estensione di criteri di rete di hello in un server con criteri di rete hello e installato il ruolo Servizi di accesso (NPS). Questo meccanismo funziona come server RADIUS hello per la progettazione. 

>[!Important]
> Assicurarsi che l'estensione dei criteri di rete hello non è installato nel server Gateway Desktop remoto.
> 

1. Scaricare hello [estensione dei criteri di rete](https://aka.ms/npsmfa). 
2. Copia hello il programma di installazione eseguibile (NpsExtnForAzureMfaInstaller.exe) toohello server NPS.
3. Nel server dei criteri di rete hello, fare doppio clic su **NpsExtnForAzureMfaInstaller.exe**. Se richiesto, fare clic su **Esegui**.
4. In hello estensione dei criteri di rete per la finestra di dialogo di autenticazione a più fattori di Azure, esaminare condizioni di licenza software hello controllare **accetto toohello condizioni di licenza**, fare clic su **installare**.
 
  ![Installazione dell'estensione per Azure MFA](./media/nps-extension-remote-desktop-gateway/image2.png)

5. In hello estensione dei criteri di rete per la finestra di dialogo di autenticazione a più fattori di Azure, fare clic su Chiudi. 

  ![Per installare l'estensione NPS per Azure MFA](./media/nps-extension-remote-desktop-gateway/image3.png)

### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a>Configurare i certificati per l'utilizzo con l'estensione dei criteri di rete hello tramite uno script di PowerShell
Successivamente, è necessario tooconfigure certificati per l'utilizzo da comunicazioni protette tooensure di hello estensione dei criteri di rete e la garanzia. i componenti dei criteri di rete di Hello includono uno script di Windows PowerShell che configura un certificato autofirmato per l'utilizzo con criteri di rete. 

lo script di Hello esegue hello seguenti azioni:

* Crea un certificato autofirmato
* Associa una chiave pubblica del certificato tooservice principale in Azure AD
* Archivi hello certificato nell'archivio computer locale hello
* Concede l'accesso utente di rete toohello chiave privata del certificato toohello
* Riavvia il servizio Server dei criteri di rete

Se si desidera toouse i propri certificati, è necessario tooassociate hello pubblico del principio di servizio toohello certificato in Azure AD e così via.

script di hello toouse, fornire le credenziali di amministratore AD Azure estensione hello e hello ID tenant di Azure AD copiato in precedenza. Eseguire script hello in ogni server dei criteri di rete in cui è installato l'estensione dei criteri di rete hello. Quindi hello seguenti:

1. Aprire un prompt di Windows PowerShell come amministratore.
2. Al prompt di PowerShell hello digitare **cd 'c:\Programmi\Microsoft Files\Microsoft\AzureMfa\Config'**e premere **invio**.
3. Digitare _.\AzureMfsNpsExtnConfigSetup.ps1_ e premere **INVIO**. script Hello controlla toosee se è installato il modulo di Azure Active Directory PowerShell hello. Se non è installato, script hello verrà installato il modulo hello.

  ![Azure AD PowerShell](./media/nps-extension-remote-desktop-gateway/image4.png)
  
4. Al termine dello script hello verifica installazione hello del modulo di PowerShell hello, Visualizza la finestra di dialogo modulo di Azure Active Directory PowerShell hello. Nella finestra di dialogo hello, immettere le credenziali di amministratore di Azure AD e la password e fare clic su **Accedi**.

  ![Aprire l'account di PowerShell](./media/nps-extension-remote-desktop-gateway/image5.png)

5. Quando richiesto, incollare l'ID tenant hello copiato negli Appunti toohello in precedenza e premere **invio**.

  ![Immettere l'ID tenant](./media/nps-extension-remote-desktop-gateway/image6.png)

6. script Hello crea un certificato autofirmato ed esegue altre modifiche alla configurazione. output di Hello deve essere come immagine di hello illustrato di seguito.

  ![Certificato autofirmato](./media/nps-extension-remote-desktop-gateway/image7.png)

## <a name="configure-nps-components-on-remote-desktop-gateway"></a>Configurare i componenti di Server dei criteri di rete in Gateway Desktop remoto
In questa sezione configurare criteri di autorizzazione connessioni Gateway Desktop remoto hello e altre impostazioni di RADIUS.

flusso di autenticazione Hello richiede che RADIUS lo scambio di messaggi tra hello Gateway Desktop remoto e hello server criteri di rete in cui è installato hello Server dei criteri di rete. Ciò significa che è necessario configurare le impostazioni dei client RADIUS nel Gateway Desktop remoto sia hello server dei criteri di rete in cui è installato l'estensione dei criteri di rete hello. 

### <a name="configure-remote-desktop-gateway-connection-authorization-policies-toouse-central-store"></a>Configurare l'archivio centrale di Gateway Desktop remoto connessione autorizzazioni criteri toouse
Criteri di autorizzazione di connessione Desktop remoto (criteri di autorizzazione del desktop remoto) specificano i requisiti di hello per server Gateway Desktop remoto di tooa connessione. I criteri di autorizzazione connessioni Desktop remoto possono essere archiviati in locale (impostazione predefinita) oppure in un archivio di criteri di autorizzazione connessioni Desktop remoto centrale che esegue Server dei criteri di rete. tooconfigure l'integrazione di Azure MFA con Servizi Desktop remoto, è necessario utilizzare hello toospecify di un archivio centrale.

1. Nel server Gateway Desktop remoto hello aprire **Server Manager**. 
2. Scegliere dal menu hello **strumenti**, punto troppo**Servizi Desktop remoto**, quindi fare clic su **Gestione Gateway Desktop remoto**.

  ![Servizi Desktop remoto](./media/nps-extension-remote-desktop-gateway/image8.png)

3. In hello Gestione Gateway Desktop remoto, fare clic sul  **\[nome Server\] (Local)**, fare clic su **proprietà**.

  ![Server Name](./media/nps-extension-remote-desktop-gateway/image9.png)

4. Nella finestra di dialogo Proprietà hello, selezionare hello **autorizzazione connessioni desktop remoto** scheda archivio.
5. Nella scheda archivio desktop remoto hello selezionare **Server centrale,**. 
6. In hello **immettere un nome o indirizzo IP per server hello dei criteri di rete** campo, di tipo hello indirizzo IP o server di nome di server hello in cui è installato l'estensione dei criteri di rete hello.

  ![Immettere il nome o l'indirizzo IP](./media/nps-extension-remote-desktop-gateway/image10.png)
  
7. Fare clic su **Aggiungi**.
8. In hello **segreto condiviso** nella finestra di dialogo immettere un segreto condiviso e quindi fare clic su **OK**. Assicurarsi di registrare il segreto condiviso e archiviare i record di hello in modo sicuro.

 >[!NOTE]
 >Segreto condiviso viene utilizzato tooestablish trust tra client e server RADIUS hello. Creare una password lunga e complessa.
 >

 ![Segreto condiviso](./media/nps-extension-remote-desktop-gateway/image11.png)

9. Fare clic su **OK** tooclose hello finestra di dialogo.

### <a name="configure-radius-timeout-value-on-remote-desktop-gateway-nps"></a>Configurare il valore di timeout RADIUS in Server dei criteri di rete per Gateway Desktop remoto
è ora le credenziali degli utenti toovalidate, eseguire la verifica in due passaggi, ricevere risposte tooensure vi e risposta tooRADIUS messaggi, è un valore di timeout RADIUS hello tooadjust necessarie.

1. Nel server Gateway Desktop remoto di hello, in Server Manager fare clic su **strumenti**, quindi fare clic su **Server dei criteri di rete**. 
2. In hello **dei criteri di rete (locale)** espandere **client e server RADIUS**e selezionare **Server RADIUS remoti**.

 ![Gruppi di server RADIUS remoti](./media/nps-extension-remote-desktop-gateway/image12.png)

3. Nel riquadro dei dettagli di hello, fare doppio clic su **gruppo del SERVER GATEWAY Servizi terminal**.

 >[!NOTE]
 >Questo gruppo di Server RADIUS è stato creato durante la configurazione hello server centrale per i criteri dei criteri di rete. Hello Gateway Desktop remoto inoltra RADIUS messaggi toothis server o un gruppo di server, se più di un gruppo di hello.
 >

4. In hello **proprietà gruppo di SERVER GATEWAY Servizi terminal** la finestra di dialogo, l'indirizzo IP selezionare hello o nome del server dei criteri di rete configurate toostore desktop remoto CAPs hello e quindi fare clic su **modifica**. 

 ![Gruppo di server gateway di Servizi terminal](./media/nps-extension-remote-desktop-gateway/image13.png)

5. In hello **modifica Server RADIUS** la finestra di dialogo, seleziona hello **il bilanciamento del carico** scheda.
6. In hello **il bilanciamento del carico** scheda hello **numero di secondi senza risposta prima che la richiesta venga annullata** campo, modificare il valore di predefinito hello da 3 tooa valore compreso tra 30 e 60 secondi.
7. In hello **numero di secondi tra le richieste quando il server viene identificato come non disponibile** campo, modificare il valore predefinito hello di 30 secondi tooa valore uguale tooor maggiore del valore di hello specificato nel passaggio precedente hello.

 ![Modificare il server RADIUS](./media/nps-extension-remote-desktop-gateway/image14.png)

8.  Fare clic su OK due volte le finestre di dialogo tooclose hello.

### <a name="verify-connection-request-policies"></a>Verificare i criteri di richiesta di connessione 
Per impostazione predefinita, quando si configura Gateway Desktop remoto di hello toouse archivio criteri centrali per i criteri di autorizzazione di connessione, hello Gateway Desktop remoto è il server dei criteri di rete toohello di tooforward configurato perno richieste. server dei criteri di rete Hello con estensione di autenticazione a più fattori di Azure hello installato, richiesta di accesso RADIUS hello processi. Hello alla procedura seguente viene illustrato come criterio di richiesta connessione predefinita di tooverify hello. 

1. Espandere hello Gateway Desktop remoto, nella console Criteri di rete (locale) hello **criteri**e selezionare **criteri richiesta di connessione**.
2. Fare clic con il pulsante destro del mouse su **Criteri di richiesta di connessione** e fare doppio clic su **CRITERI DI AUTORIZZAZIONE GATEWAY DI SERVIZI TERMINAL**.
3. In hello **le proprietà di criteri di autorizzazione GATEWAY di Servizi terminal** finestra di dialogo fare clic su hello **impostazioni** scheda.
4. Nella scheda **Impostazioni** fare clic su **Autenticazione** in Inoltro richiesta di connessione. Client RADIUS è configurato tooforward richieste di autenticazione.

 ![Impostazioni di autenticazione](./media/nps-extension-remote-desktop-gateway/image15.png)
 
5. Fare clic su **Annulla**. 

## <a name="configure-nps-on-hello-server-where-hello-nps-extension-is-installed"></a>Configurare i criteri di rete nel server di hello in cui è installato hello estensione dei criteri di rete
Hello dei criteri di rete server in cui estensione di criteri di rete hello esigenze installato toobe tooexchange in grado di RADIUS messaggi al server dei criteri di rete hello hello Gateway Desktop remoto. tooenable questo messaggio di scambio, è necessario disporre tooconfigure hello NPS componenti nel server di hello in cui è installato il servizio di estensione dei criteri di rete hello. 

### <a name="register-server-in-active-directory"></a>Registrare il server in Active Directory
toofunction correttamente in questo scenario, server dei criteri di rete hello deve toobe registrato in Active Directory.

1. Aprire **Server Manager**.
2. In Server Manager fare clic su **Strumenti** e quindi su **Server dei criteri di rete**. 
3. Nella console di Server dei criteri di rete hello, fare doppio clic su **dei criteri di rete (locale)**, quindi fare clic su **Registra server in Active Directory**. 
4. Fare clic su **OK** due volte.

 ![Registrare il server in Active Directory](./media/nps-extension-remote-desktop-gateway/image16.png)

5. Lasciare aperta per la procedura successiva hello hello console.

### <a name="create-and-configure-radius-client"></a>Creare e configurare il client RADIUS 
Hello Gateway Desktop remoto deve toobe configurato come server dei criteri di rete toohello client RADIUS. 

1. Nel server dei criteri di rete hello in cui è installato, hello estensione dei criteri di rete in hello **dei criteri di rete (locale)** console, fare doppio clic su **client RADIUS** e fare clic su **New**.

 ![Nuovo client RADIUS](./media/nps-extension-remote-desktop-gateway/image17.png)

2. In hello **client RADIUS nuovo** finestra di dialogo immettere un nome descrittivo, ad esempio _Gateway_, e hello indirizzo IP o nome DNS del server Gateway Desktop remoto hello. 
3. In hello **segreto condiviso** hello e **Conferma segreto condiviso** immettere hello stesso segreto usata in precedenza.

 ![Nome e indirizzo](./media/nps-extension-remote-desktop-gateway/image18.png)

4. Fare clic su **OK** la finestra di dialogo di tooclose hello RADIUS nuovo client.

### <a name="configure-network-policy"></a>Configurare i criteri di rete
Server dei criteri di rete di hello richiamo con hello estensione di autenticazione a più fattori di Azure è archivio criteri centrali designato hello per hello criteri di autorizzazione di connessione (CAP). Pertanto, è necessario tooimplement un limite per le richieste di connessione valida tooauthorize di hello dei criteri di rete server.  

1. Nella console Criteri di rete (locale) hello espandere **criteri**, fare clic su **criteri di rete**.
2. Fare doppio clic su **server di accesso di connessioni tooother**, fare clic su **duplicato criteri**. 

 ![Duplica criterio](./media/nps-extension-remote-desktop-gateway/image19.png)

3. Fare doppio clic su **server di accesso alla copia di connessioni tooother**, fare clic su **proprietà**.

 ![Proprietà di rete](./media/nps-extension-remote-desktop-gateway/image20.png)

4. In hello **server di accesso alla copia di connessioni tooother** nella finestra di dialogo nel nome dei criteri, immettere un nome appropriato, ad esempio **RDG_CAP**. Selezionare **Criterio attivato** e fare clic su **Concedi accesso**. Facoltativamente, in Tipo di server di accesso alla rete selezionare **Gateway Desktop remoto** oppure lasciare l'impostazione **Non specificato**.

 ![Copia di Connessioni ad altri server di accesso remoto](./media/nps-extension-remote-desktop-gateway/image21.png)

5.  Fare clic su hello **vincoli** e selezionare **Consenti client tooconnect senza la negoziazione di un metodo di autenticazione**.

 ![Consentire ai client tooconnect](./media/nps-extension-remote-desktop-gateway/image22.png)

6. Facoltativamente, fare clic su hello **condizioni** scheda e aggiungere le condizioni che devono essere soddisfatti per hello connessione toobe autorizzato, ad esempio, l'appartenenza a un gruppo di Windows specifico.

 ![Condizioni](./media/nps-extension-remote-desktop-gateway/image23.png)

7. Fare clic su **OK**. Quando richiesto tooview hello argomento della Guida corrispondente, fare clic su **n**.
8. Verificare che il nuovo criterio sia nella parte superiore di hello dell'elenco di hello, che è abilitato il criterio di hello, e che garantisce l'accesso.

 ![Criteri di rete](./media/nps-extension-remote-desktop-gateway/image24.png)

## <a name="verify-configuration"></a>Verificare la configurazione
configurazione di hello tooverify, è necessario toolog su hello Gateway Desktop remoto con un client RDP appropriato. Essere toouse che un account che è consentito per i criteri di autorizzazione di connessione ed è abilitato per Azure MFA. 

Come illustrato nell'immagine di hello riportata di seguito, è possibile utilizzare hello **accesso Web Desktop remoto** pagina.

![Accesso Web Desktop remoto](./media/nps-extension-remote-desktop-gateway/image25.png)

Durante l'immissione correttamente le credenziali per l'autenticazione principale, la finestra di dialogo connessione Desktop remoto di hello viene visualizzato lo stato avvio connessione remota, come illustrato di seguito. 

Se correttamente l'autenticazione con il metodo di autenticazione secondario hello configurati in precedenza in Azure MFA, si è connesso toohello risorse. Tuttavia, se l'autenticazione secondaria hello non ha esito positivo, è stato negato tooresource di accesso. 

![Avviare la connessione remota](./media/nps-extension-remote-desktop-gateway/image26.png)

Nell'esempio riportato di seguito, hello autenticatore hello app su un dispositivo Windows phone è l'autenticazione secondaria hello tooprovide utilizzato.

![Account](./media/nps-extension-remote-desktop-gateway/image27.png)

Dopo aver eseguito l'autenticazione utilizzando il metodo di autenticazione secondaria hello, si è connessi in hello Gateway Desktop remoto come di consueto. Tuttavia, sono necessari toouse un metodo di autenticazione secondaria usando un'app per dispositivi mobili in un dispositivo attendibile hello accesso processo è più sicuro rispetto a quanto sarebbe altrimenti.

### <a name="view-event-viewer-logs-for-successful-logon-events"></a>Visualizzare i log del Visualizzatore eventi per individuare gli eventi di accesso riusciti
tooview hello ha esito positivo-eventi di accesso nei log di Visualizzatore eventi di Windows hello, è possibile emettere hello seguente comando di Windows PowerShell hello tooquery servizi Terminal di Windows e log di sicurezza di Windows.

tooquery ha esito positivo-eventi di accesso nei registri operativi del Gateway hello _(Visualizzatore Eventi\registri applicazioni e servizi Logs\Microsoft\Windows\TerminalServices-Gateway\Operational_, utilizzare hello seguenti comandi:

* _Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '300'} | FL 
* Questo comando Visualizza gli eventi di Windows che mostrano utente hello soddisfatti i requisiti dei criteri di autorizzazione risorse (Desktop remoto RAP) ed è stato concesso l'accesso.

![Visualizzare il Visualizzatore eventi](./media/nps-extension-remote-desktop-gateway/image28.png)

* _Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '200'} | FL
* Questo comando Visualizza gli eventi di hello che mostrano quando l'utente ha soddisfatto i requisiti dei criteri di autorizzazione di connessione.

![Autorizzazione connessioni](./media/nps-extension-remote-desktop-gateway/image29.png)

È anche possibile visualizzare questo log e filtrarlo in base agli ID evento 300 e 200. eventi di accesso riusciti tooquery nei registri di Visualizzatore eventi di sicurezza hello, utilizzare hello comando seguente:

* _Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL 
* Questo comando può essere eseguito su uno dei criteri di rete centrale hello o hello Server Gateway Desktop remoto. 

![Eventi di accesso riusciti](./media/nps-extension-remote-desktop-gateway/image30.png)

È inoltre possibile visualizzare il Registro di protezione hello o hello servizi di accesso e criteri di rete visualizzazione personalizzata, come illustrato di seguito:

![Servizi di accesso e criteri di rete](./media/nps-extension-remote-desktop-gateway/image31.png)

Nel server di hello in cui è installato l'estensione dei criteri di rete hello per Azure MFA, è possibile trovare i registri applicazione Visualizzatore eventi estensione toohello specifico in _applicazioni e servizi Logs\Microsoft\AzureMfa_. 

![Log applicazioni del Visualizzatore eventi](./media/nps-extension-remote-desktop-gateway/image32.png)

## <a name="troubleshoot-guide"></a>Guida per la risoluzione dei problemi

Se la configurazione hello non funziona come previsto, hello primo luogo toostart tootroubleshoot è tooverify che hello utente è configurato toouse Azure MFA. Avere utente hello connettersi toohello [portale di Azure](https://portal.azure.com). Se all'utente viene richiesta l'autenticazione secondaria e può eseguire l'autenticazione, la configurazione di Azure MFA è corretta.

Se l'autenticazione a più fattori di Azure funziona per gli utenti di hello, esaminare i registri eventi rilevanti hello. Sono inclusi i registri eventi di protezione, Gateway è operativo e Azure MFA hello discussi sono trattati nella sezione precedente hello. 

Di seguito è illustrato un esempio di output di un log di sicurezza che mostra un evento di accesso non riuscito (ID evento 6273).

![Evento di accesso non riuscito](./media/nps-extension-remote-desktop-gateway/image33.png)

Di seguito è un evento correlato dai registri AzureMFA hello:

![Log di Azure MFA](./media/nps-extension-remote-desktop-gateway/image34.png)

tooperform avanzate di risoluzione dei problemi opzioni, consultare hello NPS formato file registro del database in cui è installato hello server NPS. Questi file di log vengono creati nella cartella _%SystemRoot%\System32\Logs_ come file di testo con valori delimitati da virgole. 

Per una descrizione di questi file di log, vedere [Interpret NPS Database Format Log Files](https://technet.microsoft.com/library/cc771748.aspx) (Interpretare i file di log in formato database di Server dei criteri di rete). le voci di Hello in questi file di log possono essere difficile toointerpret senza importarle in un foglio di calcolo o di un database. È possibile trovare diversi parser IAS tooassist online in interpretazione hello i file di log. 

Hello immagine riportata di seguito viene illustrato hello output di una tale scaricabile [applicazione shareware](http://www.deepsoftware.com/iasviewer). 

![App shareware](./media/nps-extension-remote-desktop-gateway/image35.png)

Infine, per altre opzioni di risoluzione dei problemi, è possibile usare uno strumento di analisi di protocolli, ad esempio [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx). 

immagine di sotto di Microsoft Message Analyzer Hello viene filtrato nel protocollo RADIUS che contiene il nome utente di hello il traffico di rete **Contoso\AliceC**.

![Microsoft Message Analyzer](./media/nps-extension-remote-desktop-gateway/image36.png)

## <a name="next-steps"></a>Passaggi successivi
[Come tooget Azure multi-Factor Authentication](multi-factor-authentication-versions-plans.md)

[Gateway Desktop remoto e server Azure Multi-Factor Authentication utilizzando RADIUS](multi-factor-authentication-get-started-server-rdg.md)

[Integrare le directory locali con Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md)
