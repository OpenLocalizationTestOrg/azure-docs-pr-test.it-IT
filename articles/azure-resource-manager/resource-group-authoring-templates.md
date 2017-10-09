---
title: Gestione risorse aaaAzure struttura di modello e la sintassi | Documenti Microsoft
description: "Descrive la struttura hello e le proprietà dei modelli di gestione risorse di Azure utilizzando la sintassi dichiarativa JSON."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/14/2017
ms.author: tomfitz
ms.openlocfilehash: b0709852f8777c91cc1704d6bca16257a017d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="8f75c-103">Comprendere la struttura di hello e sintassi dei modelli di gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="8f75c-103">Understand hello structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="8f75c-104">Questo argomento descrive la struttura hello di un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f75c-104">This topic describes hello structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="8f75c-105">Presenta diverse sezioni di hello di un modello e hello proprietà che è disponibili in quelle sezioni.</span><span class="sxs-lookup"><span data-stu-id="8f75c-105">It presents hello different sections of a template and hello properties that are available in those sections.</span></span> <span data-ttu-id="8f75c-106">modello Hello è costituito da JSON e le espressioni che è possibile utilizzare valori tooconstruct per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="8f75c-106">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="8f75c-107">Per un'esercitazione dettagliata sulla creazione di un modello, vedere [Creare il primo modello di Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="8f75c-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

## <a name="template-format"></a><span data-ttu-id="8f75c-108">Formato del modello</span><span class="sxs-lookup"><span data-stu-id="8f75c-108">Template format</span></span>
<span data-ttu-id="8f75c-109">Nella struttura più semplice, un modello contiene hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="8f75c-109">In its simplest structure, a template contains hello following elements:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| <span data-ttu-id="8f75c-110">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="8f75c-110">Element name</span></span> | <span data-ttu-id="8f75c-111">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8f75c-111">Required</span></span> | <span data-ttu-id="8f75c-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8f75c-112">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8f75c-113">$schema</span><span class="sxs-lookup"><span data-stu-id="8f75c-113">$schema</span></span> |<span data-ttu-id="8f75c-114">Sì</span><span class="sxs-lookup"><span data-stu-id="8f75c-114">Yes</span></span> |<span data-ttu-id="8f75c-115">Percorso del file di schema hello JSON che descrive una versione di hello hello della lingua del modello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-115">Location of hello JSON schema file that describes hello version of hello template language.</span></span> <span data-ttu-id="8f75c-116">Utilizzare l'URL di hello illustrato nell'esempio sopra riportato hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-116">Use hello URL shown in hello preceding example.</span></span> |
| <span data-ttu-id="8f75c-117">contentVersion</span><span class="sxs-lookup"><span data-stu-id="8f75c-117">contentVersion</span></span> |<span data-ttu-id="8f75c-118">Sì</span><span class="sxs-lookup"><span data-stu-id="8f75c-118">Yes</span></span> |<span data-ttu-id="8f75c-119">Versione del modello di hello (ad esempio, 1.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="8f75c-119">Version of hello template (such as 1.0.0.0).</span></span> <span data-ttu-id="8f75c-120">Questo elemento accetta tutti i valori.</span><span class="sxs-lookup"><span data-stu-id="8f75c-120">You can provide any value for this element.</span></span> <span data-ttu-id="8f75c-121">Durante la distribuzione di risorse utilizzando il modello di hello, questo valore può essere utilizzato toomake che viene utilizzato il modello di destra hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-121">When deploying resources using hello template, this value can be used toomake sure that hello right template is being used.</span></span> |
| <span data-ttu-id="8f75c-122">parameters</span><span class="sxs-lookup"><span data-stu-id="8f75c-122">parameters</span></span> |<span data-ttu-id="8f75c-123">No</span><span class="sxs-lookup"><span data-stu-id="8f75c-123">No</span></span> |<span data-ttu-id="8f75c-124">I valori forniti durante la distribuzione è eseguita la distribuzione di risorse toocustomize.</span><span class="sxs-lookup"><span data-stu-id="8f75c-124">Values that are provided when deployment is executed toocustomize resource deployment.</span></span> |
| <span data-ttu-id="8f75c-125">variables</span><span class="sxs-lookup"><span data-stu-id="8f75c-125">variables</span></span> |<span data-ttu-id="8f75c-126">No</span><span class="sxs-lookup"><span data-stu-id="8f75c-126">No</span></span> |<span data-ttu-id="8f75c-127">Valori utilizzati come frammenti JSON in espressioni di linguaggio modello toosimplify modello hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-127">Values that are used as JSON fragments in hello template toosimplify template language expressions.</span></span> |
| <span data-ttu-id="8f75c-128">resources</span><span class="sxs-lookup"><span data-stu-id="8f75c-128">resources</span></span> |<span data-ttu-id="8f75c-129">Sì</span><span class="sxs-lookup"><span data-stu-id="8f75c-129">Yes</span></span> |<span data-ttu-id="8f75c-130">Tipi di risorse che vengono distribuite o aggiornate in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8f75c-130">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="8f75c-131">outputs</span><span class="sxs-lookup"><span data-stu-id="8f75c-131">outputs</span></span> |<span data-ttu-id="8f75c-132">No</span><span class="sxs-lookup"><span data-stu-id="8f75c-132">No</span></span> |<span data-ttu-id="8f75c-133">Valori restituiti dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="8f75c-133">Values that are returned after deployment.</span></span> |

<span data-ttu-id="8f75c-134">Ogni elemento contiene proprietà che è possibile impostare.</span><span class="sxs-lookup"><span data-stu-id="8f75c-134">Each element contains properties you can set.</span></span> <span data-ttu-id="8f75c-135">Hello di esempio seguente contiene una sintassi completa di hello per un modello:</span><span class="sxs-lookup"><span data-stu-id="8f75c-135">hello following example contains hello full syntax for a template:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  
        "<parameter-name>" : {
            "type" : "<type-of-parameter-value>",
            "defaultValue": "<default-value-of-parameter>",
            "allowedValues": [ "<array-of-allowed-values>" ],
            "minValue": <minimum-value-for-int>,
            "maxValue": <maximum-value-for-int>,
            "minLength": <minimum-length-for-string-or-array>,
            "maxLength": <maximum-length-for-string-or-array-parameters>,
            "metadata": {
                "description": "<description-of-hello parameter>" 
            }
        }
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "condition": "<boolean-value-whether-to-deploy>",
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": {
              "<tag-name1>": "<tag-value1>",
              "<tag-name2>": "<tag-value2>"
          },
          "comments": "<your-reference-notes>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>",
              "mode": "<serial-or-parallel>",
              "batchSize": "<number-to-deploy-serially>"
          },
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": {
              "<settings-for-the-resource>",
              "copy": [
                  {
                      "name": ,
                      "count": ,
                      "input": {}
                  }
              ]
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

