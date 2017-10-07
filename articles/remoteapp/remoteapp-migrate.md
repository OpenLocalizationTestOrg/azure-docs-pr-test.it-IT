---
title: dati dell'utente da Azure RemoteApp aaaMigrate | Documenti Microsoft
description: Informazioni su come toomigrate i dati utente da e verso Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aefc6ccc2c6173754acf6cad06102f27c8cb1d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-data-into-and-out-of-azure-remoteapp"></a><span data-ttu-id="bbc6a-103">Come toomigrate dati dentro e fuori da Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="bbc6a-103">How toomigrate data into and out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bbc6a-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="bbc6a-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="bbc6a-106">È possibile utilizzare molti strumenti e metodi tootransfer [dati utente](remoteapp-upd.md) dentro e fuori da Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-106">You can use many different tools and methods tootransfer [user data](remoteapp-upd.md) into and out of Azure RemoteApp.</span></span> <span data-ttu-id="bbc6a-107">Ecco alcuni metodi:</span><span class="sxs-lookup"><span data-stu-id="bbc6a-107">Here are a few methods:</span></span>

* <span data-ttu-id="bbc6a-108">Copiare e incollare i dati usando la condivisione degli Appunti</span><span class="sxs-lookup"><span data-stu-id="bbc6a-108">Copy and paste using clipboard sharing</span></span>
* <span data-ttu-id="bbc6a-109">Copiare i file e i dati server file tooa</span><span class="sxs-lookup"><span data-stu-id="bbc6a-109">Copy files and data tooa file server</span></span>
* <span data-ttu-id="bbc6a-110">Copiare i file tooOneDrive per le aziende tramite un browser</span><span class="sxs-lookup"><span data-stu-id="bbc6a-110">Copy files tooOneDrive for Business through a browser</span></span>
* <span data-ttu-id="bbc6a-111">Copiare i file mediante il reindirizzamento</span><span class="sxs-lookup"><span data-stu-id="bbc6a-111">Copy files using redirection</span></span>

> [!NOTE]
> <span data-ttu-id="bbc6a-112">È possibile abilitare hello OneDrive per Business o i Consumer di agenti di sincronizzazione - essi [non sono supportati](remoteapp-onedrive.md) in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-112">You cannot enable hello OneDrive for Business or Consumer sync agents - they [are not supported](remoteapp-onedrive.md) in Azure RemoteApp.</span></span>
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a><span data-ttu-id="bbc6a-113">Usare l'operazione di copia e incolla in Esplora file</span><span class="sxs-lookup"><span data-stu-id="bbc6a-113">Use copy and paste in File Explorer</span></span>
<span data-ttu-id="bbc6a-114">Copia e Incolla di utilizzo degli Appunti hello è abilitato nelle distribuzioni di RemoteApp [per impostazione predefinita](remoteapp-redirection.md).</span><span class="sxs-lookup"><span data-stu-id="bbc6a-114">Copy and paste using hello clipboard is enabled in RemoteApp deployments [by default](remoteapp-redirection.md).</span></span> <span data-ttu-id="bbc6a-115">Gli utenti possono quindi copiare i file tra le app RemoteApp e del PC locale.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-115">This lets users copy files between their local PC and RemoteApp apps.</span></span> <span data-ttu-id="bbc6a-116">Spesso, tramite hello normali usano le App in RemoteApp, gli utenti abbiano salvato i file che tootheir - lo spostamento di dati da RemoteApp sono facili:</span><span class="sxs-lookup"><span data-stu-id="bbc6a-116">Often, through hello normal course of using apps in RemoteApp, users have saved files tootheir UPDs - moving that data out of RemoteApp is easy:</span></span>

1. <span data-ttu-id="bbc6a-117">[Pubblicare Esplora file come app](remoteapp-publish.md) in una raccolta RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-117">[Publish File Explorer as an app](remoteapp-publish.md) in a RemoteApp collection.</span></span> <span data-ttu-id="bbc6a-118">Si noti che questa è un'attività amministrativa.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-118">(Note that this is an administrative task.)</span></span>
2. <span data-ttu-id="bbc6a-119">Diretto utenti toolaunch hello Esplora File app che è stato pubblicato e toouse che toocopy e incollare i file nella loro UPD ed esplicitamente.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-119">Direct your users toolaunch hello File Explorer app you published and toouse that toocopy and paste files both into their UPD and out of it.</span></span>

## <a name="upload-files-and-data-tooa-file-server-by-using-standard-network-file-copy"></a><span data-ttu-id="bbc6a-120">Caricare i file e dati tooa file server mediante copia dei file di rete standard</span><span class="sxs-lookup"><span data-stu-id="bbc6a-120">Upload files and data tooa file server by using standard network file copy</span></span>
<span data-ttu-id="bbc6a-121">Spesso le organizzazioni di utilizzare dati generale toostore di file server.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-121">Often organizations use file servers toostore general data.</span></span> <span data-ttu-id="bbc6a-122">Se si conosce il nome di server hello o un percorso, gli utenti possono cercare hello rete locale server hello e quindi copiare i file, analogamente a quanto avveniva in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-122">If you know hello server name or location, your users can browse hello local network for hello server and then copy their files there, much like they did above.</span></span> <span data-ttu-id="bbc6a-123">Si verrà nuovamente desidera toopublish tooRemoteApp di Esplora File e quindi condividerlo con gli utenti.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-123">Again you'll want toopublish File Explorer tooRemoteApp and then share it with your users.</span></span>

