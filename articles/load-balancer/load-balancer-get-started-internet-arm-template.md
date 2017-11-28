---
title: bilanciamento del carico con una connessione Internet aaaCreate - modello di Azure | Documenti Microsoft
description: Informazioni su come una connessione Internet toocreate bilanciamento del carico in Gestione risorse di un modello
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: b24f4729-4559-4458-8527-71009d242647
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 2bce8cb87303838f3bc732d51228ab46d8015552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a><span data-ttu-id="54fd8-103">Creazione di un servizio di bilanciamento del carico Internet mediante l'uso di un modello</span><span class="sxs-lookup"><span data-stu-id="54fd8-103">Creating an Internet facing load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="54fd8-104">Portale</span><span class="sxs-lookup"><span data-stu-id="54fd8-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="54fd8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="54fd8-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="54fd8-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="54fd8-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="54fd8-107">Modello</span><span class="sxs-lookup"><span data-stu-id="54fd8-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="54fd8-108">Questo articolo descrive il modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="54fd8-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="54fd8-109">È anche possibile [informazioni su come una connessione Internet toocreate bilanciamento del carico utilizzando il modello di distribuzione classica](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="54fd8-109">You can also [Learn how toocreate an Internet facing load balancer using classic deployment model](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="54fd8-110">Distribuire il modello di hello utilizzando fare clic su toodeploy</span><span class="sxs-lookup"><span data-stu-id="54fd8-110">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="54fd8-111">modello di Hello esempio disponibile nel repository pubblico hello utilizza un file di parametro contenente hello predefiniti i valori utilizzati toogenerate hello lo scenario descritto sopra.</span><span class="sxs-lookup"><span data-stu-id="54fd8-111">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="54fd8-112">toodeploy questo modello utilizzando fare clic su toodeploy, seguire [questo collegamento](http://go.microsoft.com/fwlink/?LinkId=544801), fare clic su **distribuire tooAzure**, sostituire i valori di parametro predefiniti hello se necessario e seguire le istruzioni di hello nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="54fd8-112">toodeploy this template using click toodeploy, follow [this link](http://go.microsoft.com/fwlink/?LinkId=544801), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="54fd8-113">Distribuire il modello di hello tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="54fd8-113">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="54fd8-114">modello di hello toodeploy scaricato tramite PowerShell, seguire i passaggi di hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="54fd8-114">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="54fd8-115">Se non si è mai usato Azure PowerShell, vedere [come tooInstall e configurare Azure PowerShell](/powershell/azure/overview) e seguire le istruzioni di hello tutti hello modo toohello terminare toosign in Azure e selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="54fd8-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="54fd8-116">Eseguire hello **New AzureRmResourceGroupDeployment** toocreate cmdlet un gruppo di risorse utilizzando hello modello.</span><span class="sxs-lookup"><span data-stu-id="54fd8-116">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toocreate a resource group using hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="54fd8-117">Distribuire il modello di hello utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="54fd8-117">Deploy hello template by using hello Azure CLI</span></span>

<span data-ttu-id="54fd8-118">modello di hello toodeploy utilizzando hello CLI di Azure, seguire i passaggi di hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="54fd8-118">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="54fd8-119">Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="54fd8-119">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="54fd8-120">Eseguire hello **modalità di configurazione azure** tooswitch tooResource Manager modalità comando, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="54fd8-120">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="54fd8-121">Ecco l'output di hello previsto per comando hello sopra indicato:</span><span class="sxs-lookup"><span data-stu-id="54fd8-121">Here is hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="54fd8-122">Dal browser, passare troppo[hello modello delle Guide rapide](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copiare il contenuto di hello del file json hello e incollare in un nuovo file nel computer.</span><span class="sxs-lookup"><span data-stu-id="54fd8-122">From your browser, navigate too[hello Quickstart Template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copy hello contents of hello json file and paste into a new file in your computer.</span></span> <span data-ttu-id="54fd8-123">Per questo scenario, si sarebbero copiando i valori hello sotto tooa file denominato **c:\lb\azuredeploy.parameters.json**.</span><span class="sxs-lookup"><span data-stu-id="54fd8-123">For this scenario, you would be copying hello values below tooa file named **c:\lb\azuredeploy.parameters.json**.</span></span>
4. <span data-ttu-id="54fd8-124">Eseguire hello **distribuzione gruppo di azure creare** cmdlet toodeploy hello nuovo bilanciamento del carico utilizzando il modello di hello e parametro file scaricato e modificato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="54fd8-124">Run hello **azure group deployment create** cmdlet toodeploy hello new load balancer by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="54fd8-125">elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.</span><span class="sxs-lookup"><span data-stu-id="54fd8-125">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a><span data-ttu-id="54fd8-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="54fd8-126">Next steps</span></span>

[<span data-ttu-id="54fd8-127">Introduzione alla configurazione del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="54fd8-127">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="54fd8-128">Configurare una modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="54fd8-128">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="54fd8-129">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="54fd8-129">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
