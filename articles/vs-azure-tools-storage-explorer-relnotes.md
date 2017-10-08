---
title: note sulla versione di aaaMicrosoft Esplora archivi Azure (anteprima) | Documenti Microsoft
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
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a><span data-ttu-id="9b4ba-103">Note sulla versione di Microsoft Azure Storage Explorer (anteprima)</span><span class="sxs-lookup"><span data-stu-id="9b4ba-103">Microsoft Azure Storage Explorer (Preview) release notes</span></span>

<span data-ttu-id="9b4ba-104">Questo articolo contiene una versione di hello release notes per Azure Storage Explorer 0.8.16 (anteprima), nonché le note sulla versione per le versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-104">This article contains hello release notes for Azure Storage Explorer 0.8.16 (Preview) release, as well as release notes for previous versions.</span></span>

<span data-ttu-id="9b4ba-105">[Esplora archivi di Microsoft Azure (anteprima)](./vs-azure-tools-storage-manage-with-storage-explorer.md) è un'applicazione autonoma che consente di utilizzare tooeasily dati di archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-105">[Microsoft Azure Storage Explorer (Preview)](./vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, macOS, and Linux.</span></span>

## <a name="version-0816-preview"></a><span data-ttu-id="9b4ba-106">Versione 0.8.16 (anteprima)</span><span class="sxs-lookup"><span data-stu-id="9b4ba-106">Version 0.8.16 (Preview)</span></span>
<span data-ttu-id="9b4ba-107">21/08/2017</span><span class="sxs-lookup"><span data-stu-id="9b4ba-107">8/21/2017</span></span>

