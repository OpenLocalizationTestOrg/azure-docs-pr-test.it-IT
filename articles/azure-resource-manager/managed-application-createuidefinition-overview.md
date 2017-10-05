---
title: Informazioni sulla creazione di una definizione dell'interfaccia utente per le applicazioni gestite di Azure | Microsoft Docs
description: Illustra come creare definizioni dell'interfaccia utente per le applicazioni gestite di Azure
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/11/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 176b891538f85c5638a2321561c3d8bd377d245b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-createuidefinition"></a><span data-ttu-id="4b5f5-103">Introduzione a CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="4b5f5-103">Getting started with CreateUiDefinition</span></span>
<span data-ttu-id="4b5f5-104">Questo documento illustra i concetti di base di CreateUiDefinition, che consente al portale di Azure di generare l'interfaccia utente per la creazione di un'applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-104">This document introduces the core concepts of a CreateUiDefinition, which is used by the Azure portal to generate the user interface for creating a managed application.</span></span>

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

<span data-ttu-id="4b5f5-105">CreateUiDefinition contiene sempre tre proprietà:</span><span class="sxs-lookup"><span data-stu-id="4b5f5-105">A CreateUiDefinition always contains three properties:</span></span> 

* <span data-ttu-id="4b5f5-106">handler</span><span class="sxs-lookup"><span data-stu-id="4b5f5-106">handler</span></span>
* <span data-ttu-id="4b5f5-107">version</span><span class="sxs-lookup"><span data-stu-id="4b5f5-107">version</span></span>
* <span data-ttu-id="4b5f5-108">Parametri</span><span class="sxs-lookup"><span data-stu-id="4b5f5-108">parameters</span></span>

