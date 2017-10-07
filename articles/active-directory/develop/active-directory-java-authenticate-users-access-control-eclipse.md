---
title: aaaHow toouse il controllo di accesso (linguaggio) | Documenti Microsoft
description: Informazioni su come toodevelop e l'utilizzo di controllo di accesso con Java in Azure.
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 247dfd59-0221-4193-97ec-4f3ebe01d3c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: cbbce3b1a05eabf3b86a8cb91db1bde92dbb8960
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthenticate-web-users-with-azure-access-control-service-using-eclipse"></a>Come tooAuthenticate utenti Web con accesso controllo servizio Azure usando Eclipse
Questa guida illustra come toouse hello servizio Azure Access Control (ACS) all'interno di hello Azure Toolkit per Eclipse. Per ulteriori informazioni su ACS, vedere hello [passaggi successivi](#next_steps) sezione.

> [!NOTE]
> Hello filtro di controllo di Azure Access Services è una versione community technology preview. Come versione preliminare, non è formalmente supportata da Microsoft.
> 
> 

## <a name="what-is-acs"></a>Informazioni su ACS
La maggior parte degli sviluppatori non ha esperienza nell'ambito delle identità e in genere non desidera dedicare tempo a sviluppare meccanismi di autenticazione e autorizzazione per le applicazioni e i servizi. ACS è un servizio di Azure che fornisce un metodo semplice per l'autenticazione degli utenti che necessitano di tooaccess le applicazioni web e servizi senza la necessità di logica di autenticazione complessa toofactor nel codice.

Hello seguenti caratteristiche sono disponibile in ACS:

* Integrazione con Windows Identity Foundation (WIF).
* Supporto per i provider di identità Web più diffusi, tra cui Windows Live ID, Google, Yahoo! e Facebook.
* Supporto per Active Directory Federation Services (ADFS) 2.0.
* Un Open Data Protocol (OData)-servizio di gestione che fornisce l'accesso programmatico tooACS impostazioni di base.
* Portale di gestione che consente l'accesso amministrativo toohello le impostazioni di ACS.

Per altre informazioni sul servizio di controllo di accesso, vedere [Servizio di controllo di accesso 2.0][Access Control Service 2.0].

## <a name="concepts"></a>Concetti
ACS di Azure è basato su entità hello dell'identità basata sulle attestazioni, un approccio coerente toocreating i meccanismi di autenticazione per le applicazioni in esecuzione in locale o nel cloud hello. Identità basata sulle attestazioni fornisce un modo comune per le applicazioni e servizi tooacquire le informazioni di identità necessarie sugli utenti all'interno dell'azienda, in altre organizzazioni e su Internet hello.

attività di hello toocomplete in questa Guida, è necessario comprendere hello seguenti concetti:

**Client** -nel contesto di hello di questa procedura-tooguide, si tratta di un browser che sta tentando l'applicazione web di toogain accesso tooyour.

**Applicazione relying party (RP)** -applicazione un relying Party è un sito Web o servizio che usano l'outsourcing autorità di autenticazione tooone esterno. Nella terminologia di identità, diciamo che hello RP considera attendibile l'autorità. Questa guida illustra come tooconfigure il tootrust applicazione ACS.

**Token** : un token è una raccolta di dati di sicurezza rilasciata quando un utente viene autenticato. Contiene un set di *attestazioni*, gli attributi di hello utente autenticato. Un'attestazione può corrispondere al nome dell'utente, a un identificatore del ruolo svolto dall'utente, alla sua età e così via. Un token è firmato digitalmente in genere, il che significa può sempre essere tooits indietro origine dell'autorità di certificazione e il relativo contenuto non possa essere manomessa. Un'utente guadagni accesso tooa applicazione relying Party presentando un token valido emesso da un'autorità che considera attendibile l'applicazione relying Party hello.

