---
title: aaaDynamic accelerazione sito tramite rete CDN di Azure
description: Approfondimento dell'accelerazione sito dinamico
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: v-semcev
ms.openlocfilehash: 37e6312ae5e83448f2d87c95ef48c387355748bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-site-acceleration-via-azure-cdn"></a>Accelerazione sito dinamico tramite la rete CDN di Azure

Con l'esplosione di hello di social networking, commercio elettronico e web hyper personalizzata hello, viene generata una rapido aumento percentuale hello contenuto servita tooend utenti in tempo reale. Gli utenti si aspettano esperienze Web rapide, affidabili e personalizzate, indipendentemente da browser, posizione, dispositivo o rete. Tuttavia, innovazioni molto hello che queste esperienze così coinvolgere anche rallentare il download di pagina e mettere a rischio di qualità di esperienza utente hello hello. 

Funzionalità CDN standard include hello possibilità toocache file più vicino tooend utenti toospeed le opzioni di distribuzione dei file statici. Tuttavia, con le applicazioni web dinamiche, che il contenuto in posizioni del bordo di memorizzazione nella cache perché server hello genera contenuti di hello nel comportamento toouser della risposta. Velocizzare il recapito di hello di tale contenuto è più complessa della memorizzazione nella cache perimetrale tradizionali e richiede una soluzione end-to-end che ottimizzazioni ogni elemento lungo hello intero percorso dati dall'inizio toodelivery. Con Azure CDN dinamica del sito accelerazione (DSA), hello migliorare le prestazioni delle pagine web con contenuto dinamico sono misurabile.

Rete CDN di Azure da Akamai e Verizon offre ottimizzazione DSA tramite hello **ottimizzato per** menu durante la creazione dell'endpoint.

## <a name="configuring-cdn-endpoint-tooaccelerate-delivery-of-dynamic-files"></a>Configurazione di recapito di tooaccelerate endpoint della rete CDN di file dinamici

È possibile configurare la distribuzione di toooptimize endpoint rete CDN di file dinamici tramite il portale di Azure selezionando hello **accelerazione dinamica del sito** per l'opzione hello **ottimizzato per** Selezione proprietà durante creazione dell'endpoint Hello. È inoltre possibile utilizzare le API REST o uno qualsiasi dei hello client SDK toodo hello stessa operazione a livello di codice. 

### <a name="probe-path"></a>Percorso probe
Percorso di sondaggio è un tooDynamic specifiche funzionalità accelerazione del sito, e uno valido è necessario per la creazione. DSA utilizza una piccola *percorso di sondaggio* file posizionato in hello origine toooptimize routing configurazioni di rete per hello CDN. È possibile scaricare e caricare il sito tooyour file di esempio o utilizzare un asset esistente con l'origine corrispondente a circa 10 KB per il percorso di sondaggio hello invece se asset hello esiste.

> [!Note]
> Alla funzionalità Accelerazione sito dinamico si applicano costi aggiuntivi. Per ulteriori informazioni, vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/cdn/) per ulteriori informazioni.

Hello schermate seguenti illustrano il processo di hello tramite il portale di Azure.
 
![Aggiunta di un nuovo endpoint di rete CDN](./media/cdn-dynamic-site-acceleration/01_Endpoint_Profile.png) 

*Figura 1: Aggiunta di un nuovo endpoint CDN da hello profilo CDN*
 
![Creazione di un nuovo endpoint di rete CDN con Accelerazione sito dinamico](./media/cdn-dynamic-site-acceleration/02_Optimized_DSA.png)  

*Figura 2: Creazione di un endpoint di rete CDN tramite la selezione dell'ottimizzazione basata su Accelerazione sito dinamico*

Una volta creato l'endpoint rete CDN hello, si applica le ottimizzazioni DSA hello per tutti i file che corrispondono a determinati criteri. Hello seguente sezione viene descritto l'ottimizzazione DSA in dettaglio.

## <a name="dsa-optimization-using-azure-cdn"></a>Ottimizzazione basata su Accelerazione sito dinamico tramite la rete CDN di Azure

Accelerazione di sito dinamico nella rete CDN di Azure consente di velocizzare il recapito di asset dinamico utilizzando hello tecniche seguenti:

-   Ottimizzazione delle route
-   Ottimizzazioni del protocollo TCP
-   Prelettura degli oggetti (solo Akamai)
-   Compressione di immagini mobile (solo Akamai)

### <a name="route-optimization"></a>Ottimizzazione delle route

