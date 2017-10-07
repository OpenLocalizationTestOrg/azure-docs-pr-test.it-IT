---
title: aaaIntegrate un'app con una rete virtuale di Azure
description: Illustra come tooconnect un'app in Azure App Service tooa esistente o nuova rete virtuale di Azure
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: 90bc6ec6-133d-4d87-a867-fcf77da75f5a
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: ccompy
ms.openlocfilehash: a93c504481400245b02220b541a008a7c874d10a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-app-with-an-azure-virtual-network"></a>Integrare un'app in una rete virtuale di Azure
Questo documento vengono descritte funzionalità di integrazione di rete virtuale Azure App Service hello e Mostra come tooset, configurarlo con le App in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). Se non si ha familiarità con le reti virtuali di Azure (Vnet), questa è una funzionalità che consente di tooplace molte delle risorse di Azure in una rete routeable internet non è possibile controllare l'accesso a. Queste reti possono quindi essere reti locali tooyour connesso tramite una vasta gamma di tecnologie VPN. toolearn ulteriori informazioni sulle reti virtuali di Azure, iniziare con informazioni hello qui: [Panoramica di rete virtuale di Azure][VNETOverview]. 

Hello Azure App Service presenta due forme. 

1. sistemi multi-tenant Hello che supportano la gamma completa di hello di piani tariffari
2. funzionalità premium ambiente del servizio App (ASE) Hello, che consente di distribuire in una rete virtuale. 

Questo documento tratta dell'integrazione rete virtuale, ma non dell'ambiente del servizio app. Se si desidera ulteriori informazioni sulla funzionalità hello ASE toolearn, iniziare con informazioni hello qui: [introduzione di ambiente del servizio App][ASEintro].

Integrazione della rete virtuale fornisce il tooresources di accesso di app web nella rete virtuale, ma non concede all'app web di accesso privata tooyour dalla rete virtuale hello. Accesso al sito privata fa riferimento toomaking app accessibile solo da una rete privata, ad esempio all'interno di una rete virtuale di Azure. L'accesso privato al sito è disponibile solo con un ambiente del servizio app configurato con un servizio di bilanciamento del carico interno (ILB). Per informazioni dettagliate sull'uso di ASE un bilanciamento del carico interno, iniziare con articolo hello: [creazione e utilizzo di un ASE ILB][ILBASE]. 

Uno scenario comune in cui si utilizzerebbe l'integrazione della rete virtuale è abilitazione dell'accesso da database tooa app web o un servizio web in esecuzione in una macchina virtuale nella rete virtuale di Azure. Con l'integrazione della rete virtuale, non è necessario tooexpose un endpoint pubblico per le applicazioni nella VM ma può utilizzare indirizzi instradabile su internet non privato hello. 

funzionalità di integrazione della rete virtuale Hello:

* richiede un piano tariffario Standard, Premium o Isolated 
* funziona con reti virtuali classiche o di Resource Manager 
* supporta TCP e UDP
* funziona con le app Web, le app per dispositivi mobili e le app per le API
* consente un tooonly tooconnect app 1 rete virtuale alla volta
* Consente di toofive toobe reti virtuali è integrato con un piano di servizio App 
* Consente di hello stessa rete virtuale toobe utilizzato da più applicazioni in un piano di servizio App
* supporta un contratto di servizio con disponibilità del 99,9% a causa di contratto di servizio toohello su hello Gateway di rete virtuale

Tra le operazioni non supportate da Integrazione rete virtuale:

* montaggio di un'unità
* integrazione di AD 
* NetBios
* accesso al sito privato

### <a name="getting-started"></a>introduttiva
Ecco alcuni aspetti tookeep presente prima della connessione di rete virtuale tooa app web:

* Integrazione rete virtuale funziona solo con le app dei piani tariffari **Standard**, **Premium** o **Isolated**. Se si abilita la funzionalità hello e quindi tooan il piano di servizio App non supportato prezzi piano App perdere loro toohello connessioni reti virtuali in uso. 
* Se la rete virtuale di destinazione esiste già, deve avere VPN point-to-site abilitata con un gateway con routing dinamico prima di poter essere app tooan connesso. Non è possibile attivare la VPN da punto a sito se il gateway è configurato con il routing statico.
* Hello rete virtuale deve essere hello stessa sottoscrizione del Plan(ASP) di servizio App. 
* le app di Hello che si integrano con una rete virtuale usano hello DNS specificato per tale rete virtuale.
* Per impostazione predefinita le applicazioni di integrazione solo instradare il traffico in una rete virtuale in base a route hello definiti in una rete virtuale. 

