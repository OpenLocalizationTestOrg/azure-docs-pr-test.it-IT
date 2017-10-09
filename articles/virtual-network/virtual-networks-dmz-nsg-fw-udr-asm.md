---
title: 'Esempio: aaaDMZ compilare tooProtect una rete Perimetrale reti con un Firewall, UDR e NSG | Documenti Microsoft'
description: Creare una rete perimetrale con un firewall, routing definito dall'utente e un gruppo di sicurezza di rete
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: dc01ccfb-27b0-4887-8f0b-2792f770ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc121f9cd5fe3c3e9ac2c70fbb7d982a80bb345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="example-3--build-a-dmz-tooprotect-networks-with-a-firewall-udr-and-nsg"></a>Esempio 3: compilazione tooProtect una rete Perimetrale reti con un Firewall, UDR e NSG
[Restituire la pagina sicurezza limite Best Practices toohello][HOME]

Questo esempio illustra come creare una rete perimetrale con un firewall, quattro server Windows, routing definito dall'utente, inoltro IP e gruppi di sicurezza di rete. Ogni tooprovide comandi rilevanti hello in modo dettagliato anche una comprensione più approfondita di ogni passaggio. È inoltre disponibile un Scenario di traffico sezione tooprovide un'analisi approfondita dettagliate come traffico procede attraverso i livelli di difesa hello hello rete Perimetrale. Infine, nella sezione dei riferimenti hello è codice completo hello e istruzione toobuild questo ambiente tootest e sperimentare vari scenari. 

