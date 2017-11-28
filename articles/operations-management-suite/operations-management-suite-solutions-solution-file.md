---
title: soluzioni di gestione aaaCreating Operations Management Suite (OMS) | Documenti Microsoft
description: "Soluzioni di gestione estendono le funzionalità di hello di Operations Management Suite (OMS), fornendo gli scenari di gestione di pacchetti che è possibile aggiungere l'area di lavoro OMS tootheir.  Questo articolo fornisce informazioni dettagliate su come creare toobe di soluzioni di gestione utilizzato nel proprio ambiente o resi disponibili tooyour clienti."
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
ms.openlocfilehash: f408df1b21f519fd1eb2cbeb19cca18f6c4161f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a><span data-ttu-id="9d13a-104">Creazione di una soluzione di gestione in Operations Management Suite (OMS) (anteprima)</span><span class="sxs-lookup"><span data-stu-id="9d13a-104">Creating a management solution file in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="9d13a-105">Questa è una documentazione preliminare per la creazione di soluzioni di gestione in OMS attualmente disponibili in versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="9d13a-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="9d13a-106">Qualsiasi schema descritto di seguito è soggetto toochange.</span><span class="sxs-lookup"><span data-stu-id="9d13a-106">Any schema described below is subject toochange.</span></span>  

