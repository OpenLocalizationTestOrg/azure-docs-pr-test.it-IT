---
title: Risolvere i problemi di connessione SSH a una macchina virtuale di Azure | Documentazione Microsoft
description: Come risolvere i problemi, ad esempio una connessione SSH non riuscita o rifiutata per una macchina virtuale di Azure che esegue Linux.
keywords: connessione SSH rifiutata, errore SSH, SSH Azure, connessione SSH non riuscita
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: iainfou
ms.openlocfilehash: 3a282c8b2c2ba2749de6a2d3688bd57d75703b22
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-ssh-connections-to-an-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="e68be-104">Risoluzione dei problemi di connessione SSH a una macchina virtuale Linux di Azure che ha esito negativo, genera errori o è stata rifiutata.</span><span class="sxs-lookup"><span data-stu-id="e68be-104">Troubleshoot SSH connections to an Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="e68be-105">Sono vari i motivi per cui possono verificarsi errori Secure Shell (SSH), la connessione SSH non riesce o viene rifiutata durante il tentativo di connessione a una macchina virtuale Linux.</span><span class="sxs-lookup"><span data-stu-id="e68be-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try to connect to a Linux virtual machine (VM).</span></span> <span data-ttu-id="e68be-106">Questo articolo consente di individuare i problemi e correggerli.</span><span class="sxs-lookup"><span data-stu-id="e68be-106">This article helps you find and correct the problems.</span></span> <span data-ttu-id="e68be-107">È possibile usare il portale di Azure, l'interfaccia della riga di comando Azure o l'estensione dell'accesso alle VM per Linux per risolvere i problemi di connessione.</span><span class="sxs-lookup"><span data-stu-id="e68be-107">You can use the Azure portal, Azure CLI, or VM Access Extension for Linux to troubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="e68be-108">Per ricevere assistenza in qualsiasi punto di questo articolo, contattare gli esperti di Azure nei [forum MSDN e Stack Overflow relativi ad Azure](http://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="e68be-108">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="e68be-109">In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="e68be-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="e68be-110">Accedere al sito del [supporto di Azure](http://azure.microsoft.com/support/options/) e selezionare **Ottenere supporto**.</span><span class="sxs-lookup"><span data-stu-id="e68be-110">Go to the [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="e68be-111">Per informazioni sull'uso del supporto di Azure, leggere le [Domande frequenti sul supporto di Azure](http://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="e68be-111">For information about using Azure Support, read the [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="e68be-112">Passaggi rapidi per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="e68be-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="e68be-113">Dopo ogni passaggio della procedura di risoluzione dei problemi, tentare la riconnessione alla VM.</span><span class="sxs-lookup"><span data-stu-id="e68be-113">After each troubleshooting step, try reconnecting to the VM.</span></span>

1. <span data-ttu-id="e68be-114">Reimpostare la configurazione SSH.</span><span class="sxs-lookup"><span data-stu-id="e68be-114">Reset the SSH configuration.</span></span>
2. <span data-ttu-id="e68be-115">Reimpostare le credenziali per l'utente.</span><span class="sxs-lookup"><span data-stu-id="e68be-115">Reset the credentials for the user.</span></span>
3. <span data-ttu-id="e68be-116">Verificare che le regole del [gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md) consentano il traffico SSH.</span><span class="sxs-lookup"><span data-stu-id="e68be-116">Verify the [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="e68be-117">Verificare l'esistenza di una regola del gruppo di sicurezza di rete che consente il traffico SSH (per impostazione predefinita, la porta TCP 22).</span><span class="sxs-lookup"><span data-stu-id="e68be-117">Ensure that a Network Security Group rule exists to permit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="e68be-118">Non è possibile usare il reindirizzamento o mapping delle porte senza usare Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="e68be-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="e68be-119">Controllare l'[integrità delle risorse della VM](../../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e68be-119">Check the [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="e68be-120">Assicurarsi che la macchina virtuale venga segnalata come integra.</span><span class="sxs-lookup"><span data-stu-id="e68be-120">Ensure that the VM reports as being healthy.</span></span>
   * <span data-ttu-id="e68be-121">Se si dispone della diagnostica di avvio abilitata, verificare che la macchina virtuale non segnali errori di avvio nei log.</span><span class="sxs-lookup"><span data-stu-id="e68be-121">If you have boot diagnostics enabled, verify the VM is not reporting boot errors in the logs.</span></span>
5. <span data-ttu-id="e68be-122">Riavviare la VM.</span><span class="sxs-lookup"><span data-stu-id="e68be-122">Restart the VM.</span></span>
6. <span data-ttu-id="e68be-123">Distribuire di nuovo la VM.</span><span class="sxs-lookup"><span data-stu-id="e68be-123">Redeploy the VM.</span></span>

<span data-ttu-id="e68be-124">Continuare la lettura per la procedura di risoluzione dei problemi e spiegazioni più dettagliate.</span><span class="sxs-lookup"><span data-stu-id="e68be-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-to-troubleshoot-ssh-connection-issues"></a><span data-ttu-id="e68be-125">Metodi disponibili per risolvere i problemi di connessione SSH</span><span class="sxs-lookup"><span data-stu-id="e68be-125">Available methods to troubleshoot SSH connection issues</span></span>
<span data-ttu-id="e68be-126">È possibile reimpostare le credenziali o la configurazione SSH usando uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e68be-126">You can reset credentials or SSH configuration using one of the following methods:</span></span>

* <span data-ttu-id="e68be-127">[Portale di Azure](#use-the-azure-portal): indicato per ripristinare rapidamente la configurazione SSH o la chiave SSH nel caso in cui non siano stati installati gli strumenti di Azure.</span><span class="sxs-lookup"><span data-stu-id="e68be-127">[Azure portal](#use-the-azure-portal) - great if you need to quickly reset the SSH configuration or SSH key and you don't have the Azure tools installed.</span></span>
* <span data-ttu-id="e68be-128">[Interfaccia della riga di comando di Azure 2.0](#use-the-azure-cli-20): se ci si trova già nella riga di comando, reimpostare rapidamente le credenziali o la configurazione SSH.</span><span class="sxs-lookup"><span data-stu-id="e68be-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on the command line, quickly reset the SSH configuration or credentials.</span></span> <span data-ttu-id="e68be-129">È possibile anche usare l'[interfaccia della riga di comando di Azure 1.0](#use-the-azure-cli-10)</span><span class="sxs-lookup"><span data-stu-id="e68be-129">You can also use the [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="e68be-130">[Estensione VMAccessForLinux di Azure](#use-the-vmaccess-extension): creare e usare di nuovo i file di definizione JSON per reimpostare le credenziali utente o la configurazione di SSH.</span><span class="sxs-lookup"><span data-stu-id="e68be-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files to reset the SSH configuration or user credentials.</span></span>

<span data-ttu-id="e68be-131">Dopo ogni passaggio della procedura di risoluzione dei problemi, ritentare di connettersi alla VM.</span><span class="sxs-lookup"><span data-stu-id="e68be-131">After each troubleshooting step, try connecting to your VM again.</span></span> <span data-ttu-id="e68be-132">Se ancora non è possibile connettersi, procedere al passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="e68be-132">If you still cannot connect, try the next step.</span></span>

## <a name="use-the-azure-portal"></a><span data-ttu-id="e68be-133">Usare il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e68be-133">Use the Azure portal</span></span>
<span data-ttu-id="e68be-134">Il portale di Azure offre un modo rapido per reimpostare le credenziali utente o la configurazione SSH senza installare nessuno degli strumenti presenti nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="e68be-134">The Azure portal provides a quick way to reset the SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="e68be-135">Selezionare la macchina virtuale nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e68be-135">Select your VM in the Azure portal.</span></span> <span data-ttu-id="e68be-136">Scorrere verso il basso la sezione **Supporto e risoluzione dei problemi** e selezionare **Reimposta password** come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e68be-136">Scroll down to the **Support + Troubleshooting** section and select **Reset password** as in the following example:</span></span>

![Reimpostare le credenziali o la configurazione SSH nel portale di Azure](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-the-ssh-configuration"></a><span data-ttu-id="e68be-138">Reimpostare la configurazione SSH</span><span class="sxs-lookup"><span data-stu-id="e68be-138">Reset the SSH configuration</span></span>
<span data-ttu-id="e68be-139">Come primo passaggio, selezionare `Reset configuration only` dal menu a discesa **Modalità** come nella schermata precedente, quindi fare clic sul pulsante **Reimposta**.</span><span class="sxs-lookup"><span data-stu-id="e68be-139">As a first step, select `Reset configuration only` from the **Mode** drop-down menu as in the preceding screenshot, then click the **Reset** button.</span></span> <span data-ttu-id="e68be-140">Dopo aver completato questa operazione, provare ad accedere nuovamente alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e68be-140">Once this action has completed, try to access your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="e68be-141">Reimpostare le credenziali SSH di un utente</span><span class="sxs-lookup"><span data-stu-id="e68be-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="e68be-142">Per reimpostare le credenziali di un utente esistente, selezionare `Reset SSH public key` o `Reset password` dal menu a discesa **Modalità** come nella schermata precedente.</span><span class="sxs-lookup"><span data-stu-id="e68be-142">To reset the credentials of an existing user, select either `Reset SSH public key` or `Reset password` from the **Mode** drop-down menu as in the preceding screenshot.</span></span> <span data-ttu-id="e68be-143">Specificare il nome utente e la chiave SSH o la nuova password, quindi fare clic sul pulsante **Reimposta**.</span><span class="sxs-lookup"><span data-stu-id="e68be-143">Specify the username and an SSH key or new password, then click the **Reset** button.</span></span>

<span data-ttu-id="e68be-144">Da questo menu è possibile anche creare un utente con privilegi sudo nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e68be-144">You can also create a user with sudo privileges on the VM from this menu.</span></span> <span data-ttu-id="e68be-145">Inserire il nuovo nome utente e la password o la chiave SSH associata, quindi fare clic sul pulsante **Reimposta**.</span><span class="sxs-lookup"><span data-stu-id="e68be-145">Enter a new username and associated password or SSH key, and then click the **Reset** button.</span></span>

## <a name="use-the-azure-cli-20"></a><span data-ttu-id="e68be-146">Usare l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e68be-146">Use the Azure CLI 2.0</span></span>
<span data-ttu-id="e68be-147">Se non è già stato fatto, installare la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e accedere a un account di Azure tramite il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e68be-147">If you haven't already, install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="e68be-148">Se è stata creata e caricata un'immagine del disco Linux personalizzata, verificare che sia installato l'[agente Linux di Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in versione 2.0.5 o successiva.</span><span class="sxs-lookup"><span data-stu-id="e68be-148">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="e68be-149">Per le macchine virtuali create tramite le immagini della raccolta, questa estensione dell'accesso è già installata e configurata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e68be-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="e68be-150">Reimpostare la configurazione SSH</span><span class="sxs-lookup"><span data-stu-id="e68be-150">Reset SSH configuration</span></span>
<span data-ttu-id="e68be-151">È possibile provare inizialmente a reimpostare la configurazione SSH ai valori predefiniti e riavviare quindi il server SSH nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e68be-151">You can initially try resetting the SSH configuration to default values and rebooting the SSH server on the VM.</span></span> <span data-ttu-id="e68be-152">Il nome dell'account utente e la password o le chiavi SSH non verranno modificati.</span><span class="sxs-lookup"><span data-stu-id="e68be-152">Note that this does not change the user account name, password, or SSH keys.</span></span>
<span data-ttu-id="e68be-153">L'esempio seguente usa [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) per reimpostare la configurazione SSH nella macchina virtuale denominata `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e68be-153">The following example uses [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) to reset the SSH configuration on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e68be-154">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="e68be-154">Use your own values as follows:</span></span>

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="e68be-155">Reimpostare le credenziali SSH di un utente</span><span class="sxs-lookup"><span data-stu-id="e68be-155">Reset SSH credentials for a user</span></span>
<span data-ttu-id="e68be-156">L'esempio seguente usa il comando [az vm user update](/cli/azure/vm/user#update) per reimpostare le credenziali per `myUsername` sul valore specificato in `myPassword`, nella macchina virtuale denominata `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e68be-156">The following example uses [az vm user update](/cli/azure/vm/user#update) to reset the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e68be-157">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="e68be-157">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="e68be-158">Se si usa l'autenticazione con chiave SSH, è possibile reimpostare la chiave SSH per un determinato utente.</span><span class="sxs-lookup"><span data-stu-id="e68be-158">If using SSH key authentication, you can reset the SSH key for a given user.</span></span> <span data-ttu-id="e68be-159">L'esempio seguente usa il comando **az vm access set-linux-user** per aggiornare la chiave SSH memorizzata in `~/.ssh/id_rsa.pub` per l'utente denominato `myUsername`, nella VM denominata `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e68be-159">The following example uses **az vm access set-linux-user** to update the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e68be-160">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="e68be-160">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-the-vmaccess-extension"></a><span data-ttu-id="e68be-161">Usare l'estensione VMAccess</span><span class="sxs-lookup"><span data-stu-id="e68be-161">Use the VMAccess extension</span></span>
<span data-ttu-id="e68be-162">L'estensione di accesso alla macchina virtuale per Linux legge un file json che definisce le azioni da eseguire. Queste azioni includono la reimpostazione SSHD, la reimpostazione di una chiave SSH o l'aggiunta di un utente.</span><span class="sxs-lookup"><span data-stu-id="e68be-162">The VM Access Extension for Linux reads in a json file that defines actions to carry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="e68be-163">È comunque possibile usare l'interfaccia della riga di comando di Azure per chiamare l'estensione VMAccess, ma è possibile anche usare di nuovo i file json tra più macchine virtuali, se desiderato.</span><span class="sxs-lookup"><span data-stu-id="e68be-163">You still use the Azure CLI to call the VMAccess extension, but you can reuse the json files across multiple VMs if desired.</span></span> <span data-ttu-id="e68be-164">Questo approccio consente di creare un archivio di file json da chiamare per determinati scenari.</span><span class="sxs-lookup"><span data-stu-id="e68be-164">This approach allows you to create a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="e68be-165">Reimpostare un disco SSHD</span><span class="sxs-lookup"><span data-stu-id="e68be-165">Reset SSHD</span></span>
<span data-ttu-id="e68be-166">Creare un file denominato `settings.json` con il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="e68be-166">Create a file named `settings.json` with the following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="e68be-167">Tramite l'interfaccia della riga di comando di Azure chiamare l'estensione `VMAccessForLinux` per reimpostare la connessione SSHD specificando il file json.</span><span class="sxs-lookup"><span data-stu-id="e68be-167">Using the Azure CLI, you then call the `VMAccessForLinux` extension to reset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="e68be-168">L'esempio seguente usa [az vm extension set](/cli/azure/vm/extension#set) per reimpostare SSHD nella macchina virtuale denominata `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e68be-168">The following example uses [az vm extension set](/cli/azure/vm/extension#set) to reset SSHD on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e68be-169">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="e68be-169">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="e68be-170">Reimpostare le credenziali SSH di un utente</span><span class="sxs-lookup"><span data-stu-id="e68be-170">Reset SSH credentials for a user</span></span>
<span data-ttu-id="e68be-171">Se il disco SSHD funziona correttamente, è possibile reimpostare le credenziali di un determinato utente.</span><span class="sxs-lookup"><span data-stu-id="e68be-171">If SSHD appears to function correctly, you can reset the credentials for a giver user.</span></span> <span data-ttu-id="e68be-172">Per reimpostare la password per un utente, creare un file denominato `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="e68be-172">To reset the password for a user, create a file named `settings.json`.</span></span> <span data-ttu-id="e68be-173">L'esempio seguente reimposta le credenziali per `myUsername` sul valore specificato in `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="e68be-173">The following example resets the credentials for `myUsername` to the value specified in `myPassword`.</span></span> <span data-ttu-id="e68be-174">Immettere le seguenti righe nel file `settings.json` con valori personalizzati:</span><span class="sxs-lookup"><span data-stu-id="e68be-174">Enter the following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="e68be-175">In alternativa, per reimpostare la chiave SSH per un utente, creare innanzitutto un file denominato `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="e68be-175">Or to reset the SSH key for a user, first create a file named `settings.json`.</span></span> <span data-ttu-id="e68be-176">L'esempio seguente reimposta le credenziali per `myUsername` sul valore specificato in `myPassword` nella macchina virtuale denominata `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e68be-176">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e68be-177">Immettere le seguenti righe nel file `settings.json` con valori personalizzati:</span><span class="sxs-lookup"><span data-stu-id="e68be-177">Enter the following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="e68be-178">Dopo aver creato il file json, usare l'interfaccia della riga di comando di Azure per chiamare l'estensione `VMAccessForLinux` per reimpostare le credenziali dell'utente SSH specificando il file json.</span><span class="sxs-lookup"><span data-stu-id="e68be-178">After creating your json file, use the Azure CLI to call the `VMAccessForLinux` extension to reset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="e68be-179">L'esempio seguente reimposta le credenziali sulla macchina virtuale denominata `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e68be-179">The following example resets credentials on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e68be-180">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="e68be-180">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-the-azure-cli-10"></a><span data-ttu-id="e68be-181">Usare l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="e68be-181">Use the Azure CLI 1.0</span></span>
<span data-ttu-id="e68be-182">Se necessario, [installare l'interfaccia della riga di comando di Azure 1.0 e connettersi alla sottoscrizione di Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e68be-182">If you haven't already, [install the Azure CLI 1.0 and connect to your Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="e68be-183">Verificare di usare la modalità di Resource Manager come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="e68be-183">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="e68be-184">Se è stata creata e caricata un'immagine del disco Linux personalizzata, verificare che sia installato l'[agente Linux di Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in versione 2.0.5 o successiva.</span><span class="sxs-lookup"><span data-stu-id="e68be-184">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="e68be-185">Per le macchine virtuali create tramite le immagini della raccolta, questa estensione dell'accesso è già installata e configurata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e68be-185">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="e68be-186">Reimpostare la configurazione SSH</span><span class="sxs-lookup"><span data-stu-id="e68be-186">Reset SSH configuration</span></span>
<span data-ttu-id="e68be-187">La configurazione del disco SSHD in sé può essere errata oppure il servizio ha rilevato un errore.</span><span class="sxs-lookup"><span data-stu-id="e68be-187">The SSHD configuration itself may be misconfigured or the service encountered an error.</span></span> <span data-ttu-id="e68be-188">È possibile reimpostare il disco SSHD per controllare la validità della configurazione SSH.</span><span class="sxs-lookup"><span data-stu-id="e68be-188">You can reset SSHD to make sure the SSH configuration itself is valid.</span></span> <span data-ttu-id="e68be-189">La reimpostazione SSHD deve essere il primo passaggio da eseguire per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="e68be-189">Resetting SSHD should be the first troubleshooting step you take.</span></span>

<span data-ttu-id="e68be-190">L'esempio seguente reimposta SSHD su una macchina virtuale denominata `myVM` nel gruppo di risorse `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e68be-190">The following example resets SSHD on a VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="e68be-191">Usare i nomi della macchina virtuale e del gruppo di risorse personalizzati come segue:</span><span class="sxs-lookup"><span data-stu-id="e68be-191">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="e68be-192">Reimpostare le credenziali SSH di un utente</span><span class="sxs-lookup"><span data-stu-id="e68be-192">Reset SSH credentials for a user</span></span>
<span data-ttu-id="e68be-193">Se il disco SSHD funziona correttamente, è possibile reimpostare la password di un determinato utente.</span><span class="sxs-lookup"><span data-stu-id="e68be-193">If SSHD appears to function correctly, you can reset the password for a giver user.</span></span> <span data-ttu-id="e68be-194">L'esempio seguente reimposta le credenziali per `myUsername` sul valore specificato in `myPassword` nella macchina virtuale denominata `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e68be-194">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e68be-195">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="e68be-195">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="e68be-196">Se si usa l'autenticazione con chiave SSH, è possibile reimpostare la chiave SSH per un determinato utente.</span><span class="sxs-lookup"><span data-stu-id="e68be-196">If using SSH key authentication, you can reset the SSH key for a given user.</span></span> <span data-ttu-id="e68be-197">L'esempio seguente aggiorna la chiave SSH archiviata in `~/.ssh/id_rsa.pub` per l'utente denominato `myUsername` nella macchina virtuale denominata `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e68be-197">The following example updates the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e68be-198">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="e68be-198">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="e68be-199">Riavviare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e68be-199">Restart a VM</span></span>
<span data-ttu-id="e68be-200">Se sono state reimpostate la configurazione SSH e le credenziali utente o si è verificato un errore durante queste operazioni, è possibile provare a riavviare la macchina virtuale per risolvere i problemi di calcolo alla base.</span><span class="sxs-lookup"><span data-stu-id="e68be-200">If you have reset the SSH configuration and user credentials, or encountered an error in doing so, you can try restarting the VM to address underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="e68be-201">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e68be-201">Azure portal</span></span>
<span data-ttu-id="e68be-202">Per riavviare una macchina virtuale dal portale di Azure, selezionare la macchina virtuale e scegliere il pulsante **Riavvia** come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e68be-202">To restart a VM using the Azure portal, select your VM and click the **Restart** button as in the following example:</span></span>

![Riavviare una macchina virtuale nel portale di Azure](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="e68be-204">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="e68be-204">Azure CLI 1.0</span></span>
<span data-ttu-id="e68be-205">L'esempio seguente riavvia la macchina virtuale denominata `myVM` nel gruppo di risorse `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e68be-205">The following example restarts the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="e68be-206">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="e68be-206">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="e68be-207">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e68be-207">Azure CLI 2.0</span></span>
<span data-ttu-id="e68be-208">L'esempio seguente usa il comando [az vm restart](/cli/azure/vm#restart) per riavviare la macchina virtuale denominata `myVM` nel gruppo di risorse denominato `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e68be-208">The following example uses [az vm restart](/cli/azure/vm#restart) to restart the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="e68be-209">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="e68be-209">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="e68be-210">Ridistribuire una VM</span><span class="sxs-lookup"><span data-stu-id="e68be-210">Redeploy a VM</span></span>
<span data-ttu-id="e68be-211">È possibile ridistribuire una VM in un altro nodo all'interno di Azure, correggendo eventuali problemi di rete sottostanti.</span><span class="sxs-lookup"><span data-stu-id="e68be-211">You can redeploy a VM to another node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="e68be-212">Per informazioni su come eseguire questa operazione, vedere [Ridistribuzione della macchina virtuale su un nuovo nodo di Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e68be-212">For information about redeploying a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="e68be-213">Al termine di questa operazione i dati temporanei del disco andranno persi e gli indirizzi IP dinamici associati alla macchina virtuale saranno aggiornati.</span><span class="sxs-lookup"><span data-stu-id="e68be-213">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="e68be-214">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e68be-214">Azure portal</span></span>
<span data-ttu-id="e68be-215">Per ridistribuire una macchina virtuale dal portale di Azure, selezionare la macchina virtuale e scorrere verso il basso fino alla sezione **Supporto e risoluzione dei problemi**.</span><span class="sxs-lookup"><span data-stu-id="e68be-215">To redeploy a VM using the Azure portal, select your VM and scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="e68be-216">Fare clic sul pulsante **Ridistribuisci** come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e68be-216">Click the **Redeploy** button as in the following example:</span></span>

![Ridistribuire una macchina virtuale nel portale di Azure](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="e68be-218">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="e68be-218">Azure CLI 1.0</span></span>
<span data-ttu-id="e68be-219">L'esempio seguente ridistribuisce la macchina virtuale denominata `myVM` nel gruppo di risorse `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e68be-219">The following example redeploys the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="e68be-220">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="e68be-220">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="e68be-221">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e68be-221">Azure CLI 2.0</span></span>
<span data-ttu-id="e68be-222">L'esempio seguente usa il comando [az vm redeploy](/cli/azure/vm#redeploy) per ridistribuire la macchina virtuale denominata `myVM` nel gruppo di risorse denominato `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e68be-222">The following example use [az vm redeploy](/cli/azure/vm#redeploy) to redeploy the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="e68be-223">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="e68be-223">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-the-classic-deployment-model"></a><span data-ttu-id="e68be-224">VM create con il modello di distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="e68be-224">VMs created by using the Classic deployment model</span></span>
<span data-ttu-id="e68be-225">Per risolvere gli errori di connessione SSH più comuni nelle VM create con il modello di distribuzione classica, provare a eseguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="e68be-225">Try these steps to resolve the most common SSH connection failures for VMs that were created by using the classic deployment model.</span></span> <span data-ttu-id="e68be-226">Dopo ogni passaggio, tentare la riconnessione alla VM.</span><span class="sxs-lookup"><span data-stu-id="e68be-226">After each step, try reconnecting to the VM.</span></span>

* <span data-ttu-id="e68be-227">Reimpostare l'accesso remoto dal [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e68be-227">Reset remote access from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e68be-228">Nel portale di Azure, selezionare la macchina virtuale e fare clic sul pulsante **Reimposta accesso remoto**.</span><span class="sxs-lookup"><span data-stu-id="e68be-228">On the Azure portal, select your VM and click the **Reset Remote...** button.</span></span>
* <span data-ttu-id="e68be-229">Riavviare la VM.</span><span class="sxs-lookup"><span data-stu-id="e68be-229">Restart the VM.</span></span> <span data-ttu-id="e68be-230">Nel [portale di Azure](https://portal.azure.com) selezionare la macchina virtuale e fare clic sul pulsante **Riavvia**.</span><span class="sxs-lookup"><span data-stu-id="e68be-230">On the [Azure portal](https://portal.azure.com), select your VM and click the **Restart** button.</span></span>
    
* <span data-ttu-id="e68be-231">Ridistribuire la VM su un nuovo nodo di Azure.</span><span class="sxs-lookup"><span data-stu-id="e68be-231">Redeploy the VM to a new Azure node.</span></span> <span data-ttu-id="e68be-232">Per informazioni su come eseguire questa operazione, vedere [Ridistribuzione della macchina virtuale su un nuovo nodo di Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e68be-232">For information about how to redeploy a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="e68be-233">Al termine di questa operazione i dati temporanei del disco andranno persi e gli indirizzi IP dinamici associati alla macchina virtuale saranno aggiornati.</span><span class="sxs-lookup"><span data-stu-id="e68be-233">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span></span>
* <span data-ttu-id="e68be-234">Seguire le istruzioni in [Come reimpostare una password o SSH per le macchine virtuali basate su Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) per:</span><span class="sxs-lookup"><span data-stu-id="e68be-234">Follow the instructions in [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="e68be-235">Reimpostare la password o la chiave SSH.</span><span class="sxs-lookup"><span data-stu-id="e68be-235">Reset the password or SSH key.</span></span>
  * <span data-ttu-id="e68be-236">Creare un account utente *sudo*.</span><span class="sxs-lookup"><span data-stu-id="e68be-236">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="e68be-237">Reimpostare la configurazione SSH.</span><span class="sxs-lookup"><span data-stu-id="e68be-237">Reset the SSH configuration.</span></span>
* <span data-ttu-id="e68be-238">Controllare l'integrità delle risorse della VM per eventuali problemi di piattaforma.</span><span class="sxs-lookup"><span data-stu-id="e68be-238">Check the VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="e68be-239">Selezionare la macchina virtuale e scorrere verso il basso fino a **Impostazioni** > **Controlla integrità**.</span><span class="sxs-lookup"><span data-stu-id="e68be-239">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e68be-240">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e68be-240">Additional resources</span></span>
* <span data-ttu-id="e68be-241">Se non si riesce ancora a eseguire la configurazione SSH sulla macchina virtuale dopo aver eseguito la relativa procedura, usare i [passaggi dettagliati per la risoluzione dei problemi](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per esaminare altre procedure per la risoluzione del problema.</span><span class="sxs-lookup"><span data-stu-id="e68be-241">If you are still unable to SSH to your VM after following the after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to review additional steps to resolve your issue.</span></span>
* <span data-ttu-id="e68be-242">Per altre informazioni sulla risoluzione dei problemi di accesso dell'applicazione, vedere [Risoluzione dei problemi di accesso a un'applicazione in esecuzione su una macchina virtuale di Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e68be-242">For more information about troubleshooting application access, see [Troubleshoot access to an application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="e68be-243">Per altre informazioni sulla risoluzione dei problemi di macchine virtuali create con il modello di distribuzione classica, vedere l'articolo su come [reimpostare una password o SSH per macchine virtuali basate su Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e68be-243">For more information about troubleshooting virtual machines that were created by using the classic deployment model, see [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

