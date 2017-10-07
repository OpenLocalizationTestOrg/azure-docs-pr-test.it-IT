---
title: Considerazioni su aaaNetworking con un ambiente del servizio App di Azure
description: Viene illustrato il traffico di rete hello ASE e come tooset NSGs e UDRs con il tipo di base
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 955a4d84-94ca-418d-aa79-b57a5eb8cb85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ccompy
ms.openlocfilehash: d4d3000f4d4d75814b1e6d47079d967334eb1a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="networking-considerations-for-an-app-service-environment"></a>Considerazioni sulla rete per un ambiente del servizio app #

## <a name="overview"></a>Panoramica ##

 L'[ambiente del servizio app di Azure][Intro] è una distribuzione di Servizio app di Azure in una subnet nella rete virtuale di Azure (VNet). È possibile distribuire un ambiente del servizio app in due modi:

- **ASE esterno**: espone hello App ASE ospitate su un indirizzo IP accessibile tramite internet. Per altre informazioni, vedere [Create an External ASE][MakeExternalASE] (Creare un ambiente del servizio app esterno).
- **Bilanciamento del carico interno ASE**: espone hello App ASE ospitate su un indirizzo IP all'interno della rete virtuale. endpoint interno Hello è un bilanciamento del carico interno (ILB), motivo per cui è definita ASE un bilanciamento del carico interno. Per altre informazioni, vedere [Create and use an ILB ASE][MakeILBASE] (Creare e usare un ambiente del servizio app ILB).

Esistono ora due versioni dell'ambiente del servizio app: ASEv1 e ASEv2. Per informazioni su ASEv1, vedere [tooApp introduzione dell'ambiente del servizio v1][ASEv1Intro]. Un ambiente ASEv1 può essere distribuito in una rete virtuale classica o di Resource Manager. Un ambiente ASEv2 può essere distribuito solo in una rete virtuale di Resource Manager.

Tutte le chiamate da un ASE che toohello internet lasciare hello rete virtuale tramite un indirizzo VIP assegnato per hello ASE. Hello IP pubblico di questo indirizzo VIP è quindi hello IP di origine per tutte le chiamate da hello ASE che toohello internet. Se le app hello nel ASE tooresources chiamate in una rete virtuale o su una connessione VPN, hello IP di origine è uno dei hello gli indirizzi IP nella subnet hello utilizzato per la base. Poiché hello ASE è all'interno di hello rete virtuale, consente inoltre di accedere alle risorse all'interno di hello rete virtuale senza configurazione aggiuntiva. Se hello rete virtuale è connessa tooyour dalla rete locale, nel ASE inoltre hanno accesso tooresources non esiste. Non è necessario tooconfigure hello ASE o app qualsiasi ulteriormente.

![Ambiente del servizio app esterno][1] 

Se si dispone di un ASE esterno, VIP pubblico hello è inoltre endpoint hello che le app ASE risolvere toofor:

* HTTP/S. 
* FTP/S. 
* Distribuzione Web.
* Debug remoto.

![Ambiente del servizio app con bilanciamento del carico interno][2]

Se si dispone di una base di bilanciamento del carico interno, l'indirizzo IP hello del bilanciamento del carico interno hello è endpoint hello per HTTP/S, FTP/S, distribuzione web e il debug remoto.

porte di accesso app normale Hello sono:

| Uso | Da | Anche|
|----------|---------|-------------|
|  HTTP/HTTPS  | Configurabile dall'utente |  80, 443 |
|  FTP/FTPS    | Configurabile dall'utente |  21, 990, 10001-10020 |
|  Debug remoto in Visual Studio  |  Configurabile dall'utente |  4016, 4018, 4020, 4022 |

