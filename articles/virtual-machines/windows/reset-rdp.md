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
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a><span data-ttu-id="dd41b-103">Come tooreset hello servizio Desktop remoto o la password di account di accesso in una macchina virtuale Windows</span><span class="sxs-lookup"><span data-stu-id="dd41b-103">How tooreset hello Remote Desktop service or its login password in a Windows VM</span></span>
<span data-ttu-id="dd41b-104">Se non è possibile connettersi tooa Windows virtual machine (VM), è possibile reimpostare la password di amministratore locale hello o ripristinare hello Desktop remoto configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="dd41b-104">If you can't connect tooa Windows virtual machine (VM), you can reset hello local administrator password or reset hello Remote Desktop service configuration.</span></span> <span data-ttu-id="dd41b-105">È possibile utilizzare l'estensione di accesso alla VM Azure portal o hello hello in Azure PowerShell tooreset hello. la password.</span><span class="sxs-lookup"><span data-stu-id="dd41b-105">You can use either hello Azure portal or hello VM Access extension in Azure PowerShell tooreset hello password.</span></span> <span data-ttu-id="dd41b-106">Se si usa PowerShell, assicurarsi di aver hello [modulo di PowerShell più recente installato e configurato](/powershell/azure/overview) e vengono firmati in tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd41b-106">If you are using PowerShell, make sure that you have hello [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in tooyour Azure subscription.</span></span> <span data-ttu-id="dd41b-107">È anche possibile [eseguire questi passaggi per macchine virtuali create con modello di distribuzione classica hello](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="dd41b-107">You can also [perform these steps for VMs created with hello Classic deployment model](reset-rdp.md).</span></span>

## <a name="ways-tooreset-configuration-or-credentials"></a><span data-ttu-id="dd41b-108">Configurazione tooreset metodi o le credenziali</span><span class="sxs-lookup"><span data-stu-id="dd41b-108">Ways tooreset configuration or credentials</span></span>
<span data-ttu-id="dd41b-109">È possibile reimpostare i Servizi Desktop remoto e le credenziali in modi diversi, in base alle esigenze specifiche:</span><span class="sxs-lookup"><span data-stu-id="dd41b-109">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="dd41b-110">Reimpostare usando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="dd41b-110">Reset using hello Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="dd41b-111">Ripristinare con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd41b-111">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="dd41b-112">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="dd41b-112">Azure portal</span></span>
<span data-ttu-id="dd41b-113">menu del portale hello tooexpand, fare clic sulle barre hello tre nell'angolo superiore sinistro di hello e quindi fare clic su **macchine virtuali**:</span><span class="sxs-lookup"><span data-stu-id="dd41b-113">tooexpand hello portal menu, click hello three bars in hello upper left corner and then click **Virtual machines**:</span></span>

