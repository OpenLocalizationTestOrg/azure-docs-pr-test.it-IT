---
title: esempi di aaaPowerShell per gestire i gruppi in Azure Active Directory | Documenti Microsoft
description: In questa pagina vengono toohelp esempi di PowerShell gestire i gruppi in Azure Active Directory
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
ms.openlocfilehash: ba049babc436e99a290f20899b3a87bcfa811d9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a><span data-ttu-id="0f5fd-104">Cmdlet di Azure Active Directory versione 2 per la gestione dei gruppi</span><span class="sxs-lookup"><span data-stu-id="0f5fd-104">Azure Active Directory version 2 cmdlets for group management</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0f5fd-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0f5fd-105">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="0f5fd-106">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="0f5fd-106">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="0f5fd-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f5fd-107">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="0f5fd-108">In questo articolo contiene esempi di come toouse PowerShell toomanage i gruppi in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0f5fd-108">This article contains examples of how toouse PowerShell toomanage your groups in Azure Active Directory (Azure AD).</span></span>  <span data-ttu-id="0f5fd-109">Indica inoltre come tooget impostare con il modulo di Azure AD PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-109">It also tells you how tooget set up with hello Azure AD PowerShell module.</span></span> <span data-ttu-id="0f5fd-110">In primo luogo, è necessario [scaricare il modulo di Azure AD PowerShell hello](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="0f5fd-110">First, you must [download hello Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="installing-hello-azure-ad-powershell-module"></a><span data-ttu-id="0f5fd-111">Installazione del modulo di Azure AD PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="0f5fd-111">Installing hello Azure AD PowerShell module</span></span>
<span data-ttu-id="0f5fd-112">hello tooinstall modulo Azure AD PowerShell, usare hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-112">tooinstall hello Azure AD PowerShell module, use hello following commands:</span></span>

    PS C:\Windows\system32> install-module azuread

<span data-ttu-id="0f5fd-113">tooverify che hello modulo è stato installato, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-113">tooverify that hello module was installed, use hello following command:</span></span>

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

<span data-ttu-id="0f5fd-114">Ora è possibile iniziare a utilizzare i cmdlet di hello nel modulo hello.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-114">Now you can start using hello cmdlets in hello module.</span></span> <span data-ttu-id="0f5fd-115">Per una descrizione completa di hello cmdlet nel modulo hello Azure AD, consultare la documentazione di riferimento online toohello per [Azure Active Directory PowerShell versione 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="0f5fd-115">For a full description of hello cmdlets in hello Azure AD module, please refer toohello online reference documentation for [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="connecting-toohello-directory"></a><span data-ttu-id="0f5fd-116">Connessione directory toohello</span><span class="sxs-lookup"><span data-stu-id="0f5fd-116">Connecting toohello directory</span></span>
<span data-ttu-id="0f5fd-117">Prima di iniziare la gestione dei gruppi tramite i cmdlet PowerShell di Azure Active Directory, è necessario connettersi desiderato toomanage directory toohello di sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-117">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session toohello directory you want toomanage.</span></span> <span data-ttu-id="0f5fd-118">Utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-118">Use hello following command:</span></span>

    PS C:\Windows\system32> Connect-AzureAD

<span data-ttu-id="0f5fd-119">Hello cmdlet è richiesto per hello credenziali si desidera che la directory toouse tooaccess.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-119">hello cmdlet prompts you for hello credentials you want toouse tooaccess your directory.</span></span> <span data-ttu-id="0f5fd-120">In questo esempio, utilizziamo karen@drumkit.onmicrosoft.com tooaccess hello directory dimostrazione.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-120">In this example, we are using karen@drumkit.onmicrosoft.com tooaccess hello demonstration directory.</span></span> <span data-ttu-id="0f5fd-121">Hello cmdlet restituisce è stata stabilita una sessione di hello tooshow conferma tooyour directory:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-121">hello cmdlet returns a confirmation tooshow hello session was connected successfully tooyour directory:</span></span>

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

<span data-ttu-id="0f5fd-122">Ora è possibile avviare l'utilizzo di hello AzureAD cmdlet toomanage gruppi nella directory.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-122">Now you can start using hello AzureAD cmdlets toomanage groups in your directory.</span></span>