Ciò vale se si usa un ambiente del servizio app esterno o con bilanciamento del carico. Se si è su un ASE esterno, si raggiunge tali porte VIP pubblico hello. Se si è su una base di bilanciamento del carico interno, si raggiunge tali porte in hello bilanciamento del carico interno. Se si blocca la porta 443, è possibile che un effetto su alcune funzionalità esposte nel portale di hello. Per altre informazioni, vedere [Dipendenze per il portale](#portaldep).

## <a name="ase-dependencies"></a>Dipendenze dell'ambiente del servizio app ##

Una dipendenza per l'accesso in ingresso dell'ambiente del servizio app è:

| Uso | Da | Anche|
|-----|------|----|
| gestione | Indirizzi di gestione del servizio app | Subnet dell'ambiente del servizio app: 454, 455 |
|  Comunicazione interna dell'ambiente del servizio app | Subnet dell'ambiente del servizio app: tutte le porte | Subnet dell'ambiente del servizio app: tutte le porte
|  Consenti bilanciamento del carico di Azure in ingresso | Servizio di bilanciamento del carico di Azure | Subnet dell'ambiente del servizio app: tutte le porte
|  Indirizzi IP assegnati alle app | Indirizzi assegnati alle app | Subnet dell'ambiente del servizio app: tutte le porte

Hello il traffico in entrata fornisce comandi e il controllo di hello ASE nel monitoraggio toosystem aggiunta. sono elencati gli IP di origine Hello per il traffico in hello [gestione ASE indirizzi] [ ASEManagement] documento. configurazione di sicurezza di rete Hello deve tooallow accesso da tutti gli indirizzi IP sulle porte 454 e 455.

All'interno di subnet hello ASE esistono molte porte utilizzate per la comunicazione di un componente interno e può essere modificata.  Ciò richiede tutte le porte hello in hello ASE subnet toobe accessibile dalla subnet ASE hello. 

Per le comunicazioni tra Bilanciamento carico di Azure hello e porte minime hello subnet ASE hello hello toobe che è necessario aprire sono 454, 455 e 16001. porta 16001 Hello viene utilizzato per mantenere traffico alive tra bilanciamento del carico hello e ASE hello. Se si utilizza un ASE di bilanciamento del carico interno è possibile bloccare il traffico verso il basso toojust hello 454, 455, 16001 porte.  Se si utilizza un ASE esterno è necessario tootake in porte di accesso account hello app normale.  Se si usano indirizzi app assegnata, è necessario tooopen è tooall porte.  Quando l'app specifica tooa viene assegnato un indirizzo, bilanciamento del carico hello utilizzerà le porte che non sono noti in anticipo toosend HTTP e HTTPS traffico toohello ASE.

Se si usano indirizzi IP assegnati app occorre traffico tooallow da hello che subnet di ASE tooyour App toohello assegnare gli indirizzi IP.

Per l'accesso in uscita, un ambiente del servizio app dipende da più sistemi esterni. Tali dipendenze di sistema sono definiti con nomi DNS e non eseguire il mapping di set di indirizzi IP fissato tooa. Di conseguenza, hello ASE richiede l'accesso in uscita dall'hello ASE tooall di subnet IP esterno in una vasta gamma di porte. Un ASE ha hello seguendo le dipendenze in uscita:

| Uso | Da | Anche|
|-----|------|----|
| Archiviazione di Azure | Subnet dell'ambiente del servizio app | table.core.windows.net, blob.core.windows.net, queue.core.windows.net, file.core.windows.net: 80, 443, 445 (445 necessaria solo per ASEv1.) |
| Database SQL di Azure | Subnet dell'ambiente del servizio app | database.windows.net: 1433, 11000-11999, 14000-14999 (per altre informazioni, vedere [Porte successive alla 1433 per ADO.NET 4.5](../../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md))|
| Gestione di Azure | Subnet dell'ambiente del servizio app | management.core.windows.net, management.azure.com: 443 
| Verifica dei certificati SSL |  Subnet dell'ambiente del servizio app            |  ocsp.msocsp.com, mscrl.microsoft.com, crl.microsoft.com: 443
| Azure Active Directory        | Subnet dell'ambiente del servizio app            |  Internet: 443
| Gestione del servizio app        | Subnet dell'ambiente del servizio app            |  Internet: 443
| DNS di Azure                     | Subnet dell'ambiente del servizio app            |  Internet: 53
| Comunicazione interna dell'ambiente del servizio app    | Subnet dell'ambiente del servizio app: tutte le porte |  Subnet dell'ambiente del servizio app: tutte le porte

Se hello ASE perde l'accesso dipendenze toothese, non funziona. Quando ciò si verifica tempo sufficiente, hello ASE viene sospesa.

### <a name="customer-dns"></a>DNS del cliente ###

Se hello rete virtuale è configurata con un server DNS definito dall'utente, i carichi di lavoro tenant hello utilizzarlo. Hello ASE deve comunque toocommunicate con DNS di Azure per scopi di gestione. 

Se hello rete virtuale è configurata con un cliente DNS sul server DNS hello deve essere raggiungibile dalla subnet hello contenente hello ASE hello altro lato di una rete VPN.

<a name="portaldep"></a>

## <a name="portal-dependencies"></a>Dipendenze per il portale ##

Dipendenze funzionali toohello ASE di addizione, esistono alcuni esperienza del portale correlato toohello elementi aggiuntivi. Alcune delle funzionalità di hello di hello portale di Azure dipendono site_ too_SCM accesso diretto. Per ogni app nel Servizio app di Azure esistono due URL. primo URL Hello è tooaccess l'app. secondo URL Hello è tooaccess hello SCM sito, denominato anche hello _console Kudu_. Le funzionalità che utilizzano il sito di Gestione controllo servizi hello includono:

-   Processi Web
-   Funzioni
-   Streaming dei log
-   Kudu
-   Estensioni
-   Esplora processi
-   Console

Quando si utilizza un ASE ILB, sito SCM hello non è accessibile dall'esterno hello rete virtuale di internet. Quando l'app è ospitato in una base di bilanciamento del carico interno, alcune funzionalità non funzionerà dal portale hello.  

Molte di tali funzionalità che dipendono dal sito SCM hello sono disponibili anche direttamente nella console Kudu hello. È possibile connettersi tooit direttamente anziché tramite il portale di hello. Se l'app è ospitato in una base di bilanciamento del carico interno, utilizzare la pubblicazione toosign credenziali in. sito Hello URL tooaccess hello SCM di un'applicazione ospitata in una base di bilanciamento del carico interno è hello seguente formato: 

```
<appname>.scm.<domain name hello ILB ASE was created with> 
```

Se la base di bilanciamento del carico interno è il nome di dominio di hello *contoso.net* e il nome dell'app è *testapp*, app hello viene raggiunto in *testapp.contoso.net*. sito SCM Hello nella relativa viene raggiunto in *testapp.scm.contoso.net*.

### <a name="functions-and-web-jobs"></a>Funzioni e processi Web ###

Funzioni sia Web i processi dipendono hello SCM sito ma sono supportati per l'utilizzo nel portale di hello, anche se le app ASE un bilanciamento del carico interno, purché il browser può raggiungere sito SCM hello.  Se si utilizza un certificato autofirmato con ASE il bilanciamento del carico interno, è necessario tooenable il tootrust browser che del certificato.  Per Internet Explorer e bordo che indica che il certificato di hello dispone toobe in condizioni di attendibilità computer hello di archivio.  Se si utilizza Chrome, che significa che certificato hello nel browser hello è accettato in precedenza selezionando presumibilmente sito scm hello direttamente.  la soluzione migliore Hello è toouse un certificato commerciale nella catena di browser hello di trust.  

## <a name="ase-ip-addresses"></a>Indirizzi IP dell'ambiente del servizio app ##

Un ASE ha qualche toobe di indirizzi IP comunicata. Sono:

- **Indirizzo IP in ingresso pubblico**: usato per il traffico di app in un ambiente del servizio app esterno e per il traffico di gestione sia per un ambiente del servizio app esterno che con bilanciamento del carico interno.
- **Indirizzo IP pubblico in uscita**: utilizzato come hello "da" IP per le connessioni in uscita da hello ASE tale hello lasciare rete virtuale, che non vengono instradati verso il basso di una connessione VPN.
- **Indirizzo IP con bilanciamento del carico interno**: se si usa un ambiente del servizio app con bilanciamento del carico interno.
- **Indirizzi SSL basati su IP assegnati alle app**: possibili solo con un ambiente del servizio app esterno e quando è configurato SSL basato su IP.

Tutti questi indirizzi IP sono facilmente visibili in un ASEv2 nel portale di Azure hello dall'interfaccia utente di ASE hello. Se si dispone di una base di bilanciamento del carico interno, viene elencato IP hello per hello bilanciamento del carico interno.

![Indirizzi IP][3]

### <a name="app-assigned-ip-addresses"></a>Indirizzi IP assegnati alle app ###

Con un ASE esterno, è possibile assegnare gli indirizzi IP tooindividual app. Ciò non è possibile con un ambiente del servizio app con bilanciamento del carico interno. Per ulteriori informazioni su come tooconfigure toohave l'app proprio indirizzo IP, vedere [associare un esistente SSL certificato tooAzure web App personalizzate](../../app-service-web/app-service-web-tutorial-custom-ssl.md).

Quando un'applicazione ha il proprio indirizzo SSL basato su IP, hello ASE riserva due porte toomap toothat l'indirizzo IP. Una porta è per il traffico HTTP, e hello altri porta per HTTPS. Tali porte sono elencate nell'interfaccia utente di base nella sezione di indirizzi IP hello hello. Il traffico deve essere in grado di tooreach tali porte da VIP hello o App hello sono inaccessibili. Questo requisito è importante tooremember quando si configura rete sicurezza gruppi.

## <a name="network-security-groups"></a>Gruppi di sicurezza di rete ##

[Gruppi di sicurezza di rete] [ NSGs] forniscono l'accesso alla rete di hello possibilità toocontrol all'interno di una rete virtuale. Quando si usa il portale di hello, è implicita regola Nega a toodeny priorità più bassa hello tutti gli elementi. Quello che è necessario creare sono le regole di autorizzazione.

In un tipo di base, non è necessario accesso toohello macchine virtuali utilizzate toohost hello ASE stesso. Tali macchine virtuali si trovano in una sottoscrizione gestita da Microsoft. Se si desidera toorestrict accesso toohello App hello ASE, impostare NSGs nella subnet ASE hello. In questo modo, prestare particolare attenzione dipendenze ASE toohello. Se si bloccano tutte le dipendenze, hello ASE smette di funzionare.

NSGs può essere configurato tramite hello portale di Azure o PowerShell. informazioni di Hello riportate di seguito viene illustrato hello portale di Azure. Per creare e gestire NSGs nel portale di hello come una risorsa di primo livello sotto **rete**.

Quando i requisiti in ingresso e in uscita hello vengono presi in considerazione, hello NSGs dovrebbe essere simile NSGs toohello illustrato in questo esempio. intervallo di indirizzi di rete virtuale Hello è _192.168.250.0/16_, senza che sia hello subnet ASE hello in _192.168.251.128/25_.

nella parte superiore di hello dell'elenco di hello in questo esempio vengono illustrati i requisiti in ingresso primi due Hello per toofunction ASE hello. Essi abilitare la gestione di ASE e consentire hello ASE toocommunicate con se stesso. Hello altre voci sono tutti i tenant configurabile e può essere regolato rete accesso toohello ASE hosting delle applicazioni. 

![Regole di sicurezza in ingresso][4]

Una regola predefinita consente hello gli indirizzi IP nella subnet di ASE toohello tootalk rete virtuale hello. Un'altra regola predefinita consente di bilanciamento del carico di hello, noto anche come VIP pubblico hello, toocommunicate con hello ASE. Selezionare le regole predefinite di hello toosee, **regole predefinite** toohello Avanti **Aggiungi** icona. Se si inserisce un'istruzione deny tutte le altre regole dopo hello NSG regole illustrato, impedire il traffico tra l'indirizzo VIP hello e ASE hello. tooprevent traffico proveniente da aggiungere all'interno di rete virtuale, hello tooallow la propria regola in ingresso. Utilizzare un tooAzureLoadBalancer uguale origine con una destinazione di **qualsiasi** e un intervallo di porte di  **\*** . Poiché regola gruppo hello è applicato toohello ASE subnet, è necessario toobe specifiche nella destinazione hello.

Se è stato assegnato una app tooyour di indirizzo IP, accertarsi di mantenere hello porte aperte. Selezionare le porte, hello toosee **ambiente del servizio App** > **gli indirizzi IP**.  

Tutti gli elementi di hello mostrati in hello segue le regole in uscita sono necessarie, tranne l'ultimo elemento hello. Che consentono accesso toohello ASE dipendenze della rete che sono stata rilevate più indietro in questo articolo. Se si bloccano una o più di queste voci, l'ambiente del servizio app smette di funzionare. Hello ultimo elemento hello elenco consente la toocommunicate ASE con altre risorse in una rete virtuale.

![Regole di sicurezza in uscita][5]

Dopo aver definito i NSGs, assegnare loro toohello subnet che si trova il ASE su. Se non si ricorda hello rete virtuale di base o una subnet, è possibile visualizzarlo dal portale di gestione ASE hello. tooassign hello subnet tooyour NSG passare toohello subnet dell'interfaccia utente e selezionare hello gruppo.

## <a name="routes"></a>Route ##

Le route diventano problematiche più di frequente quando si configura la rete virtuale con Azure ExpressRoute. Esistono tre tipi di route in una rete virtuale:

-   Route di sistema
-   Route BGP
-   Route definite dall'utente

Le route BGP sono prioritarie rispetto alle route di sistema. Le route definite dall'utente sono prioritarie rispetto alle route BGP. Per altre informazioni sulle route nelle reti virtuali di Azure, vedere [Panoramica delle route definite dall'utente][UDRs].