![Rete perimetrale bidirezionale con appliance virtuale di rete, gruppo di sicurezza di rete e routing definito dall'utente][1]

## <a name="environment-setup"></a>Configurazione dell'ambiente
In questo esempio è associata una sottoscrizione che contiene la seguente sintassi hello:

* Tre servizi cloud, "SecSvc001", "FrontEnd001" e "BackEnd001".
* Una rete virtuale, "CorpNetwork", con tre subnet: "SecNet", "FrontEnd" e "BackEnd"
* Un accessorio virtuale di rete, in questo esempio un firewall, connesso toohello SecNet subnet
* Un server Windows che rappresenta un server Web applicazioni ("IIS01").
* Due server Windows che rappresentano server back-end applicazioni ("AppVM01", "AppVM02")
* Un server Windows che rappresenta un server DNS ("DNS01")

Nella sezione dei riferimenti hello sotto è uno script di PowerShell che compilerà la maggior parte dell'ambiente hello descritto in precedenza. Macchine virtuali hello di compilazione e le reti virtuali, anche se vengono eseguite dallo script di esempio hello, non sono descritti in dettaglio in questo documento.

ambiente di hello toobuild:

1. Salvare file xml configurazione rete hello inclusi nella sezione dei riferimenti hello (aggiornata con i nomi, la posizione e scenario hello dato toomatch di indirizzi IP)
2. Le variabili utente di aggiornamento hello nello script di hello script toomatch hello ambiente hello è toobe eseguite (sottoscrizioni, nomi di servizio e così via)
3. Eseguire script hello in PowerShell

**Nota**: area hello indicato nell'hello script di PowerShell deve corrispondere area hello indicato nel file xml di configurazione rete hello.

Una volta hello script viene eseguito correttamente può essere prelevato hello post-script come segue:

1. Impostare le regole firewall hello, questa attività viene descritta in hello sezione seguente: descrizione della regola Firewall.
2. Facoltativamente, nella sezione dei riferimenti hello sono due script tooset hello web server e il server di app con un tooallow di applicazione web semplice test con questa configurazione di rete Perimetrale.

Una volta hello script viene eseguito correttamente le regole del firewall hello saranno necessario toobe completato, questo aspetto è illustrato nella sezione hello: regole del Firewall.

## <a name="user-defined-routing-udr"></a>Routing definito dall'utente
Per impostazione predefinita, hello seguendo le route di sistema è definito come:

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

Hello VNETLocal è sempre prefissi di indirizzo hello definito di hello rete virtuale per tale rete specifico (ad esempio passerà da ' tooVNet di rete virtuale a seconda della modalità di definizione di ogni rete virtuale di specifiche). route sistema rimanenti Hello sono statiche e predefiniti come illustrato in precedenza.

Per priorità, le route vengono elaborate tramite il metodo di corrispondenza di prefisso più lunga (LPM) hello, pertanto hello più specifico route nella tabella di hello sarebbe applicare tooa indirizzo di destinazione specificato.

Pertanto, verrà indirizzato attraverso destinazione tooits di rete virtuale hello a causa di route 10.0.0.0/16 toohello traffico (ad esempio toohello DNS01 server 10.0.2.4) per la rete locale hello (10.0.0.0/16). In altre parole, per 10.0.2.4, hello 10.0.0.0/16 route è una route più specifico hello, anche se 0.0.0.0/0 e hello 10.0.0.0/8 inoltre possibile applicare, ma poiché sono meno specifici non influiscono sul traffico. Pertanto hello traffico too10.0.2.4 avrebbe un hop successivo della rete locale virtuale hello e indirizzare semplicemente toohello destinazione.

Se il traffico è stato creato, ad esempio 10.1.1.1, non applica route 10.0.0.0/16 hello, ma 10.0.0.0/8 hello sarebbe hello più specifico e il traffico hello sarebbe eliminato ("black holed") poiché l'hop successivo hello è Null. 

Se destinazione hello non è stato applicato tooany di prefissi Null hello o prefissi VNETLocal hello, quindi è necessario seguire hello meno specifico routing, 0.0.0.0/0 e indirizzato toohello Internet come hop successivo hello e pertanto il bordo di internet di Azure.

Se sono presenti due prefissi identici nella tabella di route hello, hello Ecco ordine hello di preferenza in base all'attributo di "origine" hello route:

1. "VirtualAppliance" = una tabella di Route definite dall'utente aggiunti manualmente toohello
2. "VPNGateway" = una Route Dynamic BGP (se usato con le reti ibride), aggiunto da un protocollo di rete dinamiche, queste route potrebbero cambiare nel tempo come protocollo dinamica hello riflette automaticamente le modifiche apportate nella rete il peering
3. "Default" = hello sistema route, hello voci statiche hello e di rete virtuale locale, come illustrato nella tabella di route hello precedente.

> [!NOTE]
> È ora possibile usare l'utente definito Routing (UDR) con ExpressRoute e i gateway VPN tooforce in uscita e appliance virtuale di rete indirizzato tooa toobe (NVA) il traffico in ingresso tra più sedi locali.
> 
> 

#### <a name="creating-hello-local-routes"></a>Creazione di hello route locali
In questo esempio, sono necessarie due tabelle di routing, uno per le subnet front-end e back-end di hello. Ogni tabella viene caricato con routing statico appropriato per hello subnet specificato. A scopo di hello di questo esempio, ogni tabella dispone di tre delle route:

1. Traffico della subnet locale senza Hop successivo definito tooallow subnet locale il traffico toobypass hello firewall
2. Traffico di rete virtuale con un Hop successivo definito come firewall, si esegue l'override regola predefinita hello che consente di direttamente tooroute il traffico di rete virtuale locale
3. Il traffico rimanente tutti (0 o 0) con un Hop successivo è definito come hello firewall

Una volta create le tabelle di routing hello sono subnet tootheir associato. Per la tabella routing subnet front-end hello, dopo aver creato e associato subnet toohello dovrebbe essere simile al seguente:

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


Per questo esempio, comandi vengono utilizzati toobuild tabella di route hello hello seguenti, aggiungere una route definita dall'utente e quindi associare subnet tooa tabella route di hello (nota; tutti gli elementi sotto a partire da un segno di dollaro (ad esempio: $BESubnet) sono variabili definite dall'utente da uno script di hello in Hello sezione di riferimento di questo documento):

1. È necessario creare prima tabella di routing base hello. Questo frammento viene illustrato creare hello hello tabella per la subnet di back-end hello. Nello script hello, per la subnet front-end hello viene creata anche una tabella corrispondente.
   
     New-AzureRouteTable -Name $BERouteTableName `
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. Una volta creata la tabella di route hello, è possibile aggiungere route definite dall'utente specifici. In questo frammento, (0.0.0.0/0) di tutto il traffico verrà instradato tramite dell'appliance virtuale hello (una variabile, $VMIP [0], viene utilizzato toopass in hello l'indirizzo IP assegnato al momento dell'appliance virtuale hello creato in precedenza in script hello). Nello script hello, viene anche creata una regola corrispondente nella tabella di hello front-end.
   
     Get-AzureRouteTable $BERouteTableName | `
   
         Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. Hello sopra la voce di route sostituiranno route di hello predefinita "0.0.0.0/0", ma regola 10.0.0.0/16 predefinita di hello ancora esistente che consente il traffico all'interno di hello rete virtuale tooroute direttamente toohello destinazione e non toohello dispositivo di rete virtuale. toocorrect che questa regola di seguire hello comportamento deve essere aggiunto.
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. A questo punto è un toobe scelta effettuata. Con hello sopra due route tutto il traffico verrà instradato toohello firewall per la valutazione, anche il traffico all'interno di una singola subnet. Questo è preferibile, ma tooallow il traffico all'interno di un tooroute subnet locale senza coinvolgere firewall hello è possibile aggiungere una regola di terza, molto specifica. Questa route stati che qualsiasi indirizzo destine per la subnet locale hello sufficiente route sono direttamente (NextHopType = VNETLocal).
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. Infine, con hello tabella di routing creati e popolati con una route definite dall'utente, hello tabella deve essere in ora subnet tooa associato. Nello script hello, tabella di route hello front-end è anche associato toohello subnet front-end. Ecco uno script di associazione hello per subnet back-end hello.
   
     Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a>Inoltro IP
TooUDR una funzionalità complementare, è l'inoltro IP. Si tratta di un'impostazione in un dispositivo virtuale che consente il traffico tooreceive non specificamente indirizzati toohello dispositivo e quindi inoltrare tale destinazione finale tooits di traffico.

Ad esempio, se il traffico da AppVM01 server DNS01 toohello richiesta, UDR invierebbe questo firewall toohello. Con attivato l'inoltro IP, il traffico di hello per destinazione DNS01 hello (10.0.2.4) verrà accettato dal dispositivo hello (10.0.0.4) e quindi inoltrato da destinazione finale tooits (10.0.2.4). Senza l'inoltro IP attivato hello Firewall, il traffico verrebbe non accettato dal dispositivo hello anche se la tabella di route hello dispone di firewall hello come hop successivo hello. 

> [!IMPORTANT]
> È critico tooremember tooenable l'inoltro IP in combinazione con il Routing definito dall'utente.
> 
> 

La configurazione dell'inoltro IP è costituita da un singolo comando e può essere eseguita al momento della creazione della macchina virtuale. In hello flusso di questo frammento di codice di esempio hello verso la fine hello dello script hello è raggruppato con comandi UDR hello:

1. Chiamare l'istanza di VM hello del dispositivo virtuale, hello in questo caso i firewall e attivare l'inoltro IP (nota; qualsiasi elemento in rosso a partire da un segno di dollaro (ad esempio: $VMName[0]) è una variabile definita dall'utente da uno script di hello nella sezione di riferimento hello di questo documento. Hello zero tra parentesi quadre, [0] rappresenta hello prima VM nella matrice hello di macchine virtuali, per toowork di script di esempio hello senza alcuna modifica, hello prima macchina virtuale (VM 0) deve essere hello firewall):
   
     Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | `
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a>Gruppi di sicurezza di rete (NGS)
In questo esempio viene creato un gruppo di sicurezza di rete, in cui viene poi caricata una singola regola. Questo gruppo viene quindi associato solo toohello front-end e back-end nelle subnet (non hello SecNet). Viene compilato in modo dichiarativo hello seguente regola:

1. Qualsiasi tipo di traffico (tutte le porte) da hello Internet toohello viene negato l'intera rete virtuale (tutte le subnet)

Anche se in questo esempio vengono usati i gruppi di sicurezza di rete, lo scopo principale consiste nel creare un secondo livello di difesa contro errori di configurazione manuale. Vogliamo tooblock traffico tutto in ingresso da hello tooeither tramite internet hello front-end o subnet di back-end, il traffico solo flusso tramite firewall toohello di subnet SecNet hello (e quindi, se appropriata in toohello front-end o back-end subnet). Inoltre, con regole UDR hello sul posto, tutto il traffico che in hello subnet front-end o back-end sarebbe indirizzato out toohello firewall (grazie tooUDR). firewall Hello verrà visualizzato come un flusso asimmetrico e riduzione in caso di traffico in uscita hello. In questo modo sono disponibili tre livelli di hello protezione sicurezza front-end e back-end subnet; 1) senza aprire gli endpoint in hello FrontEnd001 e servizi cloud BackEnd001, 2) NSGs negare il traffico da Internet, firewall hello 3) eliminazione traffico asimmetrico di hello.

Un punto di interesse riguardanti hello il gruppo di sicurezza di rete in questo esempio è che contenga una sola regola, illustrata di seguito, ovvero toodeny internet traffico toohello intera rete virtuale che comprende subnet sicurezza hello. 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet `
        from hello Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

Tuttavia, poiché hello è solo di gruppo associata toohello front-end e back-end subnet, hello regola non è elaborata sul traffico in ingresso toohello subnet di sicurezza. Di conseguenza, anche se regola gruppo hello è indicato alcun indirizzo di tooany il traffico Internet nella rete virtuale, hello perché non è mai stata NSG hello associato subnet sicurezza toohello traffico verrà instradato toohello subnet di sicurezza.

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a>Regole del firewall
Regole di inoltro sul firewall hello, saranno necessario toobe creato. Poiché firewall hello è traffico di blocco o inoltro tutto in ingresso, uscita e all'interno della rete virtuale sono necessarie numerose regole del firewall. Inoltre, tutto il traffico in ingresso verrà raggiunto l'indirizzo IP pubblico del servizio di sicurezza hello (su porte diverse), toobe elaborati dal firewall hello. Consiglia di flussi logici di hello toodiagram prima di configurare le subnet hello e variazioni tooavoid di regole firewall in un secondo momento. Hello nella figura seguente è una vista logica hello regole del firewall per questo esempio:

![Vista logica di hello regole del Firewall][2]

> [!NOTE]
> In base a hello che Appliance virtuale di rete utilizzato, porte di gestione di hello possono variare. In questo esempio si fa riferimento a Barracuda NextGen Firewall, che usa le porte 22, 801 e 807. Consultare hello accessorio fornitore documentazione toofind hello esatta porte utilizzate per la gestione dei dispositivi hello in uso.
> 
> 

### <a name="logical-rule-description"></a>Descrizione della regola logica
Nel diagramma logico hello sopra, subnet sicurezza hello non viene visualizzato perché firewall hello è l'unica risorsa di hello subnet e questo diagramma verrà visualizzati le regole del firewall hello e come essi logicamente consentire o negare i flussi di traffico e non hello indirizzato percorso effettivo. Inoltre, due ottetti dell'indirizzo IP locale hello per facilitarne la lettura dell'ultima porte hello selezionate per il traffico RDP hello sono porte nell'intervallo superiore (8014 – 8026) e sono stati selezionati toosomewhat allinearlo hello (ad esempio indirizzo del server locale 10.0.1.4 è associato porta esterna 8014), tuttavia possibile utilizzare qualsiasi porta superiore non in conflitto.

Per questo esempio sono necessari 7 tipi di regole, ovvero:

* Regole esterne (per il traffico in ingresso):
  1. Regola Del firewall Management: Questa regola di reindirizzamento App consente porte di gestione del traffico toopass toohello dell'appliance virtuale di rete hello.
  2. Le regole di RDP (per ogni server di windows): queste quattro regole (uno per ogni server) consente la gestione di hello singoli server tramite RDP. Questo potrebbe anche essere inserito in una regola a seconda delle funzionalità di hello di hello dispositivo di rete virtuale in uso.
  3. Regole del traffico di applicazione: Esistono due regole del traffico dell'applicazione hello prima per il traffico web front-end di hello e hello secondo per il traffico di back-end hello (ad esempio server toodata livello web). configurazione di Hello di queste regole dipenderà dall'architettura di rete hello (in cui vengono collocati i server) e flussi di traffico (il tipo di traffico hello direzione flussi e le porte utilizzate).
     * prima regola Hello consentirà hello effettivo traffico tooreach hello applicazione server applicazioni. Mentre hello altre regole consentono per la sicurezza, gestione, e così via, le regole di applicazione sono tooaccess utenti o servizi esterni quali consentire applicazioni hello. Per questo esempio, non esiste un singolo server web sulla porta 80, pertanto una singola applicazione regola del firewall reindirizzerà il traffico in entrata toohello IP esterno, indirizzo IP interno di toohello web server. Hello reindirizzato sessione traffico potrebbe essere stato NAT toohello interno del server.
     * seconda regola del traffico di applicazione è Hello hello tootalk toohello AppVM01 server di back-end regola tooallow hello Server Web (ma non AppVM02) tramite qualsiasi porta.
* Regole interne (per il traffico tra reti virtuali)
  1. Regola di tooInternet in uscita: questa regola consentirà il traffico da qualsiasi rete toopass toohello selezionato reti. Questa regola è in genere una regola predefinita già installati nel firewall hello, ma in uno stato disabilitato. È consigliabile abilitarla per questo esempio.
  2. Regola DNS: Questa regola consente solo DNS (porta 53) traffico toopass toohello server DNS. Per questo ambiente che maggior parte del traffico da hello front-end toohello back-end è bloccata, questa regola consente DNS in modo specifico da una qualsiasi subnet locale.
  3. Subnet tooSubnet regola: questa regola è tooallow qualsiasi server in back hello terminare server tooany tooconnect di subnet nella subnet front-end hello (ma non hello inversa).
* Regola alternativo (per il traffico che non soddisfa uno qualsiasi dei hello precedente):
  1. Nega tutte le regole di traffico: Questo deve essere sempre regola finale di hello (in termini di priorità) e di conseguenza un traffico flussi avrà esito negativo toomatch qualsiasi hello precedenti regole che verranno eliminati da questa regola. Questa è una regola predefinita ed è solitamente attivata, quindi non sono in genere necessarie modifiche.

> [!TIP]
> Regola di traffico applicazione secondo hello, qualsiasi porta è consentita per semplice di questo esempio, in un hello uno scenario reale più specifici intervalli di porte e indirizzi devono essere utilizzato tooreduce superficie di attacco hello di questa regola.
> 
> 

<br />

> [!IMPORTANT]
> Una volta tutte hello sopra le regole vengono create, è importante priorità hello tooreview del traffico di tooensure ogni regola verrà consentita o negata in base alle esigenze. Per questo esempio, le regole di hello sono in ordine di priorità. È facile toobe bloccati dal firewall hello a causa di regole ordinate toomis. Come minimo, verificare che Gestione hello per firewall hello stesso sia sempre assoluto regola priorità più alta hello.
> 
> 

### <a name="rule-prerequisites"></a>Prerequisiti delle regole
Uno dei prerequisiti per i firewall di hello hello macchina virtuale in esecuzione sono endpoint pubblici. Per il traffico di hello firewall tooprocess endpoint pubblici appropriato hello deve essere aperto. Esistono tre tipi di traffico in questo esempio; 1) Gestione traffico toocontrol hello firewall e le regole del firewall, server di windows hello toocontrol il traffico RDP 2) e il traffico di 3) dell'applicazione. Questi includono hello tre colonne di tipi di traffico in hello superiore metà della vista logica delle regole del firewall hello sopra.

