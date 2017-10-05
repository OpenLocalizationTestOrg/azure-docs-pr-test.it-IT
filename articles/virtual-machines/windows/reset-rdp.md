---
title: Reimpostare la password o la configurazione di Desktop remoto in una VM Windows | Microsoft Docs
description: Informazioni su come reimpostare la password di un account o i servizi Desktop remoto in una VM Windows tramite il portale di Azure o Azure PowerShell.
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
ms.openlocfilehash: 2e002e3f336422b8fa1eceece889cd083e355a68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-the-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a><span data-ttu-id="cc115-103">Come reimpostare il servizio Desktop remoto o la relativa password di accesso in una VM Windows</span><span class="sxs-lookup"><span data-stu-id="cc115-103">How to reset the Remote Desktop service or its login password in a Windows VM</span></span>
<span data-ttu-id="cc115-104">Se non è possibile connettersi a una macchina virtuale Windows, è possibile reimpostare la password di amministratore locale o la configurazione del servizio Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="cc115-104">If you can't connect to a Windows virtual machine (VM), you can reset the local administrator password or reset the Remote Desktop service configuration.</span></span> <span data-ttu-id="cc115-105">È possibile usare il portale di Azure o l'estensione di accesso alla VM in Azure PowerShell per reimpostare la password.</span><span class="sxs-lookup"><span data-stu-id="cc115-105">You can use either the Azure portal or the VM Access extension in Azure PowerShell to reset the password.</span></span> <span data-ttu-id="cc115-106">Se si usa PowerShell, verificare che il [modulo di PowerShell più recente sia installato e configurato](/powershell/azure/overview) e di avere eseguito l'accesso alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="cc115-106">If you are using PowerShell, make sure that you have the [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in to your Azure subscription.</span></span> <span data-ttu-id="cc115-107">È anche possibile [eseguire questi passaggi per le macchine virtuali create con il modello di distribuzione classica](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="cc115-107">You can also [perform these steps for VMs created with the Classic deployment model](reset-rdp.md).</span></span>

## <a name="ways-to-reset-configuration-or-credentials"></a><span data-ttu-id="cc115-108">Modalità per ripristinare la configurazione o le credenziali</span><span class="sxs-lookup"><span data-stu-id="cc115-108">Ways to reset configuration or credentials</span></span>
<span data-ttu-id="cc115-109">È possibile reimpostare i Servizi Desktop remoto e le credenziali in modi diversi, in base alle esigenze specifiche:</span><span class="sxs-lookup"><span data-stu-id="cc115-109">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="cc115-110">Ripristinare con il Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="cc115-110">Reset using the Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="cc115-111">Ripristinare con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc115-111">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="cc115-112">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="cc115-112">Azure portal</span></span>
<span data-ttu-id="cc115-113">Per espandere il menu del portale, fare clic sulle tre barre nell'angolo superiore sinistro e quindi fare clic su **Macchine virtuali**:</span><span class="sxs-lookup"><span data-stu-id="cc115-113">To expand the portal menu, click the three bars in the upper left corner and then click **Virtual machines**:</span></span>

