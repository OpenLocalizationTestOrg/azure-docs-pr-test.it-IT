---
title: Montare una condivisione file di Azure e accedere alla condivisione in Windows | Microsoft Docs
description: Montare una condivisione file di Azure e accedere alla condivisione in Windows.
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
ms.openlocfilehash: e911e787cd1e29b2bbeaa648869c50245f2dd9ba
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="mount-an-azure-file-share-and-access-the-share-in-windows"></a><span data-ttu-id="0be50-103">Montare una condivisione file di Azure e accedere alla condivisione in Windows</span><span class="sxs-lookup"><span data-stu-id="0be50-103">Mount an Azure File share and access the share in Windows</span></span>
<span data-ttu-id="0be50-104">[Archiviazione file di Azure](storage-dotnet-how-to-use-files.md) è il file system cloud facile da usare di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0be50-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy to use cloud file system.</span></span> <span data-ttu-id="0be50-105">Le condivisioni file di Azure possono essere montate in Windows e Windows Server.</span><span class="sxs-lookup"><span data-stu-id="0be50-105">Azure File shares can be mounted in Windows and Windows Server.</span></span> <span data-ttu-id="0be50-106">Questo articolo illustra tre diversi modi per montare una condivisione file di Azure in Windows: con l'interfaccia utente di Esplora file, tramite PowerShell e tramite il prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="0be50-106">This article shows three different ways to mount an Azure File share on Windows: with the File Explorer UI, via PowerShell, and via the Command Prompt.</span></span> 

<span data-ttu-id="0be50-107">Per montare una condivisione file di Azure al di fuori dell'area di Azure in cui è ospitata, ad esempio in locale o in un'area di Azure diversa, il sistema operativo deve supportare SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="0be50-107">In order to mount an Azure File share outside of the Azure region it is hosted in, such as on-premises or in a different Azure region, the OS must support SMB 3.0.</span></span> 

<span data-ttu-id="0be50-108">La condivisione file di Azure può essere montata nel computer Windows in locale o in una VM di Azure a seconda della versione del sistema operativo,</span><span class="sxs-lookup"><span data-stu-id="0be50-108">Azure File share can be mounted on Windows machine either on-premises or in Azure VM depending on OS version.</span></span> <span data-ttu-id="0be50-109">come illustrato nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="0be50-109">Below table illustrates the</span></span> 