> [!IMPORTANT]
> Una chiave takeway qui è tooremember che **tutti** proverrà il traffico attraverso il firewall hello. Così tooremote desktop toohello IIS01 server, anche se è in servizio di Cloud Front-End hello e sulla subnet Front-End hello, tooaccess dobbiamo tooRDP toohello firewall sul server porta 8014 e attendere la richiesta RDP hello firewall tooroute hello internamente la porta RDP IIS01 toohello. Hello "Connetti" del portale di Azure pulsante non funzionerà poiché non esiste alcun diretto tooIIS01 percorso RDP (per quanto possibile vedere portale hello). Ciò significa che tutte le connessioni da hello internet sarà toohello servizio di sicurezza e una porta, ad esempio secscv001.cloudapp.net:xxxx (Buongiorno riferimento diagramma per il mapping di porta esterna e indirizzo IP interno e porta hello).
> 
> 

Un endpoint può essere aperto sia in fase di creazione della macchina virtuale di hello o post-compilazione come viene eseguita in uno script di esempio hello e illustrato di seguito in questo frammento di codice (nota; qualsiasi elemento che inizia con un segno di dollaro (ad esempio: $VMName[$i]) è una variabile definita dall'utente da uno script di hello in hello referen sezione di stima di cardinalità di questo documento. Hello "$i" tra parentesi quadre, [$i], rappresenta il numero di matrice hello di una macchina virtuale specifica in una matrice di macchine virtuali):

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

Anche se non è chiaramente indicato qui di scadenza toohello utilizzo di variabili, ma gli endpoint sono **solo** aperto su hello servizio Cloud di protezione. Si tratta di tooensure che tutto il traffico in ingresso viene gestito (indirizzati NAT aveva eliminate) da firewall hello.

Un client di gestione sarà necessario toobe installato su un firewall di hello toomanage PC e creare configurazioni di hello necessarie. Vedere fornitore documentazione fornita dal firewall (o altri NVA) hello in modo toomanage hello dispositivo. resto Hello di questa sezione e la sezione successiva di hello, la creazione delle regole Firewall, descriverà configurazione hello del firewall hello stesso, tramite il client Gestione fornitori hello (ossia, non hello portale di Azure o PowerShell).

Istruzioni per il download di client e connessione toohello Barracuda utilizzato in questo esempio sono disponibili qui: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)

Una volta effettuato l'accesso nel firewall hello ma prima di creare regole del firewall, sono disponibili due classi di oggetti dei prerequisiti che possono semplificare la Creazione regole di hello; Oggetti di rete e del servizio.

