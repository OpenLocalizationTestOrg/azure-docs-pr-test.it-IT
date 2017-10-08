---
title: aaaUse hello Azure Batch Rendering servizio toorender nel cloud hello | Documenti Microsoft
description: Eseguire il rendering di processi nelle macchine virtuali di Azure direttamente da Maya e con pagamento in base al consumo.
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: tamram
ms.openlocfilehash: 3fb78d883311bbc3ab62743b7d1b111ffad177cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-rendering-service"></a>Introduzione a hello servizio Batch per il Rendering

Hello del servizio per il Rendering di Azure Batch offre funzionalità di rendering a livello di cloud con cadenza pagamento in base all'utilizzo. servizio Batch per il Rendering di Hello gestisce pianificazione dei processi e accodamento, la gestione errori e tentativi e la scalabilità automatica per il processo di rendering. Hello servizio Batch per il Rendering supporta Maya di Autodesk, 3ds Max e vostro giocatore, con supporto per le altre applicazioni sarà presto disponibile. Hello Batch plug-in per Maya 2017 rende facile toostart un processo per il rendering in Azure dalla propria scrivania. 

## <a name="supported-applications"></a>Applicazioni supportate

Hello servizio Batch per il Rendering supporta attualmente hello seguenti applicazioni:

- Autodesk Maya
- Autodesk 3ds Max
- Autodesk Arnold

## <a name="prerequisites"></a>Prerequisiti

servizio Batch per il Rendering di hello toouse, è necessario:

