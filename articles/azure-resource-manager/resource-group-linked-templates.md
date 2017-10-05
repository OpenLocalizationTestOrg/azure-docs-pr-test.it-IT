---
title: Collegare modelli per la distribuzione di Azure | Microsoft Docs
description: Descrive come usare i modelli collegati in un modello di Azure Resource Manager per creare una soluzione basata su un modello modulare. Mostra come passare i valori dei parametri, specificare un file di parametri e gli URL creati in modo dinamico.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 27d8c4b2-1e24-45fe-88fd-8cf98a6bb2d2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: 8b58a83ffd473500dd3f76c09e251f9208527d4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a><span data-ttu-id="7f587-104">Uso di modelli collegati nella distribuzione di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="7f587-104">Using linked templates when deploying Azure resources</span></span>
<span data-ttu-id="7f587-105">Dall'interno di un modello di Azure Resource Manager è possibile collegarsi a un altro modello che consente di scomporre la distribuzione in un set di modelli di destinazione specifici.</span><span class="sxs-lookup"><span data-stu-id="7f587-105">From within one Azure Resource Manager template, you can link to another template, which enables you to decompose your deployment into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="7f587-106">In modo analogo alla scomposizione di un'applicazione in diverse classi di codice, la scomposizione offre vantaggi in termini di testing, riuso e leggibilità.</span><span class="sxs-lookup"><span data-stu-id="7f587-106">As with decomposing an application into several code classes, decomposition provides benefits in terms of testing, reuse, and readability.</span></span>  

<span data-ttu-id="7f587-107">È possibile passare parametri da un modello principale a un modello collegato. Tali parametri possono venire associati direttamente ai parametri e alle variabili esposti dal modello chiamante.</span><span class="sxs-lookup"><span data-stu-id="7f587-107">You can pass parameters from a main template to a linked template, and those parameters can directly map to parameters or variables exposed by the calling template.</span></span> <span data-ttu-id="7f587-108">Il modello collegato può inoltre passare una variabile di output al modello di origine, consentendo un scambio bidirezionale di dati tra modelli.</span><span class="sxs-lookup"><span data-stu-id="7f587-108">The linked template can also pass an output variable back to the source template, enabling a two-way data exchange between templates.</span></span>

## <a name="linking-to-a-template"></a><span data-ttu-id="7f587-109">Collegamento a un modello</span><span class="sxs-lookup"><span data-stu-id="7f587-109">Linking to a template</span></span>
<span data-ttu-id="7f587-110">Per creare un collegamento tra due modelli, aggiungere una risorsa di distribuzione all'interno del modello principale che punta al modello collegato.</span><span class="sxs-lookup"><span data-stu-id="7f587-110">You create a link between two templates by adding a deployment resource within the main template that points to the linked template.</span></span> <span data-ttu-id="7f587-111">Impostare la proprietà **templateLink** sull'URI del modello collegato.</span><span class="sxs-lookup"><span data-stu-id="7f587-111">You set the **templateLink** property to the URI of the linked template.</span></span> <span data-ttu-id="7f587-112">È possibile specificare i valori dei parametri per il modello collegato direttamente nel modello o in un file di parametri.</span><span class="sxs-lookup"><span data-stu-id="7f587-112">You can provide parameter values for the linked template directly in your template or in a parameter file.</span></span> <span data-ttu-id="7f587-113">Nel seguente esempio viene utilizzata la proprietà **parameters** per specificare direttamente un valore di parametro.</span><span class="sxs-lookup"><span data-stu-id="7f587-113">The following example uses the **parameters** property to specify a parameter value directly.</span></span>

```json
"resources": [ 
  { 
      "apiVersion": "2017-05-10", 
      "name": "linkedTemplate", 
      "type": "Microsoft.Resources/deployments", 
      "properties": { 
        "mode": "incremental", 
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion": "1.0.0.0"
        }, 
        "parameters": { 
          "StorageAccountName":{"value": "[parameters('StorageAccountName')]"} 
        } 
      } 
  } 
] 
```