Per questo esempio, tre gli oggetti di rete denominata devono essere definito (uno per la subnet front-end hello e subnet di back-end hello, anche un oggetto di rete per l'indirizzo IP di hello del server DNS hello). toocreate rete denominata. a partire dal dashboard di hello Barracuda NG amministratore client, passare scheda Configurazione toohello, nella sezione di configurazione Operational hello fare clic su set di regole, fare clic su "Reti" nel menu di hello oggetti Firewall, quindi fare clic su Nuovo dal menu Modifica reti hello. oggetto di rete Hello è ora possibile creare, mediante l'aggiunta di hello nome e un prefisso di hello:

![Creare un oggetto di rete di front-end][3]

Verrà creata una rete per la subnet front-end hello denominata, deve creare un oggetto simile per la subnet di back-end hello anche. Subnet hello ora possibile fare riferimento più facilmente in base al nome regole di firewall hello.

Per l'oggetto Server DNS hello:

![Creare un oggetto server DNS][4]

Questo riferimento di indirizzo IP singolo verrà utilizzato in una regola DNS in un secondo momento nel documento di hello.

gli oggetti, prerequisiti secondo Hello sono oggetti di servizi. Questi rappresenteranno porte di connessione RDP hello per ogni server. Poiché l'oggetto servizio RDP esistente hello è la porta RDP predefinito toohello associato, 3389, nuovi servizi possono essere creati tooallow traffico da porte esterne hello (8014 8026). le nuove porte di Hello anche possibile aggiungere servizio RDP esistente toohello, ma per la dimostrazione, è possibile creare una singola regola per ogni server. toocreate una nuova regola RDP per un server. a partire dal dashboard di client dispositivo Barracuda NG Admin hello, passare scheda Configurazione toohello, in configurazione operativa hello sezione Ruleset, quindi fare clic su "Servizi" nel menu di oggetti di Firewall, scorrere verso il basso l'elenco di hello servizi hello scegliere hello Servizio "RDP". Ora è disponibile un oggetto servizio RDP-Copy1 che può essere modificato. Fare clic con il pulsante destro del mouse su RDP-Copy1 e scegliere Edit. Fare doppio clic su RDP Copy1 e selezionare Modifica, hello Modifica oggetto servizio si aprirà la finestra come illustrato di seguito:

![Copiare la regola RDP predefinita][5]

i valori Hello possono quindi essere modificato toorepresent hello servizio RDP per un server specifico. Per hello AppVM01 sopra predefinito regola RDP deve essere modificato tooreflect un nuovo nome del servizio, descrizione, e la porta RDP esterno utilizzato in hello diagramma nella figura 8 (Nota: hello porte vengono modificate da hello predefinito RDP è 3389 porta esterna toohello che viene usata per questo server specifico, nel caso di hello di porta esterna di AppVM01 hello è 8025) hello servizio modificato è illustrato di seguito:

![Regola AppVM01][6]

Questo processo deve essere ripetuto toocreate servizi RDP per hello rimanenti server. AppVM02 DNS01 e IIS01. Creazione Hello di questi servizi consentirà la creazione di regole hello più semplice e più ovvio nella sezione successiva hello.

> [!NOTE]
> Un servizio RDP per hello Firewall non è necessaria per due motivi. firewall 1) prima di hello VM è un'immagine di basati su Linux in modo che verrebbe utilizzato SSH sulla porta 22 per la gestione delle macchine Virtuali anziché RDP e 2) la porta 22 e due altre porte di gestione sono consentiti nella regola gestione primo hello descritto di seguito tooallow per la connettività di gestione.
> 
> 

### <a name="firewall-rules-creation"></a>Creazione di regole del firewall
In questo esempio si usano tre tipi di regole del firewall ognuna con icone distinte:

regola di reindirizzare l'applicazione Hello: ![icona di reindirizzamento dell'applicazione][7]

la regola NAT di destinazione di Hello: ![icona NAT di destinazione][8]

regola di Pass Hello: ![passare icona][9]

Ulteriori informazioni su queste regole sono reperibile nel sito web di Barracuda hello.

toocreate hello seguendo regole (o verificare le regole predefinite esistente), a partire dal dashboard di hello Barracuda NG amministratore client, passare scheda Configurazione toohello, hello configurazione operativa sezione selezionare il set di regole. Chiamata di una griglia, "Main regole" mostrerà hello esistente regole attive e disattivate il firewall. In hello angolo superiore destro di questa griglia è una piccola verde "+" fare clic su questo toocreate una nuova regola (Nota: il firewall può essere "bloccato" per le modifiche, se viene visualizzato un pulsante contrassegnato come "Lock" e si toocreate Impossibile o modificare le regole, fare clic su questo pulsante troppo "sbloccare" hello se regola t e consentire la modifica). Se si desidera tooedit una regola esistente, selezionare la regola, fare doppio clic su e scegliere Modifica regola.

Una volta le regole vengono create e/o modificate, devono essere inseriti toohello firewall e quindi attivato, se ciò non avviene regola hello le modifiche apportate verranno rese effettive. il processo di attivazione e push Hello è descritta di seguito le descrizioni delle regole di hello dettagli.

specifiche di Hello del toocomplete ogni regola richiesta in questo esempio sono descritti di seguito:

* **Regola di gestione del firewall**: regole di reindirizzamento di questa App consente il traffico toopass toohello di porte di gestione del dispositivo di rete virtuale hello, in questo esempio un NextGen Firewall Barracuda. porte di gestione di Hello siano 801, 807 e, facoltativamente, 22. le porte interne ed esterne Hello sono hello stesso (ad esempio alcuna conversione porta). Questa regola, SETUP-MGMT-ACCESS, è una regola predefinita e abilitata per impostazione predefinita in Barracuda NextGen Firewall versione 6.1.
  
    ![Regola di gestione del firewall][10]

> [!TIP]
> Hello spazio degli indirizzi di origine nella regola è qualsiasi, se hello intervalli di indirizzi IP di gestione sono note, riducendo l'ambito consentirebbe di ridurre anche porte di gestione toohello superficie di attacco hello.
> 
> 

* **Le regole di RDP**: le regole NAT destinazione questi consente la gestione di hello singoli server tramite RDP.
  Esistono quattro campi critici necessari toocreate questa regola:
  
  1. Origine: tooallow RDP da qualsiasi luogo e riferimento hello "Any" viene utilizzato nel campo di origine hello.
  2. Servizio-utilizzare l'oggetto servizio appropriato creato in precedenza, in questo caso "AppVM01 RDP" hello, porte esterne hello reindirizzare toohello server l'indirizzo IP locale e tooport 3386 (porta RDP hello predefinita). Questa regola specifica è per tooAppVM01 accesso RDP.
  3. Destinazione: deve essere hello *locale porta nel firewall hello*, "DCHP 1 IP locale" o eth0 se utilizza indirizzi IP statici. numero ordinale di Hello (scheda eth1 eth0, e così via) potrebbe essere diverso se il dispositivo di rete dispone di più interfacce locale. Si tratta di hello porta firewall hello vengono inviati da (potrebbero essere hello stesso come porta di ricezione hello), destinazione indirizzato effettiva hello è nel campo destinazione elenco hello.
  4. Reindirizzamento: in questa sezione viene appliance virtuale hello in tooultimately reindirizzare il traffico. reindirizzamento più semplice di Hello è tooplace hello IP e porta (facoltativa) nel campo destinazione elenco hello. Se nessuna porta è la porta di destinazione hello utilizzato nella richiesta in ingresso hello sarà utilizzato (ovvero nessuna conversione), se una porta è definita una porta di hello saranno anche NAT insieme hello IP indirizzo Net. MSMQ.
     
     ![Regola firewall RDP][11]
     
     Un totale di quattro regole RDP necessario toobe creato: 
     
     | Nome regola | Server | Service | Target List |
     | --- | --- | --- | --- |
     | RDP-to-IIS01 |IIS01 |IIS01 RDP |10.0.1.4:3389 |
     | RDP-to-DNS01 |DNS01 |DNS01 RDP |10.0.2.4:3389 |
     | RDP-to-AppVM01 |AppVM01 |AppVM01 RDP |10.0.2.5:3389 |
     | RDP-to-AppVM02 |AppVM02 |AppVm02 RDP |10.0.2.6:3389 |

> [!TIP]
> In quanto l'ambito hello di hello origine e i campi servizio riduce la superficie di attacco hello. ambito più limitato Hello che consentirà la funzionalità deve essere utilizzato.
> 
> 

