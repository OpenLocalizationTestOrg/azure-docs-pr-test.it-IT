---
title: aaaLink modelli per la distribuzione di Azure | Documenti Microsoft
description: Viene descritto come toouse collegato modelli in un toocreate modello di gestione risorse di Azure una soluzione di modello modulare. Illustra come specificare un file di parametri, valori dei parametri toopass e creati in modo dinamico gli URL.
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
ms.openlocfilehash: b935b1810db5ce894d009403cd4bb945cab34ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a><span data-ttu-id="f799b-104">Uso di modelli collegati nella distribuzione di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="f799b-104">Using linked templates when deploying Azure resources</span></span>
<span data-ttu-id="f799b-105">All'interno di un modello di gestione risorse di Azure, è possibile collegare tooanother modello, che consentono di toodecompose la distribuzione in un set di modelli di destinazione, scopo specifico.</span><span class="sxs-lookup"><span data-stu-id="f799b-105">From within one Azure Resource Manager template, you can link tooanother template, which enables you toodecompose your deployment into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="f799b-106">In modo analogo alla scomposizione di un'applicazione in diverse classi di codice, la scomposizione offre vantaggi in termini di testing, riuso e leggibilità.</span><span class="sxs-lookup"><span data-stu-id="f799b-106">As with decomposing an application into several code classes, decomposition provides benefits in terms of testing, reuse, and readability.</span></span>  

<span data-ttu-id="f799b-107">È possibile passare parametri da un modello di collegato tooa principale dei modelli, e tali parametri è possono mappare direttamente tooparameters o variabili esposte dal modello di chiamata hello.</span><span class="sxs-lookup"><span data-stu-id="f799b-107">You can pass parameters from a main template tooa linked template, and those parameters can directly map tooparameters or variables exposed by hello calling template.</span></span> <span data-ttu-id="f799b-108">modello collegato Hello è inoltre possibile passare un modello di origine toohello nascosto variabile output, l'abilitazione di uno scambio di dati bidirezionale tra modelli.</span><span class="sxs-lookup"><span data-stu-id="f799b-108">hello linked template can also pass an output variable back toohello source template, enabling a two-way data exchange between templates.</span></span>

## <a name="linking-tooa-template"></a><span data-ttu-id="f799b-109">Collegamento tooa modello</span><span class="sxs-lookup"><span data-stu-id="f799b-109">Linking tooa template</span></span>
<span data-ttu-id="f799b-110">Si crea un collegamento tra due modelli mediante l'aggiunta di una risorsa di distribuzione nel modello principale hello punti toohello modello collegato.</span><span class="sxs-lookup"><span data-stu-id="f799b-110">You create a link between two templates by adding a deployment resource within hello main template that points toohello linked template.</span></span> <span data-ttu-id="f799b-111">Impostare hello **templateLink** toohello proprietà URI del modello collegato hello.</span><span class="sxs-lookup"><span data-stu-id="f799b-111">You set hello **templateLink** property toohello URI of hello linked template.</span></span> <span data-ttu-id="f799b-112">È possibile fornire i valori dei parametri per il modello collegato hello direttamente nel modello o in un file di parametro.</span><span class="sxs-lookup"><span data-stu-id="f799b-112">You can provide parameter values for hello linked template directly in your template or in a parameter file.</span></span> <span data-ttu-id="f799b-113">esempio Hello utilizza hello **parametri** toospecify proprietà direttamente un valore di parametro.</span><span class="sxs-lookup"><span data-stu-id="f799b-113">hello following example uses hello **parameters** property toospecify a parameter value directly.</span></span>

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