## <a name="enabling-vnet-integration"></a>Abilitazione della funzionalità Integrazione rete virtuale
Questo documento è incentrato principalmente sull'utilizzo di hello portale di Azure per l'integrazione della rete virtuale. tooenable integrazione della rete virtuale con l'app tramite PowerShell, seguire le direzioni di hello qui: [la connessione di rete virtuale tooyour app tramite PowerShell][IntPowershell].

È necessario tooconnect opzione hello app tooa esistente o nuova rete virtuale. Se si crea una nuova rete come parte dell'integrazione, quindi inoltre la creazione di toojust hello rete virtuale, un gateway con routing dinamico è preconfigurato per l'utente e punto tooSite VPN è abilitato. 

> [!NOTE]
> La configurazione di una nuova integrazione di reti virtuali può richiedere diversi minuti. 
> 
> 

tooenable integrazione della rete virtuale, aprire l'app impostazioni e quindi selezionare la rete. Hello dell'interfaccia utente visualizzata offre tre opzioni di rete. Questa guida tratta solo la funzionalità Integrazione rete virtuale, anche se le connessioni ibride e gli ambienti del servizio app sono descritti più avanti in questo documento. 

Se l'app non è presente in hello prezzi piano corretta, hello dell'interfaccia utente consente tooscale tooa il piano superiore prezzi piano di propria scelta.

![][1]

### <a name="enabling-vnet-integration-with-a-pre-existing-vnet"></a>Abilitazione della funzionalità Integrazione rete virtuale con una rete virtuale preesistente
interfaccia utente di integrazione di rete virtuale Hello consente tooselect da un elenco delle reti virtuali. Hello reti virtuali classiche indicare che sono ad esempio con la parola hello "Classico" nel nome di rete virtuale toohello avanti tra parentesi. elenco Hello è ordinato in modo che hello VNets Gestione risorse vengono elencati per primi. In hello immagine illustrato di seguito è possibile vedere che è possibile selezionare solo una rete virtuale. Una rete virtuale può risultare disattivata per diversi motivi, ad esempio:

* Hello rete virtuale si trova in un'altra sottoscrizione che l'account ha accesso a
* Hello rete virtuale non dispone di tooSite punto abilitato
* Hello rete virtuale non dispone di un gateway con routing dinamico

![][2]

integrazione tooenable semplicemente fare clic su rete virtuale che si desidera toointegrate con hello. Dopo aver selezionato hello rete virtuale, l'app viene riavviato automaticamente per effetto di tootake modifiche hello. 

##### <a name="enable-point-toosite-in-a-classic-vnet"></a>Abilita punto tooSite in una rete virtuale classica
Se la rete virtuale non è un gateway né né tooSite punto, è necessario tooset il primo backup. toodo per una rete virtuale classica, passare toohello [portale di Azure] [ AzurePortal] e visualizzare elenco hello di Networks(classic) virtuale. Da qui, fare clic su rete hello toointegrate con desiderato e fare clic sulla casella hello in Essentials chiamato le connessioni VPN. Da qui è possibile creare la VPN punto toosite e anche fare in modo creare un gateway. Dopo che si naviga hello punto toosite con esperienza di creazione gateway è circa 30 minuti prima che sia pronto. 

![][8]

##### <a name="enabling-point-toosite-in-a-resource-manager-vnet"></a>Abilitazione tooSite punto in un gestore delle risorse di VNet
tooconfigure VNet un gestore delle risorse con un gateway e tooSite punto, è possibile utilizzare PowerShell come descritto in questo caso, [configurare una Point-to-Site connessione tooa rete virtuale con PowerShell] [ V2VNETP2S] o utilizzare hello portale di Azure come descritto in questo caso, [configura una Point-to-Site connessione tooa rete virtuale usando hello Azure portal][V2VNETPortal]. Hello UI tooperform questa funzionalità non è ancora disponibile. Si noti che è necessario toocreate certificati per la configurazione di hello tooSite punto. Quando ci si connette la rete virtuale di toohello WebApp viene configurato automaticamente. 

