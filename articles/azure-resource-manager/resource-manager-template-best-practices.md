---
title: aaaBest procedure consigliate per la creazione di modelli di gestione risorse | Documenti Microsoft
description: Linee guida per la semplificazione dei modelli di Azure Resource Manager.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: ec9bbe218c4f2c6a92ca44b5e9c9c71029e22151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a><span data-ttu-id="99d03-103">Procedure consigliate per la creazione di modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="99d03-103">Best practices for creating Azure Resource Manager templates</span></span>
<span data-ttu-id="99d03-104">Queste linee guida consentono di creare modelli di Azure Resource Manager toouse semplice e affidabile.</span><span class="sxs-lookup"><span data-stu-id="99d03-104">These guidelines can help you create Azure Resource Manager templates that are reliable and easy toouse.</span></span> <span data-ttu-id="99d03-105">linee guida di Hello sono solo suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="99d03-105">hello guidelines are only suggestions.</span></span> <span data-ttu-id="99d03-106">e non come requisiti assoluti, salvo diversa indicazione.</span><span class="sxs-lookup"><span data-stu-id="99d03-106">They are not requirements, except where noted.</span></span> <span data-ttu-id="99d03-107">Lo scenario potrebbe richiedere una variante di uno di hello seguenti approcci o esempi.</span><span class="sxs-lookup"><span data-stu-id="99d03-107">Your scenario might require a variation of one of hello following approaches or examples.</span></span>

## <a name="resource-names"></a><span data-ttu-id="99d03-108">Nomi di risorse</span><span class="sxs-lookup"><span data-stu-id="99d03-108">Resource names</span></span>
<span data-ttu-id="99d03-109">In genere vengono usati tre tipi di nomi di risorse in Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="99d03-109">Generally, you work with three types of resource names in Resource Manager:</span></span>

* <span data-ttu-id="99d03-110">Nomi di risorse che devono essere univoci.</span><span class="sxs-lookup"><span data-stu-id="99d03-110">Resource names that must be unique.</span></span>
* <span data-ttu-id="99d03-111">I nomi delle risorse che non sono necessari toobe univoco, ma si sceglie un nome che può aiutarti a identificare una risorsa in base al contesto tooprovide.</span><span class="sxs-lookup"><span data-stu-id="99d03-111">Resource names that are not required toobe unique, but you choose tooprovide a name that can help you identify a resource based on context.</span></span>
* <span data-ttu-id="99d03-112">Nomi di risorse che possono essere generici.</span><span class="sxs-lookup"><span data-stu-id="99d03-112">Resource names that can be generic.</span></span>

 <span data-ttu-id="99d03-113">Per informazioni sulle restrizioni relative ai nomi di risorse, vedere [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md)(Convenzioni di denominazione consigliate per le risorse di Azure).</span><span class="sxs-lookup"><span data-stu-id="99d03-113">For information about resource name restrictions, see [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md).</span></span>

### <a name="unique-resource-names"></a><span data-ttu-id="99d03-114">Nomi di risorse univoci</span><span class="sxs-lookup"><span data-stu-id="99d03-114">Unique resource names</span></span>
<span data-ttu-id="99d03-115">È necessario fornire un nome univoco per qualsiasi tipo di risorsa con un endpoint di accesso ai dati.</span><span class="sxs-lookup"><span data-stu-id="99d03-115">You must provide a unique resource name for any resource type that has a data access endpoint.</span></span> <span data-ttu-id="99d03-116">Alcuni tipi di risorse comuni che richiedono un nome univoco includono:</span><span class="sxs-lookup"><span data-stu-id="99d03-116">Some common resource types that require a unique name include:</span></span>

* <span data-ttu-id="99d03-117">Archiviazione di Azure<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="99d03-117">Azure Storage<sup>1</sup></span></span> 
* <span data-ttu-id="99d03-118">Funzionalità app Web del servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="99d03-118">Web Apps feature of Azure App Service</span></span>
* <span data-ttu-id="99d03-119">SQL Server</span><span class="sxs-lookup"><span data-stu-id="99d03-119">SQL Server</span></span>
* <span data-ttu-id="99d03-120">Insieme di credenziali chiave Azure</span><span class="sxs-lookup"><span data-stu-id="99d03-120">Azure Key Vault</span></span>
* <span data-ttu-id="99d03-121">Cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="99d03-121">Azure Redis Cache</span></span>
* <span data-ttu-id="99d03-122">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="99d03-122">Azure Batch</span></span>
* <span data-ttu-id="99d03-123">Gestione traffico di Azure</span><span class="sxs-lookup"><span data-stu-id="99d03-123">Azure Traffic Manager</span></span>
* <span data-ttu-id="99d03-124">Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="99d03-124">Azure Search</span></span>
* <span data-ttu-id="99d03-125">HDInsight di Azure</span><span class="sxs-lookup"><span data-stu-id="99d03-125">Azure HDInsight</span></span>

