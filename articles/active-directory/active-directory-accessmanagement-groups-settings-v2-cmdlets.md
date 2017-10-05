---
title: Esempi di PowerShell per la gestione di gruppi in Azure Active Directory | Microsoft Docs
description: Questa pagina riporta esempi di PowerShell per la gestione dei gruppi in Azure Active Directory
keywords: Azure AD, Azure Active Directory, PowerShell, gruppi, gestione dei gruppi
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7a5023dc-2727-4c25-8254-b531fc3244ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: rodejo
ms.openlocfilehash: a81820bc778c26f6e8051e2817ebd2b9c24b697a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a><span data-ttu-id="3836f-104">Cmdlet di Azure Active Directory versione 2 per la gestione dei gruppi</span><span class="sxs-lookup"><span data-stu-id="3836f-104">Azure Active Directory version 2 cmdlets for group management</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3836f-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3836f-105">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="3836f-106">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="3836f-106">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="3836f-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3836f-107">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="3836f-108">Questo articolo contiene esempi di come usare PowerShell per gestire i gruppi in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3836f-108">This article contains examples of how to use PowerShell to manage your groups in Azure Active Directory (Azure AD).</span></span>  <span data-ttu-id="3836f-109">Offre inoltre informazioni su come configurare il modulo Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3836f-109">It also tells you how to get set up with the Azure AD PowerShell module.</span></span> <span data-ttu-id="3836f-110">In primo luogo è necessario [scaricare il modulo Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="3836f-110">First, you must [download the Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="installing-the-azure-ad-powershell-module"></a><span data-ttu-id="3836f-111">Installazione del modulo Azure AD PowerShell</span><span class="sxs-lookup"><span data-stu-id="3836f-111">Installing the Azure AD PowerShell module</span></span>
<span data-ttu-id="3836f-112">Per installare il modulo Azure AD PowerShell, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3836f-112">To install the Azure AD PowerShell module, use the following commands:</span></span>

    PS C:\Windows\system32> install-module azuread

<span data-ttu-id="3836f-113">Per verificare che il modulo sia stato installato, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3836f-113">To verify that the module was installed, use the following command:</span></span>

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

