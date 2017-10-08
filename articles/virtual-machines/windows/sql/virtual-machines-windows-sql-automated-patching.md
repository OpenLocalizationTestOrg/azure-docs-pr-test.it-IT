---
title: aaaAutomated patch per macchine virtuali di SQL Server (gestione delle risorse) | Documenti Microsoft
description: "Vengono illustrate funzionalità di patch automatizzate hello per SQL Server le macchine virtuali in esecuzione in Azure tramite Gestione risorse."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 58232e92-318f-456b-8f0a-2201a541e08d
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 8bb8d0fb265e69d7bbf1fa047f5ceef02e7c56fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a>Applicazione automatica delle patch per SQL Server nelle macchine virtuali di Azure (Resource Manager)
> [!div class="op_single_selector"]
> * [Gestione risorse](virtual-machines-windows-sql-automated-patching.md)
> * [Classico](../classic/sql-automated-patching.md)
> 
> 

L'applicazione automatica delle patch stabilisce un periodo di manutenzione per una macchina virtuale di Azure su cui è in esecuzione SQL Server. Gli aggiornamenti automatici possono essere installati solo durante questo periodo di manutenzione. Per SQL Server, questo rescriction garantisce che gli aggiornamenti del sistema e tutti i riavvii associati in fase di possibili migliore hello per database hello. L'applicazione di patch automatizzati dipende hello [estensione di SQL Server IaaS Agent](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

versione classica di hello tooview di questo articolo, vedere [applicazione automatica di patch per SQL Server in macchine virtuali di Azure classico](../classic/sql-automated-patching.md).

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

* [Installare i comandi di PowerShell di Azure più recenti hello](/powershell/azure/overview) se si prevede di tooconfigure applicazione automatica di patch con PowerShell.

> [!NOTE]
> L'applicazione di patch automatizzato si basa su hello estensione agente IaaS di SQL Server. Per impostazione predefinita, le attuali immagini della raccolta di macchine virtuali di SQL aggiungono questa estensione. Per altre informazioni, vedere [Estensione Agente IaaS di SQL Server](virtual-machines-windows-sql-server-agent-extension.md).
> 
> 

## <a name="settings"></a>Impostazioni
Hello nella tabella seguente descrive le opzioni di hello che possono essere configurate per l'applicazione automatica di patch. passaggi di configurazione effettivi Hello variano a seconda che si utilizzi hello portale di Azure o i comandi di Windows PowerShell per Azure.

| Impostazione | Valori possibili | Descrizione |
| --- | --- | --- |
| **Applicazione automatica delle patch** |Enable/Disable (disabilitato) |Abilita o disabilita l'applicazione automatica delle patch per una macchina virtuale di Azure. |
| **Pianificazione della manutenzione** |Ogni giorno, lunedì, martedì, mercoledì, giovedì, venerdì, sabato, domenica |pianificazione di Hello per scaricare e installare gli aggiornamenti di Microsoft Windows e SQL Server per la macchina virtuale. |
| **Ora di inizio manutenzione** |0-24 |Hello avvio locale ora tooupdate hello macchina virtuale. |
| **Durata dell'intervallo di manutenzione** |30-180 |numero di Hello di minuti consentiti toocomplete hello download e installazione degli aggiornamenti. |
| **Categoria delle patch** |Importante |categoria di Hello di toodownload gli aggiornamenti e installare. |

## <a name="configuration-in-hello-portal"></a>Configurazione di hello portale
È possibile utilizzare hello tooconfigure portale Azure patch automatizzate durante il provisioning o per le macchine virtuali esistenti.

### <a name="new-vms"></a>Nuove VM
Hello utilizzare tooconfigure portale Azure quando si crea una nuova macchina virtuale di SQL Server nel modello di distribuzione di gestione risorse di hello patch automatizzate.

In hello **impostazioni di SQL Server** pannello seleziona **l'applicazione automatica di patch**. schermata del portale di Azure seguente Hello Mostra hello **patch automatizzate SQL** blade.

![Applicazione automatizzata di patch SQL nel portale di Azure](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

Per contesto, vedere l'argomento completo hello in [provisioning di una macchina virtuale di SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>VM esistenti
Per le macchine virtuali SQL Server esistenti, selezionare la macchina virtuale SQL Server. Selezionare quindi hello **configurazione di SQL Server** sezione di hello **impostazioni** blade.

![Applicazione automatizzata di patch SQL per le VM esistenti](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

In hello **configurazione di SQL Server** pannello, fare clic su hello **modifica** pulsante hello automatizzata sezione applicazione di patch.

![Configurare l'applicazione automatizzata di patch SQL per le VM esistenti](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

Al termine, fare clic su hello **OK** pulsante nella parte inferiore di hello di hello **configurazione di SQL Server** pannello toosave le modifiche.

Se si sta abilitando patch automatizzate per hello prima volta, Azure Configura hello agente IaaS di SQL Server in background hello. Durante questo periodo, hello portale di Azure potrebbe non visualizzare che viene configurato l'applicazione automatica di patch. Attendere alcuni minuti per hello agente toobe installato, configurato. Dopo tale hello Azure portal riflettono le nuove impostazioni hello.

> [!NOTE]
> È inoltre possibile configurare l'applicazione automatica delle patch mediante un modello. Per altre informazioni, vedere l'articolo relativo al [modello di avvio rapido di Azure per l'applicazione automatica delle patch](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).
> 
> 

## <a name="configuration-with-powershell"></a>Configurazione con PowerShell
Dopo il provisioning VM SQL, utilizzare PowerShell tooconfigure applicazione automatica di patch.

Nell'esempio seguente di hello, PowerShell è usato tooconfigure applicazione automatica di patch in una VM esistente di SQL Server. Hello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** comando Configura una nuova finestra di manutenzione per gli aggiornamenti automatici.

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

In base a questo esempio, hello nella tabella seguente vengono descritti hello pratiche effetti sulla destinazione hello macchina virtuale di Azure:

| . | Effetto |
| --- | --- |
| **DayOfWeek** |Patch installate ogni giovedì. |
| **MaintenanceWindowStartingHour** |Inizio degli aggiornamenti alle ore 11:00. |
| **MaintenanceWindowsDuration** |Le patch devono essere installate entro 120 minuti. In base a ora di inizio hello, devono essere completate entro le 13.00. |
| **PatchCategory** |Hello unica impostazione possibile per questo parametro è **importante**. |

Potrebbe richiedere diversi minuti tooinstall e configurare hello agente IaaS di SQL Server.

toodisable patch automatizzate, esecuzione hello stesso script senza hello **-abilitare** parametro toohello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**. assenza di hello Hello **-abilitare** funzionalità di parametro segnali hello comando toodisable hello.

## <a name="next-steps"></a>Passaggi successivi
Per informazioni sulle altre attività di automazione disponibili, vedere [Estensione Agente IaaS di SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

Per altre informazioni sull'esecuzione di SQL Server nelle VM di Azure, vedere [Panoramica di SQL Server nelle macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md).

