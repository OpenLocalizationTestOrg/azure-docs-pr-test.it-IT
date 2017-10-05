---
title: Rendere persistenti i file in Azure Cloud Shell (Anteprima) | Microsoft Docs
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
ms.openlocfilehash: 61a8bfcf3704f361432400771d8fcc8b81927b53
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a><span data-ttu-id="25374-103">Rendere persistenti i file in Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="25374-103">Persist files in Azure Cloud Shell</span></span>
<span data-ttu-id="25374-104">Cloud Shell si avvale dell'archiviazione file di Azure per rendere persistenti i file in più sessioni.</span><span class="sxs-lookup"><span data-stu-id="25374-104">Cloud Shell takes advantage of Azure File storage to persist files across sessions.</span></span>

## <a name="set-up-a-clouddrive-file-share"></a><span data-ttu-id="25374-105">Configurare una condivisione file `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="25374-105">Set up a `clouddrive` file share</span></span>
<span data-ttu-id="25374-106">Al primo avvio Cloud Shell richiede di associare una condivisione file nuova o esistente per mantenere i file in più sessioni.</span><span class="sxs-lookup"><span data-stu-id="25374-106">On initial start, Cloud Shell prompts you to associate a new or existing file share to persist files across sessions.</span></span>

### <a name="create-new-storage"></a><span data-ttu-id="25374-107">Creare una nuova risorsa di archiviazione</span><span class="sxs-lookup"><span data-stu-id="25374-107">Create new storage</span></span>

<span data-ttu-id="25374-108">Quando si usano le impostazioni di base e si seleziona una sola sottoscrizione, Cloud Shell crea tre risorse per conto dell'utente nell'area di Azure supportata più vicina all'utente:</span><span class="sxs-lookup"><span data-stu-id="25374-108">When you use basic settings and select only a subscription, Cloud Shell creates three resources on your behalf in the supported region that's nearest to you:</span></span>
* <span data-ttu-id="25374-109">Gruppo di risorse: `cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="25374-109">Resource group: `cloud-shell-storage-<region>`</span></span>
* <span data-ttu-id="25374-110">Account di archiviazione: `cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="25374-110">Storage account: `cs<uniqueGuid>`</span></span>
* <span data-ttu-id="25374-111">Condivisione file: `cs-<user>-<domain>-com-<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="25374-111">File share: `cs-<user>-<domain>-com-<uniqueGuid>`</span></span>

![Impostazione della sottoscrizione](media/basic-storage.png)

<span data-ttu-id="25374-113">La condivisione viene montata come `clouddrive` nella directory `$Home`.</span><span class="sxs-lookup"><span data-stu-id="25374-113">The file share mounts as `clouddrive` in your `$Home` directory.</span></span> <span data-ttu-id="25374-114">La condivisione file viene usata anche per archiviare un'immagine da 5 GB creata automaticamente, che si aggiorna automaticamente e rende persistente la directory `$Home`.</span><span class="sxs-lookup"><span data-stu-id="25374-114">The file share is also used to store a 5-GB image that's created for you and that automatically updates and persists your `$Home` directory.</span></span> <span data-ttu-id="25374-115">Questa azione viene eseguita una sola volta e la condivisione file viene ripetuta automaticamente nelle sessioni successive.</span><span class="sxs-lookup"><span data-stu-id="25374-115">This is a one-time action, and the file share mounts automatically in subsequent sessions.</span></span>

### <a name="use-existing-resources"></a><span data-ttu-id="25374-116">Usare le risorse esistenti</span><span class="sxs-lookup"><span data-stu-id="25374-116">Use existing resources</span></span>

<span data-ttu-id="25374-117">Con l'opzione Avanzate è possibile associare risorse esistenti.</span><span class="sxs-lookup"><span data-stu-id="25374-117">By using the advanced option, you can associate existing resources.</span></span> <span data-ttu-id="25374-118">Al prompt di impostazione dell'archiviazione, selezionare **Mostra impostazioni avanzate** per visualizzare le opzioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="25374-118">When the storage setup prompt appears, select **Show advanced settings** to view additional options.</span></span> <span data-ttu-id="25374-119">Le condivisioni file esistenti ricevono un'immagine utente di 5 GB per mantenere persistente la directory `$Home`.</span><span class="sxs-lookup"><span data-stu-id="25374-119">Existing file shares receive a 5-GB user image to persist your `$Home` directory.</span></span> <span data-ttu-id="25374-120">I menu a discesa vengono filtrati in base all'area Cloud Shell e agli account di archiviazione con ridondanza locale e geografica.</span><span class="sxs-lookup"><span data-stu-id="25374-120">The drop-down menus are filtered for your Cloud Shell region and for local-redundant & geo-redundant storage accounts.</span></span>

![Impostazione del gruppo di risorse](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a><span data-ttu-id="25374-122">Limitare la creazione di risorse con i criteri delle risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="25374-122">Restrict resource creation with an Azure resource policy</span></span>
<span data-ttu-id="25374-123">Gli account di archiviazione che si creano in Cloud Shell sono contrassegnati con `ms-resource-usage:azure-cloud-shell`.</span><span class="sxs-lookup"><span data-stu-id="25374-123">Storage accounts that you create in Cloud Shell are tagged with `ms-resource-usage:azure-cloud-shell`.</span></span> <span data-ttu-id="25374-124">Se si desidera impedire agli utenti di creare account di archiviazione con Cloud Shell, creare [criteri di risorse di Azure per tag](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) che vengono attivati dal tag specificato.</span><span class="sxs-lookup"><span data-stu-id="25374-124">If you want to disallow users from creating storage accounts in Cloud Shell, create an [Azure resource policy for tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) that are triggered by this specific tag.</span></span>

## <a name="how-cloud-shell-works"></a><span data-ttu-id="25374-125">Funzionamento di Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="25374-125">How Cloud Shell works</span></span>
<span data-ttu-id="25374-126">Cloud Shell rende persistenti i file tramite entrambe le modalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="25374-126">Cloud Shell persists files through both of the following methods:</span></span>
* <span data-ttu-id="25374-127">Creazione di un'immagine del disco della directory `$Home` per rendere persistenti tutti i contenuti della directory.</span><span class="sxs-lookup"><span data-stu-id="25374-127">Creating a disk image of your `$Home` directory to persist all contents within the directory.</span></span> <span data-ttu-id="25374-128">L'immagine del disco viene salvata nella condivisione file specificata come `acc_<User>.img` in `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img` e le modifiche vengono automaticamente sincronizzate.</span><span class="sxs-lookup"><span data-stu-id="25374-128">The disk image is saved in your specified file share as `acc_<User>.img` at `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, and it automatically syncs changes.</span></span>

