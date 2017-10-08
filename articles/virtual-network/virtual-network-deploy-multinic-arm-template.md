---
title: "aaaCreate una macchina virtuale con più schede di rete: modello di gestione risorse di Azure | Documenti Microsoft"
description: "Creare una VM con più schede di interfaccia di rete mediante un modello di Azure Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 486f7dd5-cf2f-434c-85d1-b3e85c427def
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5d9ffcbd40c72dc18ae6de38e739eb5e45bf669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a><span data-ttu-id="0b472-103">Creare una macchina virtuale con più schede di interfaccia di rete usando un modello</span><span class="sxs-lookup"><span data-stu-id="0b472-103">Create a VM with multiple NICs using a template</span></span>
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="0b472-104">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0b472-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="0b472-105">In questo articolo viene illustrato l'utilizzo modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché hello [modello di distribuzione classica](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0b472-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="0b472-106">i passaggi seguenti Hello utilizzano un gruppo di risorse denominato *IaaSStory* per i server WEB di hello e un gruppo di risorse denominato *IaaSStory-back-end* per i server hello DB.</span><span class="sxs-lookup"><span data-stu-id="0b472-106">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b472-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0b472-107">Prerequisites</span></span>
<span data-ttu-id="0b472-108">Prima di poter creare hello server di database, è necessario hello toocreate *IaaSStory* gruppo di risorse con tutte le risorse necessarie hello per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="0b472-108">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="0b472-109">completare queste risorse, toocreate hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0b472-109">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="0b472-110">Passare troppo[pagina modello hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="0b472-110">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="0b472-111">Nella pagina toohello destra del modello di hello **gruppo di risorse padre**, fare clic su **distribuire tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="0b472-111">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="0b472-112">Se necessario, modificare i valori di parametro hello, quindi seguire i passaggi hello nel gruppo di risorse hello toodeploy portale hello anteprima di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b472-112">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b472-113">Assicurarsi che i nomi degli account di archiviazione siano univoci.</span><span class="sxs-lookup"><span data-stu-id="0b472-113">Make sure your storage account names are unique.</span></span> <span data-ttu-id="0b472-114">In Azure non sono infatti ammessi nomi di account di archiviazione duplicati.</span><span class="sxs-lookup"><span data-stu-id="0b472-114">You cannot have duplicate storage account names in Azure.</span></span>
> 

## <a name="understand-hello-deployment-template"></a><span data-ttu-id="0b472-115">Comprendere il modello di distribuzione hello</span><span class="sxs-lookup"><span data-stu-id="0b472-115">Understand hello deployment template</span></span>
<span data-ttu-id="0b472-116">Prima di distribuire il modello di hello fornito con questa documentazione, assicurarsi che comprendere le funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0b472-116">Before you deploy hello template provided with this documentation, make sure you understand what it does.</span></span> <span data-ttu-id="0b472-117">Hello passaggi fornita una buona panoramica del modello di hello:</span><span class="sxs-lookup"><span data-stu-id="0b472-117">hello following steps provide a good overview of hello template:</span></span>

