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
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a><span data-ttu-id="0e64e-103">Creare un report degli accessi per il controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="0e64e-103">Create an access report for Role-Based Access Control</span></span>
<span data-ttu-id="0e64e-104">Ogni volta che un utente concede o revoca l'accesso all'interno delle sottoscrizioni, le modifiche vengono registrate negli eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e64e-104">Any time someone grants or revokes access within your subscriptions, the changes get logged in Azure events.</span></span> <span data-ttu-id="0e64e-105">È possibile creare report della cronologia delle modifiche relative all'accesso per visualizzare tutte le modifiche degli ultimi 90 giorni.</span><span class="sxs-lookup"><span data-stu-id="0e64e-105">You can create access change history reports to see all changes for the past 90 days.</span></span>

## <a name="create-a-report-with-azure-powershell"></a><span data-ttu-id="0e64e-106">Creare un rapporto con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e64e-106">Create a report with Azure PowerShell</span></span>
<span data-ttu-id="0e64e-107">Per creare un report della cronologia delle modifiche relative all'accesso in PowerShell, usare il comando [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog).</span><span class="sxs-lookup"><span data-stu-id="0e64e-107">To create an access change history report in PowerShell, use the [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) command.</span></span>

<span data-ttu-id="0e64e-108">Quando si chiama questo comando, è possibile specificare la proprietà delle assegnazioni da elencare, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0e64e-108">When you call this command, you can specify which property of the assignments you want listed, including the following:</span></span>

| <span data-ttu-id="0e64e-109">Proprietà</span><span class="sxs-lookup"><span data-stu-id="0e64e-109">Property</span></span> | <span data-ttu-id="0e64e-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0e64e-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0e64e-111">**Azione**</span><span class="sxs-lookup"><span data-stu-id="0e64e-111">**Action**</span></span> |<span data-ttu-id="0e64e-112">Indica se l'accesso è stato concesso o revocato.</span><span class="sxs-lookup"><span data-stu-id="0e64e-112">Whether access was granted or revoked</span></span> |
| <span data-ttu-id="0e64e-113">**Chiamante**</span><span class="sxs-lookup"><span data-stu-id="0e64e-113">**Caller**</span></span> |<span data-ttu-id="0e64e-114">Proprietario responsabile della modifica all'accesso.</span><span class="sxs-lookup"><span data-stu-id="0e64e-114">The owner responsible for the access change</span></span> |
| <span data-ttu-id="0e64e-115">**PrincipalId**</span><span class="sxs-lookup"><span data-stu-id="0e64e-115">**PrincipalId**</span></span> | <span data-ttu-id="0e64e-116">L'identificatore univoco dell'utente, del gruppo o dell'applicazione che è stato assegnato al ruolo</span><span class="sxs-lookup"><span data-stu-id="0e64e-116">The unique identifier of the user, group, or application that was assigned the role</span></span> |
| <span data-ttu-id="0e64e-117">**PrincipalName**</span><span class="sxs-lookup"><span data-stu-id="0e64e-117">**PrincipalName**</span></span> |<span data-ttu-id="0e64e-118">Nome dell'utente, del gruppo o dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0e64e-118">The name of the user, group, or application</span></span> |
| <span data-ttu-id="0e64e-119">**PrincipalType**</span><span class="sxs-lookup"><span data-stu-id="0e64e-119">**PrincipalType**</span></span> |<span data-ttu-id="0e64e-120">Indica se l'assegnazione era destinata a un utente, un gruppo o un'applicazione</span><span class="sxs-lookup"><span data-stu-id="0e64e-120">Whether the assignment was for a user, group, or application</span></span> |
| <span data-ttu-id="0e64e-121">**RoleDefinitionId**</span><span class="sxs-lookup"><span data-stu-id="0e64e-121">**RoleDefinitionId**</span></span> |<span data-ttu-id="0e64e-122">GUID del ruolo concesso o revocato.</span><span class="sxs-lookup"><span data-stu-id="0e64e-122">The GUID of the role that was granted or revoked</span></span> |
| <span data-ttu-id="0e64e-123">**RoleName**</span><span class="sxs-lookup"><span data-stu-id="0e64e-123">**RoleName**</span></span> |<span data-ttu-id="0e64e-124">Ruolo concesso o revocato.</span><span class="sxs-lookup"><span data-stu-id="0e64e-124">The role that was granted or revoked</span></span> |
| <span data-ttu-id="0e64e-125">**Ambito**</span><span class="sxs-lookup"><span data-stu-id="0e64e-125">**Scope**</span></span> | <span data-ttu-id="0e64e-126">L'identificatore univoco della sottoscrizione, del gruppo di risorse o della risorsa a cui si applica l'assegnazione</span><span class="sxs-lookup"><span data-stu-id="0e64e-126">The unique identifier of the subscription, resource group, or resource that the assignment applies to</span></span> | 
| <span data-ttu-id="0e64e-127">**ScopeName**</span><span class="sxs-lookup"><span data-stu-id="0e64e-127">**ScopeName**</span></span> |<span data-ttu-id="0e64e-128">Nome della sottoscrizione, del gruppo di risorse o della risorsa.</span><span class="sxs-lookup"><span data-stu-id="0e64e-128">The name of the subscription, resource group, or resource</span></span> |
| <span data-ttu-id="0e64e-129">**ScopeType**</span><span class="sxs-lookup"><span data-stu-id="0e64e-129">**ScopeType**</span></span> |<span data-ttu-id="0e64e-130">Indica se l'assegnazione era a livello di ambito della sottoscrizione, del gruppo di risorse e della risorsa.</span><span class="sxs-lookup"><span data-stu-id="0e64e-130">Whether the assignment was at the subscription, resource group, or resource scope</span></span> |
| <span data-ttu-id="0e64e-131">**Timestamp**</span><span class="sxs-lookup"><span data-stu-id="0e64e-131">**Timestamp**</span></span> |<span data-ttu-id="0e64e-132">Data e ora in cui l'accesso è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="0e64e-132">The date and time that access was changed</span></span> |

