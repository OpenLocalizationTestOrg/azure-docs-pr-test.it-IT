---
title: Esempio di PowerShell - Controllo e rilevamento delle minacce per un database SQL di Azure | Microsoft Docs
description: Esempio di script di Azure PowerShell per configurare il controllo e il rilevamento delle minacce in un database SQL di Azure
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
ms.openlocfilehash: e039d35474bff3b066a6605a97e04d4a81c365eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-configure-sql-database-auditing-and-threat-detection"></a><span data-ttu-id="8e6ae-103">Usare PowerShell per configurare il controllo e il rilevamento delle minacce per il database SQL</span><span class="sxs-lookup"><span data-stu-id="8e6ae-103">Use PowerShell to configure SQL Database auditing and threat detection</span></span>

<span data-ttu-id="8e6ae-104">Questo esempio di script di PowerShell configura il controllo e il rilevamento delle minacce del database SQL.</span><span class="sxs-lookup"><span data-stu-id="8e6ae-104">This PowerShell script example configures SQL Database auditing and threat detection.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="8e6ae-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="8e6ae-105">Sample script</span></span>

<span data-ttu-id="8e6ae-106">[!code-powershell[principale](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configurare il controllo e il rilevamento delle minacce")]</span><span class="sxs-lookup"><span data-stu-id="8e6ae-106">[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="8e6ae-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="8e6ae-107">Clean up deployment</span></span>

<span data-ttu-id="8e6ae-108">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="8e6ae-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="8e6ae-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="8e6ae-109">Script explanation</span></span>

<span data-ttu-id="8e6ae-110">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="8e6ae-110">This script uses the following commands.</span></span> <span data-ttu-id="8e6ae-111">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="8e6ae-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8e6ae-112">Comando</span><span class="sxs-lookup"><span data-stu-id="8e6ae-112">Command</span></span> | <span data-ttu-id="8e6ae-113">Note</span><span class="sxs-lookup"><span data-stu-id="8e6ae-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8e6ae-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8e6ae-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="8e6ae-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="8e6ae-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8e6ae-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="8e6ae-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="8e6ae-117">Crea un server logico che ospita un database o un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="8e6ae-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="8e6ae-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="8e6ae-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="8e6ae-119">Crea un database in un server logico come database singolo o in pool.</span><span class="sxs-lookup"><span data-stu-id="8e6ae-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="8e6ae-120">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="8e6ae-120">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="8e6ae-121">Crea un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8e6ae-121">Creates a Storage account.</span></span> |
| [<span data-ttu-id="8e6ae-122">Set-AzureRmSqlDatabaseAuditingPolicy</span><span class="sxs-lookup"><span data-stu-id="8e6ae-122">Set-AzureRmSqlDatabaseAuditingPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | <span data-ttu-id="8e6ae-123">Imposta i criteri di controllo per un database.</span><span class="sxs-lookup"><span data-stu-id="8e6ae-123">Sets the auditing policy for a database.</span></span> |
| [<span data-ttu-id="8e6ae-124">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="8e6ae-124">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | <span data-ttu-id="8e6ae-125">Imposta i criteri di rilevamento delle minacce in un database.</span><span class="sxs-lookup"><span data-stu-id="8e6ae-125">Sets a threat detection policy on a database.</span></span> |
| [<span data-ttu-id="8e6ae-126">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8e6ae-126">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="8e6ae-127">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="8e6ae-127">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="8e6ae-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8e6ae-128">Next steps</span></span>

<span data-ttu-id="8e6ae-129">Per altre informazioni su Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8e6ae-129">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8e6ae-130">Per altri esempi, vedere tra gli [script di PowerShell per database SQL di Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8e6ae-130">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