<span data-ttu-id="8f75c-136">Verranno esaminati sezioni hello del modello di hello in dettaglio più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="8f75c-136">We examine hello sections of hello template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="8f75c-137">Espressioni e funzioni</span><span class="sxs-lookup"><span data-stu-id="8f75c-137">Expressions and functions</span></span>
<span data-ttu-id="8f75c-138">sintassi di base del modello di hello Hello è JSON.</span><span class="sxs-lookup"><span data-stu-id="8f75c-138">hello basic syntax of hello template is JSON.</span></span> <span data-ttu-id="8f75c-139">Tuttavia, espressioni e funzioni estendono hello JSON i valori disponibili nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-139">However, expressions and functions extend hello JSON values available within hello template.</span></span>  <span data-ttu-id="8f75c-140">Le espressioni sono scritte in valori letterali stringa JSON il cui primo e ultimo carattere sono tra parentesi quadre hello: `[` e `]`, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="8f75c-140">Expressions are written within JSON string literals whose first and last characters are hello brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="8f75c-141">il valore di Hello dell'espressione hello viene valutato quando viene distribuito il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-141">hello value of hello expression is evaluated when hello template is deployed.</span></span> <span data-ttu-id="8f75c-142">Durante la scrittura di un valore letterale stringa, il risultato di hello della valutazione di espressione hello può essere di tipo JSON diverso, ad esempio una matrice o un numero intero, a seconda espressione effettiva hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-142">While written as a string literal, hello result of evaluating hello expression can be of a different JSON type, such as an array or integer, depending on hello actual expression.</span></span>  <span data-ttu-id="8f75c-143">una stringa letterale iniziare con una parentesi quadra toohave `[`, ma non viene interpretato come un'espressione, aggiungere una stringa di hello toostart tra parentesi quadre aggiuntive con `[[`.</span><span class="sxs-lookup"><span data-stu-id="8f75c-143">toohave a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket toostart hello string with `[[`.</span></span>

<span data-ttu-id="8f75c-144">In genere, si usano espressioni con operazioni tooperform funzioni per la configurazione di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-144">Typically, you use expressions with functions tooperform operations for configuring hello deployment.</span></span> <span data-ttu-id="8f75c-145">Proprio come in JavaScript, le chiamate di funzione sono formattate come `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="8f75c-145">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="8f75c-146">Fare riferimento alle proprietà utilizzando gli operatori di hello punto e [index].</span><span class="sxs-lookup"><span data-stu-id="8f75c-146">You reference properties by using hello dot and [index] operators.</span></span>

<span data-ttu-id="8f75c-147">Hello di esempio seguente viene illustrato come toouse diverse funzioni durante la costruzione di valori:</span><span class="sxs-lookup"><span data-stu-id="8f75c-147">hello following example shows how toouse several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="8f75c-148">Per hello l'elenco completo delle funzioni di modello, vedere [funzioni di modello di gestione risorse di Azure](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="8f75c-148">For hello full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="8f75c-149">parameters</span><span class="sxs-lookup"><span data-stu-id="8f75c-149">Parameters</span></span>
<span data-ttu-id="8f75c-150">Nella sezione parametri di hello del modello di hello, specificare i valori che è possibile immettere quando si distribuisce hello risorse.</span><span class="sxs-lookup"><span data-stu-id="8f75c-150">In hello parameters section of hello template, you specify which values you can input when deploying hello resources.</span></span> <span data-ttu-id="8f75c-151">Valori di questi parametri consentono di distribuzione hello toocustomize fornendo i valori che sono specifiche per un particolare ambiente (ad esempio sviluppo, test e produzione).</span><span class="sxs-lookup"><span data-stu-id="8f75c-151">These parameter values enable you toocustomize hello deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="8f75c-152">Non si dispone tooprovide parametri nel modello, ma senza parametri del modello potrebbe distribuire sempre hello stesse risorse con hello nomi, percorsi e le stesse proprietà.</span><span class="sxs-lookup"><span data-stu-id="8f75c-152">You do not have tooprovide parameters in your template, but without parameters your template would always deploy hello same resources with hello same names, locations, and properties.</span></span>

