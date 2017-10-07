---
title: aaaSecuring accesso tooAzure RemoteApp e oltre | Documenti Microsoft
description: Informazioni su come proteggere l'accesso tooAzure RemoteApp con accesso condizionale in Azure Active Directory
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: a19b0b09-ab26-4beb-80bb-33a46da39887
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 98dfe69e2f5fa5014b6eb3157e01f131c287134d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="securing-access-tooazure-remoteapp-and-beyond"></a>Protezione accesso tooAzure RemoteApp e oltre
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

In questo articolo viene verrà fornita una panoramica di come un amministratore può impostare un canale di proteggere l'accesso a partire dall'utente finale di hello, tramite Azure RemoteApp e terminano con una risorsa protetta, ad esempio un database SQL o un'altra applicazione back-end. obiettivo di Hello è toomake assicurarsi che solo gli utenti autorizzati hello riunione desiderato condizioni possono accedere le applicazioni remote e che hello back-end sicuro accessibile solo dall'ambiente di Azure RemoteApp hello controllato e non da altri percorsi.

Sono disponibili 3 aree principali salve deve toolook in:

![Considerazioni sull'accesso condizionale di Azure RemoteApp](./media/remoteapp-secureaccess/ra-conditionalenvironment.png)

Continuare a leggere per informazioni e le risposte alle domande toothese.

## <a name="who-can-access-hello-collection"></a>Chi può accedere raccolta hello?
messaggio per l'amministratore sceglie utenti hello che possano accedere alle applicazioni remote nell'insieme di hello. È possibile usare gli account aziendali o dell'istituto di istruzione di Azure Active Directory (Azure AD), in precedenza denominati "account aziendali", o gli account Microsoft, ad esempio @outlook.com. La maggior parte degli scenari aziendali di utilizzare gli account di Azure AD, consentono di utilizzare le funzionalità di accesso condizionale illustrate più avanti e sono inoltre scelta solo di hello per le raccolte di dominio. il resto di Hello di hello articolo si presuppone il che usano degli account Azure AD con Azure RemoteApp.

**Risultati ottenuti:**

Utilizzo di Azure AD account toocontrol accesso tooAzure che RemoteApp offre due operazioni:

1. È sempre sapere quali utenti possono accedere le applicazioni è stata pubblicata e accedere a tali applicazioni qualsiasi back-end si connettono hello.
2. Controlliamo hello sottostante AD Azure, è possibile creare e gli account utente di eliminazione, impostare i criteri password, utilizzano l'autenticazione a più fattori e così via. 

## <a name="how-is-hello-collection-accessed-from-where"></a>Come avviene insieme hello? Da dove?
In genere gli amministratori vogliono toodefine criteri per l'accesso a un ambiente con connessione Internet pubblico, ad esempio Azure RemoteApp. Ad esempio, desiderano tooensure che gli utenti che accedono ambiente hello dall'esterno alla rete aziendale hello accedano toouse multi-factor authentication (MFA) toogain; o forse devono essere bloccate completamente.

Azure RemoteApp consente agli amministratori funzionalità di hello disponibili tramite i criteri di accesso condizionale di Azure AD Premium tooset per il proprio ambiente di Azure RemoteApp. È inoltre possibile utilizzare report avanzati e avvisi toomonitor funzionalità modalità di accesso ambiente hello.

### <a name="how-tooset-up-conditional-access-for-azure-remoteapp"></a>Come tooset di accesso condizionale per Azure RemoteApp
È in corso toowalk tramite uno scenario di esempio: hello Azure RemoteApp amministratore ambiente toohello di tooblock accesso quando gli utenti sono di fuori di rete aziendale hello.

> [!NOTE]
> Si presuppone che l'aggiornamento AD Azure toohello livello Premium e che sia stato creato almeno una raccolta di Azure RemoteApp.
> 
> 

1. Nel portale di Azure fare clic su hello **Active Directory** scheda. Fare clic su directory hello si tooconfigure.
   
   Ricorda: L'accesso condizionale è una proprietà di directory e non di Azure RemoteApp, in modo tutta la configurazione viene eseguita a livello di directory hello. Questo significa anche occorre toobe hello directory amministratore toomake queste modifiche.
2. Fare clic su **applicazioni**, quindi fare clic su **Microsoft Azure RemoteApp** tooset di accesso condizionale. Si noti che è possibile configurare l'accesso condizionale per ogni singola applicazione "software come un servizio" nella directory.
   ![Configurazione dell'accesso condizionale per Azure RemoteApp](./media/remoteapp-secureaccess/ra-conditionalaccessscreen.png)
3. In hello **configura** scheda, impostare **abilitare le regole di accesso** tooON.
   ![Abilitare le regole di accesso per Azure RemoteApp](./media/remoteapp-secureaccess/ra-enableaccessrules.png)
4. È ora possibile configurare varie regole e scegliere chi tooapply a:
   
   1. Scegliere **bloccare l'accesso quando non al lavoro** toocompletely impedire agli utenti l'accesso a Azure RemoteApp dall'ambiente di rete hello specificate.
   2. Scegliere l'opzione hello sotto toodefine hello indirizzi IP che costituiscono la "rete attendibile". Tutti gli altri indirizzi verranno rifiutati.
5. Verificare la configurazione avviando il client Azure RemoteApp hello da un indirizzo IP di fuori intervallo hello specificato. Dopo avere eseguito l'accesso con le credenziali di Azure AD, verrà visualizzato un messaggio simile a questo:

![Accesso negato tooAzure RemoteApp](./media/remoteapp-secureaccess/ra-accessdenied.png)

### <a name="future-conditional-access-features"></a>Funzionalità di accesso condizionale future
il team di Azure Active Directory Hello funziona sulle nuove funzionalità di accesso condizionale. Gli amministratori saranno in grado di toocreate nuovi tipi di regole regole di percorso basato su rete. Non appena l'anteprima pubblica di nuove funzionalità di hello dovrebbe essere disponibile.

### <a name="how-toomonitor-access-tooazure-remoteapp"></a>Modalità di accesso tooAzure RemoteApp toomonitor
Toouse un grande funzionalità con accesso condizionale è una funzionalità di reporting di hello Azure Active Directory Premium. È possibile utilizzare i report toomonitor che accede al proprio ambiente e rilevare eventuali attività sospette.

Ad esempio, è possibile visualizzare nomi di hello di utenti hello che Azure RemoteApp, quante volte è stato ottenuto questo e quando.

1. Nel portale di Azure fare clic su **Active Directory**e quindi sulla directory.
2. Passare toohello **report** scheda.
3. Selezionare nell'elenco dei report hello **utilizzo dell'applicazione** in **integrato applicazioni**.
   
   Verranno visualizzate alcune statistiche aggregate per Azure RemoteApp. 
   ![Statistiche di accesso di Azure RemoteApp aggregate](./media/remoteapp-secureaccess/ra-accessstats.png)
4. Fare clic su hello applicazione tooreveal informazioni agli utenti l'accesso a Azure RemoteApp.
   ![Statistiche di accesso utente per Azure RemoteApp](./media/remoteapp-secureaccess/ra-userstats.png)

### <a name="summary"></a>Riepilogo
Con Azure Active Directory Premium è possibile impostare regole tooAzure RemoteApp di accesso (e altri software come un servizio le applicazioni disponibili tramite Azure AD). Le regole sono attualmente limitate toonetwork criteri di posizione in base ma verranno in futuro hello esteso tooother aspetti della gestione aziendale.

Azure AD Premium offre inoltre reporting e il monitoraggio di funzionalità che estendono ulteriormente hello controllo salve ha sull'ambiente di Azure RemoteApp.

## <a name="how-do-i-make-sure-my-secure-resource-is-accessible-only-from-my-azure-remoteapp-environment"></a>Come verificare che la risorsa sicura sia accessibile solo dall'ambiente Azure RemoteApp?
Nelle sezioni precedenti di questo articolo è incentrata sulla protezione di ambiente di Azure RemoteApp toohello di accesso. È stata eseguita che scegliendo utenti hello sono consentiti l'accesso e impostare il controllo di accesso regole toofurther sull'utilizzo di servizio hello.

Uno scenario comune per le distribuzioni di Azure RemoteApp è che le applicazioni remote hello necessitino toocommunicate con una risorsa di back-end, ad esempio un database SQL. Questa risorsa è ospitata in locale (ad esempio in una rete aziendale) o nel cloud hello (ad esempio in Azure IaaS). Gli amministratori desiderano spesso toomake accertarsi che risorse back-end hello accessibile solo dalle applicazioni distribuite tramite Azure RemoteApp e non, ad esempio da un'applicazione in esecuzione direttamente in PC un e l'accesso a Internet pubblico. Azure RemoteApp viene spesso visualizzato come hello-gestiti centralmente e ambiente protetto e pertanto l'unico percorso di hello attraverso il quale gli utenti devono interagire con hello risorse back-end.

soluzione hello è tooplace entrambi hello Azure RemoteApp ambiente e risorsa protetta di hello in hello stesso Azure rete virtuale (VNET). Se la risorsa di hello è in un altro sito, è possibile stabilire una connessione VPN da sito a sito, ad esempio un rete virtuale spanning hello data center di Azure toocreate e hello cliente nell'ambiente locale.

Azure RemoteApp supporta due tipi di distribuzione di raccolte in cui è possibile specificare la propria rete virtuale:

* Non appartenenti a un dominio: hello applicazioni hanno "di visibilità" di hello altre risorse nella rete virtuale hello. Ad esempio, questo può essere utilizzato tooconnect applicazioni tooa database SQL viene utilizzata l'autenticazione di SQL (applicazioni eseguono l'autenticazione utente hello direttamente nel database hello)
* Dominio: hello usate da RemoteApp di Azure le macchine virtuali sono tooa aggiunti a un controller di dominio nella rete virtuale hello. Ciò è utile quando le applicazioni di hello devono tooauthenticate su un Controller di dominio di Windows in risorse di back-end tooa accesso tooget ordine.
  ![Raccolta appartenente a un dominio in Azure RemoteApp](./media/remoteapp-secureaccess/ra-domainjoined.png)

### <a name="how-toocreate-a-secure-connection-between-azure-and-my-on-premises-environment"></a>Come toocreate una connessione sicura tra Azure e l'ambiente locale
Le opzioni di configurazione per connettere gli ambienti Azure e locali sono diverse. Una buona panoramica delle opzioni di hello è disponibile qui.

Con Azure RemoteApp necessario tooconfigure innanzitutto la rete virtuale e quindi utilizzarla durante il processo di creazione hello della raccolta. 

## <a name="hello-complete-solution"></a>soluzione completa di Hello
diagramma di Hello seguente mostra la soluzione completa di hello è stata creata in un canale protetto di accesso dall'utente finale di hello, RemoteApp tramite Azure (ARA), in risorse di back-end hello.
![Protezione di Azure RemoteApp](./media/remoteapp-secureaccess/ra-secureoverview.png) nella fase 1 si hello utenti selezionati e creare regole di accesso che determinano come ARA accessibili. Nel seguente esempio hello è consentire l'accesso solo per gli utenti che lavorano dalla rete aziendale hello. Gli utenti non conforme non saranno in qualsiasi ambiente ARA di tooaccess in grado di hello.
Nella fase 2 esposta risorse back-end hello solo tramite la configurazione di rete virtuale/VPN hello che si controllata. Azure RemoteApp è stato inserito in hello stessa rete virtuale. risultato finale Hello è che la risorsa hello solo è possibile accedere tramite ambiente ARA hello.