* <span data-ttu-id="25374-129">Montaggio della condivisione file specificata come `clouddrive` nella directory `$Home` per l'interazione diretta con la condivisione file.</span><span class="sxs-lookup"><span data-stu-id="25374-129">Mounting your specified file share as `clouddrive` in your `$Home` directory for direct file share interaction.</span></span> <span data-ttu-id="25374-130">Viene eseguito il mapping di `/Home/<User>/clouddrive` a `fileshare.storage.windows.net/fileshare`.</span><span class="sxs-lookup"><span data-stu-id="25374-130">`/Home/<User>/clouddrive` is mapped to `fileshare.storage.windows.net/fileshare`.</span></span>
 
> [!NOTE]
> <span data-ttu-id="25374-131">Tutti i file della directory `$Home`, come le chiavi SSH, vengono mantenuti nell'immagine del disco utente archiviata nella condivisione file montata.</span><span class="sxs-lookup"><span data-stu-id="25374-131">All files in your `$Home` directory, such as SSH keys, are persisted in your user disk image, which is stored in your mounted file share.</span></span> <span data-ttu-id="25374-132">Applicare le procedure consigliate quando si rendono persistenti le informazioni nella directory `$Home` e nella condivisione file montata.</span><span class="sxs-lookup"><span data-stu-id="25374-132">Apply best practices when you persist information in your `$Home` directory and mounted file share.</span></span>

