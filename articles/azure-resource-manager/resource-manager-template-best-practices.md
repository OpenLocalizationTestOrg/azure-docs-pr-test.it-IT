---
title: Procedure consigliate per la creazione di modelli di Resource Manager| Microsoft Docs
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
ms.openlocfilehash: a23301ba88279af3f7bf4d353ae808e9eeb0900d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a><span data-ttu-id="b7981-103">Procedure consigliate per la creazione di modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b7981-103">Best practices for creating Azure Resource Manager templates</span></span>
<span data-ttu-id="b7981-104">Le linee guida seguenti consentono di creare modelli di Azure Resource Manager affidabili e facili da usare;</span><span class="sxs-lookup"><span data-stu-id="b7981-104">These guidelines can help you create Azure Resource Manager templates that are reliable and easy to use.</span></span> <span data-ttu-id="b7981-105">sono quindi da considerare solo come suggerimenti</span><span class="sxs-lookup"><span data-stu-id="b7981-105">The guidelines are only suggestions.</span></span> <span data-ttu-id="b7981-106">e non come requisiti assoluti, salvo diversa indicazione.</span><span class="sxs-lookup"><span data-stu-id="b7981-106">They are not requirements, except where noted.</span></span> <span data-ttu-id="b7981-107">I diversi scenari potrebbero richiedere una variazione rispetto agli approcci o esempi seguenti.</span><span class="sxs-lookup"><span data-stu-id="b7981-107">Your scenario might require a variation of one of the following approaches or examples.</span></span>

## <a name="resource-names"></a><span data-ttu-id="b7981-108">Nomi di risorse</span><span class="sxs-lookup"><span data-stu-id="b7981-108">Resource names</span></span>
<span data-ttu-id="b7981-109">In genere vengono usati tre tipi di nomi di risorse in Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="b7981-109">Generally, you work with three types of resource names in Resource Manager:</span></span>

* <span data-ttu-id="b7981-110">Nomi di risorse che devono essere univoci.</span><span class="sxs-lookup"><span data-stu-id="b7981-110">Resource names that must be unique.</span></span>
* <span data-ttu-id="b7981-111">Nomi di risorse che non devono necessariamente essere univoci, ma che si desidera rendano possibile l'identificazione di una risorsa in base al contesto.</span><span class="sxs-lookup"><span data-stu-id="b7981-111">Resource names that are not required to be unique, but you choose to provide a name that can help you identify a resource based on context.</span></span>
* <span data-ttu-id="b7981-112">Nomi di risorse che possono essere generici.</span><span class="sxs-lookup"><span data-stu-id="b7981-112">Resource names that can be generic.</span></span>

 <span data-ttu-id="b7981-113">Per informazioni sulle restrizioni relative ai nomi di risorse, vedere [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md)(Convenzioni di denominazione consigliate per le risorse di Azure).</span><span class="sxs-lookup"><span data-stu-id="b7981-113">For information about resource name restrictions, see [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md).</span></span>

### <a name="unique-resource-names"></a><span data-ttu-id="b7981-114">Nomi di risorse univoci</span><span class="sxs-lookup"><span data-stu-id="b7981-114">Unique resource names</span></span>
<span data-ttu-id="b7981-115">È necessario fornire un nome univoco per qualsiasi tipo di risorsa con un endpoint di accesso ai dati.</span><span class="sxs-lookup"><span data-stu-id="b7981-115">You must provide a unique resource name for any resource type that has a data access endpoint.</span></span> <span data-ttu-id="b7981-116">Alcuni tipi di risorse comuni che richiedono un nome univoco includono:</span><span class="sxs-lookup"><span data-stu-id="b7981-116">Some common resource types that require a unique name include:</span></span>

* <span data-ttu-id="b7981-117">Archiviazione di Azure<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="b7981-117">Azure Storage<sup>1</sup></span></span> 
* <span data-ttu-id="b7981-118">Funzionalità app Web del servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="b7981-118">Web Apps feature of Azure App Service</span></span>
* <span data-ttu-id="b7981-119">SQL Server</span><span class="sxs-lookup"><span data-stu-id="b7981-119">SQL Server</span></span>
* <span data-ttu-id="b7981-120">Insieme di credenziali chiave Azure</span><span class="sxs-lookup"><span data-stu-id="b7981-120">Azure Key Vault</span></span>
* <span data-ttu-id="b7981-121">Cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="b7981-121">Azure Redis Cache</span></span>
* <span data-ttu-id="b7981-122">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="b7981-122">Azure Batch</span></span>
* <span data-ttu-id="b7981-123">Gestione traffico di Azure</span><span class="sxs-lookup"><span data-stu-id="b7981-123">Azure Traffic Manager</span></span>
* <span data-ttu-id="b7981-124">Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="b7981-124">Azure Search</span></span>
* <span data-ttu-id="b7981-125">HDInsight di Azure</span><span class="sxs-lookup"><span data-stu-id="b7981-125">Azure HDInsight</span></span>

