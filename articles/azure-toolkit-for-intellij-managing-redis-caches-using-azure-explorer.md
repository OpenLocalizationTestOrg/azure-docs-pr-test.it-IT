---
title: utilizzando la cache Redis aaaManaging hello Esplora Azure per IntelliJ | Documenti Microsoft
description: Informazioni su come toomanage il redis di Azure vengono memorizzati nella cache tramite Esplora Azure hello per IntelliJ.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/14/2017
ms.author: robmcm
ms.openlocfilehash: 76ba37a2a35c26d0045e17003181108992eb957d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-redis-caches-using-hello-azure-explorer-for-intellij"></a><span data-ttu-id="5b11f-103">Gestione delle cache Redis di hello Azure Explorer IntelliJ</span><span class="sxs-lookup"><span data-stu-id="5b11f-103">Managing Redis Caches using hello Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="5b11f-104">Esplora Azure, che fa parte di hello Azure Toolkit per IntelliJ, fornisce agli sviluppatori Java con una soluzione da usare per la gestione di redis cache nel loro account Azure all'interno di hello IntelliJ IDE Hello.</span><span class="sxs-lookup"><span data-stu-id="5b11f-104">hello Azure Explorer, which is part of hello Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing redis caches in their Azure account from inside hello IntelliJ IDE.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-intellij"></a><span data-ttu-id="5b11f-105">Creare una Cache Redis tramite IntelliJ</span><span class="sxs-lookup"><span data-stu-id="5b11f-105">Create a Redis Cache by using IntelliJ</span></span>

<span data-ttu-id="5b11f-106">Hello seguendo i passaggi illustrati hello passaggi toocreate una cache redis tramite hello Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="5b11f-106">hello following steps walk you through hello steps toocreate a redis cache using hello Azure Explorer.</span></span>

1. <span data-ttu-id="5b11f-107">Accedi tooyour account Azure utilizzando i passaggi di hello hello [Sign In istruzioni per hello Azure Toolkit per IntelliJ] articolo.</span><span class="sxs-lookup"><span data-stu-id="5b11f-107">Sign in tooyour Azure account using hello steps in hello [Sign In Instructions for hello Azure Toolkit for IntelliJ] article.</span></span>

1. <span data-ttu-id="5b11f-108">In hello **Esplora Azure** finestra degli strumenti, espandere hello **Azure** nodo, fare doppio clic su **cache Redis**, quindi fare clic su **Create Cache Redis**.</span><span class="sxs-lookup"><span data-stu-id="5b11f-108">In hello **Azure Explorer** tool window, expand hello **Azure** node, right-click **Redis Caches**, and then click **Create Redis Cache**.</span></span>

   ![Creare un menu di Cache Redis][CR01]

1. <span data-ttu-id="5b11f-110">Quando hello **nuova Cache Redis** viene visualizzata la finestra di dialogo, specificare hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="5b11f-110">When hello **New Redis Cache** dialog box appears, specify hello following options:</span></span>

   ![Finestra di dialogo Crea nuova Cache Redis][CR02]

   <span data-ttu-id="5b11f-112">a.</span><span class="sxs-lookup"><span data-stu-id="5b11f-112">a.</span></span> <span data-ttu-id="5b11f-113">**Nome DNS**: Specifica il sottodominio DNS hello per cache redis nuovo hello, che vengono anteposti troppo ". redis.cache.windows .net", ad esempio: *wingtiptoys.redis.cache.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="5b11f-113">**DNS Name**: Specifies hello DNS subdomain for hello new redis cache, which are prepended too".redis.cache.windows.net"; for example: *wingtiptoys.redis.cache.windows.net*.</span></span>

   <span data-ttu-id="5b11f-114">b.</span><span class="sxs-lookup"><span data-stu-id="5b11f-114">b.</span></span> <span data-ttu-id="5b11f-115">**Sottoscrizione**: specifica sottoscrizione di Azure da toouse per cache redis nuovo hello hello.</span><span class="sxs-lookup"><span data-stu-id="5b11f-115">**Subscription**: Specifies hello Azure subscription you want toouse for hello new redis cache.</span></span>

   <span data-ttu-id="5b11f-116">c.</span><span class="sxs-lookup"><span data-stu-id="5b11f-116">c.</span></span> <span data-ttu-id="5b11f-117">**Gruppo di risorse**: Specifica il gruppo di risorse hello per la cache redis, occorre toochoose di hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="5b11f-117">**Resource Group**: Specifies hello resource group for your redis cache; you need toochoose one of hello following options:</span></span>
      * <span data-ttu-id="5b11f-118">**Crea nuovo**: Specifica che si desidera toocreate un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="5b11f-118">**Create New**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="5b11f-119">**Usa esistente**: specifica che sarà possibile scegliere in un elenco i gruppi di risorse associati all'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="5b11f-119">**Use Existing**: Specifies that you will choose from a list of resource groups associated with your Azure account.</span></span>

   <span data-ttu-id="5b11f-120">d.</span><span class="sxs-lookup"><span data-stu-id="5b11f-120">d.</span></span> <span data-ttu-id="5b11f-121">**Percorso**: Specifica il percorso di hello in cui viene creata la cache redis; ad esempio, *Stati Uniti occidentali*.</span><span class="sxs-lookup"><span data-stu-id="5b11f-121">**Location**: Specifies hello location where your redis cache is created; for example, *West US*.</span></span>

   <span data-ttu-id="5b11f-122">e.</span><span class="sxs-lookup"><span data-stu-id="5b11f-122">e.</span></span> <span data-ttu-id="5b11f-123">**Livello di prezzo**: Specifica il livello di prezzo utilizza la cache redis; questa impostazione determina il numero di hello di connessioni client.</span><span class="sxs-lookup"><span data-stu-id="5b11f-123">**Pricing Tier**: Specifies which pricing tier your redis cache uses; this setting determines hello number of client connections.</span></span> <span data-ttu-id="5b11f-124">(Per altre informazioni, vedere [Prezzi di Cache Redis].)</span><span class="sxs-lookup"><span data-stu-id="5b11f-124">(For more information, see [Redis Cache Pricing].)</span></span>

   <span data-ttu-id="5b11f-125">f.</span><span class="sxs-lookup"><span data-stu-id="5b11f-125">f.</span></span> <span data-ttu-id="5b11f-126">**Porta non SSL**: specifica se la Cache Redis consente le connessioni non SSL. Per impostazione predefinita, sono consentite solo le connessioni SSL.</span><span class="sxs-lookup"><span data-stu-id="5b11f-126">**Non-SSL port**: Specifies whether your redis cache allows non-SSL connections; by default, only SSL connections are allowed.</span></span>

