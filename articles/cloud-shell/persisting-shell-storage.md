---
title: file aaaPersist nella Shell di Cloud di Azure (anteprima) | Documenti Microsoft
description: Procedura dettagliata su come Azure Cloud Shell rende persistenti i file.
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: b230453d5551c545553d63559741950206e4f1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a><span data-ttu-id="7b88e-103">Rendere persistenti i file in Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="7b88e-103">Persist files in Azure Cloud Shell</span></span>
<span data-ttu-id="7b88e-104">Shell cloud consente di sfruttare i file toopersist di archiviazione di File di Azure tra le sessioni.</span><span class="sxs-lookup"><span data-stu-id="7b88e-104">Cloud Shell takes advantage of Azure File storage toopersist files across sessions.</span></span>

## <a name="set-up-a-clouddrive-file-share"></a><span data-ttu-id="7b88e-105">Configurare una condivisione file `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="7b88e-105">Set up a `clouddrive` file share</span></span>
<span data-ttu-id="7b88e-106">All'avvio iniziale, Shell Cloud richiede tooassociate condivisione file nuovo o esistente di file toopersist tra sessioni.</span><span class="sxs-lookup"><span data-stu-id="7b88e-106">On initial start, Cloud Shell prompts you tooassociate a new or existing file share toopersist files across sessions.</span></span>

### <a name="create-new-storage"></a><span data-ttu-id="7b88e-107">Creare una nuova risorsa di archiviazione</span><span class="sxs-lookup"><span data-stu-id="7b88e-107">Create new storage</span></span>

