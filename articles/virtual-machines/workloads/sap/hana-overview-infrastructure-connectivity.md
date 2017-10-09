---
title: "aaaInfrastructure e connettività tooSAP HANA in Azure (istanze di grandi dimensioni) | Documenti Microsoft"
description: "Configurare toouse infrastruttura richiede la connettività SAP HANA in Azure (istanze di grandi dimensioni)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0af34fbd82413bf63981036a76eaa264d8299ec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-infrastructure-and-connectivity-on-azure"></a>Infrastruttura e connettività a SAP HANA (istanze di grandi dimensioni) in Azure 

Alcune definizioni prima di leggere questa guida. In [Panoramica e architettura di SAP HANA (istanze Large) in Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) vengono illustrate le due classi diverse di istanze Large di Hana con:

- S72, S72m, S144, S144m, S192 e S192m, con cui verrà fatto riferimento hello tooas 'una classe Type' di SKU.
- S384, S384m, S384xm, S576, S768 e S960, con cui verrà fatto riferimento tooas hello 'Class Type II' di SKU.

gli identificatori di classe Hello sono toobe corso utilizzati hello istanza di grandi dimensioni HANA documentazione tooeventually riferimento toodifferent funzionalità e requisiti di base per gli SKU istanza grande HANA.

Altre definizioni di uso frequente includono:
- **Indicatore di istanza di grandi dimensioni:** uno stack infrastruttura hardware SAP HANA TDI certificate e dedicati toorun le istanze di SAP HANA in Azure.
- **SAP HANA in Azure (istanze di grandi dimensioni):** nome ufficiale per l'offerta di hello in Azure toorun HANA istanze in SAP HANA TDI Certificate hardware che viene distribuito in timbri di istanza di grandi dimensioni in diverse aree di Azure. Hello correlati termine **istanza grande HANA** è l'abbreviazione di SAP HANA in Azure (istanze di grandi dimensioni) e viene ampiamente utilizzata questa Guida alla distribuzione tecnica.
 

Dopo l'acquisto di hello di SAP HANA in Azure (istanze di grandi dimensioni) è stato finalizzato tra i team dell'account aziendale Microsoft hello, hello informazioni seguenti sono richiesto da Microsoft toodeploy HANA grandi istanza unità:

- Nome del cliente
- Informazioni di contatto aziendali (inclusi indirizzo e-mail e numero di telefono)
- Informazioni di contatto tecniche (inclusi indirizzo e-mail e numero di telefono)
- Informazioni di contatto di rete tecniche (inclusi indirizzo e-mail e numero di telefono)
- Area di distribuzione di Azure: Stati Uniti occidentali, Stati Uniti orientali, Australia orientale, Australia sudorientale, Europa occidentale e Nord Europa a partire da luglio 
- 2017)
- Confermare l'SKU (configurazione) di SAP HANA in Azure (istanze grandi)
- Come già descritti in dettaglio in hello panoramica e documento sull'architettura HANA istanze di grandi dimensioni, per ogni area di Azure viene distribuito in:
    - / 29 intervallo di indirizzi IP per le connessioni Expressroute P2P che si connettono a istanze di grandi dimensioni tooHANA reti virtuali di Azure
    - Blocco CIDR di un /24 utilizzato per hello Pool IP Server HANA grandi dimensioni istanze
- valori intervallo indirizzi IP Hello utilizzati nell'attributo di spazio degli indirizzi di rete virtuale hello di ogni rete virtuale di Azure che si connette toohello HANA istanze di grandi dimensioni
- Dati per ogni sistema di istanze HANA di grandi dimensioni:
  - Nome host da usare, preferibilmente con un nome di dominio completo
  - Indirizzo IP desiderato per unità di istanza di grandi dimensioni HANA hello fuori intervallo di indirizzi del Pool di Server IP - hello tenere presente che hello primi 30 degli indirizzi IP in hello Pool IP Server intervallo di indirizzi sono riservati per scopi interni all'interno delle istanze di grandi dimensioni HANA
  - Nome di SID di SAP HANA per l'istanza di SAP HANA hello (volumi di disco correlati a SAP HANA hello toocreate obbligatorio). Hello HANA SID è necessaria per la creazione di autorizzazioni di hello per <sidadm> volumi NFS hello ricevono unità istanza grande HANA toohello associata. Inoltre viene utilizzato come uno dei componenti del nome hello hello di volumi di dischi che è montati. Se si desidera toorun più di un'istanza HANA nell'unità di hello, è necessario toolist più HANA SID. ognuno dei quali ottiene un set separato di volumi assegnati.
  - Hello groupid hello hana sidadm utente dispone in hello del sistema operativo Linux è necessario toocreate hello necessarie correlate a SAP HANA volumi. installazione di SAP HANA Hello in genere Crea gruppo sapsys hello con un id gruppo di 1001. utente hana sidadm Hello fa parte di tale gruppo
  - Hello userid hello hana sidadm utente dispone in hello del sistema operativo Linux è necessario toocreate hello necessarie correlate a SAP HANA volumi. Se si eseguono più istanze HANA su unità hello, è necessario toolist tutti hello <sid>adm utenti 