### <a name="creating-a-pre-configured-vnet"></a>Creazione di una rete virtuale preconfigurata
Se si desidera toocreate una nuova rete virtuale configurata con un gateway e Point-to-Site, hello servizio App di rete dell'interfaccia utente non ha hello funzionalità toodo tale ma solo per una rete virtuale di gestione risorse. Se si desidera toocreate una rete virtuale classica con un gateway e Point-to-Site, è necessario toodo questo manualmente tramite l'interfaccia utente di rete hello. 

toocreate VNet un gestore delle risorse tramite hello interfaccia utente di integrazione di rete virtuale, selezionare semplicemente **Crea nuova rete virtuale** e fornire il:

* Nome della rete virtuale
* Blocco di indirizzi della rete virtuale
* Nome della subnet
* Blocco di indirizzi della subnet
* Blocco di indirizzi del gateway
* Blocco di indirizzi della connessione da punto a sito

Se si desidera questo tooany tooconnect di rete virtuale altre reti, è consigliabile evitare il prelievo di spazio di indirizzi IP che si sovrappone a tali reti. 

> [!NOTE]
> Creazione di gestione risorse VNet con un gateway richiede circa 30 minuti e attualmente non si integra hello rete virtuale con l'app. Dopo aver creata la rete virtuale con gateway hello è necessario toocome tooyour indietro app interfaccia utente di integrazione di rete virtuale e selezionare nuova rete virtuale.
> 
> 

![][3]

Le reti virtuali di Azure in genere vengono create all'interno di indirizzi di rete privati. Da hello predefinito integrazione della rete virtuale funzionalità consente di instradare tutto il traffico destinato a tali intervalli di indirizzi IP in una rete virtuale. intervalli di indirizzi IP privati Hello sono:

* 10.0.0.0/8 - questo è hello stesso come 10.0.0.0 - 10.255.255.255
* 172.16.0.0/12 - questo è hello stesso come 172.16.0.0 - 172.31.255.255 
* 192.168.0.0/16 - questo è hello stesso come 192.168.0.0 - 192.168.255.255

Hello spazio degli indirizzi di rete virtuale deve toobe specificato nella notazione CIDR. Se non si ha familiarità con la notazione CIDR, è un metodo per specificare i blocchi di indirizzi utilizzando un indirizzo IP e un intero che rappresenta la maschera di rete hello. Come riferimento rapido, tenere presente che 10.1.0.0/24 equivale a 256 indirizzi e 10.1.0.0/25 equivale a 128 indirizzi. Un indirizzo IPv4 che termina con /32 equivale a 1 indirizzo. 

Se si imposta qui hello informazioni sul server DNS, che è impostato per la rete virtuale. Dopo la creazione della rete virtuale è possibile modificare queste informazioni da hello esperienze degli utenti di rete virtuale. Se si modifica hello DNS di hello rete virtuale, è necessario tooperform un'operazione di rete di sincronizzazione.

Quando si crea una rete virtuale classica utilizzando hello interfaccia utente di integrazione di rete virtuale, crea una rete virtuale in hello stesso gruppo di risorse dell'app. 

## <a name="how-hello-system-works"></a>Funzionamento del sistema hello
In hello include informazioni su questa funzionalità si basa sulle tooconnect tecnologia VPN Point-to-Site il tooyour app rete virtuale. Le app nei Siti Web di Microsoft Azure presentano un'architettura del sistema multi-tenant che preclude il provisioning di un'app direttamente in una rete virtuale come si fa con le macchine virtuali. Tramite la compilazione sulla tecnologia point-to-site limitiamo macchina rete accesso toojust hello virtuale che ospita l'applicazione hello. Accedere alla rete toohello viene ulteriormente limitato in tali host dell'applicazione in modo che le app possono accedere solo reti hello configurarli tooaccess. 

![][4]

Se non è configurato un server DNS con la rete virtuale, l'app sarà necessario toouse IP indirizzi tooreach risorse nella rete virtuale hello. Quando si utilizzano gli indirizzi IP, tenere presente che hello dei principali vantaggi di questa funzionalità che consente gli indirizzi privati toouse hello all'interno della rete privata. Se si imposta l'app di toouse gli indirizzi IP pubblici per una delle macchine virtuali, è quindi possibile non utilizza funzionalità di integrazione della rete virtuale hello e comunicano attraverso hello internet.