database SQL di Azure Hello ASE hello viene utilizzato il sistema di hello toomanage è presente un firewall. Comunicazione toooriginate da hello VIP pubblico ASE richiede. Database SQL toohello connessioni da hello ASE verrà negato se vengono inviati verso il basso hello connessione ExpressRoute e un altro indirizzo IP.

Se l'invio delle richieste di gestione di risposte tooincoming verso il basso hello ExpressRoute, indirizzo di risposta hello è diverso da quello di destinazione originale hello. Questa mancata corrispondenza interrompe la comunicazione TCP hello.

Per i toowork ASE mentre la rete virtuale è configurata con ExpressRoute, toodo cosa più semplice hello è:

-   Configurare ExpressRoute tooadvertise _0.0.0.0/0_. Per impostazione predefinita, tutto il traffico locale in uscita viene forzato.
-   Creare una route definita dall'utente. Applicarlo subnet toohello contenente hello ASE con un prefisso dell'indirizzo _0.0.0.0/0_ e tipo di hop di un successivo _Internet_.

Se si apportano queste due modifiche, il traffico destinato a internet proveniente dalla subnet ASE hello non è forzato ExpressRoute hello e hello ASE works. 

> [!IMPORTANT]
> route Hello definite in un UDR devono essere sufficientemente specifica tootake precedenza su qualsiasi route annunciate dalla configurazione di ExpressRoute hello. Hello esempio precedente Usa intervallo di indirizzi hello ampie 0.0.0.0/0. Può essere accidentalmente sostituito dagli annunci di route che usano intervalli di indirizzi più specifici.
>
> ASEs non sono supportate con ExpressRoute configurazioni cross-annunciano le route da hello peering pubblico toohello peering privato percorso. Le configurazioni di ExpressRoute con peering pubblico configurato riceveranno gli annunci di route da Microsoft. gli annunci Hello contengono un elevato numero di intervalli di indirizzi IP di Microsoft Azure. Se gli intervalli di indirizzi hello tra annunciati nel percorso di peering privato hello, tutti i pacchetti di rete in uscita dalla subnet hello del ASE sono infrastruttura di rete locale del cliente tooa tunneling forzato. Questo flusso di rete non è attualmente supportato con ambienti del servizio app. Un problema di toothis soluzione è toostop le route tra annunci hello peering pubblico toohello peering privato percorso.

