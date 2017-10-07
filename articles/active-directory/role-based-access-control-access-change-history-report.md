---
title: creazione di report aaaAccess - RBAC Azure | Documenti Microsoft
description: Generare un report che elenca tutte le modifiche nell'accesso tooyour le sottoscrizioni di Azure con Role-Based Access Control tramite hello ultimi 90 giorni.
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
ms.openlocfilehash: 9ad85d3d8e66ce167032638a35e4afffb46d3892
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a>Creare un report degli accessi per il controllo degli accessi in base al ruolo
Ogni volta che un utente concede o revoca l'accesso all'interno delle sottoscrizioni, le modifiche di hello vengono registrate gli eventi di Azure. È possibile creare accesso Modifica cronologia report toosee tutte le modifiche per hello ultimi 90 giorni.

## <a name="create-a-report-with-azure-powershell"></a>Creare un rapporto con Azure PowerShell
un accesso toocreate modificare report della cronologia in PowerShell, usare hello [Get AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) comando.

Quando si chiama questo comando, è possibile specificare le proprietà delle assegnazioni di hello desiderato, inclusi hello seguenti:

| Proprietà | Descrizione |
| --- | --- |
| **Azione** |Indica se l'accesso è stato concesso o revocato. |
| **Chiamante** |Modifica proprietario Hello responsabile per l'accesso hello |
| **PrincipalId** | Identificatore univoco dell'applicazione che è stato assegnato il ruolo di hello, gruppo o utente hello Hello |
| **PrincipalName** |nome Hello di hello utente, gruppo o applicazione |
| **PrincipalType** |Se l'assegnazione hello è per un utente, gruppo o l'applicazione |
| **RoleDefinitionId** |GUID del ruolo hello che è stato concesso o revocato Hello |
| **RoleName** |ruolo Hello che è stato concesso o revocato |
| **Ambito** | Identificatore univoco di Hello della sottoscrizione di hello, gruppo di risorse o una risorsa hello assegnazione applica troppo| 
| **ScopeName** |nome di Hello della sottoscrizione hello, gruppo di risorse o risorsa |
| **ScopeType** |Se l'assegnazione hello è nell'ambito di risorsa, gruppo di risorse o di sottoscrizione hello |
| **Timestamp** |Hello data e ora di accesso è stato modificato. |

Questo comando di esempio sono elencate tutte le modifiche di accesso nella sottoscrizione hello per hello ultimi sette giorni:

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - Schermata](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a>Creare un rapporto con l’interfaccia di riga di comando di Azure
toocreate un report di cronologia modifiche di access in hello Azure interfaccia della riga di comando (CLI), utilizzare hello `azure role assignment changelog list` comando.

## <a name="export-tooa-spreadsheet"></a>Esportare tooa foglio di calcolo
toosave hello report o modificare i dati di hello, l'accesso hello esportazione le modifiche in un file con estensione csv. È quindi possibile visualizzare report hello in un foglio di calcolo per la revisione.

![Log delle modifiche visualizzato come foglio di calcolo - Schermata](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a>Passaggi successivi
* Utilizzare i [ruoli personalizzati nel Controllo degli accessi in base al ruolo di Azure](role-based-access-control-custom-roles.md)
* Informazioni su come toomanage [RBAC Azure con powershell](role-based-access-control-manage-access-powershell.md)

