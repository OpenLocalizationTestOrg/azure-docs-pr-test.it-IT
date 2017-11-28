---
title: criteri di lab toospecific autorizzazioni utente aaaGrant | Documenti Microsoft
description: Informazioni su come criteri lab toospecific toogrant utente le autorizzazioni in DevTest Labs in base alle esigenze di ciascun utente
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
ms.openlocfilehash: 35647ab837243188f06566cdf365b67fe33a3865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="grant-user-permissions-toospecific-lab-policies"></a><span data-ttu-id="cab1b-103">Concedere le autorizzazioni utente criteri lab toospecific</span><span class="sxs-lookup"><span data-stu-id="cab1b-103">Grant user permissions toospecific lab policies</span></span>
## <a name="overview"></a><span data-ttu-id="cab1b-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="cab1b-104">Overview</span></span>
<span data-ttu-id="cab1b-105">Questo articolo illustra come toouse criteri lab particolare tooa di PowerShell toogrant agli utenti le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="cab1b-105">This article illustrates how toouse PowerShell toogrant users permissions tooa particular lab policy.</span></span> <span data-ttu-id="cab1b-106">In questo modo, le autorizzazioni possono essere applicate in base alle esigenze di ciascun utente.</span><span class="sxs-lookup"><span data-stu-id="cab1b-106">That way, permissions can be applied based on each user's needs.</span></span> <span data-ttu-id="cab1b-107">Ad esempio, è possibile toogrant impostazioni dei criteri un determinato utente hello possibilità toochange hello VM, ma non hello costo criteri.</span><span class="sxs-lookup"><span data-stu-id="cab1b-107">For example, you might want toogrant a particular user hello ability toochange hello VM policy settings, but not hello cost policies.</span></span>