toocreate un UDR, seguire questi passaggi:

1. Passare toohello portale di Azure. Selezionare **Rete** > **Tabelle route**.

2. Creare una nuova tabella di route in hello stessa regione della rete virtuale.

3. Dall'interfaccia utente per le tabelle route selezionare **Route** > **Aggiungi**.

4. Set hello **tipo dell'hop successivo** troppo**Internet** hello e **prefisso dell'indirizzo** troppo**0.0.0.0/0**. Selezionare **Salva**.

    Quindi possibile vedere simile alla seguente hello:

    ![Route funzionali][6]

5. Dopo aver creato una nuova tabella di routing hello, andare subnet toohello che contiene il tipo di base. Selezionare la tabella di routing hello elenco nel portale di hello. Dopo aver salvato la modifica hello, dovrebbe quindi NSGs hello e le route indicate con la subnet.

    ![Gruppi di sicurezza di rete e route][7]

### <a name="deploy-into-existing-azure-virtual-networks-that-are-integrated-with-expressroute"></a>Distribuzione nelle reti virtuali di Azure esistenti integrate con ExpressRoute ###

toodeploy il ASE in una rete virtuale che si integra con ExpressRoute, preconfigurare subnet hello in cui si desidera ASE hello distribuito. Utilizzare quindi un toodeploy modello di gestione risorse è. toocreate un ASE in una rete virtuale è già configurato ExpressRoute:

