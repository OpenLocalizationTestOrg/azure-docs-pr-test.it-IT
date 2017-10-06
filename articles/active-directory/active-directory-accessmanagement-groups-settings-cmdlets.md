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
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a>Cmdlet di Azure Active Directory per la configurazione delle impostazioni di gruppo

> [!IMPORTANT]
> Solo i gruppi di 365 tooOffice si applica questo contenuto. Per ulteriori informazioni su come impostare gruppi di sicurezza toocreate utenti tooallow, `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` come descritto in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0). 

Le impostazioni di Gruppi di Office 365 vengono configurare con un oggetto Settings e un oggetto SettingsTemplate. Inizialmente, non verranno visualizzati tutti gli oggetti impostazioni nella directory, perché la directory è configurata con le impostazioni predefinite di hello. le impostazioni predefinite di hello toochange, è necessario creare un nuovo oggetto impostazioni utilizzando un modello di impostazioni. I modelli di impostazioni sono definiti da Microsoft. Sono disponibili diversi modelli di impostazioni. impostazioni di gruppo tooconfigure Office 365 per la directory, utilizzare il modello di hello denominato "Group.Unified". impostazioni del gruppo tooconfigure Office 365 in un singolo gruppo, utilizzare il modello di hello denominato "Group.Unified.Guest". Questo modello è gruppo tooan Office 365 di accesso guest toomanage utilizzato. 

