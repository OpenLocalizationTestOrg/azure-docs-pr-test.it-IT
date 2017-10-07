---
title: aaaDesigning l'infrastruttura di rete per il ripristino di emergenza | Documenti Microsoft
description: In questo articolo vengono illustrate alcune considerazioni sulla progettazione di rete per Azure Site Recovery
services: site-recovery
documentationcenter: 
author: prateek9us
manager: jwhit
editor: 
ms.assetid: ce787731-d930-4f00-a309-e2fbc2e1f53b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pratshar
ms.openlocfilehash: 18bafa1b8b334192bfaf2f4aeba9f090011041ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="designing-your-network-for-disaster-recovery"></a>Progettazione della rete per il ripristino di emergenza

Questo articolo è diretto tooIT professionisti IT responsabili della progettazione, implementazione e supporto di continuità aziendale e dell'infrastruttura di ripristino di emergenza e che vogliono tooleverage toosupport di Microsoft Azure Site Recovery (ripristino automatico di sistema) e migliorare i propri servizi BCDR. Questo articolo illustra alcune considerazioni pratiche sulla strutturazione della rete nel sito di ripristino di emergenza, sia esso Azure o un altro sito locale. 

## <a name="overview"></a>Panoramica
[Sito di Azure (ripristino)](https://azure.microsoft.com/services/site-recovery/) è un servizio di Microsoft Azure che Orchestra hello protezione e ripristino delle applicazioni virtualizzate per business continuity ripristino di emergenza. Questo documento è quello previsto tooguide hello lettore processo hello di progettazione delle reti hello, porre l'attenzione sull'architettura di intervalli IP e subnet nel sito di ripristino di emergenza hello, durante la replica delle macchine virtuali (VM) utilizzando il ripristino del sito.

Inoltre, in questo articolo viene illustrato come il ripristino del sito consente l'architettura e implementazione di servizi BCDR toosupport un Data Center virtuale multisito in fase di test o di emergenza.

In un mondo in cui tutti gli utenti prevede connettività 24/7, è più importante tookeep mai l'infrastruttura e l'esecuzione di applicazioni. scopo di Hello di continuità aziendale e ripristino di emergenza (BCDR) è componenti toorestore non riuscito in modo organizzazione hello rapidamente possibile riprendere le normali operazioni. Lo sviluppo toodeal strategie di ripristino di emergenza con eventi improbabile, devastanti è molto impegnativo. A causa delle difficoltà inerenti toohello stima hello futuro, in particolare per quanto riguarda gli eventi tooimprobable e hello elevato costo tooprovide adeguate misure di protezione contro catastrofi di ampia portate.

Nell'ambito di un piano di ripristino di emergenza è necessario definire l'obiettivo del tempo di ripristino (RTO, Recovery Time Objective) e l'obiettivo del punto di ripristino (RPO, Recovery Point Objective), indispensabili per la pianificazione BCDR. Quando un'eventuale emergenza data center del cliente hello, mediante Azure Site Recovery, i clienti possono rapidamente (RTO basso) portare online le macchine virtuali replicate nel hello data center secondario o Microsoft Azure con perdita di dati minimo (RPO ridotto).

Il failover è reso possibile dalla ripristino automatico di sistema che inizialmente copia designate macchine virtuali da hello dati primario center toohello data center secondario o tooAzure (a seconda dello scenario di hello) e quindi aggiorna periodicamente le repliche hello. Durante la pianificazione dell'infrastruttura, la progettazione della rete deve essere considerata un potenziale collo di bottiglia che può impedire di raggiungere gli obiettivi RTO e RPO aziendali.  

Quando gli amministratori prevede toodeploy una soluzione di ripristino di emergenza, una delle domande hello in prestando attenzione ai è come macchina virtuale hello sarà raggiungibile dopo aver completato il failover hello. Ripristino automatico di sistema consente hello amministratore toochoose hello rete toowhich una macchina virtuale sarà connessa tooafter failover. Se il sito primario di hello è Azure o è un sito locale gestito da un server VMM, quindi a questo scopo, tramite il Mapping di rete. Altre informazioni, vedere [Mapping di rete in Azure tooAzure ripristino di emergenza](site-recovery-network-mapping-azure-to-azure.md) e [Mapping di rete da VMM](site-recovery-network-mapping.md)


Durante la progettazione di rete hello per il sito di ripristino di hello, messaggio per l'amministratore ha due alternative:

* Utilizzare un diverso intervallo di indirizzi IP per rete hello nel sito di ripristino. In questo scenario hello di macchina virtuale dopo il failover verrà visualizzato un nuovo indirizzo IP e amministratore hello avrebbe toodo un aggiornamento DNS. 
* Utilizzare stesso intervallo di indirizzi IP per rete hello nel sito di ripristino hello. In determinati scenari amministratori preferiscono gli indirizzi IP di hello tooretain hanno nel sito primario di hello anche dopo il failover hello. Un amministratore ha tooupdate hello route tooindicate hello nuovo percorso di indirizzi IP hello in condizioni normali. Ma in uno scenario di hello in cui una subnet con estensione viene distribuita tra hello primario e siti di ripristino di hello, mantenendo gli indirizzi IP hello per le macchine virtuali hello diventa un'opzione attraente. L'estensione di una subnet da un tooan di rete locale rete di Azure o tra due reti di Azure non è possibile.  

Quando gli amministratori pianifica toodeploy una soluzione di ripristino di emergenza, una delle domande hello in cui i è come applicazioni hello sarà raggiungibile dopo aver completato il failover hello. Applicazioni moderne sono quasi sempre dipendenti da toosome gradi, di rete fisicamente lo spostamento di un servizio da un sito tooanother rappresenta un problema di rete. Nelle soluzioni di ripristino di emergenza questo problema viene gestito principalmente in due modi. Hello primo approccio è toomaintain indirizzi IP fissato. Nonostante i servizi di hello lo spostamento e hello in diverse ubicazioni fisiche di server di hosting, configurazione degli indirizzi IP hello con tali applicazioni richiedere toohello nuova posizione. Hello secondo approccio prevede completamente modifica indirizzo IP hello durante la transizione hello in hello il sito ripristinato. Ogni approccio presenta diverse varianti di implementazione che vengono riepilogate sotto.

Durante la progettazione di rete hello per il sito di ripristino di hello, messaggio per l'amministratore ha due alternative:

## <a name="option-1-retain-ip-addresses"></a>Opzione 1: Mantenere gli indirizzi IP
Utilizzando indirizzi IP fissi da una prospettiva di processo di ripristino di emergenza, verrà visualizzata tooimplement metodo più semplice di toobe hello, ma dispone di un numero di potenziali problemi che, in pratica, renderlo hello approccio meno frequenti. Azure Site Recovery fornisce funzionalità di hello tooretain degli indirizzi IP hello in tutti gli scenari. Prima che si decide di IP tooretain, appropriata attenzione vincoli toohello che impone alle funzionalità di failover hello. Esaminiamo i fattori che consentono un decisione tooretain indirizzi IP di, o non toomake hello. A tale scopo, è possibile usare una subnet estesa o eseguire un failover completo della subnet.

### <a name="stretched-subnet"></a>Subnet estesa
Di seguito subnet hello viene reso disponibile contemporaneamente in primari e i percorsi di ripristino di emergenza. In pratica significa che è possibile spostare un server e il secondo sito toohello configurazione IP (livello 3) e la rete hello indirizzerà nuovo percorso di hello traffico toohello automaticamente. Si tratta di semplici toodeal con da una prospettiva di server, ma dispone di una serie di sfide:

* Considerando il livello 2 (livello di collegamento dati), tale approccio richiederà apparecchiature di rete in grado di gestire una VLAN estesa, ma non dovrebbe essere un problema perché oggi questo tipo di apparecchiature è ampiamente disponibile. problema di secondo e più difficile Hello sono estendendo hello dominio di errore potenziali VLAN hello viene esteso tooboth siti, diventando essenzialmente un singolo punto di errore. Anche se è un'eventualità improbabile, è accaduto che una broadcast storm fosse avviata, ma non potesse essere isolata. Sono state riscontrate opinioni diverse in merito a quest'ultimo problema e se da un lato sono state effettuate con successo molte implementazioni, dall'altro c'è stato anche un netto rifiuto di implementare questa tecnologia.
* Subnet con estensione non è possibile se si usa Microsoft Azure come hello del sito di ripristino di emergenza.

### <a name="subnet-failover"></a>Failover sulla subnet
È possibile tooimplement subnet failover tooobtain hello vantaggi hello estesa subnet soluzioni descritte in precedenza senza l'estensione subnet hello in più siti. Qui qualsiasi subnet specificata sarà presente nel sito 1 o nel sito 2, ma mai in entrambi i siti contemporaneamente. In ordine toomaintain hello spazio degli indirizzi IP nell'evento hello di un failover, è possibile disporre di tooprogrammatically per le subnet hello router infrastruttura toomove hello da un sito tooanother. In un hello scenario di failover subnet sarebbe spostamento con hello associate macchine virtuali protette. Hello svantaggio toothis consiste nell'evento hello di un errore sono toomove hello intera subnet, che potrebbe essere OK ma può influire sulle considerazioni di granularità failover hello.

Esaminiamo come un'organizzazione fittizia denominata Contoso è in grado di tooreplicate relativo percorso di ripristino di macchine virtuali tooa durante l'esecuzione del failover intera subnet hello. Verrà esaminata in modo Contoso è in grado di toomanage le subnet mentre la replica delle macchine virtuali tra due sedi percorsi e quindi si parlerà subnet funzionamento del failover quando [Azure viene utilizzato come sito di ripristino di emergenza hello](#failover-to-azure).

#### <a name="failover-from-on-premises-tooazure"></a>Failover da locale tooAzure 
Sito di Azure (ripristino) consente toobe Azure utilizzato come un sito di ripristino di emergenza per le macchine virtuali.  

Verrà ora esaminato uno scenario in cui una società fittizia, denominata Woodgrove Bank, ha un'infrastruttura locale che ospita le applicazioni line-of-business, mentre le applicazioni per dispositivi mobili sono ospitate in Azure. La connettività tra le VM di Woodgrove Bank in Azure e i server locali è fornita da una rete privata virtuale (VPN) da sito a sito (S2S) o da ExpressRoute. Azure toobe considerato come un'estensione di Woodgrove Bank locale rete VPN S2S consente la rete virtuale di Woodgrove Bank. Questa comunicazione è abilitata dalla VPN S2S tra il perimetro di Woodgrove Bank e la rete virtuale di Azure. Ora Woodgrove vuole toouse ASR tooreplicate relativi carichi di lavoro in esecuzione area Azure primaria tooanother area di Azure. Questa opzione di soddisfare esigenze di hello Woodgrove, che richiede un'opzione di ripristino di emergenza conveniente e toostore in grado di dati in ambienti di cloud pubblico. Woodgrove ha toodeal con applicazioni e le configurazioni che dipendono dal livello di codice gli indirizzi IP, pertanto hanno un requisito tooretain indirizzi IP per le applicazioni dopo l'esito negativo su tooanother area di Azure.

Woodgrove ha deciso di indirizzi IP tooassign dall'intervallo (172.16.1.0/24, 172.16.2.0/24) tooits risorse di indirizzo IP in esecuzione in Azure.

Per Woodgrove toobe in grado di tooreplicate tooAzure relative macchine virtuali, mantenendo gli indirizzi IP hello, una rete virtuale di Azure deve toobe creato. Deve essere un'estensione della rete locale hello in modo che le applicazioni possono failover da hello locale del sito tooAzure senza problemi. Azure consente tooadd site-to-site, nonché point-to-site VPN connettività toohello reti virtuali create in Azure. Quando si configura la connessione site-to-site, rete di Azure consente percorso locale toohello traffico tooroute (Azure chiama rete locale) solo se l'intervallo di indirizzi IP hello è diverso dall'intervallo di indirizzi IP locale hello, poiché Azure non supporto per l'estensione di subnet.  Ciò significa che se dispone di un 192.168.1.0/24 subnet locale, non è possibile aggiungere 192.168.1.0/24 una rete locale in hello rete di Azure. È previsto poiché Azure non riconosce che non esistono attivi sono macchine virtuali nella subnet hello e subnet hello viene creato solo per scopi di ripristino di emergenza. toobe toocorrectly in grado di routing del traffico da una subnet hello rete di Azure in rete hello e hello rete locale non deve essere in conflitto.

![Prima del failover sulla subnet](./media/site-recovery-network-design/network-design7.png)

Prima del failover

toohelp Woodgrove soddisfare i requisiti aziendali, è necessario hello tooimplement flussi di lavoro seguente:

* Creare una rete aggiuntiva, chiamare prendano rete di ripristino, in cui le macchine virtuali sottoposte a failover hello verrebbe create.
* tooensure che hello IP per una macchina virtuale vengono mantenuti dopo un failover, vedere toohello Configura scheda proprietà della macchina virtuale, specificare hello stesso indirizzo IP hello VM è locale e quindi fare clic su Salva. Quando hello VM è stato eseguito il failover, Azure Site Recovery assegnerà hello macchina virtuale di toohello IP fornito.

![Proprietà di rete](./media/site-recovery-network-design/network-design8.png)

Dopo il failover hello viene attivato e le macchine virtuali hello vengono create in hello ripristino rete con IP hello desiderato, rete toothis connettività può essere stabilita utilizzando un [tooVnet di rete virtuale connessione](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Se necessario, è possibile creare script per questa azione.  Come descritto nella sezione precedente hello sul failover subnet, anche nel caso di hello di tooAzure di failover, le route potrebbe avere toobe modificate in modo appropriato tooreflect che 192.168.1.0/24 ora è stata spostata tooAzure.

![Dopo il failover sulla subnet](./media/site-recovery-network-design/network-design9.png)

Dopo il failover

Se non è una rete di Azure' ', come mostrato nell'immagine di hello precedente. È possibile creare una connessione vpn toosite di sito tra il 'Sito primario' e 'Ripristino rete' dopo il failover hello.  


#### <a name="failover-tooa-secondary-on-premises-site"></a>Failover tooa secondaria locale del sito
Esaminiamo uno scenario in cui si desidera mantenere IP hello di ognuna delle macchine virtuali hello e failover hello completare subnet insieme. sito primario di Hello dispone di applicazioni in esecuzione in 192.168.1.0/24 subnet. Quando si verifica il failover hello, tutte le macchine virtuali hello che fanno parte di questa subnet verrà eseguite il failover del sito di ripristino toohello e conservare gli indirizzi IP. Le route avrà toobe modificato in modo appropriato i fatti di hello tooreflect che tutte le macchine virtuali hello toosubnet 192.168.1.0/24 appartenenti a questo punto sono stati spostati toohello sito di ripristino.

In hello hello nella figura seguente esegue il routing tra un sito primario e sito di ripristino, terzo sito e del sito primario e sito terzo e il sito di ripristino avrà toobe modificate in modo appropriato.

Hello seguenti immagini Mostra hello subnet prima del failover hello. Subnet 192.168.0.1/24 è attiva su hello sito primario prima del failover hello e diventa attivo di hello sito di ripristino dopo il failover hello

![Prima del failover](./media/site-recovery-network-design/network-design2.png)

Prima del failover

immagine di Hello seguente mostra le reti e le subnet dopo il failover.

![Dopo il failover](./media/site-recovery-network-design/network-design3.png)

Dopo il failover

Nel sito secondario in locale e si utilizza un toomanage server VMM viene quindi quando abilitazione della protezione per una macchina virtuale specifica, ripristino automatico di sistema dovrà allocare le risorse di rete in base toohello del flusso di lavoro seguente:

* Ripristino automatico di sistema alloca un indirizzo IP per ogni interfaccia di rete nella macchina virtuale hello da hello pool indirizzi IP statici definiti nella rete pertinente di hello per ogni istanza di System Center VMM.
* Se l'amministratore di hello definisce hello stesso l'indirizzo IP di pool per rete hello nel sito di ripristino hello come che hello pool di indirizzi IP di hello potrebbe allocare rete nel sito primario di hello, durante l'allocazione hello IP indirizzo toohello replica macchina virtuale ASR hello stesso Indirizzo IP della macchina virtuale primaria hello.  indirizzo IP di Hello è riservato in VMM ma non è impostato come IP di failover nell'host Hyper-v hello. IP di Failover in un host Hyper-v è stata impostata solo prima del failover hello.


Se hello stesso IP non è disponibile, ripristino automatico di sistema potrebbe allocare un altro indirizzo IP disponibile dal pool di indirizzi IP hello definito.

Dopo aver hello che VM è abilitata per la protezione è possibile utilizzare seguente esempio script tooverify hello IP che è stata allocata macchina virtuale toohello. Hello stesso IP potrebbe essere impostato come IP di Failover e assegnato toohello VM al momento di hello di failover:

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

> [!NOTE]
> Nello scenario di hello in macchine virtuali utilizzano DHCP, gestione hello degli indirizzi IP è completamente di fuori controllo hello di ripristino automatico di sistema. Un amministratore ha tooensure che hello DHCP servono hello indirizzi IP del server nel sito di ripristino hello possono essere utilizzato da hello stesso intervallo di quella del sito primario di hello.
>
>



## <a name="option-2-changing-ip-addresses"></a>Opzione 2: Modifica degli indirizzi IP
Questo approccio sembra prevalenti toobe hello in base a ciò che abbiamo visto. Assume il formato di hello della modifica indirizzo IP hello di ogni macchina virtuale che è coinvolto nel failover hello. Uno svantaggio di questo approccio richiede hello in arrivo rete too'learn' applicazione hello al IPx è ora in IPy. Anche se IPx e IPy sono i nomi logici, le voci DNS sono in genere toobe modificato o scaricati in tutta la rete hello e le voci memorizzate nella cache nelle tabelle di rete hanno toobe aggiornato o scaricato, pertanto un tempo di inattività può essere dovuto a seconda di come infrastruttura DNS hello è è stata impostata. Questi problemi possono essere limitati utilizzando i valori bassi di durata (TTL) nel caso di hello di applicazioni intranet e [gestione traffico di Azure con ASR](http://azure.microsoft.com/blog/2015/03/03/reduce-rto-by-using-azure-traffic-manager-with-azure-site-recovery/) per internet applicazioni basate su

### <a name="changing-hello-ip-addresses---illustration"></a>Modifica degli indirizzi IP di hello - figura
Esaminiamo scenario hello in cui si intende toouse diversi indirizzi IP in siti di ripristino di hello e hello primario. Nel seguente esempio hello è necessario anche un terzo sito da dove è possono accedere applicazioni hello ospitate nel sito primario o di ripristino.

![Indirizzo IP diverso - Prima del failover](./media/site-recovery-network-design/network-design10.png)


Nella figura hello precedente sono presenti alcune applicazioni ospitate in subnet 192.168.1.0/24 subnet nel sito primario di hello e sono stati configurati toocome backup nel sito di ripristino hello in subnet 172.16.1.0/24 dopo un failover. La configurazione dei percorsi di rete o delle connessioni VPN è avvenuta in modo corretto, pertanto tutti e tre i siti dispongono dell'accesso reciproco.

Come immagine di hello riportata di seguito, dopo il failover di una o più applicazioni, essi verranno ripristinati nella subnet ripristino hello. In questo caso non vincolata toofailover hello intera subnet in hello contemporaneamente. Modifiche non sono necessari tooreconfigure VPN o rete route. Un failover e alcuni aggiornamenti DNS verificheranno che le applicazioni rimangano accessibili. Se gli aggiornamenti dinamici tooallow configurato hello DNS hello le macchine virtuali potrebbe registrare personalmente hello nuovo indirizzo IP quando vengono avviati dopo un failover.

![Indirizzo IP diverso - Dopo il failover](./media/site-recovery-network-design/network-design11.png)


Dopo la macchina virtuale di replica hello di eseguire il failover potrebbe essere un indirizzo IP che non è uguali hello come indirizzo IP hello della macchina virtuale primaria hello. Macchine virtuali verranno aggiornati i server DNS hello che utilizzano dopo l'avvio. Le voci DNS in genere toobe modificato o scaricati in tutta la rete hello e le voci memorizzate nella cache nelle tabelle di rete hanno toobe aggiornato o cancellata, pertanto non è insolito toobe affrontare tempi di inattività durante l'inserimento di tali modifiche di stato sul posto. È possibile ridurre tale problema nei modi seguenti:

* Utilizzando valori TTL bassi per le applicazioni Intranet.
* Usando Gestione traffico di Azure con ASR per le applicazioni basate su Internet.
* Con hello seguenti script all'interno di ripristino prevede tooupdate hello Server DNS tooensure un aggiornamento tempestivo (hello script non è obbligatorio se è configurata la registrazione dinamica DNS hello)

        param(
        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord

### <a name="changing-hello-ip-addresses--dr-tooazure"></a>Indirizzi IP hello modifica: tooAzure di ripristino di emergenza
Hello [installazione dell'infrastruttura di rete per Microsoft Azure come un sito di ripristino di emergenza](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) post di blog spiega come hello toosetup richiesto Azure infrastruttura di rete durante il mantenimento di indirizzi IP non è un requisito. Inizia con la descrizione di un'applicazione hello e quindi controllare la modalità toosetup rete locale e in Azure e quindi concludere come toodo un failover di test e un failover pianificato.

## <a name="next-steps"></a>Passaggi successivi
[Informazioni su](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) come il ripristino del sito esegue il mapping di reti di origine e destinazione quando un server VMM viene utilizzato toomanage hello primario di sito.
