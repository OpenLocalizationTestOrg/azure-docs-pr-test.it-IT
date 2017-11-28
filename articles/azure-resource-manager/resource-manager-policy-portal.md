---
title: aaaAzure portale per i criteri di risorse | Documenti Microsoft
description: Viene descritto come toouse toocreate portale Azure e gestire i criteri di gestione risorse. I criteri possono essere applicati a hello sottoscrizione o gruppi di risorse.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: ce6413386317e532b63761a24458b85c996af4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-tooassign-and-manage-resource-policies"></a><span data-ttu-id="ff723-104">Utilizzare tooassign portale Azure e gestire i criteri di risorse</span><span class="sxs-lookup"><span data-stu-id="ff723-104">Use Azure portal tooassign and manage resource policies</span></span>
<span data-ttu-id="ff723-105">portale di Azure Hello consente le sottoscrizioni e si tooassign criteri tooresource gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="ff723-105">hello Azure portal enables you tooassign resource policies tooresource groups and subscriptions.</span></span> <span data-ttu-id="ff723-106">interfaccia utente di Hello rende i criteri di hello tooselect semplice che si desidera tooassign e specificano i valori dei parametri per tale criterio impostazioni dei criteri toocustomize hello.</span><span class="sxs-lookup"><span data-stu-id="ff723-106">hello user interface makes it easy tooselect hello policy that you want tooassign, and specify parameter values for that policy toocustomize hello policy settings.</span></span> 

<span data-ttu-id="ff723-107">tooassign criteri tramite il portale di hello, definizione dei criteri hello deve esistere già nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ff723-107">tooassign a policy through hello portal, hello policy definition must already exist in your subscription.</span></span> <span data-ttu-id="ff723-108">La sottoscrizione ha diverse definizioni di criteri predefiniti che sono pronte per si tooassign tooresource gruppi o le sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="ff723-108">Your subscription has several built-in policy definitions that are ready for you tooassign tooresource groups or subscriptions.</span></span> <span data-ttu-id="ff723-109">Vengono visualizzati questi criteri predefiniti e i criteri personalizzati definiti quando si utilizza criteri tooassign portale hello.</span><span class="sxs-lookup"><span data-stu-id="ff723-109">You see these built-in policies and any custom policies you have defined when using hello portal tooassign policies.</span></span> <span data-ttu-id="ff723-110">Per un'introduzione toopolicies e come toodefine personalizzare criteri, vedere [Panoramica criteri delle risorse](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ff723-110">For an introduction toopolicies and how toodefine customized policy, see [Resource policy overview](resource-manager-policy.md).</span></span>

<span data-ttu-id="ff723-111">I criteri vengono ereditati da tutte le risorse figlio.</span><span class="sxs-lookup"><span data-stu-id="ff723-111">Policies are inherited by all child resources.</span></span> <span data-ttu-id="ff723-112">Se il criterio viene applicato tooa gruppo di risorse, è pertanto applicabile tooall risorse di hello in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ff723-112">So, if a policy is applied tooa resource group, it is applicable tooall hello resources in that resource group.</span></span> <span data-ttu-id="ff723-113">In questo articolo, termini hello **ambito** fa riferimento il gruppo di risorse toohello o una sottoscrizione che viene assegnato il criterio di hello.</span><span class="sxs-lookup"><span data-stu-id="ff723-113">In this article, hello term **scope** refers toohello resource group or subscription that is assigned hello policy.</span></span> 

<span data-ttu-id="ff723-114">I criteri vengono valutati durante la creazione e l'aggiornamento delle risorse (operazioni PUT e PATCH).</span><span class="sxs-lookup"><span data-stu-id="ff723-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="ff723-115">Assegnare i criteri</span><span class="sxs-lookup"><span data-stu-id="ff723-115">Assign a policy</span></span>

1. <span data-ttu-id="ff723-116">tooassign un tooeither criteri un gruppo di risorse o una sottoscrizione, selezionare il gruppo di risorse o di una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ff723-116">tooassign a policy tooeither a resource group or subscription, select that resource group or subscription.</span></span> <span data-ttu-id="ff723-117">Nelle impostazioni di hello, selezionare **criteri**.</span><span class="sxs-lookup"><span data-stu-id="ff723-117">In hello settings, select **Policies**.</span></span>

   ![selezionare i criteri](./media/resource-manager-policy-portal/select-policies.png)

