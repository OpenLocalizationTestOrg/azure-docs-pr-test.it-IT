---
title: rilevamento di minaccia controllo esempio aaaPowerShell-Azure SQL Database | Documenti Microsoft
description: Azure PowerShell esempio script tooconfigure controllo & minaccia rilevamento in un Database di SQL Azure
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 97e057ac6efe5e730404ae796bc01e7e5c70df35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-sql-database-auditing-and-threat-detection"></a><span data-ttu-id="544f9-103">Utilizzare PowerShell tooconfigure Database SQL di controllo e di minaccia il rilevamento</span><span class="sxs-lookup"><span data-stu-id="544f9-103">Use PowerShell tooconfigure SQL Database auditing and threat detection</span></span>

<span data-ttu-id="544f9-104">Questo esempio di script di PowerShell configura il controllo e il rilevamento delle minacce del database SQL.</span><span class="sxs-lookup"><span data-stu-id="544f9-104">This PowerShell script example configures SQL Database auditing and threat detection.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="544f9-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="544f9-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]

## <a name="clean-up-deployment"></a><span data-ttu-id="544f9-106">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="544f9-106">Clean up deployment</span></span>

<span data-ttu-id="544f9-107">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello e tutte le risorse associate.</span><span class="sxs-lookup"><span data-stu-id="544f9-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="544f9-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="544f9-108">Script explanation</span></span>

<span data-ttu-id="544f9-109">Questo script utilizza hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="544f9-109">This script uses hello following commands.</span></span> <span data-ttu-id="544f9-110">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="544f9-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="544f9-111">Comando</span><span class="sxs-lookup"><span data-stu-id="544f9-111">Command</span></span> | <span data-ttu-id="544f9-112">Note</span><span class="sxs-lookup"><span data-stu-id="544f9-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="544f9-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="544f9-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="544f9-114">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="544f9-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="544f9-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="544f9-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="544f9-116">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="544f9-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="544f9-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="544f9-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="544f9-118">Crea un database in un server logico come database singolo o in pool.</span><span class="sxs-lookup"><span data-stu-id="544f9-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="544f9-119">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="544f9-119">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="544f9-120">Crea un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="544f9-120">Creates a Storage account.</span></span> |
| [<span data-ttu-id="544f9-121">Set-AzureRmSqlDatabaseAuditingPolicy</span><span class="sxs-lookup"><span data-stu-id="544f9-121">Set-AzureRmSqlDatabaseAuditingPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | <span data-ttu-id="544f9-122">Imposta i criteri di controllo hello per un database.</span><span class="sxs-lookup"><span data-stu-id="544f9-122">Sets hello auditing policy for a database.</span></span> |
| [<span data-ttu-id="544f9-123">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="544f9-123">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | <span data-ttu-id="544f9-124">Imposta i criteri di rilevamento delle minacce in un database.</span><span class="sxs-lookup"><span data-stu-id="544f9-124">Sets a threat detection policy on a database.</span></span> |
| [<span data-ttu-id="544f9-125">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="544f9-125">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="544f9-126">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="544f9-126">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="544f9-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="544f9-127">Next steps</span></span>

<span data-ttu-id="544f9-128">Per ulteriori informazioni su hello Azure PowerShell, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="544f9-128">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="544f9-129">Ulteriori esempi di script di PowerShell per Database SQL sono reperibile in hello [gli script di PowerShell per Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="544f9-129">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