<span data-ttu-id="f799b-114">Come altri tipi di risorse, è possibile impostare le dipendenze tra modello collegato hello e altre risorse.</span><span class="sxs-lookup"><span data-stu-id="f799b-114">Like other resource types, you can set dependencies between hello linked template and other resources.</span></span> <span data-ttu-id="f799b-115">Di conseguenza, quando le altre risorse richiedono un valore di output dal modello collegato hello, è possibile verificare che sia distribuito modello collegato hello prima li.</span><span class="sxs-lookup"><span data-stu-id="f799b-115">Therefore, when other resources require an output value from hello linked template, you can make sure hello linked template is deployed before them.</span></span> <span data-ttu-id="f799b-116">In alternativa, quando il modello di hello collegato si basa su altre risorse, per verificare se che altre risorse distribuite prima modello collegato hello.</span><span class="sxs-lookup"><span data-stu-id="f799b-116">Or, when hello linked template relies on other resources, you can make sure other resources are deployed before hello linked template.</span></span> <span data-ttu-id="f799b-117">È possibile recuperare un valore da un modello collegato con hello la seguente sintassi:</span><span class="sxs-lookup"><span data-stu-id="f799b-117">You can retrieve a value from a linked template with hello following syntax:</span></span>

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

<span data-ttu-id="f799b-118">Hello del servizio Gestione risorse deve essere in grado di tooaccess modello collegato di hello.</span><span class="sxs-lookup"><span data-stu-id="f799b-118">hello Resource Manager service must be able tooaccess hello linked template.</span></span> <span data-ttu-id="f799b-119">È possibile specificare un file locale o un file che è disponibile solo in una rete locale per il modello collegato hello.</span><span class="sxs-lookup"><span data-stu-id="f799b-119">You cannot specify a local file or a file that is only available on your local network for hello linked template.</span></span> <span data-ttu-id="f799b-120">È possibile fornire solo un valore URI che includa **http** o **https**.</span><span class="sxs-lookup"><span data-stu-id="f799b-120">You can only provide a URI value that includes either **http** or **https**.</span></span> <span data-ttu-id="f799b-121">È il modello collegato in un account di archiviazione e utilizzo hello URI per l'elemento, come illustrato nell'esempio seguente hello tooplace:</span><span class="sxs-lookup"><span data-stu-id="f799b-121">One option is tooplace your linked template in a storage account, and use hello URI for that item, such as shown in hello following example:</span></span>

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

<span data-ttu-id="f799b-122">Sebbene il modello collegato hello devono essere disponibile esternamente, non è necessario toobe toohello generalmente disponibili pubblico.</span><span class="sxs-lookup"><span data-stu-id="f799b-122">Although hello linked template must be externally available, it does not need toobe generally available toohello public.</span></span> <span data-ttu-id="f799b-123">È possibile aggiungere l'account di archiviazione privato tooa modello che è proprietario dell'account di archiviazione accessibile tooonly hello.</span><span class="sxs-lookup"><span data-stu-id="f799b-123">You can add your template tooa private storage account that is accessible tooonly hello storage account owner.</span></span> <span data-ttu-id="f799b-124">È quindi possibile creare un accesso tooenable token di accesso condiviso (firma) durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f799b-124">Then, you create a shared access signature (SAS) token tooenable access during deployment.</span></span> <span data-ttu-id="f799b-125">Aggiungere tale toohello token SAS URI per il modello collegato hello.</span><span class="sxs-lookup"><span data-stu-id="f799b-125">You add that SAS token toohello URI for hello linked template.</span></span> <span data-ttu-id="f799b-126">Per conoscere la procedura per la configurazione di un modello in un account di archiviazione e per la generazione di un token con firma di accesso condiviso, consultare [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) (Distribuire le risorse con i modelli di Resource Manager e Azure PowerShell) o [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md) (Distribuire le risorse con i modelli di Azure Resource Manager e l'interfaccia della riga di comando di Azure).</span><span class="sxs-lookup"><span data-stu-id="f799b-126">For steps on setting up a template in a storage account and generating a SAS token, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) or [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> 

<span data-ttu-id="f799b-127">Hello di esempio seguente viene illustrato un modello padre tale modello tooanother collegamenti.</span><span class="sxs-lookup"><span data-stu-id="f799b-127">hello following example shows a parent template that links tooanother template.</span></span> <span data-ttu-id="f799b-128">è possibile accedere con un token di firma di accesso condiviso che viene passato come un parametro di modello collegato Hello.</span><span class="sxs-lookup"><span data-stu-id="f799b-128">hello linked template is accessed with a SAS token that is passed in as a parameter.</span></span>

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

