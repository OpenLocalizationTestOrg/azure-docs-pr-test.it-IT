---
title: aaaAutomated patch per macchine virtuali di SQL Server (versione classica) | Documenti Microsoft
description: "Vengono illustrate funzionalità di patch automatizzate hello per SQL Server le macchine virtuali in esecuzione in Azure utilizzando la modalità di distribuzione classica hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 737b2f65-08b9-4f54-b867-e987730265a8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 2ef06b95705fc457605d6eb2fbc0afd490321843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a>Applicazione automatica delle patch per SQL Server in macchine virtuali di Azure (distribuzione classica)
> [!div class="op_single_selector"]
> * [Gestione risorse](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [Classico](../classic/sql-automated-patching.md)
> 
> 

L'applicazione automatica delle patch stabilisce un periodo di manutenzione per una macchina virtuale di Azure su cui è in esecuzione SQL Server. Gli aggiornamenti automatici possono essere installati solo durante questo periodo di manutenzione. Per SQL Server, in questo modo che gli aggiornamenti del sistema e tutti i riavvii associati in fase di possibili migliore hello per database hello. L'applicazione di patch automatizzati dipende hello [estensione di SQL Server IaaS Agent](../classic/sql-server-agent-extension.md).

> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. tooview hello Gestione risorse di questo articolo, vedere [applicazione automatica di patch per SQL Server in Gestione risorse di macchine virtuali Azure](../sql/virtual-machines-windows-sql-automated-patching.md).

## <a name="prerequisites"></a>Prerequisiti
toouse automatica di patch, prendere in considerazione hello seguenti prerequisiti:

**Sistema operativo**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**Versione di SQL Server**:

* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

**Azure PowerShell**:

* [Installare i comandi di PowerShell di Azure più recenti hello](/powershell/azure/overview).

**Estensione di SQL Server IaaS**:

* [Installare l'estensione di SQL Server IaaS hello](../classic/sql-server-agent-extension.md).

## <a name="settings"></a>Impostazioni
Hello nella tabella seguente descrive le opzioni di hello che possono essere configurate per l'applicazione automatica di patch. Per le macchine virtuali classiche, è necessario utilizzare PowerShell tooconfigure queste impostazioni.

| Impostazione | Valori possibili | Descrizione |
| --- | --- | --- |
| **Applicazione automatica delle patch** |Enable/Disable (disabilitato) |Abilita o disabilita l'applicazione automatica delle patch per una macchina virtuale di Azure. |
| **Pianificazione della manutenzione** |Ogni giorno, lunedì, martedì, mercoledì, giovedì, venerdì, sabato, domenica |pianificazione di Hello per scaricare e installare gli aggiornamenti di Microsoft Windows e SQL Server per la macchina virtuale. |
| **Ora di inizio manutenzione** |0-24 |Hello avvio locale ora tooupdate hello macchina virtuale. |
| **Durata dell'intervallo di manutenzione** |30-180 |numero di Hello di minuti consentiti toocomplete hello download e installazione degli aggiornamenti. |
| **Categoria delle patch** |Importante |categoria di Hello di toodownload gli aggiornamenti e installare. |

## <a name="configuration-with-powershell"></a>Configurazione con PowerShell
Nell'esempio seguente di hello, PowerShell è usato tooconfigure applicazione automatica di patch in una VM esistente di SQL Server. Hello **New-AzureVMSqlServerAutoPatchingConfig** comando Configura una nuova finestra di manutenzione per gli aggiornamenti automatici.

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

In base a questo esempio, hello nella tabella seguente vengono descritti hello pratiche effetti sulla destinazione hello macchina virtuale di Azure:

| . | Effetto |
| --- | --- |
| **DayOfWeek** |Patch installate ogni giovedì. |
| **MaintenanceWindowStartingHour** |Inizio degli aggiornamenti alle ore 11:00. |
| **MaintenanceWindowsDuration** |Le patch devono essere installate entro 120 minuti. In base a ora di inizio hello, devono essere completate entro le 13.00. |
| **PatchCategory** |Hello solo possibile impostazione per questo parametro è "Importante". |

Potrebbe richiedere diversi minuti tooinstall e configurare hello agente IaaS di SQL Server.

toodisable patch automatizzate, esecuzione hello stesso script senza hello - Enable parametro toohello New-AzureVMSqlServerAutoPatchingConfig. Come con l'installazione, può richiedere diversi minuti toodisable applicazione automatica di patch.

## <a name="next-steps"></a>Passaggi successivi
Per informazioni sulle altre attività di automazione disponibili, vedere [Estensione Agente IaaS di SQL Server](../classic/sql-server-agent-extension.md).

Per altre informazioni sull'esecuzione di SQL Server nelle VM di Azure, vedere [Panoramica di SQL Server nelle macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