1. <span data-ttu-id="0b472-118">Passare troppo[pagina modello hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="0b472-118">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="0b472-119">Fare clic su **azuredeploy.json** tooopen file di modello hello.</span><span class="sxs-lookup"><span data-stu-id="0b472-119">Click **azuredeploy.json** tooopen hello template file.</span></span>
3. <span data-ttu-id="0b472-120">Hello preavviso *osType* parametro elencato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0b472-120">Notice hello *osType* parameter listed below.</span></span> <span data-ttu-id="0b472-121">Questo parametro è utilizzato tooselect quali toouse immagine di macchina virtuale per server di database hello, insieme al sistema operativo più le impostazioni correlate.</span><span class="sxs-lookup"><span data-stu-id="0b472-121">This parameter is used tooselect what VM image toouse for hello database server, along with multiple operating system related settings.</span></span>

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS toouse for VMs: Windows or Ubuntu."
      }
    },
    ```

4. <span data-ttu-id="0b472-122">Scorrere verso il basso toohello elenco di variabili e controllare la definizione di hello per hello **dbVMSetting** variabili, elencate di seguito.</span><span class="sxs-lookup"><span data-stu-id="0b472-122">Scroll down toohello list of variables, and check hello definition for hello **dbVMSetting** variables, listed below.</span></span> <span data-ttu-id="0b472-123">Riceve uno degli elementi di matrice hello contenuti in hello **dbVMSettings** variabile.</span><span class="sxs-lookup"><span data-stu-id="0b472-123">It receives one of hello array elements contained in hello **dbVMSettings** variable.</span></span> <span data-ttu-id="0b472-124">Se si ha familiarità con la terminologia di sviluppo software, è possibile visualizzare hello **dbVMSettings** variabile come una tabella hash o un dizionario.</span><span class="sxs-lookup"><span data-stu-id="0b472-124">If you are familiar with software development terminology, you can view hello **dbVMSettings** variable as a hash table, or a dictionary.</span></span>

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. <span data-ttu-id="0b472-125">È possibile decidere toodeploy macchine virtuali di Windows in esecuzione SQL in hello back-end.</span><span class="sxs-lookup"><span data-stu-id="0b472-125">Suppose you decide toodeploy Windows VMs running SQL in hello back-end.</span></span> <span data-ttu-id="0b472-126">Quindi hello valore per **osType** sarebbe *Windows*, hello e **dbVMSetting** variabile conterrebbe elemento hello elencato di seguito, che rappresenta il valore prima di hello in hello **dbVMSettings** variabile.</span><span class="sxs-lookup"><span data-stu-id="0b472-126">Then hello value for **osType** would be *Windows*, and hello **dbVMSetting** variable would contain hello element listed below, which represents hello first value in hello **dbVMSettings** variable.</span></span>

    ```json
    "Windows": {
      "vmSize": "Standard_DS3",
      "publisher": "MicrosoftSQLServer",
      "offer": "SQL2014SP1-WS2012R2",
      "sku": "Standard",
      "version": "latest",
      "vmName": "DB",
      "osdisk": "osdiskdb",
      "datadisk": "datadiskdb",
      "nicName": "NICDB",
      "ipAddress": "192.168.2.",
      "extensionDeployment": "",
      "avsetName": "ASDB",
      "remotePort": 3389,
      "dbPort": 1433
    },
    ```

6. <span data-ttu-id="0b472-127">Hello preavviso **vmSize** contiene il valore di hello *Standard_DS3*.</span><span class="sxs-lookup"><span data-stu-id="0b472-127">Notice hello **vmSize** contains hello value *Standard_DS3*.</span></span> <span data-ttu-id="0b472-128">Solo determinate dimensioni di macchina virtuale consentono di utilizzare hello di più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="0b472-128">Only certain VM sizes allow for hello use of multiple NICs.</span></span> <span data-ttu-id="0b472-129">È possibile verificare le dimensioni delle macchine Virtuali supportano più schede di rete tramite la lettura di hello [dimensioni delle macchine Virtuali di Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [le dimensioni di VM Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articoli.</span><span class="sxs-lookup"><span data-stu-id="0b472-129">You can verify which VM sizes support multiple NICs by reading hello [Windows VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux VM sizes](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articles.</span></span>

7. <span data-ttu-id="0b472-130">Scorrere verso il basso troppo**risorse** e hello primo elemento.</span><span class="sxs-lookup"><span data-stu-id="0b472-130">Scroll down too**resources** and notice hello first element.</span></span> <span data-ttu-id="0b472-131">Questo descrive un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="0b472-131">It describes a storage account.</span></span> <span data-ttu-id="0b472-132">Questo account di archiviazione sarà dischi di dati utilizzati toomaintain hello utilizzati da ogni macchina virtuale del database.</span><span class="sxs-lookup"><span data-stu-id="0b472-132">This storage account will be used toomaintain hello data disks used by each database VM.</span></span> <span data-ttu-id="0b472-133">In questo scenario, ogni macchina virtuale del database dispone di un disco del sistema operativo archiviato nell'archiviazione consueta e due dischi dati archiviati nell'archiviazione dell'unità SSD (premium).</span><span class="sxs-lookup"><span data-stu-id="0b472-133">In this scenario, each database VM has an OS disk stored in regular storage, and two data disks stored in SSD (premium) storage.</span></span>

    ```json
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[parameters('prmStorageName')]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "Storage Account - Premium"
      },
      "properties": {
      "accountType": "[parameters('prmStorageType')]"
      }
    },
    ```

8. <span data-ttu-id="0b472-134">Scorrere verso il basso toohello risorsa successiva, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0b472-134">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="0b472-135">Questa risorsa rappresenta hello che NIC utilizzato per l'accesso al database in ogni macchina virtuale del database.</span><span class="sxs-lookup"><span data-stu-id="0b472-135">This resource represents hello NIC used for database access in each database VM.</span></span> <span data-ttu-id="0b472-136">Utilizzo di hello preavviso di hello **copia** funzione in questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="0b472-136">Notice hello use of hello **copy** function in this resource.</span></span> <span data-ttu-id="0b472-137">modello Hello consente toodeploy come più macchine virtuali che si desidera, in base a hello **dbCount** parametro.</span><span class="sxs-lookup"><span data-stu-id="0b472-137">hello template allows you toodeploy as many VMs as you want, based on hello **dbCount** parameter.</span></span> <span data-ttu-id="0b472-138">È pertanto necessario toocreate hello stessa quantità di schede di rete per l'accesso al database, uno per ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0b472-138">Therefore you need toocreate hello same amount of NICs for database access, one for each VM.</span></span>

    ```json
    {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[concat(variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DB DA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(4))]",
            "subnet": {
              "id": "[variables('backEndSubnetRef')]"
            }
          }
         }
       ] 
     }
    },
    ```

9. <span data-ttu-id="0b472-139">Scorrere verso il basso toohello risorsa successiva, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0b472-139">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="0b472-140">Questa risorsa rappresenta hello che NIC utilizzato per la gestione in ogni macchina virtuale del database.</span><span class="sxs-lookup"><span data-stu-id="0b472-140">This resource represents hello NIC used for management in each database VM.</span></span> <span data-ttu-id="0b472-141">Ancora una volta, è necessaria una di queste schede di interfaccia di rete per ogni macchina virtuale del database.</span><span class="sxs-lookup"><span data-stu-id="0b472-141">Once again, you need one of these NICs for each database VM.</span></span> <span data-ttu-id="0b472-142">Hello preavviso **sicurezza di rete** elemento, il collegamento di un gruppo che consente accesso tooRDP/SSH toothis NIC solo.</span><span class="sxs-lookup"><span data-stu-id="0b472-142">Notice hello **networkSecurityGroup** element, linking an NSG that allows access tooRDP/SSH toothis NIC only.</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[concat(variables('dbVMSetting').nicName, '-RA-',copyindex(1))]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "NetworkInterfaces - DB RA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "networkSecurityGroup": {
             "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('remoteAccessNSGName'))]"
             },
             "privateIPAllocationMethod": "Static",
             "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(54))]",
             "subnet": {
              "id": "[variables('backEndSubnetRef')]"
             }
           }
          }
        ]
      }
    },
```