<span data-ttu-id="7b88e-108">Quando si utilizzano le impostazioni di base e selezionare solo una sottoscrizione, Shell di Cloud crea tre risorse per conto dell'utente nell'area di hello supportato più vicino al tooyou:</span><span class="sxs-lookup"><span data-stu-id="7b88e-108">When you use basic settings and select only a subscription, Cloud Shell creates three resources on your behalf in hello supported region that's nearest tooyou:</span></span>
* <span data-ttu-id="7b88e-109">Gruppo di risorse: `cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="7b88e-109">Resource group: `cloud-shell-storage-<region>`</span></span>
* <span data-ttu-id="7b88e-110">Account di archiviazione: `cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="7b88e-110">Storage account: `cs<uniqueGuid>`</span></span>
* <span data-ttu-id="7b88e-111">Condivisione file: `cs-<user>-<domain>-com-<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="7b88e-111">File share: `cs-<user>-<domain>-com-<uniqueGuid>`</span></span>

![impostazioni di sottoscrizione Hello](media/basic-storage.png)

<span data-ttu-id="7b88e-113">condivisione di file Hello collega come `clouddrive` nel `$Home` directory.</span><span class="sxs-lookup"><span data-stu-id="7b88e-113">hello file share mounts as `clouddrive` in your `$Home` directory.</span></span> <span data-ttu-id="7b88e-114">Hello condivisione file è anche usato toostore un'immagine di 5 GB che viene creata automaticamente per l'utente e che gli aggiornamenti e viene mantenuta la `$Home` directory.</span><span class="sxs-lookup"><span data-stu-id="7b88e-114">hello file share is also used toostore a 5-GB image that's created for you and that automatically updates and persists your `$Home` directory.</span></span> <span data-ttu-id="7b88e-115">Si tratta di un'azione singola e condivisione di file hello Monta automaticamente nelle sessioni successive.</span><span class="sxs-lookup"><span data-stu-id="7b88e-115">This is a one-time action, and hello file share mounts automatically in subsequent sessions.</span></span>

### <a name="use-existing-resources"></a><span data-ttu-id="7b88e-116">Usare le risorse esistenti</span><span class="sxs-lookup"><span data-stu-id="7b88e-116">Use existing resources</span></span>

<span data-ttu-id="7b88e-117">Tramite l'opzione avanzata hello, è possibile associare le risorse esistenti.</span><span class="sxs-lookup"><span data-stu-id="7b88e-117">By using hello advanced option, you can associate existing resources.</span></span> <span data-ttu-id="7b88e-118">Quando viene visualizzata hello archiviazione installazione richiesta, selezionare **Mostra impostazioni avanzate** tooview ulteriori opzioni.</span><span class="sxs-lookup"><span data-stu-id="7b88e-118">When hello storage setup prompt appears, select **Show advanced settings** tooview additional options.</span></span> <span data-ttu-id="7b88e-119">Condivisioni di file esistenti ricevono un toopersist immagine utente 5 GB il `$Home` directory.</span><span class="sxs-lookup"><span data-stu-id="7b88e-119">Existing file shares receive a 5-GB user image toopersist your `$Home` directory.</span></span> <span data-ttu-id="7b88e-120">menu a discesa Hello vengono filtrati per paese Shell Cloud e per gli account di archiviazione con ridondanza geografica e con ridondanza locale.</span><span class="sxs-lookup"><span data-stu-id="7b88e-120">hello drop-down menus are filtered for your Cloud Shell region and for local-redundant & geo-redundant storage accounts.</span></span>

![impostazione di gruppo di risorse Hello](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a><span data-ttu-id="7b88e-122">Limitare la creazione di risorse con i criteri delle risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="7b88e-122">Restrict resource creation with an Azure resource policy</span></span>
<span data-ttu-id="7b88e-123">Gli account di archiviazione che si creano in Cloud Shell sono contrassegnati con `ms-resource-usage:azure-cloud-shell`.</span><span class="sxs-lookup"><span data-stu-id="7b88e-123">Storage accounts that you create in Cloud Shell are tagged with `ms-resource-usage:azure-cloud-shell`.</span></span> <span data-ttu-id="7b88e-124">Se si desidera che gli utenti toodisallow dalla creazione di account di archiviazione in Cloud Shell, creare un [criteri delle risorse di Azure per i tag](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) che vengono attivate da questo tag specifico.</span><span class="sxs-lookup"><span data-stu-id="7b88e-124">If you want toodisallow users from creating storage accounts in Cloud Shell, create an [Azure resource policy for tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) that are triggered by this specific tag.</span></span>

## <a name="how-cloud-shell-works"></a><span data-ttu-id="7b88e-125">Funzionamento di Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="7b88e-125">How Cloud Shell works</span></span>
<span data-ttu-id="7b88e-126">Shell cloud persiste file tramite entrambi hello dei seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="7b88e-126">Cloud Shell persists files through both of hello following methods:</span></span>
* <span data-ttu-id="7b88e-127">Creazione di un'immagine di disco del `$Home` toopersist directory tutti contenuto all'interno di directory hello.</span><span class="sxs-lookup"><span data-stu-id="7b88e-127">Creating a disk image of your `$Home` directory toopersist all contents within hello directory.</span></span> <span data-ttu-id="7b88e-128">immagine del disco Hello viene salvato nella condivisione di file specificato come `acc_<User>.img` in `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, e venga eseguita automaticamente la sincronizzazione delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="7b88e-128">hello disk image is saved in your specified file share as `acc_<User>.img` at `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, and it automatically syncs changes.</span></span>

* <span data-ttu-id="7b88e-129">Montaggio della condivisione file specificata come `clouddrive` nella directory `$Home` per l'interazione diretta con la condivisione file.</span><span class="sxs-lookup"><span data-stu-id="7b88e-129">Mounting your specified file share as `clouddrive` in your `$Home` directory for direct file share interaction.</span></span> <span data-ttu-id="7b88e-130">`/Home/<User>/clouddrive`viene eseguito il mapping troppo`fileshare.storage.windows.net/fileshare`.</span><span class="sxs-lookup"><span data-stu-id="7b88e-130">`/Home/<User>/clouddrive` is mapped too`fileshare.storage.windows.net/fileshare`.</span></span>
 
> [!NOTE]
> <span data-ttu-id="7b88e-131">Tutti i file della directory `$Home`, come le chiavi SSH, vengono mantenuti nell'immagine del disco utente archiviata nella condivisione file montata.</span><span class="sxs-lookup"><span data-stu-id="7b88e-131">All files in your `$Home` directory, such as SSH keys, are persisted in your user disk image, which is stored in your mounted file share.</span></span> <span data-ttu-id="7b88e-132">Applicare le procedure consigliate quando si rendono persistenti le informazioni nella directory `$Home` e nella condivisione file montata.</span><span class="sxs-lookup"><span data-stu-id="7b88e-132">Apply best practices when you persist information in your `$Home` directory and mounted file share.</span></span>

## <a name="use-hello-clouddrive-command"></a><span data-ttu-id="7b88e-133">Hello utilizzare `clouddrive` comando</span><span class="sxs-lookup"><span data-stu-id="7b88e-133">Use hello `clouddrive` command</span></span>
<span data-ttu-id="7b88e-134">Con la Shell di Cloud, è possibile eseguire un comando denominato `clouddrive`, che consente di toomanually aggiornamento hello condivisione file che tooCloud montato Shell.</span><span class="sxs-lookup"><span data-stu-id="7b88e-134">With Cloud Shell, you can run a command called `clouddrive`, which enables you toomanually update hello file share that's mounted tooCloud Shell.</span></span>
<span data-ttu-id="7b88e-135">![Comando di "clouddrive" hello in esecuzione](media/clouddrive-h.png)</span><span class="sxs-lookup"><span data-stu-id="7b88e-135">![Running hello "clouddrive" command](media/clouddrive-h.png)</span></span>

## <a name="mount-a-new-clouddrive"></a><span data-ttu-id="7b88e-136">Montare un nuovo elemento `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="7b88e-136">Mount a new `clouddrive`</span></span>