<span data-ttu-id="99d03-126"><sup>1</sup> I nomi di account di archiviazione devono essere formati da lettere minuscole, un massimo di 24 caratteri e non devono includere alcun segno meno.</span><span class="sxs-lookup"><span data-stu-id="99d03-126"><sup>1</sup> Storage account names also must be lowercase, 24 characters or less, and not have any hyphens.</span></span>

<span data-ttu-id="99d03-127">Se si fornisce un parametro per un nome di risorsa, è necessario fornire un nome univoco, quando si distribuiscono risorse hello.</span><span class="sxs-lookup"><span data-stu-id="99d03-127">If you provide a parameter for a resource name, you must provide a unique name when you deploy hello resource.</span></span> <span data-ttu-id="99d03-128">Facoltativamente, è possibile creare una variabile che utilizza hello [uniqueString()](resource-group-template-functions-string.md#uniquestring) toogenerate un nome di funzione.</span><span class="sxs-lookup"><span data-stu-id="99d03-128">Optionally, you can create a variable that uses hello [uniqueString()](resource-group-template-functions-string.md#uniquestring) function toogenerate a name.</span></span> 

<span data-ttu-id="99d03-129">È anche possibile desidera tooadd un prefisso o suffisso toohello **uniqueString** risultato.</span><span class="sxs-lookup"><span data-stu-id="99d03-129">You also might want tooadd a prefix or suffix toohello **uniqueString** result.</span></span> <span data-ttu-id="99d03-130">Modifica nome univoco di hello può identificare più facilmente il tipo di risorsa hello dal nome hello.</span><span class="sxs-lookup"><span data-stu-id="99d03-130">Modifying hello unique name can help you more easily identify hello resource type from hello name.</span></span> <span data-ttu-id="99d03-131">Ad esempio, è possibile generare un nome univoco per un account di archiviazione tramite hello segue variabile:</span><span class="sxs-lookup"><span data-stu-id="99d03-131">For example, you can generate a unique name for a storage account by using hello following variable:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a><span data-ttu-id="99d03-132">Nomi di risorse per l'identificazione</span><span class="sxs-lookup"><span data-stu-id="99d03-132">Resource names for identification</span></span>
<span data-ttu-id="99d03-133">Alcuni tipi di risorsa potrebbe essere necessario tooname, ma i relativi nomi non devono toobe univoco.</span><span class="sxs-lookup"><span data-stu-id="99d03-133">Some resource types you might want tooname, but their names do not have toobe unique.</span></span> <span data-ttu-id="99d03-134">Per questi tipi di risorsa, è possibile fornire un nome che identifica il contesto di risorsa hello sia il tipo di risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="99d03-134">For these resource types, you can provide a name that identifies both hello resource context and hello resource type.</span></span> <span data-ttu-id="99d03-135">Specificare un nome descrittivo che consente di identificare risorse hello in un elenco di risorse.</span><span class="sxs-lookup"><span data-stu-id="99d03-135">Provide a descriptive name that helps you identify hello resource in a list of resources.</span></span> <span data-ttu-id="99d03-136">Se è necessario un nome di risorsa diverso per distribuzioni diverse toouse, è possibile utilizzare un parametro per il nome di hello:</span><span class="sxs-lookup"><span data-stu-id="99d03-136">If you need toouse a different resource name for different deployments, you can use a parameter for hello name:</span></span>

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "hello name of hello VM toocreate."
        }
    }
}
```

<span data-ttu-id="99d03-137">Se non è necessario toopass in un nome durante la distribuzione, è possibile utilizzare una variabile:</span><span class="sxs-lookup"><span data-stu-id="99d03-137">If you do not need toopass in a name during deployment, you can use a variable:</span></span> 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

<span data-ttu-id="99d03-138">In alternativa si può usare un valore hardcoded:</span><span class="sxs-lookup"><span data-stu-id="99d03-138">You also can use a hard-coded value:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a><span data-ttu-id="99d03-139">Nomi di risorse generici</span><span class="sxs-lookup"><span data-stu-id="99d03-139">Generic resource names</span></span>
<span data-ttu-id="99d03-140">Per i tipi di risorse per lo più accessibile tramite una risorsa diversa, è possibile utilizzare un nome generico che è hardcoded nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="99d03-140">For resource types that you mostly access through a different resource, you can use a generic name that is hard-coded in hello template.</span></span> <span data-ttu-id="99d03-141">Ad esempio, è possibile impostare un nome generico e standard per le regole del firewall in SQL server:</span><span class="sxs-lookup"><span data-stu-id="99d03-141">For example, you can set a standard, generic name for firewall rules on a SQL server:</span></span>

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a><span data-ttu-id="99d03-142">parameters</span><span class="sxs-lookup"><span data-stu-id="99d03-142">Parameters</span></span>
<span data-ttu-id="99d03-143">Hello informazioni seguenti possono essere utili quando si utilizzano parametri:</span><span class="sxs-lookup"><span data-stu-id="99d03-143">hello following information can be helpful when you work with parameters:</span></span>

* <span data-ttu-id="99d03-144">Ridurre al minimo l'uso di parametri.</span><span class="sxs-lookup"><span data-stu-id="99d03-144">Minimize your use of parameters.</span></span> <span data-ttu-id="99d03-145">Se possibile, usare una variabile o un valore letterale.</span><span class="sxs-lookup"><span data-stu-id="99d03-145">Whenever possible, use a variable or a literal value.</span></span> <span data-ttu-id="99d03-146">Specificare parametri solo per questi scenari:</span><span class="sxs-lookup"><span data-stu-id="99d03-146">Use parameters only for these scenarios:</span></span>
   
   * <span data-ttu-id="99d03-147">Impostazioni che si desidera toouse variazioni di base tooenvironment (SKU, dimensioni e dalla capacità).</span><span class="sxs-lookup"><span data-stu-id="99d03-147">Settings that you want toouse variations of according tooenvironment (SKU, size, capacity).</span></span>
   * <span data-ttu-id="99d03-148">Nomi delle risorse che si desidera toospecify per facilitare l'identificazione.</span><span class="sxs-lookup"><span data-stu-id="99d03-148">Resource names that you want toospecify for easy identification.</span></span>
   * <span data-ttu-id="99d03-149">Valori di uso frequente toocomplete altre attività (ad esempio, un nome utente di amministratore).</span><span class="sxs-lookup"><span data-stu-id="99d03-149">Values that you use frequently toocomplete other tasks (such as an admin user name).</span></span>
   * <span data-ttu-id="99d03-150">Segreti (ad esempio password).</span><span class="sxs-lookup"><span data-stu-id="99d03-150">Secrets (such as passwords).</span></span>
   * <span data-ttu-id="99d03-151">numero di Hello o una matrice di valori toouse quando si creano più istanze di un tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="99d03-151">hello number or array of values toouse when you create multiple instances of a resource type.</span></span>
* <span data-ttu-id="99d03-152">Usare la notazione Camel per i nomi dei parametri.</span><span class="sxs-lookup"><span data-stu-id="99d03-152">Use camel case for parameter names.</span></span>
* <span data-ttu-id="99d03-153">Fornire una descrizione di ogni parametro nei metadati hello:</span><span class="sxs-lookup"><span data-stu-id="99d03-153">Provide a description of every parameter in hello metadata:</span></span>

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "hello type of hello new storage account created toostore hello VM disks."
           }
       }
   }
   ```

