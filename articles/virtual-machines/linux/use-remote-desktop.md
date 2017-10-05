---
title: Usare Desktop remoto per una macchina virtuale Linux di Azure| Documentazione Microsoft
description: Informazioni sull'installazione e la configurazione di Desktop remoto (xrdp) per collegarsi a una macchina virtuale Linux di Azure usando strumenti grafici
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
ms.openlocfilehash: d8d6130a270285c84c1dd057a3512cdeb39287f6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="install-and-configure-remote-desktop-to-connect-to-a-linux-vm-in-azure"></a><span data-ttu-id="b6466-103">Installare e configurare Desktop remoto per connettersi a una VM Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="b6466-103">Install and configure Remote Desktop to connect to a Linux VM in Azure</span></span>
<span data-ttu-id="b6466-104">Le macchine virtuali Linux (VM) di Azure in genere vengono gestite dalla riga di comando tramite una connessione secure shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="b6466-104">Linux virtual machines (VMs) in Azure are usually managed from the command line using a secure shell (SSH) connection.</span></span> <span data-ttu-id="b6466-105">Quando si è nuovi a Linux, o per scenari di risoluzione dei problemi rapidi, l'uso di desktop remoto potrebbe risultare più facile.</span><span class="sxs-lookup"><span data-stu-id="b6466-105">When new to Linux, or for quick troubleshooting scenarios, the use of remote desktop may be easier.</span></span> <span data-ttu-id="b6466-106">Questo articolo illustra come installare e configurare un ambiente desktop ([xfce](https://www.xfce.org)) e desktop remoto ([xrdp](http://www.xrdp.org)) per VM Linux usando il modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b6466-106">This article details how to install and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp.org)) for your Linux VM using the Resource Manager deployment model.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b6466-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b6466-107">Prerequisites</span></span>
<span data-ttu-id="b6466-108">Questo articolo richiede l'esistenza di una VM Linux di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6466-108">This article requires an existing Linux VM in Azure.</span></span> <span data-ttu-id="b6466-109">Se è necessario creare una macchina virtuale, usare uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b6466-109">If you need to create a VM, use one of the following methods:</span></span>

