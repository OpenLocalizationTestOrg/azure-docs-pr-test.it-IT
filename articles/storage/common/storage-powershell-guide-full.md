---
title: aaaUsing Azure PowerShell con l'archiviazione di Azure | Documenti Microsoft
description: Informazioni su come toouse hello cmdlet PowerShell di Azure per toocreate di archiviazione di Azure e gestire gli account di archiviazione; utilizzo di BLOB, tabelle, code e i file; configurare e analitica di archiviazione di query e creare firme di accesso condiviso.
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 17d638e741911ceafb9777d5c2fce7bfe533e50c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a>Uso di Azure PowerShell con Archiviazione di Azure
## <a name="overview"></a>Panoramica
Azure PowerShell è un modulo che fornisce i cmdlet toomanage Azure tramite Windows PowerShell. Corrisponde a una shell della riga di comando basata su attività e un linguaggio di scripting progettato appositamente per l'amministrazione del sistema. Con PowerShell, è possibile controllare facilmente e automatizzare l'amministrazione di hello di applicazioni e i servizi di Azure. Ad esempio, è possibile utilizzare hello tooperform di cmdlet hello stessa attività che è possibile eseguire tramite hello [portale di Azure](https://portal.azure.com).

In questa Guida, si esamineranno come hello toouse [cmdlet di archiviazione di Azure](/powershell/module/azurerm.storage/#storage) tooperform un'ampia gamma di attività di sviluppo e amministrazione con l'archiviazione di Azure.

Nella guida si presuppone una certa esperienza nell'uso di [Archiviazione di Azure](https://azure.microsoft.com/documentation/services/storage/) e [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx). Guida di Hello fornisce un numero di script utilizzo hello toodemonstrate di PowerShell con l'archiviazione di Azure. È necessario aggiornare le variabili dello script hello in base alla configurazione prima di eseguire ogni script.

Hello prima sezione in questa guida fornisce una panoramica di archiviazione di Azure e PowerShell. Per informazioni dettagliate e istruzioni, avviare da hello [prerequisiti per l'utilizzo di Azure PowerShell con l'archiviazione di Azure](#prerequisites-for-using-azure-powershell-with-azure-storage).

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a>Introduzione ad Archiviazione di Azure e PowerShell in 5 minuti
In questa sezione illustra come tooaccess di archiviazione di Azure tramite PowerShell in 5 minuti.

**Nuovo tooAzure:** ottenere una sottoscrizione di Microsoft Azure e un account Microsoft associato a tale sottoscrizione. Per informazioni sulle opzioni di acquisto di Azure, vedere la [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/), le [opzioni di acquisto](https://azure.microsoft.com/pricing/purchase-options/) e le [offerte per i membri](https://azure.microsoft.com/pricing/member-offers/) (per i membri di MSDN, Microsoft Partner Network, BizSpark e altri programmi Microsoft).

Per altre informazioni sulle sottoscrizioni di Azure, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) .

**Dopo aver creato una sottoscrizione e un account di Microsoft Azure:**

1. Scaricare e installare più recente hello [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).
2. Avviare Windows PowerShell Integrated Scripting Environment (ISE): Nel computer locale, passare toohello **avviare** menu. Tipo **strumenti di amministrazione** e fare clic su toorun è. In hello **strumenti di amministrazione** finestra, fare doppio clic su **Windows PowerShell ISE**, fare clic su **Esegui come amministratore**.
3. In **Windows PowerShell ISE**, fare clic su **File** > **New** toocreate un nuovo file script.
4. A questo punto, verrà fornita è un semplice script che mostra base tooaccess di comandi di PowerShell di archiviazione di Azure. script Hello chiederà innanzitutto il tooadd le credenziali di account Azure account Azure toohello PowerShell ambiente locale. Quindi, hello script impostare il valore predefinito di hello sottoscrizione di Azure e creare un nuovo account di archiviazione in Azure. Successivamente, hello script creare un nuovo contenitore in questo nuovo account di archiviazione e caricare un contenitore toothat (blob) di file di immagine esistente. Dopo aver hello script permette di elencare tutti i BLOB nel contenitore, verrà creare una nuova directory di destinazione nel computer locale e scaricare i file di immagine hello.
5. In hello seguente sezione di codice, selezionare script hello tra la sezione Osservazioni hello **#begin** e **#end**. Premere CTRL + C toocopy è toohello Appunti.

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. In **Windows PowerShell ISE**, premere script hello toocopy CTRL + V. Fare clic su **File** > **Salva**. In hello **Salva con nome** finestra di dialogo, il nome del tipo hello del file di script hello, ad esempio "mystoragescript". Fare clic su **Salva**.
7. A questo punto, è necessario tooupdate hello scripting di variabili in base alle impostazioni di configurazione. È necessario aggiornare hello **$SubscriptionName** variabile con la propria sottoscrizione. È possibile mantenere hello altre variabili come specificato nello script hello o aggiornarle nel modo desiderato.
   
   * **$SubscriptionName:** è necessario aggiornare questa variabile con il proprio nome di sottoscrizione. Effettuare una delle hello dopo tre modi toolocate hello nome della sottoscrizione:
     
    a. In **Windows PowerShell ISE**, fare clic su **File** > **New** toocreate un nuovo file script. Esempio hello copia script toohello nuovo file di script e fare clic su **Debug** > **eseguire**. Hello lo script seguente verrà prima chiedere il tooadd le credenziali di account di Azure dell'ambiente di PowerShell locale toohello account Azure e di visualizzare tutte le sottoscrizioni di hello che sono connessi toohello sessione di PowerShell locale. Prendere nota del nome hello della sottoscrizione hello che si desidera toouse durante questa esercitazione:
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    b. toolocate e copiare la sottoscrizione nome nel hello [portale di Azure](https://portal.azure.com)in hello menu Hub hello a sinistra, fare clic su **sottoscrizioni**. Copia nome hello di sottoscrizione che si desidera toouse durante l'esecuzione di script hello in questa Guida.
     
     ![Portale di Azure](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    c. toolocate e copiare la sottoscrizione nome nel hello [portale di Azure classico](https://manage.windowsazure.com/), scorrere verso il basso e fare clic su **impostazioni** sul lato sinistro di portale hello hello. Fare clic su **sottoscrizioni** toosee un elenco delle sottoscrizioni. Copia nome hello di sottoscrizione che si desidera toouse durante l'esecuzione di script hello specificato in questa Guida.
     
     ![portale di Azure classico](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * **$StorageAccountName:** utilizzare hello dato nome nello script hello o immettere un nuovo nome per l'account di archiviazione. **Importante:** nome hello hello dell'account di archiviazione deve essere univoco in Azure. Utilizzare caratteri minuscoli.
   * **$Location:** utilizzare hello "Stati Uniti occidentali" specificato nello script hello o scegliere altre posizioni di Azure, ad esempio Stati Uniti orientali, Europa settentrionale e così via.
   * **$ContainerName:** utilizzare hello dato nome nello script hello o immettere un nuovo nome per il contenitore.
   * **$ImageToUpload:** immettere un'immagine di tooa percorso sul computer locale, ad esempio: "C:\Images\HelloWorld.png".
   * **$DestinationFolder:** immettere un percorso tooa directory locale toostore scaricare i file dall'archiviazione di Azure, ad esempio: "C:\DownloadImages".
8. Dopo aver aggiornato le variabili dello script hello nel file "mystoragescript.ps1" hello, fare clic su **File** > **salvare**. Quindi, fare clic su **Debug** > **eseguire** o premere **F5** script hello toorun.  

Dopo l'esecuzione di script hello è una cartella di destinazione locale che include i file di immagine scaricato hello. Hello seguente schermata mostra un esempio dell'output:

![Scaricare BLOB](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> Hello "Introduzione a PowerShell e di archiviazione di Azure in 5 minuti" sezione fornita una rapida introduzione su come toouse Azure PowerShell con l'archiviazione di Azure. Per informazioni dettagliate e istruzioni, si consiglia di hello tooread le sezioni seguenti.
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a>Prerequisiti per l'uso di Azure PowerShell con Archiviazione di Azure
È necessario un account e sottoscrizione toorun hello cmdlet di Azure PowerShell fornito in questa Guida, come descritto in precedenza.

Azure PowerShell è un modulo che fornisce i cmdlet toomanage Azure tramite Windows PowerShell. Per informazioni sull'installazione e configurazione di Azure PowerShell, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview). È consigliabile scaricare e installare o aggiornare il modulo PowerShell di Azure più recente di toohello prima di utilizzare questa Guida.

È possibile eseguire i cmdlet di hello nella console di Windows PowerShell standard hello o hello Windows PowerShell Integrated Scripting Environment (ISE). Ad esempio, tooopen **Windows PowerShell ISE**passare dal menu Start toohello, digitare strumenti di amministrazione e fare clic su toorun è. Nella finestra Strumenti di amministrazione di hello, fare doppio clic su Windows PowerShell ISE, fare clic su Esegui come amministratore.

## <a name="how-toomanage-storage-accounts-in-azure"></a>Come account di archiviazione toomanage in Azure

Di seguito è illustrata la gestione degli account di archiviazione in Azure con PowerShell

### <a name="how-tooset-a-default-azure-subscription"></a>Come tooset predefinito sottoscrizione di Azure
toomanage archiviazione di Azure con Azure PowerShell, è necessario tooauthenticate ambiente client con Azure tramite l'autenticazione di Azure Active Directory o l'autenticazione basata su certificato. Per informazioni dettagliate, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) esercitazione. Questa guida utilizza l'autenticazione di Azure Active Directory hello.

1. In Windows PowerShell ISE, digitare hello successivo comando tooadd account Azure toohello PowerShell ambiente locale:

    ```powershell
    Add-AzureAccount
    ```

2. Nella finestra "Accedi tooMicrosoft Azure" hello, indirizzo di posta elettronica di tipo hello e la password associata al proprio account. Azure autentica e Salva le informazioni sulle credenziali hello e chiude la finestra hello.

3. Quindi, eseguire hello comando tooview hello Azure gli account nell'ambiente di PowerShell locale e verificare che l'account sia elencato di seguito:
   
    ```powershell
    Get-AzureAccount
    ```
4. Quindi, eseguire hello seguente cmdlet tooview tutte le sottoscrizioni di hello che sono connessi toohello sessione di PowerShell locale e verificare che la sottoscrizione sia elencata:

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. tooset predefinito sottoscrizione di Azure, eseguire il cmdlet Select-AzureSubscription hello:

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. Verificare nome hello della sottoscrizione predefinita hello esegue il cmdlet Get-AzureSubscription hello:

    ```powershell
    Get-AzureSubscription -Default
    ```

7. toosee tutti hello cmdlet di PowerShell disponibili per l'archiviazione di Azure, eseguire:
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a>Come toocreate un nuovo account di archiviazione di Azure
toouse archiviazione di Azure, è necessario un account di archiviazione. Dopo aver configurato la sottoscrizione di tooyour tooconnect computer, è possibile creare un nuovo account di archiviazione di Azure.

1. Eseguire toofind di cmdlet Get-AzureLocation hello tutte le posizioni dei Data Center disponibili hello:

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. Successivamente, eseguire toocreate di cmdlet New-AzureStorageAccount hello un nuovo account di archiviazione. Hello seguente viene creato un nuovo account di archiviazione nel Data Center di hello "Stati Uniti occidentali".
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> nome di Hello dell'account di archiviazione deve essere univoco all'interno di Azure e deve essere minuscole. Per le convenzioni di denominazione e le restrizioni, vedere [Informazioni sugli account di archiviazione di Azure](../storage-create-storage-account.md) e [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx) (Assegnazione di nome e riferimento a contenitori, BLOB e metadati).
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a>Come tooset un account di archiviazione di Azure predefinito
È possibile avere più account di archiviazione nella sottoscrizione. È possibile scegliere uno di essi e impostarlo come account di archiviazione di hello predefinito per tutti hello archiviazione comandi in hello stessa sessione di PowerShell. Ciò consente di comandi di archiviazione di Azure PowerShell hello toorun senza specificare in modo esplicito il contesto di archiviazione hello.

1. tooset un account di archiviazione predefinito per la sottoscrizione, è possibile eseguire i cmdlet Set-AzureSubscription hello.

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. Successivamente, eseguire Get-AzureSubscription hello cmdlet tooverify che l'account di archiviazione hello è associata con l'account della sottoscrizione predefinita. Questo comando restituisce le proprietà di sottoscrizione hello nella sottoscrizione corrente di hello incluso il relativo account di archiviazione corrente.

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a>Come toolist account di archiviazione di Azure tutte in una sottoscrizione
Ogni sottoscrizione di Azure può essere composto too100 gli account di archiviazione. Per informazioni più aggiornate di hello sui limiti, vedere [sottoscrizione Azure e limiti dei servizi, quote e vincoli](../../azure-subscription-service-limits.md).

Eseguire hello toofind cmdlet out hello nome e lo stato hello di account di archiviazione nella sottoscrizione corrente hello seguenti:

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a>Come toocreate un contesto di archiviazione di Azure
Contesto di archiviazione di Azure è un oggetto in credenziali di archiviazione hello tooencapsulate di PowerShell. Utilizzando un contesto di archiviazione durante l'esecuzione di qualsiasi cmdlet successivi consente si tooauthenticate la richiesta senza specificare in modo esplicito l'account di archiviazione hello e la relativa chiave di accesso. È possibile creare un contesto di archiviazione in molti modi, ad esempio usando la chiave di accesso e il nome dell'account di archiviazione, il token di firma di accesso condiviso, la stringa di connessione o il valore anonimo. Per ulteriori informazioni, vedere [Nuovo AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).  

Utilizzare uno dei seguenti tre modi toocreate hello un contesto di archiviazione:

* Eseguire hello [Get AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) toofind cmdlet out chiave di accesso hello archiviazione primaria per l'account di archiviazione di Azure. Successivamente, chiamare hello [New AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) toocreate cmdlet un contesto di archiviazione:

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* Generare un token di firma di accesso condiviso per un contenitore di archiviazione di Azure e usarlo toocreate un contesto di archiviazione:

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    Per altre informazioni, vedere [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) e [Uso delle firme di accesso condiviso (SAS)](../storage-dotnet-shared-access-signature-part-1.md).

* In alcuni casi, è consigliabile gli endpoint del servizio hello toospecify quando si crea un nuovo contesto di archiviazione. Potrebbe essere necessario quando è stato registrato un nome di dominio personalizzato per l'account di archiviazione con il servizio di Blob hello o si desidera toouse una firma di accesso condiviso per accedere alle risorse di archiviazione. Impostare gli endpoint del servizio hello in una stringa di connessione e utilizzare toocreate un nuovo contesto di archiviazione come illustrato di seguito:

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

Per ulteriori informazioni su come tooconfigure una stringa di connessione di archiviazione, vedere [la configurazione delle stringhe di connessione](../storage-configure-connection-string.md).

Configurare il computer e appreso come toomanage sottoscrizioni e account di archiviazione tramite Azure PowerShell, passare toohello successiva sezione toolearn come BLOB di Azure toomanage e gli snapshot del blob.

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a>Come tooretrieve e rigenerare le chiavi di archiviazione di Azure
Un account di archiviazione di Azure viene fornito con due chiavi. Utilizzare le chiavi di hello tooretrieve cmdlet seguente.

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

Utilizzare hello seguente cmdlet tooretrieve una chiave specifica. I valori validi sono Primary e Secondary.  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

Se si desidera tooregenerate le chiavi, utilizzare hello cmdlet seguente. I valori validi per -KeyType sono "Primary" e "Secondary".

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a>Come BLOB di Azure toomanage
Archiviazione Blob di Azure è un servizio per l'archiviazione di grandi quantità di dati non strutturati, ad esempio dati di testo o binario, che è possibile accedere da qualsiasi in HelloWorld tramite HTTP o HTTPS. In questa sezione si presuppone che si conoscono già i concetti di hello Azure Blob Storage Service. Per informazioni dettagliate, vedere [Introduzione all'archivio BLOB di Azure con .NET](../blobs/storage-dotnet-how-to-use-blobs.md) e [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx) (Concetti relativi al servizio BLOB).

### <a name="how-toocreate-a-container"></a>Come un contenitore toocreate
Ogni BLOB nell'archiviazione di Azure deve risiedere in un contenitore. È possibile creare un contenitore privato utilizzando il cmdlet New-AzureStorageContainer hello:

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> Esistono tre livelli di accesso in lettura anonimo: **Off**, **BLOB** e **contenitore**. tooprevent anonimo accesso troppo accedere tooblobs, il parametro di autorizzazione del set di hello**Off**. Per impostazione predefinita, hello nuovo contenitore è privato e accessibile solo dal proprietario dell'account hello. in lettura pubblico anonimo tooallow tooblob di accedere alle risorse, ma non toocontainer metadati o toohello elenco di BLOB nel contenitore di hello, impostare il parametro di autorizzazione hello troppo**Blob**. in lettura pubblico completo tooallow tooblob di accedere alle risorse e i metadati del contenitore elenco hello di BLOB nel contenitore di hello, impostare il parametro di autorizzazione hello troppo**contenitore**. Per ulteriori informazioni, vedere [gestire BLOB e accesso in lettura anonimo toocontainers](../blobs/storage-manage-access-to-resources.md).
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a>Come tooupload un blob in un contenitore
In Archiviazione BLOB di Azure sono supportati BLOB in blocchi e BLOB di pagine. Per altre informazioni, vedere [Informazioni sui BLOB in blocchi, sui BLOB di aggiunta e sui BLOB di pagine](http://msdn.microsoft.com/library/azure/ee691964.aspx).

i BLOB nel contenitore tooa tooupload, è possibile utilizzare hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet. Per impostazione predefinita, questo comando Carica blob in blocchi tooa hello file locali. tipo di hello toospecify per blob hello, è possibile utilizzare il parametro - BlobType hello.

esempio Hello esegue hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) tooget cmdlet hello tutti i file nella cartella specificata hello e quindi li passa cmdlet successivo toohello utilizzando l'operatore pipeline hello. Hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet carica contenitore tooyour di hello file locali:

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a>Come toodownload BLOB da un contenitore
Hello di esempio seguente viene illustrato come toodownload BLOB da un contenitore. esempio Hello stabilisce prima una tooAzure connessione archiviazione utilizzando il contesto account di archiviazione di hello che include nome account di archiviazione hello e la relativa chiave di accesso primaria. Quindi, hello esempio recupera un riferimento di blob utilizzando hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet. Successivamente, esempio hello utilizza hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) BLOB toodownload cmdlet nella cartella di destinazione locale hello.

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a>Come toocopy BLOB da un tooanother di contenitore di archiviazione
È possibile copiare i BLOB tra aree e account di archiviazione in modo asincrono. Hello esempio seguente viene illustrato come toocopy BLOB da archiviazione di un contenitore tooanother in due diversi account di archiviazione. esempio Hello prima imposta le variabili per gli account di archiviazione di origine e di destinazione e quindi crea un contesto per ogni account di archiviazione. Successivamente, esempio hello copia BLOB dal contenitore destinazione hello origine contenitore toohello utilizzando hello [inizio AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet. Hello si presuppone che i contenitori e account di archiviazione di origine e destinazione hello esistano già.

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

In questo esempio viene eseguita una copia asincrona. È possibile monitorare lo stato di hello di ogni copia eseguendo hello [Get AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.

### <a name="how-toocopy-blobs-from-a-secondary-location"></a>Come toocopy BLOB da una posizione secondaria
È possibile copiare BLOB dal percorso secondario di hello di un account RA-GRS abilitato.

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a>Come toodelete un blob
un blob, toodelete innanzitutto ottenere un riferimento di blob, quindi chiamare cmdlet Remove-AzureStorageBlob hello su di esso. Hello di esempio seguente elimina tutti i BLOB hello in un contenitore specificato. esempio Hello prima imposta le variabili per un account di archiviazione e quindi crea un contesto di archiviazione. Successivamente, hello esempio recupera un riferimento di blob utilizzando hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) hello cmdlet e viene eseguito [Remove AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove BLOB da un contenitore di archiviazione di Azure.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a>Come toomanage Azure blob snapshot
Azure consente di creare uno snapshot di un BLOB. Uno snapshot è una versione di sola lettura di un BLOB eseguito in un determinato momento. Una volta creato uno snapshot, è possibile leggerlo, copiarlo o eliminarlo, ma non modificarlo. Gli snapshot forniscono un modo tooback backup di un blob così come viene visualizzato in un momento. Per ulteriori informazioni, vedere [Creazione di uno Snapshot di un BLOB](http://msdn.microsoft.com/library/azure/hh488361.aspx).

### <a name="how-toocreate-a-blob-snapshot"></a>Come toocreate uno snapshot di blob
toocreate dello stile di vita di un blob, innanzitutto ottenere un riferimento di blob e quindi chiamare hello `ICloudBlob.CreateSnapshot` metodo su di esso. Hello esempio seguente imposta prima di tutto le variabili per un account di archiviazione e quindi crea un contesto di archiviazione. Successivamente, hello esempio recupera un riferimento di blob utilizzando hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) hello cmdlet e viene eseguito [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) toocreate metodo uno snapshot.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a>La modalità snapshot di toolist un blob
Non ci sono limiti agli snapshot creati per un BLOB. È possibile elencare gli snapshot di hello associati tootrack i blob degli snapshot correnti. esempio Hello utilizza un hello predefinito di blob e chiama [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) snapshot hello toolist di cmdlet del blob.  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a>Come toocopy uno snapshot di un blob
È possibile copiare uno snapshot di uno snapshot di blob toorestore hello. Per informazioni dettagliate e le restrizioni, vedere [Creazione di uno Snapshot di un BLOB](http://msdn.microsoft.com/library/azure/hh488361.aspx). Hello esempio seguente imposta prima di tutto le variabili per un account di archiviazione e quindi crea un contesto di archiviazione. Successivamente, esempio hello definisce le variabili di nome contenitore e del blob hello. esempio Hello recupera un riferimento di blob utilizzando hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) hello cmdlet e viene eseguito [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) toocreate metodo uno snapshot. Esempio hello esegue quindi hello [inizio AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) snapshot hello toocopy di cmdlet di un blob utilizzando l'oggetto ICloudBlob hello per blob di origine hello. Essere assicurarsi che le variabili di hello tooupdate in base alla configurazione prima di esempio hello in esecuzione. Si noti che hello di esempio seguente si presuppone che hello contenitori di origine e di destinazione e il blob di origine hello esiste già.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

Ora che si è appreso come BLOB di Azure toomanage e relativi snapshot con Azure PowerShell, passare toohello successiva sezione toolearn come toomanage tabelle, code e i file.

## <a name="how-toomanage-azure-tables-and-table-entities"></a>Come Azure toomanage tabelle e le entità di tabella
Servizio di archiviazione tabelle di Azure è un archivio dati NoSQL, che è possibile utilizzare set di grandi dimensioni toostore e query di dati strutturati non relazionali. componenti principali di Hello del servizio hello sono tabelle, entità e proprietà. una tabella è una raccolta di entità. Un'entità è un set di proprietà. Ogni entità può avere proprietà too252, che sono tutte le coppie nome-valore. In questa sezione si presuppone che si ha già familiarità con concetti del servizio di archiviazione tabelle Azure hello. Per informazioni dettagliate, vedere [hello comprensione modello di dati del servizio tabelle](http://msdn.microsoft.com/library/azure/dd179338.aspx) e [Introduzione all'archiviazione tabelle di Azure usando .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md).

In hello seguenti sottosezioni, si apprenderà come toomanage archiviazione tabelle di Azure del servizio con Azure PowerShell. Hello scenari trattati includono **creazione**, **eliminazione**, e **recupero** **tabelle**, così come **aggiunta**, **l'esecuzione di query**, e **l'eliminazione di entità di tabella**.

### <a name="how-toocreate-a-table"></a>Come toocreate una tabella
Ogni tabella deve risiedere in un account di archiviazione di Azure. Hello esempio seguente viene illustrato come toocreate una tabella in archiviazione di Azure. esempio Hello stabilisce prima una tooAzure connessione archiviazione utilizzando il contesto account di archiviazione di hello che include nome account di archiviazione hello e la relativa chiave di accesso. Viene quindi utilizzato hello [New AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) toocreate cmdlet una tabella in archiviazione di Azure.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a>Come tooretrieve una tabella
È possibile eseguire query e recuperare una o tutte le tabelle di un account di archiviazione. Hello esempio seguente viene illustrato come tooretrieve una determinata tabella utilizzando hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

Se si chiama il cmdlet Get-AzureStorageTable hello senza parametri, ottiene tutte le tabelle di archiviazione per un account di archiviazione.

### <a name="how-toodelete-a-table"></a>Come toodelete una tabella
È possibile eliminare una tabella da un account di archiviazione tramite hello [Remove AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a>Come toomanage tabella entità
Attualmente, Azure PowerShell non fornisce direttamente i cmdlet toomanage entità della tabella. tooperform operazioni su entità tabella, è possibile utilizzare le classi di hello all'hello [Azure Storage Client Library per .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).

#### <a name="how-tooadd-table-entities"></a>Come tooadd tabella entità
tooadd tabella tooa un'entità, creare innanzitutto un oggetto che definisce le proprietà dell'entità. Un'entità può contenere proprietà too255, incluse 3 proprietà di sistema: **PartitionKey**, **RowKey**, e **Timestamp**. L'utente è responsabile per l'inserimento e aggiornamento dei valori hello di **PartitionKey** e **RowKey**. server Hello gestisce il valore di hello di **Timestamp**, che non può essere modificato. Hello insieme **PartitionKey** e **RowKey** identificare in modo univoco ogni entità in una tabella.

* **PartitionKey**: determina partizione hello archiviati in entità hello.
* **RowKey**: identifica in modo univoco l'entità hello all'interno della partizione hello.

È possibile definire le proprietà personalizzate di too252 per un'entità. Per ulteriori informazioni, vedere [hello comprensione modello di dati del servizio tabelle](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Hello esempio seguente viene illustrato come tabella di tooa tooadd entità. Hello riportato di seguito viene illustrato tooretrieve hello tabella employee e come aggiungere alcune entità al suo interno. Prima di tutto, stabilisce un tooAzure connessione archiviazione utilizzando il contesto account di archiviazione di hello che include nome account di archiviazione hello e la relativa chiave di accesso. Successivamente, viene recuperata hello data tabella utilizzando hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. Se non esiste nella tabella hello, hello [New AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet è toocreate utilizzata una tabella in archiviazione di Azure. Successivamente, hello esempio definisce una funzione personalizzata nella tabella toohello entità tooadd Aggiungi entità specificando ogni di partizione e chiave di riga. hello chiamate di funzione Hello Aggiungi entità [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) toocreate classe un oggetto entità. In un secondo momento, esempio hello chiama hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) metodo su questo tooadd oggetto entità tooa tabella.

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a>Come tooquery tabella entità
tooquery una tabella, utilizzare hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) classe. Hello seguente si presuppone di aver già eseguire script hello all'hello come sezione entità tooadd di questa Guida. esempio Hello stabilisce prima una tooAzure connessione archiviazione utilizzando il contesto archiviazione hello, che include nome account di archiviazione hello e la relativa chiave di accesso. Successivamente, si tenta di tabella di dipendenti"hello creato in precedenza" tooretrieve utilizzando hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. Chiamare il metodo hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet hello Microsoft.WindowsAzure.Storage.Table.TableQuery classe crea un nuovo oggetto di query. esempio Hello ricerca entità hello che dispongono di una colonna di 'ID' il cui valore è 1, come specificato in un filtro di stringa. Per informazioni dettagliate, vedere [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx) (Esecuzione di query su tabelle ed entità). Quando si esegue questa query, restituisce tutte le entità che soddisfano i criteri di filtro hello.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a>Come toodelete tabella entità
È possibile eliminare un'entità utilizzando le relative chiavi di riga e di partizione. Hello seguente si presuppone di aver già eseguire script hello all'hello come sezione entità tooadd di questa Guida. esempio Hello stabilisce prima una tooAzure connessione archiviazione utilizzando il contesto archiviazione hello, che include nome account di archiviazione hello e la relativa chiave di accesso. Successivamente, si tenta di tabella di dipendenti"hello creato in precedenza" tooretrieve utilizzando hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. Se hello tabella esiste, l'esempio hello chiama hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) tooretrieve metodo un'entità in base ai relativi valori chiavi di riga e di partizione. Passare quindi hello entità toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) toodelete metodo.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a>Come mettere in coda e coda di messaggi toomanage Azure
Archiviazione delle code di Azure è un servizio per l'archiviazione di un numero elevato di messaggi che è possibile accedere da qualsiasi in HelloWorld tramite chiamate autenticate tramite HTTP o HTTPS. In questa sezione si presuppone che si conoscono già i concetti di hello servizio di archiviazione di Accodamento di Azure. Per informazioni dettagliate, vedere [Introduzione all'archivio code di Azure con .NET](../storage-dotnet-how-to-use-queues.md).

Questa sezione verranno illustrate le modalità di servizio con Azure PowerShell toomanage l'archiviazione delle code di Azure. Hello scenari trattati includono **inserimento** e **eliminazione** coda di messaggi, nonché **creazione**, **eliminazione**, e**il recupero delle code**.

### <a name="how-toocreate-a-queue"></a>Come toocreate una coda
Hello esempio stabilisce prima una tooAzure connessione archiviazione utilizzando il contesto account di archiviazione di hello che include nome account di archiviazione hello e la relativa chiave di accesso. Successivamente, chiama [New AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) toocreate cmdlet una coda denominata 'queuename'.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

Per informazioni sulle convenzioni di denominazione per il servizio di accodamento di Azure, vedere [Denominazione di code e metadati](http://msdn.microsoft.com/library/azure/dd179349.aspx).

### <a name="how-tooretrieve-a-queue"></a>Come tooretrieve una coda
È possibile eseguire una query e recuperare un elenco di tutte le code di hello in un account di archiviazione o di una coda specifica. Hello esempio seguente viene illustrato come una coda specificata tramite tooretrieve hello [Get AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

Se si chiama hello [Get AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet senza parametri, ottiene un elenco di tutte le code di hello.

### <a name="how-toodelete-a-queue"></a>Come toodelete una coda
toodelete una coda e tutti i messaggi hello in esso contenuti, cmdlet Remove-AzureStorageQueue hello chiamata. Hello di esempio seguente viene illustrato come una coda specificata tramite toodelete hello cmdlet Remove-AzureStorageQueue.

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a>Come tooinsert un messaggio in una coda
tooinsert un messaggio in una coda esistente, creare innanzitutto una nuova istanza di hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) classe. Successivamente, chiamare hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) metodo. È possibile creare un oggetto CloudQueueMessage da una stringa in formato UTF-8 o da una matrice di byte.

Hello di esempio seguente viene illustrato come tooadd tooa coda di messaggi. esempio Hello stabilisce prima una tooAzure connessione archiviazione utilizzando il contesto account di archiviazione di hello che include nome account di archiviazione hello e la relativa chiave di accesso. Successivamente, viene recuperato utilizzando hello la coda specificata hello [Get AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet. Se la coda hello, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet viene utilizzato toocreate un'istanza di hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) classe. In un secondo momento, esempio hello chiama hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) metodo su questo tooadd di oggetto del messaggio è tooa coda. Ecco il codice che consente di recuperare una coda e inserisce il messaggio hello 'MessageInfo':

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a>Il messaggio successivo toode-coda hello
Il codice consente di rimuovere un messaggio da una coda in due passaggi. Quando si chiama hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) metodo, di ottenere il messaggio hello successivo in una coda. Un messaggio restituito da **GetMessage** diventa invisibile tooany altro codice la lettura dei messaggi dalla coda. toofinish messaggio hello rimozione dalla coda di hello, è necessario chiamare anche hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) metodo. Questo processo in due passaggi della rimozione di un messaggio garantisce che se il codice non tooprocess che possibile ottenere un messaggio a causa di un errore toohardware o software, un'altra istanza del codice stesso messaggio hello e riprovare. Il codice chiama **DeleteMessage** subito dopo il messaggio hello è stato elaborato.

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a>Come file di Azure toomanage condivide e i file
Archiviazione di File di Azure offre archiviazione condivisa per applicazioni che utilizzano il protocollo SMB standard di hello. Macchine virtuali di Microsoft Azure e servizi cloud possono condividere i dati di file nei componenti delle applicazioni tramite condivisioni montate e applicazioni locali possono accedere ai dati dei file in una condivisione tramite API di archiviazione di File hello o Azure PowerShell.

Per informazioni dettagliate su Archiviazione file di Azure, vedere [Introduzione ad Archiviazione file di Azure in Windows](../storage-dotnet-how-to-use-files.md) e [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx) (API REST del servizio file).

## <a name="how-tooset-and-query-storage-analytics"></a>La modalità query e tooset analitica di archiviazione
È possibile utilizzare [Analitica di archiviazione di Azure](../storage-analytics.md) toocollect metriche per l'account di archiviazione di Azure e sulle richieste di dati del log inviati tooyour account di archiviazione. È possibile utilizzare stato toomonitor hello metriche di archiviazione di un account di archiviazione e l'archiviazione registrazione toodiagnose e risolvere i problemi con l'account di archiviazione. È possibile configurare il monitoraggio tramite hello portale di Azure o Windows PowerShell o a livello di programmazione tramite libreria client di archiviazione hello. Registrazione di archiviazione si verifica sul lato server e consente toorecord dettagli per le richieste con esito positivo e non riuscite nell'account di archiviazione. Questi log consentono di dettagli toosee di lettura, scrittura e le operazioni di eliminazione contro le tabelle, code e BLOB, nonché motivi hello per le richieste non riuscite.

toolearn tooenable e visualizzare i dati di metrica di archiviazione usando PowerShell, vedere [come tooenable metriche di archiviazione con PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).

toolearn tooenable e recuperare dati di registrazione archiviazione usando PowerShell, vedere [come tooenable archiviazione registrazione tramite PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) e [ricerca dei dati di log di registrazione archiviazione](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).
Per informazioni dettagliate sull'uso di metriche di archiviazione e i problemi di archiviazione tootroubleshoot alla registrazione di archiviazione, vedere [monitoraggio, diagnostica e risoluzione dei problemi di archiviazione di Microsoft Azure](../storage-monitoring-diagnosing-troubleshooting.md).

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a>Come toomanage condiviso (SAS) di firma di accesso e criteri di accesso archiviati
Firme di accesso condiviso sono una parte importante del modello di sicurezza hello per le applicazioni che utilizzano l'archiviazione di Azure. Sono utili per fornire autorizzazioni limitate tooyour storage account tooclients che non dovrebbero essere chiave dell'account hello. Per impostazione predefinita, solo il hello proprietario dell'account di archiviazione hello può accedere BLOB, tabelle e code all'interno di tale account. Se il servizio o l'applicazione deve toomake questi client tooother disponibili risorse senza condividere la chiave di accesso, sono disponibili tre opzioni:

* Impostare autorizzazioni toopermit accesso in lettura anonimo toohello contenitore di un contenitore e i relativi BLOB. Questa operazione non è consentita per le tabelle o le code.
* Utilizzare una firma di accesso condiviso che concede toocontainers diritti di accesso limitato, BLOB, code e tabelle per un intervallo di tempo specifico.
* Utilizzare un tooobtain di criteri di accesso archiviati un ulteriore livello di controllo sulle firme di accesso condiviso per un contenitore o i relativi BLOB, per una coda o per una tabella. Hello criteri di accesso archiviati consentono ora di inizio hello toochange, ora di scadenza o le autorizzazioni per una firma, o toorevoke dopo è stata eseguita.

Una firma di accesso condiviso può assumere una delle due forme seguenti:

* **Firma di accesso condiviso ad hoc**: quando si crea una firma di accesso condiviso ad hoc, l'ora di inizio hello, ora di scadenza e le autorizzazioni per hello SAS vengono specificate in hello URI SAS. Questo tipo di firma di accesso condiviso può essere creato per un contenitore, un BLOB, una tabella e una coda e non è revocabile.
* **Firma di accesso condiviso con criteri di accesso archiviati**: è definito un criterio di accesso archiviati in un contenitore di risorse un contenitore blob, tabella o coda - ed è possibile utilizzarlo toomanage vincoli per uno o più firme di accesso condiviso. Quando si associa una firma di accesso condiviso con criteri di accesso archiviati, hello SAS eredita i vincoli di hello: hello ora di inizio, ora di scadenza e le autorizzazioni - definite per i criteri di accesso archiviato hello. Questo tipo di firma di accesso condiviso è revocabile.

Per ulteriori informazioni, vedere [tramite firme di accesso condiviso (SAS)](../storage-dotnet-shared-access-signature-part-1.md) e [gestire BLOB e accesso in lettura anonimo toocontainers](../blobs/storage-manage-access-to-resources.md).

Nelle sezioni successive di hello, si apprenderà come toocreate un criterio di accesso stored e token di firma di accesso condiviso per le tabelle di Azure. Azure PowerShell fornisce cmdlet simili per contenitori, BLOB e code. script di hello toorun in questa sezione, scaricare hello [Azure PowerShell versione 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) o versione successiva.

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a>Il token di firma di accesso condiviso toocreate basata su criteri
Utilizzare toocreate di cmdlet New-AzureStorageTableStoredAccessPolicy hello un nuovo criterio di accesso archiviati. Chiamare quindi hello [New AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) toocreate cmdlet un nuovo token di firma basata su criteri di accesso condiviso per una tabella di archiviazione di Azure.

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a>Come toocreate un token di firma di accesso condiviso ad hoc (non revocabile)
Hello utilizzare [New AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) toocreate cmdlet un token di firma di accesso condiviso (non revocabile) a ad hoc nuovo per una tabella di archiviazione di Azure:

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a>Come criteri di accesso archiviati toocreate
Utilizzare toocreate cmdlet New-AzureStorageTableStoredAccessPolicy hello un nuovo criterio di accesso archiviati per una tabella di archiviazione di Azure:

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a>Come criteri di accesso archiviati tooupdate
Utilizzare tooupdate di cmdlet Set-AzureStorageTableStoredAccessPolicy hello un criterio di accesso archiviati per una tabella di archiviazione di Azure:

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a>Come criteri di accesso archiviati toodelete
Utilizzare toodelete cmdlet Remove-AzureStorageTableStoredAccessPolicy hello criteri di accesso archiviati in una tabella di archiviazione di Azure:

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a>Come toouse di archiviazione di Azure per governo degli Stati Uniti e Cina di Azure
Un ambiente Azure è una distribuzione indipendente di Microsoft Azure, ad esempio [Azure Government per il governo degli Stati Uniti](https://azure.microsoft.com/features/gov/), [AzureCloud per Azure globale](https://portal.azure.com) e [AzureChinaCloud per Azure gestito da 21Vianet in Cina](http://www.windowsazure.cn/). È possibile distribuire nuovi ambienti Azure per il governo degli Stati Uniti e Azure Cina.

Archiviazione di Azure con AzureChinaCloud toouse, è necessario un contesto di archiviazione associato AzureChinaCloud toocreate. Seguire tooget questi passaggi per iniziare:

1. Eseguire hello [Get AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee cmdlet hello ambienti Azure disponibili:
   
    ```powershell
    Get-AzureEnvironment
    ```

2. Aggiungere un tooWindows account Cina di Azure PowerShell:
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. Creare un contesto di archiviazione per un account AzureChinaCloud:
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

Archiviazione di Azure toouse con [Stati Uniti degli Stati Uniti](https://azure.microsoft.com/features/gov/), è necessario definire un nuovo ambiente e creare un nuovo contesto di archiviazione con questo ambiente:

1. Eseguire hello [Get AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee cmdlet hello ambienti Azure disponibili:

    ```powershell
    Get-AzureEnvironment
    ```

2. Aggiungere un tooWindows di account di Azure del governo PowerShell:
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. Creare un contesto di archiviazione per un account AzureUSGovernment:
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
Per altre informazioni, vedere:

* [Guida per gli sviluppatori di Microsoft Azure Government](../../azure-government/documentation-government-developer-guide.md).
* [Panoramica delle differenze nella creazione di un'applicazione in China Service](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a>Passaggi successivi
In questa Guida, si è appreso come toomanage archiviazione di Azure con Azure PowerShell. Per altre informazioni, vedere gli articoli e le risorse correlati seguenti:

* [Documentazione di Archiviazione di Azure](https://azure.microsoft.com/documentation/services/storage/)
* [Cmdlet di PowerShell per Archiviazione di Azure](/powershell/module/azurerm.storage/#storage)
* [Riferimenti Windows PowerShell](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