**Provider di identità (IP)** : un provider di identità è un'autorità che autentica le identità degli utenti e rilascia token di sicurezza. lavoro effettivo di Hello del rilascio di token è implementato anche se un servizio speciale denominato la servizio Token di sicurezza (STS). Esempi tipici di provider di identità comprendono Windows Live ID, Facebook, archivi di utenti business (come Active Directory) e così via.
Una volta ACS tootrust configurato un indirizzo IP, sistema hello verrà accettati e convalidati i token emessi da tale IP. ACS può consentire a più indirizzi IP in una sola volta, che significa che, quando l'applicazione considera attendibile ACS, è possibile offrire immediatamente il hello tooall applicazione autenticati da hello tutti gli indirizzi IP che ACS considera attendibile per conto dell'utente.

**Provider di federazione (FP)** : i provider di identità (IP) hanno una conoscenza diretta degli utenti, li autenticano usando le relative credenziali e rilasciano attestazioni sulle informazioni disponibili sugli utenti. Un provider di federazione è un'autorità di tipo diverso, in quanto anziché autenticare gli utenti direttamente, funge da intermediario di autenticazione tra una relying party e uno o più indirizzi IP. Provider di identità e provider di federazione rilasciano token di sicurezza, quindi usano entrambi il Servizio token di sicurezza (STS). ACS è un provider di federazione.

**Il motore regole di ACS** -logica hello tootransform utilizzati i token in ingresso da tootokens gli indirizzi IP attendibili devono toobe utilizzati da hello RP viene codificato nel modulo di semplice le regole di trasformazione di attestazioni. ACS è dotato di un motore di regole che applica qualsiasi logica di trasformazione specificata per la relying party.

**Spazio dei nomi ACS** : lo spazio dei nomi costituisce la partizione di primo livello di ACS da usare per organizzare le impostazioni. Uno spazio dei nomi contiene un elenco di indirizzi IP attendibili, applicazioni relying Party hello desiderato tooserve, che si prevede che le regole di hello hello regola motore tooprocess i token in ingresso con e così via. Uno spazio dei nomi espone vari endpoint che verrà utilizzato da un'applicazione hello e il tooperform tooget ACS sviluppatore relativa funzione.

Hello figura riportata di seguito viene illustrato l'autenticazione ACS con un'applicazione web.

![Diagramma di flusso di ACS][acs_flow]

1. Hello client (in questo caso un browser) richiede una pagina hello RP.
2. Poiché hello richiesta non è ancora autenticato, hello relying Party reindirizza l'autorità di toohello utente hello che considera attendibili, ovvero ACS. Hello ACS presenta hello scelta hello degli indirizzi IP che sono state specificate per questa relying Party. l'utente Hello seleziona IP appropriato hello.
3. Hello client esamina la pagina di autenticazione toohello indirizzi IP e richiede toolog utente hello in.
4. Dopo l'autenticazione client hello (ad esempio, l'identità hello immissione delle credenziali), hello IP rilascia un token di sicurezza.
5. Dopo aver emesso un token di sicurezza, hello IP reindirizza hello client tooACS e client hello invia il token di sicurezza hello emesso da hello tooACS IP.
6. ACS convalida i token di sicurezza hello emesso da hello IP, gli input hello identità delle attestazioni nel token nel motore regole di hello ACS, calcola le attestazioni di identità output di hello e genera un nuovo token di sicurezza che contiene tali attestazioni di output.
7. ACS reindirizza hello client toohello RP. client Hello invia hello nuovo token di sicurezza rilasciato da ACS toohello RP. Hello RP convalida firma hello hello token di sicurezza rilasciato da ACS, hello attestazioni nel token di convalida e restituisce una pagina hello richiesto originariamente.

## <a name="prerequisites"></a>Prerequisiti
attività di hello toocomplete in questa Guida, è necessario seguente hello:

* Java Developer Kit (JDK) v 1.6 o versione successiva.
* IDE Eclipse per sviluppatori Java EE, Indigo o versione successiva. È possibile scaricare il pacchetto all'indirizzo <http://www.eclipse.org/downloads/>. 
* La distribuzione di un server Web basato su Java o un server applicazioni, come Apache Tomcat, GlassFish, JBoss Application Server o Jetty.
* Una sottoscrizione di Azure, che può essere ottenuta all'indirizzo <http://www.microsoft.com/windowsazure/offers/>.
* Aprile 2014 Hello Azure Toolkit per Eclipse, rilasciare o versione successiva. Per ulteriori informazioni, vedere [installazione hello Azure Toolkit per Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690946.aspx).
* Un certificato x. 509 viene toouse con l'applicazione. Questo certificato è necessario in entrambi i formati di certificato pubblico (.cer) e certificato di scambio di informazioni personali (.PFX). Le opzioni per la creazione di questo certificato verranno descritte più avanti in questa esercitazione.
* Conoscenza hello Azure compute emulatore e la distribuzione tecniche descritte in [la creazione di un'applicazione Hello World per Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx).

## <a name="create-an-acs-namespace"></a>Creare uno spazio dei nomi ACS
toobegin utilizzando il servizio di controllo di accesso (ACS) in Azure, è necessario creare uno spazio dei nomi ACS. spazio dei nomi Hello fornisce un ambito univoco per l'indirizzamento di risorse ACS all'interno dell'applicazione.

1. Accedere al hello [il portale di gestione di Azure][Azure Management Portal].
2. Fare clic su **Active Directory**. 
3. toocreate un nuovo spazio dei nomi di controllo di accesso, fare clic su **New**, fare clic su **servizi App**, fare clic su **controllo di accesso**, quindi fare clic su **creazione rapida** . 
4. Immettere un nome per lo spazio dei nomi hello. Azure consente di verificare che il nome hello sia univoco.
5. Selezionare l'area di hello in cui hello viene utilizzato lo spazio dei nomi. Per prestazioni ottimali hello, utilizzare l'area di hello in cui si distribuisce l'applicazione.
6. Se si dispone di più di una sottoscrizione, selezionare una sottoscrizione di hello che si desidera toouse per spazio dei nomi ACS hello.
7. Fare clic su **Crea**.

Azure crea e attiva hello dello spazio dei nomi. Attendere fino a quando non è stato hello del nuovo spazio dei nomi hello **Active** prima di continuare. 

## <a name="add-identity-providers"></a>Aggiunta di un provider di identità
In questa attività, aggiungere gli indirizzi IP toouse con l'applicazione relying Party per l'autenticazione. A scopo dimostrativo, questa attività viene illustrato come tooadd Windows Live come un indirizzo IP, ma è possibile usare uno qualsiasi di indirizzi IP elencati nel portale di gestione ACS hello hello.

1. In hello [il portale di gestione di Azure][Azure Management Portal], fare clic su **Active Directory**, selezionare uno spazio dei nomi di controllo di accesso e quindi fare clic su **Gestisci**. verrà visualizzata la finestra di Hello portale di gestione ACS.
2. Nel riquadro di spostamento a sinistra hello di hello portale di gestione ACS, fare clic su **provider di identità**.
3. Windows Live ID è abilitato per impostazione predefinita e non può essere eliminato. Ai fini di questa esercitazione, verrà usato solo Windows Live ID. Questa schermata è, tuttavia, in cui è possibile aggiungere altri indirizzi IP, fare clic su hello **Aggiungi** pulsante.

Windows Live ID è abilitato come provider di identità per lo spazio dei nomi ACS. Specificare quindi l'applicazione web Java (toobe creato in un secondo momento) come relying Party.

## <a name="add-a-relying-party-application"></a>Aggiungere un'applicazione relying party
In questa attività è configurare ACS toorecognize alle applicazioni web Java come un'applicazione relying Party valida.

1. Nel portale di gestione ACS hello, fare clic su **le applicazioni Relying party**.
2. In hello **Relying Party Applications** pagina, fare clic su **Aggiungi**.
3. In hello **Aggiungi applicazione Relying Party** pagina, hello seguenti:
   
   1. In **nome**, nome del tipo hello di hello RP. Ai fini di questa esercitazione, digitare **Azure Web App**.
   2. In **Mode** (Modalità) selezionare **Enter settings manually** (Immettere le informazioni manualmente).
   3. In **dell'area di autenticazione**, si applica tipo hello URI toowhich hello token di sicurezza rilasciato da ACS. Per questa attività digitare **http://localhost:8080/**.
      ![Area di autenticazione dell'applicazione relying party nell'emulatore di calcolo][relying_party_realm_emulator]
   4. In **Return URL** tipo hello URL toowhich ACS restituisce il token di sicurezza di hello. Per questa attività, digitare **http://localhost:8080/MyACSHelloWorld/index.jsp**
      ![URL restituito dell'applicazione relying party nell'emulatore di calcolo][relying_party_return_url_emulator]
   5. Accettare i valori predefiniti di hello resto hello dei campi di hello.
4. Fare clic su **Salva**.

È stato correttamente configurato l'applicazione web Java quando viene eseguita nell'emulatore di calcolo di Azure hello (in http://localhost:8080 /) toobe relying Party nello spazio dei nomi ACS. Successivamente, creare regole hello ACS Usa le attestazioni tooprocess per hello RP.

## <a name="create-rules"></a>Creazione di regole
In questa attività si definiscono regole di hello che determinano come attestazioni vengono passate da indirizzi IP tooyour RP. A scopo di hello di questa Guida, verrà semplicemente configurato valori e tipi di attestazione di input di ACS toocopy hello direttamente nel token di output di hello, senza il filtro o modificarli.

1. Nella pagina principale del portale di gestione ACS hello, fare clic su **gruppi di regole**.
2. In hello **gruppi di regole** pagina, fare clic su **Default Rule Group for App Web di Azure**.
3. In hello **Edit Rule Group** pagina, fare clic su **genera**.
4. In hello **generare regole: Default Rule Group for App Web di Azure** pagina, verificare che sia selezionata Windows Live ID e quindi fare clic su **genera**.    
5. In hello **Edit Rule Group** pagina, fare clic su **salvare**.

## <a name="upload-a-certificate-tooyour-acs-namespace"></a>Caricare uno spazio dei nomi ACS tooyour certificato
In questa attività si carica una. Certificato PFX che verrà utilizzato toosign le richieste di token create da spazio dei nomi ACS.

1. Nella pagina principale del portale di gestione ACS hello, fare clic su **certificati e chiavi**.
2. In hello **certificati e chiavi** pagina, fare clic su **Aggiungi** sopra **la firma di Token**.
3. In hello **aggiungere Token Signing Certificate or Key** pagina:
   1. In hello **utilizzato per** fare clic su **Relying Party Application** e selezionare **App Web di Azure** (che deve essere impostato in precedenza come nome hello dell'applicazione relying party).
   2. In hello **tipo** selezionare **certificato x. 509**.
   3. In hello **certificato** sezione, fare clic sul pulsante Sfoglia hello e passare i file del certificato x. 509 toohello che si desidera toouse. Si tratta di un file .PFX. Selezionare il file hello, fare clic su **aprire**, quindi immettere la password del certificato hello in hello **Password** casella di testo. Si noti che a fini di test è possibile utilizzare un certificato autofirmato. toocreate un certificato autofirmato, utilizzare hello **New** pulsante hello **libreria filtro ACS** (descritta più avanti), finestra di dialogo oppure utilizzare hello **encutil.exe** utilità da hello [sito Web del progetto] [ project website] di hello Azure Starter Kit per Java.
   4. Assicurarsi che **Make Primary** sia selezionato. Il **aggiungere Token Signing Certificate or Key** pagina dovrebbe essere simile toohello seguente.
       ![Aggiunta di un certificato di firma di token][add_token_signing_cert]
   5. Fare clic su **salvare** toosave le impostazioni e chiudere hello **aggiungere Token Signing Certificate or Key** pagina.

Esaminare le informazioni di hello hello integrazione dell'applicazione pagina e copia hello URI che sarà necessario tooconfigure il toouse di applicazione web Java ACS.

## <a name="review-hello-application-integration-page"></a>Pagina di integrazione dell'applicazione hello revisione
È possibile trovare tutte le informazioni di hello e hello codice necessario tooconfigure l'applicazione (applicazione relying Party Buongiorno) toowork web Java con ACS nella pagina di integrazione dell'applicazione hello di hello portale di gestione ACS. Queste informazioni sono necessarie per la configurazione dell'applicazione Web Java per l'autenticazione federata.

1. Nel portale di gestione ACS hello, fare clic su **integrazione dell'applicazione**.  
2. In hello **integrazione dell'applicazione** pagina, fare clic su **pagine di accesso**.
3. In hello **Login Page Integration** pagina, fare clic su **App Web di Azure**.

In hello **Login Page Integration: App Web di Azure** URL hello elencato nella pagina **opzione 1: pagina di accesso ospitata ACS tooan collegamento** verrà utilizzato nell'applicazione web Java. Questo valore sarà necessario quando si aggiunge hello Azure Access Control Services Filter libreria tooyour applicazione Java.

## <a name="create-a-java-web-application"></a>Creazione di un'applicazione Web Java
1. Nel menu hello in Eclipse fare clic su **File**, fare clic su **New**, quindi fare clic su **progetto Web dinamico**. (Se non viene visualizzato **progetto Web dinamico** elencati tra i progetti disponibili dopo aver fatto clic **File**, **New**, quindi hello seguente: fare clic su **File**, fare clic su **New**, fare clic su **progetto**, espandere **Web**, fare clic su **progetto Web dinamico**, fare clic su  **Successivamente**.) Ai fini di questa esercitazione, denominare il progetto di hello **MyACSHelloWorld**. (Assicurarsi usare questo nome, i passaggi successivi in questa esercitazione prevedono il toobe file WAR denominato MyACSHelloWorld). Verrà visualizzata una schermata simile toohello seguenti:
   
    ![Creazione di un progetto Hello World a titolo di esempio per ACS][create_acs_hello_world]
   
    Fare clic su **Finish**.
2. Nella visualizzazione Project Explorer di Eclipse espandere **MyACSHelloWorld**. Fare clic con il pulsante destro del mouse su **WebContent**, scegliere **New** e quindi fare clic su **JSP File**.
3. In hello **New JSP File** finestra di dialogo, il nome file di hello **index.jsp**. Mantenere cartella padre hello MyACSHelloWorld/WebContent, come illustrato nell'esempio hello:
   
    ![Aggiunta di un file JSP a titolo di esempio per ACS][add_jsp_file_acs]
   
    Fare clic su **Avanti**.
4. In hello **Select JSP Template** selezionare **New JSP File (html)** e fare clic su **fine**.
5. All'apertura di file di hello index.jsp in Eclipse, aggiungere testo toodisplay **ACS Hello World!** all'interno di hello esistente `<body>` elemento. L'aggiornamento `<body>` contenuto deve essere visualizzato come riportato di seguito hello:
   
        <body>
          <b><% out.println("Hello ACS World!"); %></b>
        </body>
   
    Salvare index.jsp.

## <a name="add-hello-acs-filter-library-tooyour-application"></a>Aggiungere l'applicazione di filtro ACS libreria tooyour hello
1. In Project Explorer di Eclipse fare clic con il pulsante destro del mouse su **MyACSHelloWorld**, scegliere **Build Path** (Percorso di compilazione) e quindi fare clic su **Configure Build Path** (Configura il percorso di compilazione).
2. In hello **Java Build Path** finestra di dialogo, fare clic su hello **librerie** scheda.
3. Fare clic su **Add Library**.
4. Fare clic su **Azure Access Control Services Filter (by MS Open Tech)** (Filtro servizi di controllo di accesso di Azure - di MS Open Tech) e quindi su **Next** (Avanti). Hello **Azure Access Control Services Filter** viene visualizzata una finestra di dialogo.  (hello **percorso** campo potrebbe essere un percorso diverso, a seconda di dove è stato installato, Eclipse e il numero di versione di hello potrebbe essere diverso, a seconda degli aggiornamenti software.)
   
    ![Aggiunta di una libreria di filtri ACS][add_acs_filter_lib]
5. Utilizzando un browser aprire toohello **Login Page Integration** pagina di hello portale di gestione, elencati in hello copia hello URL **opzione 1: pagina di accesso ospitata ACS tooan collegamento** campo e incollarlo in hello **Endpoint di autenticazione ACS** campo della finestra di dialogo Eclipse hello.
6. Utilizzando un browser aprire toohello **Edit Relying Party Application** pagina di hello portale di gestione, elencati in hello copia hello URL **dell'area di autenticazione** campo e incollarlo in hello **area di autenticazione della Relying Party**  campo della finestra di dialogo Eclipse hello.
7. All'interno di hello **sicurezza** sezione della finestra dialogo Eclipse hello, se si desidera toouse un certificato esistente, fare clic su **Sfoglia**, passare toohello certificato desiderato toouse, selezionarla, fare clic su  **Aprire**. Oppure, se si desidera toocreate un nuovo certificato, fare clic su **New** toodisplay hello **nuovo certificato** finestra di dialogo, quindi specificare nome del file con estensione pfx hello hello nuova password hello e nome del file con estensione cer hello certificato.
8. Controllare **certificato hello incorpora nel file WAR hello**. Incorporamento certificato hello in questo modo incluso nella distribuzione senza dover toomanually aggiungerlo come componente. (Se è invece necessario archiviare esternamente il certificato dal file WAR, è possibile aggiungere il certificato di hello come un componente del ruolo e deselezionare **certificato hello incorpora nel file WAR hello**.)
9. [Facoltativo] Mantenere l'opzione **Require HTTPS connections** selezionata. Se si imposta questa opzione, è necessario tooaccess l'applicazione utilizzando il protocollo HTTPS hello. Se non si desidera toorequire le connessioni HTTPS, deselezionare questa opzione.
10. Per una distribuzione emulatore di calcolo toohello il **filtro ACS di Azure** impostazioni avrà un aspetto simile toohello seguente.
    
    ![Impostazioni di filtro ACS di Azure per un toohello distribuzione emulatore di calcolo][add_acs_filter_lib_emulator]
11. Fare clic su **Finish**.
12. Fare clic su **Yes** nella finestra di dialogo che conferma la creazione di un file web.xml.
13. Fare clic su **OK** tooclose hello **Java Build Path** finestra di dialogo.

## <a name="deploy-toohello-compute-emulator"></a>Distribuire l'emulatore di calcolo toohello
1. In Project Explorer di Eclipse fare clic con il pulsante destro del mouse su **MyACSHelloWorld**, scegliere **Azure** e quindi fare clic su **Package for Azure** (Pacchetto per Azure).
2. In **Project name** (Nome progetto) digitare **MyAzureACSProject** e fare clic su **Next** (Avanti).
3. Selezionare un JDK e un server applicazioni. (Questi passaggi vengono descritti in dettaglio in hello [la creazione di un'applicazione Hello World per Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) esercitazione).
4. Fare clic su **Finish**.
5. Fare clic su hello **Run in Azure Emulator** pulsante.
6. Verrà avviata l'applicazione web Java nell'emulatore di calcolo hello, chiudere tutte le istanze del browser (in modo che tutte le sessioni del browser corrente non interferiscono con il test di account di accesso ACS).
7. Eseguire l'applicazione aprendo nel browser <http://localhost:8080/MyACSHelloWorld/> o <https://localhost:8080/MyACSHelloWorld/>, se è stata selezionata l'opzione **Require HTTPS connections** (Richiedi connessioni HTTPS). Verrà richiesto per un account di accesso di Windows Live ID, quindi è opportuno tenere toohello URL restituito specificato per l'applicazione relying party.
8. Al termine dell'operazione di visualizzazione dell'applicazione, fare clic su hello **Reimposta emulatore di Azure** pulsante.

## <a name="deploy-tooazure"></a>Distribuire tooAzure
tooAzure toodeploy, è necessario toochange hello relying party dell'area di autenticazione e URL restituito per lo spazio dei nomi ACS.

1. All'interno di hello portale di gestione di Azure, in hello **Edit Relying Party Application** , modificare **dell'area di autenticazione** toobe hello URL del sito distribuito. Sostituire **esempio** con nome DNS di hello specificato per la distribuzione.
   
    ![Area di autenticazione dell'applicazione relying party da utilizzare in produzione][relying_party_realm_production]
2. Modificare **URL restituito** toobe hello URL dell'applicazione. Sostituire **esempio** con nome DNS di hello specificato per la distribuzione.
   
    ![URL restituito dell'applicazione relying party da usare in produzione][relying_party_return_url_production]
3. Fare clic su **salvare** toosave l'aggiornata parte delle relying party dell'area di autenticazione e URL restituito cambia.
4. Mantenere hello **Login Page Integration** pagina Apri nel browser, sarà necessario toocopy da quest'ultimo a breve.
5. In Project Explorer di Eclipse fare clic con il pulsante destro del mouse su **MyACSHelloWorld**, scegliere **Build Path** (Percorso di compilazione) e quindi fare clic su **Configure Build Path** (Configura il percorso di compilazione).
6. Fare clic su hello **librerie** scheda, fare clic su **Azure Access Control Services Filter**, quindi fare clic su **modifica**.
7. Utilizzando un browser aprire toohello **Login Page Integration** pagina di hello portale di gestione, elencati in hello copia hello URL **opzione 1: pagina di accesso ospitata ACS tooan collegamento** campo e incollarlo in hello **Endpoint di autenticazione ACS** campo della finestra di dialogo Eclipse hello.
8. Utilizzando un browser aprire toohello **Edit Relying Party Application** pagina di hello portale di gestione, elencati in hello copia hello URL **dell'area di autenticazione** campo e incollarlo in hello **area di autenticazione della Relying Party**  campo della finestra di dialogo Eclipse hello.
9. All'interno di hello **sicurezza** sezione della finestra dialogo Eclipse hello, se si desidera toouse un certificato esistente, fare clic su **Sfoglia**, passare toohello certificato desiderato toouse, selezionarla, fare clic su  **Aprire**. Oppure, se si desidera toocreate un nuovo certificato, fare clic su **New** toodisplay hello **nuovo certificato** finestra di dialogo, quindi specificare nome del file con estensione pfx hello hello nuova password hello e nome del file con estensione cer hello certificato.
10. Mantenere **certificato hello incorpora nel file WAR hello** selezionata, presupponendo che si desidera tooembed hello certificato nel file WAR hello.
11. [Facoltativo] Mantenere l'opzione **Require HTTPS connections** selezionata. Se si imposta questa opzione, è necessario tooaccess l'applicazione utilizzando il protocollo HTTPS hello. Se non si desidera toorequire le connessioni HTTPS, deselezionare questa opzione.
12. Per una distribuzione tooAzure, le impostazioni del filtro ACS di Azure avrà un aspetto simile toohello seguente.
    
    ![Impostazioni del filtro ACS di Azure per la distribuzione in produzione][add_acs_filter_lib_production]
13. Fare clic su **fine** tooclose hello **Modifica libreria** finestra di dialogo.
14. Fare clic su **OK** tooclose hello **le proprietà per MyACSHelloWorld** finestra di dialogo.
15. In Eclipse, fare clic su hello **pubblicare tooAzure Cloud** pulsante. Rispondere a richieste toohello, analogamente a come fatto in hello **toodeploy tooAzure l'applicazione** sezione di hello [la creazione di un'applicazione Hello World per Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) argomento. 

Dopo l'applicazione web è stata distribuita, chiudere tutte le sessioni del browser di aprire, eseguire l'applicazione web e verrà richiesto l'URL dell'applicazione relying party toosign con le credenziali Windows Live ID, seguito da inviati toohello restituito.

Al termine utilizzando l'applicazione Hello World di ACS, memorizzare distribuzione hello toodelete (è possibile ottenere informazioni come una distribuzione in hello toodelete [la creazione di un'applicazione Hello World per Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) argomento).

## <a name="next_steps"></a>Passaggi successivi
Per un esame di hello Security asserzione Markup Language (SAML) restituita da un'applicazione tooyour ACS, vedere [come tooview SAML restituito dal servizio di controllo di accesso di Azure hello][How tooview SAML returned by hello Azure Access Control Service]. toofurther esplorare funzionalità ACS e tooexperiment con scenari più sofisticati, vedere [Access Control Service 2.0][Access Control Service 2.0].

Inoltre, questo hello di esempio utilizzato **certificato hello incorpora nel file WAR hello** opzione. Questa opzione rende il certificato di hello toodeploy semplice. Se invece si desidera tookeep certificato di firma separato dal file WAR, è possibile utilizzare hello tecnica seguente:

1. All'interno di hello **sicurezza** sezione di hello **Azure Access Control Services Filter** finestra di dialogo digitare **${env. JAVA_HOME}/mycert.cer** e deselezionare **certificato hello incorpora nel file WAR hello**. Se il nome del certificato in uso è diverso, modificare il nome del file mycert.cer di conseguenza. Fare clic su **fine** finestra di dialogo tooclose hello.
2. Certificato di hello copia come un componente nella distribuzione: In Project Explorer di Eclipse, espandere **MyAzureACSProject**, fare doppio clic su **WorkerRole1**, fare clic su **proprietà** , espandere **ruolo Azure**, fare clic su **componenti**.
3. Fare clic su **Aggiungi**.
4. All'interno di hello **Add Component** finestra di dialogo:
   
   1. In hello **importazione** sezione:
      1. Hello utilizzare **File** pulsante toonavigate toohello certificato toouse. 
      2. In **Method** (Metodo) selezionare **copy** (Copia).
   2. Per **come nome**, fare clic sulla casella di testo hello e accettare il nome di predefinito hello.
   3. In hello **Distribuisci** sezione:
      1. In **Method** (Metodo) selezionare **copy** (Copia).
      2. Per **toodirectory**, tipo **JAVA_HOME %**.
   4. Il **Add Component** finestra di dialogo dovrebbe essere simile toohello seguente.
      
       ![Aggiunta di un componente certificato][add_cert_component]
   5. Fare clic su **OK**.

A questo punto, il certificato verrà incluso nella distribuzione. Si noti che incorporare certificato hello in file WAR hello o aggiungerlo come distribuzione tooyour componente, è necessario tooupload hello certificato tooyour spazio dei nomi come descritto in hello [caricare uno spazio dei nomi ACS tooyour certificato] [ Upload a certificate tooyour ACS namespace] sezione.

[What is ACS?]: #what-is
[Concepts]: #concepts
[Prerequisites]: #pre
[Create a Java web application]: #create-java-app
[Create an ACS Namespace]: #create-namespace
[Add Identity Providers]: #add-IP
[Add a Relying Party Application]: #add-RP
[Create Rules]: #create-rules
[Upload a certificate tooyour ACS namespace]: #upload-certificate
[Review hello Application Integration Page]: #review-app-int
[Configure Trust between ACS and Your ASP.NET Web Application]: #config-trust
[Add hello ACS Filter library tooyour application]: #add_acs_filter_library
[Deploy toohello compute emulator]: #deploy_compute_emulator
[Deploy tooAzure]: #deploy_azure
[Next steps]: #next_steps
[project website]: http://wastarterkit4java.codeplex.com/releases/view/61026
[How tooview SAML returned by hello Azure Access Control Service]: active-directory-java-view-saml-returned-by-access-control.md
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[Windows Identity Foundation]: http://www.microsoft.com/download/en/details.aspx?id=17331
[Windows Identity Foundation SDK]: http://www.microsoft.com/download/en/details.aspx?id=4451
[Azure Management Portal]: https://manage.windowsazure.com
[acs_flow]: ./media/active-directory-java-authenticate-users-access-control-eclipse/ACSFlow.png

<!-- Eclipse-specific -->
[add_acs_filter_lib]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibrary.png
[add_acs_filter_lib_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibraryEmulator.png
[add_acs_filter_lib_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibraryProduction.png

[relying_party_realm_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyRealmEmulator.png
[relying_party_return_url_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyReturnURLEmulator.png
[relying_party_realm_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyRealmProduction.png
[relying_party_return_url_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyReturnURLProduction.png
[add_cert_component]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddCertificateComponent.png
[add_jsp_file_acs]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddJSPFileACS.png
[create_acs_hello_world]: ./media/active-directory-java-authenticate-users-access-control-eclipse/CreateACSHelloWorld.png
[add_token_signing_cert]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddTokenSigningCertificate.png