Ottimizzazione dell'itinerario è importante perché hello Internet è dinamico, in cui il traffico e temporaneamente le interruzioni pianificate vengono costantemente la topologia di rete hello. Hello protocollo BGP (Border Gateway) è protocollo di routing hello di hello Internet, ma potrebbero essere presenti più veloci delle route tramite intermediari server Point of Presence (PoP). 

Ottimizzazione dell'itinerario sceglie origine toohello percorso ottimale di hello in modo che un sito viene continuamente contenuto accessibile e dinamico viene recapitato utenti tooend tramite hello più veloce e più affidabile route possibili. 

rete Akamai Hello utilizza i dati in tempo reale di tecniche toocollect e confrontare i diversi percorsi tramite vari nodi server Akamai hello, nonché delle route BGP predefinita di hello in hello aprire Internet toodetermine hello più veloce route tra origine hello e hello Bordo della rete CDN. Queste tecniche permettono di evitare lunghe route e punti di congestione in Internet. 

Analogamente, hello Verizon rete utilizza una combinazione di Anycast DNS, ad alta capacità supporta estrazioni e controlli di integrità, toodetermine hello migliore gateway toobest route di dati da hello origine toohello client.
 
Di conseguenza, il contenuto completamente dinamico e transazionale viene recapitato più veloce e più affidabile tooend utenti, anche quando è uncacheable. 

### <a name="tcp-optimizations"></a>Ottimizzazioni del protocollo TCP

Protocollo TCP (Transmission Control) è standard hello della suite di protocolli Internet hello toodeliver informazioni tra applicazioni su reti IP.  Per impostazione predefinita, esistono diverse back e via richieste necessarie tooset di una connessione TCP, nonché congestions rete tooavoid di limiti, determinando inefficienze su larga scala. La rete CDN di Azure con tecnologia Akamai gestisce tutti questi aspetti tramite ottimizzazioni in tre aree: 

 - Eliminazione della lentezza di avvio
 - Uso di connessioni persistenti
 - Ottimizzazione dei parametri dei pacchetti TCP (solo Akamai)

#### <a name="eliminating-slow-start"></a>Eliminazione della lentezza di avvio

*Avvio lento* fa parte del protocollo TCP hello che impedisce la congestione della rete limitando hello quantità dei dati inviati in rete hello. Inizia con dimensioni di finestra di congestione di piccole dimensioni tra mittente e destinatario fino a quando non viene raggiunto hello massimo o la perdita di pacchetti viene rilevata.

La rete CDN di Azure con tecnologie Akamai e Verizon elimina la lentezza di avvio in tre passaggi:

1.  Sia Akamai del Verizon integrità di utilizzo di rete e larghezza di banda di monitoraggio della larghezza di banda di toomeasure hello delle connessioni tra server PoP edge.
2. le metriche Hello vengono condivisi tra server PoP edge in modo che ogni server è a conoscenza di condizioni della rete hello e l'integrità del server di hello altri POP attorno a esse.  
3. server di Hello CDN edge sono ora in grado di toomake scontati alcuni parametri di trasmissione, ad esempio le dimensioni di finestra ottimali hello devono essere durante la comunicazione con gli altri server della rete CDN edge la prossimità. Questo passaggio significa che può essere aumentato dimensioni della finestra di congestione iniziale hello se integrità hello di connessione di hello tra hello CDN lato server è in grado di trasferimenti di dati di pacchetto superiori.  

#### <a name="leveraging-persistent-connections"></a>Uso di connessioni persistenti

Utilizza una rete CDN, un minor numero di computer univoci connessione server di origine tooyour confrontato direttamente con gli utenti si connettono direttamente tooyour origine. Rete CDN di Azure da Akamai e Verizon pool anche tooestablish insieme di richieste utente meno connessioni con origine hello.

Come accennato in precedenza, le connessioni TCP eseguire più richieste avanti e indietro tooestablish un handshake una nuova connessione. Connessioni permanenti, noto anche come "Keep-Alive HTTP," riutilizzare le connessioni TCP esistenti per più HTTP richieste toosave tempi di round trip e velocizzare il recapito. 

rete Verizon Hello invia anche pacchetti keep-alive periodici sulla tooprevent di connessione TCP hello aperta la connessione venga chiusa.

#### <a name="tuning-tcp-packet-parameters"></a>Ottimizzazione dei parametri dei pacchetti TCP