## <a name="managing-hello-vnet-integrations"></a>La gestione di integrazioni tra reti virtuali hello
Hello tooconnect possibilità e disconnettere tooa che rete virtuale è a livello di applicazione. Le operazioni che possono influire sulla hello integrazione della rete virtuale tra più applicazioni sono a livello di ASP. Dall'interfaccia utente che viene visualizzata a livello di app hello hello, è possibile ottenere informazioni dettagliate su una rete virtuale. Maggior parte delle stesse informazioni vengono inoltre visualizzate hello ASP livello hello. 

![][5]

Dalla pagina di hello lo stato della funzionalità di rete, è possibile visualizzare se l'applicazione è connessa tooyour rete virtuale. Se il gateway della rete virtuale è inattivo per qualsiasi motivo, la rete viene visualizzata come non connessa. 

informazioni di Hello è ora disponibile tooyou nell'app hello è hello stesso livello dell'interfaccia utente integrazione tra reti virtuali come le informazioni di dettaglio hello ricevute hello ASP. Nel dettaglio:

* Nome di rete virtuale - questo collegamento apre hello rete virtuale di Azure dell'interfaccia utente
* Posizione - rispecchia percorso hello di una rete virtuale. È possibile toointegrate con una rete virtuale in un altro percorso.
* -Stato del certificato sono presenti i certificati utilizzati toosecure hello VPN connessione tra l'applicazione hello e hello rete virtuale. Ciò indica un tooensure test siano sincronizzate.
* Lo stato del gateway, il gateway è necessario verso il basso per qualsiasi motivo quindi l'app non è possibile accedere alle risorse hello rete virtuale. 
* Spazio degli indirizzi di rete virtuale - hello uno spazio di indirizzi IP per la rete virtuale. 
* Spazio degli indirizzi punto tooSite - si tratta di spazio di indirizzi IP toosite punto hello per la rete virtuale. L'app viene comunicazione come proveniente da una delle hello in questo spazio di indirizzi IP. 
* Spazio di indirizzi toosite del sito - è possibile utilizzare sito tooSite VPN tooconnect tooyour la rete virtuale locale risorse o tooother rete virtuale. È necessario che configurato gli intervalli IP hello definita con la connessione VPN visualizzato qui.
* Server DNS: qui sono elencati gli eventuali server DNS configurati con la rete virtuale.
* Gli indirizzi IP indirizzato toohello rete virtuale: sono presenti un elenco di indirizzi IP della rete virtuale con routing definito per, e agli indirizzi visualizzati. 

Hello solo l'operazione da eseguire nella visualizzazione di app hello dell'integrazione della rete virtuale è toodisconnect l'app da hello rete virtuale è attualmente connesso. toodo questa semplicemente fare clic su Disconnetti nella parte superiore di hello. Questa azione non modifica la rete virtuale. Hello rete virtuale e la relativa configurazione, inclusi gateway hello rimane invariato. Se desideri quindi toodelete la rete virtuale, è necessario risorse di hello di eliminazione toofirst in esso inclusi gateway hello. 

Visualizza piano di servizio App Hello dispone di un numero di operazioni aggiuntive. È anche possibile accedervi in modo diverso rispetto a dall'applicazione hello. hello tooreach dell'interfaccia utente di rete di ASP semplicemente aprire l'interfaccia utente di ASP e scorrere verso il basso. fino a raggiungere l'elemento denominato Stato funzionalità di rete. L'elemento fornisce alcuni dettagli secondari sull'integrazione di reti virtuali. Facendo clic su questa interfaccia consente di aprire hello stato interfaccia utente funzionalità di rete. Se si fa quindi clic su "fare clic qui toomanage", hello dell'interfaccia utente che elenca le integrazioni tra reti virtuali in questo ASP apre hello.

![][6]

percorso di Hello del hello ASP è buona tooremember durante la ricerca nei percorsi di hello di reti virtuali che si sta integrando con hello. Quando hello rete virtuale si trova in un'altra posizione sono problemi di latenza toosee molto più probabili. 

le reti virtuali integrate con Hello è un promemoria per il numero di reti virtuali, che le app sono integrate con questa ASP e il numero è possibile disporre di. 

toosee aggiungere dettagli su ogni rete virtuale, fare clic sul hello rete virtuale in questione. Inoltre dettagli toohello che sono stati annotati in precedenza, si può anche visualizzare un elenco di App hello in questo ASP che usano tale rete virtuale. 

