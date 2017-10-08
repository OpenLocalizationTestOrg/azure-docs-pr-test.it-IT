---
title: integrazione di aaaVPN con Azure MFA con l'estensione dei criteri di rete | Documenti Microsoft
description: Questo articolo viene illustrato come integrare l'infrastruttura VPN con Azure MFA con estensione Server dei criteri di rete (NPS) hello per Microsoft Azure.
services: active-directory
keywords: Azure MFA, integrazione VPN, Azure Active Directory, estensione di Server dei criteri di rete
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
ms.openlocfilehash: 5e120f7633121385d9cc5d7bec97ecaa1ec7cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-vpn-infrastructure-with-azure-multi-factor-authentication-mfa-using-hello-network-policy-server-nps-extension-for-azure"></a>Integrare l'infrastruttura VPN con Azure multi-Factor Authentication (MFA) tramite l'estensione dei criteri di rete Server () hello per Azure

## <a name="overview"></a>Panoramica

Hello estensione dei criteri di rete del servizio () per Azure consente alle organizzazioni utilizzando l'autenticazione di client RADIUS Remote Authentication Dial-In utente Service () toosafeguard basato su cloud [Azure multi-Factor Authentication (MFA)](multi-factor-authentication-get-started-server-rdg.md), che fornisce la verifica in due passaggi.

Questo articolo vengono fornite istruzioni per l'integrazione dell'infrastruttura Criteri di rete hello con autenticazione a più fattori di Azure utilizzando l'estensione dei criteri di rete hello per la verifica in due passaggi sicura tooenable Azure per gli utenti che tentano di rete tooyour tooconnect utilizzando una connessione VPN. 

Hello servizi di accesso (NPS) e criteri di rete offre alle organizzazioni hello seguenti funzionalità:

* Specificare i percorsi centrale per la gestione di hello e controllo di rete richieste toospecify in grado di connettersi, le ore del giorno sono consentite le connessioni, la durata di hello delle connessioni e hello livello di sicurezza che i client devono utilizzare tooconnect e così via. Invece che specificare questi criteri in ogni VPN o server Gateway Desktop remoto, è possibile specificarli una sola volta in una posizione centrale. viene utilizzato il protocollo RADIUS Hello tooprovide hello centralizzato di autenticazione, autorizzazione e Accounting (AAA). 
* Stabilire e applicare criteri di integrità client Protezione accesso rete (NAP) che determinano se i dispositivi vengono concesse le risorse toonetwork di accesso con restrizioni o senza restrizioni.
* Forniscono un mezzo tooenforce autenticazione e autorizzazione per accedere ai punti di accesso wireless che supportano too802.1x e commutatori Ethernet.    

Per altre informazioni, vedere [Server dei criteri di rete (NPS)](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-top). 

sicurezza tooenhance e fornire un livello elevato di conformità, le organizzazioni possono integrare dei criteri di rete con Azure MFA tooensure che gli utenti usano verifica in due passaggi toobe in grado di connettersi toohello porta virtuale sul server VPN hello. Per gli utenti toobe consentito l'accesso, è necessario specificare la combinazione di nome utente/password con le informazioni utente hello dispone dei relativi controlli. Queste informazioni devono essere attendibili e non facilmente duplicabili, ad esempio un numero di telefono cellulare, un numero di rete fissa, un'applicazione in un dispositivo mobile e così via.

Toohello precedente la disponibilità di hello estensione dei criteri di rete per Azure, i clienti che desideravano tooimplement di verifica in due passaggi per integrato dei criteri di rete e gli ambienti Azure MFA era tooconfigure e gestiscono un Server separato di autenticazione a più fattori nell'ambiente locale hello come documentati in Gateway Desktop remoto e il Server Azure multi-Factor Authentication tramite RADIUS.

disponibilità Hello hello estensione di criteri di rete per Azure offre ora organizzazioni hello scelta toodeploy una soluzione di autenticazione a più fattori in locale o un basato su cloud MFA soluzione toosecure client l'autenticazione RADIUS.
 
## <a name="authentication-flow"></a>Flusso di autenticazione
Quando un utente si connette tooa porta virtuale su un server VPN, devono prima autenticarsi usando un'ampia gamma di protocolli, che consente l'uso di hello di una combinazione di nome utente/password e i metodi di autenticazione basata su certificato. 

In aggiunta tooauthenticating e verificare l'identità, gli utenti devono disporre hello appropriate autorizzazioni di accesso. In implementazioni semplici, vengono impostate le autorizzazioni di accesso che consentono l'accesso direttamente negli oggetti utente di Active Directory hello. 

 ![Proprietà utente](./media/nps-extension-vpn/image1.png)

Per le implementazioni semplici, ogni server VPN concede o nega l'accesso in base a criteri definiti in ogni server VPN locale.

Nelle implementazioni di dimensioni maggiori e più scalabile hello criteri che concedere o negare l'accesso VPN sono centralizzati nei server RADIUS. In questo caso, server VPN hello funge da server RADIUS tooa i messaggi di account e di un server di accesso (client RADIUS) che inoltra le richieste di connessione. tooconnect toohello porta virtuale sul server VPN hello, gli utenti devono essere autenticati e soddisfano le condizioni di hello definite in modo centralizzato nel server RADIUS. 

