---
title: "Procedura: Come distribuire un servizio Web in più aree | Documentazione Microsoft"
description: Procedura per distribuire (copiare) un nuovo servizio Web in altre aree.
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
ms.openlocfilehash: 3895537bbca72e687838ff5013c291dfee3be707
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-web-service-to-multiple-regions"></a><span data-ttu-id="66a84-103">Procedura: Come distribuire un servizio Web in più aree</span><span class="sxs-lookup"><span data-stu-id="66a84-103">How to deploy a Web Service to multiple regions</span></span>
<span data-ttu-id="66a84-104">I nuovi servizi Web di Azure consentono di distribuire facilmente un servizio Web in più aree, senza la necessità di più sottoscrizioni o aree di lavoro.</span><span class="sxs-lookup"><span data-stu-id="66a84-104">The New Azure Web Services allow you to easily deploy a web service to multiple regions without needing multiple subscriptions or workspaces.</span></span> 

<span data-ttu-id="66a84-105">I prezzi sono specifici per ogni area. È quindi necessario definire un piano di fatturazione per ogni area in cui verrà distribuito il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="66a84-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy the web service.</span></span>

## <a name="to-create-a-plan-in-another-region"></a><span data-ttu-id="66a84-106">Per creare un piano in un'altra area</span><span class="sxs-lookup"><span data-stu-id="66a84-106">To create a plan in another region</span></span>
1. <span data-ttu-id="66a84-107">Accedere a [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/)(Servizi Web Microsoft Azure Machine Learning).</span><span class="sxs-lookup"><span data-stu-id="66a84-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span></span>
2. <span data-ttu-id="66a84-108">Fare clic sull'opzione del menu **Plans** (Piani).</span><span class="sxs-lookup"><span data-stu-id="66a84-108">Click the **Plans** menu option.</span></span>
3. <span data-ttu-id="66a84-109">Nella pagina della panoramica Plans (Piani), fare clic su **New**(Nuovo).</span><span class="sxs-lookup"><span data-stu-id="66a84-109">On the Plans over view page, click **New**.</span></span>
4. <span data-ttu-id="66a84-110">Nell'elenco a discesa **Subscription** (Sottoscrizione) selezionare la sottoscrizione in cui risiederà il nuovo piano.</span><span class="sxs-lookup"><span data-stu-id="66a84-110">From the **Subscription** dropdown, select the subscription in which the new plan will reside.</span></span>
5. <span data-ttu-id="66a84-111">Nell'elenco a discesa **Regione** (Area) selezionare un'area per il nuovo piano.</span><span class="sxs-lookup"><span data-stu-id="66a84-111">From the **Region** dropdown, select a region for the new plan.</span></span> <span data-ttu-id="66a84-112">Le opzioni del piano per l'area selezionata verranno visualizzate nella sezione **Plan Options** (Opzioni del piano) della pagina.</span><span class="sxs-lookup"><span data-stu-id="66a84-112">The Plan Options for the selected region will display in the **Plan Options** section of the page.</span></span>
6. <span data-ttu-id="66a84-113">Nell'elenco a discesa **Resource Group** (Gruppo di risorse) selezionare un gruppo di risorse per il piano.</span><span class="sxs-lookup"><span data-stu-id="66a84-113">From the **Resource Group** dropdown, select a resource group for the plan.</span></span> <span data-ttu-id="66a84-114">Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="66a84-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
7. <span data-ttu-id="66a84-115">In **Plan Name** (Nome piano) digitare il nome del piano.</span><span class="sxs-lookup"><span data-stu-id="66a84-115">In **Plan Name** type the name of the plan.</span></span>
8. <span data-ttu-id="66a84-116">In **Plan Options**(Opzioni piano) selezionare il livello di fatturazione per il nuovo piano.</span><span class="sxs-lookup"><span data-stu-id="66a84-116">Under **Plan Options**, click the billing level for the new plan.</span></span>
9. <span data-ttu-id="66a84-117">Fare clic su **Create**.</span><span class="sxs-lookup"><span data-stu-id="66a84-117">Click **Create**.</span></span>

## <a name="deploying-the-web-service-to-another-region"></a><span data-ttu-id="66a84-118">Distribuzione di un servizio Web in un'altra area</span><span class="sxs-lookup"><span data-stu-id="66a84-118">Deploying the web service to another region</span></span>
1. <span data-ttu-id="66a84-119">Fare clic sull'opzione del menu **Web Services** (Servizi Web).</span><span class="sxs-lookup"><span data-stu-id="66a84-119">Click the **Web Services** menu option.</span></span>
2. <span data-ttu-id="66a84-120">Selezionare il servizio Web da distribuire in una nuova area.</span><span class="sxs-lookup"><span data-stu-id="66a84-120">Select the Web Service you are deploying to a new region.</span></span>
3. <span data-ttu-id="66a84-121">Fare clic su **Copy**.</span><span class="sxs-lookup"><span data-stu-id="66a84-121">Click **Copy**.</span></span>
4. <span data-ttu-id="66a84-122">In **Web Service Name**(Nome servizio Web) digitare un nuovo nome per il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="66a84-122">In **Web Service Name**, type a new name for the web service.</span></span>
5. <span data-ttu-id="66a84-123">In **Web service description**(Descrizione servizio Web) immettere una descrizione per il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="66a84-123">In **Web service description**, type a description for the web service.</span></span>
6. <span data-ttu-id="66a84-124">Nell'elenco a discesa **Subscription** (Sottoscrizione) selezionare la sottoscrizione in cui risiederà il nuovo servizio Web.</span><span class="sxs-lookup"><span data-stu-id="66a84-124">From the **Subscription** dropdown, select the subscription in which the new web service will reside.</span></span>
7. <span data-ttu-id="66a84-125">Nell'elenco a discesa **Resource Group** (Gruppo di risorse) selezionare un gruppo di risorse per il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="66a84-125">From the **Resource Group** dropdown, select a resource group for the web service.</span></span> <span data-ttu-id="66a84-126">Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="66a84-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="66a84-127">Nell'elenco a discesa **Region** (Area) selezionare l'area in cui si desidera distribuire il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="66a84-127">From the **Region** dropdown, select the region in which to deploy the web service.</span></span>
9. <span data-ttu-id="66a84-128">Nell'elenco a discesa **Storage account** (Account di archiviazione) selezionare un account di archiviazione in cui archiviare il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="66a84-128">From the **Storage account** dropdown, select a storage account in which to store the web service.</span></span>
10. <span data-ttu-id="66a84-129">Nell'elenco a discesa **Price Plan** (Piano tariffario) selezionare un piano nell'area scelta nel passaggio 8.</span><span class="sxs-lookup"><span data-stu-id="66a84-129">From the **Price Plan** dropdown, select a plan in the region you selected in step 8.</span></span>
11. <span data-ttu-id="66a84-130">Fare clic su **Copy**.</span><span class="sxs-lookup"><span data-stu-id="66a84-130">Click **Copy**.</span></span>

