---
title: Distribuire le risorse con il modello e l'interfaccia della riga di comando di Azure | Microsoft Docs
description: Utilizzare Azure Resource Manager e l'interfaccia della riga di comando di Azure per distribuire una risorsa in Azure. Le risorse sono definite in un modello di Resource Manager.
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
ms.openlocfilehash: 4f1d5f4cc48470f8906edb28628006dd1996bd3a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a><span data-ttu-id="3ac97-104">Distribuire le risorse con i modelli di Azure Resource Manager e l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="3ac97-104">Deploy resources with Resource Manager templates and Azure CLI</span></span>

<span data-ttu-id="3ac97-105">Questo argomento illustra come usare l'interfaccia della riga di comando di Azure 2.0 con modelli di Resource Manager per distribuire risorse in Azure.</span><span class="sxs-lookup"><span data-stu-id="3ac97-105">This topic explains how to use Azure CLI 2.0 with Resource Manager templates to deploy your resources to Azure.</span></span> <span data-ttu-id="3ac97-106">Per comprendere i concetti di distribuzione e gestione delle soluzioni di Azure, vedere [Panoramica di Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3ac97-106">If you are not familiar with the concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>  

<span data-ttu-id="3ac97-107">Il modello di Resource Manager che si distribuisce può essere un file locale nel computer o un file esterno che si trova in un repository come GitHub.</span><span class="sxs-lookup"><span data-stu-id="3ac97-107">The Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="3ac97-108">Il modello che viene distribuito in questo articolo è disponibile nella sezione [Modello di esempio](#sample-template) o come [modello di account di archiviazione in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="3ac97-108">The template you deploy in this article is available in the [Sample template](#sample-template) section, or as a [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

<span data-ttu-id="3ac97-109">Se l'interfaccia della riga di comando di Azure non è installata, è possibile usare [Cloud Shell](#deploy-template-from-cloud-shell).</span><span class="sxs-lookup"><span data-stu-id="3ac97-109">If you do not have Azure CLI installed, you can use the [Cloud Shell](#deploy-template-from-cloud-shell).</span></span>

## <a name="deploy-local-template"></a><span data-ttu-id="3ac97-110">Distribuire un modello locale</span><span class="sxs-lookup"><span data-stu-id="3ac97-110">Deploy local template</span></span>

<span data-ttu-id="3ac97-111">Per distribuire le risorse in Azure, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3ac97-111">When deploying resources to Azure, you:</span></span>

1. <span data-ttu-id="3ac97-112">Accedere all'account Azure</span><span class="sxs-lookup"><span data-stu-id="3ac97-112">Log in to your Azure account</span></span>
2. <span data-ttu-id="3ac97-113">Creare un gruppo di risorse che funge da contenitore per le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="3ac97-113">Create a resource group that serves as the container for the deployed resources.</span></span> <span data-ttu-id="3ac97-114">Il nome del gruppo di risorse può contenere solo caratteri alfanumerici, punti, caratteri di sottolineatura, trattini e parentesi.</span><span class="sxs-lookup"><span data-stu-id="3ac97-114">The name of the resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="3ac97-115">Può contenere fino a 90 caratteri.</span><span class="sxs-lookup"><span data-stu-id="3ac97-115">It can be up to 90 characters.</span></span> <span data-ttu-id="3ac97-116">Non può terminare con un punto.</span><span class="sxs-lookup"><span data-stu-id="3ac97-116">It cannot end in a period.</span></span>
3. <span data-ttu-id="3ac97-117">Distribuire nel gruppo di risorse il modello che definisce le risorse da creare.</span><span class="sxs-lookup"><span data-stu-id="3ac97-117">Deploy to the resource group the template that defines the resources to create</span></span>

<span data-ttu-id="3ac97-118">Un modello può includere parametri che consentono di personalizzare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3ac97-118">A template can include parameters that enable you to customize the deployment.</span></span> <span data-ttu-id="3ac97-119">Può includere ad esempio valori specifici per un determinato ambiente (di sviluppo, test e produzione).</span><span class="sxs-lookup"><span data-stu-id="3ac97-119">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="3ac97-120">Il modello di esempio definisce un parametro per lo SKU dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3ac97-120">The sample template defines a parameter for the storage account SKU.</span></span> 

<span data-ttu-id="3ac97-121">L'esempio seguente crea un gruppo di risorse e distribuisce un modello dal computer locale:</span><span class="sxs-lookup"><span data-stu-id="3ac97-121">The following example creates a resource group, and deploys a template from your local machine:</span></span>

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="3ac97-122">Per il completamento della distribuzione sarà necessario attendere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="3ac97-122">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="3ac97-123">Al termine, viene visualizzato un messaggio che include il risultato:</span><span class="sxs-lookup"><span data-stu-id="3ac97-123">When it finishes, you see a message that includes the result:</span></span>

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a><span data-ttu-id="3ac97-124">Distribuire un modello esterno</span><span class="sxs-lookup"><span data-stu-id="3ac97-124">Deploy external template</span></span>

<span data-ttu-id="3ac97-125">Anziché archiviare i modelli di Resource Manager nel computer locale, è consigliabile archiviarli in una posizione esterna,</span><span class="sxs-lookup"><span data-stu-id="3ac97-125">Instead of storing Resource Manager templates on your local machine, you may prefer to store them in an external location.</span></span> <span data-ttu-id="3ac97-126">ad esempio in un repository di controllo del codice sorgente come GitHub.</span><span class="sxs-lookup"><span data-stu-id="3ac97-126">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="3ac97-127">È possibile, in alternativa, archiviarli in un account di archiviazione di Azure per consentire l'accesso condiviso nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="3ac97-127">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="3ac97-128">Per distribuire un modello esterno, usare il parametro **template-uri**.</span><span class="sxs-lookup"><span data-stu-id="3ac97-128">To deploy an external template, use the **template-uri** parameter.</span></span> <span data-ttu-id="3ac97-129">Usare l'URI indicato nell'esempio per distribuire il modello di esempio da GitHub.</span><span class="sxs-lookup"><span data-stu-id="3ac97-129">Use the URI in the example to deploy the sample template from GitHub.</span></span>
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="3ac97-130">L'esempio precedente richiede l'utilizzo di un URI accessibile pubblicamente per il modello, che funziona per la maggior parte degli scenari. Il proprio modello non deve infatti includere dati riservati.</span><span class="sxs-lookup"><span data-stu-id="3ac97-130">The preceding example requires a publicly accessible URI for the template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="3ac97-131">Se è necessario specificare dati riservati, ad esempio una password di amministratore, passare il valore come parametro protetto.</span><span class="sxs-lookup"><span data-stu-id="3ac97-131">If you need to specify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="3ac97-132">Se invece si preferisce che il modello usato non sia accessibile pubblicamente, è possibile proteggerlo archiviandolo in un contenitore di archiviazione privato.</span><span class="sxs-lookup"><span data-stu-id="3ac97-132">However, if you do not want your template to be publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="3ac97-133">Per informazioni sulla distribuzione di un modello che richiede un token di firma di accesso condiviso (SAS), vedere [Distribuire un modello privato con un token di firma di accesso condiviso](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="3ac97-133">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="3ac97-134">Distribuire il modello da Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="3ac97-134">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="3ac97-135">È possibile usare [Cloud Shell](../cloud-shell/overview.md) per eseguire i comandi dell'interfaccia della riga di comando di Azure per la distribuzione del modello.</span><span class="sxs-lookup"><span data-stu-id="3ac97-135">You can use [Cloud Shell](../cloud-shell/overview.md) to run the Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="3ac97-136">Tuttavia, è prima necessario caricare il modello nella condivisione file per Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="3ac97-136">However, you must first load your template into the file share for your Cloud Shell.</span></span> <span data-ttu-id="3ac97-137">Per informazioni sulla configurazione di Cloud Shell per il primo utilizzo, vedere [Panoramica di Azure Cloud Shell](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="3ac97-137">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="3ac97-138">Accedere al [Portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3ac97-138">Log in to the [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="3ac97-139">Selezionare il gruppo di risorse di Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="3ac97-139">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="3ac97-140">Il modello del nome è `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="3ac97-140">The name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Selezionare il gruppo di risorse](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. <span data-ttu-id="3ac97-142">Selezionare l'account di archiviazione per Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="3ac97-142">Select the storage account for your Cloud Shell.</span></span>

   ![Selezionare l'account di archiviazione](./media/resource-group-template-deploy-cli/select-storage.png)

4. <span data-ttu-id="3ac97-144">Selezionare **File**.</span><span class="sxs-lookup"><span data-stu-id="3ac97-144">Select **Files**.</span></span>

   ![Selezione dei file](./media/resource-group-template-deploy-cli/select-files.png)

5. <span data-ttu-id="3ac97-146">Selezionare la condivisione file per Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="3ac97-146">Select the file share for Cloud Shell.</span></span> <span data-ttu-id="3ac97-147">Il modello del nome è `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="3ac97-147">The name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Selezionare la condivisione file](./media/resource-group-template-deploy-cli/select-file-share.png)

6. <span data-ttu-id="3ac97-149">Selezionare **Aggiungi directory**.</span><span class="sxs-lookup"><span data-stu-id="3ac97-149">Select **Add directory**.</span></span>

   ![Aggiungi directory](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. <span data-ttu-id="3ac97-151">Assegnare il nome **templates** e scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="3ac97-151">Name it **templates**, and select **Okay**.</span></span>

   ![Assegnare il nome alla directory](./media/resource-group-template-deploy-cli/name-templates.png)

8. <span data-ttu-id="3ac97-153">Selezionare la nuova directory.</span><span class="sxs-lookup"><span data-stu-id="3ac97-153">Select your new directory.</span></span>

   ![Selezionare la directory](./media/resource-group-template-deploy-cli/select-templates.png)

9. <span data-ttu-id="3ac97-155">Selezionare **Carica**.</span><span class="sxs-lookup"><span data-stu-id="3ac97-155">Select **Upload**.</span></span>

   ![Selezionare Carica](./media/resource-group-template-deploy-cli/select-upload.png)

10. <span data-ttu-id="3ac97-157">Trovare e caricare il modello.</span><span class="sxs-lookup"><span data-stu-id="3ac97-157">Find and upload your template.</span></span>

   ![Caricare il file](./media/resource-group-template-deploy-cli/upload-files.png)

11. <span data-ttu-id="3ac97-159">Aprire il prompt.</span><span class="sxs-lookup"><span data-stu-id="3ac97-159">Open the prompt.</span></span>

   ![Aprire Cloud Shell](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. <span data-ttu-id="3ac97-161">Immettere i comandi seguenti in Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="3ac97-161">Enter the following commands in the Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

## <a name="parameter-files"></a><span data-ttu-id="3ac97-162">File dei parametri</span><span class="sxs-lookup"><span data-stu-id="3ac97-162">Parameter files</span></span>

<span data-ttu-id="3ac97-163">Invece di passare i parametri come valori inline nello script, può risultare più facile usare un file JSON che contenga i valori dei parametri.</span><span class="sxs-lookup"><span data-stu-id="3ac97-163">Rather than passing parameters as inline values in your script, you may find it easier to use a JSON file that contains the parameter values.</span></span> <span data-ttu-id="3ac97-164">Il file dei parametri deve essere nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="3ac97-164">The parameter file must be in the following format:</span></span>

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

<span data-ttu-id="3ac97-165">Si noti che la sezione dei parametri include un nome di parametro che corrisponde al parametro definito nel modello (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="3ac97-165">Notice that the parameters section includes a parameter name that matches the parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="3ac97-166">Il file dei parametri contiene un valore per il parametro.</span><span class="sxs-lookup"><span data-stu-id="3ac97-166">The parameter file contains a value for the parameter.</span></span> <span data-ttu-id="3ac97-167">Questo valore viene passato automaticamente al modello durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3ac97-167">This value is automatically passed to the template during deployment.</span></span> <span data-ttu-id="3ac97-168">È possibile creare più file dei parametri per scenari di distribuzione diversi e successivamente passare il file dei parametri appropriato.</span><span class="sxs-lookup"><span data-stu-id="3ac97-168">You can create multiple parameter files for different deployment scenarios, and then pass in the appropriate parameter file.</span></span> 

<span data-ttu-id="3ac97-169">Copiare l'esempio precedente e salvarlo come file denominato `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="3ac97-169">Copy the preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="3ac97-170">Per passare un file dei parametri locale, usare `@` per specificare un file locale denominato storage.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="3ac97-170">To pass a local parameter file, use `@` to specify a local file named storage.parameters.json.</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a><span data-ttu-id="3ac97-171">Testare una distribuzione del modello</span><span class="sxs-lookup"><span data-stu-id="3ac97-171">Test a template deployment</span></span>

<span data-ttu-id="3ac97-172">Per testare il modello e i valori dei parametri senza distribuire effettivamente le risorse, usare il comando [az group deployment validate](/cli/azure/group/deployment#validate).</span><span class="sxs-lookup"><span data-stu-id="3ac97-172">To test your template and parameter values without actually deploying any resources, use [az group deployment validate](/cli/azure/group/deployment#validate).</span></span> 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

<span data-ttu-id="3ac97-173">Se non vengono rilevati errori, il comando restituisce informazioni sulla distribuzione di test.</span><span class="sxs-lookup"><span data-stu-id="3ac97-173">If no errors are detected, the command returns information about the test deployment.</span></span> <span data-ttu-id="3ac97-174">Si noti nello specifico che il valore dell'**errore** è null.</span><span class="sxs-lookup"><span data-stu-id="3ac97-174">In particular, notice that the **error** value is null.</span></span>

```azurecli
{
  "error": null,
  "properties": {
      ...
```

<span data-ttu-id="3ac97-175">Se viene rilevato un errore, il comando restituisce un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="3ac97-175">If an error is detected, the command returns an error message.</span></span> <span data-ttu-id="3ac97-176">Il tentativo, ad esempio, di passare un valore non corretto per lo SKU dell'account di archiviazione, restituisce l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="3ac97-176">For example, attempting to pass an incorrect value for the storage account SKU, returns the following error:</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'The provided value 'badSKU' for the template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. The parameter value is not part of the allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

<span data-ttu-id="3ac97-177">Se il modello contiene un errore di sintassi, il comando restituisce un errore che indica l'impossibilità di analizzare il modello.</span><span class="sxs-lookup"><span data-stu-id="3ac97-177">If your template has a syntax error, the command returns an error indicating it could not parse the template.</span></span> <span data-ttu-id="3ac97-178">Il messaggio contiene il numero di riga e la posizione dell'errore di analisi.</span><span class="sxs-lookup"><span data-stu-id="3ac97-178">The message indicates the line number and position of the parsing error.</span></span>

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

<span data-ttu-id="3ac97-179">Per usare la modalità completa, usare il parametro `mode`:</span><span class="sxs-lookup"><span data-stu-id="3ac97-179">To use complete mode, use the `mode` parameter:</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

## <a name="sample-template"></a><span data-ttu-id="3ac97-180">Modello di esempio</span><span class="sxs-lookup"><span data-stu-id="3ac97-180">Sample template</span></span>

<span data-ttu-id="3ac97-181">Il modello seguente viene usato per gli esempi in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="3ac97-181">The following template is used for the examples in this topic.</span></span> <span data-ttu-id="3ac97-182">Copiarlo e salvarlo come file denominato storage.json.</span><span class="sxs-lookup"><span data-stu-id="3ac97-182">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="3ac97-183">Per informazioni su come creare questo modello, vedere [Creare il primo modello di Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="3ac97-183">To understand how to create this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="3ac97-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3ac97-184">Next steps</span></span>
* <span data-ttu-id="3ac97-185">Gli esempi inclusi in questo articolo distribuiscono risorse a un gruppo di risorse nella sottoscrizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="3ac97-185">The examples in this article deploy resources to a resource group in your default subscription.</span></span> <span data-ttu-id="3ac97-186">Per usare una sottoscrizione diversa, vedere [Gestire più sottoscrizioni di Azure](/cli/azure/manage-azure-subscriptions-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3ac97-186">To use a different subscription, see [Manage multiple Azure subscriptions](/cli/azure/manage-azure-subscriptions-azure-cli).</span></span>
* <span data-ttu-id="3ac97-187">Per uno script di esempio completo che consente di distribuire un modello, vedere lo [script di distribuzione di modelli di Resource Manager](resource-manager-samples-cli-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="3ac97-187">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-cli-deploy.md).</span></span>
* <span data-ttu-id="3ac97-188">Per informazioni su come definire i parametri nel modello, vedere [Comprendere la struttura e la sintassi dei modelli di Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3ac97-188">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="3ac97-189">Per suggerimenti su come risolvere i comuni errori di distribuzione, vedere [Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="3ac97-189">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="3ac97-190">Per informazioni sulla distribuzione di un modello che richiede un token di firma di accesso condiviso, vedere [Distribuire un modello privato con un token di firma di accesso condiviso](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="3ac97-190">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="3ac97-191">Per indicazioni su come le aziende possono usare Resource Manager per gestire efficacemente le sottoscrizioni, vedere [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Scaffolding aziendale Azure - Governance prescrittiva per le sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="3ac97-191">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
