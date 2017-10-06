---
title: aaaManage Azure Analysis Services con PowerShell | Documenti Microsoft
description: Gestione di Azure Analysis Services con PowerShell.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: owend
ms.openlocfilehash: bc4250bf77b5a0d86c1049ee57493bcf2a1f0c1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-analysis-services-with-powershell"></a>Gestire Azure Analysis Services con PowerShell

Questo articolo descrive i cmdlet utilizzati tooperform Azure Analysis Services server e database di Gestione attività di PowerShell. 

Attività di gestione di server, ad esempio la creazione o eliminazione di un server, la sospensione o ripresa delle operazioni del server o modifica del livello di servizio hello (livello) utilizzare i cmdlet di gestione risorse di Azure (Azure Resource Manager). Altre attività per la gestione di database, ad esempio aggiunta o rimozione di membri del ruolo, all'elaborazione o il partizionamento di utilizzare i cmdlet inclusi in hello stesso modulo SqlServer come SQL Server Analysis Services.

## <a name="permissions"></a>Autorizzazioni
La maggior parte delle attività di PowerShell è necessario che disporre dei privilegi di amministratore sul server di Analysis Services hello che si sta gestendo. Le attività di PowerShell pianificate sono operazioni automatiche. account di Hello in esecuzione dell'utilità di pianificazione di hello deve disporre dei privilegi di amministratore nel server di Analysis Services hello. 

Per operazioni del server utilizzando i cmdlet di Azure Resource Manager, l'account o hello in esecuzione dell'utilità di pianificazione deve anche appartenere toohello ruolo di proprietario per la risorsa hello in [gestire accesso controllo (RBAC)](../active-directory/role-based-access-control-what-is.md). 

## <a name="server-operations"></a>Operazioni del server 
Cmdlet di Azure Analysis Services sono inclusi in hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) modulo componente. i moduli dei cmdlet tooinstall Azure Resource Manager, vedere [i cmdlet di Azure Resource Manager](/powershell/azure/overview) in PowerShell Gallery hello.

|Cmdlet|Descrizione| 
|------------|-----------------| 
|[Export-AzureAnalysisServicesInstance](/powershell/module/azurerm.analysisservices/export-azureanalysisservicesinstancelog)|Esportazioni log toofile.| 
|[Get-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/get-azurermanalysisservicesserver)|Ottiene i dettagli di un'istanza del server.|  
|[New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver)|Crea un'istanza del server.|
|[Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/remove-azurermanalysisservicesserver)|Rimuove un'istanza del server.|  
|[Suspend-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/suspend-azurermanalysisservicesserver)|Sospende un'istanza del server.| 
|[Resume-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/resume-azurermanalysisservicesserver)|Riprende un'istanza del server.|  
|[Set-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/set-azurermanalysisservicesserver)|Modifica un'istanza del server.|   
|[Test-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/test-azurermanalysisservicesserver)|Test hello esistenza di un'istanza del server.| 

## <a name="database-operations"></a>Operazioni del database

Azure Analysis Services, le operazioni di database di hello stesso [SqlServer](https://www.powershellgallery.com/packages/SqlServer) modulo come SQL Server Analysis Services. Non tutti i cmdlet tuttavia sono supportati in Azure Analysis Services. 

modulo SqlServer Hello fornisce cmdlet di gestione di database specifici dell'attività nonché i cmdlet di uso generale Invoke-ASCmd hello che accetta un protocollo Tabular Model Scripting Language (TMSL) eseguire una query o script. cmdlet seguenti nel modulo SqlServer hello Hello sono supportati per Azure Analysis Services.

  
|Cmdlet|Descrizione|
|------------|-----------------| 
|[Add-RoleMember](https://msdn.microsoft.com/library/hh510167.aspx)|Aggiungere un ruolo del database membro tooa.| 
|[Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet)|Esegue il backup di un database di Analysis Services.|  
|[Remove-RoleMember](https://msdn.microsoft.com/library/hh510173.aspx)|Rimuove un membro da un ruolo del database.|   
|[Invoke-ASCmd](https://msdn.microsoft.com/library/hh479579.aspx)|Esegue uno script TMSL.|
|[Invoke-ProcessASDatabase](https://msdn.microsoft.com/library/mt651773.aspx)|Elabora un database.|  
|[Invoke-ProcessPartition](https://msdn.microsoft.com/library/hh510164.aspx)|Elabora una partizione.| 
|[Invoke-ProcessTable](https://msdn.microsoft.com/library/mt651774.aspx)|Elabora una tabella.|  
|[Merge-Partition](https://msdn.microsoft.com/library/hh479576.aspx)|Unisce una partizione.|  
|[Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet)|Ripristina un database di Analysis Services.| 
  

## <a name="related-information"></a>Informazioni correlate

* [Scaricare il modulo PowerShell di SQL Server](https://docs.microsoft.com/sql/ssms/download-sql-server-ps-module)   
* [Scaricare SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)   
* [Modulo SqlServer in PowerShell Gallery](https://www.powershellgallery.com/packages/SqlServer)    
* [Tabular Model Programming for Compatibility Level 1200](https://msdn.microsoft.com/library/mt712541.aspx) (Programmazione di modelli tabulari per il livello di compatibilità 1200)