<span data-ttu-id="9d13a-107">Le soluzioni di gestione in Operations Management Suite (OMS) vengono implementate come [modelli di Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="9d13a-107">Management solutions in Operations Management Suite (OMS) are implemented as [Resource Manager templates](../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>  <span data-ttu-id="9d13a-108">attività principali Hello per apprendere come tooauthor soluzioni di gestione, è fondamentale comprendere come troppo[creare un modello](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9d13a-108">hello main task in learning how tooauthor management solutions is learning how too[author a template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="9d13a-109">Questo articolo fornisce informazioni dettagliate univoci dei modelli utilizzati per le soluzioni e come risorse tipica soluzione tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="9d13a-109">This article provides unique details of templates used for solutions and how tooconfigure typical solution resources.</span></span>


## <a name="tools"></a><span data-ttu-id="9d13a-110">Strumenti</span><span class="sxs-lookup"><span data-stu-id="9d13a-110">Tools</span></span>

<span data-ttu-id="9d13a-111">È possibile utilizzare qualsiasi toowork editor di testo con i file di soluzione, ma è consigliabile l'utilizzo delle funzionalità di hello fornite in Visual Studio o codice di Visual Studio, come descritto in hello seguenti articoli.</span><span class="sxs-lookup"><span data-stu-id="9d13a-111">You can use any text editor toowork with solution files, but we recommend leveraging hello features provided in Visual Studio or Visual Studio Code as described in hello following articles.</span></span>

- [<span data-ttu-id="9d13a-112">Creazione e distribuzione di gruppi di risorse di Azure tramite Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9d13a-112">Creating and deploying Azure resource groups through Visual Studio</span></span>](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [<span data-ttu-id="9d13a-113">Utilizzo dei modelli di Azure Resource Manager nel codice di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9d13a-113">Working with Azure Resource Manager Templates in Visual Studio Code</span></span>](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a><span data-ttu-id="9d13a-114">Structure</span><span class="sxs-lookup"><span data-stu-id="9d13a-114">Structure</span></span>
<span data-ttu-id="9d13a-115">struttura di base di un file di soluzione di gestione Hello è hello stesso come un [modello di gestione risorse](../azure-resource-manager/resource-group-authoring-templates.md#template-format) cui è indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9d13a-115">hello basic structure of a management solution file is hello same as a [Resource Manager Template](../azure-resource-manager/resource-group-authoring-templates.md#template-format) which is as follows.</span></span>  <span data-ttu-id="9d13a-116">Hello sezioni seguenti vengono descritti gli elementi di livello superiore di hello ed e il relativo contenuto in una soluzione.</span><span class="sxs-lookup"><span data-stu-id="9d13a-116">Each of hello sections below describes hello top level elements and and their contents in a solution.</span></span>  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a><span data-ttu-id="9d13a-117">parameters</span><span class="sxs-lookup"><span data-stu-id="9d13a-117">Parameters</span></span>
<span data-ttu-id="9d13a-118">[I parametri](../azure-resource-manager/resource-group-authoring-templates.md#parameters) sono valori richiesti dall'utente hello quando installano la soluzione di gestione hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) are values that you require from hello user when they install hello management solution.</span></span>  <span data-ttu-id="9d13a-119">Ci sono parametri standard comuni a tutte le soluzioni ed è possibile aggiungere altri parametri in base a quanto necessario per la soluzione specifica.</span><span class="sxs-lookup"><span data-stu-id="9d13a-119">There are standard parameters that all solutions will have, and you can add additional parameters as required for your particular solution.</span></span>  <span data-ttu-id="9d13a-120">Modo gli utenti forniscono i valori dei parametri quando si installa la soluzione dipenderà determinato parametro hello e la modalità di installazione soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-120">How users will provide parameter values when they install your solution will depend on hello particular parameter and how hello solution is being installed.</span></span>

<span data-ttu-id="9d13a-121">Quando un utente installa la soluzione di gestione tramite hello [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) o [modelli di avvio rapido di Azure](operations-management-suite-solutions.md#finding-and-installing-management-solutions) sono tooselect richiesta un [OMS dell'area di lavoro e account di automazione ](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span><span class="sxs-lookup"><span data-stu-id="9d13a-121">When a user installs your management solution through hello [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) or [Azure QuickStart templates](operations-management-suite-solutions.md#finding-and-installing-management-solutions) they are prompted tooselect an [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span></span>  <span data-ttu-id="9d13a-122">Questi sono valori hello toopopulate utilizzato di ciascun parametro hello standard.</span><span class="sxs-lookup"><span data-stu-id="9d13a-122">These are used toopopulate hello values of each of hello standard parameters.</span></span>  <span data-ttu-id="9d13a-123">Hello utente non vengono richieste toodirectly fornire valori per parametri standard hello, ma sono valori tooprovide richiesta per i parametri aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="9d13a-123">hello user is not prompted toodirectly provide values for hello standard parameters, but they are prompted tooprovide values for any additional parameters.</span></span>

<span data-ttu-id="9d13a-124">Quando utente hello installa la soluzione [un altro metodo](operations-management-suite-solutions.md#finding-and-installing-management-solutions), devono specificare un valore per tutti i parametri standard e tutti i parametri aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="9d13a-124">When hello user installs your solution [another method](operations-management-suite-solutions.md#finding-and-installing-management-solutions), they must provide a value for all standard parameters and all additional parameters.</span></span>

<span data-ttu-id="9d13a-125">Di seguito è illustrato un parametro di esempio.</span><span class="sxs-lookup"><span data-stu-id="9d13a-125">A sample parameter is shown below.</span></span>  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

<span data-ttu-id="9d13a-126">Hello nella tabella seguente vengono descritti gli attributi di hello di un parametro.</span><span class="sxs-lookup"><span data-stu-id="9d13a-126">hello following table describes hello attributes of a parameter.</span></span>

| <span data-ttu-id="9d13a-127">Attributo</span><span class="sxs-lookup"><span data-stu-id="9d13a-127">Attribute</span></span> | <span data-ttu-id="9d13a-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9d13a-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9d13a-129">type</span><span class="sxs-lookup"><span data-stu-id="9d13a-129">type</span></span> |<span data-ttu-id="9d13a-130">Tipo di dati per il parametro hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-130">Data type for hello parameter.</span></span> <span data-ttu-id="9d13a-131">controllo di input Hello visualizzato per l'utente hello dipende dal tipo di dati hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-131">hello input control displayed for hello user depends on hello data type.</span></span><br><br><span data-ttu-id="9d13a-132">bool - Casella di riepilogo a discesa</span><span class="sxs-lookup"><span data-stu-id="9d13a-132">bool - Drop down box</span></span><br><span data-ttu-id="9d13a-133">string - Casella di testo</span><span class="sxs-lookup"><span data-stu-id="9d13a-133">string - Text box</span></span><br><span data-ttu-id="9d13a-134">int - Casella di testo</span><span class="sxs-lookup"><span data-stu-id="9d13a-134">int - Text box</span></span><br><span data-ttu-id="9d13a-135">securestring - Campo della password</span><span class="sxs-lookup"><span data-stu-id="9d13a-135">securestring - Password field</span></span><br> |
| <span data-ttu-id="9d13a-136">category</span><span class="sxs-lookup"><span data-stu-id="9d13a-136">category</span></span> |<span data-ttu-id="9d13a-137">Categoria facoltativo per il parametro hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-137">Optional category for hello parameter.</span></span>  <span data-ttu-id="9d13a-138">Parametri in hello stessa categoria vengono raggruppati insieme.</span><span class="sxs-lookup"><span data-stu-id="9d13a-138">Parameters in hello same category are grouped together.</span></span> |
| <span data-ttu-id="9d13a-139">control</span><span class="sxs-lookup"><span data-stu-id="9d13a-139">control</span></span> |<span data-ttu-id="9d13a-140">Funzionalità aggiuntiva per i parametri di stringa.</span><span class="sxs-lookup"><span data-stu-id="9d13a-140">Additional functionality for string parameters.</span></span><br><br><span data-ttu-id="9d13a-141">datetime - Viene visualizzato un controllo Datetime.</span><span class="sxs-lookup"><span data-stu-id="9d13a-141">datetime - Datetime control is displayed.</span></span><br><span data-ttu-id="9d13a-142">GUID - valore Guid viene generato automaticamente e non viene visualizzato il parametro hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-142">guid - Guid value is automatically generated, and hello parameter is not displayed.</span></span> |
| <span data-ttu-id="9d13a-143">description</span><span class="sxs-lookup"><span data-stu-id="9d13a-143">description</span></span> |<span data-ttu-id="9d13a-144">Descrizione facoltativa per il parametro hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-144">Optional description for hello parameter.</span></span>  <span data-ttu-id="9d13a-145">Visualizzato in un parametro di toohello informazioni successivo fumetto.</span><span class="sxs-lookup"><span data-stu-id="9d13a-145">Displayed in an information balloon next toohello parameter.</span></span> |

### <a name="standard-parameters"></a><span data-ttu-id="9d13a-146">Parametri standard</span><span class="sxs-lookup"><span data-stu-id="9d13a-146">Standard parameters</span></span>
<span data-ttu-id="9d13a-147">Hello nella tabella seguente elenca hello parametri standard per tutte le soluzioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="9d13a-147">hello following table lists hello standard parameters for all management solutions.</span></span>  <span data-ttu-id="9d13a-148">Questi valori vengono popolati per utente hello anziché richiedere il loro quando la soluzione viene installata dal hello Azure Marketplace o Guida rapida di modelli.</span><span class="sxs-lookup"><span data-stu-id="9d13a-148">These values are populated for hello user instead of prompting for them when your solution is installed from hello Azure Marketplace or Quickstart templates.</span></span>  <span data-ttu-id="9d13a-149">utente Hello deve fornire valori per tali se soluzione hello viene installato con un altro metodo.</span><span class="sxs-lookup"><span data-stu-id="9d13a-149">hello user must provide values for them if hello solution is installed with another method.</span></span>

> [!NOTE]
> <span data-ttu-id="9d13a-150">interfaccia utente di Hello nei modelli di Azure Marketplace e Guida introduttiva hello prevede che i nomi di parametro hello nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-150">hello user interface in hello Azure Marketplace and Quickstart templates is expecting hello parameter names in hello table.</span></span>  <span data-ttu-id="9d13a-151">Se si utilizzano nomi di parametro diversi quindi verrà richiesto all'utente hello e non viene automaticamente popolate.</span><span class="sxs-lookup"><span data-stu-id="9d13a-151">If you use different parameter names then hello user will be prompted for them, and they will not be automatically populated.</span></span>
>
>

| <span data-ttu-id="9d13a-152">.</span><span class="sxs-lookup"><span data-stu-id="9d13a-152">Parameter</span></span> | <span data-ttu-id="9d13a-153">Tipo</span><span class="sxs-lookup"><span data-stu-id="9d13a-153">Type</span></span> | <span data-ttu-id="9d13a-154">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9d13a-154">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="9d13a-155">accountName</span><span class="sxs-lookup"><span data-stu-id="9d13a-155">accountName</span></span> |<span data-ttu-id="9d13a-156">string</span><span class="sxs-lookup"><span data-stu-id="9d13a-156">string</span></span> |<span data-ttu-id="9d13a-157">Nome dell'account di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9d13a-157">Azure Automation account name.</span></span> |
| <span data-ttu-id="9d13a-158">pricingTier</span><span class="sxs-lookup"><span data-stu-id="9d13a-158">pricingTier</span></span> |<span data-ttu-id="9d13a-159">string</span><span class="sxs-lookup"><span data-stu-id="9d13a-159">string</span></span> |<span data-ttu-id="9d13a-160">Piano tariffario dell'area di lavoro di Log Analytics e dell'account di Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9d13a-160">Pricing tier of both Log Analytics workspace and Azure Automation account.</span></span> |
| <span data-ttu-id="9d13a-161">regionId</span><span class="sxs-lookup"><span data-stu-id="9d13a-161">regionId</span></span> |<span data-ttu-id="9d13a-162">string</span><span class="sxs-lookup"><span data-stu-id="9d13a-162">string</span></span> |<span data-ttu-id="9d13a-163">Area di hello account di automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9d13a-163">Region of hello Azure Automation account.</span></span> |
| <span data-ttu-id="9d13a-164">solutionName</span><span class="sxs-lookup"><span data-stu-id="9d13a-164">solutionName</span></span> |<span data-ttu-id="9d13a-165">string</span><span class="sxs-lookup"><span data-stu-id="9d13a-165">string</span></span> |<span data-ttu-id="9d13a-166">Nome della soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-166">Name of hello solution.</span></span>  <span data-ttu-id="9d13a-167">Se si distribuisce la soluzione tramite i modelli di avvio rapido, è necessario definire solutionName come un parametro che consente di definire una stringa invece richiedere hello utente toospecify uno.</span><span class="sxs-lookup"><span data-stu-id="9d13a-167">If you are deploying your solution through Quickstart templates, then you should define solutionName as a parameter so you can define a string instead requiring hello user toospecify one.</span></span> |
| <span data-ttu-id="9d13a-168">workspaceName</span><span class="sxs-lookup"><span data-stu-id="9d13a-168">workspaceName</span></span> |<span data-ttu-id="9d13a-169">string</span><span class="sxs-lookup"><span data-stu-id="9d13a-169">string</span></span> |<span data-ttu-id="9d13a-170">Nome dell'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="9d13a-170">Log Analytics workspace name.</span></span> |
| <span data-ttu-id="9d13a-171">workspaceRegionId</span><span class="sxs-lookup"><span data-stu-id="9d13a-171">workspaceRegionId</span></span> |<span data-ttu-id="9d13a-172">string</span><span class="sxs-lookup"><span data-stu-id="9d13a-172">string</span></span> |<span data-ttu-id="9d13a-173">Area dell'area di lavoro Log Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-173">Region of hello Log Analytics workspace.</span></span> |


<span data-ttu-id="9d13a-174">Di seguito è la struttura hello parametri hello standard che è possibile copiare e incollare il file di soluzione.</span><span class="sxs-lookup"><span data-stu-id="9d13a-174">Following is hello structure of hello standard parameters that you can copy and paste into your solution file.</span></span>  

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
                   "description": "Region of hello Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of hello Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


<span data-ttu-id="9d13a-175">Si fa riferimento a valori tooparameter in altri elementi di soluzione hello con sintassi hello **parametri ('parameter name')**.</span><span class="sxs-lookup"><span data-stu-id="9d13a-175">You refer tooparameter values in other elements of hello solution with hello syntax **parameters('parameter name')**.</span></span>  <span data-ttu-id="9d13a-176">Ad esempio, tooaccess hello Nome area di lavoro, si utilizzerebbe **parameters('workspaceName')**</span><span class="sxs-lookup"><span data-stu-id="9d13a-176">For example, tooaccess hello workspace name, you would use **parameters('workspaceName')**</span></span>

## <a name="variables"></a><span data-ttu-id="9d13a-177">variables</span><span class="sxs-lookup"><span data-stu-id="9d13a-177">Variables</span></span>
<span data-ttu-id="9d13a-178">[Le variabili](../azure-resource-manager/resource-group-authoring-templates.md#variables) sono valori che verrà utilizzato nel resto di hello della soluzione di gestione di hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-178">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are values that you will use in hello rest of hello management solution.</span></span>  <span data-ttu-id="9d13a-179">Questi valori non sono esposti toohello utente installa la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-179">These values are not exposed toohello user installing hello solution.</span></span>  <span data-ttu-id="9d13a-180">Si tratta di autore hello tooprovide prevista con un'unica posizione in cui è possibile gestire i valori che possono essere utilizzati più volte nella soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-180">They are intended tooprovide hello author with a single location where they can manage values that may be used multiple times throughout hello solution.</span></span> <span data-ttu-id="9d13a-181">È necessario inserire qualsiasi soluzione tooyour specifico di valori nelle variabili come toohard anziché la codifica hello **risorse** elemento.</span><span class="sxs-lookup"><span data-stu-id="9d13a-181">You should put any values specific tooyour solution in variables as opposed toohard coding them in hello **resources** element.</span></span>  <span data-ttu-id="9d13a-182">Questo rende più leggibile il codice hello e consente tooeasily modificare questi valori nelle versioni successive.</span><span class="sxs-lookup"><span data-stu-id="9d13a-182">This makes hello code more readable and allows you tooeasily change these values in later versions.</span></span>

<span data-ttu-id="9d13a-183">Di seguito è riportato un esempio di elemento **variables** con i parametri tipici usati nelle soluzioni.</span><span class="sxs-lookup"><span data-stu-id="9d13a-183">Following is an example of a **variables** element with typical parameters used in solutions.</span></span>

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="9d13a-184">Si fa riferimento a valori toovariable tramite la soluzione hello con sintassi hello **variabili ('variable name')**.</span><span class="sxs-lookup"><span data-stu-id="9d13a-184">You refer toovariable values through hello solution with hello syntax **variables('variable name')**.</span></span>  <span data-ttu-id="9d13a-185">Ad esempio, tooaccess hello variabile SolutionName, si utilizzerebbe **variables('SolutionName')**.</span><span class="sxs-lookup"><span data-stu-id="9d13a-185">For example, tooaccess hello SolutionName variable, you would use **variables('SolutionName')**.</span></span>

<span data-ttu-id="9d13a-186">È possibile anche definire variabili complesse che moltiplicano set di valori;</span><span class="sxs-lookup"><span data-stu-id="9d13a-186">You can also define complex variables that multiple sets of values.</span></span>  <span data-ttu-id="9d13a-187">risultano particolarmente utili nelle soluzioni di gestione in cui si definiscono più proprietà per diversi tipi di risorse.</span><span class="sxs-lookup"><span data-stu-id="9d13a-187">These are particularly useful in management solutions where you are defining multiple properties for different types of resources.</span></span>  <span data-ttu-id="9d13a-188">Ad esempio, è Impossibile ristrutturare le variabili della soluzione hello illustrate in precedenza toohello seguente.</span><span class="sxs-lookup"><span data-stu-id="9d13a-188">For example, you could restructure hello solution variables shown above toohello following.</span></span>

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="9d13a-189">In questo caso, si fa riferimento toovariable valori tramite la soluzione hello con sintassi hello **variables('variable name').property**.</span><span class="sxs-lookup"><span data-stu-id="9d13a-189">In this case, you refer toovariable values through hello solution with hello syntax **variables('variable name').property**.</span></span>  <span data-ttu-id="9d13a-190">Ad esempio, tooaccess hello variabile nome di soluzione, si utilizzerebbe **variables('Solution'). Nome**.</span><span class="sxs-lookup"><span data-stu-id="9d13a-190">For example, tooaccess hello Solution Name variable, you would use **variables('Solution').Name**.</span></span>

## <a name="resources"></a><span data-ttu-id="9d13a-191">Risorse</span><span class="sxs-lookup"><span data-stu-id="9d13a-191">Resources</span></span>
<span data-ttu-id="9d13a-192">[Risorse](../azure-resource-manager/resource-group-authoring-templates.md#resources) definire hello diverse risorse che installerà e configurerà la soluzione di gestione.</span><span class="sxs-lookup"><span data-stu-id="9d13a-192">[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) define hello different resources that your management solution will install and configure.</span></span>  <span data-ttu-id="9d13a-193">Questo sarà hello più grande e la parte più complesse del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-193">This will be hello largest and most complex portion of hello template.</span></span>  <span data-ttu-id="9d13a-194">È possibile ottenere struttura hello e una descrizione completa degli elementi di risorsa in [modelli Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span><span class="sxs-lookup"><span data-stu-id="9d13a-194">You can get hello structure and complete description of resource elements in [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span></span>  <span data-ttu-id="9d13a-195">In altri articoli di questa documentazione sono descritti i tipi di risorse definiti più comunemente.</span><span class="sxs-lookup"><span data-stu-id="9d13a-195">Different resources that you will typically define are detailed in other articles in this documentation.</span></span> 


### <a name="dependencies"></a><span data-ttu-id="9d13a-196">Dipendenze</span><span class="sxs-lookup"><span data-stu-id="9d13a-196">Dependencies</span></span>
<span data-ttu-id="9d13a-197">Hello **dependsOn** elementi specifica un [dipendenza](../azure-resource-manager/resource-group-define-dependencies.md) in un'altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="9d13a-197">hello **dependsOn** elements specifies a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on another resource.</span></span>  <span data-ttu-id="9d13a-198">Quando si installa la soluzione hello, non viene creata una risorsa fino a quando tutte le relative dipendenze sono state create.</span><span class="sxs-lookup"><span data-stu-id="9d13a-198">When hello solution is installed, a resource is not created until all of its dependencies have been created.</span></span>  <span data-ttu-id="9d13a-199">La soluzione potrebbe ad esempio [avviare un runbook](operations-management-suite-solutions-resources-automation.md#runbooks) quando viene installata usando una [risorsa processo](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span><span class="sxs-lookup"><span data-stu-id="9d13a-199">For example, your solution might [start a runbook](operations-management-suite-solutions-resources-automation.md#runbooks) when it's installed using a [job resource](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span></span>  <span data-ttu-id="9d13a-200">risorsa di processo Hello sarebbe dipende hello runbook risorsa toomake runbook hello sia stata creata prima che venga creato il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-200">hello job resource would be dependent on hello runbook resource toomake sure that hello runbook is created before hello job is created.</span></span>

### <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="9d13a-201">Area di lavoro OMS e account di Automazione</span><span class="sxs-lookup"><span data-stu-id="9d13a-201">OMS workspace and Automation account</span></span>
<span data-ttu-id="9d13a-202">Soluzioni di gestione richiedono un [area di lavoro OMS](../log-analytics/log-analytics-manage-access.md) toocontain visualizzazioni e un [account di automazione](../automation/automation-security-overview.md#automation-account-overview) toocontain runbook e le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="9d13a-202">Management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) toocontain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks and related resources.</span></span>  <span data-ttu-id="9d13a-203">Questi devono essere disponibili prima hello risorse nella soluzione hello vengono create e non devono essere definite nella soluzione hello stessa.</span><span class="sxs-lookup"><span data-stu-id="9d13a-203">These must be available before hello resources in hello solution are created and should not be defined in hello solution itself.</span></span>  <span data-ttu-id="9d13a-204">utente Hello verrà [specificare un account e l'area di lavoro](operations-management-suite-solutions.md#oms-workspace-and-automation-account) quando si distribuisce la soluzione, ma come autore hello è necessario considerare hello seguenti punti.</span><span class="sxs-lookup"><span data-stu-id="9d13a-204">hello user will [specify a workspace and account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) when they deploy your solution, but as hello author you should consider hello following points.</span></span>

## <a name="solution-resource"></a><span data-ttu-id="9d13a-205">Risorse della soluzione</span><span class="sxs-lookup"><span data-stu-id="9d13a-205">Solution resource</span></span>
<span data-ttu-id="9d13a-206">Ogni soluzione richiede una voce di risorsa in hello **risorse** elemento che definisce una soluzione di hello stessa.</span><span class="sxs-lookup"><span data-stu-id="9d13a-206">Each solution requires a resource entry in hello **resources** element that defines hello solution itself.</span></span>  <span data-ttu-id="9d13a-207">Ciò avrà un tipo di **Microsoft.OperationsManagement/solutions** e hello seguente struttura.</span><span class="sxs-lookup"><span data-stu-id="9d13a-207">This will have a type of **Microsoft.OperationsManagement/solutions** and have hello following structure.</span></span> <span data-ttu-id="9d13a-208">Ciò include [parametri standard](#parameters) e [variabili](#variables) che sono di proprietà in genere utilizzate toodefine della soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-208">This includes [standard parameters](#parameters) and [variables](#variables) that are typically used toodefine properties of hello solution.</span></span>


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




### <a name="dependencies"></a><span data-ttu-id="9d13a-209">Dipendenze</span><span class="sxs-lookup"><span data-stu-id="9d13a-209">Dependencies</span></span>
<span data-ttu-id="9d13a-210">Hello soluzione risorsa deve avere un [dipendenza](../azure-resource-manager/resource-group-define-dependencies.md) in tutte le altre risorse nella soluzione hello poiché devono tooexist prima di creare soluzioni hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-210">hello solution resource must have a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on every other resource in hello solution since they need tooexist before hello solution can be created.</span></span>  <span data-ttu-id="9d13a-211">Questo scopo, aggiungere una voce per ogni risorsa in hello **dependsOn** elemento.</span><span class="sxs-lookup"><span data-stu-id="9d13a-211">You do this by adding an entry for each resource in hello **dependsOn** element.</span></span>

### <a name="properties"></a><span data-ttu-id="9d13a-212">Proprietà</span><span class="sxs-lookup"><span data-stu-id="9d13a-212">Properties</span></span>
<span data-ttu-id="9d13a-213">Hello soluzione hello alcune proprietà della risorsa in hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="9d13a-213">hello solution resource has hello properties in hello following table.</span></span>  <span data-ttu-id="9d13a-214">Sono incluse risorse hello a cui fa riferimento e contenuti da soluzione hello che definisce la modalità di gestione risorse di hello dopo l'installazione della soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-214">This includes hello resources referenced and contained by hello solution which defines how hello resource is managed after hello solution is installed.</span></span>  <span data-ttu-id="9d13a-215">Ogni risorsa nella soluzione hello dovrebbe essere elencato in entrambi hello **referencedResources** o hello **containedResources** proprietà.</span><span class="sxs-lookup"><span data-stu-id="9d13a-215">Each resource in hello solution should be listed in either hello **referencedResources** or hello **containedResources** property.</span></span>

| <span data-ttu-id="9d13a-216">Proprietà</span><span class="sxs-lookup"><span data-stu-id="9d13a-216">Property</span></span> | <span data-ttu-id="9d13a-217">Description</span><span class="sxs-lookup"><span data-stu-id="9d13a-217">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9d13a-218">workspaceResourceId</span><span class="sxs-lookup"><span data-stu-id="9d13a-218">workspaceResourceId</span></span> |<span data-ttu-id="9d13a-219">ID dell'area di lavoro di Log Analitica hello in forma di hello  *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<nome area di lavoro\>*.</span><span class="sxs-lookup"><span data-stu-id="9d13a-219">ID of hello Log Analytics workspace in hello form *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Workspace Name\>*.</span></span> |
| <span data-ttu-id="9d13a-220">referencedResources</span><span class="sxs-lookup"><span data-stu-id="9d13a-220">referencedResources</span></span> |<span data-ttu-id="9d13a-221">Elenco delle risorse nella soluzione hello che non devono essere rimossi quando la soluzione hello viene rimossa.</span><span class="sxs-lookup"><span data-stu-id="9d13a-221">List of resources in hello solution that should not be removed when hello solution is removed.</span></span> |
| <span data-ttu-id="9d13a-222">containedResources</span><span class="sxs-lookup"><span data-stu-id="9d13a-222">containedResources</span></span> |<span data-ttu-id="9d13a-223">Elenco delle risorse nella soluzione hello che devono essere rimossi quando la soluzione hello viene rimossa.</span><span class="sxs-lookup"><span data-stu-id="9d13a-223">List of resources in hello solution that should be removed when hello solution is removed.</span></span> |

<span data-ttu-id="9d13a-224">esempio Hello precedente è una soluzione con un runbook, a una pianificazione e visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="9d13a-224">hello example  above is for a solution with a runbook, a schedule, and view.</span></span>  <span data-ttu-id="9d13a-225">pianificazione di Hello e runbook sono *riferimento* in hello **proprietà** elemento in modo non vengono rimossi quando la soluzione hello viene rimosso.</span><span class="sxs-lookup"><span data-stu-id="9d13a-225">hello schedule and runbook are *referenced* in hello  **properties**  element so they are not removed when hello solution is removed.</span></span>  <span data-ttu-id="9d13a-226">visualizzazione di Hello è *contenuti* viene rimosso quando viene rimossa la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-226">hello view is *contained* so it is removed when hello solution is removed.</span></span>

### <a name="plan"></a><span data-ttu-id="9d13a-227">Pianificazione</span><span class="sxs-lookup"><span data-stu-id="9d13a-227">Plan</span></span>
<span data-ttu-id="9d13a-228">Hello **piano** entità della risorsa di soluzione hello dispone di proprietà hello in hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="9d13a-228">hello **plan** entity of hello solution resource has hello properties in hello following table.</span></span>

| <span data-ttu-id="9d13a-229">Proprietà</span><span class="sxs-lookup"><span data-stu-id="9d13a-229">Property</span></span> | <span data-ttu-id="9d13a-230">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9d13a-230">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9d13a-231">name</span><span class="sxs-lookup"><span data-stu-id="9d13a-231">name</span></span> |<span data-ttu-id="9d13a-232">Nome della soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-232">Name of hello solution.</span></span> |
| <span data-ttu-id="9d13a-233">version</span><span class="sxs-lookup"><span data-stu-id="9d13a-233">version</span></span> |<span data-ttu-id="9d13a-234">Versione della soluzione hello, come determinato dall'autore hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-234">Version of hello solution as determined by hello author.</span></span> |
| <span data-ttu-id="9d13a-235">product</span><span class="sxs-lookup"><span data-stu-id="9d13a-235">product</span></span> |<span data-ttu-id="9d13a-236">Soluzione di hello tooidentify stringa univoca.</span><span class="sxs-lookup"><span data-stu-id="9d13a-236">Unique string tooidentify hello solution.</span></span> |
| <span data-ttu-id="9d13a-237">publisher</span><span class="sxs-lookup"><span data-stu-id="9d13a-237">publisher</span></span> |<span data-ttu-id="9d13a-238">Server di pubblicazione della soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="9d13a-238">Publisher of hello solution.</span></span> |



## <a name="sample"></a><span data-ttu-id="9d13a-239">Esempio</span><span class="sxs-lookup"><span data-stu-id="9d13a-239">Sample</span></span>
<span data-ttu-id="9d13a-240">È possibile visualizzare esempi di file della soluzione con una risorsa di soluzione in hello posizioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="9d13a-240">You can view samples of solution files with a solution resource at hello following locations.</span></span>

- [<span data-ttu-id="9d13a-241">Risorse di Automazione</span><span class="sxs-lookup"><span data-stu-id="9d13a-241">Automation resources</span></span>](operations-management-suite-solutions-resources-automation.md#sample)
- [<span data-ttu-id="9d13a-242">Risorse di ricerca e di avviso</span><span class="sxs-lookup"><span data-stu-id="9d13a-242">Search and alert resources</span></span>](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a><span data-ttu-id="9d13a-243">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9d13a-243">Next steps</span></span>
* <span data-ttu-id="9d13a-244">[Aggiungere avvisi e le ricerche salvate](operations-management-suite-solutions-resources-searches-alerts.md) tooyour soluzione di gestione.</span><span class="sxs-lookup"><span data-stu-id="9d13a-244">[Add saved searches and alerts](operations-management-suite-solutions-resources-searches-alerts.md) tooyour management solution.</span></span>
* <span data-ttu-id="9d13a-245">[Aggiungere visualizzazioni](operations-management-suite-solutions-resources-views.md) tooyour soluzione di gestione.</span><span class="sxs-lookup"><span data-stu-id="9d13a-245">[Add views](operations-management-suite-solutions-resources-views.md) tooyour management solution.</span></span>
* <span data-ttu-id="9d13a-246">[Aggiungere i runbook e altre risorse di automazione](operations-management-suite-solutions-resources-automation.md) tooyour soluzione di gestione.</span><span class="sxs-lookup"><span data-stu-id="9d13a-246">[Add runbooks and other Automation resources](operations-management-suite-solutions-resources-automation.md) tooyour management solution.</span></span>
* <span data-ttu-id="9d13a-247">Informazioni sul supporto di hello [modelli Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9d13a-247">Learn hello details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="9d13a-248">Cercare i [modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates) per esempi di modelli di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9d13a-248">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
