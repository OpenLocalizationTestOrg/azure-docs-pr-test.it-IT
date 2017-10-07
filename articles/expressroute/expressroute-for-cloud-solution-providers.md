---
title: aaaAzure ExpressRoute per il provider di soluzioni Cloud | Documenti Microsoft
description: In questo articolo vengono fornite informazioni per il provider di servizi Cloud che tooincorporate desidera Azure ExpressRoute alle offerte e servizi.
documentationcenter: na
services: expressroute
author: richcar
manager: carmonm
editor: 
ms.assetid: f6c5f8ee-40ba-41a1-ae31-67669ca419a6
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: richcar
ms.openlocfilehash: 062ecbb5e461e4384b01c4ac478cab696b7ed398
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-for-cloud-solution-providers-csp"></a>ExpressRoute per Cloud Solution Provider (CSP)
Microsoft fornisce servizi di Hyper-scala per rivenditori tradizionali e nuovi servizi e soluzioni per i clienti senza hello tooinvest lo sviluppo di questi nuovi servizi è necessario effettuare il provisioning di toobe toorapidly in grado di server di distribuzione (CSP). tooallow hello Provider di soluzioni Cloud (CSP) hello possibilità toodirectly gestire questi nuovi servizi, Microsoft fornisce API che consentono di hello CSP toomanage risorse di Microsoft Azure per conto del cliente e applicazioni. Una di queste risorse è ExpressRoute. ExpressRoute consente hello CSP tooconnect cliente risorse tooAzure servizi esistenti. ExpressRoute è un tooservices di collegamento ad alta velocità le comunicazioni private in Azure. 

ExpresRoute è costituita da una coppia di circuiti per la disponibilità elevata che sono collegati tooa singolo cliente sottoscrizioni e non può essere condiviso da più clienti. Ogni circuito deve essere interrotto in un router diverso toomaintain hello a disponibilità elevata.

> [!NOTE]
> Poiché in ExpressRoute esistono limiti di larghezza di banda e di connessione, le implementazioni di grandi dimensioni/complesse richiederanno più circuiti di ExpressRoute per un singolo cliente.
> 
> 

Microsoft Azure offre un numero crescente di servizi che è possibile offrire ai clienti di tooyour.  sfruttare toobest questi servizi sarà necessario utilizzare hello ExpressRoute connessioni tooprovide ad alta velocità a bassa latenza accesso toohello ambiente Microsoft Azure.

## <a name="microsoft-azure-management"></a>Gestione di Microsoft Azure
Microsoft offre CSP API toomanage le sottoscrizioni dei clienti Azure hello consentendo l'integrazione a livello di codice con i propri sistemi di gestione del servizio. Le funzionalità di gestione supportate sono disponibili [qui](https://msdn.microsoft.com/library/partnercenter/dn974944.aspx).

## <a name="microsoft-azure-resource-management"></a>Gestione di risorse di Microsoft Azure
A seconda di hello contratto con il cliente determinerà come verrà gestiti sottoscrizione hello. Hello CSP poter gestire direttamente la creazione di hello e manutenzione delle risorse o ai clienti di hello possa mantenere il controllo della sottoscrizione di Microsoft Azure hello e creare risorse di Azure hello secondo necessità. Se il cliente gestisce creazione hello delle risorse nella propria sottoscrizione di Microsoft Azure verrà utilizzato uno dei due modelli: "Connetti tramite" modello di, o "Direct-To". Questi modelli sono descritti in dettaglio nelle sezioni che seguono hello.  

### <a name="connect-through-model"></a>Modello di connessione indiretta
![testo alternativo](./media/expressroute-for-cloud-solution-providers/connect-through.png)  

Nel modello di hello, connettersi tramite hello CSP crea una connessione diretta tra il Data Center e sottoscrizione di Azure del cliente. connessione diretta Hello viene effettuata utilizzando ExpressRoute, la connessione di rete con Azure. Rete tooyour si connette quindi al cliente. Questo scenario richiede che tale cliente hello attraversa hello CSP rete tooaccess servizi di Azure. 

Se il cliente dispone di altre sottoscrizioni di Azure non gestiti da hello, viene utilizzato hello i propri servizi di toothose tooconnect connessione privata, il provisioning nella sottoscrizione non CSP hello o di rete Internet pubblica. 

