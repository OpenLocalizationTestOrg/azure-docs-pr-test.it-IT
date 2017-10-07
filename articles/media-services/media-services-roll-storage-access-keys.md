---
title: le chiavi di accesso ai servizi multimediali aaaUpdate dopo l'operazione di archiviazione | Documenti Microsoft
description: In questo articolo offrono indicazioni su come le chiavi di accesso tooupdate Media Services dopo l'operazione di archiviazione.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a892ebb0-0ea0-4fc8-b715-60347cc5c95b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: milanga;cenkdin;juliako
ms.openlocfilehash: 26fa7a75a73397842aaebda59516a00f68ab97f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a><span data-ttu-id="e2ab8-103">Aggiornare Servizi multimediali dopo il rollover delle chiavi di accesso alle risorse di archiviazione</span><span class="sxs-lookup"><span data-stu-id="e2ab8-103">Update Media Services after rolling storage access keys</span></span>

<span data-ttu-id="e2ab8-104">Quando si crea un nuovo account di servizi multimediali di Azure (AMS), verrà anche chiesto tooselect account di archiviazione di Azure che è utilizzato toostore i contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-104">When you create a new Azure Media Services (AMS) account, you are also asked tooselect an Azure Storage account that is used toostore your media content.</span></span> <span data-ttu-id="e2ab8-105">È possibile aggiungere tooyour gli account di archiviazione più di un account di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-105">You can add more than one storage accounts tooyour Media Services account.</span></span> <span data-ttu-id="e2ab8-106">Questo argomento viene illustrato come chiavi per l'archiviazione toorotate.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-106">This topic shows how toorotate storage keys.</span></span> <span data-ttu-id="e2ab8-107">Viene inoltre illustrato come archiviazione tooadd account tooa account di supporto.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-107">It also shows how tooadd storage accounts tooa media account.</span></span> 

