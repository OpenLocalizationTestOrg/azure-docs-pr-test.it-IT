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
# <a name="uninstall-elastic-database-jobs-components"></a>Disinstallare i componenti dei processi di database elastici
**I processi di Database elastici** componenti possono essere disinstallati utilizzando hello portale o PowerShell.

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a>Disinstallare i componenti di processi di Database elastico utilizzando hello portale di Azure
1. Aprire hello [portale di Azure](https://portal.azure.com/).
2. Passare a sottoscrizione toohello contenente **i processi di Database elastico** componenti, vale a dire hello sottoscrizione in cui Database elastici sono stati installati i componenti di processi.
3. Fare clic su **Sfoglia** e quindi su **Gruppi di risorse**.
4. Gruppo di risorse selezionare hello denominato "__ElasticDatabaseJob".
5. Eliminare il gruppo di risorse hello.

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a>Disinstallare i componenti dei processi dei database elastici tramite PowerShell
1. Avviare una finestra di comando di Microsoft Azure PowerShell e passare sottodirectory strumenti toohello nella cartella Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x hello: tipo **cd strumenti**.
   
     PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools
2. Eseguire uno script di PowerShell.\UninstallElasticDatabaseJobs.ps1 hello.
   
     PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1

O semplicemente eseguire hello lo script seguente, supponendo che predefiniti i valori in cui è utilizzato per l'installazione dei componenti di hello:

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

## <a name="next-steps"></a>Passaggi successivi
i processi di Database elastico toore-installazione, vedere [installazione del servizio processo di Database elastico hello](sql-database-elastic-jobs-service-installation.md)

Per ulteriori informazioni sui processi dei database elastici, vedere [Panoramica dei processi di database elastici](sql-database-elastic-jobs-overview.md).

<!--Image references-->