<span data-ttu-id="7f587-114">Come altri tipi di risorse, è possibile impostare le dipendenze tra il modello collegato e altre risorse.</span><span class="sxs-lookup"><span data-stu-id="7f587-114">Like other resource types, you can set dependencies between the linked template and other resources.</span></span> <span data-ttu-id="7f587-115">Pertanto, quando le altre risorse richiedono un valore di output presente nel modello collegato, è possibile accertarsi di distribuire il modello collegato prima di queste risorse.</span><span class="sxs-lookup"><span data-stu-id="7f587-115">Therefore, when other resources require an output value from the linked template, you can make sure the linked template is deployed before them.</span></span> <span data-ttu-id="7f587-116">Viceversa, quando il modello collegato dipende da altre risorse, è possibile accertarsi di distribuire le altre risorse prima di questo modello.</span><span class="sxs-lookup"><span data-stu-id="7f587-116">Or, when the linked template relies on other resources, you can make sure other resources are deployed before the linked template.</span></span> <span data-ttu-id="7f587-117">Per recuperare un valore da un modello collegato, è possibile usare la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="7f587-117">You can retrieve a value from a linked template with the following syntax:</span></span>

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

<span data-ttu-id="7f587-118">Il servizio Resource Manager deve poter accedere al modello collegato.</span><span class="sxs-lookup"><span data-stu-id="7f587-118">The Resource Manager service must be able to access the linked template.</span></span> <span data-ttu-id="7f587-119">Non è possibile specificare un file locale o un file che sia disponibile unicamente nella rete locale per il modello collegato.</span><span class="sxs-lookup"><span data-stu-id="7f587-119">You cannot specify a local file or a file that is only available on your local network for the linked template.</span></span> <span data-ttu-id="7f587-120">È possibile fornire solo un valore URI che includa **http** o **https**.</span><span class="sxs-lookup"><span data-stu-id="7f587-120">You can only provide a URI value that includes either **http** or **https**.</span></span> <span data-ttu-id="7f587-121">È possibile scegliere di inserire il modello collegato in un account di archiviazione e usare l'URI per tale elemento, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="7f587-121">One option is to place your linked template in a storage account, and use the URI for that item, such as shown in the following example:</span></span>

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

<span data-ttu-id="7f587-122">Anche se il modello collegato deve essere disponibile esternamente, non è necessario che sia pubblicamente disponibile.</span><span class="sxs-lookup"><span data-stu-id="7f587-122">Although the linked template must be externally available, it does not need to be generally available to the public.</span></span> <span data-ttu-id="7f587-123">È possibile aggiungere il modello a un account di archiviazione privato accessibile solo al proprietario dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7f587-123">You can add your template to a private storage account that is accessible to only the storage account owner.</span></span> <span data-ttu-id="7f587-124">Creare quindi un token di firma di accesso condiviso per consentire l'accesso durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="7f587-124">Then, you create a shared access signature (SAS) token to enable access during deployment.</span></span> <span data-ttu-id="7f587-125">Aggiungere il token con firma di accesso condiviso all'URI del modello collegato.</span><span class="sxs-lookup"><span data-stu-id="7f587-125">You add that SAS token to the URI for the linked template.</span></span> <span data-ttu-id="7f587-126">Per conoscere la procedura per la configurazione di un modello in un account di archiviazione e per la generazione di un token con firma di accesso condiviso, consultare [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) (Distribuire le risorse con i modelli di Resource Manager e Azure PowerShell) o [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md) (Distribuire le risorse con i modelli di Azure Resource Manager e l'interfaccia della riga di comando di Azure).</span><span class="sxs-lookup"><span data-stu-id="7f587-126">For steps on setting up a template in a storage account and generating a SAS token, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) or [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> 

<span data-ttu-id="7f587-127">Nell'esempio seguente viene illustrato un modello padre che si collega a un altro modello.</span><span class="sxs-lookup"><span data-stu-id="7f587-127">The following example shows a parent template that links to another template.</span></span> <span data-ttu-id="7f587-128">È possibile accedere al modello collegato con un token di firma di accesso condiviso passato come parametro.</span><span class="sxs-lookup"><span data-stu-id="7f587-128">The linked template is accessed with a SAS token that is passed in as a parameter.</span></span>

```json
"parameters": {
    "sasToken": { "type": "securestring" }
},
"resources": [
    {
        "apiVersion": "2017-05-10",
        "name": "linkedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
          "mode": "incremental",
          "templateLink": {
            "uri": "[concat('https://storagecontosotemplates.blob.core.windows.net/templates/helloworld.json', parameters('sasToken'))]",
            "contentVersion": "1.0.0.0"
          }
        }
    }
],
```

<span data-ttu-id="7f587-129">Anche se il token viene passato come stringa sicura, l'URI del modello collegato, incluso il token di firma di accesso condiviso, è registrato nelle operazioni di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="7f587-129">Even though the token is passed in as a secure string, the URI of the linked template, including the SAS token, is logged in the deployment operations.</span></span> <span data-ttu-id="7f587-130">Per limitare l'esposizione, impostare una scadenza per il token.</span><span class="sxs-lookup"><span data-stu-id="7f587-130">To limit exposure, set an expiration for the token.</span></span>

