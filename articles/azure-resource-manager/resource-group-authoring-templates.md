---
title: Struttura e sintassi del modello di Azure Resource Manger | Documentazione Microsoft
description: "Descrive la struttura e le proprietà dei modelli di Azure Resource Manager con la sintassi dichiarativa JSON."
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
ms.openlocfilehash: dc9b64062d7f68c83aa090eec96744819a5ca423
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="understand-the-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="73264-103">Comprendere la struttura e la sintassi dei modelli di Azure Resource Manger</span><span class="sxs-lookup"><span data-stu-id="73264-103">Understand the structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="73264-104">Questo argomento descrive la struttura di un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="73264-104">This topic describes the structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="73264-105">Presenta le diverse sezioni di un modello e le proprietà disponibili in queste sezioni.</span><span class="sxs-lookup"><span data-stu-id="73264-105">It presents the different sections of a template and the properties that are available in those sections.</span></span> <span data-ttu-id="73264-106">Il modello è composto da JSON ed espressioni che è possibile usare per creare valori per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="73264-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="73264-107">Per un'esercitazione dettagliata sulla creazione di un modello, vedere [Creare il primo modello di Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="73264-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

## <a name="template-format"></a><span data-ttu-id="73264-108">Formato del modello</span><span class="sxs-lookup"><span data-stu-id="73264-108">Template format</span></span>
<span data-ttu-id="73264-109">La struttura più semplice di un modello è costituita dagli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="73264-109">In its simplest structure, a template contains the following elements:</span></span>

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