![Cercare la macchina virtuale di Azure](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="dd41b-115">**La reimpostazione della password dell'account amministratore locale hello**</span><span class="sxs-lookup"><span data-stu-id="dd41b-115">**Reset hello local administrator account password**</span></span>

<span data-ttu-id="dd41b-116">Selezionare la macchina virtuale Windows, quindi fare clic su **Supporto e risoluzione dei problemi** > **Reimposta password**.</span><span class="sxs-lookup"><span data-stu-id="dd41b-116">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="dd41b-117">viene visualizzato il pannello di reimpostazione della password Hello:</span><span class="sxs-lookup"><span data-stu-id="dd41b-117">hello password reset blade is displayed:</span></span>

![Pagina di reimpostazione della password](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

<span data-ttu-id="dd41b-119">Immettere nome utente hello e una nuova password, quindi fare clic su **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="dd41b-119">Enter hello username and a new password, then click **Update**.</span></span> <span data-ttu-id="dd41b-120">Provare a riconnettersi tooyour macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dd41b-120">Try connecting tooyour VM again.</span></span>

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="dd41b-121">**Reimposta configurazione del servizio Desktop remoto hello**</span><span class="sxs-lookup"><span data-stu-id="dd41b-121">**Reset hello Remote Desktop service configuration**</span></span>

<span data-ttu-id="dd41b-122">Selezionare la macchina virtuale Windows, quindi fare clic su **Supporto e risoluzione dei problemi** > **Reimposta password**.</span><span class="sxs-lookup"><span data-stu-id="dd41b-122">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="dd41b-123">Pannello di reimpostazione della password Hello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="dd41b-123">hello password reset blade is displayed.</span></span> 

![Ripristinare la configurazione RDP](./media/reset-rdp/Portal-RM-RDP-Reset.png)

<span data-ttu-id="dd41b-125">Selezionare **configurazione per la reimpostazione solo** dal menu a discesa hello, quindi fare clic su **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="dd41b-125">Select **Reset configuration only** from hello drop-down menu, then click **Update**.</span></span> <span data-ttu-id="dd41b-126">Provare a riconnettersi tooyour macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dd41b-126">Try connecting tooyour VM again.</span></span>


## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="dd41b-127">Estensione VMAccess e PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd41b-127">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="dd41b-128">Assicurarsi di avere hello [modulo di PowerShell più recente installato e configurato](/powershell/azure/overview) e vengono firmati nella sottoscrizione di Azure con hello tooyour `Login-AzureRmAccount` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dd41b-128">Make sure that you have hello [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in tooyour Azure subscription with hello `Login-AzureRmAccount` cmdlet.</span></span>

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="dd41b-129">**La reimpostazione della password dell'account amministratore locale hello**</span><span class="sxs-lookup"><span data-stu-id="dd41b-129">**Reset hello local administrator account password**</span></span>
<span data-ttu-id="dd41b-130">Reimpostazione hello amministratore password o nome utente con hello [Set AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dd41b-130">Reset hello administrator password or user name with hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="dd41b-131">Creare le credenziali dell'account come segue:</span><span class="sxs-lookup"><span data-stu-id="dd41b-131">Create your account credentials as follows:</span></span>

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> <span data-ttu-id="dd41b-132">Se si digita un nome diverso account amministratore locale corrente hello nella VM, hello estensione VMAccess Rinomina l'account amministratore locale hello, assegna l'account toothat password specificata e genera un evento di disconnessione di Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="dd41b-132">If you type a different name than hello current local administrator account on your VM, hello VMAccess extension renames hello local administrator account, assigns your specified password toothat account, and issues a Remote Desktop logoff event.</span></span> <span data-ttu-id="dd41b-133">Se l'account amministratore locale hello la macchina virtuale è disabilitato, viene abilitato hello estensione VMAccess.</span><span class="sxs-lookup"><span data-stu-id="dd41b-133">If hello local administrator account on your VM is disabled, hello VMAccess extension enables it.</span></span>

<span data-ttu-id="dd41b-134">dopo gli aggiornamenti di esempio Hello hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup` toohello credenziali specificate.</span><span class="sxs-lookup"><span data-stu-id="dd41b-134">hello following example updates hello VM named `myVM` in hello resource group named `myResourceGroup` toohello credentials specified.</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="dd41b-135">**Reimposta configurazione del servizio Desktop remoto hello**</span><span class="sxs-lookup"><span data-stu-id="dd41b-135">**Reset hello Remote Desktop service configuration**</span></span>
<span data-ttu-id="dd41b-136">Ripristinare accesso remoto tooyour VM con hello [Set AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dd41b-136">Reset remote access tooyour VM with hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="dd41b-137">esempio Hello Reimposta estensione accesso hello denominata `myVMAccess` nella macchina virtuale denominata hello `myVM` in hello `myResourceGroup` gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="dd41b-137">hello following example resets hello access extension named `myVMAccess` on hello VM named `myVM` in hello `myResourceGroup` resource group:</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> <span data-ttu-id="dd41b-138">In qualsiasi momento una VM può avere un solo agente di accesso.</span><span class="sxs-lookup"><span data-stu-id="dd41b-138">At any point, a VM can have only a single VM access agent.</span></span> <span data-ttu-id="dd41b-139">la proprietà agente tooset hello VM accesso correttamente, hello `-ForceRerun` opzione può essere utilizzata.</span><span class="sxs-lookup"><span data-stu-id="dd41b-139">tooset hello VM access agent properties successfully, hello `-ForceRerun` option can be used.</span></span> <span data-ttu-id="dd41b-140">Quando si utilizza `-ForceRerun`, assicurarsi che toouse hello dello stesso nome per l'agente di accesso alla macchina virtuale hello utilizzato in tutti i comandi precedenti.</span><span class="sxs-lookup"><span data-stu-id="dd41b-140">When using `-ForceRerun`, make sure toouse hello same name for hello VM access agent as used in any previous commands.</span></span>

<span data-ttu-id="dd41b-141">Se non è possibile connettersi in remoto macchina virtuale tooyour, vedere più passaggi tootry in [risolvere i problemi di Desktop remoto connessioni tooa basati su Windows macchina virtuale di Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd41b-141">If you still can't connect remotely tooyour virtual machine, see more steps tootry at [Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="next-steps"></a><span data-ttu-id="dd41b-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dd41b-142">Next steps</span></span>
<span data-ttu-id="dd41b-143">Se non risponde hello estensione accesso alle macchine Virtuali di Azure e si desidera password hello tooreset non è possibile, è possibile [reimpostazione hello locale password di Windows non in linea](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd41b-143">If hello Azure VM access extension does not respond and you are unable tooreset hello password, you can [reset hello local Windows password offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="dd41b-144">Questo metodo è un processo più avanzato e richiede tooconnect hello disco rigido virtuale di hello problematico VM tooanother macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dd41b-144">This method is a more advanced process and requires you tooconnect hello virtual hard disk of hello problematic VM tooanother VM.</span></span> <span data-ttu-id="dd41b-145">Seguire i passaggi di hello descritte in questo articolo innanzitutto e cercano solo metodo di reimpostazione della password non in linea hello come ultima risorsa.</span><span class="sxs-lookup"><span data-stu-id="dd41b-145">Follow hello steps documented in this article first, and only attempt hello offline password reset method as a last resort.</span></span>

[<span data-ttu-id="dd41b-146">Estensioni VM e funzionalità di Azure</span><span class="sxs-lookup"><span data-stu-id="dd41b-146">Azure VM extensions and features</span></span>](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="dd41b-147">Connettersi tooan macchina virtuale di Azure con RDP o SSH</span><span class="sxs-lookup"><span data-stu-id="dd41b-147">Connect tooan Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="dd41b-148">Risolvere i problemi relativi a Desktop remoto connessioni tooa basati su Windows macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="dd41b-148">Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine</span></span>](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