Riguardo tooactions vi sono due operazioni principali. Hello viene innanzitutto le route tooadd hello possibilità che l'unità di traffico lasciando l'app in una rete virtuale. seconda azione Hello è certificati toosync possibilità di hello e informazioni di rete.

![][7]

**Routing** come indicato in precedenza route hello definiti in una rete virtuale sono viene usata per indirizzare il traffico in rete virtuale dall'app. Sebbene in cui i clienti desiderano toosend aggiuntive il traffico in uscita da un'app in hello rete virtuale e per essi questa funzionalità viene fornita, esistono alcuni utilizzi. Cosa accade traffico toohello dopo che i clienti di hello toohow consente di configurare la rete virtuale. 

**I certificati** hello stato certificato riflette un segno di spunta eseguita da hello toovalidate di servizio App che i certificati di hello che si sono usando per la connessione VPN hello sono ancora valido. Quando è abilitata l'integrazione della rete virtuale, quindi se si tratta di toothat delle integrazione prima rete virtuale di hello da qualsiasi App in questo ASP è uno scambio di sicurezza di hello certificati tooensure della connessione hello obbligatorio. Insieme ai certificati hello si ottiene la configurazione del DNS hello, route e altre operazioni simili che descrivono la rete hello.
Se tali certificati o le informazioni di rete viene modificato, è necessario tooclick "Rete di sincronizzazione". **NOTA**: la sincronizzazione della rete provoca una breve interruzione della connettività tra l'app e la rete virtuale. Mentre l'app non viene riavviato, una perdita di connettività hello potrebbe causare il funzionamento di toonot del sito in modo corretto. 

## <a name="accessing-on-premises-resources"></a>Accesso alle risorse locali
Uno dei vantaggi di hello della funzionalità di integrazione della rete virtuale hello è che se è connesso alla rete virtuale tooyour locale rete con un tooSite sito VPN App può avere accesso alle risorse locali di tooyour dall'app. Per questo toowork potrebbe essere necessario tooupdate il gateway VPN locale con hello instrada per l'intervallo di IP tooSite punto. Quando hello sito tooSite VPN è prima di tutto configurare quindi gli script di hello utilizzati tooconfigure deve impostare i percorsi inclusi la VPN tooSite punto. Se si aggiunta hello VPN tooSite punto dopo aver creato il tooSite sito VPN, è necessario route hello tooupdate manualmente. Informazioni dettagliate su come toodo che variano per ogni gateway e non sono descritti di seguito. 

> [!NOTE]
> funzionalità di integrazione della rete virtuale Hello non si integra un'app con una rete virtuale che dispone di un ExpressRoute Gateway. Anche se è configurato il ExpressRoute Gateway hello in [modalità di coesistenza] [ VPNERCoex] hello integrazione della rete virtuale non funziona. Se sono necessarie risorse tooaccess tramite una connessione ExpressRoute, è quindi possibile utilizzare un [ambiente del servizio App][ASE], che viene eseguita in una rete virtuale.
> 
> 

## <a name="pricing-details"></a>Dettagli prezzi
Ci sono alcuni prezzi sfumature da prendere in considerazione quando si usa hello funzionalità di integrazione della rete virtuale. Vi sono addebiti correlati 3 toohello uso di questa funzionalità:

* Requisiti del piano tariffario ASP
* Costi di trasferimento dati
* Costi del gateway VPN

Per il toouse in grado di App toobe questa funzionalità, hanno bisogno toobe in un piano di servizio App Premium o Standard. Per altre informazioni sui costi, vedere i [prezzi del servizio app][ASPricing]. 

Scadenza modo toohello tooSite punto VPN vengono gestite, è sempre un addebito per i dati in uscita tramite la connessione a integrazione della rete virtuale anche se in rete virtuale hello hello stesso centro dati. toosee quali sono tali spese, andare al: [dettagli prezzi di trasferire dati][DataPricing]. 

ultimo elemento Hello è il costo di hello del gateway di rete virtuale hello. Se non è necessario gateway hello per qualcos'altro come sito tooSite VPN, quindi di pagamento per la funzionalità di integrazione della rete virtuale hello toosupport gateway. Per informazioni su questi costi, vedere i [prezzi di Gateway VPN][VNETPricing]. 

