---
title: aaaHow tooUse controllo di accesso basato sui ruoli in Gestione API di Azure | Documenti Microsoft
description: Informazioni su come toouse hello ruoli predefiniti e creare ruoli personalizzati in Gestione API di Azure
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: apimpm
ms.openlocfilehash: c51da2ff6886ebcaf796022e3a759c67f36670a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-role-based-access-control-in-azure-api-management"></a>Modalità tooUse controllo di accesso basato sui ruoli in Gestione API di Azure
Gestione API di Azure si basa su gestione di controllo di accesso gestire (RBAC) tooenable accesso granulare per le entità (ad esempio, API, criteri) e servizi di gestione API. Questo articolo viene fornita una panoramica dei ruoli predefiniti e personalizzati di hello in Gestione API. Se si desidera visualizzare ulteriori dettagli sulla gestione dell'accesso in hello portale di Azure, vedere [Introduzione alla gestione di accesso nel portale di Azure hello](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)

## <a name="built-in-roles"></a>Ruoli predefiniti
Gestione API attualmente sono disponibili 3 ruoli predefiniti e aggiungerà 2 più ruoli in hello prossimo futuro. Questi ruoli possono essere assegnati ad ambiti diversi, tra cui una sottoscrizione, un gruppo di risorse e una singola istanza di Gestione API. Ad esempio, se l'utente di tooan a livello di gruppo di risorse hello è assegnato il ruolo di "Lettura di servizio Gestione API di Azure" hello, quindi hello utente disporrà dell'accesso in lettura tooall gestione API istanze all'interno di hello gruppo di risorse. 

Hello nella tabella seguente vengono fornite brevi descrizioni di hello ruoli predefiniti. È possibile assegnare questi ruoli mediante hello portale di Azure o altri strumenti incluso Azure [PowerShell](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-powershell), Azure [interfaccia della riga di comando](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-azure-cli), e [API REST](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-rest). Per informazioni dettagliate su come tooassign ruoli predefiniti, vedere [utilizzare le risorse di sottoscrizione di Azure tooyour accesso toomanage assegnazioni ruolo](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/).

| Ruolo          | Accesso in lettura<sup>[1]</sup> | Accesso in scrittura<sup>[2]</sup> | Creazione, eliminazione e ridimensionamento di servizi, configurazione dominio personalizzato e VPN | Accesso toolegacy Publsiher portale | Descrizione
| ------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| Collaboratore Servizio Gestione API di Azure | ✓ | ✓  | ✓  | ✓ | Utente con privilegi avanzati. Completo di servizi di gestione tooAPI accesso CRUD ed entità (ad esempio, API, criteri). Dispone di accesso toohello publisher legacy portale. |
| Ruolo lettura del servizio Gestione API di Azure | ✓ | | || Entità e i servizi di gestione tooAPI di accesso in sola lettura. |
| Operatore del servizio Gestione API di Azure | ✓ | | ✓ | | Può gestire i servizi Gestione API, ma non le entità.|
| Editor del servizio Gestione API di Azure<sup>*</sup> | ✓ | ✓ | |  | Può gestire le entità Gestione API, ma non i servizi.|
| Gestione contenuto del servizio Gestione API di Azure<sup>*</sup> | ✓ | | | ✓ | Può gestire il portale per sviluppatori. Accesso in sola lettura tooservices ed entità.|

<sup>[1] servizi di gestione di accesso in lettura tooAPI ed entità (ad esempio, API, criteri)</sup>

<sup>Accesso in scrittura [2] tooAPI Gestione servizi e le entità, tranne opeartions seguenti: 1) istanza creazione, eliminazione e scalabilità e configurazione nome del dominio personalizzato 3) configurazione VPN 2)</sup>

<sup>\*ruolo di Editor servizio Hello saranno disponibile quando si esegue la migrazione di interfaccia utente di amministrazione di tutti da hello esistente publisher portale toohello portale di Azure. Hello ruolo Gestione contenuto saranno disponibile dopo il portale di pubblicazione hello viene effettuato il refactoring tooonly contenere portale per sviluppatori di funzionalità correlate toomanaging hello.</sup>  


## <a name="custom-roles"></a>Ruoli personalizzati
Se nessuno dei ruoli predefiniti hello soddisfare esigenze specifiche, ruoli personalizzati possono essere creati tooprovide più granulare access management per le entità di gestione API. Ad esempio, è possibile creare un ruolo personalizzato che ha accesso in sola lettura tooan servizio Gestione API ma solo accesso in scrittura tooone specifiche API. toolearn ulteriori informazioni sui ruoli personalizzati, vedere [ruoli personalizzati in Azure RBAC](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles). 

Quando si crea un ruolo personalizzato, è più facile toostart con uno dei ruoli predefiniti di hello. Modificare hello attributi tooadd azioni hello, NotActions o AssignableScopes, quindi salvare le modifiche di hello come un nuovo ruolo. Hello esempio inizia con il ruolo di "Lettura di servizio Gestione API di Azure" hello e crea un ruolo personalizzato denominato "Editor API Calculator". ruolo personalizzata Hello può essere assegnato solo tooa che API specifica verrà pertanto solo dispone di accesso toothat API. 

```
$role = Get-AzureRmRoleDefinition "API Management Service Reader Role"
$role.Id = $null
$role.Name = 'Calculator API Contributor'
$role.Description = 'Has read access tooContoso APIM instance and write access toohello Calculator API.'
$role.Actions.Add('Microsoft.ApiManagement/service/apis/write')
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add('/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>')
New-AzureRmRoleDefinition -Role $role
New-AzureRmRoleAssignment -ObjectId <object ID of hello user account> -RoleDefinitionName 'Calculator API Contributor' -Scope '/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>'
```

## <a name="watch-a-video-overview"></a>Guardare un video introduttivo

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Role-Based-Access-Control-in-API-Management/player]
> 
> 

## <a name="next-steps"></a>Passaggi successivi

* Informazioni sul controllo degli accessi in base al ruolo in Azure
  * [Introduzione alla gestione di accesso nel portale di Azure hello](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Utilizzare le risorse di sottoscrizione di Azure tooyour accesso toomanage assegnazioni ruolo](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Ruoli personalizzati nel Controllo degli accessi in base al ruolo di Azure](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles)