* **Regole del traffico di applicazione**: sono presenti due regole del traffico di applicazione, hello prima per il traffico web front-end di hello e hello secondo per il traffico di back-end hello (ad esempio server toodata livello web). Queste regole dipenderà dall'architettura di rete hello (in cui vengono collocati i server) e flussi di traffico (il tipo di traffico hello direzione flussi e le porte utilizzate).
  
    Innanzitutto descritto è regola di hello front-end per il traffico web:
  
    ![Regola firewall Web][12]
  
    Questa regola NAT di destinazione consente hello effettivo traffico tooreach hello applicazione server applicazioni. Mentre hello altre regole consentono per la sicurezza, gestione, e così via, le regole di applicazione sono tooaccess utenti o servizi esterni quali consentire applicazioni hello. Per questo esempio, non esiste un singolo server web sulla porta 80, pertanto hello singola applicazione regola del firewall reindirizzerà il traffico in entrata toohello IP esterno, indirizzo IP interno di toohello web server.
  
    **Nota**: che non sono disponibili porte assegnate nel campo destinazione elenco hello, pertanto hello in ingresso porta 80 (o 443 per hello servizio selezionato) da utilizzare nel reindirizzamento hello del server web hello. Se il server web hello è in ascolto su una porta diversa, ad esempio 8080, campo elenco destinazione hello potrebbe essere tooallow too10.0.1.4:8080 aggiornato per il reindirizzamento delle porte hello anche.
  
    Regola del traffico di applicazione successivo è Hello hello tootalk toohello AppVM01 server di back-end regola tooallow hello Server Web (ma non AppVM02) tramite qualsiasi servizio:
  
    ![Regola firewall AppVM01][13]
  
    Questa regola di Pass consente a qualsiasi server IIS su hello tooreach di subnet front-end hello AppVM01 (indirizzo IP 10.0.2.5) su qualsiasi porta, utilizzando i dati di tooaccess protocollo richiesti dall'applicazione web hello.
  
    In questa schermata un "\<esplicita dest\>" viene usato in hello destinazione campo toosignify 10.0.2.5 come destinazione di hello. Può essere denominato esplicita come illustrato o un oggetto di rete (come avveniva in prerequisiti hello per il server DNS hello). Si tratta di amministratore toohello di firewall hello verrà utilizzato il metodo toowhich. tooadd 10.0.2.5 come un Explict Desitnation, fare doppio clic sulla riga vuota prima di hello in \<esplicita dest\> e immettere l'indirizzo hello nella finestra di hello che viene visualizzato.
  
    Con questa regola passare, non è necessario alcun NAT poiché si tratta di traffico interno, pertanto hello metodo di connessione può essere impostata troppo "SNAT n".
  
    **Nota**: rete di origine hello in questa regola è qualsiasi risorsa nella subnet front-end hello, se è solo uno, o noto il numero specifico di server web, un oggetto di rete le risorse potrebbero essere creati toobe più toothose esatti indirizzi IP specifici anziché intera subnet front-end di Hello.

> [!TIP]
> Questa regola utilizza il servizio di hello "Any" toomake hello toosetup più semplice applicazione di esempio e utilizzare, sarà inoltre ICMPv4 (ping) in una singola regola. Questa non è comunque una procedura consigliata. Hello porte e protocolli ("servizi") devono essere minimo possibile toohello ristretto che consente di superficie di attacco hello tooreduce operazione applicazione oltre questo limite.
> 
> 

<br />

> [!TIP]
> Anche se questa regola Mostra un riferimento esplicito dest in uso, un approccio coerente deve essere utilizzato in tutta la configurazione del firewall hello. È consigliabile che hello denominato oggetto di rete utilizzabile in tutto per semplificare la leggibilità e facilità di supporto. Hello esplicita-dest è qui usato da solo tooshow un metodo alternativo di riferimento e non è in genere consigliabile (soprattutto per le configurazioni complesse).
> 
> 

* **In uscita tooInternet regola**: passare a questa regola consentirà il traffico da qualsiasi destinazione reti di origine rete toopass toohello selezionato. Questa regola è una regola predefinita in genere già firewall Barracuda NextGen hello, ma è in uno stato disabilitato. Facendo clic su questa regola può accedere a hello comando di attivare la regola. regola di Hello illustrato di seguito è stato modificato tooadd hello due subnet locali che sono state create come riferimenti nella sezione dei prerequisiti di hello di questo attributo di origine documento toohello di questa regola.
  
    ![Regola firewall in uscita][14]
* **Regola DNS**: passare a questa regola consente solo DNS (porta 53) traffico toopass toohello server DNS. Per questo ambiente che maggior parte del traffico da hello front-end toohello back-end è bloccata, questa regola consente in particolare DNS.
  
    ![Regola firewall DNS][15]
  
    **Nota**: In questa schermata è incluso hello ripresa metodo di connessione. Poiché questa regola per il traffico indirizzo IP toointernal IP interno, non è necessario alcun NATing, questo hello metodo di connessione è troppo "SNAT No" per questa regola di sessione.
* **Subnet tooSubnet regola**: passare a questa regola è una regola predefinita che è stata attivata e tooallow modificato qualsiasi server nel nuovo hello finiscono con server di subnet tooconnect tooany hello subnet front-end. Questa regola è interno tutti traffico pertanto hello metodo di connessione può essere impostata tooNo SNAT.
  
    ![Regola firewall Intra-VNet][16]
  
    **Nota**: hello bidirezionale casella di controllo non è selezionata (non è selezionata nella maggior parte delle regole), questo aspetto è fondamentale per la regola in quanto rende questa regola "unidirezionale", una connessione può essere avviata dalla rete di front-end toohello subnet back-end hello, ma non hello inversa. Se la casella di controllo viene selezionata, la regola consente il traffico bidirezionale, che in base al diagramma logico in questo articolo non è auspicabile.
* **Negare tutte le regole di traffico**: deve sempre essere regola finale di hello (in termini di priorità) e un traffico flussi toomatch ha esito negativo di una delle regole precedenti hello pertanto verranno eliminato da questa regola. Questa è una regola predefinita ed è solitamente attivata, quindi non sono in genere necessarie modifiche. 
  
    ![Regola firewall Deny][17]

> [!IMPORTANT]
> Una volta tutte hello sopra le regole vengono create, è importante priorità hello tooreview del traffico di tooensure ogni regola verrà consentita o negata in base alle esigenze. Per questo esempio, le regole di hello sono in ordine di hello che vengano visualizzati nella griglia principale di regole in hello Barracuda Client di gestione di inoltro hello.
> 
> 

## <a name="rule-activation"></a>Attivazione delle regole
Con hello ruleset modificato toohello specifica del diagramma logica hello, hello ruleset deve essere caricato toohello firewall e quindi attivato.

![Attivazione delle regole firewall][18]

Nell'angolo superiore destra hello del client di gestione di hello sono un cluster di pulsanti. Fare clic su hello "inviare modifiche" pulsante toosend hello modificato regole toohello firewall, quindi fare clic sul pulsante "Attiva" hello.

Con l'attivazione del set di regole firewall hello hello è stata completata la compilazione di ambiente di esempio.

## <a name="traffic-scenarios"></a>Scenari di traffico
> [!IMPORTANT]
> Una chiave takeway è tooremember che **tutti** proverrà il traffico attraverso il firewall hello. Così tooremote desktop toohello IIS01 server, anche se è in servizio di Cloud Front-End hello e sulla subnet Front-End hello, tooaccess dobbiamo tooRDP toohello firewall sul server porta 8014 e attendere la richiesta RDP hello firewall tooroute hello internamente la porta RDP IIS01 toohello. Hello "Connetti" del portale di Azure pulsante non funzionerà poiché non esiste alcun diretto tooIIS01 percorso RDP (per quanto possibile vedere portale hello). Ciò significa che tutte le connessioni da hello internet sarà toohello servizio di sicurezza e una porta, ad esempio secscv001.cloudapp.net:xxxx.
> 
> 

Per questi scenari, hello segue le regole del firewall deve essere disponibili:

1. Firewall Management
2. TooIIS01 RDP
3. TooDNS01 RDP
4. TooAppVM01 RDP
5. TooAppVM02 RDP
6. Toohello traffico App Web
7. Traffico App tooAppVM01
8. In uscita toohello Internet
9. TooDNS01 front-end
10. Traffico tra più Subnet (solo fine toofront back-end)
11. Deny All

set di regole firewall effettivo Hello avrà probabilmente molte altre regole toothese aggiunta, le regole di hello qualsiasi dato firewall disporrà di numeri di priorità diversi rispetto a quelli elencati di seguito hello. Questo elenco e dei numeri sono tooprovide pertinenza solo queste undici regole e la priorità relativa di hello tra loro. In altre parole; firewall effettivo hello, hello "RDP tooIIS01" potrebbe essere regola numero 5, ma come è di sotto di regole "Gestione Firewall" hello e versioni successive regola "RDP tooDNS01" hello che allineamento con l'intenzione di hello dell'elenco. supporta anche l'elenco Hello nell'hello brevità; consentendo scenari seguenti ad esempio "Regole firewall 9 (DNS)". Per ragioni di brevità, hello quattro regole RDP sarà collettivamente chiamati anche "hello regole RDP" quando hello traffico risulta tooRDP non correlati.