<span data-ttu-id="b7981-126"><sup>1</sup> I nomi di account di archiviazione devono essere formati da lettere minuscole, un massimo di 24 caratteri e non devono includere alcun segno meno.</span><span class="sxs-lookup"><span data-stu-id="b7981-126"><sup>1</sup> Storage account names also must be lowercase, 24 characters or less, and not have any hyphens.</span></span>

<span data-ttu-id="b7981-127">Se si specifica un parametro per un nome di risorsa, è necessario indicare un nome univoco durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b7981-127">If you provide a parameter for a resource name, you must provide a unique name when you deploy the resource.</span></span> <span data-ttu-id="b7981-128">In alternativa, è possibile creare una variabile che usi la funzione [uniqueString()](resource-group-template-functions-string.md#uniquestring) per generare un nome.</span><span class="sxs-lookup"><span data-stu-id="b7981-128">Optionally, you can create a variable that uses the [uniqueString()](resource-group-template-functions-string.md#uniquestring) function to generate a name.</span></span> 

<span data-ttu-id="b7981-129">È spesso opportuno aggiungere un prefisso o un suffisso al risultato di **uniqueString**.</span><span class="sxs-lookup"><span data-stu-id="b7981-129">You also might want to add a prefix or suffix to the **uniqueString** result.</span></span> <span data-ttu-id="b7981-130">La modifica del nome univoco consente di identificare più facilmente il tipo di risorsa in base al nome.</span><span class="sxs-lookup"><span data-stu-id="b7981-130">Modifying the unique name can help you more easily identify the resource type from the name.</span></span> <span data-ttu-id="b7981-131">Ad esempio, è possibile generare un nome univoco per un account di archiviazione usando la variabile seguente:</span><span class="sxs-lookup"><span data-stu-id="b7981-131">For example, you can generate a unique name for a storage account by using the following variable:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a><span data-ttu-id="b7981-132">Nomi di risorse per l'identificazione</span><span class="sxs-lookup"><span data-stu-id="b7981-132">Resource names for identification</span></span>
<span data-ttu-id="b7981-133">Si tratta di risorse cui si desidera attribuire un nome, ma di cui non è necessario garantire l'univocità.</span><span class="sxs-lookup"><span data-stu-id="b7981-133">Some resource types you might want to name, but their names do not have to be unique.</span></span> <span data-ttu-id="b7981-134">Per questi tipi di risorse, è sufficiente indicare un nome che identifichi il contesto e il tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="b7981-134">For these resource types, you can provide a name that identifies both the resource context and the resource type.</span></span> <span data-ttu-id="b7981-135">È opportuno attribuire un nome descrittivo che ne faciliti il riconoscimento in un elenco di risorse.</span><span class="sxs-lookup"><span data-stu-id="b7981-135">Provide a descriptive name that helps you identify the resource in a list of resources.</span></span> <span data-ttu-id="b7981-136">Se è necessario modificare il nome della risorsa durante le distribuzioni, usare un parametro per il nome:</span><span class="sxs-lookup"><span data-stu-id="b7981-136">If you need to use a different resource name for different deployments, you can use a parameter for the name:</span></span>

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "The name of the VM to create."
        }
    }
}
```

<span data-ttu-id="b7981-137">Se non è necessario modificare il nome durante la distribuzione, usare una variabile:</span><span class="sxs-lookup"><span data-stu-id="b7981-137">If you do not need to pass in a name during deployment, you can use a variable:</span></span> 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

<span data-ttu-id="b7981-138">In alternativa si può usare un valore hardcoded:</span><span class="sxs-lookup"><span data-stu-id="b7981-138">You also can use a hard-coded value:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a><span data-ttu-id="b7981-139">Nomi di risorse generici</span><span class="sxs-lookup"><span data-stu-id="b7981-139">Generic resource names</span></span>
<span data-ttu-id="b7981-140">Per i tipi di risorse in gran parte accessibili tramite un'altra risorsa, è possibile usare un nome generico che sia hardcoded nel modello.</span><span class="sxs-lookup"><span data-stu-id="b7981-140">For resource types that you mostly access through a different resource, you can use a generic name that is hard-coded in the template.</span></span> <span data-ttu-id="b7981-141">Ad esempio, è possibile impostare un nome generico e standard per le regole del firewall in SQL server:</span><span class="sxs-lookup"><span data-stu-id="b7981-141">For example, you can set a standard, generic name for firewall rules on a SQL server:</span></span>

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a><span data-ttu-id="b7981-142">parameters</span><span class="sxs-lookup"><span data-stu-id="b7981-142">Parameters</span></span>
<span data-ttu-id="b7981-143">Le informazioni seguenti possono essere utili quando si usano parametri:</span><span class="sxs-lookup"><span data-stu-id="b7981-143">The following information can be helpful when you work with parameters:</span></span>

* <span data-ttu-id="b7981-144">Ridurre al minimo l'uso di parametri.</span><span class="sxs-lookup"><span data-stu-id="b7981-144">Minimize your use of parameters.</span></span> <span data-ttu-id="b7981-145">Se possibile, usare una variabile o un valore letterale.</span><span class="sxs-lookup"><span data-stu-id="b7981-145">Whenever possible, use a variable or a literal value.</span></span> <span data-ttu-id="b7981-146">Specificare parametri solo per questi scenari:</span><span class="sxs-lookup"><span data-stu-id="b7981-146">Use parameters only for these scenarios:</span></span>
   
   * <span data-ttu-id="b7981-147">Impostazioni da variare in base all'ambiente (ad esempio SKU, dimensioni o capacità).</span><span class="sxs-lookup"><span data-stu-id="b7981-147">Settings that you want to use variations of according to environment (SKU, size, capacity).</span></span>
   * <span data-ttu-id="b7981-148">Nomi di risorse da specificare per facilitare l'identificazione.</span><span class="sxs-lookup"><span data-stu-id="b7981-148">Resource names that you want to specify for easy identification.</span></span>
   * <span data-ttu-id="b7981-149">Valori usati spesso per completare altre attività (ad esempio nome utente amministratore).</span><span class="sxs-lookup"><span data-stu-id="b7981-149">Values that you use frequently to complete other tasks (such as an admin user name).</span></span>
   * <span data-ttu-id="b7981-150">Segreti (ad esempio password).</span><span class="sxs-lookup"><span data-stu-id="b7981-150">Secrets (such as passwords).</span></span>
   * <span data-ttu-id="b7981-151">Il numero o la matrice di valori da usare durante la creazione di più istanze di un tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="b7981-151">The number or array of values to use when you create multiple instances of a resource type.</span></span>
* <span data-ttu-id="b7981-152">Usare la notazione Camel per i nomi dei parametri.</span><span class="sxs-lookup"><span data-stu-id="b7981-152">Use camel case for parameter names.</span></span>
* <span data-ttu-id="b7981-153">Indicare una descrizione nei metadati per ogni parametro:</span><span class="sxs-lookup"><span data-stu-id="b7981-153">Provide a description of every parameter in the metadata:</span></span>

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "The type of the new storage account created to store the VM disks."
           }
       }
   }
   ```