Rete CDN di Azure da Akamai anche Ottimizza parametri hello che controllano le connessioni a server-server e riduce la quantità di hello di prolungate round trip necessari tooretrieve contenuto incorporata nel sito hello utilizzando hello tecniche seguenti:

1.  Aumento della finestra di congestione iniziale hello in modo che più pacchetti possono essere inviati senza attendere un acknowledgement.
2.  Ridurre il timeout di ritrasmissione iniziale hello in modo che viene rilevata una perdita e ritrasmissione avviene in modo più rapido.
3.  Decrescente hello minimo e un massimo di ritrasmettere tempo di attesa hello tooreduce timeout prima di presumere che i pacchetti sono stati persi durante la trasmissione.

### <a name="object-prefetch-akamai-only"></a>Prelettura degli oggetti (solo Akamai)

La maggior parte dei siti Web è costituita da una pagina HTML che fa riferimento a diverse altre risorse, come immagini e script. In genere, quando un client richiede una pagina Web, browser hello Scarica per prima cosa analizza hello HTML oggetto e quindi effettua richieste aggiuntive asset toolinked toofully necessario caricare la pagina hello. 

*Prelettura* è una tecnica tooretrieve immagini e gli script incorporati in hello pagina HTML hello HTML viene servita toohello browser, mentre prima hello browser rende anche queste richieste di oggetto. 

Con hello **prelettura** opzione è attivata in fase di hello quando hello rete CDN browser del client di hello HTML della pagina di base toohello, hello CDN Analizza file hello HTML e ulteriori richieste per tutte le risorse collegate e memorizzarlo nella cache. Quando hello client effettua richieste hello per le risorse collegata hello, server perimetrale della rete CDN di hello già dispone di oggetti richiesti hello e utilizzarlo li immediatamente senza un'origine toohello di andata e ritorno. Questa ottimizzazione è utile per contenuti memorizzabili e non memorizzabili nella cache.

### <a name="adaptive-image-compression-akamai-only"></a>Compressione di immagini adattiva (solo Akamai)

Alcuni dispositivi, in particolare quelli per dispositivi mobili, esperienza velocità di rete da tootime ora. In questi scenari, è più utile per le immagini più piccole di hello utente tooreceive nella relativa pagina Web più rapidamente anziché restare in attesa di molto tempo per le immagini ad alta risoluzione.

Questa funzionalità consente di monitorare la qualità rete automaticamente e utilizza i metodi standard di compressione JPEG quando la velocità di rete sono tempi di recapito tooimprove più lenti.

Compressione di immagini adattiva | Estensioni di file  
--- | ---  
Compressione JPEG | JPG, JPEG, JPE, JIG, JGIG, JGI

## <a name="caching"></a>Memorizzazione nella cache

Con DSA, memorizzazione nella cache è disabilitata per impostazione predefinita in hello CDN, anche quando l'origine hello include intestazioni cache-controllo/scade in risposta hello. Questa impostazione predefinita è stata disattivata perché DSA viene in genere utilizzato per gli asset dinamici che dovrebbero non essere memorizzati nella cache dal momento che sono client tooeach univoco e attivando la memorizzazione nella cache per impostazione predefinita è possibile interrompere questo comportamento.

Se si dispone di un sito Web con una combinazione di risorse statiche e dinamiche, è migliore tootake un ibrido approccio tooget hello migliori prestazioni. 

Se si utilizza ADN con Verizon Premium, è possibile attivare la memorizzazione nella cache in casi specifici utilizzando hello motore regole di business.  

In alternativa è toouse due endpoint di rete CDN. Uno con le risorse dinamiche toodeliver DSA e un altro endpoint con un'ottimizzazione statico digitare, ad esempio generale recapito web toodelivery memorizzabile nella cache asset. In ordine tooaccomplish questo alternativo, si modificherà il toolink gli URL di pagina Web direttamente toohello asset su hello endpoint rete CDN Prevedi toouse. 

Ad esempio: `mydynamic.azureedge.net/index.html` è una pagina dinamica e viene caricato da endpoint DSA hello.  Hello pagina html fa riferimento a più risorse statiche, ad esempio librerie JavaScript o le immagini caricate da hello endpoint rete CDN statico, ad esempio `mystatic.azureedge.net/banner.jpg` e `mystatic.azureedge.net/scripts.js`. 

È possibile trovare un esempio [qui](https://docs.microsoft.com/azure/cdn/cdn-cloud-service-with-cdn#controller) su come toouse controller in ASP.NET web contenuto tooserve dell'applicazione tramite un URL CDN specifico.