1. <span data-ttu-id="5b11f-127">Dopo aver specificato tutte le impostazioni della Cache Redis, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5b11f-127">When you have specified all your redis cache settings, click **OK**.</span></span>

<span data-ttu-id="5b11f-128">Dopo aver creata la cache redis, verrà visualizzato in Esplora Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5b11f-128">After your redis cache has been created, it will be displayed in hello Azure Explorer.</span></span>

   ![Cache Redis in Azure Explorer][CR03]

> [!NOTE]
>
> <span data-ttu-id="5b11f-130">Per ulteriori informazioni sulla configurazione di Azure redis le impostazioni della cache, vedere [come tooconfigure Cache Redis di Azure].</span><span class="sxs-lookup"><span data-stu-id="5b11f-130">For more information about configuring your Azure redis cache settings, see [How tooconfigure Azure Redis Cache].</span></span>
>

## <a name="display-hello-properties-for-your-redis-cache-in-intellij"></a><span data-ttu-id="5b11f-131">Visualizzare le proprietà di hello per le Cache Redis in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="5b11f-131">Display hello properties for your Redis Cache in IntelliJ</span></span>

1. <span data-ttu-id="5b11f-132">Esplora Azure hello destro la cache redis e fare clic su **visualizzare le proprietà**.</span><span class="sxs-lookup"><span data-stu-id="5b11f-132">In hello Azure Explorer, right-click your redis cache and click **Show properties**.</span></span>

   ![Azure Esplora menu toodisplay proprietà di contesto per una cache redis][SP01]

1. <span data-ttu-id="5b11f-134">Hello Azure Explorer consente di visualizzare proprietà di hello per la cache redis.</span><span class="sxs-lookup"><span data-stu-id="5b11f-134">hello Azure Explorer displays hello properties for your redis cache.</span></span>

   ![Proprietà della Cache Redis][SP02]

## <a name="delete-your-redis-cache-by-using-intellij"></a><span data-ttu-id="5b11f-136">Eliminare la Cache Redis tramite IntelliJ</span><span class="sxs-lookup"><span data-stu-id="5b11f-136">Delete your Redis Cache by using IntelliJ</span></span>

1. <span data-ttu-id="5b11f-137">Esplora Azure hello destro la cache redis e fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="5b11f-137">In hello Azure Explorer, right-click your redis cache and click **Delete**.</span></span>

   ![Esplora contesto menu toodelete una cache redis di Azure][DE01]

1. <span data-ttu-id="5b11f-139">Fare clic su **Sì** quando richiesto toodelete la cache redis.</span><span class="sxs-lookup"><span data-stu-id="5b11f-139">Click **Yes** when prompted toodelete your redis cache.</span></span>

   ![Eliminare il prompt della Cache Redis][DE02]

## <a name="next-steps"></a><span data-ttu-id="5b11f-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5b11f-141">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="5b11f-142">Per ulteriori informazioni sulle cache redis di Azure, le impostazioni di configurazione e sui prezzi, vedere hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="5b11f-142">For more information about Azure redis caches, configuration settings and pricing, see hello following links:</span></span>

* <span data-ttu-id="5b11f-143">[Cache Redis di Azure]</span><span class="sxs-lookup"><span data-stu-id="5b11f-143">[Azure Redis Cache]</span></span>
* <span data-ttu-id="5b11f-144">[Documentazione di Cache Redis]</span><span class="sxs-lookup"><span data-stu-id="5b11f-144">[Redis Cache Documentation]</span></span>
* <span data-ttu-id="5b11f-145">[Prezzi di Cache Redis]</span><span class="sxs-lookup"><span data-stu-id="5b11f-145">[Redis Cache Pricing]</span></span>
* <span data-ttu-id="5b11f-146">[come tooconfigure Cache Redis di Azure]</span><span class="sxs-lookup"><span data-stu-id="5b11f-146">[How tooconfigure Azure Redis Cache]</span></span>

<!-- URL List -->

[Prezzi di Cache Redis]: https://azure.microsoft.com/pricing/details/cache/
[Cache Redis di Azure]: https://azure.microsoft.com/services/cache/
[Documentazione di Cache Redis]: ./redis-cache/index.md
[come tooconfigure Cache Redis di Azure]: ./redis-cache/cache-configure.md
[Sign In istruzioni per hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE02.png
