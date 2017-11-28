---
title: problemi di connessione SSH aaaTroubleshoot tooan macchina virtuale di Azure | Documenti Microsoft
description: Come tootroubleshoot problemi, ad esempio 'Connessione SSH non riuscito' o 'Connessione SSH rifiutata' per una macchina virtuale di Azure che eseguono Linux.
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
ms.openlocfilehash: dfb4e75e571c8306edf5f300c4e0f07a5fe7750a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="92aed-104">Risoluzione dei problemi tooan connessioni SSH VM Linux di Azure non riesce, gli errori, che è stata rifiutata</span><span class="sxs-lookup"><span data-stu-id="92aed-104">Troubleshoot SSH connections tooan Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="92aed-105">Esistono vari motivi che si verificano errori di Secure Shell (SSH), gli errori di connessione SSH o SSH viene rifiutato quando si tenta di macchina virtuale di Linux tooa tooconnect (VM).</span><span class="sxs-lookup"><span data-stu-id="92aed-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try tooconnect tooa Linux virtual machine (VM).</span></span> <span data-ttu-id="92aed-106">In questo articolo consente di trovare e problemi di hello corretto.</span><span class="sxs-lookup"><span data-stu-id="92aed-106">This article helps you find and correct hello problems.</span></span> <span data-ttu-id="92aed-107">È possibile utilizzare hello portale di Azure CLI di Azure o estensione accesso della macchina virtuale per Linux tootroubleshoot e risolvere i problemi di connessione.</span><span class="sxs-lookup"><span data-stu-id="92aed-107">You can use hello Azure portal, Azure CLI, or VM Access Extension for Linux tootroubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="92aed-108">Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti in [hello forum MSDN di Azure e di Overflow dello Stack](http://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="92aed-108">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="92aed-109">In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="92aed-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="92aed-110">Passare toohello [sito del supporto tecnico di Azure](http://azure.microsoft.com/support/options/) e selezionare **ottenere supporto**.</span><span class="sxs-lookup"><span data-stu-id="92aed-110">Go toohello [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="92aed-111">Per informazioni sull'utilizzo di supporto di Azure, leggere hello [supporto tecnico di Microsoft Azure domande frequenti su](http://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="92aed-111">For information about using Azure Support, read hello [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="92aed-112">Passaggi rapidi per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="92aed-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="92aed-113">Dopo ogni passaggio della risoluzione dei problemi, provare a riconnettersi toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="92aed-113">After each troubleshooting step, try reconnecting toohello VM.</span></span>

1. <span data-ttu-id="92aed-114">Reimposta configurazione SSH hello.</span><span class="sxs-lookup"><span data-stu-id="92aed-114">Reset hello SSH configuration.</span></span>
2. <span data-ttu-id="92aed-115">Reimpostare le credenziali di hello per utente hello.</span><span class="sxs-lookup"><span data-stu-id="92aed-115">Reset hello credentials for hello user.</span></span>
3. <span data-ttu-id="92aed-116">Verificare hello [Network Security Group](../../virtual-network/virtual-networks-nsg.md) regole consentono il traffico SSH.</span><span class="sxs-lookup"><span data-stu-id="92aed-116">Verify hello [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="92aed-117">Verificare che una regola del gruppo di sicurezza di rete esista traffico SSH toopermit (per impostazione predefinita, la porta TCP 22).</span><span class="sxs-lookup"><span data-stu-id="92aed-117">Ensure that a Network Security Group rule exists toopermit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="92aed-118">Non è possibile usare il reindirizzamento o mapping delle porte senza usare Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="92aed-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="92aed-119">Controllare hello [integrità delle risorse di VM](../../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="92aed-119">Check hello [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="92aed-120">Verificare che hello VM report come integro.</span><span class="sxs-lookup"><span data-stu-id="92aed-120">Ensure that hello VM reports as being healthy.</span></span>
   * <span data-ttu-id="92aed-121">Se è abilitata la diagnostica di avvio, verificare gli errori di avvio nei registri hello hello VM non è in corso.</span><span class="sxs-lookup"><span data-stu-id="92aed-121">If you have boot diagnostics enabled, verify hello VM is not reporting boot errors in hello logs.</span></span>
5. <span data-ttu-id="92aed-122">Riavviare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="92aed-122">Restart hello VM.</span></span>
6. <span data-ttu-id="92aed-123">Ridistribuire hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="92aed-123">Redeploy hello VM.</span></span>

<span data-ttu-id="92aed-124">Continuare la lettura per la procedura di risoluzione dei problemi e spiegazioni più dettagliate.</span><span class="sxs-lookup"><span data-stu-id="92aed-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a><span data-ttu-id="92aed-125">Problemi di connessione SSH tootroubleshoot metodi disponibili</span><span class="sxs-lookup"><span data-stu-id="92aed-125">Available methods tootroubleshoot SSH connection issues</span></span>
<span data-ttu-id="92aed-126">È possibile reimpostare le credenziali o la configurazione SSH utilizzando uno dei seguenti metodi hello:</span><span class="sxs-lookup"><span data-stu-id="92aed-126">You can reset credentials or SSH configuration using one of hello following methods:</span></span>

* <span data-ttu-id="92aed-127">[Portale di Azure](#use-the-azure-portal) : eccellente se è necessario tooquickly Reimposta configurazione SSH hello o chiave SSH e non avere hello installati gli strumenti di Azure.</span><span class="sxs-lookup"><span data-stu-id="92aed-127">[Azure portal](#use-the-azure-portal) - great if you need tooquickly reset hello SSH configuration or SSH key and you don't have hello Azure tools installed.</span></span>
* <span data-ttu-id="92aed-128">[Azure CLI 2.0](#use-the-azure-cli-20) : se sono già nella riga di comando hello rapidamente la reimpostazione della configurazione di SSH hello o le credenziali.</span><span class="sxs-lookup"><span data-stu-id="92aed-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on hello command line, quickly reset hello SSH configuration or credentials.</span></span> <span data-ttu-id="92aed-129">È inoltre possibile utilizzare hello [1.0 CLI di Azure](#use-the-azure-cli-10)</span><span class="sxs-lookup"><span data-stu-id="92aed-129">You can also use hello [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="92aed-130">[L'estensione VMAccessForLinux Azure](#use-the-vmaccess-extension) : creare e riutilizzare json definizione file tooreset hello SSH configurazione o credenziali dell'utente.</span><span class="sxs-lookup"><span data-stu-id="92aed-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files tooreset hello SSH configuration or user credentials.</span></span>

<span data-ttu-id="92aed-131">Dopo ogni passaggio della risoluzione dei problemi, provare a riconnettersi tooyour macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="92aed-131">After each troubleshooting step, try connecting tooyour VM again.</span></span> <span data-ttu-id="92aed-132">Se non è possibile connettersi, provare a passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="92aed-132">If you still cannot connect, try hello next step.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="92aed-133">Utilizzare hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="92aed-133">Use hello Azure portal</span></span>
<span data-ttu-id="92aed-134">Hello portale di Azure fornisce un hello tooreset rapidamente le credenziali utente o di configurazione di SSH senza installare gli strumenti nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="92aed-134">hello Azure portal provides a quick way tooreset hello SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="92aed-135">Selezionare la macchina virtuale nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="92aed-135">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="92aed-136">Scorrere verso il basso toohello **supporto + Troubleshooting** sezione e selezionare **reimpostazione password** come hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="92aed-136">Scroll down toohello **Support + Troubleshooting** section and select **Reset password** as in hello following example:</span></span>

![Configurazione SSH per la reimpostazione o credenziali nel portale di Azure hello](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a><span data-ttu-id="92aed-138">Reimposta configurazione SSH hello</span><span class="sxs-lookup"><span data-stu-id="92aed-138">Reset hello SSH configuration</span></span>
<span data-ttu-id="92aed-139">Come primo passaggio, selezionare `Reset configuration only` da hello **modalità** dal menu a discesa in hello precedente schermata, quindi fare clic su hello **reimpostare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="92aed-139">As a first step, select `Reset configuration only` from hello **Mode** drop-down menu as in hello preceding screenshot, then click hello **Reset** button.</span></span> <span data-ttu-id="92aed-140">Una volta completata questa azione, riprovare tooaccess la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="92aed-140">Once this action has completed, try tooaccess your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="92aed-141">Reimpostare le credenziali SSH di un utente</span><span class="sxs-lookup"><span data-stu-id="92aed-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="92aed-142">le credenziali di hello tooreset di un utente esistente, selezionare l'opzione `Reset SSH public key` o `Reset password` da hello **modalità** dal menu a discesa come hello precedente schermata.</span><span class="sxs-lookup"><span data-stu-id="92aed-142">tooreset hello credentials of an existing user, select either `Reset SSH public key` or `Reset password` from hello **Mode** drop-down menu as in hello preceding screenshot.</span></span> <span data-ttu-id="92aed-143">Specificare nome utente di hello e una chiave SSH o nuova password, quindi fare clic su hello **reimpostare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="92aed-143">Specify hello username and an SSH key or new password, then click hello **Reset** button.</span></span>

<span data-ttu-id="92aed-144">È anche possibile creare un utente con privilegi sudo su hello VM da questo menu.</span><span class="sxs-lookup"><span data-stu-id="92aed-144">You can also create a user with sudo privileges on hello VM from this menu.</span></span> <span data-ttu-id="92aed-145">Immettere un nuovo nome utente e password associata o una chiave SSH e quindi fare clic su hello **reimpostare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="92aed-145">Enter a new username and associated password or SSH key, and then click hello **Reset** button.</span></span>

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="92aed-146">Utilizzare hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="92aed-146">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="92aed-147">Se hai già fatto, installare più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) e accedere con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="92aed-147">If you haven't already, install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="92aed-148">Se è stato creato e caricato un'immagine del disco Linux personalizzata, verificare che hello [agente Linux di Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versione 2.0.5 o versione successiva è installato.</span><span class="sxs-lookup"><span data-stu-id="92aed-148">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="92aed-149">Per le macchine virtuali create tramite le immagini della raccolta, questa estensione dell'accesso è già installata e configurata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="92aed-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="92aed-150">Reimpostare la configurazione SSH</span><span class="sxs-lookup"><span data-stu-id="92aed-150">Reset SSH configuration</span></span>
<span data-ttu-id="92aed-151">È possibile inizialmente try reimpostazione hello SSH toodefault i valori di configurazione e il riavvio server SSH hello hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="92aed-151">You can initially try resetting hello SSH configuration toodefault values and rebooting hello SSH server on hello VM.</span></span> <span data-ttu-id="92aed-152">Si noti che ciò non modifica il nome di account utente di hello, password o le chiavi SSH.</span><span class="sxs-lookup"><span data-stu-id="92aed-152">Note that this does not change hello user account name, password, or SSH keys.</span></span>
<span data-ttu-id="92aed-153">Hello seguente utilizza [az vm utente reset-ssh](/cli/azure/vm/user#reset-ssh) tooreset hello SSH configurazione macchina virtuale denominata hello `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="92aed-153">hello following example uses [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) tooreset hello SSH configuration on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="92aed-154">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="92aed-154">Use your own values as follows:</span></span>

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="92aed-155">Reimpostare le credenziali SSH di un utente</span><span class="sxs-lookup"><span data-stu-id="92aed-155">Reset SSH credentials for a user</span></span>
<span data-ttu-id="92aed-156">Hello seguente utilizza [aggiornamento dell'utente vm az](/cli/azure/vm/user#update) tooreset hello le credenziali per `myUsername` toohello valore specificato in `myPassword`, nella macchina virtuale denominata hello `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="92aed-156">hello following example uses [az vm user update](/cli/azure/vm/user#update) tooreset hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="92aed-157">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="92aed-157">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="92aed-158">Se si utilizza l'autenticazione con chiave SSH, è possibile reimpostare la chiave SSH hello per un determinato utente.</span><span class="sxs-lookup"><span data-stu-id="92aed-158">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="92aed-159">Hello seguente utilizza **az vm accesso utente di linux set** tooupdate hello SSH chiave archiviata in `~/.ssh/id_rsa.pub` per utente hello denominato `myUsername`, nella macchina virtuale denominata hello `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="92aed-159">hello following example uses **az vm access set-linux-user** tooupdate hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="92aed-160">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="92aed-160">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a><span data-ttu-id="92aed-161">Utilizzare l'estensione VMAccess hello</span><span class="sxs-lookup"><span data-stu-id="92aed-161">Use hello VMAccess extension</span></span>
<span data-ttu-id="92aed-162">legge un file json che definisce le azioni toocarry out Hello estensione accesso della macchina virtuale per Linux. Queste azioni includono la reimpostazione SSHD, la reimpostazione di una chiave SSH o l'aggiunta di un utente.</span><span class="sxs-lookup"><span data-stu-id="92aed-162">hello VM Access Extension for Linux reads in a json file that defines actions toocarry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="92aed-163">È comunque usare hello toocall di hello Azure CLI estensione VMAccess, ma è possibile riutilizzare i file json hello in più macchine virtuali se lo si desidera.</span><span class="sxs-lookup"><span data-stu-id="92aed-163">You still use hello Azure CLI toocall hello VMAccess extension, but you can reuse hello json files across multiple VMs if desired.</span></span> <span data-ttu-id="92aed-164">Questo approccio consente toocreate un archivio di file json che può essere chiamato per specificato scenari.</span><span class="sxs-lookup"><span data-stu-id="92aed-164">This approach allows you toocreate a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="92aed-165">Reimpostare un disco SSHD</span><span class="sxs-lookup"><span data-stu-id="92aed-165">Reset SSHD</span></span>
<span data-ttu-id="92aed-166">Creare un file denominato `settings.json` con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="92aed-166">Create a file named `settings.json` with hello following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="92aed-167">Utilizzando hello CLI di Azure, è possibile quindi chiamare hello `VMAccessForLinux` estensione tooreset connessione SSHD specificando il file json.</span><span class="sxs-lookup"><span data-stu-id="92aed-167">Using hello Azure CLI, you then call hello `VMAccessForLinux` extension tooreset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="92aed-168">Hello seguente utilizza [az vm estensione set](/cli/azure/vm/extension#set) tooreset SSHD nella macchina virtuale denominata hello `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="92aed-168">hello following example uses [az vm extension set](/cli/azure/vm/extension#set) tooreset SSHD on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="92aed-169">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="92aed-169">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="92aed-170">Reimpostare le credenziali SSH di un utente</span><span class="sxs-lookup"><span data-stu-id="92aed-170">Reset SSH credentials for a user</span></span>
<span data-ttu-id="92aed-171">Se SSHD toofunction venga visualizzato correttamente, è possibile reimpostare le credenziali di hello per un utente donatore.</span><span class="sxs-lookup"><span data-stu-id="92aed-171">If SSHD appears toofunction correctly, you can reset hello credentials for a giver user.</span></span> <span data-ttu-id="92aed-172">password di hello tooreset per un utente, creare un file denominato `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="92aed-172">tooreset hello password for a user, create a file named `settings.json`.</span></span> <span data-ttu-id="92aed-173">esempio Hello Reimposta credenziali hello per `myUsername` toohello valore specificato in `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="92aed-173">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`.</span></span> <span data-ttu-id="92aed-174">Immettere hello righe in seguito il `settings.json` file, utilizzando i valori personalizzati:</span><span class="sxs-lookup"><span data-stu-id="92aed-174">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="92aed-175">O tooreset hello chiave SSH per un utente, creare innanzitutto un file denominato `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="92aed-175">Or tooreset hello SSH key for a user, first create a file named `settings.json`.</span></span> <span data-ttu-id="92aed-176">esempio Hello Reimposta credenziali hello per `myUsername` toohello valore specificato in `myPassword`, nella macchina virtuale denominata hello `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="92aed-176">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="92aed-177">Immettere hello righe in seguito il `settings.json` file, utilizzando i valori personalizzati:</span><span class="sxs-lookup"><span data-stu-id="92aed-177">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="92aed-178">Dopo avere creato il file json, utilizzare hello toocall CLI di Azure di hello `VMAccessForLinux` tooreset estensione le credenziali dell'utente SSH specificando il file json.</span><span class="sxs-lookup"><span data-stu-id="92aed-178">After creating your json file, use hello Azure CLI toocall hello `VMAccessForLinux` extension tooreset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="92aed-179">esempio Hello Reimposta credenziali sulla macchina virtuale denominata hello `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="92aed-179">hello following example resets credentials on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="92aed-180">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="92aed-180">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="92aed-181">Utilizzare hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="92aed-181">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="92aed-182">Se hai già fatto, [installare hello Azure CLI 1.0 e connettere tooyour sottoscrizione di Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="92aed-182">If you haven't already, [install hello Azure CLI 1.0 and connect tooyour Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="92aed-183">Verificare di usare la modalità di Resource Manager come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="92aed-183">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="92aed-184">Se è stato creato e caricato un'immagine del disco Linux personalizzata, verificare che hello [agente Linux di Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versione 2.0.5 o versione successiva è installato.</span><span class="sxs-lookup"><span data-stu-id="92aed-184">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="92aed-185">Per le macchine virtuali create tramite le immagini della raccolta, questa estensione dell'accesso è già installata e configurata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="92aed-185">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="92aed-186">Reimpostare la configurazione SSH</span><span class="sxs-lookup"><span data-stu-id="92aed-186">Reset SSH configuration</span></span>
<span data-ttu-id="92aed-187">configurazione di SSHD Hello stessa sia configurato correttamente o hello servizio ha rilevato un errore.</span><span class="sxs-lookup"><span data-stu-id="92aed-187">hello SSHD configuration itself may be misconfigured or hello service encountered an error.</span></span> <span data-ttu-id="92aed-188">È possibile reimpostare toomake SSHD che configurazione SSH hello stesso sia valido.</span><span class="sxs-lookup"><span data-stu-id="92aed-188">You can reset SSHD toomake sure hello SSH configuration itself is valid.</span></span> <span data-ttu-id="92aed-189">Reimpostazione SSHD deve essere hello sulla risoluzione dei problemi innanzitutto che eseguire.</span><span class="sxs-lookup"><span data-stu-id="92aed-189">Resetting SSHD should be hello first troubleshooting step you take.</span></span>

<span data-ttu-id="92aed-190">esempio Hello Reimposta SSHD in una macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="92aed-190">hello following example resets SSHD on a VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="92aed-191">Usare i nomi della macchina virtuale e del gruppo di risorse personalizzati come segue:</span><span class="sxs-lookup"><span data-stu-id="92aed-191">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="92aed-192">Reimpostare le credenziali SSH di un utente</span><span class="sxs-lookup"><span data-stu-id="92aed-192">Reset SSH credentials for a user</span></span>
<span data-ttu-id="92aed-193">Se SSHD toofunction venga visualizzato correttamente, è possibile reimpostare la password di hello per un utente donatore.</span><span class="sxs-lookup"><span data-stu-id="92aed-193">If SSHD appears toofunction correctly, you can reset hello password for a giver user.</span></span> <span data-ttu-id="92aed-194">esempio Hello Reimposta credenziali hello per `myUsername` toohello valore specificato in `myPassword`, nella macchina virtuale denominata hello `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="92aed-194">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="92aed-195">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="92aed-195">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="92aed-196">Se si utilizza l'autenticazione con chiave SSH, è possibile reimpostare la chiave SSH hello per un determinato utente.</span><span class="sxs-lookup"><span data-stu-id="92aed-196">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="92aed-197">dopo gli aggiornamenti di esempio Hello hello chiave SSH archiviata in `~/.ssh/id_rsa.pub` per utente hello denominato `myUsername`, nella macchina virtuale denominata hello `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="92aed-197">hello following example updates hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="92aed-198">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="92aed-198">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="92aed-199">Riavviare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="92aed-199">Restart a VM</span></span>
<span data-ttu-id="92aed-200">Se si hanno reimpostare le credenziali di configurazione e dell'utente SSH hello o ha rilevato un errore in tal modo, è possibile provare a riavviare hello VM tooaddress sottostanti i problemi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="92aed-200">If you have reset hello SSH configuration and user credentials, or encountered an error in doing so, you can try restarting hello VM tooaddress underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="92aed-201">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="92aed-201">Azure portal</span></span>
<span data-ttu-id="92aed-202">toorestart una macchina virtuale utilizzando hello Azure selezionare portale, hello la macchina virtuale e fare clic su **riavviare** pulsante come hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="92aed-202">toorestart a VM using hello Azure portal, select your VM and click hello **Restart** button as in hello following example:</span></span>

![Riavviare una macchina virtuale nel portale di Azure hello](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="92aed-204">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="92aed-204">Azure CLI 1.0</span></span>
<span data-ttu-id="92aed-205">Dopo il riavvio di esempio Hello hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="92aed-205">hello following example restarts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="92aed-206">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="92aed-206">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="92aed-207">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="92aed-207">Azure CLI 2.0</span></span>
<span data-ttu-id="92aed-208">Hello seguente utilizza [riavvio vm az](/cli/azure/vm#restart) toorestart hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="92aed-208">hello following example uses [az vm restart](/cli/azure/vm#restart) toorestart hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="92aed-209">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="92aed-209">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="92aed-210">Ridistribuire una VM</span><span class="sxs-lookup"><span data-stu-id="92aed-210">Redeploy a VM</span></span>
<span data-ttu-id="92aed-211">È possibile ridistribuire un nodo tooanother della macchina virtuale in Azure, che può correggere eventuali problemi di rete sottostante.</span><span class="sxs-lookup"><span data-stu-id="92aed-211">You can redeploy a VM tooanother node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="92aed-212">Per informazioni sulla ridistribuzione di una macchina virtuale, vedere [ridistribuire toonew macchina virtuale Azure nodo](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="92aed-212">For information about redeploying a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="92aed-213">Al termine di questa operazione, dati su disco temporaneo andranno persi e verranno aggiornati gli indirizzi IP dinamici che sono associati a macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="92aed-213">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="92aed-214">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="92aed-214">Azure portal</span></span>
<span data-ttu-id="92aed-215">tooredeploy una macchina virtuale utilizzando hello Azure selezionare portale, la macchina virtuale e scorrere verso il basso toohello **supporto + Troubleshooting** sezione.</span><span class="sxs-lookup"><span data-stu-id="92aed-215">tooredeploy a VM using hello Azure portal, select your VM and scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="92aed-216">Fare clic su hello **ridistribuire** pulsante come hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="92aed-216">Click hello **Redeploy** button as in hello following example:</span></span>

![Ridistribuire una macchina virtuale in hello portale di Azure](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="92aed-218">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="92aed-218">Azure CLI 1.0</span></span>
<span data-ttu-id="92aed-219">Hello seguenti distribuzioni di esempio hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="92aed-219">hello following example redeploys hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="92aed-220">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="92aed-220">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="92aed-221">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="92aed-221">Azure CLI 2.0</span></span>
<span data-ttu-id="92aed-222">Hello in seguito ad esempio [Ridistribuisci vm az](/cli/azure/vm#redeploy) tooredeploy hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="92aed-222">hello following example use [az vm redeploy](/cli/azure/vm#redeploy) tooredeploy hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="92aed-223">Usare i valori personalizzati come di seguito:</span><span class="sxs-lookup"><span data-stu-id="92aed-223">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a><span data-ttu-id="92aed-224">Macchine virtuali create con modello di distribuzione classica hello</span><span class="sxs-lookup"><span data-stu-id="92aed-224">VMs created by using hello Classic deployment model</span></span>
<span data-ttu-id="92aed-225">Ripetere questi passaggi tooresolve hello più comuni SSH errori di connessione per le macchine virtuali che sono state create tramite il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="92aed-225">Try these steps tooresolve hello most common SSH connection failures for VMs that were created by using hello classic deployment model.</span></span> <span data-ttu-id="92aed-226">Dopo ogni passaggio, provare a riconnettersi toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="92aed-226">After each step, try reconnecting toohello VM.</span></span>

* <span data-ttu-id="92aed-227">Reimpostare l'accesso remoto da hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="92aed-227">Reset remote access from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="92aed-228">Hello portale di Azure, selezionare la macchina virtuale e fare clic su hello **Reimposta accesso remoto...**  pulsante.</span><span class="sxs-lookup"><span data-stu-id="92aed-228">On hello Azure portal, select your VM and click hello **Reset Remote...** button.</span></span>
* <span data-ttu-id="92aed-229">Riavviare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="92aed-229">Restart hello VM.</span></span> <span data-ttu-id="92aed-230">In hello [portale di Azure](https://portal.azure.com), selezionare la macchina virtuale e fare clic su hello **riavviare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="92aed-230">On hello [Azure portal](https://portal.azure.com), select your VM and click hello **Restart** button.</span></span>
    
* <span data-ttu-id="92aed-231">Ridistribuire hello VM tooa nuovo nodo di Azure.</span><span class="sxs-lookup"><span data-stu-id="92aed-231">Redeploy hello VM tooa new Azure node.</span></span> <span data-ttu-id="92aed-232">Per informazioni su come tooredeploy una macchina virtuale, vedere [ridistribuire toonew macchina virtuale Azure nodo](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="92aed-232">For information about how tooredeploy a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="92aed-233">Al termine di questa operazione, dati su disco temporaneo andranno persi e verranno aggiornati gli indirizzi IP dinamici che sono associati a macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="92aed-233">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
* <span data-ttu-id="92aed-234">Seguire le istruzioni hello [come tooreset una password o SSH per le macchine virtuali basate su Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) per:</span><span class="sxs-lookup"><span data-stu-id="92aed-234">Follow hello instructions in [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="92aed-235">Hello di reimpostazione password o chiave SSH.</span><span class="sxs-lookup"><span data-stu-id="92aed-235">Reset hello password or SSH key.</span></span>
  * <span data-ttu-id="92aed-236">Creare un account utente *sudo*.</span><span class="sxs-lookup"><span data-stu-id="92aed-236">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="92aed-237">Reimposta configurazione SSH hello.</span><span class="sxs-lookup"><span data-stu-id="92aed-237">Reset hello SSH configuration.</span></span>
* <span data-ttu-id="92aed-238">Controllare l'integrità delle risorse della macchina virtuale di hello per eventuali problemi della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="92aed-238">Check hello VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="92aed-239">Selezionare la macchina virtuale e scorrere verso il basso fino a **Impostazioni** > **Controlla integrità**.</span><span class="sxs-lookup"><span data-stu-id="92aed-239">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92aed-240">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="92aed-240">Additional resources</span></span>
* <span data-ttu-id="92aed-241">Se si riesce ancora tooSSH tooyour VM dopo seguente hello dopo i passaggi, vedere [ulteriori passaggi di risoluzione dei problemi](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview ulteriori passaggi tooresolve il problema.</span><span class="sxs-lookup"><span data-stu-id="92aed-241">If you are still unable tooSSH tooyour VM after following hello after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview additional steps tooresolve your issue.</span></span>
* <span data-ttu-id="92aed-242">Per ulteriori informazioni sulla risoluzione dei problemi di accesso all'applicazione, vedere [applicazione tooan accesso di risoluzione dei problemi in esecuzione in una macchina virtuale di Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="92aed-242">For more information about troubleshooting application access, see [Troubleshoot access tooan application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="92aed-243">Per ulteriori informazioni sulla risoluzione dei problemi delle macchine virtuali che sono state create tramite il modello di distribuzione classica hello, vedere [come tooreset una password o SSH per le macchine virtuali basate su Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="92aed-243">For more information about troubleshooting virtual machines that were created by using hello classic deployment model, see [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

