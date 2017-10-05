---
title: Note sulla versione di Microsoft Azure Storage Explorer (anteprima) | Microsoft Docs
description: Note sulla versione di Microsoft Azure Storage Explorer (anteprima)
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 63a24f6b153390533bba0888fd1051508c65bf6e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a><span data-ttu-id="4821a-103">Note sulla versione di Microsoft Azure Storage Explorer (anteprima)</span><span class="sxs-lookup"><span data-stu-id="4821a-103">Microsoft Azure Storage Explorer (Preview) release notes</span></span>

<span data-ttu-id="4821a-104">Questo articolo contiene le note sulla versione di anteprima di Azure Storage Explorer 0.8.16, nonché sulle versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="4821a-104">This article contains the release notes for Azure Storage Explorer 0.8.16 (Preview) release, as well as release notes for previous versions.</span></span>

<span data-ttu-id="4821a-105">[Microsoft Azure Storage Explorer (anteprima)](./vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma che consente di usare facilmente dati di Archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="4821a-105">[Microsoft Azure Storage Explorer (Preview)](./vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you to easily work with Azure Storage data on Windows, macOS, and Linux.</span></span>

## <a name="version-0816-preview"></a><span data-ttu-id="4821a-106">Versione 0.8.16 (anteprima)</span><span class="sxs-lookup"><span data-stu-id="4821a-106">Version 0.8.16 (Preview)</span></span>
<span data-ttu-id="4821a-107">21/08/2017</span><span class="sxs-lookup"><span data-stu-id="4821a-107">8/21/2017</span></span>

### <a name="download-azure-storage-explorer-0816-preview"></a><span data-ttu-id="4821a-108">Download di Azure Storage Explorer 0.8.16 (anteprima)</span><span class="sxs-lookup"><span data-stu-id="4821a-108">Download Azure Storage Explorer 0.8.16 (Preview)</span></span>
- [<span data-ttu-id="4821a-109">Azure Storage Explorer 0.8.16 (anteprima) per Windows</span><span class="sxs-lookup"><span data-stu-id="4821a-109">Azure Storage Explorer 0.8.16 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=708343)
- [<span data-ttu-id="4821a-110">Azure Storage Explorer 0.8.16 (anteprima) per Mac</span><span class="sxs-lookup"><span data-stu-id="4821a-110">Azure Storage Explorer 0.8.16 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=708342)
- [<span data-ttu-id="4821a-111">Azure Storage Explorer 0.8.16 (anteprima) per Linux</span><span class="sxs-lookup"><span data-stu-id="4821a-111">Azure Storage Explorer 0.8.16 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a><span data-ttu-id="4821a-112">Nuovo</span><span class="sxs-lookup"><span data-stu-id="4821a-112">New</span></span>
* <span data-ttu-id="4821a-113">Quando si apre un BLOB, Storage Explorer richiederà di caricare il file scaricato se viene rilevata una modifica</span><span class="sxs-lookup"><span data-stu-id="4821a-113">When you open a blob, Storage Explorer will prompt you to upload the downloaded file if a change is detected</span></span>
* <span data-ttu-id="4821a-114">Esperienza di accesso ad Azure Stack migliorata</span><span class="sxs-lookup"><span data-stu-id="4821a-114">Enhanced Azure Stack sign-in experience</span></span>
* <span data-ttu-id="4821a-115">Miglioramento delle prestazioni per il caricamento/download contemporanei di molti file di piccole dimensioni</span><span class="sxs-lookup"><span data-stu-id="4821a-115">Improved the performance of uploading/downloading many small files at the same time</span></span>


### <a name="fixes"></a><span data-ttu-id="4821a-116">Correzioni</span><span class="sxs-lookup"><span data-stu-id="4821a-116">Fixes</span></span>
* <span data-ttu-id="4821a-117">Per alcuni tipi di BLOB, la scelta della sostituzione in presenza di un conflitto di caricamento talvolta comporta il riavvio del caricamento.</span><span class="sxs-lookup"><span data-stu-id="4821a-117">For some blob types, choosing to "replace" during an upload conflict would sometimes result in the upload being restarted.</span></span> 
* <span data-ttu-id="4821a-118">Nella versione 0.8.15 i caricamenti rimangono talvolta bloccati al 99%.</span><span class="sxs-lookup"><span data-stu-id="4821a-118">In version 0.8.15, uploads would sometimes stall at 99%.</span></span>
* <span data-ttu-id="4821a-119">Durante il caricamento di file in una condivisione file, se si sceglie di caricare in una directory non ancora esistente, il caricamento ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="4821a-119">When uploading files to a file share, if you chose to upload to a directory which did not yet exist, your upload would fail.</span></span>
* <span data-ttu-id="4821a-120">Storage Explorer generava timestamp non corretti per le firme di accesso condiviso e le query di tabella.</span><span class="sxs-lookup"><span data-stu-id="4821a-120">Storage Explorer was incorrectly generating time stamps for shared access signatures and table queries.</span></span>


<span data-ttu-id="4821a-121">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="4821a-121">Known Issues</span></span>
* <span data-ttu-id="4821a-122">L'uso di una stringa di connessione con nome e chiave attualmente non funziona.</span><span class="sxs-lookup"><span data-stu-id="4821a-122">Using a name and key connection string does not currently work.</span></span> <span data-ttu-id="4821a-123">Questo problema verrà risolto nella prossima versione.</span><span class="sxs-lookup"><span data-stu-id="4821a-123">It will be fixed in the next release.</span></span> <span data-ttu-id="4821a-124">Fino ad allora è possibile collegarsi con nome e chiave.</span><span class="sxs-lookup"><span data-stu-id="4821a-124">Until then you can use attach with name and key.</span></span>
* <span data-ttu-id="4821a-125">Se si tenta di aprire un file con un nome di file di Windows non valido, il download genera un errore di file non trovato.</span><span class="sxs-lookup"><span data-stu-id="4821a-125">If you try to open a file with an invalid Windows file name, the download will result in a file not found error.</span></span>
* <span data-ttu-id="4821a-126">L'azione "Annulla" per un'attività potrebbe impiegare qualche istante per diventare effettiva.</span><span class="sxs-lookup"><span data-stu-id="4821a-126">After clicking "Cancel" on a task, it may take a while for that task to cancel.</span></span> <span data-ttu-id="4821a-127">Si tratta di un limite della libreria di nodi di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4821a-127">This is a limitation of the Azure Storage Node library.</span></span>
* <span data-ttu-id="4821a-128">Dopo aver completato il caricamento di un blob, viene aggiornata la scheda che ha avviato il caricamento.</span><span class="sxs-lookup"><span data-stu-id="4821a-128">After completing a blob upload, the tab which initiated the upload is refreshed.</span></span> <span data-ttu-id="4821a-129">Questa è una modifica rispetto al comportamento precedente. Verrà inoltre visualizzata nuovamente la radice del contenitore in cui ci si trova.</span><span class="sxs-lookup"><span data-stu-id="4821a-129">This is a change from previous behavior, and will also cause you to be taken back to the root of the container you are in.</span></span>
* <span data-ttu-id="4821a-130">Se si sceglie il certificato PIN/smart card non corretto, è necessario il riavvio per fare in modo che Storage Explorer dimentichi tale decisione.</span><span class="sxs-lookup"><span data-stu-id="4821a-130">If you choose the wrong PIN/Smartcard certificate, then you will need to restart in order to have Storage Explorer forget that decision.</span></span>
* <span data-ttu-id="4821a-131">Il pannello delle impostazioni dell'account potrebbe indicare che è necessario immettere nuovamente le credenziali per filtrare le sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="4821a-131">The account settings panel may show that you need to reenter credentials to filter subscriptions.</span></span>
* <span data-ttu-id="4821a-132">La ridenominazione di BLOB singoli o all'interno di un contenitore BLOB rinominato non mantiene gli snapshot.</span><span class="sxs-lookup"><span data-stu-id="4821a-132">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="4821a-133">Tutte le altre proprietà e i metadati di BLOB, file ed entità vengono conservati durante un'operazione di ridenominazione.</span><span class="sxs-lookup"><span data-stu-id="4821a-133">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="4821a-134">Sebbene Azure Stack attualmente non supporta le condivisioni file, viene comunque visualizzato un nodo delle condivisioni di file in un account di archiviazione di Azure Stack associato.</span><span class="sxs-lookup"><span data-stu-id="4821a-134">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span>
* <span data-ttu-id="4821a-135">Per gli utenti di Ubuntu 14.04, è necessario assicurarsi che GCC sia aggiornato. Questa operazione può essere eseguita tramite i comandi seguenti e riavviando successivamente il computer:</span><span class="sxs-lookup"><span data-stu-id="4821a-135">For users on Ubuntu 14.04, you will need to ensure GCC is up to date - this can be done by running the following commands, and then restarting your machine:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* <span data-ttu-id="4821a-136">Per gli utenti di Ubuntu 17.04, è necessario installare GConf. Questa operazione può essere eseguita tramite i comandi seguenti e riavviando successivamente il computer:</span><span class="sxs-lookup"><span data-stu-id="4821a-136">For users on Ubuntu 17.04, you will need to install GConf - this can be done by running the following commands, and then restarting your machine:</span></span>

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a><span data-ttu-id="4821a-137">Versione 0.8.14 (anteprima)</span><span class="sxs-lookup"><span data-stu-id="4821a-137">Version 0.8.14 (Preview)</span></span>
<span data-ttu-id="4821a-138">22/06/2017</span><span class="sxs-lookup"><span data-stu-id="4821a-138">06/22/2017</span></span>

### <a name="download-azure-storage-explorer-0814-preview"></a><span data-ttu-id="4821a-139">Download di Azure Storage Explorer 0.8.14 (anteprima)</span><span class="sxs-lookup"><span data-stu-id="4821a-139">Download Azure Storage Explorer 0.8.14 (Preview)</span></span>
* [<span data-ttu-id="4821a-140">Download di Azure Storage Explorer 0.8.14 (anteprima) per Windows</span><span class="sxs-lookup"><span data-stu-id="4821a-140">Download Azure Storage Explorer 0.8.14 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=809306)
* [<span data-ttu-id="4821a-141">Download di Azure Storage Explorer 0.8.14 (anteprima) per Mac</span><span class="sxs-lookup"><span data-stu-id="4821a-141">Download Azure Storage Explorer 0.8.14 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=809307)
* [<span data-ttu-id="4821a-142">Download di Azure Storage Explorer 0.8.14 (anteprima) per Linux</span><span class="sxs-lookup"><span data-stu-id="4821a-142">Download Azure Storage Explorer 0.8.14 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a><span data-ttu-id="4821a-143">Nuovo</span><span class="sxs-lookup"><span data-stu-id="4821a-143">New</span></span>

* <span data-ttu-id="4821a-144">Versione aggiornata di Electron a 1.7.2 per usufruire di numerosi aggiornamenti importanti sulla sicurezza</span><span class="sxs-lookup"><span data-stu-id="4821a-144">Updated Electron version to 1.7.2 in order to take advantage of several critical security updates</span></span>
* <span data-ttu-id="4821a-145">È ora possibile accedere rapidamente alla guida online di risoluzione dei problemi dal menu Guida</span><span class="sxs-lookup"><span data-stu-id="4821a-145">You can now quickly access the online troubleshooting guide from the help menu</span></span>
* <span data-ttu-id="4821a-146">[Guida][2]alla risoluzione dei problemi di Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="4821a-146">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="4821a-147">[Istruzioni][3]per stabilire la connessione a una sottoscrizione di Azure Stack</span><span class="sxs-lookup"><span data-stu-id="4821a-147">[Instructions][3] on connecting to an Azure Stack subscription</span></span>

### <a name="known-issues"></a><span data-ttu-id="4821a-148">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="4821a-148">Known Issues</span></span>

* <span data-ttu-id="4821a-149">Su Linux, i pulsanti nella finestra di conferma Elimina cartella non vengono registrati con i clic del mouse.</span><span class="sxs-lookup"><span data-stu-id="4821a-149">Buttons on the delete folder confirmation dialog don't register with the mouse clicks on Linux.</span></span> <span data-ttu-id="4821a-150">Una soluzione alternativa consiste nell'usare il tasto Invio</span><span class="sxs-lookup"><span data-stu-id="4821a-150">Workaround is to use the Enter key</span></span>
* <span data-ttu-id="4821a-151">Se si sceglie il certificato PIN/smart card non corretto, è necessario il riavvio per fare in modo che Storage Explorer dimentichi tale selezione</span><span class="sxs-lookup"><span data-stu-id="4821a-151">If you choose the wrong PIN/Smartcard certificate then you will need to restart in order to have Storage Explorer forget the decision</span></span>
* <span data-ttu-id="4821a-152">Il caricamento simultaneo di più di 3 gruppi di BLOB o di file può causare errori</span><span class="sxs-lookup"><span data-stu-id="4821a-152">Having more than 3 groups of blobs or files uploading at the same time may cause errors</span></span>
* <span data-ttu-id="4821a-153">Il pannello delle impostazioni dell'account potrebbe indicare che è necessario immettere nuovamente le credenziali per filtrare le sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="4821a-153">The account settings panel may show that you need to reenter credentials in order to filter subscriptions</span></span>
* <span data-ttu-id="4821a-154">La ridenominazione di BLOB singoli o all'interno di un contenitore BLOB rinominato non mantiene gli snapshot.</span><span class="sxs-lookup"><span data-stu-id="4821a-154">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="4821a-155">Tutte le altre proprietà e i metadati di BLOB, file ed entità vengono conservati durante un'operazione di ridenominazione.</span><span class="sxs-lookup"><span data-stu-id="4821a-155">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="4821a-156">Sebbene Azure Stack attualmente non supporta le condivisioni file, viene comunque visualizzato un nodo delle condivisioni di file in un account di archiviazione di Azure Stack associato.</span><span class="sxs-lookup"><span data-stu-id="4821a-156">Although Azure Stack doesn't currently support File Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="4821a-157">Ubuntu 14.04 richiede l'aggiornamento della versione gcc. La procedura per effettuare l'aggiornamento è riportata qui sotto:</span><span class="sxs-lookup"><span data-stu-id="4821a-157">Ubuntu 14.04 install needs gcc version updated or upgraded – steps to upgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a><span data-ttu-id="4821a-158">Versioni precedenti</span><span class="sxs-lookup"><span data-stu-id="4821a-158">Previous releases</span></span>

* [<span data-ttu-id="4821a-159">Versione 0.8.13</span><span class="sxs-lookup"><span data-stu-id="4821a-159">Version 0.8.13</span></span>](#version-0813)
* [<span data-ttu-id="4821a-160">Versione 0.8.12/0.8.11/0.8.10</span><span class="sxs-lookup"><span data-stu-id="4821a-160">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>](#version-0812--0811--0810)
* [<span data-ttu-id="4821a-161">Versione 0.8.9/0.8.8</span><span class="sxs-lookup"><span data-stu-id="4821a-161">Version 0.8.9 / 0.8.8</span></span>](#version-089--088)
* [<span data-ttu-id="4821a-162">Versione 0.8.7</span><span class="sxs-lookup"><span data-stu-id="4821a-162">Version 0.8.7</span></span>](#version-087)
* [<span data-ttu-id="4821a-163">Versione 0.8.6</span><span class="sxs-lookup"><span data-stu-id="4821a-163">Version 0.8.6</span></span>](#version-086)
* [<span data-ttu-id="4821a-164">Versione 0.8.5</span><span class="sxs-lookup"><span data-stu-id="4821a-164">Version 0.8.5</span></span>](#version-085)
* [<span data-ttu-id="4821a-165">Versione 0.8.4</span><span class="sxs-lookup"><span data-stu-id="4821a-165">Version 0.8.4</span></span>](#version-084)
* [<span data-ttu-id="4821a-166">Versione 0.8.3</span><span class="sxs-lookup"><span data-stu-id="4821a-166">Version 0.8.3</span></span>](#version-083)
* [<span data-ttu-id="4821a-167">Versione 0.8.2</span><span class="sxs-lookup"><span data-stu-id="4821a-167">Version 0.8.2</span></span>](#version-082)
* [<span data-ttu-id="4821a-168">Versione 0.8.0</span><span class="sxs-lookup"><span data-stu-id="4821a-168">Version 0.8.0</span></span>](#version-080)
* [<span data-ttu-id="4821a-169">Versione 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="4821a-169">Version 0.7.20160509.0</span></span>](#version-07201605090)
* [<span data-ttu-id="4821a-170">Versione 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="4821a-170">Version 0.7.20160325.0</span></span>](#version-07201603250)
* [<span data-ttu-id="4821a-171">Versione 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="4821a-171">Version 0.7.20160129.1</span></span>](#version-07201601291)
* [<span data-ttu-id="4821a-172">Versione 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="4821a-172">Version 0.7.20160105.0</span></span>](#version-07201601050)
* [<span data-ttu-id="4821a-173">Versione 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="4821a-173">Version 0.7.20151116.0</span></span>](#version-07201511160)


### <a name="version-0813"></a><span data-ttu-id="4821a-174">Versione 0.8.13</span><span class="sxs-lookup"><span data-stu-id="4821a-174">Version 0.8.13</span></span>
<span data-ttu-id="4821a-175">12/05/2017</span><span class="sxs-lookup"><span data-stu-id="4821a-175">05/12/2017</span></span>

#### <a name="new"></a><span data-ttu-id="4821a-176">Nuovo</span><span class="sxs-lookup"><span data-stu-id="4821a-176">New</span></span>

* <span data-ttu-id="4821a-177">[Guida][2]alla risoluzione dei problemi di Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="4821a-177">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="4821a-178">[Istruzioni][3]per stabilire la connessione a una sottoscrizione di Azure Stack</span><span class="sxs-lookup"><span data-stu-id="4821a-178">[Instructions][3] on connecting to an Azure Stack subscription</span></span>

#### <a name="fixes"></a><span data-ttu-id="4821a-179">Correzioni</span><span class="sxs-lookup"><span data-stu-id="4821a-179">Fixes</span></span>

* <span data-ttu-id="4821a-180">Corretto: il caricamento del file aveva una probabilità elevata di causare un errore di memoria insufficiente</span><span class="sxs-lookup"><span data-stu-id="4821a-180">Fixed: File upload had a high chance of causing an out of memory error</span></span>
* <span data-ttu-id="4821a-181">Corretto: è ora possibile accedere con PIN/smart card</span><span class="sxs-lookup"><span data-stu-id="4821a-181">Fixed: You can now sign in with PIN/Smartcard</span></span>
* <span data-ttu-id="4821a-182">Corretto: l'azione Apri nel portale ora funziona con Azure China, Azure Germany, Azure US Government e Azure Stack</span><span class="sxs-lookup"><span data-stu-id="4821a-182">Fixed: Open in Portal now works with Azure China, Azure Germany, Azure US Government, and Azure Stack</span></span>
* <span data-ttu-id="4821a-183">Corretto: durante il caricamento di una cartella in un contenitore BLOB, talvolta si verificava un errore "Operazione non valida"</span><span class="sxs-lookup"><span data-stu-id="4821a-183">Fixed: While uploading a folder to a blob container, an "Illegal operation" error would sometimes occur</span></span>
* <span data-ttu-id="4821a-184">Corretto: selezionare tutto ciò che è stato disabilitato durante la gestione di snapshot</span><span class="sxs-lookup"><span data-stu-id="4821a-184">Fixed: Select all was disabled while managing snapshots</span></span>
* <span data-ttu-id="4821a-185">Corretto: i metadati del BLOB di base avrebbero potuto venire sovrascritti dopo aver visualizzato le proprietà dei relativi snapshot</span><span class="sxs-lookup"><span data-stu-id="4821a-185">Fixed: The metadata of the base blob might get overwritten after viewing the properties of its snapshots</span></span>

#### <a name="known-issues"></a><span data-ttu-id="4821a-186">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="4821a-186">Known Issues</span></span>

* <span data-ttu-id="4821a-187">Se si sceglie il certificato PIN/smart card non corretto, è necessario il riavvio per fare in modo che Storage Explorer dimentichi tale selezione</span><span class="sxs-lookup"><span data-stu-id="4821a-187">If you choose the wrong PIN/Smartcard certificate then you will need to restart in order to have Storage Explorer forget the decision</span></span>
* <span data-ttu-id="4821a-188">Mentre viene eseguito lo zoom avanti o indietro, il livello di zoom può momentaneamente ripristinare il livello predefinito</span><span class="sxs-lookup"><span data-stu-id="4821a-188">While zoomed in or out, the zoom level may momentarily reset to the default level</span></span>
* <span data-ttu-id="4821a-189">Il caricamento simultaneo di più di 3 gruppi di BLOB o di file può causare errori</span><span class="sxs-lookup"><span data-stu-id="4821a-189">Having more than 3 groups of blobs or files uploading at the same time may cause errors</span></span>
* <span data-ttu-id="4821a-190">Il pannello delle impostazioni dell'account potrebbe indicare che è necessario immettere nuovamente le credenziali per filtrare le sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="4821a-190">The account settings panel may show that you need to reenter credentials in order to filter subscriptions</span></span>
* <span data-ttu-id="4821a-191">La ridenominazione di BLOB singoli o all'interno di un contenitore BLOB rinominato non mantiene gli snapshot.</span><span class="sxs-lookup"><span data-stu-id="4821a-191">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="4821a-192">Tutte le altre proprietà e i metadati di BLOB, file ed entità vengono conservati durante un'operazione di ridenominazione.</span><span class="sxs-lookup"><span data-stu-id="4821a-192">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="4821a-193">Sebbene Azure Stack attualmente non supporta le condivisioni file, viene comunque visualizzato un nodo delle condivisioni di file in un account di archiviazione di Azure Stack associato.</span><span class="sxs-lookup"><span data-stu-id="4821a-193">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="4821a-194">Ubuntu 14.04 richiede l'aggiornamento della versione gcc. La procedura per effettuare l'aggiornamento è riportata qui sotto:</span><span class="sxs-lookup"><span data-stu-id="4821a-194">Ubuntu 14.04 install needs gcc version updated or upgraded – steps to upgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a><span data-ttu-id="4821a-195">Versione 0.8.12/0.8.11/0.8.10</span><span class="sxs-lookup"><span data-stu-id="4821a-195">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>
<span data-ttu-id="4821a-196">07/04/2017</span><span class="sxs-lookup"><span data-stu-id="4821a-196">04/07/2017</span></span>

#### <a name="new"></a><span data-ttu-id="4821a-197">Nuovo</span><span class="sxs-lookup"><span data-stu-id="4821a-197">New</span></span>

* <span data-ttu-id="4821a-198">Storage Explorer si chiude automaticamente quando si installa un aggiornamento dalla notifica di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="4821a-198">Storage Explorer will now automatically close when you install an update from the update notification</span></span>
* <span data-ttu-id="4821a-199">L'accesso rapido sul posto fornisce un'esperienza ottimizzata per l'uso con le risorse a cui si accede di frequente</span><span class="sxs-lookup"><span data-stu-id="4821a-199">In-place quick access provides an enhanced experience for working with your frequently accessed resources</span></span>
* <span data-ttu-id="4821a-200">Nell'editor del contenitore BLOB, è ora possibile visualizzare a quale macchina virtuale appartiene un BLOB dedicato</span><span class="sxs-lookup"><span data-stu-id="4821a-200">In the Blob Container editor, you can now see which virtual machine a leased blob belongs to</span></span>
* <span data-ttu-id="4821a-201">È ora possibile comprimere il pannello di sinistra</span><span class="sxs-lookup"><span data-stu-id="4821a-201">You can now collapse the left side panel</span></span>
* <span data-ttu-id="4821a-202">L'azione Individuazione ora viene eseguito contemporaneamente al download</span><span class="sxs-lookup"><span data-stu-id="4821a-202">Discovery now runs at the same time as download</span></span>
* <span data-ttu-id="4821a-203">Usare Statistiche negli editor Contenitore BLOB, Condivisione File e Tabelle per visualizzare le dimensioni della risorsa o selezione</span><span class="sxs-lookup"><span data-stu-id="4821a-203">Use Statistics in the Blob Container, File Share, and Table editors to see the size of your resource or selection</span></span>
* <span data-ttu-id="4821a-204">È ora possibile accedere agli account di Azure Stack basati su Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="4821a-204">You can now sign-in to Azure Active Directory (AAD) based Azure Stack accounts.</span></span> 
* <span data-ttu-id="4821a-205">È ora possibile caricare file di archivio superiori ai 32 MB per gli account di archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="4821a-205">You can now upload archive files over 32MB to Premium storage accounts</span></span>
* <span data-ttu-id="4821a-206">Supporto di accessibilità migliorato</span><span class="sxs-lookup"><span data-stu-id="4821a-206">Improved accessibility support</span></span>
* <span data-ttu-id="4821a-207">È ora possibile aggiungere certificati SSL attendibili X.509 codificati Base-64 andando su Modifica -&gt; Certificati SSL -&gt; Importa certificati</span><span class="sxs-lookup"><span data-stu-id="4821a-207">You can now add trusted Base-64 encoded X.509 SSL certificates by going to Edit -&gt; SSL Certificates -&gt; Import Certificates</span></span>

#### <a name="fixes"></a><span data-ttu-id="4821a-208">Correzioni</span><span class="sxs-lookup"><span data-stu-id="4821a-208">Fixes</span></span>

* <span data-ttu-id="4821a-209">Corretto: dopo l'aggiornamento delle credenziali dell'account, la visualizzazione albero talvolta non veniva aggiornata automaticamente</span><span class="sxs-lookup"><span data-stu-id="4821a-209">Fixed: after refreshing an account's credentials, the tree view would sometimes not automatically refresh</span></span>
* <span data-ttu-id="4821a-210">Corretto: la generazione di una firma di accesso condiviso per le code e le tabelle dell'emulatore dà origine a un URL non valido</span><span class="sxs-lookup"><span data-stu-id="4821a-210">Fixed: generating a SAS for emulator queues and tables would result in an invalid URL</span></span>
* <span data-ttu-id="4821a-211">Corretto: gli account di archiviazione premium possono ora essere espansi mentre è abilitato un proxy</span><span class="sxs-lookup"><span data-stu-id="4821a-211">Fixed: premium storage accounts can now be expanded while a proxy is enabled</span></span>
* <span data-ttu-id="4821a-212">Corretto: il pulsante Applica nella pagina di gestione degli account non funziona se si aveva selezionato 1 o 0 account</span><span class="sxs-lookup"><span data-stu-id="4821a-212">Fixed: the apply button on the accounts management page would not work if you had 1 or 0 accounts selected</span></span>
* <span data-ttu-id="4821a-213">Corretto: il caricamento di BLOB che richiedono le risoluzioni di conflitti potrebbe non andare a buon termine - corretto in 0.8.11</span><span class="sxs-lookup"><span data-stu-id="4821a-213">Fixed: uploading blobs that require conflict resolutions may fail - fixed in 0.8.11</span></span> 
* <span data-ttu-id="4821a-214">Corretto: l'invio di commenti e suggerimenti veniva interrotto nella versione 0.8.11 - corretto in 0.8.12</span><span class="sxs-lookup"><span data-stu-id="4821a-214">Fixed: sending feedback was broken in 0.8.11 - fixed in 0.8.12</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="4821a-215">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="4821a-215">Known Issues</span></span>

* <span data-ttu-id="4821a-216">Dopo l'aggiornamento a 0.8.10, è necessario aggiornare tutte le credenziali.</span><span class="sxs-lookup"><span data-stu-id="4821a-216">After upgrading to 0.8.10, you will need to refresh all of your credentials.</span></span>
* <span data-ttu-id="4821a-217">Mentre viene eseguito lo zoom avanti o indietro, il livello di zoom può momentaneamente ripristinare il livello predefinito.</span><span class="sxs-lookup"><span data-stu-id="4821a-217">While zoomed in or out, the zoom level may momentarily reset to the default level.</span></span>
* <span data-ttu-id="4821a-218">Il caricamento simultaneo di più di 3 gruppi di BLOB o di file può causare errori.</span><span class="sxs-lookup"><span data-stu-id="4821a-218">Having more than 3 groups of blobs or files uploading at the same time may cause errors.</span></span>
* <span data-ttu-id="4821a-219">Il pannello delle impostazioni dell'account potrebbe indicare che è necessario immettere nuovamente le credenziali per filtrare le sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="4821a-219">The account settings panel may show that you need to reenter credentials in order to filter subscriptions.</span></span>
* <span data-ttu-id="4821a-220">La ridenominazione di BLOB singoli o all'interno di un contenitore BLOB rinominato non mantiene gli snapshot.</span><span class="sxs-lookup"><span data-stu-id="4821a-220">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="4821a-221">Tutte le altre proprietà e i metadati di BLOB, file ed entità vengono conservati durante un'operazione di ridenominazione.</span><span class="sxs-lookup"><span data-stu-id="4821a-221">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="4821a-222">Sebbene Azure Stack attualmente non supporta le condivisioni file, viene comunque visualizzato un nodo delle condivisioni di file in un account di archiviazione di Azure Stack associato.</span><span class="sxs-lookup"><span data-stu-id="4821a-222">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="4821a-223">Ubuntu 14.04 richiede l'aggiornamento della versione gcc. La procedura per effettuare l'aggiornamento è riportata qui sotto:</span><span class="sxs-lookup"><span data-stu-id="4821a-223">Ubuntu 14.04 install needs gcc version updated or upgraded – steps to upgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a><span data-ttu-id="4821a-224">Versione 0.8.9/0.8.8</span><span class="sxs-lookup"><span data-stu-id="4821a-224">Version 0.8.9 / 0.8.8</span></span>
<span data-ttu-id="4821a-225">23/02/2017</span><span class="sxs-lookup"><span data-stu-id="4821a-225">02/23/2017</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="4821a-226">Nuovo</span><span class="sxs-lookup"><span data-stu-id="4821a-226">New</span></span>

* <span data-ttu-id="4821a-227">Storage Explorer 0.8.9 scaricherà automaticamente la versione più recente degli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="4821a-227">Storage Explorer 0.8.9 will automatically download the latest version for updates.</span></span>
* <span data-ttu-id="4821a-228">Hotfix: l'uso di un URI di firma di accesso condiviso generato da portale per collegare un account di archiviazione comporta un errore.</span><span class="sxs-lookup"><span data-stu-id="4821a-228">Hotfix: using a portal generated SAS URI to attach a storage account would result in an error.</span></span>
* <span data-ttu-id="4821a-229">È ora possibile creare, gestire e alzare di livello degli snapshot di BLOB.</span><span class="sxs-lookup"><span data-stu-id="4821a-229">You can now create, manage, and promote blob snapshots.</span></span>
* <span data-ttu-id="4821a-230">È ora possibile accedere agli account di Azure China, Azure Germany e Azure US Government.</span><span class="sxs-lookup"><span data-stu-id="4821a-230">You can now sign in to Azure China, Azure Germany, and Azure US Government accounts.</span></span>
* <span data-ttu-id="4821a-231">È ora possibile modificare il livello di zoom.</span><span class="sxs-lookup"><span data-stu-id="4821a-231">You can now change the zoom level.</span></span> <span data-ttu-id="4821a-232">Usare le opzioni nel menu Visualizza per Zoom avanti, Zoom indietro e Reimposta zoom.</span><span class="sxs-lookup"><span data-stu-id="4821a-232">Use the options in the View menu to Zoom In, Zoom Out, and Reset Zoom.</span></span>
* <span data-ttu-id="4821a-233">I caratteri Unicode sono ora supportati nei metadati dell'utente per file e BLOB.</span><span class="sxs-lookup"><span data-stu-id="4821a-233">Unicode characters are now supported in user metadata for blobs and files.</span></span>
* <span data-ttu-id="4821a-234">Miglioramenti all'accessibilità.</span><span class="sxs-lookup"><span data-stu-id="4821a-234">Accessibility improvements.</span></span>
* <span data-ttu-id="4821a-235">Le note sulla versione successiva possono essere visualizzate dalla notifica di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="4821a-235">The next version's release notes can be viewed from the update notification.</span></span> <span data-ttu-id="4821a-236">È inoltre possibile visualizzare le note sulla versione attuale dal menu Guida.</span><span class="sxs-lookup"><span data-stu-id="4821a-236">You can also view the current release notes from the Help menu.</span></span>

#### <a name="fixes"></a><span data-ttu-id="4821a-237">Correzioni</span><span class="sxs-lookup"><span data-stu-id="4821a-237">Fixes</span></span>

* <span data-ttu-id="4821a-238">Corretto: il numero di versione viene ora visualizzato correttamente nel Pannello di controllo in Windows</span><span class="sxs-lookup"><span data-stu-id="4821a-238">Fixed: the version number is now correctly displayed in Control Panel on Windows</span></span>
* <span data-ttu-id="4821a-239">Corretto: la ricerca non è più limitata a 50.000 nodi</span><span class="sxs-lookup"><span data-stu-id="4821a-239">Fixed: search is no longer limited to 50,000 nodes</span></span>
* <span data-ttu-id="4821a-240">Corretto: caricamento predefinito in una condivisione di file se non esiste già una directory di destinazione</span><span class="sxs-lookup"><span data-stu-id="4821a-240">Fixed: upload to a file share spun forever if the destination directory did not already exist</span></span>
* <span data-ttu-id="4821a-241">Corretto: maggiore stabilità per processi di caricamento e download prolungati</span><span class="sxs-lookup"><span data-stu-id="4821a-241">Fixed: improved stability for long uploads and downloads</span></span>

#### <a name="known-issues"></a><span data-ttu-id="4821a-242">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="4821a-242">Known Issues</span></span>

* <span data-ttu-id="4821a-243">Mentre viene eseguito lo zoom avanti o indietro, il livello di zoom può momentaneamente ripristinare il livello predefinito.</span><span class="sxs-lookup"><span data-stu-id="4821a-243">While zoomed in or out, the zoom level may momentarily reset to the default level.</span></span>
* <span data-ttu-id="4821a-244">Accesso rapido funziona solo con gli elementi basati su sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="4821a-244">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="4821a-245">Questa versione non supporta le risorse locali e le risorse collegate tramite chiave o token di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="4821a-245">Local resources or resources attached via key or SAS token are not supported in this release.</span></span>
* <span data-ttu-id="4821a-246">Accesso rapido può impiegare alcuni secondi per passare alla risorsa di destinazione, a seconda del numero di risorse presenti.</span><span class="sxs-lookup"><span data-stu-id="4821a-246">It may take Quick Access a few seconds to navigate to the target resource, depending on how many resources you have.</span></span>
* <span data-ttu-id="4821a-247">Il caricamento simultaneo di più di 3 gruppi di BLOB o di file può causare errori.</span><span class="sxs-lookup"><span data-stu-id="4821a-247">Having more than 3 groups of blobs or files uploading at the same time may cause errors.</span></span>

<span data-ttu-id="4821a-248">16/12/2016</span><span class="sxs-lookup"><span data-stu-id="4821a-248">12/16/2016</span></span>
### <a name="version-087"></a><span data-ttu-id="4821a-249">Versione 0.8.7</span><span class="sxs-lookup"><span data-stu-id="4821a-249">Version 0.8.7</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="4821a-250">Nuovo</span><span class="sxs-lookup"><span data-stu-id="4821a-250">New</span></span>

* <span data-ttu-id="4821a-251">È possibile scegliere come risolvere i conflitti all'inizio di una sessione di aggiornamento, download o copia nella finestra Attività</span><span class="sxs-lookup"><span data-stu-id="4821a-251">You can choose how to resolve conflicts at the beginning of an update, download or copy session in the Activities window</span></span>
* <span data-ttu-id="4821a-252">È possibile passare il mouse su una scheda per visualizzare il percorso completo della risorsa di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4821a-252">Hover over a tab to see the full path of the storage resource</span></span>
* <span data-ttu-id="4821a-253">Quando si fa clic su una scheda, si sincronizza con il relativo percorso nel riquadro di spostamento a sinistra</span><span class="sxs-lookup"><span data-stu-id="4821a-253">When you click on a tab, it synchronizes with its location in the left side navigation pane</span></span>

#### <a name="fixes"></a><span data-ttu-id="4821a-254">Correzioni</span><span class="sxs-lookup"><span data-stu-id="4821a-254">Fixes</span></span>

* <span data-ttu-id="4821a-255">Corretto: Storage Explorer è ora un'app attendibile su Mac</span><span class="sxs-lookup"><span data-stu-id="4821a-255">Fixed: Storage Explorer is now a trusted app on Mac</span></span>
* <span data-ttu-id="4821a-256">Corretto: Ubuntu 14.04 è supportato nuovamente</span><span class="sxs-lookup"><span data-stu-id="4821a-256">Fixed: Ubuntu 14.04 is again supported</span></span>
* <span data-ttu-id="4821a-257">Corretto: a volte l'interfaccia utente Aggiungi account lampeggiava durante il caricamento delle sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="4821a-257">Fixed: Sometimes the add account UI flashes when loading subscriptions</span></span>
* <span data-ttu-id="4821a-258">Corretto: a volte non tutte le risorse di archiviazione venivano elencate nel riquadro di spostamento a sinistra</span><span class="sxs-lookup"><span data-stu-id="4821a-258">Fixed: Sometimes not all storage resources were listed in the left side navigation pane</span></span>
* <span data-ttu-id="4821a-259">Corretto: a volte il riquadro azioni visualizzava azioni vuote</span><span class="sxs-lookup"><span data-stu-id="4821a-259">Fixed: The action pane sometimes displayed empty actions</span></span>
* <span data-ttu-id="4821a-260">Corretto: le dimensioni della finestra dell'ultima sessione chiusa vengono ora mantenute</span><span class="sxs-lookup"><span data-stu-id="4821a-260">Fixed: The window size from the last closed session is now retained</span></span>
* <span data-ttu-id="4821a-261">Corretto: è possibile aprire più schede per la stessa risorsa usando il menu di scelta rapida</span><span class="sxs-lookup"><span data-stu-id="4821a-261">Fixed: You can open multiple tabs for the same resource using the context menu</span></span>

#### <a name="known-issues"></a><span data-ttu-id="4821a-262">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="4821a-262">Known Issues</span></span>

* <span data-ttu-id="4821a-263">Accesso rapido funziona solo con gli elementi basati su sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="4821a-263">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="4821a-264">Questa versione non supporta le risorse locali e le risorse collegate tramite chiave o token di firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="4821a-264">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="4821a-265">Accesso rapido può impiegare alcuni secondi per passare alla risorsa di destinazione, a seconda del numero di risorse presenti</span><span class="sxs-lookup"><span data-stu-id="4821a-265">It may take Quick Access a few seconds to navigate to the target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="4821a-266">Il caricamento simultaneo di più di 3 gruppi di BLOB o di file può causare errori</span><span class="sxs-lookup"><span data-stu-id="4821a-266">Having more than 3 groups of blobs or files uploading at the same time may cause errors</span></span>
* <span data-ttu-id="4821a-267">È possibile eseguire la ricerca in un massimo di 50.000 nodi circa. Se si supera tale limite, le prestazioni potrebbero risultare peggiorate o potrebbero essere generate eccezioni non gestite</span><span class="sxs-lookup"><span data-stu-id="4821a-267">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>
* <span data-ttu-id="4821a-268">La prima volta che si usa Storage Explorer in macOS potrebbero essere visualizzate diverse richieste di autorizzazione dell'utente per l'accesso a Keychain.</span><span class="sxs-lookup"><span data-stu-id="4821a-268">For the first time using the Storage Explorer on macOS, you might see multiple prompts asking for user's permission to access keychain.</span></span> <span data-ttu-id="4821a-269">È consigliabile selezionare Consenti sempre per non visualizzare più la richiesta di conferma</span><span class="sxs-lookup"><span data-stu-id="4821a-269">We suggest you select Always Allow so the prompt won't show up again</span></span>

<span data-ttu-id="4821a-270">18/11/2016</span><span class="sxs-lookup"><span data-stu-id="4821a-270">11/18/2016</span></span>
### <a name="version-086"></a><span data-ttu-id="4821a-271">Versione 0.8.6</span><span class="sxs-lookup"><span data-stu-id="4821a-271">Version 0.8.6</span></span>

#### <a name="new"></a><span data-ttu-id="4821a-272">Nuovo</span><span class="sxs-lookup"><span data-stu-id="4821a-272">New</span></span>

* <span data-ttu-id="4821a-273">Possibilità di aggiungere ad Accesso rapido i servizi usati più di frequente per semplificare la navigazione</span><span class="sxs-lookup"><span data-stu-id="4821a-273">You can now pin most frequently used services to the Quick Access for easy navigation</span></span>
* <span data-ttu-id="4821a-274">Possibilità di aprire più editor in schede diverse.</span><span class="sxs-lookup"><span data-stu-id="4821a-274">You can now open multiple editors in different tabs.</span></span> <span data-ttu-id="4821a-275">Clic singolo per aprire una scheda temporanea. Doppio clic per aprire una scheda permanente. È anche possibile fare clic sulla scheda temporanea per renderla permanente</span><span class="sxs-lookup"><span data-stu-id="4821a-275">Single click to open a temporary tab; double click to open a permanent tab. You can also click on the temporary tab to make it a permanent tab</span></span>
* <span data-ttu-id="4821a-276">Sono stati apportati miglioramenti evidenti a prestazioni e stabilità per operazioni di caricamento e download, soprattutto per file di grandi dimensioni in computer veloci</span><span class="sxs-lookup"><span data-stu-id="4821a-276">We have made noticeable performance and stability improvements for uploads and downloads, especially for large files on fast machines</span></span>
* <span data-ttu-id="4821a-277">Possibilità di creare cartelle vuote "virtuali" in contenitori BLOB</span><span class="sxs-lookup"><span data-stu-id="4821a-277">Empty "virtual" folders can now be created in blob containers</span></span>
* <span data-ttu-id="4821a-278">È stato reintrodotto l'ambito di ricerca con la nuova ricerca avanzata con sottostringa, pertanto ora vi sono due opzioni di ricerca:</span><span class="sxs-lookup"><span data-stu-id="4821a-278">We have re-introduced scoped search with our new enhanced substring search, so you now have two options for searching:</span></span> 
    * <span data-ttu-id="4821a-279">Ricerca globale: è sufficiente immettere solo un termine di ricerca nella casella di testo di ricerca</span><span class="sxs-lookup"><span data-stu-id="4821a-279">Global search - just enter a search term into the search textbox</span></span>
    * <span data-ttu-id="4821a-280">Ricerca con ambito: fare clic sull'icona della lente di ingrandimento accanto a un nodo, quindi aggiungere un termine di ricerca alla fine del percorso o fare clic con il pulsante destro del mouse e selezionare "Cerca da qui"</span><span class="sxs-lookup"><span data-stu-id="4821a-280">Scoped search - click the magnifying glass icon next to a node, then add a search term to the end of the path, or right-click and select "Search from Here"</span></span>
* <span data-ttu-id="4821a-281">Sono stati aggiunti vari temi: Chiaro (impostazione predefinita), Scuro, Nero a contrasto elevato e Bianco a contrasto elevato.</span><span class="sxs-lookup"><span data-stu-id="4821a-281">We have added various themes: Light (default), Dark, High Contrast Black, and High Contrast White.</span></span> <span data-ttu-id="4821a-282">Scegliere Modifica -&gt; Temi per modificare le preferenze dei temi</span><span class="sxs-lookup"><span data-stu-id="4821a-282">Go to Edit -&gt; Themes to change your theming preference</span></span>
* <span data-ttu-id="4821a-283">È possibile modificare le proprietà di BLOB e file</span><span class="sxs-lookup"><span data-stu-id="4821a-283">You can modify Blob and file properties</span></span>
* <span data-ttu-id="4821a-284">Sono ora supportati i messaggi in coda codificati (base64) e non codificati</span><span class="sxs-lookup"><span data-stu-id="4821a-284">We now support encoded (base64) and unencoded queue messages</span></span>
* <span data-ttu-id="4821a-285">In Linux è ora necessario un sistema operativo a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="4821a-285">On Linux, a 64-bit OS is now required.</span></span> <span data-ttu-id="4821a-286">Per questa versione è supportato solo Ubuntu 16.04.1 LTS a 64 bit</span><span class="sxs-lookup"><span data-stu-id="4821a-286">For this release we only support 64-bit Ubuntu 16.04.1 LTS</span></span>
* <span data-ttu-id="4821a-287">È stato aggiornato il logo</span><span class="sxs-lookup"><span data-stu-id="4821a-287">We have updated our logo!</span></span>

#### <a name="fixes"></a><span data-ttu-id="4821a-288">Correzioni</span><span class="sxs-lookup"><span data-stu-id="4821a-288">Fixes</span></span>

* <span data-ttu-id="4821a-289">Corretto: problemi di blocco della schermata</span><span class="sxs-lookup"><span data-stu-id="4821a-289">Fixed: Screen freezing problems</span></span>
* <span data-ttu-id="4821a-290">Corretto: sicurezza avanzata</span><span class="sxs-lookup"><span data-stu-id="4821a-290">Fixed: Enhanced security</span></span>
* <span data-ttu-id="4821a-291">Corretto: a volte venivano visualizzati account collegati doppi</span><span class="sxs-lookup"><span data-stu-id="4821a-291">Fixed: Sometimes duplicate attached accounts could appear</span></span>
* <span data-ttu-id="4821a-292">Corretto: un blob con un tipo di contenuto non definito poteva generare un'eccezione</span><span class="sxs-lookup"><span data-stu-id="4821a-292">Fixed: A blob with an undefined content type could generate an exception</span></span>
* <span data-ttu-id="4821a-293">Corretto: non era possibile aprire il pannello Query in una tabella vuota</span><span class="sxs-lookup"><span data-stu-id="4821a-293">Fixed: Opening the Query Panel on an empty table was not possible</span></span>
* <span data-ttu-id="4821a-294">Corretto: bug delle variabili in Cerca</span><span class="sxs-lookup"><span data-stu-id="4821a-294">Fixed: Varies bugs in Search</span></span>
* <span data-ttu-id="4821a-295">Corretto: il numero delle risorse che è possibile caricare tramite "Carica altro" è stato aumentato da 50 a 100</span><span class="sxs-lookup"><span data-stu-id="4821a-295">Fixed: Increased the number of resources loaded from 50 to 100 when clicking "Load More"</span></span>
* <span data-ttu-id="4821a-296">Corretto: alla prima esecuzione, se si è effettuato l'accesso a un account, vengono ora selezionate tutte le sottoscrizioni per tale account per impostazione predefinita</span><span class="sxs-lookup"><span data-stu-id="4821a-296">Fixed: On first run, if an account is signed into, we now select all subscriptions for that account by default</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="4821a-297">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="4821a-297">Known Issues</span></span>

* <span data-ttu-id="4821a-298">Questa versione di Storage Explorer non può essere eseguita in Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="4821a-298">This release of the Storage Explorer does not run on Ubuntu 14.04</span></span>
* <span data-ttu-id="4821a-299">Per aprire più schede per la stessa risorsa, non fare clic in modo continuo sulla stessa risorsa.</span><span class="sxs-lookup"><span data-stu-id="4821a-299">To open multiple tabs for the same resource, do not continuously click on the same resource.</span></span> <span data-ttu-id="4821a-300">Fare clic su un'altra risorsa, tornare indietro e quindi fare clic sulla risorsa originale per aprirla nuovamente in un'altra scheda</span><span class="sxs-lookup"><span data-stu-id="4821a-300">Click on another resource and then go back and then click on the original resource to open it again in another tab</span></span> 
* <span data-ttu-id="4821a-301">Accesso rapido funziona solo con gli elementi basati su sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="4821a-301">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="4821a-302">Questa versione non supporta le risorse locali e le risorse collegate tramite chiave o token di firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="4821a-302">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="4821a-303">Accesso rapido può impiegare alcuni secondi per passare alla risorsa di destinazione, a seconda del numero di risorse presenti</span><span class="sxs-lookup"><span data-stu-id="4821a-303">It may take Quick Access a few seconds to navigate to the target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="4821a-304">Il caricamento simultaneo di più di 3 gruppi di BLOB o di file può causare errori</span><span class="sxs-lookup"><span data-stu-id="4821a-304">Having more than 3 groups of blobs or files uploading at the same time may cause errors</span></span>
* <span data-ttu-id="4821a-305">È possibile eseguire la ricerca in un massimo di 50.000 nodi circa. Se si supera tale limite, le prestazioni potrebbero risultare peggiorate o potrebbero essere generate eccezioni non gestite</span><span class="sxs-lookup"><span data-stu-id="4821a-305">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>

<span data-ttu-id="4821a-306">03/10/2016</span><span class="sxs-lookup"><span data-stu-id="4821a-306">10/03/2016</span></span>
### <a name="version-085"></a><span data-ttu-id="4821a-307">Versione 0.8.5</span><span class="sxs-lookup"><span data-stu-id="4821a-307">Version 0.8.5</span></span>

#### <a name="new"></a><span data-ttu-id="4821a-308">Nuovo</span><span class="sxs-lookup"><span data-stu-id="4821a-308">New</span></span>

* <span data-ttu-id="4821a-309">È ora possibile usare le chiavi di firma di accesso condiviso generate dal portale per collegarsi all'account di archiviazione e alle risorse</span><span class="sxs-lookup"><span data-stu-id="4821a-309">Can now use Portal-generated SAS keys to attach to Storage Accounts and resources</span></span>

#### <a name="fixes"></a><span data-ttu-id="4821a-310">Correzioni</span><span class="sxs-lookup"><span data-stu-id="4821a-310">Fixes</span></span>

* <span data-ttu-id="4821a-311">Corretto: a volte la race condition durante la ricerca faceva sì che i nodi diventassero non espandibili</span><span class="sxs-lookup"><span data-stu-id="4821a-311">Fixed: race condition during search sometimes caused nodes to become non-expandable</span></span>
* <span data-ttu-id="4821a-312">Corretto: "Usa HTTP" non funziona quando ci si connette agli account di archiviazione con il nome account e la chiave</span><span class="sxs-lookup"><span data-stu-id="4821a-312">Fixed: "Use HTTP" doesn't work when connecting to Storage Accounts with account name and key</span></span>
* <span data-ttu-id="4821a-313">Corretto: le chiavi di firma di accesso condiviso (specialmente quelle generati da portale) restituiscono un errore "barra finale"</span><span class="sxs-lookup"><span data-stu-id="4821a-313">Fixed: SAS keys (specially Portal-generated ones) return a "trailing slash" error</span></span>
* <span data-ttu-id="4821a-314">Corretto: problemi di importazione della tabella</span><span class="sxs-lookup"><span data-stu-id="4821a-314">Fixed: table import issues</span></span>
    * <span data-ttu-id="4821a-315">In alcuni casi la chiave di partizione e la chiave di riga venivano annullate</span><span class="sxs-lookup"><span data-stu-id="4821a-315">Sometimes partition key and row key were reversed</span></span>
    * <span data-ttu-id="4821a-316">Impossibile leggere le chiavi di partizione "null"</span><span class="sxs-lookup"><span data-stu-id="4821a-316">Unable to read "null" Partition Keys</span></span>

#### <a name="known-issues"></a><span data-ttu-id="4821a-317">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="4821a-317">Known Issues</span></span>

* <span data-ttu-id="4821a-318">È possibile eseguire la ricerca in un massimo di 50.000 nodi circa. Se si supera tale limite, le prestazioni potrebbero risultare peggiorate</span><span class="sxs-lookup"><span data-stu-id="4821a-318">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>
* <span data-ttu-id="4821a-319">Azure Stack attualmente non supporta i file, quindi il tentativo di espandere File genera un errore</span><span class="sxs-lookup"><span data-stu-id="4821a-319">Azure Stack doesn't currently support Files, so trying to expand Files will show an error</span></span>

<span data-ttu-id="4821a-320">12/09/2016</span><span class="sxs-lookup"><span data-stu-id="4821a-320">09/12/2016</span></span>
### <a name="version-084"></a><span data-ttu-id="4821a-321">Versione 0.8.4</span><span class="sxs-lookup"><span data-stu-id="4821a-321">Version 0.8.4</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="4821a-322">Nuovo</span><span class="sxs-lookup"><span data-stu-id="4821a-322">New</span></span>

* <span data-ttu-id="4821a-323">Generazione di collegamenti diretti ad account di archiviazione, contenitori, code, tabelle o condivisioni file per accedere facilmente alle risorse e condividerle - Supporto Windows e Mac OS</span><span class="sxs-lookup"><span data-stu-id="4821a-323">Generate direct links to storage accounts, containers, queues, tables, or file shares for sharing and easy access to your resources - Windows and Mac OS support</span></span>
* <span data-ttu-id="4821a-324">Ricerca di contenitori BLOB, tabelle, code, condivisioni file o account di archiviazione dalla casella di ricerca</span><span class="sxs-lookup"><span data-stu-id="4821a-324">Search for your blob containers, tables, queues, file shares, or storage accounts from the search box</span></span>
* <span data-ttu-id="4821a-325">È ora possibile raggruppare le clausole nel generatore di query della tabella</span><span class="sxs-lookup"><span data-stu-id="4821a-325">You can now group clauses in the table query builder</span></span>
* <span data-ttu-id="4821a-326">Rinominare e copiare/incollare contenitori BLOB, condivisioni file, tabelle, BLOB, cartelle di BLOB, file e directory all'interno di contenitori e account collegati alla firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="4821a-326">Rename and copy/paste blob containers, file shares, tables, blobs, blob folders, files and directories from within SAS-attached accounts and containers</span></span>
* <span data-ttu-id="4821a-327">Quando vengono ridenominati e copiati contenitori BLOB e condivisioni file, proprietà e metadati vengono mantenuti</span><span class="sxs-lookup"><span data-stu-id="4821a-327">Renaming and copying blob containers and file shares now preserve properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="4821a-328">Correzioni</span><span class="sxs-lookup"><span data-stu-id="4821a-328">Fixes</span></span>

* <span data-ttu-id="4821a-329">Corretto: impossibile modificare le voci della tabella se contengono le proprietà di tipo booleano o binario</span><span class="sxs-lookup"><span data-stu-id="4821a-329">Fixed: cannot edit table entities if they contain boolean or binary properties</span></span>

#### <a name="known-issues"></a><span data-ttu-id="4821a-330">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="4821a-330">Known Issues</span></span>

* <span data-ttu-id="4821a-331">È possibile eseguire la ricerca in un massimo di 50.000 nodi circa. Se si supera tale limite, le prestazioni potrebbero risultare peggiorate</span><span class="sxs-lookup"><span data-stu-id="4821a-331">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>

<span data-ttu-id="4821a-332">03/08/2016</span><span class="sxs-lookup"><span data-stu-id="4821a-332">08/03/2016</span></span>
### <a name="version-083"></a><span data-ttu-id="4821a-333">Versione 0.8.3</span><span class="sxs-lookup"><span data-stu-id="4821a-333">Version 0.8.3</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="4821a-334">Nuovo</span><span class="sxs-lookup"><span data-stu-id="4821a-334">New</span></span>

* <span data-ttu-id="4821a-335">Ridenominazione di contenitori, tabelle e condivisioni file</span><span class="sxs-lookup"><span data-stu-id="4821a-335">Rename containers, tables, file shares</span></span>
* <span data-ttu-id="4821a-336">Migliore esperienza con il Generatore di query</span><span class="sxs-lookup"><span data-stu-id="4821a-336">Improved Query builder experience</span></span>
* <span data-ttu-id="4821a-337">Possibilità di salvare e caricare le query</span><span class="sxs-lookup"><span data-stu-id="4821a-337">Ability to save and load queries</span></span>
* <span data-ttu-id="4821a-338">Collegamenti diretti ad account di archiviazione o contenitori, code, tabelle o condivisioni file per accedere facilmente alle risorse e condividerle (solo su Windows, supporto per macOS presto disponibile)</span><span class="sxs-lookup"><span data-stu-id="4821a-338">Direct links to storage accounts or containers, queues, tables, or file shares for sharing and easily accessing your resources (Windows-only - macOS support coming soon!)</span></span>
* <span data-ttu-id="4821a-339">Possibilità di gestire e configurare regole CORS</span><span class="sxs-lookup"><span data-stu-id="4821a-339">Ability to manage and configure CORS rules</span></span>

#### <a name="fixes"></a><span data-ttu-id="4821a-340">Correzioni</span><span class="sxs-lookup"><span data-stu-id="4821a-340">Fixes</span></span>

* <span data-ttu-id="4821a-341">Corretto: gli account di Microsoft richiedono la riautenticazione ogni 8-12 ore</span><span class="sxs-lookup"><span data-stu-id="4821a-341">Fixed: Microsoft Accounts require re-authentication every 8-12 hours</span></span>

#### <a name="known-issues"></a><span data-ttu-id="4821a-342">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="4821a-342">Known Issues</span></span>

* <span data-ttu-id="4821a-343">In alcuni casi l'interfaccia utente potrebbe sembrare bloccata. Per risolvere il problema, ingrandire la finestra</span><span class="sxs-lookup"><span data-stu-id="4821a-343">Sometimes the UI might appear frozen - maximizing the window helps resolve this issue</span></span>
* <span data-ttu-id="4821a-344">L'installazione di macOS potrebbe richiedere autorizzazioni elevate</span><span class="sxs-lookup"><span data-stu-id="4821a-344">macOS install may require elevated permissions</span></span>
* <span data-ttu-id="4821a-345">Il pannello delle impostazioni dell'account potrebbe indicare che è necessario immettere nuovamente le credenziali per filtrare le sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="4821a-345">Account settings panel may show that you need to reenter credentials in order to filter subscriptions</span></span>
* <span data-ttu-id="4821a-346">Quando si ridenominano condivisioni file, contenitori BLOB e tabelle non vengono conservati i metadati o altre proprietà nel contenitore, ad esempio la quota di condivisione file, il livello di accesso pubblico o i criteri di accesso</span><span class="sxs-lookup"><span data-stu-id="4821a-346">Renaming file shares, blob containers, and tables does not preserve metadata or other properties on the container, such as file share quota, public access level or access policies</span></span>
* <span data-ttu-id="4821a-347">La ridenominazione di BLOB singoli o all'interno di un contenitore BLOB rinominato non mantiene gli snapshot.</span><span class="sxs-lookup"><span data-stu-id="4821a-347">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="4821a-348">Tutte le altre proprietà e i metadati di BLOB, file ed entità vengono conservati durante un'operazione di ridenominazione</span><span class="sxs-lookup"><span data-stu-id="4821a-348">All other properties and metadata for blobs, files and entities are preserved during a rename</span></span>
* <span data-ttu-id="4821a-349">La copia o la ridenominazione delle risorse non funziona all'interno di account associati alla firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="4821a-349">Copying or renaming resources does not work within SAS-attached accounts</span></span>

<span data-ttu-id="4821a-350">07/07/2016</span><span class="sxs-lookup"><span data-stu-id="4821a-350">07/07/2016</span></span>
### <a name="version-082"></a><span data-ttu-id="4821a-351">Versione 0.8.2</span><span class="sxs-lookup"><span data-stu-id="4821a-351">Version 0.8.2</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="4821a-352">Nuovo</span><span class="sxs-lookup"><span data-stu-id="4821a-352">New</span></span>

* <span data-ttu-id="4821a-353">Gli account di archiviazione vengono raggruppati in sottoscrizioni. L'archiviazione e le risorse di sviluppo collegate tramite chiave o firma di accesso condiviso vengono visualizzate nel nodo (locale e collegato)</span><span class="sxs-lookup"><span data-stu-id="4821a-353">Storage Accounts are grouped by subscriptions; development storage and resources attached via key or SAS are shown under (Local and Attached) node</span></span>
* <span data-ttu-id="4821a-354">Disconnettersi dagli account nel pannello "Impostazioni account Azure"</span><span class="sxs-lookup"><span data-stu-id="4821a-354">Sign off from accounts in "Azure Account Settings" panel</span></span>
* <span data-ttu-id="4821a-355">Configurare le impostazioni proxy per abilitare e gestire l'accesso</span><span class="sxs-lookup"><span data-stu-id="4821a-355">Configure proxy settings to enable and manage sign-in</span></span>
* <span data-ttu-id="4821a-356">Creare e interrompere i lease di blob</span><span class="sxs-lookup"><span data-stu-id="4821a-356">Create and break blob leases</span></span>
* <span data-ttu-id="4821a-357">Aprire contenitori BLOB, code, tabelle e i file con un unico clic</span><span class="sxs-lookup"><span data-stu-id="4821a-357">Open blob containers, queues, tables, and files with single-click</span></span>

#### <a name="fixes"></a><span data-ttu-id="4821a-358">Correzioni</span><span class="sxs-lookup"><span data-stu-id="4821a-358">Fixes</span></span>

* <span data-ttu-id="4821a-359">Corretto: i messaggi in coda con le librerie .NET o Java non vengono decodificati correttamente da base64</span><span class="sxs-lookup"><span data-stu-id="4821a-359">Fixed: queue messages inserted with .NET or Java libraries are not properly decoded from base64</span></span>
* <span data-ttu-id="4821a-360">Corretto: le tabelle $metrics non vengono visualizzate per gli account di archiviazione Blob</span><span class="sxs-lookup"><span data-stu-id="4821a-360">Fixed: $metrics tables are not shown for Blob Storage accounts</span></span>
* <span data-ttu-id="4821a-361">Corretto: il nodo delle tabelle non funziona per l'archiviazione locale (sviluppo)</span><span class="sxs-lookup"><span data-stu-id="4821a-361">Fixed: tables node does not work for local (Development) storage</span></span>

#### <a name="known-issues"></a><span data-ttu-id="4821a-362">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="4821a-362">Known Issues</span></span>

* <span data-ttu-id="4821a-363">L'installazione di macOS potrebbe richiedere autorizzazioni elevate</span><span class="sxs-lookup"><span data-stu-id="4821a-363">macOS install may require elevated permissions</span></span>

<span data-ttu-id="4821a-364">15/06/2016</span><span class="sxs-lookup"><span data-stu-id="4821a-364">06/15/2016</span></span>
### <a name="version-080"></a><span data-ttu-id="4821a-365">Versione 0.8.0</span><span class="sxs-lookup"><span data-stu-id="4821a-365">Version 0.8.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="4821a-366">Nuovo</span><span class="sxs-lookup"><span data-stu-id="4821a-366">New</span></span>

* <span data-ttu-id="4821a-367">Supporto per condivisione file: visualizzazione, caricamento, download, copia di file e directory, URI della firma di accesso condiviso (creazione e la connessione)</span><span class="sxs-lookup"><span data-stu-id="4821a-367">File share support: viewing, uploading, downloading, copying files and directories, SAS URIs (create and connect)</span></span>
* <span data-ttu-id="4821a-368">Esperienza utente migliorata in termini di connessione a Storage con chiavi di account o URI della firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="4821a-368">Improved user experience for connecting to Storage with SAS URIs or account keys</span></span>
* <span data-ttu-id="4821a-369">Risultati della query relativa alla tabella di esportazione</span><span class="sxs-lookup"><span data-stu-id="4821a-369">Export table query results</span></span>
* <span data-ttu-id="4821a-370">Riordinamento e personalizzazione delle colonne della tabella</span><span class="sxs-lookup"><span data-stu-id="4821a-370">Table column reordering and customization</span></span>
* <span data-ttu-id="4821a-371">Visualizzazione dei contenitori BLOB $logs e delle tabelle $metrics per gli account di archiviazione con le metriche abilitate</span><span class="sxs-lookup"><span data-stu-id="4821a-371">Viewing $logs blob containers and $metrics tables for Storage Accounts with enabled metrics</span></span>
* <span data-ttu-id="4821a-372">Comportamento di esportazione e importazione migliorato, include ora il tipo di valore della proprietà</span><span class="sxs-lookup"><span data-stu-id="4821a-372">Improved export and import behavior, now includes property value type</span></span>

#### <a name="fixes"></a><span data-ttu-id="4821a-373">Correzioni</span><span class="sxs-lookup"><span data-stu-id="4821a-373">Fixes</span></span>

* <span data-ttu-id="4821a-374">Corretto: il caricamento o il download di BLOB di grandi dimensioni può essere incompleto</span><span class="sxs-lookup"><span data-stu-id="4821a-374">Fixed: uploading or downloading large blobs can result in incomplete uploads/downloads</span></span>
* <span data-ttu-id="4821a-375">Corretto: la modifica, l'aggiunta o l'importazione di un'entità con un valore numerico ("1") ne comporta il raddoppiamento</span><span class="sxs-lookup"><span data-stu-id="4821a-375">Fixed: editing, adding, or importing an entity with a numeric string value ("1") will convert it to double</span></span>
* <span data-ttu-id="4821a-376">Corretto: impossibile espandere il nodo della tabella nell'ambiente di sviluppo locale</span><span class="sxs-lookup"><span data-stu-id="4821a-376">Fixed: Unable to expand the table node in the local development environment</span></span>

#### <a name="known-issues"></a><span data-ttu-id="4821a-377">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="4821a-377">Known Issues</span></span>

* <span data-ttu-id="4821a-378">L tabelle $metrics non sono visibili per gli account di archiviazione Blob</span><span class="sxs-lookup"><span data-stu-id="4821a-378">$metrics tables are not visible for Blob Storage accounts</span></span>
* <span data-ttu-id="4821a-379">I messaggi in coda aggiunti a livello di programmazione potrebbe non essere visualizzati correttamente se i messaggi vengono codificati tramite la codifica Base64</span><span class="sxs-lookup"><span data-stu-id="4821a-379">Queue messages added programmatically may not be displayed correctly if the messages are encoded using Base64 encoding</span></span>

<span data-ttu-id="4821a-380">17/05/2016</span><span class="sxs-lookup"><span data-stu-id="4821a-380">05/17/2016</span></span>
### <a name="version-07201605090"></a><span data-ttu-id="4821a-381">Versione 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="4821a-381">Version 0.7.20160509.0</span></span>

#### <a name="new"></a><span data-ttu-id="4821a-382">Nuovo</span><span class="sxs-lookup"><span data-stu-id="4821a-382">New</span></span>

* <span data-ttu-id="4821a-383">Migliore gestione degli errori per i crash dell'app</span><span class="sxs-lookup"><span data-stu-id="4821a-383">Better error handling for app crashes</span></span>

#### <a name="fixes"></a><span data-ttu-id="4821a-384">Correzioni</span><span class="sxs-lookup"><span data-stu-id="4821a-384">Fixes</span></span>

* <span data-ttu-id="4821a-385">Correzione del bug per cui i messaggi sulla barra delle informazioni talvolta non vengono visualizzati quando sono necessarie credenziali di accesso</span><span class="sxs-lookup"><span data-stu-id="4821a-385">Fixed bug where InfoBar messages sometimes don't show up when sign-in credentials were required</span></span>

#### <a name="known-issues"></a><span data-ttu-id="4821a-386">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="4821a-386">Known Issues</span></span>

* <span data-ttu-id="4821a-387">Tabelle: in fase di aggiunta, modifica o importazione di un'entità che dispone di una proprietà con un valore numerico ambiguo, ad esempio "1" o "1.0", quando l'utente tenta di inviare il valore come un `Edm.String`, questo ritornerà indietro attraverso l'API del client come Edm.Double</span><span class="sxs-lookup"><span data-stu-id="4821a-387">Tables: Adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and the user tries to send it as an `Edm.String`, the value will come back through the client API as an Edm.Double</span></span>

<span data-ttu-id="4821a-388">31/03/2016</span><span class="sxs-lookup"><span data-stu-id="4821a-388">03/31/2016</span></span>

### <a name="version-07201603250"></a><span data-ttu-id="4821a-389">Versione 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="4821a-389">Version 0.7.20160325.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="4821a-390">Nuovo</span><span class="sxs-lookup"><span data-stu-id="4821a-390">New</span></span>

* <span data-ttu-id="4821a-391">Supporto tabella: visualizzazione, esecuzione di query, esportazione, importazione e operazioni CRUD per le entità</span><span class="sxs-lookup"><span data-stu-id="4821a-391">Table support: viewing, querying, export, import, and CRUD operations for entities</span></span>
* <span data-ttu-id="4821a-392">Supporto coda: visualizzazione, aggiunta, rimozione dei messaggi dalla coda</span><span class="sxs-lookup"><span data-stu-id="4821a-392">Queue support: viewing, adding, dequeueing messages</span></span>
* <span data-ttu-id="4821a-393">Generazione di URI della firma di accesso condiviso per gli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4821a-393">Generating SAS URIs for Storage Accounts</span></span>
* <span data-ttu-id="4821a-394">La connessione agli account di archiviazione con l'URI della firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="4821a-394">Connecting to Storage Accounts with SAS URIs</span></span>
* <span data-ttu-id="4821a-395">Notifiche di aggiornamento per gli aggiornamenti futuri di Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="4821a-395">Update notifications for future updates to Storage Explorer</span></span>
* <span data-ttu-id="4821a-396">Aspetto aggiornato</span><span class="sxs-lookup"><span data-stu-id="4821a-396">Updated look and feel</span></span>

#### <a name="fixes"></a><span data-ttu-id="4821a-397">Correzioni</span><span class="sxs-lookup"><span data-stu-id="4821a-397">Fixes</span></span>

* <span data-ttu-id="4821a-398">Miglioramenti dell'affidabilità e delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="4821a-398">Performance and reliability improvements</span></span>

### <a name="known-issues-amp-mitigations"></a><span data-ttu-id="4821a-399">Problemi noti &amp; Prevenzione</span><span class="sxs-lookup"><span data-stu-id="4821a-399">Known Issues &amp; Mitigations</span></span>

* <span data-ttu-id="4821a-400">Il download di file BLOB di grandi dimensioni non funziona correttamente. È consigliabile usare AzCopy fino alla risoluzione del problema</span><span class="sxs-lookup"><span data-stu-id="4821a-400">Download of large blob files does not work correctly - we recommend using AzCopy while we address this issue</span></span> 
* <span data-ttu-id="4821a-401">Le credenziali dell'account non verranno recuperate o memorizzate nella cache se non è possibile trovare la cartella home o questa non può essere scritta</span><span class="sxs-lookup"><span data-stu-id="4821a-401">Account credentials will not be retrieved nor cached if the home folder cannot be found or cannot be written to</span></span>
* <span data-ttu-id="4821a-402">In fase di aggiunta, modifica o importazione di un'entità che dispone di una proprietà con un valore numerico ambiguo, ad esempio "1" o "1.0", quando l'utente tenta di inviare il valore come un `Edm.String`, questo ritornerà indietro attraverso l'API del client come Edm.Double</span><span class="sxs-lookup"><span data-stu-id="4821a-402">If we are adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and the user tries to send it as an `Edm.String`, the value will come back through the client API as an Edm.Double</span></span>
* <span data-ttu-id="4821a-403">Quando si importano file CSV con i record su più righe, i dati possono venire tagliati o mescolati</span><span class="sxs-lookup"><span data-stu-id="4821a-403">When importing CSV files with multiline records, the data may get chopped or scrambled</span></span>

<span data-ttu-id="4821a-404">03/02/2016</span><span class="sxs-lookup"><span data-stu-id="4821a-404">02/03/2016</span></span>

### <a name="version-07201601291"></a><span data-ttu-id="4821a-405">Versione 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="4821a-405">Version 0.7.20160129.1</span></span>

#### <a name="fixes"></a><span data-ttu-id="4821a-406">Correzioni</span><span class="sxs-lookup"><span data-stu-id="4821a-406">Fixes</span></span>

* <span data-ttu-id="4821a-407">Miglioramento delle prestazioni complessive durante il caricamento, il download e la copia di BLOB</span><span class="sxs-lookup"><span data-stu-id="4821a-407">Improved overall performance when uploading, downloading and copying blobs</span></span>

<span data-ttu-id="4821a-408">14/01/2016</span><span class="sxs-lookup"><span data-stu-id="4821a-408">01/14/2016</span></span>

### <a name="version-07201601050"></a><span data-ttu-id="4821a-409">Versione 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="4821a-409">Version 0.7.20160105.0</span></span>

#### <a name="new"></a><span data-ttu-id="4821a-410">Nuovo</span><span class="sxs-lookup"><span data-stu-id="4821a-410">New</span></span>

* <span data-ttu-id="4821a-411">Supporto Linux (funzionalità analoghe a OSX)</span><span class="sxs-lookup"><span data-stu-id="4821a-411">Linux support (parity features to OSX)</span></span>
* <span data-ttu-id="4821a-412">Aggiunta di contenitori BLOB con la chiave di firma di accesso condiviso (SAS)</span><span class="sxs-lookup"><span data-stu-id="4821a-412">Add blob containers with Shared Access Signatures (SAS) key</span></span>
* <span data-ttu-id="4821a-413">Aggiunta degli account di archiviazione per Azure China</span><span class="sxs-lookup"><span data-stu-id="4821a-413">Add Storage Accounts for Azure China</span></span>
* <span data-ttu-id="4821a-414">Aggiunta di account di archiviazione con endpoint personalizzati</span><span class="sxs-lookup"><span data-stu-id="4821a-414">Add Storage Accounts with custom endpoints</span></span>
* <span data-ttu-id="4821a-415">Apertura e visualizzazione di BLOB di testo e immagine del contenuto</span><span class="sxs-lookup"><span data-stu-id="4821a-415">Open and view the contents text and picture blobs</span></span>
* <span data-ttu-id="4821a-416">Visualizzazione e modifica di metadati e proprietà di BLOB</span><span class="sxs-lookup"><span data-stu-id="4821a-416">View and edit blob properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="4821a-417">Correzioni</span><span class="sxs-lookup"><span data-stu-id="4821a-417">Fixes</span></span>

* <span data-ttu-id="4821a-418">Corretto: a volte il caricamento o il download di un numero elevato di BLOB (500+) può risultare in una schermata bianca dell'app</span><span class="sxs-lookup"><span data-stu-id="4821a-418">Fixed: uploading or download a large number of blobs (500+) may sometimes cause the app to have a white screen</span></span> 
* <span data-ttu-id="4821a-419">Corretto: quando si imposta il livello di accesso pubblico del contenitore BLOB, il nuovo valore non viene aggiornato finché non si imposta nuovamente lo stato attivo sul contenitore.</span><span class="sxs-lookup"><span data-stu-id="4821a-419">Fixed: when setting blob container public access level, the new value is not updated until you re-set the focus on the container.</span></span> <span data-ttu-id="4821a-420">Inoltre, per impostazione predefinita la finestra di dialogo è sempre impostata su "Nessun accesso pubblico" e non sul valore effettivo corrente.</span><span class="sxs-lookup"><span data-stu-id="4821a-420">Also, the dialog always defaults to "No public access", and not the actual current value.</span></span>
* <span data-ttu-id="4821a-421">Miglioramenti generali della tastiera/accessibilità e del supporto interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="4821a-421">Better overall keyboard/accessibility and UI support</span></span>
* <span data-ttu-id="4821a-422">Wrapping di testo della cronologia di navigazione quando è lungo con spazio</span><span class="sxs-lookup"><span data-stu-id="4821a-422">Breadcrumbs history text wraps when it's long with white space</span></span>
* <span data-ttu-id="4821a-423">La finestra di dialogo della firma di accesso condiviso supporta la convalida dell'input</span><span class="sxs-lookup"><span data-stu-id="4821a-423">SAS dialog supports input validation</span></span>
* <span data-ttu-id="4821a-424">L'archiviazione locale continua a essere disponibile anche se le credenziali utente sono scadute</span><span class="sxs-lookup"><span data-stu-id="4821a-424">Local storage continues to be available even if user credentials have expired</span></span>
* <span data-ttu-id="4821a-425">Quando viene eliminato un contenitore BLOB aperto, viene chiuso Esplora risorse BLOB sul lato destro</span><span class="sxs-lookup"><span data-stu-id="4821a-425">When an opened blob container is deleted, the blob explorer on the right side is closed</span></span>

#### <a name="known-issues"></a><span data-ttu-id="4821a-426">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="4821a-426">Known Issues</span></span>

* <span data-ttu-id="4821a-427">Linux richiede l'aggiornamento della versione gcc. La procedura per effettuare l'aggiornamento è riportata qui sotto:</span><span class="sxs-lookup"><span data-stu-id="4821a-427">Linux install needs gcc version updated or upgraded – steps to upgrade are below:</span></span> 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

<span data-ttu-id="4821a-428">18/11/2015</span><span class="sxs-lookup"><span data-stu-id="4821a-428">11/18/2015</span></span>
### <a name="version-07201511160"></a><span data-ttu-id="4821a-429">Versione 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="4821a-429">Version 0.7.20151116.0</span></span>

#### <a name="new"></a><span data-ttu-id="4821a-430">Nuovo</span><span class="sxs-lookup"><span data-stu-id="4821a-430">New</span></span>

* <span data-ttu-id="4821a-431">Versioni per macOS e Windows</span><span class="sxs-lookup"><span data-stu-id="4821a-431">macOS, and Windows versions</span></span>
* <span data-ttu-id="4821a-432">Accesso per visualizzare gli account di archiviazione: possibilità di usare l'account aziendale, l'account Microsoft, 2FA e così via.</span><span class="sxs-lookup"><span data-stu-id="4821a-432">Sign in to view your Storage Accounts – use your Org Account, Microsoft Account, 2FA, etc.</span></span>
* <span data-ttu-id="4821a-433">Archivio di sviluppo locale (usare l'emulatore di archiviazione, solo Windows)</span><span class="sxs-lookup"><span data-stu-id="4821a-433">Local development storage (use storage emulator, Windows-only)</span></span>
* <span data-ttu-id="4821a-434">Supporto di Azure Resource Manager e delle risorse Classic</span><span class="sxs-lookup"><span data-stu-id="4821a-434">Azure Resource Manager and Classic resource support</span></span>
* <span data-ttu-id="4821a-435">Creazione ed eliminazione di BLOB, code o tabelle</span><span class="sxs-lookup"><span data-stu-id="4821a-435">Create and delete blobs, queues, or tables</span></span>
* <span data-ttu-id="4821a-436">Ricerca di BLOB, code o tabelle specifiche</span><span class="sxs-lookup"><span data-stu-id="4821a-436">Search for specific blobs, queues, or tables</span></span>
* <span data-ttu-id="4821a-437">Esplorazione del contenuto dei contenitori BLOB</span><span class="sxs-lookup"><span data-stu-id="4821a-437">Explore the contents of blob containers</span></span>
* <span data-ttu-id="4821a-438">Visualizzazione e spostamento tra directory</span><span class="sxs-lookup"><span data-stu-id="4821a-438">View and navigate through directories</span></span>
* <span data-ttu-id="4821a-439">Caricamento, download ed eliminazione di BLOB e cartelle</span><span class="sxs-lookup"><span data-stu-id="4821a-439">Upload, download, and delete blobs and folders</span></span>
* <span data-ttu-id="4821a-440">Visualizzazione e modifica di metadati e proprietà di BLOB</span><span class="sxs-lookup"><span data-stu-id="4821a-440">View and edit blob properties and metadata</span></span>
* <span data-ttu-id="4821a-441">Generazione di chiavi di firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="4821a-441">Generate SAS keys</span></span>
* <span data-ttu-id="4821a-442">Gestione e creazione di SAP (Stored Access Policies)</span><span class="sxs-lookup"><span data-stu-id="4821a-442">Manage and create Stored Access Policies (SAP)</span></span>
* <span data-ttu-id="4821a-443">Ricerca di BLOB in base al prefisso</span><span class="sxs-lookup"><span data-stu-id="4821a-443">Search for blobs by prefix</span></span>
* <span data-ttu-id="4821a-444">Trascinamento della selezione di file da caricare o scaricare</span><span class="sxs-lookup"><span data-stu-id="4821a-444">Drag 'n drop files to upload or download</span></span>

#### <a name="known-issues"></a><span data-ttu-id="4821a-445">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="4821a-445">Known Issues</span></span>

* <span data-ttu-id="4821a-446">Quando si imposta il livello di accesso pubblico del contenitore BLOB, il nuovo valore non viene aggiornato finché non si imposta nuovamente lo stato attivo sul contenitore</span><span class="sxs-lookup"><span data-stu-id="4821a-446">When setting blob container public access level, the new value is not updated until you re-set the focus on the container</span></span>
* <span data-ttu-id="4821a-447">Quando si apre la finestra di dialogo per impostare il livello di accesso pubblico, viene sempre visualizzato "Nessun accesso pubblico" come valore predefinito e non il valore corrente effettivo</span><span class="sxs-lookup"><span data-stu-id="4821a-447">When you open the dialog to set the public access level, it always shows "No public access" as the default, and not the actual current value</span></span>
* <span data-ttu-id="4821a-448">Impossibile rinominare i BLOB scaricati</span><span class="sxs-lookup"><span data-stu-id="4821a-448">Cannot rename downloaded blobs</span></span>
* <span data-ttu-id="4821a-449">Le voci del log attività a volte rimangono "bloccate" in stato in corso quando si verifica un errore, e l'errore non viene visualizzato</span><span class="sxs-lookup"><span data-stu-id="4821a-449">Activity log entries will sometimes get "stuck" in an in progress state when an error occurs, and the error is not displayed</span></span>
* <span data-ttu-id="4821a-450">A volte si verifica un crash o diventa completamente bianco quando si cerca di caricare o scaricare un numero elevato di BLOB</span><span class="sxs-lookup"><span data-stu-id="4821a-450">Sometimes crashes or turns completely white when trying to upload or download a large number of blobs</span></span>
* <span data-ttu-id="4821a-451">In alcuni casi l'annullamento di un'operazione di copia non funziona</span><span class="sxs-lookup"><span data-stu-id="4821a-451">Sometimes canceling a copy operation does not work</span></span>
* <span data-ttu-id="4821a-452">Durante la creazione di un contenitore (BLOB/coda/tabella), se si immette un nome non valido di input e si procede alla creazione di un altro nome in un altro tipo di contenitore non è possibile impostare lo stato attivo sul nuovo tipo</span><span class="sxs-lookup"><span data-stu-id="4821a-452">During creating a container (blob/queue/table), if you input an invalid name and proceed to create another under a different container type you cannot set focus on the new type</span></span>
* <span data-ttu-id="4821a-453">Impossibile creare una nuova cartella o rinominare una cartella</span><span class="sxs-lookup"><span data-stu-id="4821a-453">Can't create new folder or rename folder</span></span>




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md