## <a name="retrieving-groups"></a><span data-ttu-id="0f5fd-123">Recupero di gruppi</span><span class="sxs-lookup"><span data-stu-id="0f5fd-123">Retrieving groups</span></span>
<span data-ttu-id="0f5fd-124">tooretrieve gruppi esistenti dalla directory di cui che è possibile utilizzare hello cmdlet Get-AzureADGroups.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-124">tooretrieve existing groups from your directory you can use hello Get-AzureADGroups cmdlet.</span></span> <span data-ttu-id="0f5fd-125">tooretrieve tutti i gruppi nella directory di hello, utilizzare hello cmdlet senza parametri:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-125">tooretrieve all groups in hello directory, use hello cmdlet without parameters:</span></span>

    PS C:\Windows\system32> get-azureadgroup

<span data-ttu-id="0f5fd-126">cmdlet di Hello restituisce tutti i gruppi nella directory connessa hello.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-126">hello cmdlet returns all groups in hello connected directory.</span></span>

<span data-ttu-id="0f5fd-127">È possibile utilizzare hello - objectID parametro tooretrieve un gruppo specifico per il quale è specificare objectID del gruppo di hello:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-127">You can use hello -objectID parameter tooretrieve a specific group for which you specify hello group’s objectID:</span></span>

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

<span data-ttu-id="0f5fd-128">cmdlet di Hello restituisce ora gruppo hello cui objectID corrisponde al valore hello del parametro hello immessi:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-128">hello cmdlet now returns hello group whose objectID matches hello value of hello parameter you entered:</span></span>

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

<span data-ttu-id="0f5fd-129">È possibile cercare un gruppo specifico usando hello - parametro filter.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-129">You can search for a specific group using hello -filter parameter.</span></span> <span data-ttu-id="0f5fd-130">Questo parametro utilizza una clausola di filtro ODATA e restituisce tutti i gruppi che corrispondono al filtro hello, come in hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-130">This parameter takes an ODATA filter clause and returns all groups that match hello filter, as in hello following example:</span></span>

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
> <span data-ttu-id="0f5fd-131">i cmdlet di AzureAD PowerShell Hello implementare hello query OData standard.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-131">hello AzureAD PowerShell cmdlets implement hello OData query standard.</span></span> <span data-ttu-id="0f5fd-132">Per ulteriori informazioni, vedere **$filter** in [opzioni di query di sistema OData utilizzando l'endpoint OData hello](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span><span class="sxs-lookup"><span data-stu-id="0f5fd-132">For more information, see **$filter** in [OData system query options using hello OData endpoint](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span></span>

## <a name="creating-groups"></a><span data-ttu-id="0f5fd-133">Creazione di gruppi</span><span class="sxs-lookup"><span data-stu-id="0f5fd-133">Creating groups</span></span>
<span data-ttu-id="0f5fd-134">toocreate un nuovo gruppo nella directory, utilizzare cmdlet di hello AzureADGroup di nuovo.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-134">toocreate a new group in your directory, use hello New-AzureADGroup cmdlet.</span></span> <span data-ttu-id="0f5fd-135">Questo cmdlet crea un nuovo gruppo di sicurezza denominato "Marketing":</span><span class="sxs-lookup"><span data-stu-id="0f5fd-135">This cmdlet creates a new security group called “Marketing":</span></span>

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a><span data-ttu-id="0f5fd-136">Aggiornamento di gruppi</span><span class="sxs-lookup"><span data-stu-id="0f5fd-136">Updating groups</span></span>
<span data-ttu-id="0f5fd-137">tooupdate un gruppo esistente, utilizzare il cmdlet Set-AzureADGroup hello.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-137">tooupdate an existing group, use hello Set-AzureADGroup cmdlet.</span></span> <span data-ttu-id="0f5fd-138">In questo esempio, stiamo cambiando hello proprietà DisplayName del gruppo di hello ""Intune Administrators.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-138">In this example, we’re changing hello DisplayName property of hello group “Intune Administrators.”</span></span> <span data-ttu-id="0f5fd-139">È in primo luogo, stiamo ricerca gruppo hello utilizzando i cmdlet Get-AzureADGroup hello e filtro utilizzando l'attributo DisplayName hello:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-139">First, we’re finding hello group using hello Get-AzureADGroup cmdlet and filter using hello DisplayName attribute:</span></span>

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

<span data-ttu-id="0f5fd-140">Successivamente, stiamo cambiando hello descrizione toohello nuovo valore della proprietà "Amministratori dispositivo Intune":</span><span class="sxs-lookup"><span data-stu-id="0f5fd-140">Next, we’re changing hello Description property toohello new value “Intune Device Administrators”:</span></span>

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

<span data-ttu-id="0f5fd-141">Ora è ritrovare gruppo hello, è possibile notare proprietà Description hello viene aggiornato tooreflect hello nuovo valore:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-141">Now if we find hello group again, we see hello Description property is updated tooreflect hello new value:</span></span>

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

