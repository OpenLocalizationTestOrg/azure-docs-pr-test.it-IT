---
title: il primo modello di gestione risorse di Azure aaaCreate | Documenti Microsoft
description: Toocreating una Guida dettagliata del primo modello di gestione risorse di Azure. Viene visualizzato come toouse hello riferimento di modello per un modello di archiviazione account toocreate hello.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/27/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 92e6d6bb7094fe0e4537ee080704967862804bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a><span data-ttu-id="499f7-104">Creare e distribuire il primo modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="499f7-104">Create and deploy your first Azure Resource Manager template</span></span>
<span data-ttu-id="499f7-105">In questo argomento illustra procedure hello di creazione del primo modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="499f7-105">This topic walks you through hello steps of creating your first Azure Resource Manager template.</span></span> <span data-ttu-id="499f7-106">Modelli di gestione risorse sono file JSON che definiscono le risorse di hello toodeploy è necessario per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="499f7-106">Resource Manager templates are JSON files that define hello resources you need toodeploy for your solution.</span></span> <span data-ttu-id="499f7-107">concetti di hello toounderstand associati a una distribuzione e gestione di soluzioni di Azure, vedere [Panoramica di gestione risorse di Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="499f7-107">toounderstand hello concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span> <span data-ttu-id="499f7-108">Se si dispone di risorse esistenti e si desidera tooget un modello per le risorse, vedere [esportare un modello di gestione risorse di Azure da risorse esistenti](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="499f7-108">If you have existing resources and want tooget a template for those resources, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

<span data-ttu-id="499f7-109">modelli toocreate e rivedere, è necessario un editor di JSON.</span><span class="sxs-lookup"><span data-stu-id="499f7-109">toocreate and revise templates, you need a JSON editor.</span></span> <span data-ttu-id="499f7-110">[Visual Studio Code](https://code.visualstudio.com/) è un editor di codice, leggero, open source e multipiattaforma.</span><span class="sxs-lookup"><span data-stu-id="499f7-110">[Visual Studio Code](https://code.visualstudio.com/) is a lightweight, open-source, cross-platform code editor.</span></span> <span data-ttu-id="499f7-111">È consigliabile usare Visual Studio Code per la creazione di modelli di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="499f7-111">We strongly recommend using Visual Studio Code for creating Resource Manager templates.</span></span> <span data-ttu-id="499f7-112">In questo argomento si presuppone che venga usato Visual Studio Code. Se tuttavia si ha un altro editor JSON (ad esempio, Visual Studio), è possibile usare tale editor.</span><span class="sxs-lookup"><span data-stu-id="499f7-112">This topic assumes you are using VS Code; however, if you have another JSON editor (like Visual Studio), you can use that editor.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="499f7-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="499f7-113">Prerequisites</span></span>

* <span data-ttu-id="499f7-114">Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="499f7-114">Visual Studio Code.</span></span> <span data-ttu-id="499f7-115">Se necessario, installarlo da [https://code.visualstudio.com/](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="499f7-115">If needed, install it from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="499f7-116">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="499f7-116">An Azure subscription.</span></span> <span data-ttu-id="499f7-117">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="499f7-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-template"></a><span data-ttu-id="499f7-118">Creare il modello</span><span class="sxs-lookup"><span data-stu-id="499f7-118">Create template</span></span>

<span data-ttu-id="499f7-119">Iniziamo con un modello semplice che consente di distribuire una sottoscrizione tooyour account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="499f7-119">Let's start with a simple template that deploys a storage account tooyour subscription.</span></span>

1. <span data-ttu-id="499f7-120">Selezionare **File** > **Nuovo file**.</span><span class="sxs-lookup"><span data-stu-id="499f7-120">Select **File** > **New File**.</span></span> 

   ![Nuovo file](./media/resource-manager-create-first-template/new-file.png)

2. <span data-ttu-id="499f7-122">Copiare e incollare la seguente sintassi JSON nel file hello:</span><span class="sxs-lookup"><span data-stu-id="499f7-122">Copy and paste hello following JSON syntax into your file:</span></span>

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
     },
     "variables": {
     },
     "resources": [
       {
         "name": "[concat('storage', uniqueString(resourceGroup().id))]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "sku": {
           "name": "Standard_LRS"
         },
         "kind": "Storage",
         "location": "South Central US",
         "tags": {},
         "properties": {}
       }
     ],
     "outputs": {  }
   }
   ```

   <span data-ttu-id="499f7-123">I nomi degli account di archiviazione dispone di numerose restrizioni che li rendono difficile tooset.</span><span class="sxs-lookup"><span data-stu-id="499f7-123">Storage account names have several restrictions that make them difficult tooset.</span></span> <span data-ttu-id="499f7-124">nome Hello deve essere compresa tra 3 e 24 caratteri, utilizzare solo numeri e lettere minuscole e univoco.</span><span class="sxs-lookup"><span data-stu-id="499f7-124">hello name must be between 3 and 24 characters in length, use only numbers and lower-case letters, and be unique.</span></span> <span data-ttu-id="499f7-125">il modello precedente Hello utilizza hello [uniqueString](resource-group-template-functions-string.md#uniquestring) funzione toogenerate un valore hash.</span><span class="sxs-lookup"><span data-stu-id="499f7-125">hello preceding template uses hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function toogenerate a hash value.</span></span> <span data-ttu-id="499f7-126">valore questo hash toogive più vale a dire, viene aggiunto il prefisso hello *archiviazione*.</span><span class="sxs-lookup"><span data-stu-id="499f7-126">toogive this hash value more meaning, it adds hello prefix *storage*.</span></span> 

3. <span data-ttu-id="499f7-127">Salvare questo file come **azuredeploy.json** tooa di cartella locale.</span><span class="sxs-lookup"><span data-stu-id="499f7-127">Save this file as **azuredeploy.json** tooa local folder.</span></span>

   ![Salvare il modello](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a><span data-ttu-id="499f7-129">Distribuire il modello</span><span class="sxs-lookup"><span data-stu-id="499f7-129">Deploy template</span></span>

<span data-ttu-id="499f7-130">Si sono pronti toodeploy questo modello.</span><span class="sxs-lookup"><span data-stu-id="499f7-130">You are ready toodeploy this template.</span></span> <span data-ttu-id="499f7-131">Utilizzare PowerShell o Azure CLI toocreate un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="499f7-131">You use either PowerShell or Azure CLI toocreate a resource group.</span></span> <span data-ttu-id="499f7-132">Sarà quindi possibile distribuire un gruppo di risorse toothat di account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="499f7-132">Then, you deploy a storage account toothat resource group.</span></span>

* <span data-ttu-id="499f7-133">Per PowerShell, usare hello seguendo i comandi dalla cartella hello contenente hello modello:</span><span class="sxs-lookup"><span data-stu-id="499f7-133">For PowerShell, use hello following commands from hello folder containing hello template:</span></span>

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* <span data-ttu-id="499f7-134">Per un'installazione locale di CLI di Azure, utilizzare hello seguendo i comandi dalla cartella hello contenente il modello di hello:</span><span class="sxs-lookup"><span data-stu-id="499f7-134">For a local installation of Azure CLI, use hello following commands from hello folder containing hello template:</span></span>

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

<span data-ttu-id="499f7-135">Al termine del processo di distribuzione, nel gruppo di risorse hello l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="499f7-135">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="499f7-136">Distribuire il modello da Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="499f7-136">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="499f7-137">È possibile utilizzare [Shell Cloud](../cloud-shell/overview.md) toorun hello CLI di Azure i comandi per la distribuzione del modello.</span><span class="sxs-lookup"><span data-stu-id="499f7-137">You can use [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="499f7-138">Tuttavia, è necessario caricare prima il modello in una condivisione di file hello per la Shell di Cloud.</span><span class="sxs-lookup"><span data-stu-id="499f7-138">However, you must first load your template into hello file share for your Cloud Shell.</span></span> <span data-ttu-id="499f7-139">Per informazioni sulla configurazione di Cloud Shell per il primo utilizzo, vedere [Panoramica di Azure Cloud Shell](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="499f7-139">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="499f7-140">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="499f7-140">Log in toohello [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="499f7-141">Selezionare il gruppo di risorse di Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="499f7-141">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="499f7-142">modello di nome Hello è `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="499f7-142">hello name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Selezionare il gruppo di risorse](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. <span data-ttu-id="499f7-144">Selezionare un account di archiviazione hello per la Shell di Cloud.</span><span class="sxs-lookup"><span data-stu-id="499f7-144">Select hello storage account for your Cloud Shell.</span></span>

   ![Selezionare l'account di archiviazione](./media/resource-manager-create-first-template/select-storage.png)

4. <span data-ttu-id="499f7-146">Selezionare **File**.</span><span class="sxs-lookup"><span data-stu-id="499f7-146">Select **Files**.</span></span>

   ![Selezione dei file](./media/resource-manager-create-first-template/select-files.png)

5. <span data-ttu-id="499f7-148">Selezionare condivisione file hello per Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="499f7-148">Select hello file share for Cloud Shell.</span></span> <span data-ttu-id="499f7-149">modello di nome Hello è `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="499f7-149">hello name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Selezionare la condivisione file](./media/resource-manager-create-first-template/select-file-share.png)

6. <span data-ttu-id="499f7-151">Selezionare **Aggiungi directory**.</span><span class="sxs-lookup"><span data-stu-id="499f7-151">Select **Add directory**.</span></span>

   ![Aggiungi directory](./media/resource-manager-create-first-template/select-add-directory.png)

7. <span data-ttu-id="499f7-153">Assegnare il nome **templates** e scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="499f7-153">Name it **templates**, and select **Okay**.</span></span>

   ![Assegnare il nome alla directory](./media/resource-manager-create-first-template/name-templates.png)

8. <span data-ttu-id="499f7-155">Selezionare la nuova directory.</span><span class="sxs-lookup"><span data-stu-id="499f7-155">Select your new directory.</span></span>

   ![Selezionare la directory](./media/resource-manager-create-first-template/select-templates.png)

9. <span data-ttu-id="499f7-157">Selezionare **Carica**.</span><span class="sxs-lookup"><span data-stu-id="499f7-157">Select **Upload**.</span></span>

   ![Selezionare Carica](./media/resource-manager-create-first-template/select-upload.png)

10. <span data-ttu-id="499f7-159">Trovare e caricare il modello.</span><span class="sxs-lookup"><span data-stu-id="499f7-159">Find and upload your template.</span></span>

   ![Caricare il file](./media/resource-manager-create-first-template/upload-files.png)

11. <span data-ttu-id="499f7-161">Prompt dei comandi aprire hello.</span><span class="sxs-lookup"><span data-stu-id="499f7-161">Open hello prompt.</span></span>

   ![Aprire Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. <span data-ttu-id="499f7-163">Immettere i seguenti comandi nella Shell di Cloud hello hello:</span><span class="sxs-lookup"><span data-stu-id="499f7-163">Enter hello following commands in hello Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

<span data-ttu-id="499f7-164">Al termine del processo di distribuzione, nel gruppo di risorse hello l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="499f7-164">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="customize-hello-template"></a><span data-ttu-id="499f7-165">Personalizzare il modello di hello</span><span class="sxs-lookup"><span data-stu-id="499f7-165">Customize hello template</span></span>

<span data-ttu-id="499f7-166">modello Hello funziona correttamente, ma non è flessibile.</span><span class="sxs-lookup"><span data-stu-id="499f7-166">hello template works fine, but it is not flexible.</span></span> <span data-ttu-id="499f7-167">Distribuisce sempre un tooSouth di archiviazione con ridondanza locale, Stati Uniti centrali.</span><span class="sxs-lookup"><span data-stu-id="499f7-167">It always deploys a locally redundant storage tooSouth Central US.</span></span> <span data-ttu-id="499f7-168">nome Hello è sempre *archiviazione* seguita da un valore hash.</span><span class="sxs-lookup"><span data-stu-id="499f7-168">hello name is always *storage* followed by a hash value.</span></span> <span data-ttu-id="499f7-169">tooenable utilizzando il modello di hello per diversi scenari, aggiungere parametri toohello modello.</span><span class="sxs-lookup"><span data-stu-id="499f7-169">tooenable using hello template for different scenarios, add parameters toohello template.</span></span>

<span data-ttu-id="499f7-170">Hello riportato di seguito sezione parametri hello con due parametri.</span><span class="sxs-lookup"><span data-stu-id="499f7-170">hello following example shows hello parameters section with two parameters.</span></span> <span data-ttu-id="499f7-171">primo parametro Hello `storageSKU` consente tipo hello toospecify di ridondanza.</span><span class="sxs-lookup"><span data-stu-id="499f7-171">hello first parameter `storageSKU` enables you toospecify hello type of redundancy.</span></span> <span data-ttu-id="499f7-172">Limita i valori hello che è possibile passare toovalues validi per un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="499f7-172">It limits hello values you can pass in toovalues that are valid for a storage account.</span></span> <span data-ttu-id="499f7-173">Specifica anche un valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="499f7-173">It also specifies a default value.</span></span> <span data-ttu-id="499f7-174">secondo parametro Hello `storageNamePrefix` è set tooallow un massimo di 11 caratteri.</span><span class="sxs-lookup"><span data-stu-id="499f7-174">hello second parameter `storageNamePrefix` is set tooallow a maximum of 11 characters.</span></span> <span data-ttu-id="499f7-175">Specifica un valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="499f7-175">It specifies a default value.</span></span>

```json
"parameters": {
  "storageSKU": {
    "type": "string",
    "allowedValues": [
      "Standard_LRS",
      "Standard_ZRS",
      "Standard_GRS",
      "Standard_RAGRS",
      "Premium_LRS"
    ],
    "defaultValue": "Standard_LRS",
    "metadata": {
      "description": "hello type of replication toouse for hello storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

<span data-ttu-id="499f7-176">Nella sezione variabili hello, aggiungere una variabile denominata `storageName`.</span><span class="sxs-lookup"><span data-stu-id="499f7-176">In hello variables section, add a variable named `storageName`.</span></span> <span data-ttu-id="499f7-177">Combina il valore di prefisso hello dai parametri hello e un valore hash hello [uniqueString](resource-group-template-functions-string.md#uniquestring) (funzione).</span><span class="sxs-lookup"><span data-stu-id="499f7-177">It combines hello prefix value from hello parameters and a hash value from hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span> <span data-ttu-id="499f7-178">Usa hello [toLower](resource-group-template-functions-string.md#tolower) funzione tooconvert toolowercase di tutti i caratteri.</span><span class="sxs-lookup"><span data-stu-id="499f7-178">It uses hello [toLower](resource-group-template-functions-string.md#tolower) function tooconvert all characters toolowercase.</span></span>

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

<span data-ttu-id="499f7-179">toouse questi nuovi valori per l'account di archiviazione, modificare la definizione di risorsa hello:</span><span class="sxs-lookup"><span data-stu-id="499f7-179">toouse these new values for your storage account, change hello resource definition:</span></span>

```json
"resources": [
  {
    "name": "[variables('storageName')]",
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2016-01-01",
    "sku": {
      "name": "[parameters('storageSKU')]"
    },
    "kind": "Storage",
    "location": "[resourceGroup().location]",
    "tags": {},
    "properties": {}
  }
],
```

<span data-ttu-id="499f7-180">Si noti che hello nome dell'account di archiviazione hello è ora impostato variabile toohello che è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="499f7-180">Notice that hello name of hello storage account is now set toohello variable that you added.</span></span> <span data-ttu-id="499f7-181">nome SKU Hello è impostato un valore toohello del parametro hello.</span><span class="sxs-lookup"><span data-stu-id="499f7-181">hello SKU name is set toohello value of hello parameter.</span></span> <span data-ttu-id="499f7-182">ubicazione Hello hello stesso percorso del gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="499f7-182">hello location is set hello same location as hello resource group.</span></span>

<span data-ttu-id="499f7-183">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="499f7-183">Save your file.</span></span> 

<span data-ttu-id="499f7-184">Dopo aver completato i passaggi di hello in questo articolo, il modello è ora simile a:</span><span class="sxs-lookup"><span data-stu-id="499f7-184">After completing hello steps in this article, your template now looks like:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
      }
    }
  },
  "variables": {
    "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {}
    }
  ],
  "outputs": {  }
}
```

## <a name="redeploy-template"></a><span data-ttu-id="499f7-185">Ridistribuire il modello</span><span class="sxs-lookup"><span data-stu-id="499f7-185">Redeploy template</span></span>

<span data-ttu-id="499f7-186">Ridistribuire il modello di hello con valori diversi.</span><span class="sxs-lookup"><span data-stu-id="499f7-186">Redeploy hello template with different values.</span></span>

<span data-ttu-id="499f7-187">Per PowerShell, usare:</span><span class="sxs-lookup"><span data-stu-id="499f7-187">For PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

<span data-ttu-id="499f7-188">Per l'interfaccia della riga di comando di Azure usare:</span><span class="sxs-lookup"><span data-stu-id="499f7-188">For Azure CLI, use:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

<span data-ttu-id="499f7-189">Per hello Shell Cloud, è possibile caricare la condivisione di file toohello modello modificato.</span><span class="sxs-lookup"><span data-stu-id="499f7-189">For hello Cloud Shell, upload your changed template toohello file share.</span></span> <span data-ttu-id="499f7-190">Sovrascrivi file esistente hello.</span><span class="sxs-lookup"><span data-stu-id="499f7-190">Overwrite hello existing file.</span></span> <span data-ttu-id="499f7-191">Usare quindi hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="499f7-191">Then, use hello following command:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a><span data-ttu-id="499f7-192">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="499f7-192">Clean up resources</span></span>

<span data-ttu-id="499f7-193">Quando non è più necessario, è possibile pulire le risorse di hello che eliminando il gruppo di risorse hello è stato distribuito.</span><span class="sxs-lookup"><span data-stu-id="499f7-193">When no longer needed, clean up hello resources you deployed by deleting hello resource group.</span></span>

<span data-ttu-id="499f7-194">Per PowerShell, usare:</span><span class="sxs-lookup"><span data-stu-id="499f7-194">For PowerShell, use:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

<span data-ttu-id="499f7-195">Per l'interfaccia della riga di comando di Azure usare:</span><span class="sxs-lookup"><span data-stu-id="499f7-195">For Azure CLI, use:</span></span>

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a><span data-ttu-id="499f7-196">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="499f7-196">Next steps</span></span>
* <span data-ttu-id="499f7-197">toolearn ulteriori informazioni su struttura hello di un modello, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="499f7-197">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="499f7-198">toolearn sulle proprietà hello per un account di archiviazione, vedere [riferimento del modello gli account di archiviazione](/azure/templates/microsoft.storage/storageaccounts).</span><span class="sxs-lookup"><span data-stu-id="499f7-198">toolearn about hello properties for a storage account, see [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts).</span></span>
* <span data-ttu-id="499f7-199">modelli completo di tooview per molti tipi diversi di soluzioni, vedere hello [modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="499f7-199">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