### <a name="prerequisites-for-manual-mounting"></a><span data-ttu-id="7b88e-137">Prerequisiti per il montaggio manuale</span><span class="sxs-lookup"><span data-stu-id="7b88e-137">Prerequisites for manual mounting</span></span>
<span data-ttu-id="7b88e-138">È possibile aggiornare una condivisione di file hello associata Cloud Shell utilizzando hello `clouddrive mount` comando.</span><span class="sxs-lookup"><span data-stu-id="7b88e-138">You can update hello file share that's associated with Cloud Shell by using hello `clouddrive mount` command.</span></span>

<span data-ttu-id="7b88e-139">Se si monta una condivisione di file esistente, deve essere l'account di archiviazione hello:</span><span class="sxs-lookup"><span data-stu-id="7b88e-139">If you mount an existing file share, hello storage accounts must be:</span></span>
* <span data-ttu-id="7b88e-140">Archiviazione con ridondanza locale o condivisioni di file di archiviazione con ridondanza geografica toosupport.</span><span class="sxs-lookup"><span data-stu-id="7b88e-140">Locally-redundant storage or geo-redundant storage toosupport file shares.</span></span>
* <span data-ttu-id="7b88e-141">Trovarsi nell'area assegnata.</span><span class="sxs-lookup"><span data-stu-id="7b88e-141">Located in your assigned region.</span></span> <span data-ttu-id="7b88e-142">Quando si è onboarding, area hello vengono assegnati toois elencati nella casella Nome gruppo di risorse hello `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="7b88e-142">When you are onboarding, hello region you are assigned toois listed in hello resource group name `cloud-shell-storage-<region>`.</span></span>