## <a name="troubleshooting"></a>Risoluzione dei problemi
Mentre la funzionalità hello è facile tooset, ciò non significa che l'esperienza sarà problema disponibile. In caso problemi di accesso l'endpoint desiderato vi sono alcune utilità, è possibile usare la connettività tootest dalla console di app hello. Le console disponibili sono due: Uno dalla console Kudu hello e hello altri console hello in grado di raggiungere in hello portale di Azure. console di Kudu toohello tooget dall'app passare tooTools -> Kudu. Questo è hello stesso che troppo [nomesito]. n e t. Una volta che toohello tooget relativo a apre semplicemente passare toohello Debug console scheda console ospitati del portale Azure quindi dall'app passare tooTools -> Console. 

#### <a name="tools"></a>Strumenti
il ping di strumenti Hello, nslookup e tracert non funzionano tramite la console hello a causa di vincoli toosecurity. void di hello toofill sono state aggiunti due strumenti. Funzionalità di ordine tootest DNS è stato aggiunto uno strumento denominato nameresolver.exe. sintassi di Hello è:

    nameresolver.exe hostname [optional: DNS Server]

È possibile utilizzare i nomi host hello nameresolver toocheck che l'applicazione dipende. In questo modo è possibile verificare se si dispone di un valore non è configurato con il server DNS o potrebbe non essere server DNS di accesso tooyour.

strumento Avanti Hello consente tootest per TCP connettività tooa host e porta combinazione. Questo strumento viene chiamato tcpping.exe e hello sintassi è:

    tcpping.exe hostname [optional: port]

utilità tcpping Hello indica se è possibile raggiungere una porta e un host specifico. Può visualizzare solo il completamento se: non è un'applicazione in ascolto su una combinazione di host e porta hello ed è l'accesso alla rete l'host specificato toohello di app e la porta.

#### <a name="debugging-access-toovnet-hosted-resources"></a>Debug tooVNet accesso risorse ospitate
L'app potrebbe non riuscire a raggiungere un host e una porta specifici per una serie di motivi. La maggior parte del tempo di hello è una delle tre operazioni:

* **Sia presente un firewall in hello modo** se è presente un firewall in modo hello, verrà raggiunto il timeout TCP hello. che in questo caso è di 21 secondi. Usare la connettività di hello tcpping strumento tootest. Timeout TCP può essere a causa di operazioni toomany oltre i firewall ma partire da qui. 
* **DNS non è accessibile** timeout DNS hello è tre secondi per il server DNS. Se si dispone di due server DNS, il timeout di hello è 6 secondi. Utilizzare nameresolver toosee se DNS funziona correttamente. Tenere presente che usino hello la rete virtuale è configurata con DNS non è possibile utilizzare nslookup.
* **Intervallo IP P2S non valido** intervallo IP di hello toosite punto deve toobe in intervalli IP privati hello RFC 1918 (10.0.0.0-10.255.255.255 / 172.16.0.0-172.31.255.255 / 192.168.0.0-192.168.255.255). Se l'intervallo hello utilizza indirizzi IP all'esterno che, ciò non funziona. 

Se il problema non rispondono a tali elementi, cerca innanzitutto per operazioni semplici di hello come: 

* Hello Gateway viene visualizzato come backup nel portale di hello?
* I certificati vengono visualizzati come sincronizzati?
* Chiunque ha modificare la configurazione di rete hello senza effettuare una rete"sincronizzazione" in ASP hello interessata? 

Se il gateway è inattivo, è necessario riattivarlo. Se i certificati non sono sincronizzati, Vai a visualizzazione ASP toohello dell'integrazione della rete virtuale e hit "Rete di sincronizzazione". Se si ritiene che è una configurazione di rete virtuale sono state apportate modifiche tooyour e non è stato sincronizzazione sarebbe con le pagine ASP, quindi passare vista ASP toohello dell'integrazione della rete virtuale e hit "Rete di sincronizzazione" Just come promemoria, causando una breve interruzione del servizio con la connessione di rete virtuale e le app . 

Se tutto è accettabile, è necessario toodig in un po' più approfondito:

* Sono sono le app usando le risorse di integrazione della rete virtuale tooreach in hello stessa rete virtuale? 
* Può passare toohello console di app e usare tcpping tooreach tutte le altre risorse in una rete virtuale? 

