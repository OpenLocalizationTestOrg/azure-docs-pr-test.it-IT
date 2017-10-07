---
title: aaaReset hello password o la configurazione di Desktop remoto in una macchina virtuale Windows | Documenti Microsoft
description: Informazioni su come hello tooreset password dell'account o i Servizi Desktop remoto in una macchina virtuale Windows usando il portale di Azure o Azure PowerShell.
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 45c69812-d3e4-48de-a98d-39a0f5675777
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 5258df7196621f0adb50debd08dd248922a966de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a>Come tooreset hello servizio Desktop remoto o la password di account di accesso in una macchina virtuale Windows
Se non è possibile connettersi tooa Windows virtual machine (VM), è possibile reimpostare la password di amministratore locale hello o ripristinare hello Desktop remoto configurazione del servizio. È possibile utilizzare l'estensione di accesso alla VM Azure portal o hello hello in Azure PowerShell tooreset hello. la password. Se si usa PowerShell, assicurarsi di aver hello [modulo di PowerShell più recente installato e configurato](/powershell/azure/overview) e vengono firmati in tooyour sottoscrizione di Azure. È anche possibile [eseguire questi passaggi per macchine virtuali create con modello di distribuzione classica hello](reset-rdp.md).

## <a name="ways-tooreset-configuration-or-credentials"></a>Configurazione tooreset metodi o le credenziali
È possibile reimpostare i Servizi Desktop remoto e le credenziali in modi diversi, in base alle esigenze specifiche:

- [Reimpostare usando hello portale di Azure](#azure-portal)
- [Ripristinare con Azure PowerShell](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a>Portale di Azure
menu del portale hello tooexpand, fare clic sulle barre hello tre nell'angolo superiore sinistro di hello e quindi fare clic su **macchine virtuali**:

![Cercare la macchina virtuale di Azure](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-hello-local-administrator-account-password"></a>**La reimpostazione della password dell'account amministratore locale hello**

Selezionare la macchina virtuale Windows, quindi fare clic su **Supporto e risoluzione dei problemi** > **Reimposta password**. viene visualizzato il pannello di reimpostazione della password Hello:

![Pagina di reimpostazione della password](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

Immettere nome utente hello e una nuova password, quindi fare clic su **aggiornamento**. Provare a riconnettersi tooyour macchina virtuale.

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Reimposta configurazione del servizio Desktop remoto hello**

Selezionare la macchina virtuale Windows, quindi fare clic su **Supporto e risoluzione dei problemi** > **Reimposta password**. Pannello di reimpostazione della password Hello viene visualizzato. 

![Ripristinare la configurazione RDP](./media/reset-rdp/Portal-RM-RDP-Reset.png)

Selezionare **configurazione per la reimpostazione solo** dal menu a discesa hello, quindi fare clic su **aggiornamento**. Provare a riconnettersi tooyour macchina virtuale.


## <a name="vmaccess-extension-and-powershell"></a>Estensione VMAccess e PowerShell
Assicurarsi di avere hello [modulo di PowerShell più recente installato e configurato](/powershell/azure/overview) e vengono firmati nella sottoscrizione di Azure con hello tooyour `Login-AzureRmAccount` cmdlet.

### <a name="reset-hello-local-administrator-account-password"></a>**La reimpostazione della password dell'account amministratore locale hello**
Reimpostazione hello amministratore password o nome utente con hello [Set AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) cmdlet di PowerShell. Creare le credenziali dell'account come segue:

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> Se si digita un nome diverso account amministratore locale corrente hello nella VM, hello estensione VMAccess Rinomina l'account amministratore locale hello, assegna l'account toothat password specificata e genera un evento di disconnessione di Desktop remoto. Se l'account amministratore locale hello la macchina virtuale è disabilitato, viene abilitato hello estensione VMAccess.

dopo gli aggiornamenti di esempio Hello hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup` toohello credenziali specificate.

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Reimposta configurazione del servizio Desktop remoto hello**
Ripristinare accesso remoto tooyour VM con hello [Set AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) cmdlet di PowerShell. esempio Hello Reimposta estensione accesso hello denominata `myVMAccess` nella macchina virtuale denominata hello `myVM` in hello `myResourceGroup` gruppo di risorse:

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> In qualsiasi momento una VM può avere un solo agente di accesso. la proprietà agente tooset hello VM accesso correttamente, hello `-ForceRerun` opzione può essere utilizzata. Quando si utilizza `-ForceRerun`, assicurarsi che toouse hello dello stesso nome per l'agente di accesso alla macchina virtuale hello utilizzato in tutti i comandi precedenti.

Se non è possibile connettersi in remoto macchina virtuale tooyour, vedere più passaggi tootry in [risolvere i problemi di Desktop remoto connessioni tooa basati su Windows macchina virtuale di Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


## <a name="next-steps"></a>Passaggi successivi
Se non risponde hello estensione accesso alle macchine Virtuali di Azure e si desidera password hello tooreset non è possibile, è possibile [reimpostazione hello locale password di Windows non in linea](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Questo metodo è un processo più avanzato e richiede tooconnect hello disco rigido virtuale di hello problematico VM tooanother macchina virtuale. Seguire i passaggi di hello descritte in questo articolo innanzitutto e cercano solo metodo di reimpostazione della password non in linea hello come ultima risorsa.

[Estensioni VM e funzionalità di Azure](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Connettersi tooan macchina virtuale di Azure con RDP o SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[Risolvere i problemi relativi a Desktop remoto connessioni tooa basati su Windows macchina virtuale di Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

