---
title: Creare una VM con un indirizzo IP pubblico statico - Modello di Azure Resource Manager | Documentazione Microsoft
description: Informazioni su come creare una VM con un indirizzo IP pubblico statico mediante un modello di Azure Resource Manager.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d551085a-c7ed-4ec6-b4c3-e9e1cebb774c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2f503aa60fdd9b7cf66ef482a1041e34c88e5c01
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a><span data-ttu-id="c5bce-103">Creare una VM con un indirizzo IP pubblico statico mediante un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c5bce-103">Create a VM with a static public IP address using an Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c5bce-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c5bce-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="c5bce-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5bce-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="c5bce-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="c5bce-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="c5bce-107">Modello</span><span class="sxs-lookup"><span data-stu-id="c5bce-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * <span data-ttu-id="c5bce-108">[PowerShell (Classic)](virtual-networks-reserved-public-ip.md) (PowerShell (classico))</span><span class="sxs-lookup"><span data-stu-id="c5bce-108">[PowerShell (Classic)](virtual-networks-reserved-public-ip.md)</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="c5bce-109">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c5bce-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c5bce-110">Questo articolo illustra l'uso del modello di distribuzione Resource Manager che Microsoft consiglia di usare invece del modello di distribuzione classica per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="c5bce-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a><span data-ttu-id="c5bce-111">Risorse indirizzo IP pubblico in un file di modello</span><span class="sxs-lookup"><span data-stu-id="c5bce-111">Public IP address resources in a template file</span></span>
<span data-ttu-id="c5bce-112">È possibile visualizzare e scaricare il [modello di esempio](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="c5bce-112">You can view and download the [sample template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span></span>

<span data-ttu-id="c5bce-113">La sezione seguente illustra la definizione della risorsa IP pubblico in base allo scenario precedente:</span><span class="sxs-lookup"><span data-stu-id="c5bce-113">The following section shows the definition of the public IP resource, based on the scenario above:</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('webVMSetting').pipName]",
  "location": "[variables('location')]",
  "properties": {
    "publicIPAllocationMethod": "Static"
  },
  "tags": {
    "displayName": "PublicIPAddress - Web"
  }
},
```

<span data-ttu-id="c5bce-114">Notare la proprietà **publicIPAllocationMethod** impostata su *Statico*.</span><span class="sxs-lookup"><span data-stu-id="c5bce-114">Notice the **publicIPAllocationMethod** property, which is set to *Static*.</span></span> <span data-ttu-id="c5bce-115">Questa proprietà può essere *Dinamico* (valore predefinito) o *Statico*.</span><span class="sxs-lookup"><span data-stu-id="c5bce-115">This property can be either *Dynamic* (default value) or *Static*.</span></span> <span data-ttu-id="c5bce-116">Impostarla su Static garantisce che l'indirizzo IP pubblico assegnato non verrà mai modificato.</span><span class="sxs-lookup"><span data-stu-id="c5bce-116">Setting it to static guarantees that the public IP address assigned will never change.</span></span>

<span data-ttu-id="c5bce-117">La sezione seguente illustra l'associazione dell'IP pubblico con un'interfaccia di rete:</span><span class="sxs-lookup"><span data-stu-id="c5bce-117">The following section shows the association of the public IP address with a network interface:</span></span>

```json
  {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('webVMSetting').nicName]",
    "location": "[variables('location')]",
    "tags": {
    "displayName": "NetworkInterface - Web"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('webVMSetting').pipName)]",
      "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
          "privateIPAllocationMethod": "Static",
          "privateIPAddress": "[variables('webVMSetting').ipAddress]",
          "publicIPAddress": {
          "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('webVMSetting').pipName)]"
          },
          "subnet": {
            "id": "[variables('frontEndSubnetRef')]"
          }
        }
      }
    ]
  }
},
```

<span data-ttu-id="c5bce-118">Si noti che la proprietà **publicIPAddress** punta all'**Id** di una risorsa denominata **variables('webVMSetting').pipName**.</span><span class="sxs-lookup"><span data-stu-id="c5bce-118">Notice the **publicIPAddress** property pointing to the **Id** of a resource named **variables('webVMSetting').pipName**.</span></span> <span data-ttu-id="c5bce-119">È il nome della risorsa IP pubblico illustrata sopra.</span><span class="sxs-lookup"><span data-stu-id="c5bce-119">That is the name of the public IP resource shown above.</span></span>

<span data-ttu-id="c5bce-120">Infine, l'interfaccia di rete di cui sopra è elencata nella proprietà **networkProfile** della VM in fase di creazione.</span><span class="sxs-lookup"><span data-stu-id="c5bce-120">Finally, the network interface above is listed in the **networkProfile** property of the VM being created.</span></span>

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="c5bce-121">Distribuire il modello tramite clic per la distribuzione</span><span class="sxs-lookup"><span data-stu-id="c5bce-121">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="c5bce-122">Il modello di esempio disponibile nel repository pubblico usa un file di parametro che contiene i valori predefiniti usati per generare lo scenario descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c5bce-122">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="c5bce-123">Per distribuire questo modello tramite clic per la distribuzione, fare clic su **Deploy to Azure** (Distribuisci in Azure) nel file Readme.md per il modello [VM with static PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) modello(VM con PIP statico).</span><span class="sxs-lookup"><span data-stu-id="c5bce-123">To deploy this template using click to deploy, click **Deploy to Azure** in the Readme.md file for the [VM with static PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) template.</span></span> <span data-ttu-id="c5bce-124">Se richiesto, sostituire i valori predefiniti dei parametri e immettere i valori per i parametri vuoti.</span><span class="sxs-lookup"><span data-stu-id="c5bce-124">Replace the default parameter values if desired and enter values for the blank parameters.</span></span>  <span data-ttu-id="c5bce-125">Seguire le istruzioni nel portale per creare una macchina virtuale con un indirizzo IP pubblico statico.</span><span class="sxs-lookup"><span data-stu-id="c5bce-125">Follow the instructions in the portal to create a virtual machine with a static public IP address.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="c5bce-126">Distribuire il modello tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5bce-126">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="c5bce-127">Per distribuire il modello scaricato tramite PowerShell, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="c5bce-127">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="c5bce-128">Se non è mai stato usato Azure PowerShell, completare la procedura descritta nell'articolo [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c5bce-128">If you have never used Azure PowerShell, complete the steps in the [How to Install and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="c5bce-129">In una console PowerShell, eseguire il cmdlet `New-AzureRmResourceGroup` per creare un nuovo gruppo di risorse, se necessario.</span><span class="sxs-lookup"><span data-stu-id="c5bce-129">In a PowerShell console, run the `New-AzureRmResourceGroup` cmdlet to create a new resource group, if necessary.</span></span> <span data-ttu-id="c5bce-130">Se è già stato creato un gruppo di risorse, andare al passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="c5bce-130">If you already have a resource group created, go to step 3.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    <span data-ttu-id="c5bce-131">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="c5bce-131">Expected output:</span></span>
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. <span data-ttu-id="c5bce-132">In una console di PowerShell, eseguire il cmdlet `New-AzureRmResourceGroupDeployment` per distribuire il modello.</span><span class="sxs-lookup"><span data-stu-id="c5bce-132">In a PowerShell console, run the `New-AzureRmResourceGroupDeployment` cmdlet to deploy the template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    <span data-ttu-id="c5bce-133">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="c5bce-133">Expected output:</span></span>
   
        DeploymentName    : DeployVM
        ResourceGroupName : PIPTEST
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
                            Uri            : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/mas
                            ter/IaaS-Story/03-Static-public-IP/azuredeploy.json
                            ContentVersion : 1.0.0.0
   
        Parameters        :
                            Name                      Type                       Value     
                            ========================  =========================  ==========
                            vnetName                  String                     WTestVNet
                            vnetPrefix                String                     192.168.0.0/16
                            frontEndSubnetName        String                     FrontEnd  
                            frontEndSubnetPrefix      String                     192.168.1.0/24
                            storageAccountNamePrefix  String                     iaasestd  
                            stdStorageType            String                     Standard_LRS
                            osType                    String                     Windows   
                            adminUsername             String                     adminUser
                            adminPassword             SecureString                         
   
        Outputs           :

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="c5bce-134">Distribuire il modello tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="c5bce-134">Deploy the template by using the Azure CLI</span></span>
<span data-ttu-id="c5bce-135">Per distribuire il modello tramite l'interfaccia della riga di comando di Azure, completare la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c5bce-135">To deploy the template by using the Azure CLI, complete the following steps:</span></span>

1. <span data-ttu-id="c5bce-136">Se non è stata mai usata l'interfaccia della riga di comando di Azure, seguire la procedura riportata nell'articolo [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md) per installarla e configurarla.</span><span class="sxs-lookup"><span data-stu-id="c5bce-136">If you have never used Azure CLI, follow the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md) article to install and configure it.</span></span>
2. <span data-ttu-id="c5bce-137">Eseguire il comando `azure config mode` per passare alla modalità Gestione risorse, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c5bce-137">Run the `azure config mode` command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="c5bce-138">Di seguito è riportato l'output previsto per il comando precedente:</span><span class="sxs-lookup"><span data-stu-id="c5bce-138">The expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="c5bce-139">Aprire il [file dei parametri](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), selezionarne il contenuto e salvarlo in un file nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="c5bce-139">Open the [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), select its content, and save it to a file in your computer.</span></span> <span data-ttu-id="c5bce-140">Per questo esempio, i parametri vengono salvati in un file denominato *parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="c5bce-140">For this example, the parameters are saved to a file named *parameters.json*.</span></span> <span data-ttu-id="c5bce-141">Modificare i valori dei parametri all'interno del file, se richiesto, ma, come minimo, è consigliabile modificare il valore del parametro adminPassword in una password complessa e univoca.</span><span class="sxs-lookup"><span data-stu-id="c5bce-141">Change the parameter values within the file if desired, but at a minimum, it's recommended that you change the value for the adminPassword parameter to a unique, complex password.</span></span>
4. <span data-ttu-id="c5bce-142">Eseguire il cmdlet `azure group deployment create` per distribuire la nuova rete virtuale usando il modello e i file dei parametri scaricati e modificati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c5bce-142">Run the `azure group deployment create` cmd to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="c5bce-143">Nel comando seguente sostituire <path> con il percorso in cui è stato salvato il file.</span><span class="sxs-lookup"><span data-stu-id="c5bce-143">In the command below, replace <path> with the path you saved the file to.</span></span> 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    <span data-ttu-id="c5bce-144">Output previsto (elenca i valori usati per i parametri):</span><span class="sxs-lookup"><span data-stu-id="c5bce-144">Expected output (lists parameter values used):</span></span>

        info:    Executing command group create
        + Getting resource group PIPTEST2
        + Creating resource group PIPTEST2
        info:    Created resource group PIPTEST2
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/PIPTEST2
        data:    Name:                PIPTEST2
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