<span data-ttu-id="8f75c-153">Definire i parametri con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="8f75c-153">You define parameters with hello following structure:</span></span>

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-hello parameter>" 
        }
    }
}
```

| <span data-ttu-id="8f75c-154">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="8f75c-154">Element name</span></span> | <span data-ttu-id="8f75c-155">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8f75c-155">Required</span></span> | <span data-ttu-id="8f75c-156">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8f75c-156">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8f75c-157">parameterName</span><span class="sxs-lookup"><span data-stu-id="8f75c-157">parameterName</span></span> |<span data-ttu-id="8f75c-158">Sì</span><span class="sxs-lookup"><span data-stu-id="8f75c-158">Yes</span></span> |<span data-ttu-id="8f75c-159">Nome del parametro hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-159">Name of hello parameter.</span></span> <span data-ttu-id="8f75c-160">Deve essere un identificatore JavaScript valido.</span><span class="sxs-lookup"><span data-stu-id="8f75c-160">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="8f75c-161">type</span><span class="sxs-lookup"><span data-stu-id="8f75c-161">type</span></span> |<span data-ttu-id="8f75c-162">Sì</span><span class="sxs-lookup"><span data-stu-id="8f75c-162">Yes</span></span> |<span data-ttu-id="8f75c-163">Tipo di valore del parametro hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-163">Type of hello parameter value.</span></span> <span data-ttu-id="8f75c-164">Dopo questa tabella, vedere elenco hello dei tipi consentiti.</span><span class="sxs-lookup"><span data-stu-id="8f75c-164">See hello list of allowed types after this table.</span></span> |
| <span data-ttu-id="8f75c-165">defaultValue</span><span class="sxs-lookup"><span data-stu-id="8f75c-165">defaultValue</span></span> |<span data-ttu-id="8f75c-166">No</span><span class="sxs-lookup"><span data-stu-id="8f75c-166">No</span></span> |<span data-ttu-id="8f75c-167">Valore predefinito per il parametro hello, se viene fornito alcun valore per il parametro hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-167">Default value for hello parameter, if no value is provided for hello parameter.</span></span> |
| <span data-ttu-id="8f75c-168">allowedValues</span><span class="sxs-lookup"><span data-stu-id="8f75c-168">allowedValues</span></span> |<span data-ttu-id="8f75c-169">No</span><span class="sxs-lookup"><span data-stu-id="8f75c-169">No</span></span> |<span data-ttu-id="8f75c-170">Matrice di valori consentiti per toomake parametro hello assicurarsi che venga fornito valore destro hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-170">Array of allowed values for hello parameter toomake sure that hello right value is provided.</span></span> |
| <span data-ttu-id="8f75c-171">minValue</span><span class="sxs-lookup"><span data-stu-id="8f75c-171">minValue</span></span> |<span data-ttu-id="8f75c-172">No</span><span class="sxs-lookup"><span data-stu-id="8f75c-172">No</span></span> |<span data-ttu-id="8f75c-173">valore minimo di Hello per i parametri di tipo int, questo valore è inclusivo.</span><span class="sxs-lookup"><span data-stu-id="8f75c-173">hello minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="8f75c-174">maxValue</span><span class="sxs-lookup"><span data-stu-id="8f75c-174">maxValue</span></span> |<span data-ttu-id="8f75c-175">No</span><span class="sxs-lookup"><span data-stu-id="8f75c-175">No</span></span> |<span data-ttu-id="8f75c-176">Hello valore massimo per i parametri di tipo int, questo valore è inclusivo.</span><span class="sxs-lookup"><span data-stu-id="8f75c-176">hello maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="8f75c-177">minLength</span><span class="sxs-lookup"><span data-stu-id="8f75c-177">minLength</span></span> |<span data-ttu-id="8f75c-178">No</span><span class="sxs-lookup"><span data-stu-id="8f75c-178">No</span></span> |<span data-ttu-id="8f75c-179">lunghezza minima di Hello per stringa secureString e parametri di tipo matrice, questo valore è inclusivo.</span><span class="sxs-lookup"><span data-stu-id="8f75c-179">hello minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="8f75c-180">maxLength</span><span class="sxs-lookup"><span data-stu-id="8f75c-180">maxLength</span></span> |<span data-ttu-id="8f75c-181">No</span><span class="sxs-lookup"><span data-stu-id="8f75c-181">No</span></span> |<span data-ttu-id="8f75c-182">Hello lunghezza massima consentita per i parametri di tipo matrice, stringa e secureString, questo valore è inclusivo.</span><span class="sxs-lookup"><span data-stu-id="8f75c-182">hello maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="8f75c-183">description</span><span class="sxs-lookup"><span data-stu-id="8f75c-183">description</span></span> |<span data-ttu-id="8f75c-184">No</span><span class="sxs-lookup"><span data-stu-id="8f75c-184">No</span></span> |<span data-ttu-id="8f75c-185">Descrizione del parametro hello che viene visualizzata toousers tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-185">Description of hello parameter that is displayed toousers through hello portal.</span></span> |

<span data-ttu-id="8f75c-186">Hello tipi consentiti e i valori sono:</span><span class="sxs-lookup"><span data-stu-id="8f75c-186">hello allowed types and values are:</span></span>

* <span data-ttu-id="8f75c-187">**string**</span><span class="sxs-lookup"><span data-stu-id="8f75c-187">**string**</span></span>
* <span data-ttu-id="8f75c-188">**secureString**</span><span class="sxs-lookup"><span data-stu-id="8f75c-188">**secureString**</span></span>
* <span data-ttu-id="8f75c-189">**int**</span><span class="sxs-lookup"><span data-stu-id="8f75c-189">**int**</span></span>
* <span data-ttu-id="8f75c-190">**bool**</span><span class="sxs-lookup"><span data-stu-id="8f75c-190">**bool**</span></span>
* <span data-ttu-id="8f75c-191">**object**</span><span class="sxs-lookup"><span data-stu-id="8f75c-191">**object**</span></span> 
* <span data-ttu-id="8f75c-192">**secureObject**</span><span class="sxs-lookup"><span data-stu-id="8f75c-192">**secureObject**</span></span>
* <span data-ttu-id="8f75c-193">**array**</span><span class="sxs-lookup"><span data-stu-id="8f75c-193">**array**</span></span>

<span data-ttu-id="8f75c-194">toospecify un parametro come facoltativo, fornire un valore predefinito (può essere una stringa vuota).</span><span class="sxs-lookup"><span data-stu-id="8f75c-194">toospecify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="8f75c-195">Se si specifica un nome di parametro nel modello che corrisponde a un parametro di modello di hello toodeploy comando hello, sussiste ambiguità sui valori hello forniti.</span><span class="sxs-lookup"><span data-stu-id="8f75c-195">If you specify a parameter name in your template that matches a parameter in hello command toodeploy hello template, there is potential ambiguity about hello values you provide.</span></span> <span data-ttu-id="8f75c-196">Gestione risorse consente di risolvere questa confusione aggiungendo il suffisso hello **FromTemplate** toohello parametro di modello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-196">Resource Manager resolves this confusion by adding hello postfix **FromTemplate** toohello template parameter.</span></span> <span data-ttu-id="8f75c-197">Ad esempio, se si include un parametro denominato **ResourceGroupName** nel modello, è in conflitto con hello **ResourceGroupName** parametro hello [ Nuovo AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8f75c-197">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="8f75c-198">Durante la distribuzione, si è tooprovide richiesto un valore per **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="8f75c-198">During deployment, you are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="8f75c-199">In generale, si dovrebbe evitare questa confusione, non denominazione dei parametri con hello stesso nome come parametri utilizzati per operazioni di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="8f75c-199">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="8f75c-200">Tutte le password, chiavi e altri segreti devono usare hello **secureString** tipo.</span><span class="sxs-lookup"><span data-stu-id="8f75c-200">All passwords, keys, and other secrets should use hello **secureString** type.</span></span> <span data-ttu-id="8f75c-201">Se si passano dati sensibili in un oggetto JSON, utilizzare hello **secureObject** tipo.</span><span class="sxs-lookup"><span data-stu-id="8f75c-201">If you pass sensitive data in a JSON object, use hello **secureObject** type.</span></span> <span data-ttu-id="8f75c-202">Non è possibile leggere i parametri di modello di tipo secureString o secureObject dopo la distribuzione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="8f75c-202">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="8f75c-203">Ad esempio, hello seguente voce nella cronologia della distribuzione hello Mostra hello valore per una stringa e un oggetto, ma non per secureString e secureObject.</span><span class="sxs-lookup"><span data-stu-id="8f75c-203">For example, hello following entry in hello deployment history shows hello value for a string and object but not for secureString and secureObject.</span></span>
>
> ![visualizzare i valori della distribuzione](./media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="8f75c-205">Hello seguente esempio viene illustrato come toodefine parametri:</span><span class="sxs-lookup"><span data-stu-id="8f75c-205">hello following example shows how toodefine parameters:</span></span>

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

<span data-ttu-id="8f75c-206">Per il parametro hello tooinput come valori durante la distribuzione, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="8f75c-206">For how tooinput hello parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="8f75c-207">variables</span><span class="sxs-lookup"><span data-stu-id="8f75c-207">Variables</span></span>
<span data-ttu-id="8f75c-208">Nella sezione variabili hello è costruire valori che possono essere utilizzati in tutto il modello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-208">In hello variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="8f75c-209">Non è necessario toodefine variabili, ma semplificano spesso il modello riducendo le espressioni complesse.</span><span class="sxs-lookup"><span data-stu-id="8f75c-209">You do not need toodefine variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="8f75c-210">Definire le variabili con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="8f75c-210">You define variables with hello following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="8f75c-211">Hello seguente esempio viene illustrato come toodefine una variabile che viene costruita dai due valori di parametro:</span><span class="sxs-lookup"><span data-stu-id="8f75c-211">hello following example shows how toodefine a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="8f75c-212">Hello esempio successivo mostra una variabile che è un tipo complesso di JSON e le variabili sono costituite da altre variabili:</span><span class="sxs-lookup"><span data-stu-id="8f75c-212">hello next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a><span data-ttu-id="8f75c-213">Risorse</span><span class="sxs-lookup"><span data-stu-id="8f75c-213">Resources</span></span>
<span data-ttu-id="8f75c-214">Nella sezione risorse hello, definire le risorse di hello che vengono distribuite o aggiornate.</span><span class="sxs-lookup"><span data-stu-id="8f75c-214">In hello resources section, you define hello resources that are deployed or updated.</span></span> <span data-ttu-id="8f75c-215">In questa sezione può diventare complicata perché è necessario comprendere i tipi di hello distribuisce i valori corretti di tooprovide hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-215">This section can get complicated because you must understand hello types you are deploying tooprovide hello right values.</span></span> <span data-ttu-id="8f75c-216">Per hello risorse valori specifici (apiVersion, tipo e proprietà) che è necessario tooset, vedere [definire le risorse nei modelli di Azure Resource Manager](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="8f75c-216">For hello resource-specific values (apiVersion, type, and properties) that you need tooset, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="8f75c-217">Si definiscono le risorse con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="8f75c-217">You define resources with hello following structure:</span></span>

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| <span data-ttu-id="8f75c-218">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="8f75c-218">Element name</span></span> | <span data-ttu-id="8f75c-219">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8f75c-219">Required</span></span> | <span data-ttu-id="8f75c-220">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8f75c-220">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8f75c-221">condition</span><span class="sxs-lookup"><span data-stu-id="8f75c-221">condition</span></span> | <span data-ttu-id="8f75c-222">No</span><span class="sxs-lookup"><span data-stu-id="8f75c-222">No</span></span> | <span data-ttu-id="8f75c-223">Valore booleano che indica se la risorsa hello viene distribuita.</span><span class="sxs-lookup"><span data-stu-id="8f75c-223">Boolean value that indicates whether hello resource is deployed.</span></span> |
| <span data-ttu-id="8f75c-224">apiVersion</span><span class="sxs-lookup"><span data-stu-id="8f75c-224">apiVersion</span></span> |<span data-ttu-id="8f75c-225">Sì</span><span class="sxs-lookup"><span data-stu-id="8f75c-225">Yes</span></span> |<span data-ttu-id="8f75c-226">Versione di hello toouse di API REST per la creazione di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-226">Version of hello REST API toouse for creating hello resource.</span></span> |
| <span data-ttu-id="8f75c-227">type</span><span class="sxs-lookup"><span data-stu-id="8f75c-227">type</span></span> |<span data-ttu-id="8f75c-228">Sì</span><span class="sxs-lookup"><span data-stu-id="8f75c-228">Yes</span></span> |<span data-ttu-id="8f75c-229">Tipo di risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-229">Type of hello resource.</span></span> <span data-ttu-id="8f75c-230">Questo valore è una combinazione di spazio dei nomi hello del provider di risorse hello e il tipo di risorsa hello (ad esempio **Microsoft.Storage/storageAccounts**).</span><span class="sxs-lookup"><span data-stu-id="8f75c-230">This value is a combination of hello namespace of hello resource provider and hello resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="8f75c-231">name</span><span class="sxs-lookup"><span data-stu-id="8f75c-231">name</span></span> |<span data-ttu-id="8f75c-232">Sì</span><span class="sxs-lookup"><span data-stu-id="8f75c-232">Yes</span></span> |<span data-ttu-id="8f75c-233">Nome della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-233">Name of hello resource.</span></span> <span data-ttu-id="8f75c-234">nome di Hello deve rispettare le restrizioni dei componenti URI definite in RFC3986.</span><span class="sxs-lookup"><span data-stu-id="8f75c-234">hello name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="8f75c-235">Inoltre, servizi di Azure che espongono parti toooutside nome risorsa di hello convalidare toomake nome hello che non sia un tentativo toospoof un'altra identità.</span><span class="sxs-lookup"><span data-stu-id="8f75c-235">In addition, Azure services that expose hello resource name toooutside parties validate hello name toomake sure it is not an attempt toospoof another identity.</span></span> |
| <span data-ttu-id="8f75c-236">location</span><span class="sxs-lookup"><span data-stu-id="8f75c-236">location</span></span> |<span data-ttu-id="8f75c-237">Variabile</span><span class="sxs-lookup"><span data-stu-id="8f75c-237">Varies</span></span> |<span data-ttu-id="8f75c-238">Posizioni geografiche supportate di hello forniva risorse.</span><span class="sxs-lookup"><span data-stu-id="8f75c-238">Supported geo-locations of hello provided resource.</span></span> <span data-ttu-id="8f75c-239">È possibile selezionare una delle posizioni disponibili hello, ma in genere rende toopick senso che gli utenti tooyour Chiudi.</span><span class="sxs-lookup"><span data-stu-id="8f75c-239">You can select any of hello available locations, but typically it makes sense toopick one that is close tooyour users.</span></span> <span data-ttu-id="8f75c-240">In genere, è anche consigliabile tooplace risorse che interagiscono tra loro hello stessa area.</span><span class="sxs-lookup"><span data-stu-id="8f75c-240">Usually, it also makes sense tooplace resources that interact with each other in hello same region.</span></span> <span data-ttu-id="8f75c-241">La maggior parte dei tipi di risorsa richiede una posizione, ma alcuni tipi (ad esempio un'assegnazione di ruolo) non la richiedono.</span><span class="sxs-lookup"><span data-stu-id="8f75c-241">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="8f75c-242">Vedere [Impostare la posizione delle risorse nei modelli di Azure Resource Manager](resource-manager-template-location.md).</span><span class="sxs-lookup"><span data-stu-id="8f75c-242">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="8f75c-243">tags</span><span class="sxs-lookup"><span data-stu-id="8f75c-243">tags</span></span> |<span data-ttu-id="8f75c-244">No</span><span class="sxs-lookup"><span data-stu-id="8f75c-244">No</span></span> |<span data-ttu-id="8f75c-245">Tag associati a risorse hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-245">Tags that are associated with hello resource.</span></span> <span data-ttu-id="8f75c-246">Vedere [Applicare i tag alle risorse nei modelli di Azure Resource Manager](resource-manager-template-tags.md).</span><span class="sxs-lookup"><span data-stu-id="8f75c-246">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="8f75c-247">commenti</span><span class="sxs-lookup"><span data-stu-id="8f75c-247">comments</span></span> |<span data-ttu-id="8f75c-248">No</span><span class="sxs-lookup"><span data-stu-id="8f75c-248">No</span></span> |<span data-ttu-id="8f75c-249">Le note per documentare le risorse di hello nel modello</span><span class="sxs-lookup"><span data-stu-id="8f75c-249">Your notes for documenting hello resources in your template</span></span> |
| <span data-ttu-id="8f75c-250">copy</span><span class="sxs-lookup"><span data-stu-id="8f75c-250">copy</span></span> |<span data-ttu-id="8f75c-251">No</span><span class="sxs-lookup"><span data-stu-id="8f75c-251">No</span></span> |<span data-ttu-id="8f75c-252">Se è necessaria più di un'istanza, hello numero di risorse toocreate.</span><span class="sxs-lookup"><span data-stu-id="8f75c-252">If more than one instance is needed, hello number of resources toocreate.</span></span> <span data-ttu-id="8f75c-253">modalità predefinita di Hello è parallela.</span><span class="sxs-lookup"><span data-stu-id="8f75c-253">hello default mode is parallel.</span></span> <span data-ttu-id="8f75c-254">Specificare la modalità seriale quando non si desidera che tutti o hello toodeploy risorse in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="8f75c-254">Specify serial mode when you do not want all or hello resources toodeploy at hello same time.</span></span> <span data-ttu-id="8f75c-255">Per altre informazioni, vedere [Creare più istanze di risorse in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="8f75c-255">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="8f75c-256">dependsOn</span><span class="sxs-lookup"><span data-stu-id="8f75c-256">dependsOn</span></span> |<span data-ttu-id="8f75c-257">No</span><span class="sxs-lookup"><span data-stu-id="8f75c-257">No</span></span> |<span data-ttu-id="8f75c-258">Risorse da distribuire prima della distribuzione di questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="8f75c-258">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="8f75c-259">Gestione risorse valuta hello le dipendenze tra le risorse e li distribuisce nell'ordine corretto hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-259">Resource Manager evaluates hello dependencies between resources and deploys them in hello correct order.</span></span> <span data-ttu-id="8f75c-260">Quando le risorse non sono interdipendenti, vengono distribuite in parallelo.</span><span class="sxs-lookup"><span data-stu-id="8f75c-260">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="8f75c-261">Hello valore può essere un elenco delimitato da virgole di una risorsa di nomi o gli identificatori univoci di risorse.</span><span class="sxs-lookup"><span data-stu-id="8f75c-261">hello value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="8f75c-262">Elencare solo le risorse distribuite in questo modello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-262">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="8f75c-263">Le risorse non definite in questo modello devono essere già esistenti.</span><span class="sxs-lookup"><span data-stu-id="8f75c-263">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="8f75c-264">Evitare di aggiungere dipendenze non necessarie perché possono rallentare la distribuzione e creare dipendenze circolari.</span><span class="sxs-lookup"><span data-stu-id="8f75c-264">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="8f75c-265">Per indicazioni sull'impostazione delle dipendenze, vedere l'articolo relativo alla [definizione delle dipendenze nei modelli di Azure Resource Manager](resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="8f75c-265">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="8f75c-266">properties</span><span class="sxs-lookup"><span data-stu-id="8f75c-266">properties</span></span> |<span data-ttu-id="8f75c-267">No</span><span class="sxs-lookup"><span data-stu-id="8f75c-267">No</span></span> |<span data-ttu-id="8f75c-268">Impostazioni di configurazione specifiche delle risorse.</span><span class="sxs-lookup"><span data-stu-id="8f75c-268">Resource-specific configuration settings.</span></span> <span data-ttu-id="8f75c-269">i valori Hello per le proprietà di hello sono hello stesso come valori hello forniti nel corpo della richiesta hello per hello API REST (metodo PUT) toocreate hello risorsa.</span><span class="sxs-lookup"><span data-stu-id="8f75c-269">hello values for hello properties are hello same as hello values you provide in hello request body for hello REST API operation (PUT method) toocreate hello resource.</span></span> <span data-ttu-id="8f75c-270">È inoltre possibile specificare un toocreate matrice copia più istanze di una proprietà.</span><span class="sxs-lookup"><span data-stu-id="8f75c-270">You can also specify a copy array toocreate multiple instances of a property.</span></span> <span data-ttu-id="8f75c-271">Per altre informazioni, vedere [Creare più istanze di risorse in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="8f75c-271">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="8f75c-272">resources</span><span class="sxs-lookup"><span data-stu-id="8f75c-272">resources</span></span> |<span data-ttu-id="8f75c-273">No</span><span class="sxs-lookup"><span data-stu-id="8f75c-273">No</span></span> |<span data-ttu-id="8f75c-274">Risorse figlio che dipendono dalla risorsa hello da definire.</span><span class="sxs-lookup"><span data-stu-id="8f75c-274">Child resources that depend on hello resource being defined.</span></span> <span data-ttu-id="8f75c-275">Specificare solo i tipi di risorse che sono consentiti dallo schema hello della risorsa padre hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-275">Only provide resource types that are permitted by hello schema of hello parent resource.</span></span> <span data-ttu-id="8f75c-276">Hello nome completo del tipo di risorsa figlio hello include tipo di risorsa padre hello, ad esempio **Microsoft.Web/sites/extensions**.</span><span class="sxs-lookup"><span data-stu-id="8f75c-276">hello fully qualified type of hello child resource includes hello parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="8f75c-277">Dipendenza dalla risorsa padre hello non è implicita.</span><span class="sxs-lookup"><span data-stu-id="8f75c-277">Dependency on hello parent resource is not implied.</span></span> <span data-ttu-id="8f75c-278">È necessario definirla in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="8f75c-278">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="8f75c-279">sezione delle risorse Hello contiene una matrice di hello toodeploy di risorse.</span><span class="sxs-lookup"><span data-stu-id="8f75c-279">hello resources section contains an array of hello resources toodeploy.</span></span> <span data-ttu-id="8f75c-280">All'interno di ogni risorsa è anche possibile definire una matrice di risorse figlio.</span><span class="sxs-lookup"><span data-stu-id="8f75c-280">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="8f75c-281">La sezione resources potrebbe quindi avere una struttura simile a questa:</span><span class="sxs-lookup"><span data-stu-id="8f75c-281">Therefore, your resources section could have a structure like:</span></span>

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

<span data-ttu-id="8f75c-282">Per altre informazioni sulla definizione delle risorse figlio, vedere [Impostare il nome e il tipo di una risorsa figlio in un modello di Resource Manager](resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="8f75c-282">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

<span data-ttu-id="8f75c-283">Hello **condizione** elemento specifica se la risorsa hello è distribuita.</span><span class="sxs-lookup"><span data-stu-id="8f75c-283">hello **condition** element specifies whether hello resource is deployed.</span></span> <span data-ttu-id="8f75c-284">un valore per questo elemento Hello risolve tootrue o false.</span><span class="sxs-lookup"><span data-stu-id="8f75c-284">hello value for this element resolves tootrue or false.</span></span> <span data-ttu-id="8f75c-285">Ad esempio, toospecify se viene distribuito un nuovo account di archiviazione, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="8f75c-285">For example, toospecify whether a new storage account is deployed, use:</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="8f75c-286">Per un esempio di utilizzo di una risorsa nuova o esistente, vedere [Modello di condizione nuovo o esistente](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="8f75c-286">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="8f75c-287">toospecify se una macchina virtuale viene distribuita con una password o chiave SSH, definire due versioni della macchina virtuale hello nel modello e utilizzare **condizione** toodifferentiate utilizzo.</span><span class="sxs-lookup"><span data-stu-id="8f75c-287">toospecify whether a virtual machine is deployed with a password or SSH key, define two versions of hello virtual machine in your template and use **condition** toodifferentiate usage.</span></span> <span data-ttu-id="8f75c-288">Passare un parametro che specifica quali toodeploy scenario.</span><span class="sxs-lookup"><span data-stu-id="8f75c-288">Pass a parameter that specifies which scenario toodeploy.</span></span>

```json
{
    "condition": "[equals(parameters('passwordOrSshKey'),'password')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'password')]",
    "properties": {
        "osProfile": {
            "computerName": "[variables('vmName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
        },
        ...
    },
    ...
},
{
    "condition": "[equals(parameters('passwordOrSshKey'),'sshKey')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'ssh')]",
    "properties": {
        "osProfile": {
            "linuxConfiguration": {
                "disablePasswordAuthentication": "true",
                "ssh": {
                    "publicKeys": [
                        {
                            "path": "[variables('sshKeyPath')]",
                            "keyData": "[parameters('adminSshKey')]"
                        }
                    ]
                }
            }
        },
        ...
    },
    ...
}
``` 

<span data-ttu-id="8f75c-289">Per un esempio di utilizzo di una password o una macchina virtuale di toodeploy chiave SSH, vedere [nome utente o SSH modello condizione](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="8f75c-289">For an example of using a password or SSH key toodeploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="outputs"></a><span data-ttu-id="8f75c-290">outputs</span><span class="sxs-lookup"><span data-stu-id="8f75c-290">Outputs</span></span>
<span data-ttu-id="8f75c-291">Nella sezione di output di hello, specificare i valori restituiti dalla distribuzione.</span><span class="sxs-lookup"><span data-stu-id="8f75c-291">In hello Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="8f75c-292">Ad esempio, è possibile restituire hello URI tooaccess una risorsa distribuita.</span><span class="sxs-lookup"><span data-stu-id="8f75c-292">For example, you could return hello URI tooaccess a deployed resource.</span></span>

<span data-ttu-id="8f75c-293">Hello seguente illustra la struttura hello di una definizione di output:</span><span class="sxs-lookup"><span data-stu-id="8f75c-293">hello following example shows hello structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="8f75c-294">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="8f75c-294">Element name</span></span> | <span data-ttu-id="8f75c-295">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="8f75c-295">Required</span></span> | <span data-ttu-id="8f75c-296">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8f75c-296">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8f75c-297">outputName</span><span class="sxs-lookup"><span data-stu-id="8f75c-297">outputName</span></span> |<span data-ttu-id="8f75c-298">Sì</span><span class="sxs-lookup"><span data-stu-id="8f75c-298">Yes</span></span> |<span data-ttu-id="8f75c-299">Nome del valore di output di hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-299">Name of hello output value.</span></span> <span data-ttu-id="8f75c-300">Deve essere un identificatore JavaScript valido.</span><span class="sxs-lookup"><span data-stu-id="8f75c-300">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="8f75c-301">type</span><span class="sxs-lookup"><span data-stu-id="8f75c-301">type</span></span> |<span data-ttu-id="8f75c-302">Sì</span><span class="sxs-lookup"><span data-stu-id="8f75c-302">Yes</span></span> |<span data-ttu-id="8f75c-303">Tipo di valore di output di hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-303">Type of hello output value.</span></span> <span data-ttu-id="8f75c-304">I valori di output supportano hello stesso tipi come parametri di input di modello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-304">Output values support hello same types as template input parameters.</span></span> |
| <span data-ttu-id="8f75c-305">value</span><span class="sxs-lookup"><span data-stu-id="8f75c-305">value</span></span> |<span data-ttu-id="8f75c-306">Sì</span><span class="sxs-lookup"><span data-stu-id="8f75c-306">Yes</span></span> |<span data-ttu-id="8f75c-307">Espressione del linguaggio di modello valutata e restituita come valore di output.</span><span class="sxs-lookup"><span data-stu-id="8f75c-307">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="8f75c-308">Hello esempio seguente mostra un valore che viene restituito nella sezione di output di hello.</span><span class="sxs-lookup"><span data-stu-id="8f75c-308">hello following example shows a value that is returned in hello Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="8f75c-309">Per altre informazioni sull'utilizzo dell'output, vedere [Condivisione dello stato in modelli di Azure Resource Manager](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="8f75c-309">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="template-limits"></a><span data-ttu-id="8f75c-310">Limiti del modello</span><span class="sxs-lookup"><span data-stu-id="8f75c-310">Template limits</span></span>

<span data-ttu-id="8f75c-311">Limita le dimensioni di hello di too1 il modello file KB too64 MB e ogni parametro.</span><span class="sxs-lookup"><span data-stu-id="8f75c-311">Limit hello size of your template too1 MB, and each parameter file too64 KB.</span></span> <span data-ttu-id="8f75c-312">limite di 1 MB Hello applica lo stato finale di toohello del modello di hello dopo che è stato espanso con definizioni di risorse iterativo e i valori di variabili e parametri.</span><span class="sxs-lookup"><span data-stu-id="8f75c-312">hello 1-MB limit applies toohello final state of hello template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

<span data-ttu-id="8f75c-313">Si è anche limitati a:</span><span class="sxs-lookup"><span data-stu-id="8f75c-313">You are also limited to:</span></span>

* <span data-ttu-id="8f75c-314">256 parametri</span><span class="sxs-lookup"><span data-stu-id="8f75c-314">256 parameters</span></span>
* <span data-ttu-id="8f75c-315">256 variabili</span><span class="sxs-lookup"><span data-stu-id="8f75c-315">256 variables</span></span>
* <span data-ttu-id="8f75c-316">800 risorse (incluso il conteggio copie)</span><span class="sxs-lookup"><span data-stu-id="8f75c-316">800 resources (including copy count)</span></span>
* <span data-ttu-id="8f75c-317">64 valori di output</span><span class="sxs-lookup"><span data-stu-id="8f75c-317">64 output values</span></span>
* <span data-ttu-id="8f75c-318">24.576 caratteri in un'espressione di modello</span><span class="sxs-lookup"><span data-stu-id="8f75c-318">24,576 characters in a template expression</span></span>

<span data-ttu-id="8f75c-319">È possibile superare alcuni limiti del modello usando un modello annidato.</span><span class="sxs-lookup"><span data-stu-id="8f75c-319">You can exceed some template limits by using a nested template.</span></span> <span data-ttu-id="8f75c-320">Per altre informazioni, vedere [Uso di modelli collegati nella distribuzione di risorse di Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8f75c-320">For more information, see [Using linked templates when deploying Azure resources](resource-group-linked-templates.md).</span></span> <span data-ttu-id="8f75c-321">numero di hello tooreduce di parametri, variabili o output, è possibile combinare più valori in un oggetto.</span><span class="sxs-lookup"><span data-stu-id="8f75c-321">tooreduce hello number of parameters, variables, or outputs, you can combine several values into an object.</span></span> <span data-ttu-id="8f75c-322">Per altre informazioni, vedere [Oggetti come parametri](resource-manager-objects-as-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="8f75c-322">For more information, see [Objects as parameters](resource-manager-objects-as-parameters.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f75c-323">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8f75c-323">Next steps</span></span>
* <span data-ttu-id="8f75c-324">modelli completo di tooview per molti tipi diversi di soluzioni, vedere hello [modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="8f75c-324">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="8f75c-325">Per informazioni dettagliate sulle funzioni hello è possibile usare dall'interno di un modello, vedere [funzioni di modello di gestione risorse di Azure](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="8f75c-325">For details about hello functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="8f75c-326">toocombine più modelli durante la distribuzione, vedere [con modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8f75c-326">toocombine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="8f75c-327">Potrebbe essere necessario toouse risorse esistenti all'interno di un gruppo di risorse diverso.</span><span class="sxs-lookup"><span data-stu-id="8f75c-327">You may need toouse resources that exist within a different resource group.</span></span> <span data-ttu-id="8f75c-328">Questo scenario è comune quando si usano account di archiviazione o reti virtuali condivisi tra più gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="8f75c-328">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="8f75c-329">Per ulteriori informazioni, vedere hello [funzione resourceId](resource-group-template-functions-resource.md#resourceid).</span><span class="sxs-lookup"><span data-stu-id="8f75c-329">For more information, see hello [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