Ricordare anche che sono gruppi di sicurezza di rete sul posto per il traffico internet in entrata su hello front-end e back-end subnet.

#### <a name="allowed-internet-tooweb-server"></a>(Consentito) Internet tooWeb Server
1. L'utente Internet richiede una pagina HTTP a SecSvc001.CloudApp.Net (servizio cloud per Internet).
2. Traffico passa del servizio cloud tramite endpoint aperto interfaccia toofirewall porta 80 del 10.0.0.4:80
3. Nessun gruppo assegnato tooSecurity subnet, pertanto le regole di sistema NSG consentono traffico toofirewall
4. Traffico raggiunge l'indirizzo IP interno del firewall hello (10.0.1.4)
5. Il firewall inizia l'elaborazione delle regole:
   1. FW regola 1 (FW Mgmt) non è applicabile, spostare toonext regola
   2. Regole FW 2-5 (regole di RDP) non si applicano, spostare toonext regola
   3. FW regola 6 (App: Web) viene applicato, il traffico è consentito, firewall NAT è too10.0.1.4 (IIS01)
6. subnet front-end Hello inizia l'elaborazione della regola in ingresso:
   1. NSG regola 1 (blocco Internet) non è valida (il traffico è stato NAT usasse firewall hello, indirizzo di origine hello è ora pertanto firewall hello nella subnet sicurezza hello e visibili subnet front-end hello traffico "local" toobe di gruppo ed è pertanto consentita), spostare toonext regola
   2. GRUPPO regole predefinite per consentire il traffico toosubnet subnet, è consentito il traffico, arrestare l'elaborazione della regola NSG
7. Iis01 è in ascolto per il traffico web, riceve la richiesta e avvia l'elaborazione richiesta hello
8. Iis01 tenta tooinitiates un tooAppVM01 sessione FTP nella subnet back-end
9. route UDR Hello nella subnet front-end rende hop successivo di hello firewall hello
10. Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.
11. Il firewall inizia l'elaborazione delle regole:
    1. FW regola 1 (FW Mgmt) non è applicabile, spostare toonext regola
    2. Non applicare FW regola 2-5 (regole di RDP), spostare toonext regola
    3. FW regola 6 (App: Web) non si applicano, spostare toonext regola
    4. Regola FW 7 (App: back-end) viene applicato, è consentito il traffico, firewall inoltra il traffico too10.0.2.5 (AppVM01)
12. subnet di back-end Hello inizia l'elaborazione della regola in ingresso:
    1. Regola di gruppo 1 (blocco Internet) non è applicabile, spostare toonext regola
    2. GRUPPO regole predefinite per consentire il traffico toosubnet subnet, è consentito il traffico, arrestare l'elaborazione della regola NSG
13. AppVM01 riceve la richiesta di hello e avvia la sessione hello e risponde
14. route UDR Hello nella subnet back-end rende hop successivo di hello firewall hello
15. Poiché esistono non è consentita alcuna regola di gruppo in uscita su hello risposta hello subnet di back-end
16. Poiché questo restituisce il traffico su un firewall hello sessione stabilita passa server web di hello risposta toohello indietro (IIS01)
17. La subnet front-end inizia l'elaborazione delle regole in ingresso:
    1. Regola di gruppo 1 (blocco Internet) non è applicabile, spostare toonext regola
    2. GRUPPO regole predefinite per consentire il traffico toosubnet subnet, è consentito il traffico, arrestare l'elaborazione della regola NSG
18. server IIS Hello riceve risposta hello, completa la transazione hello con AppVM01 e quindi completa compilazione hello risposta HTTP, la risposta HTTP viene inviata toohello richiedente
19. Poiché esistono non è consentita alcuna regola di gruppo in uscita su hello risposta hello di subnet front-end
20. Poiché si tratta di hello risposta tooan stabilita la sessione NAT è accettata dal firewall hello e Hello HTTP risposta riscontri hello firewall
21. firewall Hello Reindirizza quindi hello risposta back toohello utente Internet
22. Poiché non esistono regole in uscita di gruppo o hop UDR in subnet front-end hello è consentita una risposta hello e hello utente Internet riceve hello web pagina richiesta.

#### <a name="allowed-internet-rdp-toobackend"></a>(Consentito) TooBackend Internet RDP
1. Amministratore del server su internet richiede tooAppVM01 sessione RDP tramite SecSvc001.CloudApp.Net:8025, dove 8025 è numero di porta hello assegnati all'utente per la regola del firewall "RDP tooAppVM01" hello
2. servizio cloud Hello passa il traffico attraverso endpoint aperto hello porta 8025 toofirewall interfaccia 10.0.0.4:8025
3. Nessun gruppo assegnato tooSecurity subnet, pertanto le regole di sistema NSG consentono traffico toofirewall
4. Il firewall inizia l'elaborazione delle regole:
   1. FW regola 1 (FW Mgmt) non è applicabile, spostare toonext regola
   2. Non si applica la regola 2 FW (RDP IIS), spostare toonext regola
   3. Regola di FW 3 (DNS01 RDP) non è applicabile, spostare toonext regola
   4. Applicare la regola FW 4 (AppVM01 RDP), è consentito il traffico, firewall NAT è too10.0.2.5:3386 (porta RDP in AppVM01)
5. subnet di back-end Hello inizia l'elaborazione della regola in ingresso:
   1. NSG regola 1 (blocco Internet) non è valida (il traffico è stato NAT usasse firewall hello, indirizzo di origine hello è ora pertanto firewall hello nella subnet sicurezza hello e visualizzati in base alla subnet di back-end hello traffico "local" toobe di gruppo ed è pertanto consentita), spostare toonext regola
   2. GRUPPO regole predefinite per consentire il traffico toosubnet subnet, è consentito il traffico, arrestare l'elaborazione della regola NSG
6. AppVM01 è in ascolto del traffico RDP e risponde.
7. Senza regole del gruppo di sicurezza di rete in uscita sono applicabili le regole predefinite e il traffico restituito è consentito.
8. Le route UDR il traffico in uscita toohello firewall come hop successivo hello
9. Poiché questo è restituzione di traffico in un firewall hello sessione stabilita passa utente internet di hello risposta toohello indietro
10. La sessione RDP è abilitata.
11. AppVM01 richiede il nome utente e la password.

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a>(Consentito) Ricerca DNS del server Web sul server DNS
1. Web Server, IIS01, necessita di un feed di dati in www.data.gov, ma è necessario tooresolve hello indirizzo.
2. Hello configurazione di rete per gli elenchi di rete virtuale hello DNS01 (10.0.2.4 nella subnet back-end hello) come server DNS primario hello, IIS01 invia hello DNS richiesta tooDNS01
3. Le route UDR il traffico in uscita toohello firewall come hop successivo hello
4. Nessuna regola di gruppo in uscita è subnet front-end toohello associato, è consentito il traffico
5. Il firewall inizia l'elaborazione delle regole:
   1. FW regola 1 (FW Mgmt) non è applicabile, spostare toonext regola
   2. Non applicare FW regola 2-5 (regole di RDP), spostare toonext regola
   3. Non applicare, spostare toonext regola FW regole 6 e 7 (regole di App)
   4. FW regola 8 (tooInternet) non è applicabile, spostare toonext regola
   5. Applicare FW regola 9 (DNS), è consentito il traffico, firewall inoltra il traffico too10.0.2.4 (DNS01)
6. subnet di back-end Hello inizia l'elaborazione della regola in ingresso:
   1. Regola di gruppo 1 (blocco Internet) non è applicabile, spostare toonext regola
   2. GRUPPO regole predefinite per consentire il traffico toosubnet subnet, è consentito il traffico, arrestare l'elaborazione della regola NSG
