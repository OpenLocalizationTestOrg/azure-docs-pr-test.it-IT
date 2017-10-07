---
title: Trend Micro Deep Security in una macchina virtuale aaaInstall | Documenti Microsoft
description: Questo articolo viene descritto come tooinstall e configurare Trend Micro security in una macchina virtuale creata con modello di distribuzione classica hello in Azure.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a>Come tooinstall e configurare Trend Micro Deep Security come servizio in una macchina virtuale Windows
> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

In questo articolo illustra come tooinstall e configurare Trend Micro Deep Security come servizio in una nuova o esistente macchina virtuale (VM) che esegue Windows Server. Deep Security as a Service offre protezione antimalware, un firewall, un sistema di prevenzione delle intrusioni e il monitoraggio dell'integrità.

Hello client viene installato come un'estensione di sicurezza tramite hello agente della macchina virtuale. In una nuova macchina virtuale, installare hello Deep Security Agent, come hello che agente della macchina virtuale viene creato automaticamente da hello portale di Azure.

Una macchina virtuale esistente creata tramite portale classico hello, hello CLI di Azure o PowerShell potrebbe non disporre di un agente di macchine Virtuali. Per una macchina virtuale esistente che non dispone di hello agente della macchina virtuale, è necessario toodownload ed è necessario prima installarlo. In questo articolo vengono descritte entrambe le situazioni.

Se si dispone di una sottoscrizione corrente da Trend Micro per una soluzione locale, è possibile utilizzare toohelp proteggere macchine virtuali di Azure. Se non si è ancora clienti, è possibile iscriversi per una sottoscrizione di valutazione. Per ulteriori informazioni su questa soluzione, vedere hello Trend Micro post di blog [Microsoft Azure VM agente di estensione per Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a>Installare hello Deep Security Agent in una nuova macchina virtuale

Hello [portale di Azure](http://portal.azure.com) consente di installare l'estensione di sicurezza Trend Micro hello quando si utilizza un'immagine da hello **Marketplace** macchina virtuale di toocreate hello. Se si sta creando una singola macchina virtuale, l'uso del portale di hello è una protezione tooadd facilmente da Trend Micro.

Con una voce da hello **Marketplace** apre una procedura guidata che consente di imposta la macchina virtuale hello. Utilizzare hello **impostazioni** blade, pannello di terzo hello della procedura guidata hello, hello tooinstall estensione di sicurezza Trend Micro.  Per istruzioni generali, vedere [creare una macchina virtuale Windows in esecuzione in Azure portal hello](tutorial.md).

Quando si ottengono toohello **impostazioni** pannello della procedura guidata hello hello i passaggi seguenti:

1. Fare clic su **estensioni**, quindi fare clic su **aggiungere estensione** nel riquadro successivo di hello.

   ![Iniziare ad aggiungere l'estensione hello][1]

2. Selezionare **Deep Security Agent** in hello **nuova risorsa** riquadro. Nel riquadro di hello Deep Security Agent, fare clic su **crea**.

   ![Identificare Deep Security Agent][2]

3. Immettere hello **identificatore del Tenant** e **Password di attivazione Tenant** per estensione hello. Se lo si desidera, è possibile immettere un **identificatore dei criteri di sicurezza**. Quindi, fare clic su **OK** client hello tooadd.

   ![Immettere i dettagli relativi all'estensione][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a>Installare hello Deep Security Agent in una macchina virtuale esistente
agente di hello tooinstall in una macchina virtuale esistente, è necessario hello seguenti elementi:

* modulo di Azure PowerShell Hello, versione 0.8.2 o successive, installato nel computer locale. È possibile controllare la versione hello di Azure PowerShell che è stato installato tramite hello **Get-Module azure | versione formato tabella** comando. Per istruzioni e una versione più recente toohello di collegamento, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview). Accedi con sottoscrizione di Azure tooyour `Add-AzureAccount`.
* Agente VM installato nella macchina virtuale di destinazione hello Hello.

Verificare innanzitutto che hello che agente VM è già installato. Specificare nome del servizio cloud hello e nome della macchina virtuale e quindi eseguire hello seguenti comandi in un prompt dei comandi di Azure PowerShell a livello di amministratore. Sostituire tutto il contenuto all'interno di virgolette hello, tra cui hello < e > caratteri.

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

Se non si conosce il nome di macchina virtuale e servizio cloud hello, eseguire **Get-AzureVM** toodisplay che le informazioni su tutti hello macchine virtuali nella sottoscrizione corrente.

Se hello **write-host** comando restituisce **True**, hello è installato l'agente di macchine Virtuali. Se restituisce **False**, vedere le istruzioni di hello e toohello un collegamento Scarica nel post di blog di Azure hello [agente VM ed estensioni - parte 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).

Se è installato l'agente VM hello, eseguire questi comandi.

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a>Passaggi successivi
Sono necessari alcuni minuti per toostart agente hello in esecuzione quando viene installato. Successivamente, è necessario tooactivate Deep Security nella macchina virtuale hello in modo da poter essere gestito da un gestore protezione completa. Vedere i seguenti articoli per le istruzioni aggiuntive hello:

* Articolo di Trend Micro sulla [sicurezza cloud immediata per Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)
* Oggetto [script Windows PowerShell di esempio](http://go.microsoft.com/fwlink/?LinkId=404100) macchina virtuale di hello tooconfigure
* [Istruzioni](http://go.microsoft.com/fwlink/?LinkId=404099) per esempio hello

## <a name="additional-resources"></a>Risorse aggiuntive
[Come toolog nella macchina virtuale tooa che esegue Windows Server]

[Estensioni VM e funzionalità di Azure]

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[Come toolog nella macchina virtuale tooa che esegue Windows Server]:connect-logon.md
[Estensioni VM e funzionalità di Azure]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
