---
title: risorse aaaDeploy con Azure CLI e modello | Documenti Microsoft
description: Utilizzare Gestione risorse di Azure e Azure CLI toodeploy un tooAzure di risorse. risorse di Hello vengono definite in un modello di gestione risorse.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 493b7932-8d1e-4499-912c-26098282ec95
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: tomfitz
ms.openlocfilehash: 9f8bb9a8720399390a407030d2d32bcd97d32f13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a><span data-ttu-id="90e81-104">Distribuire le risorse con i modelli di Azure Resource Manager e l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="90e81-104">Deploy resources with Resource Manager templates and Azure CLI</span></span>

<span data-ttu-id="90e81-105">Questo argomento viene illustrato come toouse 2.0 CLI di Azure con Gestione risorse modelli toodeploy tooAzure le risorse.</span><span class="sxs-lookup"><span data-stu-id="90e81-105">This topic explains how toouse Azure CLI 2.0 with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="90e81-106">Se non si ha familiarità con concetti hello della distribuzione e gestione di soluzioni di Azure, vedere [Panoramica di gestione risorse di Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="90e81-106">If you are not familiar with hello concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>  

<span data-ttu-id="90e81-107">il modello di gestione risorse di Hello è distribuire può essere un file nel computer locale o un file esterno che si trova in un archivio come GitHub.</span><span class="sxs-lookup"><span data-stu-id="90e81-107">hello Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="90e81-108">modello Hello si distribuisce in questo articolo è disponibile in hello [modello di esempio](#sample-template) sezione, oppure come un [modello di account di archiviazione in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="90e81-108">hello template you deploy in this article is available in hello [Sample template](#sample-template) section, or as a [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

<span data-ttu-id="90e81-109">Se non si dispone di Azure CLI installato, è possibile utilizzare hello [Shell Cloud](#deploy-template-from-cloud-shell).</span><span class="sxs-lookup"><span data-stu-id="90e81-109">If you do not have Azure CLI installed, you can use hello [Cloud Shell](#deploy-template-from-cloud-shell).</span></span>

## <a name="deploy-local-template"></a><span data-ttu-id="90e81-110">Distribuire un modello locale</span><span class="sxs-lookup"><span data-stu-id="90e81-110">Deploy local template</span></span>

<span data-ttu-id="90e81-111">Quando si distribuisce tooAzure risorse, è:</span><span class="sxs-lookup"><span data-stu-id="90e81-111">When deploying resources tooAzure, you:</span></span>

1. <span data-ttu-id="90e81-112">Accedi tooyour account Azure</span><span class="sxs-lookup"><span data-stu-id="90e81-112">Log in tooyour Azure account</span></span>
2. <span data-ttu-id="90e81-113">Creare un gruppo di risorse che funge da contenitore hello per le risorse di hello distribuito.</span><span class="sxs-lookup"><span data-stu-id="90e81-113">Create a resource group that serves as hello container for hello deployed resources.</span></span> <span data-ttu-id="90e81-114">nome Hello hello del gruppo di risorse possa includere solo caratteri alfanumerici, punti, caratteri di sottolineatura, trattini e parentesi.</span><span class="sxs-lookup"><span data-stu-id="90e81-114">hello name of hello resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="90e81-115">Può trattarsi di too90 caratteri.</span><span class="sxs-lookup"><span data-stu-id="90e81-115">It can be up too90 characters.</span></span> <span data-ttu-id="90e81-116">Non può terminare con un punto.</span><span class="sxs-lookup"><span data-stu-id="90e81-116">It cannot end in a period.</span></span>
3. <span data-ttu-id="90e81-117">Distribuire toohello risorse gruppo hello modello che definisce hello risorse toocreate</span><span class="sxs-lookup"><span data-stu-id="90e81-117">Deploy toohello resource group hello template that defines hello resources toocreate</span></span>

<span data-ttu-id="90e81-118">Un modello può includere parametri che consentono la distribuzione di hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="90e81-118">A template can include parameters that enable you toocustomize hello deployment.</span></span> <span data-ttu-id="90e81-119">Può includere ad esempio valori specifici per un determinato ambiente (di sviluppo, test e produzione).</span><span class="sxs-lookup"><span data-stu-id="90e81-119">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="90e81-120">modello di esempio Hello definisce un parametro per l'account di archiviazione hello SKU.</span><span class="sxs-lookup"><span data-stu-id="90e81-120">hello sample template defines a parameter for hello storage account SKU.</span></span> 

<span data-ttu-id="90e81-121">Hello di esempio seguente crea un gruppo di risorse e distribuisce un modello dal computer locale:</span><span class="sxs-lookup"><span data-stu-id="90e81-121">hello following example creates a resource group, and deploys a template from your local machine:</span></span>

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="90e81-122">distribuzione di Hello può richiedere alcuni minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="90e81-122">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="90e81-123">Al termine, viene visualizzato un messaggio che include i risultati di hello:</span><span class="sxs-lookup"><span data-stu-id="90e81-123">When it finishes, you see a message that includes hello result:</span></span>

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a><span data-ttu-id="90e81-124">Distribuire un modello esterno</span><span class="sxs-lookup"><span data-stu-id="90e81-124">Deploy external template</span></span>

<span data-ttu-id="90e81-125">Invece di archiviare i modelli di gestione risorse nel computer locale, è preferibile toostore multipla in una posizione esterna.</span><span class="sxs-lookup"><span data-stu-id="90e81-125">Instead of storing Resource Manager templates on your local machine, you may prefer toostore them in an external location.</span></span> <span data-ttu-id="90e81-126">ad esempio in un repository di controllo del codice sorgente come GitHub.</span><span class="sxs-lookup"><span data-stu-id="90e81-126">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="90e81-127">È possibile, in alternativa, archiviarli in un account di archiviazione di Azure per consentire l'accesso condiviso nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="90e81-127">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="90e81-128">toodeploy un modello esterno, usare hello **modello uri** parametro.</span><span class="sxs-lookup"><span data-stu-id="90e81-128">toodeploy an external template, use hello **template-uri** parameter.</span></span> <span data-ttu-id="90e81-129">Utilizzare Ciao URI hello esempio toodeploy hello modello di esempio da GitHub.</span><span class="sxs-lookup"><span data-stu-id="90e81-129">Use hello URI in hello example toodeploy hello sample template from GitHub.</span></span>
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="90e81-130">Hello esempio precedente richiede un URI accessibile pubblicamente per il modello di hello, che può essere usato per la maggior parte degli scenari perché il modello non deve includere dati riservati.</span><span class="sxs-lookup"><span data-stu-id="90e81-130">hello preceding example requires a publicly accessible URI for hello template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="90e81-131">Se è necessario toospecify dati riservati (ad esempio una password di amministratore), passare il valore come parametro sicura.</span><span class="sxs-lookup"><span data-stu-id="90e81-131">If you need toospecify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="90e81-132">Tuttavia, se si desidera toobe il modello accessibile pubblicamente, è possibile proteggerli da archiviare in un contenitore di archiviazione privato.</span><span class="sxs-lookup"><span data-stu-id="90e81-132">However, if you do not want your template toobe publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="90e81-133">Per informazioni sulla distribuzione di un modello che richiede un token di firma di accesso condiviso (SAS), vedere [Distribuire un modello privato con un token di firma di accesso condiviso](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="90e81-133">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="90e81-134">Distribuire il modello da Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="90e81-134">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="90e81-135">È possibile utilizzare [Shell Cloud](../cloud-shell/overview.md) toorun hello CLI di Azure i comandi per la distribuzione del modello.</span><span class="sxs-lookup"><span data-stu-id="90e81-135">You can use [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="90e81-136">Tuttavia, è necessario caricare prima il modello in una condivisione di file hello per la Shell di Cloud.</span><span class="sxs-lookup"><span data-stu-id="90e81-136">However, you must first load your template into hello file share for your Cloud Shell.</span></span> <span data-ttu-id="90e81-137">Per informazioni sulla configurazione di Cloud Shell per il primo utilizzo, vedere [Panoramica di Azure Cloud Shell](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="90e81-137">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="90e81-138">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="90e81-138">Log in toohello [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="90e81-139">Selezionare il gruppo di risorse di Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="90e81-139">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="90e81-140">modello di nome Hello è `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="90e81-140">hello name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Selezionare il gruppo di risorse](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. <span data-ttu-id="90e81-142">Selezionare un account di archiviazione hello per la Shell di Cloud.</span><span class="sxs-lookup"><span data-stu-id="90e81-142">Select hello storage account for your Cloud Shell.</span></span>

   ![Selezionare l'account di archiviazione](./media/resource-group-template-deploy-cli/select-storage.png)

4. <span data-ttu-id="90e81-144">Selezionare **File**.</span><span class="sxs-lookup"><span data-stu-id="90e81-144">Select **Files**.</span></span>

   ![Selezione dei file](./media/resource-group-template-deploy-cli/select-files.png)

5. <span data-ttu-id="90e81-146">Selezionare condivisione file hello per Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="90e81-146">Select hello file share for Cloud Shell.</span></span> <span data-ttu-id="90e81-147">modello di nome Hello è `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="90e81-147">hello name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Selezionare la condivisione file](./media/resource-group-template-deploy-cli/select-file-share.png)

6. <span data-ttu-id="90e81-149">Selezionare **Aggiungi directory**.</span><span class="sxs-lookup"><span data-stu-id="90e81-149">Select **Add directory**.</span></span>

   ![Aggiungi directory](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. <span data-ttu-id="90e81-151">Assegnare il nome **templates** e scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="90e81-151">Name it **templates**, and select **Okay**.</span></span>

   ![Assegnare il nome alla directory](./media/resource-group-template-deploy-cli/name-templates.png)

8. <span data-ttu-id="90e81-153">Selezionare la nuova directory.</span><span class="sxs-lookup"><span data-stu-id="90e81-153">Select your new directory.</span></span>

   ![Selezionare la directory](./media/resource-group-template-deploy-cli/select-templates.png)

9. <span data-ttu-id="90e81-155">Selezionare **Carica**.</span><span class="sxs-lookup"><span data-stu-id="90e81-155">Select **Upload**.</span></span>

   ![Selezionare Carica](./media/resource-group-template-deploy-cli/select-upload.png)

10. <span data-ttu-id="90e81-157">Trovare e caricare il modello.</span><span class="sxs-lookup"><span data-stu-id="90e81-157">Find and upload your template.</span></span>

   ![Caricare il file](./media/resource-group-template-deploy-cli/upload-files.png)

11. <span data-ttu-id="90e81-159">Prompt dei comandi aprire hello.</span><span class="sxs-lookup"><span data-stu-id="90e81-159">Open hello prompt.</span></span>

   ![Aprire Cloud Shell](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. <span data-ttu-id="90e81-161">Immettere i seguenti comandi nella Shell di Cloud hello hello:</span><span class="sxs-lookup"><span data-stu-id="90e81-161">Enter hello following commands in hello Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

## <a name="parameter-files"></a><span data-ttu-id="90e81-162">File dei parametri</span><span class="sxs-lookup"><span data-stu-id="90e81-162">Parameter files</span></span>

<span data-ttu-id="90e81-163">Anziché il passaggio di parametri come valori inline nello script, può risultare più semplice toouse un file JSON che contiene i valori dei parametri hello.</span><span class="sxs-lookup"><span data-stu-id="90e81-163">Rather than passing parameters as inline values in your script, you may find it easier toouse a JSON file that contains hello parameter values.</span></span> <span data-ttu-id="90e81-164">file di parametro Hello deve essere nel seguente formato hello:</span><span class="sxs-lookup"><span data-stu-id="90e81-164">hello parameter file must be in hello following format:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

<span data-ttu-id="90e81-165">Si noti che la sezione parametri di hello include un nome di parametro corrispondente parametro hello definito nel modello (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="90e81-165">Notice that hello parameters section includes a parameter name that matches hello parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="90e81-166">file di parametro Hello contiene un valore per il parametro hello.</span><span class="sxs-lookup"><span data-stu-id="90e81-166">hello parameter file contains a value for hello parameter.</span></span> <span data-ttu-id="90e81-167">Questo valore viene passato automaticamente toohello modello durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="90e81-167">This value is automatically passed toohello template during deployment.</span></span> <span data-ttu-id="90e81-168">È possibile creare più file di parametro per diversi scenari di distribuzione e quindi passare nel file di parametro appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="90e81-168">You can create multiple parameter files for different deployment scenarios, and then pass in hello appropriate parameter file.</span></span> 

<span data-ttu-id="90e81-169">Copiare l'esempio sopra riportato hello e salvarlo come un file denominato `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="90e81-169">Copy hello preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="90e81-170">Utilizzare un file di parametro locale, toopass `@` toospecify un file locale denominato storage.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="90e81-170">toopass a local parameter file, use `@` toospecify a local file named storage.parameters.json.</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a><span data-ttu-id="90e81-171">Testare una distribuzione del modello</span><span class="sxs-lookup"><span data-stu-id="90e81-171">Test a template deployment</span></span>

<span data-ttu-id="90e81-172">Utilizzare i valori di parametro e modello senza distribuire effettivamente le risorse, tootest [distribuzione gruppo az convalidare](/cli/azure/group/deployment#validate).</span><span class="sxs-lookup"><span data-stu-id="90e81-172">tootest your template and parameter values without actually deploying any resources, use [az group deployment validate](/cli/azure/group/deployment#validate).</span></span> 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

<span data-ttu-id="90e81-173">Se non vengono rilevati errori, il comando hello restituisce informazioni sulla distribuzione dei test hello.</span><span class="sxs-lookup"><span data-stu-id="90e81-173">If no errors are detected, hello command returns information about hello test deployment.</span></span> <span data-ttu-id="90e81-174">In particolare, si noti che hello **errore** valore è null.</span><span class="sxs-lookup"><span data-stu-id="90e81-174">In particular, notice that hello **error** value is null.</span></span>

```azurecli
{
  "error": null,
  "properties": {
      ...
```

<span data-ttu-id="90e81-175">Se viene rilevato un errore, il comando hello restituisce un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="90e81-175">If an error is detected, hello command returns an error message.</span></span> <span data-ttu-id="90e81-176">Ad esempio, il tentativo di un valore non corretto per l'account di archiviazione hello SKU, toopass restituisce hello errore seguente:</span><span class="sxs-lookup"><span data-stu-id="90e81-176">For example, attempting toopass an incorrect value for hello storage account SKU, returns hello following error:</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'hello provided value 'badSKU' for hello template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. hello parameter value is not part of hello allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

<span data-ttu-id="90e81-177">Se il modello dispone di un errore di sintassi, il comando hello restituisce un errore che indica che non è stato possibile analizzare il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="90e81-177">If your template has a syntax error, hello command returns an error indicating it could not parse hello template.</span></span> <span data-ttu-id="90e81-178">messaggio Hello indica il numero di riga hello e la posizione di hello errore di analisi.</span><span class="sxs-lookup"><span data-stu-id="90e81-178">hello message indicates hello line number and position of hello parsing error.</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template parse failed: 'After parsing a value an unexpected character was encountered:
      \". Path 'variables', line 31, position 3.'.",
    "target": null
  },
  "properties": null
}
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="90e81-179">modalità completa toouse, utilizzare hello `mode` parametro:</span><span class="sxs-lookup"><span data-stu-id="90e81-179">toouse complete mode, use hello `mode` parameter:</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

## <a name="sample-template"></a><span data-ttu-id="90e81-180">Modello di esempio</span><span class="sxs-lookup"><span data-stu-id="90e81-180">Sample template</span></span>

<span data-ttu-id="90e81-181">Hello modello seguente viene utilizzato per gli esempi di hello in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="90e81-181">hello following template is used for hello examples in this topic.</span></span> <span data-ttu-id="90e81-182">Copiarlo e salvarlo come file denominato storage.json.</span><span class="sxs-lookup"><span data-stu-id="90e81-182">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="90e81-183">toounderstand come toocreate questo modello, vedere [creare il primo modello di gestione risorse di Azure](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="90e81-183">toounderstand how toocreate this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="90e81-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="90e81-184">Next steps</span></span>
* <span data-ttu-id="90e81-185">esempi di Hello in questo articolo distribuire un gruppo di risorse tooa risorse nella sottoscrizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="90e81-185">hello examples in this article deploy resources tooa resource group in your default subscription.</span></span> <span data-ttu-id="90e81-186">toouse una sottoscrizione diversa, vedere [gestiscono più sottoscrizioni Azure](/cli/azure/manage-azure-subscriptions-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="90e81-186">toouse a different subscription, see [Manage multiple Azure subscriptions](/cli/azure/manage-azure-subscriptions-azure-cli).</span></span>
* <span data-ttu-id="90e81-187">Per uno script di esempio completo che consente di distribuire un modello, vedere lo [script di distribuzione di modelli di Resource Manager](resource-manager-samples-cli-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="90e81-187">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-cli-deploy.md).</span></span>
* <span data-ttu-id="90e81-188">toounderstand toodefine parametri nel modello, vedere [comprendere hello struttura e la sintassi dei modelli di Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="90e81-188">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="90e81-189">Per suggerimenti su come risolvere i comuni errori di distribuzione, vedere [Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="90e81-189">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="90e81-190">Per informazioni sulla distribuzione di un modello che richiede un token di firma di accesso condiviso, vedere [Distribuire un modello privato con un token di firma di accesso condiviso](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="90e81-190">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="90e81-191">Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="90e81-191">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