### <a name="download-azure-storage-explorer-0816-preview"></a><span data-ttu-id="9b4ba-108">Download di Azure Storage Explorer 0.8.16 (anteprima)</span><span class="sxs-lookup"><span data-stu-id="9b4ba-108">Download Azure Storage Explorer 0.8.16 (Preview)</span></span>
- [<span data-ttu-id="9b4ba-109">Azure Storage Explorer 0.8.16 (anteprima) per Windows</span><span class="sxs-lookup"><span data-stu-id="9b4ba-109">Azure Storage Explorer 0.8.16 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=708343)
- [<span data-ttu-id="9b4ba-110">Azure Storage Explorer 0.8.16 (anteprima) per Mac</span><span class="sxs-lookup"><span data-stu-id="9b4ba-110">Azure Storage Explorer 0.8.16 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=708342)
- [<span data-ttu-id="9b4ba-111">Azure Storage Explorer 0.8.16 (anteprima) per Linux</span><span class="sxs-lookup"><span data-stu-id="9b4ba-111">Azure Storage Explorer 0.8.16 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a><span data-ttu-id="9b4ba-112">Nuovo</span><span class="sxs-lookup"><span data-stu-id="9b4ba-112">New</span></span>
* <span data-ttu-id="9b4ba-113">Quando si apre un blob, Esplora archivi richiederà file hello scaricato tooupload se viene rilevata una modifica</span><span class="sxs-lookup"><span data-stu-id="9b4ba-113">When you open a blob, Storage Explorer will prompt you tooupload hello downloaded file if a change is detected</span></span>
* <span data-ttu-id="9b4ba-114">Esperienza di accesso ad Azure Stack migliorata</span><span class="sxs-lookup"><span data-stu-id="9b4ba-114">Enhanced Azure Stack sign-in experience</span></span>
* <span data-ttu-id="9b4ba-115">Prestazioni migliorate hello caricamento/scaricamento di molti piccoli file hello stesso tempo</span><span class="sxs-lookup"><span data-stu-id="9b4ba-115">Improved hello performance of uploading/downloading many small files at hello same time</span></span>


### <a name="fixes"></a><span data-ttu-id="9b4ba-116">Correzioni</span><span class="sxs-lookup"><span data-stu-id="9b4ba-116">Fixes</span></span>
* <span data-ttu-id="9b4ba-117">Per alcuni tipi di blob, scelta troppo "replace" durante un conflitto di caricamento talvolta comporta il caricamento di hello in fase di riavvio.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-117">For some blob types, choosing too"replace" during an upload conflict would sometimes result in hello upload being restarted.</span></span> 
* <span data-ttu-id="9b4ba-118">Nella versione 0.8.15 i caricamenti rimangono talvolta bloccati al 99%.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-118">In version 0.8.15, uploads would sometimes stall at 99%.</span></span>
* <span data-ttu-id="9b4ba-119">Durante il caricamento di condivisione file tooa di file, se si sceglie di directory di tooa tooupload che ancora non esiste, il caricamento avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-119">When uploading files tooa file share, if you chose tooupload tooa directory which did not yet exist, your upload would fail.</span></span>
* <span data-ttu-id="9b4ba-120">Storage Explorer generava timestamp non corretti per le firme di accesso condiviso e le query di tabella.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-120">Storage Explorer was incorrectly generating time stamps for shared access signatures and table queries.</span></span>


<span data-ttu-id="9b4ba-121">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="9b4ba-121">Known Issues</span></span>
* <span data-ttu-id="9b4ba-122">L'uso di una stringa di connessione con nome e chiave attualmente non funziona.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-122">Using a name and key connection string does not currently work.</span></span> <span data-ttu-id="9b4ba-123">Si verrà risolto nella prossima versione di hello.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-123">It will be fixed in hello next release.</span></span> <span data-ttu-id="9b4ba-124">Fino ad allora è possibile collegarsi con nome e chiave.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-124">Until then you can use attach with name and key.</span></span>
* <span data-ttu-id="9b4ba-125">Se si tenta di tooopen un file con un nome di file non valido di Windows, il download di hello comporterà un errore file non trovato.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-125">If you try tooopen a file with an invalid Windows file name, hello download will result in a file not found error.</span></span>
* <span data-ttu-id="9b4ba-126">Dopo aver fatto clic "Annulla" per un'attività, potrebbe richiedere un po' di tempo per toocancel tale attività.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-126">After clicking "Cancel" on a task, it may take a while for that task toocancel.</span></span> <span data-ttu-id="9b4ba-127">Si tratta di una limitazione della libreria di hello nodo archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-127">This is a limitation of hello Azure Storage Node library.</span></span>
* <span data-ttu-id="9b4ba-128">Dopo aver completato il caricamento di un blob, scheda hello che ha avviato il caricamento di hello viene aggiornata.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-128">After completing a blob upload, hello tab which initiated hello upload is refreshed.</span></span> <span data-ttu-id="9b4ba-129">Questa è una modifica dal comportamento precedente e provocherà inoltre toobe ritirato toohello radice del contenitore di hello in.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-129">This is a change from previous behavior, and will also cause you toobe taken back toohello root of hello container you are in.</span></span>
* <span data-ttu-id="9b4ba-130">Se si sceglie di hello certificati smart card PIN o errato, sarà necessario toorestart in ordine toohave Esplora archivi dimenticare tale decisione.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-130">If you choose hello wrong PIN/Smartcard certificate, then you will need toorestart in order toohave Storage Explorer forget that decision.</span></span>
* <span data-ttu-id="9b4ba-131">impostazioni del Pannello di Hello account potrebbero mostrare che è necessario che le sottoscrizioni di toofilter credenziali tooreenter.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-131">hello account settings panel may show that you need tooreenter credentials toofilter subscriptions.</span></span>
* <span data-ttu-id="9b4ba-132">La ridenominazione di BLOB singoli o all'interno di un contenitore BLOB rinominato non mantiene gli snapshot.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-132">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="9b4ba-133">Tutte le altre proprietà e i metadati di BLOB, file ed entità vengono conservati durante un'operazione di ridenominazione.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-133">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="9b4ba-134">Sebbene Azure Stack attualmente non supporta le condivisioni file, viene comunque visualizzato un nodo delle condivisioni di file in un account di archiviazione di Azure Stack associato.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-134">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span>
* <span data-ttu-id="9b4ba-135">Per gli utenti Ubuntu 14.04, sarà necessario tooensure GCC sia attivo toodate - questa operazione può essere eseguita tramite l'esecuzione di hello i comandi seguenti e quindi riavviare il computer:</span><span class="sxs-lookup"><span data-stu-id="9b4ba-135">For users on Ubuntu 14.04, you will need tooensure GCC is up toodate - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* <span data-ttu-id="9b4ba-136">Per gli utenti 17.04 Ubuntu, sarà necessario tooinstall GConf - questo scopo, in esecuzione hello i comandi seguenti e quindi riavviare il computer:</span><span class="sxs-lookup"><span data-stu-id="9b4ba-136">For users on Ubuntu 17.04, you will need tooinstall GConf - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a><span data-ttu-id="9b4ba-137">Versione 0.8.14 (anteprima)</span><span class="sxs-lookup"><span data-stu-id="9b4ba-137">Version 0.8.14 (Preview)</span></span>
<span data-ttu-id="9b4ba-138">22/06/2017</span><span class="sxs-lookup"><span data-stu-id="9b4ba-138">06/22/2017</span></span>

### <a name="download-azure-storage-explorer-0814-preview"></a><span data-ttu-id="9b4ba-139">Download di Azure Storage Explorer 0.8.14 (anteprima)</span><span class="sxs-lookup"><span data-stu-id="9b4ba-139">Download Azure Storage Explorer 0.8.14 (Preview)</span></span>
* [<span data-ttu-id="9b4ba-140">Download di Azure Storage Explorer 0.8.14 (anteprima) per Windows</span><span class="sxs-lookup"><span data-stu-id="9b4ba-140">Download Azure Storage Explorer 0.8.14 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=809306)
* [<span data-ttu-id="9b4ba-141">Download di Azure Storage Explorer 0.8.14 (anteprima) per Mac</span><span class="sxs-lookup"><span data-stu-id="9b4ba-141">Download Azure Storage Explorer 0.8.14 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=809307)
* [<span data-ttu-id="9b4ba-142">Download di Azure Storage Explorer 0.8.14 (anteprima) per Linux</span><span class="sxs-lookup"><span data-stu-id="9b4ba-142">Download Azure Storage Explorer 0.8.14 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a><span data-ttu-id="9b4ba-143">Nuovo</span><span class="sxs-lookup"><span data-stu-id="9b4ba-143">New</span></span>

* <span data-ttu-id="9b4ba-144">Too1.7.2 di versione elettronici aggiornato in diversi aggiornamenti critici della protezione sfruttare tootake ordine</span><span class="sxs-lookup"><span data-stu-id="9b4ba-144">Updated Electron version too1.7.2 in order tootake advantage of several critical security updates</span></span>
* <span data-ttu-id="9b4ba-145">È possibile ora accedere rapidamente nella Guida in linea sulla risoluzione dei problemi hello dal menu di hello?</span><span class="sxs-lookup"><span data-stu-id="9b4ba-145">You can now quickly access hello online troubleshooting guide from hello help menu</span></span>
* <span data-ttu-id="9b4ba-146">[Guida][2]alla risoluzione dei problemi di Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="9b4ba-146">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="9b4ba-147">[Istruzioni] [ 3] sulla connessione di sottoscrizione di Azure Stack tooan</span><span class="sxs-lookup"><span data-stu-id="9b4ba-147">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

### <a name="known-issues"></a><span data-ttu-id="9b4ba-148">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="9b4ba-148">Known Issues</span></span>

* <span data-ttu-id="9b4ba-149">I pulsanti nella finestra di dialogo Conferma cartella delete hello non registra con il clic del mouse hello in Linux.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-149">Buttons on hello delete folder confirmation dialog don't register with hello mouse clicks on Linux.</span></span> <span data-ttu-id="9b4ba-150">Soluzione alternativa è l'invio di toouse hello</span><span class="sxs-lookup"><span data-stu-id="9b4ba-150">Workaround is toouse hello Enter key</span></span>
* <span data-ttu-id="9b4ba-151">Se si sceglie di hello certificati smart card PIN o errato, sarà necessario toorestart in ordine toohave Esplora archivi dimenticare decisione hello</span><span class="sxs-lookup"><span data-stu-id="9b4ba-151">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="9b4ba-152">Più di 3 gruppi di BLOB o i file di caricamento in hello stesso tempo può causare errori</span><span class="sxs-lookup"><span data-stu-id="9b4ba-152">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="9b4ba-153">impostazioni del Pannello di account Hello possono indicare che sono necessarie le credenziali di tooreenter nelle sottoscrizioni toofilter ordine</span><span class="sxs-lookup"><span data-stu-id="9b4ba-153">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="9b4ba-154">La ridenominazione di BLOB singoli o all'interno di un contenitore BLOB rinominato non mantiene gli snapshot.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-154">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="9b4ba-155">Tutte le altre proprietà e i metadati di BLOB, file ed entità vengono conservati durante un'operazione di ridenominazione.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-155">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="9b4ba-156">Sebbene Azure Stack attualmente non supporta le condivisioni file, viene comunque visualizzato un nodo delle condivisioni di file in un account di archiviazione di Azure Stack associato.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-156">Although Azure Stack doesn't currently support File Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="9b4ba-157">Di seguito sono Ubuntu 14.04 esigenze di installare le versioni o aggiornare – tooupgrade passaggi:</span><span class="sxs-lookup"><span data-stu-id="9b4ba-157">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a><span data-ttu-id="9b4ba-158">Versioni precedenti</span><span class="sxs-lookup"><span data-stu-id="9b4ba-158">Previous releases</span></span>

* [<span data-ttu-id="9b4ba-159">Versione 0.8.13</span><span class="sxs-lookup"><span data-stu-id="9b4ba-159">Version 0.8.13</span></span>](#version-0813)
* [<span data-ttu-id="9b4ba-160">Versione 0.8.12/0.8.11/0.8.10</span><span class="sxs-lookup"><span data-stu-id="9b4ba-160">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>](#version-0812--0811--0810)
* [<span data-ttu-id="9b4ba-161">Versione 0.8.9/0.8.8</span><span class="sxs-lookup"><span data-stu-id="9b4ba-161">Version 0.8.9 / 0.8.8</span></span>](#version-089--088)
* [<span data-ttu-id="9b4ba-162">Versione 0.8.7</span><span class="sxs-lookup"><span data-stu-id="9b4ba-162">Version 0.8.7</span></span>](#version-087)
* [<span data-ttu-id="9b4ba-163">Versione 0.8.6</span><span class="sxs-lookup"><span data-stu-id="9b4ba-163">Version 0.8.6</span></span>](#version-086)
* [<span data-ttu-id="9b4ba-164">Versione 0.8.5</span><span class="sxs-lookup"><span data-stu-id="9b4ba-164">Version 0.8.5</span></span>](#version-085)
* [<span data-ttu-id="9b4ba-165">Versione 0.8.4</span><span class="sxs-lookup"><span data-stu-id="9b4ba-165">Version 0.8.4</span></span>](#version-084)
* [<span data-ttu-id="9b4ba-166">Versione 0.8.3</span><span class="sxs-lookup"><span data-stu-id="9b4ba-166">Version 0.8.3</span></span>](#version-083)
* [<span data-ttu-id="9b4ba-167">Versione 0.8.2</span><span class="sxs-lookup"><span data-stu-id="9b4ba-167">Version 0.8.2</span></span>](#version-082)
* [<span data-ttu-id="9b4ba-168">Versione 0.8.0</span><span class="sxs-lookup"><span data-stu-id="9b4ba-168">Version 0.8.0</span></span>](#version-080)
* [<span data-ttu-id="9b4ba-169">Versione 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="9b4ba-169">Version 0.7.20160509.0</span></span>](#version-07201605090)
* [<span data-ttu-id="9b4ba-170">Versione 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="9b4ba-170">Version 0.7.20160325.0</span></span>](#version-07201603250)
* [<span data-ttu-id="9b4ba-171">Versione 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="9b4ba-171">Version 0.7.20160129.1</span></span>](#version-07201601291)
* [<span data-ttu-id="9b4ba-172">Versione 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="9b4ba-172">Version 0.7.20160105.0</span></span>](#version-07201601050)
* [<span data-ttu-id="9b4ba-173">Versione 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="9b4ba-173">Version 0.7.20151116.0</span></span>](#version-07201511160)


### <a name="version-0813"></a><span data-ttu-id="9b4ba-174">Versione 0.8.13</span><span class="sxs-lookup"><span data-stu-id="9b4ba-174">Version 0.8.13</span></span>
<span data-ttu-id="9b4ba-175">12/05/2017</span><span class="sxs-lookup"><span data-stu-id="9b4ba-175">05/12/2017</span></span>

#### <a name="new"></a><span data-ttu-id="9b4ba-176">Nuovo</span><span class="sxs-lookup"><span data-stu-id="9b4ba-176">New</span></span>

* <span data-ttu-id="9b4ba-177">[Guida][2]alla risoluzione dei problemi di Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="9b4ba-177">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="9b4ba-178">[Istruzioni] [ 3] sulla connessione di sottoscrizione di Azure Stack tooan</span><span class="sxs-lookup"><span data-stu-id="9b4ba-178">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

#### <a name="fixes"></a><span data-ttu-id="9b4ba-179">Correzioni</span><span class="sxs-lookup"><span data-stu-id="9b4ba-179">Fixes</span></span>

* <span data-ttu-id="9b4ba-180">Corretto: il caricamento del file aveva una probabilità elevata di causare un errore di memoria insufficiente</span><span class="sxs-lookup"><span data-stu-id="9b4ba-180">Fixed: File upload had a high chance of causing an out of memory error</span></span>
* <span data-ttu-id="9b4ba-181">Corretto: è ora possibile accedere con PIN/smart card</span><span class="sxs-lookup"><span data-stu-id="9b4ba-181">Fixed: You can now sign in with PIN/Smartcard</span></span>
* <span data-ttu-id="9b4ba-182">Corretto: l'azione Apri nel portale ora funziona con Azure China, Azure Germany, Azure US Government e Azure Stack</span><span class="sxs-lookup"><span data-stu-id="9b4ba-182">Fixed: Open in Portal now works with Azure China, Azure Germany, Azure US Government, and Azure Stack</span></span>
* <span data-ttu-id="9b4ba-183">Problema risolto: Durante il caricamento di un contenitore di blob tooa cartella, un errore "Operazione non valida" talvolta si verificherebbe</span><span class="sxs-lookup"><span data-stu-id="9b4ba-183">Fixed: While uploading a folder tooa blob container, an "Illegal operation" error would sometimes occur</span></span>
* <span data-ttu-id="9b4ba-184">Corretto: selezionare tutto ciò che è stato disabilitato durante la gestione di snapshot</span><span class="sxs-lookup"><span data-stu-id="9b4ba-184">Fixed: Select all was disabled while managing snapshots</span></span>
* <span data-ttu-id="9b4ba-185">Problema risolto: hello metadati del blob di base hello potrebbero essere sovrascritte dopo la visualizzazione delle proprietà hello relativi snapshot</span><span class="sxs-lookup"><span data-stu-id="9b4ba-185">Fixed: hello metadata of hello base blob might get overwritten after viewing hello properties of its snapshots</span></span>

#### <a name="known-issues"></a><span data-ttu-id="9b4ba-186">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="9b4ba-186">Known Issues</span></span>

* <span data-ttu-id="9b4ba-187">Se si sceglie di hello certificati smart card PIN o errato, sarà necessario toorestart in ordine toohave Esplora archivi dimenticare decisione hello</span><span class="sxs-lookup"><span data-stu-id="9b4ba-187">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="9b4ba-188">Mentre è stato eseguito lo zoom avanti o indietro, il livello di zoom hello momentaneamente possibile reimpostare livello predefinito toohello</span><span class="sxs-lookup"><span data-stu-id="9b4ba-188">While zoomed in or out, hello zoom level may momentarily reset toohello default level</span></span>
* <span data-ttu-id="9b4ba-189">Più di 3 gruppi di BLOB o i file di caricamento in hello stesso tempo può causare errori</span><span class="sxs-lookup"><span data-stu-id="9b4ba-189">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="9b4ba-190">impostazioni del Pannello di account Hello possono indicare che sono necessarie le credenziali di tooreenter nelle sottoscrizioni toofilter ordine</span><span class="sxs-lookup"><span data-stu-id="9b4ba-190">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="9b4ba-191">La ridenominazione di BLOB singoli o all'interno di un contenitore BLOB rinominato non mantiene gli snapshot.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-191">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="9b4ba-192">Tutte le altre proprietà e i metadati di BLOB, file ed entità vengono conservati durante un'operazione di ridenominazione.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-192">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="9b4ba-193">Sebbene Azure Stack attualmente non supporta le condivisioni file, viene comunque visualizzato un nodo delle condivisioni di file in un account di archiviazione di Azure Stack associato.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-193">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="9b4ba-194">Di seguito sono Ubuntu 14.04 esigenze di installare le versioni o aggiornare – tooupgrade passaggi:</span><span class="sxs-lookup"><span data-stu-id="9b4ba-194">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a><span data-ttu-id="9b4ba-195">Versione 0.8.12/0.8.11/0.8.10</span><span class="sxs-lookup"><span data-stu-id="9b4ba-195">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>
<span data-ttu-id="9b4ba-196">07/04/2017</span><span class="sxs-lookup"><span data-stu-id="9b4ba-196">04/07/2017</span></span>

#### <a name="new"></a><span data-ttu-id="9b4ba-197">Nuovo</span><span class="sxs-lookup"><span data-stu-id="9b4ba-197">New</span></span>

* <span data-ttu-id="9b4ba-198">Esplora archivi verrà chiuso automaticamente quando si installa un aggiornamento da una notifica di aggiornamento hello</span><span class="sxs-lookup"><span data-stu-id="9b4ba-198">Storage Explorer will now automatically close when you install an update from hello update notification</span></span>
* <span data-ttu-id="9b4ba-199">L'accesso rapido sul posto fornisce un'esperienza ottimizzata per l'uso con le risorse a cui si accede di frequente</span><span class="sxs-lookup"><span data-stu-id="9b4ba-199">In-place quick access provides an enhanced experience for working with your frequently accessed resources</span></span>
* <span data-ttu-id="9b4ba-200">Nell'editor di hello contenitore Blob, è ora possibile visualizzare un blob con lease appartiene alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="9b4ba-200">In hello Blob Container editor, you can now see which virtual machine a leased blob belongs to</span></span>
* <span data-ttu-id="9b4ba-201">È ora possibile comprimere il riquadro di sinistra hello</span><span class="sxs-lookup"><span data-stu-id="9b4ba-201">You can now collapse hello left side panel</span></span>
* <span data-ttu-id="9b4ba-202">Individuazione ora viene eseguito nel hello stesso tempo come download</span><span class="sxs-lookup"><span data-stu-id="9b4ba-202">Discovery now runs at hello same time as download</span></span>
* <span data-ttu-id="9b4ba-203">Le statistiche di utilizzo nel contenitore Blob, condivisione File e tabella editor toosee hello le dimensioni della risorsa o selezione hello</span><span class="sxs-lookup"><span data-stu-id="9b4ba-203">Use Statistics in hello Blob Container, File Share, and Table editors toosee hello size of your resource or selection</span></span>
* <span data-ttu-id="9b4ba-204">È possibile adesso Accedi tooAzure Active Directory (AAD) basato su account di Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-204">You can now sign-in tooAzure Active Directory (AAD) based Azure Stack accounts.</span></span> 
* <span data-ttu-id="9b4ba-205">È possibile ora i file di archivio di caricamento di account di archiviazione di più di 32 MB tooPremium</span><span class="sxs-lookup"><span data-stu-id="9b4ba-205">You can now upload archive files over 32MB tooPremium storage accounts</span></span>
* <span data-ttu-id="9b4ba-206">Supporto di accessibilità migliorato</span><span class="sxs-lookup"><span data-stu-id="9b4ba-206">Improved accessibility support</span></span>
* <span data-ttu-id="9b4ba-207">È ora possibile aggiungere Base-64 attendibili i certificati x. 509 SSL per la codifica verrà tooEdit -&gt; i certificati SSL -&gt; importazione certificati</span><span class="sxs-lookup"><span data-stu-id="9b4ba-207">You can now add trusted Base-64 encoded X.509 SSL certificates by going tooEdit -&gt; SSL Certificates -&gt; Import Certificates</span></span>

#### <a name="fixes"></a><span data-ttu-id="9b4ba-208">Correzioni</span><span class="sxs-lookup"><span data-stu-id="9b4ba-208">Fixes</span></span>

* <span data-ttu-id="9b4ba-209">Problema risolto: dopo l'aggiornamento delle credenziali dell'account, visualizzazione albero hello sarebbe talvolta viene aggiornata automaticamente</span><span class="sxs-lookup"><span data-stu-id="9b4ba-209">Fixed: after refreshing an account's credentials, hello tree view would sometimes not automatically refresh</span></span>
* <span data-ttu-id="9b4ba-210">Corretto: la generazione di una firma di accesso condiviso per le code e le tabelle dell'emulatore dà origine a un URL non valido</span><span class="sxs-lookup"><span data-stu-id="9b4ba-210">Fixed: generating a SAS for emulator queues and tables would result in an invalid URL</span></span>
* <span data-ttu-id="9b4ba-211">Corretto: gli account di archiviazione premium possono ora essere espansi mentre è abilitato un proxy</span><span class="sxs-lookup"><span data-stu-id="9b4ba-211">Fixed: premium storage accounts can now be expanded while a proxy is enabled</span></span>
* <span data-ttu-id="9b4ba-212">Problema risolto: hello pulsante Applica per gli account di hello pagina di gestione non funziona se si dispone di 0 o 1 account selezionati</span><span class="sxs-lookup"><span data-stu-id="9b4ba-212">Fixed: hello apply button on hello accounts management page would not work if you had 1 or 0 accounts selected</span></span>
* <span data-ttu-id="9b4ba-213">Corretto: il caricamento di BLOB che richiedono le risoluzioni di conflitti potrebbe non andare a buon termine - corretto in 0.8.11</span><span class="sxs-lookup"><span data-stu-id="9b4ba-213">Fixed: uploading blobs that require conflict resolutions may fail - fixed in 0.8.11</span></span> 
* <span data-ttu-id="9b4ba-214">Corretto: l'invio di commenti e suggerimenti veniva interrotto nella versione 0.8.11 - corretto in 0.8.12</span><span class="sxs-lookup"><span data-stu-id="9b4ba-214">Fixed: sending feedback was broken in 0.8.11 - fixed in 0.8.12</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="9b4ba-215">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="9b4ba-215">Known Issues</span></span>

* <span data-ttu-id="9b4ba-216">Dopo l'aggiornamento too0.8.10, sarà necessario toorefresh tutte le credenziali.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-216">After upgrading too0.8.10, you will need toorefresh all of your credentials.</span></span>
* <span data-ttu-id="9b4ba-217">Mentre è stato eseguito lo zoom avanti o indietro, il livello di zoom hello può reimpostare momentaneamente livello predefinito toohello.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-217">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="9b4ba-218">Più di 3 gruppi di BLOB o i file di caricamento in hello stesso tempo può causare errori.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-218">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>
* <span data-ttu-id="9b4ba-219">impostazioni del Pannello di Hello account potrebbero mostrare che sono necessarie le credenziali di tooreenter nelle sottoscrizioni toofilter ordine.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-219">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions.</span></span>
* <span data-ttu-id="9b4ba-220">La ridenominazione di BLOB singoli o all'interno di un contenitore BLOB rinominato non mantiene gli snapshot.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-220">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="9b4ba-221">Tutte le altre proprietà e i metadati di BLOB, file ed entità vengono conservati durante un'operazione di ridenominazione.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-221">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="9b4ba-222">Sebbene Azure Stack attualmente non supporta le condivisioni file, viene comunque visualizzato un nodo delle condivisioni di file in un account di archiviazione di Azure Stack associato.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-222">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="9b4ba-223">Di seguito sono Ubuntu 14.04 esigenze di installare le versioni o aggiornare – tooupgrade passaggi:</span><span class="sxs-lookup"><span data-stu-id="9b4ba-223">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a><span data-ttu-id="9b4ba-224">Versione 0.8.9/0.8.8</span><span class="sxs-lookup"><span data-stu-id="9b4ba-224">Version 0.8.9 / 0.8.8</span></span>
<span data-ttu-id="9b4ba-225">23/02/2017</span><span class="sxs-lookup"><span data-stu-id="9b4ba-225">02/23/2017</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="9b4ba-226">Nuovo</span><span class="sxs-lookup"><span data-stu-id="9b4ba-226">New</span></span>

* <span data-ttu-id="9b4ba-227">Esplora archivi 0.8.9 scaricherà automaticamente una versione più recente di hello per gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-227">Storage Explorer 0.8.9 will automatically download hello latest version for updates.</span></span>
* <span data-ttu-id="9b4ba-228">Hotfix: tramite un portale generato tooattach URI SAS che un account di archiviazione comporta un errore.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-228">Hotfix: using a portal generated SAS URI tooattach a storage account would result in an error.</span></span>
* <span data-ttu-id="9b4ba-229">È ora possibile creare, gestire e alzare di livello degli snapshot di BLOB.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-229">You can now create, manage, and promote blob snapshots.</span></span>
* <span data-ttu-id="9b4ba-230">È ora possibile accedere tooAzure Cina, Germania Azure e Azure del governo account.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-230">You can now sign in tooAzure China, Azure Germany, and Azure US Government accounts.</span></span>
* <span data-ttu-id="9b4ba-231">È ora possibile modificare il livello di zoom hello.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-231">You can now change hello zoom level.</span></span> <span data-ttu-id="9b4ba-232">Utilizzare opzioni hello tooZoom menu Visualizza di hello In, Zoom indietro e reimposta Zoom.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-232">Use hello options in hello View menu tooZoom In, Zoom Out, and Reset Zoom.</span></span>
* <span data-ttu-id="9b4ba-233">I caratteri Unicode sono ora supportati nei metadati dell'utente per file e BLOB.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-233">Unicode characters are now supported in user metadata for blobs and files.</span></span>
* <span data-ttu-id="9b4ba-234">Miglioramenti all'accessibilità.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-234">Accessibility improvements.</span></span>
* <span data-ttu-id="9b4ba-235">note sulla versione della versione di Hello Avanti possono essere visualizzati dalla notifica di aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-235">hello next version's release notes can be viewed from hello update notification.</span></span> <span data-ttu-id="9b4ba-236">È inoltre possibile visualizzare hello note sulla versione corrente dal menu di hello.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-236">You can also view hello current release notes from hello Help menu.</span></span>

#### <a name="fixes"></a><span data-ttu-id="9b4ba-237">Correzioni</span><span class="sxs-lookup"><span data-stu-id="9b4ba-237">Fixes</span></span>

* <span data-ttu-id="9b4ba-238">Problema risolto: il numero di versione di hello è ora visualizzato correttamente nel Pannello di controllo in Windows</span><span class="sxs-lookup"><span data-stu-id="9b4ba-238">Fixed: hello version number is now correctly displayed in Control Panel on Windows</span></span>
* <span data-ttu-id="9b4ba-239">Problema risolto: ricerca non è più limitato too50, nodi 000</span><span class="sxs-lookup"><span data-stu-id="9b4ba-239">Fixed: search is no longer limited too50,000 nodes</span></span>
* <span data-ttu-id="9b4ba-240">Problema risolto: condivisione di file di caricamento tooa ruotato per sempre se la directory di destinazione hello non esisteva</span><span class="sxs-lookup"><span data-stu-id="9b4ba-240">Fixed: upload tooa file share spun forever if hello destination directory did not already exist</span></span>
* <span data-ttu-id="9b4ba-241">Corretto: maggiore stabilità per processi di caricamento e download prolungati</span><span class="sxs-lookup"><span data-stu-id="9b4ba-241">Fixed: improved stability for long uploads and downloads</span></span>

#### <a name="known-issues"></a><span data-ttu-id="9b4ba-242">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="9b4ba-242">Known Issues</span></span>

* <span data-ttu-id="9b4ba-243">Mentre è stato eseguito lo zoom avanti o indietro, il livello di zoom hello può reimpostare momentaneamente livello predefinito toohello.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-243">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="9b4ba-244">Accesso rapido funziona solo con gli elementi basati su sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-244">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="9b4ba-245">Questa versione non supporta le risorse locali e le risorse collegate tramite chiave o token di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-245">Local resources or resources attached via key or SAS token are not supported in this release.</span></span>
* <span data-ttu-id="9b4ba-246">Accesso rapido può richiedere alcuni secondi toonavigate toohello risorsa di destinazione, a seconda di quanti di risorse.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-246">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have.</span></span>
* <span data-ttu-id="9b4ba-247">Più di 3 gruppi di BLOB o i file di caricamento in hello stesso tempo può causare errori.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-247">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>

<span data-ttu-id="9b4ba-248">16/12/2016</span><span class="sxs-lookup"><span data-stu-id="9b4ba-248">12/16/2016</span></span>
### <a name="version-087"></a><span data-ttu-id="9b4ba-249">Versione 0.8.7</span><span class="sxs-lookup"><span data-stu-id="9b4ba-249">Version 0.8.7</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="9b4ba-250">Nuovo</span><span class="sxs-lookup"><span data-stu-id="9b4ba-250">New</span></span>

* <span data-ttu-id="9b4ba-251">È possibile scegliere come conflitti tooresolve all'inizio di hello di un aggiornamento, scaricare o copiare sessione nella finestra attività hello</span><span class="sxs-lookup"><span data-stu-id="9b4ba-251">You can choose how tooresolve conflicts at hello beginning of an update, download or copy session in hello Activities window</span></span>
* <span data-ttu-id="9b4ba-252">Passare il mouse su un percorso completo di hello toosee scheda della risorsa di archiviazione hello</span><span class="sxs-lookup"><span data-stu-id="9b4ba-252">Hover over a tab toosee hello full path of hello storage resource</span></span>
* <span data-ttu-id="9b4ba-253">Quando si fa clic su una scheda, sincronizzazione con la posizione nel riquadro di spostamento sinistra hello</span><span class="sxs-lookup"><span data-stu-id="9b4ba-253">When you click on a tab, it synchronizes with its location in hello left side navigation pane</span></span>

#### <a name="fixes"></a><span data-ttu-id="9b4ba-254">Correzioni</span><span class="sxs-lookup"><span data-stu-id="9b4ba-254">Fixes</span></span>

* <span data-ttu-id="9b4ba-255">Corretto: Storage Explorer è ora un'app attendibile su Mac</span><span class="sxs-lookup"><span data-stu-id="9b4ba-255">Fixed: Storage Explorer is now a trusted app on Mac</span></span>
* <span data-ttu-id="9b4ba-256">Corretto: Ubuntu 14.04 è supportato nuovamente</span><span class="sxs-lookup"><span data-stu-id="9b4ba-256">Fixed: Ubuntu 14.04 is again supported</span></span>
* <span data-ttu-id="9b4ba-257">Problema risolto: Talvolta hello aggiungere l'account dell'interfaccia utente lampeggia quando il caricamento delle sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="9b4ba-257">Fixed: Sometimes hello add account UI flashes when loading subscriptions</span></span>
* <span data-ttu-id="9b4ba-258">Problema risolto: Talvolta non tutte le risorse di archiviazione sono state elencate nel riquadro di spostamento sinistra hello</span><span class="sxs-lookup"><span data-stu-id="9b4ba-258">Fixed: Sometimes not all storage resources were listed in hello left side navigation pane</span></span>
* <span data-ttu-id="9b4ba-259">Problema risolto: hello azione talvolta visualizzato il riquadro azioni vuote</span><span class="sxs-lookup"><span data-stu-id="9b4ba-259">Fixed: hello action pane sometimes displayed empty actions</span></span>
* <span data-ttu-id="9b4ba-260">Problema risolto: dimensioni della finestra hello dalla sessione chiusa l'ultima volta hello ora mantenute</span><span class="sxs-lookup"><span data-stu-id="9b4ba-260">Fixed: hello window size from hello last closed session is now retained</span></span>
* <span data-ttu-id="9b4ba-261">Problema risolto: È possibile aprire più schede per hello stessa risorsa utilizzando il menu di scelta rapida hello</span><span class="sxs-lookup"><span data-stu-id="9b4ba-261">Fixed: You can open multiple tabs for hello same resource using hello context menu</span></span>

#### <a name="known-issues"></a><span data-ttu-id="9b4ba-262">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="9b4ba-262">Known Issues</span></span>

* <span data-ttu-id="9b4ba-263">Accesso rapido funziona solo con gli elementi basati su sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-263">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="9b4ba-264">Questa versione non supporta le risorse locali e le risorse collegate tramite chiave o token di firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="9b4ba-264">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="9b4ba-265">Accesso rapido può richiedere alcuni secondi toonavigate toohello risorsa di destinazione, a seconda di quanti di risorse</span><span class="sxs-lookup"><span data-stu-id="9b4ba-265">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="9b4ba-266">Più di 3 gruppi di BLOB o i file di caricamento in hello stesso tempo può causare errori</span><span class="sxs-lookup"><span data-stu-id="9b4ba-266">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="9b4ba-267">È possibile eseguire la ricerca in un massimo di 50.000 nodi circa. Se si supera tale limite, le prestazioni potrebbero risultare peggiorate o potrebbero essere generate eccezioni non gestite</span><span class="sxs-lookup"><span data-stu-id="9b4ba-267">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>
* <span data-ttu-id="9b4ba-268">Per hello primo accesso tramite Esplora archivi hello in macOS, si potrebbero notare più prompt chiede portachiavi tooaccess di autorizzazione dell'utente.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-268">For hello first time using hello Storage Explorer on macOS, you might see multiple prompts asking for user's permission tooaccess keychain.</span></span> <span data-ttu-id="9b4ba-269">È consigliabile che selezionare Consenti sempre in modo non verranno visualizzati prompt hello nuovamente</span><span class="sxs-lookup"><span data-stu-id="9b4ba-269">We suggest you select Always Allow so hello prompt won't show up again</span></span>

<span data-ttu-id="9b4ba-270">18/11/2016</span><span class="sxs-lookup"><span data-stu-id="9b4ba-270">11/18/2016</span></span>
### <a name="version-086"></a><span data-ttu-id="9b4ba-271">Versione 0.8.6</span><span class="sxs-lookup"><span data-stu-id="9b4ba-271">Version 0.8.6</span></span>

#### <a name="new"></a><span data-ttu-id="9b4ba-272">Nuovo</span><span class="sxs-lookup"><span data-stu-id="9b4ba-272">New</span></span>

* <span data-ttu-id="9b4ba-273">È possibile ora pin utilizzati più frequentemente servizi toohello accesso rapido per semplificare la navigazione</span><span class="sxs-lookup"><span data-stu-id="9b4ba-273">You can now pin most frequently used services toohello Quick Access for easy navigation</span></span>
* <span data-ttu-id="9b4ba-274">Possibilità di aprire più editor in schede diverse.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-274">You can now open multiple editors in different tabs.</span></span> <span data-ttu-id="9b4ba-275">A singolo clic tooopen una scheda temporanea. Fare doppio clic su una scheda permanente tooopen. È possibile anche fare clic su toomake scheda temporaneo hello è una scheda permanente</span><span class="sxs-lookup"><span data-stu-id="9b4ba-275">Single click tooopen a temporary tab; double click tooopen a permanent tab. You can also click on hello temporary tab toomake it a permanent tab</span></span>
* <span data-ttu-id="9b4ba-276">Sono stati apportati miglioramenti evidenti a prestazioni e stabilità per operazioni di caricamento e download, soprattutto per file di grandi dimensioni in computer veloci</span><span class="sxs-lookup"><span data-stu-id="9b4ba-276">We have made noticeable performance and stability improvements for uploads and downloads, especially for large files on fast machines</span></span>
* <span data-ttu-id="9b4ba-277">Possibilità di creare cartelle vuote "virtuali" in contenitori BLOB</span><span class="sxs-lookup"><span data-stu-id="9b4ba-277">Empty "virtual" folders can now be created in blob containers</span></span>
* <span data-ttu-id="9b4ba-278">È stato reintrodotto l'ambito di ricerca con la nuova ricerca avanzata con sottostringa, pertanto ora vi sono due opzioni di ricerca:</span><span class="sxs-lookup"><span data-stu-id="9b4ba-278">We have re-introduced scoped search with our new enhanced substring search, so you now have two options for searching:</span></span> 
    * <span data-ttu-id="9b4ba-279">Globale ricerca - immettere solo un termine di ricerca nella casella di ricerca testo hello</span><span class="sxs-lookup"><span data-stu-id="9b4ba-279">Global search - just enter a search term into hello search textbox</span></span>
    * <span data-ttu-id="9b4ba-280">La ricerca con ambita, fare clic su hello lente di ingrandimento icona tooa nodo successivo, quindi aggiungere un fine toohello termine di ricerca del percorso di hello, o fare doppio clic su e selezionare "ricerca da"</span><span class="sxs-lookup"><span data-stu-id="9b4ba-280">Scoped search - click hello magnifying glass icon next tooa node, then add a search term toohello end of hello path, or right-click and select "Search from Here"</span></span>
* <span data-ttu-id="9b4ba-281">Sono stati aggiunti vari temi: Chiaro (impostazione predefinita), Scuro, Nero a contrasto elevato e Bianco a contrasto elevato.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-281">We have added various themes: Light (default), Dark, High Contrast Black, and High Contrast White.</span></span> <span data-ttu-id="9b4ba-282">Passare tooEdit -&gt; toochange temi le preferenze di temi</span><span class="sxs-lookup"><span data-stu-id="9b4ba-282">Go tooEdit -&gt; Themes toochange your theming preference</span></span>
* <span data-ttu-id="9b4ba-283">È possibile modificare le proprietà di BLOB e file</span><span class="sxs-lookup"><span data-stu-id="9b4ba-283">You can modify Blob and file properties</span></span>
* <span data-ttu-id="9b4ba-284">Sono ora supportati i messaggi in coda codificati (base64) e non codificati</span><span class="sxs-lookup"><span data-stu-id="9b4ba-284">We now support encoded (base64) and unencoded queue messages</span></span>
* <span data-ttu-id="9b4ba-285">In Linux è ora necessario un sistema operativo a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-285">On Linux, a 64-bit OS is now required.</span></span> <span data-ttu-id="9b4ba-286">Per questa versione è supportato solo Ubuntu 16.04.1 LTS a 64 bit</span><span class="sxs-lookup"><span data-stu-id="9b4ba-286">For this release we only support 64-bit Ubuntu 16.04.1 LTS</span></span>
* <span data-ttu-id="9b4ba-287">È stato aggiornato il logo</span><span class="sxs-lookup"><span data-stu-id="9b4ba-287">We have updated our logo!</span></span>

#### <a name="fixes"></a><span data-ttu-id="9b4ba-288">Correzioni</span><span class="sxs-lookup"><span data-stu-id="9b4ba-288">Fixes</span></span>

* <span data-ttu-id="9b4ba-289">Corretto: problemi di blocco della schermata</span><span class="sxs-lookup"><span data-stu-id="9b4ba-289">Fixed: Screen freezing problems</span></span>
* <span data-ttu-id="9b4ba-290">Corretto: sicurezza avanzata</span><span class="sxs-lookup"><span data-stu-id="9b4ba-290">Fixed: Enhanced security</span></span>
* <span data-ttu-id="9b4ba-291">Corretto: a volte venivano visualizzati account collegati doppi</span><span class="sxs-lookup"><span data-stu-id="9b4ba-291">Fixed: Sometimes duplicate attached accounts could appear</span></span>
* <span data-ttu-id="9b4ba-292">Corretto: un blob con un tipo di contenuto non definito poteva generare un'eccezione</span><span class="sxs-lookup"><span data-stu-id="9b4ba-292">Fixed: A blob with an undefined content type could generate an exception</span></span>
* <span data-ttu-id="9b4ba-293">Problema risolto: Hello apertura pannello della Query in una tabella vuota non è stato possibile</span><span class="sxs-lookup"><span data-stu-id="9b4ba-293">Fixed: Opening hello Query Panel on an empty table was not possible</span></span>
* <span data-ttu-id="9b4ba-294">Corretto: bug delle variabili in Cerca</span><span class="sxs-lookup"><span data-stu-id="9b4ba-294">Fixed: Varies bugs in Search</span></span>
* <span data-ttu-id="9b4ba-295">Problema risolto: Aumentato il numero di hello delle risorse caricate dal 50 too100 quando facendo clic su "Più carico"</span><span class="sxs-lookup"><span data-stu-id="9b4ba-295">Fixed: Increased hello number of resources loaded from 50 too100 when clicking "Load More"</span></span>
* <span data-ttu-id="9b4ba-296">Corretto: alla prima esecuzione, se si è effettuato l'accesso a un account, vengono ora selezionate tutte le sottoscrizioni per tale account per impostazione predefinita</span><span class="sxs-lookup"><span data-stu-id="9b4ba-296">Fixed: On first run, if an account is signed into, we now select all subscriptions for that account by default</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="9b4ba-297">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="9b4ba-297">Known Issues</span></span>

* <span data-ttu-id="9b4ba-298">Questa versione di hello Esplora archivi non vengono eseguite Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="9b4ba-298">This release of hello Storage Explorer does not run on Ubuntu 14.04</span></span>
* <span data-ttu-id="9b4ba-299">tooopen più schede per la stessa risorsa, non sempre si fare clic su hello hello stessa risorsa.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-299">tooopen multiple tabs for hello same resource, do not continuously click on hello same resource.</span></span> <span data-ttu-id="9b4ba-300">Fare clic su un'altra risorsa e quindi tornare indietro e quindi fare clic su tooopen risorsa originale hello nuovo in un'altra scheda</span><span class="sxs-lookup"><span data-stu-id="9b4ba-300">Click on another resource and then go back and then click on hello original resource tooopen it again in another tab</span></span> 
* <span data-ttu-id="9b4ba-301">Accesso rapido funziona solo con gli elementi basati su sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-301">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="9b4ba-302">Questa versione non supporta le risorse locali e le risorse collegate tramite chiave o token di firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="9b4ba-302">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="9b4ba-303">Accesso rapido può richiedere alcuni secondi toonavigate toohello risorsa di destinazione, a seconda di quanti di risorse</span><span class="sxs-lookup"><span data-stu-id="9b4ba-303">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="9b4ba-304">Più di 3 gruppi di BLOB o i file di caricamento in hello stesso tempo può causare errori</span><span class="sxs-lookup"><span data-stu-id="9b4ba-304">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="9b4ba-305">È possibile eseguire la ricerca in un massimo di 50.000 nodi circa. Se si supera tale limite, le prestazioni potrebbero risultare peggiorate o potrebbero essere generate eccezioni non gestite</span><span class="sxs-lookup"><span data-stu-id="9b4ba-305">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>

<span data-ttu-id="9b4ba-306">03/10/2016</span><span class="sxs-lookup"><span data-stu-id="9b4ba-306">10/03/2016</span></span>
### <a name="version-085"></a><span data-ttu-id="9b4ba-307">Versione 0.8.5</span><span class="sxs-lookup"><span data-stu-id="9b4ba-307">Version 0.8.5</span></span>

#### <a name="new"></a><span data-ttu-id="9b4ba-308">Nuovo</span><span class="sxs-lookup"><span data-stu-id="9b4ba-308">New</span></span>

* <span data-ttu-id="9b4ba-309">Possono ora utilizzare generato portale SAS chiavi tooattach tooStorage account e risorse</span><span class="sxs-lookup"><span data-stu-id="9b4ba-309">Can now use Portal-generated SAS keys tooattach tooStorage Accounts and resources</span></span>

#### <a name="fixes"></a><span data-ttu-id="9b4ba-310">Correzioni</span><span class="sxs-lookup"><span data-stu-id="9b4ba-310">Fixes</span></span>

* <span data-ttu-id="9b4ba-311">Problema risolto: race condition durante la ricerca talvolta causata toobecome nodi non espandibili</span><span class="sxs-lookup"><span data-stu-id="9b4ba-311">Fixed: race condition during search sometimes caused nodes toobecome non-expandable</span></span>
* <span data-ttu-id="9b4ba-312">Problema risolto: "Usa HTTP" non viene eseguita quando la connessione di account tooStorage con chiave e il nome dell'account</span><span class="sxs-lookup"><span data-stu-id="9b4ba-312">Fixed: "Use HTTP" doesn't work when connecting tooStorage Accounts with account name and key</span></span>
* <span data-ttu-id="9b4ba-313">Corretto: le chiavi di firma di accesso condiviso (specialmente quelle generati da portale) restituiscono un errore "barra finale"</span><span class="sxs-lookup"><span data-stu-id="9b4ba-313">Fixed: SAS keys (specially Portal-generated ones) return a "trailing slash" error</span></span>
* <span data-ttu-id="9b4ba-314">Corretto: problemi di importazione della tabella</span><span class="sxs-lookup"><span data-stu-id="9b4ba-314">Fixed: table import issues</span></span>
    * <span data-ttu-id="9b4ba-315">In alcuni casi la chiave di partizione e la chiave di riga venivano annullate</span><span class="sxs-lookup"><span data-stu-id="9b4ba-315">Sometimes partition key and row key were reversed</span></span>
    * <span data-ttu-id="9b4ba-316">Non è possibile tooread "null", le chiavi di partizione</span><span class="sxs-lookup"><span data-stu-id="9b4ba-316">Unable tooread "null" Partition Keys</span></span>

#### <a name="known-issues"></a><span data-ttu-id="9b4ba-317">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="9b4ba-317">Known Issues</span></span>

* <span data-ttu-id="9b4ba-318">È possibile eseguire la ricerca in un massimo di 50.000 nodi circa. Se si supera tale limite, le prestazioni potrebbero risultare peggiorate</span><span class="sxs-lookup"><span data-stu-id="9b4ba-318">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>
* <span data-ttu-id="9b4ba-319">Stack di Azure attualmente non supporta i file, in modo tooexpand file durante il tentativo verrà visualizzato un errore</span><span class="sxs-lookup"><span data-stu-id="9b4ba-319">Azure Stack doesn't currently support Files, so trying tooexpand Files will show an error</span></span>

<span data-ttu-id="9b4ba-320">12/09/2016</span><span class="sxs-lookup"><span data-stu-id="9b4ba-320">09/12/2016</span></span>
### <a name="version-084"></a><span data-ttu-id="9b4ba-321">Versione 0.8.4</span><span class="sxs-lookup"><span data-stu-id="9b4ba-321">Version 0.8.4</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="9b4ba-322">Nuovo</span><span class="sxs-lookup"><span data-stu-id="9b4ba-322">New</span></span>

* <span data-ttu-id="9b4ba-323">Generare gli account toostorage di collegamenti diretti, contenitori, le code, tabelle o condivisioni di file per la condivisione e di facile accesso alle risorse di tooyour - Windows e Mac OS supporta</span><span class="sxs-lookup"><span data-stu-id="9b4ba-323">Generate direct links toostorage accounts, containers, queues, tables, or file shares for sharing and easy access tooyour resources - Windows and Mac OS support</span></span>
* <span data-ttu-id="9b4ba-324">Ricerca per i contenitori blob, tabelle, code, condivisioni file o la casella di ricerca hello gli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="9b4ba-324">Search for your blob containers, tables, queues, file shares, or storage accounts from hello search box</span></span>
* <span data-ttu-id="9b4ba-325">È ora possibile raggruppare le clausole nel generatore di query di tabella hello</span><span class="sxs-lookup"><span data-stu-id="9b4ba-325">You can now group clauses in hello table query builder</span></span>
* <span data-ttu-id="9b4ba-326">Rinominare e copiare/incollare contenitori BLOB, condivisioni file, tabelle, BLOB, cartelle di BLOB, file e directory all'interno di contenitori e account collegati alla firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="9b4ba-326">Rename and copy/paste blob containers, file shares, tables, blobs, blob folders, files and directories from within SAS-attached accounts and containers</span></span>
* <span data-ttu-id="9b4ba-327">Quando vengono ridenominati e copiati contenitori BLOB e condivisioni file, proprietà e metadati vengono mantenuti</span><span class="sxs-lookup"><span data-stu-id="9b4ba-327">Renaming and copying blob containers and file shares now preserve properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="9b4ba-328">Correzioni</span><span class="sxs-lookup"><span data-stu-id="9b4ba-328">Fixes</span></span>

* <span data-ttu-id="9b4ba-329">Corretto: impossibile modificare le voci della tabella se contengono le proprietà di tipo booleano o binario</span><span class="sxs-lookup"><span data-stu-id="9b4ba-329">Fixed: cannot edit table entities if they contain boolean or binary properties</span></span>

#### <a name="known-issues"></a><span data-ttu-id="9b4ba-330">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="9b4ba-330">Known Issues</span></span>

* <span data-ttu-id="9b4ba-331">È possibile eseguire la ricerca in un massimo di 50.000 nodi circa. Se si supera tale limite, le prestazioni potrebbero risultare peggiorate</span><span class="sxs-lookup"><span data-stu-id="9b4ba-331">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>

<span data-ttu-id="9b4ba-332">03/08/2016</span><span class="sxs-lookup"><span data-stu-id="9b4ba-332">08/03/2016</span></span>
### <a name="version-083"></a><span data-ttu-id="9b4ba-333">Versione 0.8.3</span><span class="sxs-lookup"><span data-stu-id="9b4ba-333">Version 0.8.3</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="9b4ba-334">Nuovo</span><span class="sxs-lookup"><span data-stu-id="9b4ba-334">New</span></span>

* <span data-ttu-id="9b4ba-335">Ridenominazione di contenitori, tabelle e condivisioni file</span><span class="sxs-lookup"><span data-stu-id="9b4ba-335">Rename containers, tables, file shares</span></span>
* <span data-ttu-id="9b4ba-336">Migliore esperienza con il Generatore di query</span><span class="sxs-lookup"><span data-stu-id="9b4ba-336">Improved Query builder experience</span></span>
* <span data-ttu-id="9b4ba-337">Query di carico e toosave possibilità</span><span class="sxs-lookup"><span data-stu-id="9b4ba-337">Ability toosave and load queries</span></span>
* <span data-ttu-id="9b4ba-338">Gli account o contenitori, le code, tabelle di toostorage di collegamenti diretti, condivisioni file o per la condivisione e facilmente l'accesso alle risorse (solo Windows - macOS supportano sarà presto disponibile!)</span><span class="sxs-lookup"><span data-stu-id="9b4ba-338">Direct links toostorage accounts or containers, queues, tables, or file shares for sharing and easily accessing your resources (Windows-only - macOS support coming soon!)</span></span>
* <span data-ttu-id="9b4ba-339">Toomanage possibilità e configurare le regole CORS</span><span class="sxs-lookup"><span data-stu-id="9b4ba-339">Ability toomanage and configure CORS rules</span></span>

#### <a name="fixes"></a><span data-ttu-id="9b4ba-340">Correzioni</span><span class="sxs-lookup"><span data-stu-id="9b4ba-340">Fixes</span></span>

* <span data-ttu-id="9b4ba-341">Corretto: gli account di Microsoft richiedono la riautenticazione ogni 8-12 ore</span><span class="sxs-lookup"><span data-stu-id="9b4ba-341">Fixed: Microsoft Accounts require re-authentication every 8-12 hours</span></span>

#### <a name="known-issues"></a><span data-ttu-id="9b4ba-342">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="9b4ba-342">Known Issues</span></span>

* <span data-ttu-id="9b4ba-343">Talvolta hello dell'interfaccia utente potrebbe sembrare bloccata, ingrandire la finestra hello consente di risolvere il problema</span><span class="sxs-lookup"><span data-stu-id="9b4ba-343">Sometimes hello UI might appear frozen - maximizing hello window helps resolve this issue</span></span>
* <span data-ttu-id="9b4ba-344">L'installazione di macOS potrebbe richiedere autorizzazioni elevate</span><span class="sxs-lookup"><span data-stu-id="9b4ba-344">macOS install may require elevated permissions</span></span>
* <span data-ttu-id="9b4ba-345">Pannello impostazioni account potrebbe mostrare che sono necessarie le credenziali di tooreenter nelle sottoscrizioni toofilter ordine</span><span class="sxs-lookup"><span data-stu-id="9b4ba-345">Account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="9b4ba-346">Ridenominazione di condivisioni file, i contenitori di blob e tabelle non mantiene i metadati o altre proprietà nel contenitore di hello, ad esempio la quota di condivisione file, il livello di accesso pubblico o criteri di accesso</span><span class="sxs-lookup"><span data-stu-id="9b4ba-346">Renaming file shares, blob containers, and tables does not preserve metadata or other properties on hello container, such as file share quota, public access level or access policies</span></span>
* <span data-ttu-id="9b4ba-347">La ridenominazione di BLOB singoli o all'interno di un contenitore BLOB rinominato non mantiene gli snapshot.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-347">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="9b4ba-348">Tutte le altre proprietà e i metadati di BLOB, file ed entità vengono conservati durante un'operazione di ridenominazione</span><span class="sxs-lookup"><span data-stu-id="9b4ba-348">All other properties and metadata for blobs, files and entities are preserved during a rename</span></span>
* <span data-ttu-id="9b4ba-349">La copia o la ridenominazione delle risorse non funziona all'interno di account associati alla firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="9b4ba-349">Copying or renaming resources does not work within SAS-attached accounts</span></span>

<span data-ttu-id="9b4ba-350">07/07/2016</span><span class="sxs-lookup"><span data-stu-id="9b4ba-350">07/07/2016</span></span>
### <a name="version-082"></a><span data-ttu-id="9b4ba-351">Versione 0.8.2</span><span class="sxs-lookup"><span data-stu-id="9b4ba-351">Version 0.8.2</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="9b4ba-352">Nuovo</span><span class="sxs-lookup"><span data-stu-id="9b4ba-352">New</span></span>

* <span data-ttu-id="9b4ba-353">Gli account di archiviazione vengono raggruppati in sottoscrizioni. L'archiviazione e le risorse di sviluppo collegate tramite chiave o firma di accesso condiviso vengono visualizzate nel nodo (locale e collegato)</span><span class="sxs-lookup"><span data-stu-id="9b4ba-353">Storage Accounts are grouped by subscriptions; development storage and resources attached via key or SAS are shown under (Local and Attached) node</span></span>
* <span data-ttu-id="9b4ba-354">Disconnettersi dagli account nel pannello "Impostazioni account Azure"</span><span class="sxs-lookup"><span data-stu-id="9b4ba-354">Sign off from accounts in "Azure Account Settings" panel</span></span>
* <span data-ttu-id="9b4ba-355">Configurare tooenable impostazioni proxy e gestire l'accesso</span><span class="sxs-lookup"><span data-stu-id="9b4ba-355">Configure proxy settings tooenable and manage sign-in</span></span>
* <span data-ttu-id="9b4ba-356">Creare e interrompere i lease di blob</span><span class="sxs-lookup"><span data-stu-id="9b4ba-356">Create and break blob leases</span></span>
* <span data-ttu-id="9b4ba-357">Aprire contenitori BLOB, code, tabelle e i file con un unico clic</span><span class="sxs-lookup"><span data-stu-id="9b4ba-357">Open blob containers, queues, tables, and files with single-click</span></span>

#### <a name="fixes"></a><span data-ttu-id="9b4ba-358">Correzioni</span><span class="sxs-lookup"><span data-stu-id="9b4ba-358">Fixes</span></span>

* <span data-ttu-id="9b4ba-359">Corretto: i messaggi in coda con le librerie .NET o Java non vengono decodificati correttamente da base64</span><span class="sxs-lookup"><span data-stu-id="9b4ba-359">Fixed: queue messages inserted with .NET or Java libraries are not properly decoded from base64</span></span>
* <span data-ttu-id="9b4ba-360">Corretto: le tabelle $metrics non vengono visualizzate per gli account di archiviazione Blob</span><span class="sxs-lookup"><span data-stu-id="9b4ba-360">Fixed: $metrics tables are not shown for Blob Storage accounts</span></span>
* <span data-ttu-id="9b4ba-361">Corretto: il nodo delle tabelle non funziona per l'archiviazione locale (sviluppo)</span><span class="sxs-lookup"><span data-stu-id="9b4ba-361">Fixed: tables node does not work for local (Development) storage</span></span>

#### <a name="known-issues"></a><span data-ttu-id="9b4ba-362">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="9b4ba-362">Known Issues</span></span>

* <span data-ttu-id="9b4ba-363">L'installazione di macOS potrebbe richiedere autorizzazioni elevate</span><span class="sxs-lookup"><span data-stu-id="9b4ba-363">macOS install may require elevated permissions</span></span>

<span data-ttu-id="9b4ba-364">15/06/2016</span><span class="sxs-lookup"><span data-stu-id="9b4ba-364">06/15/2016</span></span>
### <a name="version-080"></a><span data-ttu-id="9b4ba-365">Versione 0.8.0</span><span class="sxs-lookup"><span data-stu-id="9b4ba-365">Version 0.8.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="9b4ba-366">Nuovo</span><span class="sxs-lookup"><span data-stu-id="9b4ba-366">New</span></span>

* <span data-ttu-id="9b4ba-367">Supporto per condivisione file: visualizzazione, caricamento, download, copia di file e directory, URI della firma di accesso condiviso (creazione e la connessione)</span><span class="sxs-lookup"><span data-stu-id="9b4ba-367">File share support: viewing, uploading, downloading, copying files and directories, SAS URIs (create and connect)</span></span>
* <span data-ttu-id="9b4ba-368">Esperienza utente migliorata per la connessione tooStorage con URI SAS o le chiavi dell'account</span><span class="sxs-lookup"><span data-stu-id="9b4ba-368">Improved user experience for connecting tooStorage with SAS URIs or account keys</span></span>
* <span data-ttu-id="9b4ba-369">Risultati della query relativa alla tabella di esportazione</span><span class="sxs-lookup"><span data-stu-id="9b4ba-369">Export table query results</span></span>
* <span data-ttu-id="9b4ba-370">Riordinamento e personalizzazione delle colonne della tabella</span><span class="sxs-lookup"><span data-stu-id="9b4ba-370">Table column reordering and customization</span></span>
* <span data-ttu-id="9b4ba-371">Visualizzazione dei contenitori BLOB $logs e delle tabelle $metrics per gli account di archiviazione con le metriche abilitate</span><span class="sxs-lookup"><span data-stu-id="9b4ba-371">Viewing $logs blob containers and $metrics tables for Storage Accounts with enabled metrics</span></span>
* <span data-ttu-id="9b4ba-372">Comportamento di esportazione e importazione migliorato, include ora il tipo di valore della proprietà</span><span class="sxs-lookup"><span data-stu-id="9b4ba-372">Improved export and import behavior, now includes property value type</span></span>

#### <a name="fixes"></a><span data-ttu-id="9b4ba-373">Correzioni</span><span class="sxs-lookup"><span data-stu-id="9b4ba-373">Fixes</span></span>

* <span data-ttu-id="9b4ba-374">Corretto: il caricamento o il download di BLOB di grandi dimensioni può essere incompleto</span><span class="sxs-lookup"><span data-stu-id="9b4ba-374">Fixed: uploading or downloading large blobs can result in incomplete uploads/downloads</span></span>
* <span data-ttu-id="9b4ba-375">Problema risolto: la modifica, aggiunta o l'importazione di un'entità con un valore numerico ("1") verrà convertito toodouble</span><span class="sxs-lookup"><span data-stu-id="9b4ba-375">Fixed: editing, adding, or importing an entity with a numeric string value ("1") will convert it toodouble</span></span>
* <span data-ttu-id="9b4ba-376">Problema risolto: Nodo della tabella hello tooexpand Impossibile nell'ambiente di sviluppo locale hello</span><span class="sxs-lookup"><span data-stu-id="9b4ba-376">Fixed: Unable tooexpand hello table node in hello local development environment</span></span>

#### <a name="known-issues"></a><span data-ttu-id="9b4ba-377">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="9b4ba-377">Known Issues</span></span>

* <span data-ttu-id="9b4ba-378">L tabelle $metrics non sono visibili per gli account di archiviazione Blob</span><span class="sxs-lookup"><span data-stu-id="9b4ba-378">$metrics tables are not visible for Blob Storage accounts</span></span>
* <span data-ttu-id="9b4ba-379">Coda di messaggi a livello di programmazione può non essere visualizzata correttamente messaggi hello vengono codificati utilizzando la codifica Base64</span><span class="sxs-lookup"><span data-stu-id="9b4ba-379">Queue messages added programmatically may not be displayed correctly if hello messages are encoded using Base64 encoding</span></span>

<span data-ttu-id="9b4ba-380">17/05/2016</span><span class="sxs-lookup"><span data-stu-id="9b4ba-380">05/17/2016</span></span>
### <a name="version-07201605090"></a><span data-ttu-id="9b4ba-381">Versione 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="9b4ba-381">Version 0.7.20160509.0</span></span>

#### <a name="new"></a><span data-ttu-id="9b4ba-382">Nuovo</span><span class="sxs-lookup"><span data-stu-id="9b4ba-382">New</span></span>

* <span data-ttu-id="9b4ba-383">Migliore gestione degli errori per i crash dell'app</span><span class="sxs-lookup"><span data-stu-id="9b4ba-383">Better error handling for app crashes</span></span>

#### <a name="fixes"></a><span data-ttu-id="9b4ba-384">Correzioni</span><span class="sxs-lookup"><span data-stu-id="9b4ba-384">Fixes</span></span>

* <span data-ttu-id="9b4ba-385">Correzione del bug per cui i messaggi sulla barra delle informazioni talvolta non vengono visualizzati quando sono necessarie credenziali di accesso</span><span class="sxs-lookup"><span data-stu-id="9b4ba-385">Fixed bug where InfoBar messages sometimes don't show up when sign-in credentials were required</span></span>

#### <a name="known-issues"></a><span data-ttu-id="9b4ba-386">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="9b4ba-386">Known Issues</span></span>

* <span data-ttu-id="9b4ba-387">Tabelle: Aggiunta, modifica, o l'importazione di un'entità che dispone di una proprietà con un valore numerico in modo ambiguo, ad esempio "1" o "1.0", e hello toosend tenta di utente come un `Edm.String`, il valore di hello, verrà ripristinato tramite client hello API come un EDM</span><span class="sxs-lookup"><span data-stu-id="9b4ba-387">Tables: Adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>

<span data-ttu-id="9b4ba-388">31/03/2016</span><span class="sxs-lookup"><span data-stu-id="9b4ba-388">03/31/2016</span></span>

### <a name="version-07201603250"></a><span data-ttu-id="9b4ba-389">Versione 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="9b4ba-389">Version 0.7.20160325.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="9b4ba-390">Nuovo</span><span class="sxs-lookup"><span data-stu-id="9b4ba-390">New</span></span>

* <span data-ttu-id="9b4ba-391">Supporto tabella: visualizzazione, esecuzione di query, esportazione, importazione e operazioni CRUD per le entità</span><span class="sxs-lookup"><span data-stu-id="9b4ba-391">Table support: viewing, querying, export, import, and CRUD operations for entities</span></span>
* <span data-ttu-id="9b4ba-392">Supporto coda: visualizzazione, aggiunta, rimozione dei messaggi dalla coda</span><span class="sxs-lookup"><span data-stu-id="9b4ba-392">Queue support: viewing, adding, dequeueing messages</span></span>
* <span data-ttu-id="9b4ba-393">Generazione di URI della firma di accesso condiviso per gli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="9b4ba-393">Generating SAS URIs for Storage Accounts</span></span>
* <span data-ttu-id="9b4ba-394">Connessione tooStorage account con l'URI di firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="9b4ba-394">Connecting tooStorage Accounts with SAS URIs</span></span>
* <span data-ttu-id="9b4ba-395">Aggiornare notifiche per gli aggiornamenti futuri tooStorage Explorer</span><span class="sxs-lookup"><span data-stu-id="9b4ba-395">Update notifications for future updates tooStorage Explorer</span></span>
* <span data-ttu-id="9b4ba-396">Aspetto aggiornato</span><span class="sxs-lookup"><span data-stu-id="9b4ba-396">Updated look and feel</span></span>

#### <a name="fixes"></a><span data-ttu-id="9b4ba-397">Correzioni</span><span class="sxs-lookup"><span data-stu-id="9b4ba-397">Fixes</span></span>

* <span data-ttu-id="9b4ba-398">Miglioramenti dell'affidabilità e delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="9b4ba-398">Performance and reliability improvements</span></span>

### <a name="known-issues-amp-mitigations"></a><span data-ttu-id="9b4ba-399">Problemi noti &amp; Prevenzione</span><span class="sxs-lookup"><span data-stu-id="9b4ba-399">Known Issues &amp; Mitigations</span></span>

* <span data-ttu-id="9b4ba-400">Il download di file BLOB di grandi dimensioni non funziona correttamente. È consigliabile usare AzCopy fino alla risoluzione del problema</span><span class="sxs-lookup"><span data-stu-id="9b4ba-400">Download of large blob files does not work correctly - we recommend using AzCopy while we address this issue</span></span> 
* <span data-ttu-id="9b4ba-401">Le credenziali dell'account non essere recuperate o memorizzate nella cache se hello home directory non è stata trovata o non può essere scritta</span><span class="sxs-lookup"><span data-stu-id="9b4ba-401">Account credentials will not be retrieved nor cached if hello home folder cannot be found or cannot be written to</span></span>
* <span data-ttu-id="9b4ba-402">Se è in aggiunta, modifica o l'importazione di un'entità che dispone di una proprietà con un valore numerico in modo ambiguo, ad esempio "1" o "1.0", e utente hello prova toosend come un `Edm.String`, il valore di hello, verrà ripristinato tramite client hello API come un EDM</span><span class="sxs-lookup"><span data-stu-id="9b4ba-402">If we are adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>
* <span data-ttu-id="9b4ba-403">Quando si importa il file CSV con i record su più righe, hello possano ottenere abbassate o crittografati</span><span class="sxs-lookup"><span data-stu-id="9b4ba-403">When importing CSV files with multiline records, hello data may get chopped or scrambled</span></span>

<span data-ttu-id="9b4ba-404">03/02/2016</span><span class="sxs-lookup"><span data-stu-id="9b4ba-404">02/03/2016</span></span>

### <a name="version-07201601291"></a><span data-ttu-id="9b4ba-405">Versione 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="9b4ba-405">Version 0.7.20160129.1</span></span>

#### <a name="fixes"></a><span data-ttu-id="9b4ba-406">Correzioni</span><span class="sxs-lookup"><span data-stu-id="9b4ba-406">Fixes</span></span>

* <span data-ttu-id="9b4ba-407">Miglioramento delle prestazioni complessive durante il caricamento, il download e la copia di BLOB</span><span class="sxs-lookup"><span data-stu-id="9b4ba-407">Improved overall performance when uploading, downloading and copying blobs</span></span>

<span data-ttu-id="9b4ba-408">14/01/2016</span><span class="sxs-lookup"><span data-stu-id="9b4ba-408">01/14/2016</span></span>

### <a name="version-07201601050"></a><span data-ttu-id="9b4ba-409">Versione 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="9b4ba-409">Version 0.7.20160105.0</span></span>

#### <a name="new"></a><span data-ttu-id="9b4ba-410">Nuovo</span><span class="sxs-lookup"><span data-stu-id="9b4ba-410">New</span></span>

* <span data-ttu-id="9b4ba-411">Supporto Linux (tooOSX funzionalità parità)</span><span class="sxs-lookup"><span data-stu-id="9b4ba-411">Linux support (parity features tooOSX)</span></span>
* <span data-ttu-id="9b4ba-412">Aggiunta di contenitori BLOB con la chiave di firma di accesso condiviso (SAS)</span><span class="sxs-lookup"><span data-stu-id="9b4ba-412">Add blob containers with Shared Access Signatures (SAS) key</span></span>
* <span data-ttu-id="9b4ba-413">Aggiunta degli account di archiviazione per Azure China</span><span class="sxs-lookup"><span data-stu-id="9b4ba-413">Add Storage Accounts for Azure China</span></span>
* <span data-ttu-id="9b4ba-414">Aggiunta di account di archiviazione con endpoint personalizzati</span><span class="sxs-lookup"><span data-stu-id="9b4ba-414">Add Storage Accounts with custom endpoints</span></span>
* <span data-ttu-id="9b4ba-415">Aprire e visualizzare il BLOB di testo e immagine contenuto hello</span><span class="sxs-lookup"><span data-stu-id="9b4ba-415">Open and view hello contents text and picture blobs</span></span>
* <span data-ttu-id="9b4ba-416">Visualizzazione e modifica di metadati e proprietà di BLOB</span><span class="sxs-lookup"><span data-stu-id="9b4ba-416">View and edit blob properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="9b4ba-417">Correzioni</span><span class="sxs-lookup"><span data-stu-id="9b4ba-417">Fixes</span></span>

* <span data-ttu-id="9b4ba-418">Problema risolto: il caricamento o download un numero elevato di oggetti BLOB (500 +) in alcuni casi potrebbe essere hello app toohave uno schermo bianco</span><span class="sxs-lookup"><span data-stu-id="9b4ba-418">Fixed: uploading or download a large number of blobs (500+) may sometimes cause hello app toohave a white screen</span></span> 
* <span data-ttu-id="9b4ba-419">Problema risolto: quando si imposta il livello di accesso pubblico contenitore blob, hello nuovo valore non viene aggiornato finché non si imposta nuovamente lo stato attivo hello nel contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-419">Fixed: when setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container.</span></span> <span data-ttu-id="9b4ba-420">Inoltre, finestra di dialogo hello verrà sempre troppo "non accesso pubblica" e non hello corrente il valore effettivo.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-420">Also, hello dialog always defaults too"No public access", and not hello actual current value.</span></span>
* <span data-ttu-id="9b4ba-421">Miglioramenti generali della tastiera/accessibilità e del supporto interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="9b4ba-421">Better overall keyboard/accessibility and UI support</span></span>
* <span data-ttu-id="9b4ba-422">Wrapping di testo della cronologia di navigazione quando è lungo con spazio</span><span class="sxs-lookup"><span data-stu-id="9b4ba-422">Breadcrumbs history text wraps when it's long with white space</span></span>
* <span data-ttu-id="9b4ba-423">La finestra di dialogo della firma di accesso condiviso supporta la convalida dell'input</span><span class="sxs-lookup"><span data-stu-id="9b4ba-423">SAS dialog supports input validation</span></span>
* <span data-ttu-id="9b4ba-424">Archiviazione locale continua toobe disponibile anche se le credenziali utente sono scadute</span><span class="sxs-lookup"><span data-stu-id="9b4ba-424">Local storage continues toobe available even if user credentials have expired</span></span>
* <span data-ttu-id="9b4ba-425">Durante l'eliminazione di un contenitore blob aperto Esplora blob hello sul lato destro hello è chiuso</span><span class="sxs-lookup"><span data-stu-id="9b4ba-425">When an opened blob container is deleted, hello blob explorer on hello right side is closed</span></span>

#### <a name="known-issues"></a><span data-ttu-id="9b4ba-426">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="9b4ba-426">Known Issues</span></span>

* <span data-ttu-id="9b4ba-427">Di seguito sono necessità di installare Linux versione gcc o aggiornata – tooupgrade passaggi:</span><span class="sxs-lookup"><span data-stu-id="9b4ba-427">Linux install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span> 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

<span data-ttu-id="9b4ba-428">18/11/2015</span><span class="sxs-lookup"><span data-stu-id="9b4ba-428">11/18/2015</span></span>
### <a name="version-07201511160"></a><span data-ttu-id="9b4ba-429">Versione 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="9b4ba-429">Version 0.7.20151116.0</span></span>

#### <a name="new"></a><span data-ttu-id="9b4ba-430">Nuovo</span><span class="sxs-lookup"><span data-stu-id="9b4ba-430">New</span></span>

* <span data-ttu-id="9b4ba-431">Versioni per macOS e Windows</span><span class="sxs-lookup"><span data-stu-id="9b4ba-431">macOS, and Windows versions</span></span>
* <span data-ttu-id="9b4ba-432">Accedi tooview gli account di archiviazione: utilizzare l'Account aziendale, l'Account Microsoft, 2FA, e così via.</span><span class="sxs-lookup"><span data-stu-id="9b4ba-432">Sign in tooview your Storage Accounts – use your Org Account, Microsoft Account, 2FA, etc.</span></span>
* <span data-ttu-id="9b4ba-433">Archivio di sviluppo locale (usare l'emulatore di archiviazione, solo Windows)</span><span class="sxs-lookup"><span data-stu-id="9b4ba-433">Local development storage (use storage emulator, Windows-only)</span></span>
* <span data-ttu-id="9b4ba-434">Supporto di Azure Resource Manager e delle risorse Classic</span><span class="sxs-lookup"><span data-stu-id="9b4ba-434">Azure Resource Manager and Classic resource support</span></span>
* <span data-ttu-id="9b4ba-435">Creazione ed eliminazione di BLOB, code o tabelle</span><span class="sxs-lookup"><span data-stu-id="9b4ba-435">Create and delete blobs, queues, or tables</span></span>
* <span data-ttu-id="9b4ba-436">Ricerca di BLOB, code o tabelle specifiche</span><span class="sxs-lookup"><span data-stu-id="9b4ba-436">Search for specific blobs, queues, or tables</span></span>
* <span data-ttu-id="9b4ba-437">Esplorare il contenuto di hello di contenitori di blob</span><span class="sxs-lookup"><span data-stu-id="9b4ba-437">Explore hello contents of blob containers</span></span>
* <span data-ttu-id="9b4ba-438">Visualizzazione e spostamento tra directory</span><span class="sxs-lookup"><span data-stu-id="9b4ba-438">View and navigate through directories</span></span>
* <span data-ttu-id="9b4ba-439">Caricamento, download ed eliminazione di BLOB e cartelle</span><span class="sxs-lookup"><span data-stu-id="9b4ba-439">Upload, download, and delete blobs and folders</span></span>
* <span data-ttu-id="9b4ba-440">Visualizzazione e modifica di metadati e proprietà di BLOB</span><span class="sxs-lookup"><span data-stu-id="9b4ba-440">View and edit blob properties and metadata</span></span>
* <span data-ttu-id="9b4ba-441">Generazione di chiavi di firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="9b4ba-441">Generate SAS keys</span></span>
* <span data-ttu-id="9b4ba-442">Gestione e creazione di SAP (Stored Access Policies)</span><span class="sxs-lookup"><span data-stu-id="9b4ba-442">Manage and create Stored Access Policies (SAP)</span></span>
* <span data-ttu-id="9b4ba-443">Ricerca di BLOB in base al prefisso</span><span class="sxs-lookup"><span data-stu-id="9b4ba-443">Search for blobs by prefix</span></span>
* <span data-ttu-id="9b4ba-444">Trascinare ' n' rilascio tooupload file o download</span><span class="sxs-lookup"><span data-stu-id="9b4ba-444">Drag 'n drop files tooupload or download</span></span>

#### <a name="known-issues"></a><span data-ttu-id="9b4ba-445">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="9b4ba-445">Known Issues</span></span>

* <span data-ttu-id="9b4ba-446">Quando si imposta il livello di accesso pubblico contenitore blob, nuovo valore hello non è aggiornato finché non si imposta nuovamente lo stato attivo hello nel contenitore hello</span><span class="sxs-lookup"><span data-stu-id="9b4ba-446">When setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container</span></span>
* <span data-ttu-id="9b4ba-447">Quando si apre a livello di accesso pubblico hello tooset hello finestra di dialogo, non viene sempre "Nessun accesso pubblico" come valore predefinito di hello e non hello effettivo valore corrente</span><span class="sxs-lookup"><span data-stu-id="9b4ba-447">When you open hello dialog tooset hello public access level, it always shows "No public access" as hello default, and not hello actual current value</span></span>
* <span data-ttu-id="9b4ba-448">Impossibile rinominare i BLOB scaricati</span><span class="sxs-lookup"><span data-stu-id="9b4ba-448">Cannot rename downloaded blobs</span></span>
* <span data-ttu-id="9b4ba-449">Le voci di log attività rimane talvolta "bloccato" in corso un stato quando si verifica un errore e non viene visualizzato errore hello</span><span class="sxs-lookup"><span data-stu-id="9b4ba-449">Activity log entries will sometimes get "stuck" in an in progress state when an error occurs, and hello error is not displayed</span></span>
* <span data-ttu-id="9b4ba-450">Talvolta gli arresti anomali attiva completamente bianco durante il tentativo di tooupload o scarica un numero elevato di BLOB</span><span class="sxs-lookup"><span data-stu-id="9b4ba-450">Sometimes crashes or turns completely white when trying tooupload or download a large number of blobs</span></span>
* <span data-ttu-id="9b4ba-451">In alcuni casi l'annullamento di un'operazione di copia non funziona</span><span class="sxs-lookup"><span data-stu-id="9b4ba-451">Sometimes canceling a copy operation does not work</span></span>
* <span data-ttu-id="9b4ba-452">Durante la creazione di un contenitore (coda/blob o tabella), se è un nome non valido di input e procedere toocreate un altro in un tipo di contenitore diverso non è possibile impostare lo stato attivo sul nuovo tipo di hello</span><span class="sxs-lookup"><span data-stu-id="9b4ba-452">During creating a container (blob/queue/table), if you input an invalid name and proceed toocreate another under a different container type you cannot set focus on hello new type</span></span>
* <span data-ttu-id="9b4ba-453">Impossibile creare una nuova cartella o rinominare una cartella</span><span class="sxs-lookup"><span data-stu-id="9b4ba-453">Can't create new folder or rename folder</span></span>




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md