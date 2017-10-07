---
title: aaaImport ed esportare dati in Cache Redis di Azure | Documenti Microsoft
description: Informazioni su come tooand tooimport ed esportazione di dati dall'archiviazione blob con le istanze di Cache Redis di Azure premium
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 4a68ac38-87af-4075-adab-569d37d7cc9e
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: sdanie
ms.openlocfilehash: f17464b207f1c652952f4da63ca147473fee2759
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-data-in-azure-redis-cache"></a>Importare ed esportare dati in Cache Redis di Azure
Importazione/esportazione è un'operazione di gestione dati Cache Redis di Azure, che consente di tooimport dati in Cache Redis di Azure o esportare i dati dalla Cache Redis di Azure mediante importazione ed esportazione di uno snapshot del Database di Cache Redis (RDB) da un blob di tooa cache premium in di Azure Account di archiviazione. 

- **Esportare** -è possibile esportare il tooa di snapshot di Azure Redis Cache RDB Blob di pagine.
- **Importare**: è possibile importare gli snapshot RDB di Cache Redis da un BLOB di pagine o da un BLOB in blocchi.

Importazione/esportazione consente toomigrate tra istanze diverse di Cache Redis di Azure o memorizzare nella cache di hello con i dati prima dell'uso.

In questo articolo viene fornita una Guida per l'importazione ed esportazione di dati con Cache Redis di Azure e vengono fornite le risposte hello toocommonly domande frequenti.

> [!IMPORTANT]
> La funzionalità Importazione/Esportazione è disponibile in anteprima solo per le cache del [piano Premium](cache-premium-tier-intro.md) .
>
>

## <a name="import"></a>Importa
Importazione può essere utilizzati toobring Redis compatibile RDB file da qualsiasi server Redis in esecuzione in qualsiasi cloud o di un ambiente, compresi Redis in esecuzione in Linux, Windows o di qualsiasi provider di cloud come Amazon Web Services e altre. Importazione di dati è un toocreate facilmente una cache con dati pre-popolati. Durante il processo di importazione hello Cache Redis di Azure Carica file RDB hello dall'archiviazione di Azure in memoria e quindi inserisce chiavi hello nella cache di hello.

