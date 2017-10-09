---
title: aaaUse PowerShell tooget avviato con l'archivio Azure Data Lake | Documenti Microsoft
description: Usare Azure PowerShell toocreate un account archivio Data Lake ed eseguire operazioni di base
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 9c958bfd63e412ec0b0a4113a149f61aee026bc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a>Introduzione all'archivio Azure Data Lake mediante Azure PowerShell
> [!div class="op_single_selector"]
> * [Portale](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [SDK per Java](data-lake-store-get-started-java-sdk.md)
> * [API REST](data-lake-store-get-started-rest-api.md)
> * [Interfaccia della riga di comando di Azure 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Informazioni sulla modalità di memorizzazione una Data Lake di Azure di toouse Azure PowerShell toocreate account e di eseguire operazioni di base, ad esempio creare cartelle, caricare e scaricare file di dati, eliminare l'account, e così via. Per altre informazioni su Data Lake Store, vedere [Panoramica di Data Lake Store](data-lake-store-overview.md).

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, è necessario disporre delle seguenti hello:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 o versioni successive**. Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

## <a name="authentication"></a>Autenticazione
In questo articolo utilizza un approccio più semplice di autenticazione con archivio Data Lake in cui ti trovi tooenter richieste le credenziali dell'account Azure. Hello accesso livello tooData Lake archivio account file system e quindi è disciplinato dal livello di accesso hello di hello utente connesso. Tuttavia, esistono altri approcci come ben tooauthenticate con archivio Data Lake, che sono **autenticazione dell'utente finale** o **authentication service to service**. Per istruzioni e ulteriori informazioni su come tooauthenticate, vedere [autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md) o [authentication Service to service](data-lake-store-authenticate-using-active-directory.md).

## <a name="create-an-azure-data-lake-store-account"></a>Creare un account di Azure Data Lake Store
1. Dal desktop, aprire una nuova finestra di Windows PowerShell e immettere hello seguente frammento di codice toolog in tooyour account Azure, impostare la sottoscrizione hello e registrare il provider di archivio Data Lake hello. Quando richiesto toolog, assicurarsi che si accede con uno dei hello admininistrators/proprietario della sottoscrizione:

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. Un account di Archivio Azure Data Lake è associato a un gruppo di risorse di Azure. Per iniziare, creare un gruppo di risorse di Azure.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    ![Creare un gruppo di risorse di Azure](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")
3. Creare un account Archivio Azure Data Lake. specificare nome Hello deve contenere solo lettere minuscole e numeri.

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    ![Creare un account di Azure Data Lake Store](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")
4. Verificare che account hello è stato creato correttamente.

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    deve trattarsi di output di Hello **True**.

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a>Creare strutture di directory in Azure Data Lake Store
È possibile creare le directory sotto la toomanage account archivio Azure Data Lake e archiviare i dati.

1. Specificare una directory radice.

        $myrootdir = "/"
2. Creare una nuova directory denominata **mynewdirectory** sotto la radice specificata hello.

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. Verificare che la nuova directory hello viene creata correttamente.

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    Dovrebbe visualizzare un output simile hello seguente:

    ![Verificare la directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")

## <a name="upload-data-tooyour-azure-data-lake-store"></a>Caricare l'archivio dati tooyour Azure Data Lake
È possibile caricare l'archivio data Lake di tooData direttamente in hello livello o tooa directory radice che è stato creato all'interno di account hello. Hello i frammenti di codice riportato di seguito viene illustrato come tooupload alcune directory toohello dati di esempio (**mynewdirectory**) creata nella sezione precedente hello.

Se si sta cercando alcuni tooupload di dati di esempio, è possibile ottenere hello **dati ambulanza** cartella hello [Git Repository di Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData). Scaricare il file hello e archiviarlo in una directory locale nel computer in uso, ad esempio C:\sampledata\.

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a>Rinominare, scaricare ed eliminare i dati da Data Lake Store
toorename un file, utilizzare hello comando seguente:

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

toodownload un file, utilizzare hello comando seguente:

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

toodelete un file, utilizzare hello comando seguente:

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

Quando richiesto, immettere **Y** elemento hello toodelete. Se si dispone di più di un file toodelete, è possibile fornire tutti i percorsi di hello separati da virgola.

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a>Eliminare l'account di Azure Data Lake Store
Utilizzare hello comando che segue toodelete account archivio Data Lake.

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

Quando richiesto, immettere **Y** account hello toodelete.

## <a name="performance-guidance-while-using-powershell"></a>Linee guida sulle prestazioni durante l'uso di PowerShell

Di seguito è hello impostazioni più importanti che possono essere ottimizzate tooget hello ottenere prestazioni ottimali durante l'utilizzo di PowerShell toowork con archivio Data Lake:

| Proprietà            | Default | Descrizione |
|---------------------|---------|-------------|
| PerFileThreadCount  | 10      | Questo parametro consente di numero di hello toochoose di thread paralleli per caricare o scaricare ciascun file. Questo numero rappresenta i thread max hello che possono essere allocati per ogni file, ma è possibile ottenere meno thread a seconda dello scenario (ad esempio, se si sta caricando un file di 1 KB, si otterrà un thread anche se richiede di 20 thread).  |
| ConcurrentFileCount | 10      | Questo parametro viene usato specificamente per il caricamento e il download delle cartelle. Questo parametro determina il numero di hello di file simultanei che possono essere caricate o scaricate. Questo numero rappresenta hello il numero massimo di file simultanei che possono essere caricati o scaricati in una sola volta, ma è possibile ottenere inferiore di concorrenza a seconda dello scenario (ad esempio, se si siano caricando due file, si otterranno due caricamenti di file simultanee, anche se si richiede 15). |

**Esempio**

Questo comando Scarica i file da un'unità locale di archivio Azure Data Lake toohello utente tramite 20 thread per file e di 100 file simultanei.

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-hello-value-tooset-for-these-parameters"></a>Come è possibile determinare hello valore tooset per questi parametri?

Ecco alcune linee guida che è possibile usare.

* **Passaggio 1: Determinare il numero totale di thread di hello** -è consigliabile iniziare il calcolo toouse numero totale di thread di hello. Come regola generale, è consigliabile usare 6 thread per ogni core fisico.

        Total thread count = total physical cores * 6

    **Esempio**

    Presupponendo che si esegue PowerShell hello comandi da una macchina virtuale D14 con 16 core

        Total thread count = 16 cores * 6 = 96 threads


* **Passaggio 2: Calcolare PerFileThreadCount** -si calcola il nostro PerFileThreadCount in base alle dimensioni di hello dei file hello. Per i file di dimensioni inferiori a 2,5 GB, sono non infatti toochange è necessario questo parametro hello valore predefinito di 10 è sufficiente. Per i file più grandi di 2,5 GB, è consigliabile utilizzare 10 thread come base hello per hello prima 2,5 GB e aggiungere 1 thread per ogni incremento di 256 MB aggiuntivi nelle dimensioni dei file. Se si copia una cartella con un'ampia gamma di dimensioni dei file, è consigliabile raggrupparle in file di dimensioni simili. Il raggruppamento in file di dimensioni diverse può comportare prestazioni non ottimali. Se non è possibile toogroup dimensioni del file simile, è necessario impostare PerFileThreadCount in base alle dimensioni del file hello più grande.

        PerFileThreadCount = 10 threads for hello first 2.5GB + 1 thread for each additional 256MB increase in file size

    **Esempio**

    Se che si dispone di 100 file compreso tra 1GB too10GB, utilizziamo hello dimensioni per l'equazione, leggerà hello seguente del file di 10GB come hello più grande.

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* **Passaggio 3: Calcolare ConcurrentFilecount** -utilizza il numero totale di thread di hello e PerFileThreadCount toocalculate ConcurrentFileCount basati su hello seguente equazione.

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    **Esempio**

    In base ai valori di esempio hello che utilizziamo

        96 = 40 * ConcurrentFileCount

    In tal caso, **ConcurrentFileCount** è **2.4**, che è possibile arrotondare troppo**2**.

### <a name="further-tuning"></a>Ottimizzazione ulteriore

È possibile richiedere un'ulteriore ottimizzazione perché è un intervallo di toowork le dimensioni dei file con. Hello sopra calcolo funziona anche se tutte o la maggior parte dei file hello sono più grandi e più simili toohello intervallo di 10GB. Se invece sono presenti diverse dimensioni di file con molti file più piccoli, è possibile ridurre PerFileThreadCount. Grazie alla riduzione hello PerFileThreadCount, migliorare ConcurrentFileCount. In tal caso, se si suppone che la maggior parte di questo file sono più piccolo nell'intervallo di 5GB hello, è possibile eseguire nuovamente il calcolo:

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

In tal caso, **ConcurrentFileCount** verrà ora 96/20, vale a dire 4.8, arrotondata troppo**4**.

È possibile continuare tootune queste impostazioni modificando hello **PerFileThreadCount** verticale a seconda distribuzione hello delle dimensioni dei file.

### <a name="limitation"></a>Limitazione

* **Numero di file è minore di ConcurrentFileCount**: se il numero di hello dei file che si sta caricando è minore di hello **ConcurrentFileCount** che è stato calcolato, quindi è necessario ridurre  **ConcurrentFileCount** toobe toohello uguale numero di file. È possibile utilizzare qualsiasi esempio di thread rimanenti tooincrease **PerFileThreadCount**.

* **Troppi thread**: se si aumenta thread conteggio troppa senza aumentare la dimensione del cluster, si corre il rischio di hello di riduzione delle prestazioni. Possono esistere problemi di contesa durante il cambio di contesto su hello della CPU.

* **Concorrenza insufficiente**: se la concorrenza hello non è sufficiente, quindi il cluster potrebbe essere troppo piccolo. È possibile aumentare il numero di hello dei nodi del cluster in modo da maggiore concorrenza.

* **Errori di limitazione**: se la concorrenza è troppo elevata, è possibile che vengano visualizzati errori di limitazione. Se vengono visualizzati errori di limitazione, si deve ridurre concorrenza hello o contattare Microsoft.

## <a name="next-steps"></a>Passaggi successivi
* [Proteggere i dati in Data Lake Store](data-lake-store-secure-data.md)
* [Usare Azure Data Lake Analytics con Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usare Azure HDInsight con Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