* <span data-ttu-id="99d03-154">Definire i valori predefiniti per i parametri (ad eccezione delle password e delle chiavi SSH):</span><span class="sxs-lookup"><span data-stu-id="99d03-154">Define default values for parameters (except for passwords and SSH keys):</span></span>
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "hello type of hello new storage account created toostore hello VM disks."
            }
        }
   }
   ```

* <span data-ttu-id="99d03-155">Usare **SecureString** per tutte le password e i segreti:</span><span class="sxs-lookup"><span data-stu-id="99d03-155">Use **SecureString** for all passwords and secrets:</span></span> 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "hello value of hello secret toostore in hello vault."
           }
       }
   }
   ```

* <span data-ttu-id="99d03-156">Quando possibile, non utilizzare un percorso di toospecify di parametro.</span><span class="sxs-lookup"><span data-stu-id="99d03-156">Whenever possible, don't use a parameter toospecify location.</span></span> <span data-ttu-id="99d03-157">Utilizzare invece hello **percorso** proprietà hello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="99d03-157">Instead, use hello **location** property of hello resource group.</span></span> <span data-ttu-id="99d03-158">Utilizzando hello **gruppo di risorse () .location** espressione per tutte le risorse, le risorse nel modello hello vengono distribuite in hello stesso percorso del gruppo di risorse hello:</span><span class="sxs-lookup"><span data-stu-id="99d03-158">By using hello **resourceGroup().location** expression for all your resources, resources in hello template are deployed in hello same location as hello resource group:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   <span data-ttu-id="99d03-159">Se un tipo di risorsa è supportato in solo un numero limitato di percorsi, è un percorso valido direttamente nel modello di hello toospecify.</span><span class="sxs-lookup"><span data-stu-id="99d03-159">If a resource type is supported in only a limited number of locations, you might want toospecify a valid location directly in hello template.</span></span> <span data-ttu-id="99d03-160">Se è necessario utilizzare un **percorso** parametro condividere tale valore del parametro quanto possibile con le risorse che sono probabilmente toobe in hello nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="99d03-160">If you must use a **location** parameter, share that parameter value as much as possible with resources that are likely toobe in hello same location.</span></span> <span data-ttu-id="99d03-161">Questo riduce il numero di hello di volte in cui gli utenti vengono richiesto di informazioni sul percorso tooprovide.</span><span class="sxs-lookup"><span data-stu-id="99d03-161">This minimizes hello number of times users are asked tooprovide location information.</span></span>
* <span data-ttu-id="99d03-162">Evitare di utilizzare un parametro o una variabile per la versione API hello per un tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="99d03-162">Avoid using a parameter or variable for hello API version for a resource type.</span></span> <span data-ttu-id="99d03-163">I valori e le proprietà delle risorse possono variare in base al numero di versione.</span><span class="sxs-lookup"><span data-stu-id="99d03-163">Resource properties and values can vary by version number.</span></span> <span data-ttu-id="99d03-164">In un editor di codice IntelliSense non può determinare schema corretto hello quando è impostato versione API hello tooa parametro o variabile.</span><span class="sxs-lookup"><span data-stu-id="99d03-164">IntelliSense in a code editor cannot determine hello correct schema when hello API version is set tooa parameter or variable.</span></span> <span data-ttu-id="99d03-165">Livello di codice hello invece la versione API nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="99d03-165">Instead, hard-code hello API version in hello template.</span></span>

