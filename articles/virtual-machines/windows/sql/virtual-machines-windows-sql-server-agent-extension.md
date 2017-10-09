---
title: "attività di gestione aaaAutomate nelle macchine virtuali di SQL (gestione delle risorse) | Documenti Microsoft"
description: "In questo argomento viene descritto come toomanage hello estensione agente SQL Server, che consente di automatizzare attività di amministrazione di SQL Server specifiche. Queste includono il backup automatizzato, l'applicazione automatica delle patch e l'integrazione dell'insieme di credenziali delle chiavi di Azure. In questo argomento Usa la modalità di distribuzione di gestione risorse hello."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: effe4e2f-35b5-490a-b5ef-b06746083da4
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ae917612c4af59f12c0b083440673bdc555e9d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-resource-manager"></a>Automatizzare le attività di gestione in macchine virtuali di Azure con hello estensione di SQL Server Agent (gestione delle risorse)
> [!div class="op_single_selector"]
> * [Gestione risorse](virtual-machines-windows-sql-server-agent-extension.md)
> * [Classico](../classic/sql-server-agent-extension.md)
> 
> 

Hello estensione agente IaaS di SQL Server (SQLIaaSExtension) viene eseguito su macchine virtuali di Azure tooautomate attività di amministrazione. In questo argomento viene fornita una panoramica di servizi di hello supportati dall'estensione hello, nonché istruzioni per l'installazione, stato e rimozione.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

versione classica di hello tooview di questo articolo, vedere [estensione di SQL Server Agent per le macchine virtuali classiche di SQL Server](../classic/sql-server-agent-extension.md).

## <a name="supported-services"></a>Servizi supportati
Estensione di SQL Server IaaS Agent Hello supporta hello seguenti attività di amministrazione:

| Funzionalità di amministrazione | Descrizione |
| --- | --- |
| **Backup automatico di SQL** |Consente di automatizzare hello pianificazione dei backup per tutti i database per l'istanza predefinita di hello di SQL Server in VM hello. Per altre informazioni, vedere [Backup automatico per SQL Server nelle macchine virtuali di Azure (Resource Manager)](virtual-machines-windows-sql-automated-backup.md). |
| **Applicazione automatica delle patch di SQL** |Configura una finestra di manutenzione durante gli aggiornamenti inserisce tooyour macchina virtuale può richiedere, pertanto è possibile evitare gli aggiornamenti durante le ore di punta per il carico di lavoro. Per altre informazioni, vedere [Applicazione automatica delle patch per SQL Server nelle macchine virtuali di Azure (Resource Manager)](virtual-machines-windows-sql-automated-patching.md). |
| **Integrazione di Azure Key Vault** |Abilita è tooautomatically installare e configurare l'insieme di credenziali chiave di Azure nella VM SQL Server. Per altre informazioni, vedere [Configurare l'integrazione dell'insieme di credenziali delle chiavi di Azure per SQL Server in Macchine virtuali di Azure (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md). |

Dopo aver installato e in esecuzione, hello estensione di SQL Server IaaS Agent disponibili queste funzionalità di amministrazione nel Pannello di SQL Server hello di hello macchina virtuale nel portale di Azure hello e tramite Azure PowerShell per le immagini di SQL Server marketplace e tramite Azure PowerShell per le installazioni manuali dell'estensione hello. 

## <a name="prerequisites"></a>Prerequisiti
Requisiti toouse hello estensione agente IaaS di SQL Server nella VM:

**Sistema operativo**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**Versioni di SQL Server**:

* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

**Azure PowerShell**:

* [Scaricare e configurare i comandi di PowerShell di Azure più recenti hello](/powershell/azure/overview)

## <a name="installation"></a>Installazione
Hello estensione agente IaaS di SQL Server viene installato automaticamente quando si esegue il provisioning di una delle immagini della raccolta di macchine virtuali SQL Server hello. Se è necessario estensione hello tooreinstall manualmente su una di queste macchine virtuali di SQL Server, utilizzare hello comando PowerShell seguente:

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

È inoltre possibile tooinstall hello estensione agente IaaS di SQL Server in una macchina virtuale del sistema operativo Windows Server. Questa soluzione è supportata solo se SQL Server è stato installato manualmente sul computer. Quindi installare hello estensione manualmente utilizzando hello stesso **Set AzureVMSqlServerExtension** cmdlet di PowerShell.

> [!NOTE]
> Se si installa manualmente hello estensione agente IaaS di SQL Server in una VM solo sistema operativo Windows Server, è possibile gestire non le impostazioni di configurazione di SQL Server hello tramite hello portale di Azure. In questo scenario è necessario eseguire tutte le modifiche con PowerShell.

## <a name="status"></a>Stato
Tooverify un modo che sia installato l'estensione hello è lo stato dell'agente hello tooview in hello portale di Azure. Selezionare **tutte le impostazioni** in hello pannello macchine virtuali e quindi fare clic su **estensioni**. Dovrebbe essere hello **SQLIaaSExtension** estensione elencati.

![Estensione Agente IaaS di SQL Server nel portale di Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

È inoltre possibile utilizzare hello **Get AzureVMSqlServerExtension** cmdlet Powershell di Azure.

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

comando precedente Hello conferma agente hello viene installato e fornisce informazioni sullo stato generale. È anche possibile ottenere informazioni specifiche sullo stato Backup automatizzato e l'applicazione di patch con hello i comandi seguenti.

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a>Rimozione
Nel portale di Azure hello, è possibile disinstallare l'estensione hello facendo clic sui puntini di sospensione hello in hello **estensioni** pannello delle proprietà di macchina virtuale. Fare quindi clic su **Elimina**.

![Disinstallare hello estensione agente IaaS di SQL Server nel portale di Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

È inoltre possibile utilizzare hello **Remove AzureRmVMSqlServerExtension** cmdlet di Powershell.

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a>Passaggi successivi
Iniziare a utilizzare uno dei servizi di hello supportati dall'estensione hello. Per ulteriori informazioni, vedere gli argomenti di hello elencati in hello [servizi supportati](#supported-services) sezione di questo articolo.

Per altre informazioni sull'esecuzione di SQL Server in Macchine virtuali di Azure, vedere [Panoramica di SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md).