<span data-ttu-id="f799b-129">Anche se il token hello viene passato come stringa sicura, hello URI del modello collegato hello, incluso il token di firma di accesso condiviso hello, viene registrato nelle operazioni di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="f799b-129">Even though hello token is passed in as a secure string, hello URI of hello linked template, including hello SAS token, is logged in hello deployment operations.</span></span> <span data-ttu-id="f799b-130">esposizione di toolimit, impostare una scadenza per il token hello.</span><span class="sxs-lookup"><span data-stu-id="f799b-130">toolimit exposure, set an expiration for hello token.</span></span>

<span data-ttu-id="f799b-131">Resource Manager gestisce ogni modello collegato come una distribuzione distinta.</span><span class="sxs-lookup"><span data-stu-id="f799b-131">Resource Manager handles each linked template as a separate deployment.</span></span> <span data-ttu-id="f799b-132">Nella cronologia di distribuzione hello per il gruppo di risorse hello, vedrai distribuzioni separate per padre hello e i modelli annidati.</span><span class="sxs-lookup"><span data-stu-id="f799b-132">In hello deployment history for hello resource group, you see separate deployments for hello parent and nested templates.</span></span>

![cronologia della distribuzione](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-tooa-parameter-file"></a><span data-ttu-id="f799b-134">Il collegamento di file di parametro tooa</span><span class="sxs-lookup"><span data-stu-id="f799b-134">Linking tooa parameter file</span></span>
<span data-ttu-id="f799b-135">esempio Hello utilizza hello **parametersLink** file dei parametri di proprietà toolink tooa.</span><span class="sxs-lookup"><span data-stu-id="f799b-135">hello next example uses hello **parametersLink** property toolink tooa parameter file.</span></span>

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

<span data-ttu-id="f799b-136">valore dell'URI Hello per file collegato parametro hello non può essere un file locale e deve includere una **http** o **https**.</span><span class="sxs-lookup"><span data-stu-id="f799b-136">hello URI value for hello linked parameter file cannot be a local file, and must include either **http** or **https**.</span></span> <span data-ttu-id="f799b-137">file di parametro Hello può essere limitato tooaccess tramite un token di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="f799b-137">hello parameter file can also be limited tooaccess through a SAS token.</span></span>

## <a name="using-variables-toolink-templates"></a><span data-ttu-id="f799b-138">Utilizzo di variabili toolink modelli</span><span class="sxs-lookup"><span data-stu-id="f799b-138">Using variables toolink templates</span></span>
<span data-ttu-id="f799b-139">Negli esempi precedenti Hello mostrano i valori di URL hardcoded per i collegamenti di modello hello.</span><span class="sxs-lookup"><span data-stu-id="f799b-139">hello previous examples showed hard-coded URL values for hello template links.</span></span> <span data-ttu-id="f799b-140">Questo approccio potrebbe funzionare per un modello semplice ma non funziona correttamente in caso di uso di un ampio set di modelli modulari.</span><span class="sxs-lookup"><span data-stu-id="f799b-140">This approach might work for a simple template but it does not work well when working with a large set of modular templates.</span></span> <span data-ttu-id="f799b-141">In alternativa, è possibile creare una variabile statica che archivia un URL di base per il modello principale hello e quindi creare in modo dinamico gli URL per i modelli di hello collegato da tale URL di base.</span><span class="sxs-lookup"><span data-stu-id="f799b-141">Instead, you can create a static variable that stores a base URL for hello main template and then dynamically create URLs for hello linked templates from that base URL.</span></span> <span data-ttu-id="f799b-142">Il vantaggio di Hello di questo approccio è che è possibile spostare o divisione modello hello poiché è sufficiente variabile statica di hello toochange nel modello principale hello.</span><span class="sxs-lookup"><span data-stu-id="f799b-142">hello benefit of this approach is you can easily move or fork hello template because you only need toochange hello static variable in hello main template.</span></span> <span data-ttu-id="f799b-143">modello principale Hello passa hello URI di hello scomposto modello corretto.</span><span class="sxs-lookup"><span data-stu-id="f799b-143">hello main template passes hello correct URIs throughout hello decomposed template.</span></span>

<span data-ttu-id="f799b-144">Hello esempio seguente viene illustrato come una base toocreate URL toouse due URL per collegato modelli (**sharedTemplateUrl** e **vmTemplate**).</span><span class="sxs-lookup"><span data-stu-id="f799b-144">hello following example shows how toouse a base URL toocreate two URLs for linked templates (**sharedTemplateUrl** and **vmTemplate**).</span></span> 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

<span data-ttu-id="f799b-145">È inoltre possibile utilizzare [distribuzione ()](resource-group-template-functions-deployment.md#deployment) tooget hello URL di base per il modello corrente hello e utilizzare l'URL hello tooget per gli altri modelli hello nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="f799b-145">You can also use [deployment()](resource-group-template-functions-deployment.md#deployment) tooget hello base URL for hello current template, and use that tooget hello URL for other templates in hello same location.</span></span> <span data-ttu-id="f799b-146">Questo approccio è utile se viene modificato il percorso del modello (probabilmente dovuto tooversioning) o si desidera tooavoid rigido codifica URL nel file di modello hello.</span><span class="sxs-lookup"><span data-stu-id="f799b-146">This approach is useful if your template location changes (maybe due tooversioning) or you want tooavoid hard coding URLs in hello template file.</span></span> 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a><span data-ttu-id="f799b-147">Esempio completo</span><span class="sxs-lookup"><span data-stu-id="f799b-147">Complete example</span></span>
<span data-ttu-id="f799b-148">Hello modelli di esempio seguente mostra una disposizione semplificata dei modelli collegati tooillustrate alcuni dei concetti hello in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="f799b-148">hello following example templates show a simplified arrangement of linked templates tooillustrate several of hello concepts in this article.</span></span> <span data-ttu-id="f799b-149">Si presuppone che i modelli di hello sono stati aggiunti toohello stesso contenitore in un account di archiviazione con accesso pubblico disattivato.</span><span class="sxs-lookup"><span data-stu-id="f799b-149">It assumes hello templates have been added toohello same container in a storage account with public access turned off.</span></span> <span data-ttu-id="f799b-150">modello collegato Hello passa un valore toohello indietro principale dei modelli in hello **restituisce** sezione.</span><span class="sxs-lookup"><span data-stu-id="f799b-150">hello linked template passes a value back toohello main template in hello **outputs** section.</span></span>

<span data-ttu-id="f799b-151">Hello **parent.json** file costituito da:</span><span class="sxs-lookup"><span data-stu-id="f799b-151">hello **parent.json** file consists of:</span></span>

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

<span data-ttu-id="f799b-152">Hello **helloworld.json** file costituito da:</span><span class="sxs-lookup"><span data-stu-id="f799b-152">hello **helloworld.json** file consists of:</span></span>

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

<span data-ttu-id="f799b-153">In PowerShell, ottenere un token per il contenitore di hello e distribuire modelli hello con:</span><span class="sxs-lookup"><span data-stu-id="f799b-153">In PowerShell, you get a token for hello container and deploy hello templates with:</span></span>

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

<span data-ttu-id="f799b-154">2.0 CLI di Azure, ottenere un token per il contenitore di hello e distribuire modelli hello con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="f799b-154">In Azure CLI 2.0, you get a token for hello container and deploy hello templates with hello following code:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f799b-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f799b-155">Next steps</span></span>
* <span data-ttu-id="f799b-156">vedere toolearn sulla definizione di ordine di distribuzione hello per le risorse, hello [definizione delle dipendenze nei modelli di gestione risorse di Azure](resource-group-define-dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="f799b-156">toolearn about hello defining hello deployment order for your resources, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md)</span></span>
* <span data-ttu-id="f799b-157">toolearn come una risorsa toodefine ma creare molte istanze di, vedere [creare più istanze delle risorse di gestione risorse di Azure](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="f799b-157">toolearn how toodefine one resource but create many instances of it, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>

