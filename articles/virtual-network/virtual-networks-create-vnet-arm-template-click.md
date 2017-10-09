---
title: aaaCreate una rete virtuale | Modello di gestione risorse di Azure | Documenti Microsoft
description: Informazioni su come toocreate un virtuale di rete utilizzando un modello di gestione risorse di Azure.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 69530861-2f97-4a6e-b336-a7baf2690044
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b9c289433ff2a84bec19eac25fa28ab40d131c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a><span data-ttu-id="e8dda-103">Creare una rete virtuale usando un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e8dda-103">Create a virtual network using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="e8dda-104">Azure offre due modelli di distribuzione, ovvero Azure Resource Manager e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="e8dda-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="e8dda-105">Si consiglia di creare risorse modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="e8dda-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="e8dda-106">altre informazioni sulle toolearn hello le differenze tra hello due modelli, leggere hello [modelli di distribuzione Azure comprendere](../azure-resource-manager/resource-manager-deployment-model.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="e8dda-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="e8dda-107">In questo articolo viene illustrato come una rete virtuale tramite la distribuzione di gestione risorse di hello toocreate modello utilizzando un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="e8dda-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using an Azure Resource Manager template.</span></span> <span data-ttu-id="e8dda-108">È anche possibile creare una rete virtuale tramite Gestione risorse di usare altri strumenti o creare una rete virtuale tramite il modello di distribuzione classica hello selezionando un'opzione diversa da hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="e8dda-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
- [<span data-ttu-id="e8dda-109">Portale</span><span class="sxs-lookup"><span data-stu-id="e8dda-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
- [<span data-ttu-id="e8dda-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8dda-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
- [<span data-ttu-id="e8dda-111">CLI</span><span class="sxs-lookup"><span data-stu-id="e8dda-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
- [<span data-ttu-id="e8dda-112">Modello</span><span class="sxs-lookup"><span data-stu-id="e8dda-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
- [<span data-ttu-id="e8dda-113">Portale (versione classica)</span><span class="sxs-lookup"><span data-stu-id="e8dda-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
- [<span data-ttu-id="e8dda-114">PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="e8dda-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [<span data-ttu-id="e8dda-115">Interfaccia della riga di comando (versione classica)</span><span class="sxs-lookup"><span data-stu-id="e8dda-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

<span data-ttu-id="e8dda-116">Si apprenderà come toodownload e modificare esistente modello ARM da GitHub e distribuire il modello di hello da GitHub, PowerShell e hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="e8dda-116">You will learn how toodownload and modify and existing ARM template from GitHub, and deploy hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="e8dda-117">Se si distribuisce il modello ARM hello direttamente da GitHub, senza alcuna modifica, semplicemente ignorare troppo[distribuire un modello da github](#deploy-the-arm-template-by-using-click-to-deploy).</span><span class="sxs-lookup"><span data-stu-id="e8dda-117">If you are simply deploying hello ARM template directly from GitHub, without any changes, skip too[deploy a template from github](#deploy-the-arm-template-by-using-click-to-deploy).</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="e8dda-118">Scaricare e comprendere il modello di Azure Resource Manager hello</span><span class="sxs-lookup"><span data-stu-id="e8dda-118">Download and understand hello Azure Resource Manager template</span></span>
<span data-ttu-id="e8dda-119">È possibile scaricare hello modello esistente per la creazione di una rete virtuale e due subnet da GitHub, apportare le modifiche potrebbe essere necessario e riutilizzarlo.</span><span class="sxs-lookup"><span data-stu-id="e8dda-119">You can download hello existing template for creating a VNet and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="e8dda-120">toodo in tal caso, completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e8dda-120">toodo so, complete hello following steps:</span></span>

1. <span data-ttu-id="e8dda-121">Passare troppo[pagina modello di esempio hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="e8dda-121">Navigate too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="e8dda-122">Fare clic su **azuredeploy.json**, quindi fare clic su **RAW**.</span><span class="sxs-lookup"><span data-stu-id="e8dda-122">Click **azuredeploy.json**, and then click **RAW**.</span></span>
3. <span data-ttu-id="e8dda-123">Salvare tooa file hello una cartella locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="e8dda-123">Save hello file tooa a local folder on your computer.</span></span>
4. <span data-ttu-id="e8dda-124">Se si ha familiarità con i modelli, è possibile ignorare toostep 7.</span><span class="sxs-lookup"><span data-stu-id="e8dda-124">If you are familiar with templates, skip toostep 7.</span></span>
5. <span data-ttu-id="e8dda-125">Aprire file hello appena salvato e osservare il contenuto di hello in **parametri** nella riga 5.</span><span class="sxs-lookup"><span data-stu-id="e8dda-125">Open hello file you just saved and look at hello contents under **parameters** in line 5.</span></span> <span data-ttu-id="e8dda-126">I parametri del modello ARM costituiscono un segnaposto per i valori che possono essere compilati durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e8dda-126">ARM template parameters provide a placeholder for values that can be filled out during deployment.</span></span>
   
   | <span data-ttu-id="e8dda-127">Parametro</span><span class="sxs-lookup"><span data-stu-id="e8dda-127">Parameter</span></span> | <span data-ttu-id="e8dda-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e8dda-128">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="e8dda-129">**location**</span><span class="sxs-lookup"><span data-stu-id="e8dda-129">**location**</span></span> |<span data-ttu-id="e8dda-130">Area in cui verrà creato hello rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="e8dda-130">Azure region where hello VNet will be created</span></span> |
   | <span data-ttu-id="e8dda-131">**vnetName**</span><span class="sxs-lookup"><span data-stu-id="e8dda-131">**vnetName**</span></span> |<span data-ttu-id="e8dda-132">Nome per hello nuova rete virtuale</span><span class="sxs-lookup"><span data-stu-id="e8dda-132">Name for hello new VNet</span></span> |
   | <span data-ttu-id="e8dda-133">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="e8dda-133">**addressPrefix**</span></span> |<span data-ttu-id="e8dda-134">Spazio di indirizzi per hello rete virtuale, nel formato CIDR</span><span class="sxs-lookup"><span data-stu-id="e8dda-134">Address space for hello VNet, in CIDR format</span></span> |
   | <span data-ttu-id="e8dda-135">**subnet1Name**</span><span class="sxs-lookup"><span data-stu-id="e8dda-135">**subnet1Name**</span></span> |<span data-ttu-id="e8dda-136">Nome per hello prima rete virtuale</span><span class="sxs-lookup"><span data-stu-id="e8dda-136">Name for hello first VNet</span></span> |
   | <span data-ttu-id="e8dda-137">**subnet1Prefix**</span><span class="sxs-lookup"><span data-stu-id="e8dda-137">**subnet1Prefix**</span></span> |<span data-ttu-id="e8dda-138">Blocco CIDR per la prima subnet hello</span><span class="sxs-lookup"><span data-stu-id="e8dda-138">CIDR block for hello first subnet</span></span> |
   | <span data-ttu-id="e8dda-139">**subnet2Name**</span><span class="sxs-lookup"><span data-stu-id="e8dda-139">**subnet2Name**</span></span> |<span data-ttu-id="e8dda-140">Nome per hello seconda rete virtuale</span><span class="sxs-lookup"><span data-stu-id="e8dda-140">Name for hello second VNet</span></span> |
   | <span data-ttu-id="e8dda-141">**subnet2Prefix**</span><span class="sxs-lookup"><span data-stu-id="e8dda-141">**subnet2Prefix**</span></span> |<span data-ttu-id="e8dda-142">Blocco CIDR per subnet secondo hello</span><span class="sxs-lookup"><span data-stu-id="e8dda-142">CIDR block for hello second subnet</span></span> |
   
   > [!IMPORTANT]
   > <span data-ttu-id="e8dda-143">I modelli di Gestione risorse di Azure conservati in GitHub possono cambiare nel tempo.</span><span class="sxs-lookup"><span data-stu-id="e8dda-143">Azure Resource Manager templates maintained in GitHub can change over time.</span></span> <span data-ttu-id="e8dda-144">Accertarsi di controllare il modello di hello prima di utilizzarlo.</span><span class="sxs-lookup"><span data-stu-id="e8dda-144">Make sure you check hello template before using it.</span></span>
   > 
   > 
6. <span data-ttu-id="e8dda-145">Controllare il contenuto hello **risorse** e osservare l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="e8dda-145">Check hello content under **resources** and notice hello following:</span></span>
   
   * <span data-ttu-id="e8dda-146">**type**.</span><span class="sxs-lookup"><span data-stu-id="e8dda-146">**type**.</span></span> <span data-ttu-id="e8dda-147">Tipo di risorsa viene creato dal modello hello.</span><span class="sxs-lookup"><span data-stu-id="e8dda-147">Type of resource being created by hello template.</span></span> <span data-ttu-id="e8dda-148">In questo caso, **Microsoft.Network/virtualNetworks**, che rappresenta una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e8dda-148">In this case, **Microsoft.Network/virtualNetworks**, which represent a VNet.</span></span>
   * <span data-ttu-id="e8dda-149">**name**.</span><span class="sxs-lookup"><span data-stu-id="e8dda-149">**name**.</span></span> <span data-ttu-id="e8dda-150">Nome per la risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="e8dda-150">Name for hello resource.</span></span> <span data-ttu-id="e8dda-151">Avviso hello utilizzo di **[parameters('vnetName')]**, che significa hello verrà nome fornito come input utente hello o un file dei parametri durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e8dda-151">Notice hello use of **[parameters('vnetName')]**, which means hello name will provided as input by hello user or a parameter file during deployment.</span></span>
   * <span data-ttu-id="e8dda-152">**properties**.</span><span class="sxs-lookup"><span data-stu-id="e8dda-152">**properties**.</span></span> <span data-ttu-id="e8dda-153">Elenco di proprietà per la risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="e8dda-153">List of properties for hello resource.</span></span> <span data-ttu-id="e8dda-154">Questo modello Usa proprietà spazio e la subnet dell'indirizzo hello durante la creazione della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e8dda-154">This template uses hello address space and subnet properties during VNet creation.</span></span>
7. <span data-ttu-id="e8dda-155">Passare troppo[pagina modello di esempio hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="e8dda-155">Navigate back too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
8. <span data-ttu-id="e8dda-156">Fare clic su **azuredeploy-parameters.json** e quindi su **RAW**.</span><span class="sxs-lookup"><span data-stu-id="e8dda-156">Click **azuredeploy-paremeters.json**, and then click **RAW**.</span></span>
9. <span data-ttu-id="e8dda-157">Salvare tooa file hello una cartella locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="e8dda-157">Save hello file tooa a local folder on your computer.</span></span>
10. <span data-ttu-id="e8dda-158">Aprire il file hello che appena salvato e modificare i valori hello per i parametri di hello.</span><span class="sxs-lookup"><span data-stu-id="e8dda-158">Open hello file you just saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="e8dda-159">Utilizzare hello seguente i valori inferiori toodeploy hello rete virtuale descritto nello scenario hello:</span><span class="sxs-lookup"><span data-stu-id="e8dda-159">Use hello following values below toodeploy hello VNet described in hello scenario:</span></span>

    ```json
        {
          "location": {
            "value": "Central US"
          },
          "vnetName": {
              "value": "TestVNet"
          },
          "addressPrefix": {
              "value": "192.168.0.0/16"
          },
          "subnet1Name": {
              "value": "FrontEnd"
          },
          "subnet1Prefix": {
            "value": "192.168.1.0/24"
          },
          "subnet2Name": {
              "value": "BackEnd"
          },
          "subnet2Prefix": {
              "value": "192.168.2.0/24"
          }
        }
    ```

11. <span data-ttu-id="e8dda-160">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="e8dda-160">Save hello file.</span></span>


## <a name="deploy-hello-template-using-powershell"></a><span data-ttu-id="e8dda-161">Distribuire il modello di hello tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8dda-161">Deploy hello template using PowerShell</span></span>

<span data-ttu-id="e8dda-162">Completare hello dopo passaggi toodeploy hello template che è stato scaricato tramite PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e8dda-162">Complete hello following steps toodeploy hello template you downloaded by using PowerShell:</span></span>

1. <span data-ttu-id="e8dda-163">Installare e configurare Azure PowerShell, completare i passaggi hello hello [come tooInstall e configurare Azure PowerShell](/powershell/azure/overview) articolo.</span><span class="sxs-lookup"><span data-stu-id="e8dda-163">Install and configure Azure PowerShell by completing hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="e8dda-164">Eseguire hello successivo comando toocreate un nuovo gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="e8dda-164">Run hello following command toocreate a new resource group:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="e8dda-165">comando Hello crea un gruppo di risorse denominato *TestRG* in hello *centrale Usa* area di azure.</span><span class="sxs-lookup"><span data-stu-id="e8dda-165">hello command creates a resource group named *TestRG* in hello *Central US* azure region.</span></span> <span data-ttu-id="e8dda-166">Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e8dda-166">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="e8dda-167">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="e8dda-167">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. <span data-ttu-id="e8dda-168">Eseguire hello toodeploy hello nuova rete virtuale utilizzando i file modello/parametro hello è stato scaricato e modificato di sopra di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e8dda-168">Run hello following command toodeploy hello new VNet using hello template and parameter files you downloaded and modified above:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    <span data-ttu-id="e8dda-169">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="e8dda-169">Expected output:</span></span>
   
        DeploymentName    : TestVNetDeployment
        ResourceGroupName : TestRG
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
        Parameters        :
                            Name             Type                       Value
                            ===============  =========================  ==========
                            location         String                     Central US
                            vnetName         String                     TestVNet
                            addressPrefix    String                     192.168.0.0/16
                            subnet1Prefix    String                     192.168.1.0/24
                            subnet1Name      String                     FrontEnd
                            subnet2Prefix    String                     192.168.2.0/24
                            subnet2Name      String                     BackEnd
   
        Outputs           :
4. <span data-ttu-id="e8dda-170">Comando che segue hello esecuzione proprietà hello tooview di hello nuova rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="e8dda-170">Run hello following command tooview hello properties of hello new VNet:</span></span>

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    <span data-ttu-id="e8dda-171">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="e8dda-171">Expected output:</span></span>

        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : centralus
        Id                : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              :
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              },
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="deploy-hello-template-using-click-to-deploy"></a><span data-ttu-id="e8dda-172">Distribuire il modello di hello utilizzando fare clic su da distribuire</span><span class="sxs-lookup"><span data-stu-id="e8dda-172">Deploy hello template using click-to-deploy</span></span>

<span data-ttu-id="e8dda-173">È possibile riutilizzare predefiniti repository di GitHub di tooa caricati modelli, Gestione risorse di Azure gestiti da Microsoft e aprire toohello community.</span><span class="sxs-lookup"><span data-stu-id="e8dda-173">You can reuse pre-defined Azure Resource Manager templates uploaded tooa GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="e8dda-174">Questi modelli possono essere distribuiti direttamente da GitHub, o scaricati e modificati toofit le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="e8dda-174">These templates can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> <span data-ttu-id="e8dda-175">toodeploy un modello che crea una rete virtuale con due subnet, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e8dda-175">toodeploy a template that creates a VNet with two subnets, complete hello following steps:</span></span>

1. <span data-ttu-id="e8dda-176">Da un browser, passare troppo[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="e8dda-176">From a browser, navigate too[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
2. <span data-ttu-id="e8dda-177">Scorrere verso il basso l'elenco di hello dei modelli e fare clic su **101-rete virtuale due subnet**.</span><span class="sxs-lookup"><span data-stu-id="e8dda-177">Scroll down hello list of templates, and click **101-vnet-two-subnets**.</span></span> <span data-ttu-id="e8dda-178">Controllare hello **README.md** file, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="e8dda-178">Check hello **README.md** file, as shown below.</span></span>

    ![File READEME.md in github](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. <span data-ttu-id="e8dda-180">Fare clic su **distribuire tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="e8dda-180">Click **Deploy tooAzure**.</span></span> <span data-ttu-id="e8dda-181">Se necessario, immettere le credenziali di accesso di Azure.</span><span class="sxs-lookup"><span data-stu-id="e8dda-181">If necessary, enter your Azure login credentials.</span></span> 
4. <span data-ttu-id="e8dda-182">In hello **parametri** pannello, immettere i valori hello desidera toouse toocreate nuova rete virtuale e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8dda-182">In hello **Parameters** blade, enter hello values you want toouse toocreate your new VNet, and then click **OK**.</span></span> <span data-ttu-id="e8dda-183">Hello nella figura seguente mostra i valori hello per uno scenario di hello:</span><span class="sxs-lookup"><span data-stu-id="e8dda-183">hello following figure shows hello values for hello scenario:</span></span>
   
    ![Parametri del modello ARM](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. <span data-ttu-id="e8dda-185">Fare clic su **gruppo di risorse** e selezionare un tooadd gruppo di risorse hello tra oppure fare clic su **Crea nuovo** tooadd hello rete virtuale tooa nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e8dda-185">Click **Resource group** and select a resource group tooadd hello VNet to, or click **Create new** tooadd hello VNet tooa new resource group.</span></span> <span data-ttu-id="e8dda-186">Hello nella figura seguente mostra hello di risorse di gruppo per un nuovo gruppo di risorse denominato **TestRG**:</span><span class="sxs-lookup"><span data-stu-id="e8dda-186">hello following figure shows hello resource group settings for a new resource group called **TestRG**:</span></span>

    ![Gruppo di risorse](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. <span data-ttu-id="e8dda-188">Se necessario, modificare hello **sottoscrizione** e **percorso** le impostazioni per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e8dda-188">If necessary, change hello **Subscription** and **Location** settings for your VNet.</span></span>
7. <span data-ttu-id="e8dda-189">Se non si desidera toosee hello rete virtuale come un riquadro in hello **schermata iniziale**, disabilitare **tooStartboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="e8dda-189">If you do not want toosee hello VNet as a tile in hello **Startboard**, disable **Pin tooStartboard**.</span></span>
8. <span data-ttu-id="e8dda-190">Fare clic su **legali**, leggere le condizioni di hello e fare clic su **acquistare** tooagree.</span><span class="sxs-lookup"><span data-stu-id="e8dda-190">Click **Legal terms**, read hello terms, and click **Buy** tooagree.</span></span> 
9. <span data-ttu-id="e8dda-191">Fare clic su **crea** toocreate hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e8dda-191">Click **Create** toocreate hello VNet.</span></span>
   
    ![Invio del riquadro di distribuzione nel portale di anteprima](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. <span data-ttu-id="e8dda-193">Una volta completata la distribuzione di hello, hello portale di Azure selezionare **più servizi**, tipo *reti virtuali* nella casella Filtro hello visualizzata, quindi fare clic su Pannello di reti virtuali di virtuale reti toosee hello.</span><span class="sxs-lookup"><span data-stu-id="e8dda-193">Once hello deployment is complete, in hello Azure portal click **More services**, type *virtual networks* in hello filter box that appears, then click Virtual networks toosee hello Virtual networks blade.</span></span> <span data-ttu-id="e8dda-194">Nel Pannello di hello, fare clic su *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="e8dda-194">In hello blade, click *TestVNet*.</span></span> <span data-ttu-id="e8dda-195">In hello *TestVNet* pannello, fare clic su **subnet** subnet hello creato toosee, come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="e8dda-195">In hello *TestVNet* blade, click **Subnets** toosee hello created subnets, as shown in hello following picture:</span></span>
    
     ![Creare una rete virtuale nel portale di anteprima](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a><span data-ttu-id="e8dda-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e8dda-197">Next steps</span></span>

<span data-ttu-id="e8dda-198">Informazioni su come tooconnect:</span><span class="sxs-lookup"><span data-stu-id="e8dda-198">Learn how tooconnect:</span></span>

- <span data-ttu-id="e8dda-199">Una rete virtuale tooa di macchina virtuale (VM) da lettura hello [creare una macchina virtuale Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) o [creare una VM Linux](../virtual-machines/linux/quick-create-portal.md) articoli.</span><span class="sxs-lookup"><span data-stu-id="e8dda-199">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="e8dda-200">Anziché creare una rete virtuale e subnet nei passaggi hello degli articoli hello, è possibile selezionare una rete virtuale esistente e subnet tooconnect una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e8dda-200">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="e8dda-201">Hello reti virtuali di rete virtuale tooother leggendo hello [connettere reti virtuali](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="e8dda-201">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="e8dda-202">rete locale tooan rete virtuale Hello utilizza una rete privata virtuale (VPN) da sito a sito o un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e8dda-202">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="e8dda-203">Ulteriori informazioni, leggere hello [connettere una rete locale tooan di rete virtuale tramite una VPN site-to-site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [collegare un circuito ExpressRoute di tooan rete virtuale](../expressroute/expressroute-howto-linkvnet-arm.md) articoli.</span><span class="sxs-lookup"><span data-stu-id="e8dda-203">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
