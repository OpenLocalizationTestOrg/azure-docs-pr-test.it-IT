---
title: Configurare le impostazioni di gruppo usando i cmdlet di Azure Active Directory | Microsoft Docs
description: Come gestire le impostazioni dei gruppi con i cmdlet di Azure Active Directory
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
ms.openlocfilehash: 0d89f12955b90c7e1a8301b7c3a1a92e7f62d085
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="90cb2-103">Cmdlet di Azure Active Directory per la configurazione delle impostazioni di gruppo</span><span class="sxs-lookup"><span data-stu-id="90cb2-103">Azure Active Directory cmdlets for configuring group settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="90cb2-104">Questo contenuto si applica solo ai gruppi di Office 365.</span><span class="sxs-lookup"><span data-stu-id="90cb2-104">This content applies only to Office 365 groups.</span></span> <span data-ttu-id="90cb2-105">Per altre informazioni su come consentire agli utenti di creare gruppi di sicurezza, configurare il valore `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` come illustrato in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="90cb2-105">For more information on how to allow users to create Security groups, set `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span> 

<span data-ttu-id="90cb2-106">Le impostazioni di Gruppi di Office 365 vengono configurare con un oggetto Settings e un oggetto SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="90cb2-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="90cb2-107">Non vengono inizialmente visualizzati oggetti Settings nella directory, perché la directory è configurata con le impostazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="90cb2-107">Initially, you don't see any Settings objects in your directory, because your directory is configured with the default settings.</span></span> <span data-ttu-id="90cb2-108">Per modificarle, è necessario creare un nuovo oggetto Settings usando un modello di impostazioni.</span><span class="sxs-lookup"><span data-stu-id="90cb2-108">To change the default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="90cb2-109">I modelli di impostazioni sono definiti da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="90cb2-109">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="90cb2-110">Sono disponibili diversi modelli di impostazioni.</span><span class="sxs-lookup"><span data-stu-id="90cb2-110">There are several different settings templates.</span></span> <span data-ttu-id="90cb2-111">Per configurare le impostazioni di gruppo di Office 365 per la directory, usare il modello denominato "Group.Unified".</span><span class="sxs-lookup"><span data-stu-id="90cb2-111">To configure Office 365 group settings for your directory, you use the template named "Group.Unified".</span></span> <span data-ttu-id="90cb2-112">Per configurare le impostazioni di gruppo di Office 365 per un singolo gruppo, usare il modello denominato "Group.Unified.Guest".</span><span class="sxs-lookup"><span data-stu-id="90cb2-112">To configure Office 365 group settings on a single group, use the template named "Group.Unified.Guest".</span></span> <span data-ttu-id="90cb2-113">Questo modello viene usato per gestire l'accesso guest a un gruppo di Office 365.</span><span class="sxs-lookup"><span data-stu-id="90cb2-113">This template is used to manage guest access to an Office 365 group.</span></span> 

<span data-ttu-id="90cb2-114">I cmdlet fanno parte del modulo Azure Active Directory PowerShell V2.</span><span class="sxs-lookup"><span data-stu-id="90cb2-114">The cmdlets are part of the Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="90cb2-115">Per istruzioni sul download e sull'installazione del modulo nel computer, vedere l'articolo [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/) (Azure Active Directory PowerShell versione 2).</span><span class="sxs-lookup"><span data-stu-id="90cb2-115">For instructions how to download and install the module on your computer, see the article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="90cb2-116">È possibile installare la versione 2 del modulo da [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="90cb2-116">You can install the version 2 release of the module from [the PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="retrieve-a-specific-settings-value"></a><span data-ttu-id="90cb2-117">Recuperare un valore di impostazione specifico</span><span class="sxs-lookup"><span data-stu-id="90cb2-117">Retrieve a specific settings value</span></span>
<span data-ttu-id="90cb2-118">Se si conosce il nome dell'impostazione da recuperare, è possibile usare il cmdlet seguente per recuperare il valore corrente dell'impostazione.</span><span class="sxs-lookup"><span data-stu-id="90cb2-118">If you know the name of the setting you want to retrieve, you can use the below cmdlet to retrieve the current settings value.</span></span> <span data-ttu-id="90cb2-119">In questo esempio viene recuperato il valore per un'impostazione denominata "UsageGuidelinesUrl".</span><span class="sxs-lookup"><span data-stu-id="90cb2-119">In this example, we're retrieving the value for a setting named "UsageGuidelinesUrl."</span></span> <span data-ttu-id="90cb2-120">Più avanti in questo capitolo sono disponibili altre informazioni sulle impostazioni di directory e i rispettivi nomi.</span><span class="sxs-lookup"><span data-stu-id="90cb2-120">You can read more about directory settings and their names further down in this article.</span></span>

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-the-directory-level"></a><span data-ttu-id="90cb2-121">Creare le impostazioni a livello di directory</span><span class="sxs-lookup"><span data-stu-id="90cb2-121">Create settings at the directory level</span></span>
<span data-ttu-id="90cb2-122">I passaggi seguenti consentono di creare le impostazioni a livello di directory, applicabili a tutti i gruppi di Office 365 (gruppi unificati) presenti nella directory stessa.</span><span class="sxs-lookup"><span data-stu-id="90cb2-122">These steps create settings at directory level, which apply to all Office 365 groups (Unified groups) in the directory.</span></span>

1. <span data-ttu-id="90cb2-123">Nei cmdlet DirectorySettings è necessario specificare l'ID del SettingsTemplate che si vuole usare.</span><span class="sxs-lookup"><span data-stu-id="90cb2-123">In the DirectorySettings cmdlets, you must specify the ID of the SettingsTemplate you want to use.</span></span> <span data-ttu-id="90cb2-124">Se non si conosce l'ID, questo cmdlet restituisce l'elenco di tutti i modelli di impostazioni:</span><span class="sxs-lookup"><span data-stu-id="90cb2-124">If you do not know this ID, this cmdlet returns the list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="90cb2-125">Questa chiamata del cmdlet restituirà tutti i modelli disponibili:</span><span class="sxs-lookup"><span data-stu-id="90cb2-125">This cmdlet call returns all templates that are available:</span></span>
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Unified Group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define the different settings that can be used for the associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. <span data-ttu-id="90cb2-126">Per aggiungere un URL alle linee guida sull'utilizzo, è necessario innanzitutto ottenere l'oggetto SettingsTemplate che definisce il valore di URL delle linee guida sull'utilizzo, vale a dire il modello Group.Unified:</span><span class="sxs-lookup"><span data-stu-id="90cb2-126">To add a usage guideline URL, first you need to get the SettingsTemplate object that defines the usage guideline URL value; that is, the Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="90cb2-127">Successivamente, creare un nuovo oggetto impostazioni sulla base del modello:</span><span class="sxs-lookup"><span data-stu-id="90cb2-127">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="90cb2-128">Aggiornare quindi il valore delle linee guida sull'utilizzo:</span><span class="sxs-lookup"><span data-stu-id="90cb2-128">Then update the usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. <span data-ttu-id="90cb2-129">Infine, applicare le impostazioni:</span><span class="sxs-lookup"><span data-stu-id="90cb2-129">Finally, apply the settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

<span data-ttu-id="90cb2-130">Al termine, il cmdlet restituisce l'ID del nuovo oggetto Settings:</span><span class="sxs-lookup"><span data-stu-id="90cb2-130">Upon successful completion, the cmdlet returns the ID of the new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
<span data-ttu-id="90cb2-131">Di seguito sono riportate le impostazioni definite in SettingsTemplate di Group.Unified.</span><span class="sxs-lookup"><span data-stu-id="90cb2-131">Here are the settings defined in the Group.Unified SettingsTemplate.</span></span>

| <span data-ttu-id="90cb2-132">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="90cb2-132">**Setting**</span></span> | <span data-ttu-id="90cb2-133">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="90cb2-133">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="90cb2-134">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="90cb2-134">EnableGroupCreation</span></span><li><span data-ttu-id="90cb2-135">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="90cb2-135">Type: Boolean</span></span><li><span data-ttu-id="90cb2-136">Valore predefinito: True</span><span class="sxs-lookup"><span data-stu-id="90cb2-136">Default: True</span></span> |<span data-ttu-id="90cb2-137">La bandierina che indica se sia consentito creare il gruppo unificato nella directory.</span><span class="sxs-lookup"><span data-stu-id="90cb2-137">The flag indicating whether Unified Group creation is allowed in the directory.</span></span> |
|  <ul><li><span data-ttu-id="90cb2-138">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="90cb2-138">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="90cb2-139">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="90cb2-139">Type: String</span></span><li><span data-ttu-id="90cb2-140">Predefinito: ""</span><span class="sxs-lookup"><span data-stu-id="90cb2-140">Default: “”</span></span> |<span data-ttu-id="90cb2-141">GUID del gruppo di sicurezza i cui membri sono autorizzati a creare gruppi unificati anche quando EnableGroupCreation == false.</span><span class="sxs-lookup"><span data-stu-id="90cb2-141">GUID of the security group for which the members are allowed to create Unified Groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="90cb2-142">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="90cb2-142">UsageGuidelinesUrl</span></span><li><span data-ttu-id="90cb2-143">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="90cb2-143">Type: String</span></span><li><span data-ttu-id="90cb2-144">Predefinito: ""</span><span class="sxs-lookup"><span data-stu-id="90cb2-144">Default: “”</span></span> |<span data-ttu-id="90cb2-145">Collegamento alle linee guida sull'utilizzo dei gruppi.</span><span class="sxs-lookup"><span data-stu-id="90cb2-145">A link to the Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="90cb2-146">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="90cb2-146">ClassificationDescriptions</span></span><li><span data-ttu-id="90cb2-147">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="90cb2-147">Type: String</span></span><li><span data-ttu-id="90cb2-148">Predefinito: ""</span><span class="sxs-lookup"><span data-stu-id="90cb2-148">Default: “”</span></span> | <span data-ttu-id="90cb2-149">Elenco delimitato da virgole di descrizioni di classificazione.</span><span class="sxs-lookup"><span data-stu-id="90cb2-149">A comma-delimited list of classification descriptions.</span></span> |
|  <ul><li><span data-ttu-id="90cb2-150">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="90cb2-150">DefaultClassification</span></span><li><span data-ttu-id="90cb2-151">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="90cb2-151">Type: String</span></span><li><span data-ttu-id="90cb2-152">Predefinito: ""</span><span class="sxs-lookup"><span data-stu-id="90cb2-152">Default: “”</span></span> | <span data-ttu-id="90cb2-153">Classificazione da usare come classificazione predefinita per un gruppo, se non specificata.</span><span class="sxs-lookup"><span data-stu-id="90cb2-153">The classification that is to be used as the default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="90cb2-154">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="90cb2-154">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="90cb2-155">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="90cb2-155">Type: String</span></span><li><span data-ttu-id="90cb2-156">Predefinito: ""</span><span class="sxs-lookup"><span data-stu-id="90cb2-156">Default: “”</span></span> |<span data-ttu-id="90cb2-157">Non ancora implementato</span><span class="sxs-lookup"><span data-stu-id="90cb2-157">Not implemented yet</span></span>
|  <ul><li><span data-ttu-id="90cb2-158">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="90cb2-158">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="90cb2-159">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="90cb2-159">Type: Boolean</span></span><li><span data-ttu-id="90cb2-160">Valore predefinito: False</span><span class="sxs-lookup"><span data-stu-id="90cb2-160">Default: False</span></span> | <span data-ttu-id="90cb2-161">Valore booleano che indica se un utente guest può essere o meno un proprietario di gruppi.</span><span class="sxs-lookup"><span data-stu-id="90cb2-161">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="90cb2-162">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="90cb2-162">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="90cb2-163">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="90cb2-163">Type: Boolean</span></span><li><span data-ttu-id="90cb2-164">Valore predefinito: True</span><span class="sxs-lookup"><span data-stu-id="90cb2-164">Default: True</span></span> | <span data-ttu-id="90cb2-165">Valore booleano che indica se un utente guest ha o meno accesso al contenuto dei gruppi unificati.</span><span class="sxs-lookup"><span data-stu-id="90cb2-165">Boolean indicating whether or not a guest user can have access to Unified groups' content.</span></span> |
|  <ul><li><span data-ttu-id="90cb2-166">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="90cb2-166">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="90cb2-167">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="90cb2-167">Type: String</span></span><li><span data-ttu-id="90cb2-168">Predefinito: ""</span><span class="sxs-lookup"><span data-stu-id="90cb2-168">Default: “”</span></span> | <span data-ttu-id="90cb2-169">URL di un collegamento alle linee guida per l'utilizzo dei gruppi.</span><span class="sxs-lookup"><span data-stu-id="90cb2-169">The url of a link to the guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="90cb2-170">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="90cb2-170">AllowToAddGuests</span></span><li><span data-ttu-id="90cb2-171">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="90cb2-171">Type: Boolean</span></span><li><span data-ttu-id="90cb2-172">Valore predefinito: True</span><span class="sxs-lookup"><span data-stu-id="90cb2-172">Default: True</span></span> | <span data-ttu-id="90cb2-173">Valore booleano che indica se è consentito o meno aggiungere utenti guest a questa directory.</span><span class="sxs-lookup"><span data-stu-id="90cb2-173">A boolean indicating whether or not is allowed to add guests to this directory.</span></span>|
|  <ul><li><span data-ttu-id="90cb2-174">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="90cb2-174">ClassificationList</span></span><li><span data-ttu-id="90cb2-175">Tipo: String</span><span class="sxs-lookup"><span data-stu-id="90cb2-175">Type: String</span></span><li><span data-ttu-id="90cb2-176">Predefinito: ""</span><span class="sxs-lookup"><span data-stu-id="90cb2-176">Default: “”</span></span> |<span data-ttu-id="90cb2-177">Un elenco delimitato da virgole dei valori di classificazione validi che è possibile applicare ai gruppi unificati.</span><span class="sxs-lookup"><span data-stu-id="90cb2-177">A comma-delimited list of valid classification values that can be applied to Unified Groups.</span></span> |
|  <ul><li><span data-ttu-id="90cb2-178">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="90cb2-178">EnableGroupCreation</span></span><li><span data-ttu-id="90cb2-179">Tipo: Boolean</span><span class="sxs-lookup"><span data-stu-id="90cb2-179">Type: Boolean</span></span><li><span data-ttu-id="90cb2-180">Valore predefinito: True</span><span class="sxs-lookup"><span data-stu-id="90cb2-180">Default: True</span></span> | <span data-ttu-id="90cb2-181">Valore booleano che indica se gli utenti non amministratori possono creare nuovi gruppi unificati.</span><span class="sxs-lookup"><span data-stu-id="90cb2-181">A boolean indicating whether or not non-admin users can create new Unified groups.</span></span> |


## <a name="read-settings-at-the-directory-level"></a><span data-ttu-id="90cb2-182">Leggere le impostazioni a livello di directory</span><span class="sxs-lookup"><span data-stu-id="90cb2-182">Read settings at the directory level</span></span>
<span data-ttu-id="90cb2-183">Quelli che seguono sono i passaggi necessari per leggere le impostazioni a livello di directory, che si applicano a tutti i gruppi di Office presenti nella directory.</span><span class="sxs-lookup"><span data-stu-id="90cb2-183">These steps read settings at directory level, which apply to all Office groups in the directory.</span></span>

1. <span data-ttu-id="90cb2-184">Leggere tutte le impostazioni della directory esistenti:</span><span class="sxs-lookup"><span data-stu-id="90cb2-184">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="90cb2-185">Questo cmdlet restituisce un elenco di tutte le impostazioni della directory:</span><span class="sxs-lookup"><span data-stu-id="90cb2-185">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="90cb2-186">Leggere tutte le impostazioni di un determinato gruppo:</span><span class="sxs-lookup"><span data-stu-id="90cb2-186">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="90cb2-187">Leggere tutti i valori delle impostazioni di directory di un oggetto Settings della directory specifico, usando il GUID delle impostazioni:</span><span class="sxs-lookup"><span data-stu-id="90cb2-187">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="90cb2-188">Questo cmdlet restituisce i nomi e valori in questo oggetto Settings per il gruppo specifico:</span><span class="sxs-lookup"><span data-stu-id="90cb2-188">This cmdlet returns the names and values in this settings object for this specific group:</span></span>
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

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="90cb2-189">Aggiornare le impostazioni per un gruppo specifico</span><span class="sxs-lookup"><span data-stu-id="90cb2-189">Update settings for a specific group</span></span>

1. <span data-ttu-id="90cb2-190">Cercare il modello di impostazioni denominato "Groups.Unified.Guest"</span><span class="sxs-lookup"><span data-stu-id="90cb2-190">Search for the settings template named "Groups.Unified.Guest"</span></span>
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
2. <span data-ttu-id="90cb2-191">Recuperare l'oggetto modello per il modello Groups.Unified.Guest:</span><span class="sxs-lookup"><span data-stu-id="90cb2-191">Retrieve the template object for the Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="90cb2-192">Creare un nuovo oggetto Settings dal modello:</span><span class="sxs-lookup"><span data-stu-id="90cb2-192">Create a new settings object from the template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="90cb2-193">Impostare il valore richiesto:</span><span class="sxs-lookup"><span data-stu-id="90cb2-193">Set the setting to the required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="90cb2-194">Creare la nuova impostazione per il gruppo richiesto nella directory:</span><span class="sxs-lookup"><span data-stu-id="90cb2-194">Create the new setting for the required group in the directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-the-directory-level"></a><span data-ttu-id="90cb2-195">Aggiornare le impostazioni a livello di directory</span><span class="sxs-lookup"><span data-stu-id="90cb2-195">Update settings at the directory level</span></span>

<span data-ttu-id="90cb2-196">Questi passaggi consentono di aggiornare le impostazioni a livello di directory, applicabili a tutti i gruppi unificati nella directory.</span><span class="sxs-lookup"><span data-stu-id="90cb2-196">These steps update settings at directory level, which apply to all Unified groups in the directory.</span></span> <span data-ttu-id="90cb2-197">Questi esempi presuppongono che nella directory esista già un oggetto Settings.</span><span class="sxs-lookup"><span data-stu-id="90cb2-197">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="90cb2-198">Trovare l'oggetto Settings esistente:</span><span class="sxs-lookup"><span data-stu-id="90cb2-198">Find the existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="90cb2-199">Aggiornare il valore:</span><span class="sxs-lookup"><span data-stu-id="90cb2-199">Update the value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="90cb2-200">Aggiornare l'impostazione:</span><span class="sxs-lookup"><span data-stu-id="90cb2-200">Update the setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-the-directory-level"></a><span data-ttu-id="90cb2-201">Rimuovere le impostazioni a livello di directory</span><span class="sxs-lookup"><span data-stu-id="90cb2-201">Remove settings at the directory level</span></span>
<span data-ttu-id="90cb2-202">Questo passaggio consente di rimuovere le impostazioni a livello di directory, che si applicano a tutti i gruppi di Office presenti nella directory.</span><span class="sxs-lookup"><span data-stu-id="90cb2-202">This step removes settings at directory level, which apply to all Office groups in the directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="90cb2-203">Riferimento alla sintassi cmdlet</span><span class="sxs-lookup"><span data-stu-id="90cb2-203">Cmdlet syntax reference</span></span>
<span data-ttu-id="90cb2-204">Per altre informazioni su Azure Active Directory PowerShell, consultare la documentazione sui [cmdlet di Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="90cb2-204">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="90cb2-205">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="90cb2-205">Additional reading</span></span>

* [<span data-ttu-id="90cb2-206">Gestione dell'accesso alle risorse tramite i gruppi di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="90cb2-206">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="90cb2-207">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="90cb2-207">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
