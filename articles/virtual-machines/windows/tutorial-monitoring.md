---
title: aaaAzure monitoraggio e macchine virtuali di Windows | Documenti Microsoft
description: 'Esercitazione: monitorare una macchina virtuale Windows con Azure PowerShell'
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/04/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 191dc5a30d41c25a9e38f8ec2a32efdc05e03015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a>Monitorare una macchina virtuale Windows con Azure PowerShell

Monitoraggio Azure utilizza avvio toocollect gli agenti e i dati sulle prestazioni da macchine virtuali di Azure, memorizzare i dati nell'archiviazione di Azure e renderlo accessibile tramite il portale, il modulo di Azure PowerShell hello e hello CLI di Azure. In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Abilitare la diagnostica di avvio in una macchina virtuale
> * Visualizzare la diagnostica di avvio
> * Visualizzare le metriche host della macchina virtuale
> * Installare l'estensione diagnostica hello
> * Visualizzare le metriche della macchina virtuale
> * Creare un avviso
> * Configurare il monitoraggio avanzato

Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo. Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind. Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).

esempio di hello toocomplete in questa esercitazione, è necessario disporre di una macchina virtuale esistente. Se necessario, questo [script di esempio](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) può crearne una appositamente. Quando si utilizza l'esercitazione di hello, sostituire il gruppo di risorse hello, nome della macchina virtuale e posizione dove necessario.

## <a name="view-boot-diagnostics"></a>Visualizzare la diagnostica di avvio

Come avviare macchine virtuali di Windows, agente di diagnostica di avvio di hello acquisisce l'output dello schermo che può essere utilizzato per la risoluzione dei problemi relativi a scopo. Questa funzionalità è abilitata per impostazione predefinita. Hello acquisiti schermata catture vengono archiviati in un account di archiviazione di Azure, viene anche creato per impostazione predefinita. 

È possibile ottenere dati di diagnostica di avvio hello con hello [Get AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) comando. Nel seguente esempio di hello, la diagnostica di avvio è radice toohello scaricato hello * c:\* unità. 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a>Visualizzare le metriche host

Una macchina virtuale Windows ha una macchina virtuale host dedicata in Azure con cui interagisce. Le metriche vengono automaticamente raccolte per hello Host e possono essere visualizzate nel portale di Azure hello.

