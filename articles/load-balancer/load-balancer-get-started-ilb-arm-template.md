---
title: aaaCreate un bilanciamento del carico interno - modello di Azure | Documenti Microsoft
description: Informazioni su come toocreate un interno bilanciamento del carico utilizzando un modello di gestione risorse
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
ms.openlocfilehash: 3ffa8178b863367cd79e2bc2b7ce4e45b23267e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a><span data-ttu-id="02aa2-103">Creare un servizio di bilanciamento del carico interno usando un modello</span><span class="sxs-lookup"><span data-stu-id="02aa2-103">Create an internal load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="02aa2-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="02aa2-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="02aa2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="02aa2-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="02aa2-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="02aa2-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="02aa2-107">Modello</span><span class="sxs-lookup"><span data-stu-id="02aa2-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="02aa2-108">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="02aa2-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="02aa2-109">In questo articolo viene illustrato l'utilizzo modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché hello [modello di distribuzione classica](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="02aa2-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="02aa2-110">Distribuire il modello di hello utilizzando fare clic su toodeploy</span><span class="sxs-lookup"><span data-stu-id="02aa2-110">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="02aa2-111">modello di Hello esempio disponibile nel repository pubblico hello utilizza un file di parametro contenente hello predefiniti i valori utilizzati toogenerate hello lo scenario descritto sopra.</span><span class="sxs-lookup"><span data-stu-id="02aa2-111">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="02aa2-112">toodeploy questo modello utilizzando fare clic su toodeploy, seguire [questo collegamento](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), fare clic su **distribuire tooAzure**, sostituire i valori di parametro predefiniti hello se necessario e seguire le istruzioni di hello nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="02aa2-112">toodeploy this template using click toodeploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="02aa2-113">Distribuire il modello di hello tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="02aa2-113">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="02aa2-114">modello di hello toodeploy scaricato tramite PowerShell, seguire i passaggi di hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="02aa2-114">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="02aa2-115">Se non si è mai usato Azure PowerShell, vedere [come tooInstall e configurare Azure PowerShell](/powershell/azure/overview) e seguire le istruzioni di hello tutti hello modo toohello terminare toosign in Azure e selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="02aa2-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="02aa2-116">Scaricare disco locale tooyour hello parametri file.</span><span class="sxs-lookup"><span data-stu-id="02aa2-116">Download hello parameters file tooyour local disk.</span></span>
3. <span data-ttu-id="02aa2-117">Modificare il file hello e salvarlo.</span><span class="sxs-lookup"><span data-stu-id="02aa2-117">Edit hello file and save it.</span></span>
4. <span data-ttu-id="02aa2-118">Eseguire hello **New AzureRmResourceGroupDeployment** toocreate cmdlet un gruppo di risorse utilizzando hello modello.</span><span class="sxs-lookup"><span data-stu-id="02aa2-118">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toocreate a resource group using hello template.</span></span>

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="02aa2-119">Distribuire il modello di hello utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="02aa2-119">Deploy hello template by using hello Azure CLI</span></span>

<span data-ttu-id="02aa2-120">modello di hello toodeploy utilizzando hello CLI di Azure, seguire i passaggi di hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="02aa2-120">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="02aa2-121">Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="02aa2-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="02aa2-122">Eseguire hello **modalità di configurazione azure** tooswitch tooResource Manager modalità comando, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="02aa2-122">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="02aa2-123">Ecco l'output di hello previsto per comando hello sopra indicato:</span><span class="sxs-lookup"><span data-stu-id="02aa2-123">Here is hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="02aa2-124">Aprire il file di parametro hello, selezionare il contenuto e salvarlo tooa file nel computer.</span><span class="sxs-lookup"><span data-stu-id="02aa2-124">Open hello parameter file, select its contents, and save it tooa file in your computer.</span></span> <span data-ttu-id="02aa2-125">Per questo esempio, sono stati salvati i file di parametri hello troppo*parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="02aa2-125">For this example, we saved hello parameters file too*parameters.json*.</span></span>
4. <span data-ttu-id="02aa2-126">Eseguire hello **distribuzione gruppo di azure creare** toodeploy hello nuovo bilanciamento del carico interno utilizzando il modello di hello e parametro di comando file scaricato e modificato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="02aa2-126">Run hello **azure group deployment create** command toodeploy hello new internal load balancer by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="02aa2-127">elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.</span><span class="sxs-lookup"><span data-stu-id="02aa2-127">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a><span data-ttu-id="02aa2-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="02aa2-128">Next steps</span></span>

[<span data-ttu-id="02aa2-129">Configurare una modalità di distribuzione del servizio di bilanciamento del carico utilizzando l’affinità dell’IP di origine</span><span class="sxs-lookup"><span data-stu-id="02aa2-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="02aa2-130">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="02aa2-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

