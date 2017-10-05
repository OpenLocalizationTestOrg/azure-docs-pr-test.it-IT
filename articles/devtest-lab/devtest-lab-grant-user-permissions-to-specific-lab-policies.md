---
title: Concedere le autorizzazioni utente per specifici criteri di lab | Documentazione Microsoft
description: Informazioni su come concedere le autorizzazioni utente per criteri di lab specifici nei laboratori di sviluppo/test in base alle esigenze di ogni utente
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 5ca829f0-eb69-40a1-ae26-03a629db1d7e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 0bd9f83257834d9681479ba9117c48ffd6d6e166
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="grant-user-permissions-to-specific-lab-policies"></a><span data-ttu-id="a5589-103">Concedere le autorizzazioni utente per specifici criteri di lab</span><span class="sxs-lookup"><span data-stu-id="a5589-103">Grant user permissions to specific lab policies</span></span>
## <a name="overview"></a><span data-ttu-id="a5589-104">Overview</span><span class="sxs-lookup"><span data-stu-id="a5589-104">Overview</span></span>
<span data-ttu-id="a5589-105">In questo articolo viene illustrato come usare PowerShell per concedere agli utenti autorizzazioni per un particolare criterio di lab.</span><span class="sxs-lookup"><span data-stu-id="a5589-105">This article illustrates how to use PowerShell to grant users permissions to a particular lab policy.</span></span> <span data-ttu-id="a5589-106">In questo modo, le autorizzazioni possono essere applicate in base alle esigenze di ciascun utente.</span><span class="sxs-lookup"><span data-stu-id="a5589-106">That way, permissions can be applied based on each user's needs.</span></span> <span data-ttu-id="a5589-107">Ad esempio, è possibile concedere a un determinato utente la possibilità di modificare le impostazioni dei criteri delle macchine virtuali, ma non i criteri dei costi.</span><span class="sxs-lookup"><span data-stu-id="a5589-107">For example, you might want to grant a particular user the ability to change the VM policy settings, but not the cost policies.</span></span>

## <a name="policies-as-resources"></a><span data-ttu-id="a5589-108">Criteri come risorse</span><span class="sxs-lookup"><span data-stu-id="a5589-108">Policies as resources</span></span>
<span data-ttu-id="a5589-109">Come descritto nell'articolo [Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-control-configure.md) , il controllo degli accessi in base al ruolo consente la gestione specifica degli accessi delle risorse per Azure.</span><span class="sxs-lookup"><span data-stu-id="a5589-109">As discussed in the [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC enables fine-grained access management of resources for Azure.</span></span> <span data-ttu-id="a5589-110">Usando il Controllo degli accessi in base al ruolo di Azure, è possibile separare compiti all'interno del team DevOps e concedere agli utenti solo la quantità di accesso di cui hanno bisogno per svolgere il proprio lavoro.</span><span class="sxs-lookup"><span data-stu-id="a5589-110">Using RBAC, you can segregate duties within your DevOps team and grant only the amount of access to users that they need to perform their jobs.</span></span>

<span data-ttu-id="a5589-111">Nei lab di sviluppo/test un criterio è un tipo di risorsa che abilita l'azione del controllo degli accessi in base al ruolo **Microsoft.DevTestLab/labs/policySets/policies/**.</span><span class="sxs-lookup"><span data-stu-id="a5589-111">In DevTest Labs, a policy is a resource type that enables the RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span></span> <span data-ttu-id="a5589-112">Ogni criterio di lab è una risorsa del tipo di risorsa Criterio e può essere assegnato come ambito a un ruolo del controllo degli accessi in base al ruolo.</span><span class="sxs-lookup"><span data-stu-id="a5589-112">Each lab policy is a resource in the Policy resource type, and can be assigned as a scope to an RBAC role.</span></span>

