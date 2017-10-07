---
title: la creazione di definizione dell'interfaccia utente per le applicazioni gestite Azure aaaUnderstand | Documenti Microsoft
description: Viene descritto come definizioni dell'interfaccia utente toocreate per le applicazioni gestite di Azure
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
ms.openlocfilehash: d53ddf438c24d5a6cb8dd53ca0b4694ab0462515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-createuidefinition"></a><span data-ttu-id="8e84c-103">Introduzione a CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="8e84c-103">Getting started with CreateUiDefinition</span></span>
<span data-ttu-id="8e84c-104">Questo documento introduce i concetti di base hello di un CreateUiDefinition, utilizzato dall'interfaccia utente di hello toogenerate portale Azure hello per la creazione di un'applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="8e84c-104">This document introduces hello core concepts of a CreateUiDefinition, which is used by hello Azure portal toogenerate hello user interface for creating a managed application.</span></span>

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

<span data-ttu-id="8e84c-105">CreateUiDefinition contiene sempre tre proprietà:</span><span class="sxs-lookup"><span data-stu-id="8e84c-105">A CreateUiDefinition always contains three properties:</span></span> 

* <span data-ttu-id="8e84c-106">handler</span><span class="sxs-lookup"><span data-stu-id="8e84c-106">handler</span></span>
* <span data-ttu-id="8e84c-107">version</span><span class="sxs-lookup"><span data-stu-id="8e84c-107">version</span></span>
* <span data-ttu-id="8e84c-108">parameters</span><span class="sxs-lookup"><span data-stu-id="8e84c-108">parameters</span></span>