## <a name="use-the-clouddrive-command"></a><span data-ttu-id="25374-133">Usare il comando `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="25374-133">Use the `clouddrive` command</span></span>
<span data-ttu-id="25374-134">Con Cloud Shell è possibile eseguire un comando denominato `clouddrive`, che consente di aggiornare manualmente la condivisione file montata in Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="25374-134">With Cloud Shell, you can run a command called `clouddrive`, which enables you to manually update the file share that's mounted to Cloud Shell.</span></span>
<span data-ttu-id="25374-135">![Esecuzione del comando "clouddrive"](media/clouddrive-h.png)</span><span class="sxs-lookup"><span data-stu-id="25374-135">![Running the "clouddrive" command](media/clouddrive-h.png)</span></span>

## <a name="mount-a-new-clouddrive"></a><span data-ttu-id="25374-136">Montare un nuovo elemento `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="25374-136">Mount a new `clouddrive`</span></span>

### <a name="prerequisites-for-manual-mounting"></a><span data-ttu-id="25374-137">Prerequisiti per il montaggio manuale</span><span class="sxs-lookup"><span data-stu-id="25374-137">Prerequisites for manual mounting</span></span>
<span data-ttu-id="25374-138">È possibile aggiornare la condivisione file associata a Cloud Shell usando il comando `clouddrive mount`.</span><span class="sxs-lookup"><span data-stu-id="25374-138">You can update the file share that's associated with Cloud Shell by using the `clouddrive mount` command.</span></span>

<span data-ttu-id="25374-139">Se si monta una condivisione file esistente, gli account di archiviazione devono avere le caratteristiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="25374-139">If you mount an existing file share, the storage accounts must be:</span></span>
* <span data-ttu-id="25374-140">Essere account di archiviazione con ridondanza locale o geografica per supportare le condivisioni file.</span><span class="sxs-lookup"><span data-stu-id="25374-140">Locally-redundant storage or geo-redundant storage to support file shares.</span></span>
* <span data-ttu-id="25374-141">Trovarsi nell'area assegnata.</span><span class="sxs-lookup"><span data-stu-id="25374-141">Located in your assigned region.</span></span> <span data-ttu-id="25374-142">Durante l'onboarding, l'area a cui si è assegnati viene elencata nel nome del gruppo di risorse `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="25374-142">When you are onboarding, the region you are assigned to is listed in the resource group name `cloud-shell-storage-<region>`.</span></span>

### <a name="supported-storage-regions"></a><span data-ttu-id="25374-143">Aree di archiviazione supportate</span><span class="sxs-lookup"><span data-stu-id="25374-143">Supported storage regions</span></span>
<span data-ttu-id="25374-144">I file di Azure devono risiedere nella stessa area del computer Cloud Shell in cui vengono montati.</span><span class="sxs-lookup"><span data-stu-id="25374-144">The Azure files must reside in the same region as the Cloud Shell machine that you're mounting them to.</span></span> <span data-ttu-id="25374-145">I cluster Cloud Shell esistono attualmente nelle aree seguenti:</span><span class="sxs-lookup"><span data-stu-id="25374-145">Cloud Shell clusters currently exist in the following regions:</span></span>
|<span data-ttu-id="25374-146">Area</span><span class="sxs-lookup"><span data-stu-id="25374-146">Area</span></span>|<span data-ttu-id="25374-147">Region</span><span class="sxs-lookup"><span data-stu-id="25374-147">Region</span></span>|
|---|---|
|<span data-ttu-id="25374-148">Americhe</span><span class="sxs-lookup"><span data-stu-id="25374-148">Americas</span></span>|<span data-ttu-id="25374-149">Stati Uniti orientali, Stati Uniti centro-meridionali, Stati Uniti occidentali</span><span class="sxs-lookup"><span data-stu-id="25374-149">East US, South Central US, West US</span></span>|
|<span data-ttu-id="25374-150">Europa</span><span class="sxs-lookup"><span data-stu-id="25374-150">Europe</span></span>|<span data-ttu-id="25374-151">Europa settentrionale, Europa occidentale</span><span class="sxs-lookup"><span data-stu-id="25374-151">North Europe, West Europe</span></span>|
|<span data-ttu-id="25374-152">Asia/Pacifico</span><span class="sxs-lookup"><span data-stu-id="25374-152">Asia Pacific</span></span>|<span data-ttu-id="25374-153">India centrale, Asia sud-orientale</span><span class="sxs-lookup"><span data-stu-id="25374-153">India Central, Southeast Asia</span></span>|

