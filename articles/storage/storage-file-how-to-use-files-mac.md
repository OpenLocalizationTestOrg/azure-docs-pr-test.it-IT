---
title: Montare una condivisione file di Azure tramite SMB con macOS | Microsoft Docs
description: Informazioni su come montare una condivisione file di Azure tramite SMB con macOS.
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
ms.openlocfilehash: 428086910273d10a68cb8193df377a4db267d6a3
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a><span data-ttu-id="658ab-103">Montare una condivisione file di Azure tramite SMB con macOS</span><span class="sxs-lookup"><span data-stu-id="658ab-103">Mount Azure File share over SMB with macOS</span></span>
<span data-ttu-id="658ab-104">[Archiviazione file di Azure](storage-dotnet-how-to-use-files.md) è un servizio di Microsoft che consente di creare e usare condivisioni file di rete in Azure usando lo standard di settore.</span><span class="sxs-lookup"><span data-stu-id="658ab-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's service that enables you to create and use network file shares in the Azure using the industry standard.</span></span> <span data-ttu-id="658ab-105">Le condivisioni file di Azure possono essere montate in macOS Sierra (10.12) ed El Capitan (10.11).</span><span class="sxs-lookup"><span data-stu-id="658ab-105">Azure File shares can be mounted in macOS Sierra (10.12) and El Capitan (10.11).</span></span> <span data-ttu-id="658ab-106">Questo articolo illustra due diversi modi di montare una condivisione file di Azure in macOS con l'interfaccia utente del Finder e usando il terminale.</span><span class="sxs-lookup"><span data-stu-id="658ab-106">This article shows two different ways to mount an Azure File share on macOS with the Finder UI and using the Terminal.</span></span>

