---
title: aaaDeploy risorse con PowerShell e modello | Documenti Microsoft
description: Utilizzare Gestione risorse di Azure e Azure PowerShell toodeploy un tooAzure di risorse. risorse di Hello vengono definite in un modello di gestione risorse.
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
ms.openlocfilehash: 41506811ba3c2ea5df6313db70978ade50f71161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="300d6-104">Distribuire le risorse con i modelli di Azure Resource Manager e Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="300d6-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="300d6-105">Questo argomento viene illustrato come toouse Azure PowerShell con Gestione risorse modelli toodeploy tooAzure le risorse.</span><span class="sxs-lookup"><span data-stu-id="300d6-105">This topic explains how toouse Azure PowerShell with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="300d6-106">Se non si ha familiarità con concetti hello della distribuzione e gestione di soluzioni di Azure, vedere [Panoramica di gestione risorse di Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="300d6-106">If you are not familiar with hello concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="300d6-107">il modello di gestione risorse di Hello è distribuire può essere un file nel computer locale o un file esterno che si trova in un archivio come GitHub.</span><span class="sxs-lookup"><span data-stu-id="300d6-107">hello Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="300d6-108">modello Hello si distribuisce in questo articolo è disponibile in hello [modello di esempio](#sample-template) sezione, oppure come [modello di account di archiviazione in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="300d6-108">hello template you deploy in this article is available in hello [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="300d6-109">Distribuire un modello dal computer locale</span><span class="sxs-lookup"><span data-stu-id="300d6-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="300d6-110">Quando si distribuisce tooAzure risorse, è:</span><span class="sxs-lookup"><span data-stu-id="300d6-110">When deploying resources tooAzure, you:</span></span>

1. <span data-ttu-id="300d6-111">Accedi tooyour account Azure</span><span class="sxs-lookup"><span data-stu-id="300d6-111">Log in tooyour Azure account</span></span>
2. <span data-ttu-id="300d6-112">Creare un gruppo di risorse che funge da contenitore hello per le risorse di hello distribuito.</span><span class="sxs-lookup"><span data-stu-id="300d6-112">Create a resource group that serves as hello container for hello deployed resources.</span></span> <span data-ttu-id="300d6-113">nome Hello hello del gruppo di risorse possa includere solo caratteri alfanumerici, punti, caratteri di sottolineatura, trattini e parentesi.</span><span class="sxs-lookup"><span data-stu-id="300d6-113">hello name of hello resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="300d6-114">Può trattarsi di too90 caratteri.</span><span class="sxs-lookup"><span data-stu-id="300d6-114">It can be up too90 characters.</span></span> <span data-ttu-id="300d6-115">Non può terminare con un punto.</span><span class="sxs-lookup"><span data-stu-id="300d6-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="300d6-116">Distribuire toohello risorse gruppo hello modello che definisce hello risorse toocreate</span><span class="sxs-lookup"><span data-stu-id="300d6-116">Deploy toohello resource group hello template that defines hello resources toocreate</span></span>

<span data-ttu-id="300d6-117">Un modello può includere parametri che consentono la distribuzione di hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="300d6-117">A template can include parameters that enable you toocustomize hello deployment.</span></span> <span data-ttu-id="300d6-118">Può includere ad esempio valori specifici per un determinato ambiente (di sviluppo, test e produzione).</span><span class="sxs-lookup"><span data-stu-id="300d6-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="300d6-119">modello di esempio Hello definisce un parametro per l'account di archiviazione hello SKU.</span><span class="sxs-lookup"><span data-stu-id="300d6-119">hello sample template defines a parameter for hello storage account SKU.</span></span>

<span data-ttu-id="300d6-120">Hello di esempio seguente crea un gruppo di risorse e distribuisce un modello dal computer locale:</span><span class="sxs-lookup"><span data-stu-id="300d6-120">hello following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="300d6-121">distribuzione di Hello può richiedere alcuni minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="300d6-121">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="300d6-122">Al termine, viene visualizzato un messaggio che include i risultati di hello:</span><span class="sxs-lookup"><span data-stu-id="300d6-122">When it finishes, you see a message that includes hello result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="300d6-123">Distribuire un modello da un'origine esterna</span><span class="sxs-lookup"><span data-stu-id="300d6-123">Deploy a template from an external source</span></span>