## <a name="policies-as-resources"></a><span data-ttu-id="cab1b-108">Criteri come risorse</span><span class="sxs-lookup"><span data-stu-id="cab1b-108">Policies as resources</span></span>
<span data-ttu-id="cab1b-109">Come descritto in hello [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) articolo RBAC consente la gestione di accesso con granularità fine delle risorse per Azure.</span><span class="sxs-lookup"><span data-stu-id="cab1b-109">As discussed in hello [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC enables fine-grained access management of resources for Azure.</span></span> <span data-ttu-id="cab1b-110">Usa tale controllo, è possibile separare i compiti all'interno del team di DevOps e concedere solo quantità hello di accesso toousers necessarie tooperform i processi.</span><span class="sxs-lookup"><span data-stu-id="cab1b-110">Using RBAC, you can segregate duties within your DevOps team and grant only hello amount of access toousers that they need tooperform their jobs.</span></span>

<span data-ttu-id="cab1b-111">In DevTest Labs, un criterio è un tipo di risorsa che consente di azione RBAC hello **Microsoft.DevTestLab/labs/policySets/policies/**.</span><span class="sxs-lookup"><span data-stu-id="cab1b-111">In DevTest Labs, a policy is a resource type that enables hello RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span></span> <span data-ttu-id="cab1b-112">Ogni criterio lab è una risorsa nel tipo di risorsa criteri hello e può essere assegnato il ruolo RBAC tooan ambito.</span><span class="sxs-lookup"><span data-stu-id="cab1b-112">Each lab policy is a resource in hello Policy resource type, and can be assigned as a scope tooan RBAC role.</span></span>

<span data-ttu-id="cab1b-113">Ad esempio, in ordine toogrant agli utenti di lettura/scrittura autorizzazione toohello **dimensioni delle macchine Virtuali consentite** criteri, è necessario creare un ruolo personalizzato che funziona con hello **Microsoft.DevTestLab/labs/policySets/policies/** * azione, quindi assegnare hello utenti appropriati toothis ruolo personalizzato nell'ambito di hello di **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span><span class="sxs-lookup"><span data-stu-id="cab1b-113">For example, in order toogrant users read/write permission toohello **Allowed VM Sizes** policy, you would create a custom role that works with hello **Microsoft.DevTestLab/labs/policySets/policies/*** action, and then assign hello appropriate users toothis custom role in hello scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span></span>

<span data-ttu-id="cab1b-114">toolearn ulteriori informazioni sui ruoli personalizzati in RBAC, vedere hello [controllo di accesso di ruoli personalizzato](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="cab1b-114">toolearn more about custom roles in RBAC, see hello [Custom roles access control](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="creating-a-lab-custom-role-using-powershell"></a><span data-ttu-id="cab1b-115">Creazione di un ruolo personalizzato lab tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="cab1b-115">Creating a lab custom role using PowerShell</span></span>
<span data-ttu-id="cab1b-116">In ordine tooget avviato, è necessario hello tooread seguente articolo verrà illustrato come tooinstall e configurare i cmdlet di Azure PowerShell hello: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span><span class="sxs-lookup"><span data-stu-id="cab1b-116">In order tooget started, you’ll need tooread hello following article, which will explain how tooinstall and configure hello Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span></span>

<span data-ttu-id="cab1b-117">Dopo aver impostato hello cmdlet PowerShell di Azure, è possibile eseguire hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="cab1b-117">Once you’ve set up hello Azure PowerShell cmdlets, you can perform hello following tasks:</span></span>

* <span data-ttu-id="cab1b-118">Elenco di tutte le operazioni di hello/azioni per un provider di risorse</span><span class="sxs-lookup"><span data-stu-id="cab1b-118">List all hello operations/actions for a resource provider</span></span>
* <span data-ttu-id="cab1b-119">Elencare le azioni di un particolare ruolo:</span><span class="sxs-lookup"><span data-stu-id="cab1b-119">List actions in a particular role:</span></span>
* <span data-ttu-id="cab1b-120">Creare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="cab1b-120">Create a custom role</span></span>

<span data-ttu-id="cab1b-121">Hello lo script di PowerShell seguente vengono illustrati esempi di come tooperform queste attività:</span><span class="sxs-lookup"><span data-stu-id="cab1b-121">hello following PowerShell script illustrates examples of how tooperform these tasks:</span></span>

    ‘List all hello operations/actions for a resource provider.
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

## <a name="assigning-permissions-tooa-user-for-a-specific-policy-using-custom-roles"></a><span data-ttu-id="cab1b-122">Assegnazione di autorizzazioni tooa utente per un criterio specifico utilizzando ruoli personalizzati</span><span class="sxs-lookup"><span data-stu-id="cab1b-122">Assigning permissions tooa user for a specific policy using custom roles</span></span>
<span data-ttu-id="cab1b-123">Dopo aver definito i ruoli personalizzati, è possibile assegnarli toousers.</span><span class="sxs-lookup"><span data-stu-id="cab1b-123">Once you’ve defined your custom roles, you can assign them toousers.</span></span> <span data-ttu-id="cab1b-124">In ordine tooassign utente tooa ruolo personalizzato, è innanzitutto necessario ottenere hello **ObjectId** che rappresenta tale utente.</span><span class="sxs-lookup"><span data-stu-id="cab1b-124">In order tooassign a custom role tooa user, you must first obtain hello **ObjectId** representing that user.</span></span> <span data-ttu-id="cab1b-125">toodo utilizzati, hello **Get AzureRmADUser** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cab1b-125">toodo that, use hello **Get-AzureRmADUser** cmdlet.</span></span>

<span data-ttu-id="cab1b-126">Nell'esempio seguente di hello, hello **ObjectId** di hello *SomeUser* utente è 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span><span class="sxs-lookup"><span data-stu-id="cab1b-126">In hello following example, hello **ObjectId** of hello *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span></span>

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

<span data-ttu-id="cab1b-127">Dopo aver hello **ObjectId** per utente hello e un nome di ruolo personalizzata, è possibile assegnare a tale utente toohello ruolo con hello **New AzureRmRoleAssignment** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="cab1b-127">Once you have hello **ObjectId** for hello user and a custom role name, you can assign that role toohello user with hello **New-AzureRmRoleAssignment** cmdlet:</span></span>

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

<span data-ttu-id="cab1b-128">Nell'esempio precedente hello hello **AllowedVmSizesInLab** criteri vengono usati.</span><span class="sxs-lookup"><span data-stu-id="cab1b-128">In hello previous example, hello **AllowedVmSizesInLab** policy is used.</span></span> <span data-ttu-id="cab1b-129">È possibile utilizzare uno qualsiasi dei seguenti criteri hello:</span><span class="sxs-lookup"><span data-stu-id="cab1b-129">You can use any of hello following polices:</span></span>

* <span data-ttu-id="cab1b-130">MaxVmsAllowedPerUser</span><span class="sxs-lookup"><span data-stu-id="cab1b-130">MaxVmsAllowedPerUser</span></span>
* <span data-ttu-id="cab1b-131">MaxVmsAllowedPerLab</span><span class="sxs-lookup"><span data-stu-id="cab1b-131">MaxVmsAllowedPerLab</span></span>
* <span data-ttu-id="cab1b-132">AllowedVmSizesInLab</span><span class="sxs-lookup"><span data-stu-id="cab1b-132">AllowedVmSizesInLab</span></span>
* <span data-ttu-id="cab1b-133">LabVmsShutdown</span><span class="sxs-lookup"><span data-stu-id="cab1b-133">LabVmsShutdown</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="cab1b-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cab1b-134">Next steps</span></span>
<span data-ttu-id="cab1b-135">Una volta sono state concesse le autorizzazioni toospecific lab i criteri utente, ecco alcuni tooconsider passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="cab1b-135">Once you've granted user permissions toospecific lab policies, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="cab1b-136">[Lab tooa accesso sicuro](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="cab1b-136">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="cab1b-137">[Definire i criteri del lab](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="cab1b-137">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="cab1b-138">[Creare un modello di lab](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="cab1b-138">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="cab1b-139">[Creare elementi personalizzati per le VM](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="cab1b-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="cab1b-140">[Aggiungere una macchina virtuale con lab tooa elementi](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="cab1b-140">[Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