## <a name="deleting-groups"></a><span data-ttu-id="0f5fd-142">Eliminazione di gruppi</span><span class="sxs-lookup"><span data-stu-id="0f5fd-142">Deleting groups</span></span>
<span data-ttu-id="0f5fd-143">gruppi toodelete dalla directory, utilizzare i cmdlet Remove-AzureADGroup hello come segue:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-143">toodelete groups from your directory, use hello Remove-AzureADGroup cmdlet as follows:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a><span data-ttu-id="0f5fd-144">Gestione dei membri dei gruppi</span><span class="sxs-lookup"><span data-stu-id="0f5fd-144">Managing members of groups</span></span>
<span data-ttu-id="0f5fd-145">Se è necessario nuovo gruppo di tooa membri tooadd, utilizzare il cmdlet Add-AzureADGroupMember hello.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-145">If you need tooadd new members tooa group, use hello Add-AzureADGroupMember cmdlet.</span></span> <span data-ttu-id="0f5fd-146">Questo comando aggiunge un gruppo di amministratori di Intune toohello membro che è stato usato nell'esempio precedente hello:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-146">This command adds a member toohello Intune Administrators group we used in hello previous example:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="0f5fd-147">il parametro - ObjectId Hello è hello ObjectID di hello gruppo toowhich desideriamo tooadd un membro e - RefObjectId hello è hello ObjectID dell'utente hello desideriamo tooadd come gruppo toohello membro.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-147">hello -ObjectId parameter is hello ObjectID of hello group toowhich we want tooadd a member, and hello -RefObjectId is hello ObjectID of hello user we want tooadd as a member toohello group.</span></span>

<span data-ttu-id="0f5fd-148">i membri esistenti tooget hello di un gruppo, utilizzare cmdlet Get-AzureADGroupMember hello, come nel seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-148">tooget hello existing members of a group, use hello Get-AzureADGroupMember cmdlet, as in this example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

<span data-ttu-id="0f5fd-149">membro hello tooremove è stato aggiunto in precedenza toohello gruppo, utilizzare Remove-AzureADGroupMember hello cmdlet, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-149">tooremove hello member we previously added toohello group, use hello Remove-AzureADGroupMember cmdlet, as is shown here:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="0f5fd-150">tooverify hello gruppo appartenenze di un utente, utilizzare cmdlet Select-AzureADGroupIdsUserIsMemberOf hello.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-150">tooverify hello group membership(s) of a user, use hello Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span></span> <span data-ttu-id="0f5fd-151">Questo cmdlet accetta come parametri hello ObjectId dell'utente hello per le appartenenze toocheck hello e un elenco di gruppi per le appartenenze hello che toocheck.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-151">This cmdlet takes as its parameters hello ObjectId of hello user for which toocheck hello group memberships, and a list of groups for which toocheck hello memberships.</span></span> <span data-ttu-id="0f5fd-152">elenco di Hello di gruppi deve essere fornita sotto forma di hello di una variabile complesso di tipo "Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck", quindi è innanzitutto necessario creare una variabile con tipo:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-152">hello list of groups must be provided in hello form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span></span>

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

<span data-ttu-id="0f5fd-153">È quindi necessario fornire valori per hello toocheck di ID dei gruppi nell'attributo hello "ID" dei gruppi di questa variabile di tipo complesso:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-153">Next, we provide values for hello groupIds toocheck in hello attribute “GroupIds” of this complex variable:</span></span>

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

<span data-ttu-id="0f5fd-154">A questo punto, se si desidera che le appartenenze al gruppo di un utente con 72cd4bbd-2594-40a2-935c-016f3cfeeeea ObjectID in più gruppi di hello in $g toocheck hello, da utilizzare:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-154">Now, if we want toocheck hello group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against hello groups in $g, we should use:</span></span>

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


<span data-ttu-id="0f5fd-155">il valore di Hello restituito è un elenco di gruppi di cui l'utente è membro.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-155">hello value returned is a list of groups of which this user is a member.</span></span> <span data-ttu-id="0f5fd-156">È inoltre possibile applicare questo toocheck metodo contatti, gruppi o entità servizio l'appartenenza a un determinato elenco di gruppi, utilizzando AzureADGroupIdsContactIsMemberOf selezionare, selezionare AzureADGroupIdsGroupIsMemberOf o Selezionare AzureADGroupIdsServicePrincipalIsMemberOf</span><span class="sxs-lookup"><span data-stu-id="0f5fd-156">You can also apply this method toocheck Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span></span>