<span data-ttu-id="0e64e-133">Questo comando di esempio elenca tutte le modifiche relative all'accesso nella sottoscrizione per gli ultimi 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="0e64e-133">This example command lists all access changes in the subscription for the past seven days:</span></span>

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - Schermata](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a><span data-ttu-id="0e64e-135">Creare un rapporto con l’interfaccia di riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="0e64e-135">Create a report with Azure CLI</span></span>
<span data-ttu-id="0e64e-136">Per creare un report della cronologia delle modifiche relative all'accesso nell'interfaccia della riga di comando, usare il comando `azure role assignment changelog list` .</span><span class="sxs-lookup"><span data-stu-id="0e64e-136">To create an access change history report in the Azure command-line interface (CLI), use the `azure role assignment changelog list` command.</span></span>

## <a name="export-to-a-spreadsheet"></a><span data-ttu-id="0e64e-137">Esportare in un foglio di calcolo</span><span class="sxs-lookup"><span data-stu-id="0e64e-137">Export to a spreadsheet</span></span>
<span data-ttu-id="0e64e-138">Per salvare il report o modificare i dati, esportare le modifiche relative all'accesso in un file CSV.</span><span class="sxs-lookup"><span data-stu-id="0e64e-138">To save the report, or manipulate the data, export the access changes into a .csv file.</span></span> <span data-ttu-id="0e64e-139">Sarà quindi possibile visualizzare il report in un foglio di calcolo per la revisione.</span><span class="sxs-lookup"><span data-stu-id="0e64e-139">You can then view the report in a spreadsheet for review.</span></span>

![Log delle modifiche visualizzato come foglio di calcolo - Schermata](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a><span data-ttu-id="0e64e-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0e64e-141">Next steps</span></span>
* <span data-ttu-id="0e64e-142">Utilizzare i [ruoli personalizzati nel Controllo degli accessi in base al ruolo di Azure](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="0e64e-142">Work with [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>
* <span data-ttu-id="0e64e-143">Informazioni sono disponibili in [Gestire il controllo degli accessi in base al ruolo con Azure PowerShell](role-based-access-control-manage-access-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="0e64e-143">Learn how to manage [Azure RBAC with powershell](role-based-access-control-manage-access-powershell.md)</span></span>

