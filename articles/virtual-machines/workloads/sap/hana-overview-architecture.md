---
title: aaaOverview e architettura di SAP HANA in Azure (istanze di grandi dimensioni) | Documenti Microsoft
description: Panoramica dell'architettura della procedura tooDeploy SAP HANA in Azure (istanze di grandi dimensioni).
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
ms.openlocfilehash: e3ee6864af37ac322635eaef43e3c20101e3a769
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-overview-and-architecture-on-azure"></a>Panoramica e architettura di SAP HANA (istanze Large) in Azure

## <a name="what-is-sap-hana-on-azure-large-instances"></a>SAP HANA in Azure (istanze Large)

SAP HANA in Azure (istanza di grandi dimensioni) è una soluzione unica di tooAzure. Inoltre tooproviding macchine virtuali di Azure a scopo di hello distribuzione ed esecuzione di SAP HANA, Azure offre hello toorun possibilità e la distribuzione di SAP HANA su server bare metal tooyou dedicato come un cliente. Hello SAP HANA in soluzioni di Azure (istanze di grandi dimensioni) si basa su hardware bare metal di server/host non condivisi assegnato tooyou come un cliente. hardware del server Hello è incorporato nella maggiori timbri contenenti compute/server, rete e infrastruttura di archiviazione. Questa combinazione ha la certificazione HANA TDI. offerta di servizio Hello di SAP HANA in Azure (istanze di grandi dimensioni) offre vari SKU di server diverso o dimensioni, a partire da unità che dispongono di 72 CPU e 768 GB memoria toounits aventi 960 CPU e memoria di 20 TB.

isolamento di cliente Hello all'interno di timbro infrastruttura hello viene eseguita nel tenant, che in dettaglio il seguente aspetto:

- Rete: isolamento dei clienti nello stack dell'infrastruttura tramite rete virtuali per ogni tenant assegnato al cliente. Un tenant viene assegnato tooa singolo cliente. Un cliente può avere più tenant. isolamento rete Hello di tenant impedisce la comunicazione di rete tra i tenant nel livello di hello infrastruttura timbro. Anche se i tenant appartengono toohello stesso cliente.
- Componenti di archiviazione: isolamento tramite macchine virtuali di archiviazione che abbiano volumi di archiviazione assegnato tooit. Volumi di archiviazione possono essere assegnati solo macchina di virtuale archiviazione tooone. Una macchina virtuale di archiviazione viene assegnata in modo esclusivo tooone single-tenant nello stack di certificati di infrastruttura di SAP HANA TDI hello. Di conseguenza i volumi di archiviazione assegnati macchina virtuale di archiviazione tooa accessibili in uno specifico e correlati tenant solo. E non sono visibili tra tenant distribuito diversi hello.
- Server o host: un'unità server o host non viene condivisa tra clienti o tenant. Un host o server distribuite tooa cliente, è un'unità atomica bare metal calcolo assegnato tooone single-tenant. **Non** vengono usati partizionamenti hardware o software con i quali un cliente potrebbe ritrovarsi a condividere un host o un server con un altro cliente. Volumi di archiviazione assegnati toohello archiviazione macchina virtuale tenant specifico hello sono montati toosuch un server. Un tenant può disporre di una unità di server toomany di SKU diverse assegnata in modo esclusivo.
- All'interno di un SAP HANA del timbro dell'infrastruttura di Azure (istanza di grandi dimensioni), molti tenant diversi vengono distribuiti e isolamento rispetto a altro tramite i concetti di hello tenant a livello di rete, archiviazione e calcolo. 


Queste unità server bare metal sono toorun supportati SAP HANA solo. livello di applicazione SAP Hello o middleware del carico di lavoro è in esecuzione in macchine virtuali di Microsoft Azure. indicatori di infrastruttura Hello in esecuzione hello SAP HANA in Azure (istanza di grandi dimensioni) unità sono connessi toohello rete Azure backbone, in tal caso, la connettività a bassa latenza tra SAP HANA in unità di Azure (istanza di grandi dimensioni) e macchine virtuali di Azure fornito.

Questo documento è uno dei cinque documenti, che riguardano l'argomento hello di SAP HANA in Azure (istanza di grandi dimensioni). In questo documento, passiamo attraverso l'architettura di base hello, responsabilità, i servizi forniti e su un alto livello tramite le funzionalità della soluzione hello. La maggior parte delle aree di hello, ad esempio rete e connettività, hello altri quattro documenti sono relativi dettagli e drill-down. documentazione di Hello di SAP HANA in Azure (istanza di grandi dimensioni) non copre gli aspetti dell'installazione di SAP NetWeaver o le distribuzioni di SAP NetWeaver in macchine virtuali di Azure. Questo argomento viene descritto nella documentazione separata nell'hello stesso contenitore di documentazione. 


Hello composto da cinque parti di questa guida illustra hello seguenti argomenti:

- [Panoramica e architettura di SAP HANA (istanze di grandi dimensioni) in Azure](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Infrastruttura e connettività a SAP HANA (istanze di grandi dimensioni) in Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Come tooinstall e configurare SAP HANA (istanze di grandi dimensioni) in Azure](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Disponibilità elevata e ripristino di emergenza di SAP HANA (istanze di grandi dimensioni) in Azure](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Risoluzione dei problemi e monitoraggio di SAP HANA in Azure (istanze di grandi dimensioni)](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="definitions"></a>Definizioni

Molte definizioni comuni vengono ampiamente utilizzate in hello architettura e Guida alla distribuzione di documentazione tecnica. Hello nota seguenti termini e i relativi significati:

- **IaaS:** (Infrastructure as a Service) infrastruttura distribuita come servizio
- **PaaS:** (Platform as a Service) piattaforma distribuita come servizio
- **SaaS:** (Software as a Service) software come servizio
- **Componente SAP:** singola applicazione SAP, ad esempio ECC, BW, Solution Manager o EP. I componenti SAP possono essere basati su tecnologie ABAP o Java tradizionali o su un'applicazione non basata su NetWeaver, ad esempio Business Objects.
- **Ambiente SAP:** uno o più componenti SAP raggruppati logicamente tooperform una funzione di business, ad esempio Development, QAS, Training, ripristino di emergenza o di produzione.
- **Landscape SAP:** fa riferimento toohello le intera risorse SAP nel landscape IT. Hello landscape SAP include tutti di produzione e ambienti non di produzione.
- **Il sistema SAP:** hello combinazione del livello DBMS e applicazione di un sistema di sviluppo ERP SAP, sistema di test BW SAP, sistema di produzione CRM SAP e così via. Le distribuzioni di Azure non supportano la divisione di questi due livelli tra l'istanza locale e Azure. Un sistema SAP deve quindi essere distribuito o in locale o in Azure. Tuttavia, è possibile distribuire i sistemi diversi di hello di un landscape SAP in Azure o in locale. Ad esempio, è possibile distribuire i sistemi hello CRM SAP sviluppo e test in Azure, durante la distribuzione hello CRM SAP produzione sistema locale. SAP HANA in Azure (istanze di grandi dimensioni), è destinata di host di livello dell'applicazione SAP hello dei sistemi SAP in macchine virtuali di Azure e istanza di SAP HANA correlati in un'unità nell'indicatore dell'istanza di grandi dimensioni HANA hello hello.
- **Indicatore di istanza di grandi dimensioni:** uno stack infrastruttura hardware SAP HANA TDI certificate e dedicati toorun le istanze di SAP HANA in Azure.
- **SAP HANA in Azure (istanze di grandi dimensioni):** nome ufficiale per l'offerta di hello in Azure toorun HANA istanze in SAP HANA TDI Certificate hardware che viene distribuito in timbri di istanza di grandi dimensioni in diverse aree di Azure. Hello correlati termine **istanza grande HANA** è l'abbreviazione di SAP HANA in Azure (istanze di grandi dimensioni) e viene ampiamente utilizzata questa Guida alla distribuzione tecnica.
- **Cross-premise:** viene descritto uno scenario in cui le macchine virtuali sono distribuite tooan sottoscrizione di Azure con site-to-site, multi-sito o ExpressRoute connettività tra Data Center locale hello e Azure. Nella documentazione comune su Azure questi tipi di distribuzioni vengono definiti anche scenari cross-premise. motivo Hello connessione hello è tooextend domini locali, Active Directory/OpenLDAP on-premise e DNS in locale in Azure. Hello locale orizzontale è estesa toohello risorse di Azure di hello sottoscrizioni di Azure. Grazie a questa estensione, hello macchine virtuali può far parte del dominio locale hello. Gli utenti di dominio del dominio locale hello possono accedere ai server hello ed eseguire servizi su tali macchine virtuali (ad esempio servizi DBMS). La comunicazione e la risoluzione dei nomi tra VM distribuite in locale e VM distribuite in Azure sono consentite. Ad esempio è uno scenario tipico di hello in quali SAP la maggior parte delle attività vengono distribuiti. Vedere le guide di hello di [pianificazione e progettazione per il Gateway VPN](../../../vpn-gateway/vpn-gateway-plan-design.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) e [creare una rete virtuale con una connessione da sito a sito usando il portale di Azure hello](../../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per informazioni più dettagliate.
- **Tenant:** un cliente distribuito nello stamp di istanze Large di HANA viene isolato in un "tenant". Un tenant è isolato in rete hello, archiviazione e il livello di calcolo di altri tenant. In tal caso, tale unità di archiviazione e calcolo toohello assegnati diversi tenant non è possibile comunicare o comunicare tra loro in hello istanza grande HANA timestamp livello. Un cliente può scegliere distribuzioni toohave in diversi tenant. Anche in questo caso, non avviene alcuna comunicazione tra i tenant nel livello di istanza grande HANA timbro hello.

Sono disponibili un'ampia gamma di risorse aggiuntive che sono state pubblicate su un argomento hello della distribuzione del carico di lavoro SAP nel cloud pubblico di Microsoft Azure. È consigliabile che tutti gli utenti di pianificazione e l'esecuzione di una distribuzione di SAP HANA in Azure sia esperti e tenere in considerazione entità hello di IaaS di Azure e distribuzione hello dei carichi di lavoro SAP in Azure IaaS. Hello risorse seguenti forniscono ulteriori informazioni e prima di continuare è necessario fare riferimento:


- [Uso di soluzioni SAP nelle macchine virtuali di Microsoft Azure](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="certification"></a>Certificazione

Oltre alle hello certificazione NetWeaver, SAP richiede una certificazione speciale per SAP HANA toosupport SAP HANA in determinate infrastrutture, ad esempio IaaS di Azure.

core Hello nota SAP NetWeaver e grado tooa certificazione SAP HANA, è [SAP nota #1928533-applicazioni SAP in Azure: tipi di prodotti supportati e macchina virtuale di Azure](https://launchpad.support.sap.com/#/notes/1928533).

Anche [SAP Note #2316233 - SAP HANA on Microsoft Azure (Large Instances)](https://launchpad.support.sap.com/#/notes/2316233/E) (Nota di supporto SAP 2316233 - SAP HANA in Microsoft Azure (istanze di grandi dimensioni)) rappresenta uno strumento utile. Vengono illustrate soluzioni hello descritti in questa Guida. Sono inoltre supportati toorun SAP HANA in tipo di hello GS5 VM di Azure. [Le informazioni in questo caso sono pubblicate nel sito Web SAP hello](http://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html).

Hello SAP HANA in soluzioni di Azure (istanze di grandi dimensioni) di cui tooin SAP nota #2316233 offre a Microsoft e i clienti SAP hello possibilità toodeploy grandi SAP Business Suite, SAP Business Warehouse (BW), HANA S/4, BW/4HANA o altri carichi di lavoro di SAP HANA in Azure. soluzione hello è basato su hello certificata timbro hardware dedicato a SAP HANA ([SAP HANA adattato Datacenter integrazione-TDI](https://scn.sap.com/docs/DOC-63140)). In esecuzione come un TDI di SAP HANA soluzione configurata consente con certezza hello di sapere che tutte le applicazioni basate su SAP HANA (compresi SAP Business Suite in SAP HANA, SAP Business Warehouse (BW) in SAP HANA, S4/HANA e BW4/HANA) sono toowork in corso hello infrastruttura hardware.

Toorunning confrontati SAP HANA in macchine virtuali di Azure questa soluzione offre un vantaggio: consente di molto più grandi volumi di memoria. Se si desidera tooenable questa soluzione, esistono alcuni toounderstand gli aspetti chiave:

- livello dell'applicazione SAP Hello e non SAP applicazioni eseguiti in macchine virtuali di Azure (VM) che sono ospitati in timbri di hello consuete hardware di Azure.
- Cliente infrastruttura locale, data center, e le distribuzioni di applicazioni sono piattaforma cloud di Microsoft Azure toohello connesso tramite Azure ExpressRoute (scelta consigliata) o rete privata virtuale (VPN, Virtual Private Network). Active Directory (AD) e DNS vengono estesi anche in Azure.
- istanza del database SAP HANA Hello per carico di lavoro HANA viene eseguito in SAP HANA in Azure (istanze di grandi dimensioni). indicatore dell'istanza di grandi dimensioni Hello è connesso in rete di Azure, allo scopo di interagisce con istanza HANA hello in esecuzione nelle istanze di grandi dimensioni HANA software in esecuzione in macchine virtuali di Azure.
- L'hardware di SAP HANA in Azure (istanze di grandi dimensioni) è dedicato e viene fornito in un'infrastruttura distribuita come servizio (IaaS) con SUSE Linux Enterprise Server o Red Hat Enterprise Linux preinstallato. Come con macchine virtuali di Azure, ulteriormente gli aggiornamenti e manutenzione del sistema operativo toohello è responsabilità dell'utente.
- Installazione di HANA o eventuali componenti aggiuntivi necessari toorun SAP HANA in unità di istanze di grandi dimensioni HANA è responsabilità dell'utente, così come tutte le rispettive operazioni in corso e amministrazioni di SAP HANA in Azure.
- Inoltre toohello soluzioni descritte di seguito, è possibile installare altri componenti nella sottoscrizione di Azure che si connette tooSAP HANA in Azure (istanze di grandi dimensioni).  Ad esempio, i componenti che consentono la comunicazione con e/o direttamente database SAP HANA toohello (server di salto, RDP server SAP HANA Studio SAP Data Services per gli scenari SAP BI, o soluzioni di monitoraggio di rete).
- Come in Azure, le istanze Large di HANA offrono il supporto di funzionalità di disponibilità elevata e ripristino di emergenza.

## <a name="architecture"></a>Architettura

A livello generale, hello SAP HANA in soluzioni di Azure (istanze di grandi dimensioni) è livello dell'applicazione SAP hello che risiedono in macchine virtuali di Azure e hello il livello di database che risiede nell'hardware TDI SAP configurato che si trova in un indicatore dell'istanza di grandi dimensioni in hello stessa regione di Azure che è connesso tooAzure IaaS.

> [!NOTE]
> È necessario a livello dell'applicazione SAP hello toodeploy in hello stessa regione di Azure come livello DBMS di SAP hello. Questa regola è ben documentata nelle informazioni pubblicate relative al carico di lavoro SAP in Azure. 

Hello architettura complessiva di SAP HANA in Azure (istanze di grandi dimensioni) fornisce una configurazione di hardware certificato SAP TDI (non virtualizzato, bare metal, il server ad alte prestazioni per il database SAP HANA hello) e il possibilità hello e la flessibilità di Azure tooscale risorse per hello SAP toomeet di livello applicazione alle esigenze.

![Panoramica dell'architettura di SAP HANA in Azure (istanze di grandi dimensioni)](./media/hana-overview-architecture/image1-architecture.png)

architettura di Hello illustrata è suddivisa in tre sezioni:

- **A destra:** un'infrastruttura locale che esegue diverse applicazioni nei data center con gli utenti finali che accedono ad applicazioni line-of-business, ad esempio SAP. In teoria, questo on-premise infrastruttura viene quindi connesso tooAzure con Azure [ExpressRoute](https://azure.microsoft.com/services/expressroute/).

- **Center:** Mostra IaaS di Azure e, in questo caso, l'utilizzo di macchine virtuali di Azure toohost SAP o altre applicazioni che utilizzano SAP HANA come un sistema DBMS. Istanze di dimensioni inferiori HANA che forniscono una funzione con memoria hello macchine virtuali di Azure vengono distribuite nelle macchine virtuali di Azure con il livello di applicazione. Informazioni sulle [macchine virtuali](https://azure.microsoft.com/services/virtual-machines/).
<br />Rete di Azure è il sistema SAP toogroup utilizzato insieme alle altre applicazioni in reti virtuali di Azure (Vnet). Queste reti virtuali connettono i sistemi locali tooon nonché tooSAP HANA in Azure (istanze di grandi dimensioni).
<br />Per le applicazioni SAP NetWeaver e i database che sono supportate toorun in Microsoft Azure, vedere [SAP supporto nota #1928533-applicazioni SAP in Azure: tipi di prodotti supportati e macchina virtuale di Azure](https://launchpad.support.sap.com/#/notes/1928533). Per la documentazione sulla distribuzione di soluzioni SAP in Azure, vedere:

  -  [Uso di SAP in macchine virtuali (VM) Windows](../../virtual-machines-windows-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
  -  [Uso di soluzioni SAP nelle macchine virtuali di Microsoft Azure](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

- **Left:** Mostra hello SAP HANA TDI nell'indicatore dell'istanza di grandi dimensioni di Azure hello hardware certificato. unità di istanza di grandi dimensioni HANA Hello sono connesso toohello reti virtuali di Azure della sottoscrizione tramite hello stessa tecnologia di connettività hello da locale ad Azure.

indicatore dell'istanza di grandi dimensioni di Azure Hello stesso combina hello seguenti componenti:

- **Elaborazione:** server basati su processori Intel Xeon E7-8890v3 o Intel Xeon E7-8890v4 che forniscono funzionalità di elaborazione necessario hello e sono certificate di SAP HANA.
- **Rete:** A unificata dell'infrastruttura di rete ad alta velocità che collega hello elaborazione, archiviazione e i componenti di rete LAN.
- **Archiviazione:** un'infrastruttura di archiviazione a cui si accede tramite un'infrastruttura di rete unificata. Capacità di archiviazione specifico viene fornito a seconda di hello specifico SAP HANA, sulla configurazione di Azure (istanze di grandi dimensioni) da distribuire (ulteriori capacità di archiviazione è disponibile un costo mensile aggiuntivo).

All'interno di infrastruttura di multi-tenant hello dell'indicatore dell'istanza di grandi dimensioni hello, i clienti vengono distribuiti come tenant isolate. In fase di distribuzione del tenant di hello, è necessario tooname una sottoscrizione di Azure all'interno della registrazione di Azure. Questo hello toobe corso sottoscrizione di Azure, hello HANA delle istanze di grandi dimensioni verrà fatturata a fronte di toobe. Questi tenant ha una sottoscrizione di Azure di toohello relazione 1:1. Rete buona norma che è possibile tooaccess un'unità istanza grande HANA distribuito in un tenant in un'area di Azure da diverse reti virtuali di Azure, che appartiene toodifferent le sottoscrizioni di Azure. Anche le sottoscrizioni di Azure è necessario toobelong toohello registrazione Azure stesso. 

Analogamente alle VM di Azure, SAP HANA in Azure (istanze di grandi dimensioni) è disponibile in più aree di Azure. Le funzionalità di ripristino di emergenza toooffer ordine, è possibile scegliere tooopt in. Timbri di istanza di grandi dimensioni differenti all'interno di un'area geografica politica sono connessi tooeach altri. Ad esempio, HANA timbri istanza di grandi dimensioni in Stati Uniti occidentali e Stati Uniti orientali connessi tramite un collegamento di rete dedicata a scopo di hello della replica di ripristino di emergenza. 

Così come è possibile scegliere tra diversi tipi di VM con Macchine virtuali di Azure, è possibile scegliere tra diverse SKU delle istanze HANA di grandi dimensioni personalizzate per tipi diversi di carichi di lavoro di SAP HANA. SAP applica rapporti socket tooprocessor di memoria per diversi carichi di lavoro in base alle generazioni di processori Intel hello, sono disponibili quattro diversi tipi SKU disponibili:

A partire da luglio 2017, SAP HANA in Azure (istanze di grandi dimensioni) è disponibile in diverse configurazioni in Europa settentrionale e Stati Uniti orientali, Australia orientale, Australia sudorientale, Europa occidentale e hello Azure aree di Stati Uniti occidentali:

| Soluzione SAP | CPU | Memoria | Archiviazione | Disponibilità |
| --- | --- | --- | --- | --- |
| Ottimizzata per OLAP: SAP BW, BW/4HANA<br /> o SAP HANA per carico di lavoro OLAP generico | SAP HANA in Azure S72<br /> – 2 x processore Intel® Xeon® E7-8890 v3<br /> 36 core CPU e 72 thread CPU |  768 GB |  3 TB | Disponibile |
| --- | SAP HANA in Azure S144<br /> – 4 x processore Intel® Xeon® E7-8890 v3<br /> 72 core CPU e 144 thread CPU |  1,5 TB |  6 TB | Non più disponibile |
| --- | SAP HANA in Azure S192<br /> – 4 x processore Intel® Xeon® E7-8890 v4<br /> 96 core CPU e 192 thread CPU |  2 TB |  8 TB | Disponibile |
| --- | SAP HANA in Azure S384<br /> – 8 x processore Intel® Xeon® E7-8890 v4<br /> 192 core CPU e 384 thread CPU |  4 TB |  16 TB | TooOrder pronto |
| Ottimizzata per OLTP: SAP Business Suite<br /> in SAP HANA o S/4HANA (OLTP),<br /> OLTP generico | SAP HANA in Azure S72m<br /> – 2 x processore Intel® Xeon® E7-8890 v3<br /> 36 core CPU e 72 thread CPU |  1,5 TB |  6 TB | Disponibile |
|---| SAP HANA in Azure S144m<br /> – 4 x processore Intel® Xeon® E7-8890 v3<br /> 72 core CPU e 144 thread CPU |  3 TB |  12 TB | Non più disponibile |
|---| SAP HANA in Azure S192m<br /> – 4 x processore Intel® Xeon® E7-8890 v4<br /> 96 core CPU e 192 thread CPU  |  4 TB |  16 TB | Disponibile |
|---| SAP HANA in Azure S384m<br /> – 8 x processore Intel® Xeon® E7-8890 v4<br /> 192 core CPU e 384 thread CPU |  6 TB |  18 TB | TooOrder pronto |
|---| SAP HANA in Azure S384xm<br /> – 8 x processore Intel® Xeon® E7-8890 v4<br /> 192 core CPU e 384 thread CPU |  8 TB |  22 TB |  TooOrder pronto |
|---| SAP HANA in Azure S576<br /> – 12 x processore Intel® Xeon® E7-8890 v4<br /> 288 core CPU e 576 thread CPU |  12 TB |  28 TB | TooOrder pronto |
|---| SAP HANA in Azure S768<br /> – 16 x processore Intel® Xeon® E7-8890 v4<br /> 384 core CPU e 768 thread CPU |  16 TB |  36 TB | TooOrder pronto |
|---| SAP HANA in Azure S960<br /> – 20 x processore Intel® Xeon® E7-8890 v4<br /> 480 core CPU e 960 thread CPU |  20 TB |  46 TB | TooOrder pronto |

- Core CPU = totale di core di CPU non-hyper-threading di somma hello di processori hello dell'unità di hello del server.
- Thread di CPU = totale di thread di calcolo fornite da hyper-threading di core CPU della somma hello dei processori hello dell'unità di hello del server. Tutte le unità vengono configurate toouse predefinito Hyper-Threading.


Hello diverse configurazioni precedenti che sono disponibili o 'non sono disponibili più' vengono fatto riferimento in [&#2316233; nota con il supporto di SAP-SAP HANA in Microsoft Azure (istanze di grandi dimensioni)](https://launchpad.support.sap.com/#/notes/2316233/E). le configurazioni di Hello, che sono contrassegnate come 'Pronto tooOrder' troverà prima dell'entrata in hello nota SAP. Tuttavia, tali istanza SKU può essere ordinata già per hello sei diverse aree di Azure hello servizio dell'istanza di grandi dimensioni HANA è disponibile.

configurazioni specifiche di Hello scelte dipendono dal carico di lavoro, le risorse della CPU e memoria desiderata. È possibile che hello tooleverage di carico di lavoro OLTP SKU che sono ottimizzati per il carico di lavoro OLAP. 

hardware Hello base per tutte le offerte di hello sono SAP HANA TDI Certificate. Tuttavia, viene fatta la distinzione tra due classi diverse di hardware, che divide SKU hello in:

- S72, S72m, S144, S144m, S192 e S192m, con cui verrà fatto riferimento hello tooas 'una classe Type' di SKU.
- S384, S384m, S384xm, S576, S768 e S960, con cui verrà fatto riferimento tooas hello 'Class Type II' di SKU.

È importante toonote un indicatore dell'istanza di grandi dimensioni HANA completo non è allocata in modo esclusivo per un singolo cliente &#39; utilizzare s. Ciò si applica rack toohello delle risorse di calcolo e di archiviazione connesso tramite un'infrastruttura di rete, anche la distribuzione in Azure. Infrastruttura di HANA istanze di grandi dimensioni, come ad esempio, Azure distribuisce diversi clienti &quot;tenant&quot; che sono isolati uno da altro in hello seguenti tre livelli:

- Rete: Isolamento tramite reti virtuali all'interno di indicatore dell'istanza di grandi dimensioni HANA hello.
- Spazio di archiviazione: isolamento tramite macchine virtuali di archiviazione a cui sono assegnati volumi di archiviazione e isolamento dei volumi di archiviazione tra i tenant.
- Calcolo: Assegnazione dedicato di server unità tooa single-tenant. Nessun partizionamento hardware o software delle unità server. Nessuna condivisione di una singola unità server o host tra i tenant. 

Di conseguenza, le distribuzioni di hello di unità di istanze di grandi dimensioni HANA tra tenant diversi non sono visibili tooeach altri. Né può HANA grandi unità istanza distribuita in diversi tenant di comunicare direttamente tra loro a livello di hello istanza grande HANA timbro. Solo HANA grandi istanza unità all'interno di un tenant può comunicare altri nel livello di istanza grande HANA timbro hello tooeach.
Un tenant distribuito nell'indicatore dell'istanza di grandi dimensioni hello viene assegnato tooone consigliabile fatturazione sottoscrizione di Azure. Tuttavia, wise rete sia accessibile da reti virtuali di Azure di altre sottoscrizioni di Azure all'interno di hello registrazione Azure stesso. Se si distribuisce con un'altra sottoscrizione di Azure in hello stessa regione di Azure, è anche possibile scegliere tooask per un tenant di istanza di grandi dimensioni HANA separato.

Esistono differenze significative tra l'esecuzione di SAP HANA in istanze HANA di grandi dimensioni e l'esecuzione di SAP HANA in VM di Azure distribuite in Azure:

- Non esiste alcun livello di virtualizzazione per SAP HANA in Azure (istanze di grandi dimensioni). Ottenere prestazioni di hello di hardware bare metal sottostante hello.
- A differenza di Azure, hello SAP HANA nel server di Azure (istanze di grandi dimensioni) è dedicato tooa specifico cliente. Non è in alcun modo possibile che un'unità server o host venga partizionata a livello hardware o software. Di conseguenza, un'unità di istanza di grandi dimensioni HANA viene utilizzata come assegnato come tooa intero tenant e con tale tooyou come un cliente. Un riavvio o arresto del server di hello non comporta automaticamente del sistema operativo toohello e SAP HANA distribuito in un altro server. (Per tipo classe SKU, hello unica eccezione si verifica se un server che si verifichino problemi e la ridistribuzione deve toobe eseguita in un altro server.)
- A differenza di Azure, in cui vengono selezionati i tipi di processore host per il rapporto costo/prestazioni migliori di hello, tipi di processore hello scelti per SAP HANA in Azure (istanze di grandi dimensioni) sono hello più potenti di linea di processori Intel E7v3 ed E7v4 hello.


### <a name="running-multiple-sap-hana-instances-on-one-hana-large-instance-unit"></a>Esecuzione di più istanze di SAP HANA in un'unità di istanze Large di HANA
È possibile toohost più istanze SAP HANA attiva si trova in unità di istanza di grandi dimensioni HANA hello. In ordine toostill forniscono funzionalità di hello di snapshot di archiviazione e ripristino di emergenza, questa configurazione richiede un volume impostato per ogni istanza. Al momento, unità di istanza di grandi dimensioni HANA hello possono essere suddivisi come segue:

- S72, S72m, S144, S192: Avvio unità In incrementi di 256 GB con 256 GB hello più piccolo. Incrementi pari a 256 GB, 512 GB e così via, possono essere combinato toohello massima di memoria hello dell'unità di hello.
- S144m e S192m: In incrementi di 256 GB con unità più piccola di hello 512 GB. Incrementi come 512 GB, 768 GB e così via, possono essere combinato toohello massima di memoria hello dell'unità di hello.
- Tipo di classe II: In incrementi di 512 GB con hello più piccola unità di 2 TB di avvio. Incrementi come 512 GB, 1 TB, 1,5 TB e così via, possono essere combinato toohello massima di memoria hello dell'unità di hello.

Di seguito sono riportati alcuni esempi dell'esecuzione di più istanze di SAP HANA:

| SKU | Dimensione della memoria | Dimensioni di archiviazione | Dimensioni con più database |
| --- | --- | --- | --- |
| S72 | 768 GB | 3 TB | 1 istanza di HANA da 768 GB<br /> o 1 istanza da 512 GB + 1 istanza da 256 GB<br /> o 3 istanze da 256 GB | 
| S72m | 768 GB | 3 TB | 3 istanze di HANA da 512 GB<br />o 1 istanza da 512 GB + 1 istanza da 1 TB<br />o 6 istanze da 256 GB<br />o 1 istanza da 1,5 TB | 
| S192m | 4 TB | 16 TB | 8 istanze da 512 GB<br />o 4 istanze da 1 TB<br />o 4 istanze da 512 GB + 2 istanze da 1 TB<br />o 4 istanze da 768 GB + 2 istanze da 512 GB<br />o 1 istanza da 4 TB |
| S384xm | 8 TB | 22 TB | 4 istanze da 2 TB<br />o 2 istanze da 4 TB<br />o 2 istanze da 3 TB + 1 istanza da 2 TB<br />o 2 istanze da 2,5 TB + 1 istanza da 3 TB<br />o 1 istanza da 8 TB |


È possibile ottenere idea hello. Esistono certamente altre varianti. 


## <a name="operations-model-and-responsibilities"></a>Responsabilità e modello operativo

servizio Hello fornito con SAP HANA in Azure (istanze di grandi dimensioni) è allineato con i servizi IaaS di Azure. Il cliente ottiene una delle istanze HANA di grandi dimensioni con un sistema operativo installato ottimizzato per SAP HANA. Come con le macchine virtuali IaaS di Azure, la maggior parte delle attività hello di protezione avanzata del sistema operativo, installare software aggiuntivo, è necessario installare HANA, hello operativo hello del sistema operativo e HANA e aggiornamento hello del sistema operativo e HANA è responsabilità dell'utente. Microsoft non impone al cliente aggiornamenti del sistema operativo o di HANA.

![Responsabilità di SAP HANA in Azure (istanze di grandi dimensioni)](./media/hana-overview-architecture/image2-responsibilities.png)

Come si vede nella figura hello riportata sopra, multi-tenant infrastruttura SAP HANA in Azure (istanze di grandi dimensioni) è un'offerta di servizio. E di conseguenza, la divisione hello di responsabilità confine del sistema operativo infrastruttura hello, per hello parte la maggior parte delle. Microsoft è responsabile per tutti gli aspetti del servizio hello sotto la riga hello del sistema operativo hello e si è responsabili sopra la riga hello, tra cui sistema operativo hello. Pertanto, più recenti metodi locale che è possibile utilizzare per la gestione del sistema operativo, base, la gestione delle applicazioni, sicurezza e conformità possono continuare toobe utilizzato. sistemi di Hello vengono visualizzati come se sono in rete per quanto riguarda tutti.

Tuttavia, questo servizio è ottimizzato per SAP HANA, pertanto vi sono aree in cui l'utente e Microsoft necessario capacità dell'infrastruttura sottostante di toowork toouse insieme hello per ottenere risultati ottimali.

Hello seguente elenco vengono forniti ulteriori dettagli su ciascuno dei livelli di hello e responsabilità dell'utente:

**Connessione di rete:** tutti hello reti interne per l'indicatore dell'istanza di grandi dimensioni hello esegue SAP HANA, lo spazio di archiviazione toohello accesso, la connettività tra le istanze di hello (per scalabilità orizzontale e altre funzioni), orizzontale toohello connettività e connettività tooAzure dove livello dell'applicazione SAP hello è ospitato in macchine virtuali di Azure. È inclusa inoltre la connettività WAN tra data center di Azure per la replica a scopo di ripristino di emergenza. Tutte le reti sono partizionate in base al tenant hello e QOS applicati.

**Archiviazione:** hello virtualizzato archiviazione partizionata per tutti i volumi necessari dai server SAP HANA hello, nonché per gli snapshot. 

**Server:** hello dedicato server fisici toorun hello SAP HANA DBs tootenants assegnato. Hello Server di tipo una classe hello di SKU sono indipendenti e possono essere hardware. Con questi tipi di server, configurazione del server hello verrà raccolti e gestiti nei profili che possono essere spostati da un hardware fisico di tooanother hardware fisico. Un tale (manuale) spostamento di un profilo per le operazioni può essere confrontato con un bit tooAzure servizio correzione. server Hello di hello Type II classe SKU non offrono tale funzionalità.

**SDDC:** software di gestione di hello toomanage utilizzati dati Center come entità software definito. Consente a Microsoft toopool risorse per motivi di prestazioni, disponibilità e scalabilità.

**Sistema operativo:** hello del sistema operativo scelto (SUSE Linux o Red Hat Linux) in esecuzione nel server di hello. vengono fornite le immagini di Hello del sistema operativo sono immagini di hello fornite da hello singoli Linux fornitore tooMicrosoft a scopo di hello dell'esecuzione di SAP HANA. Si è toohave necessarie una sottoscrizione con il fornitore Linux hello per immagine ottimizzata di SAP HANA specifica hello. Responsabilità dell'utente includono la registrazione di immagini hello con fornitore del sistema operativo hello. Dal punto di hello del passaggio da Microsoft, è responsabile anche per qualsiasi ulteriormente l'applicazione di patch del sistema operativo Linux di hello. Anche questa patch include pacchetti aggiuntivi che potrebbero essere necessari per una corretta installazione di SAP HANA (vedere la documentazione di installazione HANA del tooSAP e note su SAP) e che non sono state inserite dal fornitore Linux specifico hello nella loro SAP HANA immagini del sistema operativo ottimizzate. responsabilità di Hello del cliente hello include anche l'applicazione di patch di hello del sistema operativo che è correlato toomalfunction/ottimizzazione di hello del sistema operativo e l'hardware del server specifiche correlate toohello driver. Qualsiasi protezione o l'applicazione di patch funzionale di hello del sistema operativo. La responsabilità del cliente ricade inoltre nel monitoraggio e nella pianificazione della capacità di:

- Utilizzo delle risorse della CPU
- Utilizzo della memoria
- Volumi di disco correlati toofree spazio e IOPS latenza
- Traffico del volume di rete tra le istanze HANA di grandi dimensioni e il livello applicazione SAP

infrastruttura Hello di istanze di grandi dimensioni HANA fornisce funzionalità per il backup e ripristino del volume del sistema operativo hello. Anche l'uso di queste funzionalità è responsabilità del cliente.

**Middleware:** hello istanza di SAP HANA, principalmente. L'amministrazione, le operazioni e il monitoraggio sono responsabilità del cliente. Funzionalità è stata fornita che consente di snapshot di archiviazione toouse per scopi di ripristino di emergenza e backup/ripristino. Queste funzionalità sono fornite dall'infrastruttura di hello. Tra le responsabilità del cliente, tuttavia, rientra anche la progettazione della disponibilità elevata o del ripristino di emergenza con queste funzionalità, il relativo uso e il monitoraggio della corretta esecuzione degli snapshot di archiviazione.

**Dati:** i dati gestiti da SAP HANA e altri dati, ad esempio file di backup nei volumi o condivisioni di file. Responsabilità dell'utente includono il monitoraggio spazio libero su disco e la gestione del contenuto di hello nei volumi di hello e monitoraggio hello stata completata l'esecuzione dei backup di volumi di disco e di snapshot di archiviazione. Tuttavia, la corretta esecuzione di siti tooDR la replica di dati è responsabilità di hello di Microsoft.

**Applicazioni:** hello le istanze dell'applicazione SAP o, in caso di applicazioni non SAP, livello di applicazione hello di tali applicazioni. Responsabilità dell'utente includono la distribuzione, amministrazione, operazioni e monitoraggio di tali applicazioni relative toocapacity pianificazione dell'utilizzo delle risorse della CPU, il consumo di memoria, utilizzo dell'archiviazione di Azure e il consumo di larghezza di banda di rete all'interno di Reti virtuali di Azure e da reti virtuali di Azure tooSAP HANA in Azure (istanze di grandi dimensioni).

**WAN:** hello connessioni è stabilire da distribuzioni tooAzure locale per i carichi di lavoro. Per la connettività, tutti i clienti con istanze Large di HANA usano Azure ExpressRoute. Questa connessione non è parte di hello SAP HANA in soluzioni di Azure (istanze di grandi dimensioni), pertanto l'utente è responsabile per l'installazione di hello di questa connessione.

**Archivio:** è preferibile tooarchive copie di dati con i propri metodi gli account di archiviazione. L'archiviazione comporta gestione, conformità, costi e operazioni. Il cliente è responsabile della generazione di copie di archivio e backup in Azure e della relativa archiviazione in modo conforme.

Vedere hello [contratto di servizio per SAP HANA in Azure (istanze di grandi dimensioni)](https://azure.microsoft.com/support/legal/sla/sap-hana-large/v1_0/).

## <a name="sizing"></a>Ridimensionamento

Il ridimensionamento per le istanze HANA di grandi dimensioni non è diverso dal ridimensionamento per HANA in generale. Esistenti e distribuiti i sistemi, si desidera toomove da altri tooHANA RDBMS, SAP fornisce una serie di report eseguiti in sistemi SAP esistenti. Se il database di hello tooHANA spostata, questi report controllare dati hello e calcolare i requisiti di memoria per l'istanza HANA hello. Leggere hello tooget note su SAP seguenti ulteriori informazioni su come toorun questi report e in che modo tooobtain le patch/versioni più recenti:

- [SAP Note #1793345 - Sizing for SAP Suite on HANA](https://launchpad.support.sap.com/#/notes/1793345) (Nota SAP 1793345: ridimensionamento della suite SAP in HANA)
- [SAP Note #1872170 - Suite on HANA and S/4 HANA sizing report](https://launchpad.support.sap.com/#/notes/1872170) (Nota SAP 1872170: report sul ridimensionamento della suite in HANA e S/4 HANA)
- [SAP Note #2121330 - FAQ: SAP BW on HANA Sizing Report](https://launchpad.support.sap.com/#/notes/2121330) (Nota SAP 2121330: domande frequenti: report sul ridimensionamento di SAP BW in HANA)
- [SAP Note #1736976 - Sizing Report for BW on HANA](https://launchpad.support.sap.com/#/notes/1736976) (Nota SAP 1736976: report sul ridimensionamento per BW in HANA)
- [SAP Note #2296290 - New Sizing Report for BW on HANA](https://launchpad.support.sap.com/#/notes/2296290) (Nota SAP 2296290: nuovo report sul ridimensionamento per BW in HANA)

Per le implementazioni di campo verde Ridimensiona rapido SAP è toocalculate disponibili i requisiti di memoria dell'implementazione di hello del software SAP HANA.

I requisiti di memoria HANA aumenta man mano che aumenta il volume di dati, pertanto si desidera conoscere il consumo di memoria hello ora toobe e deve essere in grado di toopredict toobe corso in è hello future. In base ai requisiti di memoria hello, sarà quindi possibile mappare la domanda in uno dei hello HANA SKU di istanza di grandi dimensioni.

## <a name="requirements"></a>Requisiti

Questo elenco include i requisiti per l'esecuzione di SAP HANA in Azure (istanze Large).

**Microsoft Azure:**

- Una sottoscrizione di Azure che può essere collegati tooSAP HANA in Azure (istanze di grandi dimensioni).
- Contratto di supporto tecnico Premier Microsoft. Vedere [SAP supporto nota #2015553-SAP in Microsoft Azure: prerequisiti supporto](https://launchpad.support.sap.com/#/notes/2015553) per informazioni specifiche correlate toorunning SAP in Azure. Con unità di grandi dimensioni istanza HANA 384 e più CPU, è necessario anche tooextend hello tooinclude contratto Premier Support la risposta rapida di Azure (ARR).
- Presenza di istanze di grandi dimensioni hello HANA SKU necessario dopo l'esecuzione di un oggetto di ridimensionamento esercitarsi con SAP.

**Connettività di rete:**

- Azure ExpressRoute tra tooAzure locale: tooconnect il tooAzure Data Center locale, verificare che tooorder almeno una connessione di Gbps 1 dal provider di servizi Internet. 

**Sistema operativo:**

- Licenze per SUSE Linux Enterprise Server 12 per applicazioni SAP.

> [!NOTE] 
> Hello del sistema operativo fornito da Microsoft non è registrato con SUSE, né è connesso a un'istanza SMT.

- SUSE Linux Subscription Management Tool (SMT) distribuito in una VM di Azure. Questo consente hello per SAP HANA in Azure (istanze di grandi dimensioni) toobe registrati e aggiornati rispettivamente dal SUSE (come sono senza accesso a internet data center di istanze di grandi dimensioni HANA). 
- Licenze per Red Hat Enterprise Linux 6.7 o 7.2 per SAP HANA.

> [!NOTE]
> Hello del sistema operativo fornito da Microsoft non è registrato con Red Hat e non è connesso it tooa Red Hat gestione della sottoscrizione di istanza.

- Red Hat Subscription Manager distribuito in una VM di Azure. Gestione della sottoscrizione di Red Hat Hello consente hello per SAP HANA in Azure (istanze di grandi dimensioni) toobe registrati e aggiornati rispettivamente da Red Hat (perché non è presente alcun accesso diretto a internet all'interno di hello tenant distribuito su indicatore dell'istanza di grandi dimensioni di Azure hello).
- SAP richiede il supporto del contratto con il provider di Linux nonché toohave. Questo requisito non viene cancellato dalla soluzione hello di istanze di grandi dimensioni HANA o hello fatto che l'esecuzione di Linux in Azure. A differenza di alcuni hello Linux Azure immagini della raccolta, Commissione di servizio hello non è incluso nell'offerta di soluzione hello di istanze di grandi dimensioni HANA. È compito dell'utente come un toofulfill hello requisiti del cliente di SAP sui contratti di supporto con server di distribuzione Linux hello.   
   - Per SUSE Linux, cercare il contratto di requisiti di supporto in hello [SAP nota #1984787 - SUSE LINUX Enterprise Server 12: note sull'installazione](https://launchpad.support.sap.com/#/notes/1984787) e [SAP nota #1056161 - SUSE priorità supporto per le applicazioni SAP](https://launchpad.support.sap.com/#/notes/1056161).
   - Per Red Hat Linux, è necessario toohave i livelli di sottoscrizione corretto di hello che includono il supporto e il servizio (Aggiorna i sistemi operativi toohello HANA istanze di grandi dimensioni. Red Hat consiglia di ottenere una sottoscrizione "RHEL for SAP Business Applications". Per informazioni dettagliate su supporto e assistenza, vedere [SAP Note #2002167 - Red Hat Enterprise Linux 7.x: Installation and Upgrade](https://launchpad.support.sap.com/#/notes/2002167) (Nota SAP 2002167 - Red Hat Enterprise Linux 7.x: installazione e aggiornamento) e [SAP Note #1496410 - Red Hat Enterprise Linux 6.x: Installation and Upgrade](https://launchpad.support.sap.com/#/notes/1496410) (Nota SAP 1496410 - Red Hat Enterprise Linux 6.x: installazione e aggiornamento).

**Database:**

- Licenze e componenti di installazione software per SAP HANA (edizione Platform o Enterprise).

**Applicazioni:**

- Licenze e componenti di installazione software per tutte le applicazioni SAP connessione tooSAP HANA e correlati SAP supportano i contratti.
- Licenze e componenti di installazione software per tutte le applicazioni SAP non utilizzato in relazione tooSAP HANA nell'ambiente di Azure (istanze di grandi dimensioni) e relativi contratti di supporto.

**Competenze:**

- Esperienza e conoscenza di IaaS di Azure e relativi componenti.
- Esperienza e conoscenza sulla distribuzione del carico di lavoro SAP in Azure.
- Certificazione personale dell'installazione di SAP HANA.
- SAP architetto competenze toodesign la disponibilità elevata e ripristino di emergenza intorno a SAP HANA.

**SAP:**

- È previsto che il cliente sia un cliente SAP con un contratto di supporto con SAP.
- In particolare per le implementazioni nella classe di tipo II di SKU istanza grande HANA hello, è consigliabile tooconsult con SAP nelle versioni di SAP HANA e l'eventuale configurazioni di grandi dimensioni hardware di scalabilità verticale.


## <a name="storage"></a>Archiviazione

Hello layout di archiviazione per SAP HANA in Azure (istanze di grandi dimensioni) è configurata per SAP HANA sulla gestione dei servizi di Azure tramite SAP indicazioni documentati in hello [i requisiti di archiviazione di SAP HANA](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) white paper relativo alle.

Istanze di grandi dimensioni HANA Hello di hello una classe di tipo vengono forniti con volume di memoria hello quattro volte come volume di archiviazione. Per il tipo di hello classe II di unità di istanza di grandi dimensioni HANA archiviazione hello non sarà toobe quattro volte superiore. unità di Hello dotati di un volume, il cui scopo è per l'archiviazione dei backup del log delle transazioni HANA. Trovare altre informazioni, vedere [come tooinstall e configurare SAP HANA (istanze di grandi dimensioni) in Azure](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Vedere hello in termini di allocazione di memoria nella tabella seguente. Hello tabella approssimativamente capacità hello per diversi volumi hello fornito con diverse unità di istanza di grandi dimensioni HANA hello.

| SKU delle istanze Large di HANA | hana/data | hana/log | hana/shared | HANA/log/backup |
| --- | --- | --- | --- | --- |
| S72 | 1280 GB | 512 GB | 768 GB | 512 GB |
| S72m | 3328 GB | 768 GB |1280 GB | 768 GB |
| S192 | 4608 GB | 1024 GB | 1536 GB | 1024 GB |
| S192m | 11.520 GB | 1536 GB | 1792 GB | 1536 GB |
| S384 | 11.520 GB | 1536 GB | 1792 GB | 1536 GB |
| S384m | 12.000 GB | 2050 GB | 2050 GB | 2040 GB |
| S384xm | 16.000 GB | 2050 GB | 2050 GB | 2040 GB |
| S576 | 20.000 GB | 3100 GB | 2050 GB | 3100 GB |
| S768 | 28.000 GB | 3100 GB | 2050 GB | 3100 GB |
| S960 | 36.000 GB | 4100 GB | 2050 GB | 4100 GB |


Volumi distribuiti effettivi possono variare leggermente in base alla distribuzione e strumento che viene utilizzato tooshow hello delle dimensioni del volume.

In caso di suddivisione di uno SKU delle istanze Large di HANA, alcuni esempi delle possibili parti della divisione saranno simili ai seguenti:

| Partizione di memoria in GB | hana/data | hana/log | hana/shared | HANA/log/backup |
| --- | --- | --- | --- | --- |
| 256 | 400 GB | 160 GB | 304 GB | 160 GB |
| 512 | 768 GB | 384 GB | 512 GB | 384 GB |
| 768 | 1280 GB | 512 GB | 768 GB | 512 GB |
| 1024 | 1792 GB | 640 GB | 1024 GB | 640 GB |
| 1536 | 3328 GB | 768 GB | 1280 GB | 768 GB |


Queste dimensioni sono numeri approssimativa di volume che possono variare leggermente a seconda distribuzione e gli strumenti utilizzati toolook volumi hello. Sono ipotizzabili anche altre dimensioni di partizione, ad esempio 2,5 TB. La dimensione di archiviazione verrebbero calcolata con una formula simile utilizzato per le partizioni hello precedente. termine Hello 'partitions' non indicano che le risorse della CPU, memoria o sistema operativo hello sono in alcun modo partizionate. Indica solo le partizioni di archiviazione per istanze HANA diverse hello è toodeploy su una singola unità HANA istanza di grandi dimensioni. 

È come un cliente potrebbe essere necessario per uno spazio di archiviazione, è necessario hello possibilità tooadd archiviazione toopurchase ulteriore spazio di archiviazione in unità di 1 TB. Questo ulteriore spazio di archiviazione può essere aggiunti come altro volume o può essere utilizzato tooextend uno o più volumi esistenti di hello. Non è dimensioni hello toodecrease possibili dei volumi hello come distribuzione originale e documentato principalmente da tabelle hello precedente. Non è inoltre nomi di hello toochange possibili di volumi hello o nomi di montaggio. volumi di archiviazione Hello come descritto in precedenza sono unità di istanza di grandi dimensioni HANA toohello collegato come NFS4 volumi.

È come un cliente può scegliere toouse snapshot di archiviazione di emergenza e backup/ripristino scopi di ripristino. Maggiori dettagli su questo argomento sono presenti on [Disponibilità elevata e ripristino di emergenza di SAP HANA (istanze di grandi dimensioni) in Azure](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="encryption-of-data-at-rest"></a>Crittografia dei dati inattivi
archiviazione Hello utilizzato per le istanze di grandi dimensioni HANA consente una crittografia trasparente dei dati di hello archiviati su dischi hello. In fase di distribuzione di un'unità istanza grande HANA è hello opzione toohave questo tipo di crittografia è abilitata. È anche possibile scegliere toochange tooencrypted volumi dopo la distribuzione di hello già. spostamento di Hello dai volumi tooencrypted senza crittografia è trasparente e non richiede un tempo di inattività. 

Con il tipo classe SKU, avvio di hello volume hello LUN viene archiviato, hello è crittografata. In caso di tipo hello classe II di SKU di HANA istanze di grandi dimensioni, è necessario l'avvio di hello tooencrypt LUN con i metodi del sistema operativo. 


## <a name="networking"></a>Rete

architettura di Hello di rete di Azure è una distribuzione di toosuccessful componente chiave di applicazioni SAP in istanze di grandi dimensioni HANA. In genere, le distribuzioni di SAP HANA in Azure (istanze di grandi dimensioni) dispongono di un panorama applicativo di SAP più ampio con varie soluzioni SAP e varie dimensioni di database, utilizzo delle risorse della CPU e utilizzo della memoria. È probabile che non tutti i sistemi SAP siano basati su SAP HANA e che quindi il panorama applicativo SAP sia un ibrido che include quanto segue:

- Sistemi SAP distribuiti in locale. A causa delle dimensioni tootheir, questi sistemi attualmente non possono essere ospitati in Azure; un esempio classico sarebbe un sistema ERP SAP di produzione in esecuzione in Microsoft SQL Server (come database hello) che richiede più CPU o risorse di memoria macchine virtuali di Azure possono fornire.
- Sistemi SAP basati su SAP HANA distribuiti in locale.
- Sistemi SAP distribuiti in VM di Azure. Questi sistemi potrebbero essere sviluppo, test, sandbox, o istanze di produzione per le applicazioni basate su SAP NetWeaver hello che è possano distribuire correttamente in Azure (su macchine virtuali), in base alle esigenze di memoria e il consumo di risorse. Questi sistemi possono anche essere basati su database come SQL Server o SAP HANA. Vedere rispettivamente [SAP Support Note #1928533 - SAP Applications on Azure: Supported Products and Azure VM types](https://launchpad.support.sap.com/#/notes/1928533/E) (Nota di supporto SAP 1928533 - Applicazioni SAP in Azure: prodotti supportati e tipi di VM di Azure) e [SAP HANA Certified IaaS Platforms](http://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html) (Piattaforme IaaS certificate per SAP HANA).
- Server applicazioni SAP distribuiti in Azure (nelle VM) che utilizzano SAP HANA in Azure (istanza di grandi dimensioni) in moduli per istanze di grandi dimensioni in Azure.

Nonostante un panorama applicativo SAP ibrido (con quattro o più diversi scenari di distribuzione) sia tipico, in molti casi i clienti hanno un panorama applicativo SAP completo in esecuzione in Azure. Come macchine virtuali di Microsoft Azure sono sempre più potente, sta aumentando il numero di hello di clienti lo spostamento di tutte le relative soluzioni SAP in Azure.

Rete nel contesto di hello dei sistemi SAP distribuiti in Azure di Azure non sia complicata. È basato su hello principi seguenti:

- Reti virtuali di Azure (Vnet) necessario toobe connesso toohello Azure ExpressRoute circuito che si connette rete tooon locale.
- Un circuito ExpressRoute connessione in genere tooAzure locale deve disporre di una larghezza di banda di 1 Gbps. La larghezza di banda minima larghezza di banda adeguata per il trasferimento dei dati tra sistemi locali e in esecuzione in macchine virtuali di Azure (così come i sistemi tooAzure connessione da utenti finali locale).
- Tutti i sistemi SAP in Azure è necessario toobe configurate in reti virtuali di Azure toocommunicate tra loro.
- Active Directory e DNS ospitati in locale sono estesi in Azure tramite ExpressRoute da locale.


> [!NOTE] 
> Dal punto di vista fatturazione, solo una singola sottoscrizione di Azure può essere collegata solo tooone single-tenant in un indicatore dell'istanza di grandi dimensioni in un'area specifica di Azure e viceversa un singolo tenant di indicatore di istanza di grandi dimensioni possono essere collegate solo tooone sottoscrizione di Azure. Ciò è tooany non sono diversi altri oggetti fatturabili in Azure

Distribuzione di SAP HANA in Azure (istanze di grandi dimensioni) in più aree di Azure diversi, i risultati in un toobe tenant separata è distribuito in hello indicatore dell'istanza di grandi dimensioni. Tuttavia, è possibile eseguire entrambe in hello landscape SAP stesso, purché queste istanze sono parte di hello stessa sottoscrizione di Azure. 

> [!IMPORTANT] 
> SAP HANA in Azure (istanze di grandi dimensioni) supporta solo la distribuzione di Azure Resource Management.

 

### <a name="additional-azure-vnet-information"></a>Informazioni aggiuntive sulla rete virtuale di Azure

In ordine tooconnect tooExpressRoute una rete virtuale di Azure, è necessario creare un gateway di Azure (vedere [relative ai gateway di rete virtuale per ExpressRoute](../../../expressroute/expressroute-about-virtual-network-gateways.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Un gateway di Azure può essere usato con ExpressRoute tooan infrastruttura all'esterno di Azure (o un indicatore di istanza di grandi dimensioni di Azure tooan), o tooconnect tra reti virtuali di Azure (vedere [configurare una connessione di rete per Gestione risorse con PowerShell ](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). È possibile connettersi hello Azure gateway tooa al massimo quattro diverse connessioni ExpressRoute, purché tali connessioni provenienti da diversi router Microsoft Enterprise Edge (MSEE).  Per altre informazioni, vedere [Infrastruttura e connettività di SAP HANA (istanze Large) in Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

> [!NOTE] 
> Hello velocità effettiva che fornisce un gateway di Azure è diversa per entrambi i casi di utilizzo (vedere [sul Gateway VPN](../../../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). la velocità effettiva massima Hello che è possibile ottenere con un gateway di rete virtuale è 10 Gbps, utilizzando una connessione ExpressRoute. Tenere presente che la copia dei file tra una macchina virtuale di Azure che si trovano in una rete virtuale di Azure e un sistema locale (come un flusso di sola copia) non raggiungere la velocità effettiva di completo hello del gateway diversi hello SKU. tooleverage hello completo della larghezza di banda del gateway di rete virtuale hello nei flussi paralleli di un singolo file, è necessario utilizzare più flussi o copia di file diverso.


### <a name="networking-architecture-for-hana-large-instances"></a>Architettura di rete per istanze Large di HANA
architettura di rete per le istanze di grandi dimensioni HANA Hello come illustrato di seguito, può essere suddivisi in quattro diverse parti:

- Rete locale e tooAzure connessione ExpressRoute. Questa parte è il dominio di clienti hello e tooAzure connesso tramite ExpressRoute. Questa è la parte hello in basso a destra hello grafica hello riportato di seguito.
- Rete di Azure, illustrata brevemente sopra, con reti virtuali di Azure anche in questo caso con gateway. Si tratta di un'area in cui è necessario progettazioni di toofind hello appropriato per i requisiti delle applicazioni, sicurezza e i requisiti di conformità. Utilizzo di istanze di grandi dimensioni HANA è un altro punto di considerazione in termini di numero di reti virtuali e Azure toochoose SKU di gateway da. Questa è la parte hello in alto a destra hello grafica hello.
- Connettività delle istanze Large di HANA ad Azure tramite la tecnologia ExpressRoute. Questa parte è distribuita e gestita da Microsoft. È sufficiente toodo come un cliente è tooprovide alcuni intervalli di indirizzi IP e dopo la distribuzione delle risorse durante la connessione a istanze di grandi dimensioni HANA hello hello ExpressRoute circuit toohello VNet(s) Azure (vedere [infrastruttura SAP HANA (istanze di grandi dimensioni) e connettività in Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). 
- Rete nelle istanze Large di HANA, in gran parte trasparente per il cliente.

![Rete virtuale di Azure connessa tooSAP HANA in Azure (istanze di grandi dimensioni) e locale](./media/hana-overview-architecture/image3-on-premises-infrastructure.png)

tabelle dei fatti Hello utilizzare istanze di grandi dimensioni HANA non modifica hello requisito tooget le risorse locali connessi tramite tooAzure ExpressRoute. Viene anche modificata necessità hello di disporre di uno o più reti virtuali che eseguono le macchine virtuali di Azure hello quale livello di applicazione hello host che si connette a istanze HANA toohello ospitate nell'unità HANA istanza di grandi dimensioni. 

le distribuzioni di tooSAP differenza Hello in pure Azure, viene fornito con fact hello che:

- unità istanza grande HANA Hello del tenant cliente sono connessi tramite un altro circuito ExpressRoute nel VNet(s) di Azure. In condizioni di carico tooseparate ordine, hello locale tooAzure VNets ExpressRoute collegamenti e collegamenti tra reti virtuali di Azure e istanze di grandi dimensioni HANA non condividono hello stesso router.
- profilo di carico di lavoro Hello tra livello dell'applicazione SAP hello e hello HANA istanza è un carattere diverso di numerose richieste di piccole dimensioni e potenziamento come dati trasferisce (set di risultati) da SAP HANA nel livello applicazione hello.
- architettura dell'applicazione SAP Hello è più sensibili toonetwork latenza di scenari tipici in cui i dati ottiene scambiati tra locale e Azure.
- gateway di rete virtuale Hello ha almeno due connessioni ExpressRoute ed entrambe le connessioni condividono hello massimo della larghezza di banda per i dati in ingresso del gateway di rete virtuale hello.

latenza di rete Hello esperto tra macchine virtuali di Azure e HANA grandi unità di istanza può essere maggiore di una tipico latenza round trip di rete VM per VM. Dipende hello regione di Azure, i valori hello misurati possono superare il round trip latenza ms 0,7 hello classificata come inferiore alla media in [SAP nota #1100926 - domande frequenti: prestazioni di rete](https://launchpad.support.sap.com/#/notes/1100926/E). Nonostante ciò, la distribuzione da parte dei clienti di applicazioni SAP di produzione basate su SAP HANA in istanze Large di SAP HANA ha avuto esito positivo. i clienti di Hello che distribuito segnalato notevoli miglioramenti eseguendo le applicazioni SAP in SAP HANA tramite le istanze di grandi HANA unità. È comunque consigliabile testare accuratamente i processi aziendali nelle istanze Large di HANA in Azure.
 
Ordine tooprovide deterministica della latenza di rete tra macchine virtuali di Azure e HANA istanza di grandi dimensioni, è essenziale scelta hello di hello SKU di Gateway di rete virtuale di Azure. A differenza dei modelli di traffico hello tra on-premise e macchine virtuali di Azure, il modello di traffico hello tra macchine virtuali di Azure e le istanze di grandi dimensioni HANA possibile sviluppare piccoli ma elevate picchi di richieste e toobe di volumi di dati trasmessi. In ordine toohave tali burst gestito, è consigliabile utilizzo hello di hello UltraPerformance SKU di Gateway. Per la classe di tipo II di SKU istanza grande HANA hello, l'utilizzo di hello del gateway UltraPerformance hello SKU come Gateway di rete virtuale di Azure è obbligatoria.  

> [!IMPORTANT] 
> Specificato hello complessivo traffico di rete tra un'applicazione hello SAP e il livello di database hello solo ad alte prestazioni o gateway UltraPerformance SKU per le reti virtuali è supportata per la connessione tooSAP HANA in Azure (istanze di grandi dimensioni). Per grandi HANA istanza tipo II SKU, è supportato solo hello UltraPerformance SKU di Gateway come Gateway di rete virtuale di Azure.



### <a name="single-sap-system"></a>Sistema SAP singolo

infrastruttura locale Hello illustrato in precedenza viene connesso tramite ExpressRoute in Azure e hello circuito ExpressRoute si connette in un Microsoft Enterprise Edge Router (MSEE) (vedere [Panoramica tecnica su ExpressRoute](../../../expressroute/expressroute-introduction.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Una volta stabilita, tale route a cui si connette il backbone di Microsoft Azure hello e tutte le aree di Azure sono accessibili.

> [!NOTE] 
> Per l'esecuzione di scenari SAP in Azure, connettersi toohello MSEE più vicino toohello area di Azure nel landscape SAP hello. Azure timbri di istanza di grandi dimensioni sono connesse tramite dedicato MSEE dispositivi toominimize latenza di rete tra macchine virtuali di Azure in timbri IaaS di Azure e l'istanza di grandi dimensioni.

gateway di rete virtuale per macchine virtuali di Azure che ospita le istanze dell'applicazione SAP, hello Hello è connesso toothat circuito ExpressRoute e stessa rete virtuale hello è connesso tooa separato Router MSEE dedicato tooconnecting tooLarge istanza timbri.

Questo è un esempio semplice di un singolo sistema SAP, in cui hello livello dell'applicazione SAP è ospitato in Azure e database SAP HANA hello viene eseguito in SAP HANA in Azure (istanze di grandi dimensioni). presupposto Hello è la larghezza di banda hello gateway rete virtuale di 2 GB/s o velocità effettiva di 10 GB/s non rappresenta un collo di bottiglia.

### <a name="multiple-sap-systems-or-large-sap-systems"></a>Sistemi SAP multipli o sistemi SAP di grandi dimensioni

Se vengono distribuiti i sistemi SAP più grandi sistemi SAP connessione tooSAP HANA in Azure (istanze di grandi dimensioni) &#39; velocità effettiva di hello tooassume ragionevole s del gateway di rete virtuale hello potrebbe diventare un collo di bottiglia. In tal caso, è necessario toosplit livelli dell'applicazione hello in più reti virtuali di Azure. Inoltre potrebbe essere consigliabile toocreate speciali reti virtuali che si connettono tooHANA istanze di grandi dimensioni per i casi come:

- Esecuzione di backup direttamente dal hello HANA istanze in istanze di grandi dimensioni HANA tooa macchina virtuale in Azure che ospita le condivisioni NFS
- Copia di backup di grandi dimensioni o altri file da spazio dell'istanza di grandi dimensioni di HANA toodisk unità gestito in Azure.

Utilizzo di reti virtuali separate che evita di host macchine virtuali per la gestione archiviazione hello impatto per i file di grandi dimensioni o di trasferimento dei dati da istanze di grandi dimensioni HANA tooAzure nel Gateway di rete virtuale che svolge le macchine virtuali hello in esecuzione a livello dell'applicazione SAP hello hello. 

Per un'architettura di rete più scalabile:

- Utilizzare più reti virtuali di Azure per un livello applicazione SAP singolo e di dimensioni maggiori.
- Distribuire una rete virtuale di Azure separato per ogni sistema SAP distribuito, confrontati toocombining hello di questi sistemi SAP in subnet separate nella stessa rete virtuale.

 Un'architettura di rete più scalabile per SAP HANA in Azure (istanze di grandi dimensioni):

![Distribuzione del livello applicazione SAP su più reti virtuali di Azure](./media/hana-overview-architecture/image4-networking-architecture.png)

Distribuzione livello dell'applicazione SAP hello o componenti, su più reti virtuali di Azure, come illustrato in precedenza, è stato introdotto un overhead di latenza inevitabile che si sono verificati durante la comunicazione tra applicazioni hello ospitate in tali reti virtuali di Azure. Per impostazione predefinita, il traffico di rete hello tra macchine virtuali di Azure si trova nella route reti virtuali diversa tramite hello router MSEE in questa configurazione. A partire da settembre 2016, tuttavia, questo routing può essere ottimizzato. Hello modo toooptimize e ridurre la latenza di hello nelle comunicazioni tra due reti virtuali sono peering reti virtuali di Azure all'interno di hello stessa area. Anche se tali reti virtuali si trovano in sottoscrizioni diverse. Utilizzo rete virtuale di Azure peering, comunicazioni hello tra le macchine virtuali in due reti virtuali di Azure diversi possono utilizzare hello Azure rete backbone toodirectly comunicare tra loro. In tal modo latenza simili che mostra come se sarebbe hello macchine virtuali hello stessa rete virtuale. Mentre il traffico, intervalli di indirizzi IP che sono connessi tramite il gateway di rete virtuale di Azure hello, indirizzamento viene instradato tramite hello singoli gateway di rete virtuale di hello rete virtuale. È possibile ottenere informazioni dettagliate su una rete virtuale di Azure peering nell'articolo hello [peering reti virtuali](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).


### <a name="routing-in-azure"></a>Routing in Azure

Tenere presenti due importanti considerazioni sul routing di rete per SAP HANA in Azure (istanze di grandi dimensioni):

1. SAP HANA in Azure (istanze di grandi dimensioni) è accessibile solo dalle macchine virtuali di Azure in connessione ExpressRoute hello dedicato. non è direttamente da on-premise. Alcuni client di amministrazione e le applicazioni che necessitano dell'accesso diretto, ad esempio SAP Solution Manager in esecuzione in locale, non è possibile connettersi a database SAP HANA toohello.

2. SAP HANA in unità di Azure (istanze di grandi dimensioni) hanno un indirizzo IP assegnato dall'indirizzo di Pool IP Server hello intervallo di valori come cliente hello inviato (vedere [infrastruttura SAP HANA (istanze di grandi dimensioni) e la connettività in Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per informazioni dettagliate).  Questo indirizzo IP è possibile accedere tramite hello Azure ExpressRoute che si connette a reti virtuali di Azure tooHANA in Azure (istanze di grandi dimensioni) e le sottoscrizioni. è stata direttamente assegnato unità hardware toohello Hello indirizzo IP assegnato fuori intervallo di indirizzi del Pool di IP di Server e non è NAT'ed più come in questo caso hello nelle distribuzioni prima di hello di questa soluzione. 

> [!NOTE] 
> Se è necessario tooconnect tooSAP HANA in Azure (istanze di grandi dimensioni) in un _del data warehouse_ scenario, in cui le applicazioni e/o gli utenti finali devono database SAP HANA di toohello tooconnect (direttamente in esecuzione), deve essere un altro componente di rete utilizzato: un proxy inverso tooroute dati, tooand da. Ad esempio, F5 BIG-IP, NGINX con Gestione traffico distribuita in Azure come soluzione di routing del traffico o del firewall virtuale.

### <a name="internet-connectivity-of-hana-large-instances"></a>Connettività Internet delle istanze di grandi dimensioni HANA
Le istanze di grandi dimensioni HANA NON hanno una connettività internet diretta. Questo limita la capacità di, ad esempio registrare l'immagine del sistema operativo hello direttamente il fornitore del sistema operativo di hello. Di conseguenza potrebbe essere necessario toowork con server SLES SMT locale o Gestione sottoscrizione RHEL

### <a name="data-encryption-between-azure-vms-and-hana-large-instances"></a>Crittografia dei dati tra istanze di grandi dimensioni HANA e macchine virtuali di Azure
I dati trasferiti tra le istanze di grandi dimensioni HANA e le macchine virtuali di Azure non vengono crittografati. Esclusivamente per lo scambio di hello tra hello lato HANA DBMS e le applicazioni JDBC/ODBC basato su, tuttavia, è possibile abilitare la crittografia del traffico. Vedere [questa documentazione di SAP](http://help-legacy.sap.com/saphelp_hanaplatform/helpdata/en/db/d3d887bb571014bf05ca887f897b99/content.htm?frameset=/en/dd/a2ae94bb571014a48fc3b22f8e919e/frameset.htm&current_toc=/en/de/ec02ebbb57101483bdf3194c301d2e/plain.htm&node_id=20&show_children=false).

### <a name="using-hana-large-instance-units-in-multiple-regions"></a>Uso di unità di istanze Large di HANA in più aree

Potrebbe essere altri toodeploy motivi SAP HANA in Azure (istanze di grandi dimensioni) in più aree di Azure, oltre a ripristino di emergenza. Si supponga di tooaccess HANA istanze di grandi dimensioni da ognuna delle macchine virtuali hello distribuite in hello diverse reti virtuali in regioni hello. Poiché gli indirizzi IP di hello assegnati toohello diversa unità HANA istanze di grandi dimensioni non vengono propagate di là hello reti virtuali di Azure (che si è connessi direttamente tramite le relative istanze toohello gateway), non vi è una lieve modifica toohello progettazione di rete virtuale illustrati in precedenza: un Gateway di rete virtuale di Azure in grado di gestire quattro circuiti ExpressRoute diversi fuori MSEEs diverse e ogni rete virtuale che è connesso tooone di indicatori di grandi dimensioni istanza hello può essere connesso toohello indicatore dell'istanza di grandi dimensioni in un'altra area di Azure.

![Reti virtuali di Azure connessa tooAzure timbri di istanza di grandi dimensioni in diverse aree di Azure](./media/hana-overview-architecture/image8-multiple-regions.png)

Hello sopra illustrata nella figura hello come diverse reti virtuali di Azure in entrambe le aree sono circuiti ExpressRoute diversi tootwo connessa che vengono utilizzati tooconnect tooSAP HANA in Azure (istanze di grandi dimensioni) in entrambe le aree di Azure. le connessioni di Hello appena introdotto sono linee rosse rettangolare hello. Con queste connessioni, fuori hello reti virtuali di Azure, le macchine virtuali hello in esecuzione in una di tali reti virtuali possono accedere a ognuna di hello diverse istanze di grandi dimensioni HANA unità distribuita in due aree hello. Come vedere nella grafica hello precedente, si presuppone la presenza di due connessioni ExpressRoute da on-premise toohello due aree di Azure; consigliato per motivi di ripristino di emergenza.

> [!IMPORTANT] 
> Se si utilizzano più circuiti ExpressRoute, anteponendo percorso AS e le impostazioni BGP preferenza locale devono essere utilizzato tooensure corretto routing del traffico di.


