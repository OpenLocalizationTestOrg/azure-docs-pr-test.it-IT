---
title: strumento di processi aaaHow toouninstall database elastico
description: Come toouninstall hello strumento i processi di database elastico
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
ms.openlocfilehash: 3bc1e889d5042bc3eaa9fd9da89816737e0b8df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="20284-103">Disinstallare i componenti dei processi di database elastici</span><span class="sxs-lookup"><span data-stu-id="20284-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="20284-104">**I processi di Database elastici** componenti possono essere disinstallati utilizzando hello portale o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="20284-104">**Elastic Database jobs** components can be uninstalled using either hello Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a><span data-ttu-id="20284-105">Disinstallare i componenti di processi di Database elastico utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="20284-105">Uninstall Elastic Database jobs components using hello Azure portal</span></span>
1. <span data-ttu-id="20284-106">Aprire hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="20284-106">Open hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="20284-107">Passare a sottoscrizione toohello contenente **i processi di Database elastico** componenti, vale a dire hello sottoscrizione in cui Database elastici sono stati installati i componenti di processi.</span><span class="sxs-lookup"><span data-stu-id="20284-107">Navigate toohello subscription that contains **Elastic Database jobs** components, namely hello subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="20284-108">Fare clic su **Sfoglia** e quindi su **Gruppi di risorse**.</span><span class="sxs-lookup"><span data-stu-id="20284-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="20284-109">Gruppo di risorse selezionare hello denominato "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="20284-109">Select hello resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="20284-110">Eliminare il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="20284-110">Delete hello resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="20284-111">Disinstallare i componenti dei processi dei database elastici tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="20284-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="20284-112">Avviare una finestra di comando di Microsoft Azure PowerShell e passare sottodirectory strumenti toohello nella cartella Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x hello: tipo **cd strumenti**.</span><span class="sxs-lookup"><span data-stu-id="20284-112">Launch a Microsoft Azure PowerShell command window and navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="20284-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span><span class="sxs-lookup"><span data-stu-id="20284-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span></span>
2. <span data-ttu-id="20284-114">Eseguire uno script di PowerShell.\UninstallElasticDatabaseJobs.ps1 hello.</span><span class="sxs-lookup"><span data-stu-id="20284-114">Execute hello .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="20284-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="20284-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="20284-116">O semplicemente eseguire hello lo script seguente, supponendo che predefiniti i valori in cui è utilizzato per l'installazione dei componenti di hello:</span><span class="sxs-lookup"><span data-stu-id="20284-116">Or simply, execute hello following script, assuming default values where used on installation of hello components:</span></span>

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "hello Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing hello Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing hello Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a><span data-ttu-id="20284-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="20284-117">Next steps</span></span>
<span data-ttu-id="20284-118">i processi di Database elastico toore-installazione, vedere [installazione del servizio processo di Database elastico hello](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="20284-118">toore-install Elastic Database jobs, see [Installing hello Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="20284-119">Per ulteriori informazioni sui processi dei database elastici, vedere [Panoramica dei processi di database elastici](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="20284-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->


