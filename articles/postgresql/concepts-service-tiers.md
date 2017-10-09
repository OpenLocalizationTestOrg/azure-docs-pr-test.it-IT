---
title: aaa "Piani tariffari nel Database di Azure per PostgreSQL"
description: Piani tariffari in Database di Azure per PostgreSQL
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.custom: mvc
ms.service: postgresql
ms.topic: article
ms.date: 05/31/2017
ms.openlocfilehash: f10389dd2ad1ff04e83b02786a407c10140a007b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-options-and-performance-understand-whats-available-in-each-pricing-tier"></a>Opzioni e prestazioni di Database di Azure per PostgreSQL: funzionalità disponibili in ogni piano tariffario
Quando si crea un Database di Azure per server PostgreSQL, si decide tre opzioni principali risorse hello tooconfigure allocate per il server. Queste scelte impatto sulle prestazioni di hello e la scalabilità del server di hello.
- Piano tariffario 
- Unità di calcolo
- Archiviazione (GB)

Ogni piano tariffario offre una gamma di toochoose (unità di calcolo) i livelli di prestazioni, a seconda dei requisiti di carichi di lavoro. Livelli di prestazioni superiore forniscono risorse aggiuntive per il server toodeliver progettato una velocità effettiva. È possibile modificare il livello di prestazioni del server hello all'interno di un piano tariffario virtualmente senza tempi di inattività dell'applicazione.

> [!IMPORTANT]
> Servizio di hello è in anteprima pubblica, non c'è un accordo di livello di servizio (SLA) garantito.

In un'istanza di Database di Azure per il server PostgreSQL è possibile avere uno o più database. È possibile rifiutare un singolo database per ogni server tooutilize toocreate tutte le risorse di hello o creare più database tooshare risorse hello. 

## <a name="choose-a-pricing-tier"></a>Scegliere un piano tariffario
Nell'anteprima, Database di Azure per PostgreSQL offre due piani tariffari: Basic e Standard. Il piano Premium non è ancora disponibile, ma lo sarà presto. 

Hello nella tabella seguente vengono forniti esempi di hello adatti per carichi di lavoro di applicazioni diverso migliori livelli di prezzo.

| Piano tariffario  | Carichi di lavoro di destinazione |
| :----------- | :----------------|
| Basic | Adatto in particolare a piccoli carichi di lavoro che richiedono livelli di calcolo e archiviazione scalabili senza garanzia di IOPS. Ad esempio, server usati per lo sviluppo o i test oppure applicazioni su scala ridotta usate raramente. |
| Standard | Hello go-toooption per cloud di garantire le applicazioni che necessitano di IOPS con velocità effettiva elevata. Tra gli esempi sono incluse le applicazioni analitiche e Web. |
| Premium | Soluzione ottimale per i carichi di lavoro che richiedono una bassa latenza per transazioni e I/O. Fornisce il supporto migliore hello per molti utenti simultanei. Toodatabases applicabili che supportano applicazioni mission-critical.<br />piano tariffario Premium Hello non è disponibile in anteprima. |

toodecide sui prezzi di un livello, primo avvio determinando se il carico di lavoro richiede una garanzia IOPS. In caso affermativo, scegliere il piano tariffario Standard.

| **Caratteristiche del piano tariffario** | **Basic** | **Standard** |
| :------------------------ | :-------- | :----------- |
| Unità di calcolo massime | 100 | 800 | 
| Archiviazione massima totale | 1 TB | 1 TB | 
| IOPS di archiviazione garantite | N/D  | Sì | 
| Archiviazione IOPS massima | N/D  | 3,000 | 
| Periodo di conservazione dei backup dei database | 7 giorni | 35 giorni | 

Durante l'intervallo di tempo anteprima hello, è possibile modificare il piano tariffario dopo aver creato il server di hello. In futuro hello, verrà tooupgrade possibili o effettuare il downgrade di un server da un livello tooanother piano tariffario.

