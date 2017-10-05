---
title: Portale di Azure per i criteri delle risorse | Microsoft Docs
description: "Descrive come usare il portale di Azure per creare e gestire i criteri di Resource Manager. È possibile applicare i criteri alla sottoscrizione o a gruppi di risorse."
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
ms.openlocfilehash: 868b2cc1559053057d17b34c03e2e31347f399bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-portal-to-assign-and-manage-resource-policies"></a><span data-ttu-id="54e02-104">Usare il portale di Azure per assegnare e gestire i criteri delle risorse</span><span class="sxs-lookup"><span data-stu-id="54e02-104">Use Azure portal to assign and manage resource policies</span></span>
<span data-ttu-id="54e02-105">Il portale di Azure consente di assegnare i criteri delle risorse a gruppi di risorse e sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="54e02-105">The Azure portal enables you to assign resource policies to resource groups and subscriptions.</span></span> <span data-ttu-id="54e02-106">L'interfaccia utente rende più semplice la selezione dei criteri da assegnare e la specifica dei valori dei parametri dei criteri per personalizzare le impostazioni dei criteri.</span><span class="sxs-lookup"><span data-stu-id="54e02-106">The user interface makes it easy to select the policy that you want to assign, and specify parameter values for that policy to customize the policy settings.</span></span> 

<span data-ttu-id="54e02-107">Per assegnare i criteri tramite il portale è necessario che la definizione dei criteri sia già presente nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="54e02-107">To assign a policy through the portal, the policy definition must already exist in your subscription.</span></span> <span data-ttu-id="54e02-108">La sottoscrizione include diverse definizioni di criteri predefiniti che è possibile assegnare a gruppi di risorse o sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="54e02-108">Your subscription has several built-in policy definitions that are ready for you to assign to resource groups or subscriptions.</span></span> <span data-ttu-id="54e02-109">I criteri predefiniti e i criteri personalizzati definiti vengono visualizzati quando si usa il portale per assegnare i criteri.</span><span class="sxs-lookup"><span data-stu-id="54e02-109">You see these built-in policies and any custom policies you have defined when using the portal to assign policies.</span></span> <span data-ttu-id="54e02-110">Per un'introduzione ai criteri e alla definizione di criteri personalizzati, vedere [Cenni preliminari sui criteri delle risorse](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="54e02-110">For an introduction to policies and how to define customized policy, see [Resource policy overview](resource-manager-policy.md).</span></span>

<span data-ttu-id="54e02-111">I criteri vengono ereditati da tutte le risorse figlio.</span><span class="sxs-lookup"><span data-stu-id="54e02-111">Policies are inherited by all child resources.</span></span> <span data-ttu-id="54e02-112">Se quindi un criterio viene applicato a un gruppo di risorse, è applicabile a tutte le risorse in tale gruppo.</span><span class="sxs-lookup"><span data-stu-id="54e02-112">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span></span> <span data-ttu-id="54e02-113">In questo articolo il termine **ambito** si riferisce al gruppo di risorse o alla sottoscrizione cui vengono assegnati i criteri.</span><span class="sxs-lookup"><span data-stu-id="54e02-113">In this article, the term **scope** refers to the resource group or subscription that is assigned the policy.</span></span> 

<span data-ttu-id="54e02-114">I criteri vengono valutati durante la creazione e l'aggiornamento delle risorse (operazioni PUT e PATCH).</span><span class="sxs-lookup"><span data-stu-id="54e02-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="54e02-115">Assegnare i criteri</span><span class="sxs-lookup"><span data-stu-id="54e02-115">Assign a policy</span></span>

1. <span data-ttu-id="54e02-116">Per assegnare i criteri a un gruppo di risorse o a una sottoscrizione, selezionare il gruppo di risorse o la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="54e02-116">To assign a policy to either a resource group or subscription, select that resource group or subscription.</span></span> <span data-ttu-id="54e02-117">Nelle impostazioni selezionare **Criteri**.</span><span class="sxs-lookup"><span data-stu-id="54e02-117">In the settings, select **Policies**.</span></span>

   ![selezionare i criteri](./media/resource-manager-policy-portal/select-policies.png)