![Cercare la macchina virtuale di Azure](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-the-local-administrator-account-password"></a><span data-ttu-id="cc115-115">**Reimpostare una password dell'account amministratore locale**</span><span class="sxs-lookup"><span data-stu-id="cc115-115">**Reset the local administrator account password**</span></span>

<span data-ttu-id="cc115-116">Selezionare la macchina virtuale Windows, quindi fare clic su **Supporto e risoluzione dei problemi** > **Reimposta password**.</span><span class="sxs-lookup"><span data-stu-id="cc115-116">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="cc115-117">Viene visualizzato il pannello per la reimpostazione della password:</span><span class="sxs-lookup"><span data-stu-id="cc115-117">The password reset blade is displayed:</span></span>

![Pagina di reimpostazione della password](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

<span data-ttu-id="cc115-119">Immettere il nome utente e una nuova password, quindi fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="cc115-119">Enter the username and a new password, then click **Update**.</span></span> <span data-ttu-id="cc115-120">Provare a connettersi di nuovo alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cc115-120">Try connecting to your VM again.</span></span>

### <a name="reset-the-remote-desktop-service-configuration"></a><span data-ttu-id="cc115-121">**Reimpostare la configurazione del servizio Desktop remoto**</span><span class="sxs-lookup"><span data-stu-id="cc115-121">**Reset the Remote Desktop service configuration**</span></span>

<span data-ttu-id="cc115-122">Selezionare la macchina virtuale Windows, quindi fare clic su **Supporto e risoluzione dei problemi** > **Reimposta password**.</span><span class="sxs-lookup"><span data-stu-id="cc115-122">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="cc115-123">Viene visualizzato il pannello per la reimpostazione della password.</span><span class="sxs-lookup"><span data-stu-id="cc115-123">The password reset blade is displayed.</span></span> 

![Ripristinare la configurazione RDP](./media/reset-rdp/Portal-RM-RDP-Reset.png)

<span data-ttu-id="cc115-125">Selezionare **Reset configuration only** (Ripristina solo la configurazione) dal menu a discesa, quindi fare clic su **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="cc115-125">Select **Reset configuration only** from the drop-down menu, then click **Update**.</span></span> <span data-ttu-id="cc115-126">Provare a connettersi di nuovo alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cc115-126">Try connecting to your VM again.</span></span>


## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="cc115-127">Estensione VMAccess e PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc115-127">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="cc115-128">Verificare che il [modulo di PowerShell più recente sia installato e configurato](/powershell/azure/overview) e di avere eseguito l'accesso alla sottoscrizione di Azure con il cmdlet `Login-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="cc115-128">Make sure that you have the [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in to your Azure subscription with the `Login-AzureRmAccount` cmdlet.</span></span>

### <a name="reset-the-local-administrator-account-password"></a><span data-ttu-id="cc115-129">**Reimpostare una password dell'account amministratore locale**</span><span class="sxs-lookup"><span data-stu-id="cc115-129">**Reset the local administrator account password**</span></span>
<span data-ttu-id="cc115-130">Ripristinare la password o il nome utente di amministratore usando il cmdlet di PowerShell [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension).</span><span class="sxs-lookup"><span data-stu-id="cc115-130">Reset the administrator password or user name with the [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="cc115-131">Creare le credenziali dell'account come segue:</span><span class="sxs-lookup"><span data-stu-id="cc115-131">Create your account credentials as follows:</span></span>

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> <span data-ttu-id="cc115-132">Se si digita un nome diverso rispetto all'account di amministratore locale attuale sulla macchina virtuale, l'estensione VMAccess assegnerà un nuovo nome all'account amministratore locale, assegnerà la password specificata a tale account ed effettuerà la disconnessione da Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="cc115-132">If you type a different name than the current local administrator account on your VM, the VMAccess extension renames the local administrator account, assigns your specified password to that account, and issues a Remote Desktop logoff event.</span></span> <span data-ttu-id="cc115-133">Se l'account amministratore locale sulla macchina virtuale è disabilitato, l'estensione VMAccess lo abilita.</span><span class="sxs-lookup"><span data-stu-id="cc115-133">If the local administrator account on your VM is disabled, the VMAccess extension enables it.</span></span>

<span data-ttu-id="cc115-134">Nell'esempio seguente le credenziali della macchina virtuale denominata `myVM` nel gruppo di risorse denominato `myResourceGroup` vengono aggiornate alle credenziali specificate.</span><span class="sxs-lookup"><span data-stu-id="cc115-134">The following example updates the VM named `myVM` in the resource group named `myResourceGroup` to the credentials specified.</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-the-remote-desktop-service-configuration"></a><span data-ttu-id="cc115-135">**Reimpostare la configurazione del servizio Desktop remoto**</span><span class="sxs-lookup"><span data-stu-id="cc115-135">**Reset the Remote Desktop service configuration**</span></span>
<span data-ttu-id="cc115-136">Reimpostare l'accesso remoto alla macchina virtuale con il cmdlet di PowerShell [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension).</span><span class="sxs-lookup"><span data-stu-id="cc115-136">Reset remote access to your VM with the [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="cc115-137">Nell'esempio seguente viene ripristinata l'estensione di accesso denominata `myVMAccess` nella macchina virtuale denominata `myVM` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="cc115-137">The following example resets the access extension named `myVMAccess` on the VM named `myVM` in the `myResourceGroup` resource group:</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> <span data-ttu-id="cc115-138">In qualsiasi momento una VM può avere un solo agente di accesso.</span><span class="sxs-lookup"><span data-stu-id="cc115-138">At any point, a VM can have only a single VM access agent.</span></span> <span data-ttu-id="cc115-139">Per impostare le proprietà dell'agente di accesso alla macchina virtuale, è possibile usare l'opzione `-ForceRerun`.</span><span class="sxs-lookup"><span data-stu-id="cc115-139">To set the VM access agent properties successfully, the `-ForceRerun` option can be used.</span></span> <span data-ttu-id="cc115-140">Quando si usa `-ForceRerun`, assicurarsi di usare lo stesso nome per l'agente di accesso alla macchina virtuale impostato nei comandi precedenti.</span><span class="sxs-lookup"><span data-stu-id="cc115-140">When using `-ForceRerun`, make sure to use the same name for the VM access agent as used in any previous commands.</span></span>

<span data-ttu-id="cc115-141">Se non è ancora possibile connettersi in remoto alla macchina virtuale, vedere altre procedure da provare in [Risolvere i problemi di connessioni Desktop remoto a una macchina virtuale di Azure che esegue Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc115-141">If you still can't connect remotely to your virtual machine, see more steps to try at [Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="next-steps"></a><span data-ttu-id="cc115-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cc115-142">Next steps</span></span>
<span data-ttu-id="cc115-143">Se l'estensione di accesso alla VM di Azure non risponde ed è impossibile reimpostare la password, [reimpostare la password di Windows locale offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc115-143">If the Azure VM access extension does not respond and you are unable to reset the password, you can [reset the local Windows password offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="cc115-144">Questo metodo è un processo più avanzato e richiede di connettere il disco rigido virtuale della VM problematica a un'altra VM.</span><span class="sxs-lookup"><span data-stu-id="cc115-144">This method is a more advanced process and requires you to connect the virtual hard disk of the problematic VM to another VM.</span></span> <span data-ttu-id="cc115-145">Seguire prima i passaggi illustrati in questo articolo e provare a reimpostare la password offline solo come ultima risorsa.</span><span class="sxs-lookup"><span data-stu-id="cc115-145">Follow the steps documented in this article first, and only attempt the offline password reset method as a last resort.</span></span>

[<span data-ttu-id="cc115-146">Estensioni VM e funzionalità di Azure</span><span class="sxs-lookup"><span data-stu-id="cc115-146">Azure VM extensions and features</span></span>](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="cc115-147">Connettersi a una macchina virtuale di Azure con RDP o SSH</span><span class="sxs-lookup"><span data-stu-id="cc115-147">Connect to an Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="cc115-148">Risolvere i problemi di connessioni Desktop remoto a una macchina virtuale di Azure basata su Windows</span><span class="sxs-lookup"><span data-stu-id="cc115-148">Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine</span></span>](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

