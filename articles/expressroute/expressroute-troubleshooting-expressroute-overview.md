---
title: "Verifica della connettività: guida alla risoluzione dei problemi di Azure ExpressRoute | Microsoft Docs"
description: "Questa pagina vengono fornite istruzioni sulla risoluzione dei problemi e convalida della connettività tooend fine di un circuito ExpressRoute."
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 713c39c7eafd77a4380b2a91902a9686f2ce1d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="verifying-expressroute-connectivity"></a>Verifica della connettività di ExpressRoute
ExpressRoute, che estende una rete locale nel cloud di Microsoft hello su una connessione privata mediante un provider di connettività, prevede hello seguenti tre aree di rete distinti:

-   Rete del cliente
-   Rete del provider
-   Datacenter Microsoft

scopo di Hello di questo documento è toohelp utente tooidentify dove (o anche se) esiste un problema di connettività e all'interno della zona, che in tal modo tooseek Guida dal problema di hello tooresolve team appropriato. Se il supporto tecnico Microsoft è necessario tooresolve un problema, aprire un ticket di supporto con [supporto Microsoft][Support].

> [!IMPORTANT]
> Questo documento è previsto toohelp la diagnosi e la risoluzione dei problemi di tipo semplici. Non è previsto toobe una sostituzione per il supporto tecnico Microsoft. Aprire un ticket di supporto con [supporto Microsoft] [ Support] in caso di problema hello toosolve Impossibile utilizzando istruzioni hello disponibili.
>
>

## <a name="overview"></a>Panoramica
Hello diagramma seguente mostra la connettività logico hello di una rete di tooMicrosoft cliente tramite ExpressRoute.
[![1]][1]

Nel precedente diagramma di hello, hello numeri indicano i punti chiave di rete. punti di rete Hello fa riferimento spesso questo articolo il numero associato.

A seconda della connettività di ExpressRoute hello modello (Cloud Exchange condivisione percorso, connessione Ethernet o Any per qualsiasi (IPVPN)) hello rete punti 3 e 4 potrebbero essere switch (dispositivi di livello 2). di seguito sono riportati i punti chiave di rete Hello illustrati:

1.  Dispositivo di calcolo del cliente (ad esempio, un server o un PC)
2.  CE: router perimetrali del cliente 
3.  PE (rivolti verso i CE): router/switch perimetrali del provider rivolti verso i router perimetrali del cliente. Cui tooas PE CEs in questo documento.
4.  PE (rivolti verso gli MSEE): router/switch perimetrali del provider rivolti verso gli MSEE. Cui tooas PE MSEEs in questo documento.
5.  MSEE: router ExpressRoute Microsoft Enterprise Edge (MSEE)
6.  Gateway di rete virtuale (VNet)
7.  Dispositivo di rete virtuale di Azure hello di calcolo

Se si utilizzano i modelli di connettività Cloud Exchange condivisione percorso o connessione Ethernet hello, router perimetrale del cliente hello (2) si possa stabilire BGP peering con MSEEs (5). I punti 3 e 4 sono ancora presenti, ma in forma trasparente, come dispositivi di livello 2.

Se si utilizza modello di integrazione applicativa hello Any per qualsiasi (IPVPN), hello PEs (con connessione MSEE) (4) si possa stabilire BGP peering con MSEEs (5). Le route propagherebbe quindi rete cliente toohello indietro tramite una rete hello IPVPN service provider.

>[!NOTE]
>Per la disponibilità elevata di ExpressRoute, Microsoft richiede una coppia ridondante di sessioni BGP tra MSEE (5) e PE-MSEE (4). Si consiglia anche una coppia ridondante di percorsi di rete tra rete del cliente e PE-CE. Nel modello (IPVPN) Any per qualsiasi connessione, tuttavia, un singolo dispositivo CE (2) può essere connesso tooone o più file PE (3).
>
>

