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
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a><span data-ttu-id="935c3-103">Come servizio Desktop remoto di hello tooreset o la password di account di accesso in una macchina virtuale Windows creata mediante modello di distribuzione classica hello</span><span class="sxs-lookup"><span data-stu-id="935c3-103">How tooreset hello Remote Desktop service or its login password in a Windows VM created using hello Classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="935c3-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="935c3-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="935c3-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="935c3-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="935c3-106">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="935c3-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="935c3-107">È anche possibile [eseguire questi passaggi per macchine virtuali create con modello di distribuzione di gestione risorse di hello](../reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="935c3-107">You can also [perform these steps for VMs created with hello Resource Manager deployment model](../reset-rdp.md).</span></span>

<span data-ttu-id="935c3-108">Se non è possibile connettersi tooa Windows virtual machine (VM), è possibile reimpostare la password di amministratore locale hello o ripristinare hello Desktop remoto configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="935c3-108">If you can't connect tooa Windows virtual machine (VM), you can reset hello local administrator password or reset hello Remote Desktop service configuration.</span></span> <span data-ttu-id="935c3-109">È possibile utilizzare l'estensione di accesso alla VM Azure portal o hello hello in Azure PowerShell tooreset hello. la password.</span><span class="sxs-lookup"><span data-stu-id="935c3-109">You can use either hello Azure portal or hello VM Access extension in Azure PowerShell tooreset hello password.</span></span>