### <a name="supported-storage-regions"></a><span data-ttu-id="7b88e-143">Aree di archiviazione supportate</span><span class="sxs-lookup"><span data-stu-id="7b88e-143">Supported storage regions</span></span>
<span data-ttu-id="7b88e-144">Hello Azure file devono risiedere in hello stessa area hello Cloud Shell macchina che si sta montaggio per.</span><span class="sxs-lookup"><span data-stu-id="7b88e-144">hello Azure files must reside in hello same region as hello Cloud Shell machine that you're mounting them to.</span></span> <span data-ttu-id="7b88e-145">I cluster Shell cloud attualmente esistono nel hello seguenti aree:</span><span class="sxs-lookup"><span data-stu-id="7b88e-145">Cloud Shell clusters currently exist in hello following regions:</span></span>
|<span data-ttu-id="7b88e-146">Area</span><span class="sxs-lookup"><span data-stu-id="7b88e-146">Area</span></span>|<span data-ttu-id="7b88e-147">Region</span><span class="sxs-lookup"><span data-stu-id="7b88e-147">Region</span></span>|
|---|---|
|<span data-ttu-id="7b88e-148">Americhe</span><span class="sxs-lookup"><span data-stu-id="7b88e-148">Americas</span></span>|<span data-ttu-id="7b88e-149">Stati Uniti orientali, Stati Uniti centro-meridionali, Stati Uniti occidentali</span><span class="sxs-lookup"><span data-stu-id="7b88e-149">East US, South Central US, West US</span></span>|
|<span data-ttu-id="7b88e-150">Europa</span><span class="sxs-lookup"><span data-stu-id="7b88e-150">Europe</span></span>|<span data-ttu-id="7b88e-151">Europa settentrionale, Europa occidentale</span><span class="sxs-lookup"><span data-stu-id="7b88e-151">North Europe, West Europe</span></span>|
|<span data-ttu-id="7b88e-152">Asia/Pacifico</span><span class="sxs-lookup"><span data-stu-id="7b88e-152">Asia Pacific</span></span>|<span data-ttu-id="7b88e-153">India centrale, Asia sud-orientale</span><span class="sxs-lookup"><span data-stu-id="7b88e-153">India Central, Southeast Asia</span></span>|

### <a name="hello-clouddrive-mount-command"></a><span data-ttu-id="7b88e-154">Hello `clouddrive mount` comando</span><span class="sxs-lookup"><span data-stu-id="7b88e-154">hello `clouddrive mount` command</span></span>

> [!NOTE]
> <span data-ttu-id="7b88e-155">Se si sta il montaggio di una nuova condivisione file, una nuova immagine utente viene creata per il `$Home` directory, in quanto precedente `$Home` immagine viene mantenuta nella condivisione di file precedente hello.</span><span class="sxs-lookup"><span data-stu-id="7b88e-155">If you're mounting a new file share, a new user image is created for your `$Home` directory, because your previous `$Home` image is kept in hello previous file share.</span></span>

<span data-ttu-id="7b88e-156">Eseguire hello `clouddrive mount` con hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="7b88e-156">Run hello `clouddrive mount` command with hello following parameters:</span></span>

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

<span data-ttu-id="7b88e-157">eseguire ulteriori dettagli, tooview `clouddrive mount -h`, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7b88e-157">tooview more details, run `clouddrive mount -h`, as shown here:</span></span>

