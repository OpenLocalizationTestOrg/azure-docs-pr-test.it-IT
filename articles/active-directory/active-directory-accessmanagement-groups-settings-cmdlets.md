---
title: le impostazioni di gruppo aaaConfigure utilizzando i cmdlet di Azure Active Directory | Documenti Microsoft
description: Come gestire le impostazioni di hello per gruppi con i cmdlet di Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 9f2090e6-3af4-4f07-bbb2-1d18dae89b73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro;
ms.openlocfilehash: 46db49d9dec3eaa41c97ca74c57854189eddc16d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="0a913-103">Cmdlet di Azure Active Directory per la configurazione delle impostazioni di gruppo</span><span class="sxs-lookup"><span data-stu-id="0a913-103">Azure Active Directory cmdlets for configuring group settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a913-104">Solo i gruppi di 365 tooOffice si applica questo contenuto.</span><span class="sxs-lookup"><span data-stu-id="0a913-104">This content applies only tooOffice 365 groups.</span></span> <span data-ttu-id="0a913-105">Per ulteriori informazioni su come impostare gruppi di sicurezza toocreate utenti tooallow, `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` come descritto in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="0a913-105">For more information on how tooallow users toocreate Security groups, set `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span> 

<span data-ttu-id="0a913-106">Le impostazioni di Gruppi di Office 365 vengono configurare con un oggetto Settings e un oggetto SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="0a913-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="0a913-107">Inizialmente, non verranno visualizzati tutti gli oggetti impostazioni nella directory, perché la directory è configurata con le impostazioni predefinite di hello.</span><span class="sxs-lookup"><span data-stu-id="0a913-107">Initially, you don't see any Settings objects in your directory, because your directory is configured with hello default settings.</span></span> <span data-ttu-id="0a913-108">le impostazioni predefinite di hello toochange, è necessario creare un nuovo oggetto impostazioni utilizzando un modello di impostazioni.</span><span class="sxs-lookup"><span data-stu-id="0a913-108">toochange hello default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="0a913-109">I modelli di impostazioni sono definiti da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0a913-109">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="0a913-110">Sono disponibili diversi modelli di impostazioni.</span><span class="sxs-lookup"><span data-stu-id="0a913-110">There are several different settings templates.</span></span> <span data-ttu-id="0a913-111">impostazioni di gruppo tooconfigure Office 365 per la directory, utilizzare il modello di hello denominato "Group.Unified".</span><span class="sxs-lookup"><span data-stu-id="0a913-111">tooconfigure Office 365 group settings for your directory, you use hello template named "Group.Unified".</span></span> <span data-ttu-id="0a913-112">impostazioni del gruppo tooconfigure Office 365 in un singolo gruppo, utilizzare il modello di hello denominato "Group.Unified.Guest".</span><span class="sxs-lookup"><span data-stu-id="0a913-112">tooconfigure Office 365 group settings on a single group, use hello template named "Group.Unified.Guest".</span></span> <span data-ttu-id="0a913-113">Questo modello è gruppo tooan Office 365 di accesso guest toomanage utilizzato.</span><span class="sxs-lookup"><span data-stu-id="0a913-113">This template is used toomanage guest access tooan Office 365 group.</span></span> 

