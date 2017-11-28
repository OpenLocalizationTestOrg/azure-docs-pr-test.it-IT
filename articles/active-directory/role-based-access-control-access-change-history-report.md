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
# <a name="create-an-access-report-for-role-based-access-control"></a><span data-ttu-id="c9d75-103">Creare un report degli accessi per il controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="c9d75-103">Create an access report for Role-Based Access Control</span></span>
<span data-ttu-id="c9d75-104">Ogni volta che un utente concede o revoca l'accesso all'interno delle sottoscrizioni, le modifiche di hello vengono registrate gli eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="c9d75-104">Any time someone grants or revokes access within your subscriptions, hello changes get logged in Azure events.</span></span> <span data-ttu-id="c9d75-105">È possibile creare accesso Modifica cronologia report toosee tutte le modifiche per hello ultimi 90 giorni.</span><span class="sxs-lookup"><span data-stu-id="c9d75-105">You can create access change history reports toosee all changes for hello past 90 days.</span></span>

## <a name="create-a-report-with-azure-powershell"></a><span data-ttu-id="c9d75-106">Creare un rapporto con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9d75-106">Create a report with Azure PowerShell</span></span>
<span data-ttu-id="c9d75-107">un accesso toocreate modificare report della cronologia in PowerShell, usare hello [Get AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) comando.</span><span class="sxs-lookup"><span data-stu-id="c9d75-107">toocreate an access change history report in PowerShell, use hello [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) command.</span></span>

<span data-ttu-id="c9d75-108">Quando si chiama questo comando, è possibile specificare le proprietà delle assegnazioni di hello desiderato, inclusi hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="c9d75-108">When you call this command, you can specify which property of hello assignments you want listed, including hello following:</span></span>

| <span data-ttu-id="c9d75-109">Proprietà</span><span class="sxs-lookup"><span data-stu-id="c9d75-109">Property</span></span> | <span data-ttu-id="c9d75-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c9d75-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c9d75-111">**Azione**</span><span class="sxs-lookup"><span data-stu-id="c9d75-111">**Action**</span></span> |<span data-ttu-id="c9d75-112">Indica se l'accesso è stato concesso o revocato.</span><span class="sxs-lookup"><span data-stu-id="c9d75-112">Whether access was granted or revoked</span></span> |
| <span data-ttu-id="c9d75-113">**Chiamante**</span><span class="sxs-lookup"><span data-stu-id="c9d75-113">**Caller**</span></span> |<span data-ttu-id="c9d75-114">Modifica proprietario Hello responsabile per l'accesso hello</span><span class="sxs-lookup"><span data-stu-id="c9d75-114">hello owner responsible for hello access change</span></span> |
| <span data-ttu-id="c9d75-115">**PrincipalId**</span><span class="sxs-lookup"><span data-stu-id="c9d75-115">**PrincipalId**</span></span> | <span data-ttu-id="c9d75-116">Identificatore univoco dell'applicazione che è stato assegnato il ruolo di hello, gruppo o utente hello Hello</span><span class="sxs-lookup"><span data-stu-id="c9d75-116">hello unique identifier of hello user, group, or application that was assigned hello role</span></span> |
| <span data-ttu-id="c9d75-117">**PrincipalName**</span><span class="sxs-lookup"><span data-stu-id="c9d75-117">**PrincipalName**</span></span> |<span data-ttu-id="c9d75-118">nome Hello di hello utente, gruppo o applicazione</span><span class="sxs-lookup"><span data-stu-id="c9d75-118">hello name of hello user, group, or application</span></span> |
| <span data-ttu-id="c9d75-119">**PrincipalType**</span><span class="sxs-lookup"><span data-stu-id="c9d75-119">**PrincipalType**</span></span> |<span data-ttu-id="c9d75-120">Se l'assegnazione hello è per un utente, gruppo o l'applicazione</span><span class="sxs-lookup"><span data-stu-id="c9d75-120">Whether hello assignment was for a user, group, or application</span></span> |
| <span data-ttu-id="c9d75-121">**RoleDefinitionId**</span><span class="sxs-lookup"><span data-stu-id="c9d75-121">**RoleDefinitionId**</span></span> |<span data-ttu-id="c9d75-122">GUID del ruolo hello che è stato concesso o revocato Hello</span><span class="sxs-lookup"><span data-stu-id="c9d75-122">hello GUID of hello role that was granted or revoked</span></span> |
| <span data-ttu-id="c9d75-123">**RoleName**</span><span class="sxs-lookup"><span data-stu-id="c9d75-123">**RoleName**</span></span> |<span data-ttu-id="c9d75-124">ruolo Hello che è stato concesso o revocato</span><span class="sxs-lookup"><span data-stu-id="c9d75-124">hello role that was granted or revoked</span></span> |
| <span data-ttu-id="c9d75-125">**Ambito**</span><span class="sxs-lookup"><span data-stu-id="c9d75-125">**Scope**</span></span> | <span data-ttu-id="c9d75-126">Identificatore univoco di Hello della sottoscrizione di hello, gruppo di risorse o una risorsa hello assegnazione applica troppo</span><span class="sxs-lookup"><span data-stu-id="c9d75-126">hello unique identifier of hello subscription, resource group, or resource that hello assignment applies too</span></span>| 
| <span data-ttu-id="c9d75-127">**ScopeName**</span><span class="sxs-lookup"><span data-stu-id="c9d75-127">**ScopeName**</span></span> |<span data-ttu-id="c9d75-128">nome di Hello della sottoscrizione hello, gruppo di risorse o risorsa</span><span class="sxs-lookup"><span data-stu-id="c9d75-128">hello name of hello subscription, resource group, or resource</span></span> |
| <span data-ttu-id="c9d75-129">**ScopeType**</span><span class="sxs-lookup"><span data-stu-id="c9d75-129">**ScopeType**</span></span> |<span data-ttu-id="c9d75-130">Se l'assegnazione hello è nell'ambito di risorsa, gruppo di risorse o di sottoscrizione hello</span><span class="sxs-lookup"><span data-stu-id="c9d75-130">Whether hello assignment was at hello subscription, resource group, or resource scope</span></span> |
| <span data-ttu-id="c9d75-131">**Timestamp**</span><span class="sxs-lookup"><span data-stu-id="c9d75-131">**Timestamp**</span></span> |<span data-ttu-id="c9d75-132">Hello data e ora di accesso è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="c9d75-132">hello date and time that access was changed</span></span> |