| <span data-ttu-id="0be50-110">Versione di Windows</span><span class="sxs-lookup"><span data-stu-id="0be50-110">Windows Version</span></span>        | <span data-ttu-id="0be50-111">Versione SMB</span><span class="sxs-lookup"><span data-stu-id="0be50-111">SMB Version</span></span> |<span data-ttu-id="0be50-112">Montabile in VM di Azure</span><span class="sxs-lookup"><span data-stu-id="0be50-112">Mountable On Azure VM</span></span>|<span data-ttu-id="0be50-113">Montabile in locale</span><span class="sxs-lookup"><span data-stu-id="0be50-113">Mountable On-Premise</span></span>|
|------------------------|-------------|---------------------|---------------------|
| <span data-ttu-id="0be50-114">Windows 7</span><span class="sxs-lookup"><span data-stu-id="0be50-114">Windows 7</span></span>              | <span data-ttu-id="0be50-115">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="0be50-115">SMB 2.1</span></span>     | <span data-ttu-id="0be50-116">Sì</span><span class="sxs-lookup"><span data-stu-id="0be50-116">Yes</span></span>                 | <span data-ttu-id="0be50-117">No</span><span class="sxs-lookup"><span data-stu-id="0be50-117">No</span></span>                  |
| <span data-ttu-id="0be50-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="0be50-118">Windows Server 2008 R2</span></span> | <span data-ttu-id="0be50-119">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="0be50-119">SMB 2.1</span></span>     | <span data-ttu-id="0be50-120">Sì</span><span class="sxs-lookup"><span data-stu-id="0be50-120">Yes</span></span>                 | <span data-ttu-id="0be50-121">No</span><span class="sxs-lookup"><span data-stu-id="0be50-121">No</span></span>                  |
| <span data-ttu-id="0be50-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="0be50-122">Windows 8</span></span>              | <span data-ttu-id="0be50-123">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="0be50-123">SMB 3.0</span></span>     | <span data-ttu-id="0be50-124">Sì</span><span class="sxs-lookup"><span data-stu-id="0be50-124">Yes</span></span>                 | <span data-ttu-id="0be50-125">Sì</span><span class="sxs-lookup"><span data-stu-id="0be50-125">Yes</span></span>                 |
| <span data-ttu-id="0be50-126">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="0be50-126">Windows Server 2012</span></span>    | <span data-ttu-id="0be50-127">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="0be50-127">SMB 3.0</span></span>     | <span data-ttu-id="0be50-128">Sì</span><span class="sxs-lookup"><span data-stu-id="0be50-128">Yes</span></span>                 | <span data-ttu-id="0be50-129">Sì</span><span class="sxs-lookup"><span data-stu-id="0be50-129">Yes</span></span>                 |
| <span data-ttu-id="0be50-130">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0be50-130">Windows Server 2012 R2</span></span> | <span data-ttu-id="0be50-131">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="0be50-131">SMB 3.0</span></span>     | <span data-ttu-id="0be50-132">Sì</span><span class="sxs-lookup"><span data-stu-id="0be50-132">Yes</span></span>                 | <span data-ttu-id="0be50-133">Sì</span><span class="sxs-lookup"><span data-stu-id="0be50-133">Yes</span></span>                 |
| <span data-ttu-id="0be50-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="0be50-134">Windows 10</span></span>             | <span data-ttu-id="0be50-135">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="0be50-135">SMB 3.0</span></span>     | <span data-ttu-id="0be50-136">Sì</span><span class="sxs-lookup"><span data-stu-id="0be50-136">Yes</span></span>                 | <span data-ttu-id="0be50-137">Sì</span><span class="sxs-lookup"><span data-stu-id="0be50-137">Yes</span></span>                 |

> [!Note]  
> <span data-ttu-id="0be50-138">È sempre consigliabile seguire l'articolo della KB più recente per la propria versione di Windows.</span><span class="sxs-lookup"><span data-stu-id="0be50-138">We always recommend taking the most recent KB for your version of Windows.</span></span>

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a><span data-ttu-id="0be50-139"></a>Prerequisiti per il montaggio della condivisione file di Azure con Windows</span><span class="sxs-lookup"><span data-stu-id="0be50-139"></a>Prerequisites for Mounting Azure File Share with Windows</span></span> 
* <span data-ttu-id="0be50-140">**Nome dell'account di archiviazione**: per montare una condivisione file di Azure, sarà necessario il nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0be50-140">**Storage Account Name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="0be50-141">**Chiave dell'account di archiviazione**: per montare una condivisione file di Azure, sarà necessaria la chiave dell'account primaria (o secondaria).</span><span class="sxs-lookup"><span data-stu-id="0be50-141">**Storage Account Key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="0be50-142">Le chiavi di firma di accesso condiviso non sono attualmente supportate per il montaggio.</span><span class="sxs-lookup"><span data-stu-id="0be50-142">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="0be50-143">**Assicurarsi che la porta 445 sia aperta**: Archiviazione file di Azure usa il protocollo SMB.</span><span class="sxs-lookup"><span data-stu-id="0be50-143">**Ensure port 445 is open**: Azure File storage uses SMB protocol.</span></span> <span data-ttu-id="0be50-144">SMB comunica tramite la porta TCP 445: verificare che il firewall non blocchi le porte TCP 445 dal computer client.</span><span class="sxs-lookup"><span data-stu-id="0be50-144">SMB communicates over TCP port 445 - check to see if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-the-azure-file-share-with-file-explorer"></a><span data-ttu-id="0be50-145">Montare la condivisione file di Azure con Esplora file</span><span class="sxs-lookup"><span data-stu-id="0be50-145">Mount the Azure File share with File Explorer</span></span>
> [!Note]  
> <span data-ttu-id="0be50-146">Tenere presente che le istruzioni seguenti si basano su Windows 10 e potrebbero essere leggermente diverse per le versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="0be50-146">Note that the following instructions are shown on Windows 10 and may differ slightly on older releases.</span></span> 

