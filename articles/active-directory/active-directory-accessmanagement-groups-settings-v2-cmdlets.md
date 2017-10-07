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
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a>Cmdlet di Azure Active Directory versione 2 per la gestione dei gruppi
> [!div class="op_single_selector"]
> * [Portale di Azure](active-directory-groups-create-azure-portal.md)
> * [Portale di Azure classico](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

In questo articolo contiene esempi di come toouse PowerShell toomanage i gruppi in Azure Active Directory (Azure AD).  Indica inoltre come tooget impostare con il modulo di Azure AD PowerShell hello. In primo luogo, è necessario [scaricare il modulo di Azure AD PowerShell hello](https://www.powershellgallery.com/packages/AzureAD/).

## <a name="installing-hello-azure-ad-powershell-module"></a>Installazione del modulo di Azure AD PowerShell hello
hello tooinstall modulo Azure AD PowerShell, usare hello seguenti comandi:

    PS C:\Windows\system32> install-module azuread

tooverify che hello modulo è stato installato, utilizzare hello comando seguente:

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

Ora è possibile iniziare a utilizzare i cmdlet di hello nel modulo hello. Per una descrizione completa di hello cmdlet nel modulo hello Azure AD, consultare la documentazione di riferimento online toohello per [Azure Active Directory PowerShell versione 2](/powershell/azure/install-adv2?view=azureadps-2.0).

## <a name="connecting-toohello-directory"></a>Connessione directory toohello
Prima di iniziare la gestione dei gruppi tramite i cmdlet PowerShell di Azure Active Directory, è necessario connettersi desiderato toomanage directory toohello di sessione di PowerShell. Utilizzare hello comando seguente:

    PS C:\Windows\system32> Connect-AzureAD

Hello cmdlet è richiesto per hello credenziali si desidera che la directory toouse tooaccess. In questo esempio, utilizziamo karen@drumkit.onmicrosoft.com tooaccess hello directory dimostrazione. Hello cmdlet restituisce è stata stabilita una sessione di hello tooshow conferma tooyour directory:

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

Ora è possibile avviare l'utilizzo di hello AzureAD cmdlet toomanage gruppi nella directory.

## <a name="retrieving-groups"></a>Recupero di gruppi
tooretrieve gruppi esistenti dalla directory di cui che è possibile utilizzare hello cmdlet Get-AzureADGroups. tooretrieve tutti i gruppi nella directory di hello, utilizzare hello cmdlet senza parametri:

    PS C:\Windows\system32> get-azureadgroup

cmdlet di Hello restituisce tutti i gruppi nella directory connessa hello.

È possibile utilizzare hello - objectID parametro tooretrieve un gruppo specifico per il quale è specificare objectID del gruppo di hello:

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

cmdlet di Hello restituisce ora gruppo hello cui objectID corrisponde al valore hello del parametro hello immessi:

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

È possibile cercare un gruppo specifico usando hello - parametro filter. Questo parametro utilizza una clausola di filtro ODATA e restituisce tutti i gruppi che corrispondono al filtro hello, come in hello di esempio seguente:

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
> i cmdlet di AzureAD PowerShell Hello implementare hello query OData standard. Per ulteriori informazioni, vedere **$filter** in [opzioni di query di sistema OData utilizzando l'endpoint OData hello](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).

## <a name="creating-groups"></a>Creazione di gruppi
toocreate un nuovo gruppo nella directory, utilizzare cmdlet di hello AzureADGroup di nuovo. Questo cmdlet crea un nuovo gruppo di sicurezza denominato "Marketing":

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a>Aggiornamento di gruppi
tooupdate un gruppo esistente, utilizzare il cmdlet Set-AzureADGroup hello. In questo esempio, stiamo cambiando hello proprietà DisplayName del gruppo di hello ""Intune Administrators. È in primo luogo, stiamo ricerca gruppo hello utilizzando i cmdlet Get-AzureADGroup hello e filtro utilizzando l'attributo DisplayName hello:

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

Successivamente, stiamo cambiando hello descrizione toohello nuovo valore della proprietà "Amministratori dispositivo Intune":

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

Ora è ritrovare gruppo hello, è possibile notare proprietà Description hello viene aggiornato tooreflect hello nuovo valore:

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

## <a name="deleting-groups"></a>Eliminazione di gruppi
gruppi toodelete dalla directory, utilizzare i cmdlet Remove-AzureADGroup hello come segue:

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a>Gestione dei membri dei gruppi
Se è necessario nuovo gruppo di tooa membri tooadd, utilizzare il cmdlet Add-AzureADGroupMember hello. Questo comando aggiunge un gruppo di amministratori di Intune toohello membro che è stato usato nell'esempio precedente hello:

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

il parametro - ObjectId Hello è hello ObjectID di hello gruppo toowhich desideriamo tooadd un membro e - RefObjectId hello è hello ObjectID dell'utente hello desideriamo tooadd come gruppo toohello membro.

i membri esistenti tooget hello di un gruppo, utilizzare cmdlet Get-AzureADGroupMember hello, come nel seguente esempio:

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

membro hello tooremove è stato aggiunto in precedenza toohello gruppo, utilizzare Remove-AzureADGroupMember hello cmdlet, come illustrato di seguito:

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

tooverify hello gruppo appartenenze di un utente, utilizzare cmdlet Select-AzureADGroupIdsUserIsMemberOf hello. Questo cmdlet accetta come parametri hello ObjectId dell'utente hello per le appartenenze toocheck hello e un elenco di gruppi per le appartenenze hello che toocheck. elenco di Hello di gruppi deve essere fornita sotto forma di hello di una variabile complesso di tipo "Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck", quindi è innanzitutto necessario creare una variabile con tipo:

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

È quindi necessario fornire valori per hello toocheck di ID dei gruppi nell'attributo hello "ID" dei gruppi di questa variabile di tipo complesso:

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

A questo punto, se si desidera che le appartenenze al gruppo di un utente con 72cd4bbd-2594-40a2-935c-016f3cfeeeea ObjectID in più gruppi di hello in $g toocheck hello, da utilizzare:

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


il valore di Hello restituito è un elenco di gruppi di cui l'utente è membro. È inoltre possibile applicare questo toocheck metodo contatti, gruppi o entità servizio l'appartenenza a un determinato elenco di gruppi, utilizzando AzureADGroupIdsContactIsMemberOf selezionare, selezionare AzureADGroupIdsGroupIsMemberOf o Selezionare AzureADGroupIdsServicePrincipalIsMemberOf

## <a name="managing-owners-of-groups"></a>Gestione dei proprietari dei gruppi
gruppo proprietari tooa tooadd, consente di utilizzare hello Aggiungi AzureADGroupOwner cmdlet:

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

il parametro - ObjectId Hello è hello ObjectID di hello gruppo toowhich desideriamo tooadd un proprietario e - RefObjectId hello è hello ObjectID dell'utente hello desideriamo tooadd come proprietario del gruppo di hello.

i proprietari di hello tooretrieve di un gruppo, usare il cmdlet Get-AzureADGroupOwner hello:

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

cmdlet di Hello restituisce elenco hello di proprietari per il gruppo specificato hello:

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

Se si desidera tooremove un proprietario di un gruppo, utilizzare cmdlet Remove-AzureADGroupOwner hello:

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a>Alias riservati 
Quando viene creato un gruppo, determinati endpoint consentono hello utente finale toospecify un toobe mailNickname o alias utilizzato come parte dell'indirizzo di posta elettronica hello del gruppo di hello. Solo è possibile creare gruppi con hello seguendo gli alias di posta elettronica con privilegi elevati da un amministratore globale di Azure AD. 
  
* abuse 
* admin 
* entità 
* hostmaster 
* majordomo 
* postmaster 
* root 
* secure 
* security 
* ssl-admin 
* webmaster 

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni su Azure Active Directory PowerShell, consultare la documentazione sui [cmdlet di Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).

* [Gestione di accesso tooresources con gruppi di Azure Active Directory](active-directory-manage-groups.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
