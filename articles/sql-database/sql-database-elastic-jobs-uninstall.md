---
title: Come disinstallare lo strumento processi di database elastico
description: Come disinstallare lo strumento processi di database elastico
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: bfc9d820-edbd-4fca-bfbf-1f339cfcc448
ms.service: sql-database
ms.workload: sql-database
ms.custom: scale out apps
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: ae7f0bce452a0a86f6f1e4d9b0c93a0fa1727f21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="5239c-103">Disinstallare i componenti dei processi di database elastici</span><span class="sxs-lookup"><span data-stu-id="5239c-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="5239c-104">**Processi di database elastici** possono essere disinstallati utilizzando il portale o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5239c-104">**Elastic Database jobs** components can be uninstalled using either the Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-the-azure-portal"></a><span data-ttu-id="5239c-105">Disinstallare i componenti dei processi di database elastici utilizzando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5239c-105">Uninstall Elastic Database jobs components using the Azure portal</span></span>
1. <span data-ttu-id="5239c-106">Aprire il [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5239c-106">Open the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5239c-107">Passare alla sottoscrizione che contiene i componenti dei **processi di database elastici** , vale a dire la sottoscrizione in cui i componenti dei processi di database elastici sono stati installati.</span><span class="sxs-lookup"><span data-stu-id="5239c-107">Navigate to the subscription that contains **Elastic Database jobs** components, namely the subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="5239c-108">Fare clic su **Sfoglia** e quindi su **Gruppi di risorse**.</span><span class="sxs-lookup"><span data-stu-id="5239c-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="5239c-109">Selezionare il gruppo di risorse denominato "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="5239c-109">Select the resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="5239c-110">Eliminare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="5239c-110">Delete the resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="5239c-111">Disinstallare i componenti dei processi dei database elastici tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="5239c-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="5239c-112">Avviare una finestra di comando di Microsoft Azure PowerShell e passare alla sottodirectory strumenti nella cartella Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x: digitare **cd strumenti**.</span><span class="sxs-lookup"><span data-stu-id="5239c-112">Launch a Microsoft Azure PowerShell command window and navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="5239c-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span><span class="sxs-lookup"><span data-stu-id="5239c-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span></span>
2. <span data-ttu-id="5239c-114">Eseguire lo script .\UninstallElasticDatabaseJobs.ps1 di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5239c-114">Execute the .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="5239c-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="5239c-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="5239c-116">O semplicemente, eseguire lo script seguente, supponendo che i valori predefiniti se utilizzati nell'installazione dei componenti:</span><span class="sxs-lookup"><span data-stu-id="5239c-116">Or simply, execute the following script, assuming default values where used on installation of the components:</span></span>

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "The Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing the Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing the Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a><span data-ttu-id="5239c-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5239c-117">Next steps</span></span>
<span data-ttu-id="5239c-118">Per reinstallare i processi di database elastici, vedere [Installazione del servizio processo di database elastico](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="5239c-118">To re-install Elastic Database jobs, see [Installing the Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="5239c-119">Per ulteriori informazioni sui processi dei database elastici, vedere [Panoramica dei processi di database elastici](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5239c-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->