<span data-ttu-id="8e84c-109">Per le applicazioni gestite, deve essere sempre gestore `Microsoft.Compute.MultiVm`, e la versione più recente supportato hello è `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="8e84c-109">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and hello latest supported version is `0.1.2-preview`.</span></span>

<span data-ttu-id="8e84c-110">schema Hello di proprietà parametri hello dipende dalla combinazione di hello del gestore specificato hello e versione.</span><span class="sxs-lookup"><span data-stu-id="8e84c-110">hello schema of hello parameters property depends on hello combination of hello specified handler and version.</span></span> <span data-ttu-id="8e84c-111">Per le applicazioni gestite, proprietà hello supportato sono `basics`, `steps`, e `outputs`.</span><span class="sxs-lookup"><span data-stu-id="8e84c-111">For managed applications, hello supported properties are `basics`, `steps`, and `outputs`.</span></span> <span data-ttu-id="8e84c-112">Nozioni di base e passaggi proprietà Hello contengono hello _elementi_ , ad esempio caselle di testo ed elenchi a discesa - toobe visualizzati in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8e84c-112">hello basics and steps properties contain hello _elements_ - like textboxes and dropdowns - toobe displayed in hello Azure portal.</span></span> <span data-ttu-id="8e84c-113">output di Hello è toomap utilizzati valori di output di hello di hello elementi specificati toohello parametri di modello di distribuzione Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="8e84c-113">hello outputs property is used toomap hello output values of hello specified elements toohello parameters of hello Azure Resource Manager deployment template.</span></span>

<span data-ttu-id="8e84c-114">L'inclusione di `$schema` è consigliata ma facoltativa.</span><span class="sxs-lookup"><span data-stu-id="8e84c-114">Including `$schema` is recommended, but optional.</span></span> <span data-ttu-id="8e84c-115">Se specificato, hello valore per `version` deve corrispondere una versione di hello hello `$schema` URI.</span><span class="sxs-lookup"><span data-stu-id="8e84c-115">If specified, hello value for `version` must match hello version within hello `$schema` URI.</span></span>

## <a name="basics"></a><span data-ttu-id="8e84c-116">Nozioni di base</span><span class="sxs-lookup"><span data-stu-id="8e84c-116">Basics</span></span>
<span data-ttu-id="8e84c-117">Hello nozioni di base è sempre hello primo passaggio della procedura guidata hello generata hello portale di Azure analizza un CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="8e84c-117">hello Basics step is always hello first step of hello wizard generated when hello Azure portal parses a CreateUiDefinition.</span></span> <span data-ttu-id="8e84c-118">Inoltre specificare gli elementi di hello toodisplaying `basics`, portale hello inserisce elementi per la sottoscrizione di hello toochoose gli utenti, gruppo di risorse e posizione per la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="8e84c-118">In addition toodisplaying hello elements specified in `basics`, hello portal injects elements for users toochoose hello subscription, resource group, and location for hello deployment.</span></span> <span data-ttu-id="8e84c-119">In genere, gli elementi che eseguono query per i parametri a livello di distribuzione, ad esempio hello nome delle credenziali di un cluster o un amministratore, devono andare in questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="8e84c-119">Generally, elements that query for deployment-wide parameters, like hello name of a cluster or administrator credentials, should go in this step.</span></span>

<span data-ttu-id="8e84c-120">Se il comportamento di un elemento dipende dalla sottoscrizione, gruppo di risorse o percorso dell'utente hello, tale elemento può essere utilizzato in Nozioni di base.</span><span class="sxs-lookup"><span data-stu-id="8e84c-120">If an element's behavior depends on hello user's subscription, resource group, or location, then that element can't be used in basics.</span></span> <span data-ttu-id="8e84c-121">Ad esempio, **Microsoft.Compute.SizeSelector** varia a seconda sottoscrizione e il percorso toodetermine hello elenco dell'utente hello di dimensioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="8e84c-121">For example, **Microsoft.Compute.SizeSelector** depends on hello user's subscription and location toodetermine hello list of available sizes.</span></span> <span data-ttu-id="8e84c-122">È quindi possibile usare **Microsoft.Compute.SizeSelector** solo nelle proprietà steps.</span><span class="sxs-lookup"><span data-stu-id="8e84c-122">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span></span> <span data-ttu-id="8e84c-123">In genere, solo gli elementi in hello **Microsoft.Common** dello spazio dei nomi può essere usato in Nozioni di base.</span><span class="sxs-lookup"><span data-stu-id="8e84c-123">Generally, only elements in hello **Microsoft.Common** namespace can be used in basics.</span></span> <span data-ttu-id="8e84c-124">Anche se alcuni elementi in altri spazi dei nomi (ad esempio **Microsoft.Compute.Credentials**) che non dipendono dal contesto dell'utente hello, sono ancora consentiti.</span><span class="sxs-lookup"><span data-stu-id="8e84c-124">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on hello user's context, are still allowed.</span></span>

## <a name="steps"></a><span data-ttu-id="8e84c-125">Passi</span><span class="sxs-lookup"><span data-stu-id="8e84c-125">Steps</span></span>
<span data-ttu-id="8e84c-126">proprietà passaggi Hello può contenere zero o più toodisplay passaggi aggiuntivi dopo nozioni di base, ognuno dei quali contiene uno o più elementi.</span><span class="sxs-lookup"><span data-stu-id="8e84c-126">hello steps property can contain zero or more additional steps toodisplay after basics, each of which contains one or more elements.</span></span> <span data-ttu-id="8e84c-127">È possibile aggiungere passaggi per ogni ruolo o a livello di applicazione hello da distribuire.</span><span class="sxs-lookup"><span data-stu-id="8e84c-127">Consider adding steps per role or tier of hello application being deployed.</span></span> <span data-ttu-id="8e84c-128">Ad esempio, è possibile aggiungere un passaggio per gli input per i nodi master hello e un passaggio per i nodi di lavoro hello in un cluster.</span><span class="sxs-lookup"><span data-stu-id="8e84c-128">For example, add a step for inputs for hello master nodes, and a step for hello worker nodes in a cluster.</span></span>

## <a name="outputs"></a><span data-ttu-id="8e84c-129">outputs</span><span class="sxs-lookup"><span data-stu-id="8e84c-129">Outputs</span></span>
<span data-ttu-id="8e84c-130">portale di Azure Hello utilizza hello `outputs` gli elementi di proprietà toomap da `basics` e `steps` toohello parametri di modello di distribuzione Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="8e84c-130">hello Azure portal uses hello `outputs` property toomap elements from `basics` and `steps` toohello parameters of hello Azure Resource Manager deployment template.</span></span> <span data-ttu-id="8e84c-131">Hello chiavi del dizionario sono nomi di hello hello dei parametri di modello e i valori hello sono proprietà degli oggetti di output di hello dagli elementi hello a cui fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="8e84c-131">hello keys of this dictionary are hello names of hello template parameters, and hello values are properties of hello output objects from hello referenced elements.</span></span>

## <a name="functions"></a><span data-ttu-id="8e84c-132">Funzioni</span><span class="sxs-lookup"><span data-stu-id="8e84c-132">Functions</span></span>
<span data-ttu-id="8e84c-133">Simile troppo[funzioni di modello](resource-group-template-functions.md) in Gestione risorse di Azure (entrambi nella sintassi e la funzionalità), CreateUiDefinition fornisce funzioni per l'utilizzo degli elementi input e output, nonché le funzionalità, ad esempio istruzioni condizionali.</span><span class="sxs-lookup"><span data-stu-id="8e84c-133">Similar too[template functions](resource-group-template-functions.md) in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e84c-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8e84c-134">Next steps</span></span>
<span data-ttu-id="8e84c-135">CreateUiDefinition ha uno schema semplice,</span><span class="sxs-lookup"><span data-stu-id="8e84c-135">CreateUiDefinition itself has a simple schema.</span></span> <span data-ttu-id="8e84c-136">profondità di reale Hello di esso viene fornito da tutti gli elementi di hello è supportato e funzioni, quali hello documenti seguenti descrivono in modo dettagliato wondrous:</span><span class="sxs-lookup"><span data-stu-id="8e84c-136">hello real depth of it comes from all hello supported elements and functions, which hello following documents describe in wondrous detail:</span></span>

- [<span data-ttu-id="8e84c-137">Elementi</span><span class="sxs-lookup"><span data-stu-id="8e84c-137">Elements</span></span>](managed-application-createuidefinition-elements.md)
- [<span data-ttu-id="8e84c-138">Funzioni</span><span class="sxs-lookup"><span data-stu-id="8e84c-138">Functions</span></span>](managed-application-createuidefinition-functions.md)

<span data-ttu-id="8e84c-139">Per uno schema JSON corrente per CreateUiDefinition, vedere qui: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span><span class="sxs-lookup"><span data-stu-id="8e84c-139">A current JSON schema for CreateUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span></span> 

<span data-ttu-id="8e84c-140">Nelle versioni successive è disponibile in hello nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="8e84c-140">Later versions will be available at hello same location.</span></span> <span data-ttu-id="8e84c-141">Sostituire hello `0.1.2-preview` parte dell'URL di hello e hello `version` valore con l'identificatore di versione di hello intendi toouse.</span><span class="sxs-lookup"><span data-stu-id="8e84c-141">Replace hello `0.1.2-preview` portion of hello URL and hello `version` value with hello version identifier you intend toouse.</span></span> <span data-ttu-id="8e84c-142">gli identificatori di versione di Hello attualmente supportato sono `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, e `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="8e84c-142">hello currently supported version identifiers are `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, and `0.1.2-preview`.</span></span>