<span data-ttu-id="3836f-114">A questo punto è possibile iniziare a usare i cmdlet nel modulo.</span><span class="sxs-lookup"><span data-stu-id="3836f-114">Now you can start using the cmdlets in the module.</span></span> <span data-ttu-id="3836f-115">Per una descrizione completa dei cmdlet nel modulo Azure AD, consultare la documentazione di riferimento online per [Azure Active Directory PowerShell versione 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="3836f-115">For a full description of the cmdlets in the Azure AD module, please refer to the online reference documentation for [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="connecting-to-the-directory"></a><span data-ttu-id="3836f-116">Connessione alla directory</span><span class="sxs-lookup"><span data-stu-id="3836f-116">Connecting to the directory</span></span>
<span data-ttu-id="3836f-117">Prima di iniziare la gestione di gruppi mediante i cmdlet PowerShell di Azure AD, è necessario connettere la sessione di PowerShell alla directory da gestire.</span><span class="sxs-lookup"><span data-stu-id="3836f-117">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session to the directory you want to manage.</span></span> <span data-ttu-id="3836f-118">Usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3836f-118">Use the following command:</span></span>

    PS C:\Windows\system32> Connect-AzureAD

<span data-ttu-id="3836f-119">Il cmdlet richiede le credenziali da usare per accedere alla directory.</span><span class="sxs-lookup"><span data-stu-id="3836f-119">The cmdlet prompts you for the credentials you want to use to access your directory.</span></span> <span data-ttu-id="3836f-120">In questo esempio si usa karen@drumkit.onmicrosoft.com per accedere alla directory dimostrativa.</span><span class="sxs-lookup"><span data-stu-id="3836f-120">In this example, we are using karen@drumkit.onmicrosoft.com to access the demonstration directory.</span></span> <span data-ttu-id="3836f-121">Il cmdlet restituisce un messaggio di conferma per indicare che la sessione è stata connessa correttamente alla directory:</span><span class="sxs-lookup"><span data-stu-id="3836f-121">The cmdlet returns a confirmation to show the session was connected successfully to your directory:</span></span>

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

<span data-ttu-id="3836f-122">A questo punto è possibile iniziare a usare i cmdlet di Azure AD per gestire i gruppi nella directory.</span><span class="sxs-lookup"><span data-stu-id="3836f-122">Now you can start using the AzureAD cmdlets to manage groups in your directory.</span></span>

## <a name="retrieving-groups"></a><span data-ttu-id="3836f-123">Recupero di gruppi</span><span class="sxs-lookup"><span data-stu-id="3836f-123">Retrieving groups</span></span>
<span data-ttu-id="3836f-124">Per recuperare i gruppi esistenti dalla directory è possibile usare il cmdlet Get-AzureADGroups.</span><span class="sxs-lookup"><span data-stu-id="3836f-124">To retrieve existing groups from your directory you can use the Get-AzureADGroups cmdlet.</span></span> <span data-ttu-id="3836f-125">Per recuperare tutti i gruppi nella directory, usare il cmdlet senza parametri:</span><span class="sxs-lookup"><span data-stu-id="3836f-125">To retrieve all groups in the directory, use the cmdlet without parameters:</span></span>

    PS C:\Windows\system32> get-azureadgroup

<span data-ttu-id="3836f-126">Il cmdlet restituisce tutti i gruppi nella directory connessa.</span><span class="sxs-lookup"><span data-stu-id="3836f-126">The cmdlet returns all groups in the connected directory.</span></span>

<span data-ttu-id="3836f-127">È possibile usare il parametro -objectID per recuperare un gruppo specifico indicando l'objectID del gruppo:</span><span class="sxs-lookup"><span data-stu-id="3836f-127">You can use the -objectID parameter to retrieve a specific group for which you specify the group’s objectID:</span></span>

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

<span data-ttu-id="3836f-128">Il cmdlet restituisce ora il gruppo il cui objectID corrisponde al valore del parametro immesso:</span><span class="sxs-lookup"><span data-stu-id="3836f-128">The cmdlet now returns the group whose objectID matches the value of the parameter you entered:</span></span>

    DeletionTimeStamp            :
    ObjectId                     : e29bae11-4ac0-450c-bc37-6dae8f3da61b
    ObjectType                   : Group
    Description                  :
    DirSyncEnabled               :
    DisplayName                  : Pacific NW Support
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 9bb4139b-60a1-434a-8c0d-7c1f8eee2df9
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

<span data-ttu-id="3836f-129">È possibile cercare un gruppo specifico usando il parametro -filter.</span><span class="sxs-lookup"><span data-stu-id="3836f-129">You can search for a specific group using the -filter parameter.</span></span> <span data-ttu-id="3836f-130">Questo parametro accetta una clausola di filtro ODATA e restituisce tutti i gruppi che corrispondono al filtro, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="3836f-130">This parameter takes an ODATA filter clause and returns all groups that match the filter, as in the following example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

> [!NOTE] 
> <span data-ttu-id="3836f-131">I cdmlet di AzureAD PowerShell implementano lo standard di query OData.</span><span class="sxs-lookup"><span data-stu-id="3836f-131">The AzureAD PowerShell cmdlets implement the OData query standard.</span></span> <span data-ttu-id="3836f-132">Per altre informazioni, vedere **$filter** in [Opzioni query di sistema OData usando l'endpoint OData](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span><span class="sxs-lookup"><span data-stu-id="3836f-132">For more information, see **$filter** in [OData system query options using the OData endpoint](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span></span>

## <a name="creating-groups"></a><span data-ttu-id="3836f-133">Creazione di gruppi</span><span class="sxs-lookup"><span data-stu-id="3836f-133">Creating groups</span></span>
<span data-ttu-id="3836f-134">Per creare un nuovo gruppo nella directory, usare il cmdlet New-AzureADGroup.</span><span class="sxs-lookup"><span data-stu-id="3836f-134">To create a new group in your directory, use the New-AzureADGroup cmdlet.</span></span> <span data-ttu-id="3836f-135">Questo cmdlet crea un nuovo gruppo di sicurezza denominato "Marketing":</span><span class="sxs-lookup"><span data-stu-id="3836f-135">This cmdlet creates a new security group called “Marketing":</span></span>

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a><span data-ttu-id="3836f-136">Aggiornamento di gruppi</span><span class="sxs-lookup"><span data-stu-id="3836f-136">Updating groups</span></span>
<span data-ttu-id="3836f-137">Per aggiornare un gruppo esistente, usare il cmdlet Set-AzureADGroup.</span><span class="sxs-lookup"><span data-stu-id="3836f-137">To update an existing group, use the Set-AzureADGroup cmdlet.</span></span> <span data-ttu-id="3836f-138">In questo esempio stiamo cambiando la proprietà DisplayName del gruppo "Amministratori di Intune".</span><span class="sxs-lookup"><span data-stu-id="3836f-138">In this example, we’re changing the DisplayName property of the group “Intune Administrators.”</span></span> <span data-ttu-id="3836f-139">In primo luogo si cerca il gruppo mediante il cmdlet Get-AzureADGroup e si applica il filtro tramite l'attributo DisplayName:</span><span class="sxs-lookup"><span data-stu-id="3836f-139">First, we’re finding the group using the Get-AzureADGroup cmdlet and filter using the DisplayName attribute:</span></span>

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

<span data-ttu-id="3836f-140">Quindi si cambia la proprietà Description nel nuovo valore "Amministratori di dispositivi Intune":</span><span class="sxs-lookup"><span data-stu-id="3836f-140">Next, we’re changing the Description property to the new value “Intune Device Administrators”:</span></span>

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

<span data-ttu-id="3836f-141">Ora, se si cerca il gruppo nuovamente, si noterà che la proprietà Description è stata aggiornata con il nuovo valore:</span><span class="sxs-lookup"><span data-stu-id="3836f-141">Now if we find the group again, we see the Description property is updated to reflect the new value:</span></span>

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Device Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

## <a name="deleting-groups"></a><span data-ttu-id="3836f-142">Eliminazione di gruppi</span><span class="sxs-lookup"><span data-stu-id="3836f-142">Deleting groups</span></span>
<span data-ttu-id="3836f-143">Per eliminare gruppi dalla directory, usare il cmdlet Remove-AzureADGroup come segue:</span><span class="sxs-lookup"><span data-stu-id="3836f-143">To delete groups from your directory, use the Remove-AzureADGroup cmdlet as follows:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a><span data-ttu-id="3836f-144">Gestione dei membri dei gruppi</span><span class="sxs-lookup"><span data-stu-id="3836f-144">Managing members of groups</span></span>
<span data-ttu-id="3836f-145">Per aggiungere nuovi membri a un gruppo, si usa il cmdlet Add-AzureADGroupMember.</span><span class="sxs-lookup"><span data-stu-id="3836f-145">If you need to add new members to a group, use the Add-AzureADGroupMember cmdlet.</span></span> <span data-ttu-id="3836f-146">Questo comando aggiunge un membro al gruppo degli amministratori di Intune che abbiamo usato nell'esempio precedente:</span><span class="sxs-lookup"><span data-stu-id="3836f-146">This command adds a member to the Intune Administrators group we used in the previous example:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="3836f-147">Il parametro -ObjectId è il valore ObjectID del gruppo a cui si vuole aggiungere un membro e -RefObjectId è il valore ObjectID dell'utente da aggiungere come membro al gruppo.</span><span class="sxs-lookup"><span data-stu-id="3836f-147">The -ObjectId parameter is the ObjectID of the group to which we want to add a member, and the -RefObjectId is the ObjectID of the user we want to add as a member to the group.</span></span>

<span data-ttu-id="3836f-148">Per ottenere i membri di un gruppo esistente, usare il cmdlet Get-AzureADGroupMember, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="3836f-148">To get the existing members of a group, use the Get-AzureADGroupMember cmdlet, as in this example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

<span data-ttu-id="3836f-149">Per rimuovere il membro aggiunto al gruppo in precedenza, usare il cmdlet Remove-AzureADGroupMember, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3836f-149">To remove the member we previously added to the group, use the Remove-AzureADGroupMember cmdlet, as is shown here:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="3836f-150">Per verificare l'appartenenza al gruppo di un utente, usare il cmdlet Select-AzureADGroupIdsUserIsMemberOf.</span><span class="sxs-lookup"><span data-stu-id="3836f-150">To verify the group membership(s) of a user, use the Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span></span> <span data-ttu-id="3836f-151">Questo cmdlet accetta come parametri il valore ObjectId dell'utente di cui controllare l'appartenenza al gruppo e l'elenco dei gruppi da controllare.</span><span class="sxs-lookup"><span data-stu-id="3836f-151">This cmdlet takes as its parameters the ObjectId of the user for which to check the group memberships, and a list of groups for which to check the memberships.</span></span> <span data-ttu-id="3836f-152">L'elenco dei gruppi deve essere fornito sotto forma di variabile complessa di tipo "Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck", pertanto è necessario innanzitutto creare una variabile con tale tipo:</span><span class="sxs-lookup"><span data-stu-id="3836f-152">The list of groups must be provided in the form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span></span>

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

<span data-ttu-id="3836f-153">È quindi necessario fornire i valori per i groupId da controllare nell'attributo "GroupIds" della variabile complessa:</span><span class="sxs-lookup"><span data-stu-id="3836f-153">Next, we provide values for the groupIds to check in the attribute “GroupIds” of this complex variable:</span></span>

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

<span data-ttu-id="3836f-154">Se si desidera controllare l'appartenenza di un utente con ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea ai gruppi di $g, si usa:</span><span class="sxs-lookup"><span data-stu-id="3836f-154">Now, if we want to check the group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against the groups in $g, we should use:</span></span>

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


<span data-ttu-id="3836f-155">Il valore restituito è un elenco dei gruppi di cui l'utente è membro.</span><span class="sxs-lookup"><span data-stu-id="3836f-155">The value returned is a list of groups of which this user is a member.</span></span> <span data-ttu-id="3836f-156">È possibile applicare questo metodo anche per controllare l'appartenenza di contatti, gruppi o entità servizio a un elenco di gruppi, tramite Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf o Select-AzureADGroupIdsServicePrincipalIsMemberOf</span><span class="sxs-lookup"><span data-stu-id="3836f-156">You can also apply this method to check Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span></span>

## <a name="managing-owners-of-groups"></a><span data-ttu-id="3836f-157">Gestione dei proprietari dei gruppi</span><span class="sxs-lookup"><span data-stu-id="3836f-157">Managing owners of groups</span></span>
<span data-ttu-id="3836f-158">Per aggiungere proprietari a un gruppo, usare il cmdlet AzureADGroupOwner:</span><span class="sxs-lookup"><span data-stu-id="3836f-158">To add owners to a group, use the Add-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="3836f-159">Il parametro -ObjectId è il valore ObjectID del gruppo a cui si vuole aggiungere un proprietario e -RefObjectId è il valore ObjectID dell'utente da aggiungere come proprietario al gruppo.</span><span class="sxs-lookup"><span data-stu-id="3836f-159">The -ObjectId parameter is the ObjectID of the group to which we want to add an owner, and the -RefObjectId is the ObjectID of the user we want to add as an owner of the group.</span></span>

<span data-ttu-id="3836f-160">Per recuperare i proprietari di un gruppo, usare il cmdlet Get-AzureADGroupOwner:</span><span class="sxs-lookup"><span data-stu-id="3836f-160">To retrieve the owners of a group, use the Get-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

<span data-ttu-id="3836f-161">Il cmdlet restituisce l'elenco dei proprietari per il gruppo specificato:</span><span class="sxs-lookup"><span data-stu-id="3836f-161">The cmdlet returns the list of owners for the specified group:</span></span>

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

<span data-ttu-id="3836f-162">Per rimuovere un proprietario da un gruppo, usare il cmdlet Remove-AzureADGroupOwner:</span><span class="sxs-lookup"><span data-stu-id="3836f-162">If you want to remove an owner from a group, use the Remove-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a><span data-ttu-id="3836f-163">Alias riservati</span><span class="sxs-lookup"><span data-stu-id="3836f-163">Reserved aliases</span></span> 
<span data-ttu-id="3836f-164">Quando viene creato un gruppo, alcuni endpoint consentono all'utente finale di specificare un attributo mailNickname o un alias da usare come parte dell'indirizzo e-mail del gruppo.</span><span class="sxs-lookup"><span data-stu-id="3836f-164">When a group is created, certain endpoints allow the end user to specify a mailNickname or alias to be used as part of the email address of the group.</span></span> <span data-ttu-id="3836f-165">I gruppi con gli alias di posta elettronica con privilegi elevati seguenti possono essere creati solo da un amministratore globale di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3836f-165">Groups with the following highly privileged email aliases can only be created by an Azure AD global administrator.</span></span> 
  
* <span data-ttu-id="3836f-166">abuse</span><span class="sxs-lookup"><span data-stu-id="3836f-166">abuse</span></span> 
* <span data-ttu-id="3836f-167">admin</span><span class="sxs-lookup"><span data-stu-id="3836f-167">admin</span></span> 
* <span data-ttu-id="3836f-168">entità</span><span class="sxs-lookup"><span data-stu-id="3836f-168">administrator</span></span> 
* <span data-ttu-id="3836f-169">hostmaster</span><span class="sxs-lookup"><span data-stu-id="3836f-169">hostmaster</span></span> 
* <span data-ttu-id="3836f-170">majordomo</span><span class="sxs-lookup"><span data-stu-id="3836f-170">majordomo</span></span> 
* <span data-ttu-id="3836f-171">postmaster</span><span class="sxs-lookup"><span data-stu-id="3836f-171">postmaster</span></span> 
* <span data-ttu-id="3836f-172">root</span><span class="sxs-lookup"><span data-stu-id="3836f-172">root</span></span> 
* <span data-ttu-id="3836f-173">secure</span><span class="sxs-lookup"><span data-stu-id="3836f-173">secure</span></span> 
* <span data-ttu-id="3836f-174">security</span><span class="sxs-lookup"><span data-stu-id="3836f-174">security</span></span> 
* <span data-ttu-id="3836f-175">ssl-admin</span><span class="sxs-lookup"><span data-stu-id="3836f-175">ssl-admin</span></span> 
* <span data-ttu-id="3836f-176">webmaster</span><span class="sxs-lookup"><span data-stu-id="3836f-176">webmaster</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3836f-177">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3836f-177">Next steps</span></span>
<span data-ttu-id="3836f-178">Per altre informazioni su Azure Active Directory PowerShell, consultare la documentazione sui [cmdlet di Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="3836f-178">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

* [<span data-ttu-id="3836f-179">Gestione dell'accesso alle risorse tramite i gruppi di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3836f-179">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="3836f-180">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3836f-180">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
