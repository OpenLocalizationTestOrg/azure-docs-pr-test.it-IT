---
title: Aggiornare Servizi multimediali dopo il rollover delle chiavi di accesso alle risorse di archiviazione | Microsoft Docs
description: "Questo articolo fornisce informazioni sulle modalità per aggiornare Servizi multimediali dopo aver eseguito il rollover delle chiavi di accesso alle risorse di archiviazione."
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
ms.openlocfilehash: 304e72e0d2d4a7e95df513e6d5481def9eae3f68
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a><span data-ttu-id="8c7ce-103">Aggiornare Servizi multimediali dopo il rollover delle chiavi di accesso alle risorse di archiviazione</span><span class="sxs-lookup"><span data-stu-id="8c7ce-103">Update Media Services after rolling storage access keys</span></span>

<span data-ttu-id="8c7ce-104">Quando si crea un nuovo account di Servizi multimediali di Azure (AMS), viene chiesto di selezionare anche un account di archiviazione di Azure da usare per l'archiviazione dei contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-104">When you create a new Azure Media Services (AMS) account, you are also asked to select an Azure Storage account that is used to store your media content.</span></span> <span data-ttu-id="8c7ce-105">È possibile aggiungere più di un account di archiviazione all'account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-105">You can add more than one storage accounts to your Media Services account.</span></span> <span data-ttu-id="8c7ce-106">In questo argomento viene illustrato come far ruotare le chiavi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-106">This topic shows how to rotate storage keys.</span></span> <span data-ttu-id="8c7ce-107">Viene inoltre illustrato come aggiungere gli account di archiviazione a un account multimediale.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-107">It also shows how to add storage accounts to a media account.</span></span> 

