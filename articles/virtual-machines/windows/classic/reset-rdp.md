---
title: aaaReset hello password o la configurazione di Desktop remoto in una macchina virtuale Windows in Azure | Documenti Microsoft
description: Informazioni su come password dell'account o i Servizi Desktop remoto in una macchina virtuale Windows creata mediante hello Classic distribuzione modello tooreset hello portale di Azure o Azure PowerShell.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 1721a91fc6c89b46df74e76dfcf918b1c4c77a4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a>Come servizio Desktop remoto di hello tooreset o la password di account di accesso in una macchina virtuale Windows creata mediante modello di distribuzione classica hello
> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. È anche possibile [eseguire questi passaggi per macchine virtuali create con modello di distribuzione di gestione risorse di hello](../reset-rdp.md).

Se non è possibile connettersi tooa Windows virtual machine (VM), è possibile reimpostare la password di amministratore locale hello o ripristinare hello Desktop remoto configurazione del servizio. È possibile utilizzare l'estensione di accesso alla VM Azure portal o hello hello in Azure PowerShell tooreset hello. la password.

## <a name="ways-tooreset-configuration-or-credentials"></a>Configurazione tooreset metodi o le credenziali
È possibile reimpostare i Servizi Desktop remoto e le credenziali in modi diversi, in base alle esigenze specifiche:

- [Reimpostare usando hello portale di Azure](#azure-portal)
- [Ripristinare con Azure PowerShell](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a>Portale di Azure
È possibile utilizzare hello [portale di Azure](https://portal.azure.com) tooreset hello servizio Desktop remoto. menu del portale hello tooexpand, fare clic sulle barre hello tre nell'angolo superiore sinistro di hello e quindi fare clic su **macchine virtuali (classico)**:

![Cercare la macchina virtuale di Azure](./media/reset-rdp/Portal-Select-Classic-VM.png)

Selezionare la macchina virtuale di Windows e quindi fare clic su **Reimposta accesso remoto...** . hello seguente viene visualizzata la finestra Configurazione di Desktop remoto tooreset hello:

![Ripristinare la pagina di configurazione RDP](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

È inoltre possibile reimpostare hello username e password dell'account amministratore locale hello. Dalla macchina virtuale fare clic su **Supporto e risoluzione dei problemi** > **Reimposta password**. viene visualizzato il pannello di reimpostazione della password Hello:

![Pagina di reimpostazione della password](./media/reset-rdp/Portal-PW-Reset-Windows.png)

Dopo aver immesso hello nuovo nome utente e password, fare clic su **salvare**.

## <a name="vmaccess-extension-and-powershell"></a>Estensione VMAccess e PowerShell
Verificare che hello che agente VM viene installato nella macchina virtuale hello. estensione VMAccess Hello non deve necessariamente toobe installato prima di poterla utilizzare, purché hello agente della macchina virtuale è disponibile. Verificare che hello che agente VM è già stato installato utilizzando hello comando seguente. (Sostituire "myCloudService" e "myVM", i nomi di hello del servizio cloud e la macchina virtuale, rispettivamente. Per individuare questi nomi eseguire `Get-AzureVM` senza parametri.

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

Se hello **write-host** comando Visualizza **True**, hello è installato l'agente di macchine Virtuali. Se viene visualizzato **False**, vedere le istruzioni di hello e un collegamento di toohello scaricare hello [agente VM ed estensioni - parte 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) post di blog di Azure.

Se è stato creato tramite il portale di hello macchina virtuale hello, controllare se `$vm.GetInstance().ProvisionGuestAgent` restituisce **True**. In caso contrario, è possibile impostarla usando questo comando:

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

Questo comando impedisce l'errore seguente quando si esegue hello hello **Set-AzureVMExtension** comando passaggi successivi hello: "Dell'agente Guest di eseguire il provisioning è necessario attivare oggetto macchina virtuale hello prima di impostare l'estensione dell'accesso VM IaaS."

### <a name="reset-hello-local-administrator-account-password"></a>**La reimpostazione della password dell'account amministratore locale hello**
Creare una credenziale di accesso con nome dell'account administrator locale corrente hello e una nuova password e quindi eseguire hello `Set-AzureVMAccessExtension` come indicato di seguito.

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

Se si digita un nome diverso da quello corrente hello, hello estensione VMAccess Rinomina l'account amministratore locale hello, assegna l'account di toothat password hello e genera un Desktop remoto uscita. Se l'account amministratore locale hello è disabilitato, viene abilitato hello estensione VMAccess.

Questi comandi anche la configurazione del servizio Desktop remoto hello reimpostano.

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Reimposta configurazione del servizio Desktop remoto hello**
tooreset hello servizio configurazione di Desktop remoto, eseguire hello comando seguente:

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

Hello estensione VMAccess esegue due comandi nella macchina virtuale hello:

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

Questo comando abilita gruppo di Windows Firewall incorporato hello che consenta il traffico in ingresso di Desktop remoto, che utilizza la porta TCP 3389.

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

Questo comando imposta hello fDenyTSConnections del Registro di sistema valore too0, abilitare le connessioni Desktop remoto.

## <a name="next-steps"></a>Passaggi successivi
Se non risponde hello estensione accesso alle macchine Virtuali di Azure e si desidera password hello tooreset non è possibile, è possibile [reimpostazione hello locale password di Windows non in linea](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Questo metodo è un processo più avanzato e richiede tooconnect hello disco rigido virtuale di hello problematico VM tooanother macchina virtuale. Seguire i passaggi di hello descritte in questo articolo innanzitutto e cercano solo metodo di reimpostazione della password non in linea hello come ultima risorsa.

[Estensioni VM e funzionalità di Azure](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Connettersi tooan macchina virtuale di Azure con RDP o SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[Risolvere i problemi relativi a Desktop remoto connessioni tooa basati su Windows macchina virtuale di Azure](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