2. <span data-ttu-id="ff723-119">Selezionare un'assegnazione di criteri per questo ambito, toocreate **aggiungere assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ff723-119">toocreate a policy assignment for this scope, select **Add assignment**.</span></span>

   ![aggiungere un'assegnazione](./media/resource-manager-policy-portal/add-assignment.png)

3. <span data-ttu-id="ff723-121">Selezionare i criteri di hello da tooassign.</span><span class="sxs-lookup"><span data-stu-id="ff723-121">Select hello policy you want tooassign.</span></span> <span data-ttu-id="ff723-122">Anche se non sono state aggiunte sottoscrizioni di tooyour le definizioni dei criteri, vedrai i criteri predefiniti hello che sono disponibili per l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="ff723-122">Even if you have not added any policy definitions tooyour subscription, you see hello built-in policies that are available for assignment.</span></span> <span data-ttu-id="ff723-123">I criteri predefiniti sono applicabili a numerosi scenari comuni.</span><span class="sxs-lookup"><span data-stu-id="ff723-123">These built-in policies cover many common scenarios.</span></span>

   ![selezionare la definizione](./media/resource-manager-policy-portal/select-definition.png)

4. <span data-ttu-id="ff723-125">Dopo aver selezionato un criterio, vedere una descrizione dei criteri di hello e i parametri per tale criterio.</span><span class="sxs-lookup"><span data-stu-id="ff723-125">After selecting a policy, you see a description of hello policy, and any parameters for that policy.</span></span> <span data-ttu-id="ff723-126">Ad esempio, hello seguente immagine Mostra hello **consentiti percorsi** parametro, è necessario per i criteri di hello che limitano i percorsi disponibili hello.</span><span class="sxs-lookup"><span data-stu-id="ff723-126">For example, hello following image shows hello **Allowed locations** parameter, which is required for hello policy that restricts hello available locations.</span></span>

   ![visualizzazione dei parametri](./media/resource-manager-policy-portal/show-parameters.png)

5. <span data-ttu-id="ff723-128">Tramite l'interfaccia utente di hello, selezionare hello toospecify di valori per i parametri dei criteri hello (ad esempio i percorsi di hello che possono essere usati per la distribuzione).</span><span class="sxs-lookup"><span data-stu-id="ff723-128">Through hello user interface, select hello values toospecify for hello policy parameters (such as hello locations that can be used for deployment).</span></span>

   ![selezionare i valori dei parametri](./media/resource-manager-policy-portal/select-parameters.png)

6. <span data-ttu-id="ff723-130">Fornire valori per hello altri parametri.</span><span class="sxs-lookup"><span data-stu-id="ff723-130">Provide values for hello other parameters.</span></span> <span data-ttu-id="ff723-131">ambito Hello viene assegnato automaticamente nel pannello hello selezionato quando si avvia l'assegnazione dei criteri hello.</span><span class="sxs-lookup"><span data-stu-id="ff723-131">hello scope is automatically assigned based on hello blade you selected when starting hello policy assignment.</span></span> <span data-ttu-id="ff723-132">Selezionare **OK** al termine dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="ff723-132">Select **OK** when done.</span></span>

   ![definire i parametri](./media/resource-manager-policy-portal/define-parameters.png)

  <span data-ttu-id="ff723-134">È stato assegnato il criterio di hello toohello specificato ambito.</span><span class="sxs-lookup"><span data-stu-id="ff723-134">You have assigned hello policy toohello specified scope.</span></span>

## <a name="view-policy-assignments"></a><span data-ttu-id="ff723-135">Visualizzare le assegnazioni di criteri</span><span class="sxs-lookup"><span data-stu-id="ff723-135">View policy assignments</span></span>

<span data-ttu-id="ff723-136">Dopo l'assegnazione di un criterio, è visualizzata nell'elenco di hello dei criteri per tale ambito.</span><span class="sxs-lookup"><span data-stu-id="ff723-136">After assigning a policy, you see it in hello list of policies for that scope.</span></span> <span data-ttu-id="ff723-137">Hello **dettagli** scheda Mostra un riepilogo dell'assegnazione di criteri hello.</span><span class="sxs-lookup"><span data-stu-id="ff723-137">hello **Details** tab shows a summary of hello policy assignment.</span></span>

![visualizzare i dettagli](./media/resource-manager-policy-portal/show-details.png)

<span data-ttu-id="ff723-139">Hello **regola di assegnazione** scheda Mostra hello JSON per la definizione dei criteri hello.</span><span class="sxs-lookup"><span data-stu-id="ff723-139">hello **Assignment rule** tab shows hello JSON for hello policy definition.</span></span>

![visualizzare la regola di assegnazione](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a><span data-ttu-id="ff723-141">Modificare un'assegnazione di criteri esistente</span><span class="sxs-lookup"><span data-stu-id="ff723-141">Change an existing policy assignment</span></span>

<span data-ttu-id="ff723-142">Selezionare un criterio, toochange **modifica assegnazione** o **eliminare**</span><span class="sxs-lookup"><span data-stu-id="ff723-142">toochange a policy, select **Edit assignment** or **Delete**</span></span>

![modificare o eliminare l'assegnazione](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a><span data-ttu-id="ff723-144">Assegnare criteri personalizzati</span><span class="sxs-lookup"><span data-stu-id="ff723-144">Assign custom policies</span></span>

<span data-ttu-id="ff723-145">Se sono stati definiti criteri personalizzati nella sottoscrizione, sono disponibili per l'assegnazione tramite il portale di hello tali criteri.</span><span class="sxs-lookup"><span data-stu-id="ff723-145">If you have defined custom policies in your subscription, those policies are available for assignment through hello portal.</span></span> <span data-ttu-id="ff723-146">I criteri personalizzati sono preceduti da **[Personalizzato]**</span><span class="sxs-lookup"><span data-stu-id="ff723-146">Those policies are prefaced with **[Custom]**</span></span>

![criteri personalizzati](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a><span data-ttu-id="ff723-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ff723-148">Next steps</span></span>
* <span data-ttu-id="ff723-149">toolearn sulla sintassi di hello JSON per la definizione di criteri, vedere [Panoramica criteri delle risorse](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ff723-149">toolearn about hello JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="ff723-150">Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="ff723-150">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="ff723-151">schema dei criteri di Hello è pubblicato nella [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="ff723-151">hello policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