<span data-ttu-id="4b5f5-109">Per le applicazioni gestite la proprietà handler deve essere sempre `Microsoft.Compute.MultiVm` e la versione supportata più recente è `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-109">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and the latest supported version is `0.1.2-preview`.</span></span>

<span data-ttu-id="4b5f5-110">Lo schema della proprietà parameters dipende dalla combinazione delle proprietà handler e version specificate.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-110">The schema of the parameters property depends on the combination of the specified handler and version.</span></span> <span data-ttu-id="4b5f5-111">Per le applicazioni gestite sono supportate le proprietà `basics`, `steps` e `outputs`.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-111">For managed applications, the supported properties are `basics`, `steps`, and `outputs`.</span></span> <span data-ttu-id="4b5f5-112">Le proprietà basics e steps contengono _elementi_, ad esempio caselle di testo ed elenchi a discesa, da visualizzare nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-112">The basics and steps properties contain the _elements_ - like textboxes and dropdowns - to be displayed in the Azure portal.</span></span> <span data-ttu-id="4b5f5-113">La proprietà outputs viene usata per il mapping dei valori di output degli elementi specificati ai parametri del modello di distribuzione Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-113">The outputs property is used to map the output values of the specified elements to the parameters of the Azure Resource Manager deployment template.</span></span>

<span data-ttu-id="4b5f5-114">L'inclusione di `$schema` è consigliata ma facoltativa.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-114">Including `$schema` is recommended, but optional.</span></span> <span data-ttu-id="4b5f5-115">Se specificato, il valore per la proprietà `version` deve corrispondere alla versione nell'URI di `$schema`.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-115">If specified, the value for `version` must match the version within the `$schema` URI.</span></span>

## <a name="basics"></a><span data-ttu-id="4b5f5-116">Nozioni di base</span><span class="sxs-lookup"><span data-stu-id="4b5f5-116">Basics</span></span>
<span data-ttu-id="4b5f5-117">Il passaggio relativo alle informazioni di base è sempre il primo passaggio della procedura guidata generata quando il portale di Azure analizza CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-117">The Basics step is always the first step of the wizard generated when the Azure portal parses a CreateUiDefinition.</span></span> <span data-ttu-id="4b5f5-118">Oltre a visualizzare gli elementi specificati in `basics`, il portale inserisce elementi che consentono agli utenti di scegliere la sottoscrizione, il gruppo di risorse e la posizione della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-118">In addition to displaying the elements specified in `basics`, the portal injects elements for users to choose the subscription, resource group, and location for the deployment.</span></span> <span data-ttu-id="4b5f5-119">In genere gli elementi che eseguono query per parametri a livello di distribuzione, ad esempio il nome di un cluster o le credenziali dell'amministratore, devono essere inseriti in questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-119">Generally, elements that query for deployment-wide parameters, like the name of a cluster or administrator credentials, should go in this step.</span></span>

<span data-ttu-id="4b5f5-120">Se il comportamento di un elemento dipende dalla sottoscrizione, dal gruppo di risorse o dalla posizione dell'utente, non è possibile usare tale elemento per le proprietà basics.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-120">If an element's behavior depends on the user's subscription, resource group, or location, then that element can't be used in basics.</span></span> <span data-ttu-id="4b5f5-121">Ad esempio, **Microsoft.Compute.SizeSelector** dipende dalla sottoscrizione e dalla posizione dell'utente per la determinazione dell'elenco delle dimensioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-121">For example, **Microsoft.Compute.SizeSelector** depends on the user's subscription and location to determine the list of available sizes.</span></span> <span data-ttu-id="4b5f5-122">È quindi possibile usare **Microsoft.Compute.SizeSelector** solo nelle proprietà steps.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-122">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span></span> <span data-ttu-id="4b5f5-123">In genere è possibile usare nelle proprietà basics solo gli elementi disponibili nello spazio dei nomi **Microsoft.Common**.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-123">Generally, only elements in the **Microsoft.Common** namespace can be used in basics.</span></span> <span data-ttu-id="4b5f5-124">Sono tuttavia consentiti alcuni elementi disponibili in altri spazi dei nomi, ad esempio **Microsoft.Compute.Credentials**, che non dipendono dal contesto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-124">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on the user's context, are still allowed.</span></span>

## <a name="steps"></a><span data-ttu-id="4b5f5-125">Passi</span><span class="sxs-lookup"><span data-stu-id="4b5f5-125">Steps</span></span>
<span data-ttu-id="4b5f5-126">La proprietà steps può contenere zero o più passaggi aggiuntivi da visualizzare dopo la proprietà basics, ognuna delle quali contiene uno o più elementi.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-126">The steps property can contain zero or more additional steps to display after basics, each of which contains one or more elements.</span></span> <span data-ttu-id="4b5f5-127">Prendere in considerazione l'aggiunta di passaggi per ogni ruolo o livello dell'applicazione in fase di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-127">Consider adding steps per role or tier of the application being deployed.</span></span> <span data-ttu-id="4b5f5-128">Aggiungere ad esempio un passaggio per gli input dei nodi master e un passaggio per i nodi di lavoro in un cluster.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-128">For example, add a step for inputs for the master nodes, and a step for the worker nodes in a cluster.</span></span>

## <a name="outputs"></a><span data-ttu-id="4b5f5-129">Output</span><span class="sxs-lookup"><span data-stu-id="4b5f5-129">Outputs</span></span>
<span data-ttu-id="4b5f5-130">Il portale di Azure usa la proprietà `outputs` per il mapping di elementi da `basics` e `steps` ai parametri del modello di distribuzione Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-130">The Azure portal uses the `outputs` property to map elements from `basics` and `steps` to the parameters of the Azure Resource Manager deployment template.</span></span> <span data-ttu-id="4b5f5-131">Le chiavi di questo dizionario sono i nomi dei parametri del modello e i valori sono le proprietà degli oggetti di output dagli elementi a cui si fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-131">The keys of this dictionary are the names of the template parameters, and the values are properties of the output objects from the referenced elements.</span></span>

## <a name="functions"></a><span data-ttu-id="4b5f5-132">Funzioni</span><span class="sxs-lookup"><span data-stu-id="4b5f5-132">Functions</span></span>
<span data-ttu-id="4b5f5-133">Analogamente alle [funzioni del modello](resource-group-template-functions.md) in Azure Resource Manager, a livello di sintassi e di funzionalità, CreateUiDefinition offre funzioni per l'uso di input e output degli elementi, oltre a funzionalità quali le istruzioni condizionali.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-133">Similar to [template functions](resource-group-template-functions.md) in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b5f5-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4b5f5-134">Next steps</span></span>
<span data-ttu-id="4b5f5-135">CreateUiDefinition ha uno schema semplice,</span><span class="sxs-lookup"><span data-stu-id="4b5f5-135">CreateUiDefinition itself has a simple schema.</span></span> <span data-ttu-id="4b5f5-136">ma supporta numerosi elementi e funzioni, illustrati in modo dettagliato nei documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4b5f5-136">The real depth of it comes from all the supported elements and functions, which the following documents describe in wondrous detail:</span></span>

- [<span data-ttu-id="4b5f5-137">Elementi</span><span class="sxs-lookup"><span data-stu-id="4b5f5-137">Elements</span></span>](managed-application-createuidefinition-elements.md)
- [<span data-ttu-id="4b5f5-138">Funzioni</span><span class="sxs-lookup"><span data-stu-id="4b5f5-138">Functions</span></span>](managed-application-createuidefinition-functions.md)

<span data-ttu-id="4b5f5-139">Per uno schema JSON corrente per CreateUiDefinition, vedere qui: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-139">A current JSON schema for CreateUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span></span> 

<span data-ttu-id="4b5f5-140">Le versioni più aggiornate verranno rese disponibili nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-140">Later versions will be available at the same location.</span></span> <span data-ttu-id="4b5f5-141">Sostituire la parte `0.1.2-preview` dell'URL e il valore `version` con l'identificatore della versione da usare.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-141">Replace the `0.1.2-preview` portion of the URL and the `version` value with the version identifier you intend to use.</span></span> <span data-ttu-id="4b5f5-142">Gli identificatori attualmente supportati per la versione sono `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview` e `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="4b5f5-142">The currently supported version identifiers are `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, and `0.1.2-preview`.</span></span>