## <a name="understand-hello-price"></a>Comprendere il prezzo di hello
Quando si crea un nuovo Database di Azure per PostgreSQL all'interno di hello [portale Azure](https://portal.azure.com/#create/Microsoft.PostgreSQLServer), fare clic su hello **tariffario** pannello e hello costo mensile viene visualizzato in base alle opzioni di hello è stato selezionato. Se non si dispone di una sottoscrizione di Azure, utilizzare hello tooget calcolatore dei prezzi Azure un prezzo stimato. Visitare hello [calcolatore dei costi Azure](https://azure.microsoft.com/pricing/calculator/) sito Web, quindi fare clic su **aggiungere elementi**, espandere hello **database** categoria e scegliere **per i Database di Azure PostgreSQL** opzioni hello toocustomize.

## <a name="choose-a-performance-level-compute-units"></a>Scegliere un livello di prestazioni, ovvero le unità di calcolo
Dopo aver determinato hello piano tariffario per il Database di Azure per server PostgreSQL, si è pronti toodetermine livello di prestazioni hello selezionando hello numero di unità di calcolo necessarie. Si può iniziare con 200 e 400 unità di calcolo per le applicazioni che richiedono maggiore concorrenza degli utenti per i propri carichi di lavoro analitici o Web che si regolano in modo regolare in base alle esigenze. 

Calcolo delle unità sono una misura della velocità effettiva di elaborazione della CPU che è garantita tooa disponibili toobe singolo Database di Azure per server PostgreSQL. Un'unità di calcolo è una misura combinata di risorse di CPU e memoria.  Per altre informazioni, vedere [Spiegazione delle unità di calcolo](concepts-compute-unit-and-storage.md)

### <a name="basic-pricing-tier-performance-levels"></a>Livelli di prestazioni del piano tariffario Basic:

| **Livello di prestazioni** | **50** | **100** |
| :-------------------- | :----- | :------ |
| Unità di calcolo massime | 50 | 100 |
| Spazio di archiviazione incluso | 50 GB | 50 GB |
| Spazio di archiviazione del server massimo\* | 1 TB | 1 TB |

### <a name="standard-pricing-tier-performance-levels"></a>Livelli di prestazioni del piano tariffario Standard:

| **Livello di prestazioni** | **100** | **200** | **400** | **800** |
| :-------------------- | :------ | :------ | :------ | :------ |
| Unità di calcolo massime | 100 | 200 | 400 | 800 |
| Spazio di archiviazione e IOPS predisposte inclusi | 125 GB<br/> 375 operazioni di I/O al secondo | 125 GB<br/> 375 operazioni di I/O al secondo | 125 GB<br/> 375 operazioni di I/O al secondo | 125 GB<br/> 375 operazioni di I/O al secondo |
| Spazio di archiviazione del server massimo\* | 1 TB | 1 TB | 1 TB | 1 TB |
| Numero massimo di IOPS predisposte nel server | 3.000 operazioni di I/O al secondo | 3.000 operazioni di I/O al secondo | 3.000 operazioni di I/O al secondo | 3.000 operazioni di I/O al secondo |
| Numero massimo di IOPS predisposte nel server per GB | 3 IOPS fisse per GB | 3 IOPS fisse per GB | 3 IOPS fisse per GB | 3 IOPS fisse per GB |

\*Dimensioni di archiviazione del server max, dimensioni massime di archiviazione sottoposto a provisioning toohello fa riferimento per il server.

## <a name="storage"></a>Archiviazione 
configurazione dell'archiviazione Hello definisce hello di archiviazione capacità disponibile tooan Database di Azure per server PostgreSQL. archiviazione Hello utilizzato dal servizio hello include i file di database hello, log delle transazioni e i registri del server PostgreSQL hello. Prendere in considerazione i database di dimensioni hello di spazio di archiviazione necessario toohost e hello requisiti relativi alle prestazioni (IOPS) quando si seleziona la configurazione di archiviazione hello.