- Creare un hello toohost subnet ASE.

    > [!NOTE]
    > Nessun altro elemento può essere nella subnet hello ma ASE hello. Essere toochoose che uno spazio di indirizzi che consente la crescita futura. Non è possibile modificare questa impostazione in un secondo momento. È consigliabile una dimensione pari a `/25` con 128 indirizzi.

- Creare UDRs (ad esempio, le tabelle di route) come descritto in precedenza e impostarlo su subnet hello.
- Creare hello ASE utilizzando un modello di gestione delle risorse, come descritto in [creare un ASE utilizzando un modello di gestione risorse][MakeASEfromTemplate].

<!--Image references-->
[1]: ./media/network_considerations_with_an_app_service_environment/networkase-overflow.png
[2]: ./media/network_considerations_with_an_app_service_environment/networkase-overflow2.png
[3]: ./media/network_considerations_with_an_app_service_environment/networkase-ipaddresses.png
[4]: ./media/network_considerations_with_an_app_service_environment/networkase-inboundnsg.png
[5]: ./media/network_considerations_with_an_app_service_environment/networkase-outboundnsg.png
[6]: ./media/network_considerations_with_an_app_service_environment/networkase-udr.png
[7]: ./media/network_considerations_with_an_app_service_environment/networkase-subnet.png

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[ASEManagement]: ./management-addresses.md