In presenza di una di hello precedente, quindi l'integrazione della rete virtuale è appropriato e problema hello è altra. Si tratta in cui ottiene toobe più complessa poiché non esiste alcun toosee semplice perché non è possibile raggiungere una host: porta. Alcune delle cause hello includono:

* è presente un firewall nell'host di impedire l'accesso toohello applicazione porta dall'intervallo di IP toosite punto. Il passaggio tra subnet spesso richiede l'accesso pubblico.
* L'host di destinazione è inattivo.
* L'applicazione è inattiva.
* era hello errato IP o nome host
* L'applicazione è in ascolto su una porta diversa da quella prevista. È possibile verificare che in tale host e usando "netstat - aon" dal prompt dei comandi cmd hello. Vengono visualizzati gli ID processo in ascolto e le relative porte. 
* i gruppi di sicurezza di rete configurati in modo tale che impediscono di host applicazioni tooyour di accesso e la porta dall'intervallo di IP toosite punto

Tenere presente che non si conosce quali IP dell'intervallo IP tooSite punto che verrà utilizzati dall'applicazione, pertanto è necessario accedere tooallow dall'intero intervallo hello. 

Di seguito è riportata la procedura di debug aggiuntiva:

* accedere a un'altra macchina virtuale in tooreach la rete virtuale e tentativo la risorsa host: porta da qui. A questo scopo è possibile usare alcune utilità ping TCP o telnet, se necessario. Hello scopo qui è toodetermine solo se la connettività è presente questo altre VM. 
* visualizzare un'applicazione in un'altra macchina virtuale e testare toothat accesso host e porta dalla console hello dall'app

#### <a name="on-premises-resources"></a>Risorse locali ####
Se l'applicazione non riesce a raggiungere le risorse locali, innanzitutto hello che è consigliabile controllare è se è possibile raggiungere una risorsa in una rete virtuale. Se funziona, provare a un'applicazione locale hello tooreach da una macchina virtuale nella rete virtuale hello. A questo scopo è possibile usare telnet o un'utilità ping TCP. Se la macchina virtuale non riesce a raggiungere la risorsa locale, verificare che la connessione VPN da sito tooSite sia funzionante. Se funziona, controllare hello operazioni indicati in precedenza e configurazione del gateway locale hello e lo stato. 

Ora se la rete virtuale ospitato VM può raggiungere il sistema locale, ma l'app non può quindi motivo hello è probabilmente una delle seguenti hello:

* i percorsi non sono configurati con gli intervalli IP punto toosite nel gateway locale
* i gruppi di sicurezza di rete bloccano l'accesso per l'intervallo di IP tooSite punto
* i firewall locale stanno bloccando il traffico dall'intervallo di IP tooSite punto
* si dispone di un Route(UDR) definito dall'utente in una rete virtuale che impedisce che il traffico tooSite punto basato su raggiungere la rete locale

## <a name="hybrid-connections-and-app-service-environments"></a>Connessioni ibride e ambienti del servizio App
Esistono tre funzionalità che consentono di accedere alle risorse di tooVNet ospitato. Sono:

* Integrazione rete virtuale
* connessioni ibride
* Ambienti del servizio app

Le connessioni ibride richiede tooinstall un agente di inoltro chiamato hello Manager(HCM) connessione ibrida nella rete. Hello HCM deve toobe tooconnect in grado di tooAzure nonché tooyour applicazione. Questa soluzione è particolarmente vantaggiosa se adottata da una rete remota, come la propria rete locale o un'altra rete ospitata sul cloud, poiché non richiede un endpoint accessibile da Internet. Hello HCM viene eseguito solo in Windows ed è possibile disporre di istanze toofive tooprovide la disponibilità elevata. Le connessioni ibride supporta solo TCP tuttavia e ogni endpoint HC dispone di combinazione di toomatch tooa host: porta specifica. 

funzionalità di ambiente del servizio App Hello consente toorun un'istanza di servizio App di Azure hello in una rete virtuale. In questo modo le app possono accedere alle risorse nella rete virtuale senza eseguire altri passaggi. Alcune di hello altri vantaggi di un ambiente del servizio App sono che è possibile utilizzare Dv2 basato su ruoli di lavoro con backup too14 GB di RAM. Un altro vantaggio è che è possibile scalare hello sistema toomeet le proprie esigenze. A differenza di hello multi-tenant ambienti in cui la pagina ASP istanze too20 limitata, in un ASE è possibile ridimensionare le istanze di too100 ASP. Una delle operazioni di hello che con una base che non sono presenti con integrazione della rete virtuale è che un ambiente del servizio App può funzionare con una VPN ExpressRoute. 