| <span data-ttu-id="73264-110">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="73264-110">Element name</span></span> | <span data-ttu-id="73264-111">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="73264-111">Required</span></span> | <span data-ttu-id="73264-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="73264-112">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="73264-113">$schema</span><span class="sxs-lookup"><span data-stu-id="73264-113">$schema</span></span> |<span data-ttu-id="73264-114">Sì</span><span class="sxs-lookup"><span data-stu-id="73264-114">Yes</span></span> |<span data-ttu-id="73264-115">Percorso del file di schema JSON che descrive la versione del linguaggio del modello.</span><span class="sxs-lookup"><span data-stu-id="73264-115">Location of the JSON schema file that describes the version of the template language.</span></span> <span data-ttu-id="73264-116">Usare l'URL riportato nell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="73264-116">Use the URL shown in the preceding example.</span></span> |
| <span data-ttu-id="73264-117">contentVersion</span><span class="sxs-lookup"><span data-stu-id="73264-117">contentVersion</span></span> |<span data-ttu-id="73264-118">Sì</span><span class="sxs-lookup"><span data-stu-id="73264-118">Yes</span></span> |<span data-ttu-id="73264-119">Versione del modello (ad esempio 1.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="73264-119">Version of the template (such as 1.0.0.0).</span></span> <span data-ttu-id="73264-120">Questo elemento accetta tutti i valori.</span><span class="sxs-lookup"><span data-stu-id="73264-120">You can provide any value for this element.</span></span> <span data-ttu-id="73264-121">Quando si distribuiscono risorse tramite il modello, è possibile usare questo valore per assicurarsi che venga usato il modello corretto.</span><span class="sxs-lookup"><span data-stu-id="73264-121">When deploying resources using the template, this value can be used to make sure that the right template is being used.</span></span> |
| <span data-ttu-id="73264-122">parameters</span><span class="sxs-lookup"><span data-stu-id="73264-122">parameters</span></span> |<span data-ttu-id="73264-123">No</span><span class="sxs-lookup"><span data-stu-id="73264-123">No</span></span> |<span data-ttu-id="73264-124">Valori forniti durante la distribuzione per personalizzare la distribuzione di risorse.</span><span class="sxs-lookup"><span data-stu-id="73264-124">Values that are provided when deployment is executed to customize resource deployment.</span></span> |
| <span data-ttu-id="73264-125">variables</span><span class="sxs-lookup"><span data-stu-id="73264-125">variables</span></span> |<span data-ttu-id="73264-126">No</span><span class="sxs-lookup"><span data-stu-id="73264-126">No</span></span> |<span data-ttu-id="73264-127">Valori usati come frammenti JSON nel modello per semplificare le espressioni di linguaggio del modello.</span><span class="sxs-lookup"><span data-stu-id="73264-127">Values that are used as JSON fragments in the template to simplify template language expressions.</span></span> |
| <span data-ttu-id="73264-128">resources</span><span class="sxs-lookup"><span data-stu-id="73264-128">resources</span></span> |<span data-ttu-id="73264-129">Sì</span><span class="sxs-lookup"><span data-stu-id="73264-129">Yes</span></span> |<span data-ttu-id="73264-130">Tipi di risorse che vengono distribuite o aggiornate in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="73264-130">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="73264-131">outputs</span><span class="sxs-lookup"><span data-stu-id="73264-131">outputs</span></span> |<span data-ttu-id="73264-132">No</span><span class="sxs-lookup"><span data-stu-id="73264-132">No</span></span> |<span data-ttu-id="73264-133">Valori restituiti dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="73264-133">Values that are returned after deployment.</span></span> |

<span data-ttu-id="73264-134">Ogni elemento contiene proprietà che è possibile impostare.</span><span class="sxs-lookup"><span data-stu-id="73264-134">Each element contains properties you can set.</span></span> <span data-ttu-id="73264-135">L'esempio seguente contiene la sintassi completa per un modello:</span><span class="sxs-lookup"><span data-stu-id="73264-135">The following example contains the full syntax for a template:</span></span>

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
                "description": "<description-of-the parameter>" 
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

<span data-ttu-id="73264-136">Le sezioni del modello verranno esaminate in modo dettagliato più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="73264-136">We examine the sections of the template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="73264-137">Espressioni e funzioni</span><span class="sxs-lookup"><span data-stu-id="73264-137">Expressions and functions</span></span>
<span data-ttu-id="73264-138">La sintassi di base del modello è JSON.</span><span class="sxs-lookup"><span data-stu-id="73264-138">The basic syntax of the template is JSON.</span></span> <span data-ttu-id="73264-139">Le espressioni e le funzioni estendono ad ogni modo i valori JSON disponibili all'interno del modello.</span><span class="sxs-lookup"><span data-stu-id="73264-139">However, expressions and functions extend the JSON values available within the template.</span></span>  <span data-ttu-id="73264-140">Le espressioni vengono scritte all'interno di valori letterali stringa JSON il cui primo e ultimo carattere sono le parentesi quadre: rispettivamente`[` e `]`.</span><span class="sxs-lookup"><span data-stu-id="73264-140">Expressions are written within JSON string literals whose first and last characters are the brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="73264-141">Il valore dell'espressione viene valutato quando viene distribuito il modello.</span><span class="sxs-lookup"><span data-stu-id="73264-141">The value of the expression is evaluated when the template is deployed.</span></span> <span data-ttu-id="73264-142">Sebbene sia scritto come valore letterale stringa, il risultato della valutazione dell'espressione può essere di un tipo JSON diverso, ad esempio una matrice o un numero intero, a seconda dell'espressione effettiva.</span><span class="sxs-lookup"><span data-stu-id="73264-142">While written as a string literal, the result of evaluating the expression can be of a different JSON type, such as an array or integer, depending on the actual expression.</span></span>  <span data-ttu-id="73264-143">Per avere una stringa letterale che inizi con una parentesi quadra `[`, ma che non venga interpretata come espressione, è necessario aggiungere un'altra parentesi in modo che la stringa inizi con `[[`.</span><span class="sxs-lookup"><span data-stu-id="73264-143">To have a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket to start the string with `[[`.</span></span>

<span data-ttu-id="73264-144">Solitamente, si usano espressioni con funzioni per eseguire operazioni per la configurazione della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="73264-144">Typically, you use expressions with functions to perform operations for configuring the deployment.</span></span> <span data-ttu-id="73264-145">Proprio come in JavaScript, le chiamate di funzione sono formattate come `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="73264-145">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="73264-146">Per i riferimenti alle proprietà si usano il punto e gli operatori [index].</span><span class="sxs-lookup"><span data-stu-id="73264-146">You reference properties by using the dot and [index] operators.</span></span>

<span data-ttu-id="73264-147">L'esempio seguente illustra come usare diverse funzioni al momento di costruite i valori:</span><span class="sxs-lookup"><span data-stu-id="73264-147">The following example shows how to use several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="73264-148">Per l’elenco completo delle funzioni del modello, vedere [Funzioni del modello di Gestione risorse di Azure](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="73264-148">For the full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="73264-149">parameters</span><span class="sxs-lookup"><span data-stu-id="73264-149">Parameters</span></span>
<span data-ttu-id="73264-150">Nella sezione parameters del modello si possono specificare i valori che è possibile immettere durante la distribuzione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="73264-150">In the parameters section of the template, you specify which values you can input when deploying the resources.</span></span> <span data-ttu-id="73264-151">I valori dei parametri consentono di personalizzare la distribuzione fornendo valori specifici per un determinato ambiente, ad esempio sviluppo, test e produzione.</span><span class="sxs-lookup"><span data-stu-id="73264-151">These parameter values enable you to customize the deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="73264-152">Non è obbligatorio specificare i parametri nel modello, ma senza di essi il modello distribuisce sempre le stesse risorse con lo stesso nome, località e proprietà.</span><span class="sxs-lookup"><span data-stu-id="73264-152">You do not have to provide parameters in your template, but without parameters your template would always deploy the same resources with the same names, locations, and properties.</span></span>

<span data-ttu-id="73264-153">I parametri vengono definiti con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="73264-153">You define parameters with the following structure:</span></span>

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
            "description": "<description-of-the parameter>" 
        }
    }
}
```

| <span data-ttu-id="73264-154">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="73264-154">Element name</span></span> | <span data-ttu-id="73264-155">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="73264-155">Required</span></span> | <span data-ttu-id="73264-156">Descrizione</span><span class="sxs-lookup"><span data-stu-id="73264-156">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="73264-157">parameterName</span><span class="sxs-lookup"><span data-stu-id="73264-157">parameterName</span></span> |<span data-ttu-id="73264-158">Sì</span><span class="sxs-lookup"><span data-stu-id="73264-158">Yes</span></span> |<span data-ttu-id="73264-159">Nome del parametro.</span><span class="sxs-lookup"><span data-stu-id="73264-159">Name of the parameter.</span></span> <span data-ttu-id="73264-160">Deve essere un identificatore JavaScript valido.</span><span class="sxs-lookup"><span data-stu-id="73264-160">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="73264-161">type</span><span class="sxs-lookup"><span data-stu-id="73264-161">type</span></span> |<span data-ttu-id="73264-162">Sì</span><span class="sxs-lookup"><span data-stu-id="73264-162">Yes</span></span> |<span data-ttu-id="73264-163">Tipo di valore del parametro.</span><span class="sxs-lookup"><span data-stu-id="73264-163">Type of the parameter value.</span></span> <span data-ttu-id="73264-164">Vedere l'elenco dei tipi consentiti riportato dopo questa tabella.</span><span class="sxs-lookup"><span data-stu-id="73264-164">See the list of allowed types after this table.</span></span> |
| <span data-ttu-id="73264-165">defaultValue</span><span class="sxs-lookup"><span data-stu-id="73264-165">defaultValue</span></span> |<span data-ttu-id="73264-166">No</span><span class="sxs-lookup"><span data-stu-id="73264-166">No</span></span> |<span data-ttu-id="73264-167">Valore predefinito per il parametro, se non viene fornito alcun valore per il parametro.</span><span class="sxs-lookup"><span data-stu-id="73264-167">Default value for the parameter, if no value is provided for the parameter.</span></span> |
| <span data-ttu-id="73264-168">allowedValues</span><span class="sxs-lookup"><span data-stu-id="73264-168">allowedValues</span></span> |<span data-ttu-id="73264-169">No</span><span class="sxs-lookup"><span data-stu-id="73264-169">No</span></span> |<span data-ttu-id="73264-170">Matrice di valori consentiti per il parametro per assicurare che venga fornito il valore corretto.</span><span class="sxs-lookup"><span data-stu-id="73264-170">Array of allowed values for the parameter to make sure that the right value is provided.</span></span> |
| <span data-ttu-id="73264-171">minValue</span><span class="sxs-lookup"><span data-stu-id="73264-171">minValue</span></span> |<span data-ttu-id="73264-172">No</span><span class="sxs-lookup"><span data-stu-id="73264-172">No</span></span> |<span data-ttu-id="73264-173">Il valore minimo per i parametri di tipo int, questo valore è inclusivo.</span><span class="sxs-lookup"><span data-stu-id="73264-173">The minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="73264-174">maxValue</span><span class="sxs-lookup"><span data-stu-id="73264-174">maxValue</span></span> |<span data-ttu-id="73264-175">No</span><span class="sxs-lookup"><span data-stu-id="73264-175">No</span></span> |<span data-ttu-id="73264-176">Il valore massimo per i parametri di tipo int, questo valore è inclusivo.</span><span class="sxs-lookup"><span data-stu-id="73264-176">The maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="73264-177">minLength</span><span class="sxs-lookup"><span data-stu-id="73264-177">minLength</span></span> |<span data-ttu-id="73264-178">No</span><span class="sxs-lookup"><span data-stu-id="73264-178">No</span></span> |<span data-ttu-id="73264-179">Lunghezza minima per i parametri di tipo string, secureString e array. Questo valore è inclusivo.</span><span class="sxs-lookup"><span data-stu-id="73264-179">The minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="73264-180">maxLength</span><span class="sxs-lookup"><span data-stu-id="73264-180">maxLength</span></span> |<span data-ttu-id="73264-181">No</span><span class="sxs-lookup"><span data-stu-id="73264-181">No</span></span> |<span data-ttu-id="73264-182">Lunghezza massima per i parametri di tipo string, secureString e array. Questo valore è inclusivo.</span><span class="sxs-lookup"><span data-stu-id="73264-182">The maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="73264-183">Descrizione</span><span class="sxs-lookup"><span data-stu-id="73264-183">description</span></span> |<span data-ttu-id="73264-184">No</span><span class="sxs-lookup"><span data-stu-id="73264-184">No</span></span> |<span data-ttu-id="73264-185">Descrizione del parametro visualizzato agli utenti nel portale.</span><span class="sxs-lookup"><span data-stu-id="73264-185">Description of the parameter that is displayed to users through the portal.</span></span> |

<span data-ttu-id="73264-186">I valori e i tipi consentiti sono:</span><span class="sxs-lookup"><span data-stu-id="73264-186">The allowed types and values are:</span></span>

* <span data-ttu-id="73264-187">**string**</span><span class="sxs-lookup"><span data-stu-id="73264-187">**string**</span></span>
* <span data-ttu-id="73264-188">**secureString**</span><span class="sxs-lookup"><span data-stu-id="73264-188">**secureString**</span></span>
* <span data-ttu-id="73264-189">**int**</span><span class="sxs-lookup"><span data-stu-id="73264-189">**int**</span></span>
* <span data-ttu-id="73264-190">**bool**</span><span class="sxs-lookup"><span data-stu-id="73264-190">**bool**</span></span>
* <span data-ttu-id="73264-191">**object**</span><span class="sxs-lookup"><span data-stu-id="73264-191">**object**</span></span> 
* <span data-ttu-id="73264-192">**secureObject**</span><span class="sxs-lookup"><span data-stu-id="73264-192">**secureObject**</span></span>
* <span data-ttu-id="73264-193">**array**</span><span class="sxs-lookup"><span data-stu-id="73264-193">**array**</span></span>

<span data-ttu-id="73264-194">Per specificare un parametro come facoltativo, fornire un valore defaultValue (che può essere anche una stringa vuota).</span><span class="sxs-lookup"><span data-stu-id="73264-194">To specify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="73264-195">Se nel modello si specifica un nome di parametro che corrisponde a un parametro nel comando per distribuire il modello, si crea una potenziale ambiguità in merito ai valori forniti.</span><span class="sxs-lookup"><span data-stu-id="73264-195">If you specify a parameter name in your template that matches a parameter in the command to deploy the template, there is potential ambiguity about the values you provide.</span></span> <span data-ttu-id="73264-196">Resource Manager risolve questa confusione aggiungendo il suffisso **FromTemplate** al parametro del modello.</span><span class="sxs-lookup"><span data-stu-id="73264-196">Resource Manager resolves this confusion by adding the postfix **FromTemplate** to the template parameter.</span></span> <span data-ttu-id="73264-197">Se, ad esempio, si include un parametro denominato **ResourceGroupName** nel modello, si crea un conflitto con il parametro **ResourceGroupName** nel cmdlet [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="73264-197">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="73264-198">Durante la distribuzione verrà quindi richiesto di specificare un valore per **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="73264-198">During deployment, you are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="73264-199">In generale, è consigliabile evitare questa confusione non attribuendo ai parametri lo stesso nome dei parametri usati per operazioni di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="73264-199">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="73264-200">Per tutte le password, le chiavi e altre informazioni riservate si consiglia di usare il tipo **secureString** .</span><span class="sxs-lookup"><span data-stu-id="73264-200">All passwords, keys, and other secrets should use the **secureString** type.</span></span> <span data-ttu-id="73264-201">Se si passano dati sensibili in un oggetto JSON, usare il tipo **secureObject**.</span><span class="sxs-lookup"><span data-stu-id="73264-201">If you pass sensitive data in a JSON object, use the **secureObject** type.</span></span> <span data-ttu-id="73264-202">Non è possibile leggere i parametri di modello di tipo secureString o secureObject dopo la distribuzione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="73264-202">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="73264-203">La voce seguente nella cronologia di distribuzione indica ad esempio il valore per una stringa e un oggetto, ma non per secureString e secureObject.</span><span class="sxs-lookup"><span data-stu-id="73264-203">For example, the following entry in the deployment history shows the value for a string and object but not for secureString and secureObject.</span></span>
>
> ![visualizzare i valori della distribuzione](./media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="73264-205">Il seguente esempio mostra come definire i parametri:</span><span class="sxs-lookup"><span data-stu-id="73264-205">The following example shows how to define parameters:</span></span>

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

<span data-ttu-id="73264-206">Per informazioni sull'immissione di valori di parametro durante la distribuzione vedere [Distribuire le risorse con i modelli di Azure Resource Manager e Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="73264-206">For how to input the parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="73264-207">variables</span><span class="sxs-lookup"><span data-stu-id="73264-207">Variables</span></span>
<span data-ttu-id="73264-208">Nella sezione variables è possibile costruire valori da usare in tutto il modello.</span><span class="sxs-lookup"><span data-stu-id="73264-208">In the variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="73264-209">Non è obbligatorio definire le variabili, che però permettono spesso di semplificare il modello riducendo le espressioni complesse.</span><span class="sxs-lookup"><span data-stu-id="73264-209">You do not need to define variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="73264-210">Le variabili vengono definite con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="73264-210">You define variables with the following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="73264-211">Nell'esempio seguente viene illustrato come definire una variabile creata da due valori di parametro:</span><span class="sxs-lookup"><span data-stu-id="73264-211">The following example shows how to define a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="73264-212">Nell'esempio successivo viene illustrata una variabile che rappresenta un tipo JSON complesso e variabili create da altre variabili:</span><span class="sxs-lookup"><span data-stu-id="73264-212">The next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

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

## <a name="resources"></a><span data-ttu-id="73264-213">resources</span><span class="sxs-lookup"><span data-stu-id="73264-213">Resources</span></span>
<span data-ttu-id="73264-214">Nella sezione risorse è possibile definire le risorse da distribuire o aggiornare.</span><span class="sxs-lookup"><span data-stu-id="73264-214">In the resources section, you define the resources that are deployed or updated.</span></span> <span data-ttu-id="73264-215">Questa sezione può risultare complicata perché per specificare i valori corretti è necessario conoscere i tipi da distribuire.</span><span class="sxs-lookup"><span data-stu-id="73264-215">This section can get complicated because you must understand the types you are deploying to provide the right values.</span></span> <span data-ttu-id="73264-216">Per i valori specifici della risorsa (apiVersion, tipo e proprietà) che è necessario impostare, vedere [Define resources in Azure Resource Manager templates](/azure/templates/) (Definire risorse nei modelli di Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="73264-216">For the resource-specific values (apiVersion, type, and properties) that you need to set, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="73264-217">Le risorse vengono definite con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="73264-217">You define resources with the following structure:</span></span>

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

| <span data-ttu-id="73264-218">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="73264-218">Element name</span></span> | <span data-ttu-id="73264-219">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="73264-219">Required</span></span> | <span data-ttu-id="73264-220">Descrizione</span><span class="sxs-lookup"><span data-stu-id="73264-220">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="73264-221">condition</span><span class="sxs-lookup"><span data-stu-id="73264-221">condition</span></span> | <span data-ttu-id="73264-222">No</span><span class="sxs-lookup"><span data-stu-id="73264-222">No</span></span> | <span data-ttu-id="73264-223">Valore booleano che indica se la risorsa viene distribuita.</span><span class="sxs-lookup"><span data-stu-id="73264-223">Boolean value that indicates whether the resource is deployed.</span></span> |
| <span data-ttu-id="73264-224">apiVersion</span><span class="sxs-lookup"><span data-stu-id="73264-224">apiVersion</span></span> |<span data-ttu-id="73264-225">Sì</span><span class="sxs-lookup"><span data-stu-id="73264-225">Yes</span></span> |<span data-ttu-id="73264-226">Versione dell'API REST da utilizzare per la creazione della risorsa.</span><span class="sxs-lookup"><span data-stu-id="73264-226">Version of the REST API to use for creating the resource.</span></span> |
| <span data-ttu-id="73264-227">type</span><span class="sxs-lookup"><span data-stu-id="73264-227">type</span></span> |<span data-ttu-id="73264-228">Sì</span><span class="sxs-lookup"><span data-stu-id="73264-228">Yes</span></span> |<span data-ttu-id="73264-229">Tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="73264-229">Type of the resource.</span></span> <span data-ttu-id="73264-230">Questo valore è una combinazione dello spazio dei nomi del provider di risorse e del tipo di risorsa, ad esempio **Microsoft.Storage/storageAccounts**.</span><span class="sxs-lookup"><span data-stu-id="73264-230">This value is a combination of the namespace of the resource provider and the resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="73264-231">name</span><span class="sxs-lookup"><span data-stu-id="73264-231">name</span></span> |<span data-ttu-id="73264-232">Sì</span><span class="sxs-lookup"><span data-stu-id="73264-232">Yes</span></span> |<span data-ttu-id="73264-233">Nome della risorsa.</span><span class="sxs-lookup"><span data-stu-id="73264-233">Name of the resource.</span></span> <span data-ttu-id="73264-234">Il nome deve rispettare le restrizioni dei componenti URI definite dallo standard RFC3986.</span><span class="sxs-lookup"><span data-stu-id="73264-234">The name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="73264-235">I servizi Azure che rendono visibile il nome della risorsa a terze parti convalidano anche il nome, per garantire che non si tratti di un tentativo di spoofing per un'identità alternativa.</span><span class="sxs-lookup"><span data-stu-id="73264-235">In addition, Azure services that expose the resource name to outside parties validate the name to make sure it is not an attempt to spoof another identity.</span></span> |
| <span data-ttu-id="73264-236">location</span><span class="sxs-lookup"><span data-stu-id="73264-236">location</span></span> |<span data-ttu-id="73264-237">Variabile</span><span class="sxs-lookup"><span data-stu-id="73264-237">Varies</span></span> |<span data-ttu-id="73264-238">Aree geografiche supportate della risorsa specificata.</span><span class="sxs-lookup"><span data-stu-id="73264-238">Supported geo-locations of the provided resource.</span></span> <span data-ttu-id="73264-239">È possibile selezionare qualsiasi località disponibile, ma è in genere opportuno sceglierne una vicina agli utenti.</span><span class="sxs-lookup"><span data-stu-id="73264-239">You can select any of the available locations, but typically it makes sense to pick one that is close to your users.</span></span> <span data-ttu-id="73264-240">Di solito è anche opportuno inserire le risorse che interagiscono tra loro nella stessa area.</span><span class="sxs-lookup"><span data-stu-id="73264-240">Usually, it also makes sense to place resources that interact with each other in the same region.</span></span> <span data-ttu-id="73264-241">La maggior parte dei tipi di risorsa richiede una posizione, ma alcuni tipi (ad esempio un'assegnazione di ruolo) non la richiedono.</span><span class="sxs-lookup"><span data-stu-id="73264-241">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="73264-242">Vedere [Impostare la posizione delle risorse nei modelli di Azure Resource Manager](resource-manager-template-location.md).</span><span class="sxs-lookup"><span data-stu-id="73264-242">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="73264-243">tags</span><span class="sxs-lookup"><span data-stu-id="73264-243">tags</span></span> |<span data-ttu-id="73264-244">No</span><span class="sxs-lookup"><span data-stu-id="73264-244">No</span></span> |<span data-ttu-id="73264-245">Tag associati alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="73264-245">Tags that are associated with the resource.</span></span> <span data-ttu-id="73264-246">Vedere [Applicare i tag alle risorse nei modelli di Azure Resource Manager](resource-manager-template-tags.md).</span><span class="sxs-lookup"><span data-stu-id="73264-246">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="73264-247">commenti</span><span class="sxs-lookup"><span data-stu-id="73264-247">comments</span></span> |<span data-ttu-id="73264-248">No</span><span class="sxs-lookup"><span data-stu-id="73264-248">No</span></span> |<span data-ttu-id="73264-249">Le note per documentare le risorse nel modello</span><span class="sxs-lookup"><span data-stu-id="73264-249">Your notes for documenting the resources in your template</span></span> |
| <span data-ttu-id="73264-250">copy</span><span class="sxs-lookup"><span data-stu-id="73264-250">copy</span></span> |<span data-ttu-id="73264-251">No</span><span class="sxs-lookup"><span data-stu-id="73264-251">No</span></span> |<span data-ttu-id="73264-252">Numero di risorse da creare, se sono necessarie più istanze.</span><span class="sxs-lookup"><span data-stu-id="73264-252">If more than one instance is needed, the number of resources to create.</span></span> <span data-ttu-id="73264-253">La modalità predefinita è parallela.</span><span class="sxs-lookup"><span data-stu-id="73264-253">The default mode is parallel.</span></span> <span data-ttu-id="73264-254">Specificare la modalità seriale quando si desidera che non tutte le risorse vengano distribuite contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="73264-254">Specify serial mode when you do not want all or the resources to deploy at the same time.</span></span> <span data-ttu-id="73264-255">Per altre informazioni, vedere [Creare più istanze di risorse in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="73264-255">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="73264-256">dependsOn</span><span class="sxs-lookup"><span data-stu-id="73264-256">dependsOn</span></span> |<span data-ttu-id="73264-257">No</span><span class="sxs-lookup"><span data-stu-id="73264-257">No</span></span> |<span data-ttu-id="73264-258">Risorse da distribuire prima della distribuzione di questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="73264-258">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="73264-259">Resource Manager valuta le dipendenze tra le risorse e le distribuisce nell'ordine corretto.</span><span class="sxs-lookup"><span data-stu-id="73264-259">Resource Manager evaluates the dependencies between resources and deploys them in the correct order.</span></span> <span data-ttu-id="73264-260">Quando le risorse non sono interdipendenti, vengono distribuite in parallelo.</span><span class="sxs-lookup"><span data-stu-id="73264-260">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="73264-261">Il valore può essere un elenco delimitato da virgole di nomi o identificatori univoci di risorse.</span><span class="sxs-lookup"><span data-stu-id="73264-261">The value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="73264-262">Elencare solo le risorse distribuite in questo modello.</span><span class="sxs-lookup"><span data-stu-id="73264-262">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="73264-263">Le risorse non definite in questo modello devono essere già esistenti.</span><span class="sxs-lookup"><span data-stu-id="73264-263">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="73264-264">Evitare di aggiungere dipendenze non necessarie perché possono rallentare la distribuzione e creare dipendenze circolari.</span><span class="sxs-lookup"><span data-stu-id="73264-264">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="73264-265">Per indicazioni sull'impostazione delle dipendenze, vedere l'articolo relativo alla [definizione delle dipendenze nei modelli di Azure Resource Manager](resource-group-define-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="73264-265">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="73264-266">properties</span><span class="sxs-lookup"><span data-stu-id="73264-266">properties</span></span> |<span data-ttu-id="73264-267">No</span><span class="sxs-lookup"><span data-stu-id="73264-267">No</span></span> |<span data-ttu-id="73264-268">Impostazioni di configurazione specifiche delle risorse.</span><span class="sxs-lookup"><span data-stu-id="73264-268">Resource-specific configuration settings.</span></span> <span data-ttu-id="73264-269">I valori per l'elemento properties corrispondono esattamente a quelli specificati nel corpo della richiesta per l'operazione API REST (metodo PUT) per creare la risorsa.</span><span class="sxs-lookup"><span data-stu-id="73264-269">The values for the properties are the same as the values you provide in the request body for the REST API operation (PUT method) to create the resource.</span></span> <span data-ttu-id="73264-270">È inoltre possibile specificare una matrice di copia per creare più istanze di una proprietà.</span><span class="sxs-lookup"><span data-stu-id="73264-270">You can also specify a copy array to create multiple instances of a property.</span></span> <span data-ttu-id="73264-271">Per altre informazioni, vedere [Creare più istanze di risorse in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="73264-271">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="73264-272">resources</span><span class="sxs-lookup"><span data-stu-id="73264-272">resources</span></span> |<span data-ttu-id="73264-273">No</span><span class="sxs-lookup"><span data-stu-id="73264-273">No</span></span> |<span data-ttu-id="73264-274">Risorse figlio che dipendono dalla risorsa in via di definizione.</span><span class="sxs-lookup"><span data-stu-id="73264-274">Child resources that depend on the resource being defined.</span></span> <span data-ttu-id="73264-275">Specificare solo tipi di risorsa consentiti dallo schema della risorsa padre.</span><span class="sxs-lookup"><span data-stu-id="73264-275">Only provide resource types that are permitted by the schema of the parent resource.</span></span> <span data-ttu-id="73264-276">Il nome di tipo completo della risorsa figlio include il tipo della risorsa padre, ad esempio **Microsoft.Web/sites/extensions**.</span><span class="sxs-lookup"><span data-stu-id="73264-276">The fully qualified type of the child resource includes the parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="73264-277">La dipendenza dalla risorsa padre non è implicita.</span><span class="sxs-lookup"><span data-stu-id="73264-277">Dependency on the parent resource is not implied.</span></span> <span data-ttu-id="73264-278">È necessario definirla in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="73264-278">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="73264-279">La sezione resources contiene una matrice delle risorse da distribuire.</span><span class="sxs-lookup"><span data-stu-id="73264-279">The resources section contains an array of the resources to deploy.</span></span> <span data-ttu-id="73264-280">All'interno di ogni risorsa è anche possibile definire una matrice di risorse figlio.</span><span class="sxs-lookup"><span data-stu-id="73264-280">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="73264-281">La sezione resources potrebbe quindi avere una struttura simile a questa:</span><span class="sxs-lookup"><span data-stu-id="73264-281">Therefore, your resources section could have a structure like:</span></span>

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

<span data-ttu-id="73264-282">Per altre informazioni sulla definizione delle risorse figlio, vedere [Impostare il nome e il tipo di una risorsa figlio in un modello di Resource Manager](resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="73264-282">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

<span data-ttu-id="73264-283">L'elemento **condition** specifica se la risorsa viene distribuita.</span><span class="sxs-lookup"><span data-stu-id="73264-283">The **condition** element specifies whether the resource is deployed.</span></span> <span data-ttu-id="73264-284">Il valore di questo elemento restituisce true o false.</span><span class="sxs-lookup"><span data-stu-id="73264-284">The value for this element resolves to true or false.</span></span> <span data-ttu-id="73264-285">Ad esempio, per specificare se viene distribuito un nuovo account di archiviazione, usare:</span><span class="sxs-lookup"><span data-stu-id="73264-285">For example, to specify whether a new storage account is deployed, use:</span></span>

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

<span data-ttu-id="73264-286">Per un esempio di utilizzo di una risorsa nuova o esistente, vedere [Modello di condizione nuovo o esistente](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="73264-286">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="73264-287">Per specificare se una macchina virtuale viene distribuita con una password o una chiave SSH, definire due versioni della macchina virtuale nel modello e utilizzare **condition** per differenziare l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="73264-287">To specify whether a virtual machine is deployed with a password or SSH key, define two versions of the virtual machine in your template and use **condition** to differentiate usage.</span></span> <span data-ttu-id="73264-288">Passare un parametro che specifichi lo scenario da distribuire.</span><span class="sxs-lookup"><span data-stu-id="73264-288">Pass a parameter that specifies which scenario to deploy.</span></span>

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

<span data-ttu-id="73264-289">Per un esempio di utilizzo di una password o di una chiave SSH per la distribuzione di una macchina virtuale, vedere [Modello di condizione basato su nome utente o SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="73264-289">For an example of using a password or SSH key to deploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="outputs"></a><span data-ttu-id="73264-290">Output</span><span class="sxs-lookup"><span data-stu-id="73264-290">Outputs</span></span>
<span data-ttu-id="73264-291">Nella sezione dell'output è possibile specificare i valori restituiti dalla distribuzione.</span><span class="sxs-lookup"><span data-stu-id="73264-291">In the Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="73264-292">Ad esempio, è possibile restituire l'URI per accedere a una risorsa distribuita.</span><span class="sxs-lookup"><span data-stu-id="73264-292">For example, you could return the URI to access a deployed resource.</span></span>

<span data-ttu-id="73264-293">L'esempio seguente illustra la struttura di una definizione di output:</span><span class="sxs-lookup"><span data-stu-id="73264-293">The following example shows the structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="73264-294">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="73264-294">Element name</span></span> | <span data-ttu-id="73264-295">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="73264-295">Required</span></span> | <span data-ttu-id="73264-296">Descrizione</span><span class="sxs-lookup"><span data-stu-id="73264-296">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="73264-297">outputName</span><span class="sxs-lookup"><span data-stu-id="73264-297">outputName</span></span> |<span data-ttu-id="73264-298">Sì</span><span class="sxs-lookup"><span data-stu-id="73264-298">Yes</span></span> |<span data-ttu-id="73264-299">Nome del valore di output.</span><span class="sxs-lookup"><span data-stu-id="73264-299">Name of the output value.</span></span> <span data-ttu-id="73264-300">Deve essere un identificatore JavaScript valido.</span><span class="sxs-lookup"><span data-stu-id="73264-300">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="73264-301">type</span><span class="sxs-lookup"><span data-stu-id="73264-301">type</span></span> |<span data-ttu-id="73264-302">Sì</span><span class="sxs-lookup"><span data-stu-id="73264-302">Yes</span></span> |<span data-ttu-id="73264-303">Tipo del valore di output.</span><span class="sxs-lookup"><span data-stu-id="73264-303">Type of the output value.</span></span> <span data-ttu-id="73264-304">I valori di output supportano gli stessi tipi dei parametri di input del modello.</span><span class="sxs-lookup"><span data-stu-id="73264-304">Output values support the same types as template input parameters.</span></span> |
| <span data-ttu-id="73264-305">value</span><span class="sxs-lookup"><span data-stu-id="73264-305">value</span></span> |<span data-ttu-id="73264-306">Sì</span><span class="sxs-lookup"><span data-stu-id="73264-306">Yes</span></span> |<span data-ttu-id="73264-307">Espressione del linguaggio di modello valutata e restituita come valore di output.</span><span class="sxs-lookup"><span data-stu-id="73264-307">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="73264-308">L'esempio seguente illustra un valore che viene restituito nella sezione dell'output.</span><span class="sxs-lookup"><span data-stu-id="73264-308">The following example shows a value that is returned in the Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="73264-309">Per altre informazioni sull'utilizzo dell'output, vedere [Condivisione dello stato in modelli di Azure Resource Manager](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="73264-309">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="template-limits"></a><span data-ttu-id="73264-310">Limiti del modello</span><span class="sxs-lookup"><span data-stu-id="73264-310">Template limits</span></span>

<span data-ttu-id="73264-311">Limitare le dimensioni del modello a 1 MB e ogni file di parametri a 64 KB.</span><span class="sxs-lookup"><span data-stu-id="73264-311">Limit the size of your template to 1 MB, and each parameter file to 64 KB.</span></span> <span data-ttu-id="73264-312">Il limite di 1 MB si applica allo stato finale del modello dopo che è stato espanso con le definizioni delle risorse iterative e i valori di variabili e parametri.</span><span class="sxs-lookup"><span data-stu-id="73264-312">The 1-MB limit applies to the final state of the template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

<span data-ttu-id="73264-313">Si è anche limitati a:</span><span class="sxs-lookup"><span data-stu-id="73264-313">You are also limited to:</span></span>

* <span data-ttu-id="73264-314">256 parametri</span><span class="sxs-lookup"><span data-stu-id="73264-314">256 parameters</span></span>
* <span data-ttu-id="73264-315">256 variabili</span><span class="sxs-lookup"><span data-stu-id="73264-315">256 variables</span></span>
* <span data-ttu-id="73264-316">800 risorse (incluso il conteggio copie)</span><span class="sxs-lookup"><span data-stu-id="73264-316">800 resources (including copy count)</span></span>
* <span data-ttu-id="73264-317">64 valori di output</span><span class="sxs-lookup"><span data-stu-id="73264-317">64 output values</span></span>
* <span data-ttu-id="73264-318">24.576 caratteri in un'espressione di modello</span><span class="sxs-lookup"><span data-stu-id="73264-318">24,576 characters in a template expression</span></span>

<span data-ttu-id="73264-319">È possibile superare alcuni limiti del modello usando un modello annidato.</span><span class="sxs-lookup"><span data-stu-id="73264-319">You can exceed some template limits by using a nested template.</span></span> <span data-ttu-id="73264-320">Per altre informazioni, vedere [Uso di modelli collegati nella distribuzione di risorse di Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="73264-320">For more information, see [Using linked templates when deploying Azure resources](resource-group-linked-templates.md).</span></span> <span data-ttu-id="73264-321">Per ridurre il numero di parametri, variabili o output, è possibile combinare più valori in un oggetto.</span><span class="sxs-lookup"><span data-stu-id="73264-321">To reduce the number of parameters, variables, or outputs, you can combine several values into an object.</span></span> <span data-ttu-id="73264-322">Per altre informazioni, vedere [Oggetti come parametri](resource-manager-objects-as-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="73264-322">For more information, see [Objects as parameters](resource-manager-objects-as-parameters.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="73264-323">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="73264-323">Next steps</span></span>
* <span data-ttu-id="73264-324">Per visualizzare modelli completi per molti tipi diversi di soluzioni, vedere [Modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="73264-324">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="73264-325">Per informazioni dettagliate sulle funzioni che è possibile usare in un modello, vedere [Funzioni del modello di Azure Resource Manager](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="73264-325">For details about the functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="73264-326">Per unire più modelli durante la distribuzione, vedere [Uso di modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="73264-326">To combine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="73264-327">Potrebbe essere necessario usare le risorse esistenti all'interno di un gruppo di risorse diverso.</span><span class="sxs-lookup"><span data-stu-id="73264-327">You may need to use resources that exist within a different resource group.</span></span> <span data-ttu-id="73264-328">Questo scenario è comune quando si usano account di archiviazione o reti virtuali condivisi tra più gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="73264-328">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="73264-329">Per altre informazioni, vedere la [funzione resourceId](resource-group-template-functions-resource.md#resourceid).</span><span class="sxs-lookup"><span data-stu-id="73264-329">For more information, see the [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