7. Server DNS riceve una richiesta di hello
8. Server DNS non dispone di indirizzo hello memorizzati nella cache e richiede un server radice DNS su hello internet
9. Le route UDR il traffico in uscita toohello firewall come hop successivo hello
10. Non sono impostate regole del gruppo di sicurezza di rete in uscita sulla subnet back-end, il traffico è consentito.
11. Il firewall inizia l'elaborazione delle regole:
    1. FW regola 1 (FW Mgmt) non è applicabile, spostare toonext regola
    2. Non applicare FW regola 2-5 (regole di RDP), spostare toonext regola
    3. Non applicare, spostare toonext regola FW regole 6 e 7 (regole di App)
    4. Applicare FW regola 8 (tooInternet) è consentito il traffico, sessione SNAT tooroot di server DNS su Internet hello
12. Server DNS Internet risponde, poiché questa sessione è stata avviata dal firewall hello, risposta hello è accettata dal firewall hello
13. Poiché si tratta di una sessione stabilita, firewall hello inoltra hello risposta toohello avvio server, DNS01
14. subnet di back-end Hello inizia l'elaborazione della regola in ingresso:
    1. Regola di gruppo 1 (blocco Internet) non è applicabile, spostare toonext regola
    2. GRUPPO regole predefinite per consentire il traffico toosubnet subnet, è consentito il traffico, arrestare l'elaborazione della regola NSG
15. server DNS Hello riceve e memorizza nella cache la risposta hello e risponde quindi toohello richiesta iniziale indietro tooIIS01
16. route UDR Hello nella subnet back-end rende hop successivo di hello firewall hello
17. Nessuna regola di gruppo in uscita presenti nella subnet back-end hello, è consentito il traffico
18. Si tratta di una sessione stabilita firewall hello, risposta hello viene inoltrato dal server IIS di hello firewall toohello indietro
19. La subnet front-end inizia l'elaborazione delle regole in ingresso:
    1. Nessuna regola di gruppo che si applica tooInbound traffico dalla subnet front-end toohello di subnet back-end di hello, pertanto nessuna delle regole NSG hello applicabile
    2. regola di sistema predefinito Hello consenta il traffico tra subnet consente il traffico in modo hello traffico è consentito
20. Iis01 riceve risposta hello da DNS01

#### <a name="allowed-backend-server-toofrontend-server"></a>(Consentito) Server di back-end server tooFrontend
1. Un amministratore connesso tooAppVM02 tramite RDP richiede un file direttamente dal server IIS01 hello tramite Esplora file
2. route UDR Hello nella subnet back-end rende hop successivo di hello firewall hello
3. Poiché esistono non è consentita alcuna regola di gruppo in uscita su hello risposta hello subnet di back-end
4. Il firewall inizia l'elaborazione delle regole:
   1. FW regola 1 (FW Mgmt) non è applicabile, spostare toonext regola
   2. Non applicare FW regola 2-5 (regole di RDP), spostare toonext regola
   3. Non applicare, spostare toonext regola FW regole 6 e 7 (regole di App)
   4. FW regola 8 (tooInternet) non è applicabile, spostare toonext regola
   5. Non applicare FW regola 9 (DNS), spostare toonext regola
   6. Applicare FW regola 10 (Intra-Subnet), è consentito il traffico, firewall passa traffico too10.0.1.4 (IIS01)
5. La subnet front-end inizia l'elaborazione delle regole in ingresso:
   1. Regola di gruppo 1 (blocco Internet) non è applicabile, spostare toonext regola
   2. GRUPPO regole predefinite per consentire il traffico toosubnet subnet, è consentito il traffico, arrestare l'elaborazione della regola NSG
6. Supponendo che l'autorizzazione e autenticazione appropriate, IIS01 accetta hello richiesta e risposta
7. route UDR Hello nella subnet front-end rende hop successivo di hello firewall hello
8. Poiché esistono non è consentita alcuna regola di gruppo in uscita su hello risposta hello di subnet front-end
9. Poiché si tratta di una sessione esistente in firewall hello è consentita la risposta e firewall hello restituisce hello risposta tooAppVM02
10. La subnet back-end inizia l'elaborazione delle regole in ingresso:
    1. Regola di gruppo 1 (blocco Internet) non è applicabile, spostare toonext regola
    2. GRUPPO regole predefinite per consentire il traffico toosubnet subnet, è consentito il traffico, arrestare l'elaborazione della regola NSG
11. AppVM02 riceve risposta hello

#### <a name="denied-internet-direct-tooweb-server"></a>(Negato) Internet diretta tooWeb Server
1. Utente Internet tenta tooaccess hello server web, IIS01, tramite hello FrontEnd001.CloudApp.Net servizio
2. Poiché non sono presenti endpoint aperto per il traffico HTTP, questa non passa attraverso hello servizio Cloud e non raggiunga il server di hello
3. Se gli endpoint hello erano aperti per qualche motivo, hello NSG (blocco Internet) in subnet front-end hello bloccano il traffico
4. Infine, route UDR subnet front-end di hello viene inviato il traffico in uscita dal firewall toohello IIS01 come hop successivo hello e firewall hello sarebbe vedere questo traffico asimmetrica e rilasciare la risposta in uscita hello pertanto esistono almeno tre livelli indipendenti difesa tra hello internet e IIS01 tramite il servizio cloud, impedendo l'accesso non autorizzato o non appropriato.

#### <a name="denied-internet-toobackend-server"></a>(Negato) Internet tooBackend Server
1. Utente Internet tenta di un file in AppVM01 tramite hello servizio BackEnd001.CloudApp.Net tooaccess
2. Poiché non sono presenti endpoint aperto per la condivisione file, questo non raggiungerebbe hello servizio Cloud e non raggiunga il server di hello
3. Se gli endpoint hello erano aperti per qualche motivo, blocca il traffico hello NSG (blocco Internet)
4. Infine, route UDR hello viene inviato il traffico in uscita dal firewall toohello AppVM01 come hop successivo hello e firewall hello sarebbe vedere questo traffico asimmetrica e rilasciare la risposta in uscita hello pertanto esistono almeno tre livelli indipendenti di difesa tra Hello internet e AppVM01 tramite il servizio cloud, impedendo l'accesso non autorizzato o non appropriato.

#### <a name="denied-frontend-server-toobackend-server"></a>(Negato) TooBackend server front-end Server
1. Si supponga IIS01 compromesso e sia in esecuzione Server subnet back-end di hello tooscan durante il tentativo di codice dannoso.
2. route UDR subnet front-end di Hello invierebbe tutto il traffico in uscita dal firewall toohello IIS01 come hop successivo hello. Non è un elemento che può essere modificato da hello compromesso macchina virtuale.
3. firewall Hello potrebbe elaborare il traffico di hello, se è stata richiesta hello tooAppVM01 o toohello DNS server per le ricerche DNS che il traffico potrebbe potenzialmente essere consentito dal firewall hello (scadenza tooFW regole 7 e 9). Tutto il resto del traffico verrebbe bloccato dalla regola firewall 11 (Deny All).
4. Se avanzate di rilevamento minacce è stato abilitato il firewall hello (non illustrata in questo documento, vedere la documentazione del fornitore hello per dispositivo di rete specifica minaccia funzionalità avanzate), anche il traffico che sarebbe necessario consentire hello base di regole di inoltro illustrati in questo documento può contribuire a evitare traffico hello contenuti firme note o modelli che una regola avanzata minaccia di flag.

#### <a name="denied-internet-dns-lookup-on-dns-server"></a>(Negato) Ricerca DNS Internet sul server DNS
1. Utente Internet tenta un record DNS interno nella DNS01 tramite servizio BackEnd001.CloudApp.Net toolookup 
2. Poiché non sono presenti endpoint aperto per il traffico DNS, questo non passa attraverso hello servizio Cloud e non raggiunga il server di hello
3. Se gli endpoint hello erano aperti per qualche motivo, regola di gruppo hello (blocco Internet) in subnet front-end hello bloccano il traffico
4. Infine, route UDR subnet back-end di hello viene inviato il traffico in uscita dal firewall toohello DNS01 come hop successivo hello e firewall hello sarebbe vedere questo traffico asimmetrica e rilasciare la risposta in uscita hello pertanto esistono almeno tre livelli indipendenti difesa tra hello internet e DNS01 tramite il servizio cloud, impedendo l'accesso non autorizzato o non appropriato.

