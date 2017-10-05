---
title: Creare un servizio di bilanciamento del carico interno - Modello di Azure | Documentazione Microsoft
description: Informazioni su come creare un servizio di bilanciamento del carico interno in Gestione risorse con un modello
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 64150862-6ced-42de-85dc-89d323257d7c
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 5e0278cf5c605298932d6ac55d147a1c43fd9d23
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a><span data-ttu-id="1a037-103">Creare un servizio di bilanciamento del carico interno usando un modello</span><span class="sxs-lookup"><span data-stu-id="1a037-103">Create an internal load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1a037-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1a037-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="1a037-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1a037-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="1a037-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="1a037-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="1a037-107">Modello</span><span class="sxs-lookup"><span data-stu-id="1a037-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="1a037-108">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1a037-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="1a037-109">Questo articolo illustra il modello di distribuzione Resource Manager che Microsoft consiglia di usare per le distribuzioni più recenti in sostituzione del [modello di distribuzione classica](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="1a037-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="1a037-110">Distribuire il modello tramite clic per la distribuzione</span><span class="sxs-lookup"><span data-stu-id="1a037-110">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="1a037-111">Il modello di esempio disponibile nel repository pubblico usa un file di parametro che contiene i valori predefiniti usati per generare lo scenario descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a037-111">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="1a037-112">Distribuire [questo modello](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer)tramite clic per la distribuzione, fare clic su **Distribuisci in Azure**, sostituire i valori del parametro predefinito se necessario e seguire le istruzioni nel portale.</span><span class="sxs-lookup"><span data-stu-id="1a037-112">To deploy this template using click to deploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="1a037-113">Distribuire il modello tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="1a037-113">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="1a037-114">Per distribuire il modello scaricato tramite PowerShell, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="1a037-114">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="1a037-115">Se è la prima volta che si utilizza Azure PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview) e seguire le istruzioni fino al termine della procedura per accedere ad Azure e selezionare la sottoscrizione desiderata.</span><span class="sxs-lookup"><span data-stu-id="1a037-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="1a037-116">Scaricare il file dei parametri sul disco locale.</span><span class="sxs-lookup"><span data-stu-id="1a037-116">Download the parameters file to your local disk.</span></span>
3. <span data-ttu-id="1a037-117">Modificare il file e salvarlo.</span><span class="sxs-lookup"><span data-stu-id="1a037-117">Edit the file and save it.</span></span>
4. <span data-ttu-id="1a037-118">Per creare un gruppo di risorse usando il modello, eseguire il cmdlet **New-AzureRmResourceGroupDeployment** .</span><span class="sxs-lookup"><span data-stu-id="1a037-118">Run the **New-AzureRmResourceGroupDeployment** cmdlet to create a resource group using the template.</span></span>

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="1a037-119">Distribuire il modello tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="1a037-119">Deploy the template by using the Azure CLI</span></span>

<span data-ttu-id="1a037-120">Per distribuire il modello tramite l'interfaccia della riga di comando di Azure, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="1a037-120">To deploy the template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="1a037-121">Se l'interfaccia della riga di comando di Azure non è mai stata usata, vedere [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md) e seguire le istruzioni fino al punto in cui si selezionano l'account e la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1a037-121">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="1a037-122">Eseguire il comando **azure config mode** per passare alla modalità Gestione risorse, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1a037-122">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="1a037-123">Di seguito è riportato l'output previsto per il comando precedente:</span><span class="sxs-lookup"><span data-stu-id="1a037-123">Here is the expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="1a037-124">Aprire il file dei parametri, selezionare i relativi contenuti e salvarlo in un file nel computer.</span><span class="sxs-lookup"><span data-stu-id="1a037-124">Open the parameter file, select its contents, and save it to a file in your computer.</span></span> <span data-ttu-id="1a037-125">In questo esempio il file dei parametri è stato salvato in *parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="1a037-125">For this example, we saved the parameters file to *parameters.json*.</span></span>
4. <span data-ttu-id="1a037-126">Eseguire il cmdlet **azure group deployment create** per distribuire il nuovo servizio di bilanciamento del carico usando i file di modello e dei parametri scaricati e modificati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a037-126">Run the **azure group deployment create** command to deploy the new internal load balancer by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="1a037-127">Nell'elenco riportato dopo l'output sono indicati i parametri usati.</span><span class="sxs-lookup"><span data-stu-id="1a037-127">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a><span data-ttu-id="1a037-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1a037-128">Next steps</span></span>

[<span data-ttu-id="1a037-129">Configurare una modalità di distribuzione del servizio di bilanciamento del carico utilizzando l’affinità dell’IP di origine</span><span class="sxs-lookup"><span data-stu-id="1a037-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="1a037-130">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="1a037-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