<span data-ttu-id="a5589-113">Ad esempio, per concedere le autorizzazioni di lettura/scrittura agli utenti per il **dimensioni delle macchine Virtuali consentite** criteri, è necessario creare un ruolo personalizzato che funziona con il **Microsoft.DevTestLab/labs/policySets/policies/*** azione, quindi assegnare gli utenti appropriati a questo ruolo personalizzato nell'ambito del **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span><span class="sxs-lookup"><span data-stu-id="a5589-113">For example, in order to grant users read/write permission to the **Allowed VM Sizes** policy, you would create a custom role that works with the **Microsoft.DevTestLab/labs/policySets/policies/*** action, and then assign the appropriate users to this custom role in the scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span></span>

<span data-ttu-id="a5589-114">Per altre informazioni sui ruoli personalizzati in RBAC, vedere il [controllo di accesso ai ruoli personalizzati](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="a5589-114">To learn more about custom roles in RBAC, see the [Custom roles access control](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="creating-a-lab-custom-role-using-powershell"></a><span data-ttu-id="a5589-115">Creazione di un ruolo personalizzato lab tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5589-115">Creating a lab custom role using PowerShell</span></span>
<span data-ttu-id="a5589-116">Per iniziare, leggere l'articolo seguente che descrive come installare e configurare i cmdlet PowerShell di Azure: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span><span class="sxs-lookup"><span data-stu-id="a5589-116">In order to get started, you’ll need to read the following article, which will explain how to install and configure the Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span></span>

<span data-ttu-id="a5589-117">Dopo aver configurato i cmdlet PowerShell di Azure, è possibile eseguire le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="a5589-117">Once you’ve set up the Azure PowerShell cmdlets, you can perform the following tasks:</span></span>

* <span data-ttu-id="a5589-118">Elencare tutte le operazioni o azioni di un provider di risorse</span><span class="sxs-lookup"><span data-stu-id="a5589-118">List all the operations/actions for a resource provider</span></span>
* <span data-ttu-id="a5589-119">Elencare le azioni di un particolare ruolo:</span><span class="sxs-lookup"><span data-stu-id="a5589-119">List actions in a particular role:</span></span>
* <span data-ttu-id="a5589-120">Creare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="a5589-120">Create a custom role</span></span>

<span data-ttu-id="a5589-121">Lo script di PowerShell seguente offre alcuni esempi di esecuzione di queste attività:</span><span class="sxs-lookup"><span data-stu-id="a5589-121">The following PowerShell script illustrates examples of how to perform these tasks:</span></span>

    ‘List all the operations/actions for a resource provider.
    Get-AzureRmProviderOperation -OperationSearchString "Microsoft.DevTestLab/*"

    ‘List actions in a particular role.
    (Get-AzureRmRoleDefinition "DevTest Labs User").Actions

    ‘Create custom role.
    $policyRoleDef = (Get-AzureRmRoleDefinition "DevTest Labs User")
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "Policy Contributor"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("/subscriptions/<SubscriptionID> ")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/policySets/policies/*")
    $policyRoleDef = (New-AzureRmRoleDefinition -Role $policyRoleDef)

## <a name="assigning-permissions-to-a-user-for-a-specific-policy-using-custom-roles"></a><span data-ttu-id="a5589-122">Assegnazione agli utenti delle autorizzazioni per un criterio specifico tramite ruoli personalizzati</span><span class="sxs-lookup"><span data-stu-id="a5589-122">Assigning permissions to a user for a specific policy using custom roles</span></span>
<span data-ttu-id="a5589-123">Dopo aver definito i ruoli personalizzati, è possibile assegnarli agli utenti.</span><span class="sxs-lookup"><span data-stu-id="a5589-123">Once you’ve defined your custom roles, you can assign them to users.</span></span> <span data-ttu-id="a5589-124">Per assegnare un ruolo personalizzato a un utente, è necessario prima ottenere il valore **ObjectId** che rappresenta l'utente.</span><span class="sxs-lookup"><span data-stu-id="a5589-124">In order to assign a custom role to a user, you must first obtain the **ObjectId** representing that user.</span></span> <span data-ttu-id="a5589-125">A tale scopo, usare il cmdlet **Get-AzureRmADUser** .</span><span class="sxs-lookup"><span data-stu-id="a5589-125">To do that, use the **Get-AzureRmADUser** cmdlet.</span></span>

<span data-ttu-id="a5589-126">Nell'esempio seguente il valore **ObjectId** dell'utente *SomeUser* è 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span><span class="sxs-lookup"><span data-stu-id="a5589-126">In the following example, the **ObjectId** of the *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span></span>

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

<span data-ttu-id="a5589-127">Dopo avere ottenuto il valore **ObjectId** dell'utente e il nome di un ruolo personalizzato, è possibile assegnare il ruolo all'utente usando il cmdlet **New-AzureRmRoleAssignment**:</span><span class="sxs-lookup"><span data-stu-id="a5589-127">Once you have the **ObjectId** for the user and a custom role name, you can assign that role to the user with the **New-AzureRmRoleAssignment** cmdlet:</span></span>

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

<span data-ttu-id="a5589-128">Nell'esempio precedente viene usato il criterio **AllowedVmSizesInLab** .</span><span class="sxs-lookup"><span data-stu-id="a5589-128">In the previous example, the **AllowedVmSizesInLab** policy is used.</span></span> <span data-ttu-id="a5589-129">È possibile usare uno dei seguenti criteri:</span><span class="sxs-lookup"><span data-stu-id="a5589-129">You can use any of the following polices:</span></span>

* <span data-ttu-id="a5589-130">MaxVmsAllowedPerUser</span><span class="sxs-lookup"><span data-stu-id="a5589-130">MaxVmsAllowedPerUser</span></span>
* <span data-ttu-id="a5589-131">MaxVmsAllowedPerLab</span><span class="sxs-lookup"><span data-stu-id="a5589-131">MaxVmsAllowedPerLab</span></span>
* <span data-ttu-id="a5589-132">AllowedVmSizesInLab</span><span class="sxs-lookup"><span data-stu-id="a5589-132">AllowedVmSizesInLab</span></span>
* <span data-ttu-id="a5589-133">LabVmsShutdown</span><span class="sxs-lookup"><span data-stu-id="a5589-133">LabVmsShutdown</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="a5589-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a5589-134">Next steps</span></span>
<span data-ttu-id="a5589-135">Dopo aver concesso le autorizzazioni utente per specifici criteri di lab, considerare i seguenti passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="a5589-135">Once you've granted user permissions to specific lab policies, here are some next steps to consider:</span></span>

* <span data-ttu-id="a5589-136">[Proteggere l'accesso a un lab](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="a5589-136">[Secure access to a lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="a5589-137">[Definire i criteri del lab](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="a5589-137">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="a5589-138">[Creare un modello di lab](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="a5589-138">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="a5589-139">[Creare elementi personalizzati per le VM](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="a5589-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="a5589-140">[Aggiungere una VM con elementi a un lab](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="a5589-140">[Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