> [!Note]  
> <span data-ttu-id="658ab-107">Prima di montare una condivisione file di Azure tramite SMB, è consigliabile disabilitare la firma dei pacchetti SMB.</span><span class="sxs-lookup"><span data-stu-id="658ab-107">Before mounting an Azure File share over SMB, we recommend disabling SMB packet signing.</span></span> <span data-ttu-id="658ab-108">In caso contrario, si potrebbe verificare una riduzione delle prestazioni quando si accede alla condivisione file di Azure da macOS.</span><span class="sxs-lookup"><span data-stu-id="658ab-108">Not doing so may yield poor performance when accessing the Azure File share from macOS.</span></span> <span data-ttu-id="658ab-109">La connessione SMB verrà crittografata e la sicurezza della connessione non risulterà compromessa.</span><span class="sxs-lookup"><span data-stu-id="658ab-109">Your SMB connection will be encrypted, so this does not affect the security of your connection.</span></span> <span data-ttu-id="658ab-110">Dal terminale i comandi seguenti disabiliteranno la firma dei pacchetti SMB, come illustrato da questo [articolo del supporto Apple sulla disabilitazione della firma dei pacchetti SMB](https://support.apple.com/HT205926):</span><span class="sxs-lookup"><span data-stu-id="658ab-110">From the terminal, the following commands will disable SMB packet signing, as described by this [Apple support article on disabling SMB packet signing](https://support.apple.com/HT205926):</span></span>  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a><span data-ttu-id="658ab-111">Prerequisiti per il montaggio di una condivisione file di Azure in macOS</span><span class="sxs-lookup"><span data-stu-id="658ab-111">Prerequisites for mounting an Azure File share on macOS</span></span>
* <span data-ttu-id="658ab-112">**Nome dell'account di archiviazione**: per montare una condivisione file di Azure, sarà necessario il nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="658ab-112">**Storage account name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="658ab-113">**Chiave dell'account di archiviazione**: per montare una condivisione file di Azure, sarà necessaria la chiave dell'account primaria (o secondaria).</span><span class="sxs-lookup"><span data-stu-id="658ab-113">**Storage account key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="658ab-114">Le chiavi di firma di accesso condiviso non sono attualmente supportate per il montaggio.</span><span class="sxs-lookup"><span data-stu-id="658ab-114">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="658ab-115">**Assicurarsi che la porta 445 sia aperta**: SMB comunica tramite la porta TCP 445.</span><span class="sxs-lookup"><span data-stu-id="658ab-115">**Ensure port 445 is open**: SMB communicates over TCP port 445.</span></span> <span data-ttu-id="658ab-116">Nel computer client (Mac) verificare che il firewall non blocchi la porta TCP 445.</span><span class="sxs-lookup"><span data-stu-id="658ab-116">On your client machine (the Mac), check to make sure your firewall is not blocking TCP port 445.</span></span>

## <a name="mount-an-azure-file-share-via-finder"></a><span data-ttu-id="658ab-117">Montare una condivisione file di Azure tramite il Finder</span><span class="sxs-lookup"><span data-stu-id="658ab-117">Mount an Azure File share via Finder</span></span>
1. <span data-ttu-id="658ab-118">**Aprire Finder**: per impostazione predefinita, il Finder è aperto in macOS, ma è possibile assicurarsi che sia l'applicazione attualmente selezionata facendo clic sull'icona con il volto di macOS sul Dock:</span><span class="sxs-lookup"><span data-stu-id="658ab-118">**Open Finder**: Finder is open on macOS by default, but you can ensure it is the currently selected application by clicking the "macOS face icon" on the dock:</span></span>  
    <span data-ttu-id="658ab-119">![Icona con il volto di macOS](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span><span class="sxs-lookup"><span data-stu-id="658ab-119">![The macOS face icon](media/storage-file-how-to-use-files-mac/mount-via-finder-1.png)</span></span>

2. <span data-ttu-id="658ab-120">**Scegliere "Connect to Server" (Connetti al server) dal menu "Vai"**: usando il percorso UNC dei [prerequisiti](#preq), convertire la doppia barra rovesciata iniziale (`\\`) in `smb://` e tutte le altre barre rovesciate (`\`) in barre (`/`).</span><span class="sxs-lookup"><span data-stu-id="658ab-120">**Select "Connect to Server" from the "Go" Menu**: Using the UNC path from the [prerequisites](#preq), convert the beginning double backslash (`\\`) to `smb://` and all other backslashes (`\`) to forwards slashes (`/`).</span></span> <span data-ttu-id="658ab-121">Il collegamento sarà simile al seguente: ![Finestra di dialogo "Connect to Server" (Connetti al server)](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span><span class="sxs-lookup"><span data-stu-id="658ab-121">Your link should look like the following: ![The "Connect to Server" dialog](./media/storage-file-how-to-use-files-mac/mount-via-finder-2.png)</span></span>

3. <span data-ttu-id="658ab-122">**Usare il nome condivisione e la chiave dell'account di archiviazione quando vengono chiesti un nome utente e una password**: quando si fa clic su "Connessione" nella finestra di dialogo "Connect to Server" (Connetti al server), verranno chiesti il nome utente e la password. Verrà automaticamente inserito il nome utente macOS.</span><span class="sxs-lookup"><span data-stu-id="658ab-122">**Use the share name and storage account key when prompted for a username and password**: When you click "Connect" on the "Connect to Server" dialog, you will be prompted for the username and password (This will be autopopulated with your macOS username).</span></span> <span data-ttu-id="658ab-123">È possibile inserire il nome condivisione o la chiave dell'account di archiviazione nel portachiavi di macOS.</span><span class="sxs-lookup"><span data-stu-id="658ab-123">You have the option of placing the share name/storage account key in your macOS Keychain.</span></span>

4. <span data-ttu-id="658ab-124">**Usare la condivisione file di Azure nel modo desiderato**: dopo avere sostituito il nome utente e la password con il nome condivisione e la chiave dell'account di archiviazione, la condivisione verrà montata.</span><span class="sxs-lookup"><span data-stu-id="658ab-124">**Use the Azure File share as desired**: After substituting the share name and storage account key in for the username and password, the share will be mounted.</span></span> <span data-ttu-id="658ab-125">È possibile usarla come qualsiasi altra cartella/condivisione file locale, anche ad esempio per trascinare e rilasciare file nella condivisione file:</span><span class="sxs-lookup"><span data-stu-id="658ab-125">You may use this as you would normally use a local folder/file share, including dragging and dropping files into the file share:</span></span>

    ![Snapshot di una condivisione file di Azure montata](./media/storage-file-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a><span data-ttu-id="658ab-127">Montare una condivisione file di Azure tramite il terminale</span><span class="sxs-lookup"><span data-stu-id="658ab-127">Mount an Azure File share via Terminal</span></span>
1. <span data-ttu-id="658ab-128">Sostituire `<storage-account-name>` con il nome del proprio account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="658ab-128">Replace `<storage-account-name>` with the name of your storage account.</span></span> <span data-ttu-id="658ab-129">Specificare la chiave dell'account di archiviazione come password quando viene chiesta.</span><span class="sxs-lookup"><span data-stu-id="658ab-129">Provide Storage Account Key as password when prompted.</span></span> 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. <span data-ttu-id="658ab-130">**Usare la condivisione file di Azure nel modo desiderato**: la condivisione file di Azure verrà montata nel punto di montaggio specificato dal comando precedente.</span><span class="sxs-lookup"><span data-stu-id="658ab-130">**Use the Azure File share as desired**: The Azure File share will be mounted at the mount point specified by the previous command.</span></span>  

    ![Snapshot della condivisione file di Azure montata](./media/storage-file-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a><span data-ttu-id="658ab-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="658ab-132">Next steps</span></span>
<span data-ttu-id="658ab-133">Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="658ab-133">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="658ab-134">Articolo del supporto Apple: Come connettersi con Condivisione file sul Mac</span><span class="sxs-lookup"><span data-stu-id="658ab-134">Apple Support Article - How to connect with File Sharing on your Mac</span></span>](https://support.apple.com/HT204445)
* [<span data-ttu-id="658ab-135">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="658ab-135">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="658ab-136">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="658ab-136">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)