Per la gestione dei servizi Azure di CSP, si presuppone che hello CSP dispone di un'identità stabilita in precedenza cliente archiviare che verrebbero quindi replicati in Azure Active Directory per la gestione della sottoscrizione CSP tramite Administrate-On-Behalf-Of (AOBO). Chiave per questo scenario ad esempio, in cui un determinato partner o un provider di servizi ha una relazione con il cliente hello, cliente hello utilizza servizi di provider attualmente o partner hello ha un tooprovide desiderio una combinazione di ospitato dal provider soluzioni ospitato da Azure tooprovide flessibilità e l'indirizzo cliente sfide e che non possono essere soddisfatti dal CSP da solo. Questo modello è illustrato nella **figura**seguente.

![testo alternativo](./media/expressroute-for-cloud-solution-providers/connect-through-model.png)

### <a name="connect-toomodel"></a>Toomodel connettersi
![testo alternativo](./media/expressroute-for-cloud-solution-providers/connect-to.png)

In Connetti toomodel hello, il provider di servizi di hello crea una connessione diretta tra Data Center del cliente, i relativi e CSP hello provisioning sottoscrizione di Azure tramite ExpressRoute su hello del cliente (customer) rete.

> [!NOTE]
> Per ExpressRoute cliente hello sarebbe necessario toocreate e gestire circuiti ExpressRoute hello.  
> 
> 

Questo scenario di connettività richiede che tale cliente hello si connette direttamente tramite un tooaccess rete cliente sottoscrizione di Azure gestita CSP, utilizzando una connessione diretta alla rete che viene creata, proprietà e gestita interamente o in parte dal cliente hello. Per questi clienti presuppone che il provider di hello non dispone attualmente di un archivio di identità cliente stabilito e provider hello contribuirebbe cliente hello nella replica dei loro archivio identità corrente in Azure Active Directory per la gestione di loro sottoscrizione tramite AOBO. I fattori chiave per questo scenario includono in un determinato partner o un provider di servizi ha una relazione con il cliente hello, cliente hello utilizza servizi di provider attualmente o partner hello è assunta tooprovide services che sono basate esclusivamente su Soluzioni ospitato in Azure senza hello necessitano per un'infrastruttura o un Data Center di provider esistenti.

![testo alternativo](./media/expressroute-for-cloud-solution-providers/connect-to-model.png)

Hello scelta tra queste due opzioni si basano sulle esigenze del cliente e attualmente necessario tooprovide Azure servizi. Dettagli Hello di questi modelli e hello associato controllo di accesso basato sui ruoli, servizi di rete, e modelli di progettazione di identità sono illustrati nei dettagli in hello seguenti collegamenti:

* **Controllo degli accessi in base al ruolo** : il controllo degli accessi in base al ruolo si basa su Azure Active Directory.  Per altre informazioni sul controllo degli accessi in base al ruolo di Azure, vedere [qui](../active-directory/role-based-access-control-configure.md).
* **Rete** – include hello diversi argomenti della rete in Microsoft Azure.
* **Azure Active Directory (AAD)** -AAD consente la gestione dell'identità hello Microsoft Azure e 3 applicazioni SaaS di terze parti. Per altre informazioni su Azure AD, vedere [qui](https://azure.microsoft.com/documentation/services/active-directory/).  

## <a name="network-speeds"></a>Velocità di rete
ExpressRoute supporta velocità di rete da 50 Mb/s too10Gb/s. Questo consente ai clienti quantità hello toopurchase larghezza di banda di rete necessaria per il proprio ambiente univoco.

> [!NOTE]
> Larghezza di banda di rete può essere aumentato in base alle esigenze senza interrompere le comunicazioni, ma la velocità della rete hello tooreduce richiede chiudere circuito hello e ricrearla alla velocità di rete inferiore hello.  
> 
> 

ExpressRoute supporta connessione hello del circuito ExpressRoute di più reti virtuali tooa singolo un migliore utilizzo delle connessioni ad alta velocità hello. Un singolo circuito ExpressRoute può essere condivise tra più sottoscrizioni di Azure di proprietà hello stesso cliente.