#### <a name="denied-internet-toosql-access-through-firewall"></a>(Negato) Accesso a Internet tooSQL tramite Firewall
1. L'utente Internet richiede dati SQL a SecSvc001.CloudApp.Net (servizio cloud per Internet).
2. Poiché non sono presenti endpoint aperto per SQL, questo non raggiungerebbe hello servizio Cloud e non raggiunga firewall hello
3. Se gli endpoint SQL sono stati aperti per qualche motivo, il firewall hello inizierebbe l'elaborazione della regola:
   1. FW regola 1 (FW Mgmt) non è applicabile, spostare toonext regola
   2. Regole FW 2-5 (regole di RDP) non si applicano, spostare toonext regola
   3. Non applicare, spostare toonext regola FW regola 6 e 7 (regole di applicazione)
   4. FW regola 8 (tooInternet) non è applicabile, spostare toonext regola
   5. Non applicare FW regola 9 (DNS), spostare toonext regola
   6. FW regola 10 (Intra-Subnet) non è applicabile, spostare toonext regola
   7. Regole firewall 11 (Deny All) applicabile, il traffico viene bloccato, l'elaborazione della regola si arresta.

## <a name="references"></a>Riferimenti
### <a name="main-script-and-network-config"></a>Script principale e configurazione di rete
Salvare uno Script completo di hello in un file di script di PowerShell. Salvare hello configurazione di rete in un file denominato "NetworkConf2.xml".
Modificare le variabili definite dall'utente di hello in base alle esigenze. Eseguire script hello, quindi seguire istruzioni di programma di installazione di un regola Firewall di hello precedente.

#### <a name="full-script"></a>Script completo
Questo script verrà, in base alle variabili definite dall'utente hello:

1. Connettersi tooan sottoscrizione di Azure
2. Creare un nuovo account di archiviazione.
3. Creare una nuova rete virtuale e tre le subnet, come definito nel file di configurazione di rete hello
4. Compilare cinque macchine virtuali, 1 firewall e 4 VM Windows Server.
5. Configurare il routing definito dall'utente, incluse le operazioni seguenti:
   1. Creazione di due nuove tabelle di route.
   2. Aggiungere le route toohello tabelle
   3. Associare subnet tooappropriate tabelle
6. Attivare l'inoltro IP hello NVA
7. Configurare il gruppo di sicurezza di rete, incluse le operazioni seguenti:
   1. Creazione di un gruppo di sicurezza di rete.
   2. Aggiunta di una regola.
   3. Subnet appropriata toohello associazione hello NSG

Questo script di PowerShell deve essere eseguito localmente in un server o un PC connesso a Internet.

> [!IMPORTANT]
> Quando si esegue lo script, in PowerShell potrebbero venire visualizzati avvisi o altri messaggi informativi. Solo i messaggi di errore formattati in rosso possono indicare un problema.
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and User Defined Routing in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Three new cloud services
       - Three Subnets (SecNet, FrontEnd, and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet
       - Three Servers on hello BackEnd Subnet
       - IP Forwading from hello FireWall out toohello internet
       - User Defined Routing FrontEnd and BackEnd Subnets toohello NVA

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind hello appropriate
      layer(s) of protection. This script serves as an example of some of hello techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and hello appropriate protections needed, and then effectively
      implement those protections.

      Security Service (SecNet subnet 10.0.0.0/24)
       myFirewall - 10.0.0.4

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       IIS01      - 10.0.1.4

      BackEnd Service (BackEnd subnet 10.0.2.0/24)
       DNS01      - 10.0.2.4
       AppVM01    - 10.0.2.5
       AppVM02    - 10.0.2.6

    #>

    # Fixed Variables
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes tooreflect your subscription and services
      # Invalid options will fail in hello validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $SecureService = "SecSvc001"
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $VNetPrefix = "10.0.0.0/16"
        $SecNet = "SecNet"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf3.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # UDR Details
        $FERouteTableName = "FrontEndSubnetRouteTable"
        $BERouteTableName = "BackEndSubnetRouteTable"

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be hello NVA.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
            Return}
        Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
              New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

      # Update Subscription Pointer tooNew Storage Account
        Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "hello SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use" -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $SecureService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

    # Build VMs
        $i=0
        $VMName | Foreach {
            Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: All traffic goes through hello firewall, so we'll need tooset up all ports here.
                #       Also, hello firewall will be redirecting traffic tooa new IP and Port in a forwarding
                #       rule, so all of these endpoint have hello same public and local port and hello firewall
                #       will do hello mapping, NATing, and/or redirection as declared in hello firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "RemoteDesktop" | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                }
            $i++
        }

    # Configure UDR and IP Forwarding
        Write-Host "Configuring UDR" -ForegroundColor Cyan

      # Create hello Route Tables
        Write-Host "Creating hello Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes tooRoute Tables
        Write-Host "Adding Routes toohello Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate hello Route Tables with hello Subnets
        Write-Host "Binding Route Tables toohello Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on hello Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign hello NSG tootwo Subnets
        # hello NSG is *not* bound toohello Security Subnet. hello result
        # is that internet traffic flows only toohello Security subnet
        # since hello NSG bound toohello Frontend and Backback subnets
        # will Deny internet traffic toothose subnets.
        Write-Host "Binding hello NSG tootwo subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a>File di configurazione di rete
Salvare il file xml con posizione aggiornata e aggiungere hello collegamento toothis file toohello $NetworkConfigFile variabile nello script hello precedente.

    <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
      <VirtualNetworkConfiguration>
        <Dns>
          <DnsServers>
            <DnsServer name="DNS01" IPAddress="10.0.2.4" />
            <DnsServer name="Level3" IPAddress="209.244.0.3" />
          </DnsServers>
        </Dns>
        <VirtualNetworkSites>
          <VirtualNetworkSite name="CorpNetwork" Location="Central US">
            <AddressSpace>
              <AddressPrefix>10.0.0.0/16</AddressPrefix>
            </AddressSpace>
            <Subnets>
              <Subnet name="SecNet">
                <AddressPrefix>10.0.0.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="FrontEnd">
                <AddressPrefix>10.0.1.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="BackEnd">
                <AddressPrefix>10.0.2.0/24</AddressPrefix>
              </Subnet>
            </Subnets>
            <DnsServersRef>
              <DnsServerRef name="DNS01" />
              <DnsServerRef name="Level3" />
            </DnsServersRef>
          </VirtualNetworkSite>
        </VirtualNetworkSites>
      </VirtualNetworkConfiguration>
    </NetworkConfiguration>

#### <a name="sample-application-scripts"></a>Script di applicazione di esempio
Se si desidera tooinstall un'applicazione di esempio per questo e altri esempi di rete Perimetrale, ne è stato fornito al collegamento hello: [Script dell'applicazione di esempio][SampleApp]

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Rete perimetrale bidirezionale con appliance virtuale di rete, gruppo di sicurezza di rete e routing definito dall'utente"
[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Vista logica di hello regole del Firewall"
[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Creare un oggetto di rete front-end"
[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Creare un oggetto server DNS"
[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Copiare la regola RDP predefinita"
[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "Regola AppVM01"
[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Icona di reindirizzamento dell'applicazione"
[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Icona di Destination NAT"
[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Icona di passaggio"
[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Regola di gestione del firewall"
[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "Regola firewall RDP"
[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Regola firewall Web"
[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "Regola firewall AppVM01"
[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Regola firewall in uscita"
[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "Regola firewall DNS"
[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Regola firewall Intra-VNet"
[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Regola firewall Deny"
[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Attivazione delle regole firewall"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