## <a name="managing-owners-of-groups"></a><span data-ttu-id="0f5fd-157">Gestione dei proprietari dei gruppi</span><span class="sxs-lookup"><span data-stu-id="0f5fd-157">Managing owners of groups</span></span>
<span data-ttu-id="0f5fd-158">gruppo proprietari tooa tooadd, consente di utilizzare hello Aggiungi AzureADGroupOwner cmdlet:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-158">tooadd owners tooa group, use hello Add-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="0f5fd-159">il parametro - ObjectId Hello è hello ObjectID di hello gruppo toowhich desideriamo tooadd un proprietario e - RefObjectId hello è hello ObjectID dell'utente hello desideriamo tooadd come proprietario del gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-159">hello -ObjectId parameter is hello ObjectID of hello group toowhich we want tooadd an owner, and hello -RefObjectId is hello ObjectID of hello user we want tooadd as an owner of hello group.</span></span>

<span data-ttu-id="0f5fd-160">i proprietari di hello tooretrieve di un gruppo, usare il cmdlet Get-AzureADGroupOwner hello:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-160">tooretrieve hello owners of a group, use hello Get-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

<span data-ttu-id="0f5fd-161">cmdlet di Hello restituisce elenco hello di proprietari per il gruppo specificato hello:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-161">hello cmdlet returns hello list of owners for hello specified group:</span></span>

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

<span data-ttu-id="0f5fd-162">Se si desidera tooremove un proprietario di un gruppo, utilizzare cmdlet Remove-AzureADGroupOwner hello:</span><span class="sxs-lookup"><span data-stu-id="0f5fd-162">If you want tooremove an owner from a group, use hello Remove-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a><span data-ttu-id="0f5fd-163">Alias riservati</span><span class="sxs-lookup"><span data-stu-id="0f5fd-163">Reserved aliases</span></span> 
<span data-ttu-id="0f5fd-164">Quando viene creato un gruppo, determinati endpoint consentono hello utente finale toospecify un toobe mailNickname o alias utilizzato come parte dell'indirizzo di posta elettronica hello del gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-164">When a group is created, certain endpoints allow hello end user toospecify a mailNickname or alias toobe used as part of hello email address of hello group.</span></span> <span data-ttu-id="0f5fd-165">Solo è possibile creare gruppi con hello seguendo gli alias di posta elettronica con privilegi elevati da un amministratore globale di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f5fd-165">Groups with hello following highly privileged email aliases can only be created by an Azure AD global administrator.</span></span> 
  
* <span data-ttu-id="0f5fd-166">abuse</span><span class="sxs-lookup"><span data-stu-id="0f5fd-166">abuse</span></span> 
* <span data-ttu-id="0f5fd-167">admin</span><span class="sxs-lookup"><span data-stu-id="0f5fd-167">admin</span></span> 
* <span data-ttu-id="0f5fd-168">entità</span><span class="sxs-lookup"><span data-stu-id="0f5fd-168">administrator</span></span> 
* <span data-ttu-id="0f5fd-169">hostmaster</span><span class="sxs-lookup"><span data-stu-id="0f5fd-169">hostmaster</span></span> 
* <span data-ttu-id="0f5fd-170">majordomo</span><span class="sxs-lookup"><span data-stu-id="0f5fd-170">majordomo</span></span> 
* <span data-ttu-id="0f5fd-171">postmaster</span><span class="sxs-lookup"><span data-stu-id="0f5fd-171">postmaster</span></span> 
* <span data-ttu-id="0f5fd-172">root</span><span class="sxs-lookup"><span data-stu-id="0f5fd-172">root</span></span> 
* <span data-ttu-id="0f5fd-173">secure</span><span class="sxs-lookup"><span data-stu-id="0f5fd-173">secure</span></span> 
* <span data-ttu-id="0f5fd-174">security</span><span class="sxs-lookup"><span data-stu-id="0f5fd-174">security</span></span> 
* <span data-ttu-id="0f5fd-175">ssl-admin</span><span class="sxs-lookup"><span data-stu-id="0f5fd-175">ssl-admin</span></span> 
* <span data-ttu-id="0f5fd-176">webmaster</span><span class="sxs-lookup"><span data-stu-id="0f5fd-176">webmaster</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0f5fd-177">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0f5fd-177">Next steps</span></span>
<span data-ttu-id="0f5fd-178">Per altre informazioni su Azure Active Directory PowerShell, consultare la documentazione sui [cmdlet di Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="0f5fd-178">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

* [<span data-ttu-id="0f5fd-179">Gestione di accesso tooresources con gruppi di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f5fd-179">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="0f5fd-180">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f5fd-180">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