### <a name="the-clouddrive-mount-command"></a><span data-ttu-id="25374-154">Comando `clouddrive mount`</span><span class="sxs-lookup"><span data-stu-id="25374-154">The `clouddrive mount` command</span></span>

> [!NOTE]
> <span data-ttu-id="25374-155">Se si monta una nuova condivisione file, viene creata una nuova immagine utente per la directory `$Home` perché l'immagine di `$Home` precedente viene mantenuta nella condivisione file precedente.</span><span class="sxs-lookup"><span data-stu-id="25374-155">If you're mounting a new file share, a new user image is created for your `$Home` directory, because your previous `$Home` image is kept in the previous file share.</span></span>

<span data-ttu-id="25374-156">Eseguire il comando `clouddrive mount` con i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="25374-156">Run the `clouddrive mount` command with the following parameters:</span></span>

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

<span data-ttu-id="25374-157">Per visualizzare altri dettagli, eseguire `clouddrive mount -h`, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="25374-157">To view more details, run `clouddrive mount -h`, as shown here:</span></span>

![Esecuzione del comando `clouddrive mount`](media/mount-h.png)

## <a name="unmount-clouddrive"></a><span data-ttu-id="25374-159">Smontare `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="25374-159">Unmount `clouddrive`</span></span>
<span data-ttu-id="25374-160">È possibile smontare in qualsiasi momento una condivisione file montata in Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="25374-160">You can unmount a file share that's mounted to Cloud Shell at any time.</span></span> <span data-ttu-id="25374-161">Dopo la disinstallazione della condivisione file verrà richiesto di installare una nuova condivisione file prima della sessione successiva.</span><span class="sxs-lookup"><span data-stu-id="25374-161">Once your file share is unmounted, you will be prompted to mount a new file share prior to your next session.</span></span>

<span data-ttu-id="25374-162">Per rimuovere una condivisione file da Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="25374-162">To remove a file share from Cloud Shell:</span></span>
1. <span data-ttu-id="25374-163">Eseguire `clouddrive unmount`.</span><span class="sxs-lookup"><span data-stu-id="25374-163">Run `clouddrive unmount`.</span></span>
2. <span data-ttu-id="25374-164">Accettare e confermare i prompt.</span><span class="sxs-lookup"><span data-stu-id="25374-164">Acknowledge and confirm the prompts.</span></span>

<span data-ttu-id="25374-165">La condivisione file continuerà a esistere a meno che non venga eliminata manualmente.</span><span class="sxs-lookup"><span data-stu-id="25374-165">Your file share will continue to exist unless you delete it manually.</span></span> <span data-ttu-id="25374-166">Cloud Shell non eseguirà più la ricerca di questa condivisione file nelle sessioni successive.</span><span class="sxs-lookup"><span data-stu-id="25374-166">Cloud Shell will no longer search for this file share on subsequent sessions.</span></span>

<span data-ttu-id="25374-167">Per visualizzare altri dettagli, eseguire `clouddrive unmount -h`, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="25374-167">To view more details, run `clouddrive unmount -h`, as shown here:</span></span>

![Esecuzione del comando "clouddrive unmount"](media/unmount-h.png)

> [!WARNING]
> <span data-ttu-id="25374-169">L'esecuzione di questo comando non elimina alcuna risorsa.</span><span class="sxs-lookup"><span data-stu-id="25374-169">Running this command will not delete any resources.</span></span> <span data-ttu-id="25374-170">L'eliminazione manuale del gruppo di risorse, dell'account di archiviazione o della condivisione file di cui è stato eseguito il mapping a Cloud Shell cancellerà l'immagine del disco della directory `$Home` ed eventuali altri file presenti nella condivisione file.</span><span class="sxs-lookup"><span data-stu-id="25374-170">Manually deleting a resource group, storage account, or file share that is mapped to Cloud Shell will permanently delete your `$Home` directory image and any other files in your file share.</span></span> <span data-ttu-id="25374-171">Questa azione non può essere annullata.</span><span class="sxs-lookup"><span data-stu-id="25374-171">This action cannot be undone.</span></span>

## <a name="list-clouddrive-file-shares"></a><span data-ttu-id="25374-172">Elencare le condivisioni file `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="25374-172">List `clouddrive` file shares</span></span>
<span data-ttu-id="25374-173">Per sapere quale condivisione file è montata come `clouddrive`, eseguire il comando `df` seguente.</span><span class="sxs-lookup"><span data-stu-id="25374-173">To discover which file share is mounted as `clouddrive`, run the following `df` command.</span></span> 