1. Nel portale di Azure hello, fare clic su **gruppi di risorse**selezionare **myResourceGroup**, quindi selezionare **myVM** nell'elenco di risorse hello.
2. Fare clic su **metriche** hello pannello VM e quindi selezionare una delle metriche Host hello in **le metriche disponibili** toosee delle prestazioni di hello Host VM.

    ![Visualizzare le metriche host](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a>Installare l'estensione di diagnostica

le metriche di base host Hello sono disponibili, ma toosee più granulare e metriche specifiche di macchina virtuale, si tooneed tooinstall hello Azure estensione diagnostica per hello VM. Hello estensione diagnostica di Azure consente un monitoraggio aggiuntivo e toobe di dati di diagnostica recuperati hello macchina virtuale. È possibile visualizzare queste misurazioni delle prestazioni e creare avvisi basati sulle modalità di funzionamento hello macchina virtuale. estensione di diagnostica Hello viene installata tramite il portale di Azure hello come segue:

1. Nel portale di Azure hello, fare clic su **gruppi di risorse**selezionare **myResourceGroup**, quindi selezionare **myVM** nell'elenco di risorse hello.
2. Fare clic su **Impostazioni di diagnostica**. elenco di Hello mostra che *diagnostica di avvio* è già stata abilitata dalla sezione precedente hello. Fare clic sulla casella di controllo hello *metriche base*.
3. Fare clic su hello **abilitare il monitoraggio a livello di guest** pulsante.

    ![Visualizzare le metriche di diagnostica](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a>Visualizzare le metriche della macchina virtuale

È possibile visualizzare le metriche VM hello in hello allo stesso modo visualizzato metriche di hello host macchina virtuale:

1. Nel portale di Azure hello, fare clic su **gruppi di risorse**selezionare **myResourceGroup**, quindi selezionare **myVM** nell'elenco di risorse hello.
2. toosee come hello macchina virtuale viene eseguita, fare clic su **metriche** hello pannello VM e quindi selezionare una delle metriche di diagnostica hello in **le metriche disponibili**.

    ![Visualizzare le metriche della macchina virtuale](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a>Creare avvisi

È possibile creare avvisi basati sulle metriche di prestazioni specifiche. Gli avvisi possono essere ad esempio toonotify utilizzato per l'utilizzo medio della CPU supera una determinata soglia o spazio su disco disponibile scende di sotto di una certa quantità. Gli avvisi vengono visualizzati nel portale di Azure hello o possono essere inviati tramite posta elettronica. È inoltre possibile attivare i runbook di automazione di Azure o Azure logica App in tooalerts risposta in corso la generazione.

Hello seguente viene creato un avviso per l'utilizzo medio della CPU.

1. Nel portale di Azure hello, fare clic su **gruppi di risorse**selezionare **myResourceGroup**, quindi selezionare **myVM** nell'elenco di risorse hello.
2. Fare clic su **regole di avviso** nel pannello VM hello, quindi fare clic su **Aggiungi avviso metrica** in alto di hello del pannello avvisi hello.
4. Inserire un **Nome** per l'avviso, ad esempio *myAlertRule*
5. tootrigger un avviso quando la percentuale della CPU supera 1.0 per cinque minuti, lasciare hello tutti gli altri valori predefiniti selezionati.
6. Facoltativamente, selezionare la casella di hello per *i proprietari, collaboratori e lettori di posta elettronica* toosend notifica di posta elettronica. azione predefinita Hello è toopresent una notifica nel portale di hello.
7. Fare clic su hello **OK** pulsante.

## <a name="advanced-monitoring"></a>Monitoraggio avanzato 

È possibile eseguire un monitoraggio più approfondito della macchina virtuale tramite [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview). Se non è già stato fatto, è possibile iscriversi per avere una [versione di prova gratuita](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) di Operations Management Suite.

Quando si dispone di accesso toohello OMS portale, è possibile trovare l'identificatore di chiave e dell'area di lavoro dell'area di lavoro hello nel pannello impostazioni hello. Hello utilizzare [Set AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) specifica tootooadd hello OMS estensione toohello macchina virtuale. Aggiornamento hello valori delle variabili in hello seguito esempio tooreflect è chiave dell'area di lavoro OMS e area di lavoro ID.  

```powershell
$omsId = "<Replace with your OMS Id>"
$omsKey = "<Replace with your OMS key>"

Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
  -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
  -VMName myVM `
  -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
  -ExtensionType "MicrosoftMonitoringAgent" `
  -TypeHandlerVersion 1.0 `
  -Settings @{"workspaceId" = $omsId} `
  -ProtectedSettings @{"workspaceKey" = $omsKey} `
  -Location eastus
```

Dopo alcuni minuti, dovrebbe essere hello nuova macchina virtuale nell'area di lavoro OMS hello. 

![Pannello OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione le macchine virtuali sono state configurate ed esaminate con il Centro sicurezza di Azure. Si è appreso come:

> [!div class="checklist"]
> * Crea rete virtuale
> * Creare un gruppo di risorse e una macchina virtuale 
> * Abilitare la diagnostica di avvio su hello VM
> * Visualizzare la diagnostica di avvio
> * Visualizzare le metriche host
> * Installare l'estensione diagnostica hello
> * Visualizzare le metriche della macchina virtuale
> * Creare un avviso
> * Configurare il monitoraggio avanzato

Spostare toohello toolearn esercitazione successiva sul Centro protezione di Azure.

> [!div class="nextstepaction"]
> [Gestire la sicurezza delle VM](./tutorial-azure-security.md)