- Un [account Azure](https://azure.microsoft.com/free/). 
- Un **account Azure Batch**. Per istruzioni sulla creazione di un account Batch in hello portale di Azure, vedere [creare un account Batch con il portale di Azure hello](batch-account-create-portal.md).
- Un **account di archiviazione di Azure**. Archiviazione di Azure vengono archiviate le risorse di Hello utilizzati per il processo di rendering. È possibile creare automaticamente un account di archiviazione quando si configura l'account Batch. È possibile anche usare un account di archiviazione esistente. toolearn più sugli account di archiviazione, vedere [come toocreate, gestire o eliminare un account di archiviazione nel portale di Azure hello](https://docs.microsoft.com/azure/storage/storage-create-storage-account).

hello toouse Batch plug-in per Maya, è necessario:

- **Maya 2017**
- **Arnold for Maya**

È inoltre possibile utilizzare hello [portale di Azure](https://portal.azure.com) toocreate pool di macchine virtuali che sono stati preconfigurati con Maya, 3ds Max e vostro giocatore. È possibile utilizzare i processi del portale toomonitor hello e diagnosticare l'attività non riuscite scaricando i registri applicazioni e la connessione in modalità remota le macchine virtuali tooindividual tramite RDP o SSH.

## <a name="basic-batch-concepts"></a>Concetti di base relativi a Batch

Prima di iniziare a utilizzare il servizio di Batch per il Rendering hello, è utile toobe approfondire alcuni concetti di Batch, inclusi i processi, i pool e i nodi di calcolo. informazioni su Azure Batch, in generale, vedere toolearn [eseguire carichi di lavoro intrinsecamente parallele con Batch](batch-technical-overview.md).

### <a name="pools"></a>Pool

Batch è un servizio piattaforma per l'esecuzione di operazioni a elevato utilizzo di calcolo, come il rendering, in un **pool** di **nodi di calcolo**. Ogni nodo di calcolo in un pool è una macchina virtuale di Azure che esegue Linux o Windows. 

Per ulteriori informazioni sui pool di Batch e nodi di calcolo, vedere hello [Pool](batch-api-basics.md#pool) e [del nodo di calcolo](batch-api-basics.md#compute-node) sezioni in [paralleli su larga scala di sviluppare soluzioni con Batch di calcolo](batch-api-basics.md).

### <a name="jobs"></a>Processi

Un Batch **processo** è una raccolta di attività eseguibili su hello nodi di calcolo in un pool. Quando si invia un processo di rendering, Batch divide processo hello in attività e distribuisce i nodi di calcolo toohello attività hello in toorun pool hello.

Per ulteriori informazioni sui processi Batch, vedere hello [processo](batch-api-basics.md#job) sezione [paralleli su larga scala di sviluppare soluzioni con Batch di calcolo](batch-api-basics.md).

## <a name="use-hello-batch-plug-in-for-maya-toosubmit-a-render-job"></a>Utilizzare hello Batch plug-in per Maya toosubmit un processo di rendering

Con hello plug-in per Maya Batch, è possibile inviare toohello un processo Batch per il Rendering servizio direttamente da Maya. Hello le sezioni seguenti descrivono come tooconfigure hello processo da hello plug-in e quindi inviarlo. 

### <a name="load-hello-batch-plug-in-in-maya"></a>Caricare il plug-in di Maya Batch hello

Hello Batch plug-in è disponibile in [GitHub](https://github.com/Azure/azure-batch-maya/releases). Decomprimere hello archivio tooa directory desiderata. È possibile caricare i plug-in hello direttamente da hello *azure_batch_maya* directory.

hello tooload plug-in di Maya:

1. Eseguire Maya.
2. Aprire **Window** (Finestra)  > **Settings/Preferences** (Impostazioni/Preferenze)  > **Plug-in Manager** (Gestione plug-in).
3. Fare clic su **Sfoglia**.
4. Passare selezionare tooand *azure_batch_maya/plug-in/AzureBatch.py*.

### <a name="authenticate-access-tooyour-batch-and-storage-accounts"></a>L'autenticazione degli account di archiviazione e Batch tooyour accesso

hello toouse plug-in, è necessario tooauthenticate usando le chiavi dell'account di archiviazione di Azure e i Batch di Azure. tooretrieve le chiavi dell'account:

1. Plug-in di Maya hello di visualizzazione e seleziona hello **Config** scheda.
2. Passare toohello [portale di Azure](https://portal.azure.com).
3. Selezionare **account Batch** dal menu a sinistra di hello. Se necessario, fare clic su **Altri servizi** e specificare _Batch_ come criterio per il filtro.
4. Individuare l'account Batch hello desiderato nell'elenco di hello.
5. Seleziona hello **chiavi** toodisplay la voce del menu del nome dell'account, URL dell'account e i tasti di scelta:
    - Incollare l'URL dell'account Batch hello in hello **servizio** campo hello plug-in Batch.
    - Nome dell'account Incolla hello in hello **Account Batch** campo.
    - Chiave dell'account primario Incolla hello in hello **chiave Batch** campo.
7. Selezionare gli account di archiviazione dal menu a sinistra di hello. Se necessario, fare clic su **Altri servizi** e specificare _Archiviazione_ come criterio per il filtro.
8. Individuare l'account di archiviazione hello desiderato nell'elenco di hello.
9. Seleziona hello **chiavi di accesso** nome account archiviazione hello toodisplay voce di menu e le chiavi.
    - Nome account di archiviazione Incolla hello in hello **Account di archiviazione** campo hello plug-in Batch.
    - Chiave dell'account primario Incolla hello in hello **chiave di archiviazione** campo.
10. Fare clic su **Authenticate** tooensure che hello plug-in può accedere a entrambi gli account.

Dopo aver eseguito l'autenticazione, set di plug-in hello hello campo status troppo**autenticato**: 

![Autenticare gli account Batch e di archiviazione](./media/batch-rendering-service/authentication.png)

### <a name="configure-a-pool-for-a-render-job"></a>Configurare un pool per un processo di rendering

Dopo avere completato l'autenticazione degli account Batch e di archiviazione, configurare un pool per il processo di rendering. Hello plug-in consente di salvare le selezioni tra le sessioni. Dopo aver impostato la configurazione consigliata, non sarà necessario toomodify, a meno che non viene modificato.

Hello nelle sezioni seguenti vengono illustrano hello sulle opzioni disponibili, disponibile in hello **Invia** scheda:

#### <a name="specify-a-new-or-existing-pool"></a>Specificare un pool nuovo o esistente

toospecify un pool in cui processo di rendering hello toorun, seleziona hello **Invia** scheda. Questa scheda offre opzioni per la creazione di un pool o per la selezione di un pool esistente:

- È possibile **automaticamente il provisioning di un pool per questo processo** (hello. opzione predefinita). Quando si sceglie questa opzione, Batch crea pool hello esclusivamente per il processo corrente di hello e automaticamente eliminazioni hello pool quando il processo di rendering di hello è stata completata. Questa opzione è consigliabile quando si dispone di un toocomplete di rendering singolo processo.
- È possibile scegliere l'opzione **Reuse an existing persistent pool** (Riutilizza un pool persistente esistente). Se si dispone di un pool esistente è inattivo, è possibile specificare tale pool per il processo di rendering hello in esecuzione, selezionarlo dall'elenco a discesa hello. Riutilizzo di un pool esistente permanente Salva hello tempi tooprovision hello pool.  
- È possibile scegliere l'opzione **Create a new persistent pool** (Crea un nuovo pool persistente). Questa opzione Crea un nuovo pool per l'esecuzione del processo di hello. Non elimina il pool di hello quando il processo di hello è completato, in modo che è possibile riutilizzarlo per i processi futuri. Selezionare questa opzione quando si dispone di un toorun continua è necessario eseguire il rendering di processi. Nei successivi processi, è possibile selezionare **riutilizzare un pool esistente permanente** toouse hello permanente pool creato per primo processo hello.

![Specificare il pool, l'immagine del sistema operativo, le dimensioni della VM e la licenza](./media/batch-rendering-service/submit.png)

Per ulteriori informazioni su come delle spese per le macchine virtuali di Azure, vedere hello [domande frequenti sui prezzi di Linux](https://azure.microsoft.com/pricing/details/virtual-machines/linux/#faq) e [domande frequenti sui prezzi di Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/#faq).

#### <a name="specify-hello-os-image-tooprovision"></a>Specificare tooprovision immagine hello del sistema operativo

È possibile specificare il tipo di hello del sistema operativo immagine toouse tooprovision di nodi di calcolo nel pool hello hello **Env** scheda (ambiente). Batch supporta attualmente hello le opzioni di immagine per il rendering dei processi seguenti:

|Sistema operativo  |Image  |
|---------|---------|
|Linux     |Anteprima di Batch CentOS |
|Windows     |Anteprima di Batch Windows |

#### <a name="choose-a-vm-size"></a>Scegliere le dimensioni per la macchina virtuale

È possibile specificare dimensioni VM hello in hello **Env** scheda. Per altre informazioni sulle dimensioni di VM disponibili, vedere [Dimensioni delle macchine virtuali Linux in Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sizes) e [Dimensioni per le macchine virtuali Windows in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes). 

![Specificare l'immagine del sistema operativo VM hello e le dimensioni nella scheda Env hello](./media/batch-rendering-service/environment.png)

#### <a name="specify-licensing-options"></a>Specificare le opzioni di licenza

È possibile specificare licenze hello desiderato toouse su hello **Env** scheda. Le opzioni includono:

- **Maya**, abilitata per impostazione predefinita.
- **Vostro giocatore**, se viene rilevato vostro giocatore come motore di rendering active hello in Maya, cui è abilitata.

 Se si desidera toorender utilizzando la propria licenza, è possibile configurare il punto di fine licenza aggiungendo tabella toohello variabili di ambiente appropriate hello. Essere toodeselect che opzioni di licenza predefinito hello in caso contrario.

> [!IMPORTANT]
> Verrà addebitato per l'utilizzo delle licenze hello durante l'eseguono di macchine virtuali in pool hello, anche se hello macchine virtuali non attualmente in uso per il rendering. tooavoid spese aggiuntive, passare toohello **pool** scheda e ridimensionare i nodi di hello pool too0 finché non si è pronti toorun un altro processo di rendering. 
>
>

#### <a name="manage-persistent-pools"></a>Gestire i pool persistenti

È possibile gestire un pool esistente permanente su hello **pool** scheda. Selezionare un pool dall'elenco di hello Visualizza lo stato corrente di hello del pool di hello.

Da hello **pool** scheda, è anche possibile eliminare il pool di hello e ridimensionare numero hello di macchine virtuali nel pool di hello. È possibile ridimensionare un tooavoid di nodi too0 pool costi tra i carichi di lavoro.

![Visualizzare, ridimensionare ed eliminare i pool](./media/batch-rendering-service/pools.png)

### <a name="configure-a-render-job-for-submission"></a>Configurare un processo di rendering per l'invio

Dopo aver specificato i parametri di hello per pool hello che verrà eseguito il processo di rendering hello, configurare il processo hello stesso. 

#### <a name="specify-scene-parameters"></a>Specificare i parametri della scena

Hello Batch plug-in rileva il motore di rendering che si sta utilizzando Maya e consente di visualizzare hello appropriato, eseguire il rendering impostazioni hello **Invia** scheda. Queste impostazioni includono fotogramma iniziale hello, frame di fine, prefisso di output e il passaggio di frame. È possibile sostituire le impostazioni di rendering hello scena file specificando impostazioni diverse in hello plug-in. Le modifiche apportate toohello Impostazioni plug-in non sono le impostazioni di rendering file scena toohello back persistente, pertanto è possibile apportare modifiche con cadenza dal processo di lavoro senza la necessità di file di scena tooreupload hello.

plug-in Hello Avvisa se hello motore selezionato in Maya di rendering non è supportata.

Se si carica una nuova scena mentre hello plug-in è aperto, fare clic su hello **aggiornamento** pulsante toomake che hello impostazioni sono state aggiornate.

#### <a name="resolve-asset-paths"></a>Risolvere i percorsi degli asset

Quando si carica hello plug-in, analizza il file di scena hello per eventuali riferimenti a file esterni. Questi riferimenti vengono visualizzati in hello **asset** scheda. Se un percorso a cui fa riferimento non può essere risolto, hello plug-in prova file hello toolocate in alcuni percorsi predefiniti, tra cui:

- percorso di Hello del file di scena hello 
- del progetto corrente Hello _sourceimages_ directory
- directory di lavoro corrente Hello. 

Se l'asset hello ancora non viene trovato, viene elencato con un'icona di avviso:

![Gli asset mancanti vengono visualizzati con un'icona di avviso](./media/batch-rendering-service/missing_assets.png)

Se si conosce il percorso di hello di un riferimento di file non risolto, è possibile fare clic su hello avviso icona toobe richiesto tooadd un percorso di ricerca. Hello plug-in quindi utilizza questo tooresolve tooattempt percorso di ricerca di tutte le risorse mancante. È possibile aggiungere qualsiasi numero di percorsi di ricerca aggiuntivi.

Quando viene risolto, il riferimento viene elencato con un'icona di colore verde chiaro:

![Asset risolti con icona di colore verde chiaro](./media/batch-rendering-service/found_assets.png)

Se la scena richiede altri file che hello plug-in non è stata rilevata, è possibile aggiungere altri file o directory. Hello utilizzare **Aggiungi file** e **Aggiungi Directory** pulsanti. Se si carica una nuova scena mentre hello plug-in è aperto, essere tooclick che **aggiornamento** riferimenti tooupdate hello scena.

#### <a name="upload-assets-tooan-asset-project"></a>Carica progetto di risorse tooan asset

Quando si invia un processo di rendering, hello a cui fa riferimento di file visualizzati nel hello **asset** scheda vengono caricati automaticamente tooAzure archiviazione come un progetto di asset. È anche possibile caricare il file di asset hello in modo indipendente da un processo di rendering, utilizzando hello **caricare** pulsante hello **asset** scheda hello asset progetto nome è specificato in hello **progetto**campo ed è denominato dopo progetto Maya corrente hello per impostazione predefinita. Quando vengono caricati i file di asset, viene mantenuta la struttura di file locale hello. 

Dopo il caricamento, qualsiasi processo di rendering può fare riferimento agli asset. Tutte le risorse caricate sono disponibili tooany processo che fa riferimento a progetto asset hello, queste vengono incluse nella scena hello o meno. progetto di asset hello toochange a cui fa riferimento il processo successivo, modifica nome hello in hello **progetto** campo hello **asset** scheda. Se sono presenti file di riferimento che si desidera tooexclude carichino, deselezionarli utilizzando il pulsante hello verde accanto a elenco hello.

#### <a name="submit-and-monitor-hello-render-job"></a>Inviare e hello monitoraggio processo di rendering.

Dopo aver configurato il processo di rendering hello in hello plug-in, fare clic su hello **processo inviare** pulsante hello **Invia** scheda toosubmit hello processo tooBatch:

![Inviare il processo di rendering hello](./media/batch-rendering-service/submit_job.png)

È possibile monitorare un processo in corso da hello **processi** scheda hello plug-in. Selezionare un processo da hello elenco toodisplay hello stato corrente del processo di hello. È inoltre possibile utilizzare toocancel questa scheda ed eliminare i processi, nonché gli output di hello toodownload e il rendering di log. 

toodownload output, modificare hello **restituisce** directory di destinazione desiderato di campo tooset hello. Fare clic su toostart di icona a forma di ingranaggio hello che controlla il processo di hello e scarica output man mano che passa un processo in background: 

![Visualizzare lo stato del processo e scaricare gli output](./media/batch-rendering-service/jobs.png)

È possibile chiudere Maya senza interrompere il processo di download di hello.

## <a name="next-steps"></a>Passaggi successivi

toolearn ulteriori informazioni sui Batch, vedere [eseguire carichi di lavoro intrinsecamente parallele con Batch](batch-technical-overview.md).