<span data-ttu-id="25374-174">Il percorso file a clouddrive indica il nome dell'account di archiviazione e la condivisione file nell'URL.</span><span class="sxs-lookup"><span data-stu-id="25374-174">The file path to clouddrive shows your storage account name and file share in the URL.</span></span> <span data-ttu-id="25374-175">Ad esempio, `//storageaccountname.file.core.windows.net/filesharename`</span><span class="sxs-lookup"><span data-stu-id="25374-175">For example, `//storageaccountname.file.core.windows.net/filesharename`</span></span>

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

## <a name="transfer-local-files-to-cloud-shell"></a><span data-ttu-id="25374-176">Trasferire file locali in Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="25374-176">Transfer local files to Cloud Shell</span></span>
<span data-ttu-id="25374-177">La directory `clouddrive` viene sincronizzata con il pannello di archiviazione del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="25374-177">The `clouddrive` directory syncs with the Azure portal storage blade.</span></span> <span data-ttu-id="25374-178">Usare questo pannello per trasferire file locali da e verso la condivisione file.</span><span class="sxs-lookup"><span data-stu-id="25374-178">Use this blade to transfer local files to or from your file share.</span></span> <span data-ttu-id="25374-179">L'aggiornamento dei file dall'interno di Cloud Shell si riflette nell'interfaccia utente grafica di archiviazione file quando il pannello viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="25374-179">Updating files from within Cloud Shell is reflected in the file storage GUI when you refresh the blade.</span></span>

### <a name="download-files"></a><span data-ttu-id="25374-180">Download dei file</span><span class="sxs-lookup"><span data-stu-id="25374-180">Download files</span></span>

![Elenco di file locali](media/download.png)
1. <span data-ttu-id="25374-182">Nel portale di Azure passare alla condivisione file montata.</span><span class="sxs-lookup"><span data-stu-id="25374-182">In the Azure portal, go to the mounted file share.</span></span>
2. <span data-ttu-id="25374-183">Selezionare il file di destinazione.</span><span class="sxs-lookup"><span data-stu-id="25374-183">Select the target file.</span></span>
3. <span data-ttu-id="25374-184">Fare clic sul pulsante **Download**.</span><span class="sxs-lookup"><span data-stu-id="25374-184">Select the **Download** button.</span></span>

### <a name="upload-files"></a><span data-ttu-id="25374-185">Caricare file</span><span class="sxs-lookup"><span data-stu-id="25374-185">Upload files</span></span>

![File locali da caricare](media/upload.png)
1. <span data-ttu-id="25374-187">Passare alla condivisione file montata.</span><span class="sxs-lookup"><span data-stu-id="25374-187">Go to your mounted file share.</span></span>
2. <span data-ttu-id="25374-188">Selezionare il pulsante **Carica**.</span><span class="sxs-lookup"><span data-stu-id="25374-188">Select the **Upload** button.</span></span>
3. <span data-ttu-id="25374-189">Selezionare uno o più file che si desidera caricare.</span><span class="sxs-lookup"><span data-stu-id="25374-189">Select the file or files that you want to upload.</span></span>
4. <span data-ttu-id="25374-190">Confermare il caricamento.</span><span class="sxs-lookup"><span data-stu-id="25374-190">Confirm the upload.</span></span>

<span data-ttu-id="25374-191">Si dovrebbe a questo punto vedere che è possibile accedere ai file nella directory `clouddrive` in Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="25374-191">You should now see the files that are accessible in your `clouddrive` directory in Cloud Shell.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25374-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25374-192">Next steps</span></span>
[<span data-ttu-id="25374-193">Avvio rapido di Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="25374-193">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="25374-194">
[Informazioni sull'archiviazione file di Azure](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span><span class="sxs-lookup"><span data-stu-id="25374-194">
[Learn about Azure File storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span></span> <br><span data-ttu-id="25374-195">
[Informazioni sui tag di archiviazione](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span><span class="sxs-lookup"><span data-stu-id="25374-195">
[Learn about storage tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span></span> <br>