<span data-ttu-id="300d6-124">Invece di archiviare i modelli di gestione risorse nel computer locale, è preferibile toostore multipla in una posizione esterna.</span><span class="sxs-lookup"><span data-stu-id="300d6-124">Instead of storing Resource Manager templates on your local machine, you may prefer toostore them in an external location.</span></span> <span data-ttu-id="300d6-125">ad esempio in un repository di controllo del codice sorgente come GitHub.</span><span class="sxs-lookup"><span data-stu-id="300d6-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="300d6-126">È possibile, in alternativa, archiviarli in un account di archiviazione di Azure per consentire l'accesso condiviso nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="300d6-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="300d6-127">toodeploy un modello esterno, usare hello **TemplateUri** parametro.</span><span class="sxs-lookup"><span data-stu-id="300d6-127">toodeploy an external template, use hello **TemplateUri** parameter.</span></span> <span data-ttu-id="300d6-128">Utilizzare Ciao URI hello esempio toodeploy hello modello di esempio da GitHub.</span><span class="sxs-lookup"><span data-stu-id="300d6-128">Use hello URI in hello example toodeploy hello sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="300d6-129">Hello esempio precedente richiede un URI accessibile pubblicamente per il modello di hello, che può essere usato per la maggior parte degli scenari perché il modello non deve includere dati riservati.</span><span class="sxs-lookup"><span data-stu-id="300d6-129">hello preceding example requires a publicly accessible URI for hello template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="300d6-130">Se è necessario toospecify dati riservati (ad esempio una password di amministratore), passare il valore come parametro sicura.</span><span class="sxs-lookup"><span data-stu-id="300d6-130">If you need toospecify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="300d6-131">Tuttavia, se si desidera toobe il modello accessibile pubblicamente, è possibile proteggerli da archiviare in un contenitore di archiviazione privato.</span><span class="sxs-lookup"><span data-stu-id="300d6-131">However, if you do not want your template toobe publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="300d6-132">Per informazioni sulla distribuzione di un modello che richiede un token di firma di accesso condiviso (SAS), vedere [Distribuire un modello privato con un token di firma di accesso condiviso](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="300d6-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="300d6-133">File dei parametri</span><span class="sxs-lookup"><span data-stu-id="300d6-133">Parameter files</span></span>

<span data-ttu-id="300d6-134">Anziché il passaggio di parametri come valori inline nello script, può risultare più semplice toouse un file JSON che contiene i valori dei parametri hello.</span><span class="sxs-lookup"><span data-stu-id="300d6-134">Rather than passing parameters as inline values in your script, you may find it easier toouse a JSON file that contains hello parameter values.</span></span> <span data-ttu-id="300d6-135">file di parametro Hello deve essere nel seguente formato hello:</span><span class="sxs-lookup"><span data-stu-id="300d6-135">hello parameter file must be in hello following format:</span></span>

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

<span data-ttu-id="300d6-136">Si noti che la sezione parametri di hello include un nome di parametro corrispondente parametro hello definito nel modello (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="300d6-136">Notice that hello parameters section includes a parameter name that matches hello parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="300d6-137">file di parametro Hello contiene un valore per il parametro hello.</span><span class="sxs-lookup"><span data-stu-id="300d6-137">hello parameter file contains a value for hello parameter.</span></span> <span data-ttu-id="300d6-138">Questo valore viene passato automaticamente toohello modello durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="300d6-138">This value is automatically passed toohello template during deployment.</span></span> <span data-ttu-id="300d6-139">È possibile creare più file di parametro per diversi scenari di distribuzione e quindi passare nel file di parametro appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="300d6-139">You can create multiple parameter files for different deployment scenarios, and then pass in hello appropriate parameter file.</span></span> 

<span data-ttu-id="300d6-140">Copiare l'esempio sopra riportato hello e salvarlo come un file denominato `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="300d6-140">Copy hello preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="300d6-141">toopass un file di parametro locale, utilizzare hello **TemplateParameterFile** parametro:</span><span class="sxs-lookup"><span data-stu-id="300d6-141">toopass a local parameter file, use hello **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="300d6-142">toopass un file di parametro esterna, utilizzare hello **TemplateParameterUri** parametro:</span><span class="sxs-lookup"><span data-stu-id="300d6-142">toopass an external parameter file, use hello **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="300d6-143">È possibile utilizzare parametri inline e un parametro locale del file in hello stessa operazione di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="300d6-143">You can use inline parameters and a local parameter file in hello same deployment operation.</span></span> <span data-ttu-id="300d6-144">Ad esempio, è possibile specificare alcuni valori nel file dei parametri locali hello e aggiungere altri valori inline durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="300d6-144">For example, you can specify some values in hello local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="300d6-145">Se si specificano valori per un parametro nel file dei parametri locali hello sia in linea, hello inline valore ha la precedenza.</span><span class="sxs-lookup"><span data-stu-id="300d6-145">If you provide values for a parameter in both hello local parameter file and inline, hello inline value takes precedence.</span></span>

<span data-ttu-id="300d6-146">Tuttavia, quando si usa un file di parametri esterni, non è possibile trasmettere altri valori, né inline né da un file locale.</span><span class="sxs-lookup"><span data-stu-id="300d6-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="300d6-147">Quando si specifica un file di parametro hello **TemplateParameterUri** parametro, in linea tutti i parametri vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="300d6-147">When you specify a parameter file in hello **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="300d6-148">Specificare tutti i valori di parametro nel file esterno hello.</span><span class="sxs-lookup"><span data-stu-id="300d6-148">Provide all parameter values in hello external file.</span></span> <span data-ttu-id="300d6-149">Se il modello include un valore importante che non è possibile includere nel file di parametro hello, aggiungere tale valore tooa chiave dell'insieme di credenziali, oppure fornire in modo dinamico tutti i valori di parametro inline.</span><span class="sxs-lookup"><span data-stu-id="300d6-149">If your template includes a sensitive value that you cannot include in hello parameter file, either add that value tooa key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="300d6-150">Se il modello include un parametro con stesso nome come uno dei parametri di hello nel comando di PowerShell hello hello, PowerShell presenta il parametro hello in base al modello con suffisso hello **FromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="300d6-150">If your template includes a parameter with hello same name as one of hello parameters in hello PowerShell command, PowerShell presents hello parameter from your template with hello postfix **FromTemplate**.</span></span> <span data-ttu-id="300d6-151">Ad esempio, un parametro denominato **ResourceGroupName** nei conflitti di modelli con hello **ResourceGroupName** parametro hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)cmdlet.</span><span class="sxs-lookup"><span data-stu-id="300d6-151">For example, a parameter named **ResourceGroupName** in your template conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="300d6-152">Si è tooprovide richiesto un valore per **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="300d6-152">You are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="300d6-153">In generale, si dovrebbe evitare questa confusione, non denominazione dei parametri con hello stesso nome come parametri utilizzati per operazioni di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="300d6-153">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="300d6-154">Testare una distribuzione del modello</span><span class="sxs-lookup"><span data-stu-id="300d6-154">Test a template deployment</span></span>

<span data-ttu-id="300d6-155">Utilizzare i valori di parametro e modello senza distribuire effettivamente le risorse, tootest [Test AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="300d6-155">tootest your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="300d6-156">Se non vengono rilevati errori, il comando hello termina senza una risposta.</span><span class="sxs-lookup"><span data-stu-id="300d6-156">If no errors are detected, hello command finishes without a response.</span></span> <span data-ttu-id="300d6-157">Se viene rilevato un errore, il comando hello restituisce un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="300d6-157">If an error is detected, hello command returns an error message.</span></span> <span data-ttu-id="300d6-158">Ad esempio, il tentativo di un valore non corretto per l'account di archiviazione hello SKU, toopass restituisce hello errore seguente:</span><span class="sxs-lookup"><span data-stu-id="300d6-158">For example, attempting toopass an incorrect value for hello storage account SKU, returns hello following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="300d6-159">Se il modello dispone di un errore di sintassi, il comando hello restituisce un errore che indica che non è stato possibile analizzare il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="300d6-159">If your template has a syntax error, hello command returns an error indicating it could not parse hello template.</span></span> <span data-ttu-id="300d6-160">messaggio Hello indica il numero di riga hello e la posizione di hello errore di analisi.</span><span class="sxs-lookup"><span data-stu-id="300d6-160">hello message indicates hello line number and position of hello parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="300d6-161">modalità completa toouse, utilizzare hello `Mode` parametro:</span><span class="sxs-lookup"><span data-stu-id="300d6-161">toouse complete mode, use hello `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="300d6-162">Modello di esempio</span><span class="sxs-lookup"><span data-stu-id="300d6-162">Sample template</span></span>

<span data-ttu-id="300d6-163">Hello modello seguente viene utilizzato per gli esempi di hello in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="300d6-163">hello following template is used for hello examples in this topic.</span></span> <span data-ttu-id="300d6-164">Copiarlo e salvarlo come file denominato storage.json.</span><span class="sxs-lookup"><span data-stu-id="300d6-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="300d6-165">toounderstand come toocreate questo modello, vedere [creare il primo modello di gestione risorse di Azure](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="300d6-165">toounderstand how toocreate this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="300d6-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="300d6-166">Next steps</span></span>
* <span data-ttu-id="300d6-167">esempi di Hello in questo articolo distribuire un gruppo di risorse tooa risorse nella sottoscrizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="300d6-167">hello examples in this article deploy resources tooa resource group in your default subscription.</span></span> <span data-ttu-id="300d6-168">toouse una sottoscrizione diversa, vedere [gestiscono più sottoscrizioni Azure](/powershell/azure/manage-subscriptions-azureps).</span><span class="sxs-lookup"><span data-stu-id="300d6-168">toouse a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="300d6-169">Per uno script di esempio completo che consente di distribuire un modello, vedere lo [script di distribuzione di modelli di Resource Manager](resource-manager-samples-powershell-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="300d6-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="300d6-170">toounderstand toodefine parametri nel modello, vedere [comprendere hello struttura e la sintassi dei modelli di Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="300d6-170">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="300d6-171">Per suggerimenti su come risolvere i comuni errori di distribuzione, vedere [Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="300d6-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="300d6-172">Per informazioni sulla distribuzione di un modello che richiede un token di firma di accesso condiviso, vedere [Distribuire un modello privato con un token di firma di accesso condiviso](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="300d6-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="300d6-173">Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="300d6-173">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