* <span data-ttu-id="b7981-154">Definire i valori predefiniti per i parametri (ad eccezione delle password e delle chiavi SSH):</span><span class="sxs-lookup"><span data-stu-id="b7981-154">Define default values for parameters (except for passwords and SSH keys):</span></span>
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "The type of the new storage account created to store the VM disks."
            }
        }
   }
   ```

* <span data-ttu-id="b7981-155">Usare **SecureString** per tutte le password e i segreti:</span><span class="sxs-lookup"><span data-stu-id="b7981-155">Use **SecureString** for all passwords and secrets:</span></span> 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "The value of the secret to store in the vault."
           }
       }
   }
   ```

* <span data-ttu-id="b7981-156">Quando possibile, evitare di usare un parametro per specificare la posizione.</span><span class="sxs-lookup"><span data-stu-id="b7981-156">Whenever possible, don't use a parameter to specify location.</span></span> <span data-ttu-id="b7981-157">Usare invece la proprietà **location** del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b7981-157">Instead, use the **location** property of the resource group.</span></span> <span data-ttu-id="b7981-158">Usando l'espressione **resourceGroup().location** per tutte le risorse, le risorse nel modello verranno distribuite nella stessa posizione del gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="b7981-158">By using the **resourceGroup().location** expression for all your resources, resources in the template are deployed in the same location as the resource group:</span></span>
   
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
   
   <span data-ttu-id="b7981-159">Se un tipo di risorsa è supportato solo in un numero limitato di posizioni, provare a specificare una posizione valida direttamente nel modello.</span><span class="sxs-lookup"><span data-stu-id="b7981-159">If a resource type is supported in only a limited number of locations, you might want to specify a valid location directly in the template.</span></span> <span data-ttu-id="b7981-160">Se è necessario usare un parametro **location**, condividere per quanto possibile il relativo valore con le risorse che potrebbero essere nella stessa posizione.</span><span class="sxs-lookup"><span data-stu-id="b7981-160">If you must use a **location** parameter, share that parameter value as much as possible with resources that are likely to be in the same location.</span></span> <span data-ttu-id="b7981-161">Questo approccio permette di ridurre al minimo il numero di volte in cui gli utenti devono dare informazioni sulla posizione.</span><span class="sxs-lookup"><span data-stu-id="b7981-161">This minimizes the number of times users are asked to provide location information.</span></span>
