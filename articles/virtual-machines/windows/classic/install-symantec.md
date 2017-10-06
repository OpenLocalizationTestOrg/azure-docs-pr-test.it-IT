---
title: Symantec Endpoint Protection in una macchina virtuale Windows in Azure aaaInstall | Documenti Microsoft
description: Informazioni su come tooinstall e configurare l'estensione di sicurezza di hello Symantec Endpoint Protection in un nuovo o esistente macchina virtuale di Azure creata con modello di distribuzione classica hello.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: iainfou
ms.openlocfilehash: cb6083366185c26c9f43ff94d835cd90725de5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a>Come tooinstall e configurare Symantec Endpoint Protection in una macchina virtuale Windows
> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

In questo articolo illustra come tooinstall e configurare i client di hello Symantec Endpoint Protection in una macchina virtuale esistente (VM) che esegue Windows Server. Questo client completo include servizi come protezione da virus e spyware, firewall e prevenzione delle intrusioni. client Hello viene installato come un'estensione di sicurezza utilizzando hello agente della macchina virtuale.

Se si dispone di una sottoscrizione esistente da Symantec per una soluzione locale, è possibile usarlo tooprotect macchine virtuali di Azure. Se non si è ancora clienti, è possibile iscriversi per una sottoscrizione di valutazione. Per altre informazioni su questa soluzione, vedere la pagina relativa all'uso di [Symantec Endpoint Protection sulla piattaforma Microsoft Azure][Symantec]. Questa pagina include anche collegamenti toolicensing informazioni e istruzioni per l'installazione client hello se si è già un cliente di Symantec.

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a>Installare Symantec Endpoint Protection in una VM esistente
Prima di iniziare, è necessario hello segue:

* modulo di Azure PowerShell Hello, versione 0.8.2 o versione successiva, nel computer in uso. È possibile controllare la versione hello di Azure PowerShell che è stato installato con hello **Get-Module azure | versione formato tabella** comando. Per istruzioni e una versione più recente toohello di collegamento, vedere [come tooInstall e configurare Azure PowerShell][PS]. Accedi con sottoscrizione di Azure tooyour `Add-AzureAccount`.
* Hello hello di agente di macchine Virtuali in esecuzione in macchine virtuali di Azure.

Verificare innanzitutto che hello che agente VM è già installato nella macchina virtuale hello. Specificare nome del servizio cloud hello e nome della macchina virtuale e quindi eseguire hello seguenti comandi in un prompt dei comandi di Azure PowerShell a livello di amministratore. Sostituire tutto il contenuto all'interno di virgolette hello, tra cui hello < e > caratteri.

> [!TIP]
> Se non si conosce il servizio di cloud hello e nomi di macchina virtuale, eseguire **Get-AzureVM** nomi hello toolist per tutte le macchine virtuali nella sottoscrizione corrente.

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

Se hello **write-host** comando Visualizza **True**, hello è installato l'agente di macchine Virtuali. Se viene visualizzato **False**, vedere le istruzioni di hello e toohello un collegamento Scarica nel post di blog di Azure hello [agente VM ed estensioni - parte 2][Agent].

Se è installato l'agente VM hello, eseguire agente di Symantec Endpoint Protection questi comandi tooinstall hello.

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

tooverify che hello Symantec estensione di sicurezza è stato installato e aggiornato:

1. Accedere a macchina virtuale toohello. Per istruzioni, vedere [come tooLog nella macchina virtuale che esegue Windows Server tooa][Logon].
2. Per Windows Server 2008 R2, fare clic su **Start > Symantec Endpoint Protection**. Per Windows Server 2012 o Windows Server 2012 R2, dalla schermata start hello, digitare **Symantec**, quindi fare clic su **Symantec Endpoint Protection**.
3. Da hello **stato** scheda di hello **stato Symantec Endpoint Protection** finestra, applicare gli aggiornamenti o riavviare se necessario.

## <a name="additional-resources"></a>Risorse aggiuntive
[Come tooLog su tooa macchina virtuale che esegue Windows Server][Logon]

[Estensioni e funzionalità delle macchine virtuali di Azure][Ext]

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
