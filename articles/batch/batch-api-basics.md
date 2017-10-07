---
title: aaaOverview di Azure Batch per gli sviluppatori | Documenti Microsoft
description: "Informazioni su funzionalità hello del servizio Batch hello e le relative API da un punto di vista di sviluppo."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 416b95f8-2d7b-4111-8012-679b0f60d204
ms.service: batch
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3da9d82572b28d05d1923166bd08c26725ca3316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-large-scale-parallel-compute-solutions-with-batch"></a>Sviluppare soluzioni di calcolo parallele su larga scala con Batch

In questa panoramica hello componenti di base del servizio Azure Batch hello, approfondiremo le funzionalità del servizio primario hello e risorse che gli sviluppatori di Batch possono utilizzare paralleli su larga scala toobuild soluzioni di calcolo.

Se si sta sviluppando un'applicazione di elaborazione distribuita o servizio che emette diretto [API REST] [ batch_rest_api] chiamate o si utilizza uno di hello [Batch SDK](batch-apis-tools.md#azure-accounts-for-batch-development), si userà molte delle risorse di hello e le funzionalità descritte in questo articolo.

> [!TIP]
> Per un toohello introduzione livello superiore, il servizio Batch, vedere [nozioni di base di Azure Batch](batch-technical-overview.md).
>
>

## <a name="batch-service-workflow"></a>Flusso di lavoro servizio Batch
Hello seguente flusso di lavoro generale è tipica di quasi tutte le applicazioni e servizi che utilizzano hello Batch per l'elaborazione parallele dei carichi di lavoro:

1. Caricare hello **i file di dati** che si desidera tooprocess tooan [di archiviazione di Azure] [ azure_storage] account. Batch include supporto incorporato per l'accesso all'archiviazione Blob di Azure e le attività è possono scaricare questi file troppo[nodi di calcolo](#compute-node) quando si eseguono attività hello.
2. Caricare hello **file dell'applicazione** che eseguiranno le attività. Questi file possono essere i file binari o gli script e le relative dipendenze e vengono eseguiti dalle attività hello nei processi utente. L'attività è possibile scaricare questi file dall'account di archiviazione oppure è possibile utilizzare hello [pacchetti di applicazioni](#application-packages) funzionalità di Batch per la gestione delle applicazioni e la distribuzione.
3. Creare un [pool](#pool) di nodi di calcolo. Quando si crea un pool, viene specificato il numero di hello dei nodi di calcolo per il pool di hello, le dimensioni e del sistema operativo hello. Quando viene eseguita ogni attività nel processo, viene assegnato tooexecute su uno dei nodi di hello del pool.
4. Creare un [processo](#job). Un processo gestisce una raccolta di attività. Associare ogni processo tooa specifici del pool in cui si eseguiranno le attività del processo.
5. Aggiungere [attività](#task) toohello processo. Ogni attività esegue un'applicazione hello o uno script caricato i file di dati hello tooprocess che il download dall'account di archiviazione. Come completamento di ogni attività, è possibile caricare il tooAzure output archiviazione.
6. Monitorare lo stato del processo e recuperare l'output dell'attività hello dall'archiviazione di Azure.

Hello sezioni seguenti descrivono queste e altre risorse del Batch che consentono di scenario di calcolo distribuito hello.

> [!NOTE]
> È necessario un [account Batch](#account) toouse hello servizio Batch. La maggior parte delle soluzioni Batch usa anche un account di [Archiviazione di Azure][azure_storage] per il recupero e l'archiviazione dei file. Batch supporta attualmente solo hello **generica** tipo di account di archiviazione, come descritto nel passaggio 5 di [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [gli account di archiviazione di Azure su](../storage/common/storage-create-storage-account.md).
>
>

## <a name="batch-service-resources"></a>Risorse del servizio Batch
Alcune delle seguenti risorse, account, hello consente di calcolare i nodi, pool, processi e attività, sono richiesti per tutte le soluzioni che utilizzano il servizio Batch hello. Altre risorse, come le pianificazioni di processi e i pacchetti dell'applicazione, sono funzionalità utili ma facoltative.

* [Account](#account)
* [Nodo di calcolo](#compute-node)
* [Pool](#pool)
* [Processo](#job)

  * [Pianificazioni dei processi](#scheduled-jobs)
* [Attività](#task)

  * [Attività di avvio](#start-task)
  * [Attività di gestione dei processi](#job-manager-task)
  * [Attività di preparazione e rilascio dei processi](#job-preparation-and-release-tasks)
  * [Attività a istanze multiple (MPI)](#multi-instance-tasks)
  * [Dipendenze dell'attività](#task-dependencies)
* [Pacchetti dell'applicazione](#application-packages)

## <a name="account"></a>Account
Un account Batch è un'entità identificata in modo univoco all'interno di hello servizio Batch. Tutte le operazioni di elaborazione sono associata a un account Batch.

È possibile creare un account Azure Batch utilizzando hello [portale di Azure](batch-account-create-portal.md) o a livello di codice, ad esempio con hello [libreria gestione .NET per Batch](batch-management-dotnet.md). Durante la creazione di account hello, è possibile associare un account di archiviazione di Azure.

### <a name="pool-allocation-mode"></a>Modalità di allocazione pool

Quando si crea un account Batch, è possibile specificare in che modo vengono allocati i [pool](#pool) di nodi di calcolo. È possibile scegliere pool tooallocate di nodi di calcolo in una sottoscrizione gestita dal Batch di Azure, oppure è possibile allocare gli oggetti nella propria sottoscrizione. Hello *modalità di allocazione del pool* proprietà per l'account di hello determina in cui vengono allocati i pool. 

toodecide quale pool toouse modalità di allocazione, tenere presente che più adatto al proprio scenario:

* **Batch servizio**: il servizio Batch è hello modalità predefinita per pool allocazione, in cui vengono allocati pool background hello in sottoscrizioni gestito di Azure. Tenere presenti questi punti chiave sulla modalità di allocazione del pool di hello servizio Batch:

    - modalità di allocazione del pool di Hello servizio Batch supporta pool sia il servizio Cloud e la macchina virtuale.
    - modalità di allocazione del pool servizio Batch Hello supporta sia l'autenticazione chiave condivisa o [l'autenticazione di Azure Active Directory](batch-aad-auth.md) (Azure AD). 
    - È possibile utilizzare i nodi di calcolo dedicato o con priorità bassa in pool allocato con la modalità di allocazione del pool di hello servizio Batch.
    - Non utilizzare modalità di allocazione del pool di hello servizio Batch se si prevede di pool di macchine virtuali di Azure toocreate da immagini di macchina virtuale personalizzate, o se si prevede di toouse una rete virtuale. Creare invece l'account con la modalità di allocazione del pool di hello sottoscrizione utente.
    - Pool di macchine virtuali eseguito il provisioning in un account creato con la modalità di allocazione del pool di hello servizio Batch deve essere creato da [macchine virtuali di Azure Marketplace] [ vm_marketplace] immagini.

* **Sottoscrizione utente**: con la modalità di allocazione del pool di sottoscrizione utente hello, pool di Batch vengono allocati nella sottoscrizione di Azure in cui viene creato l'account di hello hello. Tenere presenti questi punti chiave sulla modalità di allocazione del pool di hello sottoscrizione utente:
     
    - modalità di allocazione del pool di Hello sottoscrizione utente supporta solo i pool di macchina virtuale. Non supporta pool di Servizi cloud.
    - pool macchina virtuale toocreate da personalizzati immagini di macchina virtuale o toouse una rete virtuale con il pool di macchina virtuale, è necessario utilizzare modalità di allocazione del pool di hello sottoscrizione utente.  
    - È necessario utilizzare [l'autenticazione di Azure Active Directory](batch-aad-auth.md) con pool allocati nella sottoscrizione utente hello. 
    - Se la modalità di allocazione del pool di hello è impostata tooUser sottoscrizione, è necessario impostare un insieme di credenziali chiave di Azure per l'account Batch. 
    - È possibile utilizzare i nodi di calcolo solo dedicati in pool in un account creato con la modalità di allocazione del pool di hello sottoscrizione utente. I nodi con priorità bassa non sono supportati.
    - È possibile creare un altro pool di macchina virtuale eseguito il provisioning in un account con la modalità di allocazione del pool di hello sottoscrizione utente [macchine virtuali di Azure Marketplace] [ vm_marketplace] immagini o personalizzate immagini che si fornire.

Hello nella tabella seguente confronta hello servizio Batch e sottoscrizione utente pool allocazione modalità.

| **Modalità di allocazione pool**                 | **Servizio Batch**                                                                                       | **Sottoscrizione utente**                                                              |
|-------------------------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| **Posizione di allocazione dei pool**               | Sottoscrizione gestita da Azure                                                                           | sottoscrizione utente Hello in cui hello Batch viene creato l'account                        |
| **Configurazioni supportate**             | <ul><li>Configurazione di tipo servizio cloud</li><li>Configurazione di tipo macchina virtuale (Linux e Windows)</li></ul> | <ul><li>Configurazione di tipo macchina virtuale (Linux e Windows)</li></ul>                |
| **Immagini delle VM supportate**                  | <ul><li>Immagini di Azure Marketplace</li></ul>                                                              | <ul><li>Immagini di Azure Marketplace</li><li>Immagini personalizzate</li></ul>                   |
| **Tipi di nodi di calcolo supportati**         | <ul><li>Nodi dedicati</li><li>Nodi a priorità bassa</li></ul>                                            | <ul><li>Nodi dedicati</li></ul>                                                  |
| **Autenticazione supportata**             | <ul><li>Chiave condivisa</li><li>Azure AD</li></ul>                                                           | <ul><li>Azure AD</li></ul>                                                         |
| **Azure Key Vault necessario**             | No                                                                                                      | Sì                                                                                |
| **Quota core**                           | Determinato dalla quota core del servizio Batch                                                                          | Determinato dalla quota core della sottoscrizione                                              |
| **Supporto per le reti virtuali di Azure** | Pool creati con hello configurazione del servizio Cloud                                                      | Pool creati con hello configurazione della macchina virtuale                               |
| **Modello di distribuzione supportato per le reti virtuali**      | Reti virtuali create con il modello di distribuzione classica                                                             | Reti virtuali create con il modello di distribuzione classica hello o Gestione risorse di Azure |

## <a name="azure-storage-account"></a>Account di archiviazione di Azure

La maggior parte delle soluzioni Batch usa l'Archiviazione di Azure per archiviare i file delle risorse e i file di output.  

Batch supporta attualmente l'unico tipo di account archiviazione generica hello, come descritto nel passaggio 5 di [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [gli account di archiviazione di Azure su](../storage/common/storage-create-storage-account.md). Le attività di Batch, incluse le attività standard, le attività di avvio, le attività di preparazione del processo e le attività di rilascio del processo, devono specificare file di risorse che si trovano negli account di archiviazione per utilizzo generico.


## <a name="compute-node"></a>Nodo di calcolo
Un nodo di calcolo è una macchina virtuale di Azure (VM) o di un servizio cloud VM dedicato tooprocessing una parte del carico di lavoro dell'applicazione. dimensioni Hello di un nodo determinano il numero di hello di core CPU, memoria e dimensioni del file locale system allocata toohello nodo. È possibile creare pool di nodi Windows o Linux con servizi Cloud di Azure, le immagini da hello [macchine virtuali di Azure Marketplace][vm_marketplace], o preparare immagini personalizzate. Vedere l'esempio hello [Pool](#pool) sezione per ulteriori informazioni su queste opzioni.

Nodi possono eseguire qualsiasi file eseguibile o script che è supportato dall'ambiente del sistema operativo hello del nodo hello. inclusi \*.exe, \*.cmd, \*.bat e script di PowerShell per Windows e file binari, shell e script di Python per Linux.

Tutti i nodi di Calcolo in Batch includono anche:

* Una [struttura di cartelle](#files-and-directories) standard e le [variabili di ambiente](#environment-settings-for-tasks) associate disponibili come riferimento per le attività.
* **Firewall** impostazioni che vengono configurate toocontrol accesso.
* [Accesso remoto](#connecting-to-compute-nodes) tooboth Windows (Remote Desktop Protocol (RDP)) e i nodi di Linux (Secure Shell (SSH)).

## <a name="pool"></a>pool
Un pool è una raccolta di nodi in cui viene eseguita l'applicazione. pool Hello possono essere create manualmente dall'utente, o automaticamente da hello servizio Batch quando si specifica toobe lavoro hello eseguita. È possibile creare e gestire un pool che soddisfi i requisiti di risorse hello dell'applicazione. Un pool può essere usato solo dall'account di Batch hello in cui è stato creato. Un account Batch può avere più pool.

Pool di Azure Batch compilate sulla piattaforma di calcolo di Azure hello principale. Forniscono allocazione su larga scala, installare applicazioni, distribuzione dei dati, il monitoraggio dello stato e allineamento flessibile del numero di hello dei nodi di calcolo di un pool ([scalabilità](#scaling-compute-resources)).

Ogni nodo che viene aggiunto tooa pool viene assegnato un nome univoco e un indirizzo IP. Quando un nodo viene rimosso da un pool, le modifiche apportate al file o del sistema operativo toohello vanno perse e il nome e indirizzo IP vengono rilasciati per utilizzi futuri. Quando un nodo esce da un pool, la sua durata è terminata.

Quando si crea un pool, è possibile specificare gli attributi seguenti hello. Alcune impostazioni sono diverse, a seconda della modalità di allocazione del pool di hello di hello Batch [account](#account):

- Versione e sistema operativo dei nodi di calcolo
- Tipo di nodo di calcolo e numero di nodi di destinazione
- Dimensioni dei nodi di calcolo hello
- Criteri di ridimensionamento
- Criteri di pianificazione attività
- Stato delle comunicazioni dei nodi di calcolo
- Attività di avvio per i nodi di calcolo
- Pacchetti dell'applicazione
- Network configuration

Ognuna di queste impostazioni è descritta in dettaglio nelle sezioni che seguono hello.

> [!IMPORTANT]
> Gli account batch creati con la modalità di allocazione del pool servizio Batch hello dispongono di quote predefinito che limita il numero di hello di core in un account Batch. numero di Hello di core corrisponde toohello numero di nodi di calcolo. È possibile trovare le quote predefinite hello e istruzioni su come troppo[aumentare la quota](batch-quota-limit.md#increase-a-quota) in [quote e limiti per il servizio Azure Batch hello](batch-quota-limit.md). Se il pool è non raggiungere il numero di nodi, quota core hello possibile motivo hello.
>
>Gli account batch creati con la modalità di allocazione hello sottoscrizione utente del pool non di osservare le quote del servizio Batch hello. Al contrario, condividono in hello quota core per hello sottoscrizione specificata. Per altre informazioni, vedere [Limiti relativi a Macchine virtuali](../azure-subscription-service-limits.md#virtual-machines-limits) in [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../azure-subscription-service-limits.md).
>
>

### <a name="compute-node-operating-system-and-version"></a>Versione e sistema operativo dei nodi di calcolo

Quando si crea un pool di Batch, è possibile specificare una configurazione di macchina virtuale di Azure hello e il tipo di hello di desiderato toorun in ogni nodo di calcolo nel pool di hello sistema operativo. Hello due tipi di configurazioni disponibili nel Batch sono:

- Hello **configurazione della macchina virtuale**, che consente di specificare il pool di hello è costituito da macchine virtuali di Azure. È possibile creare queste VM da immagini Linux o Windows. 

    Quando si crea un pool in base alle hello configurazione della macchina virtuale, è necessario specificare non solo le dimensioni di hello dei nodi hello e origine hello di hello immagini utilizzate toocreate loro, ma anche hello **riferimento all'immagine di macchina virtuale** hello e Batch **agente nodo SKU** toobe installata nei nodi hello. Per altre informazioni sulla specifica di queste proprietà del pool, vedere [Effettuare il provisioning di nodi di calcolo Linux nei pool di Azure Batch](batch-linux-nodes.md).

- Hello **configurazione di servizi Cloud**, che consente di specificare il pool di hello è costituita da nodi di servizi Cloud di Azure. Servizi cloud fornisce *solo* nodi di calcolo di Windows.

    Sono elencati i sistemi operativi disponibili per i pool di configurazione di servizi Cloud in hello [versioni del sistema operativo Guest Azure e matrice di compatibilità SDK](../cloud-services/cloud-services-guestos-update-matrix.md). Quando si crea un pool che contiene i nodi di servizi Cloud, è necessario toospecify dimensione del nodo hello e il relativo *famiglia di sistemi operativi*. Servizi cloud sono tooAzure distribuito più rapidamente le macchine virtuali che eseguono Windows. Se si vuole disporre di pool di nodi di calcolo di Windows, le prestazioni di Servizi cloud in termini di tempo di distribuzione potrebbero essere migliori.

    * Hello *famiglia di sistemi operativi* determina anche le versioni di .NET installate con hello del sistema operativo.
    * Come con i ruoli di lavoro all'interno di servizi Cloud, è possibile specificare un *versione del sistema operativo* (per ulteriori informazioni sui ruoli di lavoro, vedere hello [ulteriori informazioni sui servizi cloud](../cloud-services/cloud-services-choose-me.md#tell-me-about-cloud-services) sezione hello [servizi Cloud Panoramica](../cloud-services/cloud-services-choose-me.md)).
    * Come con i ruoli di lavoro, è consigliabile specificare `*` per hello *versione del sistema operativo* in modo che i nodi hello vengono aggiornati automaticamente ed non è versioni rilasciate toonewly toocater alcun lavoro richiesto. Hello viene usata principalmente per la selezione di una specifica versione del sistema operativo tooensure compatibilità delle applicazioni, che consente di garantire la compatibilità toobe test eseguite prima di consentire toobe versione hello aggiornato. Dopo la convalida, hello *versione del sistema operativo* per pool hello possono essere aggiornate e può essere installato l'immagine del sistema operativo nuovo hello - tutte le attività in esecuzione vengono interrotti e reinserito nella coda.

Quando si crea un pool, è necessario tooselect hello appropriato **nodeAgentSkuId**, a seconda del sistema operativo di hello dell'immagine di base hello del disco rigido virtuale. È possibile ottenere un mapping del nodo disponibile agente ID SKU tootheir i riferimenti all'immagine del sistema operativo dal chiamante hello [elenco supportato nodo agente SKU](https://docs.microsoft.com/rest/api/batchservice/list-supported-node-agent-skus) operazione.

Vedere hello [Account](#account) sezione per informazioni sull'impostazione di modalità di allocazione del pool di hello quando si crea un account Batch.

#### <a name="custom-images-for-virtual-machine-pools"></a>Immagini personalizzate per pool di macchine virtuali

toouse un pool di macchine virtuali tooprovision immagine personalizzata, creare un account Batch con la modalità di allocazione del pool di hello sottoscrizione utente. In questa modalità, il pool di Batch viene allocato nella sottoscrizione hello in cui risiede l'account di hello. Vedere hello [Account](#account) sezione per informazioni sull'impostazione di modalità di allocazione del pool di hello quando si crea un account Batch.

toouse un'immagine personalizzata, è necessario immagine hello tooprepare generalizzandola. Per informazioni sulla preparazione di immagini personalizzate di Linux da macchine virtuali di Azure, vedere [acquisire toouse una macchina virtuale Linux di Azure come modello](../virtual-machines/linux/capture-image-nodejs.md). Per informazioni sulla preparazione di immagini di Windows personalizzate dalle macchine virtuali di Azure, vedere [Creare immagini personalizzate di VM con Azure PowerShell](../virtual-machines/windows/tutorial-custom-images.md). 

> [!IMPORTANT]
> Quando si prepara un'immagine personalizzata, tenere in seguito hello presente:
> - Garantire che un'immagine del sistema operativo base hello è utilizzare tooprovision i pool di Batch non sia una pre-installato le estensioni di Azure, ad esempio estensione Custom Script hello. Se l'immagine di hello contiene un'estensione di pre-installata, Azure potrebbe verificarsi problemi di distribuzione hello macchina virtuale.
> - Garantire che un'immagine del sistema operativo base hello che fornire utilizza hello unità temporanea predefinita, come hello agente nodo Batch attualmente prevista unità temporanea predefinita di hello.
>
>

toocreate un pool di configurazione della macchina virtuale usando un'immagine personalizzata, è necessario uno o più standard Azure gli account di archiviazione toostore immagini VHD personalizzate. Le immagini personalizzate vengono archiviate come BLOB. tooreference personalizzato immagini quando si crea un pool, specificare l'URI del BLOB VHD immagine personalizzata di hello per hello hello [osDisk](https://docs.microsoft.com/rest/api/batchservice/add-a-pool-to-an-account#bk_osdisk) proprietà di hello [virtualMachineConfiguration](https://docs.microsoft.com/rest/api/batchservice/add-a-pool-to-an-account#bk_vmconf) proprietà.

Verificare che gli account di archiviazione soddisfino hello seguenti criteri:   

- gli account di archiviazione Hello contiene i BLOB VHD immagine personalizzata hello necessario toobe in hello stessa sottoscrizione come hello account Batch (sottoscrizione utente hello).
- Hello specificato gli account di archiviazione necessitano toobe in hello stessa area hello account Batch.
- Attualmente sono supportati solo gli account di archiviazione Standard per utilizzo generico. Archiviazione Premium di Azure sarà supportati in hello future.
- È possibile specificare un account di archiviazione con più BLOB dei dischi rigidi virtuali personalizzati o più account di archiviazione ognuno con un singolo BLOB. È consigliabile toouse più gli account di archiviazione tooget migliori prestazioni.
- Un blob di disco rigido virtuale univoco immagine personalizzata può supportare too40 che istanze VM Linux o 20 istanze di macchina virtuale di Windows. Sarà necessario toocreate copie dei pool di toocreate blob VHD hello con più macchine virtuali. Ad esempio, è necessario un pool con 200 macchine virtuali di Windows 10 BLOB VHD univoco specificato per hello **osDisk** proprietà.

toocreate un pool da un'immagine personalizzata utilizzando hello portale di Azure:

1. Passare l'account Batch tooyour in hello portale di Azure.
2. In hello **impostazioni** blade, seleziona hello **pool** voce di menu.
3. In hello **pool** blade, seleziona hello **Aggiungi** comando; hello **aggiungere pool** pannello verrà visualizzato.
4. Selezionare **immagine personalizzata (Linux/Windows)** da hello **tipo di immagine** elenco a discesa. portale Hello Visualizza hello **immagine personalizzata** selezione. Scegliere uno o più dischi rigidi virtuali da hello stesso hello contenitore e fare clic su **selezionare** pulsante. 
    Verrà aggiunto il supporto per più dischi rigidi virtuali da diversi account di archiviazione e di contenitori diversi in hello future.
5. Seleziona hello corretto **offerta/server di pubblicazione/Sku** per i dischi rigidi virtuali personalizzati, selezionare hello desiderato **la memorizzazione nella cache** modalità, quindi compilare tutti gli altri parametri per il pool di hello di hello.
6. toocheck se un pool è basato su un'immagine personalizzata, vedere hello **del sistema operativo** proprietà nella sezione di riepilogo risorse hello di hello **Pool** blade. il valore di Hello di questa proprietà deve essere **immagine di macchina virtuale personalizzata**.
7. Vengono visualizzati tutti i dischi rigidi virtuali personalizzati associati a un pool nel pool di hello **proprietà** blade.

### <a name="compute-node-type-and-target-number-of-nodes"></a>Tipo di nodo di calcolo e numero di nodi di destinazione

Quando si crea un pool, è possibile specificare quali tipi di nodi di calcolo desiderato e hello numero di destinazione per ognuno. Hello due tipi di nodi di calcolo sono:

- **Nodi di calcolo dedicati.** I nodi di calcolo dedicati sono riservati per i carichi di lavoro. Sono più costosi di nodi con priorità bassa, ma tali toonever essere superata.

- **Nodi di calcolo con priorità bassa.** Nodi con priorità bassa sfruttare surplus della capacità in Azure toorun i carichi di lavoro di Batch. I nodi con priorità bassa hanno un costo orario inferiore a quello dei nodi dedicati e supportano carichi di lavoro che richiedono una potenza di calcolo elevata. Per altre informazioni, vedere [Usare le VM con priorità bassa in Batch](batch-low-pri-vms.md).

    Può verificarsi il superamento dei nodi di calcolo con priorità bassa quando Azure ha capacità in eccesso insufficiente. Se un nodo viene interrotto durante l'esecuzione di attività, attività hello reinserito nella coda ed eseguire nuovamente una volta che un nodo di calcolo diventa nuovamente disponibile. Nodi con priorità bassa sono un'opzione valida per i carichi di lavoro in cui tempo di completamento del processo di hello è flessibile e lavoro hello viene distribuito tra molti nodi. Prima di decidere di nodi con priorità bassa toouse per lo scenario, assicurarsi che qualsiasi lavoro perso a causa di toopreemption sarà toorecreate minima e semplice.

    Nodi di calcolo con priorità bassa sono disponibili solo per gli account Batch creati con la modalità di allocazione del pool di hello impostata troppo**servizio Batch**.

È possibile avere entrambi i nodi di calcolo con priorità bassa e dedicato in hello stesso pool. Ogni tipo di nodo &mdash; con priorità bassa e dedicato &mdash; ha la propria impostazione di destinazione, per cui è possibile specificare il numero di hello desiderato di nodi. 
    
numero di nodi di calcolo Hello è tooas di cui si fa riferimento un *destinazione* perché, in alcuni casi, il pool potrebbe non raggiungere il numero di hello desiderato di nodi. Ad esempio, un pool potrebbe non ottenere destinazione hello raggiunge hello [quota core](batch-quota-limit.md) per il Batch account prima di tutto. In alternativa, il pool di hello potrebbe non raggiungere destinazione hello se è stato applicato un ridimensionamento automatico pool toohello formula che limita hello il numero massimo di nodi.

Per informazioni sui prezzi per i nodi di calcolo dedicati e con priorità bassa, vedere [Prezzi di Batch](https://azure.microsoft.com/pricing/details/batch/).

### <a name="size-of-hello-compute-nodes"></a>Dimensioni dei nodi di calcolo hello

**Cloud Services Configuration** (Configurazione servizi cloud) sono elencate in [Dimensioni dei servizi cloud](../cloud-services/cloud-services-sizes-specs.md). Batch supporta tutte le dimensioni dei servizi cloud tranne `ExtraSmall`, `STANDARD_A1_V2` e `STANDARD_A2_V2`.

Le dimensioni disponibili per i nodi di calcolo **Configurazione macchina virtuale** sono elencate in [Dimensioni delle macchine virtuali in Azure](../virtual-machines/linux/sizes.md) (Linux) e [Dimensioni delle macchine virtuali in Azure](../virtual-machines/windows/sizes.md) (Windows). Batch supporta tutte le dimensioni delle VM di Azure tranne `STANDARD_A0` e quelle con l'archiviazione Premium (serie `STANDARD_GS`, `STANDARD_DS` e `STANDARD_DSV2`).

Quando si seleziona una dimensione del nodo di calcolo, prendere in considerazione le caratteristiche di hello e i requisiti delle applicazioni di hello che viene eseguita nei nodi hello. Aspetti come se l'applicazione hello è multithreading e la quantità di memoria che consuma consente di determinano dimensione del nodo hello più adatto e a costi contenuti. È tipico tooselect una dimensione del nodo presupponendo un'attività verrà eseguita in un nodo alla volta. Tuttavia, è possibile toohave più attività (e pertanto più istanze dell'applicazione) [eseguite in parallelo](batch-parallel-node-tasks.md) in nodi di calcolo durante l'esecuzione del processo. In questo caso, è comune toochoose una maggiore richiesta hello aumentato tooaccommodate di dimensioni nodo dell'esecuzione di attività in parallelo. Per altre informazioni, vedere [Criteri di pianificazione delle attività](#task-scheduling-policy).

Tutti i nodi di hello in un pool sono hello stessa dimensione. Se si intendono toorun applicazioni con requisiti di sistema diversi e/o livelli di carico, è consigliabile utilizzare un pool separato.

### <a name="scaling-policy"></a>Criteri di ridimensionamento

Per i carichi di lavoro dinamici, è possibile scrivere e applicare un [formula di scalabilità automatica](#scaling-compute-resources) tooa pool. periodicamente, Hello servizio Batch restituisce la formula e regola hello numero di nodi all'interno di hello pool in base a diversi pool di processi e i parametri dell'attività che è possibile specificare.

### <a name="task-scheduling-policy"></a>Criteri di pianificazione attività

Hello [numero massimo di attività per ogni nodo](batch-parallel-node-tasks.md) opzione di configurazione determina il numero massimo di hello di attività che possono essere eseguiti in parallelo in ogni nodo di calcolo nel pool di hello.

configurazione predefinita di Hello specifica che un'attività alla volta viene eseguito in un nodo, ma esistono scenari in cui è utile toohave due o più attività eseguite contemporaneamente su un nodo. Vedere hello [nello scenario di esempio](batch-parallel-node-tasks.md#example-scenario) in hello [attività simultanee nodo](batch-parallel-node-tasks.md) toosee articolo come è possibile trarre vantaggio da più attività per ogni nodo.

È inoltre possibile specificare un *tipo di riempimento* che determina se viene distribuita attività hello in modo uniforme in tutti i nodi in un pool di Batch o Pack ogni nodo con il numero massimo di hello di attività prima di assegnare nodo tooanother attività.

### <a name="communication-status-for-compute-nodes"></a>Stato delle comunicazioni dei nodi di calcolo

Nella maggior parte degli scenari, attività funzionano in modo indipendente e non è necessario toocommunicate tra loro. È tuttavia possibile che siano presenti applicazioni in cui le attività devono comunicare, ad esempio negli [scenari MPI](batch-mpi.md).

È possibile configurare un pool tooallow **le comunicazioni**, in modo che i nodi all'interno di un pool possono comunicare in fase di esecuzione. Quando la comunicazione tra nodi è abilitata, i nodi nei pool Cloud Services Configuration (Configurazione servizi cloud) possono comunicare tra loro tramite porte superiori alla 1100 e i pool Configurazione macchina virtuale non limitano il traffico su nessuna porta.

Si noti che anche abilitare le comunicazioni influisce sulla posizione hello dei nodi di hello all'interno dei cluster e potrebbe limitare il numero massimo di hello di nodi in un pool di a causa di restrizioni di distribuzione. Se l'applicazione non richiede la comunicazione tra nodi, hello servizio Batch può allocare un numero potenzialmente elevato di nodi toohello pool dal numero di cluster diversi e i Data Center tooenable maggiore potenza di elaborazione parallela.

### <a name="start-tasks-for-compute-nodes"></a>Attività di avvio per i nodi di calcolo

Hello facoltativo *avviare attività* viene eseguito in ogni nodo come nodo aggiunto pool hello e ogni volta che un nodo viene riavviato o ricreata l'immagine. attività di avvio Hello è particolarmente utile per la preparazione dei nodi di calcolo per l'esecuzione di attività, come l'installazione di applicazioni hello le attività eseguite in nodi di calcolo hello hello.

### <a name="application-packages"></a>Pacchetti dell'applicazione

È possibile specificare [pacchetti di applicazioni](#application-packages) toodeploy toohello nodi di calcolo nel pool di hello. Pacchetti di applicazioni di fornire una distribuzione semplificata e controllo delle versioni delle applicazioni hello le attività eseguite. I pacchetti dell'applicazione specificati per un pool vengono installati in ogni nodo di calcolo aggiunto al pool e ogni volta che un nodo viene riavviato o ne viene ricreata l'immagine.

> [!NOTE]
> I pacchetti dell'applicazione sono supportati in tutti i pool di Batch creati dopo il 5 luglio 2017. Sono supportate nei pool di Batch creato tra 10 marzo 2016 e 5 luglio 2017 solo se il pool di hello è stato creato utilizzando una configurazione del servizio Cloud. Pool di batch creati too10 precedente marzo 2016 non supportano pacchetti di applicazioni. Per ulteriori informazioni sull'utilizzo dell'applicazione pacchetti toodeploy i nodi di Batch tooyour applicazioni, vedere [distribuire applicazioni toocompute nodi con i pacchetti di applicazione di Batch](batch-application-packages.md).
>
>

### <a name="network-configuration"></a>Network configuration

È possibile specificare la subnet hello di un Azure [rete virtuale (VNet)](../virtual-network/virtual-networks-overview.md) nel calcolo del pool che hello nodi devono essere creati. Vedere hello [configurazione di rete Pool](#pool-network-configuration) sezione per ulteriori informazioni.


## <a name="job"></a>Job
Un processo è una raccolta di attività. Gestisce modalità di calcolo per le attività sui nodi di calcolo hello in un pool.

* il processo di Hello specifica hello **pool** in cui hello lavoro è toobe eseguire. È possibile creare un nuovo pool per ogni processo o usare un pool per più processi. È possibile creare un pool per ogni processo associato a una pianificazione o per tutti i processi associati a una pianificazione.
* È possibile specificare una **priorità del processo** facoltativa. Quando un processo viene inviato con una priorità maggiore processi attualmente in corso, attività hello per il processo di priorità più alta hello vengono inserite nella coda hello avanti rispetto all'attività per i processi con priorità inferiore hello. Le attività nei processi con priorità più bassa già in esecuzione non vengono messe in attesa.
* È possibile utilizzare processo **vincoli** toospecify determinati limiti per i processi di:

    È possibile impostare un **tempo massimo wallclock**, in modo che se un processo viene eseguito per più di hello wallclock massima di tempo specificato, il processo di hello e di tutte le attività vengono terminate.

    Batch può rilevare e quindi provare a eseguire di nuovo le attività non riuscite. È possibile specificare hello **il numero massimo di tentativi dell'attività** come vincolo, ad esempio se un'attività è *sempre* o *mai* ripetuta. Nuovo tentativo in corso un'attività, significa che l'attività hello viene reinserito nella coda toobe, eseguire di nuovo.
* L'applicazione client è possibile aggiungere il processo di tooa attività oppure è possibile specificare un [attività di gestione di processi](#job-manager-task). Un'attività di gestione di processi contiene informazioni hello toocreate necessarie attività di hello necessario per un processo, con l'attività del gestore hello processi in esecuzione in uno dei hello nodi di calcolo nel pool di hello. Hello attività di gestione di processi viene gestita in modo specifico dal Batch, viene accodato appena hello processo viene creato e viene riavviato, se si verifica un errore. È un'attività di gestione di processi *obbligatorio* per i processi creati da un [pianificazione del processo](#scheduled-jobs) perché prima viene creata un'istanza di processo hello è hello solo modo toodefine hello le attività.
* Per impostazione predefinita, i processi rimangono in stato attivo di hello quando vengono completate tutte le attività all'interno del processo di hello. È possibile modificare questo comportamento in modo che hello processo viene terminato automaticamente quando vengono completate tutte le attività nel processo di hello. Set hello processo **onAllTasksComplete** proprietà ([OnAllTasksComplete] [ net_onalltaskscomplete] in .NET per Batch) troppo*terminatejob* tooautomatically terminare il processo di hello quando di tutte le attività sono in stato di hello completata.

    Si noti che il servizio Batch hello considera un processo con *non* toohave attività di tutte le attività completate. Di conseguenza, questa opzione viene usata più comunemente con un' [attività del gestore di processi](#job-manager-task). Se si desidera chiusura automatica di processi toouse senza un gestore di processi, è necessario impostare inizialmente un nuovo processo **onAllTasksComplete** proprietà troppo*noaction*, quindi impostare troppo*terminatejob* solo dopo aver completato il processo toohello attività di aggiunta.

### <a name="job-priority"></a>Priorità del processo
È possibile assegnare una priorità toojobs creati in Batch. Hello servizio Batch utilizza il valore di priorità hello dell'ordine di hello processo toodetermine hello della pianificazione dei processi all'interno di un account (non toobe confuso con un [processo pianificato](#scheduled-jobs)). i valori di priorità Hello compresi tra -1000 too1000, con -1000 come priorità più bassa hello e da 1000 hello più alta. priorità di hello tooupdate di un processo, chiamata hello [aggiornare hello le proprietà di un processo] [ rest_update_job] operazione Batch REST (), o modificare hello [CloudJob.Priority] [ net_cloudjob_priority] proprietà (.NET per Batch).

All'interno di hello stesso account, priorità più alta i processi richiedono la programmazione di precedenza tramite i processi a priorità più bassa. Un processo con un valore di priorità più elevato in un account non ha tale precedenza di pianificazione rispetto a un altro processo con un valore di priorità inferiore in un account diverso.

La pianificazione di attività dei pool è indipendente. Tra pool diversi, non è garantito che un processo con priorità più elevato venga pianificato per primo se il relativo pool associato non ha un numero sufficiente di nodi inattivi. In hello stesso pool, i processi con hello stesso livello di priorità hanno la stessa probabilità di pianificazione.

### <a name="scheduled-jobs"></a>Scheduled jobs
[Le pianificazioni di processo] [ rest_job_schedules] consentono toocreate processi ricorrenti all'interno di hello servizio Batch. Un processo di pianificazione specifica quando i processi di toorun e include specifiche hello per hello toobe di processi eseguiti. È possibile specificare per quanto tempo durata hello della pianificazione hello - quando pianificazione hello è attiva, e la frequenza con cui i processi vengono creati durante hello pianificata periodo.

## <a name="task"></a>Attività
Un'attività è un'unità di calcolo che viene associata a un processo e viene eseguita su un nodo. Le attività vengono assegnate tooa nodo per l'esecuzione o vengono messe in coda finché non diventa disponibile un nodo. In termini semplici, un'attività esegue uno o più programmi o script in un calcolo nodo tooperform hello lavoro da svolgere.

Quando si crea un'attività, è possibile specificare:

* Hello **riga di comando** per attività hello. Si tratta di riga di comando di hello che esegue l'applicazione o script nel nodo di calcolo hello.

    È importante toonote che hello riga di comando non viene effettivamente eseguito da una shell. Pertanto, si può in modo nativo usufruire di funzionalità della shell come [variabile di ambiente](#environment-settings-for-tasks) espansione (inclusi hello `PATH`). Il vantaggio di tootake di tali funzionalità, è necessario richiamare shell hello nella riga di comando hello, ad esempio, avviando `cmd.exe` nei nodi di Windows o `/bin/sh` in Linux:

    `cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

    `/bin/sh -c MyTaskApplication $MY_ENV_VAR`

    Se l'attività deve toorun un'applicazione o script che non si trova in hello del nodo `PATH` o fare riferimento a variabili di ambiente, richiamare shell hello in modo esplicito nella riga di comando di hello attività.
* **File di risorse** contenenti hello toobe di dati elaborati. Questi file sono nodo toohello automaticamente copiati dall'archiviazione Blob di un account di archiviazione di Azure generico prima che venga eseguita la riga di comando dell'attività hello. Per ulteriori informazioni, vedere le sezioni hello [attività di avvio](#start-task) e [file e directory](#files-and-directories).
* Hello **le variabili di ambiente** richiesti dall'applicazione. Per ulteriori informazioni, vedere hello [impostazioni di ambiente per l'attività](#environment-settings-for-tasks) sezione.
* Hello **vincoli** in cui hello deve eseguire l'attività. Ad esempio, i vincoli includono il tempo massimo di hello attività hello è consentito toorun, numero massimo di hello di tentativi di un'operazione non riuscita, e hello periodo massimo di tempo che i file nella directory di lavoro dell'attività hello verranno mantenuti.
* **Pacchetti di applicazioni** toodeploy toohello nodo in cui hello è toorun pianificato l'attività di calcolo. [Pacchetti di applicazioni](#application-packages) fornire una distribuzione semplificata e controllo delle versioni delle applicazioni hello le attività eseguite. Pacchetti di applicazioni a livello di attività sono particolarmente utili in ambienti pool condiviso, in cui diversi processi vengono eseguiti in un pool e pool hello non viene eliminato quando un processo viene completato. Se il processo è l'attività più o meno di nodi nel pool di hello, pacchetti di applicazioni di attività possono ridurre al minimo il trasferimento dei dati poiché l'applicazione viene distribuita toohello solo i nodi che eseguono attività.

Inoltre tootasks definire tooperform calcolo in un nodo, hello attività speciali seguenti viene fornita dal servizio Batch hello:

* [Attività di avvio](#start-task)
* [Attività di gestione dei processi](#job-manager-task)
* [Attività di preparazione e rilascio dei processi](#job-preparation-and-release-tasks)
* [Attività a istanze multiple (MPI)](#multi-instance-tasks)
* [Dipendenze dell'attività](#task-dependencies)

### <a name="start-task"></a>Attività di avvio
Associando un **avviare attività** con un pool, è possibile preparare l'ambiente dei relativi nodi operativo hello. Ad esempio, è possibile eseguire azioni come l'installazione di applicazioni hello che eseguono le attività o l'avvio dei processi in background. attività di avvio Hello viene eseguito ogni volta che viene avviato un nodo, purché rimane nel pool di hello - inclusi quando il nodo hello è aggiunto prima toohello pool e quando viene riavviato o ricreata l'immagine.

Il vantaggio principale dell'attività di avvio hello è che può contenere le informazioni di hello che sono necessario tooconfigure un nodo di calcolo e installare applicazioni hello necessari per l'esecuzione dell'attività. Pertanto, è semplice come specificare il conteggio dei nodi hello nuova destinazione aumentando hello numero di nodi in un pool. attività di avvio Hello informazioni hello Batch servizio hello tooconfigure necessari hello nuovi nodi e li prepararsi per l'accettazione delle attività.

Come con qualsiasi attività di Azure Batch, è possibile specificare un elenco di **file di risorse** in [di archiviazione di Azure][azure_storage], inoltre tooa **riga di comando** toobe eseguito. servizio Batch Hello prima copia nodo toohello del file di risorse hello da archiviazione di Azure e quindi viene eseguita sulla riga di comando hello. Per un'attività di avvio del pool, elenco file hello contiene in genere un'applicazione hello attività e le relative dipendenze.

Tuttavia, attività di avvio hello può anche includere toobe di dati di riferimento utilizzato da tutte le attività in esecuzione nel nodo di calcolo hello. Ad esempio, la riga di comando dell'attività di avvio è stato possibile eseguire un `robocopy` attività di avvio operazione toocopy file dell'applicazione (che sono stati specificati come file di risorse e scaricato nodo toohello) da hello [directory di lavoro](#files-and-directories) toohello [cartella condivisa](#files-and-directories), quindi eseguire un file MSI o `setup.exe`.

È in genere consigliabile hello Batch servizio toowait per hello inizio attività toocomplete prima che venga considerato hello attività toobe pronto assegnato nodo, ma è possibile eseguire questa configurazione.

Se un'attività di avvio non riesce in un nodo di calcolo, quindi hello lo stato del nodo hello è aggiornato tooreflect hello errore e tutte le attività non è assegnato il nodo hello. Un'attività di avvio può non riuscire se si verifica un problema copiando i file di risorse di archiviazione, o se il processo di hello eseguito dalla riga di comando restituisce un codice di uscita diverso da zero.

Se si aggiunge o Aggiorna attività di avvio hello per un pool esistente, è necessario riavviare i relativi nodi di calcolo per i nodi toohello hello inizio attività toobe applicato.

>[!NOTE]
> Hello dimensione totale di un'attività di avvio deve essere minore o uguale too32768 caratteri, inclusi i file di risorse e le variabili di ambiente. tooensure che l'attività di avvio soddisfi questo requisito, è possibile utilizzare uno dei due approcci:
>
> 1. È possibile utilizzare applicazioni toodistribute pacchetti di applicazione o i dati in ogni nodo nel pool di Batch. Per ulteriori informazioni sui pacchetti di applicazione, vedere [distribuire applicazioni toocompute nodi con i pacchetti di applicazione di Batch](batch-application-packages.md).
> 2. È possibile creare manualmente un archivio compresso contenente i file delle applicazioni. Caricare l'archiviazione di tooAzure archivio compresso come un blob. Specificare l'archivio hello compresso come un file di risorse per l'attività di avvio. Prima di eseguire la riga di comando hello per le attività di avvio, decomprimere l'archivio di hello dalla riga di comando hello. 
>
>    archivio hello toounzip, è possibile utilizzare l'archiviazione dello strumento di propria scelta hello. Sarà necessario strumento hello tooinclude utilizzare archivio hello toounzip come un file di risorse per attività di avvio hello.
>
>

### <a name="job-manager-task"></a>Attività di gestione dei processi
In genere si usa un **attività di gestione di processi** toocontrol e/o monitoraggio processo di esecuzione, ad esempio, toocreate e inviare attività hello per un processo stabilire toorun attività aggiuntive e come determinare quando lavoro è stato completato. Tuttavia, un'attività di gestione di processi non è limitato toothese attività. È un'attività completamente competente che può eseguire azioni che sono necessari per il processo di hello. Ad esempio, un'attività di gestione di processi potrebbe scaricare un file che viene specificato come parametro, analizzare hello contenuto del file e inviare attività aggiuntive in base a tali contenuti.

Un'attività di gestione dei processi viene avviata prima di tutte le altre attività Fornisce hello seguenti caratteristiche:

* Viene automaticamente inviato come un'attività dall'hello servizio Batch quando viene creato il processo di hello.
* Si è pianificato tooexecute prima hello altre attività in un processo.
* Il nodo associato resta toobe ultimo di hello rimosso da un pool quando il pool di hello è da downsized.
* La terminazione può essere vincolata toohello chiusura di tutte le attività nel processo di hello.
* Un'attività di gestione di processi ha la priorità più alta di hello quando è necessario riavviare toobe. Se un nodo inattivo non è disponibile, hello servizio Batch potrebbe causare uno di hello in hello pool toomake spazio hello processo Gestione attività toorun altre attività in esecuzione.
* Un'attività di gestione di processi in un processo non hanno la priorità rispetto attività hello di altri processi. Tra i processi vengono rispettate solo le priorità a livello di processo.

### <a name="job-preparation-and-release-tasks"></a>Attività di preparazione e rilascio dei processi
Il servizio Batch offre attività di preparazione dei processi per la configurazione dell'esecuzione pre-processo. Le attività di rilascio dei processi vengono usate per manutenzione o pulizia post-processo.

* **Attività di preparazione del processo**: un'attività di preparazione del processo viene eseguito in tutti i nodi di calcolo che sono attività pianificate toorun, prima di qualsiasi hello vengono eseguite altre attività di processo. È possibile utilizzare un processo preparazione toocopy dati dell'attività che viene condivisa da tutte le attività, ma è univoco toohello processo, ad esempio.
* **Attività di rilascio processo**: al termine di un processo, un'attività di rilascio del processo viene eseguito su ogni nodo nel pool di hello eseguita almeno un'attività. È possibile utilizzare una versione attività toodelete dati del processo che viene copiati dall'attività di preparazione processo hello o toocompress e il caricamento dei dati diagnostici log, ad esempio.

Preparazione di entrambi i processi e attività di rilascio consentono di toospecify toorun una riga di comando quando viene richiamata l'attività hello. Le attività offrono funzionalità quali download di file, esecuzione con privilegi elevati, variabili di ambiente personalizzate, durata massima di esecuzione, numero di tentativi e periodo di conservazione dei file.

Per altre informazioni sulle attività di preparazione e rilascio dei processi, vedere [Eseguire attività di preparazione e completamento dei processi nei nodi di calcolo di Azure Batch](batch-job-prep-release.md).

### <a name="multi-instance-task"></a>Attività a istanze multiple
Oggetto [attività multi-istanza](batch-mpi.md) è un'attività che può essere contemporaneamente toorun configurato in più di un nodo di calcolo. Con le attività di più istanze, è possibile abilitare ad alte prestazioni scenari di elaborazione che richiedono un gruppo di nodi di calcolo che sono è allocati insieme tooprocess un carico di lavoro singolo (ad esempio interfaccia MPI (Message Passing)).

Per informazioni dettagliate sull'esecuzione di processi MPI in Batch tramite la libreria .NET di Batch di hello, estrarre [multi-istanza usare attività toorun applicazioni di interfaccia MPI (Message Passing) in Azure Batch](batch-mpi.md).

### <a name="task-dependencies"></a>Dipendenze dell'attività
[Le relazioni tra attività](batch-task-dependencies.md), come hello suggerito dal nome, che consentono di toospecify che un'attività dipende dal completamento di hello di altre attività prima dell'esecuzione. Questa funzionalità fornisce il supporto per le situazioni in cui un'attività "downstream" utilizza l'output di hello di un'attività "upstream", o quando un'attività upstream esegue un'inizializzazione richiesta da un'attività a valle. toouse questa funzionalità, è necessario le dipendenze di attività prima di abilitare il processo Batch. Quindi, per ogni attività che dipende da un altro (o molti altri), è possibile specificare attività hello che dipende da tale attività.

Con le dipendenze di attività, è possibile configurare scenari hello seguente:

* L'*attivitàB* dipende dall'*attivitàA*, ovvero l'esecuzione dell'*attivitàB* inizierà solo dopo il completamento dell'*attivitàA*.
* L'*attivitàC* dipende sia dall'*attivitàA* che dall'*attivitàB*.
* L'*attivitàD* dipende da un intervallo di attività, ad esempio le attività da *1* a *10*, prima che venga eseguita.

Estrarre [attività le dipendenze in Azure Batch](batch-task-dependencies.md) hello e [TaskDependencies] [ github_sample_taskdeps] codice di esempio hello [esempi di azure batch] [ github_samples] Repository GitHub per ulteriori informazioni dettagliate su questa funzionalità.

## <a name="environment-settings-for-tasks"></a>Impostazioni di ambiente per le attività
Ogni attività eseguita dal servizio Batch hello dispone di variabili di tooenvironment di accesso che verrà impostato su nodi di calcolo. Ciò include le variabili di ambiente definite dal servizio Batch hello ([definito dal servizio][msdn_env_vars]) e le variabili di ambiente personalizzato che è possibile definire per le attività. applicazioni Hello e script di che esecuzione delle attività sono variabili di ambiente toothese accesso durante l'esecuzione.

È possibile impostare le variabili di ambiente personalizzate a livello di attività o processo hello popolando hello *le impostazioni di ambiente* proprietà per queste entità. Ad esempio, vedere hello [aggiungere un processo tooa attività] [ rest_add_task] operazione (API REST di Batch) o hello [CloudTask.EnvironmentSettings] [ net_cloudtask_env] e [ CloudJob.CommonEnvironmentSettings] [ net_job_env] proprietà in .NET per Batch.

L'applicazione client o il servizio può ottenere le variabili di ambiente di un'attività, sia definito dal servizio e personalizzate, con hello [ottenere informazioni su un'attività] [ rest_get_task_info] operazione (Batch REST) o l'accesso Hello [CloudTask.EnvironmentSettings] [ net_cloudtask_env] proprietà (.NET per Batch). I processi in esecuzione su un nodo di calcolo possono accedere a queste e altre variabili di ambiente nel nodo hello, ad esempio, tramite hello familiarità `%VARIABLE_NAME%` (Windows) o `$VARIABLE_NAME` sintassi (Linux).

È possibile trovare un elenco completo di tutte le variabili di ambiente definite dal servizio in [Compute node environment variables][msdn_env_vars] (Variabili di ambiente dei nodi di calcolo).

## <a name="files-and-directories"></a>File e directory
Ogni attività ha una *directory di lavoro* in cui crea zero o più file e directory. Directory di lavoro può essere utilizzata per archiviare programma hello eseguito dall'attività hello, dati hello che vengono elaborati, e di output di hello di elaborazione hello che esegue. Tutti i file e directory di un'attività proprietà hello attività utente.

il servizio Batch Hello espone una parte del file system di hello in un nodo come hello *directory radice*. Attività possono accedere a directory radice hello facendo riferimento hello `AZ_BATCH_NODE_ROOT_DIR` variabile di ambiente. Per altre informazioni sull'uso delle variabili di ambiente, vedere [Impostazioni di ambiente per le attività](#environment-settings-for-tasks).

directory radice Hello contiene hello seguente struttura di directory:

![Struttura di directory dei nodi di calcolo][1]

* **condiviso**: la directory fornisce l'accesso in lettura/scrittura troppo*tutti* attività in esecuzione in un nodo. Qualsiasi attività che viene eseguita nel nodo hello è possibile creare, leggere, aggiornare ed eliminare i file in questa directory. Attività di accesso alla directory facendo riferimento hello `AZ_BATCH_NODE_SHARED_DIR` variabile di ambiente.
* **startup**: questa directory viene usata da un'attività di avvio come directory di lavoro. Qui vengono archiviati tutti i file hello che vengono scaricati toohello nodo attività di avvio hello. attività di avvio Hello è possibile creare, leggere, aggiornare ed eliminare i file in questa directory. Attività di accesso alla directory facendo riferimento hello `AZ_BATCH_NODE_STARTUP_DIR` variabile di ambiente.
* **Attività**: viene creata una directory per ogni attività in esecuzione sul nodo hello. È possibile accedervi facendo riferimento hello `AZ_BATCH_TASK_DIR` variabile di ambiente.

    All'interno di ogni directory di attività, hello servizio Batch crea una directory di lavoro (`wd`) il cui percorso univoco specificato da hello `AZ_BATCH_TASK_WORKING_DIR` variabile di ambiente. Questa directory fornisce attività toohello di accesso in lettura/scrittura. attività Hello è possibile creare, leggere, aggiornare ed eliminare i file in questa directory. Questa directory viene mantenuta in base a hello *RetentionTime* vincolo specificato per l'attività hello.

    `stdout.txt`e `stderr.txt`: questi file vengono scritti cartella attività toohello durante l'esecuzione di hello dell'attività hello.

> [!IMPORTANT]
> Quando un nodo viene rimosso dal pool di hello, *tutti* di hello vengono rimossi i file archiviati nel nodo hello.
>
>

## <a name="application-packages"></a>Pacchetti dell'applicazione
Hello [pacchetti di applicazioni](batch-application-packages.md) funzionalità offre semplicità di gestione e distribuzione di applicazioni toohello nodi di calcolo nei pool. È possibile caricare e gestire più versioni di hello applicazioni vengono eseguite le attività, inclusi i relativi file binari e i file di supporto. Quindi è possibile distribuire automaticamente uno o più di queste applicazioni toohello nodi di calcolo nel pool di.

È possibile specificare i pacchetti di applicazioni a livello di pool e attività hello. Quando si specificano i pacchetti di applicazioni del pool, un'applicazione hello è nodo tooevery distribuito nel pool di hello. Quando si specificano i pacchetti di applicazioni di attività, un'applicazione hello è distribuito toonodes solo che vengono pianificati toorun almeno una delle attività del processo di hello, appena prima hello esecuzione riga di comando dell'attività.

Gli handle di batch hello dettagli dell'utilizzo di archiviazione di Azure toostore i pacchetti di applicazioni e distribuirli toocompute nodi, in modo il codice e gestione overhead può essere semplificata.

toofind ulteriori informazioni sulle funzionalità di pacchetto dell'applicazione hello, estrarre [distribuire applicazioni toocompute nodi con i pacchetti di applicazione di Batch](batch-application-packages.md).

> [!NOTE]
> Se si aggiungono pool applicazioni pacchetti tooan *esistente* pool, è necessario riavviare i nodi di calcolo per un'applicazione hello pacchetti nodi toohello toobe distribuito.
>
>

## <a name="pool-and-compute-node-lifetime"></a>Durata del pool e dei nodi di calcolo
Quando si progetta la soluzione di Azure Batch, è toomake una decisione di progettazione su come e quando vengono creati pool e il tempo di calcolo nodi all'interno di tali pool vengono mantenuti disponibili.

A un'estremità dello spettro hello, è possibile creare un pool per ogni processo inviato ed eliminare il pool di hello appena terminata l'esecuzione le relative attività. Ciò Ottimizza l'utilizzo in quanto nodi hello vengono allocati solo quando necessario e arrestato come inattivo. Anche se questo significa che il processo di hello deve attendere hello nodi toobe allocata, è toonote importante che le attività sono pianificate per l'esecuzione non appena sono disponibili singolarmente, i nodi allocato e hello attività di avvio è stata completata. Batch *non* attendere che tutti i nodi all'interno di un pool siano disponibili prima dell'assegnazione attività toohello nodi. assicurando quindi il massimo utilizzo di tutti i nodi disponibili.

In hello estremità dello spettro hello, se i processi di avviare immediatamente è prioritaria hello, è possibile creare un pool di anticipo e rendere disponibili i nodi prima di inviare i processi. In questo scenario, le attività possono iniziare immediatamente, ma durante l'attesa per tali nodi potrebbero rimanere inattive toobe assegnato.

Un approccio combinato viene in genere usato per la gestione di un carico variabile ma continuo. È possibile disporre di un pool che vengono inviati a più processi, ma possono scalare il numero di hello di nodi verso l'alto o verso il basso in base a carico di lavoro toohello (vedere [scalabilità delle risorse di calcolo](#scaling-compute-resources) nella seguente sezione hello). Questa operazione può essere eseguita in modo reattivo in base al carico corrente o in modo proattivo se è possibile prevedere il carico.

## <a name="virtual-network-vnet-and-firewall-configuration"></a>Configurazione della rete virtuale e del firewall 

Quando si esegue il provisioning di un pool di nodi di calcolo di Azure Batch, è possibile associare i pool di hello con una subnet di un Azure [rete virtuale (VNet)](../virtual-network/virtual-networks-overview.md). toolearn informazioni sulla creazione di una rete virtuale con una subnet, vedere [creare una rete virtuale di Azure con subnet](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). 

 * Hello rete virtuale associata a un pool deve essere:

   * In Azure stesso hello **area** come hello account Azure Batch.
   * In hello stesso **sottoscrizione** come hello account Azure Batch.

* tipo di Hello di rete virtuale supportata dipende dal pool da allocare per hello account Batch:

    - Se la modalità di allocazione del pool di hello per l'account Batch è impostata tooBatch servizio, quindi è possibile assegnare un toopools solo tra reti virtuali create con hello **configurazione di servizi Cloud**. Inoltre, hello specificato di che rete virtuale deve essere creata con il modello di distribuzione classica hello. Le reti virtuali create con modello di distribuzione Azure Resource Manager hello non sono supportate.
 
    - Se la modalità di allocazione del pool di hello per l'account Batch è impostata tooUser sottoscrizione, quindi è possibile assegnare un toopools solo tra reti virtuali create con hello **configurazione della macchina virtuale**. I pool creati con hello **configurazione del servizio Cloud** non sono supportati. Hello che rete virtuale associata può essere creato con modello di distribuzione Azure Resource Manager hello o il modello di distribuzione classica hello.

    Per una tabella di riepilogo di supporto di rete virtuale in base a modalità di allocazione toopool, vedere hello [modalità di allocazione del Pool](#pool-allocation-mode) sezione.

* Se la modalità di allocazione del pool di hello per l'account Batch è impostata tooBatch servizio, è necessario fornire le autorizzazioni per hello tooaccess principale di servizio Batch hello rete virtuale. Hello rete virtuale è necessario assegnare hello [Classic Virtual Machine Contributor Role-Based accesso controllo (RBAC)](https://azure.microsoft.com/documentation/articles/role-based-access-built-in-roles/#classic-virtual-machine-contributor) dell'entità servizio di ruolo toohello Batch. Se hello specificato non è stato specificato il ruolo RBAC, il servizio Batch hello restituisce 400 (richiesta non valida). ruolo di hello tooadd in hello portale di Azure:

    1. Seleziona hello **VNet**, quindi **Access control (IAM)** > **ruoli** > **collaboratore alla macchina virtuale**  >  **Aggiungere**.
    2. In hello **aggiungere autorizzazioni** blade, seleziona hello **collaboratore alla macchina virtuale** ruolo.
    3. In hello **aggiungere autorizzazioni** pannello, cercare hello API Batch. Ricerca per ognuna di queste stringhe, a sua volta fino a individuare hello API:
        1. **MicrosoftAzureBatch**.
        2. **Microsoft Azure Batch**. I tenant di Azure AD più recenti potrebbero usare questo nome.
        3. **ddbf3205-c6bd-46ae-8127-60eb93363864** ID hello per hello API Batch. 
    3. Selezionare l'entità di servizio API Batch hello. 
    4. Fare clic su **Salva**.

        ![Assegnare l'entità servizio tooBatch ruolo di collaboratore alla macchina virtuale](./media/batch-api-basics/iam-add-role.png)


* Hello specificato subnet deve essere sufficiente disponibile **gli indirizzi IP** tooaccommodate hello numero totale di nodi di destinazione; vale a dire hello somma di hello `targetDedicatedNodes` e `targetLowPriorityNodes` le proprietà del pool di hello. Se non dispone di subnet hello sufficiente indirizzi IP liberi, hello servizio Batch parzialmente alloca i nodi di calcolo hello nel pool di hello e restituisce un errore di ridimensionamento.

* Hello specificato subnet deve consentire la comunicazione da hello Batch servizio toobe tooschedule in grado di operazioni sui nodi di calcolo hello. Se la comunicazione toohello nodi di calcolo viene negata da un **gruppo di sicurezza (rete)** associato hello rete virtuale, quindi hello servizio Batch Imposta stato hello dei nodi di calcolo hello troppo**inutilizzabile**.

* Se hello specificato di rete virtuale associata **rete sicurezza gruppi** e/o un **firewall**, quindi è necessario abilitare alcune porte di sistema riservato per le comunicazioni in ingresso:

- Per i pool creati con una configurazione di macchina virtuale, abilitare le porte 29876 e 29877, nonché la porta 22 per Linux e la porta 3389 per Windows. 
- Per i pool creati con una configurazione di servizio cloud, abilitare le porte 10100, 20100 e 30100. 
- Abilitare le connessioni in uscita tooAzure archiviazione sulla porta 443. Assicurarsi anche che l'endpoint di Archiviazione di Azure possa essere risolto da qualsiasi server DNS personalizzato che fornisce informazioni alla rete virtuale. In particolare, un URL di form hello `<account>.table.core.windows.net` deve poter essere risolto.

    Hello nella tabella seguente vengono descritti hello porte che è necessario tooenable per pool creati con la configurazione della macchina virtuale hello in ingresso:

    |    Porte di destinazione    |    Indirizzo IP di origine      |    Batch aggiunge gruppi di sicurezza di rete    |    Necessario per la macchina virtuale toobe utilizzabili?    |    Azione dell'utente   |
    |---------------------------|---------------------------|----------------------------|-------------------------------------|-----------------------|
    |    <ul><li>Per i pool creati con la configurazione della macchina virtuale hello: 29876, 29877</li><li>Per i pool creati con la configurazione del servizio cloud hello: 10100, 20100, 30100</li></ul>         |    Solo indirizzi IP del ruolo del servizio Batch |    Sì. Batch aggiunge NSGs hello livello di rete tooVMs di interfacce (NIC) collegate. Questi gruppi di sicurezza di rete consentono il traffico solo dagli indirizzi IP del ruolo del servizio Batch. Anche se si aprono le porte per il web intera hello, traffico hello verrà bloccarsi in hello scheda di rete. |    Sì  |  Non è necessario toospecify un gruppo, in quanto Batch consente solo gli indirizzi IP di Batch. <br /><br /> Se si specifica ugualmente un gruppo di sicurezza di rete, assicurarsi che queste porte siano aperte per il traffico in ingresso. <br /><br /> Se si specifica * come hello nel gruppo IP di origine, Batch aggiunge comunque NSGs a livello di hello del NIC associata tooVMs. |
    |    3389, 22               |    Computer di utenti, utilizzato per il debugging, in modo che è possibile accedere in remoto hello macchina virtuale.    |    No                                    |    No                     |    Aggiungere NSGs se si desidera toohello di accesso remoto (RDP/SSH) toopermit macchina virtuale.   |                 

    Hello nella tabella seguente vengono descritti hello porta di trasmissione che è necessario tooenable toopermit accesso tooAzure archiviazione:

    |    Porte in uscita    |    Destination    |    Batch aggiunge gruppi di sicurezza di rete    |    Necessario per la macchina virtuale toobe utilizzabili?    |    Azione dell'utente    |
    |------------------------|-------------------|----------------------------|-------------------------------------|------------------------|
    |    443    |    Archiviazione di Azure    |    No    |    Sì    |    Se si aggiungono qualsiasi NSGs, verificare che la porta è aperta toooutbound traffico.    |


## <a name="scaling-compute-resources"></a>Ridimensionamento delle risorse di calcolo
Con [il ridimensionamento automatico](batch-automatic-scaling.md), è possibile che il servizio di Batch hello regoli dinamicamente il numero di hello dei nodi di calcolo in un pool in base toohello carico di lavoro e risorse utilizzo corrente del proprio scenario di calcolo. In questo modo è hello toolower costo complessivo dell'esecuzione dell'applicazione utilizzando solo le risorse di hello è necessario, e il rilascio di quelli non necessari.

Per abilitare il ridimensionamento automatico, scrivere una [formula di ridimensionamento automatico](batch-automatic-scaling.md#automatic-scaling-formulas) e associarla a un pool. Hello servizio Batch utilizza hello toodetermine formula hello numero di nodi hello pool per l'intervallo di scala Avanti hello (un intervallo che è possibile configurare). È possibile specificare impostazioni di scalabilità automatica hello per un pool quando viene creato o abilitare la scalabilità in un pool in un secondo momento. È inoltre possibile aggiornare hello scalabilità impostazioni in un pool di scalabilità abilitata.

Ad esempio, ad esempio un processo richiede che si invia un numero molto elevato di toobe attività eseguita. È possibile assegnare un pool toohello formula scalabilità che consente di regolare il numero di hello di nodi nel pool di hello in base a numero corrente di hello di attività in coda e la percentuale di completamento hello di attività hello hello processo. Hello servizio Batch restituisce formula hello e periodicamente Ridimensiona pool hello, in base a carico di lavoro e le altre impostazioni di formule. servizio Hello aggiunge i nodi in base alle esigenze quando sono presenti un numero elevato di attività in coda e rimuove i nodi, quando non sono presenti attività in coda o in esecuzione.

Una formula di scalabilità può essere basata su hello seguenti metriche:

* **Metriche temporali** basate sulle statistiche di raccolti ogni cinque minuti nella hello specificato numero di ore.
* **Metriche delle risorse** : basate su utilizzo di CPU, larghezza di banda, memoria e numero di nodi.
* **Metriche delle attività**: basate sullo stato delle attività, ad esempio *Attiva* (in coda), *In esecuzione* o *Completata*.

Quando la scalabilità automatica riduce il numero di hello dei nodi di calcolo in un pool, è necessario considerare come toohandle attività in esecuzione in fase di hello di hello diminuire l'operazione. tooaccommodate, Batch fornisce un *opzione deallocazione nodo* che è possibile includere nelle formule. Ad esempio, è possibile specificare che le attività in esecuzione interrotta immediatamente, arrestate immediatamente e quindi reinserito nella coda per l'esecuzione in un altro nodo o consentite toofinish prima hello nodo viene rimosso dal pool di hello.

Per altre informazioni sulla scalabilità automatica di un'applicazione, vedere [Ridimensionare automaticamente i nodi di calcolo in un pool di Azure Batch](batch-automatic-scaling.md).

> [!TIP]
> toomaximize utilizzo delle risorse di calcolo, impostare il numero di destinazione hello di nodi toozero alla fine di hello di un processo, ma consentire toofinish attività in esecuzione.
>
>

## <a name="security-with-certificates"></a>Sicurezza con certificati
In genere necessario toouse certificati quando per crittografare o decrittografare informazioni riservate per l'attività, ad esempio hello chiave per un [account di archiviazione Azure][azure_storage]. toosupport, è possibile installare i certificati in nodi. I segreti crittografati vengono passati tootasks tramite i parametri della riga di comando o incorporati in una delle risorse dell'attività hello e certificati hello installato possono essere utilizzato toodecrypt li.

Utilizzare hello [Aggiungi certificato] [ rest_add_cert] operazione (Batch REST) o [CertificateOperations.CreateCertificate] [ net_create_cert] (Batch .NET) (metodo) tooadd tooa un certificato account Batch. È quindi possibile associare il certificato di hello con un pool di nuovo o esistente. Quando un certificato è associato a un pool, hello servizio Batch Installa certificato hello su ogni nodo nel pool di hello. Hello servizio Batch installa certificati appropriati hello all'avvio nodo hello, prima di avviare le attività (attività di avvio hello e attività del gestore processi inclusi).

Se si aggiungono i certificati tooan *esistente* pool, è necessario riavviare i nodi di calcolo per hello certificati nodi toohello toobe applicato.

## <a name="error-handling"></a>Gestione degli errori
Potrebbe essere necessario toohandle errori di attività sia le applicazioni all'interno della soluzione di Batch.

### <a name="task-failure-handling"></a>Gestione degli errori delle attività
Gli errori delle attività rientrano nelle categorie seguenti:

* **Errori di pre-elaborazione**

    Se un'attività non riesce toostart, un errore di pre-elaborazione è impostato per attività hello.  

    Errori di pre-elaborazione può verificarsi se sono stati spostati i file di risorse dell'attività hello, hello account di archiviazione non è più disponibile o si è verificato un altro problema che ha impedito hello corretta copia dei file toohello nodo.

* **Errori di caricamento file**

    Se il caricamento di file specificati per un'attività non riesce per qualsiasi motivo, un errore di caricamento del file è impostato per attività hello.

    Caricamento possono verificarsi errori se hello SAS forniti per l'accesso all'archiviazione di Azure non è valido o non fornisce autorizzazioni di scrittura, se l'account di archiviazione hello non è più disponibile o se un altro problema è stato rilevato che ha impedito hello corretta copia dei file da file nodo Hello.    

* **Errori delle applicazioni**

    processo di Hello specificato dalla riga di comando dell'attività hello può non riuscire. Hello processo viene considerato non riuscito quando viene restituito un codice di uscita diverso da zero dal processo hello che viene eseguita dall'attività hello toohave (vedere *codici di uscita attività* nella sezione successiva hello).

    Per errori dell'applicazione, è possibile configurare Batch attività hello di ripetizione tooautomatically backup tooa numero specificato di volte.

* **Errori relativi ai vincoli**

    È possibile impostare un vincolo che specifica la durata di esecuzione massimo hello per un processo o un'attività, hello *maxWallClockTime*. Questo può essere utile per terminare l'attività che non soddisfano tooprogress.

    Quando viene superata hello periodo di tempo massimo, l'attività hello è contrassegnato come *completato*, ma il codice di uscita hello è impostato troppo`0xC000013A` hello e *schedulingError* campo viene contrassegnato come `{ category:"ServerError", code="TaskEnded"}`.

### <a name="debugging-application-failures"></a>Debug degli errori delle applicazioni
* `stderr` e `stdout`

    Durante l'esecuzione, un'applicazione potrebbe produrre l'output di diagnostica che è possibile utilizzare tootroubleshoot problemi. Come accennato in hello precedente sezione [file e directory](#files-and-directories), hello servizio Batch scrive l'output standard e l'errore standard di output troppo`stdout.txt` e `stderr.txt` file nella directory attività hello in hello nodo di calcolo. È possibile utilizzare hello portale di Azure o uno dei toodownload Batch SDK hello questi file. Ad esempio, è possibile recuperare questi e altri file per la risoluzione dei problemi tramite [ComputeNode.GetNodeFile] [ net_getfile_node] e [CloudTask.GetNodeFile] [ net_getfile_task] nella libreria .NET di Batch hello.

* **Codici di uscita delle attività**

    Come accennato in precedenza, un'attività è contrassegnata come non superato dal servizio Batch hello se processo hello che viene eseguita dall'attività hello restituisce un codice di uscita diverso da zero. Quando un'attività esegue un processo, Batch popola proprietà codice di uscita dell'attività hello con hello *codice del processo di hello restituito*. È importante toonote che il codice di uscita dell'attività è **non** determinato dal servizio Batch hello. Codice di uscita dell'attività è determinato dal processo di hello o sistema operativo hello quale processo hello eseguito.

### <a name="accounting-for-task-failures-or-interruptions"></a>Considerazioni sugli errori o sulle interruzioni delle attività
In alcuni casi, le attività non riescono o vengono interrotte. Hello applicazione attività stessa potrebbe avere esito negativo, potrebbe essere riavviato nodo hello in cui hello attività è in esecuzione o nodo hello potrebbe essere rimossa dal pool hello durante un'operazione di ridimensionamento se i criteri di deallocazione del pool hello sono set di nodi tooremove immediatamente senza attendere attività toofinish. In tutti i casi, attività hello possono essere automaticamente riaccodata dal Batch per l'esecuzione in un altro nodo.

È inoltre possibile per un toocause problema saltuario toohang un'attività o richiedere tooexecute troppo lungo. È possibile impostare l'intervallo di esecuzione massimo hello per un'attività. Se viene superato l'intervallo di esecuzione massimo hello, hello servizio Batch consente di interrompere un'applicazione hello attività.

### <a name="connecting-toocompute-nodes"></a>Connessione di nodi toocompute
È possibile eseguire il debug e risoluzione dei problemi mediante l'accesso in remoto nel nodo di calcolo tooa aggiuntive. È possibile utilizzare hello toodownload portale Azure un file Remote Desktop Protocol (RDP) per i nodi di Windows e ottenere informazioni di connessione Secure Shell (SSH) per i nodi di Linux. È anche possibile farlo usando hello API Batch, ad esempio, con [.NET per Batch] [ net_rdpfile] o [Python Batch](batch-linux-nodes.md#connect-to-linux-nodes-using-ssh).

> [!IMPORTANT]
> nodo di tooa tooconnect tramite RDP o SSH, è necessario creare innanzitutto un utente nel nodo hello. toodo, è possibile utilizzare il portale di Azure, hello [aggiungere un nodo tooa di account utente] [ rest_create_user] tramite hello API REST di Batch, chiamare hello [ComputeNode.CreateComputeNodeUser] [ net_create_user] metodo in .NET per Batch o chiamata hello [add_user] [ py_add_user] metodo hello Batch Python modulo.
>
>

### <a name="troubleshooting-problematic-compute-nodes"></a>Risoluzione dei problemi dei nodi di calcolo
In situazioni in cui alcune attività non vengono superati, hello metadati di hello non è stato possibile attività tooidentify un comportamento errato di un nodo possono essere esaminati l'applicazione client di Batch o il servizio. Ogni nodo in un pool viene assegnato un ID univoco e nodo hello in cui viene eseguita un'attività viene incluso nel hello metadati dell'attività. Dopo avere identificato un "nodo problematico", è possibile intervenire in diversi modi:

* **Riavviare il nodo hello** ([REST][rest_reboot] | [.NET][net_reboot])

    Nodo hello riavviare può talvolta scompaiono latenti problemi come i processi bloccati o bloccati. Si noti che se il pool utilizza un'attività di avvio o il processo utilizza un'attività di preparazione del processo, vengono eseguiti quando il nodo hello viene riavviato.
* **Ricreare l'immagine di nodo hello** ([REST][rest_reimage] | [.NET][net_reimage])

    Consente di reinstallare hello del sistema operativo nel nodo hello. Come per il riavvio di un nodo, avviare le attività e attività di preparazione processo vengono eseguiti nuovamente nodo hello è stata ricreata l'immagine.
* **Rimuovere il nodo hello dal pool di hello** ([REST][rest_remove] | [.NET][net_remove])

    Talvolta è necessario toocompletely Rimuovi nodo di hello dal pool hello.
* **Disabilitare la pianificazione delle attività nel nodo hello** ([REST][rest_offline] | [.NET][net_offline])

    In modo efficace verrà nodo hello offline in modo che nessuna ulteriore attività vengono assegnati tooit, ma consente l'esecuzione di tooremain nodo hello e nel pool di hello. In questo modo si tooperform ulteriore analisi hello causa di errori di hello senza perdita di dati dell'attività non riuscita hello e senza nodo hello causando errori di attività aggiuntive. Ad esempio, è possibile disabilitare pianificazione delle attività nel nodo hello, quindi [accesso remoto](#connecting-to-compute-nodes) tooexamine hello i registri eventi del nodo o eseguire altre risoluzione dei problemi. Dopo aver completato l'analisi, è possibile aprire nuovamente online nodo hello abilitando la pianificazione delle attività ([REST][rest_online] | [.NET] [ net_online]), o eseguire una delle hello altre azioni descritte in precedenza.

> [!IMPORTANT]
> Con ogni azione di cui è descritto in questa sezione, il riavvio, ricreazione dell'immagine, remove e pianificazione delle attività di disattivazione: si è in grado di toospecify come attività attualmente in esecuzione nel nodo hello vengono gestite quando si esegue l'azione di hello. Ad esempio, quando si disabilita pianificazione delle attività in un nodo utilizzando libreria client .NET di Batch di hello, è possibile specificare un [DisableComputeNodeSchedulingOption] [ net_offline_option] toospecify valore di enumerazione se troppo**Terminate** esecuzione delle attività, **riaccodare** per la programmazione in altri nodi, o consentire toocomplete attività in esecuzione prima di eseguire l'azione di hello (**TaskCompletion**).
>
>

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su hello [Batch API e strumenti](batch-apis-tools.md) disponibili per la creazione di soluzioni di Batch.
* Scorrere un'applicazione di Batch di esempio illustrata dettagliatamente [introduzione hello libreria di Azure Batch per .NET](batch-dotnet-get-started.md). È inoltre disponibile un [versione di Python](batch-python-tutorial.md) nodi di calcolo di esercitazione hello che esegue un carico di lavoro in Linux.
* Scaricare e compilare hello [Explorer Batch] [ github_batchexplorer] progetto di esempio per l'utilizzo durante lo sviluppo di soluzioni di Batch. Usando Esplora Batch hello, è possibile eseguire seguente hello e altro ancora:

  * Monitorare e gestire pool, processi e attività nell'account Batch
  * Scaricare `stdout.txt`, `stderr.txt` e altri file dai nodi
  * Creare utenti nei nodi e scaricare i file RDP per l'accesso remoto
* Informazioni su come troppo[creare pool di nodi di calcolo Linux](batch-linux-nodes.md).
* Visitare hello [forum di Azure Batch] [ batch_forum] su MSDN. forum di Hello è una buona inserire domande tooask, se si sta apprendendo o esperti di utilizzo di Batch.

[1]: ./media/batch-api-basics/node-folder-structure.png

[azure_storage]: https://azure.microsoft.com/services/storage/
[batch_forum]: https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch
[cloud_service_sizes]: ../cloud-services/cloud-services-sizes-specs.md
[msmpi]: https://msdn.microsoft.com/library/bb524831.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_sample_taskdeps]:  https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch_net_api]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[msdn_env_vars]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[net_cloudjob_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobmanagertask.aspx
[net_cloudjob_priority]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.priority.aspx
[net_cloudpool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_cloudtask_env]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.environmentsettings.aspx
[net_create_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.createcertificate.aspx
[net_create_user]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.createcomputenodeuser.aspx
[net_getfile_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.getnodefile.aspx
[net_getfile_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.getnodefile.aspx
[net_job_env]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.commonenvironmentsettings.aspx
[net_multiinstancesettings]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_onalltaskscomplete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.onalltaskscomplete.aspx
[net_rdp]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.getrdpfile.aspx
[net_reboot]: https://msdn.microsoft.com/library/azure/mt631495.aspx
[net_reimage]: https://msdn.microsoft.com/library/azure/mt631496.aspx
[net_remove]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.removefrompoolasync.aspx
[net_offline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.disableschedulingasync.aspx
[net_online]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.enableschedulingasync.aspx
[net_offline_option]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.disablecomputenodeschedulingoption.aspx
[net_rdpfile]: https://msdn.microsoft.com/library/azure/Mt272127.aspx
[vnet]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_netconf

[py_add_user]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.ComputeNodeOperations.add_user

[batch_rest_api]: https://msdn.microsoft.com/library/azure/Dn820158.aspx
[rest_add_job]: https://msdn.microsoft.com/library/azure/mt282178.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_cert]: https://msdn.microsoft.com/library/azure/dn820169.aspx
[rest_add_task]: https://msdn.microsoft.com/library/azure/dn820105.aspx
[rest_create_user]: https://msdn.microsoft.com/library/azure/dn820137.aspx
[rest_get_task_info]: https://msdn.microsoft.com/library/azure/dn820133.aspx
[rest_job_schedules]: https://msdn.microsoft.com/library/azure/mt282179.aspx
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx
[rest_multiinstancesettings]: https://msdn.microsoft.com/library/azure/dn820105.aspx#multiInstanceSettings
[rest_update_job]: https://msdn.microsoft.com/library/azure/dn820162.aspx
[rest_rdp]: https://msdn.microsoft.com/library/azure/dn820120.aspx
[rest_reboot]: https://msdn.microsoft.com/library/azure/dn820171.aspx
[rest_reimage]: https://msdn.microsoft.com/library/azure/dn820157.aspx
[rest_remove]: https://msdn.microsoft.com/library/azure/dn820194.aspx
[rest_offline]: https://msdn.microsoft.com/library/azure/mt637904.aspx
[rest_online]: https://msdn.microsoft.com/library/azure/mt637907.aspx

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