Quando l'estensione dei criteri di rete per Azure hello è integrato con hello dei criteri di rete, il flusso di autenticazione ha esito positivo di hello è il seguente:

1. server VPN Hello riceve una richiesta di autenticazione da un utente VPN che include hello nome utente e password tooconnect tooa risorsa, ad esempio una sessione Desktop remoto. 
2. Funge da client RADIUS, server VPN converte messaggio di richiesta di accesso RADIUS tooa richiesta hello e Invia messaggio di hello (password crittografata) server RADIUS (NPS) toohello in cui è installato hello estensione dei criteri di rete. 
3. Hello nome utente e la verifica della combinazione di password in Active Directory. Se hello nome utente / password non è corretta, hello Server RADIUS invia un messaggio di rifiuto di accesso. 
4. Se tutte le condizioni come specificato in hello richiesta di connessione dei criteri di rete e che siano soddisfatti i criteri di rete (ad esempio, ora del giorno o gruppo di restrizioni di appartenenza), hello estensione dei criteri di rete attiva una richiesta per l'autenticazione secondaria con Azure MFA. 
5. Azure MFA comunica con Azure Active Directory, recupera i dettagli dell'utente hello ed esegue l'autenticazione secondaria hello utilizzando il metodo hello configurato dall'utente hello (messaggio di testo, app per dispositivi mobili e così via). 
6. Al completamento dell'operazione di richiesta di autenticazione a più fattori hello Azure MFA comunica l'estensione dei criteri di rete di hello risultato toohello.
7. Dopo il tentativo di connessione hello è sia autenticato e autorizzato, server dei criteri di rete hello in cui è installato l'estensione hello invia un concessione di accesso RADIUS messaggio toohello server VPN (client RADIUS).
8. utente Hello viene concesso l'accesso toohello di porta virtuale sul server VPN e di stabilisce un tunnel VPN crittografato.

## <a name="prerequisites"></a>Prerequisiti
Questa sezione descrive i prerequisiti di hello necessari prima dell'integrazione di Azure MFA con hello Gateway Desktop remoto. Prima di iniziare, è necessario disporre di hello seguenti prerequisiti soddisfatti.

* Infrastruttura VPN
* Ruolo Servizi di accesso e criteri di rete
* Licenza di Azure MFA
* Software Windows Server
* Librerie
* Azure AD con sincronizzazione con AD in locale 
* ID GUID di Azure Active Directory

### <a name="vpn-infrastructure"></a>Infrastruttura VPN
In questo articolo si presuppone che si ha un'infrastruttura VPN di lavoro utilizzando Microsoft Windows Server 2016 sul posto e il server VPN hello non è attualmente configurato tooforward connessione richieste tooa RADIUS server. Si configurerà hello VPN infrastruttura toouse un server RADIUS centrale in questa Guida.

Se si ha un'infrastruttura di lavoro sul posto, è possibile creare rapidamente questa infrastruttura dal seguente hello orientamenti di numerose esercitazioni di programma di installazione VPN che sono disponibili nel Microsoft hello e siti di terze parti. 

### <a name="network-policy-and-access-services-nps-role"></a>Ruolo Servizi di accesso e criteri di rete

servizio di ruolo dei criteri di rete Hello fornisce funzionalità di client e server RADIUS hello. Si presume che è stato installato il ruolo di server NPS hello un server membro o controller di dominio nell'ambiente in uso. In questa guida si configurerà il protocollo RADIUS per una configurazione VPN. Installare il ruolo di server NPS hello in un server _altri_ rispetto al server VPN.

Per informazioni sull'installazione di ruoli di hello dei criteri di rete servizio Windows Server 2012 o versioni successive, vedere [installare un Server dei criteri di integrità Protezione accesso alla rete](https://technet.microsoft.com/library/dd296890.aspx). Lo strumento Protezione accesso alla rete è deprecato in Windows Server 2016. Per una descrizione di procedure consigliate per i criteri di rete, tra cui hello raccomandazione tooinstall dei criteri di rete in un controller di dominio, vedere [procedure consigliate per i criteri di rete](https://technet.microsoft.com/library/cc771746).

### <a name="licenses"></a>Licenze

È richiesta una licenza per Azure MFA, disponibile tramite una sottoscrizione di Azure AD Premium, Enterprise Mobility + Security (EMS) o MFA. Per ulteriori informazioni, vedere [come tooget Azure multi-Factor Authentication](multi-factor-authentication-versions-plans.md). A scopo di test, è possibile usare una sottoscrizione della versione di valutazione gratuita.

### <a name="software"></a>Software

Hello estensione dei criteri di rete richiede Windows Server 2008 R2 SP1 o versione successiva con installato il servizio ruolo dei criteri di rete hello. Tutti i passaggi di hello in questa guida sono stati eseguiti usando Windows Server 2016.

### <a name="libraries"></a>Librerie

è necessario i seguenti due librerie di Hello:

* [Visual C++ Redistributable Packages per Visual Studio 2013 (X64)](https://www.microsoft.com/download/details.aspx?id=40784)
* _Modulo di Microsoft Azure Active Directory per Windows PowerShell versione 1.1.166.0_ o successiva. Per la versione più recente di hello e le istruzioni di installazione, vedere [Microsoft Azure Active Directory PowerShell modulo rilasciare cronologia](https://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx).

Queste librerie non sono incluso nel pacchetto hello NPS estensione file di installazione (versione 0.9.1.2), nonostante la documentazione esistente che dichiara in caso contrario. Come minimo, è necessario installare i pacchetti hello Visual C++ Redistributable per Visual Studio 2013. Hello modulo dei Microsoft Azure Active Directory per Windows PowerShell è installato, se non è già presente, tramite uno script di configurazione che viene eseguito come parte del processo di installazione di hello. Non è disponibile alcuna necessità tooinstall questo modulo anticipatamente se non è già installato.

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a>Azure Active Directory con sincronizzazione con Active Directory locale 

hello toouse estensione dei criteri di rete, in locale gli utenti devono essere sincronizzati con Azure Active Directory e abilitati per multi-Factor Authentication. Questa guida presuppone che gli utenti locali siano sincronizzati con Azure Active Directory tramite AD Connect. Le istruzioni per abilitare gli utenti per MFA sono disponibili più avanti.
Per informazioni su Azure AD Connect, vedere [Integrare le directory locali con Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md). 

### <a name="azure-active-directory-guid-id"></a>ID GUID di Azure Active Directory 
tooinstall hello dei criteri di rete, è necessario tooknow hello GUID di hello Azure Active Directory. Nella sezione successiva hello vengono fornite istruzioni per la ricerca di hello GUID di hello Azure Active Directory.

## <a name="configure-radius-for-vpn-connections"></a>Configurare RADIUS per le connessioni VPN

Se è stato installato ruolo hello del server dei criteri di rete in un server membro, è necessario tooconfigure tooauthenticate e autorizzare i client VPN che richieda connessioni VPN. 

In questa sezione si presuppone che si è installato il ruolo di Server dei criteri di rete hello ma non configurati per l'utilizzo dell'infrastruttura.

>[!NOTE]
>Se si ha già un server VPN funzionante che usa un server RADIUS centralizzato per l'autenticazione, è possibile ignorare questa sezione.
>

### <a name="register-server-in-active-directory"></a>Registrare il server in Active Directory
toofunction correttamente in questo scenario, server dei criteri di rete hello deve toobe registrato in Active Directory.

1. Aprire Server Manager.
2. In Server Manager fare clic su **Strumenti** e quindi su **Server dei criteri di rete**. 
3. Nella console di Server dei criteri di rete hello, fare doppio clic su **dei criteri di rete (locale)**, quindi fare clic su **Registra server in Active Directory**. Fare clic su **OK** due volte.

 ![Server dei criteri di rete](./media/nps-extension-vpn/image2.png)

4. Lasciare aperta per la procedura successiva hello hello console.

### <a name="use-wizard-tooconfigure-radius-server"></a>Utilizzare Configurazione guidata server RADIUS di tooconfigure
È possibile utilizzare uno standard (basata su procedura guidata) o server di configurazione avanzate opzione tooconfigure hello RADIUS. In questa sezione si presuppone l'uso di hello hello basata su procedura guidata standard l'opzione di configurazione.

1. Nella console di Server dei criteri di rete hello, fare clic su **dei criteri di rete (locale)**.
2. In Configurazione standard selezionare **Server RADIUS per connessioni remote o VPN** e quindi fare clic su **Configurazione VPN o connessioni remote**.

 ![Configurare la rete VPN](./media/nps-extension-vpn/image3.png)

3. Pagina hello selezionare remote o tipo di connessioni di rete privata virtuale, selezionare **connessioni di rete privata virtuale**, fare clic su **Avanti**.

 ![Rete privata virtuale](./media/nps-extension-vpn/image4.png)

4. Nella pagina specificare connessioni remote o VPN hello scegliere **Aggiungi**.
5. In hello **client RADIUS nuovo** nella finestra di dialogo immettere un nome descrittivo, immettere il nome risolvibile hello o l'indirizzo IP del server VPN hello e immettere una password segreta condivisa. Creare una password segreta condivisa lunga e complessa. Registrare la password specificata, in base alle esigenze per i passaggi nella sezione successiva hello.

 ![Nuovo client RADIUS](./media/nps-extension-vpn/image5.png)

6. Fare clic su **OK** e quindi su **Avanti**.
7. In hello **configurare metodi di autenticazione** accettare selezione predefinita hello (autenticazione crittografata Microsoft versione 2 (MS-CHAPv2) o scegliere un'altra opzione e fare clic su **Avanti**.

  >[!NOTE]
  >Se si configura il protocollo EAP (Extensible Authentication Protocol), è necessario usare MS CHAPv2 o PEAP. Non sono supportate altre opzioni EAP.
 
8. Nella pagina specificare gruppi di utenti hello, fare clic su **Aggiungi** e selezionare un gruppo appropriato, se presente. In caso contrario, lasciare invariata la selezione hello toogrant vuoto accesso tooall gli utenti.

 ![Specificare i gruppi di utenti](./media/nps-extension-vpn/image7.png)

9. Fare clic su **Avanti**.
10. Nella pagina specificare i filtri IP hello, fare clic su **Avanti**.
11. Nella pagina specifica impostazioni di crittografia di hello, accettare le impostazioni predefinite di hello e fare clic su **Avanti**.

 ![Specificare la crittografia](./media/nps-extension-vpn/image8.png)

12. In hello specificare un nome dell'area di autenticazione, lasciare vuoto il nome di hello, accettare l'impostazione predefinita hello e fare clic su **Avanti**.

 ![Specificare un nome dell'area di autenticazione](./media/nps-extension-vpn/image9.png)

13. Nella pagina di client RADIUS e di connessioni di rete privata virtuale o hello completamento nuove connessioni remote, fare clic su **fine**.

 ![Completare le connessioni](./media/nps-extension-vpn/image10.png)

### <a name="verify-radius-configuration"></a>Verificare la configurazione RADIUS
In questa sezione illustra in dettaglio configurazione hello che è stato creato mediante Creazione guidata hello.

1. Nel server dei criteri di rete hello, nella console Criteri di rete (locale) hello, espandere i client RADIUS e selezionare **client RADIUS**.
2. Nel riquadro dei dettagli di hello, fare doppio clic su client RADIUS hello è stato creato mediante una procedura guidata e fare clic su **proprietà**. le proprietà di Hello per il client RADIUS (server VPN hello) devono essere simili toothose illustrato di seguito.

 ![Proprietà VPN](./media/nps-extension-vpn/image11.png)

3. Fare clic su **Annulla**.
4. Nel server dei criteri di rete hello nella console Criteri di rete (locale) hello espandere **criteri**e selezionare **criteri richiesta di connessione**. Dovrebbe essere criteri le connessioni VPN hello simile immagine hello riportata di seguito.

 ![Richieste di connessione](./media/nps-extension-vpn/image12.png)

5. In Criteri selezionare **Criteri di rete**. È necessario un criterio di connessioni di rete privata virtuale (VPN, Virtual Private Network) che è simile a immagine hello riportata di seguito.

 ![Proprietà di rete](./media/nps-extension-vpn/image13.png)

## <a name="configure-vpn-server-toouse-radius-authentication"></a>Configurare l'autenticazione RADIUS toouse Server VPN
In questa sezione, configurare l'autenticazione RADIUS toouse di hello VPN server. In questa sezione si presuppone che si dispone di una configurazione di lavoro del server VPN, ma non è stato configurato l'autenticazione RADIUS toouse di hello VPN server. Dopo aver configurato il server VPN hello, si conferma che la configurazione funziona come previsto.

>[!NOTE]
>Se si ha già una configurazione del server VPN funzionante che usa l'autenticazione RADIUS, è possibile ignorare questa sezione.
>

### <a name="configure-authentication-provider"></a>Configurare il provider di autenticazione
1. Sul server VPN hello, aprire Server Manager.
2. In Server Manager fare clic su **Strumenti** e quindi su **Routing e Accesso remoto**.
3. Nella console di Routing e accesso remoto hello, fare doppio clic su  **\[nome Server\] (local)**, quindi fare clic su **proprietà**.

 ![Routing e accesso remoto](./media/nps-extension-vpn/image14.png)
 
4. In hello **[nome Server} (locale) proprietà** finestra di dialogo fare clic su hello **sicurezza** scheda. 
5. In hello **sicurezza** scheda, in provider di autenticazione, fare clic su **l'autenticazione RADIUS**e quindi **configura**.

 ![Autenticazione RADIUS](./media/nps-extension-vpn/image15.png)
 
6. Nella finestra di dialogo autenticazione RADIUS hello, fare clic su **Aggiungi**.
7. In hello Aggiungi Server RADIUS, in nome Server, aggiungere hello nome o hello indirizzo IP del server RADIUS hello che è configurato nella sezione precedente hello.
8. Segreto condiviso, fare clic su **modifica** e aggiungere hello condivisa password segreta è stato creato e registrato in precedenza.
9. Timeout (secondi), modificare tooa valore hello tra **30** e **60**. Si tratta di un tempo sufficiente toocomplete hello secondo fattore di autenticazione tooallow necessarie.
 
 ![Aggiungere il server RADIUS](./media/nps-extension-vpn/image16.png)
 
10. Fare clic su **OK** fino a chiudere tutte le finestre di dialogo.

### <a name="test-vpn-connectivity"></a>Testare la connettività VPN
In questa sezione si conferma di client VPN hello è autenticato e autorizzato dal server RADIUS hello, quando si tenta di porta virtuale di tooconnect tooVPN. Questa sezione presuppone l'uso di Windows 10 come client VPN. 

>[!NOTE]
>Se è già configurato un server VPN di VPN client tooconnect toohello e aver salvato le impostazioni di hello, è possibile ignorare hello passaggi correlati tooconfiguring e il salvataggio di un oggetto di connessione VPN.
>

1. Nel computer client VPN fare clic su **Start** e quindi su **Impostazioni** (icona a forma di ingranaggio).
2. In Impostazioni di Windows fare clic su **Rete e Internet**.
3. Fare clic su **VPN**.
4. Fare clic su **Aggiungi connessione VPN**.
5. Aggiungere una connessione VPN specificare Windows (predefinito) come hello provider VPN, quindi hello completa i campi, come appropriato, rimanenti e fare clic su **salvare**. 

 ![Aggiungere la connessione VPN](./media/nps-extension-vpn/image17.png)
 
6. Aprire hello **centro rete e condivisione** nel Pannello di controllo.
7. Fare clic su **Modifica impostazioni scheda**.

 ![Modificare le impostazioni della scheda](./media/nps-extension-vpn/image18.png)

8. Connessione di rete VPN hello destro, quindi scegliere Proprietà. 

 ![Proprietà rete VPN](./media/nps-extension-vpn/image19.png)

9. In hello VPN proprietà finestra di dialogo, fare clic su hello **sicurezza** scheda. 
10. Nella scheda sicurezza hello garantisce che solo **Microsoft CHAP versione 2 (MS-CHAP v2)** sia selezionata e fare clic su OK.

 ![Consentire i protocolli](./media/nps-extension-vpn/image20.png)

11. Connessione VPN hello di mouse e scegliere **Connetti**.
12. Nella pagina Impostazioni hello, fare clic su **Connetti**.

Una connessione viene visualizzato nel Registro di protezione hello sul server RADIUS hello come 6272 ID evento, come illustrato di seguito.

 ![Proprietà dell'evento](./media/nps-extension-vpn/image21.png)

## <a name="troubleshoot-guide"></a>Guida per la risoluzione dei problemi
Si supponga che la configurazione VPN era in esecuzione prima configurato hello VPN server toouse un server RADIUS centralizzato per l'autenticazione e autorizzazione. In questo caso, è probabile che hello potrebbe essere causato da una configurazione errata di hello Server RADIUS o hello utilizzo di un nome utente non valido o una password. Ad esempio, se si utilizza il suffisso UPN alternativo di hello nomeutente hello, il tentativo di accesso hello potrebbe non riuscire (è consigliabile utilizzare hello stesso nome dell'Account per ottenere risultati ottimali). 

tootroubleshoot questi problemi, un toostart ideale è tooexamine hello registri eventi di sicurezza su hello server RADIUS. ricerca toosave per gli eventi, è possibile utilizzare hello in base al ruolo Server di accesso e criteri di rete visualizzazione personalizzata nel Visualizzatore eventi, come illustrato di seguito. ID evento 6273 indica gli eventi in cui hello Server dei criteri di rete negato l'accesso utente tooa. 

 ![Aprire il Visualizzatore eventi](./media/nps-extension-vpn/image22.png)
 
## <a name="configure-multi-factor-authentication"></a>Configurare Multi-Factor Authentication
Questa sezione fornisce istruzioni per abilitare gli utenti per MFA e configurare gli account per la verifica in due passaggi. 

### <a name="enable-multi-factor-authentication"></a>Abilitare Multi-Factor Authentication
In questa sezione si abilitano gli account Azure AD per MFA. Hello utilizzare **portale classico** tooenable utenti per l'autenticazione a più fattori. 

1. Aprire un browser e passare troppo[https://manage.windowsazure.com](https://manage.windowsazure.com). 
2. Accedere come amministratore hello.
3. Nel portale hello spostamento a sinistra di hello, fare clic su **ACTIVE DIRECTORY**.

 ![Directory predefinita](./media/nps-extension-vpn/image23.png)

4. Nella colonna nome hello, fare clic su **Directory predefinita** (o un'altra directory, se appropriato).
5. Nella pagina introduttiva hello, fare clic su **configura**.

 ![Impostazioni predefinite di configurazione](./media/nps-extension-vpn/image24.png)

6. Nella pagina Configura hello, scorrere verso il basso e, nella sezione di hello multi-factor authentication, fare clic su **Gestisci impostazioni servizio**.

 ![Gestire le impostazioni MFA](./media/nps-extension-vpn/image25.png)
 
7. Nella pagina di multi-factor authentication hello, rivedere le impostazioni di servizio predefinito hello e quindi fare clic su **utenti**. 

 ![Utenti MFA](./media/nps-extension-vpn/image26.png)
 
8. Nella pagina utenti hello, selezionare gli utenti di hello che desidera tooenable per l'autenticazione a più fattori e quindi fare clic su **abilitare**.

 ![Proprietà](./media/nps-extension-vpn/image27.png)
 
9. Quando viene chiesto, fare clic su **Abilita Multi-Factor Auth**.

 ![Abilitare MFA](./media/nps-extension-vpn/image28.png)
 
10. Fare clic su **Close**. 
11. Aggiornare la pagina hello. lo stato di autenticazione a più fattori Hello è tooEnabled modificato.

Per informazioni su come gli utenti tooenable multi-Factor Authentication, vedere [Introduzione ad Azure multi-Factor Authentication nel cloud hello](multi-factor-authentication-get-started-cloud.md). 

### <a name="configure-accounts-for-two-step-verification"></a>Configurare gli account per la verifica in due passaggi
Una volta che un account è stato abilitato per l'autenticazione a più fattori, gli utenti non sono in grado di toosign in tooresources governato dai criteri di autenticazione a più fattori hello fino a quando non sono correttamente configurati toouse un dispositivo attendibile per hello secondo fattore di autenticazione con utilizzato verifica in due passaggi.

In questa sezione si configura un dispositivo attendibile per l'uso con la verifica in due passaggi. Sono disponibili diverse opzioni disponibili per si tooconfigure queste operazioni, tra cui hello seguenti:

* **App per dispositivi mobili**. Installare l'app Microsoft Authenticator hello in un dispositivo Windows Phone, Android o iOS. A seconda dell'organizzazione, si è applicazione hello toouse richiesto in una delle due modalità: ricevere notifiche per le verifiche (una notifica viene inserita il dispositivo tooyour) o usare il codice di verifica (necessario tooenter una verifica del codice che Aggiorna ogni 30 secondi). 
* **Chiamata o SMS sul telefono cellulare**. È possibile ricevere una chiamata o un SMS automatico. Con l'opzione di chiamata telefonica hello, si risposta chiamata hello e si preme hello # sign tooauthenticate. Con l'opzione testo hello, è possibile rispondere toohello SMS o immettere il codice di verifica hello hello sign nell'interfaccia.
* **Chiamata al telefono dell'ufficio**. Questo processo è hello corrisponde a quello descritto per telefonate automatizzate precedente.

Seguire queste istruzioni per la configurazione di una notifica push tooreceive di dispositivo toouse hello app per dispositivi mobili per la verifica.

1. Accesso troppo[https://aka.ms/mfasetup](https://aka.ms/mfasetup) o in qualsiasi sito, ad esempio [https://portal.azure.com](https://portal.azure.com), in cui è necessario tooauthenticate utilizzando le credenziali di autenticazione a più fattori abilitata. 
2. Durante l'accesso con il nome utente e password, viene visualizzata una schermata che richiede tooset account hello per verifica aggiuntiva di sicurezza.

 ![Sicurezza aggiuntiva](./media/nps-extension-vpn/image29.png)

3. Fare clic su **Imposta ora**.
4. Nella pagina verifica aggiuntiva di sicurezza di hello, selezionare un tipo di contatto (telefono per l'autenticazione, telefono dell'ufficio o app per dispositivi mobili). Selezionare quindi un paese o un'area geografica e un metodo. metodo Hello varia in base al tipo di contatto selezionato. Ad esempio, se si sceglie di app per dispositivi mobili, è possibile selezionare se le notifiche di tooreceive per verificare o toouse un codice di verifica. passaggi di Hello che seguono si supponga di scegliere **app per dispositivi mobili** come hello tipo di contatto.

 ![Autenticazione tramite telefono](./media/nps-extension-vpn/image30.png)

5. Selezionare App per dispositivi mobili, fare clic su **Ricevi notifiche per la verifica** e quindi su **Imposta**. 

 ![Verifica tramite app per dispositivi mobili](./media/nps-extension-vpn/image31.png)
 
6. Se non è già fatto, installare l'app per dispositivi mobili autenticatore hello sul dispositivo. 
7. Seguire le istruzioni hello hello app per dispositivi mobili tooscan hello presentato codice a barre o immettere manualmente le informazioni di hello e quindi fare clic su **eseguita**.

 ![Configurare l'app per dispositivi mobili](./media/nps-extension-vpn/image32.png)

8. Nella pagina verifica aggiuntiva di sicurezza di hello, fare clic su **Contact me** e risposta toonotification inviati tooyour dispositivo.
9. Nella pagina verifica aggiuntiva di sicurezza di hello, immettere un numero di contatto nel caso in cui si perde l'accesso toohello app per dispositivi mobili e fare clic su **Avanti**.

 ![Numero del telefono cellulare](./media/nps-extension-vpn/image33.png)
 
10. In hello verifica aggiuntiva di sicurezza, fare clic su **eseguita**.

dispositivo Hello è ora configurato tooprovide un secondo metodo di verifica. Per informazioni sull'impostazione degli account per la verifica in due passaggi, vedere [Configurare l'account per la verifica in due passaggi](./end-user/multi-factor-authentication-end-user-first-time.md).

## <a name="install-and-configure-nps-extension"></a>Installare e configurare l'estensione NPS

In questa sezione vengono fornite istruzioni per la configurazione VPN toouse Azure MFA per l'autenticazione client con hello Server VPN.

Quando si installa e configura l'estensione dei criteri di rete hello, tutti l'autenticazione client basata su RADIUS che viene elaborato da questo server è necessario toouse Azure MFA. Se non tutti gli utenti VPN sono registrati in Azure MFA, è possibile impostare gli utenti di tooauthenticate un altro server RADIUS che non sono configurati toouse autenticazione a più fattori. Oppure è possibile creare una voce del Registro di sistema che consente agli utenti citata tooprovide secondo fattore di autenticazione, solo se sono registrati nell'autenticazione a più fattori. 

Creare un nuovo valore stringa denominato _REQUIRE_USER_MATCH in HKLM\SOFTWARE\Microsoft\AzureMfa_e impostare tooTRUE valore hello o FALSE. 

 ![Richiesta della corrispondenza utente](./media/nps-extension-vpn/image34.png)
 
Se il valore di hello è set tooTRUE o non è impostata, tutte le richieste di autenticazione sono richiesta di autenticazione a più fattori tooan soggetto. Se il valore di hello è impostato tooFALSE, problemi di autenticazione a più fattori vengono rilasciati solo toousers registrati in autenticazione a più fattori. Utilizzare solo hello impostazione FALSE durante il testing o in ambienti di produzione durante un periodo di tempo di caricamento.

### <a name="acquire-azure-active-directory-guid-id"></a>Acquisire l'ID GUID di Azure Active Directory

Come parte della configurazione di hello di hello estensione dei criteri di rete, è necessario toosupply credenziali di amministratore e hello ID Azure Active Directory per il tenant di Azure AD. Hello passaggi riportata di seguito viene illustrato come tooget hello ID del tenant.

1. Accedere al portale di Azure toohello [https://portal.azure.com](https://portal.azure.com) come amministratore globale di hello di hello Azure tenant.
2. Nel riquadro di spostamento sinistro di hello, fare clic su hello **Azure Active Directory** icona.
3. Fare clic su **Proprietà**.
4. toocopy gli Appunti toohello ID di Directory, seleziona hello **copia** icona.
 
 ![ID directory](./media/nps-extension-vpn/image35.png)

### <a name="install-hello-nps-extension"></a>Installare l'estensione dei criteri di rete hello
Hello estensione dei criteri di rete deve toobe installato in un server con criteri di rete hello e installato il ruolo Servizi di accesso (NPS) e che funzioni come server RADIUS hello nella progettazione. Non installare l'estensione dei criteri di rete hello sul Server di Desktop remoto.

1. Scaricare l'estensione dei criteri di rete hello da [https://aka.ms/npsmfa](https://aka.ms/npsmfa). 
2. Copia hello il programma di installazione eseguibile (NpsExtnForAzureMfaInstaller.exe) toohello server NPS.
3. Nel server dei criteri di rete hello, fare doppio clic su **NpsExtnForAzureMfaInstaller.exe**. Se richiesto, fare clic su **Esegui**.
4. In hello estensione dei criteri di rete per la finestra di dialogo di autenticazione a più fattori di Azure, esaminare condizioni di licenza software hello controllare **accetto toohello condizioni di licenza**, fare clic su **installare**.

 ![Estensione NPS](./media/nps-extension-vpn/image36.png)
 
5. In hello estensione dei criteri di rete per la finestra di dialogo di autenticazione a più fattori di Azure, fare clic su **Chiudi**.  

 ![Installazione completata](./media/nps-extension-vpn/image37.png) 
 
### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a>Configurare i certificati per l'utilizzo con l'estensione dei criteri di rete hello tramite uno script di PowerShell
comunicazioni protette tooensure e la garanzia, è necessario tooconfigure certificati per l'utilizzo dall'estensione dei criteri di rete hello. i componenti dei criteri di rete di Hello includono uno script di Windows PowerShell che configura un certificato autofirmato per l'utilizzo con criteri di rete. 

lo script di Hello esegue hello seguenti azioni:

* Crea un certificato autofirmato
* Associa una chiave pubblica del certificato tooservice principale in Azure AD
* Archivi hello certificato nell'archivio computer locale hello
* Concede l'accesso toohello chiave privata del certificato toohello utente di rete
* Riavvia il servizio Server dei criteri di rete

Se si desidera toouse i propri certificati, è necessario tooassociate hello pubblico del principio di servizio toohello certificato in Azure AD e così via.
script di hello toouse, fornire le credenziali amministrative di Azure Active Directory estensione hello e hello ID tenant di Azure Active Directory è stato copiato in precedenza. Eseguire script hello in ogni server dei criteri di rete in cui si installa l'estensione dei criteri di rete hello.

1. Aprire un prompt di Windows PowerShell come amministratore.
2. Al prompt di PowerShell hello digitare _cd 'c:\Programmi\Microsoft Files\Microsoft\AzureMfa\Config'_e premere **invio**.
3. Digitare _.\AzureMfsNpsExtnConfigSetup.ps1_ e premere **INVIO**. 
 * script Hello controlla toosee se è installato il modulo di Azure Active Directory PowerShell hello. Se non è installato, script hello verrà installato il modulo hello.
 
 ![PowerShell](./media/nps-extension-vpn/image38.png)
 
4. Al termine dello script hello verifica installazione hello del modulo di PowerShell hello, Visualizza la finestra di dialogo modulo di Azure Active Directory PowerShell hello. Nella finestra di dialogo hello, immettere le credenziali di amministratore di Azure AD e la password e fare clic su **Accedi**. 
 
 ![Accesso a PowerShell](./media/nps-extension-vpn/image39.png)
 
5. Quando richiesto, incollare l'ID tenant hello copiato negli Appunti toohello in precedenza e premere **invio**. 

 ![ID tenant](./media/nps-extension-vpn/image40.png)

6. script Hello crea un certificato autofirmato ed esegue altre modifiche alla configurazione. output di Hello è come immagine di hello illustrato di seguito.

 ![Certificato autofirmato](./media/nps-extension-vpn/image41.png)

7. Riavviare il server di hello.
 
### <a name="verify-configuration"></a>Verificare la configurazione
configurazione di hello tooverify, è necessario tooestablish una nuova connessione VPN con server VPN. Durante l'immissione correttamente le credenziali per l'autenticazione principale, hello connessione VPN attende hello autenticazione secondaria toosucceed prima che venga stabilita connessione hello, come illustrato di seguito. 

 ![Verificare la configurazione](./media/nps-extension-vpn/image42.png)

Se si autentica correttamente con il metodo di verifica secondaria hello configurati in precedenza in Azure MFA, si è connesso toohello risorse. Tuttavia, se l'autenticazione secondaria hello non ha esito positivo, è stato negato tooresource di accesso. 

Nell'esempio riportato di seguito, hello autenticatore hello app su un dispositivo Windows phone è l'autenticazione secondaria hello tooprovide utilizzato.

 ![Verificare l'account](./media/nps-extension-vpn/image43.png)

Dopo aver eseguito l'autenticazione con metodo secondario hello, sono concesse porta virtuale di accesso toohello sul server VPN hello. Tuttavia, poiché è stato richiesto toouse un metodo di autenticazione secondaria usando un'app per dispositivi mobili in un dispositivo attendibile, hello log nel processo è più sicuro sarebbero utilizzando solo un nome utente o la combinazione di password.

### <a name="view-event-viewer-logs-for-successful-logon-events"></a>Visualizzare i log del Visualizzatore eventi per individuare gli eventi di accesso riusciti
eventi di accesso riusciti tooview hello nei log di Visualizzatore eventi di Windows hello, è possibile emettere hello segue registro protezione di Windows nel server dei criteri di rete hello Windows PowerShell comando tooquery hello.

eventi di accesso riusciti tooquery nei registri di Visualizzatore eventi di sicurezza hello, utilizzare hello seguente comando,
* _Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL 

 ![Visualizzatore eventi di sicurezza](./media/nps-extension-vpn/image44.png)
 
È inoltre possibile visualizzare il Registro di protezione hello o hello servizi di accesso e criteri di rete visualizzazione personalizzata, come illustrato di seguito:

 ![Accesso ai criteri di rete](./media/nps-extension-vpn/image45.png)

Nel server di hello in cui è installato l'estensione dei criteri di rete hello per Azure MFA, è possibile trovare i registri applicazione Visualizzatore eventi estensione toohello specifico in **applicazioni e servizi Logs\Microsoft\AzureMfa**. 

* _Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL

 ![Numero di eventi](./media/nps-extension-vpn/image46.png)

## <a name="troubleshoot-guide"></a>Guida per la risoluzione dei problemi
Se la configurazione hello non funziona come previsto, tootroubleshoot di toostart un ottimo strumento è tooverify che hello utente è configurato toouse Azure MFA. Avere utente hello connettersi troppo[https://portal.azure.com](https://portal.azure.com). Se viene richiesta l'autenticazione secondaria ed possibile eseguire l'autenticazione, la configurazione di Azure MFA è corretta.

Se l'autenticazione a più fattori di Azure funziona per gli utenti di hello, esaminare i registri eventi rilevanti hello. Sono inclusi i registri eventi di protezione, Gateway è operativo e Azure MFA hello discussi sono trattati nella sezione precedente hello. 

Di seguito è illustrato un esempio di output di un log di sicurezza che mostra un evento di accesso non riuscito (ID evento 6273):

 ![Log di sicurezza](./media/nps-extension-vpn/image47.png)

Di seguito è un evento correlato dai registri AzureMFA hello:

 ![Log di Azure MFA](./media/nps-extension-vpn/image48.png)

tooperform avanzate di risoluzione dei problemi opzioni, consultare hello NPS formato file registro del database in cui è installato hello server NPS. Questi file di log vengono creati nella cartella _%SystemRoot%\System32\Logs_ come file di testo con valori delimitati da virgole. Per una descrizione di questi file di log, vedere [Interpret NPS Database Format Log Files](https://technet.microsoft.com/library/cc771748.aspx) (Interpretare i file di log in formato database di Server dei criteri di rete). 

le voci di Hello in questi file di log sono difficile toointerpret senza importarle in un foglio di calcolo o di un database. È possibile trovare un numero di IAS parser online tooassist in interpretazione hello i file di log. Di seguito è l'output di hello di un tale scaricabile [applicazione shareware](http://www.deepsoftware.com/iasviewer): 

 ![Applicazione shareware](./media/nps-extension-vpn/image49.png)

Infine, per altre opzioni di risoluzione dei problemi, è possibile usare uno strumento di analisi di protocolli, ad esempio Wireshark o [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx). Hello Wireshark seguente immagine mostra i messaggi di RADIUS hello tra server VPN hello e server dei criteri di rete hello.

 ![Microsoft Message Analyzer](./media/nps-extension-vpn/image50.png)

Per altre informazioni, vedere [Integrare l'infrastruttura NPS esistente con Azure Multi-Factor Authentication](multi-factor-authentication-nps-extension.md).  

## <a name="next-steps"></a>Passaggi successivi
[Come tooget Azure multi-Factor Authentication](multi-factor-authentication-versions-plans.md)

[Gateway Desktop remoto e server Azure Multi-Factor Authentication utilizzando RADIUS](multi-factor-authentication-get-started-server-rdg.md)

[Integrare le directory locali con Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md)

