---
title: Creazione di report sull'accesso - Controllo degli accessi in base al ruolo di Azure | Documentazione Microsoft
description: Generare un report che elenca tutte le modifiche nell'accesso alle sottoscrizioni di Azure con il controllo degli accessi in base al ruolo negli ultimi 90 giorni.
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 2bc68595-145e-4de3-8b71-3a21890d13d9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4e8028ab43ed02ef0c0a1374326b07f72f97d9d9
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a>Creare un report degli accessi per il controllo degli accessi in base al ruolo
Ogni volta che un utente concede o revoca l'accesso all'interno delle sottoscrizioni, le modifiche vengono registrate negli eventi di Azure. È possibile creare report della cronologia delle modifiche relative all'accesso per visualizzare tutte le modifiche degli ultimi 90 giorni.

## <a name="create-a-report-with-azure-powershell"></a>Creare un rapporto con Azure PowerShell
Per creare un report della cronologia delle modifiche relative all'accesso in PowerShell, usare il comando [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog).

Quando si chiama questo comando, è possibile specificare la proprietà delle assegnazioni da elencare, ad esempio:

| Proprietà | Descrizione |
| --- | --- |
| **Azione** |Indica se l'accesso è stato concesso o revocato. |
| **Chiamante** |Proprietario responsabile della modifica all'accesso. |
| **PrincipalId** | L'identificatore univoco dell'utente, del gruppo o dell'applicazione che è stato assegnato al ruolo |
| **PrincipalName** |Nome dell'utente, del gruppo o dell'applicazione. |
| **PrincipalType** |Indica se l'assegnazione era destinata a un utente, un gruppo o un'applicazione |
| **RoleDefinitionId** |GUID del ruolo concesso o revocato. |
| **RoleName** |Ruolo concesso o revocato. |
| **Ambito** | L'identificatore univoco della sottoscrizione, del gruppo di risorse o della risorsa a cui si applica l'assegnazione | 
| **ScopeName** |Nome della sottoscrizione, del gruppo di risorse o della risorsa. |
| **ScopeType** |Indica se l'assegnazione era a livello di ambito della sottoscrizione, del gruppo di risorse e della risorsa. |
| **Timestamp** |Data e ora in cui l'accesso è stato modificato. |

Questo comando di esempio elenca tutte le modifiche relative all'accesso nella sottoscrizione per gli ultimi 7 giorni.

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - Schermata](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a>Creare un rapporto con l’interfaccia di riga di comando di Azure
Per creare un report della cronologia delle modifiche relative all'accesso nell'interfaccia della riga di comando, usare il comando `azure role assignment changelog list` .

## <a name="export-to-a-spreadsheet"></a>Esportare in un foglio di calcolo
Per salvare il report o modificare i dati, esportare le modifiche relative all'accesso in un file CSV. Sarà quindi possibile visualizzare il report in un foglio di calcolo per la revisione.

![Log delle modifiche visualizzato come foglio di calcolo - Schermata](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a>Passaggi successivi
* Utilizzare i [ruoli personalizzati nel Controllo degli accessi in base al ruolo di Azure](role-based-access-control-custom-roles.md)
* Informazioni sono disponibili in [Gestire il controllo degli accessi in base al ruolo con Azure PowerShell](role-based-access-control-manage-access-powershell.md)

