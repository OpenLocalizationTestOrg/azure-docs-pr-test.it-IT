---
title: aaaMount una condivisione di File di Azure e hello accesso condividono Windows | Documenti Microsoft
description: Montare una condivisione di File di Azure e la condivisione di hello access in Windows.
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 15ac468d9d7b8e0a195b024926ed4dd9790360d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a><span data-ttu-id="acf62-103">Montare una condivisione di File di Azure e la condivisione di hello access in Windows</span><span class="sxs-lookup"><span data-stu-id="acf62-103">Mount an Azure File share and access hello share in Windows</span></span>
<span data-ttu-id="acf62-104">[Archiviazione di Azure File](storage-dotnet-how-to-use-files.md) è facile toouse cloud file sistema Microsoft.</span><span class="sxs-lookup"><span data-stu-id="acf62-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="acf62-105">Le condivisioni file di Azure possono essere montate in Windows e Windows Server.</span><span class="sxs-lookup"><span data-stu-id="acf62-105">Azure File shares can be mounted in Windows and Windows Server.</span></span> <span data-ttu-id="acf62-106">Questo articolo illustra tre modi diversi toomount una condivisione di File di Azure in Windows: con interfaccia utente di Esplora File, tramite PowerShell e tramite il prompt dei comandi di hello hello.</span><span class="sxs-lookup"><span data-stu-id="acf62-106">This article shows three different ways toomount an Azure File share on Windows: with hello File Explorer UI, via PowerShell, and via hello Command Prompt.</span></span> 

<span data-ttu-id="acf62-107">Ordine toomount un File di Azure condividono di fuori di hello regione di Azure è ospitato in, ad esempio in locale o in un'area diversa di Azure, hello del sistema operativo deve supportare SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="acf62-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support SMB 3.0.</span></span> 

<span data-ttu-id="acf62-108">La condivisione file di Azure può essere montata nel computer Windows in locale o in una VM di Azure a seconda della versione del sistema operativo,</span><span class="sxs-lookup"><span data-stu-id="acf62-108">Azure File share can be mounted on Windows machine either on-premises or in Azure VM depending on OS version.</span></span> <span data-ttu-id="acf62-109">Tabella che segue illustra hello</span><span class="sxs-lookup"><span data-stu-id="acf62-109">Below table illustrates hello</span></span> 