- <span data-ttu-id="b6466-110">L'[interfaccia della riga di comando di Azure 2.0](quick-create-cli.md)</span><span class="sxs-lookup"><span data-stu-id="b6466-110">The [Azure CLI 2.0](quick-create-cli.md)</span></span>
- <span data-ttu-id="b6466-111">Il[portale di Azure](quick-create-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b6466-111">The [Azure portal](quick-create-portal.md)</span></span>


## <a name="install-a-desktop-environment-on-your-linux-vm"></a><span data-ttu-id="b6466-112">Installare un ambiente desktop nella VM Linux</span><span class="sxs-lookup"><span data-stu-id="b6466-112">Install a desktop environment on your Linux VM</span></span>
<span data-ttu-id="b6466-113">La maggior parte delle macchine virtuali Linux di Azure non presenta un ambiente desktop installato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b6466-113">Most Linux VMs in Azure do not have a desktop environment installed by default.</span></span> <span data-ttu-id="b6466-114">Le macchine virtuali Linux in genere vengono gestite usando connessioni SSH piuttosto che un ambiente desktop.</span><span class="sxs-lookup"><span data-stu-id="b6466-114">Linux VMs are commonly managed using SSH connections rather than a desktop environment.</span></span> <span data-ttu-id="b6466-115">In Linux esistono diversi ambienti desktop tra i quali è possibile scegliere.</span><span class="sxs-lookup"><span data-stu-id="b6466-115">There are various desktop environments in Linux that you can choose.</span></span> <span data-ttu-id="b6466-116">A seconda dell'ambiente desktop scelto, questo può consumare da 1 a 2 GB di spazio su disco e può impiegare da 5 a 10 minuti per installare e configurare tutti i pacchetti necessari.</span><span class="sxs-lookup"><span data-stu-id="b6466-116">Depending on your choice of desktop environment, it may consume one to 2 GB of disk space, and take 5 to 10 minutes to install and configure all the required packages.</span></span>

<span data-ttu-id="b6466-117">Nell'esempio seguente l'ambiente desktop leggero [xfce4](https://www.xfce.org/) viene installato in una macchina virtuale Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="b6466-117">The following example installs the lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span></span> <span data-ttu-id="b6466-118">I comandi per le altre distribuzioni sono leggermente diversi (ad esempio, usare `yum` per installare in Red Hat Enterprise Linux e configurare regole `selinux` appropriate, oppure usare `zypper` per installare in SUSE).</span><span class="sxs-lookup"><span data-stu-id="b6466-118">Commands for other distributions vary slightly (use `yum` to install on Red Hat Enterprise Linux and configure appropriate `selinux` rules, or use `zypper` to install on SUSE, for example).</span></span>

<span data-ttu-id="b6466-119">Innanzitutto, stabilire una connessione SSH alla VM.</span><span class="sxs-lookup"><span data-stu-id="b6466-119">First, SSH to your VM.</span></span> <span data-ttu-id="b6466-120">Nell'esempio seguente viene eseguita la connessione alla macchina virtuale denominata *myvm.westus.cloudapp.azure.com* con il nome utente di *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="b6466-120">The following example connects to the VM named *myvm.westus.cloudapp.azure.com* with the username of *azureuser*:</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="b6466-121">Se si usa Windows, per altre informazioni sull'uso di SSH, vedere [Come usare SSH con Windows in Azure](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="b6466-121">If you are using Windows and need more information on using SSH, see [How to use SSH keys with Windows](ssh-from-windows.md).</span></span>

<span data-ttu-id="b6466-122">Successivamente, installare xfce usando `apt` come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b6466-122">Next, install xfce using `apt` as follows:</span></span>

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a><span data-ttu-id="b6466-123">Installare e configurare un server di desktop remoto</span><span class="sxs-lookup"><span data-stu-id="b6466-123">Install and configure a remote desktop server</span></span>
<span data-ttu-id="b6466-124">Ora che si dispone di un ambiente desktop installato, configurare un servizio Desktop remoto per l'ascolto delle connessioni in ingresso.</span><span class="sxs-lookup"><span data-stu-id="b6466-124">Now that you have a desktop environment installed, configure a remote desktop service to listen for incoming connections.</span></span> <span data-ttu-id="b6466-125">[xrdp](http://xrdp.org) è un server Remote Desktop Protocol (RDP) open source che è disponibile nella maggior parte delle distribuzioni Linux e funziona bene con xfce.</span><span class="sxs-lookup"><span data-stu-id="b6466-125">[xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce.</span></span> <span data-ttu-id="b6466-126">Installare xrdp nella VM Ubuntu come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b6466-126">Install xrdp on your Ubuntu VM as follows:</span></span>

```bash
sudo apt-get install xrdp
```

<span data-ttu-id="b6466-127">Indicare a xrdp quale ambiente desktop usare quando si avvia la sessione.</span><span class="sxs-lookup"><span data-stu-id="b6466-127">Tell xrdp what desktop environment to use when you start your session.</span></span> <span data-ttu-id="b6466-128">Configurare xrdp per usare xfce come ambiente desktop come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b6466-128">Configure xrdp to use xfce as your desktop environment as follows:</span></span>

```bash
echo xfce4-session >~/.xsession
```

<span data-ttu-id="b6466-129">Riavviare il servizio xrdp per rendere effettive le modifiche, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b6466-129">Restart the xrdp service for the changes to take effect as follows:</span></span>

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a><span data-ttu-id="b6466-130">Impostare una password per l'account utente locale</span><span class="sxs-lookup"><span data-stu-id="b6466-130">Set a local user account password</span></span>
<span data-ttu-id="b6466-131">Se la password dell'account utente è stata impostata al momento della creazione della macchina virtuale, ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="b6466-131">If you created a password for your user account when you created your VM, skip this step.</span></span> <span data-ttu-id="b6466-132">Se si usa soltanto l'autenticazione con chiave SSH e non è stata creata una password per l'account locale, specificare una password prima di usare xrdp per accedere alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b6466-132">If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp to log in to your VM.</span></span> <span data-ttu-id="b6466-133">xrdp non può accettare chiavi SSH per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="b6466-133">xrdp cannot accept SSH keys for authentication.</span></span> <span data-ttu-id="b6466-134">Nell'esempio seguente viene specificata una password per l'account utente *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="b6466-134">The following example specifies a password for the user account *azureuser*:</span></span>

```bash
sudo passwd azureuser
```

> [!NOTE]
> <span data-ttu-id="b6466-135">Se attualmente gli accessi tramite password non sono permessi, l'impostazione della password non aggiorna la configurazione SSHD per consentirli.</span><span class="sxs-lookup"><span data-stu-id="b6466-135">Specifying a password does not update your SSHD configuration to permit password logins if it currently does not.</span></span> <span data-ttu-id="b6466-136">Dal punto di vista della sicurezza, l'utente potrebbe desiderare connettersi alla macchina virtuale con un tunnel SSH usando l'autenticazione tramite chiave e poi connettersi a xrdp.</span><span class="sxs-lookup"><span data-stu-id="b6466-136">From a security perspective, you may wish to connect to your VM with an SSH tunnel using key-based authentication and then connect to xrdp.</span></span> <span data-ttu-id="b6466-137">In questo caso, ignorare il passaggio seguente sulla creazione di una regola del gruppo di sicurezza di rete per consentire il traffico di desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="b6466-137">If so, skip the following step on creating a network security group rule to allow remote desktop traffic.</span></span>


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a><span data-ttu-id="b6466-138">Creare una regola del gruppo di sicurezza di rete per il traffico di Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="b6466-138">Create a Network Security Group rule for Remote Desktop traffic</span></span>
<span data-ttu-id="b6466-139">Per consentire al traffico di Desktop remoto di raggiungere la VM Linux, è necessario creare una regola del gruppo di sicurezza di rete che consenta al TCP sulla porta 3389 di raggiungere la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b6466-139">To allow Remote Desktop traffic to reach your Linux VM, a network security group rule needs to be created that allows TCP on port 3389 to reach your VM.</span></span> <span data-ttu-id="b6466-140">Per altre informazioni sulle regole dei gruppi di sicurezza di rete, vedere [Che cos'è un gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b6466-140">For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> <span data-ttu-id="b6466-141">È anche possibile [usare il portale di Azure per creare una regola del gruppo di sicurezza di rete](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b6466-141">You can also [use the Azure portal to create a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b6466-142">Nell'esempio seguente viene creata una regola del gruppo di sicurezza di rete con [az network nsg rule create](/cli/azure/network/nsg/rule#create) denominata *myNetworkSecurityGroupRule* per *consentire* il traffico sulla porta *tcp* *3389*.</span><span class="sxs-lookup"><span data-stu-id="b6466-142">The following examples create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) named *myNetworkSecurityGroupRule* to *allow* traffic on *tcp* port *3389*.</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a><span data-ttu-id="b6466-143">Connettere la macchina virtuale Linux con un client di Desktop remoto</span><span class="sxs-lookup"><span data-stu-id="b6466-143">Connect your Linux VM with a Remote Desktop client</span></span>
<span data-ttu-id="b6466-144">Aprire il client di Desktop remoto locale e connettersi all'indirizzo IP o nome DNS della VM Linux.</span><span class="sxs-lookup"><span data-stu-id="b6466-144">Open your local remote desktop client and connect to the IP address or DNS name of your Linux VM.</span></span> <span data-ttu-id="b6466-145">Immettere il nome utente e la password per l'account utente nella macchina virtuale come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b6466-145">Enter the username and password for the user account on your VM as follows:</span></span>

![Connettersi a xrdp usando il client di Desktop remoto](./media/use-remote-desktop/remote-desktop-client.png)

<span data-ttu-id="b6466-147">Dopo l'autenticazione, l'ambiente desktop xfce verrà caricato e apparirà come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="b6466-147">After authenticating, the xfce desktop environment will load and look similar to the following example:</span></span>

![ambiente desktop xfce tramite xrdp](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a><span data-ttu-id="b6466-149">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="b6466-149">Troubleshoot</span></span>
<span data-ttu-id="b6466-150">Se non è possibile connettersi alla VM Linux usando un client di Desktop remoto, usare `netstat` nella VM Linux per verificare che la macchina virtuale stia ascoltando le connessioni RDP come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b6466-150">If you cannot connect to your Linux VM using a Remote Desktop client, use `netstat` on your Linux VM to verify that your VM is listening for RDP connections  as follows:</span></span>

```bash
sudo netstat -plnt | grep rdp
```

<span data-ttu-id="b6466-151">Nell'esempio seguente viene mostrata la macchina virtuale in ascolto sulla porta TCP 3389 come previsto:</span><span class="sxs-lookup"><span data-stu-id="b6466-151">The following example shows the VM listening on TCP port 3389 as expected:</span></span>

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

<span data-ttu-id="b6466-152">Se il servizio xrdp non è in ascolto, in una macchina virtuale Ubuntu riavviare il servizio come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b6466-152">If the xrdp service is not listening, on an Ubuntu VM restart the service as follows:</span></span>

```bash
sudo service xrdp restart
```

<span data-ttu-id="b6466-153">Controllare i log in */var/log*Thug nella VM Ubuntu per indicazioni sul perché il servizio non risponde.</span><span class="sxs-lookup"><span data-stu-id="b6466-153">Review logs in */var/log*Thug  on your Ubuntu VM for indications as to why the service may not be responding.</span></span> <span data-ttu-id="b6466-154">È possibile anche monitorare il syslog durante un tentativo di connessione Desktop remoto per visualizzare eventuali errori:</span><span class="sxs-lookup"><span data-stu-id="b6466-154">You can also monitor the syslog during a remote desktop connection attempt to view any errors:</span></span>

```bash
tail -f /var/log/syslog
```

<span data-ttu-id="b6466-155">Altre distribuzioni Linux, ad esempio Red Hat Enterprise Linux e SUSE, possono presentare modi diversi per riavviare i servizi e posizioni dei file di log alternative da controllare.</span><span class="sxs-lookup"><span data-stu-id="b6466-155">Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways to restart services and alternate log file locations to review.</span></span>

<span data-ttu-id="b6466-156">Se non si riceve alcuna risposta nel client di Desktop remoto e non viene visualizzato nessun evento nel log di sistema, questo comportamento indica che il traffico di Desktop remoto non riesce a raggiungere la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b6466-156">If you do not receive any response in your remote desktop client and do not see any events in the system log, this behavior indicates that remote desktop traffic cannot reach the VM.</span></span> <span data-ttu-id="b6466-157">Controllare le regole del gruppo di sicurezza di rete per assicurarsi che esista una regola che consenta TCP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="b6466-157">Review your network security group rules to ensure that you have a rule to permit TCP on port 3389.</span></span> <span data-ttu-id="b6466-158">Per altre informazioni, vedere [Risolvere i problemi di connettività delle applicazioni in una macchina virtuale di Azure per Linux](../windows/troubleshoot-app-connection.md).</span><span class="sxs-lookup"><span data-stu-id="b6466-158">For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="b6466-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b6466-159">Next steps</span></span>
<span data-ttu-id="b6466-160">Per altre informazioni sulla creazione e l'uso di chiavi SSH con macchine virtuali Linux, vedere [Creare una coppia di chiavi SSH pubblica e privata per le macchine virtuali di Linux](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="b6466-160">For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

<span data-ttu-id="b6466-161">Per informazioni sull'uso di SSH da Windows, vedere [Come usare SSH con Windows in Azure](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="b6466-161">For information on using SSH from Windows, see [How to use SSH keys with Windows](ssh-from-windows.md).</span></span>