<span data-ttu-id="8c7ce-108">Per eseguire le operazioni descritte in questo argomento, è necessario utilizzare le [API ARM](https://docs.microsoft.com/rest/api/media/mediaservice) e [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span><span class="sxs-lookup"><span data-stu-id="8c7ce-108">To perform the actions described in this topic, you should be using [ARM APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span></span>  <span data-ttu-id="8c7ce-109">Per ulteriori informazioni, vedere [Gestire le risorse di Azure con PowerShell e Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="8c7ce-109">For more information, see [How to manage Azure resources with PowerShell and Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

## <a name="overview"></a><span data-ttu-id="8c7ce-110">Panoramica</span><span class="sxs-lookup"><span data-stu-id="8c7ce-110">Overview</span></span>

<span data-ttu-id="8c7ce-111">Quando viene creato un nuovo account di archiviazione, Azure genera due chiavi di accesso a 512 bit alle risorse di archiviazione, che consentono di autenticare l'accesso all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-111">When a new storage account is created, Azure generates two 512-bit storage access keys, which are used to authenticate access to your storage account.</span></span> <span data-ttu-id="8c7ce-112">Per mantenere le connessioni di archiviazione più sicure, si consiglia di rigenerare e far ruotare periodicamente la chiave di accesso alle risorse di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-112">To keep your storage connections more secure, it is recommended to periodically regenerate and rotate your storage access key.</span></span> <span data-ttu-id="8c7ce-113">Per non perdere mai la connessione all'account di archiviazione, vengono fornite due chiavi di accesso (primaria e secondaria), in modo da poter usare la prima mentre si rigenera la seconda.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-113">Two access keys (primary and secondary) are provided in order to enable you to maintain connections to the storage account using one access key while you regenerate the other access key.</span></span> <span data-ttu-id="8c7ce-114">Questa procedura viene anche denominata "rollover delle chiavi di accesso".</span><span class="sxs-lookup"><span data-stu-id="8c7ce-114">This procedure is also called "rolling access keys".</span></span>

<span data-ttu-id="8c7ce-115">Servizi multimediali dipende da una chiave di archiviazione fornita.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-115">Media Services depends on a storage key provided to it.</span></span> <span data-ttu-id="8c7ce-116">In particolare, i localizzatori che sono usati per trasmettere in streaming o scaricare gli asset dipendono dalla chiave di accesso alle risorse di archiviazione specificata.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-116">Specifically, the locators that are used to stream or download your assets depend on the specified storage access key.</span></span> <span data-ttu-id="8c7ce-117">Quando viene creato un account AMS, esso assume una dipendenza dalla chiave di accesso alle risorse di archiviazione primaria per impostazione predefinita, ma l’utente può aggiornare la chiave di archiviazione di Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-117">When an AMS account is created it takes a dependency on the primary storage access key by default but as a user you can update the storage key that AMS has.</span></span> <span data-ttu-id="8c7ce-118">È necessario comunicare a Servizi multimediali la chiave da usare, seguendo i passaggi descritti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-118">You must make sure to let Media Services know which key to use by following steps described in this topic.</span></span>  

>[!NOTE]
> <span data-ttu-id="8c7ce-119">Se si dispone di più account di archiviazione, è necessario eseguire questa procedura per ogni account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-119">If you have multiple storage accounts, you would perform this procedure with each storage account.</span></span> <span data-ttu-id="8c7ce-120">L'ordine in cui ruotare le chiavi di archiviazione non è prefissato.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-120">The order in which you rotate storage keys is not fixed.</span></span> <span data-ttu-id="8c7ce-121">È possibile ruotare prima la chiave secondaria e quindi quella principale o viceversa.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-121">You can rotate the secondary key first and then the primary key or vice versa.</span></span>
>
> <span data-ttu-id="8c7ce-122">Prima di eseguire la procedura descritta in questo argomento su un account di produzione, effettuarne il test in un account di pre-produzione.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-122">Before executing steps described in this topic on a production account, make sure to test them on a pre-production account.</span></span>
>

## <a name="steps-to-rotate-storage-keys"></a><span data-ttu-id="8c7ce-123">Passaggi per ruotare le chiavi di archiviazione</span><span class="sxs-lookup"><span data-stu-id="8c7ce-123">Steps to rotate storage keys</span></span> 
 
 1. <span data-ttu-id="8c7ce-124">Modificare la chiave primaria dell'account di archiviazione tramite il cmdlet PowerShell o il portale di [Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8c7ce-124">Change the storage account Primary key through the powershell cmdlet or [Azure](https://portal.azure.com/) portal.</span></span>
 2. <span data-ttu-id="8c7ce-125">Chiamare il cmdlet Sync-AzureRmMediaServiceStorageKeys con i parametri appropriati per forzare l'account multimediale a prendere le chiavi dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="8c7ce-125">Call Sync-AzureRmMediaServiceStorageKeys cmdlet with appropriate params to force media account to pick up storage account keys</span></span>
 
    <span data-ttu-id="8c7ce-126">Nell'esempio seguente viene illustrato come sincronizzare le chiavi con gli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-126">The following example shows how to sync keys to storage accounts.</span></span>
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. <span data-ttu-id="8c7ce-127">Attendere circa un'ora.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-127">Wait an hour or so.</span></span> <span data-ttu-id="8c7ce-128">Verificare che gli scenari di streaming funzionino.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-128">Verify the streaming scenarios are working.</span></span>
 4. <span data-ttu-id="8c7ce-129">Modificare la chiave secondaria dell'account di archiviazione tramite il cmdlet PowerShell o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-129">Change storage account secondary key through the powershell cmdlet or Azure portal.</span></span>
 5. <span data-ttu-id="8c7ce-130">Chiamare il cmdlet PowerShell Sync-AzureRmMediaServiceStorageKeys con i parametri appropriati per forzare l'account multimediale a prendere le nuove chiavi dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-130">Call Sync-AzureRmMediaServiceStorageKeys powershell with appropriate params to force media account to pick up new storage account keys.</span></span> 
 6. <span data-ttu-id="8c7ce-131">Attendere circa un'ora.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-131">Wait an hour or so.</span></span> <span data-ttu-id="8c7ce-132">Verificare che gli scenari di streaming funzionino.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-132">Verify the streaming scenarios are working.</span></span>
 
### <a name="a-powershell-cmdlet-example"></a><span data-ttu-id="8c7ce-133">Esempio di cmdlet PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c7ce-133">A powershell cmdlet example</span></span> 

<span data-ttu-id="8c7ce-134">Nell'esempio seguente viene illustrato come ottenere l'account di archiviazione e sincronizzarlo con l'account AMS.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-134">The following example demonstrates how to get the storage account and sync it with the AMS account.</span></span>

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-to-add-storage-accounts-to-your-ams-account"></a><span data-ttu-id="8c7ce-135">Passaggi per aggiungere gli account di archiviazione all'account AMS</span><span class="sxs-lookup"><span data-stu-id="8c7ce-135">Steps to add storage accounts to your AMS account</span></span>

<span data-ttu-id="8c7ce-136">L'argomento seguente illustra come aggiungere gli account di archiviazione all'account AMS: [Collegare più account di archiviazione a un account di Servizi multimediali](meda-services-managing-multiple-storage-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="8c7ce-136">The following topic shows how to add storage accounts to your AMS account: [Attach multiple storage accounts to a Media Services account](meda-services-managing-multiple-storage-accounts.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="8c7ce-137">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="8c7ce-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8c7ce-138">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="8c7ce-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="8c7ce-139">Ringraziamenti</span><span class="sxs-lookup"><span data-stu-id="8c7ce-139">Acknowledgments</span></span>
<span data-ttu-id="8c7ce-140">Siamo lieti di conferire un riconoscimento alle seguenti persone che hanno contribuito alla realizzazione di questo documento: Cenk Dingiloglu, Gada Milano, Seva Titov.</span><span class="sxs-lookup"><span data-stu-id="8c7ce-140">We would like to acknowledge the following people who contributed towards creating this document: Cenk Dingiloglu, Milan Gada, Seva Titov.</span></span>
