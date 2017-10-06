---
title: Desktop remoto di aaaUse tooa VM Linux di Azure | Documenti Microsoft
description: Informazioni su come tooinstall e configurare Desktop remoto (xrdp) tooconnect tooa VM Linux in Azure tramite strumenti grafici
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: iainfou
ms.openlocfilehash: 64d30be101ceeb49fc05bb10293ad63db358efe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a><span data-ttu-id="3477e-103">Installare e configurare Desktop remoto tooconnect tooa VM Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="3477e-103">Install and configure Remote Desktop tooconnect tooa Linux VM in Azure</span></span>
<span data-ttu-id="3477e-104">Le macchine virtuali Linux (VM) in Azure vengono solitamente gestite dalla riga di comando hello utilizzando una connessione sicura shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="3477e-104">Linux virtual machines (VMs) in Azure are usually managed from hello command line using a secure shell (SSH) connection.</span></span> <span data-ttu-id="3477e-105">Quando tooLinux nuovo, o per gli scenari di risoluzione dei problemi veloci, può risultare più semplice utilizzare hello di desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="3477e-105">When new tooLinux, or for quick troubleshooting scenarios, hello use of remote desktop may be easier.</span></span> <span data-ttu-id="3477e-106">Questo articolo come dettagli tooinstall e configurare un ambiente desktop ([xfce](https://www.xfce.org)) e desktop remoto ([xrdp](http://www.xrdp.org)) per le VM Linux con modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="3477e-106">This article details how tooinstall and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp.org)) for your Linux VM using hello Resource Manager deployment model.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="3477e-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3477e-107">Prerequisites</span></span>
<span data-ttu-id="3477e-108">Questo articolo richiede l'esistenza di una VM Linux di Azure.</span><span class="sxs-lookup"><span data-stu-id="3477e-108">This article requires an existing Linux VM in Azure.</span></span> <span data-ttu-id="3477e-109">Se è necessario toocreate una macchina virtuale, utilizzare uno dei seguenti metodi hello:</span><span class="sxs-lookup"><span data-stu-id="3477e-109">If you need toocreate a VM, use one of hello following methods:</span></span>

- <span data-ttu-id="3477e-110">Hello [CLI di Azure 2.0](quick-create-cli.md)</span><span class="sxs-lookup"><span data-stu-id="3477e-110">hello [Azure CLI 2.0](quick-create-cli.md)</span></span>
- <span data-ttu-id="3477e-111">Hello [portale di Azure](quick-create-portal.md)</span><span class="sxs-lookup"><span data-stu-id="3477e-111">hello [Azure portal](quick-create-portal.md)</span></span>


## <a name="install-a-desktop-environment-on-your-linux-vm"></a><span data-ttu-id="3477e-112">Installare un ambiente desktop nella VM Linux</span><span class="sxs-lookup"><span data-stu-id="3477e-112">Install a desktop environment on your Linux VM</span></span>
<span data-ttu-id="3477e-113">La maggior parte delle macchine virtuali Linux di Azure non presenta un ambiente desktop installato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="3477e-113">Most Linux VMs in Azure do not have a desktop environment installed by default.</span></span> <span data-ttu-id="3477e-114">Le macchine virtuali Linux in genere vengono gestite usando connessioni SSH piuttosto che un ambiente desktop.</span><span class="sxs-lookup"><span data-stu-id="3477e-114">Linux VMs are commonly managed using SSH connections rather than a desktop environment.</span></span> <span data-ttu-id="3477e-115">In Linux esistono diversi ambienti desktop tra i quali è possibile scegliere.</span><span class="sxs-lookup"><span data-stu-id="3477e-115">There are various desktop environments in Linux that you can choose.</span></span> <span data-ttu-id="3477e-116">A seconda della scelta effettuata dell'ambiente desktop, potrebbe utilizzi uno too2 GB di spazio su disco, richiedere 5 too10 minuti tooinstall e configurare tutti i pacchetti hello necessario.</span><span class="sxs-lookup"><span data-stu-id="3477e-116">Depending on your choice of desktop environment, it may consume one too2 GB of disk space, and take 5 too10 minutes tooinstall and configure all hello required packages.</span></span>

<span data-ttu-id="3477e-117">esempio Hello installa lightweight hello [xfce4](https://www.xfce.org/) ambiente desktop in una VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="3477e-117">hello following example installs hello lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span></span> <span data-ttu-id="3477e-118">I comandi per altre distribuzioni variano leggermente (utilizzare `yum` tooinstall su Red Hat Enterprise Linux e configurare appropriato `selinux` regole o utilizzare `zypper` tooinstall in SUSE, ad esempio).</span><span class="sxs-lookup"><span data-stu-id="3477e-118">Commands for other distributions vary slightly (use `yum` tooinstall on Red Hat Enterprise Linux and configure appropriate `selinux` rules, or use `zypper` tooinstall on SUSE, for example).</span></span>

<span data-ttu-id="3477e-119">Prima di tutto, SSH tooyour macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3477e-119">First, SSH tooyour VM.</span></span> <span data-ttu-id="3477e-120">esempio Hello connette toohello macchina virtuale denominata *myvm.westus.cloudapp.azure.com* con il nome utente hello di *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="3477e-120">hello following example connects toohello VM named *myvm.westus.cloudapp.azure.com* with hello username of *azureuser*:</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="3477e-121">Se si utilizza Windows e altre informazioni sull'uso di SSH, vedere [come chiavi, toouse SSH tramite Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="3477e-121">If you are using Windows and need more information on using SSH, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

<span data-ttu-id="3477e-122">Successivamente, installare xfce usando `apt` come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3477e-122">Next, install xfce using `apt` as follows:</span></span>

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a><span data-ttu-id="3477e-123">Installare e configurare un server di desktop remoto</span><span class="sxs-lookup"><span data-stu-id="3477e-123">Install and configure a remote desktop server</span></span>
<span data-ttu-id="3477e-124">Dopo aver creato un ambiente desktop installato, è possibile configurare un toolisten di servizi desktop remoto per le connessioni in ingresso.</span><span class="sxs-lookup"><span data-stu-id="3477e-124">Now that you have a desktop environment installed, configure a remote desktop service toolisten for incoming connections.</span></span> <span data-ttu-id="3477e-125">[xrdp](http://xrdp.org) è un server Remote Desktop Protocol (RDP) open source che è disponibile nella maggior parte delle distribuzioni Linux e funziona bene con xfce.</span><span class="sxs-lookup"><span data-stu-id="3477e-125">[xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce.</span></span> <span data-ttu-id="3477e-126">Installare xrdp nella VM Ubuntu come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3477e-126">Install xrdp on your Ubuntu VM as follows:</span></span>

```bash
sudo apt-get install xrdp
```

<span data-ttu-id="3477e-127">Indicare xrdp quali toouse ambiente desktop quando si avvia la sessione.</span><span class="sxs-lookup"><span data-stu-id="3477e-127">Tell xrdp what desktop environment toouse when you start your session.</span></span> <span data-ttu-id="3477e-128">Configurare xrdp toouse xfce come ambiente di desktop come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3477e-128">Configure xrdp toouse xfce as your desktop environment as follows:</span></span>

```bash
echo xfce4-session >~/.xsession
```

<span data-ttu-id="3477e-129">Riavviare servizio xrdp hello per effetto di hello modifiche tootake come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3477e-129">Restart hello xrdp service for hello changes tootake effect as follows:</span></span>

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a><span data-ttu-id="3477e-130">Impostare una password per l'account utente locale</span><span class="sxs-lookup"><span data-stu-id="3477e-130">Set a local user account password</span></span>
<span data-ttu-id="3477e-131">Se la password dell'account utente è stata impostata al momento della creazione della macchina virtuale, ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="3477e-131">If you created a password for your user account when you created your VM, skip this step.</span></span> <span data-ttu-id="3477e-132">Se solo di utilizzare l'autenticazione con chiave SSH e password di un account locale non è impostato, specificare una password prima di utilizzare xrdp toolog tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="3477e-132">If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp toolog in tooyour VM.</span></span> <span data-ttu-id="3477e-133">xrdp non può accettare chiavi SSH per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="3477e-133">xrdp cannot accept SSH keys for authentication.</span></span> <span data-ttu-id="3477e-134">esempio Hello specifica una password per l'account utente di hello *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="3477e-134">hello following example specifies a password for hello user account *azureuser*:</span></span>

```bash
sudo passwd azureuser
```

> [!NOTE]
> <span data-ttu-id="3477e-135">Specificare una password non aggiorna gli account di accesso delle password SSHD configurazione toopermit se attualmente non.</span><span class="sxs-lookup"><span data-stu-id="3477e-135">Specifying a password does not update your SSHD configuration toopermit password logins if it currently does not.</span></span> <span data-ttu-id="3477e-136">Da una prospettiva di sicurezza, è possibile desidera tooconnect tooyour macchina virtuale con un tunnel SSH utilizzando l'autenticazione basata su chiavi e quindi connettersi tooxrdp.</span><span class="sxs-lookup"><span data-stu-id="3477e-136">From a security perspective, you may wish tooconnect tooyour VM with an SSH tunnel using key-based authentication and then connect tooxrdp.</span></span> <span data-ttu-id="3477e-137">In questo caso, ignorare hello successivo passaggio nella creazione di un protezione gruppo regola tooallow remote desktop il traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="3477e-137">If so, skip hello following step on creating a network security group rule tooallow remote desktop traffic.</span></span>


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a><span data-ttu-id="3477e-138">Creare una regola del gruppo di sicurezza di rete per il traffico di Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="3477e-138">Create a Network Security Group rule for Remote Desktop traffic</span></span>
<span data-ttu-id="3477e-139">tooallow Desktop remoto traffico tooreach VM Linux, una regola gruppo di sicurezza di rete deve toobe creato che consenta il traffico TCP nella porta 3389 tooreach la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3477e-139">tooallow Remote Desktop traffic tooreach your Linux VM, a network security group rule needs toobe created that allows TCP on port 3389 tooreach your VM.</span></span> <span data-ttu-id="3477e-140">Per altre informazioni sulle regole dei gruppi di sicurezza di rete, vedere [Che cos'è un gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3477e-140">For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> <span data-ttu-id="3477e-141">È anche possibile [utilizzare una regola gruppo di sicurezza di rete di Azure toocreate portale hello](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3477e-141">You can also [use hello Azure portal toocreate a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="3477e-142">Negli esempi seguenti Hello creano una regola gruppo di sicurezza di rete con [creare una regola gruppo rete az](/cli/azure/network/nsg/rule#create) denominato *myNetworkSecurityGroupRule* troppo*consentire* traffico su *tcp* porta *3389*.</span><span class="sxs-lookup"><span data-stu-id="3477e-142">hello following examples create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) named *myNetworkSecurityGroupRule* too*allow* traffic on *tcp* port *3389*.</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a><span data-ttu-id="3477e-143">Connettere la macchina virtuale Linux con un client di Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="3477e-143">Connect your Linux VM with a Remote Desktop client</span></span>
<span data-ttu-id="3477e-144">Aprire il client desktop remoto locale e connettersi toohello l'indirizzo IP o nome DNS della VM Linux.</span><span class="sxs-lookup"><span data-stu-id="3477e-144">Open your local remote desktop client and connect toohello IP address or DNS name of your Linux VM.</span></span> <span data-ttu-id="3477e-145">Immettere hello nome utente e password per account utente di hello nella VM come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3477e-145">Enter hello username and password for hello user account on your VM as follows:</span></span>

![Connettersi tooxrdp utilizzando il client Desktop remoto](./media/use-remote-desktop/remote-desktop-client.png)

<span data-ttu-id="3477e-147">Dopo l'autenticazione, ambiente di desktop xfce hello verrà caricate ed esaminare toohello simile esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="3477e-147">After authenticating, hello xfce desktop environment will load and look similar toohello following example:</span></span>

![ambiente desktop xfce tramite xrdp](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a><span data-ttu-id="3477e-149">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="3477e-149">Troubleshoot</span></span>
<span data-ttu-id="3477e-150">Se non è possibile connettersi tooyour VM Linux utilizzando un client Desktop remoto, utilizzare `netstat` sul tooverify VM Linux che la macchina virtuale è in attesa come indicato di seguito per le connessioni RDP:</span><span class="sxs-lookup"><span data-stu-id="3477e-150">If you cannot connect tooyour Linux VM using a Remote Desktop client, use `netstat` on your Linux VM tooverify that your VM is listening for RDP connections  as follows:</span></span>

```bash
sudo netstat -plnt | grep rdp
```

<span data-ttu-id="3477e-151">Hello seguendo l'esempio hello macchina virtuale è in ascolto sulla porta TCP 3389 come previsto:</span><span class="sxs-lookup"><span data-stu-id="3477e-151">hello following example shows hello VM listening on TCP port 3389 as expected:</span></span>

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

<span data-ttu-id="3477e-152">Se non è in ascolto il servizio di xrdp hello, in una VM Ubuntu riavviare servizio hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3477e-152">If hello xrdp service is not listening, on an Ubuntu VM restart hello service as follows:</span></span>

```bash
sudo service xrdp restart
```

<span data-ttu-id="3477e-153">Revisione accede *var/log*Thug nella VM Ubuntu per indicazioni come servizio hello toowhy non risponde.</span><span class="sxs-lookup"><span data-stu-id="3477e-153">Review logs in */var/log*Thug  on your Ubuntu VM for indications as toowhy hello service may not be responding.</span></span> <span data-ttu-id="3477e-154">È anche possibile monitorare hello syslog durante un tooview tentativo di connessione desktop remoto gli eventuali errori:</span><span class="sxs-lookup"><span data-stu-id="3477e-154">You can also monitor hello syslog during a remote desktop connection attempt tooview any errors:</span></span>

```bash
tail -f /var/log/syslog
```

<span data-ttu-id="3477e-155">Altre distribuzioni Linux, ad esempio Red Hat Enterprise Linux e SUSE possono avere servizi toorestart modi diversi e tooreview percorsi di file alternativo per il log.</span><span class="sxs-lookup"><span data-stu-id="3477e-155">Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways toorestart services and alternate log file locations tooreview.</span></span>

<span data-ttu-id="3477e-156">Se si non riceve alcuna risposta il client desktop remoto e non viene visualizzato alcun evento nel Registro di sistema hello, ciò indica che il traffico di desktop remoto non riesce a raggiungere hello VM.</span><span class="sxs-lookup"><span data-stu-id="3477e-156">If you do not receive any response in your remote desktop client and do not see any events in hello system log, this behavior indicates that remote desktop traffic cannot reach hello VM.</span></span> <span data-ttu-id="3477e-157">Esaminare il tooensure di regole gruppo di sicurezza di rete di disporre di un toopermit regola TCP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="3477e-157">Review your network security group rules tooensure that you have a rule toopermit TCP on port 3389.</span></span> <span data-ttu-id="3477e-158">Per altre informazioni, vedere [Risolvere i problemi di connettività delle applicazioni in una macchina virtuale di Azure per Linux](../windows/troubleshoot-app-connection.md).</span><span class="sxs-lookup"><span data-stu-id="3477e-158">For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="3477e-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3477e-159">Next steps</span></span>
<span data-ttu-id="3477e-160">Per altre informazioni sulla creazione e l'uso di chiavi SSH con macchine virtuali Linux, vedere [Creare una coppia di chiavi SSH pubblica e privata per le macchine virtuali di Linux](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="3477e-160">For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

<span data-ttu-id="3477e-161">Per informazioni sull'utilizzo di SSH da Windows, vedere [come chiavi, toouse SSH tramite Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="3477e-161">For information on using SSH from Windows, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

