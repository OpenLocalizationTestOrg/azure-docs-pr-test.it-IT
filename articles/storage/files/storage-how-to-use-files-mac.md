---
title: condivisione di File di Azure aaaMount su SMB con macOS | Documenti Microsoft
description: Informazioni su come condividere un File di Azure toomount su SMB con macOS.
services: storage
documentationcenter: 
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
ms.openlocfilehash: 71aaec8a77b770fe147b783c0ab9f86830176bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="780de-103">Montare una condivisione file di Azure tramite SMB con macOS</span><span class="sxs-lookup"><span data-stu-id="780de-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="780de-104">[Archiviazione di Azure File](../storage-dotnet-how-to-use-files.md) il servizio che consente di toocreate e utilizzare condivisioni di file di rete in hello Azure utilizza standard di settore hello.</span><span class="sxs-lookup"><span data-stu-id="780de-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you toocreate and use network file shares in hello Azure using hello industry standard.</span></span> <span data-ttu-id="780de-105">Le condivisioni file di Azure possono essere montate in macOS Sierra (10.12) ed El Capitan (10.11).</span><span class="sxs-lookup"><span data-stu-id="780de-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="780de-106">Questo articolo illustra due modi diversi toomount una condivisione di File di Azure in macOS con hello dell'interfaccia utente di ricerca e l'utilizzo di hello Terminal.</span><span class="sxs-lookup"><span data-stu-id="780de-106">This article shows two different ways toomount an Azure File share on macOS with hello Finder UI and using hello Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="780de-107">Prima di montare una condivisione file di Azure tramite SMB, è consigliabile disabilitare la firma dei pacchetti SMB.</span><span class="sxs-lookup"><span data-stu-id="780de-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="780de-108">Operazione non può produrre un peggioramento delle prestazioni quando si accede a una condivisione hello Azure da macOS.</span><span class="sxs-lookup"><span data-stu-id="780de-108">Not doing so may yield poor performance when accessing hello Azure File share from macOS.</span></span> <span data-ttu-id="780de-109">La connessione SMB verrà crittografata, pertanto non influisce sulla protezione hello della connessione.</span><span class="sxs-lookup"><span data-stu-id="780de-109">Your SMB connection will be encrypted, so this does not affect hello security of your connection.</span></span> <span data-ttu-id="780de-110">Da hello terminal, hello seguenti comandi disabiliterà la firma dei pacchetti SMB, come descritto da questa [articolo del supporto tecnico Apple sulla disabilitazione di firma dei pacchetti SMB](https://support.apple.com/HT205926):</span><span class="sxs-lookup"><span data-stu-id="780de-110">From hello terminal, hello following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="780de-111">Prerequisiti per il montaggio di una condivisione file di Azure in macOS</span><span class="sxs-lookup"><span data-stu-id="780de-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="780de-112">**Nome account di archiviazione**: condividere un File di Azure toomount, si sarà necessario hello nome dell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="780de-112">**Storage account name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="780de-113">**Chiave dell'account di archiviazione**: condividere un File di Azure toomount, si sarà necessario hello chiave di archiviazione primaria (o secondario).</span><span class="sxs-lookup"><span data-stu-id="780de-113">**Storage account key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="780de-114">Le chiavi di firma di accesso condiviso non sono attualmente supportate per il montaggio.</span><span class="sxs-lookup"><span data-stu-id="780de-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="780de-115">**Assicurarsi che la porta 445 sia aperta**: SMB comunica tramite la porta TCP 445.</span><span class="sxs-lookup"><span data-stu-id="780de-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="780de-116">Nel computer client (Buongiorno Mac), verificare che il firewall non blocchi la porta TCP 445 toomake.</span><span class="sxs-lookup"><span data-stu-id="780de-116">On your client machine (hello Mac), check toomake sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="780de-117">Montare una condivisione file di Azure tramite il Finder</span><span class="sxs-lookup"><span data-stu-id="780de-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="780de-118">**Aprire il Finder**: Finder è aperto in macOS per impostazione predefinita, ma è possibile assicurarsi sia hello attualmente selezionato applicazione facendo clic sul pulsante hello "macOS faccia icona" nella finestra di ancoraggio hello:</span><span class="sxs-lookup"><span data-stu-id="780de-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is hello currently selected application by clicking hello "macOS face icon" on hello dock:</span></span>  
    <span data-ttu-id="780de-119">![icona di affrontare macOS Hello](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="780de-119">![hello macOS face icon](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="780de-120">**Selezionare "Connect tooServer" hello "Go" Menu**: il percorso UNC hello da hello [prerequisiti](#preq), convertire hello inizio doppia barra rovesciata (`\\`) troppo`smb://` e tutte le altre barre rovesciate (`\`) barre di tooforwards (`/`).</span><span class="sxs-lookup"><span data-stu-id="780de-120">**Select "Connect tooServer" from hello "Go" Menu**: Using hello UNC path from hello [prerequisites](#preq), convert hello beginning double backslash (`\\`) too`smb://` and all other backslashes (`\`) tooforwards slashes (`/`).</span></span> <span data-ttu-id="780de-121">Il collegamento dovrebbe essere simile hello seguente: ![finestra di dialogo "Connect tooServer" hello](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="780de-121">Your link should look like hello following: ![hello "Connect tooServer" dialog](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="780de-122">**Utilizzare hello condivisione nome e l'archiviazione chiave dell'account quando viene richiesto un nome utente e password**: quando si fa clic su "Connetti" nella finestra di dialogo "Connect tooServer" hello, verrà richiesto di hello username e password (sarà autopopulated con il macOS nome utente).</span><span class="sxs-lookup"><span data-stu-id="780de-122">**Use hello share name and storage account key when prompted for a username and password**: When you click "Connect" on hello "Connect tooServer" dialog, you will be prompted for hello username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="780de-123">È possibile hello inserimento chiave dell'account di archiviazione di nome/condivisione hello nel portachiavi di Mac OS.</span><span class="sxs-lookup"><span data-stu-id="780de-123">You have hello option of placing hello share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="780de-124">**Condivisione di File di Azure usare hello in base alle esigenze**: dopo la sostituzione di hello condivisione nome e l'archiviazione chiave dell'account in utente hello e la password, verrà montato condivisione hello.</span><span class="sxs-lookup"><span data-stu-id="780de-124">**Use hello Azure File share as desired**: After substituting hello share name and storage account key in for hello username and password, hello share will be mounted.</span></span> <span data-ttu-id="780de-125">È possibile utilizzare questo in genere si utilizza una condivisione di file/cartella locale, tra cui trascinando e rilasciando i file nella condivisione di file hello:</span><span class="sxs-lookup"><span data-stu-id="780de-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into hello file share:</span></span>

    ![Snapshot di una condivisione file di Azure montata](./media/storage-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="780de-127">Montare una condivisione file di Azure tramite il terminale</span><span class="sxs-lookup"><span data-stu-id="780de-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="780de-128">Sostituire `<storage-account-name>` con nome hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="780de-128">Replace `<storage-account-name>` with hello name of your storage account.</span></span> <span data-ttu-id="780de-129">Specificare la chiave dell'account di archiviazione come password quando viene chiesta.</span><span class="sxs-lookup"><span data-stu-id="780de-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="780de-130">**Condivisione di File di Azure usare hello in base alle esigenze**: condivisione di File di Azure hello verrà montata il punto di montaggio hello specificato dal comando precedente hello.</span><span class="sxs-lookup"><span data-stu-id="780de-130">**Use hello Azure File share as desired**: hello Azure File share will be mounted at hello mount point specified by hello previous command.</span></span>  

    ![Uno snapshot della condivisione di File di Azure hello montato](./media/storage-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="780de-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="780de-132">Next steps</span></span>
<span data-ttu-id="780de-133">Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="780de-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="780de-134">Articolo del supporto tecnico Apple - come tooconnect con la condivisione File su Mac</span><span class="sxs-lookup"><span data-stu-id="780de-134">Apple Support Article - How tooconnect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="780de-135">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="780de-135">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="780de-136">Risoluzione dei problemi in Windows</span><span class="sxs-lookup"><span data-stu-id="780de-136">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="780de-137">Risoluzione dei problemi in Linux</span><span class="sxs-lookup"><span data-stu-id="780de-137">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    