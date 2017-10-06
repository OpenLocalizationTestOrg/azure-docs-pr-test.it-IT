---
title: "attività di gestione aaaAutomate nelle macchine virtuali di SQL (versione classica) | Documenti Microsoft"
description: "In questo argomento viene descritto come toomanage hello estensione agente SQL Server, che consente di automatizzare attività di amministrazione di SQL Server specifiche. Queste includono il backup automatizzato, l'applicazione automatica delle patch e l'integrazione dell'insieme di credenziali delle chiavi di Azure. In questo argomento Usa la modalità di distribuzione classica hello."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1dc011e0526845701eaf0c365007938f9ee32ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a>Automatizzare le attività di gestione in macchine virtuali di Azure con hello estensione di SQL Server Agent (versione classica)
> [!div class="op_single_selector"]
> * [Gestione risorse](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [Classico](../classic/sql-server-agent-extension.md)
> 
>
 
Hello estensione agente IaaS di SQL Server (SQLIaaSAgent) viene eseguito su macchine virtuali di Azure tooautomate attività di amministrazione. In questo argomento viene fornita una panoramica di servizi di hello supportati dall'estensione hello, nonché istruzioni per l'installazione, stato e rimozione.

> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. tooview hello Gestione risorse di questo articolo, vedere [estensione Gestione risorse per SQL Server le macchine virtuali di SQL Server Agent](../sql/virtual-machines-windows-sql-server-agent-extension.md).

## <a name="supported-services"></a>Servizi supportati
Estensione di SQL Server IaaS Agent Hello supporta hello seguenti attività di amministrazione:

| Funzionalità di amministrazione | Descrizione |
| --- | --- |
| **Backup automatico di SQL** |Consente di automatizzare hello pianificazione dei backup per tutti i database per l'istanza predefinita di hello di SQL Server in VM hello. Per altre informazioni, vedere [Backup automatico per SQL Server in macchine virtuali di Azure (distribuzione classica)](../classic/sql-automated-backup.md). |
| **Applicazione automatica delle patch di SQL** |Configura una finestra di manutenzione durante gli aggiornamenti inserisce tooyour macchina virtuale può richiedere, pertanto è possibile evitare gli aggiornamenti durante le ore di punta per il carico di lavoro. Per altre informazioni, vedere [Applicazione automatica delle patch per SQL Server in macchine virtuali di Azure (distribuzione classica)](../classic/sql-automated-patching.md). |
| **Integrazione di Azure Key Vault** |Abilita è tooautomatically installare e configurare l'insieme di credenziali chiave di Azure nella VM SQL Server. Per altre informazioni, vedere [Configurare l'integrazione di Azure Key Vault per SQL Server in macchine virtuali di Azure (distribuzione classica)](../classic/ps-sql-keyvault.md). |

## <a name="prerequisites"></a>Prerequisiti
Requisiti toouse hello estensione agente IaaS di SQL Server nella VM:

### <a name="operating-system"></a>Sistema operativo:
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

### <a name="sql-server-versions"></a>Versioni di SQL Server:
* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

### <a name="azure-powershell"></a>Azure PowerShell:
[Scaricare e configurare i comandi di PowerShell di Azure più recenti hello](/powershell/azure/overview).

Avviare Windows PowerShell e connetterla tooyour sottoscrizione di Azure con hello **Add-AzureAccount** comando.

    Add-AzureAccount

Se si dispone di più sottoscrizioni, usare **Select-AzureSubscription** sottoscrizione hello tooselect che contiene la destinazione VM classico.

    Select-AzureSubscription -SubscriptionName <subscriptionname>

A questo punto, è possibile ottenere un elenco di macchine virtuali classiche hello e i relativi nomi di servizio associato con hello **Get-AzureVM** comando.

    Get-AzureVM

## <a name="installation"></a>Installazione
Per le macchine virtuali classiche, è necessario usare PowerShell tooinstall hello estensione agente IaaS di SQL Server e configurare i servizi associati. Hello utilizzare **Set AzureVMSqlServerExtension** estensione hello tooinstall cmdlet di PowerShell. Ad esempio, hello comando seguente installa estensione hello in una VM di Windows Server (versione classica) e gli assegna il "SQLIaaSExtension".

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

Se si aggiorna toohello la versione più recente di hello estensione agente IaaS di SQL Server, è necessario riavviare la macchina virtuale dopo l'aggiornamento dell'estensione hello.

> [!NOTE]
> Macchine virtuali classiche non è un'opzione tooinstall e configurare hello estensione SQL IaaS Agent tramite il portale di hello.
> 
> 

## <a name="status"></a>Stato
Tooverify un modo che sia installato l'estensione hello è lo stato dell'agente hello tooview in hello portale di Azure. Selezionare una macchina virtuale elencata nel pannello macchine virtuali hello e quindi fare clic su **estensioni**. Dovrebbe essere hello **SQLIaaSAgent** estensione elencati.

![Estensione Agente IaaS di SQL Server nel portale di Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

È inoltre possibile utilizzare hello **Get AzureVMSqlServerExtension** cmdlet Powershell di Azure.

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a>Rimozione
Nel portale di Azure hello, è possibile disinstallare l'estensione hello facendo clic sui puntini di sospensione hello in hello **estensioni** pannello delle proprietà di macchina virtuale. Fare clic su **Disinstalla**.

![Disinstallare hello estensione agente IaaS di SQL Server nel portale di Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

È inoltre possibile utilizzare hello **Remove AzureVMSqlServerExtension** cmdlet di Powershell.

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a>Passaggi successivi
Iniziare a utilizzare uno dei servizi di hello supportati dall'estensione hello. Per ulteriori informazioni, vedere gli argomenti di hello elencati in hello [servizi supportati](#supported-services) sezione di questo articolo.

Per altre informazioni sull'esecuzione di SQL Server in Macchine virtuali di Azure, vedere [Panoramica di SQL Server in Macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

