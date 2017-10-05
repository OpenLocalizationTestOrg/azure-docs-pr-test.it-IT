---
title: Distribuire risorse con PowerShell e i modelli | Microsoft Docs
description: Utilizzare Azure Resource Manager e Azure PowerShell per distribuire una risorsa in Azure. Le risorse sono definite in un modello di Resource Manager.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 5f395abf8ebdfbac18fd17d8183b392673e280ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="aa85a-104">Distribuire le risorse con i modelli di Azure Resource Manager e Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa85a-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="aa85a-105">Questo articolo illustra come usare Azure PowerShell con modelli di Resource Manager per distribuire risorse in Azure.</span><span class="sxs-lookup"><span data-stu-id="aa85a-105">This topic explains how to use Azure PowerShell with Resource Manager templates to deploy your resources to Azure.</span></span> <span data-ttu-id="aa85a-106">Per comprendere i concetti di distribuzione e gestione delle soluzioni di Azure, vedere [Panoramica di Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aa85a-106">If you are not familiar with the concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="aa85a-107">Il modello di Resource Manager che si distribuisce può essere un file locale nel computer o un file esterno che si trova in un repository come GitHub.</span><span class="sxs-lookup"><span data-stu-id="aa85a-107">The Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="aa85a-108">Il modello che viene distribuito in questo articolo è disponibile nella sezione [Modello di esempio](#sample-template) o come [modello di account di archiviazione in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="aa85a-108">The template you deploy in this article is available in the [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="aa85a-109">Distribuire un modello dal computer locale</span><span class="sxs-lookup"><span data-stu-id="aa85a-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="aa85a-110">Per distribuire le risorse in Azure, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="aa85a-110">When deploying resources to Azure, you:</span></span>

1. <span data-ttu-id="aa85a-111">Accedere all'account Azure</span><span class="sxs-lookup"><span data-stu-id="aa85a-111">Log in to your Azure account</span></span>
2. <span data-ttu-id="aa85a-112">Creare un gruppo di risorse che funge da contenitore per le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="aa85a-112">Create a resource group that serves as the container for the deployed resources.</span></span> <span data-ttu-id="aa85a-113">Il nome del gruppo di risorse può contenere solo caratteri alfanumerici, punti, caratteri di sottolineatura, trattini e parentesi.</span><span class="sxs-lookup"><span data-stu-id="aa85a-113">The name of the resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="aa85a-114">Può contenere fino a 90 caratteri.</span><span class="sxs-lookup"><span data-stu-id="aa85a-114">It can be up to 90 characters.</span></span> <span data-ttu-id="aa85a-115">Non può terminare con un punto.</span><span class="sxs-lookup"><span data-stu-id="aa85a-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="aa85a-116">Distribuire nel gruppo di risorse il modello che definisce le risorse da creare.</span><span class="sxs-lookup"><span data-stu-id="aa85a-116">Deploy to the resource group the template that defines the resources to create</span></span>

<span data-ttu-id="aa85a-117">Un modello può includere parametri che consentono di personalizzare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="aa85a-117">A template can include parameters that enable you to customize the deployment.</span></span> <span data-ttu-id="aa85a-118">Può includere ad esempio valori specifici per un determinato ambiente (di sviluppo, test e produzione).</span><span class="sxs-lookup"><span data-stu-id="aa85a-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="aa85a-119">Il modello di esempio definisce un parametro per lo SKU dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="aa85a-119">The sample template defines a parameter for the storage account SKU.</span></span>

<span data-ttu-id="aa85a-120">L'esempio seguente crea un gruppo di risorse e distribuisce un modello dal computer locale:</span><span class="sxs-lookup"><span data-stu-id="aa85a-120">The following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="aa85a-121">Per il completamento della distribuzione sarà necessario attendere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="aa85a-121">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="aa85a-122">Al termine, viene visualizzato un messaggio che include il risultato:</span><span class="sxs-lookup"><span data-stu-id="aa85a-122">When it finishes, you see a message that includes the result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="aa85a-123">Distribuire un modello da un'origine esterna</span><span class="sxs-lookup"><span data-stu-id="aa85a-123">Deploy a template from an external source</span></span>

<span data-ttu-id="aa85a-124">Anziché archiviare i modelli di Resource Manager nel computer locale, è consigliabile archiviarli in una posizione esterna,</span><span class="sxs-lookup"><span data-stu-id="aa85a-124">Instead of storing Resource Manager templates on your local machine, you may prefer to store them in an external location.</span></span> <span data-ttu-id="aa85a-125">ad esempio in un repository di controllo del codice sorgente come GitHub.</span><span class="sxs-lookup"><span data-stu-id="aa85a-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="aa85a-126">o, in alternativa, archiviarli in un account di archiviazione di Azure per consentire l'accesso condiviso nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="aa85a-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="aa85a-127">Per distribuire un modello esterno, usare il parametro **TemplateUri**.</span><span class="sxs-lookup"><span data-stu-id="aa85a-127">To deploy an external template, use the **TemplateUri** parameter.</span></span> <span data-ttu-id="aa85a-128">Usare l'URI indicato nell'esempio per distribuire il modello di esempio da GitHub.</span><span class="sxs-lookup"><span data-stu-id="aa85a-128">Use the URI in the example to deploy the sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="aa85a-129">L'esempio precedente richiede l'utilizzo di un URI accessibile pubblicamente per il modello, che funziona per la maggior parte degli scenari. Il proprio modello non deve infatti includere dati riservati.</span><span class="sxs-lookup"><span data-stu-id="aa85a-129">The preceding example requires a publicly accessible URI for the template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="aa85a-130">Se è necessario specificare dati riservati, ad esempio una password di amministratore, passare il valore come parametro protetto.</span><span class="sxs-lookup"><span data-stu-id="aa85a-130">If you need to specify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="aa85a-131">Se invece si preferisce che il modello usato non sia accessibile pubblicamente, è possibile proteggerlo archiviandolo in un contenitore di archiviazione privato.</span><span class="sxs-lookup"><span data-stu-id="aa85a-131">However, if you do not want your template to be publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="aa85a-132">Per informazioni sulla distribuzione di un modello che richiede un token di firma di accesso condiviso (SAS), vedere [Distribuire un modello privato con un token di firma di accesso condiviso](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="aa85a-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="aa85a-133">File dei parametri</span><span class="sxs-lookup"><span data-stu-id="aa85a-133">Parameter files</span></span>

<span data-ttu-id="aa85a-134">Invece di passare i parametri come valori inline nello script, può risultare più facile usare un file JSON che contenga i valori dei parametri.</span><span class="sxs-lookup"><span data-stu-id="aa85a-134">Rather than passing parameters as inline values in your script, you may find it easier to use a JSON file that contains the parameter values.</span></span> <span data-ttu-id="aa85a-135">Il file dei parametri deve essere nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="aa85a-135">The parameter file must be in the following format:</span></span>

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

<span data-ttu-id="aa85a-136">Si noti che la sezione dei parametri include un nome di parametro che corrisponde al parametro definito nel modello (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="aa85a-136">Notice that the parameters section includes a parameter name that matches the parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="aa85a-137">Il file dei parametri contiene un valore per il parametro.</span><span class="sxs-lookup"><span data-stu-id="aa85a-137">The parameter file contains a value for the parameter.</span></span> <span data-ttu-id="aa85a-138">Questo valore viene passato automaticamente al modello durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="aa85a-138">This value is automatically passed to the template during deployment.</span></span> <span data-ttu-id="aa85a-139">È possibile creare più file dei parametri per scenari di distribuzione diversi e successivamente passare il file dei parametri appropriato.</span><span class="sxs-lookup"><span data-stu-id="aa85a-139">You can create multiple parameter files for different deployment scenarios, and then pass in the appropriate parameter file.</span></span> 

<span data-ttu-id="aa85a-140">Copiare l'esempio precedente e salvarlo come file denominato `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="aa85a-140">Copy the preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="aa85a-141">Per passare un file dei parametri locale, usare il parametro **TemplateParameterFile**:</span><span class="sxs-lookup"><span data-stu-id="aa85a-141">To pass a local parameter file, use the **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="aa85a-142">Per passare un file dei parametri esterno, usare il parametro **TemplateParameterUri**:</span><span class="sxs-lookup"><span data-stu-id="aa85a-142">To pass an external parameter file, use the **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="aa85a-143">È possibile usare i parametri inline e un file di parametri locale nella stessa operazione di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="aa85a-143">You can use inline parameters and a local parameter file in the same deployment operation.</span></span> <span data-ttu-id="aa85a-144">Ad esempio, è possibile specificare alcuni valori nel file di parametri locale e aggiungere altri valori inline durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="aa85a-144">For example, you can specify some values in the local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="aa85a-145">Se si specificano valori per un parametro sia nel file dei parametri locale che inline, il valore inline ha la precedenza.</span><span class="sxs-lookup"><span data-stu-id="aa85a-145">If you provide values for a parameter in both the local parameter file and inline, the inline value takes precedence.</span></span>

<span data-ttu-id="aa85a-146">Tuttavia, quando si usa un file di parametri esterni, non è possibile trasmettere altri valori, né inline né da un file locale.</span><span class="sxs-lookup"><span data-stu-id="aa85a-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="aa85a-147">Quando si specifica un file di parametri nel parametro **TemplateParameterUri**, tutti i parametri inline vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="aa85a-147">When you specify a parameter file in the **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="aa85a-148">È necessario fornire tutti i valori dei parametri presenti nel file esterno.</span><span class="sxs-lookup"><span data-stu-id="aa85a-148">Provide all parameter values in the external file.</span></span> <span data-ttu-id="aa85a-149">Se il modello include un valore importante che non è possibile includere nel file dei parametri, aggiungere tale valore a un insieme di credenziali delle chiavi oppure fornire inline tutti valori dei parametri in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="aa85a-149">If your template includes a sensitive value that you cannot include in the parameter file, either add that value to a key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="aa85a-150">Se il modello include un parametro con lo stesso nome di uno dei parametri nel comando di PowerShell, PowerShell aggiunge al parametro del modello il suffisso **FromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="aa85a-150">If your template includes a parameter with the same name as one of the parameters in the PowerShell command, PowerShell presents the parameter from your template with the postfix **FromTemplate**.</span></span> <span data-ttu-id="aa85a-151">Ad esempio, un parametro denominato **ResourceGroupName** nel modello sarà in conflitto con il parametro **ResourceGroupName** nel cmdlet [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="aa85a-151">For example, a parameter named **ResourceGroupName** in your template conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="aa85a-152">Verrà quindi richiesto di fornire un valore per **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="aa85a-152">You are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="aa85a-153">In generale, è consigliabile evitare questa confusione non attribuendo ai parametri lo stesso nome dei parametri usati per operazioni di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="aa85a-153">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="aa85a-154">Testare una distribuzione del modello</span><span class="sxs-lookup"><span data-stu-id="aa85a-154">Test a template deployment</span></span>

<span data-ttu-id="aa85a-155">Per testare il modello e i valori dei parametri senza distribuire effettivamente le risorse, usare [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="aa85a-155">To test your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="aa85a-156">Se non vengono rilevati errori, il comando termina senza una risposta.</span><span class="sxs-lookup"><span data-stu-id="aa85a-156">If no errors are detected, the command finishes without a response.</span></span> <span data-ttu-id="aa85a-157">Se viene rilevato un errore, il comando restituisce un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="aa85a-157">If an error is detected, the command returns an error message.</span></span> <span data-ttu-id="aa85a-158">Il tentativo, ad esempio, di passare un valore non corretto per lo SKU dell'account di archiviazione, restituisce l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="aa85a-158">For example, attempting to pass an incorrect value for the storage account SKU, returns the following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'The provided value 'badSku' for the template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. The parameter value is not part of the allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="aa85a-159">Se il modello contiene un errore di sintassi, il comando restituisce un errore che indica l'impossibilità di analizzare il modello.</span><span class="sxs-lookup"><span data-stu-id="aa85a-159">If your template has a syntax error, the command returns an error indicating it could not parse the template.</span></span> <span data-ttu-id="aa85a-160">Il messaggio contiene il numero di riga e la posizione dell'errore di analisi.</span><span class="sxs-lookup"><span data-stu-id="aa85a-160">The message indicates the line number and position of the parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="aa85a-161">Per usare la modalità completa, usare il parametro `Mode`:</span><span class="sxs-lookup"><span data-stu-id="aa85a-161">To use complete mode, use the `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="aa85a-162">Modello di esempio</span><span class="sxs-lookup"><span data-stu-id="aa85a-162">Sample template</span></span>

<span data-ttu-id="aa85a-163">Il modello seguente viene usato per gli esempi in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="aa85a-163">The following template is used for the examples in this topic.</span></span> <span data-ttu-id="aa85a-164">Copiarlo e salvarlo come file denominato storage.json.</span><span class="sxs-lookup"><span data-stu-id="aa85a-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="aa85a-165">Per informazioni su come creare questo modello, vedere [Creare il primo modello di Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="aa85a-165">To understand how to create this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="aa85a-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aa85a-166">Next steps</span></span>
* <span data-ttu-id="aa85a-167">Gli esempi inclusi in questo articolo distribuiscono risorse a un gruppo di risorse nella sottoscrizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="aa85a-167">The examples in this article deploy resources to a resource group in your default subscription.</span></span> <span data-ttu-id="aa85a-168">Per usare una sottoscrizione diversa, vedere [Gestire più sottoscrizioni di Azure](/powershell/azure/manage-subscriptions-azureps).</span><span class="sxs-lookup"><span data-stu-id="aa85a-168">To use a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="aa85a-169">Per uno script di esempio completo che consente di distribuire un modello, vedere lo [script di distribuzione di modelli di Resource Manager](resource-manager-samples-powershell-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="aa85a-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="aa85a-170">Per informazioni su come definire i parametri nel modello, vedere [Comprendere la struttura e la sintassi dei modelli di Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="aa85a-170">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="aa85a-171">Per suggerimenti su come risolvere i comuni errori di distribuzione, vedere [Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="aa85a-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="aa85a-172">Per informazioni sulla distribuzione di un modello che richiede un token di firma di accesso condiviso, vedere [Distribuire un modello privato con un token di firma di accesso condiviso](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="aa85a-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="aa85a-173">Per indicazioni su come le aziende possono usare Resource Manager per gestire efficacemente le sottoscrizioni, vedere [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Scaffolding aziendale Azure - Governance prescrittiva per le sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="aa85a-173">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