i cmdlet di Hello sono parte del modulo di Azure Active Directory PowerShell V2 hello. Per istruzioni toodownload e installazione hello modulo nel computer in uso, vedere articolo hello [Azure Active Directory PowerShell versione 2](https://docs.microsoft.com/powershell/azuread/). È possibile installare una versione di hello versione 2 del modulo hello da [raccolta PowerShell hello](https://www.powershellgallery.com/packages/AzureAD/).

## <a name="retrieve-a-specific-settings-value"></a>Recuperare un valore di impostazione specifico
Se si conosce il nome di hello di hello impostazione desidera tooretrieve, è possibile usare hello seguito cmdlet tooretrieve hello corrente il valore delle impostazioni. In questo esempio, vengono recuperate valore hello per un'impostazione denominata "UsageGuidelinesUrl". Più avanti in questo capitolo sono disponibili altre informazioni sulle impostazioni di directory e i rispettivi nomi.

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a>Creare le impostazioni a livello di directory hello
Questi passaggi creano le impostazioni a livello di directory, che si applicano a gruppi di Office 365 tooall (gruppi unificato) nella directory hello.

1. In hello DirectorySettings cmdlet, è necessario specificare ID hello di hello SettingsTemplate desiderato toouse. Se non si conosce questo ID, questo cmdlet restituisce l'elenco di hello di tutti i modelli di impostazioni:
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  Questa chiamata del cmdlet restituirà tutti i modelli disponibili:
  
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
2. tooadd un URL delle linee guida sull'utilizzo, è necessario innanzitutto tooget hello SettingsTemplate che definisce il valore hello di URL delle linee guida sull'utilizzo; vale a dire hello Group.Unified modello:
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. Successivamente, creare un nuovo oggetto impostazioni sulla base del modello:
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. Aggiornare quindi il valore hello utilizzo delle linee guida:
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. Infine, applicare le impostazioni di hello:
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

Al completamento, hello cmdlet restituisce hello ID dell'oggetto Impostazioni nuovo hello:
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
Ecco le impostazioni di hello definite in hello Group.Unified SettingsTemplate.

| **Impostazione** | **Descrizione** |
| --- | --- |
|  <ul><li>EnableGroupCreation<li>Tipo: Boolean<li>Valore predefinito: True |flag di Hello che indica se la creazione del gruppo unificato è consentita nella directory hello. |
|  <ul><li>GroupCreationAllowedGroupId<li>Tipo: String<li>Predefinito: "" |GUID del gruppo di sicurezza hello per cui hello membri sono consentiti gruppi unificati toocreate anche quando EnableGroupCreation = = false. |
|  <ul><li>UsageGuidelinesUrl<li>Tipo: String<li>Predefinito: "" |Un collegamento toohello linee guida di utilizzo di gruppo. |
|  <ul><li>ClassificationDescriptions<li>Tipo: String<li>Predefinito: "" | Elenco delimitato da virgole di descrizioni di classificazione. |
|  <ul><li>DefaultClassification<li>Tipo: String<li>Predefinito: "" | classificazione Hello che viene utilizzato come classificazione di hello predefinita per un gruppo se non è stato specificato alcun toobe.|
|  <ul><li>PrefixSuffixNamingRequirement<li>Tipo: String<li>Predefinito: "" |Non ancora implementato
|  <ul><li>AllowGuestsToBeGroupOwner<li>Tipo: booleano<li>Valore predefinito: False | Valore booleano che indica se un utente guest può essere o meno un proprietario di gruppi. |
|  <ul><li>AllowGuestsToAccessGroups<li>Tipo: booleano<li>Valore predefinito: True | Valore booleano che indica se un utente guest può avere contenuto gruppi tooUnified di accesso. |
|  <ul><li>GuestUsageGuidelinesUrl<li>Tipo: String<li>Predefinito: "" | url di Hello di indicazioni per l'utilizzo un collegamento toohello guest. |
|  <ul><li>AllowToAddGuests<li>Tipo: booleano<li>Valore predefinito: True | Un valore booleano che indica se è consentito tooadd guest toothis directory.|
|  <ul><li>ClassificationList<li>Tipo: String<li>Predefinito: "" |Un elenco delimitato da virgole dei valori di classificazione valido che può essere applicato tooUnified gruppi. |
|  <ul><li>EnableGroupCreation<li>Tipo: Boolean<li>Valore predefinito: True | Valore booleano che indica se gli utenti non amministratori possono creare nuovi gruppi unificati. |


## <a name="read-settings-at-hello-directory-level"></a>Leggere le impostazioni a livello di directory hello
Questi passaggi leggono le impostazioni a livello di directory, che si applicano tooall gruppi di Office nella directory hello.

1. Leggere tutte le impostazioni della directory esistenti:
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  Questo cmdlet restituisce un elenco di tutte le impostazioni della directory:
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. Leggere tutte le impostazioni di un determinato gruppo:
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. Leggere tutti i valori delle impostazioni di directory di un oggetto Settings della directory specifico, usando il GUID delle impostazioni:
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  Questo cmdlet restituisce i nomi di hello e i valori in questo oggetto impostazioni per questo gruppo specifico:
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

## <a name="update-settings-for-a-specific-group"></a>Aggiornare le impostazioni per un gruppo specifico

1. Cercare hello impostazioni modello denominato "Groups.Unified.Guest"
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
2. Recuperare hello modello oggetto per il modello Groups.Unified.Guest hello:
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. Creare un nuovo oggetto impostazioni dal modello hello:
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. Impostare l'impostazione del valore toohello necessario hello:
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. Creare hello nuova impostazione per il gruppo richiesto hello nella directory hello:
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a>Aggiornare le impostazioni a livello di directory hello

Questi passaggi aggiornino le impostazioni a livello di directory, che si applicano tooall unificato gruppi nella directory hello. Questi esempi presuppongono che nella directory esista già un oggetto Settings.

1. Trovare l'oggetto impostazioni esistente hello:
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. Aggiornare il valore di hello:
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. Aggiornamento dell'impostazione hello:
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a>Rimuovere le impostazioni a livello di directory hello
Questo passaggio rimuove le impostazioni a livello di directory, che si applicano tooall gruppi di Office nella directory hello.
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a>Riferimento alla sintassi cmdlet
Per altre informazioni su Azure Active Directory PowerShell, consultare la documentazione sui [cmdlet di Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).

## <a name="additional-reading"></a>Informazioni aggiuntive

* [Gestione di accesso tooresources con gruppi di Azure Active Directory](active-directory-manage-groups.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