* <span data-ttu-id="b7981-162">Evitare di usare un parametro o una variabile per la versione dell'API per un tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="b7981-162">Avoid using a parameter or variable for the API version for a resource type.</span></span> <span data-ttu-id="b7981-163">I valori e le proprietà delle risorse possono variare in base al numero di versione.</span><span class="sxs-lookup"><span data-stu-id="b7981-163">Resource properties and values can vary by version number.</span></span> <span data-ttu-id="b7981-164">Quando la versione dell'API è impostata su un parametro o una variabile, IntelliSense negli editor di codice non può determinare lo schema corretto.</span><span class="sxs-lookup"><span data-stu-id="b7981-164">IntelliSense in a code editor cannot determine the correct schema when the API version is set to a parameter or variable.</span></span> <span data-ttu-id="b7981-165">Impostare invece la versione dell'API come hardcoded nel modello.</span><span class="sxs-lookup"><span data-stu-id="b7981-165">Instead, hard-code the API version in the template.</span></span>

## <a name="variables"></a><span data-ttu-id="b7981-166">variables</span><span class="sxs-lookup"><span data-stu-id="b7981-166">Variables</span></span>
<span data-ttu-id="b7981-167">Le informazioni seguenti possono essere utili quando si usano variabili:</span><span class="sxs-lookup"><span data-stu-id="b7981-167">The following information can be helpful when you work with variables:</span></span>