## <a name="configuring-expressroute"></a>Configurazione di ExpressRoute
ExpressRoute può essere configurato toosupport tre tipi di traffico ([domini di routing](#ExpressRoute-routing-domains)) su un singolo circuito ExpressRoute. Questo traffico viene separato nel peer Microsoft, nel peer pubblico di Azure e nel peer privato. È possibile scegliere uno o tutti i tipi di traffico toobe inviati in un singolo circuito ExpressRoute o usare più circuiti ExpressRoute a seconda delle dimensioni di hello del circuito ExpressRoute hello e isolamento per il cliente non necessaria. condizioni di sicurezza Hello del cliente potrebbero non essere consentita pubblica traffico e traffico privato tootraverse su hello stesso circuito.

### <a name="connect-through-model"></a>Modello di connessione indiretta
In un hello connect-tramite configurazione sarà responsabile di tutte hello rete tooconnect base sottoscrizioni toohello risorse datacenter i clienti ospitate in Azure. Ognuno dei clienti che desidera toouse funzionalità di Azure sarà necessaria la connessione ExpressRoute, che verrà gestita da hello è. Hello si utilizzerà hello stesso cliente di hello metodi utilizzerebbe circuito ExpressRoute di tooprocure hello. Hello si effettueranno hello stessa procedura descritta nell'articolo di hello [flussi di lavoro di ExpressRoute](expressroute-workflows.md) per provisioning del circuito e lo stato del circuito. Hello che si configurerà quindi hello protocollo BGP (Border Gateway) route toocontrol hello traffico tra rete locale hello e rete virtuale di Azure.

### <a name="connect-toomodel"></a>Toomodel connettersi
In una connessione-tooconfiguration, il cliente già include un tooAzure connessione esistente o avvierà un provider di servizi internet di toohello connessione collegamento ExpressRoute dal Data Center del cliente tooAzure direttamente, anziché il Data Center. processo di provisioning di hello toobegin al cliente verrà procedura hello come descritto in precedenza nel modello hello Connect-Through. Dopo aver stabilito il circuito hello cliente sarà necessario tooconfigure hello locale toobe router in grado di tooaccess la rete e reti virtuali di Azure.

Può contribuire alla configurazione della connessione hello e configurazione hello indirizza risorse hello tooallow in toocommunicate il Data Center con le risorse nel Data Center hello del client o risorse hello ospitate in Azure.

## <a name="expressroute-routing-domains"></a>Domini di routing ExpressRoute
ExpressRoute offre tre domini di routing: peer pubblico, privato e Microsoft. Ognuno dei domini di routing hello vengono configurate con i router identici nella configurazione attivo-attivo per la disponibilità elevata. Per altri dettagli sui domini di routing ExpressRoute, vedere [qui](expressroute-circuit-peerings.md).

È possibile definire le route personalizzate filtri tooallow solo hello itinerario o itinerari interessati tooallow necessità o meno. Per ulteriori informazioni o toosee toomake queste modifiche vedere articolo: [creare e modificare il routing per un circuito ExpressRoute con PowerShell](expressroute-howto-routing-classic.md) per ulteriori informazioni sui filtri di routing.

> [!NOTE]
> Per Microsoft e per il Peering pubblico connettività anche deve essere un indirizzo IP pubblico di proprietà cliente hello o CSP e deve rispettare le regole tooall definito. Per ulteriori informazioni, vedere hello [prerequisiti di ExpressRoute](expressroute-prerequisites.md) pagina.  
> 
> 

## <a name="routing"></a>Routing.
ExpressRoute si connette toohello Azure reti tramite hello Gateway di rete virtuale di Azure. I gateway di rete forniscono il routing per le reti virtuali di Azure.

Creazione di reti virtuali di Azure crea anche una tabella di routing predefinita per il traffico di toodirect hello tra reti virtuali da e verso la subnet hello di rete virtuale hello. Se tabella di route predefinita hello è insufficiente per la soluzione hello personalizzato route possono essere create gli accessori toocustom il traffico in uscita tooroute o tooblock instrada toospecific subnet o reti esterne.

### <a name="default-routing"></a>Routing predefinito
tabella di route predefinita Hello include hello route seguenti:

* Routing in una subnet
* Subnet per subnet all'interno di rete virtuale hello
* toohello Internet
* Da rete virtuale a rete virtuale con un gateway VPN
* Da rete virtuale a rete locale con un gateway VPN o ExpressRoute

![testo alternativo](./media/expressroute-for-cloud-solution-providers/default-routing.png)  

### <a name="user-defined-routing-udr"></a>Routing definito dall'utente
Le route definite dall'utente consentono il controllo di hello del traffico in uscita da hello assegnato subnet tooother subnet nella rete virtuale hello o su uno di hello altri gateway predefiniti (ExpressRoute; internet o VPN). tabella di routing di Hello predefinita del sistema può essere sostituita con una tabella di routing definite dall'utente che sostituisce una tabella di routing predefinita hello con route personalizzate. Con routing definito dall'utente, i clienti possono creare tooappliances route specifiche, ad esempio i firewall o dispositivi di rilevamento delle intrusioni o bloccare l'accesso toospecific subnet dalla subnet hello hosting route definite dall'utente hello. Per una panoramica delle route definite dall'utente, vedere [qui](../virtual-network/virtual-networks-udr-overview.md). 

## <a name="security"></a>Sicurezza
A seconda di quale sia il modello in uso, Connect tooor Connect-Through, il cliente definisce i criteri di sicurezza hello nella loro rete virtuale o fornisce i requisiti dei criteri di sicurezza hello toohello CSP toodefine tootheir le reti virtuali. è possibile definire Hello criteri di sicurezza seguenti:

1. **Isolamento cliente** : hello piattaforma Azure fornisce isolamento cliente archiviando info ID cliente e rete virtuale in un database protetto, ovvero tooencapsulate utilizzato traffico ogni cliente in un tunnel GRE.
2. **Il gruppo di sicurezza (gruppo) di rete** sono regole per la definizione di traffico consentito in e da subnet hello all'interno di reti virtuali in Azure. Per impostazione predefinita, hello NSG contengono blocca il traffico tooblock regole dalla rete virtuale di toohello Internet hello e le regole Consenti per il traffico all'interno di una rete virtuale. Per altre informazioni sui gruppi di sicurezza di rete, vedere [qui](https://azure.microsoft.com/blog/network-security-groups/).
3. **Il tunneling forzato** : si tratta di un'opzione tooredirect internet è associato il traffico proveniente in Azure toobe reindirizzato su hello ExpressRoute connessione toohello nel data center locale. Per altre informazioni su Imponi tunneling, vedere [qui](expressroute-routing.md#advertising-default-routes).  
4. **Crittografia** , anche se circuiti ExpressRoute hello cliente specifico tooa dedicato, è possibile violare il possibilità hello che hello provider di rete, traffico parte di un intruso tooexamine pacchetto. questo rischio, un cliente o CSP crittografare il traffico per tooaddress hello connessione mediante la definizione di criteri in modalità tunnel IPSec per tutto il traffico che si propagano tra hello in risorse locali e le risorse di Azure (vedere toohello facoltativo in modalità Tunnel IPSec per cliente 1 Nella figura 5: sicurezza ExpressRoute sopra). seconda opzione Hello sarebbe toouse appliance firewall in ogni punto di fine hello di hello circuito ExpressRoute. Questo richiederà parti 3rd aggiuntivi firewall installato sia il traffico hello tooencrypt termina tramite il circuito ExpressRoute hello toobe di macchine virtuali o dispositivi.

![testo alternativo](./media/expressroute-for-cloud-solution-providers/expressroute-security.png)  

## <a name="next-steps"></a>Passaggi successivi
Hello servizio Cloud Solution Provider fornisce un tooincrease modo i clienti di valore tooyour senza hello necessario per costosa infrastruttura e dalla capacità gli acquisti, mantenendo la posizione come provider di hello outsourcing primario. Perfetta integrazione con Microsoft Azure può essere eseguita tramite hello CSP API, consentendo toointegrate management di Microsoft Azure all'interno del Framework di gestione esistenti.  

Ulteriori informazioni visitare hello seguenti collegamenti:

[Programma Microsoft Cloud Solution Provider](https://partner.microsoft.com/en-US/Solutions/cloud-reseller-overview).  
[Ottenere pronto tootransact come un Provider di soluzioni Cloud](https://partner.microsoft.com/en-us/solutions/cloud-reseller-pre-launch).  
[Risorse Microsoft Cloud Solution Provider](https://partner.microsoft.com/en-us/solutions/cloud-reseller-resources).