> [!NOTE]
> <span data-ttu-id="bbc6a-124">server di file Hello deve trovarsi nella rete instradabile hello RemoteApp è stato distribuito in.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-124">hello file server must be on hello routable network that RemoteApp was deployed into.</span></span>
> 
> 

## <a name="copy-files-tooonedrive-for-business"></a><span data-ttu-id="bbc6a-125">Copiare i file tooOneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="bbc6a-125">Copy files tooOneDrive for Business</span></span>
<span data-ttu-id="bbc6a-126">Anche se non è possibile abilitare hello OneDrive per agente di sincronizzazione di Business in RemoteApp, è tuttavia possibile copiare file dal tooOneDrive UPD per le aziende tramite un browser.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-126">Although you cannot enable hello OneDrive for Business sync agent in RemoteApp, you can still copy files from your UPD tooOneDrive for Business through a browser.</span></span> 

1. <span data-ttu-id="bbc6a-127">Pubblicare tooRemoteApp Esplora File e quindi indicare agli utenti tooaccess hello file tramite tale app.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-127">Publish File Explorer tooRemoteApp and then tell users tooaccess hello files through that app.</span></span> 
2. <span data-ttu-id="bbc6a-128">È più semplice tootransfer file se in modalità compressa, in modo gli utenti devono creare un file con estensione zip che contiene tutti gli tooOneDrive toomove di file hello for Business.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-128">It's easiest tootransfer files if they are compressed, so users should create a .zip file that contains all of hello files toomove tooOneDrive for Business.</span></span>
3. <span data-ttu-id="bbc6a-129">Chiedere portale per gli utenti toogo toohello Office 365 e quindi passare tooOneDrive e caricare file con estensione zip hello.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-129">Ask users toogo toohello Office 365 portal, and then go tooOneDrive and upload hello .zip file.</span></span>

## <a name="copy-files-by-using-drive-redirection"></a><span data-ttu-id="bbc6a-130">Copiare i file usando il reindirizzamento delle unità</span><span class="sxs-lookup"><span data-stu-id="bbc6a-130">Copy files by using drive redirection</span></span>
<span data-ttu-id="bbc6a-131">Se è stato abilitato il [reindirizzamento delle unità](remoteapp-redirection.md), è già stata creata un'unità mappata per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-131">If you have enabled [drive redirection](remoteapp-redirection.md), you have already created a mapped drive for your users.</span></span> <span data-ttu-id="bbc6a-132">In questo caso, è possibile comprimere i file nell'unità hello reindirizzato e salvarle tootheir PC locale.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-132">In this case, they can zip their files on hello redirected drive and then save them tootheir local PC.</span></span>

## <a name="how-administrators-can-export-data"></a><span data-ttu-id="bbc6a-133">Modalità di esportazione dei dati degli amministratori</span><span class="sxs-lookup"><span data-stu-id="bbc6a-133">How administrators can export data</span></span>

<span data-ttu-id="bbc6a-134">Amministra per Azure RemoteApp è possibile esportare tutti i dischi dei profili utente (UPD) per tutte le raccolte all'interno di un tooAzure sottoscrizione Storage utilizzando Azure PowerShell cmdlet Export-AzureRemoteAppUserDisk.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-134">Administers for Azure RemoteApp can export all user profile disks (UPD) for all collections within a subscription tooAzure Storage using Azure PowerShell cmdlet, Export-AzureRemoteAppUserDisk.</span></span>  <span data-ttu-id="bbc6a-135">Non vi è alcuna possibilità tooselect singoli UPD.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-135">There is no ability tooselect individual UPD's.</span></span>  <span data-ttu-id="bbc6a-136">Quando viene eseguito il comando di PowerShell hello, ogni disco utente sarà un 50gb di dimensioni di disco fisso e archiviazione tooAzure esportato.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-136">When hello PowerShell command is executed, each user disk will be a 50gb in fixed disk size and be exported tooAzure storage.</span></span>  <span data-ttu-id="bbc6a-137">I costi di archiviazione di Azure verranno generati immediatamente per questa risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-137">Costs of Azure storage will incur immediately for this storage.</span></span>  <span data-ttu-id="bbc6a-138">Quando l'esecuzione del comando verificare che non sono presenti sessioni in caso contrario hello esportazione avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-138">When running this command ensure there are no sessions otherwise hello export will fail.</span></span>

<span data-ttu-id="bbc6a-139">Gli UPD per le distribuzioni di Azure RemoteApp aggiunte a un dominio possono solo essere riusati in una distribuzione di Servizi desktop remoto; non è possibile usare distribuzioni non aggiunte a dominio.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-139">UPD's for domain joined Azure RemoteApp deployments can only be used again in an RDS deployment, non-domain joined deployments cannot be used.</span></span>  <span data-ttu-id="bbc6a-140">Se tali dischi verranno utilizzati in una distribuzione di servizi desktop remoto, è consigliabile toouse nostri [automatizzata script](https://github.com/arcadiahlyy/aramigration) che verrà esportare, convertire e importare hello del UPD in una distribuzione di servizi desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-140">If these disks will be used in an RDS deployment we recommend toouse our [automated scripts](https://github.com/arcadiahlyy/aramigration) that will export, convert, and import hello UPD's into an RDS deployment.</span></span>