* <span data-ttu-id="b7981-168">Usare le variabili per i valori da usare più volte in un modello.</span><span class="sxs-lookup"><span data-stu-id="b7981-168">Use variables for values that you need to use more than once in a template.</span></span> <span data-ttu-id="b7981-169">Se un valore viene usato una sola volta, un valore hardcoded facilita la lettura del modello.</span><span class="sxs-lookup"><span data-stu-id="b7981-169">If a value is used only once, a hard-coded value makes your template easier to read.</span></span>
* <span data-ttu-id="b7981-170">Non è possibile usare la funzione [reference](resource-group-template-functions-resource.md#reference) nella sezione **variables** del modello.</span><span class="sxs-lookup"><span data-stu-id="b7981-170">You cannot use the [reference](resource-group-template-functions-resource.md#reference) function in the **variables** section of the template.</span></span> <span data-ttu-id="b7981-171">La funzione **reference** deriva il proprio valore dallo stato di runtime della risorsa,</span><span class="sxs-lookup"><span data-stu-id="b7981-171">The **reference** function derives its value from the resource's runtime state.</span></span> <span data-ttu-id="b7981-172">ma le variabili vengono risolte durante l'analisi iniziale del modello.</span><span class="sxs-lookup"><span data-stu-id="b7981-172">However, variables are resolved during the initial parsing of the template.</span></span> <span data-ttu-id="b7981-173">Costruire invece valori che richiedono la funzione **reference** direttamente nella sezione **resources** o **outputs** del modello.</span><span class="sxs-lookup"><span data-stu-id="b7981-173">Construct values that need the **reference** function directly in the **resources** or **outputs** section of the template.</span></span>
* <span data-ttu-id="b7981-174">Includere le variabili per i nomi di risorse che devono essere univoci, come illustrato in [Nomi di risorse](#resource-names).</span><span class="sxs-lookup"><span data-stu-id="b7981-174">Include variables for resource names that must be unique, as described in [Resource names](#resource-names).</span></span>
* <span data-ttu-id="b7981-175">È possibile raggruppare le variabili in oggetti complessi.</span><span class="sxs-lookup"><span data-stu-id="b7981-175">You can group variables into complex objects.</span></span> <span data-ttu-id="b7981-176">È possibile fare riferimento a un valore da un oggetto complesso nel formato **variable.subentry**.</span><span class="sxs-lookup"><span data-stu-id="b7981-176">Use the **variable.subentry** format to reference a value from a complex object.</span></span> <span data-ttu-id="b7981-177">Il raggruppamento delle variabili consente di tenere traccia delle variabili correlate</span><span class="sxs-lookup"><span data-stu-id="b7981-177">Grouping variables can help you track related variables.</span></span> <span data-ttu-id="b7981-178">e migliora la leggibilità del modello.</span><span class="sxs-lookup"><span data-stu-id="b7981-178">It also improves readability of the template.</span></span> <span data-ttu-id="b7981-179">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b7981-179">Here's an example:</span></span>
   
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
   > <span data-ttu-id="b7981-180">Un oggetto complesso non può contenere un'espressione che fa riferimento a un valore da un oggetto complesso.</span><span class="sxs-lookup"><span data-stu-id="b7981-180">A complex object cannot contain an expression that references a value from a complex object.</span></span> <span data-ttu-id="b7981-181">A questo scopo, definire una variabile separata.</span><span class="sxs-lookup"><span data-stu-id="b7981-181">Define a separate variable for this purpose.</span></span>
   > 
   > 
   
     <span data-ttu-id="b7981-182">Per esempi avanzati di uso di oggetti complessi come variabili, vedere [Condividere lo stato tra modelli di Azure Resource Manager](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="b7981-182">For advanced examples of using complex objects as variables, see [Share state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="resources"></a><span data-ttu-id="b7981-183">Risorse</span><span class="sxs-lookup"><span data-stu-id="b7981-183">Resources</span></span>
<span data-ttu-id="b7981-184">Le informazioni seguenti possono essere utili quando si usano le risorse:</span><span class="sxs-lookup"><span data-stu-id="b7981-184">The following information can be helpful when you work with resources:</span></span>

* <span data-ttu-id="b7981-185">Specificare **comments** per ogni risorsa nel modello per consentire ad altri collaboratori di comprendere lo scopo della risorsa:</span><span class="sxs-lookup"><span data-stu-id="b7981-185">To help other contributors understand the purpose of the resource, specify **comments** for each resource in the template:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used to store the VM disks.",
         ...
     }
   ]
   ```

* <span data-ttu-id="b7981-186">È possibile usare i tag per aggiungere metadati alle risorse.</span><span class="sxs-lookup"><span data-stu-id="b7981-186">You can use tags to add metadata to resources.</span></span> <span data-ttu-id="b7981-187">Usare i metadati per aumentare le informazioni sulle risorse.</span><span class="sxs-lookup"><span data-stu-id="b7981-187">Use metadata to add information about your resources.</span></span> <span data-ttu-id="b7981-188">Ad esempio, è possibile aggiungere metadati per registrare i dettagli di fatturazione di una risorsa.</span><span class="sxs-lookup"><span data-stu-id="b7981-188">For example, you can add metadata to record billing details for a resource.</span></span> <span data-ttu-id="b7981-189">Per altre informazioni, vedere [Uso dei tag per organizzare le risorse di Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="b7981-189">For more information, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span></span>
* <span data-ttu-id="b7981-190">Se si usa un *endpoint pubblico* nel modello, come ad esempio un endpoint pubblico di archiviazione BLOB di Azure, *non impostare come hardcoded* lo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="b7981-190">If you use a *public endpoint* in your template (such as an Azure Blob storage public endpoint), *do not hard-code* the namespace.</span></span> <span data-ttu-id="b7981-191">Usare la funzione **reference** per recuperare lo spazio dei nomi in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="b7981-191">Use the **reference** function to dynamically retrieve the namespace.</span></span> <span data-ttu-id="b7981-192">Questo approccio consente di distribuire il modello in ambienti diversi dello spazio dei nomi pubblico senza dover modificare manualmente l'endpoint nel modello.</span><span class="sxs-lookup"><span data-stu-id="b7981-192">You can use this approach to deploy the template to different public namespace environments without manually changing the endpoint in the template.</span></span> <span data-ttu-id="b7981-193">Impostare la versione dell'API sulla stessa versione in uso per l'account di archiviazione nel modello:</span><span class="sxs-lookup"><span data-stu-id="b7981-193">Set the API version to the same version that you are using for the storage account in your template:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="b7981-194">Se l'account di archiviazione viene distribuito nello stesso modello creato, non è necessario specificare lo spazio dei nomi del provider quando si fa riferimento alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="b7981-194">If the storage account is deployed in the same template that you are creating, you do not need to specify the provider namespace when you reference the resource.</span></span> <span data-ttu-id="b7981-195">La sintassi semplificata è:</span><span class="sxs-lookup"><span data-stu-id="b7981-195">This is the simplified syntax:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="b7981-196">Se nel modello sono presenti altri valori configurati per usare uno spazio dei nomi pubblico, modificarli in modo da riflettere la stessa funzione **reference**.</span><span class="sxs-lookup"><span data-stu-id="b7981-196">If you have other values in your template that are configured to use a public namespace, change these values to reflect the same **reference** function.</span></span> <span data-ttu-id="b7981-197">Ad esempio, è possibile impostare la proprietà **storageUri** del profilo di diagnostica della macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="b7981-197">For example, you can set the **storageUri** property of the virtual machine diagnostics profile:</span></span>
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   <span data-ttu-id="b7981-198">È anche possibile fare riferimento a un account di archiviazione in un gruppo di risorse diverso:</span><span class="sxs-lookup"><span data-stu-id="b7981-198">You also can reference an existing storage account that is in a different resource group:</span></span>

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* <span data-ttu-id="b7981-199">Assegnare indirizzi IP pubblici a una macchina virtuale solo se richiesto per un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b7981-199">Assign public IP addresses to a virtual machine only when an application requires it.</span></span> <span data-ttu-id="b7981-200">Per connettersi a una macchina virtuale (VM) per il debug o per la gestione o a scopi amministrativi, usare le regole NAT in ingresso, un gateway di rete virtuale o un jumpbox.</span><span class="sxs-lookup"><span data-stu-id="b7981-200">To connect to a virtual machine (VM) for debugging, or for management or administrative purposes, use inbound NAT rules, a virtual network gateway, or a jumpbox.</span></span>
   
     <span data-ttu-id="b7981-201">Per altre informazioni sulla connessione alle macchine virtuali, vedere:</span><span class="sxs-lookup"><span data-stu-id="b7981-201">For more information about connecting to virtual machines, see:</span></span>
   
   * [<span data-ttu-id="b7981-202">Eseguire macchine virtuali per un'architettura a più livelli in Azure</span><span class="sxs-lookup"><span data-stu-id="b7981-202">Run VMs for an N-tier architecture in Azure</span></span>](../guidance/guidance-compute-n-tier-vm.md)
   * [<span data-ttu-id="b7981-203">Configurare l'accesso WinRM per le macchine virtuali in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b7981-203">Set up WinRM access for VMs in Azure Resource Manager</span></span>](../virtual-machines/windows/winrm.md)
   * [<span data-ttu-id="b7981-204">Consentire l'accesso esterno alla macchina virtuale tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b7981-204">Allow external access to your VM by using the Azure portal</span></span>](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [<span data-ttu-id="b7981-205">Consentire l'accesso esterno alla macchina virtuale tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7981-205">Allow external access to your VM by using PowerShell</span></span>](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [<span data-ttu-id="b7981-206">Consentire l'accesso esterno alla macchina virtuale Linux tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b7981-206">Allow external access to your Linux VM by using Azure CLI</span></span>](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* <span data-ttu-id="b7981-207">La proprietà **domainNameLabel** deve essere univoca per gli indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="b7981-207">The **domainNameLabel** property for public IP addresses must be unique.</span></span> <span data-ttu-id="b7981-208">Il valore **domainNameLabel** deve avere una lunghezza compresa tra 3 e 63 caratteri e seguire le regole specificate dall'espressione regolare seguente: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span><span class="sxs-lookup"><span data-stu-id="b7981-208">The **domainNameLabel** value must be between 3 and 63 characters long, and follow the rules specified by this regular expression: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span></span> <span data-ttu-id="b7981-209">Dato che la funzione **uniqueString** genera una stringa lunga 13 caratteri, il parametro **dnsPrefixString** non deve superare 50 caratteri:</span><span class="sxs-lookup"><span data-stu-id="b7981-209">Because the **uniqueString** function generates a string that is 13 characters long, the **dnsPrefixString** parameter is limited to 50 characters:</span></span>

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "The DNS label for the public IP address. It must be lowercase. It should match the following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* <span data-ttu-id="b7981-210">Quando si aggiunge una password a un'estensione di script personalizzato, usare la proprietà **commandToExecute** nella proprietà **protectedSettings**:</span><span class="sxs-lookup"><span data-stu-id="b7981-210">When you add a password to a custom script extension, use the **commandToExecute** property in the **protectedSettings** property:</span></span>
   
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
   > <span data-ttu-id="b7981-211">Per garantire che i segreti passati come parametri a macchine virtuali ed estensioni siano crittografati, usare la proprietà **protectedSettings** delle estensioni pertinenti.</span><span class="sxs-lookup"><span data-stu-id="b7981-211">To ensure that secrets are encrypted when they are passed as parameters to VMs and extensions, use the **protectedSettings** property of the relevant extensions.</span></span>
   > 
   > 

## <a name="outputs"></a><span data-ttu-id="b7981-212">outputs</span><span class="sxs-lookup"><span data-stu-id="b7981-212">Outputs</span></span>
<span data-ttu-id="b7981-213">Se viene usato un modello per creare indirizzi IP pubblici, deve includere una sezione **outputs** che restituisca i dettagli dell'indirizzo IP e del nome di dominio completo (FQDN).</span><span class="sxs-lookup"><span data-stu-id="b7981-213">If you use a template to create public IP addresses, include an **outputs** section that returns details of the IP address and the fully qualified domain name (FQDN).</span></span> <span data-ttu-id="b7981-214">Questi valori di output consentiranno di recuperare facilmente i dettagli sugli indirizzi IP pubblici e sugli FQDN dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b7981-214">You can use output values to easily retrieve details about public IP addresses and FQDNs after deployment.</span></span> <span data-ttu-id="b7981-215">Quando si fa riferimento alla risorsa, usare la versione dell'API impiegata per crearla:</span><span class="sxs-lookup"><span data-stu-id="b7981-215">When you reference the resource, use the API version that you used to create it:</span></span> 

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

## <a name="single-template-vs-nested-templates"></a><span data-ttu-id="b7981-216">Modello singolo o modelli annidati</span><span class="sxs-lookup"><span data-stu-id="b7981-216">Single template vs. nested templates</span></span>
<span data-ttu-id="b7981-217">Per distribuire la soluzione, è possibile usare un modello singolo o un modello principale con più modelli annidati.</span><span class="sxs-lookup"><span data-stu-id="b7981-217">To deploy your solution, you can use either a single template or a main template with multiple nested templates.</span></span> <span data-ttu-id="b7981-218">I modelli annidati sono comuni per scenari più avanzati.</span><span class="sxs-lookup"><span data-stu-id="b7981-218">Nested templates are common for more advanced scenarios.</span></span> <span data-ttu-id="b7981-219">L'uso di un modello annidato presenta i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7981-219">Using a nested template gives you the following advantages:</span></span>

* <span data-ttu-id="b7981-220">È possibile scomporre la soluzione in componenti di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b7981-220">You can break down a solution into targeted components.</span></span>
* <span data-ttu-id="b7981-221">È possibile riusare i modelli annidati con modelli principali diversi.</span><span class="sxs-lookup"><span data-stu-id="b7981-221">You can reuse nested templates with different main templates.</span></span>

<span data-ttu-id="b7981-222">Quando si decide di scomporre la progettazione del modello in più modelli annidati, le linee guida seguenti ne consentono la standardizzazione.</span><span class="sxs-lookup"><span data-stu-id="b7981-222">If you choose to use nested templates, the following guidelines can help you standardize your template design.</span></span> <span data-ttu-id="b7981-223">Queste linee guida si basano sui [criteri di progettazione per modelli di Azure Resource Manager](best-practices-resource-manager-design-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b7981-223">These guidelines are based on [patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span></span> <span data-ttu-id="b7981-224">La progettazione consigliata include i modelli seguenti:</span><span class="sxs-lookup"><span data-stu-id="b7981-224">We recommend a design that has the following templates:</span></span>

* <span data-ttu-id="b7981-225">**Modello principale** (azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="b7981-225">**Main template** (azuredeploy.json).</span></span> <span data-ttu-id="b7981-226">Da usare per i parametri di input.</span><span class="sxs-lookup"><span data-stu-id="b7981-226">Use for the input parameters.</span></span>
* <span data-ttu-id="b7981-227">**Modello di risorse condivise**.</span><span class="sxs-lookup"><span data-stu-id="b7981-227">**Shared resources template**.</span></span> <span data-ttu-id="b7981-228">Da usare per distribuire le risorse condivise da tutte le altre risorse (ad esempio, rete virtuale e set di disponibilità).</span><span class="sxs-lookup"><span data-stu-id="b7981-228">Use to deploy shared resources that all other resources use (for example, virtual network and availability sets).</span></span> <span data-ttu-id="b7981-229">L'espressione **dependsOn** deve essere usata per assicurarsi che questo modello venga distribuito prima degli altri.</span><span class="sxs-lookup"><span data-stu-id="b7981-229">Use the **dependsOn** expression to ensure that this template is deployed before other templates.</span></span>
* <span data-ttu-id="b7981-230">**Modello di risorse facoltative**.</span><span class="sxs-lookup"><span data-stu-id="b7981-230">**Optional resources template**.</span></span> <span data-ttu-id="b7981-231">Da usare per distribuire risorse in modo condizionale in base a un parametro, ad esempio un jumpbox.</span><span class="sxs-lookup"><span data-stu-id="b7981-231">Use to conditionally deploy resources based on a parameter (for example, a jumpbox).</span></span>
* <span data-ttu-id="b7981-232">**Modello di risorse membro**.</span><span class="sxs-lookup"><span data-stu-id="b7981-232">**Member resources template**.</span></span> <span data-ttu-id="b7981-233">Ogni tipo di istanza all'interno di un livello di applicazione prevede una propria configurazione.</span><span class="sxs-lookup"><span data-stu-id="b7981-233">Each instance type within an application tier has its own configuration.</span></span> <span data-ttu-id="b7981-234">All'interno di un livello, è possibile definire diversi tipi di istanza.</span><span class="sxs-lookup"><span data-stu-id="b7981-234">Within a tier, you can define different instance types.</span></span> <span data-ttu-id="b7981-235">Ad esempio, la prima istanza crea un cluster mentre le altre vengono aggiunte al cluster esistente. Ogni tipo di istanza avrà un proprio modello di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b7981-235">(For example, the first instance creates a cluster, and additional instances are added to the existing cluster.) Each instance type has its own deployment template.</span></span>
* <span data-ttu-id="b7981-236">**Script**.</span><span class="sxs-lookup"><span data-stu-id="b7981-236">**Scripts**.</span></span> <span data-ttu-id="b7981-237">Per ogni tipo di istanza sono applicabili script ampiamente riutilizzabili, come ad esempio quelli di inizializzazione e formattazione di dischi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="b7981-237">Widely reusable scripts are applicable for each instance type (for example, initialize and format additional disks).</span></span> <span data-ttu-id="b7981-238">Gli script personalizzati vengono creati per scopi di personalizzazione specifici e variano in base al tipo di istanza.</span><span class="sxs-lookup"><span data-stu-id="b7981-238">Custom scripts that you create for a specific customization purpose are different, based on the instance type.</span></span>

![Modello annidato](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

<span data-ttu-id="b7981-240">Per altre informazioni, vedere [Uso di modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b7981-240">For more information, see [Use linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="conditionally-link-to-nested-templates"></a><span data-ttu-id="b7981-241">Collegarsi in modo condizionale al modello annidato</span><span class="sxs-lookup"><span data-stu-id="b7981-241">Conditionally link to nested templates</span></span>
<span data-ttu-id="b7981-242">È possibile collegarsi in modo condizionale ai modelli annidati usando un parametro</span><span class="sxs-lookup"><span data-stu-id="b7981-242">You can use a parameter to conditionally link to nested templates.</span></span> <span data-ttu-id="b7981-243">che diventa parte dell'URI per il modello:</span><span class="sxs-lookup"><span data-stu-id="b7981-243">The parameter becomes part of the URI for the template:</span></span>

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

## <a name="template-format"></a><span data-ttu-id="b7981-244">Formato del modello</span><span class="sxs-lookup"><span data-stu-id="b7981-244">Template format</span></span>
<span data-ttu-id="b7981-245">È consigliabile passare il modello tramite un validator JSON.</span><span class="sxs-lookup"><span data-stu-id="b7981-245">It's a good practice to pass your template through a JSON validator.</span></span> <span data-ttu-id="b7981-246">Un validator può aiutare a rimuovere virgole, parentesi e parentesi quadre estranee che potrebbero causare un errore durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b7981-246">A validator can help you remove extraneous commas, parentheses, and brackets that might cause an error during deployment.</span></span> <span data-ttu-id="b7981-247">Provare [JSONlint](http://jsonlint.com/) o un pacchetto linter per l'ambiente di modifica preferito (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="b7981-247">Try [JSONLint](http://jsonlint.com/) or a linter package for your favorite editing environment (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span></span>

<span data-ttu-id="b7981-248">È anche consigliabile formattare il codice JSON per una migliore leggibilità.</span><span class="sxs-lookup"><span data-stu-id="b7981-248">It's also a good idea to format your JSON for better readability.</span></span> <span data-ttu-id="b7981-249">È possibile usare un pacchetto formattatore JSON per l'editor locale.</span><span class="sxs-lookup"><span data-stu-id="b7981-249">You can use a JSON formatter package for your local editor.</span></span> <span data-ttu-id="b7981-250">In Visual Studio formattare il documento con **Ctrl+K, Ctrl+D**.</span><span class="sxs-lookup"><span data-stu-id="b7981-250">In Visual Studio, to format the document, press **Ctrl+K, Ctrl+D**.</span></span> <span data-ttu-id="b7981-251">In Visual Studio Code, usare **Alt+Shift+F**.</span><span class="sxs-lookup"><span data-stu-id="b7981-251">In Visual Studio Code, press **Alt+Shift+F**.</span></span> <span data-ttu-id="b7981-252">Se l'editor locale non formatta il documento, è possibile usare un [formattatore online](https://www.bing.com/search?q=json+formatter).</span><span class="sxs-lookup"><span data-stu-id="b7981-252">If your local editor doesn't format the document, you can use an [online formatter](https://www.bing.com/search?q=json+formatter).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7981-253">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b7981-253">Next steps</span></span>
* <span data-ttu-id="b7981-254">Per indicazioni sull'architettura della soluzione per le macchine virtuali, vedere [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) (Eseguire una macchina virtuale Windows in Azure) e [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md) (Eseguire una macchina virtuale Linux in Azure).</span><span class="sxs-lookup"><span data-stu-id="b7981-254">For guidance on architecting your solution for virtual machines, see [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) and [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md).</span></span>
* <span data-ttu-id="b7981-255">Per indicazioni sulla configurazione di un account di archiviazione, vedere l'[elenco di controllo di prestazioni e scalabilità per Archiviazione di Azure](../storage/common/storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="b7981-255">For guidance on setting up a storage account, see [Azure Storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>
* <span data-ttu-id="b7981-256">Per indicazioni su come le aziende possono usare Resource Manager per gestire efficacemente le sottoscrizioni, vedere [Scaffold Azure enterprise: governance prescrittiva per le sottoscrizioni](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="b7981-256">To learn about how an enterprise can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold: Prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