<span data-ttu-id="7f587-131">Resource Manager gestisce ogni modello collegato come una distribuzione distinta.</span><span class="sxs-lookup"><span data-stu-id="7f587-131">Resource Manager handles each linked template as a separate deployment.</span></span> <span data-ttu-id="7f587-132">Nella cronologia delle distribuzioni relativa al gruppo di risorse, sono visibili distribuzioni distinte per il modello padre i modelli annidati.</span><span class="sxs-lookup"><span data-stu-id="7f587-132">In the deployment history for the resource group, you see separate deployments for the parent and nested templates.</span></span>

![cronologia della distribuzione](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-to-a-parameter-file"></a><span data-ttu-id="7f587-134">Collegamento a un file di parametri</span><span class="sxs-lookup"><span data-stu-id="7f587-134">Linking to a parameter file</span></span>
<span data-ttu-id="7f587-135">Nell'esempio successivo viene utilizzata la proprietà **parametersLink** per il collegamento a un file di parametri.</span><span class="sxs-lookup"><span data-stu-id="7f587-135">The next example uses the **parametersLink** property to link to a parameter file.</span></span>

```json
"resources": [ 
  { 
     "apiVersion": "2017-05-10", 
     "name": "linkedTemplate", 
     "type": "Microsoft.Resources/deployments", 
     "properties": { 
       "mode": "incremental", 
       "templateLink": {
          "uri":"https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion":"1.0.0.0"
       }, 
       "parametersLink": { 
          "uri":"https://www.contoso.com/AzureTemplates/parameters.json",
          "contentVersion":"1.0.0.0"
       } 
     } 
  } 
] 
```

<span data-ttu-id="7f587-136">Il valore URI per il file di parametro collegato non può essere un file locale e deve includere o **http** o **https**.</span><span class="sxs-lookup"><span data-stu-id="7f587-136">The URI value for the linked parameter file cannot be a local file, and must include either **http** or **https**.</span></span> <span data-ttu-id="7f587-137">È anche possibile limitare l'accesso al file dei parametri solo tramite un token di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="7f587-137">The parameter file can also be limited to access through a SAS token.</span></span>

## <a name="using-variables-to-link-templates"></a><span data-ttu-id="7f587-138">Uso di variabili per collegare i modelli</span><span class="sxs-lookup"><span data-stu-id="7f587-138">Using variables to link templates</span></span>
<span data-ttu-id="7f587-139">Negli esempi precedenti sono illustrati i valori di URL hard-coded per i collegamenti del modello.</span><span class="sxs-lookup"><span data-stu-id="7f587-139">The previous examples showed hard-coded URL values for the template links.</span></span> <span data-ttu-id="7f587-140">Questo approccio potrebbe funzionare per un modello semplice ma non funziona correttamente in caso di uso di un ampio set di modelli modulari.</span><span class="sxs-lookup"><span data-stu-id="7f587-140">This approach might work for a simple template but it does not work well when working with a large set of modular templates.</span></span> <span data-ttu-id="7f587-141">In alternativa, è possibile creare una variabile statica contenente un URL di base per il modello principale e quindi creare dinamicamente gli URL per i modelli collegati da tale URL di base.</span><span class="sxs-lookup"><span data-stu-id="7f587-141">Instead, you can create a static variable that stores a base URL for the main template and then dynamically create URLs for the linked templates from that base URL.</span></span> <span data-ttu-id="7f587-142">Il vantaggio di questo approccio è rappresentato dal fatto che risulta più semplice spostare o scomporre il modello perché è sufficiente modificare la variabile statica nel modello principale.</span><span class="sxs-lookup"><span data-stu-id="7f587-142">The benefit of this approach is you can easily move or fork the template because you only need to change the static variable in the main template.</span></span> <span data-ttu-id="7f587-143">Il modello principale passa gli URI corretti a tutto il modello scomposto.</span><span class="sxs-lookup"><span data-stu-id="7f587-143">The main template passes the correct URIs throughout the decomposed template.</span></span>

<span data-ttu-id="7f587-144">Nell'esempio seguente viene illustrato come usare un URL di base per creare due URL per i modelli collegati (**sharedTemplateUrl** e **vmTemplate**).</span><span class="sxs-lookup"><span data-stu-id="7f587-144">The following example shows how to use a base URL to create two URLs for linked templates (**sharedTemplateUrl** and **vmTemplate**).</span></span> 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

<span data-ttu-id="7f587-145">È inoltre possibile usare [deployment ()](resource-group-template-functions-deployment.md#deployment) per ottenere l'URL di base per il modello corrente e usarlo per ottenere l'URL per altri modelli nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="7f587-145">You can also use [deployment()](resource-group-template-functions-deployment.md#deployment) to get the base URL for the current template, and use that to get the URL for other templates in the same location.</span></span> <span data-ttu-id="7f587-146">Questo approccio è utile se la posizione del modello cambia, ad esempio a causa del controllo delle versioni, o si vuole evitare la codifica di URL nel file del modello.</span><span class="sxs-lookup"><span data-stu-id="7f587-146">This approach is useful if your template location changes (maybe due to versioning) or you want to avoid hard coding URLs in the template file.</span></span> 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a><span data-ttu-id="7f587-147">Esempio completo</span><span class="sxs-lookup"><span data-stu-id="7f587-147">Complete example</span></span>
<span data-ttu-id="7f587-148">I seguenti modelli di esempio mostrano una disposizione semplificata di modelli collegati, allo scopo di illustrare alcuni dei concetti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7f587-148">The following example templates show a simplified arrangement of linked templates to illustrate several of the concepts in this article.</span></span> <span data-ttu-id="7f587-149">supponendo che i modelli siano stati aggiunti nello stesso contenitore in un account di archiviazione con accesso pubblico disattivato.</span><span class="sxs-lookup"><span data-stu-id="7f587-149">It assumes the templates have been added to the same container in a storage account with public access turned off.</span></span> <span data-ttu-id="7f587-150">Il modello collegato restituisce un valore al modello principale nella sezione **outputs** .</span><span class="sxs-lookup"><span data-stu-id="7f587-150">The linked template passes a value back to the main template in the **outputs** section.</span></span>

<span data-ttu-id="7f587-151">Il file **parent.json** è costituito da:</span><span class="sxs-lookup"><span data-stu-id="7f587-151">The **parent.json** file consists of:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "containerSasToken": { "type": "string" }
  },
  "resources": [
    {
      "apiVersion": "2017-05-10",
      "name": "linkedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "[concat(uri(deployment().properties.templateLink.uri, 'helloworld.json'), parameters('containerSasToken'))]",
          "contentVersion": "1.0.0.0"
        }
      }
    }
  ],
  "outputs": {
    "result": {
      "type": "string",
      "value": "[reference('linkedTemplate').outputs.result.value]"
    }
  }
}
```

<span data-ttu-id="7f587-152">Il file **helloworld.json** è costituito da:</span><span class="sxs-lookup"><span data-stu-id="7f587-152">The **helloworld.json** file consists of:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "variables": {},
  "resources": [],
  "outputs": {
    "result": {
        "value": "Hello World",
        "type" : "string"
    }
  }
}
```

