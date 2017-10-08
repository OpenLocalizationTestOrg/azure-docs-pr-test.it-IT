---
title: aaaCreate una macchina virtuale con un indirizzo IP pubblico statico - modello di gestione risorse di Azure | Documenti Microsoft
description: Informazioni su come toocreate una macchina virtuale con un indirizzo IP pubblico statico di indirizzi utilizzando un modello di gestione risorse di Azure.
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
ms.openlocfilehash: 6a8640ed4fad06b0e09820e6114fd6789db73847
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a><span data-ttu-id="b7b48-103">Creare una VM con un indirizzo IP pubblico statico mediante un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b7b48-103">Create a VM with a static public IP address using an Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b7b48-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b7b48-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="b7b48-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7b48-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="b7b48-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b7b48-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="b7b48-107">Modello</span><span class="sxs-lookup"><span data-stu-id="b7b48-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * <span data-ttu-id="b7b48-108">[PowerShell (Classic)](virtual-networks-reserved-public-ip.md) (PowerShell (classico))</span><span class="sxs-lookup"><span data-stu-id="b7b48-108">[PowerShell (Classic)](virtual-networks-reserved-public-ip.md)</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="b7b48-109">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b7b48-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b7b48-110">In questo articolo viene illustrato l'utilizzo di modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="b7b48-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a><span data-ttu-id="b7b48-111">Risorse indirizzo IP pubblico in un file di modello</span><span class="sxs-lookup"><span data-stu-id="b7b48-111">Public IP address resources in a template file</span></span>
<span data-ttu-id="b7b48-112">È possibile visualizzare e scaricare hello [modello di esempio](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="b7b48-112">You can view and download hello [sample template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span></span>

<span data-ttu-id="b7b48-113">Hello nella sezione seguente viene illustrata hello definizione di risorsa IP pubblica hello, a seconda dello scenario hello precedente:</span><span class="sxs-lookup"><span data-stu-id="b7b48-113">hello following section shows hello definition of hello public IP resource, based on hello scenario above:</span></span>

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

<span data-ttu-id="b7b48-114">Hello preavviso **publicIPAllocationMethod** proprietà, che è stata impostata troppo*statico*.</span><span class="sxs-lookup"><span data-stu-id="b7b48-114">Notice hello **publicIPAllocationMethod** property, which is set too*Static*.</span></span> <span data-ttu-id="b7b48-115">Questa proprietà può essere *Dinamico* (valore predefinito) o *Statico*.</span><span class="sxs-lookup"><span data-stu-id="b7b48-115">This property can be either *Dynamic* (default value) or *Static*.</span></span> <span data-ttu-id="b7b48-116">Impostazione toostatic garantisce che l'indirizzo IP pubblico hello assegnato non verrà mai modificato.</span><span class="sxs-lookup"><span data-stu-id="b7b48-116">Setting it toostatic guarantees that hello public IP address assigned will never change.</span></span>

<span data-ttu-id="b7b48-117">Hello nella sezione seguente viene illustrato associazione hello dell'indirizzo IP pubblico hello con un'interfaccia di rete:</span><span class="sxs-lookup"><span data-stu-id="b7b48-117">hello following section shows hello association of hello public IP address with a network interface:</span></span>

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

<span data-ttu-id="b7b48-118">Hello preavviso **publicIPAddress** proprietà verso toohello **Id** di una risorsa denominata **variables('webVMSetting').pipName**.</span><span class="sxs-lookup"><span data-stu-id="b7b48-118">Notice hello **publicIPAddress** property pointing toohello **Id** of a resource named **variables('webVMSetting').pipName**.</span></span> <span data-ttu-id="b7b48-119">Che è il nome di hello della risorsa IP pubblica hello illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b7b48-119">That is hello name of hello public IP resource shown above.</span></span>

<span data-ttu-id="b7b48-120">Infine, l'interfaccia di rete hello precedente è elencato in hello **profilo** proprietà di hello macchina virtuale da creare.</span><span class="sxs-lookup"><span data-stu-id="b7b48-120">Finally, hello network interface above is listed in hello **networkProfile** property of hello VM being created.</span></span>

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="b7b48-121">Distribuire il modello di hello utilizzando fare clic su toodeploy</span><span class="sxs-lookup"><span data-stu-id="b7b48-121">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="b7b48-122">modello di Hello esempio disponibile nel repository pubblico hello utilizza un file di parametro contenente hello predefiniti i valori utilizzati toogenerate hello lo scenario descritto sopra.</span><span class="sxs-lookup"><span data-stu-id="b7b48-122">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="b7b48-123">toodeploy questo modello utilizzando fare clic su toodeploy, fare clic su **distribuire tooAzure** file Readme.md hello per hello [macchina virtuale con indirizzo PIP statico](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) modello.</span><span class="sxs-lookup"><span data-stu-id="b7b48-123">toodeploy this template using click toodeploy, click **Deploy tooAzure** in hello Readme.md file for hello [VM with static PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) template.</span></span> <span data-ttu-id="b7b48-124">Sostituire i valori dei parametri predefiniti hello se lo si desidera, immettere valori per parametri vuoti hello.</span><span class="sxs-lookup"><span data-stu-id="b7b48-124">Replace hello default parameter values if desired and enter values for hello blank parameters.</span></span>  <span data-ttu-id="b7b48-125">Seguire le istruzioni hello hello portale toocreate una macchina virtuale con un indirizzo IP pubblico statico.</span><span class="sxs-lookup"><span data-stu-id="b7b48-125">Follow hello instructions in hello portal toocreate a virtual machine with a static public IP address.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="b7b48-126">Distribuire il modello di hello tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7b48-126">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="b7b48-127">modello di hello toodeploy scaricato tramite PowerShell, seguire i passaggi di hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="b7b48-127">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="b7b48-128">Se non si è mai usato Azure PowerShell, hello completato i passaggi in hello [come tooInstall e configurare Azure PowerShell](/powershell/azure/overview) articolo.</span><span class="sxs-lookup"><span data-stu-id="b7b48-128">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="b7b48-129">Nella console di PowerShell, eseguire hello `New-AzureRmResourceGroup` cmdlet toocreate un nuovo gruppo di risorse, se necessario.</span><span class="sxs-lookup"><span data-stu-id="b7b48-129">In a PowerShell console, run hello `New-AzureRmResourceGroup` cmdlet toocreate a new resource group, if necessary.</span></span> <span data-ttu-id="b7b48-130">Se si dispone già di un gruppo di risorse creato, andare toostep 3.</span><span class="sxs-lookup"><span data-stu-id="b7b48-130">If you already have a resource group created, go toostep 3.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    <span data-ttu-id="b7b48-131">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="b7b48-131">Expected output:</span></span>
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. <span data-ttu-id="b7b48-132">Nella console di PowerShell, eseguire hello `New-AzureRmResourceGroupDeployment` modello hello toodeploy di cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b7b48-132">In a PowerShell console, run hello `New-AzureRmResourceGroupDeployment` cmdlet toodeploy hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    <span data-ttu-id="b7b48-133">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="b7b48-133">Expected output:</span></span>
   
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

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="b7b48-134">Distribuire il modello di hello utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="b7b48-134">Deploy hello template by using hello Azure CLI</span></span>
<span data-ttu-id="b7b48-135">modello di hello toodeploy utilizzando hello CLI di Azure, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b7b48-135">toodeploy hello template by using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="b7b48-136">Se non si è mai usato CLI di Azure, seguire hello hello [installare e configurare hello Azure CLI](../cli-install-nodejs.md) articolo tooinstall e configurarlo.</span><span class="sxs-lookup"><span data-stu-id="b7b48-136">If you have never used Azure CLI, follow hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md) article tooinstall and configure it.</span></span>
2. <span data-ttu-id="b7b48-137">Eseguire hello `azure config mode` tooswitch tooResource Manager modalità comando, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="b7b48-137">Run hello `azure config mode` command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="b7b48-138">Hello è previsto un output di hello comando precedente:</span><span class="sxs-lookup"><span data-stu-id="b7b48-138">hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="b7b48-139">Aprire hello [file dei parametri](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), selezionare il contenuto e salvarlo tooa file nel computer.</span><span class="sxs-lookup"><span data-stu-id="b7b48-139">Open hello [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), select its content, and save it tooa file in your computer.</span></span> <span data-ttu-id="b7b48-140">Per questo esempio, i parametri di hello vengono salvati i file tooa denominato *parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="b7b48-140">For this example, hello parameters are saved tooa file named *parameters.json*.</span></span> <span data-ttu-id="b7b48-141">I valori dei parametri hello nel file hello se lo si desidera modificare, ma come minimo, è consigliabile modificare il valore di hello per hello adminPassword parametro tooa complesso password univoca.</span><span class="sxs-lookup"><span data-stu-id="b7b48-141">Change hello parameter values within hello file if desired, but at a minimum, it's recommended that you change hello value for hello adminPassword parameter tooa unique, complex password.</span></span>
4. <span data-ttu-id="b7b48-142">Eseguire hello `azure group deployment create` cmd toodeploy hello nuova rete virtuale utilizzando il modello di hello e parametro file scaricato e modificato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b7b48-142">Run hello `azure group deployment create` cmd toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="b7b48-143">Nel comando hello seguente, sostituire <path> con percorso hello è stato salvato file hello.</span><span class="sxs-lookup"><span data-stu-id="b7b48-143">In hello command below, replace <path> with hello path you saved hello file to.</span></span> 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    <span data-ttu-id="b7b48-144">Output previsto (elenca i valori usati per i parametri):</span><span class="sxs-lookup"><span data-stu-id="b7b48-144">Expected output (lists parameter values used):</span></span>

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

