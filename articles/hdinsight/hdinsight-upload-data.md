---
title: dati aaaUpload per i processi di Hadoop in HDInsight | Documenti Microsoft
description: Informazioni su come tooupload e accedere ai dati per i processi di Hadoop in HDInsight mediante hello CLI di Azure, Azure Storage Explorer, Azure PowerShell, riga di comando hello Hadoop o Sqoop.
keywords: hadoop etl, recupero dati in hadoop, caricare dati in hadoop
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 56b913ee-0f9a-4e9f-9eaf-c571f8603dd6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: jgao
ms.openlocfilehash: 15da602085d41c19789e34800f3d9e238d7d1de8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a>Caricare dati per processi Hadoop in HDInsight
Azure HDInsight include un'interfaccia completa per il file system HDFS (Hadoop Distributed File System) sull'archivio BLOB di Azure. È progettato come un'estensione HDFS per tooprovide una perfetta riscontrare toocustomers. Abilita set completo di hello dei componenti in hello Hadoop ecosistema toooperate direttamente sui dati di hello che gestisce. L'archivio BLOB di Azure e HDFS sono file system distinti, ottimizzati per l'archiviazione di dati e per l'esecuzione di calcoli su di essi. Per informazioni sui vantaggi di hello di utilizzo dell'archiviazione Blob di Azure, vedere [archiviazione Blob di Azure usare con HDInsight][hdinsight-storage].

**Prerequisiti**

Si noti hello seguente requisito prima di iniziare:

* Disporre di un cluster HDInsight di Azure. Per istruzioni, vedere [Introduzione ad Azure HDInsight][hdinsight-get-started] o [Effettuare il provisioning di cluster Hadoop in HDInsight con opzioni personalizzate][hdinsight-provision].

## <a name="why-blob-storage"></a>Informazioni sull'archivio BLOB
Azure HDInsight cluster sono in genere distribuiti i processi MapReduce toorun e cluster hello vengono eliminati dopo il completamento di tali processi. Conservazione dei dati hello nel cluster HDFS hello al termine di calcoli sarebbe un toostore costoso questi dati. Archiviazione Blob di Azure è un'elevata disponibilità, estremamente scalabile e ad alta capacità, l'opzione di archiviazione basso costo e condivisibile per i dati che viene elaborato tramite HDInsight toobe. L'archiviazione dei dati in un blob consente cluster HDInsight hello che vengono utilizzati per toobe calcolo rilasciato in modo sicuro senza perdita di dati.

### <a name="directories"></a>Directory
I contenitori di archiviazione BLOB archiviano i dati come coppie chiave-valore e non esiste una gerarchia di directory. Tuttavia hello "/" carattere può essere utilizzato all'interno di hello nome della chiave toomake appare come se un file viene archiviato in una struttura di directory. HDInsight le rileva come directory effettive.

Ad esempio, la chiave di un BLOB potrebbe essere *input/log1.txt*. Nessuna directory "input" effettiva esiste, ma a causa di presenza di toohello di hello carattere "/" nel nome della chiave hello sia aspetto hello di un percorso di file.

Per questo motivo, se si usano gli strumenti di esplorazione di Azure, è possibile notare la presenza di file da 0 byte. Questi file servono a due scopi:

* Se sono presenti le cartelle vuote, contrassegnate dell'esistenza di hello della cartella hello. Archiviazione Blob di Azure è sufficientemente appositamente tooknow che se esiste un blob denominato foo/barra, vi sia una cartella denominata **foo**. Ma solo toosignify modo una cartella vuota denominata hello **foo** consiste nel disporre di questo file speciale 0 byte sul posto.
* Contengono metadati speciale che sono necessario per hello Hadoop file system, in particolare le autorizzazioni di hello e proprietari per le cartelle di hello.

## <a name="command-line-utilities"></a>Utilità della riga di comando
Microsoft fornisce hello seguente utilità toowork con archiviazione Blob di Azure:

| Strumento | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Interfaccia della riga di comando di Azure][azurecli] |✔ |✔ |✔ |
| [Azure PowerShell][azure-powershell] | | |✔ |
| [AzCopy][azure-azcopy] | | |✔ |
| [Comando Hadoop](#commandline) |✔ |✔ |✔ |

> [!NOTE]
> Mentre hello CLI di Azure, Azure PowerShell e AzCopy possono tutti essere usato da all'esterno di Azure, hello Hadoop comando è disponibile solo in cluster di HDInsight hello e consente solo il caricamento dei dati da hello file system locale nell'archiviazione Blob di Azure.
>
>

### <a id="xplatcli"></a>
Hello CLI di Azure è uno strumento multipiattaforma consente toomanage Azure servizi. Utilizzare hello archiviazione di Blob tooAzure dati tooupload i passaggi seguenti:

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. [Installare e configurare hello CLI di Azure per Mac, Linux e Windows](../cli-install-nodejs.md).
2. Aprire un prompt dei comandi, bash o altre shell, utilizzare hello seguente tooauthenticate tooyour sottoscrizione di Azure.

        azure login

    Quando richiesto, immettere nome utente hello e una password per la sottoscrizione.
3. Immettere hello comando toolist hello gli account di archiviazione per la sottoscrizione seguente:

        azure storage account list
4. Selezionare l'account di archiviazione hello che contiene il blob hello desiderato toowork con, quindi utilizzare hello chiave hello tooretrieve di comando per l'account di seguito:

        azure storage account keys list <storage-account-name>

    Il comando dovrebbe restituire le chiavi **Primary** e **Secondary**. Hello copia **primario** valore della chiave poiché verrà utilizzato in passaggi successivi hello.
5. Utilizzare hello comando tooretrieve un elenco di contenitori di blob nell'account di archiviazione hello seguenti:

        azure storage container list -a <storage-account-name> -k <primary-key>
6. Utilizzare hello tooupload i comandi seguenti e scaricare file toohello blob:

   * tooupload un file:

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * toodownload un file:

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> Se è sempre possibile lavorare con hello stesso account di archiviazione, è possibile impostare hello seguenti variabili di ambiente invece di specificare account hello e la chiave per ogni comando:
>
> * **AZURE\_archiviazione\_ACCOUNT**: nome account di archiviazione hello
> * **AZURE\_archiviazione\_accesso\_chiave**: chiave account di archiviazione hello
>
>

### <a id="powershell"></a>Azure PowerShell
Azure PowerShell è un ambiente di scripting che è possibile utilizzare toocontrol e automatizzare la distribuzione di hello e la gestione dei carichi di lavoro in Azure. Per informazioni sulla configurazione del toorun workstation Azure PowerShell, vedere [installare e configurare Azure PowerShell](/powershell/azure/overview).

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

**tooupload tooAzure un file locale nell'archiviazione Blob**

1. Console di Azure PowerShell hello aperta come descritto in [installare e configurare Azure PowerShell](/powershell/azure/overview).
2. Impostare i valori hello di hello primi cinque variabili nel hello lo script seguente:

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get hello storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create hello storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy hello file from local workstation toohello Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. Hello Incolla in hello Azure PowerShell console toorun è toocopy hello file script.

Ad esempio PowerShell script creati toowork con HDInsight, vedere [strumenti HDInsight](https://github.com/blackmist/hdinsight-tools).

### <a id="azcopy"></a>AzCopy
AzCopy è uno strumento da riga di comando progettata attività hello toosimplify di trasferimento dei dati in e da un account di archiviazione di Azure. Può essere usato come strumento autonomo o può essere incorporato in un'applicazione esistente. [Download di AzCopy][azure-azcopy-download].

sintassi di AzCopy Hello è:

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

Per altre informazioni, vedere [AzCopy: caricamento/download di file per BLOB di Azure][azure-azcopy].

### <a id="commandline"></a>Riga di comando di Hadoop
riga di comando Hadoop Hello è utile solo per l'archiviazione dei dati nell'archiviazione blob quando i dati di hello sono già presenti nel nodo head del cluster hello.

Hello toouse ordine comando Hadoop, è innanzitutto necessario connettere il nodo head toohello utilizzando uno dei seguenti metodi hello:

* **HDInsight basato su Windows**: [connettersi tramite Desktop remoto](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)
* **HDInsight basati su Linux**: connettersi tramite SSH ([hello comando SSH](hdinsight-hadoop-linux-use-ssh-unix.md) o [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))

Una volta connessi, è possibile utilizzare hello seguente tooupload sintassi toostorage un file.

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

Ad esempio, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`

Poiché hello predefinito file system per HDInsight nell'archiviazione Blob di Azure, /example/data.txt è effettivamente in archiviazione Blob di Azure. È inoltre possibile consultare il file toohello come:

    wasb:///example/data/data.txt

oppure

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

Per un elenco di altri comandi Hadoop che funzionano con i file, vedere [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)

> [!WARNING]
> Nei cluster HBase, dimensione del blocco predefinita hello utilizzato durante la scrittura dei dati è di 256KB. Mentre funziona correttamente quando si utilizza HBase APIs o le API REST, utilizzando hello `hadoop` o `hdfs dfs` dati toowrite comandi superiori a circa 12 GB genera un errore. Vedere hello [eccezione di archiviazione per la scrittura nel blob](#storageexception) sezione riportata di seguito per ulteriori informazioni.
>
>

## <a name="graphical-clients"></a>Client con interfaccia grafica
Esistono diverse applicazioni che forniscono un'interfaccia grafica per usare Archiviazione di Azure. Hello seguito è riportato un elenco di alcune di queste applicazioni:

| Client | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Microsoft Visual Studio Tools per HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |✔ |✔ |✔ |
| [Azure Storage Explorer](http://storageexplorer.com/) |✔ |✔ |✔ |
| [Cloud Storage Studio 2](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |✔ |
| [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) | | |✔ |
| [Azure Explorer](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |✔ |
| [Cyberduck](https://cyberduck.io/) | |✔ |✔ |

### <a name="visual-studio-tools-for-hdinsight"></a>Visual Studio Tools per HDInsight
Per ulteriori informazioni, vedere [risorse collegate Naviga hello](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).

### <a id="storageexplorer"></a>Azure Storage Explorer
*Azure Storage Explorer* è uno strumento utile per analizzare e modificare dati hello nel BLOB. Si tratta di uno strumento gratuito open-source che è possibile scaricare da [http://storageexplorer.com/](http://storageexplorer.com/). codice sorgente Hello è disponibile anche in questo collegamento.

Prima di utilizzare lo strumento di hello, è necessario conoscere la chiave account e nome dell'account di archiviazione di Azure. Per istruzioni su come ottenere queste informazioni, vedere hello "procedura: visualizzazione, copia e l'archiviazione di rigenerare le chiavi di accesso" sezione di [creare, gestire o eliminare un account di archiviazione][azure-create-storage-account].

1. Eseguire Azure Storage Explorer. Se è hello prima volta che è stato eseguito hello Esplora archivi, verrà richiesto di hello **nome dell'account _Storage** e **chiave account di archiviazione**. Se è stata eseguita in precedenza, utilizzare hello **Aggiungi** pulsante tooadd un nuovo nome di account di archiviazione e la chiave.

    Immettere hello nome e chiave per l'account di archiviazione hello utilizzato dal cluster HDInsight e quindi seleziona **Salva e Apri**.

    ![HDI.AzureStorageExplorer][image-azure-storage-explorer]
2. Nell'elenco di hello di sinistra toohello contenitori dell'interfaccia hello, fare clic sul nome hello del contenitore di hello associato al cluster HDInsight. Per impostazione predefinita, questo è il nome di hello del cluster HDInsight hello, ma potrebbe essere diverso se è stato immesso un nome specifico durante la creazione di cluster hello.
3. Dalla barra degli strumenti hello, selezionare l'icona del caricamento hello.

    ![Barra degli strumenti con icona di caricamento evidenziata](./media/hdinsight-upload-data/toolbar.png)
4. Specificare un tooupload di file e quindi fare clic su **aprire**. Quando richiesto, selezionare **caricare** radice toohello del file hello tooupload hello del contenitore dell'archiviazione. Se si desidera tooupload hello tooa specifico percorso, immettere il percorso di hello hello **destinazione** campo, quindi selezionare **caricare**.

    ![Finestra di dialogo di caricamento file](./media/hdinsight-upload-data/fileupload.png)

    Al termine il caricamento di file hello, è possibile utilizzarlo dai processi nel cluster HDInsight hello.

## <a name="mount-azure-blob-storage-as-local-drive"></a>Montare l'archiviazione BLOB di Azure come unità locale
Vedere [Montaggio dell’archiviazione BLOB di Azure come unità locale](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).

## <a name="services"></a>Servizi
### <a name="azure-data-factory"></a>Data factory di Azure
Hello servizio Data Factory di Azure è un servizio completamente gestito per la composizione di servizi dello spostamento dei dati, l'elaborazione dati e archiviazione dati in una pipeline di produzione di dati semplificato, scalabile e affidabile.

Azure Data Factory può essere utilizzato toomove dati nell'archiviazione Blob di Azure o toocreate pipeline di dati che utilizzano direttamente le funzionalità di HDInsight, ad esempio Hive e Pig.

Per ulteriori informazioni, vedere hello [documentazione di Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/).

### <a id="sqoop"></a>Apache Sqoop
Sqoop è di tipo data tootransfer strumento progettato tra Hadoop e database relazionali. È possibile utilizzarlo tooimport dati da un sistema di gestione di database relazionali (RDBMS), ad esempio SQL Server, MySQL o Oracle in hello distributed file system Hadoop (HDFS), la trasformazione dei dati di hello in Hadoop MapReduce o Hive e quindi esportare i dati hello in un RDBMS.

Per altre informazioni, vedere [Usare Sqoop con HDInsight][hdinsight-use-sqoop].

## <a name="development-sdks"></a>SDK di sviluppo
Archiviazione Blob di Azure è possibile accedere utilizzando un SDK di Azure da hello seguenti linguaggi di programmazione:

* .NET
* Java
* Node.js
* PHP
* Python
* Ruby

Per ulteriori informazioni sull'installazione hello Azure SDK, vedere [download di Azure](https://azure.microsoft.com/downloads/)

## <a name="troubleshooting"></a>Risoluzione dei problemi
### <a id="storageexception"></a>Eccezione di archiviazione per la scrittura nel BLOB
**Sintomi**: quando si utilizza hello `hadoop` o `hdfs dfs` comandi toowrite i file che sono ~ 12 GB o superiore in un cluster HBase, che possono verificarsi hello errore seguente:

    ERROR azure.NativeAzureFileSystem: Encountered Storage Exception for write on Blob : example/test_large_file.bin._COPYING_ Exception details: null Error Code : RequestBodyTooLarge
    copyFromLocal: java.io.IOException
            at com.microsoft.azure.storage.core.Utility.initIOException(Utility.java:661)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:366)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:350)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:471)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:745)
    Caused by: com.microsoft.azure.storage.StorageException: hello request body is too large and exceeds hello maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

**Causa**: HBase in HDInsight cluster dimensione del blocco predefinita tooa di 256 KB durante la scrittura di archiviazione tooAzure. Quando questo viene utilizzato per HBase APIs o le API REST, si verificherà un errore quando si utilizza hello `hadoop` o `hdfs dfs` utilità della riga di comando.

**Risoluzione**: utilizzare `fs.azure.write.request.size` toospecify dimensioni maggiori del blocco. È possibile farlo in base all'utilizzo tramite hello `-D` parametro. Hello seguito è riportato un esempio di utilizzo di questo parametro con hello `hadoop` comando:

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

È inoltre possibile aumentare il valore di hello di `fs.azure.write.request.size` a livello globale tramite Ambari. Hello procedura seguente può essere utilizzato il valore di hello toochange nell'interfaccia utente Web Ambari hello:

1. Nel browser passare toohello Ambari Web UI per il cluster. Si tratta di https://CLUSTERNAME.azurehdinsight.net, in cui **CLUSTERNAME** hello nome del cluster.

    Quando richiesto, immettere il nome di amministratore hello e una password per i cluster di hello.
2. Hello il lato sinistro di schermata ciao, selezionare **HDFS**, quindi selezionare hello **configurazioni** scheda.
3. In hello **filtro...**  immettere `fs.azure.write.request.size`. Campo hello e il valore corrente verrà visualizzato al centro hello della pagina hello.
4. Modificare il valore di hello 262144 (256KB) toohello nuovo valore. ad esempio 4194304 (4 MB).

![Immagine della modifica valore hello tramite interfaccia utente Web Ambari](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

Per ulteriori informazioni sull'utilizzo Ambari, vedere [gestione dei cluster HDInsight tramite hello dell'interfaccia utente Web Ambari](hdinsight-hadoop-manage-ambari.md).

## <a name="next-steps"></a>Passaggi successivi
Ora che la modalità di lettura dei dati di tooget in HDInsight, hello seguenti come articoli toolearn tooperform analisi:

* [Introduzione ad Azure HDInsight][hdinsight-get-started]
* [Inviare processi Hadoop a livello di codice][hdinsight-submit-jobs]
* [Usare Hive con HDInsight][hdinsight-use-hive]
* [Usare Pig con HDInsight][hdinsight-use-pig]

[azure-management-portal]: https://porta.azure.com
[azure-powershell]: http://msdn.microsoft.com/library/windowsazure/jj152841.aspx

[azure-storage-client-library]: /develop/net/how-to-guides/blob-storage/
[azure-create-storage-account]:../storage/common/storage-create-storage-account.md
[azure-azcopy-download]:../storage/common/storage-use-azcopy.md
[azure-azcopy]:../storage/common/storage-use-azcopy.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md

[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[sqldatabase-create-configure]: ../sql-database-create-configure.md

[apache-sqoop-guide]: http://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[azurecli]: ../cli-install-nodejs.md


[image-azure-storage-explorer]: ./media/hdinsight-upload-data/HDI.AzureStorageExplorer.png
[image-ase-addaccount]: ./media/hdinsight-upload-data/HDI.ASEAddAccount.png
[image-ase-blob]: ./media/hdinsight-upload-data/HDI.ASEBlob.png