> [!NOTE]
> Prima di iniziare l'operazione di importazione hello, assicurarsi che il file di Database Redis (RDB) o i file vengono caricati nella pagina o BLOB in blocchi nell'archiviazione di Azure, in hello stessa regione e sottoscrizione come l'istanza di Cache Redis di Azure. Per altre informazioni, vedere [Introduzione all'archivio BLOB di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Se è stato esportato il file RDB utilizzando hello [Azure Redis Cache esportare](#export) funzionalità, il file RDB è già archiviato in un blob di pagine ed è pronto per l'importazione.
>
>

1. tooimport uno o più esportare blob di cache, [Sfoglia cache tooyour](cache-configure.md#configure-redis-cache-settings) in hello portale di Azure e fare clic su **importare dati** da hello **menu risorse**.

    ![Importa dati][cache-import-data]
2. Fare clic su **BLOB contenevano scegliere** e selezionare l'account di archiviazione hello contenente tooimport dati hello.

    ![Scegliere l'account di archiviazione][cache-import-choose-storage-account]
3. Fare clic sul contenitore hello contenente tooimport dati hello.

    ![Scegliere il contenitore][cache-import-choose-container]
4. Selezionare uno o più tooimport BLOB facendo clic a sinistra di toohello area hello del nome blob hello e quindi fare clic su **selezionare**.

    ![Scegliere il BLOB][cache-import-choose-blobs]
5. Fare clic su **importare** toobegin processo di importazione hello.

   > [!IMPORTANT]
   > cache di Hello non è accessibile dai client della cache durante il processo di importazione hello e tutti i dati esistenti nella cache di hello viene eliminati.
   >
   >

    ![Importa][cache-import-blobs]

    È possibile monitorare lo stato di avanzamento hello dell'operazione di importazione hello dalle seguenti notifiche hello dal portale di Azure hello o visualizzando gli eventi di hello in hello [log di controllo](../azure-resource-manager/resource-group-audit.md).

    ![Stato dell'importazione][cache-import-data-import-complete]

## <a name="export"></a>Esporta
Esporta consente dati hello tooexport archiviati nei file di Cache Redis di Azure tooRedis compatibili RDB. È possibile utilizzare i dati da una Cache Redis di Azure istanza tooanother o server Redis tooanother toomove funzionalità. Durante il processo di esportazione hello, viene creato un file temporaneo nella macchina virtuale che ospita hello istanza server di Cache Redis di Azure e file hello è caricato toohello definito account di archiviazione hello. Quando l'operazione di esportazione hello viene completato con stato di esito positivo o negativo, viene eliminato il file temporaneo hello.

1. contenuto corrente di hello tooexport di toostorage cache di hello, [Sfoglia cache tooyour](cache-configure.md#configure-redis-cache-settings) in hello portale di Azure e fare clic su **esportare dati** da hello **menu risorse**.

    ![Scegliere il contenitore di archiviazione][cache-export-data-choose-storage-container]
2. Fare clic su **contenitore di archiviazione scegliere** e selezionare l'account di archiviazione hello desiderato. account di archiviazione Hello deve trovarsi in hello stessa sottoscrizione e regione della cache.

   > [!IMPORTANT]
   > La funzionalità di esportazione è compatibile con i BLOB di pagine, supportati dagli account di archiviazione di Azure Resource Manager e della versione classica ma al momento non supportati dagli [account di archiviazione BLOB](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).
   >
   >

    ![Account di archiviazione][cache-export-data-choose-account]
3. Scegliere hello desiderato contenitore blob e fare clic su **selezionare**. Fare clic su un nuovo contenitore, toouse **Aggiungi contenitore** tooadd prima e quindi selezionare dall'elenco di hello.

    ![Scegliere il contenitore di archiviazione][cache-export-data-container]
4. Digitare un **prefisso del nome Blob** e fare clic su **esportare** toostart processo di esportazione hello. prefisso del nome blob Hello è usato tooprefix hello nomi dei file generati dall'operazione di esportazione.

    ![Esporta][cache-export-data]

    È possibile monitorare lo stato di avanzamento hello dell'operazione di esportazione hello dalle seguenti notifiche hello dal portale di Azure hello o visualizzando gli eventi di hello in hello [log di controllo](../azure-resource-manager/resource-group-audit.md).

    ![Esportazione dei dati completa][cache-export-data-export-complete]

    Cache rimangono disponibili per l'utilizzo durante il processo di esportazione hello.

## <a name="importexport-faq"></a>Domande frequenti su Importazione/Esportazione
In questa sezione contiene domande frequenti sulla funzionalità di importazione/esportazione hello.

* [Con quali piani tariffari è possibile usare Importazione/Esportazione?](#what-pricing-tiers-can-use-importexport)
* [È possibile importare dati da qualsiasi server Redis?](#can-i-import-data-from-any-redis-server)
* [Quali versioni RDB è possibile importare?](#what-rdb-versions-can-i-import)
* [La cache è disponibile durante un'operazione di Importazione/Esportazione?](#is-my-cache-available-during-an-importexport-operation)
* [È possibile usare Importazione/Esportazione con il cluster Redis?](#can-i-use-importexport-with-redis-cluster)
* [Come funziona Importazione/Esportazione con un'impostazione databases personalizzata?](#how-does-importexport-work-with-a-custom-databases-setting)
* [Quali sono le differenze tra la funzionalità Importazione/Esportazione e la persistenza di Redis?](#how-is-importexport-different-from-redis-persistence)
* [È possibile automatizzare la funzionalità Importazione/Esportazione con PowerShell, l'interfaccia della riga di comando o altri client di gestione?](#can-i-automate-importexport-using-powershell-cli-or-other-management-clients)
* [Durante l'operazione di Importazione/Esportazione è stato ricevuto un errore di timeout. Da cosa dipende il problema?](#i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean)
* [Viene visualizzato un errore durante l'esportazione my tooAzure dati nell'archiviazione Blob. Che cosa è successo?](#i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened)

### <a name="what-pricing-tiers-can-use-importexport"></a>Con quali piani tariffari è possibile usare Importazione/Esportazione?
Importazione/esportazione è disponibile solo in tariffario premium hello.

### <a name="can-i-import-data-from-any-redis-server"></a>È possibile importare dati da qualsiasi server Redis?
Sì, inoltre tooimporting dati esportati da istanze di Cache Redis di Azure, è possibile importare file RDB da qualsiasi server Redis in esecuzione in qualsiasi cloud o di un ambiente, ad esempio il provider di cloud come Amazon Web Services, Windows o Linux. toodo questo caricamento hello RDB file dal server Redis hello desiderato in un blob di pagine o in blocchi in un Account di archiviazione di Azure e quindi importandolo, nell'istanza di Cache Redis di Azure premium. È possibile ad esempio, dati hello tooexport dalla cache di produzione e importarlo in una cache utilizzata come parte di un ambiente di gestione temporanea per il test o la migrazione.

> [!IMPORTANT]
> toosuccessfully Importa i dati esportati da server Redis non Cache Redis di Azure quando utilizzando un blob di pagine, hello blob di paging deve essere allineata a un limite di 512 byte. Per esempio codice tooperform le necessarie riempimento byte, vedere [blog il caricamento pagina di esempio](https://github.com/JimRoberts-MS/SamplePageBlobUpload).
> 
> 

### <a name="what-rdb-versions-can-i-import"></a>Quali versioni RDB è possibile importare?

Cache Redis di Azure supporta l'importazione RDB fino alla versione 7.

### <a name="is-my-cache-available-during-an-importexport-operation"></a>La cache è disponibile durante un'operazione di Importazione/Esportazione?
* **Esportare** - cache rimangono disponibili ed è possibile continuare la cache toouse durante un'operazione di esportazione.
* **Importare** - cache diventano non disponibili quando si avvia un'operazione di importazione e rese disponibili per l'uso al termine dell'operazione di importazione hello.

### <a name="can-i-use-importexport-with-redis-cluster"></a>È possibile usare Importazione/Esportazione con il cluster Redis?
Sì. È inoltre possibile usare questa funzionalità tra una cache di cluster e una non di cluster. Poiché il cluster Redis [supporta solo database 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), i dati nei database diversi da 0 non verranno importati. Quando si importano dati di cluster di cache, le chiavi di hello ne vengono ridistribuite tra le partizioni di hello del cluster di hello.

### <a name="how-does-importexport-work-with-a-custom-databases-setting"></a>Come funziona Importazione/Esportazione con un'impostazione databases personalizzata?
Alcuni piani tariffari presentano diversi [database limiti](cache-configure.md#databases), pertanto vi sono alcune considerazioni quando si importa se è stato configurato un valore personalizzato per hello `databases` impostazione durante la creazione della cache.

* Quando si importano tooa tariffario con inferiore `databases` limite a livello di hello da cui vengono esportate:
  * Se si utilizza il numero predefinito di hello di `databases`, vale a dire 16 per tutti i piani tariffari, nessun dato venga perso.
  * Se si utilizza un numero personalizzato di `databases` che si trova all'interno dei limiti di hello per hello livello toowhich si sta importando, nessun dato venga perso.
  * Se i dati esportati contenevano i dati in un database che supera i limiti di hello del nuovo livello di hello, dati hello provenienti da questi database superiore non viene importati.

### <a name="how-is-importexport-different-from-redis-persistence"></a>Quali sono le differenze tra la funzionalità Importazione/Esportazione e la persistenza di Redis?
La persistenza della Cache Redis di Azure consente toopersist dati archiviati in Redis tooAzure archiviazione. Quando si configura la persistenza, Cache Redis di Azure viene mantenuto uno snapshot della cache Redis hello in un toodisk formato binario Redis in base a una frequenza di backup può essere configurata. Se si verifica un errore irreversibile che disabilita hello primario sia della cache di replica, i dati nella cache hello viene ripristinati automaticamente con snapshot più recente di hello. Per ulteriori informazioni, vedere [come tooconfigure persistenza dei dati per una Cache Redis di Azure Premium](cache-how-to-premium-persistence.md).

Importazione / esportazione consente toobring dati o l'esportazione dalla Cache Redis di Azure. ma non di configurare il backup e il ripristino usando la persistenza di Redis.

### <a name="can-i-automate-importexport-using-powershell-cli-or-other-management-clients"></a>È possibile automatizzare la funzionalità Importazione/Esportazione con PowerShell, l'interfaccia della riga di comando o altri client di gestione?
Sì, per PowerShell istruzioni, vedere [tooimport una cache Redis](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) e [tooexport una cache Redis](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).

### <a name="i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean"></a>Durante l'operazione di Importazione/Esportazione è stato ricevuto un errore di timeout. Da cosa dipende il problema?
Se si rimane in hello **importare dati** o **esportare dati** pannello per più di 15 minuti prima di avviare l'operazione di hello, viene visualizzato un errore con un toohello simile messaggio di errore riportato di seguito:

    hello request tooimport data into cache 'contoso55' failed with status 'error' and error 'One of hello SAS URIs provided could not be used for hello following reason: hello SAS token end time (se) must be at least 1 hour from now and hello start time (st), if given, must be at least 15 minutes in hello past.

tooresolve, avviare hello importazione o l'operazione di esportazione prima dello scadere di 15 minuti.

### <a name="i-got-an-error-when-exporting-my-data-tooazure-blob-storage-what-happened"></a>Viene visualizzato un errore durante l'esportazione my tooAzure dati nell'archiviazione Blob. Che cosa è successo?
L'esportazione funziona solo con i file RDB archiviati come BLOB di pagine. Al momento non sono supportati altri tipi di BLOB, inclusi gli account di archiviazione BLOB con livelli di accesso frequente e non frequente. Per altre informazioni, vedere [Account di archiviazione BLOB](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).

## <a name="next-steps"></a>Passaggi successivi
Informazioni su come toouse premium più memorizzano nella cache le funzionalità.

* [Livello di introduzione toohello Premium di Cache Redis di Azure](cache-premium-tier-intro.md)    

<!-- IMAGES -->
[cache-settings-import-export-menu]: ./media/cache-how-to-import-export-data/cache-settings-import-export-menu.png
[cache-export-data-choose-account]: ./media/cache-how-to-import-export-data/cache-export-data-choose-account.png
[cache-export-data-choose-storage-container]: ./media/cache-how-to-import-export-data/cache-export-data-choose-storage-container.png
[cache-export-data-container]: ./media/cache-how-to-import-export-data/cache-export-data-container.png
[cache-export-data-export-complete]: ./media/cache-how-to-import-export-data/cache-export-data-export-complete.png
[cache-export-data]: ./media/cache-how-to-import-export-data/cache-export-data.png
[cache-import-data]: ./media/cache-how-to-import-export-data/cache-import-data.png
[cache-import-choose-storage-account]: ./media/cache-how-to-import-export-data/cache-import-choose-storage-account.png
[cache-import-choose-container]: ./media/cache-how-to-import-export-data/cache-import-choose-container.png
[cache-import-choose-blobs]: ./media/cache-how-to-import-export-data/cache-import-choose-blobs.png
[cache-import-blobs]: ./media/cache-how-to-import-export-data/cache-import-blobs.png
[cache-import-data-import-complete]: ./media/cache-how-to-import-export-data/cache-import-data-import-complete.png