![Hello in esecuzione ' clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a><span data-ttu-id="7b88e-159">Smontare `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="7b88e-159">Unmount `clouddrive`</span></span>
<span data-ttu-id="7b88e-160">È possibile effettuare lo smontaggio di una condivisione di file della Shell che tooCloud montati in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="7b88e-160">You can unmount a file share that's mounted tooCloud Shell at any time.</span></span> <span data-ttu-id="7b88e-161">Dopo aver disinstallata la condivisione di file, sarà richiesta toomount un nuovo tooyour preliminare di condivisione file sessione successiva.</span><span class="sxs-lookup"><span data-stu-id="7b88e-161">Once your file share is unmounted, you will be prompted toomount a new file share prior tooyour next session.</span></span>

<span data-ttu-id="7b88e-162">un file tooremove condividere dalla Shell di Cloud:</span><span class="sxs-lookup"><span data-stu-id="7b88e-162">tooremove a file share from Cloud Shell:</span></span>
1. <span data-ttu-id="7b88e-163">Eseguire `clouddrive unmount`.</span><span class="sxs-lookup"><span data-stu-id="7b88e-163">Run `clouddrive unmount`.</span></span>
2. <span data-ttu-id="7b88e-164">Conoscenza e hello prompt di conferma.</span><span class="sxs-lookup"><span data-stu-id="7b88e-164">Acknowledge and confirm hello prompts.</span></span>

<span data-ttu-id="7b88e-165">Condivisione di file continuerà tooexist a meno che non si elimina manualmente.</span><span class="sxs-lookup"><span data-stu-id="7b88e-165">Your file share will continue tooexist unless you delete it manually.</span></span> <span data-ttu-id="7b88e-166">Cloud Shell non eseguirà più la ricerca di questa condivisione file nelle sessioni successive.</span><span class="sxs-lookup"><span data-stu-id="7b88e-166">Cloud Shell will no longer search for this file share on subsequent sessions.</span></span>

<span data-ttu-id="7b88e-167">eseguire ulteriori dettagli, tooview `clouddrive unmount -h`, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7b88e-167">tooview more details, run `clouddrive unmount -h`, as shown here:</span></span>

![Hello in esecuzione ' clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> <span data-ttu-id="7b88e-169">L'esecuzione di questo comando non elimina alcuna risorsa.</span><span class="sxs-lookup"><span data-stu-id="7b88e-169">Running this command will not delete any resources.</span></span> <span data-ttu-id="7b88e-170">Eliminazione manuale di un gruppo di risorse, account di archiviazione o condivisione file che è stato eseguito il mapping tooCloud Shell eliminerà definitivamente la `$Home` immagine di directory e qualsiasi altro file nella condivisione di file.</span><span class="sxs-lookup"><span data-stu-id="7b88e-170">Manually deleting a resource group, storage account, or file share that is mapped tooCloud Shell will permanently delete your `$Home` directory image and any other files in your file share.</span></span> <span data-ttu-id="7b88e-171">Questa azione non può essere annullata.</span><span class="sxs-lookup"><span data-stu-id="7b88e-171">This action cannot be undone.</span></span>

## <a name="list-clouddrive-file-shares"></a><span data-ttu-id="7b88e-172">Elencare le condivisioni file `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="7b88e-172">List `clouddrive` file shares</span></span>
<span data-ttu-id="7b88e-173">quali condivisione file è montato come toodiscover `clouddrive`, eseguire il seguente hello `df` comando.</span><span class="sxs-lookup"><span data-stu-id="7b88e-173">toodiscover which file share is mounted as `clouddrive`, run hello following `df` command.</span></span> 

<span data-ttu-id="7b88e-174">tooclouddrive percorso di file Hello mostra che il nome account di archiviazione e della condivisione file nell'URL hello.</span><span class="sxs-lookup"><span data-stu-id="7b88e-174">hello file path tooclouddrive shows your storage account name and file share in hello URL.</span></span> <span data-ttu-id="7b88e-175">Ad esempio, `//storageaccountname.file.core.windows.net/filesharename`</span><span class="sxs-lookup"><span data-stu-id="7b88e-175">For example, `//storageaccountname.file.core.windows.net/filesharename`</span></span>

```
justin@Azure:~$ df
Filesystem                                               1K-blocks     Used Available Use% Mounted on
overlay                                                   30428648 15585636  14826628  52% /
tmpfs                                                       986704        0    986704   0% /dev
tmpfs                                                       986704        0    986704   0% /sys/fs/cgroup
/dev/sda1                                                 30428648 15585636  14826628  52% /etc/hosts
shm                                                          65536        0     65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName        6291456  5242944   1048512  84% /usr/justin/clouddrive
/dev/loop0                                                 5160576   601652   4296780  13% /home/justin
```

## <a name="transfer-local-files-toocloud-shell"></a><span data-ttu-id="7b88e-176">Trasferimento file locali tooCloud Shell</span><span class="sxs-lookup"><span data-stu-id="7b88e-176">Transfer local files tooCloud Shell</span></span>
<span data-ttu-id="7b88e-177">Hello `clouddrive` esegue la sincronizzazione directory con il pannello di archiviazione del portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7b88e-177">hello `clouddrive` directory syncs with hello Azure portal storage blade.</span></span> <span data-ttu-id="7b88e-178">Utilizzare questo tooor di file locali pannello tootransfer dalla condivisione di file.</span><span class="sxs-lookup"><span data-stu-id="7b88e-178">Use this blade tootransfer local files tooor from your file share.</span></span> <span data-ttu-id="7b88e-179">Aggiornare i file nella Shell di Cloud viene riflessa nell'archiviazione di file hello GUI quando si aggiorna il pannello hello.</span><span class="sxs-lookup"><span data-stu-id="7b88e-179">Updating files from within Cloud Shell is reflected in hello file storage GUI when you refresh hello blade.</span></span>

### <a name="download-files"></a><span data-ttu-id="7b88e-180">Download dei file</span><span class="sxs-lookup"><span data-stu-id="7b88e-180">Download files</span></span>

![Elenco di file locali](media/download.png)
1. <span data-ttu-id="7b88e-182">Nel portale di Azure hello, andare toohello condivisione di file montati.</span><span class="sxs-lookup"><span data-stu-id="7b88e-182">In hello Azure portal, go toohello mounted file share.</span></span>
2. <span data-ttu-id="7b88e-183">Selezionare il file di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="7b88e-183">Select hello target file.</span></span>
3. <span data-ttu-id="7b88e-184">Seleziona hello **scaricare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="7b88e-184">Select hello **Download** button.</span></span>

### <a name="upload-files"></a><span data-ttu-id="7b88e-185">Caricare file</span><span class="sxs-lookup"><span data-stu-id="7b88e-185">Upload files</span></span>

![File locali toobe caricato](media/upload.png)
1. <span data-ttu-id="7b88e-187">Passare tooyour montati condivisione file.</span><span class="sxs-lookup"><span data-stu-id="7b88e-187">Go tooyour mounted file share.</span></span>
2. <span data-ttu-id="7b88e-188">Seleziona hello **caricare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="7b88e-188">Select hello **Upload** button.</span></span>
3. <span data-ttu-id="7b88e-189">Selezionare hello o i file che si desidera tooupload.</span><span class="sxs-lookup"><span data-stu-id="7b88e-189">Select hello file or files that you want tooupload.</span></span>
4. <span data-ttu-id="7b88e-190">Verificare il caricamento di hello.</span><span class="sxs-lookup"><span data-stu-id="7b88e-190">Confirm hello upload.</span></span>

<span data-ttu-id="7b88e-191">Dovrebbe essere file hello che sono accessibili nel `clouddrive` directory nella Shell di Cloud.</span><span class="sxs-lookup"><span data-stu-id="7b88e-191">You should now see hello files that are accessible in your `clouddrive` directory in Cloud Shell.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b88e-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7b88e-192">Next steps</span></span>
[<span data-ttu-id="7b88e-193">Avvio rapido di Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="7b88e-193">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="7b88e-194">
[Informazioni sull'archiviazione file di Azure](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span><span class="sxs-lookup"><span data-stu-id="7b88e-194">
[Learn about Azure File storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span></span> <br><span data-ttu-id="7b88e-195">
[Informazioni sui tag di archiviazione](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span><span class="sxs-lookup"><span data-stu-id="7b88e-195">
[Learn about storage tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span></span> <br>
