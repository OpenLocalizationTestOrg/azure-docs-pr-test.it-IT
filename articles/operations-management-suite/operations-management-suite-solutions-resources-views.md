---
title: Viste nelle soluzioni di gestione di Operations Management Suite (OMS) | Microsoft Docs
description: "Le soluzioni di gestione in Operations Management Suite (OMS) includono in genere una o più viste per visualizzare i dati.  Questo articolo descrive come esportare una vista creata da Progettazione viste e includerla in una soluzione di gestione. "
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 570b278c-2d47-4e5a-9828-7f01f31ddf8c
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 533b5564a805e0b41f2b1a4ad92e12b133220952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="views-in-operations-management-suite-oms-management-solutions-preview"></a><span data-ttu-id="a4038-104">Viste nelle soluzioni di gestione di Operations Management Suite (OMS) (anteprima)</span><span class="sxs-lookup"><span data-stu-id="a4038-104">Views in Operations Management Suite (OMS) management solutions (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="a4038-105">Questa è una documentazione preliminare per la creazione di soluzioni di gestione in OMS attualmente disponibili in versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="a4038-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="a4038-106">Qualsiasi schema descritto di seguito è soggetto a modifiche.</span><span class="sxs-lookup"><span data-stu-id="a4038-106">Any schema described below is subject to change.</span></span>    
>
>

<span data-ttu-id="a4038-107">Le [soluzioni di gestione in Operations Management Suite (OMS)](operations-management-suite-solutions.md) includono in genere una o più viste per visualizzare i dati.</span><span class="sxs-lookup"><span data-stu-id="a4038-107">[Management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions.md) will typically include one or more views to visualize data.</span></span>  <span data-ttu-id="a4038-108">Questo articolo descrive come esportare una vista creata da [Progettazione viste](../log-analytics/log-analytics-view-designer.md) e includerla in una soluzione di gestione.</span><span class="sxs-lookup"><span data-stu-id="a4038-108">This article describes how to export a view created by the [View Designer](../log-analytics/log-analytics-view-designer.md) and include it in a management solution.</span></span>  

> [!NOTE]
> <span data-ttu-id="a4038-109">Gli esempi in questo articolo usano parametri e variabili che sono richiesti o comuni nelle soluzioni di gestione e che sono descritti in [Creazione di soluzioni di gestione in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="a4038-109">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="a4038-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a4038-110">Prerequisites</span></span>
<span data-ttu-id="a4038-111">Questo articolo presuppone che si abbia già familiarità con le modalità di [creazione di una soluzione di gestione](operations-management-suite-solutions-creating.md) e la struttura di un file di soluzione.</span><span class="sxs-lookup"><span data-stu-id="a4038-111">This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of a solution file.</span></span>

## <a name="overview"></a><span data-ttu-id="a4038-112">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a4038-112">Overview</span></span>
<span data-ttu-id="a4038-113">Per includere una vista in una soluzione di gestione, si crea una **risorsa** per la vista nel [file di soluzione](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="a4038-113">To include a view in a management solution, you create a **resource** for it in the [solution file](operations-management-suite-solutions-creating.md).</span></span>  <span data-ttu-id="a4038-114">In genere, tuttavia, il codice JSON che descrive la configurazione dettagliata della vista è complesso e l'autore tipico di una soluzione probabilmente non è in grado di crearlo manualmente.</span><span class="sxs-lookup"><span data-stu-id="a4038-114">The JSON that describes the view's detailed configuration is typically complex though and not something that a typical solution author would be able to create manually.</span></span>  <span data-ttu-id="a4038-115">Il metodo più comune consiste nel creare la vista usando [Progettazione viste](../log-analytics/log-analytics-view-designer.md), esportarla e quindi aggiungere la sua configurazione dettagliata alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="a4038-115">The most common method is to create the view using the [View Designer](../log-analytics/log-analytics-view-designer.md), export it, and then add its detailed configuration to the solution.</span></span>

<span data-ttu-id="a4038-116">I passaggi di base per aggiungere una vista a una soluzione sono i seguenti.</span><span class="sxs-lookup"><span data-stu-id="a4038-116">The basic steps to add a view to a solution are as follows.</span></span>  <span data-ttu-id="a4038-117">Ogni passaggio viene descritto in modo più dettagliato nelle sezioni successive.</span><span class="sxs-lookup"><span data-stu-id="a4038-117">Each step is described in further detail in the sections below.</span></span>

1. <span data-ttu-id="a4038-118">Esportare la vista in un file.</span><span class="sxs-lookup"><span data-stu-id="a4038-118">Export the view to a file.</span></span>
2. <span data-ttu-id="a4038-119">Creare la risorsa vista nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="a4038-119">Create the view resource in the solution.</span></span>
3. <span data-ttu-id="a4038-120">Aggiungere i dettagli della vista.</span><span class="sxs-lookup"><span data-stu-id="a4038-120">Add the view details.</span></span>

## <a name="export-the-view-to-a-file"></a><span data-ttu-id="a4038-121">Esportare la vista in un file</span><span class="sxs-lookup"><span data-stu-id="a4038-121">Export the view to a file</span></span>
<span data-ttu-id="a4038-122">Seguire le istruzioni in [Progettazione viste di Log Analytics](../log-analytics/log-analytics-view-designer.md) per esportare una vista in un file.</span><span class="sxs-lookup"><span data-stu-id="a4038-122">Follow the instructions at [Log Analytics View Designer](../log-analytics/log-analytics-view-designer.md) to export a view to a file.</span></span>  <span data-ttu-id="a4038-123">Il file esportato sarà nel formato JSON con gli stessi [elementi del file di soluzione](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="a4038-123">The exported file will be in JSON format with the same [elements as the solution file](operations-management-suite-solutions-solution-file.md).</span></span>  

<span data-ttu-id="a4038-124">L'elemento **resources** del file della vista avrà una risorsa di tipo **Microsoft.OperationalInsights/workspaces** che rappresenta l'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="a4038-124">The **resources** element of the view file will have a resource with a type of **Microsoft.OperationalInsights/workspaces** that represents the OMS workspace.</span></span>  <span data-ttu-id="a4038-125">Questo elemento avrà un sottoelemento di tipo **views** che rappresenta la vista e contiene la configurazione dettagliata.</span><span class="sxs-lookup"><span data-stu-id="a4038-125">This element will have a subelement with a type of **views** that represents the view and contains its detailed configuration.</span></span>  <span data-ttu-id="a4038-126">Sarà necessario copiare i dettagli di questo elemento e incollarli nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="a4038-126">You will copy the details of this element and then copy it into your solution.</span></span>

## <a name="create-the-view-resource-in-the-solution"></a><span data-ttu-id="a4038-127">Creare la risorsa vista nella soluzione</span><span class="sxs-lookup"><span data-stu-id="a4038-127">Create the view resource in the solution</span></span>
<span data-ttu-id="a4038-128">Aggiungere la risorsa vista seguente nell'elemento **resources** del file di soluzione.</span><span class="sxs-lookup"><span data-stu-id="a4038-128">Add the following view resource to the **resources** element of your solution file.</span></span>  <span data-ttu-id="a4038-129">Vengono usate le variabili descritte di seguito, che è necessario aggiungere.</span><span class="sxs-lookup"><span data-stu-id="a4038-129">This uses variables that are described below that you must also add.</span></span>  <span data-ttu-id="a4038-130">Si noti che le proprietà **Dashboard** e **OverviewTile** sono segnaposto che verranno sovrascritti con le proprietà corrispondenti del file della vista esportato.</span><span class="sxs-lookup"><span data-stu-id="a4038-130">Note that the **Dashboard** and **OverviewTile** properties are placeholders that you will overwrite with the corresponding properties from the exported view file.</span></span>

    {
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
        "type": "Microsoft.OperationalInsights/workspaces/views",
        "location": "[parameters('workspaceregionId')]",
        "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
        "dependson": [
            ],
        "properties": {
            "Id": "[variables('ViewName')]",
            "Name": "[variables('ViewName')]",
            "DisplayName": "[variables('ViewName')]",
            "Description": "",
            "Author": "[variables('ViewAuthor')]",
            "Source": "Local",
            "Dashboard": ,
            "OverviewTile":
        }
    }

<span data-ttu-id="a4038-131">Aggiungere le variabili seguenti all'elemento variables del file di soluzione e sostituire i valori con quelli della soluzione.</span><span class="sxs-lookup"><span data-stu-id="a4038-131">Add the following variables to the variables element of the solution file and replace the values to those for your solution.</span></span>

    "LogAnalyticsApiVersion": "2015-11-01-preview",
    "ViewAuthor": "Your name."
    "ViewDescription": "Optional description of the view."
    "ViewName": "Provide a name for the view here."


<span data-ttu-id="a4038-132">Si noti che è possibile copiare l'intera risorsa vista dal file della vista esportato, ma è necessario apportare le modifiche seguenti per consentirne il funzionamento nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="a4038-132">Note that you could copy the entire view resource from your exported view file, but you would need to make the following changes for it to work in your solution.</span></span>  

* <span data-ttu-id="a4038-133">Il parametro **type** della risorsa vista deve essere modificato da **views** a **Microsoft.OperationalInsights/workspaces**.</span><span class="sxs-lookup"><span data-stu-id="a4038-133">The **type** for the view resource needs to be changed from **views** to **Microsoft.OperationalInsights/workspaces**.</span></span>
* <span data-ttu-id="a4038-134">La proprietà **name** della risorsa vista deve essere modificata per includere il nome dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="a4038-134">The **name** property for the view resource needs to be changed to include the workspace name.</span></span>
* <span data-ttu-id="a4038-135">La dipendenza dall'area di lavoro deve essere rimossa perché la risorsa area di lavoro non è definita nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="a4038-135">The dependency on the workspace needs to be removed since the workspace resource isn't defined in the solution.</span></span>
* <span data-ttu-id="a4038-136">La proprietà **DisplayName** deve essere aggiunta alla vista.</span><span class="sxs-lookup"><span data-stu-id="a4038-136">**DisplayName** property needs to be added to the view.</span></span>  <span data-ttu-id="a4038-137">I valori di **Id**, **Name** e **DisplayName** devono corrispondere.</span><span class="sxs-lookup"><span data-stu-id="a4038-137">The **Id**, **Name**, and **DisplayName** must all match.</span></span>
* <span data-ttu-id="a4038-138">I nomi dei parametri devono essere modificati in modo da corrispondere al set di parametri richiesto.</span><span class="sxs-lookup"><span data-stu-id="a4038-138">Parameter names must be changed to match the required set of parameters.</span></span>
* <span data-ttu-id="a4038-139">Le variabili devono essere definite nella soluzione e usate nelle proprietà appropriate.</span><span class="sxs-lookup"><span data-stu-id="a4038-139">Variables should be defined in the solution and used in the appropriate properties.</span></span>

## <a name="add-the-view-details"></a><span data-ttu-id="a4038-140">Aggiungere i dettagli della vista</span><span class="sxs-lookup"><span data-stu-id="a4038-140">Add the view details</span></span>
<span data-ttu-id="a4038-141">La risorsa vista nel file della vista esportato conterrà due elementi nell'elemento **properties** denominati **Dashboard** e **OverviewTile** che contengono la configurazione dettagliata della vista.</span><span class="sxs-lookup"><span data-stu-id="a4038-141">The view resource in the exported view file will contain two elements in the **properties** element named **Dashboard** and **OverviewTile** which contain the detailed configuration of the view.</span></span>  <span data-ttu-id="a4038-142">Copiare questi due elementi e il relativo contenuto nell'elemento **properties** della risorsa vista nel file di soluzione.</span><span class="sxs-lookup"><span data-stu-id="a4038-142">Copy these two elements and their contents into the **properties** element of the view resource in your solution file.</span></span>

## <a name="example"></a><span data-ttu-id="a4038-143">Esempio</span><span class="sxs-lookup"><span data-stu-id="a4038-143">Example</span></span>
<span data-ttu-id="a4038-144">L'esempio seguente mostra un file di soluzione semplice con una vista.</span><span class="sxs-lookup"><span data-stu-id="a4038-144">For example, the following sample shows a simple solution file with a view.</span></span>  <span data-ttu-id="a4038-145">Al posto del contenuto di **Dashboard** e **OverviewTile** sono visualizzati i puntini di sospensione (...) per motivi di spazio.</span><span class="sxs-lookup"><span data-stu-id="a4038-145">Ellipses (...) are shown for the **Dashboard** and **OverviewTile** contents for space reasons.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspaceName": {
                "type": "string"
            },
            "accountName": {
                "type": "string"
            },
            "workspaceRegionId": {
                "type": "string"
            },
            "regionId": {
                "type": "string"
            },
            "pricingTier": {
                "type": "string"
            }
        },
        "variables": {
            "SolutionVersion": "1.1",
            "SolutionPublisher": "Contoso",
            "SolutionName": "Contoso Solution",
            "LogAnalyticsApiVersion": "2015-11-01-preview",
            "ViewAuthor":  "user@contoso.com",
            "ViewDescription":  "This is a sample view.",
            "ViewName":  "Contoso View"
        },
        "resources": [
            {
                "name": "[concat(variables('SolutionName'), '(' ,parameters('workspacename'), ')')]",
                "location": "[parameters('workspaceRegionId')]",
                "tags": { },
                "type": "Microsoft.OperationsManagement/solutions",
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "dependsOn": [
                    "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspacename'), '/views/', variables('ViewName'))]"
                ],
                "properties": {
                    "workspaceResourceId": "[concat(resourceGroup().id, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspacename'))]",
                    "referencedResources": [
                    ],
                    "containedResources": [
                        "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/views/', variables('ViewName'))]"
                    ]
                },
                "plan": {
                    "name": "[concat(variables('SolutionName'), '(' ,parameters('workspaceName'), ')')]",
                    "Version": "[variables('SolutionVersion')]",
                    "product": "ContosoSolution",
                    "publisher": "[variables('SolutionPublisher')]",
                    "promotionCode": ""
                }
            },
            {
                "apiVersion": "[variables('LogAnalyticsApiVersion')]",
                "name": "[concat(parameters('workspaceName'), '/', variables('ViewName'))]",
                "type": "Microsoft.OperationalInsights/workspaces/views",
                "location": "[parameters('workspaceregionId')]",
                "id": "[Concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'),'/views/', variables('ViewName'))]",
                "dependson": [
                ],
                "properties": {
                    "Id": "[variables('ViewName')]",
                    "Name": "[variables('ViewName')]",
                    "DisplayName": "[variables('ViewName')]",
                    "Description": "[variables('ViewDescription')]",
                    "Author": "[variables('ViewAuthor')]",
                    "Source": "Local",
                    "Dashboard": ...,
                    "OverviewTile": ...
                }
            }
          ]
    }




## <a name="next-steps"></a><span data-ttu-id="a4038-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a4038-146">Next steps</span></span>
* <span data-ttu-id="a4038-147">Leggere le informazioni complete sulla creazione di [soluzioni di gestione](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="a4038-147">Learn complete details of creating [management solutions](operations-management-suite-solutions-creating.md).</span></span>
* <span data-ttu-id="a4038-148">Includere [runbook di Automazione nella soluzione di gestione](operations-management-suite-solutions-resources-automation.md).</span><span class="sxs-lookup"><span data-stu-id="a4038-148">Include [Automation runbooks in your management solution](operations-management-suite-solutions-resources-automation.md).</span></span>
