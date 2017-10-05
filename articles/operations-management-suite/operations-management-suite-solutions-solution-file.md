---
title: Creazione di soluzioni di gestione in Operations Management Suite (OMS) | Documentazione Microsoft
description: "Le soluzioni di gestione estendono la funzionalità di Operations Management Suite (OMS) offrendo scenari di gestione in pacchetto che i clienti possono aggiungere all'area di lavoro OMS.  In questo articolo vengono fornite informazioni dettagliate su come creare soluzioni di gestione da usare nel proprio ambiente o da rendere disponibili per i propri clienti."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/30/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee3462c13101d18921dc488b08c79e1e4e02ff3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a><span data-ttu-id="f5910-104">Creazione di una soluzione di gestione in Operations Management Suite (OMS) (anteprima)</span><span class="sxs-lookup"><span data-stu-id="f5910-104">Creating a management solution file in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="f5910-105">Questa è una documentazione preliminare per la creazione di soluzioni di gestione in OMS attualmente disponibili in versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="f5910-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="f5910-106">Qualsiasi schema descritto di seguito è soggetto a modifiche.</span><span class="sxs-lookup"><span data-stu-id="f5910-106">Any schema described below is subject to change.</span></span>  

<span data-ttu-id="f5910-107">Le soluzioni di gestione in Operations Management Suite (OMS) vengono implementate come [modelli di Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="f5910-107">Management solutions in Operations Management Suite (OMS) are implemented as [Resource Manager templates](../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>  <span data-ttu-id="f5910-108">L'attività principale della creazione di soluzioni di gestione consiste nel [creare un modello](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f5910-108">The main task in learning how to author management solutions is learning how to [author a template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="f5910-109">Questo articolo fornisce informazioni dettagliate sui modelli usati per le soluzioni e illustra come configurare le risorse tipiche di una soluzione.</span><span class="sxs-lookup"><span data-stu-id="f5910-109">This article provides unique details of templates used for solutions and how to configure typical solution resources.</span></span>


## <a name="tools"></a><span data-ttu-id="f5910-110">Strumenti</span><span class="sxs-lookup"><span data-stu-id="f5910-110">Tools</span></span>

<span data-ttu-id="f5910-111">È possibile usare qualsiasi editor di testo per interagire con i file della soluzione, ma si consiglia di avvalersi delle funzionalità disponibili in Visual Studio o Visual Studio Code, come descritto negli articoli seguenti.</span><span class="sxs-lookup"><span data-stu-id="f5910-111">You can use any text editor to work with solution files, but we recommend leveraging the features provided in Visual Studio or Visual Studio Code as described in the following articles.</span></span>

- [<span data-ttu-id="f5910-112">Creazione e distribuzione di gruppi di risorse di Azure tramite Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f5910-112">Creating and deploying Azure resource groups through Visual Studio</span></span>](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [<span data-ttu-id="f5910-113">Utilizzo dei modelli di Azure Resource Manager nel codice di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f5910-113">Working with Azure Resource Manager Templates in Visual Studio Code</span></span>](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a><span data-ttu-id="f5910-114">Structure</span><span class="sxs-lookup"><span data-stu-id="f5910-114">Structure</span></span>
<span data-ttu-id="f5910-115">La struttura di base di un file di una soluzione di gestione corrisponde a quella di un [modello di Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#template-format), come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="f5910-115">The basic structure of a management solution file is the same as a [Resource Manager Template](../azure-resource-manager/resource-group-authoring-templates.md#template-format) which is as follows.</span></span>  <span data-ttu-id="f5910-116">Ognuna delle sezioni seguenti descrive gli elementi principali di una soluzione e i relativi contenuti.</span><span class="sxs-lookup"><span data-stu-id="f5910-116">Each of the sections below describes the top level elements and and their contents in a solution.</span></span>  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a><span data-ttu-id="f5910-117">Parametri</span><span class="sxs-lookup"><span data-stu-id="f5910-117">Parameters</span></span>
<span data-ttu-id="f5910-118">I [parametri](../azure-resource-manager/resource-group-authoring-templates.md#parameters) sono valori richiesti all'utente al momento dell'installazione della soluzione di gestione.</span><span class="sxs-lookup"><span data-stu-id="f5910-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) are values that you require from the user when they install the management solution.</span></span>  <span data-ttu-id="f5910-119">Ci sono parametri standard comuni a tutte le soluzioni ed è possibile aggiungere altri parametri in base a quanto necessario per la soluzione specifica.</span><span class="sxs-lookup"><span data-stu-id="f5910-119">There are standard parameters that all solutions will have, and you can add additional parameters as required for your particular solution.</span></span>  <span data-ttu-id="f5910-120">Il modo in cui gli utenti forniranno i valori dei parametri quando installano la soluzione dipende dal parametro specifico e dalla modalità di installazione della soluzione.</span><span class="sxs-lookup"><span data-stu-id="f5910-120">How users will provide parameter values when they install your solution will depend on the particular parameter and how the solution is being installed.</span></span>

<span data-ttu-id="f5910-121">Quando un utente installa la soluzione di gestione tramite [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) o i [modelli di avvio rapido di Azure](operations-management-suite-solutions.md#finding-and-installing-management-solutions), viene chiesto di selezionare un'[area di lavoro OMS e un account di Automazione](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span><span class="sxs-lookup"><span data-stu-id="f5910-121">When a user installs your management solution through the [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) or [Azure QuickStart templates](operations-management-suite-solutions.md#finding-and-installing-management-solutions) they are prompted to select an [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span></span>  <span data-ttu-id="f5910-122">Questi elementi vengono usati per popolare i valori di ognuno dei parametri standard.</span><span class="sxs-lookup"><span data-stu-id="f5910-122">These are used to populate the values of each of the standard parameters.</span></span>  <span data-ttu-id="f5910-123">All'utente non viene chiesto di fornire direttamente i valori per i parametri standard, ma viene chiesto di fornire i valori per eventuali parametri aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="f5910-123">The user is not prompted to directly provide values for the standard parameters, but they are prompted to provide values for any additional parameters.</span></span>

<span data-ttu-id="f5910-124">Quando l'utente installa la soluzione con un [altro metodo](operations-management-suite-solutions.md#finding-and-installing-management-solutions), deve specificare un valore per tutti i parametri standard e tutti i parametri aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="f5910-124">When the user installs your solution [another method](operations-management-suite-solutions.md#finding-and-installing-management-solutions), they must provide a value for all standard parameters and all additional parameters.</span></span>

<span data-ttu-id="f5910-125">Di seguito è illustrato un parametro di esempio.</span><span class="sxs-lookup"><span data-stu-id="f5910-125">A sample parameter is shown below.</span></span>  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

<span data-ttu-id="f5910-126">La tabella seguente descrive gli attributi di un parametro.</span><span class="sxs-lookup"><span data-stu-id="f5910-126">The following table describes the attributes of a parameter.</span></span>

| <span data-ttu-id="f5910-127">Attributo</span><span class="sxs-lookup"><span data-stu-id="f5910-127">Attribute</span></span> | <span data-ttu-id="f5910-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f5910-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f5910-129">type</span><span class="sxs-lookup"><span data-stu-id="f5910-129">type</span></span> |<span data-ttu-id="f5910-130">Tipo di dati per il parametro.</span><span class="sxs-lookup"><span data-stu-id="f5910-130">Data type for the parameter.</span></span> <span data-ttu-id="f5910-131">Il controllo di input visualizzato per l'utente dipende dal tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="f5910-131">The input control displayed for the user depends on the data type.</span></span><br><br><span data-ttu-id="f5910-132">bool - Casella di riepilogo a discesa</span><span class="sxs-lookup"><span data-stu-id="f5910-132">bool - Drop down box</span></span><br><span data-ttu-id="f5910-133">string - Casella di testo</span><span class="sxs-lookup"><span data-stu-id="f5910-133">string - Text box</span></span><br><span data-ttu-id="f5910-134">int - Casella di testo</span><span class="sxs-lookup"><span data-stu-id="f5910-134">int - Text box</span></span><br><span data-ttu-id="f5910-135">securestring - Campo della password</span><span class="sxs-lookup"><span data-stu-id="f5910-135">securestring - Password field</span></span><br> |
| <span data-ttu-id="f5910-136">category</span><span class="sxs-lookup"><span data-stu-id="f5910-136">category</span></span> |<span data-ttu-id="f5910-137">Categoria facoltativa per il parametro.</span><span class="sxs-lookup"><span data-stu-id="f5910-137">Optional category for the parameter.</span></span>  <span data-ttu-id="f5910-138">I parametri della stessa categoria vengono raggruppati insieme.</span><span class="sxs-lookup"><span data-stu-id="f5910-138">Parameters in the same category are grouped together.</span></span> |
| <span data-ttu-id="f5910-139">control</span><span class="sxs-lookup"><span data-stu-id="f5910-139">control</span></span> |<span data-ttu-id="f5910-140">Funzionalità aggiuntiva per i parametri di stringa.</span><span class="sxs-lookup"><span data-stu-id="f5910-140">Additional functionality for string parameters.</span></span><br><br><span data-ttu-id="f5910-141">datetime - Viene visualizzato un controllo Datetime.</span><span class="sxs-lookup"><span data-stu-id="f5910-141">datetime - Datetime control is displayed.</span></span><br><span data-ttu-id="f5910-142">guid - Il valore Guid viene generato automaticamente e il parametro non viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="f5910-142">guid - Guid value is automatically generated, and the parameter is not displayed.</span></span> |
| <span data-ttu-id="f5910-143">description</span><span class="sxs-lookup"><span data-stu-id="f5910-143">description</span></span> |<span data-ttu-id="f5910-144">Descrizione facoltativa del parametro.</span><span class="sxs-lookup"><span data-stu-id="f5910-144">Optional description for the parameter.</span></span>  <span data-ttu-id="f5910-145">Viene visualizzata in un fumetto di informazioni accanto al parametro.</span><span class="sxs-lookup"><span data-stu-id="f5910-145">Displayed in an information balloon next to the parameter.</span></span> |

### <a name="standard-parameters"></a><span data-ttu-id="f5910-146">Parametri standard</span><span class="sxs-lookup"><span data-stu-id="f5910-146">Standard parameters</span></span>
<span data-ttu-id="f5910-147">La tabella seguente elenca i parametri standard per tutte le soluzioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="f5910-147">The following table lists the standard parameters for all management solutions.</span></span>  <span data-ttu-id="f5910-148">Quando la soluzione viene installata da Azure Marketplace o dai modelli di avvio rapido, questi valori vengono popolati automaticamente per l'utente senza che venga chiesto di immetterli.</span><span class="sxs-lookup"><span data-stu-id="f5910-148">These values are populated for the user instead of prompting for them when your solution is installed from the Azure Marketplace or Quickstart templates.</span></span>  <span data-ttu-id="f5910-149">L'utente deve fornire i valori se la soluzione viene installata con un altro metodo.</span><span class="sxs-lookup"><span data-stu-id="f5910-149">The user must provide values for them if the solution is installed with another method.</span></span>

> [!NOTE]
> <span data-ttu-id="f5910-150">L'interfaccia utente in Azure Marketplace e nei modelli di avvio rapido prevede i nomi di parametro indicati nella tabella.</span><span class="sxs-lookup"><span data-stu-id="f5910-150">The user interface in the Azure Marketplace and Quickstart templates is expecting the parameter names in the table.</span></span>  <span data-ttu-id="f5910-151">Se si usano nomi di parametro diversi, all'utente verrà chiesto di specificarli e non verranno popolati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f5910-151">If you use different parameter names then the user will be prompted for them, and they will not be automatically populated.</span></span>
>
>

| <span data-ttu-id="f5910-152">Parametro</span><span class="sxs-lookup"><span data-stu-id="f5910-152">Parameter</span></span> | <span data-ttu-id="f5910-153">Tipo</span><span class="sxs-lookup"><span data-stu-id="f5910-153">Type</span></span> | <span data-ttu-id="f5910-154">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f5910-154">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="f5910-155">accountName</span><span class="sxs-lookup"><span data-stu-id="f5910-155">accountName</span></span> |<span data-ttu-id="f5910-156">string</span><span class="sxs-lookup"><span data-stu-id="f5910-156">string</span></span> |<span data-ttu-id="f5910-157">Nome dell'account di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5910-157">Azure Automation account name.</span></span> |
| <span data-ttu-id="f5910-158">pricingTier</span><span class="sxs-lookup"><span data-stu-id="f5910-158">pricingTier</span></span> |<span data-ttu-id="f5910-159">string</span><span class="sxs-lookup"><span data-stu-id="f5910-159">string</span></span> |<span data-ttu-id="f5910-160">Piano tariffario dell'area di lavoro di Log Analytics e dell'account di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5910-160">Pricing tier of both Log Analytics workspace and Azure Automation account.</span></span> |
| <span data-ttu-id="f5910-161">regionId</span><span class="sxs-lookup"><span data-stu-id="f5910-161">regionId</span></span> |<span data-ttu-id="f5910-162">string</span><span class="sxs-lookup"><span data-stu-id="f5910-162">string</span></span> |<span data-ttu-id="f5910-163">Area dell'account di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5910-163">Region of the Azure Automation account.</span></span> |
| <span data-ttu-id="f5910-164">solutionName</span><span class="sxs-lookup"><span data-stu-id="f5910-164">solutionName</span></span> |<span data-ttu-id="f5910-165">string</span><span class="sxs-lookup"><span data-stu-id="f5910-165">string</span></span> |<span data-ttu-id="f5910-166">Nome della soluzione.</span><span class="sxs-lookup"><span data-stu-id="f5910-166">Name of the solution.</span></span>  <span data-ttu-id="f5910-167">Se si distribuisce la soluzione tramite modelli di avvio rapido, è necessario definire solutionName come un parametro, in modo da poter definire una stringa anziché richiedere all'utente di specificarne una.</span><span class="sxs-lookup"><span data-stu-id="f5910-167">If you are deploying your solution through Quickstart templates, then you should define solutionName as a parameter so you can define a string instead requiring the user to specify one.</span></span> |
| <span data-ttu-id="f5910-168">workspaceName</span><span class="sxs-lookup"><span data-stu-id="f5910-168">workspaceName</span></span> |<span data-ttu-id="f5910-169">string</span><span class="sxs-lookup"><span data-stu-id="f5910-169">string</span></span> |<span data-ttu-id="f5910-170">Nome dell'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f5910-170">Log Analytics workspace name.</span></span> |
| <span data-ttu-id="f5910-171">workspaceRegionId</span><span class="sxs-lookup"><span data-stu-id="f5910-171">workspaceRegionId</span></span> |<span data-ttu-id="f5910-172">string</span><span class="sxs-lookup"><span data-stu-id="f5910-172">string</span></span> |<span data-ttu-id="f5910-173">Area dell'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f5910-173">Region of the Log Analytics workspace.</span></span> |


<span data-ttu-id="f5910-174">Di seguito viene mostrata la struttura dei parametri standard, che è possibile copiare e incollare nel file della soluzione.</span><span class="sxs-lookup"><span data-stu-id="f5910-174">Following is the structure of the standard parameters that you can copy and paste into your solution file.</span></span>  

    "parameters": {
        "workspaceName": {
            "type": "string",
            "metadata": {
                "description": "A valid Log Analytics workspace name"
            }
        },
        "accountName": {
               "type": "string",
               "metadata": {
                   "description": "A valid Azure Automation account name"
               }
        },
        "workspaceRegionId": {
               "type": "string",
               "metadata": {
                   "description": "Region of the Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of the Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


<span data-ttu-id="f5910-175">Per fare riferimento ai valori di parametro negli altri elementi della soluzione si usa la sintassi **parameters('nome parametro')**.</span><span class="sxs-lookup"><span data-stu-id="f5910-175">You refer to parameter values in other elements of the solution with the syntax **parameters('parameter name')**.</span></span>  <span data-ttu-id="f5910-176">Per accedere, ad esempio, al nome dell'area di lavoro, usare **parameters('workspaceName')**</span><span class="sxs-lookup"><span data-stu-id="f5910-176">For example, to access the workspace name, you would use **parameters('workspaceName')**</span></span>

## <a name="variables"></a><span data-ttu-id="f5910-177">Variabili</span><span class="sxs-lookup"><span data-stu-id="f5910-177">Variables</span></span>
<span data-ttu-id="f5910-178">Le [variabili](../azure-resource-manager/resource-group-authoring-templates.md#variables) sono valori che verranno usati nella parte rimanente della soluzione di gestione.</span><span class="sxs-lookup"><span data-stu-id="f5910-178">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are values that you will use in the rest of the management solution.</span></span>  <span data-ttu-id="f5910-179">Questi valori non sono esposti all'utente che esegue l'installazione della soluzione.</span><span class="sxs-lookup"><span data-stu-id="f5910-179">These values are not exposed to the user installing the solution.</span></span>  <span data-ttu-id="f5910-180">La loro funzione è quella di offrire all'autore un'unica posizione in cui gestire i valori che possono essere usati più volte all'interno della soluzione.</span><span class="sxs-lookup"><span data-stu-id="f5910-180">They are intended to provide the author with a single location where they can manage values that may be used multiple times throughout the solution.</span></span> <span data-ttu-id="f5910-181">È consigliabile inserire eventuali valori specifici della soluzione in variabili anziché impostarli come hardcoded nell'elemento **resources**.</span><span class="sxs-lookup"><span data-stu-id="f5910-181">You should put any values specific to your solution in variables as opposed to hard coding them in the **resources** element.</span></span>  <span data-ttu-id="f5910-182">In questo modo, il codice risulta più leggibile ed è possibile modificare facilmente questi valori nelle versioni successive.</span><span class="sxs-lookup"><span data-stu-id="f5910-182">This makes the code more readable and allows you to easily change these values in later versions.</span></span>

<span data-ttu-id="f5910-183">Di seguito è riportato un esempio di elemento **variables** con i parametri tipici usati nelle soluzioni.</span><span class="sxs-lookup"><span data-stu-id="f5910-183">Following is an example of a **variables** element with typical parameters used in solutions.</span></span>

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="f5910-184">Per fare riferimento ai valori di variabile all'interno della soluzione si usa la sintassi **variables('nome variabile')**.</span><span class="sxs-lookup"><span data-stu-id="f5910-184">You refer to variable values through the solution with the syntax **variables('variable name')**.</span></span>  <span data-ttu-id="f5910-185">Per accedere, ad esempio, alla variabile SolutionName, usare **variables('SolutionName')**.</span><span class="sxs-lookup"><span data-stu-id="f5910-185">For example, to access the SolutionName variable, you would use **variables('SolutionName')**.</span></span>

<span data-ttu-id="f5910-186">È possibile anche definire variabili complesse che moltiplicano set di valori;</span><span class="sxs-lookup"><span data-stu-id="f5910-186">You can also define complex variables that multiple sets of values.</span></span>  <span data-ttu-id="f5910-187">risultano particolarmente utili nelle soluzioni di gestione in cui si definiscono più proprietà per diversi tipi di risorse.</span><span class="sxs-lookup"><span data-stu-id="f5910-187">These are particularly useful in management solutions where you are defining multiple properties for different types of resources.</span></span>  <span data-ttu-id="f5910-188">È possibile, ad esempio, ristrutturare come indicato di seguito le variabili di soluzione illustrate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f5910-188">For example, you could restructure the solution variables shown above to the following.</span></span>

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="f5910-189">In questo caso, per fare riferimento ai valori di variabile all'interno della soluzione è possibile usare la sintassi **variables('nome variabile').proprietà**.</span><span class="sxs-lookup"><span data-stu-id="f5910-189">In this case, you refer to variable values through the solution with the syntax **variables('variable name').property**.</span></span>  <span data-ttu-id="f5910-190">Per accedere, ad esempio, alla variabile SolutionName, è necessario usare **variables('Solution').Name**.</span><span class="sxs-lookup"><span data-stu-id="f5910-190">For example, to access the Solution Name variable, you would use **variables('Solution').Name**.</span></span>

## <a name="resources"></a><span data-ttu-id="f5910-191">Risorse</span><span class="sxs-lookup"><span data-stu-id="f5910-191">Resources</span></span>
<span data-ttu-id="f5910-192">Le [risorse](../azure-resource-manager/resource-group-authoring-templates.md#resources) definiscono i vari tipi di risorse che la soluzione di gestione installerà e configurerà.</span><span class="sxs-lookup"><span data-stu-id="f5910-192">[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) define the different resources that your management solution will install and configure.</span></span>  <span data-ttu-id="f5910-193">Si tratta della parte più estesa e complessa del modello.</span><span class="sxs-lookup"><span data-stu-id="f5910-193">This will be the largest and most complex portion of the template.</span></span>  <span data-ttu-id="f5910-194">È possibile ottenere informazioni sulla struttura e una descrizione completa degli elementi di risorsa in [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span><span class="sxs-lookup"><span data-stu-id="f5910-194">You can get the structure and complete description of resource elements in [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span></span>  <span data-ttu-id="f5910-195">In altri articoli di questa documentazione sono descritti i tipi di risorse definiti più comunemente.</span><span class="sxs-lookup"><span data-stu-id="f5910-195">Different resources that you will typically define are detailed in other articles in this documentation.</span></span> 


### <a name="dependencies"></a><span data-ttu-id="f5910-196">Dipendenze</span><span class="sxs-lookup"><span data-stu-id="f5910-196">Dependencies</span></span>
<span data-ttu-id="f5910-197">L'elemento **dependsOn** specifica una [dipendenza](../azure-resource-manager/resource-group-define-dependencies.md) da un'altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="f5910-197">The **dependsOn** elements specifies a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on another resource.</span></span>  <span data-ttu-id="f5910-198">Quando si installa la soluzione, una risorsa viene creata solo dopo che sono state create tutte le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="f5910-198">When the solution is installed, a resource is not created until all of its dependencies have been created.</span></span>  <span data-ttu-id="f5910-199">La soluzione potrebbe ad esempio [avviare un runbook](operations-management-suite-solutions-resources-automation.md#runbooks) quando viene installata usando una [risorsa processo](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span><span class="sxs-lookup"><span data-stu-id="f5910-199">For example, your solution might [start a runbook](operations-management-suite-solutions-resources-automation.md#runbooks) when it's installed using a [job resource](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span></span>  <span data-ttu-id="f5910-200">La risorsa processo dipenderà dalla risorsa runbook, per assicurarsi che il runbook venga creato prima del processo.</span><span class="sxs-lookup"><span data-stu-id="f5910-200">The job resource would be dependent on the runbook resource to make sure that the runbook is created before the job is created.</span></span>

### <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="f5910-201">Area di lavoro OMS e account di Automazione</span><span class="sxs-lookup"><span data-stu-id="f5910-201">OMS workspace and Automation account</span></span>
<span data-ttu-id="f5910-202">Le soluzioni di gestione richiedono un'[area di lavoro OMS](../log-analytics/log-analytics-manage-access.md) per contenere le viste e un [account di Automazione](../automation/automation-security-overview.md#automation-account-overview) per contenere i runbook e le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="f5910-202">Management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) to contain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) to contain runbooks and related resources.</span></span>  <span data-ttu-id="f5910-203">Questi elementi devono essere disponibili prima della creazione delle risorse nella soluzione e non devono essere definiti nella soluzione stessa.</span><span class="sxs-lookup"><span data-stu-id="f5910-203">These must be available before the resources in the solution are created and should not be defined in the solution itself.</span></span>  <span data-ttu-id="f5910-204">L'utente [specificherà un'area di lavoro e un account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) quando distribuisce la soluzione, ma l'autore della soluzione deve tenere presente quanto segue.</span><span class="sxs-lookup"><span data-stu-id="f5910-204">The user will [specify a workspace and account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) when they deploy your solution, but as the author you should consider the following points.</span></span>

## <a name="solution-resource"></a><span data-ttu-id="f5910-205">Risorse della soluzione</span><span class="sxs-lookup"><span data-stu-id="f5910-205">Solution resource</span></span>
<span data-ttu-id="f5910-206">Per ogni soluzione è necessario specificare una risorsa nell'elemento **resources** che definisce la soluzione stessa.</span><span class="sxs-lookup"><span data-stu-id="f5910-206">Each solution requires a resource entry in the **resources** element that defines the solution itself.</span></span>  <span data-ttu-id="f5910-207">La risorsa sarà di tipo **Microsoft.OperationsManagement/solutions** e avrà la struttura seguente.</span><span class="sxs-lookup"><span data-stu-id="f5910-207">This will have a type of **Microsoft.OperationsManagement/solutions** and have the following structure.</span></span> <span data-ttu-id="f5910-208">Sono inclusi i [parametri standard](#parameters) e le [variabili](#variables) generalmente usati per definire le proprietà della soluzione.</span><span class="sxs-lookup"><span data-stu-id="f5910-208">This includes [standard parameters](#parameters) and [variables](#variables) that are typically used to define properties of the solution.</span></span>


    {
      "name": "[concat(variables('Solution').Name, '[' ,parameters('workspacename'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
        <list-of-resources>
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
        "referencedResources": [
            <list-of-referenced-resources>
        ],
        "containedResources": [
            <list-of-contained-resources>
        ]
      },
      "plan": {
        "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
        "Version": "[variables('Solution').Version]",
        "product": "[variables('ProductName')]",
        "publisher": "[variables('Solution').Publisher]",
        "promotionCode": ""
      }
    }




### <a name="dependencies"></a><span data-ttu-id="f5910-209">Dipendenze</span><span class="sxs-lookup"><span data-stu-id="f5910-209">Dependencies</span></span>
<span data-ttu-id="f5910-210">La risorsa soluzione deve avere una [dipendenza](../azure-resource-manager/resource-group-define-dependencies.md) da ogni altra risorsa nella soluzione, perché ogni risorsa deve esistere affinché la soluzione possa essere creata.</span><span class="sxs-lookup"><span data-stu-id="f5910-210">The solution resource must have a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on every other resource in the solution since they need to exist before the solution can be created.</span></span>  <span data-ttu-id="f5910-211">A tale scopo, aggiungere una voce per ogni risorsa nell'elemento **dependsOn**.</span><span class="sxs-lookup"><span data-stu-id="f5910-211">You do this by adding an entry for each resource in the **dependsOn** element.</span></span>

### <a name="properties"></a><span data-ttu-id="f5910-212">Proprietà</span><span class="sxs-lookup"><span data-stu-id="f5910-212">Properties</span></span>
<span data-ttu-id="f5910-213">La risorsa della soluzione ha le proprietà descritte nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="f5910-213">The solution resource has the properties in the following table.</span></span>  <span data-ttu-id="f5910-214">Sono incluse le risorse cui viene fatto riferimento dalla soluzione e incluse nella soluzione che definisce come viene gestita la risorsa dopo l'installazione della soluzione.</span><span class="sxs-lookup"><span data-stu-id="f5910-214">This includes the resources referenced and contained by the solution which defines how the resource is managed after the solution is installed.</span></span>  <span data-ttu-id="f5910-215">Ogni risorsa nella soluzione deve essere presente nella proprietà **referencedResources** o **containedResources**.</span><span class="sxs-lookup"><span data-stu-id="f5910-215">Each resource in the solution should be listed in either the **referencedResources** or the **containedResources** property.</span></span>

| <span data-ttu-id="f5910-216">Proprietà</span><span class="sxs-lookup"><span data-stu-id="f5910-216">Property</span></span> | <span data-ttu-id="f5910-217">Description</span><span class="sxs-lookup"><span data-stu-id="f5910-217">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f5910-218">workspaceResourceId</span><span class="sxs-lookup"><span data-stu-id="f5910-218">workspaceResourceId</span></span> |<span data-ttu-id="f5910-219">ID dell'area di lavoro Log Analytics nel formato *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Nome area di lavoro\>*.</span><span class="sxs-lookup"><span data-stu-id="f5910-219">ID of the Log Analytics workspace in the form *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Workspace Name\>*.</span></span> |
| <span data-ttu-id="f5910-220">referencedResources</span><span class="sxs-lookup"><span data-stu-id="f5910-220">referencedResources</span></span> |<span data-ttu-id="f5910-221">Elenco delle risorse nella soluzione che non devono essere rimosse quando la soluzione viene rimossa.</span><span class="sxs-lookup"><span data-stu-id="f5910-221">List of resources in the solution that should not be removed when the solution is removed.</span></span> |
| <span data-ttu-id="f5910-222">containedResources</span><span class="sxs-lookup"><span data-stu-id="f5910-222">containedResources</span></span> |<span data-ttu-id="f5910-223">Elenco delle risorse nella soluzione che devono essere rimosse quando la soluzione viene rimossa.</span><span class="sxs-lookup"><span data-stu-id="f5910-223">List of resources in the solution that should be removed when the solution is removed.</span></span> |

<span data-ttu-id="f5910-224">L'esempio precedente si riferisce a una soluzione con un runbook, una pianificazione e una vista.</span><span class="sxs-lookup"><span data-stu-id="f5910-224">The example  above is for a solution with a runbook, a schedule, and view.</span></span>  <span data-ttu-id="f5910-225">Poiché sono presenti *riferimenti* ad essi nell'elemento **properties**, la pianificazione e il runbook non vengono rimossi quando la soluzione viene rimossa.</span><span class="sxs-lookup"><span data-stu-id="f5910-225">The schedule and runbook are *referenced* in the  **properties**  element so they are not removed when the solution is removed.</span></span>  <span data-ttu-id="f5910-226">La vista che è invece *contenuta* viene rimossa quando la soluzione viene rimossa.</span><span class="sxs-lookup"><span data-stu-id="f5910-226">The view is *contained* so it is removed when the solution is removed.</span></span>

### <a name="plan"></a><span data-ttu-id="f5910-227">Pianificazione</span><span class="sxs-lookup"><span data-stu-id="f5910-227">Plan</span></span>
<span data-ttu-id="f5910-228">L'entità **plan** della risorsa soluzione ha le proprietà descritte nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="f5910-228">The **plan** entity of the solution resource has the properties in the following table.</span></span>

| <span data-ttu-id="f5910-229">Proprietà</span><span class="sxs-lookup"><span data-stu-id="f5910-229">Property</span></span> | <span data-ttu-id="f5910-230">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f5910-230">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f5910-231">name</span><span class="sxs-lookup"><span data-stu-id="f5910-231">name</span></span> |<span data-ttu-id="f5910-232">Nome della soluzione.</span><span class="sxs-lookup"><span data-stu-id="f5910-232">Name of the solution.</span></span> |
| <span data-ttu-id="f5910-233">version</span><span class="sxs-lookup"><span data-stu-id="f5910-233">version</span></span> |<span data-ttu-id="f5910-234">Versione della soluzione determinata dall'autore.</span><span class="sxs-lookup"><span data-stu-id="f5910-234">Version of the solution as determined by the author.</span></span> |
| <span data-ttu-id="f5910-235">product</span><span class="sxs-lookup"><span data-stu-id="f5910-235">product</span></span> |<span data-ttu-id="f5910-236">Stringa univoca che identifica la soluzione.</span><span class="sxs-lookup"><span data-stu-id="f5910-236">Unique string to identify the solution.</span></span> |
| <span data-ttu-id="f5910-237">publisher</span><span class="sxs-lookup"><span data-stu-id="f5910-237">publisher</span></span> |<span data-ttu-id="f5910-238">Autore della soluzione.</span><span class="sxs-lookup"><span data-stu-id="f5910-238">Publisher of the solution.</span></span> |



## <a name="sample"></a><span data-ttu-id="f5910-239">Esempio</span><span class="sxs-lookup"><span data-stu-id="f5910-239">Sample</span></span>
<span data-ttu-id="f5910-240">Esempi di file di soluzioni con una risorsa "soluzione" sono disponibili negli articoli seguenti.</span><span class="sxs-lookup"><span data-stu-id="f5910-240">You can view samples of solution files with a solution resource at the following locations.</span></span>

- [<span data-ttu-id="f5910-241">Risorse di Automazione</span><span class="sxs-lookup"><span data-stu-id="f5910-241">Automation resources</span></span>](operations-management-suite-solutions-resources-automation.md#sample)
- [<span data-ttu-id="f5910-242">Risorse di ricerca e di avviso</span><span class="sxs-lookup"><span data-stu-id="f5910-242">Search and alert resources</span></span>](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a><span data-ttu-id="f5910-243">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f5910-243">Next steps</span></span>
* <span data-ttu-id="f5910-244">[Aggiungere ricerche salvate e avvisi](operations-management-suite-solutions-resources-searches-alerts.md) alla soluzione di gestione.</span><span class="sxs-lookup"><span data-stu-id="f5910-244">[Add saved searches and alerts](operations-management-suite-solutions-resources-searches-alerts.md) to your management solution.</span></span>
* <span data-ttu-id="f5910-245">[Aggiungere viste](operations-management-suite-solutions-resources-views.md) alla soluzione di gestione.</span><span class="sxs-lookup"><span data-stu-id="f5910-245">[Add views](operations-management-suite-solutions-resources-views.md) to your management solution.</span></span>
* <span data-ttu-id="f5910-246">[Aggiungere runbook e altre risorse di automazione](operations-management-suite-solutions-resources-automation.md) alla soluzione di gestione.</span><span class="sxs-lookup"><span data-stu-id="f5910-246">[Add runbooks and other Automation resources](operations-management-suite-solutions-resources-automation.md) to your management solution.</span></span>
* <span data-ttu-id="f5910-247">Informazioni dettagliate sulla [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f5910-247">Learn the details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="f5910-248">Cercare i [modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates) per esempi di modelli di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f5910-248">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