| <span data-ttu-id="acf62-110">Versione di Windows</span><span class="sxs-lookup"><span data-stu-id="acf62-110">Windows Version</span></span>        | <span data-ttu-id="acf62-111">Versione SMB</span><span class="sxs-lookup"><span data-stu-id="acf62-111">SMB Version</span></span> |<span data-ttu-id="acf62-112">Montabile in VM di Azure</span><span class="sxs-lookup"><span data-stu-id="acf62-112">Mountable On Azure VM</span></span>|<span data-ttu-id="acf62-113">Montabile in locale</span><span class="sxs-lookup"><span data-stu-id="acf62-113">Mountable On-Premise</span></span>|
|------------------------|-------------|---------------------|---------------------|
| <span data-ttu-id="acf62-114">Windows 7</span><span class="sxs-lookup"><span data-stu-id="acf62-114">Windows 7</span></span>              | <span data-ttu-id="acf62-115">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="acf62-115">SMB 2.1</span></span>     | <span data-ttu-id="acf62-116">Sì</span><span class="sxs-lookup"><span data-stu-id="acf62-116">Yes</span></span>                 | <span data-ttu-id="acf62-117">No</span><span class="sxs-lookup"><span data-stu-id="acf62-117">No</span></span>                  |
| <span data-ttu-id="acf62-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="acf62-118">Windows Server 2008 R2</span></span> | <span data-ttu-id="acf62-119">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="acf62-119">SMB 2.1</span></span>     | <span data-ttu-id="acf62-120">Sì</span><span class="sxs-lookup"><span data-stu-id="acf62-120">Yes</span></span>                 | <span data-ttu-id="acf62-121">No</span><span class="sxs-lookup"><span data-stu-id="acf62-121">No</span></span>                  |
| <span data-ttu-id="acf62-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="acf62-122">Windows 8</span></span>              | <span data-ttu-id="acf62-123">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="acf62-123">SMB 3.0</span></span>     | <span data-ttu-id="acf62-124">Sì</span><span class="sxs-lookup"><span data-stu-id="acf62-124">Yes</span></span>                 | <span data-ttu-id="acf62-125">Sì</span><span class="sxs-lookup"><span data-stu-id="acf62-125">Yes</span></span>                 |
| <span data-ttu-id="acf62-126">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="acf62-126">Windows Server 2012</span></span>    | <span data-ttu-id="acf62-127">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="acf62-127">SMB 3.0</span></span>     | <span data-ttu-id="acf62-128">Sì</span><span class="sxs-lookup"><span data-stu-id="acf62-128">Yes</span></span>                 | <span data-ttu-id="acf62-129">Sì</span><span class="sxs-lookup"><span data-stu-id="acf62-129">Yes</span></span>                 |
| <span data-ttu-id="acf62-130">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="acf62-130">Windows Server 2012 R2</span></span> | <span data-ttu-id="acf62-131">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="acf62-131">SMB 3.0</span></span>     | <span data-ttu-id="acf62-132">Sì</span><span class="sxs-lookup"><span data-stu-id="acf62-132">Yes</span></span>                 | <span data-ttu-id="acf62-133">Sì</span><span class="sxs-lookup"><span data-stu-id="acf62-133">Yes</span></span>                 |
| <span data-ttu-id="acf62-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="acf62-134">Windows 10</span></span>             | <span data-ttu-id="acf62-135">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="acf62-135">SMB 3.0</span></span>     | <span data-ttu-id="acf62-136">Sì</span><span class="sxs-lookup"><span data-stu-id="acf62-136">Yes</span></span>                 | <span data-ttu-id="acf62-137">Sì</span><span class="sxs-lookup"><span data-stu-id="acf62-137">Yes</span></span>                 |

> [!Note]  
> <span data-ttu-id="acf62-138">È sempre consigliabile acquisire hello KB più recente per la versione di Windows.</span><span class="sxs-lookup"><span data-stu-id="acf62-138">We always recommend taking hello most recent KB for your version of Windows.</span></span>

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a><span data-ttu-id="acf62-139"></a>Prerequisiti per il montaggio della condivisione file di Azure con Windows</span><span class="sxs-lookup"><span data-stu-id="acf62-139"></a>Prerequisites for Mounting Azure File Share with Windows</span></span> 
* <span data-ttu-id="acf62-140">**Nome Account di archiviazione**: condividere un File di Azure toomount, si sarà necessario hello nome dell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="acf62-140">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="acf62-141">**Chiave dell'Account di archiviazione**: condividere un File di Azure toomount, si sarà necessario hello chiave di archiviazione primaria (o secondario).</span><span class="sxs-lookup"><span data-stu-id="acf62-141">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="acf62-142">Le chiavi di firma di accesso condiviso non sono attualmente supportate per il montaggio.</span><span class="sxs-lookup"><span data-stu-id="acf62-142">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="acf62-143">**Assicurarsi che la porta 445 sia aperta**: Archiviazione file di Azure usa il protocollo SMB.</span><span class="sxs-lookup"><span data-stu-id="acf62-143">**Ensure port 445 is open**: Azure File storage uses SMB protocol.</span></span> <span data-ttu-id="acf62-144">SMB comunica sulla porta TCP 445 - controllare toosee se il firewall non blocchi le porte TCP 445 da computer client.</span><span class="sxs-lookup"><span data-stu-id="acf62-144">SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-with-file-explorer"></a><span data-ttu-id="acf62-145">Montare hello Azure in una condivisione con Esplora File</span><span class="sxs-lookup"><span data-stu-id="acf62-145">Mount hello Azure File share with File Explorer</span></span>
> [!Note]  
> <span data-ttu-id="acf62-146">Si noti che hello attenendosi alle istruzioni presenti in Windows 10 e possono differire leggermente in versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="acf62-146">Note that hello following instructions are shown on Windows 10 and may differ slightly on older releases.</span></span> 

