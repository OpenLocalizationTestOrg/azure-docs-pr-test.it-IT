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
# <a name="grant-user-permissions-toospecific-lab-policies"></a>Concedere le autorizzazioni utente criteri lab toospecific
## <a name="overview"></a>Panoramica
Questo articolo illustra come toouse criteri lab particolare tooa di PowerShell toogrant agli utenti le autorizzazioni. In questo modo, le autorizzazioni possono essere applicate in base alle esigenze di ciascun utente. Ad esempio, è possibile toogrant impostazioni dei criteri un determinato utente hello possibilità toochange hello VM, ma non hello costo criteri.

## <a name="policies-as-resources"></a>Criteri come risorse
Come descritto in hello [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) articolo RBAC consente la gestione di accesso con granularità fine delle risorse per Azure. Usa tale controllo, è possibile separare i compiti all'interno del team di DevOps e concedere solo quantità hello di accesso toousers necessarie tooperform i processi.

In DevTest Labs, un criterio è un tipo di risorsa che consente di azione RBAC hello **Microsoft.DevTestLab/labs/policySets/policies/**. Ogni criterio lab è una risorsa nel tipo di risorsa criteri hello e può essere assegnato il ruolo RBAC tooan ambito.

Ad esempio, in ordine toogrant agli utenti di lettura/scrittura autorizzazione toohello **dimensioni delle macchine Virtuali consentite** criteri, è necessario creare un ruolo personalizzato che funziona con hello **Microsoft.DevTestLab/labs/policySets/policies/** * azione, quindi assegnare hello utenti appropriati toothis ruolo personalizzato nell'ambito di hello di **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.

toolearn ulteriori informazioni sui ruoli personalizzati in RBAC, vedere hello [controllo di accesso di ruoli personalizzato](../active-directory/role-based-access-control-custom-roles.md).

## <a name="creating-a-lab-custom-role-using-powershell"></a>Creazione di un ruolo personalizzato lab tramite PowerShell
In ordine tooget avviato, è necessario hello tooread seguente articolo verrà illustrato come tooinstall e configurare i cmdlet di Azure PowerShell hello: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).

Dopo aver impostato hello cmdlet PowerShell di Azure, è possibile eseguire hello seguenti attività:

* Elenco di tutte le operazioni di hello/azioni per un provider di risorse
* Elencare le azioni di un particolare ruolo:
* Creare un ruolo personalizzato

Hello lo script di PowerShell seguente vengono illustrati esempi di come tooperform queste attività:

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

## <a name="assigning-permissions-tooa-user-for-a-specific-policy-using-custom-roles"></a>Assegnazione di autorizzazioni tooa utente per un criterio specifico utilizzando ruoli personalizzati
Dopo aver definito i ruoli personalizzati, è possibile assegnarli toousers. In ordine tooassign utente tooa ruolo personalizzato, è innanzitutto necessario ottenere hello **ObjectId** che rappresenta tale utente. toodo utilizzati, hello **Get AzureRmADUser** cmdlet.

Nell'esempio seguente di hello, hello **ObjectId** di hello *SomeUser* utente è 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

Dopo aver hello **ObjectId** per utente hello e un nome di ruolo personalizzata, è possibile assegnare a tale utente toohello ruolo con hello **New AzureRmRoleAssignment** cmdlet:

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

Nell'esempio precedente hello hello **AllowedVmSizesInLab** criteri vengono usati. È possibile utilizzare uno qualsiasi dei seguenti criteri hello:

* MaxVmsAllowedPerUser
* MaxVmsAllowedPerLab
* AllowedVmSizesInLab
* LabVmsShutdown

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Passaggi successivi
Una volta sono state concesse le autorizzazioni toospecific lab i criteri utente, ecco alcuni tooconsider passaggi successivi:

* [Lab tooa accesso sicuro](devtest-lab-add-devtest-user.md).
* [Definire i criteri del lab](devtest-lab-set-lab-policy.md).
* [Creare un modello di lab](devtest-lab-create-template.md).
* [Creare elementi personalizzati per le VM](devtest-lab-artifact-author.md).
* [Aggiungere una macchina virtuale con lab tooa elementi](devtest-lab-add-vm-with-artifacts.md).