Mentre che alcuni utilizzano case si sovrappongono, nessuna di queste funzionalità può sostituire tutti hello ad altri utenti. Sapere quali toouse funzionalità esigenze tooyour collegati. ad esempio:

* Se uno sviluppatore e deve semplicemente toorun un sito in Azure e hanno accesso database hello nella workstation hello in scrivania, toouse cosa più semplice hello è connessioni ibride. 
* Se si una grande organizzazione che vuole tooput un numero elevato di proprietà web nel cloud pubblico hello e gestirli nella propria rete, è possibile toogo con hello ambiente del servizio App. 
* Se si dispone di un numero di servizio App ospitato App semplicemente volere tooaccess risorse in una rete virtuale, quindi integrazione della rete virtuale è toogo modo hello. 

Oltre a casi d'uso hello, esistono alcuni semplicità gli aspetti correlati. Se la rete virtuale è già connesso tooyour rete, quindi utilizzando l'integrazione della rete virtuale in locale o un ambiente del servizio App è un modo semplice tooconsume risorse locali. Nel hello altra parte, se la rete virtuale non è connessa una rete locale tooyour è molto che più tooset overhead backup toosite un sito VPN con la rete virtuale rispetto all'installazione hello HCM. 

Oltre hello differenze funzionali, vi sono anche prezzi differenze. funzionalità di ambiente del servizio App Hello è Premium offerta di servizio ma hello offre la maggior parte delle possibilità di configurazione di rete inoltre tooother importanti funzionalità. Integrazione della rete virtuale può essere utilizzato con Standard o Premium ASP e rappresenta la soluzione ideale per l'utilizzo in modo sicuro le risorse in una rete virtuale da multi-tenant di hello servizio App. Le connessioni ibride attualmente dipende da BizTalk account, che dispone dei prezzi di livelli di avviare disponibile e quindi ottengono progressivamente più costoso in base all'ammontare hello è necessario. Quando si tratta tuttavia tooworking tra molte reti, non siano disponibili altre funzionalità come le connessioni ibride, che consentono di risorse tooaccess oltre 100 reti separate. 

<!--Image references-->
[1]: ./media/web-sites-integrate-with-vnet/vnetint-upgradeplan.png
[2]: ./media/web-sites-integrate-with-vnet/vnetint-existingvnet.png
[3]: ./media/web-sites-integrate-with-vnet/vnetint-createvnet.png
[4]: ./media/web-sites-integrate-with-vnet/vnetint-howitworks.png
[5]: ./media/web-sites-integrate-with-vnet/vnetint-appmanage.png
[6]: ./media/web-sites-integrate-with-vnet/vnetint-aspmanage.png
[7]: ./media/web-sites-integrate-with-vnet/vnetint-aspmanagedetail.png
[8]: ./media/web-sites-integrate-with-vnet/vnetint-vnetp2s.png

<!--Links-->
[VNETOverview]: http://azure.microsoft.com/documentation/articles/virtual-networks-overview/ 
[AzurePortal]: http://portal.azure.com/
[ASPricing]: http://azure.microsoft.com/pricing/details/app-service/
[VNETPricing]: http://azure.microsoft.com/pricing/details/vpn-gateway/
[DataPricing]: http://azure.microsoft.com/pricing/details/data-transfers/
[V2VNETP2S]: http://azure.microsoft.com/documentation/articles/vpn-gateway-howto-point-to-site-rm-ps/
[IntPowershell]: http://azure.microsoft.com/documentation/articles/app-service-vnet-integration-powershell/
[ASEintro]: http://docs.microsoft.com/azure/app-service/app-service-environment/intro
[ILBASE]: http://docs.microsoft.com/azure/app-service/app-service-environment/create-ilb-ase
[V2VNETPortal]: https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal
[VPNERCoex]: http://docs.microsoft.com/en-us/azure/expressroute/expressroute-howto-coexist-resource-manager
[ASE]: http://docs.microsoft.com/azure/app-service/app-service-environment/intro