2. <span data-ttu-id="54e02-119">Per creare un'assegnazione di criteri per questo ambito, selezionare **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="54e02-119">To create a policy assignment for this scope, select **Add assignment**.</span></span>

   ![aggiungere un'assegnazione](./media/resource-manager-policy-portal/add-assignment.png)

3. <span data-ttu-id="54e02-121">Selezionare i criteri che si vuole assegnare.</span><span class="sxs-lookup"><span data-stu-id="54e02-121">Select the policy you want to assign.</span></span> <span data-ttu-id="54e02-122">I criteri predefiniti disponibili per l'assegnazione sono visibili anche se non sono state assegnate definizioni dei criteri alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="54e02-122">Even if you have not added any policy definitions to your subscription, you see the built-in policies that are available for assignment.</span></span> <span data-ttu-id="54e02-123">I criteri predefiniti sono applicabili a numerosi scenari comuni.</span><span class="sxs-lookup"><span data-stu-id="54e02-123">These built-in policies cover many common scenarios.</span></span>

   ![selezionare la definizione](./media/resource-manager-policy-portal/select-definition.png)

4. <span data-ttu-id="54e02-125">Dopo la selezione dei criteri, vengono visualizzati una descrizione dei criteri e i parametri per i criteri.</span><span class="sxs-lookup"><span data-stu-id="54e02-125">After selecting a policy, you see a description of the policy, and any parameters for that policy.</span></span> <span data-ttu-id="54e02-126">Ad esempio, la figura seguente illustra il parametro **Allowed locations** (Località consentite) obbligatorio per i criteri che limitano le località disponibili.</span><span class="sxs-lookup"><span data-stu-id="54e02-126">For example, the following image shows the **Allowed locations** parameter, which is required for the policy that restricts the available locations.</span></span>

   ![visualizzazione dei parametri](./media/resource-manager-policy-portal/show-parameters.png)

5. <span data-ttu-id="54e02-128">Tramite l'interfaccia utente, selezionare i valori da specificare per i parametri dei criteri, ad esempio le località che possono essere usate per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="54e02-128">Through the user interface, select the values to specify for the policy parameters (such as the locations that can be used for deployment).</span></span>

   ![selezionare i valori dei parametri](./media/resource-manager-policy-portal/select-parameters.png)

6. <span data-ttu-id="54e02-130">Specificare i valori per gli altri parametri.</span><span class="sxs-lookup"><span data-stu-id="54e02-130">Provide values for the other parameters.</span></span> <span data-ttu-id="54e02-131">L'ambito viene assegnato automaticamente in base al pannello selezionato all'inizio dell'assegnazione dei criteri.</span><span class="sxs-lookup"><span data-stu-id="54e02-131">The scope is automatically assigned based on the blade you selected when starting the policy assignment.</span></span> <span data-ttu-id="54e02-132">Selezionare **OK** al termine dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="54e02-132">Select **OK** when done.</span></span>

   ![definire i parametri](./media/resource-manager-policy-portal/define-parameters.png)

  <span data-ttu-id="54e02-134">I criteri sono stati assegnati all'ambito specificato.</span><span class="sxs-lookup"><span data-stu-id="54e02-134">You have assigned the policy to the specified scope.</span></span>

## <a name="view-policy-assignments"></a><span data-ttu-id="54e02-135">Visualizzare le assegnazioni di criteri</span><span class="sxs-lookup"><span data-stu-id="54e02-135">View policy assignments</span></span>

<span data-ttu-id="54e02-136">Dopo l'assegnazione, i criteri vengono visualizzati nell'elenco dei criteri per l'ambito.</span><span class="sxs-lookup"><span data-stu-id="54e02-136">After assigning a policy, you see it in the list of policies for that scope.</span></span> <span data-ttu-id="54e02-137">La scheda **Dettagli** visualizza un riepilogo dell'assegnazione dei criteri.</span><span class="sxs-lookup"><span data-stu-id="54e02-137">The **Details** tab shows a summary of the policy assignment.</span></span>

![visualizzare i dettagli](./media/resource-manager-policy-portal/show-details.png)

<span data-ttu-id="54e02-139">La scheda **Regola di assegnazione** visualizza il file JSON della definizione dei criteri.</span><span class="sxs-lookup"><span data-stu-id="54e02-139">The **Assignment rule** tab shows the JSON for the policy definition.</span></span>

![visualizzare la regola di assegnazione](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a><span data-ttu-id="54e02-141">Modificare un'assegnazione di criteri esistente</span><span class="sxs-lookup"><span data-stu-id="54e02-141">Change an existing policy assignment</span></span>

<span data-ttu-id="54e02-142">Per modificare i criteri, selezionare **Modifica assegnazione** o **Elimina**</span><span class="sxs-lookup"><span data-stu-id="54e02-142">To change a policy, select **Edit assignment** or **Delete**</span></span>

![modificare o eliminare l'assegnazione](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a><span data-ttu-id="54e02-144">Assegnare criteri personalizzati</span><span class="sxs-lookup"><span data-stu-id="54e02-144">Assign custom policies</span></span>

<span data-ttu-id="54e02-145">Se sono stati definiti criteri personalizzati nella sottoscrizione, i criteri sono disponibili per l'assegnazione tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="54e02-145">If you have defined custom policies in your subscription, those policies are available for assignment through the portal.</span></span> <span data-ttu-id="54e02-146">I criteri personalizzati sono preceduti da **[Personalizzato]**</span><span class="sxs-lookup"><span data-stu-id="54e02-146">Those policies are prefaced with **[Custom]**</span></span>

![criteri personalizzati](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a><span data-ttu-id="54e02-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="54e02-148">Next steps</span></span>
* <span data-ttu-id="54e02-149">Per altre informazioni sulla sintassi JSON per la definizione dei criteri, vedere [Cenni preliminari sui criteri delle risorse](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="54e02-149">To learn about the JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="54e02-150">Per indicazioni su come le aziende possono usare Resource Manager per gestire efficacemente le sottoscrizioni, vedere [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Scaffolding aziendale Azure - Governance prescrittiva per le sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="54e02-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="54e02-151">Lo schema del criterio è pubblicato in [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="54e02-151">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

