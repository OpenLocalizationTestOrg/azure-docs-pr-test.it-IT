---
title: aaaHow toodeploy un servizio Web aree toomultiple | Documenti Microsoft
description: Passaggi toodeploy (copia) le aree tooother un nuovo servizio Web.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 21fcdb96f118c60ed98b60b1b2df833766c7c8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-web-service-toomultiple-regions"></a><span data-ttu-id="8da84-103">Come un servizio Web toodeploy toomultiple aree</span><span class="sxs-lookup"><span data-stu-id="8da84-103">How toodeploy a Web Service toomultiple regions</span></span>
<span data-ttu-id="8da84-104">Hello nuovi servizi Web di Azure consentono di tooeasily distribuire un toomultiple le aree del servizio web senza la necessità di più sottoscrizioni o aree di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8da84-104">hello New Azure Web Services allow you tooeasily deploy a web service toomultiple regions without needing multiple subscriptions or workspaces.</span></span> 

<span data-ttu-id="8da84-105">I prezzi sono specifico, che pertanto è necessario definire un piano di fatturazione per ogni area in cui verranno distribuiti servizio web hello dell'area.</span><span class="sxs-lookup"><span data-stu-id="8da84-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy hello web service.</span></span>

## <a name="toocreate-a-plan-in-another-region"></a><span data-ttu-id="8da84-106">un piano in un'altra area toocreate</span><span class="sxs-lookup"><span data-stu-id="8da84-106">toocreate a plan in another region</span></span>
1. <span data-ttu-id="8da84-107">Accedere a [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/)(Servizi Web Microsoft Azure Machine Learning).</span><span class="sxs-lookup"><span data-stu-id="8da84-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span></span>
2. <span data-ttu-id="8da84-108">Fare clic su hello **piani** opzione di menu.</span><span class="sxs-lookup"><span data-stu-id="8da84-108">Click hello **Plans** menu option.</span></span>
3. <span data-ttu-id="8da84-109">Nei piani di hello sulla pagina di visualizzazione, fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="8da84-109">On hello Plans over view page, click **New**.</span></span>
4. <span data-ttu-id="8da84-110">Da hello **sottoscrizione** sottoscrizione selezionare hello in cui hello risiederà nuovo piano di elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="8da84-110">From hello **Subscription** dropdown, select hello subscription in which hello new plan will reside.</span></span>
5. <span data-ttu-id="8da84-111">Da hello **area** elenco a discesa, selezionare un'area per il nuovo piano di hello.</span><span class="sxs-lookup"><span data-stu-id="8da84-111">From hello **Region** dropdown, select a region for hello new plan.</span></span> <span data-ttu-id="8da84-112">opzioni relative al piano di Hello per area selezionata hello visualizzerà in hello **opzioni relative al piano** sezione della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="8da84-112">hello Plan Options for hello selected region will display in hello **Plan Options** section of hello page.</span></span>
6. <span data-ttu-id="8da84-113">Da hello **gruppo di risorse** elenco a discesa Seleziona una risorsa di gruppo per il piano di hello.</span><span class="sxs-lookup"><span data-stu-id="8da84-113">From hello **Resource Group** dropdown, select a resource group for hello plan.</span></span> <span data-ttu-id="8da84-114">Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8da84-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
7. <span data-ttu-id="8da84-115">In **nome piano** nome hello del tipo di piano hello.</span><span class="sxs-lookup"><span data-stu-id="8da84-115">In **Plan Name** type hello name of hello plan.</span></span>
8. <span data-ttu-id="8da84-116">In **opzioni del piano**, fare clic su hello livello fatturazione per il nuovo piano di hello.</span><span class="sxs-lookup"><span data-stu-id="8da84-116">Under **Plan Options**, click hello billing level for hello new plan.</span></span>
9. <span data-ttu-id="8da84-117">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8da84-117">Click **Create**.</span></span>

## <a name="deploying-hello-web-service-tooanother-region"></a><span data-ttu-id="8da84-118">Distribuzione di hello web servizio tooanother area</span><span class="sxs-lookup"><span data-stu-id="8da84-118">Deploying hello web service tooanother region</span></span>
1. <span data-ttu-id="8da84-119">Fare clic su hello **servizi Web** opzione di menu.</span><span class="sxs-lookup"><span data-stu-id="8da84-119">Click hello **Web Services** menu option.</span></span>
2. <span data-ttu-id="8da84-120">Selezionare servizio Web si sta distribuendo tooa nuova area hello.</span><span class="sxs-lookup"><span data-stu-id="8da84-120">Select hello Web Service you are deploying tooa new region.</span></span>
3. <span data-ttu-id="8da84-121">Fare clic su **Copy**.</span><span class="sxs-lookup"><span data-stu-id="8da84-121">Click **Copy**.</span></span>
4. <span data-ttu-id="8da84-122">In **nome del servizio Web**, digitare un nuovo nome per il servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="8da84-122">In **Web Service Name**, type a new name for hello web service.</span></span>
5. <span data-ttu-id="8da84-123">In **descrizione servizio Web**, digitare una descrizione per il servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="8da84-123">In **Web service description**, type a description for hello web service.</span></span>
6. <span data-ttu-id="8da84-124">Da hello **sottoscrizione** sottoscrizione selezionare hello in cui hello risiederà nuovo servizio web dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="8da84-124">From hello **Subscription** dropdown, select hello subscription in which hello new web service will reside.</span></span>
7. <span data-ttu-id="8da84-125">Da hello **gruppo di risorse** elenco a discesa Seleziona una risorsa di gruppo per il servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="8da84-125">From hello **Resource Group** dropdown, select a resource group for hello web service.</span></span> <span data-ttu-id="8da84-126">Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8da84-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="8da84-127">Da hello **area** area hello selezionare nel servizio web hello toodeploy elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="8da84-127">From hello **Region** dropdown, select hello region in which toodeploy hello web service.</span></span>
9. <span data-ttu-id="8da84-128">Da hello **account di archiviazione** elenco a discesa, seleziona un account di archiviazione in cui hello toostore servizio web.</span><span class="sxs-lookup"><span data-stu-id="8da84-128">From hello **Storage account** dropdown, select a storage account in which toostore hello web service.</span></span>
10. <span data-ttu-id="8da84-129">Da hello **prezzo piano** elenco a discesa, selezionare un piano nell'area di hello selezionato nel passaggio 8.</span><span class="sxs-lookup"><span data-stu-id="8da84-129">From hello **Price Plan** dropdown, select a plan in hello region you selected in step 8.</span></span>
11. <span data-ttu-id="8da84-130">Fare clic su **Copy**.</span><span class="sxs-lookup"><span data-stu-id="8da84-130">Click **Copy**.</span></span>