10. <span data-ttu-id="0b472-143">Scorrere verso il basso toohello risorsa successiva, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0b472-143">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="0b472-144">Questa risorsa rappresenta un toobe di set di disponibilità condiviso da tutte le macchine virtuali di database.</span><span class="sxs-lookup"><span data-stu-id="0b472-144">This resource represents an availability set toobe shared by all database VMs.</span></span> <span data-ttu-id="0b472-145">In questo modo si garantisce che sarà sempre presente una macchina virtuale in hello impostata in esecuzione durante la manutenzione.</span><span class="sxs-lookup"><span data-stu-id="0b472-145">That way, you guarantee that there will always be one VM in hello set running during maintenance.</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/availabilitySets",
      "name": "[variables('dbVMSetting').avsetName]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "AvailabilitySet - DB"
      }
    },
    ```

11. <span data-ttu-id="0b472-146">Scorrere verso il basso toohello successiva risorsa.</span><span class="sxs-lookup"><span data-stu-id="0b472-146">Scroll down toohello next resource.</span></span> <span data-ttu-id="0b472-147">Questa risorsa rappresenta database hello macchine virtuali, come illustrato in hello innanzitutto alcune righe elencate di seguito.</span><span class="sxs-lookup"><span data-stu-id="0b472-147">This resource represents hello database VMs, as seen in hello first few lines listed below.</span></span> <span data-ttu-id="0b472-148">Utilizzo di hello preavviso di hello **copia** di nuovo, assicurando che vengano create più macchine virtuali in base a hello **dbCount** parametro.</span><span class="sxs-lookup"><span data-stu-id="0b472-148">Notice hello use of hello **copy** function again, ensuring that multiple VMs are created based on hello **dbCount** parameter.</span></span> <span data-ttu-id="0b472-149">Si noti inoltre hello **dependsOn** insieme.</span><span class="sxs-lookup"><span data-stu-id="0b472-149">Also notice hello **dependsOn** collection.</span></span> <span data-ttu-id="0b472-150">Vengono elencati due schede di rete viene toobe necessarie creato prima macchina virtuale viene distribuita insieme al set di disponibilità hello e account di archiviazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="0b472-150">It lists two NICs being necessary toobe created before hello VM is deployed, along with hello availability set, and hello storage account.</span></span>

    ```json
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('dbVMSetting').vmName,copyindex(1))]",
    "location": "[variables('location')]",
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-RA-', copyindex(1))]",
      "[concat('Microsoft.Compute/availabilitySets/', variables('dbVMSetting').avsetName)]",
      "[concat('Microsoft.Storage/storageAccounts/', parameters('prmStorageName'))]"
    ],
    "tags": {
      "displayName": "VMs - DB"
    },
    "copy": {
      "name": "dbvmcount",
      "count": "[parameters('dbCount')]"
    },
    ```

12. <span data-ttu-id="0b472-151">Scorrere verso il basso hello VM risorsa toohello **profilo** elemento, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0b472-151">Scroll down in hello VM resource toohello **networkProfile** element, as listed below.</span></span> <span data-ttu-id="0b472-152">Si noti che sono presenti due schede di interfaccia di rete a cui ogni macchina virtuale fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="0b472-152">Notice that there are two NICs being reference for each VM.</span></span> <span data-ttu-id="0b472-153">Quando si creano più schede di rete per una macchina virtuale, è necessario impostare hello **primario** proprietà di una delle schede di rete hello troppo*true*, e hello rest troppo*false*.</span><span class="sxs-lookup"><span data-stu-id="0b472-153">When you create multiple NICs for a VM, you must set hello **primary** property of one of hello NICs too*true*, and hello rest too*false*.</span></span>

    ```json
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-DA-',copyindex(1)))]",
          "properties": { "primary": true }
        },
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-RA-',copyindex(1)))]",
          "properties": { "primary": false }
        }
      ]
    }
    ```

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a><span data-ttu-id="0b472-154">Distribuire il modello ARM hello utilizzando fare clic su toodeploy</span><span class="sxs-lookup"><span data-stu-id="0b472-154">Deploy hello ARM template by using click toodeploy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b472-155">È necessario seguire hello [prerequisiti](#Pre-requisites) passaggi prima di seguire le istruzioni di hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="0b472-155">Make sure you follow hello [pre-requisites](#Pre-requisites) steps before following hello instructions below.</span></span>
> 

<span data-ttu-id="0b472-156">modello di Hello esempio disponibile nel repository pubblico hello utilizza un file di parametro contenente hello predefiniti i valori utilizzati toogenerate hello lo scenario descritto sopra.</span><span class="sxs-lookup"><span data-stu-id="0b472-156">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="0b472-157">toodeploy questo modello utilizzando fare clic su toodeploy, seguire [questo collegamento](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello destra **gruppo di risorse di back-end (vedere la documentazione)** fare clic su **distribuire tooAzure**, sostituire Hello valori di parametro predefiniti se necessario e seguire le istruzioni di hello nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="0b472-157">toodeploy this template using click toodeploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello right of **Backend resource group (see documentation)** click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

<span data-ttu-id="0b472-158">Figura Hello seguente mostra i contenuti di hello del hello nuovo gruppo di risorse, dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0b472-158">hello figure below shows hello contents of hello new resource group, after deployment.</span></span>

![Gruppo di risorse di back-end](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="0b472-160">Distribuire il modello di hello tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b472-160">Deploy hello template by using PowerShell</span></span>
<span data-ttu-id="0b472-161">modello di hello toodeploy scaricato tramite PowerShell, installare e configurare PowerShell completando i passaggi hello hello [installare e configurare PowerShell](/powershell/azure/overview) articolo e quindi completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0b472-161">toodeploy hello template you downloaded by using PowerShell, install and configure PowerShell by completing hello steps in hello [Install and configure PowerShell](/powershell/azure/overview) article and then complete hello following steps:</span></span>

<span data-ttu-id="0b472-162">Eseguire hello  **`New-AzureRmResourceGroup`**  toocreate cmdlet un gruppo di risorse utilizzando hello modello.</span><span class="sxs-lookup"><span data-stu-id="0b472-162">Run hello **`New-AzureRmResourceGroup`** cmdlet toocreate a resource group using hello template.</span></span>

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

<span data-ttu-id="0b472-163">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="0b472-163">Expected output:</span></span>

    ResourceGroupName : IaaSStory-Backend
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    Permissions       :
                        Actions  NotActions
                        =======  ==========
                        *
        Resources         :
                        Name                 Type                                 Location
                        ===================  ===================================  ========
                        ASDB                 Microsoft.Compute/availabilitySets   westus  
                        DB1                  Microsoft.Compute/virtualMachines    westus  
                        DB2                  Microsoft.Compute/virtualMachines    westus  
                        NICDB-DA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-DA-2           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-2           Microsoft.Network/networkInterfaces  westus  
                        wtestvnetstorageprm  Microsoft.Storage/storageAccounts    westus  
    ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="0b472-164">Distribuire il modello di hello utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="0b472-164">Deploy hello template by using hello Azure CLI</span></span>
<span data-ttu-id="0b472-165">modello di hello toodeploy utilizzando hello CLI di Azure, seguire i passaggi di hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="0b472-165">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="0b472-166">Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0b472-166">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="0b472-167">Eseguire hello  **`azure config mode`**  tooswitch tooResource Manager modalità comando, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0b472-167">Run hello **`azure config mode`** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="0b472-168">Hello è previsto output indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0b472-168">hello expected output follows:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="0b472-169">Aprire hello [file dei parametri](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), selezionare il contenuto e salvarlo tooa file nel computer.</span><span class="sxs-lookup"><span data-stu-id="0b472-169">Open hello [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), select its contents, and save it tooa file in your computer.</span></span> <span data-ttu-id="0b472-170">Per questo esempio, sono stati salvati i file di parametri hello troppo*parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="0b472-170">For this example, we saved hello parameters file too*parameters.json*.</span></span>
4. <span data-ttu-id="0b472-171">Eseguire hello  **`azure group deployment create`**  cmdlet toodeploy hello nuova rete virtuale utilizzando il modello di hello e parametro file scaricato e modificato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0b472-171">Run hello **`azure group deployment create`** cmdlet toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="0b472-172">elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.</span><span class="sxs-lookup"><span data-stu-id="0b472-172">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    <span data-ttu-id="0b472-173">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="0b472-173">Expected output:</span></span>
   
        info:    Executing command group create
        + Getting resource group IaaSStory-Backend
        + Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