<span data-ttu-id="c9d75-133">Questo comando di esempio sono elencate tutte le modifiche di accesso nella sottoscrizione hello per hello ultimi sette giorni:</span><span class="sxs-lookup"><span data-stu-id="c9d75-133">This example command lists all access changes in hello subscription for hello past seven days:</span></span>

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - Schermata](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a><span data-ttu-id="c9d75-135">Creare un rapporto con l’interfaccia di riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="c9d75-135">Create a report with Azure CLI</span></span>
<span data-ttu-id="c9d75-136">toocreate un report di cronologia modifiche di access in hello Azure interfaccia della riga di comando (CLI), utilizzare hello `azure role assignment changelog list` comando.</span><span class="sxs-lookup"><span data-stu-id="c9d75-136">toocreate an access change history report in hello Azure command-line interface (CLI), use hello `azure role assignment changelog list` command.</span></span>

## <a name="export-tooa-spreadsheet"></a><span data-ttu-id="c9d75-137">Esportare tooa foglio di calcolo</span><span class="sxs-lookup"><span data-stu-id="c9d75-137">Export tooa spreadsheet</span></span>
<span data-ttu-id="c9d75-138">toosave hello report o modificare i dati di hello, l'accesso hello esportazione le modifiche in un file con estensione csv.</span><span class="sxs-lookup"><span data-stu-id="c9d75-138">toosave hello report, or manipulate hello data, export hello access changes into a .csv file.</span></span> <span data-ttu-id="c9d75-139">È quindi possibile visualizzare report hello in un foglio di calcolo per la revisione.</span><span class="sxs-lookup"><span data-stu-id="c9d75-139">You can then view hello report in a spreadsheet for review.</span></span>

![Log delle modifiche visualizzato come foglio di calcolo - Schermata](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a><span data-ttu-id="c9d75-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c9d75-141">Next steps</span></span>
* <span data-ttu-id="c9d75-142">Utilizzare i [ruoli personalizzati nel Controllo degli accessi in base al ruolo di Azure](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="c9d75-142">Work with [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>
* <span data-ttu-id="c9d75-143">Informazioni su come toomanage [RBAC Azure con powershell](role-based-access-control-manage-access-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="c9d75-143">Learn how toomanage [Azure RBAC with powershell](role-based-access-control-manage-access-powershell.md)</span></span>