1. <span data-ttu-id="acf62-147">**Aprire Esplora File**: si possono eseguire aprendo dal Menu Start hello o premendo scelta Win + E.</span><span class="sxs-lookup"><span data-stu-id="acf62-147">**Open File Explorer**: This can be done by opening from hello Start Menu, or by pressing Win+E shortcut.</span></span>

2. <span data-ttu-id="acf62-148">**Passare l'elemento di "Questo PC" toohello sul lato sinistro hello della finestra hello. Menu hello disponibili nella barra multifunzione hello verrà modificato. Selezionare "Connetti unità di rete" dal menu Computer hello**.</span><span class="sxs-lookup"><span data-stu-id="acf62-148">**Navigate toohello "This PC" item on hello left-hand side of hello window. This will change hello menus available in hello ribbon. Under hello Computer menu, select "Map Network Drive"**.</span></span>
    
    ![Menu a discesa una schermata di hello "Connetti unità di rete"](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. <span data-ttu-id="acf62-150">**Percorso UNC di hello copia dal riquadro "Connetti" hello nel portale di Azure hello**: una descrizione dettagliata delle modalità toofind queste informazioni sono reperibili [qui](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span><span class="sxs-lookup"><span data-stu-id="acf62-150">**Copy hello UNC path from hello "Connect" pane in hello Azure portal**: A detailed description of how toofind this information can be found [here](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span></span>

    ![percorso UNC Hello dal riquadro Connetti archiviazione dei File di Azure hello](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. <span data-ttu-id="acf62-152">**Selezionare la lettera di unità hello e immettere il percorso UNC hello.**</span><span class="sxs-lookup"><span data-stu-id="acf62-152">**Select hello Drive letter and enter hello UNC path.**</span></span> 
    
    ![Una schermata della finestra di dialogo "Connetti unità di rete" hello](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. <span data-ttu-id="acf62-154">**Hello di utilizzare il nome di Account di archiviazione preceduto da `Azure\` come nome utente hello e una chiave di Account di archiviazione come password hello.**</span><span class="sxs-lookup"><span data-stu-id="acf62-154">**Use hello Storage Account Name prepended with `Azure\` as hello username and a Storage Account Key as hello password.**</span></span>
    
    ![Una schermata della finestra di dialogo hello rete](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. <span data-ttu-id="acf62-156">**Usare la condivisione file di Azure nel modo desiderato**.</span><span class="sxs-lookup"><span data-stu-id="acf62-156">**Use Azure File share as desired**.</span></span>
    
    ![La condivisione file di Azure viene ora montata](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. <span data-ttu-id="acf62-158">**Quando si toodismount pronto (o disconnettersi) in una condivisione hello Azure, è possibile farlo facendo clic sulla voce hello per condivisione hello in hello "percorsi di rete" in Esplora File e selezionando "Disconnetti"**.</span><span class="sxs-lookup"><span data-stu-id="acf62-158">**When you are ready toodismount (or disconnect) hello Azure File share, you can do so by right clicking on hello entry for hello share under hello "Network locations" in File Explorer and selecting "Disconnect"**.</span></span>

## <a name="mount-hello-azure-file-share-with-powershell"></a><span data-ttu-id="acf62-159">Montare hello Azure in una condivisione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="acf62-159">Mount hello Azure File share with PowerShell</span></span>
1. <span data-ttu-id="acf62-160">**Comando che segue di hello utilizzare Condivisione di File di Azure hello toomount**: ricordare tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` con le informazioni appropriate hello.</span><span class="sxs-lookup"><span data-stu-id="acf62-160">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. <span data-ttu-id="acf62-161">**Condivisione di File di Azure usare hello in base alle esigenze**.</span><span class="sxs-lookup"><span data-stu-id="acf62-161">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="acf62-162">**Al termine, smontare hello Azure condivisione File che utilizza hello comando seguente**.</span><span class="sxs-lookup"><span data-stu-id="acf62-162">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> <span data-ttu-id="acf62-163">È possibile utilizzare hello `-Persist` parametro `New-PSDrive` toomake hello rest toohello visibile di condivisione File di Azure di hello del sistema operativo mentre montato.</span><span class="sxs-lookup"><span data-stu-id="acf62-163">You may use hello `-Persist` parameter on `New-PSDrive` toomake hello Azure File share visible toohello rest of hello OS while mounted.</span></span>

## <a name="mount-hello-azure-file-share-with-command-prompt"></a><span data-ttu-id="acf62-164">Condivisione di File di Azure hello con il prompt dei comandi di montaggio</span><span class="sxs-lookup"><span data-stu-id="acf62-164">Mount hello Azure File share with Command Prompt</span></span>
1. <span data-ttu-id="acf62-165">**Comando che segue di hello utilizzare Condivisione di File di Azure hello toomount**: ricordare tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` con le informazioni appropriate hello.</span><span class="sxs-lookup"><span data-stu-id="acf62-165">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. <span data-ttu-id="acf62-166">**Condivisione di File di Azure usare hello in base alle esigenze**.</span><span class="sxs-lookup"><span data-stu-id="acf62-166">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="acf62-167">**Al termine, smontare hello Azure condivisione File che utilizza hello comando seguente**.</span><span class="sxs-lookup"><span data-stu-id="acf62-167">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> <span data-ttu-id="acf62-168">È possibile configurare hello Azure File condivisione tooautomatically riconnettersi al riavvio del sistema per rendere persistenti le credenziali di hello in Windows.</span><span class="sxs-lookup"><span data-stu-id="acf62-168">You can configure hello Azure File share tooautomatically reconnect on reboot by persisting hello credentials in Windows.</span></span> <span data-ttu-id="acf62-169">comando seguente Hello manterrà le credenziali di hello:</span><span class="sxs-lookup"><span data-stu-id="acf62-169">hello following command will persist hello credentials:</span></span>
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a><span data-ttu-id="acf62-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="acf62-170">Next steps</span></span>
<span data-ttu-id="acf62-171">Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="acf62-171">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="acf62-172">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="acf62-172">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="acf62-173">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="acf62-173">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="acf62-174">Articoli concettuali e video</span><span class="sxs-lookup"><span data-stu-id="acf62-174">Conceptual articles and videos</span></span>
* [<span data-ttu-id="acf62-175">Archiviazione di file in Azure: un file system SMB nel cloud senza problemi per Windows e Linux</span><span class="sxs-lookup"><span data-stu-id="acf62-175">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="acf62-176">Come toouse archiviazione di File di Azure con Linux</span><span class="sxs-lookup"><span data-stu-id="acf62-176">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="acf62-177">Supporto degli strumenti per Archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="acf62-177">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="acf62-178">Uso di Azure PowerShell con Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="acf62-178">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="acf62-179">Come toouse AzCopy con archiviazione di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="acf62-179">How toouse AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="acf62-180">Con l'archiviazione di Azure hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="acf62-180">Using hello Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="acf62-181">Risoluzione dei problemi di archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="acf62-181">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a><span data-ttu-id="acf62-182">Post di BLOG</span><span class="sxs-lookup"><span data-stu-id="acf62-182">Blog posts</span></span>
* [<span data-ttu-id="acf62-183">Archiviazione file di Azure è attualmente disponibile a livello generale</span><span class="sxs-lookup"><span data-stu-id="acf62-183">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="acf62-184">Inside Azure File storage (Analisi di Archiviazione file di Azure)</span><span class="sxs-lookup"><span data-stu-id="acf62-184">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="acf62-185">Introduzione al servizio File di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="acf62-185">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="acf62-186">La migrazione dei dati tooAzure File</span><span class="sxs-lookup"><span data-stu-id="acf62-186">Migrating data tooAzure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="acf62-187">riferimento</span><span class="sxs-lookup"><span data-stu-id="acf62-187">Reference</span></span>
* [<span data-ttu-id="acf62-188">Informazioni di riferimento sulla libreria client di archiviazione per .NET</span><span class="sxs-lookup"><span data-stu-id="acf62-188">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="acf62-189">Riferimento API REST del servizio File</span><span class="sxs-lookup"><span data-stu-id="acf62-189">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