1. <span data-ttu-id="0be50-147">**Aprire Esplora file**: per eseguire questa operazione, aprire il menu Start o premere i tasti di scelta rapida Win+E.</span><span class="sxs-lookup"><span data-stu-id="0be50-147">**Open File Explorer**: This can be done by opening from the Start Menu, or by pressing Win+E shortcut.</span></span>

2. <span data-ttu-id="0be50-148">**Passare all'elemento "Questo PC" a sinistra della finestra. Verranno cambiati i menu disponibili sulla barra multifunzione. Scegliere "Connetti unità di rete" dal menu Computer**.</span><span class="sxs-lookup"><span data-stu-id="0be50-148">**Navigate to the "This PC" item on the left-hand side of the window. This will change the menus available in the ribbon. Under the Computer menu, select "Map Network Drive"**.</span></span>
    
    ![Screenshot del menu a discesa "Connetti unità di rete"](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. <span data-ttu-id="0be50-150">**Copiare il percorso UNC dal riquadro "Connetti" nel portale di Azure**: per una descrizione dettagliata di come trovare queste informazioni, vedere [qui](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span><span class="sxs-lookup"><span data-stu-id="0be50-150">**Copy the UNC path from the "Connect" pane in the Azure portal**: A detailed description of how to find this information can be found [here](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span></span>

    ![Il percorso UNC dal riquadro Connetti di Archiviazione file di Azure](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. <span data-ttu-id="0be50-152">**Selezionare la lettera di unità e immettere il percorso UNC.**</span><span class="sxs-lookup"><span data-stu-id="0be50-152">**Select the Drive letter and enter the UNC path.**</span></span> 
    
    ![Screenshot della finestra di dialogo "Connetti unità di rete"](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. <span data-ttu-id="0be50-154">**Usare il nome account di archiviazione preceduto da `Azure\` come nome utente e una chiave dell'account di archiviazione come password.**</span><span class="sxs-lookup"><span data-stu-id="0be50-154">**Use the Storage Account Name prepended with `Azure\` as the username and a Storage Account Key as the password.**</span></span>
    
    ![Screenshot della finestra di dialogo delle credenziali di rete](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. <span data-ttu-id="0be50-156">**Usare la condivisione file di Azure nel modo desiderato**.</span><span class="sxs-lookup"><span data-stu-id="0be50-156">**Use Azure File share as desired**.</span></span>
    
    ![La condivisione file di Azure viene ora montata](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. <span data-ttu-id="0be50-158">**Per smontare (o disconnettere) la condivisione file di Azure, fare clic con il pulsante destro del mouse sulla voce relativa alla condivisione in "Percorsi di rete" in Esplora file e scegliere "Disconnetti"**.</span><span class="sxs-lookup"><span data-stu-id="0be50-158">**When you are ready to dismount (or disconnect) the Azure File share, you can do so by right clicking on the entry for the share under the "Network locations" in File Explorer and selecting "Disconnect"**.</span></span>

## <a name="mount-the-azure-file-share-with-powershell"></a><span data-ttu-id="0be50-159">Montare la condivisione file di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="0be50-159">Mount the Azure File share with PowerShell</span></span>
1. <span data-ttu-id="0be50-160">**Usare il comando seguente per montare la condivisione file di Azure**: ricordare di sostituire `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` con le informazioni appropriate.</span><span class="sxs-lookup"><span data-stu-id="0be50-160">**Use the following command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with the proper information.</span></span>

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. <span data-ttu-id="0be50-161">**Usare la condivisione file di Azure nel modo desiderato**.</span><span class="sxs-lookup"><span data-stu-id="0be50-161">**Use the Azure File share as desired**.</span></span>

3. <span data-ttu-id="0be50-162">**Al termine, smontare la condivisione file di Azure usando il comando seguente**.</span><span class="sxs-lookup"><span data-stu-id="0be50-162">**When you are finished, dismount the Azure File share using the following command**.</span></span>

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> <span data-ttu-id="0be50-163">È possibile usare il parametro `-Persist` in `New-PSDrive` per rendere la condivisione file di Azure visibile al resto del sistema operativo durante il montaggio.</span><span class="sxs-lookup"><span data-stu-id="0be50-163">You may use the `-Persist` parameter on `New-PSDrive` to make the Azure File share visible to the rest of the OS while mounted.</span></span>

## <a name="mount-the-azure-file-share-with-command-prompt"></a><span data-ttu-id="0be50-164">Montare la condivisione file di Azure con il prompt dei comandi</span><span class="sxs-lookup"><span data-stu-id="0be50-164">Mount the Azure File share with Command Prompt</span></span>
1. <span data-ttu-id="0be50-165">**Usare il comando seguente per montare la condivisione file di Azure**: ricordare di sostituire `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` con le informazioni appropriate.</span><span class="sxs-lookup"><span data-stu-id="0be50-165">**Use the following command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with the proper information.</span></span>

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. <span data-ttu-id="0be50-166">**Usare la condivisione file di Azure nel modo desiderato**.</span><span class="sxs-lookup"><span data-stu-id="0be50-166">**Use the Azure File share as desired**.</span></span>

3. <span data-ttu-id="0be50-167">**Al termine, smontare la condivisione file di Azure usando il comando seguente**.</span><span class="sxs-lookup"><span data-stu-id="0be50-167">**When you are finished, dismount the Azure File share using the following command**.</span></span>

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> <span data-ttu-id="0be50-168">È possibile configurare la condivisione file di Azure per la riconnessione automatica al riavvio rendendo persistenti le credenziali in Windows.</span><span class="sxs-lookup"><span data-stu-id="0be50-168">You can configure the Azure File share to automatically reconnect on reboot by persisting the credentials in Windows.</span></span> <span data-ttu-id="0be50-169">Il comando seguente renderà persistenti le credenziali:</span><span class="sxs-lookup"><span data-stu-id="0be50-169">The following command will persist the credentials:</span></span>
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a><span data-ttu-id="0be50-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0be50-170">Next steps</span></span>
<span data-ttu-id="0be50-171">Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="0be50-171">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="0be50-172">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="0be50-172">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="0be50-173">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="0be50-173">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="0be50-174">Articoli concettuali e video</span><span class="sxs-lookup"><span data-stu-id="0be50-174">Conceptual articles and videos</span></span>
* [<span data-ttu-id="0be50-175">Archiviazione di file in Azure: un file system SMB nel cloud senza problemi per Windows e Linux</span><span class="sxs-lookup"><span data-stu-id="0be50-175">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="0be50-176">Come usare Archiviazione file di Azure con Linux</span><span class="sxs-lookup"><span data-stu-id="0be50-176">How to use Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="0be50-177">Supporto degli strumenti per Archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="0be50-177">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="0be50-178">Uso di Azure PowerShell con Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="0be50-178">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="0be50-179">Come usare AzCopy con Archiviazione di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0be50-179">How to use AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="0be50-180">Utilizzo dell'interfaccia della riga di comando di Azure con archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="0be50-180">Using the Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="0be50-181">Risoluzione dei problemi di archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="0be50-181">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a><span data-ttu-id="0be50-182">Post di BLOG</span><span class="sxs-lookup"><span data-stu-id="0be50-182">Blog posts</span></span>
* [<span data-ttu-id="0be50-183">Archiviazione file di Azure è attualmente disponibile a livello generale</span><span class="sxs-lookup"><span data-stu-id="0be50-183">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="0be50-184">Inside Azure File storage (Analisi di Archiviazione file di Azure)</span><span class="sxs-lookup"><span data-stu-id="0be50-184">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="0be50-185">Introduzione al servizio File di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0be50-185">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="0be50-186">Migrating data to Azure File (Migrazione dei dati in File di Azure)</span><span class="sxs-lookup"><span data-stu-id="0be50-186">Migrating data to Azure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="0be50-187">Riferimento</span><span class="sxs-lookup"><span data-stu-id="0be50-187">Reference</span></span>
* [<span data-ttu-id="0be50-188">Informazioni di riferimento sulla libreria client di archiviazione per .NET</span><span class="sxs-lookup"><span data-stu-id="0be50-188">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="0be50-189">Riferimento API REST del servizio File</span><span class="sxs-lookup"><span data-stu-id="0be50-189">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