(con hello rete indicata dal numero di hello associata) vengono trattati i toovalidate un circuito ExpressRoute, hello alla procedura seguente:
1. [Convalidare il provisioning del circuito e lo stato (5)](#validate-circuit-provisioning-and-state)
2. [Convalidare la configurazione di almeno un peering di ExpressRoute (5)](#validate-peering-configuration)
3. [Convalidare ARP tra provider di servizi Microsoft e hello (collegamento tra 4 e 5)](#validate-arp-between-microsoft-and-the-service-provider)
4. [Convalidare il protocollo BGP e route su hello MSEE (BGP tra too5 4 e 5 too6 se una rete virtuale è connesso)](#validate-bgp-and-routes-on-the-msee)
5. [Controllo hello statistiche sul traffico (traffico che attraversa 5)](#check-the-traffic-statistics)

Altre convalide e controlli verranno aggiunti in hello future, verificare mensile!

##<a name="validate-circuit-provisioning-and-state"></a>Convalidare il provisioning del circuito e lo stato
Indipendentemente dal modello di integrazione applicativa hello, un circuito ExpressRoute ha toobe creato e quindi un servizio chiave generata per il provisioning del circuito. Il provisioning di un circuito ExpressRoute stabilisce connessioni ridondanti di livello 2 tra PE-MSEE (4) e MSEE (5). Per ulteriori informazioni su come toocreate, modificare, eseguire il provisioning e verificare un circuito ExpressRoute, vedere l'articolo hello [creare e modificare un circuito ExpressRoute][CreateCircuit].

>[!TIP]
>Una chiave del servizio identifica in modo univoco un circuito ExpressRoute. Questa chiave è obbligatoria per la maggior parte dei comandi di powershell hello citate in questo documento. È inoltre necessario richiedere assistenza da Microsoft o da un tootroubleshoot partner ExpressRoute un problema di ExpressRoute, fornire il servizio di hello tooreadily chiave identifica il circuito hello.
>
>

###<a name="verification-via-hello-azure-portal"></a>Verifica tramite hello portale di Azure
In hello portale di Azure, lo stato di hello di un circuito ExpressRoute può essere controllato selezionando ![2][2] su hello menu laterale a sinistra e quindi selezionando hello circuito ExpressRoute. Selezione di ExpressRoute circuito sotto "Tutte le risorse" apre il pannello di circuito ExpressRoute hello. In hello ![3][3] sezione del pannello hello, hello ExpressRoute essentials sono elencati come illustrato nella seguente cattura di schermata hello:

![4][4]    

In Essentials ExpressRoute, hello *Circuit stato* indica lo stato di hello del circuito hello in hello lato Microsoft. *Stato provider* indica se è stato circuito hello */non provisioning eseguito il provisioning* sul lato di provider di servizi di hello. 

Per un toobe di circuito ExpressRoute operativa, hello *Circuit stato* deve essere *abilitato* hello e *stato Provider* deve essere *provisioning eseguito*.

>[!NOTE]
>Se hello *Circuit stato* non è abilitato, contattare [supporto Microsoft][Support]. Se hello *stato Provider* non è disponibile, contattare il provider di servizi.
>
>

###<a name="verification-via-powershell"></a>Verifica tramite PowerShell
toolist tutti hello circuiti ExpressRoute in un gruppo di risorse, usare hello comando seguente:

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
>È possibile ottenere il nome del gruppo di risorse tramite hello portale di Azure. Vedere hello sottosezione precedente di questo documento e si noti che il nome del gruppo di risorse hello è elencato nella schermata dell'esempio hello.
>
>

tooselect un particolare circuito ExpressRoute in un gruppo di risorse, utilizzare hello comando seguente:

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

Una risposta di esempio:

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

tooconfirm se un circuito ExpressRoute è operativo, è necessario prestare particolare attenzione toohello seguenti campi:

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
>Se hello *stato di provisioning* non è abilitato, contattare [supporto Microsoft][Support]. Se hello *ServiceProviderProvisioningState* non è disponibile, contattare il provider di servizi.
>
>

###<a name="verification-via-powershell-classic"></a>Verifica tramite PowerShell (versione classica)
toolist tutti hello circuiti ExpressRoute in una sottoscrizione, utilizzare hello comando seguente:

    Get-AzureDedicatedCircuit

tooselect un particolare circuito ExpressRoute, utilizzare hello comando seguente:

    Get-AzureDedicatedCircuit -ServiceKey **************************************

Una risposta di esempio:

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

tooconfirm se un circuito ExpressRoute è operativo, prestare particolare attenzione toohello seguenti campi: ServiceProviderProvisioningState: lo stato di provisioning: abilitato

>[!NOTE]
>Se hello *stato* non è abilitato, contattare [supporto Microsoft][Support]. Se hello *ServiceProviderProvisioningState* non è disponibile, contattare il provider di servizi.
>
>

##<a name="validate-peering-configuration"></a>Convalidare la configurazione del peering
Dopo il provider di servizi di hello ha completato hello provisioning del circuito ExpressRoute hello, è possibile creare una configurazione di routing su hello circuito ExpressRoute tra MSEE (4), le prenotazioni permanenti e MSEEs (5). Ogni circuito ExpressRoute può avere uno, due o tre contesti di routing abilitati: peering privato di Azure (traffico tooprivate reti virtuali in Azure), peering pubblico di Azure (traffico toopublic gli indirizzi IP in Azure) e (traffico tooOffice 365 peering Microsoft e Dynamics 365). Per ulteriori informazioni su come toocreate e modificare la configurazione di routing, vedere l'articolo hello [creare e modificare il routing per un circuito ExpressRoute][CreatePeering].

###<a name="verification-via-hello-azure-portal"></a>Verifica tramite hello portale di Azure
>[!IMPORTANT]
>È presente un bug noto nel portale di Azure in cui il peering ExpressRoute è hello *non* visualizzata nel portale di hello se configurato dal provider di servizi di hello. Aggiunta di peering ExpressRoute tramite il portale di hello o PowerShell *sovrascrive le impostazioni del provider servizio hello*. Questa azione interrompe hello routing sul circuito ExpressRoute hello e richiede il supporto di hello hello impostazioni del servizio provider toorestore hello e ristabilire la normale di routing. Modificare solo il peering ExpressRoute hello se si è certi che il provider di servizi di hello fornisce solo servizi di livello 2.
>
>

<p/>
>[!NOTE]
>Se layer 3 viene fornito da hello peering hello e di provider di servizio sono vuote nel portale di hello, PowerShell può essere utilizzato toosee hello servizio provider configurato impostazioni.
>
>

In hello portale di Azure, lo stato di un circuito ExpressRoute può essere controllato selezionando ![2][2] su hello menu laterale a sinistra e quindi selezionando hello circuito ExpressRoute. Selezione di ExpressRoute circuito sotto "Tutte le risorse" aprire Pannello circuito ExpressRoute di hello. In hello ![3][3] sezione del pannello hello, hello ExpressRoute essentials sarà elencato come illustrato nella seguente cattura di schermata hello:

![5][5]

In hello sopra riportato, come indicato Azure contesto di routing di peering privato è abilitata, mentre Azure pubblico e contesti di routing peering Microsoft non sono abilitati. Un contesto di peering abilitato correttamente avrebbe subnet primario e secondario Point-to-(obbligatorio per il protocollo BGP) hello elencate. subnet Hello /30 vengono utilizzate per l'indirizzo IP dell'interfaccia hello di hello MSEEs e PE MSEEs. 

>[!NOTE]
>Se un peering non è abilitato, verificare se subnet primario e secondario hello assegnata corrisponde configurazione hello PE MSEEs. Se non, toochange hello configurazione router MSEE, fare riferimento troppo[creare e modificare il routing per un circuito ExpressRoute][CreatePeering]
>
>

###<a name="verification-via-powershell"></a>Verifica tramite PowerShell
tooget hello Azure privata peering dettagli di configurazione, utilizzare hello seguenti comandi:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

Una risposta di esempio, per un peering privato configurato correttamente:

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 Un contesto di peering abilitato correttamente avrebbe prefissi di indirizzo primario e secondario hello elencati. subnet Hello /30 vengono utilizzate per l'indirizzo IP dell'interfaccia hello di hello MSEEs e PE MSEEs.

tooget hello Azure pubblica peering dettagli di configurazione, utilizzare hello seguenti comandi:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

tooget hello Microsoft peering dettagli di configurazione, utilizzare hello seguenti comandi:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

Se non è configurato alcun peering, viene visualizzato un messaggio di errore. Una risposta di esempio, quando hello indicato peering (pubblico di Azure peering in questo esempio) non è configurata nel circuito hello:

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
>Se un peering non è abilitato, verificare se hello corrispondenza hello primario e secondario subnet assegnate configurazione hello collegato PE MSEE. Anche verificare se hello correggere *VlanId*, *AzureASN*, e *PeerASN* vengono utilizzati su MSEEs e se questi valori viene eseguito il mapping toohello quelli utilizzati in hello collegato PE MSEE. Se si sceglie di hash MD5, la chiave condivisa hello deve corrispondere in coppia MSEE e PE MSEE. configurazione di hello toochange in router MSEE hello, fare riferimento troppo [creare e modificare il routing per un circuito ExpressRoute] [CreatePeering].  
>
>

### <a name="verification-via-powershell-classic"></a>Verifica tramite PowerShell (versione classica)
tooget hello Azure privata peering dettagli di configurazione, utilizzare hello comando seguente:

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

Una risposta di esempio, per un peering privato configurato correttamente:

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

Abilitato correttamente, un contesto di peering avrebbe subnet peer primaria e secondaria hello elencate. subnet Hello /30 vengono utilizzate per l'indirizzo IP dell'interfaccia hello di hello MSEEs e PE MSEEs.

tooget hello Azure pubblica peering dettagli di configurazione, utilizzare hello seguenti comandi:

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

tooget hello Microsoft peering dettagli di configurazione, utilizzare hello seguenti comandi:

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
>Se peering di livello 3 sono state impostate dal provider di servizi di hello, l'impostazione di peering ExpressRoute hello tramite il portale di hello o PowerShell sovrascrive le impostazioni del provider servizio hello. Reimpostazione delle impostazioni peer hello provider lato richiede il supporto di hello hello del provider di servizi. Modificare solo il peering ExpressRoute hello se si è certi che il provider di servizi di hello fornisce solo servizi di livello 2.
>
>

<p/>
>[!NOTE]
>Se un peering non è abilitato, verificare se hello peer primario e secondario subnet assegnate corrispondenza hello configurazione su hello collegato PE MSEE. Anche verificare se hello correggere *VlanId*, *AzureAsn*, e *PeerAsn* vengono utilizzati su MSEEs e se questi valori viene eseguito il mapping toohello quelli utilizzati in hello collegato PE MSEE. configurazione di hello toochange in router MSEE hello, fare riferimento troppo [creare e modificare il routing per un circuito ExpressRoute] [CreatePeering].
>
>

## <a name="validate-arp-between-microsoft-and-hello-service-provider"></a>Convalidare ARP tra Microsoft e hello provider del servizio
In questa sezione vengono usati i comandi di PowerShell (versione classica). Se si utilizza i comandi di gestione risorse di Azure PowerShell, assicurarsi di avere accesso amministratore/coamministratore toohello sottoscrizione tramite [portale di Azure classico][OldPortal]. Per la risoluzione dei problemi mediante Gestione risorse di Azure i comandi, vedere toohello [tabelle recupero ARP nel modello di distribuzione di gestione risorse di hello] [ ARP] documento.

>[!NOTE]
>tooget ARP, sia hello portale di Azure e i comandi di PowerShell di gestione risorse di Azure può essere utilizzato. Se si verificano errori con i comandi di PowerShell di gestione risorse di Azure hello, i comandi di PowerShell classici dovrebbero funzionare come PowerShell classico comandi funzionano anche con circuiti ExpressRoute di gestione risorse di Azure.
>
>

tooget hello tabella ARP hello MSEE del router principale per il peering privato hello, usare hello comando seguente:

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

Una risposta di esempio per il comando di hello, in caso di esito positivo hello:

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

Analogamente, è possibile controllare la tabella ARP da Ciao MSEE hello hello *primario*/*secondario* percorso, per *privata* /  *Pubblica*/*Microsoft* peering.

Hello esempio seguente viene mostrato hello risposta del comando hello per un peering non esiste.

    ARP Info:
       
>[!NOTE]
>Se la tabella ARP hello non dispone di indirizzi IP delle interfacce hello eseguire il mapping di indirizzi tooMAC, hello esaminare le seguenti informazioni:
>1. Se hello primo indirizzo IP del subnet hello /30 assegnato per il collegamento hello tra hello MSEE PR e MSEE viene utilizzato nell'interfaccia hello del MSEE PR Azure Usa sempre l'indirizzo IP secondo hello per MSEEs.
>2. Verificare se cliente hello (C-Tag) e i tag VLAN servizio (S-Tag) corrispondano entrambi in coppia MSEE PR e MSEE.
>
>

## <a name="validate-bgp-and-routes-on-hello-msee"></a>Convalidare il protocollo BGP e route su hello MSEE
In questa sezione vengono usati i comandi di PowerShell (versione classica). Se si utilizza i comandi di gestione risorse di Azure PowerShell, assicurarsi di avere accesso amministratore/coamministratore toohello sottoscrizione tramite [portale di Azure classico][OldPortal]

>[!NOTE]
>tooget BGP informazioni, entrambi hello è possibile utilizzare il portale di Azure e i comandi di PowerShell di gestione risorse di Azure. Se si verificano errori con i comandi di PowerShell di gestione risorse di Azure hello, i comandi di PowerShell classici dovrebbero funzionare come PowerShell classico comandi funzionano anche con circuiti ExpressRoute di gestione risorse di Azure.
>
>

tooget hello tabella di routing (adiacente BGP) riepilogo per un particolare contesto di routing, utilizzare hello comando seguente:

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

Una risposta di esempio:

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

Come illustrato nell'esempio sopra riportato hello, hello è utile toodetermine per quanto tempo contesto routing hello è stata stabilita. Indica inoltre il numero di prefissi di route annunciate dal router di peering hello.

>[!NOTE]
>Se lo stato di hello è attivo o inattivo, controllare se hello peer primario e secondario subnet assegnate corrispondenza hello configurazione su hello collegato PE MSEE. Anche verificare se hello correggere *VlanId*, *AzureAsn*, e *PeerAsn* vengono utilizzati su MSEEs e se questi valori viene eseguito il mapping toohello quelli utilizzati in hello collegato PE MSEE. Se si sceglie di hash MD5, la chiave condivisa hello deve corrispondere in coppia MSEE e PE MSEE. configurazione di hello toochange in router MSEE hello, fare riferimento troppo[creare e modificare il routing per un circuito ExpressRoute][CreatePeering].
>
>

<p/>
>[!NOTE]
>Se alcune destinazioni non sono raggiungibili su un particolare peering, controllare la tabella di route hello di hello MSEEs appartenenti toohello particolare contesto peer. Se un prefisso corrispondente (potrebbe essere NATed IP) è presente nella tabella di routing hello, controllare se sono presenti firewall/gruppo/ACL nel percorso hello e consentono il traffico di hello.
>
>

tooget hello completa tabella di routing da MSEE su hello *primario* percorso per hello particolare *privata* contesto routing, utilizzare hello comando seguente:

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

È un risultato positivo di esempio per il comando hello:

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

Analogamente, è possibile controllare tabella di routing hello da Ciao MSEE hello *primario*/*secondario* percorso, per *privata* / *Pubblica*/*Microsoft* un contesto di peer.

Hello esempio seguente viene mostrato hello risposta del comando hello per un peering non esiste:

    Route Table Info:

##<a name="check-hello-traffic-statistics"></a>Controllare le statistiche sul traffico hello
hello tooget combinati e disconnettersi, statistiche sul traffico percorso primario e secondario - byte di un contesto di peering, utilizzare hello comando seguente:

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

Un esempio di output del comando hello è:

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

È un esempio di output del comando hello per un peering non esistente:

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni o assistenza, vedere hello seguenti collegamenti:

- [Supporto tecnico Microsoft][Support]
- [Creare e modificare un circuito ExpressRoute][CreateCircuit]
- [Creare e modificare il routing per un circuito ExpressRoute][CreatePeering]

<!--Image References-->
[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Connettività logica ExpressRoute"
[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Icona All resources"
[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Icona Overview"
[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "Schermata di esempio delle informazioni di base di ExpressRoute"
[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "Schermata di esempio delle informazioni di base di ExpressRoute"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