- ID sottoscrizione di Azure per hello sottoscrizione di Azure toowhich SAP HANA in istanze di grandi dimensioni HANA Azure sta toobe connessi direttamente. L'ID sottoscrizione fa riferimento a hello sottoscrizione di Azure, che verrà toobe addebitato hello unità HANA istanza di grandi dimensioni.

Dopo aver fornito hello informazioni disposizioni Microsoft SAP HANA in Azure (istanze di grandi dimensioni) e restituirà hello informazioni necessarie toolink le reti virtuali di Azure tooHANA istanze di grandi dimensioni e tooaccess hello istanza grande HANA unità.

## <a name="connecting-azure-vms-toohana-large-instances"></a>La connessione a istanze di grandi dimensioni tooHANA macchine virtuali di Azure

Come già accennato nel [Panoramica di SAP HANA (istanze di grandi dimensioni) e l'architettura in Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) come distribuzione minimo di istanze di grandi dimensioni HANA hello con livello di applicazione hello SAP in Azure ha un aspetto:

![Rete virtuale di Azure connessa tooSAP HANA in Azure (istanze di grandi dimensioni) e locale](./media/hana-overview-architecture/image3-on-premises-infrastructure.png)

Esaminando più da vicino su hello sul lato di rete virtuale di Azure, è realizzare hello necessario per:

- definizione di Hello di una rete virtuale di Azure che è corso toobe utilizzato toodeploy hello macchine virtuali del livello dell'applicazione SAP hello in.
- Ciò automaticamente significa che una subnet predefinita in hello è definito rete virtuale di Azure che è effettivamente hello uno utilizzato toodeploy hello macchine virtuali in.
- Hello rete virtuale di Azure creata deve toohave almeno una subnet VM e una subnet del ExpressRoute Gateway. Queste subnet devono essere assegnate a intervalli di indirizzi IP hello come descritto nelle seguenti sezioni hello e specificati.

In tal caso, vediamo un po' più vicino in hello creazione della rete virtuale di Azure HANA istanze di grandi dimensioni

### <a name="creating-hello-azure-vnet-for-hana-large-instances"></a>Creazione di rete virtuale di Azure hello HANA istanze di grandi dimensioni

>[!Note]
>Hello rete virtuale di Azure per l'istanza di grandi dimensioni HANA deve essere creata usando il modello di distribuzione del hello Azure Resource Manager. modello distribuzione di Azure precedente Hello, comunemente noto come modello di distribuzione classica, non è supportato con hello soluzione HANA istanza di grandi dimensioni.

Hello rete virtuale può essere creati utilizzando hello portale di Azure, PowerShell, un modello di Azure o CLI di Azure (vedere [creare una rete virtuale usando il portale di Azure hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). In hello l'esempio seguente, viene analizzato in una rete virtuale creata tramite hello portale di Azure.

Se si osserva nelle definizioni di hello di una rete virtuale di Azure tramite hello portale di Azure, è opportuno esaminare in alcune definizioni di hello e quelli correlazione toowhat è l'elenco di intervalli di indirizzi IP diversi. Come si parla hello **spazio degli indirizzi**, si intende lo spazio degli indirizzi hello hello rete virtuale di Azure è consentito toouse. Questo spazio di indirizzi è l'intervallo di indirizzi hello hello rete virtuale viene utilizzato per la propagazione delle route BGP. Lo **Spazio indirizzi** viene visualizzato qui:

![Spazio indirizzi della rete virtuale Azure visualizzata in hello portale di Azure](./media/hana-overview-connectivity/image1-azure-vnet-address-space.png)

In caso di hello precedente, con 10.16.0.0/16, hello rete virtuale di Azure è stato specificato un toouse intervallo di indirizzi IP di piuttosto grande e "wide". Significa che tutti gli intervalli di indirizzi IP hello successive subnet all'interno di questa rete virtuale possono avere i relativi intervalli all'interno di tale spazio di indirizzi' '. In genere non è consigliabile specificare un intervallo di indirizzi così ampio per una singola rete virtuale in Azure. Ma ottenere un ulteriore passaggio, verrà ora esaminato in subnet hello definita in hello rete virtuale di Azure:

![Subnet di rete virtuale di Azure e relativi intervalli di indirizzi IP](./media/hana-overview-connectivity/image2b-vnet-subnets.png)

Viene esaminata una rete virtuale con una prima subnet della macchina virtuale denominata "default" e una subnet denominata "GatewaySubnet".
Nella seguente sezione di hello, facciamo riferimento toohello intervallo di indirizzi IP della subnet hello, che è stato chiamato 'default' nella grafica hello come **intervallo di indirizzi IP di subnet VM di Azure**. In hello le sezioni seguenti, si fa riferimento toohello intervallo di indirizzi IP della Subnet del Gateway hello come **intervallo di indirizzi IP di Subnet Gateway di rete virtuale**. 

In caso di hello illustrato grafica hello due precedenti, vedrai che hello **spazio degli indirizzi di rete virtuale** copre entrambe, hello **intervallo di indirizzi IP di subnet VM di Azure** e hello **indirizzo IP di Subnet Gateway di rete virtuale intervallo**. 

In altri casi in cui è necessario tooconserve o essere specifiche con gli intervalli di indirizzi IP, è possibile limitare hello **spazio degli indirizzi di rete virtuale** di una rete virtuale toohello determinati intervalli utilizzato da ogni subnet. In questo caso, è possibile definire hello **spazio degli indirizzi di rete virtuale** di una rete virtuale specifica come più intervalli come illustrato di seguito:

![Spazio di indirizzi della rete virtuale di Azure con due spazi](./media/hana-overview-connectivity/image3-azure-vnet-address-space_alternate.png)

In questo caso, hello **spazio degli indirizzi di rete virtuale** è due spazi definito. Questi due spazi, vengono definiti gli intervalli di indirizzi IP identici toohello per **intervallo di indirizzi IP di subnet VM di Azure** e hello **intervallo di indirizzi IP di Subnet Gateway di rete virtuale.**

È possibile usare qualsiasi standard di denominazione per le subnet del tenant, vale a dire le subnet VM. Tuttavia, **deve essere sempre presente una sola, subnet del gateway per ogni rete virtuale** che si connette toohello SAP HANA nel circuito ExpressRoute di Azure (istanze di grandi dimensioni). E **la subnet del gateway deve sempre essere denominata "GatewaySubnet"** tooensure posizionamento corretto di gateway ExpressRoute hello.

> [!WARNING] 
> È essenziale che la subnet gateway hello è sempre denominata "GatewaySubnet".

È possibile usare più subnet VM, anche con intervalli di indirizzi non contigui. Ma come indicato in precedenza, questi intervalli di indirizzi devono essere compreso hello **spazio degli indirizzi di rete virtuale** di hello rete virtuale in formato aggregato o in un elenco di hello esatte di intervalli di subnet VM hello e hello subnet del gateway.

Riepilogo delle tabelle dei fatti importante hello su una rete virtuale di Azure che si connette tooHANA istanze di grandi dimensioni:

- È necessario hello tooMicrosoft toosubmit **spazio degli indirizzi di rete virtuale** durante l'esecuzione di una distribuzione iniziale di istanze di grandi dimensioni HANA. 
- Hello **spazio degli indirizzi di rete virtuale** può essere un intervallo più ampio che copre l'intervallo di hello per intervalli di indirizzi IP di subnet VM di Azure e l'intervallo di indirizzi IP di Subnet Gateway di rete virtuale hello.
- Oppure è possibile inviare come **spazio degli indirizzi di rete virtuale** gli intervalli di intervalli di indirizzi IP di subnet VM e intervallo di indirizzi IP di Subnet Gateway di rete virtuale hello di indirizzi più intervalli che coprono l'indirizzo IP diverso hello.
- Hello definito **spazio degli indirizzi di rete virtuale** viene utilizzata la propagazione di routing BGP.
- deve essere il nome di Hello della subnet del Gateway hello: **"GatewaySubnet".**
- Hello **spazio degli indirizzi di rete virtuale** viene utilizzato come un filtro su hello istanza grande HANA lato tooallow o impedire l'unità di istanza di grandi dimensioni HANA toohello traffico da Azure. Se le informazioni di routing BGP di rete virtuale di Azure hello hello e hello indirizzi IP configurati per il filtro sul lato di istanza di grandi dimensioni HANA hello non corrispondono, possono verificarsi problemi di connettività.
- Esistono alcuni dettagli sulle subnet del Gateway hello che sono descritte più avanti nella sezione 'Connessione tooHANA una rete virtuale grande istanza ExpressRoute'



### <a name="different-ip-address-ranges-toobe-defined"></a>Indirizzo IP diverso intervalli toobe definito 

È già stata introdotta alcune hello IP indirizzo intervalli necessarie toodeploy HANA istanze di grandi dimensioni nelle sezioni precedenti. Esistono tuttavia altri intervalli di indirizzi IP, ancora più importanti. Più in dettaglio, Hello seguenti indirizzi IP che non tutti necessario toobe inviata tooMicrosoft necessario toobe definito, prima di inviare una richiesta per la distribuzione iniziale:

- **Spazio degli indirizzi di rete virtuale:** come già introdotta in precedenza, o indirizzo IP di hello o gli intervalli è stato assegnato (o si prevede di tooassign) tooyour spazio parametro indirizzo in reti virtuali di Azure (VNet) hello connessione toohello istanze di SAP HANA grandi ambiente. È consigliabile che questo parametro di spazio degli indirizzi è valore multiriga comprende hello intervalli di Subnet VM di Azure e l'intervallo di subnet di Azure Gateway come illustrato in precedenza nella grafica hello hello. Questo intervallo NON deve sovrapporsi con gli intervalli di indirizzi ER-P2P o del pool di indirizzi IP del server. Come tooget questo o questi intervalli di indirizzi IP? il team o il provider del servizio di rete aziendale deve fornire uno o più intervalli di indirizzi IP che non siano già usati all'interno della rete. Esempio: Se la Subnet VM di Azure (vedere in precedenza) è 10.0.1.0/24 e la Subnet del Gateway di Azure (vedere di seguito) è 10.0.2.0/28, quindi lo spazio degli indirizzi di rete virtuale di Azure è consigliabile toobe due righe. 10.0.1.0/24 e 10.0.2.0/28. Anche se i valori di spazio degli indirizzi hello possono essere aggregati, si consiglia di corrispondenza degli intervalli di subnet toohello tooavoid riutilizzo accidentale dell'IP inutilizzato gli intervalli di indirizzi all'interno di spazi di indirizzi più grandi in futuro hello in un' posizione nella rete. **Hello spazio degli indirizzi di rete virtuale è un intervallo di indirizzi IP, quali toobe esigenze inviato tooMicrosoft quando richiede per una distribuzione iniziale**

- **Azure intervallo di indirizzi IP di subnet VM:** questo indirizzo IP, come descritto in precedenza già, è hello uno è stato assegnato (o si prevede di tooassign) parametro subnet di rete virtuale di Azure toohello in ambienti dell'istanza di grandi dimensioni di SAP HANA toohello connessione rete virtuale di Azure . Intervallo di indirizzi IP è tooyour di indirizzi IP utilizzati tooassign macchine virtuali di Azure. gli indirizzi IP Hello fuori intervallo consentiti tooconnect tooyour SAP HANA grandi istanza server. Se necessario, è possibile usare più subnet VM di Azure. È consigliabile usare un blocco CIDR da /24 di Microsoft per ogni subnet VM di Azure. Intervallo di indirizzi deve essere una parte di valori hello utilizzati in hello spazio degli indirizzi di rete virtuale di Azure. Come tooget questo intervallo di indirizzi IP? il team o il provider del servizio di rete aziendale deve fornire un intervallo di indirizzi IP che non sia già in uso all'interno della rete.

- **Intervallo di indirizzi IP di Subnet Gateway di rete virtuale:** a seconda di hello funzionalità che si prevede toouse, hello consigliato dimensione sarebbe:
   - Gateway ExpressRoute con prestazioni extra: blocco indirizzi da /26, necessari per gli SKU di "Classe di tipo II"
   - Coesistenza con VPN ed ExpressRoute tramite un gateway ExpressRoute ad alte prestazioni o più piccolo: blocco indirizzi da /27.
   - Tutti gli altri casi: blocco indirizzi da /28. Intervallo di indirizzi deve essere una parte dei valori hello usato nei valori di "Spazio degli indirizzi di rete virtuale" hello. Intervallo di indirizzi deve essere una parte dei valori hello usato nei valori di spazio degli indirizzi di rete virtuale di Azure hello che è necessario toosubmit tooMicrosoft. Come tooget questo intervallo di indirizzi IP? il team o il provider del servizio di rete aziendale deve fornire un intervallo di indirizzi IP che non sia già in uso all'interno della rete. 

- **Intervallo per la connettività ER P2P di indirizzi:** questo intervallo rappresenta l'intervallo IP hello per la connessione a SAP HANA grandi istanza ExpressRoute (ER) P2P. Deve essere un intervallo di indirizzi IP CIDR da /29. Questo intervallo NON deve sovrapporsi con l'intervallo di indirizzi IP locale o altri intervalli di indirizzi IP di Azure. Intervallo di indirizzi IP viene utilizzato tooset della connettività hello ER dai server dell'istanza di grandi dimensioni di SAP HANA toohello ExpressRoute Gateway tra reti virtuali di Azure. Come tooget questo intervallo di indirizzi IP? il team o il provider del servizio di rete aziendale deve fornire un intervallo di indirizzi IP che non sia già in uso all'interno della rete. **Questo intervallo è un intervallo di indirizzi IP, quali toobe esigenze inviato tooMicrosoft quando richiede per una distribuzione iniziale**
  
- **Intervallo di indirizzi del Pool IP server:** questo intervallo di indirizzi IP è tooassign utilizzati hello singoli IP indirizzo tooHANA grandi istanza server di. Hello consigliata la dimensione della subnet è un /24 CIDR block - ma se necessario può essere più piccoli tooa minimo della specifica di 64 indirizzi IP. Da questo intervallo, hello primi 30 indirizzi IP sono riservati per l'utilizzo da Microsoft. Verificare che il fatto è presi in considerazione quando si sceglie di dimensione hello dell'intervallo di hello. Questo intervallo NON deve sovrapporsi con l'indirizzo IP locale o altri indirizzi IP di Azure. Come tooget questo intervallo di indirizzi IP? il team o il provider del servizio di rete aziendale deve fornire un intervallo di indirizzi IP che non siano attualmente usati all'interno della rete. Un /24 (scelta consigliata) univoco CIDR bloccare toobe utilizzato per l'assegnazione di indirizzi IP specifici hello necessari per SAP HANA in Azure (istanze di grandi dimensioni). **Questo intervallo è un intervallo di indirizzi IP, quali toobe esigenze inviato tooMicrosoft quando richiede per una distribuzione iniziale**
 
Anche se è necessario toodefine e prevede intervalli di indirizzi IP hello precedenti, non tutti i loro necessario tooMicrosoft toobe trasmesso. hello toosummarize precedente, gli intervalli di indirizzi IP hello sono necessari tooname tooMicrosoft sono:

- Spazi di indirizzi della rete virtuale di Azure
- Intervallo di indirizzi per la connettività ER-P2P
- Intervallo di indirizzi del pool di indirizzi IP del server

Aggiungere altre reti virtuali che devono tooconnect tooHANA istanze di grandi dimensioni, è necessario toosubmit hello nuovo spazio di indirizzi VNet Azure si stanno aggiungendo tooMicrosoft. 

Ecco un esempio di diversi intervalli di hello e alcuni intervalli di esempio desiderate tooconfigure e infine specificare tooMicrosoft. Come si può notare, il valore di hello per hello spazio degli indirizzi di rete virtuale di Azure non viene aggregato nel primo esempio hello, ma non è definito da intervalli di hello di hello prima macchina virtuale di Azure subnet intervallo di indirizzi IP e l'intervallo di indirizzi IP di Subnet Gateway di rete virtuale hello. Utilizzando più subnet VM all'interno di rete virtuale di Azure hello sarebbe lavoro conseguenza mediante la configurazione e l'invio di hello IP ulteriori intervalli di indirizzi hello subnet VM aggiuntive come parte di hello spazio degli indirizzi di rete virtuale di Azure.

![Intervalli di indirizzi IP necessari nella distribuzione minima di SAP HANA in Azure (istanze Large)](./media/hana-overview-connectivity/image4b-ip-addres-ranges-necessary.png)

È anche il possibilità hello di aggregazione dei dati di hello è inviare tooMicrosoft. In tal caso, hello spazio di indirizzi della rete virtuale di Azure hello solo include uno spazio. Utilizzo di intervalli di indirizzi IP hello utilizzati nell'esempio hello in precedenza. lo spazio di indirizzi IP aggregato della rete virtuale risulterebbe come illustrato di seguito:

![Seconda possibilità di intervalli di indirizzi IP necessari nella distribuzione minima di SAP HANA in Azure (istanze Large)](./media/hana-overview-connectivity/image5b-ip-addres-ranges-necessary-one-value.png)

Come si può notare, invece di due intervalli di più piccoli che definita spazio degli indirizzi hello di hello rete virtuale di Azure, è necessario un intervallo più ampio che copre 4096 gli indirizzi IP. Questo tipo una definizione di grandi dimensioni di hello lo spazio degli indirizzi lascia alcuni intervalli di dimensioni abbastanza elevate inutilizzati. Poiché i valori di spazio degli indirizzi di rete virtuale hello vengono utilizzati per la propagazione delle route BGP, utilizzo di hello intervalli inutilizzati locale o in un' posizione nella rete causare problemi di routing. Pertanto, è consigliato tookeep hello che lo spazio degli indirizzi è maggiormente allineato con spazio degli indirizzi di subnet effettivo hello utilizzato. Se necessario, senza incorrere in tempi di inattività hello rete virtuale, è sempre possibile aggiungere nuovi valori di spazio di indirizzi in un secondo momento.
 
> [!IMPORTANT] 
> Spazio degli indirizzi di rete virtuale Azure di intervallo di ER-P2P, Pool di IP di Server, di ogni indirizzo IP deve **non** si sovrappongono reciprocamente o qualsiasi altro intervallo utilizzato altrove nella rete; ogni deve essere discreta e come grafico hello due Mostra precedenti, potrebbe non essere un subnet di qualsiasi altro intervallo. Se si verificano sovrapposizioni tra gli intervalli, hello rete virtuale di Azure non può connettersi circuito ExpressRoute toohello.

### <a name="next-steps-after-address-ranges-have-been-defined"></a>Passaggi successivi dopo la definizione degli intervalli di indirizzi
Dopo aver definiti gli intervalli di indirizzi IP hello, hello le attività seguenti necessario toohappen:

1. Inviare gli intervalli di indirizzi IP hello per spazio degli indirizzi di rete virtuale di Azure, la connettività ER P2P hello e intervallo di indirizzi del Pool IP Server, insieme ad altri dati elencati all'inizio di hello del documento hello. In questo momento, è anche possibile avviare toocreate hello rete virtuale e le subnet VM hello. 
2. Un circuito Express Route viene creato da Microsoft, tra la sottoscrizione di Azure e un indicatore dell'istanza di grandi dimensioni HANA hello.
3. Creare una rete tenant in indicatore dell'istanza di grandi dimensioni hello da Microsoft.
4. Microsoft consente di configurare funzionalità di rete in hello SAP HANA in tooaccept dell'infrastruttura di Azure (istanze di grandi dimensioni) da Azure tra reti virtuali uno spazio degli indirizzi che comunica con istanze di grandi dimensioni HANA indirizzi IP.
5. A seconda di hello acquistato specifico SAP HANA in SKU di Azure (istanze di grandi dimensioni), Microsoft assegna un'unità di calcolo in una rete tenant, allocare e montare l'archiviazione e installare il sistema operativo hello (SUSE o Red Hat Linux). Gli indirizzi IP per tali unità vengono estratti dalla hello indirizzo Pool IP Server intervallo tooMicrosoft è stato inviato.

Alla fine di hello hello processo di distribuzione, Microsoft offre hello tooyou dati seguenti:
- Informazioni necessarie tooconnect del circuito ExpressRoute di toohello VNet(s) di Azure che si connette a istanze di grandi dimensioni tooHANA reti virtuali di Azure:
     - Chiave/i di autorizzazione
     - PeerID ExpressRoute
- Dati tooaccess istanze di grandi dimensioni HANA dopo aver stabilito il circuito ExpressRoute e rete virtuale di Azure.

È anche possibile trovare la sequenza hello di connettersi a istanze di grandi dimensioni HANA in documento hello [terminare il programma di installazione per le istanze di grandi dimensioni di SAP HANA tooEnd](https://azure.microsoft.com/resources/sap-hana-on-azure-large-instances-setup/). Molte delle hello alla procedura seguente vengono visualizzati in una distribuzione di esempio in tale documento. 


## <a name="connecting-a-vnet-toohana-large-instance-expressroute"></a>Connessione tooHANA una rete virtuale grande istanza ExpressRoute

Quando si definiti tutti gli intervalli di indirizzi IP hello e ora tornato dati hello da Microsoft, è possibile avviare la connessione di rete virtuale è stato creato prima di istanze di grandi dimensioni tooHANA hello. Una volta hello che rete virtuale di Azure viene creato, un gateway ExpressRoute deve essere creato in hello rete virtuale toolink hello rete virtuale toohello circuito ExpressRoute che si connette toohello tenant del cliente in indicatore dell'istanza di grandi dimensioni hello.

> [!NOTE] 
> Questo passaggio può richiedere too30 minuti toocomplete, come nuovo gateway hello viene creato in hello designato sottoscrizione di Azure e quindi toohello connesso specificato rete virtuale di Azure.

Se esiste già un gateway, controllare se sia o meno un gateway ExpressRoute. In caso contrario, gateway hello deve essere eliminato e ricreato come gateway ExpressRoute. Se un gateway ExpressRoute è già stato stabilito, poiché hello che rete virtuale di Azure è già connessi toohello il circuito ExpressRoute per la connettività locale, procedere toohello collegamento reti virtuali sezione riportata di seguito.

- Utilizzare entrambi hello (nuovo) [portale di Azure](https://portal.azure.com/), o PowerShell toocreate un gateway VPN di ExpressRoute connesso tooyour rete virtuale.
  - Se si utilizza hello portale di Azure, aggiungere un nuovo **Virtual Network Gateway** e quindi selezionare **ExpressRoute** come tipo di gateway hello.
  - Se si sceglie invece PowerShell, scaricare e utilizzare più recente hello [Azure PowerShell SDK](https://azure.microsoft.com/downloads/) tooensure un'esperienza ottimale. Hello seguenti comandi di crea un gateway ExpressRoute. testo Hello preceduto da un  _$_  sono variabili definite dall'utente che toobe necessario aggiornata le informazioni specifiche.

```PowerShell
# These Values should already exist, update toomatch your environment
$myAzureRegion = "eastus"
$myGroupName = "SAP-East-Coast"
$myVNetName = "VNet01"

# These values are used toocreate hello gateway, update for how you wish hello GW components toobe named
$myGWName = "VNet01GW"
$myGWConfig = "VNet01GWConfig"
$myGWPIPName = "VNet01GWPIP"
$myGWSku = "HighPerformance" # Supported values for HANA Large Instances are: HighPerformance or UltraPerformance

# These Commands create hello Public IP and ExpressRoute Gateway
$vnet = Get-AzureRmVirtualNetwork -Name $myVNetName -ResourceGroupName $myGroupName
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
New-AzureRmPublicIpAddress -Name $myGWPIPName -ResourceGroupName $myGroupName `
-Location $myAzureRegion -AllocationMethod Dynamic
$gwpip = Get-AzureRmPublicIpAddress -Name $myGWPIPName -ResourceGroupName $myGroupName
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $myGWConfig -SubnetId $subnet.Id `
-PublicIpAddressId $gwpip.Id

New-AzureRmVirtualNetworkGateway -Name $myGWName -ResourceGroupName $myGroupName -Location $myAzureRegion `
-IpConfigurations $gwipconfig -GatewayType ExpressRoute `
-GatewaySku $myGWSku -VpnType PolicyBased -EnableBgp $true
```

In questo esempio è stato usato hello lo SKU del gateway ad alte prestazioni. Le opzioni disponibili sono ad alte prestazioni o UltraPerformance come hello solo gli SKU di gateway che sono supportati per SAP HANA in Azure (istanze di grandi dimensioni).

> [!IMPORTANT]
> Per le istanze di grandi dimensioni HANA di hello SKU tipi S384, S384m, S384xm, S576, S768 e S960 (tipo di classe II SKU), hello utilizzo hello SKU di Gateway UltraPerformance è obbligatorio.

### <a name="linking-vnets"></a>Collegamento delle reti virtuali

Ora che hello rete virtuale di Azure è un gateway ExpressRoute, utilizzare informazioni di autorizzazione hello fornite da Microsoft tooconnect hello ExpressRoute gateway toohello SAP HANA nel circuito ExpressRoute di Azure (istanze di grandi dimensioni) creato per questo tipo di connettività. Questo passaggio può essere eseguito mediante hello portale di Azure o PowerShell. portale Hello è consigliabile, tuttavia le istruzioni di PowerShell sono i seguenti. 

- Per eseguire hello seguenti comandi per ogni gateway di rete virtuale con un AuthGUID diverso per ogni connessione. prime due voci Hello illustrate nell'esempio di script hello provengono dalle informazioni hello fornite da Microsoft. Inoltre, hello AuthGUID è specifico per ogni rete virtuale e il relativo gateway. Pertanto, se si desidera tooadd un'altra rete virtuale di Azure, è necessario tooget AuthID un'altra per il circuito ExpressRoute che si connette HANA istanze di grandi dimensioni in Azure. 

```PowerShell
# Populate with information provided by Microsoft Onboarding team
$PeerID = "/subscriptions/9cb43037-9195-4420-a798-f87681a0e380/resourceGroups/Customer-USE-Circuits/providers/Microsoft.Network/expressRouteCircuits/Customer-USE01"
$AuthGUID = "76d40466-c458-4d14-adcf-3d1b56d1cd61"

# Your ExpressRoute Gateway Information
$myGroupName = "SAP-East-Coast"
$myGWName = "VNet01GW"
$myGWLocation = "East US"

# Define hello name for your connection
$myConnectionName = "VNet01GWConnection"

# Create a new connection between hello ER Circuit and your Gateway using hello Authorization
$gw = Get-AzureRmVirtualNetworkGateway -Name $myGWName -ResourceGroupName $myGroupName
    
New-AzureRmVirtualNetworkGatewayConnection -Name $myConnectionName `
-ResourceGroupName $myGroupName -Location $myGWLocation -VirtualNetworkGateway1 $gw `
-PeerId $PeerID -ConnectionType ExpressRoute -AuthorizationKey $AuthGUID
```

Se si desidera tooconnect hello gateway toomultiple circuiti ExpressRoute associati con la sottoscrizione, si potrebbe essere necessario tooexecute questo passaggio più volte. Ad esempio, che probabilmente saranno tooconnect hello stesso circuito ExpressRoute di toohello dei Gateway di rete virtuale che si connette rete hello tooyour rete virtuale in locale.

## <a name="adding-more-ip-addresses-or-subnets"></a>Aggiunta di più indirizzi IP o subnet

Utilizzare entrambi hello portale di Azure PowerShell o CLI durante l'aggiunta di più indirizzi IP o subnet.

In questo caso, la raccomandazione hello è tooadd hello nuovo indirizzo IP come nuovo intervallo toohello spazio degli indirizzi di rete virtuale anziché generare un nuovo intervallo di valori aggregato. In entrambi i casi, è necessario toosubmit questa modifica tooMicrosoft tooallow le connessioni che nuove IP indirizzo intervallo toohello istanza grande HANA unità nel client. È possibile aprire un supporto di Azure richiesta tooget hello nuovo indirizzo di rete virtuale spazio aggiunto. Dopo aver ricevuto una conferma, eseguire i passaggi successivi hello.

toocreate una subnet aggiuntiva da hello portale di Azure, vedere l'articolo hello [creare una rete virtuale usando il portale di Azure hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), e toocreate da PowerShell, vedere [creare una rete virtuale con PowerShell](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="adding-vnets"></a>Aggiunta di reti virtuali

Dopo aver connesso inizialmente uno o più reti virtuali di Azure, è opportuno tooadd complementari che accedono a SAP HANA in Azure (istanze di grandi dimensioni). In primo luogo, inviare una richiesta di supporto tecnico di Azure, in tale richiesta include hello informazioni specifiche identificazione hello particolare distribuzione di Azure e intervalli spazio di indirizzi IP hello di hello spazio degli indirizzi di rete virtuale di Azure. SAP HANA sulla gestione dei servizi di Azure fornisce quindi le informazioni necessarie hello è necessario tooconnect hello ExpressRoute e reti virtuali aggiuntive. Per ogni rete virtuale, è necessario un univoco chiave di autorizzazione tooconnect toohello, istanze di grandi dimensioni tooHANA circuito ExpressRoute.

Passaggi tooadd una nuova rete virtuale di Azure:

1. Completare hello innanzitutto il processo di caricamento di hello, vedere hello _creazione rete virtuale di Azure_ sezione.
2. Completare hello secondo passaggio per il processo di caricamento di hello, vedere hello _la creazione di subnet del gateway_ sezione.
3. tooconnect il toohello reti virtuali aggiuntiva, il circuito ExpressRoute istanza grande HANA aprire una richiesta di supporto tecnico di Azure con informazioni su hello nuova rete virtuale e richiedere una nuova chiave di autorizzazione.
4. Una volta notificato che l'autorizzazione di hello è completa, utilizzare le informazioni di autorizzazione forniti da Microsoft hello toocomplete hello terzo passaggio nel processo di caricamento hello, vedere hello _collegamento reti virtuali_ sezione.

## <a name="increasing-expressroute-circuit-bandwidth"></a>Aumento della larghezza di banda del circuito ExpressRoute

Consultarsi con il team di gestione dei servizi SAP HANA in Azure. Nel caso di larghezza di banda hello tooincrease consigliato di hello SAP HANA nel circuito ExpressRoute di Azure (istanze di grandi dimensioni), creare una richiesta di supporto tecnico di Azure. (È possibile richiedere un aumento di una larghezza di banda circuito singolo backup tooa massimo di 10 GB/s). Si riceverà la notifica al termine dell'operazione hello; alcuna azione aggiuntiva non necessaria tooenable questa velocità più elevata in Azure.

## <a name="adding-an-additional-expressroute-circuit"></a>Aggiunta di un circuito ExpressRoute aggiuntivo

Consultare SAP HANA sulla gestione dei servizi di Azure, se si consiglia di un circuito ExpressRoute aggiuntivo necessarie, rendere un toocreate di richiesta di supporto tecnico di Azure, un nuovo circuito ExpressRoute (e tooget autorizzazione informazioni tooconnect tooit). spazio di indirizzo Hello che verrà utilizzato su reti virtuali devono essere definite prima di effettuare la richiesta di hello, in ordine per SAP HANA sulle autorizzazioni di gestione del servizio Azure tooprovide hello.

Una volta creato nuovo circuito hello e hello SAP HANA sulla configurazione di gestione del servizio Azure è stata completata, si sta tooreceive notifica informazioni hello necessarie tooproceed. Seguire i passaggi di hello riportati sopra per la creazione e connessione hello nuova rete virtuale toothis aggiuntive il circuito. Non si tooconnect in grado di reti virtuali di Azure toothis aggiuntivo circuito se già connessi tooanother SAP HANA nel circuito ExpressRoute di Azure (istanza di grandi dimensioni) in hello stessa regione di Azure.

## <a name="deleting-a-subnet"></a>Eliminazione di una subnet

tooremove una subnet di rete virtuale, entrambe hello portale di Azure PowerShell o CLI può essere utilizzato. Se l'intervallo di indirizzi IP della rete virtuale di Azure o lo spazio di indirizzi della rete virtuale di Azure è un intervallo aggregato, non è necessario contattare Microsoft. Tranne che hello rete virtuale è ancora propagazione spazio degli indirizzi di route BGP include subnet hello eliminato. Se si intende hello IP di rete virtuale di Azure indirizzo intervallo/Azure spazio degli indirizzi di rete virtuale più intervalli di indirizzi IP di cui uno è stato assegnato tooyour eliminato subnet, eliminare che lo spazio degli indirizzi di rete virtuale e successivamente informare SAP HANA sulla gestione dei servizi di Azure tooremove dalla hello intervalli di SAP HANA in Azure (istanze di grandi dimensioni) è consentito toocommunicate con.

Mentre non è ancora specifico, dedicato Azure.com sulla rimozione di subnet, il processo di hello per la rimozione di subnet è hello inverso del processo di hello per aggiungerli. Vedere l'articolo hello [creare una rete virtuale usando il portale di Azure hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per ulteriori informazioni sulla creazione di subnet.

## <a name="deleting-a-vnet"></a>Eliminazione di una rete virtuale

Quando si elimina una rete virtuale, utilizzare uno hello portale di Azure PowerShell o CLI. SAP HANA sulla gestione dei servizi di Azure consente di rimuovere le autorizzazioni esistenti di hello in hello SAP HANA nel circuito ExpressRoute di Azure (istanze di grandi dimensioni) e rimuovere hello IP di rete virtuale di Azure indirizzo intervallo/Azure spazio degli indirizzi di rete virtuale per la comunicazione hello con istanze di grandi dimensioni HANA.

Una volta hello rete virtuale è stata rimossa, aprire un supporto di Azure richiesta tooprovide hello spazio degli indirizzi IP o gli intervalli toobe rimosso.

Mentre non è ancora specifico, dedicato Azure.com sulla rimozione di reti virtuali, il processo di hello per la rimozione di reti virtuali è hello inverso del processo di hello per l'aggiunta, di cui è descritto in precedenza. Vedere gli articoli di hello [creare una rete virtuale usando il portale di Azure hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) e [creare una rete virtuale con PowerShell](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per ulteriori informazioni sulla creazione di reti virtuali.

tooensure tutto ciò che viene rimosso, eliminare hello seguenti elementi:

- connessione ExpressRoute, Gateway di rete virtuale, Hello IP pubblico di Gateway di rete virtuale e rete virtuale

## <a name="deleting-an-expressroute-circuit"></a>Eliminazione di un circuito ExpressRoute

tooremove un SAP HANA aggiuntive nel circuito ExpressRoute di Azure (istanze di grandi dimensioni), aprire una richiesta di supporto tecnico di Azure con SAP HANA sulla gestione dei servizi di Azure e richiedere che il circuito hello deve essere eliminato. All'interno di hello sottoscrizione di Azure, è possibile eliminare o mantenere hello rete virtuale in base alle esigenze. Tuttavia, è necessario eliminare la connessione hello tra hello circuito ExpressRoute istanze di grandi dimensioni HANA e hello collegato gateway di rete virtuale.

Se si desidera tooremove una rete virtuale, seguire indicazioni di hello sull'eliminazione di una rete virtuale hello in precedenza nella sezione.


