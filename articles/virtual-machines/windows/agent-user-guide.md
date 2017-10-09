---
title: Panoramica dell'agente di macchine virtuali aaaAzure | Documenti Microsoft
description: Panoramica dell'agente di macchine virtuali di Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: nepeters
ms.openlocfilehash: b03542b9a9c711000fab18ed82e9b17ee5510bbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a>Panoramica dell'agente di macchine virtuali di Azure

Hello agente della macchina virtuale Microsoft Azure (agente AM) è un processo leggero protetto che gestisce l'interazione di VM con hello Controller di infrastruttura di Azure. Hello agente VM svolge un ruolo primario di attivazione e l'esecuzione di estensioni di macchina virtuale di Azure. Le estensioni VM rendono possibile la configurazione post-distribuzione delle macchine virtuali, ad esempio l'installazione e configurazione di software. Estensioni di macchine virtuali abilitano anche le funzionalità di ripristino, ad esempio la reimpostazione delle password amministrativa di hello di una macchina virtuale. Senza hello agente VM di Azure, è Impossibile eseguire le estensioni di macchina virtuale.

Questo documento illustra in dettaglio installazione, il rilevamento e rimozione di hello agente della macchina virtuale Azure.

## <a name="install-hello-vm-agent"></a>Installare l'agente VM hello

### <a name="azure-gallery-image"></a>Immagine della raccolta di Azure

Hello agente VM di Azure viene installato per impostazione predefinita in qualsiasi macchina virtuale Windows distribuito da un'immagine della raccolta di Azure. Quando si distribuisce un'immagine della raccolta di Azure dal portale hello, PowerShell, interfaccia della riga di comando o un modello di gestione risorse di Azure, installare hello che è anche l'agente VM di Azure. 

### <a name="manual-installation"></a>Installazione manuale

agente di macchine Virtuali di Windows Hello può essere installato manualmente utilizzando il pacchetto Windows installer. L'installazione manuale potrebbe essere necessaria quando si crea un'immagine di macchina virtuale personalizzata che verrà distribuita in Azure. toomanually installazione hello agente VM di Windows, scaricare installazione guidata agente di macchine Virtuali di hello da questo percorso [scaricare l'agente di Windows Azure VM](http://go.microsoft.com/fwlink/?LinkID=394789). 

Hello agente della macchina virtuale può essere installato facendo doppio clic sul file di programma di installazione di windows hello. Per un'installazione automatica o automatica dell'agente di macchine Virtuali hello, eseguire hello comando seguente.

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a>Rilevare hello agente della macchina virtuale

### <a name="powershell"></a>PowerShell

modulo di gestione risorse di Azure PowerShell Hello può essere utilizzato tooretrieve informazioni sulle macchine virtuali di Azure. Esecuzione `Get-AzureRmVM` restituisce gran parte delle informazioni tra cui hello provisioning stato hello agente VM di Azure.

```PowerShell
Get-AzureRmVM
```

di seguito Hello è solo un subset di hello `Get-AzureRmVM` output. Hello preavviso `ProvisionVMAgent` annidata proprietà `OSProfile`, questa proprietà può essere utilizzato toodetermine se l'agente VM hello è stato macchina virtuale distribuita toohello.

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

Hello lo script seguente può essere utilizzato tooreturn un breve elenco di nomi di macchina virtuale e lo stato di hello di hello agente della macchina virtuale.

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a>Rilevamento manuale

Quando connesso tooa macchina virtuale Windows Azure, Gestione attività può essere utilizzato tooexamine processi in esecuzione. toocheck per hello agente VM di Azure, aprire Gestione attività > fare clic sulla scheda Dettagli hello e cercare un nome di processo `WindowsAzureGuestAgent.exe`. presenza di Hello di questo processo indica che l'agente VM hello è installato.

## <a name="upgrade-hello-vm-agent"></a>Aggiornare l'agente VM hello

Hello Azure VM agente per Windows viene aggiornato automaticamente. Nuove macchine virtuali sono distribuite tooAzure, ricevono più recenti dell'agente VM hello. Immagini di macchina virtuale personalizzate devono essere aggiornato manualmente tooinclude hello nuovo VM agente.