## <a name="variables"></a><span data-ttu-id="99d03-166">variables</span><span class="sxs-lookup"><span data-stu-id="99d03-166">Variables</span></span>
<span data-ttu-id="99d03-167">Hello seguenti informazioni possono essere utili quando si utilizzano variabili:</span><span class="sxs-lookup"><span data-stu-id="99d03-167">hello following information can be helpful when you work with variables:</span></span>

* <span data-ttu-id="99d03-168">Utilizzare le variabili per i valori necessari toouse più volte in un modello.</span><span class="sxs-lookup"><span data-stu-id="99d03-168">Use variables for values that you need toouse more than once in a template.</span></span> <span data-ttu-id="99d03-169">Se un valore viene utilizzato una sola volta, un valore a livello di codice rende il tooread più semplice del modello.</span><span class="sxs-lookup"><span data-stu-id="99d03-169">If a value is used only once, a hard-coded value makes your template easier tooread.</span></span>
* <span data-ttu-id="99d03-170">Non è possibile utilizzare hello [riferimento](resource-group-template-functions-resource.md#reference) funzione hello **variabili** sezione del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="99d03-170">You cannot use hello [reference](resource-group-template-functions-resource.md#reference) function in hello **variables** section of hello template.</span></span> <span data-ttu-id="99d03-171">Hello **riferimento** funzione deriva il relativo valore dallo stato di runtime della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="99d03-171">hello **reference** function derives its value from hello resource's runtime state.</span></span> <span data-ttu-id="99d03-172">Tuttavia, le variabili vengono risolti durante l'analisi del modello di hello iniziale hello.</span><span class="sxs-lookup"><span data-stu-id="99d03-172">However, variables are resolved during hello initial parsing of hello template.</span></span> <span data-ttu-id="99d03-173">Costruire valori che devono hello **riferimento** funzione direttamente in hello **risorse** o **restituisce** sezione del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="99d03-173">Construct values that need hello **reference** function directly in hello **resources** or **outputs** section of hello template.</span></span>
* <span data-ttu-id="99d03-174">Includere le variabili per i nomi di risorse che devono essere univoci, come illustrato in [Nomi di risorse](#resource-names).</span><span class="sxs-lookup"><span data-stu-id="99d03-174">Include variables for resource names that must be unique, as described in [Resource names](#resource-names).</span></span>
* <span data-ttu-id="99d03-175">È possibile raggruppare le variabili in oggetti complessi.</span><span class="sxs-lookup"><span data-stu-id="99d03-175">You can group variables into complex objects.</span></span> <span data-ttu-id="99d03-176">Hello utilizzare **variable.subentry** formato tooreference un valore da un oggetto complesso.</span><span class="sxs-lookup"><span data-stu-id="99d03-176">Use hello **variable.subentry** format tooreference a value from a complex object.</span></span> <span data-ttu-id="99d03-177">Il raggruppamento delle variabili consente di tenere traccia delle variabili correlate</span><span class="sxs-lookup"><span data-stu-id="99d03-177">Grouping variables can help you track related variables.</span></span> <span data-ttu-id="99d03-178">Inoltre, migliora la leggibilità del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="99d03-178">It also improves readability of hello template.</span></span> <span data-ttu-id="99d03-179">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="99d03-179">Here's an example:</span></span>
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > <span data-ttu-id="99d03-180">Un oggetto complesso non può contenere un'espressione che fa riferimento a un valore da un oggetto complesso.</span><span class="sxs-lookup"><span data-stu-id="99d03-180">A complex object cannot contain an expression that references a value from a complex object.</span></span> <span data-ttu-id="99d03-181">A questo scopo, definire una variabile separata.</span><span class="sxs-lookup"><span data-stu-id="99d03-181">Define a separate variable for this purpose.</span></span>
   > 
   > 
   
     <span data-ttu-id="99d03-182">Per esempi avanzati di uso di oggetti complessi come variabili, vedere [Condividere lo stato tra modelli di Azure Resource Manager](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="99d03-182">For advanced examples of using complex objects as variables, see [Share state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="resources"></a><span data-ttu-id="99d03-183">Risorse</span><span class="sxs-lookup"><span data-stu-id="99d03-183">Resources</span></span>
<span data-ttu-id="99d03-184">Hello seguenti informazioni possono essere utili quando si lavora con risorse:</span><span class="sxs-lookup"><span data-stu-id="99d03-184">hello following information can be helpful when you work with resources:</span></span>

* <span data-ttu-id="99d03-185">toohelp altri collaboratori comprendere hello scopo della risorsa hello, specificare **commenti** per ogni risorsa nel modello hello:</span><span class="sxs-lookup"><span data-stu-id="99d03-185">toohelp other contributors understand hello purpose of hello resource, specify **comments** for each resource in hello template:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used toostore hello VM disks.",
         ...
     }
   ]
   ```

* <span data-ttu-id="99d03-186">È possibile usare tag tooadd metadati tooresources.</span><span class="sxs-lookup"><span data-stu-id="99d03-186">You can use tags tooadd metadata tooresources.</span></span> <span data-ttu-id="99d03-187">Utilizzare i metadati tooadd informazioni sulle risorse.</span><span class="sxs-lookup"><span data-stu-id="99d03-187">Use metadata tooadd information about your resources.</span></span> <span data-ttu-id="99d03-188">Ad esempio, è possibile aggiungere metadati toorecord i dettagli di fatturazione per una risorsa.</span><span class="sxs-lookup"><span data-stu-id="99d03-188">For example, you can add metadata toorecord billing details for a resource.</span></span> <span data-ttu-id="99d03-189">Per ulteriori informazioni, vedere [tramite tag tooorganize le risorse di Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="99d03-189">For more information, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>
* <span data-ttu-id="99d03-190">Se si utilizza un *endpoint pubblico* nel modello (ad esempio, un Blob di Azure storage endpoint pubblico), *eseguire hardcoded* hello dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="99d03-190">If you use a *public endpoint* in your template (such as an Azure Blob storage public endpoint), *do not hard-code* hello namespace.</span></span> <span data-ttu-id="99d03-191">Hello utilizzare **riferimento** toodynamically funzione recuperare hello dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="99d03-191">Use hello **reference** function toodynamically retrieve hello namespace.</span></span> <span data-ttu-id="99d03-192">È possibile utilizzare gli ambienti di spazio dei nomi pubblici questo approccio toodeploy hello modello toodifferent senza modificare manualmente l'endpoint di hello nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="99d03-192">You can use this approach toodeploy hello template toodifferent public namespace environments without manually changing hello endpoint in hello template.</span></span> <span data-ttu-id="99d03-193">Impostare hello API versione toohello stessa versione in uso per l'account di archiviazione hello nel modello:</span><span class="sxs-lookup"><span data-stu-id="99d03-193">Set hello API version toohello same version that you are using for hello storage account in your template:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="99d03-194">Se l'account di archiviazione hello viene distribuito in hello stesso modello che si sta creando, non è necessario spazio dei nomi del provider di hello toospecify quando si fa riferimento a risorse hello.</span><span class="sxs-lookup"><span data-stu-id="99d03-194">If hello storage account is deployed in hello same template that you are creating, you do not need toospecify hello provider namespace when you reference hello resource.</span></span> <span data-ttu-id="99d03-195">Questa è la sintassi semplificata hello:</span><span class="sxs-lookup"><span data-stu-id="99d03-195">This is hello simplified syntax:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="99d03-196">Se si dispone di altri valori nel modello toouse configurato uno spazio dei nomi pubblico, modificare questi valori tooreflect hello stesso **riferimento** (funzione).</span><span class="sxs-lookup"><span data-stu-id="99d03-196">If you have other values in your template that are configured toouse a public namespace, change these values tooreflect hello same **reference** function.</span></span> <span data-ttu-id="99d03-197">Ad esempio, è possibile impostare hello **storageUri** proprietà del profilo di diagnostica della macchina virtuale hello:</span><span class="sxs-lookup"><span data-stu-id="99d03-197">For example, you can set hello **storageUri** property of hello virtual machine diagnostics profile:</span></span>
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   <span data-ttu-id="99d03-198">È anche possibile fare riferimento a un account di archiviazione in un gruppo di risorse diverso:</span><span class="sxs-lookup"><span data-stu-id="99d03-198">You also can reference an existing storage account that is in a different resource group:</span></span>

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* <span data-ttu-id="99d03-199">Assegnare pubblica macchina di virtuale tooa di indirizzi IP solo quando richiesto da un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="99d03-199">Assign public IP addresses tooa virtual machine only when an application requires it.</span></span> <span data-ttu-id="99d03-200">tooconnect tooa macchina virtuale (VM) per il debug o per la gestione o a scopi amministrativi, utilizzare le regole NAT in ingresso, un gateway di rete virtuale o un jumpbox.</span><span class="sxs-lookup"><span data-stu-id="99d03-200">tooconnect tooa virtual machine (VM) for debugging, or for management or administrative purposes, use inbound NAT rules, a virtual network gateway, or a jumpbox.</span></span>
   
     <span data-ttu-id="99d03-201">Per ulteriori informazioni sulla connessione toovirtual macchine, vedere:</span><span class="sxs-lookup"><span data-stu-id="99d03-201">For more information about connecting toovirtual machines, see:</span></span>
   
   * [<span data-ttu-id="99d03-202">Eseguire macchine virtuali per un'architettura a più livelli in Azure</span><span class="sxs-lookup"><span data-stu-id="99d03-202">Run VMs for an N-tier architecture in Azure</span></span>](../guidance/guidance-compute-n-tier-vm.md)
   * [<span data-ttu-id="99d03-203">Configurare l'accesso WinRM per le macchine virtuali in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="99d03-203">Set up WinRM access for VMs in Azure Resource Manager</span></span>](../virtual-machines/windows/winrm.md)
   * [<span data-ttu-id="99d03-204">Consentire l'accesso esterno tooyour VM usando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="99d03-204">Allow external access tooyour VM by using hello Azure portal</span></span>](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [<span data-ttu-id="99d03-205">Consentire l'accesso esterno tooyour VM tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="99d03-205">Allow external access tooyour VM by using PowerShell</span></span>](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [<span data-ttu-id="99d03-206">Consentire l'accesso esterno tooyour VM Linux tramite CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="99d03-206">Allow external access tooyour Linux VM by using Azure CLI</span></span>](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* <span data-ttu-id="99d03-207">Hello **domainNameLabel** proprietà per gli indirizzi IP pubblici devono essere univoci.</span><span class="sxs-lookup"><span data-stu-id="99d03-207">hello **domainNameLabel** property for public IP addresses must be unique.</span></span> <span data-ttu-id="99d03-208">Hello **domainNameLabel** valore deve essere compresa tra 3 e 63 caratteri e seguire le regole di hello specificate da questa espressione regolare: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span><span class="sxs-lookup"><span data-stu-id="99d03-208">hello **domainNameLabel** value must be between 3 and 63 characters long, and follow hello rules specified by this regular expression: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span></span> <span data-ttu-id="99d03-209">Poiché hello **uniqueString** funzione genera una stringa di 13 caratteri, hello **dnsPrefixString** parametro è limitato too50 caratteri:</span><span class="sxs-lookup"><span data-stu-id="99d03-209">Because hello **uniqueString** function generates a string that is 13 characters long, hello **dnsPrefixString** parameter is limited too50 characters:</span></span>

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "hello DNS label for hello public IP address. It must be lowercase. It should match hello following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* <span data-ttu-id="99d03-210">Quando si aggiunge un'estensione di uno script personalizzato tooa password, utilizzare hello **commandToExecute** proprietà hello **protectedSettings** proprietà:</span><span class="sxs-lookup"><span data-stu-id="99d03-210">When you add a password tooa custom script extension, use hello **commandToExecute** property in hello **protectedSettings** property:</span></span>
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > <span data-ttu-id="99d03-211">tooensure che informazioni riservate vengono crittografate quando vengono passati come parametri tooVMs ed estensioni, utilizzare hello **protectedSettings** proprietà delle estensioni di hello pertinente.</span><span class="sxs-lookup"><span data-stu-id="99d03-211">tooensure that secrets are encrypted when they are passed as parameters tooVMs and extensions, use hello **protectedSettings** property of hello relevant extensions.</span></span>
   > 
   > 

## <a name="outputs"></a><span data-ttu-id="99d03-212">outputs</span><span class="sxs-lookup"><span data-stu-id="99d03-212">Outputs</span></span>
<span data-ttu-id="99d03-213">Se si utilizzano un modello toocreate gli indirizzi IP pubblici, includere un **restituisce** sezione che restituisce i dettagli di indirizzo IP hello e il nome di dominio completo hello (FQDN).</span><span class="sxs-lookup"><span data-stu-id="99d03-213">If you use a template toocreate public IP addresses, include an **outputs** section that returns details of hello IP address and hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="99d03-214">Dopo la distribuzione, è possibile utilizzare output valori tooeasily recuperare dettagli pubblica gli indirizzi IP e nomi di dominio completi.</span><span class="sxs-lookup"><span data-stu-id="99d03-214">You can use output values tooeasily retrieve details about public IP addresses and FQDNs after deployment.</span></span> <span data-ttu-id="99d03-215">Quando si fa riferimento a risorse hello, utilizzare una versione di hello API utilizzate toocreate è:</span><span class="sxs-lookup"><span data-stu-id="99d03-215">When you reference hello resource, use hello API version that you used toocreate it:</span></span> 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a><span data-ttu-id="99d03-216">Modello singolo o modelli annidati</span><span class="sxs-lookup"><span data-stu-id="99d03-216">Single template vs. nested templates</span></span>
<span data-ttu-id="99d03-217">toodeploy la soluzione, è possibile utilizzare un singolo modello o un modello principale con più modelli annidati.</span><span class="sxs-lookup"><span data-stu-id="99d03-217">toodeploy your solution, you can use either a single template or a main template with multiple nested templates.</span></span> <span data-ttu-id="99d03-218">I modelli annidati sono comuni per scenari più avanzati.</span><span class="sxs-lookup"><span data-stu-id="99d03-218">Nested templates are common for more advanced scenarios.</span></span> <span data-ttu-id="99d03-219">Utilizzo di un consente di modello nidificato hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="99d03-219">Using a nested template gives you hello following advantages:</span></span>

* <span data-ttu-id="99d03-220">È possibile scomporre la soluzione in componenti di destinazione.</span><span class="sxs-lookup"><span data-stu-id="99d03-220">You can break down a solution into targeted components.</span></span>
* <span data-ttu-id="99d03-221">È possibile riusare i modelli annidati con modelli principali diversi.</span><span class="sxs-lookup"><span data-stu-id="99d03-221">You can reuse nested templates with different main templates.</span></span>

<span data-ttu-id="99d03-222">Se si sceglie di modelli annidati toouse, hello alle linee guida consentono di standardizzare schema del modello.</span><span class="sxs-lookup"><span data-stu-id="99d03-222">If you choose toouse nested templates, hello following guidelines can help you standardize your template design.</span></span> <span data-ttu-id="99d03-223">Queste linee guida si basano sui [criteri di progettazione per modelli di Azure Resource Manager](best-practices-resource-manager-design-templates.md).</span><span class="sxs-lookup"><span data-stu-id="99d03-223">These guidelines are based on [patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span></span> <span data-ttu-id="99d03-224">È consigliabile una progettazione con hello seguenti modelli:</span><span class="sxs-lookup"><span data-stu-id="99d03-224">We recommend a design that has hello following templates:</span></span>

* <span data-ttu-id="99d03-225">**Modello principale** (azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="99d03-225">**Main template** (azuredeploy.json).</span></span> <span data-ttu-id="99d03-226">Utilizzo per i parametri di input hello.</span><span class="sxs-lookup"><span data-stu-id="99d03-226">Use for hello input parameters.</span></span>
* <span data-ttu-id="99d03-227">**Modello di risorse condivise**.</span><span class="sxs-lookup"><span data-stu-id="99d03-227">**Shared resources template**.</span></span> <span data-ttu-id="99d03-228">Le risorse che utilizzano tutte le altre risorse sono condivise toodeploy utilizzare (ad esempio, virtuale rete e la disponibilità set).</span><span class="sxs-lookup"><span data-stu-id="99d03-228">Use toodeploy shared resources that all other resources use (for example, virtual network and availability sets).</span></span> <span data-ttu-id="99d03-229">Hello utilizzare **dependsOn** espressione tooensure che questo modello viene distribuito prima di altri modelli.</span><span class="sxs-lookup"><span data-stu-id="99d03-229">Use hello **dependsOn** expression tooensure that this template is deployed before other templates.</span></span>
* <span data-ttu-id="99d03-230">**Modello di risorse facoltative**.</span><span class="sxs-lookup"><span data-stu-id="99d03-230">**Optional resources template**.</span></span> <span data-ttu-id="99d03-231">Utilizzare tooconditionally distribuire risorse in base a un parametro (ad esempio, un jumpbox).</span><span class="sxs-lookup"><span data-stu-id="99d03-231">Use tooconditionally deploy resources based on a parameter (for example, a jumpbox).</span></span>
* <span data-ttu-id="99d03-232">**Modello di risorse membro**.</span><span class="sxs-lookup"><span data-stu-id="99d03-232">**Member resources template**.</span></span> <span data-ttu-id="99d03-233">Ogni tipo di istanza all'interno di un livello di applicazione prevede una propria configurazione.</span><span class="sxs-lookup"><span data-stu-id="99d03-233">Each instance type within an application tier has its own configuration.</span></span> <span data-ttu-id="99d03-234">All'interno di un livello, è possibile definire diversi tipi di istanza.</span><span class="sxs-lookup"><span data-stu-id="99d03-234">Within a tier, you can define different instance types.</span></span> <span data-ttu-id="99d03-235">(Ad esempio, hello prima istanza di viene creato un cluster e istanze aggiuntive vengono aggiunte cluster esistente toohello.) Ogni tipo di istanza avrà un proprio modello di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="99d03-235">(For example, hello first instance creates a cluster, and additional instances are added toohello existing cluster.) Each instance type has its own deployment template.</span></span>
* <span data-ttu-id="99d03-236">**Script**.</span><span class="sxs-lookup"><span data-stu-id="99d03-236">**Scripts**.</span></span> <span data-ttu-id="99d03-237">Per ogni tipo di istanza sono applicabili script ampiamente riutilizzabili, come ad esempio quelli di inizializzazione e formattazione di dischi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="99d03-237">Widely reusable scripts are applicable for each instance type (for example, initialize and format additional disks).</span></span> <span data-ttu-id="99d03-238">Gli script personalizzati creati per uno scopo specifico di personalizzazione sono diversi, in base al tipo di istanza hello.</span><span class="sxs-lookup"><span data-stu-id="99d03-238">Custom scripts that you create for a specific customization purpose are different, based on hello instance type.</span></span>

![Modello annidato](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

<span data-ttu-id="99d03-240">Per altre informazioni, vedere [Uso di modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="99d03-240">For more information, see [Use linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="conditionally-link-toonested-templates"></a><span data-ttu-id="99d03-241">Collegare in modo condizionale toonested modelli</span><span class="sxs-lookup"><span data-stu-id="99d03-241">Conditionally link toonested templates</span></span>
<span data-ttu-id="99d03-242">È possibile utilizzare modelli di toonested un parametro tooconditionally collegamento.</span><span class="sxs-lookup"><span data-stu-id="99d03-242">You can use a parameter tooconditionally link toonested templates.</span></span> <span data-ttu-id="99d03-243">il parametro Hello diventa parte di hello URI per il modello di hello:</span><span class="sxs-lookup"><span data-stu-id="99d03-243">hello parameter becomes part of hello URI for hello template:</span></span>

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a><span data-ttu-id="99d03-244">Formato del modello</span><span class="sxs-lookup"><span data-stu-id="99d03-244">Template format</span></span>
<span data-ttu-id="99d03-245">È una buona norma toopass il modello tramite un validator JSON.</span><span class="sxs-lookup"><span data-stu-id="99d03-245">It's a good practice toopass your template through a JSON validator.</span></span> <span data-ttu-id="99d03-246">Un validator può aiutare a rimuovere virgole, parentesi e parentesi quadre estranee che potrebbero causare un errore durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="99d03-246">A validator can help you remove extraneous commas, parentheses, and brackets that might cause an error during deployment.</span></span> <span data-ttu-id="99d03-247">Provare [JSONlint](http://jsonlint.com/) o un pacchetto linter per l'ambiente di modifica preferito (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="99d03-247">Try [JSONLint](http://jsonlint.com/) or a linter package for your favorite editing environment (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span></span>

<span data-ttu-id="99d03-248">È anche una buona idea tooformat il file JSON per una migliore leggibilità.</span><span class="sxs-lookup"><span data-stu-id="99d03-248">It's also a good idea tooformat your JSON for better readability.</span></span> <span data-ttu-id="99d03-249">È possibile usare un pacchetto formattatore JSON per l'editor locale.</span><span class="sxs-lookup"><span data-stu-id="99d03-249">You can use a JSON formatter package for your local editor.</span></span> <span data-ttu-id="99d03-250">In Visual Studio, il documento di hello tooformat, premere **Ctrl + K, Ctrl + D**.</span><span class="sxs-lookup"><span data-stu-id="99d03-250">In Visual Studio, tooformat hello document, press **Ctrl+K, Ctrl+D**.</span></span> <span data-ttu-id="99d03-251">In Visual Studio Code, usare **Alt+Shift+F**.</span><span class="sxs-lookup"><span data-stu-id="99d03-251">In Visual Studio Code, press **Alt+Shift+F**.</span></span> <span data-ttu-id="99d03-252">Se l'editor locale non Formatta documento hello, è possibile utilizzare un [formattatore online](https://www.bing.com/search?q=json+formatter).</span><span class="sxs-lookup"><span data-stu-id="99d03-252">If your local editor doesn't format hello document, you can use an [online formatter](https://www.bing.com/search?q=json+formatter).</span></span>

## <a name="next-steps"></a><span data-ttu-id="99d03-253">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="99d03-253">Next steps</span></span>
* <span data-ttu-id="99d03-254">Per indicazioni sull'architettura della soluzione per le macchine virtuali, vedere [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) (Eseguire una macchina virtuale Windows in Azure) e [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md) (Eseguire una macchina virtuale Linux in Azure).</span><span class="sxs-lookup"><span data-stu-id="99d03-254">For guidance on architecting your solution for virtual machines, see [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) and [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md).</span></span>
* <span data-ttu-id="99d03-255">Per indicazioni sulla configurazione di un account di archiviazione, vedere l'[elenco di controllo di prestazioni e scalabilità per Archiviazione di Azure](../storage/common/storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="99d03-255">For guidance on setting up a storage account, see [Azure Storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>
* <span data-ttu-id="99d03-256">toolearn su come usare un'azienda tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise: governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="99d03-256">toolearn about how an enterprise can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold: Prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

