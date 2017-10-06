---
title: un server Analysis Services in Azure aaaCreate | Documenti Microsoft
description: Informazioni su come istanza di un server Analysis Services toocreate in Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a><span data-ttu-id="b65a1-103">Creare un server Azure Analysis Services nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b65a1-103">Create an Azure Analysis Services server in Azure portal</span></span>
<span data-ttu-id="b65a1-104">Questo articolo illustra la creazione di una risorsa server Analysis Services nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b65a1-104">This article walks you through creating an Analysis Services server resource in your Azure subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b65a1-105">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="b65a1-105">Before you begin</span></span>
<span data-ttu-id="b65a1-106">toocomplete questa Guida rapida, è necessario:</span><span class="sxs-lookup"><span data-stu-id="b65a1-106">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="b65a1-107">**Sottoscrizione di Azure**: visitare [versione di valutazione gratuita di Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate un account.</span><span class="sxs-lookup"><span data-stu-id="b65a1-107">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="b65a1-108">**Azure Active Directory**: la sottoscrizione deve essere associata a un tenant Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b65a1-108">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant.</span></span> <span data-ttu-id="b65a1-109">E, è necessario toobe connessi tooAzure con un account in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b65a1-109">And, you need toobe signed in tooAzure with an account in that Azure Active Directory.</span></span> <span data-ttu-id="b65a1-110">Gli account Microsoft non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="b65a1-110">Microsoft accounts are not supported.</span></span> <span data-ttu-id="b65a1-111">vedere, più toolearn [l'autenticazione e le autorizzazioni utente](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="b65a1-111">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>
* <span data-ttu-id="b65a1-112">**Gruppo di risorse**: usare un gruppo di risorse già esistente o [crearne uno nuovo](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b65a1-112">**Resource group**: Use a resource group you already have or [create a new one](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b65a1-113">La creazione di un server può avere come risultato un nuovo servizio fatturabile.</span><span class="sxs-lookup"><span data-stu-id="b65a1-113">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="b65a1-114">vedere, più toolearn [dei prezzi di Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="b65a1-114">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a><span data-ttu-id="b65a1-115">toocreate un server nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b65a1-115">toocreate a server in Azure portal</span></span>
1. <span data-ttu-id="b65a1-116">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b65a1-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="b65a1-117">Fare clic su **+ Nuovo** > **Dati e analisi** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="b65a1-117">Click **+ New** > **Data + analytics** > **Analysis Services**.</span></span>
3. <span data-ttu-id="b65a1-118">In hello **Analysis Services** pannello, compilare i campi di hello necessarie e quindi premere **crea**.</span><span class="sxs-lookup"><span data-stu-id="b65a1-118">In hello **Analysis Services** blade, fill in hello required fields, and then press **Create**.</span></span>
   
    ![Creazione del server](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * <span data-ttu-id="b65a1-120">**Nome del server**: tipo di server di hello tooreference un nome univoco utilizzato.</span><span class="sxs-lookup"><span data-stu-id="b65a1-120">**Server name**: Type a unique name used tooreference hello server.</span></span>
   * <span data-ttu-id="b65a1-121">**Sottoscrizione**: selezionare questo server attivi per sottoscrizione di hello.</span><span class="sxs-lookup"><span data-stu-id="b65a1-121">**Subscription**: Select hello subscription this server bills to.</span></span>
   * <span data-ttu-id="b65a1-122">**Gruppo di risorse**: questi contenitori fanno toohelp progettato gestire una raccolta di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b65a1-122">**Resource group**: These containers are designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="b65a1-123">vedere, più toolearn [gruppi di risorse](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b65a1-123">toolearn more, see [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="b65a1-124">**Percorso**: hello di host posizione Data Center di Azure questo server.</span><span class="sxs-lookup"><span data-stu-id="b65a1-124">**Location**: This Azure datacenter location hosts hello server.</span></span> <span data-ttu-id="b65a1-125">Selezionare una località vicina alla base di utenti più estesa.</span><span class="sxs-lookup"><span data-stu-id="b65a1-125">Choose a location nearest your largest user base.</span></span>
   * <span data-ttu-id="b65a1-126">**Piano tariffario**: selezionare un piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="b65a1-126">**Pricing tier**: Select a pricing tier.</span></span> <span data-ttu-id="b65a1-127">Sono supportati i modelli tabulari too400 GB.</span><span class="sxs-lookup"><span data-stu-id="b65a1-127">Tabular models up too400 GB are supported.</span></span> <span data-ttu-id="b65a1-128">vedere, più toolearn [dei prezzi di Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="b65a1-128">toolearn more, see [Azure Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
4. <span data-ttu-id="b65a1-129">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b65a1-129">Click **Create**.</span></span>

<span data-ttu-id="b65a1-130">La creazione richiede in genere meno di un minuto e spesso solo alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="b65a1-130">Create usually takes under a minute; often just a few seconds.</span></span> <span data-ttu-id="b65a1-131">Se si seleziona **aggiungere tooPortal**, passare toosee portale tooyour il nuovo server.</span><span class="sxs-lookup"><span data-stu-id="b65a1-131">If you selected **Add tooPortal**, navigate tooyour portal toosee your new server.</span></span> <span data-ttu-id="b65a1-132">In alternativa, passare troppo**più servizi** > **Analysis Services** toosee se il server è pronto.</span><span class="sxs-lookup"><span data-stu-id="b65a1-132">Or, navigate too**More services** > **Analysis Services** toosee if your server is ready.</span></span>

 ![Dashboard](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a><span data-ttu-id="b65a1-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b65a1-134">Next steps</span></span>
<span data-ttu-id="b65a1-135">Dopo aver creato il server, è possibile [distribuire un modello](analysis-services-deploy.md) tooit mediante SSDT o con SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="b65a1-135">Once you've created your server, you can [deploy a model](analysis-services-deploy.md) tooit by using SSDT or with SSMS.</span></span>

<span data-ttu-id="b65a1-136">Se un modello di distribuzione tooyour server si connette a origini dati locali tooon, è necessario tooinstall un [gateway dati locale](analysis-services-gateway.md) in un computer nella rete.</span><span class="sxs-lookup"><span data-stu-id="b65a1-136">If a model you deploy tooyour server connects tooon-premises data sources, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md) on a computer in your network.</span></span>