<span data-ttu-id="e2ab8-108">azioni di hello tooperform descritte in questo argomento, è consigliabile usare [API ARM](https://docs.microsoft.com/rest/api/media/mediaservice) e [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span><span class="sxs-lookup"><span data-stu-id="e2ab8-108">tooperform hello actions described in this topic, you should be using [ARM APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span></span>  <span data-ttu-id="e2ab8-109">Per ulteriori informazioni, vedere [come toomanage Azure risorse con PowerShell e Gestione risorse](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e2ab8-109">For more information, see [How toomanage Azure resources with PowerShell and Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

## <a name="overview"></a><span data-ttu-id="e2ab8-110">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e2ab8-110">Overview</span></span>

<span data-ttu-id="e2ab8-111">Quando viene creato un nuovo account di archiviazione, Azure genera due chiavi di accesso archiviazione a 512 bit, che sono utilizzati tooauthenticate accedere tooyour account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-111">When a new storage account is created, Azure generates two 512-bit storage access keys, which are used tooauthenticate access tooyour storage account.</span></span> <span data-ttu-id="e2ab8-112">tookeep le connessioni di archiviazione più sicure, che è consigliabile tooperiodically rigenerano e ruotare la chiave di accesso di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-112">tookeep your storage connections more secure, it is recommended tooperiodically regenerate and rotate your storage access key.</span></span> <span data-ttu-id="e2ab8-113">Due chiavi di accesso (primari e secondari) vengono forniti in ordine tooenable toomaintain connessioni toohello account di archiviazione utilizzando uno tasto mentre si rigenera hello altre chiavi di accesso.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-113">Two access keys (primary and secondary) are provided in order tooenable you toomaintain connections toohello storage account using one access key while you regenerate hello other access key.</span></span> <span data-ttu-id="e2ab8-114">Questa procedura viene anche denominata "rollover delle chiavi di accesso".</span><span class="sxs-lookup"><span data-stu-id="e2ab8-114">This procedure is also called "rolling access keys".</span></span>

<span data-ttu-id="e2ab8-115">Servizi multimediali dipende da una chiave di archiviazione fornita tooit.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-115">Media Services depends on a storage key provided tooit.</span></span> <span data-ttu-id="e2ab8-116">In particolare, i localizzatori hello toostream usato o scaricare gli asset dipendono dalla chiave di accesso di archiviazione specificato hello.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-116">Specifically, hello locators that are used toostream or download your assets depend on hello specified storage access key.</span></span> <span data-ttu-id="e2ab8-117">Quando viene creato un account di sistema AMS assume una dipendenza di chiave di accesso di archiviazione primaria hello per impostazione predefinita, ma come un utente è possibile aggiornare una chiave di archiviazione hello AMS con.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-117">When an AMS account is created it takes a dependency on hello primary storage access key by default but as a user you can update hello storage key that AMS has.</span></span> <span data-ttu-id="e2ab8-118">È necessario assicurarsi di servizi multimediali toolet sapere quale chiave toouse seguendo i passaggi descritti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-118">You must make sure toolet Media Services know which key toouse by following steps described in this topic.</span></span>  

>[!NOTE]
> <span data-ttu-id="e2ab8-119">Se si dispone di più account di archiviazione, è necessario eseguire questa procedura per ogni account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-119">If you have multiple storage accounts, you would perform this procedure with each storage account.</span></span> <span data-ttu-id="e2ab8-120">ordine di Hello in cui si ruotare le chiavi di archiviazione non è fisso.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-120">hello order in which you rotate storage keys is not fixed.</span></span> <span data-ttu-id="e2ab8-121">È possibile ruotare la chiave secondaria hello prima e quindi hello principale viceversa chiave o viceversa.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-121">You can rotate hello secondary key first and then hello primary key or vice versa.</span></span>
>
> <span data-ttu-id="e2ab8-122">Prima di eseguire i passaggi descritti in questo argomento in un account di produzione, assicurarsi che tootest loro un account di pre-produzione.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-122">Before executing steps described in this topic on a production account, make sure tootest them on a pre-production account.</span></span>
>

## <a name="steps-toorotate-storage-keys"></a><span data-ttu-id="e2ab8-123">Chiavi per l'archiviazione toorotate passaggi</span><span class="sxs-lookup"><span data-stu-id="e2ab8-123">Steps toorotate storage keys</span></span> 
 
 1. <span data-ttu-id="e2ab8-124">Modifica hello chiave account di archiviazione primario tramite il cmdlet powershell hello o [Azure](https://portal.azure.com/) portale.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-124">Change hello storage account Primary key through hello powershell cmdlet or [Azure](https://portal.azure.com/) portal.</span></span>
 2. <span data-ttu-id="e2ab8-125">Chiamare il cmdlet AzureRmMediaServiceStorageKeys di sincronizzazione con i parametri appropriati tooforce supporti account toopick le chiavi di account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="e2ab8-125">Call Sync-AzureRmMediaServiceStorageKeys cmdlet with appropriate params tooforce media account toopick up storage account keys</span></span>
 
    <span data-ttu-id="e2ab8-126">Hello di esempio seguente viene illustrato come toosync chiavi account toostorage.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-126">hello following example shows how toosync keys toostorage accounts.</span></span>
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. <span data-ttu-id="e2ab8-127">Attendere circa un'ora.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-127">Wait an hour or so.</span></span> <span data-ttu-id="e2ab8-128">Verificare gli scenari di streaming hello funzionino.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-128">Verify hello streaming scenarios are working.</span></span>
 4. <span data-ttu-id="e2ab8-129">Modifica chiave account di archiviazione secondario tramite i cmdlet di powershell hello o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-129">Change storage account secondary key through hello powershell cmdlet or Azure portal.</span></span>
 5. <span data-ttu-id="e2ab8-130">Chiamare powershell AzureRmMediaServiceStorageKeys di sincronizzazione con i parametri appropriati tooforce supporti account toopick di nuove chiavi dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-130">Call Sync-AzureRmMediaServiceStorageKeys powershell with appropriate params tooforce media account toopick up new storage account keys.</span></span> 
 6. <span data-ttu-id="e2ab8-131">Attendere circa un'ora.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-131">Wait an hour or so.</span></span> <span data-ttu-id="e2ab8-132">Verificare gli scenari di streaming hello funzionino.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-132">Verify hello streaming scenarios are working.</span></span>
 
### <a name="a-powershell-cmdlet-example"></a><span data-ttu-id="e2ab8-133">Esempio di cmdlet PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2ab8-133">A powershell cmdlet example</span></span> 

<span data-ttu-id="e2ab8-134">Hello esempio seguente viene illustrato come tooget hello account di archiviazione e sincronizzarlo con account hello AMS.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-134">hello following example demonstrates how tooget hello storage account and sync it with hello AMS account.</span></span>

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-tooadd-storage-accounts-tooyour-ams-account"></a><span data-ttu-id="e2ab8-135">Account di sistema AMS tooyour gli account di archiviazione di tooadd passaggi</span><span class="sxs-lookup"><span data-stu-id="e2ab8-135">Steps tooadd storage accounts tooyour AMS account</span></span>

<span data-ttu-id="e2ab8-136">Hello argomento seguente viene illustrato come archiviazione tooadd account account tooyour AMS: [allegare tooa gli account di archiviazione più account di servizi multimediali](meda-services-managing-multiple-storage-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="e2ab8-136">hello following topic shows how tooadd storage accounts tooyour AMS account: [Attach multiple storage accounts tooa Media Services account](meda-services-managing-multiple-storage-accounts.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="e2ab8-137">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="e2ab8-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e2ab8-138">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="e2ab8-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="e2ab8-139">Ringraziamenti</span><span class="sxs-lookup"><span data-stu-id="e2ab8-139">Acknowledgments</span></span>
<span data-ttu-id="e2ab8-140">Desideriamo hello tooacknowledge seguente persone che hanno contribuito per la creazione di questo documento: Cenk Dingiloglu, Milano Gada, Seva Titov.</span><span class="sxs-lookup"><span data-stu-id="e2ab8-140">We would like tooacknowledge hello following people who contributed towards creating this document: Cenk Dingiloglu, Milan Gada, Seva Titov.</span></span>