## <a name="ways-tooreset-configuration-or-credentials"></a><span data-ttu-id="935c3-110">Configurazione tooreset metodi o le credenziali</span><span class="sxs-lookup"><span data-stu-id="935c3-110">Ways tooreset configuration or credentials</span></span>
<span data-ttu-id="935c3-111">È possibile reimpostare i Servizi Desktop remoto e le credenziali in modi diversi, in base alle esigenze specifiche:</span><span class="sxs-lookup"><span data-stu-id="935c3-111">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="935c3-112">Reimpostare usando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="935c3-112">Reset using hello Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="935c3-113">Ripristinare con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="935c3-113">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="935c3-114">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="935c3-114">Azure portal</span></span>
<span data-ttu-id="935c3-115">È possibile utilizzare hello [portale di Azure](https://portal.azure.com) tooreset hello servizio Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="935c3-115">You can use hello [Azure portal](https://portal.azure.com) tooreset hello Remote Desktop service.</span></span> <span data-ttu-id="935c3-116">menu del portale hello tooexpand, fare clic sulle barre hello tre nell'angolo superiore sinistro di hello e quindi fare clic su **macchine virtuali (classico)**:</span><span class="sxs-lookup"><span data-stu-id="935c3-116">tooexpand hello portal menu, click hello three bars in hello upper left corner and then click **Virtual machines (classic)**:</span></span>

![Cercare la macchina virtuale di Azure](./media/reset-rdp/Portal-Select-Classic-VM.png)

<span data-ttu-id="935c3-118">Selezionare la macchina virtuale di Windows e quindi fare clic su **Reimposta accesso remoto...** . hello seguente viene visualizzata la finestra Configurazione di Desktop remoto tooreset hello:</span><span class="sxs-lookup"><span data-stu-id="935c3-118">Select your Windows virtual machine and then click **Reset Remote...**. hello following dialog appears tooreset hello Remote Desktop configuration:</span></span>

![Ripristinare la pagina di configurazione RDP](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

<span data-ttu-id="935c3-120">È inoltre possibile reimpostare hello username e password dell'account amministratore locale hello.</span><span class="sxs-lookup"><span data-stu-id="935c3-120">You can also reset hello username and password of hello local administrator account.</span></span> <span data-ttu-id="935c3-121">Dalla macchina virtuale fare clic su **Supporto e risoluzione dei problemi** > **Reimposta password**.</span><span class="sxs-lookup"><span data-stu-id="935c3-121">From your VM, click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="935c3-122">viene visualizzato il pannello di reimpostazione della password Hello:</span><span class="sxs-lookup"><span data-stu-id="935c3-122">hello password reset blade is displayed:</span></span>

![Pagina di reimpostazione della password](./media/reset-rdp/Portal-PW-Reset-Windows.png)

<span data-ttu-id="935c3-124">Dopo aver immesso hello nuovo nome utente e password, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="935c3-124">After you enter hello new user name and password, click **Save**.</span></span>

## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="935c3-125">Estensione VMAccess e PowerShell</span><span class="sxs-lookup"><span data-stu-id="935c3-125">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="935c3-126">Verificare che hello che agente VM viene installato nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="935c3-126">Make sure hello VM Agent is installed on hello virtual machine.</span></span> <span data-ttu-id="935c3-127">estensione VMAccess Hello non deve necessariamente toobe installato prima di poterla utilizzare, purché hello agente della macchina virtuale è disponibile.</span><span class="sxs-lookup"><span data-stu-id="935c3-127">hello VMAccess extension doesn't need toobe installed before you can use it, as long as hello VM Agent is available.</span></span> <span data-ttu-id="935c3-128">Verificare che hello che agente VM è già stato installato utilizzando hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="935c3-128">Verify that hello VM Agent is already installed by using hello following command.</span></span> <span data-ttu-id="935c3-129">(Sostituire "myCloudService" e "myVM", i nomi di hello del servizio cloud e la macchina virtuale, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="935c3-129">(Replace "myCloudService" and "myVM" by hello names of your cloud service and your VM, respectively.</span></span> <span data-ttu-id="935c3-130">Per individuare questi nomi eseguire `Get-AzureVM` senza parametri.</span><span class="sxs-lookup"><span data-stu-id="935c3-130">You can learn these names by running `Get-AzureVM` without any parameters.)</span></span>

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="935c3-131">Se hello **write-host** comando Visualizza **True**, hello è installato l'agente di macchine Virtuali.</span><span class="sxs-lookup"><span data-stu-id="935c3-131">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="935c3-132">Se viene visualizzato **False**, vedere le istruzioni di hello e un collegamento di toohello scaricare hello [agente VM ed estensioni - parte 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) post di blog di Azure.</span><span class="sxs-lookup"><span data-stu-id="935c3-132">If it displays **False**, see hello instructions and a link toohello download in hello [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blog post.</span></span>

<span data-ttu-id="935c3-133">Se è stato creato tramite il portale di hello macchina virtuale hello, controllare se `$vm.GetInstance().ProvisionGuestAgent` restituisce **True**.</span><span class="sxs-lookup"><span data-stu-id="935c3-133">If you created hello virtual machine by using hello portal, check whether `$vm.GetInstance().ProvisionGuestAgent` returns **True**.</span></span> <span data-ttu-id="935c3-134">In caso contrario, è possibile impostarla usando questo comando:</span><span class="sxs-lookup"><span data-stu-id="935c3-134">If not, you can set it by using this command:</span></span>

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

<span data-ttu-id="935c3-135">Questo comando impedisce l'errore seguente quando si esegue hello hello **Set-AzureVMExtension** comando passaggi successivi hello: "Dell'agente Guest di eseguire il provisioning è necessario attivare oggetto macchina virtuale hello prima di impostare l'estensione dell'accesso VM IaaS."</span><span class="sxs-lookup"><span data-stu-id="935c3-135">This command prevents hello following error when you're running hello **Set-AzureVMExtension** command in hello next steps: “Provision Guest Agent must be enabled on hello VM object before setting IaaS VM Access Extension.”</span></span>

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="935c3-136">**La reimpostazione della password dell'account amministratore locale hello**</span><span class="sxs-lookup"><span data-stu-id="935c3-136">**Reset hello local administrator account password**</span></span>
<span data-ttu-id="935c3-137">Creare una credenziale di accesso con nome dell'account administrator locale corrente hello e una nuova password e quindi eseguire hello `Set-AzureVMAccessExtension` come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="935c3-137">Create a sign-in credential with hello current local administrator account name and a new password, and then run hello `Set-AzureVMAccessExtension` as follows.</span></span>

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

<span data-ttu-id="935c3-138">Se si digita un nome diverso da quello corrente hello, hello estensione VMAccess Rinomina l'account amministratore locale hello, assegna l'account di toothat password hello e genera un Desktop remoto uscita. Se l'account amministratore locale hello è disabilitato, viene abilitato hello estensione VMAccess.</span><span class="sxs-lookup"><span data-stu-id="935c3-138">If you type a different name than hello current account, hello VMAccess extension renames hello local administrator account, assigns hello password toothat account, and issues a Remote Desktop sign-out. If hello local administrator account is disabled, hello VMAccess extension enables it.</span></span>

<span data-ttu-id="935c3-139">Questi comandi anche la configurazione del servizio Desktop remoto hello reimpostano.</span><span class="sxs-lookup"><span data-stu-id="935c3-139">These commands also reset hello Remote Desktop service configuration.</span></span>

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="935c3-140">**Reimposta configurazione del servizio Desktop remoto hello**</span><span class="sxs-lookup"><span data-stu-id="935c3-140">**Reset hello Remote Desktop service configuration**</span></span>
<span data-ttu-id="935c3-141">tooreset hello servizio configurazione di Desktop remoto, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="935c3-141">tooreset hello Remote Desktop service configuration, run hello following command:</span></span>

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

<span data-ttu-id="935c3-142">Hello estensione VMAccess esegue due comandi nella macchina virtuale hello:</span><span class="sxs-lookup"><span data-stu-id="935c3-142">hello VMAccess extension runs two commands on hello virtual machine:</span></span>

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

<span data-ttu-id="935c3-143">Questo comando abilita gruppo di Windows Firewall incorporato hello che consenta il traffico in ingresso di Desktop remoto, che utilizza la porta TCP 3389.</span><span class="sxs-lookup"><span data-stu-id="935c3-143">This command enables hello built-in Windows Firewall group that allows incoming Remote Desktop traffic, which uses TCP port 3389.</span></span>

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

<span data-ttu-id="935c3-144">Questo comando imposta hello fDenyTSConnections del Registro di sistema valore too0, abilitare le connessioni Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="935c3-144">This command sets hello fDenyTSConnections registry value too0, enabling Remote Desktop connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="935c3-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="935c3-145">Next steps</span></span>
<span data-ttu-id="935c3-146">Se non risponde hello estensione accesso alle macchine Virtuali di Azure e si desidera password hello tooreset non è possibile, è possibile [reimpostazione hello locale password di Windows non in linea](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="935c3-146">If hello Azure VM access extension does not respond and you are unable tooreset hello password, you can [reset hello local Windows password offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="935c3-147">Questo metodo è un processo più avanzato e richiede tooconnect hello disco rigido virtuale di hello problematico VM tooanother macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="935c3-147">This method is a more advanced process and requires you tooconnect hello virtual hard disk of hello problematic VM tooanother VM.</span></span> <span data-ttu-id="935c3-148">Seguire i passaggi di hello descritte in questo articolo innanzitutto e cercano solo metodo di reimpostazione della password non in linea hello come ultima risorsa.</span><span class="sxs-lookup"><span data-stu-id="935c3-148">Follow hello steps documented in this article first, and only attempt hello offline password reset method as a last resort.</span></span>

[<span data-ttu-id="935c3-149">Estensioni VM e funzionalità di Azure</span><span class="sxs-lookup"><span data-stu-id="935c3-149">Azure VM extensions and features</span></span>](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="935c3-150">Connettersi tooan macchina virtuale di Azure con RDP o SSH</span><span class="sxs-lookup"><span data-stu-id="935c3-150">Connect tooan Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="935c3-151">Risolvere i problemi relativi a Desktop remoto connessioni tooa basati su Windows macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="935c3-151">Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine</span></span>](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