<span data-ttu-id="0a913-114">i cmdlet di Hello sono parte del modulo di Azure Active Directory PowerShell V2 hello.</span><span class="sxs-lookup"><span data-stu-id="0a913-114">hello cmdlets are part of hello Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="0a913-115">Per istruzioni toodownload e installazione hello modulo nel computer in uso, vedere articolo hello [Azure Active Directory PowerShell versione 2](https://docs.microsoft.com/powershell/azuread/).</span><span class="sxs-lookup"><span data-stu-id="0a913-115">For instructions how toodownload and install hello module on your computer, see hello article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="0a913-116">È possibile installare una versione di hello versione 2 del modulo hello da [raccolta PowerShell hello](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="0a913-116">You can install hello version 2 release of hello module from [hello PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="retrieve-a-specific-settings-value"></a><span data-ttu-id="0a913-117">Recuperare un valore di impostazione specifico</span><span class="sxs-lookup"><span data-stu-id="0a913-117">Retrieve a specific settings value</span></span>
<span data-ttu-id="0a913-118">Se si conosce il nome di hello di hello impostazione desidera tooretrieve, è possibile usare hello seguito cmdlet tooretrieve hello corrente il valore delle impostazioni.</span><span class="sxs-lookup"><span data-stu-id="0a913-118">If you know hello name of hello setting you want tooretrieve, you can use hello below cmdlet tooretrieve hello current settings value.</span></span> <span data-ttu-id="0a913-119">In questo esempio, vengono recuperate valore hello per un'impostazione denominata "UsageGuidelinesUrl".</span><span class="sxs-lookup"><span data-stu-id="0a913-119">In this example, we're retrieving hello value for a setting named "UsageGuidelinesUrl."</span></span> <span data-ttu-id="0a913-120">Più avanti in questo capitolo sono disponibili altre informazioni sulle impostazioni di directory e i rispettivi nomi.</span><span class="sxs-lookup"><span data-stu-id="0a913-120">You can read more about directory settings and their names further down in this article.</span></span>

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a><span data-ttu-id="0a913-121">Creare le impostazioni a livello di directory hello</span><span class="sxs-lookup"><span data-stu-id="0a913-121">Create settings at hello directory level</span></span>
<span data-ttu-id="0a913-122">Questi passaggi creano le impostazioni a livello di directory, che si applicano a gruppi di Office 365 tooall (gruppi unificato) nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="0a913-122">These steps create settings at directory level, which apply tooall Office 365 groups (Unified groups) in hello directory.</span></span>

1. <span data-ttu-id="0a913-123">In hello DirectorySettings cmdlet, è necessario specificare ID hello di hello SettingsTemplate desiderato toouse.</span><span class="sxs-lookup"><span data-stu-id="0a913-123">In hello DirectorySettings cmdlets, you must specify hello ID of hello SettingsTemplate you want toouse.</span></span> <span data-ttu-id="0a913-124">Se non si conosce questo ID, questo cmdlet restituisce l'elenco di hello di tutti i modelli di impostazioni:</span><span class="sxs-lookup"><span data-stu-id="0a913-124">If you do not know this ID, this cmdlet returns hello list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="0a913-125">Questa chiamata del cmdlet restituirà tutti i modelli disponibili:</span><span class="sxs-lookup"><span data-stu-id="0a913-125">This cmdlet call returns all templates that are available:</span></span>
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Unified Group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define hello different settings that can be used for hello associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. <span data-ttu-id="0a913-126">tooadd un URL delle linee guida sull'utilizzo, è necessario innanzitutto tooget hello SettingsTemplate che definisce il valore hello di URL delle linee guida sull'utilizzo; vale a dire hello Group.Unified modello:</span><span class="sxs-lookup"><span data-stu-id="0a913-126">tooadd a usage guideline URL, first you need tooget hello SettingsTemplate object that defines hello usage guideline URL value; that is, hello Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="0a913-127">Successivamente, creare un nuovo oggetto impostazioni sulla base del modello:</span><span class="sxs-lookup"><span data-stu-id="0a913-127">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="0a913-128">Aggiornare quindi il valore hello utilizzo delle linee guida:</span><span class="sxs-lookup"><span data-stu-id="0a913-128">Then update hello usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. <span data-ttu-id="0a913-129">Infine, applicare le impostazioni di hello:</span><span class="sxs-lookup"><span data-stu-id="0a913-129">Finally, apply hello settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

<span data-ttu-id="0a913-130">Al completamento, hello cmdlet restituisce hello ID dell'oggetto Impostazioni nuovo hello:</span><span class="sxs-lookup"><span data-stu-id="0a913-130">Upon successful completion, hello cmdlet returns hello ID of hello new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
<span data-ttu-id="0a913-131">Ecco le impostazioni di hello definite in hello Group.Unified SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="0a913-131">Here are hello settings defined in hello Group.Unified SettingsTemplate.</span></span>

| <span data-ttu-id="0a913-132">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="0a913-132">**Setting**</span></span> | <span data-ttu-id="0a913-133">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="0a913-133">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="0a913-134">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="0a913-134">EnableGroupCreation</span></span><li><span data-ttu-id="0a913-135">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="0a913-135">Type: Boolean</span></span><li><span data-ttu-id="0a913-136">Valore predefinito: True</span><span class="sxs-lookup"><span data-stu-id="0a913-136">Default: True</span></span> |<span data-ttu-id="0a913-137">flag di Hello che indica se la creazione del gruppo unificato è consentita nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="0a913-137">hello flag indicating whether Unified Group creation is allowed in hello directory.</span></span> |
|  <ul><li><span data-ttu-id="0a913-138">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="0a913-138">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="0a913-139">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="0a913-139">Type: String</span></span><li><span data-ttu-id="0a913-140">Predefinito: ""</span><span class="sxs-lookup"><span data-stu-id="0a913-140">Default: “”</span></span> |<span data-ttu-id="0a913-141">GUID del gruppo di sicurezza hello per cui hello membri sono consentiti gruppi unificati toocreate anche quando EnableGroupCreation = = false.</span><span class="sxs-lookup"><span data-stu-id="0a913-141">GUID of hello security group for which hello members are allowed toocreate Unified Groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="0a913-142">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="0a913-142">UsageGuidelinesUrl</span></span><li><span data-ttu-id="0a913-143">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="0a913-143">Type: String</span></span><li><span data-ttu-id="0a913-144">Predefinito: ""</span><span class="sxs-lookup"><span data-stu-id="0a913-144">Default: “”</span></span> |<span data-ttu-id="0a913-145">Un collegamento toohello linee guida di utilizzo di gruppo.</span><span class="sxs-lookup"><span data-stu-id="0a913-145">A link toohello Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="0a913-146">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="0a913-146">ClassificationDescriptions</span></span><li><span data-ttu-id="0a913-147">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="0a913-147">Type: String</span></span><li><span data-ttu-id="0a913-148">Predefinito: ""</span><span class="sxs-lookup"><span data-stu-id="0a913-148">Default: “”</span></span> | <span data-ttu-id="0a913-149">Elenco delimitato da virgole di descrizioni di classificazione.</span><span class="sxs-lookup"><span data-stu-id="0a913-149">A comma-delimited list of classification descriptions.</span></span> |
|  <ul><li><span data-ttu-id="0a913-150">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="0a913-150">DefaultClassification</span></span><li><span data-ttu-id="0a913-151">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="0a913-151">Type: String</span></span><li><span data-ttu-id="0a913-152">Predefinito: ""</span><span class="sxs-lookup"><span data-stu-id="0a913-152">Default: “”</span></span> | <span data-ttu-id="0a913-153">classificazione Hello che viene utilizzato come classificazione di hello predefinita per un gruppo se non è stato specificato alcun toobe.</span><span class="sxs-lookup"><span data-stu-id="0a913-153">hello classification that is toobe used as hello default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="0a913-154">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="0a913-154">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="0a913-155">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="0a913-155">Type: String</span></span><li><span data-ttu-id="0a913-156">Predefinito: ""</span><span class="sxs-lookup"><span data-stu-id="0a913-156">Default: “”</span></span> |<span data-ttu-id="0a913-157">Non ancora implementato</span><span class="sxs-lookup"><span data-stu-id="0a913-157">Not implemented yet</span></span>
|  <ul><li><span data-ttu-id="0a913-158">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="0a913-158">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="0a913-159">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="0a913-159">Type: Boolean</span></span><li><span data-ttu-id="0a913-160">Valore predefinito: False</span><span class="sxs-lookup"><span data-stu-id="0a913-160">Default: False</span></span> | <span data-ttu-id="0a913-161">Valore booleano che indica se un utente guest può essere o meno un proprietario di gruppi.</span><span class="sxs-lookup"><span data-stu-id="0a913-161">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="0a913-162">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="0a913-162">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="0a913-163">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="0a913-163">Type: Boolean</span></span><li><span data-ttu-id="0a913-164">Valore predefinito: True</span><span class="sxs-lookup"><span data-stu-id="0a913-164">Default: True</span></span> | <span data-ttu-id="0a913-165">Valore booleano che indica se un utente guest può avere contenuto gruppi tooUnified di accesso.</span><span class="sxs-lookup"><span data-stu-id="0a913-165">Boolean indicating whether or not a guest user can have access tooUnified groups' content.</span></span> |
|  <ul><li><span data-ttu-id="0a913-166">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="0a913-166">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="0a913-167">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="0a913-167">Type: String</span></span><li><span data-ttu-id="0a913-168">Predefinito: ""</span><span class="sxs-lookup"><span data-stu-id="0a913-168">Default: “”</span></span> | <span data-ttu-id="0a913-169">url di Hello di indicazioni per l'utilizzo un collegamento toohello guest.</span><span class="sxs-lookup"><span data-stu-id="0a913-169">hello url of a link toohello guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="0a913-170">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="0a913-170">AllowToAddGuests</span></span><li><span data-ttu-id="0a913-171">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="0a913-171">Type: Boolean</span></span><li><span data-ttu-id="0a913-172">Valore predefinito: True</span><span class="sxs-lookup"><span data-stu-id="0a913-172">Default: True</span></span> | <span data-ttu-id="0a913-173">Un valore booleano che indica se è consentito tooadd guest toothis directory.</span><span class="sxs-lookup"><span data-stu-id="0a913-173">A boolean indicating whether or not is allowed tooadd guests toothis directory.</span></span>|
|  <ul><li><span data-ttu-id="0a913-174">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="0a913-174">ClassificationList</span></span><li><span data-ttu-id="0a913-175">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="0a913-175">Type: String</span></span><li><span data-ttu-id="0a913-176">Predefinito: ""</span><span class="sxs-lookup"><span data-stu-id="0a913-176">Default: “”</span></span> |<span data-ttu-id="0a913-177">Un elenco delimitato da virgole dei valori di classificazione valido che può essere applicato tooUnified gruppi.</span><span class="sxs-lookup"><span data-stu-id="0a913-177">A comma-delimited list of valid classification values that can be applied tooUnified Groups.</span></span> |
|  <ul><li><span data-ttu-id="0a913-178">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="0a913-178">EnableGroupCreation</span></span><li><span data-ttu-id="0a913-179">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="0a913-179">Type: Boolean</span></span><li><span data-ttu-id="0a913-180">Valore predefinito: True</span><span class="sxs-lookup"><span data-stu-id="0a913-180">Default: True</span></span> | <span data-ttu-id="0a913-181">Valore booleano che indica se gli utenti non amministratori possono creare nuovi gruppi unificati.</span><span class="sxs-lookup"><span data-stu-id="0a913-181">A boolean indicating whether or not non-admin users can create new Unified groups.</span></span> |


## <a name="read-settings-at-hello-directory-level"></a><span data-ttu-id="0a913-182">Leggere le impostazioni a livello di directory hello</span><span class="sxs-lookup"><span data-stu-id="0a913-182">Read settings at hello directory level</span></span>
<span data-ttu-id="0a913-183">Questi passaggi leggono le impostazioni a livello di directory, che si applicano tooall gruppi di Office nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="0a913-183">These steps read settings at directory level, which apply tooall Office groups in hello directory.</span></span>

1. <span data-ttu-id="0a913-184">Leggere tutte le impostazioni della directory esistenti:</span><span class="sxs-lookup"><span data-stu-id="0a913-184">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="0a913-185">Questo cmdlet restituisce un elenco di tutte le impostazioni della directory:</span><span class="sxs-lookup"><span data-stu-id="0a913-185">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="0a913-186">Leggere tutte le impostazioni di un determinato gruppo:</span><span class="sxs-lookup"><span data-stu-id="0a913-186">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="0a913-187">Leggere tutti i valori delle impostazioni di directory di un oggetto Settings della directory specifico, usando il GUID delle impostazioni:</span><span class="sxs-lookup"><span data-stu-id="0a913-187">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="0a913-188">Questo cmdlet restituisce i nomi di hello e i valori in questo oggetto impostazioni per questo gruppo specifico:</span><span class="sxs-lookup"><span data-stu-id="0a913-188">This cmdlet returns hello names and values in this settings object for this specific group:</span></span>
  ```
  Name                          Value
  ----                          -----
  ClassificationDescriptions
  DefaultClassification
  PrefixSuffixNamingRequirement
  AllowGuestsToBeGroupOwner     False 
  AllowGuestsToAccessGroups     True
  GuestUsageGuidelinesUrl
  GroupCreationAllowedGroupId
  AllowToAddGuests              True
  UsageGuidelinesUrl            <https://guideline.com>
  ClassificationList
  EnableGroupCreation           True
  ```

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="0a913-189">Aggiornare le impostazioni per un gruppo specifico</span><span class="sxs-lookup"><span data-stu-id="0a913-189">Update settings for a specific group</span></span>

1. <span data-ttu-id="0a913-190">Cercare hello impostazioni modello denominato "Groups.Unified.Guest"</span><span class="sxs-lookup"><span data-stu-id="0a913-190">Search for hello settings template named "Groups.Unified.Guest"</span></span>
  ```
  Get-AzureADDirectorySettingTemplate
  
  Id                                   DisplayName            Description
  --                                   -----------            -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified          ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest    Settings for a specific Unified Group
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application            ...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule Settings ...
  ```
2. <span data-ttu-id="0a913-191">Recuperare hello modello oggetto per il modello Groups.Unified.Guest hello:</span><span class="sxs-lookup"><span data-stu-id="0a913-191">Retrieve hello template object for hello Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="0a913-192">Creare un nuovo oggetto impostazioni dal modello hello:</span><span class="sxs-lookup"><span data-stu-id="0a913-192">Create a new settings object from hello template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="0a913-193">Impostare l'impostazione del valore toohello necessario hello:</span><span class="sxs-lookup"><span data-stu-id="0a913-193">Set hello setting toohello required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="0a913-194">Creare hello nuova impostazione per il gruppo richiesto hello nella directory hello:</span><span class="sxs-lookup"><span data-stu-id="0a913-194">Create hello new setting for hello required group in hello directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a><span data-ttu-id="0a913-195">Aggiornare le impostazioni a livello di directory hello</span><span class="sxs-lookup"><span data-stu-id="0a913-195">Update settings at hello directory level</span></span>

<span data-ttu-id="0a913-196">Questi passaggi aggiornino le impostazioni a livello di directory, che si applicano tooall unificato gruppi nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="0a913-196">These steps update settings at directory level, which apply tooall Unified groups in hello directory.</span></span> <span data-ttu-id="0a913-197">Questi esempi presuppongono che nella directory esista già un oggetto Settings.</span><span class="sxs-lookup"><span data-stu-id="0a913-197">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="0a913-198">Trovare l'oggetto impostazioni esistente hello:</span><span class="sxs-lookup"><span data-stu-id="0a913-198">Find hello existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="0a913-199">Aggiornare il valore di hello:</span><span class="sxs-lookup"><span data-stu-id="0a913-199">Update hello value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="0a913-200">Aggiornamento dell'impostazione hello:</span><span class="sxs-lookup"><span data-stu-id="0a913-200">Update hello setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a><span data-ttu-id="0a913-201">Rimuovere le impostazioni a livello di directory hello</span><span class="sxs-lookup"><span data-stu-id="0a913-201">Remove settings at hello directory level</span></span>
<span data-ttu-id="0a913-202">Questo passaggio rimuove le impostazioni a livello di directory, che si applicano tooall gruppi di Office nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="0a913-202">This step removes settings at directory level, which apply tooall Office groups in hello directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="0a913-203">Riferimento alla sintassi cmdlet</span><span class="sxs-lookup"><span data-stu-id="0a913-203">Cmdlet syntax reference</span></span>
<span data-ttu-id="0a913-204">Per altre informazioni su Azure Active Directory PowerShell, consultare la documentazione sui [cmdlet di Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="0a913-204">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="0a913-205">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0a913-205">Additional reading</span></span>

* [<span data-ttu-id="0a913-206">Gestione di accesso tooresources con gruppi di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a913-206">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="0a913-207">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a913-207">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
