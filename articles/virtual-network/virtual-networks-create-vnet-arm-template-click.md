---
title: Creare una rete virtuale | Modello di Azure Resource Manager | Documentazione Microsoft
description: Informazioni su come creare una rete virtuale usando un modello di Azure Resource Manager.
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
ms.openlocfilehash: 81602766848a91331c8d811ea1c8ec3ffae44b96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a><span data-ttu-id="c9611-103">Creare una rete virtuale usando un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c9611-103">Create a virtual network using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="c9611-104">Azure offre due modelli di distribuzione, ovvero Azure Resource Manager e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="c9611-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="c9611-105">Microsoft consiglia di creare le risorse tramite il modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c9611-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="c9611-106">Per altre informazioni sulle differenze tra i due modelli, leggere l'articolo [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) (Informazioni sui modelli di distribuzione di Azure).</span><span class="sxs-lookup"><span data-stu-id="c9611-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="c9611-107">Questo articolo illustra come creare una rete virtuale tramite il modello di distribuzione Resource Manager usando un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c9611-107">This article explains how to create a VNet through the Resource Manager deployment model using an Azure Resource Manager template.</span></span> <span data-ttu-id="c9611-108">È anche possibile creare una rete virtuale tramite Resource Manager usando altri strumenti oppure tramite il modello di distribuzione classica selezionando un'opzione diversa dall'elenco seguente:</span><span class="sxs-lookup"><span data-stu-id="c9611-108">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
- [<span data-ttu-id="c9611-109">Portale</span><span class="sxs-lookup"><span data-stu-id="c9611-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
- [<span data-ttu-id="c9611-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9611-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
- [<span data-ttu-id="c9611-111">CLI</span><span class="sxs-lookup"><span data-stu-id="c9611-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
- [<span data-ttu-id="c9611-112">Modello</span><span class="sxs-lookup"><span data-stu-id="c9611-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
- [<span data-ttu-id="c9611-113">Portale (versione classica)</span><span class="sxs-lookup"><span data-stu-id="c9611-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
- [<span data-ttu-id="c9611-114">PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="c9611-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [<span data-ttu-id="c9611-115">Interfaccia della riga di comando (versione classica)</span><span class="sxs-lookup"><span data-stu-id="c9611-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

<span data-ttu-id="c9611-116">Verrà illustrato come scaricare e modificare un modello di Gestione risorse di Azure esistente da GitHub e distribuire il modello da GitHub, PowerShell e dall'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="c9611-116">You will learn how to download and modify and existing ARM template from GitHub, and deploy the template from GitHub, PowerShell, and the Azure CLI.</span></span>

<span data-ttu-id="c9611-117">Se si sta distribuendo semplicemente il modello di Gestione risorse di Azure direttamente da GitHub, senza alcuna modifica, ignorare il passaggio per [distribuire un modello da github](#deploy-the-arm-template-by-using-click-to-deploy).</span><span class="sxs-lookup"><span data-stu-id="c9611-117">If you are simply deploying the ARM template directly from GitHub, without any changes, skip to [deploy a template from github](#deploy-the-arm-template-by-using-click-to-deploy).</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-the-azure-resource-manager-template"></a><span data-ttu-id="c9611-118">Scaricare e comprendere il modello di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="c9611-118">Download and understand the Azure Resource Manager template</span></span>
<span data-ttu-id="c9611-119">È possibile scaricare il modello esistente per la creazione di una rete virtuale e di due subnet da GitHub, apportare le modifiche desiderate e riutilizzarlo.</span><span class="sxs-lookup"><span data-stu-id="c9611-119">You can download the existing template for creating a VNet and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="c9611-120">A questo scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c9611-120">To do so, complete the following steps:</span></span>

1. <span data-ttu-id="c9611-121">Passare alla [pagina del modello di esempio](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="c9611-121">Navigate to [the sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="c9611-122">Fare clic su **azuredeploy.json**, quindi fare clic su **RAW**.</span><span class="sxs-lookup"><span data-stu-id="c9611-122">Click **azuredeploy.json**, and then click **RAW**.</span></span>
3. <span data-ttu-id="c9611-123">Salvare il file in una cartella locale nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="c9611-123">Save the file to a a local folder on your computer.</span></span>
4. <span data-ttu-id="c9611-124">Se si ha familiarità con i modelli, procedere al passaggio 7.</span><span class="sxs-lookup"><span data-stu-id="c9611-124">If you are familiar with templates, skip to step 7.</span></span>
5. <span data-ttu-id="c9611-125">Aprire il file appena salvato e visualizzare il contenuto in **parameters** nella riga 5.</span><span class="sxs-lookup"><span data-stu-id="c9611-125">Open the file you just saved and look at the contents under **parameters** in line 5.</span></span> <span data-ttu-id="c9611-126">I parametri del modello ARM costituiscono un segnaposto per i valori che possono essere compilati durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c9611-126">ARM template parameters provide a placeholder for values that can be filled out during deployment.</span></span>
   
   | <span data-ttu-id="c9611-127">Parametro</span><span class="sxs-lookup"><span data-stu-id="c9611-127">Parameter</span></span> | <span data-ttu-id="c9611-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c9611-128">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="c9611-129">**Località**</span><span class="sxs-lookup"><span data-stu-id="c9611-129">**location**</span></span> |<span data-ttu-id="c9611-130">Area di Azure in cui verrà creata la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="c9611-130">Azure region where the VNet will be created</span></span> |
   | <span data-ttu-id="c9611-131">**vnetName**</span><span class="sxs-lookup"><span data-stu-id="c9611-131">**vnetName**</span></span> |<span data-ttu-id="c9611-132">Nome per la nuova rete virtuale</span><span class="sxs-lookup"><span data-stu-id="c9611-132">Name for the new VNet</span></span> |
   | <span data-ttu-id="c9611-133">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="c9611-133">**addressPrefix**</span></span> |<span data-ttu-id="c9611-134">Spazio di indirizzi per la rete virtuale, nel formato CIDR</span><span class="sxs-lookup"><span data-stu-id="c9611-134">Address space for the VNet, in CIDR format</span></span> |
   | <span data-ttu-id="c9611-135">**subnet1Name**</span><span class="sxs-lookup"><span data-stu-id="c9611-135">**subnet1Name**</span></span> |<span data-ttu-id="c9611-136">Nome per la prima rete virtuale</span><span class="sxs-lookup"><span data-stu-id="c9611-136">Name for the first VNet</span></span> |
   | <span data-ttu-id="c9611-137">**subnet1Prefix**</span><span class="sxs-lookup"><span data-stu-id="c9611-137">**subnet1Prefix**</span></span> |<span data-ttu-id="c9611-138">Blocco CIDR per la prima subnet</span><span class="sxs-lookup"><span data-stu-id="c9611-138">CIDR block for the first subnet</span></span> |
   | <span data-ttu-id="c9611-139">**subnet2Name**</span><span class="sxs-lookup"><span data-stu-id="c9611-139">**subnet2Name**</span></span> |<span data-ttu-id="c9611-140">Nome per la seconda rete virtuale</span><span class="sxs-lookup"><span data-stu-id="c9611-140">Name for the second VNet</span></span> |
   | <span data-ttu-id="c9611-141">**subnet2Prefix**</span><span class="sxs-lookup"><span data-stu-id="c9611-141">**subnet2Prefix**</span></span> |<span data-ttu-id="c9611-142">Blocco CIDR per la seconda subnet</span><span class="sxs-lookup"><span data-stu-id="c9611-142">CIDR block for the second subnet</span></span> |
   
   > [!IMPORTANT]
   > <span data-ttu-id="c9611-143">I modelli di Gestione risorse di Azure conservati in GitHub possono cambiare nel tempo.</span><span class="sxs-lookup"><span data-stu-id="c9611-143">Azure Resource Manager templates maintained in GitHub can change over time.</span></span> <span data-ttu-id="c9611-144">Assicurarsi di aver controllato il modello prima di utilizzarlo.</span><span class="sxs-lookup"><span data-stu-id="c9611-144">Make sure you check the template before using it.</span></span>
   > 
   > 
6. <span data-ttu-id="c9611-145">Controllare il contenuto in **resources** e prendere nota di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="c9611-145">Check the content under **resources** and notice the following:</span></span>
   
   * <span data-ttu-id="c9611-146">**type**.</span><span class="sxs-lookup"><span data-stu-id="c9611-146">**type**.</span></span> <span data-ttu-id="c9611-147">Tipo di risorsa che sarà creato dal modello.</span><span class="sxs-lookup"><span data-stu-id="c9611-147">Type of resource being created by the template.</span></span> <span data-ttu-id="c9611-148">In questo caso, **Microsoft.Network/virtualNetworks**, che rappresenta una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c9611-148">In this case, **Microsoft.Network/virtualNetworks**, which represent a VNet.</span></span>
   * <span data-ttu-id="c9611-149">**name**.</span><span class="sxs-lookup"><span data-stu-id="c9611-149">**name**.</span></span> <span data-ttu-id="c9611-150">Nome della risorsa.</span><span class="sxs-lookup"><span data-stu-id="c9611-150">Name for the resource.</span></span> <span data-ttu-id="c9611-151">Notare l'utilizzo di **[parameters('vnetName')]**con cui si indica che il nome verrà specificato come input dall'utente o tramite un file di parametri durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c9611-151">Notice the use of **[parameters('vnetName')]**, which means the name will provided as input by the user or a parameter file during deployment.</span></span>
   * <span data-ttu-id="c9611-152">**properties**.</span><span class="sxs-lookup"><span data-stu-id="c9611-152">**properties**.</span></span> <span data-ttu-id="c9611-153">Elenco di proprietà per la risorsa.</span><span class="sxs-lookup"><span data-stu-id="c9611-153">List of properties for the resource.</span></span> <span data-ttu-id="c9611-154">Questo modello utilizza le proprietà relative allo spazio di indirizzi e alla subnet durante la creazione della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c9611-154">This template uses the address space and subnet properties during VNet creation.</span></span>
7. <span data-ttu-id="c9611-155">Tornare alla [pagina del modello di esempio](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="c9611-155">Navigate back to [the sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
8. <span data-ttu-id="c9611-156">Fare clic su **azuredeploy-parameters.json** e quindi su **RAW**.</span><span class="sxs-lookup"><span data-stu-id="c9611-156">Click **azuredeploy-paremeters.json**, and then click **RAW**.</span></span>
9. <span data-ttu-id="c9611-157">Salvare il file in una cartella locale nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="c9611-157">Save the file to a a local folder on your computer.</span></span>
10. <span data-ttu-id="c9611-158">Aprire il file appena salvato e modificare i valori per i parametri.</span><span class="sxs-lookup"><span data-stu-id="c9611-158">Open the file you just saved and edit the values for the parameters.</span></span> <span data-ttu-id="c9611-159">Usare i valori riportati di seguito per la distribuzione della rete virtuale descritta in questo scenario:</span><span class="sxs-lookup"><span data-stu-id="c9611-159">Use the following values below to deploy the VNet described in the scenario:</span></span>

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

11. <span data-ttu-id="c9611-160">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="c9611-160">Save the file.</span></span>


## <a name="deploy-the-template-using-powershell"></a><span data-ttu-id="c9611-161">Distribuire il modello tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9611-161">Deploy the template using PowerShell</span></span>

<span data-ttu-id="c9611-162">Per distribuire il modello scaricato tramite PowerShell, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c9611-162">Complete the following steps to deploy the template you downloaded by using PowerShell:</span></span>

1. <span data-ttu-id="c9611-163">Installare e configurare Azure PowerShell eseguendo i passaggi descritti nell'articolo [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c9611-163">Install and configure Azure PowerShell by completing the steps in the [How to Install and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="c9611-164">Usare il comando seguente per creare un nuovo gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="c9611-164">Run the following command to create a new resource group:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="c9611-165">Il comando crea un gruppo di risorse denominato *TestRG* nell'area di Azure *Stati Uniti centrali*.</span><span class="sxs-lookup"><span data-stu-id="c9611-165">The command creates a resource group named *TestRG* in the *Central US* azure region.</span></span> <span data-ttu-id="c9611-166">Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c9611-166">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="c9611-167">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="c9611-167">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. <span data-ttu-id="c9611-168">Eseguire il comando seguente per distribuire la nuova rete virtuale usando il modello e i file dei parametri scaricati e modificati in precedenza:</span><span class="sxs-lookup"><span data-stu-id="c9611-168">Run the following command to deploy the new VNet using the template and parameter files you downloaded and modified above:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    <span data-ttu-id="c9611-169">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="c9611-169">Expected output:</span></span>
   
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
4. <span data-ttu-id="c9611-170">Eseguire il comando seguente per visualizzare le proprietà della nuova rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="c9611-170">Run the following command to view the properties of the new VNet:</span></span>

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    <span data-ttu-id="c9611-171">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="c9611-171">Expected output:</span></span>

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

## <a name="deploy-the-template-using-click-to-deploy"></a><span data-ttu-id="c9611-172">Distribuire il modello tramite clic per la distribuzione</span><span class="sxs-lookup"><span data-stu-id="c9611-172">Deploy the template using click-to-deploy</span></span>

<span data-ttu-id="c9611-173">È possibile riutilizzare modelli di Azure Resource Manager predefiniti, caricarli in un repository GitHub gestito da Microsoft e renderli disponibili alla community.</span><span class="sxs-lookup"><span data-stu-id="c9611-173">You can reuse pre-defined Azure Resource Manager templates uploaded to a GitHub repository maintained by Microsoft and open to the community.</span></span> <span data-ttu-id="c9611-174">Questi modelli possono essere distribuiti immediatamente da GitHub o scaricati e modificati in base alle specifiche esigenze.</span><span class="sxs-lookup"><span data-stu-id="c9611-174">These templates can be deployed straight out of GitHub, or downloaded and modified to fit your needs.</span></span> <span data-ttu-id="c9611-175">Per distribuire un modello che crea una rete virtuale con due subnet, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c9611-175">To deploy a template that creates a VNet with two subnets, complete the following steps:</span></span>

1. <span data-ttu-id="c9611-176">Da un browser, passare a [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="c9611-176">From a browser, navigate to [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
2. <span data-ttu-id="c9611-177">Scorrere verso il basso nell'elenco dei modelli e fare clic su **101-vnet-two-subnets**.</span><span class="sxs-lookup"><span data-stu-id="c9611-177">Scroll down the list of templates, and click **101-vnet-two-subnets**.</span></span> <span data-ttu-id="c9611-178">Controllare il file **README.md** , come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c9611-178">Check the **README.md** file, as shown below.</span></span>

    ![File READEME.md in github](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. <span data-ttu-id="c9611-180">Fare clic su **Distribuzione in Azure**.</span><span class="sxs-lookup"><span data-stu-id="c9611-180">Click **Deploy to Azure**.</span></span> <span data-ttu-id="c9611-181">Se necessario, immettere le credenziali di accesso di Azure.</span><span class="sxs-lookup"><span data-stu-id="c9611-181">If necessary, enter your Azure login credentials.</span></span> 
4. <span data-ttu-id="c9611-182">Nel pannello **Parametri** immettere i valori da usare per creare la nuova rete virtuale e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c9611-182">In the **Parameters** blade, enter the values you want to use to create your new VNet, and then click **OK**.</span></span> <span data-ttu-id="c9611-183">La figura seguente mostra i valori relativi allo scenario:</span><span class="sxs-lookup"><span data-stu-id="c9611-183">The following figure shows the values for the scenario:</span></span>
   
    ![Parametri del modello ARM](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. <span data-ttu-id="c9611-185">Fare clic su **Gruppo di risorse** e selezionare un gruppo di risorse a cui aggiungere la rete virtuale oppure fare clic su **Crea nuovo** per aggiungere la rete virtuale a un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c9611-185">Click **Resource group** and select a resource group to add the VNet to, or click **Create new** to add the VNet to a new resource group.</span></span> <span data-ttu-id="c9611-186">La figura seguente mostra le impostazioni del gruppo di risorse per un nuovo gruppo di risorse denominato **TestRG**:</span><span class="sxs-lookup"><span data-stu-id="c9611-186">The following figure shows the resource group settings for a new resource group called **TestRG**:</span></span>

    ![Resource group](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. <span data-ttu-id="c9611-188">Se necessario, modificare le impostazioni relative a **Sottoscrizione** e **Località** per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c9611-188">If necessary, change the **Subscription** and **Location** settings for your VNet.</span></span>
7. <span data-ttu-id="c9611-189">Se non si vuole visualizzare la rete virtuale come riquadro nella **Schermata iniziale**, disabilitare **Aggiungi alla Schermata iniziale**.</span><span class="sxs-lookup"><span data-stu-id="c9611-189">If you do not want to see the VNet as a tile in the **Startboard**, disable **Pin to Startboard**.</span></span>
8. <span data-ttu-id="c9611-190">Fare clic su **Note legali**, leggere le condizioni e fare clic su **Acquista** per accettare.</span><span class="sxs-lookup"><span data-stu-id="c9611-190">Click **Legal terms**, read the terms, and click **Buy** to agree.</span></span> 
9. <span data-ttu-id="c9611-191">Fare clic su **Crea** per creare la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c9611-191">Click **Create** to create the VNet.</span></span>
   
    ![Invio del riquadro di distribuzione nel portale di anteprima](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. <span data-ttu-id="c9611-193">Dopo il completamento dell'operazione, nel portale di Azure fare clic su **More services** (Altri servizi), digitare *reti virtuali* nella casella dei filtri visualizzata e quindi fare clic su Reti virtuali per visualizzare il pannello Reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="c9611-193">Once the deployment is complete, in the Azure portal click **More services**, type *virtual networks* in the filter box that appears, then click Virtual networks to see the Virtual networks blade.</span></span> <span data-ttu-id="c9611-194">Nel pannello fare clic su *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="c9611-194">In the blade, click *TestVNet*.</span></span> <span data-ttu-id="c9611-195">Nel pannello *TestVNet* fare clic su **Subnet** per visualizzare le subnet create, come mostrato nella figura seguente:</span><span class="sxs-lookup"><span data-stu-id="c9611-195">In the *TestVNet* blade, click **Subnets** to see the created subnets, as shown in the following picture:</span></span>
    
     ![Creare una rete virtuale nel portale di anteprima](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a><span data-ttu-id="c9611-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c9611-197">Next steps</span></span>

<span data-ttu-id="c9611-198">Leggere le informazioni su come connettere:</span><span class="sxs-lookup"><span data-stu-id="c9611-198">Learn how to connect:</span></span>

- <span data-ttu-id="c9611-199">Una macchina virtuale (VM) a una rete virtuale negli articoli [Creare una macchina virtuale Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) o [Creare una VM Linux](../virtual-machines/linux/quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c9611-199">A virtual machine (VM) to a virtual network by reading the [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="c9611-200">Anziché creare una rete virtuale e una subnet, come illustrato nelle procedure degli articoli, è possibile selezionare una rete virtuale e una subnet esistenti a cui connettere una VM.</span><span class="sxs-lookup"><span data-stu-id="c9611-200">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="c9611-201">La rete virtuale ad altre reti virtuali nell'articolo [Connettere reti virtuali](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c9611-201">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="c9611-202">La rete virtuale a una rete locale tramite una rete privata virtuale (VPN) da sito a sito o il circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c9611-202">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="c9611-203">negli articoli [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) (Connettere una rete virtuale a una rete locale tramite una VPN da sito a sito) e [Collegare una rete virtuale a un circuito ExpressRoute](../expressroute/expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c9611-203">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