<span data-ttu-id="7f587-153">Nella PowerShell, ottenere un token per il contenitore e distribuire i modelli con:</span><span class="sxs-lookup"><span data-stu-id="7f587-153">In PowerShell, you get a token for the container and deploy the templates with:</span></span>

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

<span data-ttu-id="7f587-154">Nell'interfaccia della riga di comando 2.0 di Azure si ottiene un token per il contenitore e si distribuiscono i modelli con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="7f587-154">In Azure CLI 2.0, you get a token for the container and deploy the templates with the following code:</span></span>

```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name storagecontosotemplates \
    --query connectionString)
token=$(az storage container generate-sas \
    --name templates \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name parent.json \
    --output tsv \
    --connection-string $connection)
parameter='{"containerSasToken":{"value":"?'$token'"}}'
az group deployment create --resource-group ExampleGroup --template-uri $url?$token --parameters $parameter
```

## <a name="next-steps"></a><span data-ttu-id="7f587-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7f587-155">Next steps</span></span>
* <span data-ttu-id="7f587-156">Per informazioni sulla definizione dell'ordine di distribuzione per le risorse, vedere [Definizione delle dipendenze nei modelli di Azure Resource Manager](resource-group-define-dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="7f587-156">To learn about the defining the deployment order for your resources, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md)</span></span>
* <span data-ttu-id="7f587-157">Per informazioni su come definire una sola risorsa e crearne molte istanze, vedere [Creare più istanze di risorse in Azure Resource Manager](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="7f587-157">To learn how to define one resource but create many instances of it, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>