Alcune capacità di archiviazione è incluso almeno con ogni piano tariffario, indicato in hello precedente tabella come "Inclusi delle dimensioni di archiviazione". È possibile aggiungere capacità di archiviazione aggiuntivi quando viene creato il server di hello, in incrementi di 125 GB, di archiviazione massima consentita di toohello. Hello maggiore capacità di archiviazione può essere configurata indipendentemente dalla configurazione di unità di calcolo hello. variazioni di prezzo Hello in base all'ammontare hello di archiviazione selezionato.

configurazione di IOPS Hello in ogni livello di prestazioni relativa toohello piano tariffario e dimensioni di archiviazione hello scelto. Il piano Basic non offre la garanzia relativa alle operazioni di I/O al secondo. All'interno di hello piano tariffario Standard, hello IOPS scala proporzionalmente toomaximum dimensioni di archiviazione in un rapporto 3:1 predefinito. archiviazione Hello incluso garanzie 125 GB per 375 il provisioning di IOPS, ognuno con una dimensione dei / o di too256 KB. È possibile scegliere di ulteriore spazio di archiviazione di massimo TB too1, tooguarantee 3.000 il provisioning di IOPS.

Grafico delle metriche di monitoraggio hello in hello Azure portal o scrittura CLI di Azure comandi toomeasure hello consumo di archiviazione e IOPS. Le metriche pertinenti toomonitor sono limite di archiviazione, percentuale di memoria, spazio di archiviazione usato e percentuale dei / o.

>[!IMPORTANT]
> Mentre è in anteprima, scegliere la quantità hello di archiviazione in fase di hello quando hello server viene creato. Modifica delle dimensioni di archiviazione hello in un server esistente non è ancora supportata. 

## <a name="scaling-a-server-up-or-down"></a>Ridimensionamento di un server
Inizialmente, si sceglie hello prezzi a livello di prestazioni e quando si crea il Database di Azure per PostgreSQL. In un secondo momento, è possibile scalare hello unità di calcolo su o giù in modo dinamico, intervallo hello di hello stesso livello di prezzo. In hello portale di Azure, diapositiva hello unità di calcolo nel Pannello di livello del server hello prezzi o crearne uno script per l'esempio seguente: [monitoraggio e la scala di un singolo server PostgreSQL CLI di Azure](scripts/sample-scale-server-up-or-down.md)

Il ridimensionamento di unità di calcolo hello viene eseguito indipendentemente dalle dimensioni massime di archiviazione hello scelto.

Background hello, modifica il livello di prestazioni hello di un database consente di creare una replica del database originale hello hello nuovo livello di prestazioni e poi passa connessioni toohello replica. Non si perdono dati durante questo processo. Durante hello breve istante quando si passa sulla replica toohello, le connessioni database toohello sono disattivati, possono essere eseguito il rollback alcune transazioni in corso. Questa finestra varia, ma in media è inferiore a 4 secondi e in più del 99% dei casi è inferiore a 30 secondi. Se sono presenti grandi numeri di transazioni in corso in connessioni momento hello sono disabilitati, questa finestra può essere più lunga.

durata Hello del processo di scala intero hello dipende dalla dimensione hello sia piano tariffario del server di hello prima e dopo la modifica di hello. Un server che viene modificata l'unità di calcolo all'interno di hello piano tariffario Standard, ad esempio, deve essere completata entro pochi minuti. Hello nuove proprietà server hello non vengono applicate fino al completamento delle modifiche hello.

## <a name="next-steps"></a>Passaggi successivi
- Per altre informazioni sulle unità di calcolo, vedere [Descrizione delle unità di calcolo](concepts-compute-unit-and-storage.md)
- Informazioni su come troppo[monitoraggio e la scala di un singolo server PostgreSQL CLI di Azure](scripts/sample-scale-server-up-or-down.md)
