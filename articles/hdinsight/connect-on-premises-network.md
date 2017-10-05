---
title: Connettere HDInsight alla rete locale - Azure HDInsight | Microsoft Docs
description: Informazioni su come creare un cluster HDInsight in una rete virtuale di Azure e quindi connetterlo alla rete locale. Informazioni su come configurare la risoluzione dei nomi tra HDInsight e la rete locale usando un server DNS personalizzato.
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 6fc863010cc59e20e7d86ea9344489e574be75f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="connect-hdinsight-to-your-on-premise-network"></a><span data-ttu-id="e65a0-104">Connettere HDInsight alla rete locale</span><span class="sxs-lookup"><span data-stu-id="e65a0-104">Connect HDInsight to your on-premise network</span></span>

<span data-ttu-id="e65a0-105">Informazioni su come connettere HDInsight alla rete locale usando Reti virtuali di Azure e un gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="e65a0-105">Learn how to connect HDInsight to your on-premises network by using Azure Virtual Networks and a VPN gateway.</span></span> <span data-ttu-id="e65a0-106">Questo documento fornisce le informazioni di pianificazione su:</span><span class="sxs-lookup"><span data-stu-id="e65a0-106">This document provides planning information on:</span></span>

* <span data-ttu-id="e65a0-107">Uso di HDInsight in una rete virtuale di Azure che si connette alla rete locale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-107">Using HDInsight in an Azure Virtual Network that connects to your on-premises network.</span></span>

* <span data-ttu-id="e65a0-108">Configurazione della risoluzione dei nomi DNS tra la rete virtuale e la rete locale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-108">Configuring DNS name resolution between the virtual network and your on-premises network.</span></span>

* <span data-ttu-id="e65a0-109">Configurazione dei gruppi di sicurezza di rete per limitare l'accesso Internet per HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e65a0-109">Configuring network security groups to restrict internet access to HDInsight.</span></span>

* <span data-ttu-id="e65a0-110">Porte fornite da HDInsight nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-110">Ports provided by HDInsight on the virtual network.</span></span>

## <a name="create-the-virtual-network-configuration"></a><span data-ttu-id="e65a0-111">Creare la configurazione della rete virtuale</span><span class="sxs-lookup"><span data-stu-id="e65a0-111">Create the Virtual network configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e65a0-112">Per istruzioni dettagliate sulla connessione di HDInsight alla rete locale tramite una rete virtuale di Azure, vedere il documento [Connettere HDInsight alla rete locale](connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="e65a0-112">If you are looking for step by step guidance on connecting HDInsight to your on-premises network using an Azure Virtual Network, see the [Connect HDInsight to your on-premise network](connect-on-premises-network.md) document.</span></span>

<span data-ttu-id="e65a0-113">Vedere i documenti seguenti per informazioni su come creare una rete virtuale di Azure connessa alla rete locale:</span><span class="sxs-lookup"><span data-stu-id="e65a0-113">Use the following documents to learn how to create an Azure Virtual Network that is connected to your on-premises network:</span></span>
    
* [<span data-ttu-id="e65a0-114">Uso del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e65a0-114">Using the Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [<span data-ttu-id="e65a0-115">Uso di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e65a0-115">Using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [<span data-ttu-id="e65a0-116">Uso dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e65a0-116">Using Azure CLI</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a><span data-ttu-id="e65a0-117">Configurare la risoluzione dei nomi</span><span class="sxs-lookup"><span data-stu-id="e65a0-117">Configure name resolution</span></span>

<span data-ttu-id="e65a0-118">Per consentire a HDInsight e alle risorse nella rete aggiunta di comunicare in base al nome, è necessario eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="e65a0-118">To allow HDInsight and resources in the joined network to communicate by name, you must perform the following actions:</span></span>

* <span data-ttu-id="e65a0-119">Creare un server DNS personalizzato in Rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e65a0-119">Create a custom DNS server in the Azure Virtual Network.</span></span>

* <span data-ttu-id="e65a0-120">Configurare la rete virtuale per usare il server DNS personalizzato invece del resolver ricorsivo predefinito di Azure.</span><span class="sxs-lookup"><span data-stu-id="e65a0-120">Configure the virtual network to use the custom DNS server instead of the default Azure Recursive Resolver.</span></span>

* <span data-ttu-id="e65a0-121">Configurare l'inoltro tra il server DNS personalizzato e il server DNS locale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-121">Configure forwarding between the custom DNS server and your on-premises DNS server.</span></span>

<span data-ttu-id="e65a0-122">Questa configurazione consente il comportamento seguente:</span><span class="sxs-lookup"><span data-stu-id="e65a0-122">This configuration enables the following behavior:</span></span>

* <span data-ttu-id="e65a0-123">Le richieste per i nomi di dominio completi con il suffisso DNS __per la rete virtuale__ vengono inoltrate al server DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="e65a0-123">Requests for fully qualified domain names that have the DNS suffix __for the virtual network__ are forwarded to the custom DNS server.</span></span> <span data-ttu-id="e65a0-124">Il server DNS personalizzato inoltra quindi le richieste al resolver ricorsivo di Azure, che restituisce l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="e65a0-124">The custom DNS server then forwards these requests to the Azure Recursive Resolver, which returns the IP address.</span></span>

* <span data-ttu-id="e65a0-125">Tutte le altre richieste vengono inoltrate al server DNS locale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-125">All other requests are forwarded to the on-premises DNS server.</span></span> <span data-ttu-id="e65a0-126">Anche le richieste di risorse Internet pubbliche, ad esempio microsoft.com, vengono inoltrate al server DNS locale per la risoluzione dei nomi.</span><span class="sxs-lookup"><span data-stu-id="e65a0-126">Even requests for public internet resources such as microsoft.com are forwarded to the on-premises DNS server for name resolution.</span></span>

<span data-ttu-id="e65a0-127">Nel diagramma seguente le linee verdi sono richieste di risorse che terminano nel suffisso DNS della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-127">In the following diagram, green lines are requests for resources that end in the DNS suffix of the virtual network.</span></span> <span data-ttu-id="e65a0-128">Le linee blu sono richieste di risorse nella rete locale o nella rete Internet pubblica.</span><span class="sxs-lookup"><span data-stu-id="e65a0-128">Blue lines are requests for resources in the on-premises network or on the public internet.</span></span>

![Diagramma della modalità di risoluzione delle richieste DNS nella configurazione usata in questo documento](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a><span data-ttu-id="e65a0-130">Creare un server DNS personalizzato</span><span class="sxs-lookup"><span data-stu-id="e65a0-130">Create a custom DNS server</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e65a0-131">È necessario creare e configurare il server DNS prima di installare HDInsight nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-131">You must create and configure the DNS server before installing HDInsight into the virtual network.</span></span>

<span data-ttu-id="e65a0-132">Per creare una VM Linux che usa il software DNS [Bind](https://www.isc.org/downloads/bind/), eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e65a0-132">To create a Linux VM that uses the [Bind](https://www.isc.org/downloads/bind/) DNS software, use the following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="e65a0-133">Nella procedura seguente viene usato il [portale di Azure](https://portal.azure.com) per creare una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e65a0-133">The following steps use the [Azure portal](https://portal.azure.com) to create an Azure Virtual Machine.</span></span> <span data-ttu-id="e65a0-134">Per altri modi per creare una macchina virtuale, vedere i documenti [Creare una VM: interfaccia della riga di comando di Azure](../virtual-machines/linux/quick-create-cli.md) e [Creare una VM: Azure PowerShell](../virtual-machines/linux/quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e65a0-134">For other ways to create a virtual machine, see the [Create VM - Azure CLI](../virtual-machines/linux/quick-create-cli.md) and [Create VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documents.</span></span>

1. <span data-ttu-id="e65a0-135">Dal [portale di Azure](https://portal.azure.com) selezionare __+__, __Calcolo__ e __Ubuntu Server 16.04 LTS__.</span><span class="sxs-lookup"><span data-stu-id="e65a0-135">From the [Azure portal](https://portal.azure.com), select __+__, __Compute__, and __Ubuntu Server 16.04 LTS__.</span></span>

    ![Creare una macchina virtuale Ubuntu](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. <span data-ttu-id="e65a0-137">Nella sezione __Informazioni di base__ immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e65a0-137">From the __Basics__ section, enter the following information:</span></span>

    * <span data-ttu-id="e65a0-138">__Nome__: nome descrittivo che identifica questa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-138">__Name__: A friendly name that identifies this virtual machine.</span></span> <span data-ttu-id="e65a0-139">Ad esempio __DNSProxy__.</span><span class="sxs-lookup"><span data-stu-id="e65a0-139">For example, __DNSProxy__.</span></span>
    * <span data-ttu-id="e65a0-140">__Nome utente__: nome dell'account SSH.</span><span class="sxs-lookup"><span data-stu-id="e65a0-140">__User name__: The name of the SSH account.</span></span>
    * <span data-ttu-id="e65a0-141">__Chiave pubblica SSH__ o __Password__: metodo di autenticazione per l'account SSH.</span><span class="sxs-lookup"><span data-stu-id="e65a0-141">__SSH public key__ or __Password__: The authentication method for the SSH account.</span></span> <span data-ttu-id="e65a0-142">Si consiglia di usare le chiavi pubbliche, che sono più sicure.</span><span class="sxs-lookup"><span data-stu-id="e65a0-142">We recommend using public keys, as they are more secure.</span></span> <span data-ttu-id="e65a0-143">Per altre informazioni, vedere il documento [Creare e usare chiavi SSH per VM Linux](../virtual-machines/linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="e65a0-143">For more information, see the [Create and use SSH keys for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span></span>
    * <span data-ttu-id="e65a0-144">__Gruppo di risorse__: selezionare __Usa esistente__ e quindi selezionare il gruppo di risorse contenente la rete virtuale creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e65a0-144">__Resource group__: Select __Use existing__, and then select the resource group that contains the virtual network created earlier.</span></span>
    * <span data-ttu-id="e65a0-145">__Località__: selezionare la stessa località della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-145">__Location__: Select the same location as the virtual network.</span></span>

    ![Configurazione di base della macchina virtuale](./media/connect-on-premises-network/vm-basics.png)

    <span data-ttu-id="e65a0-147">Lasciare i valori predefiniti per le altre voci e quindi selezionare __OK__.</span><span class="sxs-lookup"><span data-stu-id="e65a0-147">Leave other entries at the default values and then select __OK__.</span></span>

3. <span data-ttu-id="e65a0-148">Nella sezione __Scegli una dimensione__ selezionare la dimensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-148">From the __Choose a size__ section, select the VM size.</span></span> <span data-ttu-id="e65a0-149">Per questa esercitazione selezionare l'opzione più piccola e a più basso costo.</span><span class="sxs-lookup"><span data-stu-id="e65a0-149">For this tutorial, select the smallest and lowest cost option.</span></span> <span data-ttu-id="e65a0-150">Per continuare, usare il pulsante __Seleziona__.</span><span class="sxs-lookup"><span data-stu-id="e65a0-150">To continue, use the __Select__ button.</span></span>

4. <span data-ttu-id="e65a0-151">Nella sezione __Impostazioni__ immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e65a0-151">From the __Settings__ section, enter the following information:</span></span>

    * <span data-ttu-id="e65a0-152">__Rete virtuale__: selezionare la rete virtuale creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e65a0-152">__Virtual network__: Select the virtual network that you created earlier.</span></span>

    * <span data-ttu-id="e65a0-153">__Subnet__: selezionare la subnet predefinita per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-153">__Subnet__: Select the default subnet for the virtual network.</span></span> <span data-ttu-id="e65a0-154">__Non__ selezionare la subnet usata dal gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="e65a0-154">Do __not__ select the subnet used by the VPN gateway.</span></span>

    * <span data-ttu-id="e65a0-155">__Account di archiviazione di diagnostica__: selezionare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="e65a0-155">__Diagnostics storage account__: Either select an existing storage account or create a new one.</span></span>

    ![Impostazioni della rete virtuale](./media/connect-on-premises-network/virtual-network-settings.png)

    <span data-ttu-id="e65a0-157">Lasciare i valori predefiniti per le altre voci e quindi selezionare __OK__ per continuare.</span><span class="sxs-lookup"><span data-stu-id="e65a0-157">Leave the other entries at the default value, then select __OK__ to continue.</span></span>

5. <span data-ttu-id="e65a0-158">Nella sezione __Acquisto__ fare clic sul pulsante __Acquista__ per creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-158">From the __Purchase__ section, select the __Purchase__ button to create the virtual machine.</span></span>

6. <span data-ttu-id="e65a0-159">Dopo che la macchina virtuale è stata creata, viene visualizzata la relativa sezione __Panoramica__.</span><span class="sxs-lookup"><span data-stu-id="e65a0-159">Once the virtual machine has been created, its __Overview__ section is displayed.</span></span> <span data-ttu-id="e65a0-160">Nell'elenco a sinistra selezionare __Proprietà__.</span><span class="sxs-lookup"><span data-stu-id="e65a0-160">From the list on the left, select __Properties__.</span></span> <span data-ttu-id="e65a0-161">Salvare i valori di __Indirizzo IP pubblico__ e __Indirizzo IP privato__.</span><span class="sxs-lookup"><span data-stu-id="e65a0-161">Save the __Public IP address__ and __Private IP address__ values.</span></span> <span data-ttu-id="e65a0-162">Verranno usati nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="e65a0-162">It will be used in the next section.</span></span>

    ![Indirizzi IP pubblico e privato](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a><span data-ttu-id="e65a0-164">Installare e configurare Bind (software DNS)</span><span class="sxs-lookup"><span data-stu-id="e65a0-164">Install and configure Bind (DNS software)</span></span>

1. <span data-ttu-id="e65a0-165">Usare SSH per connettersi all'__indirizzo IP pubblico__ della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-165">Use SSH to connect to the __public IP address__ of the virtual machine.</span></span> <span data-ttu-id="e65a0-166">L'esempio seguente consente la connessione a una macchina virtuale all'indirizzo 40.68.254.142:</span><span class="sxs-lookup"><span data-stu-id="e65a0-166">The following example connects to a virtual machine at 40.68.254.142:</span></span>

    ```bash
    ssh sshuser@40.68.254.142
    ```

    <span data-ttu-id="e65a0-167">Sostituire `sshuser` con l'account utente SSH specificato durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="e65a0-167">Replace `sshuser` with the SSH user account you specified when creating the cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e65a0-168">È possibile ottenere l'utilità `ssh` in diversi modi.</span><span class="sxs-lookup"><span data-stu-id="e65a0-168">There are a variety of ways to obtain the `ssh` utility.</span></span> <span data-ttu-id="e65a0-169">In Linux, Unix e macOS viene fornita come parte del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="e65a0-169">On Linux, Unix, and macOS, it is provided as part of the operating system.</span></span> <span data-ttu-id="e65a0-170">Se si usa Windows, prendere in considerazione una delle opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e65a0-170">If you are using Windows, consider one of the following options:</span></span>
    >
    > * [<span data-ttu-id="e65a0-171">Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="e65a0-171">Azure Cloud Shell</span></span>](../cloud-shell/quickstart.md)
    > * [<span data-ttu-id="e65a0-172">Bash in Ubuntu su Windows 10</span><span class="sxs-lookup"><span data-stu-id="e65a0-172">Bash on Ubuntu on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/about)
    > * [<span data-ttu-id="e65a0-173">Git (https://git-scm.com/)</span><span class="sxs-lookup"><span data-stu-id="e65a0-173">Git (https://git-scm.com/)</span></span>](https://git-scm.com/)
    > * [<span data-ttu-id="e65a0-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span><span class="sxs-lookup"><span data-stu-id="e65a0-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. <span data-ttu-id="e65a0-175">Per installare Bind, usare i comandi seguenti dalla sessione SSH:</span><span class="sxs-lookup"><span data-stu-id="e65a0-175">To install Bind, use the following commands from the SSH session:</span></span>

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. <span data-ttu-id="e65a0-176">Per configurare Bind per l'inoltro delle richieste di risoluzione dei nomi al server DNS locale, usare il testo seguente come contenuto del file `/etc/bind/named.conf.options`:</span><span class="sxs-lookup"><span data-stu-id="e65a0-176">To configure Bind to forward name resolution requests to your on-prem DNS server, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

        acl goodclients {
            10.0.0.0/16; # Replace with the IP address range of the virtual network
            10.1.0.0/16; # Replace with the IP address range of the on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with the IP address of the on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform to RFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > <span data-ttu-id="e65a0-177">Sostituire i valori nella sezione `goodclients` con l'intervallo di indirizzi IP della rete virtuale e della rete locale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-177">Replace the values in the `goodclients` section with the IP address range of the virtual network and on-premises network.</span></span> <span data-ttu-id="e65a0-178">Questa sezione definisce gli indirizzi da cui il server DNS accetta le richieste.</span><span class="sxs-lookup"><span data-stu-id="e65a0-178">This section defines the addresses that this DNS server accepts requests from.</span></span>
    >
    > <span data-ttu-id="e65a0-179">Sostituire la voce `192.168.0.1` nella sezione `forwarders` con l'indirizzo IP del server DNS locale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-179">Replace the `192.168.0.1` entry in the `forwarders` section with the IP address of your on-premises DNS server.</span></span> <span data-ttu-id="e65a0-180">Questa voce indirizza le richieste DNS al server DNS locale per la risoluzione.</span><span class="sxs-lookup"><span data-stu-id="e65a0-180">This entry routes DNS requests to your on-premises DNS server for resolution.</span></span>

    <span data-ttu-id="e65a0-181">Per modificare questo file, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e65a0-181">To edit this file, use the following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    <span data-ttu-id="e65a0-182">Per salvare il file, usare __CTRL+X__, __Y__ e quindi __INVIO__.</span><span class="sxs-lookup"><span data-stu-id="e65a0-182">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

4. <span data-ttu-id="e65a0-183">Dalla sessione SSH usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e65a0-183">From the SSH session, use the following command:</span></span>

    ```bash
    hostname -f
    ```

    <span data-ttu-id="e65a0-184">Il comando restituisce un valore simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="e65a0-184">This command returns a value similar to the following text:</span></span>

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    <span data-ttu-id="e65a0-185">Il testo `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` è il __suffisso DNS__ per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-185">The `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is the __DNS suffix__ for this virtual network.</span></span> <span data-ttu-id="e65a0-186">Salvare questo valore, che verrà usato in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="e65a0-186">Save this value, as it is used later.</span></span>

5. <span data-ttu-id="e65a0-187">Per configurare Bind per la risoluzione dei nomi DNS per le risorse nella rete virtuale, usare il testo seguente come contenuto del file `/etc/bind/named.conf.local`:</span><span class="sxs-lookup"><span data-stu-id="e65a0-187">To configure Bind to resolve DNS names for resources within the virtual network, use the following text as the contents of the `/etc/bind/named.conf.local` file:</span></span>

        // Replace the following with the DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # The Azure recursive resolver
        };

    > [!IMPORTANT]
    > <span data-ttu-id="e65a0-188">È necessario sostituire `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` con il suffisso DNS recuperato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e65a0-188">You must replace the `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` with the DNS suffix you retrieved earlier.</span></span>

    <span data-ttu-id="e65a0-189">Per modificare questo file, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e65a0-189">To edit this file, use the following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    <span data-ttu-id="e65a0-190">Per salvare il file, usare __CTRL+X__, __Y__ e quindi __INVIO__.</span><span class="sxs-lookup"><span data-stu-id="e65a0-190">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

6. <span data-ttu-id="e65a0-191">Per avviare Bind, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e65a0-191">To start Bind, use the following command:</span></span>

    ```bash
    sudo service bind9 restart
    ```

7. <span data-ttu-id="e65a0-192">Per verificare che Bind riesca a risolvere i nomi delle risorse nella rete locale, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e65a0-192">To verify that bind can resolve the names of resources in your on-premises network, use the following commands:</span></span>

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="e65a0-193">Sostituire `dns.mynetwork.net` con il nome di dominio completo (FQDN) di una risorsa nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-193">Replace `dns.mynetwork.net` with the fully qualified domain name (FQDN) of a resource in your on-premises network.</span></span>
    >
    > <span data-ttu-id="e65a0-194">Sostituire `10.0.0.4` con l'__indirizzo IP interno__ del server DNS personalizzato nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-194">Replace `10.0.0.4` with the __internal IP address__ of your custom DNS server in the virtual network.</span></span>

    <span data-ttu-id="e65a0-195">La risposta visualizzata sarà simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="e65a0-195">The response appears similar to the following text:</span></span>

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-the-virtual-network-to-use-the-custom-dns-server"></a><span data-ttu-id="e65a0-196">Configurare la rete virtuale per usare il server DNS personalizzato</span><span class="sxs-lookup"><span data-stu-id="e65a0-196">Configure the virtual network to use the custom DNS server</span></span>

<span data-ttu-id="e65a0-197">Per configurare la rete virtuale per usare il server DNS personalizzato invece del resolver ricorsivo di Azure, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e65a0-197">To configure the virtual network to use the custom DNS server instead of the Azure recursive resolver, use the following steps:</span></span>

1. <span data-ttu-id="e65a0-198">Nel [portale di Azure](https://portal.azure.com) selezionare la rete virtuale e quindi selezionare __Server DNS__.</span><span class="sxs-lookup"><span data-stu-id="e65a0-198">In the [Azure portal](https://portal.azure.com), select the virtual network, and then select __DNS Servers__.</span></span>

2. <span data-ttu-id="e65a0-199">Selezionare __Personalizzato__ e immettere l'__indirizzo IP interno__ del server DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="e65a0-199">Select __Custom__, and enter the __internal IP address__ of the custom DNS server.</span></span> <span data-ttu-id="e65a0-200">Infine, selezionare __Salva__.</span><span class="sxs-lookup"><span data-stu-id="e65a0-200">Finally, select __Save__.</span></span>

    ![Impostare il server DNS personalizzato per la rete](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-the-on-premises-dns-server"></a><span data-ttu-id="e65a0-202">Configurare il server DNS locale</span><span class="sxs-lookup"><span data-stu-id="e65a0-202">Configure the on-premises DNS server</span></span>

<span data-ttu-id="e65a0-203">Nella sezione precedente è stato configurato il server DNS personalizzato per inoltrare le richieste al server DNS locale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-203">In the previous section, you configured the custom DNS server to forward requests to the on-premises DNS server.</span></span> <span data-ttu-id="e65a0-204">È quindi necessario configurare il server DNS locale per inoltrare le richieste al server DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="e65a0-204">Next, you must configure the on-premises DNS server to forward requests to the custom DNS server.</span></span>

<span data-ttu-id="e65a0-205">Per i passaggi specifici su come configurare il server DNS, vedere la documentazione per il prodotto server DNS.</span><span class="sxs-lookup"><span data-stu-id="e65a0-205">For specific steps on how to configure your DNS server, consult the documentation for your DNS server software.</span></span> <span data-ttu-id="e65a0-206">Cercare i passaggi su come configurare un __server d'inoltro condizionale__.</span><span class="sxs-lookup"><span data-stu-id="e65a0-206">Look for the steps on how to configure a __conditional forwarder__.</span></span>

<span data-ttu-id="e65a0-207">L'inoltro condizionale consente di inoltrare solo le richieste per un suffisso DNS specifico.</span><span class="sxs-lookup"><span data-stu-id="e65a0-207">A conditional forward only forwards requests for a specific DNS suffix.</span></span> <span data-ttu-id="e65a0-208">In questo caso, è necessario configurare un server d'inoltro per il suffisso DNS della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-208">In this case, you must configure a forwarder for the DNS suffix of the virtual network.</span></span> <span data-ttu-id="e65a0-209">Le richieste per questo suffisso devono essere inoltrate all'indirizzo IP del server DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="e65a0-209">Requests for this suffix should be forwarded to the IP address of the custom DNS server.</span></span> 

<span data-ttu-id="e65a0-210">Il testo seguente è un esempio di una configurazione di server d'inoltro condizionale per il software DNS **Bind**:</span><span class="sxs-lookup"><span data-stu-id="e65a0-210">The following text is an example of a conditional forwarder configuration for the **Bind** DNS software:</span></span>

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # The custom DNS server's internal IP address
    };

<span data-ttu-id="e65a0-211">Per informazioni sull'uso di DNS in **Windows Server 2016**, vedere [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone).</span><span class="sxs-lookup"><span data-stu-id="e65a0-211">For information on using DNS on **Windows Server 2016**, see the [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...</span></span>

<span data-ttu-id="e65a0-212">Dopo aver configurato il server DNS locale, è possibile usare `nslookup` dalla rete locale per verificare che sia possibile risolvere i nomi nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-212">Once you have configured the on-premises DNS server, you can use `nslookup` from the on-premises network to verify that you can resolve names in the virtual network.</span></span> <span data-ttu-id="e65a0-213">Vedere l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e65a0-213">The following example</span></span> 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

<span data-ttu-id="e65a0-214">Questo esempio usa il server DNS locale in 196.168.0.4 per risolvere il nome del server DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="e65a0-214">This example uses the on-premises DNS server at 196.168.0.4 to resolve the name of the custom DNS server.</span></span> <span data-ttu-id="e65a0-215">Sostituire l'indirizzo IP con uno del server DNS locale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-215">Replace the IP address with the one for the on-premises DNS server.</span></span> <span data-ttu-id="e65a0-216">Sostituire l'indirizzo `dnsproxy` con il nome di dominio completo del server DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="e65a0-216">Replace the `dnsproxy` address with the fully qualified domain name of the custom DNS server.</span></span>

## <a name="optional-control-network-traffic"></a><span data-ttu-id="e65a0-217">Facoltativo: Controllare il traffico di rete</span><span class="sxs-lookup"><span data-stu-id="e65a0-217">Optional: Control network traffic</span></span>

<span data-ttu-id="e65a0-218">È possibile usare gruppi di sicurezza di rete (NSG) o route definite dall'utente (UDR) per controllare il traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="e65a0-218">You can use network security groups (NSG) or user-defined routes (UDR) to control network traffic.</span></span> <span data-ttu-id="e65a0-219">Gli NSG permettono di filtrare il traffico in ingresso e in uscita e di consentire o negare il traffico.</span><span class="sxs-lookup"><span data-stu-id="e65a0-219">NSGs allow you to filter inbound and outbound traffic, and allow or deny the traffic.</span></span> <span data-ttu-id="e65a0-220">Le route definite dall'utente permettono di controllare il flusso di traffico tra le risorse nella rete virtuale, in Internet e nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-220">UDRs allow you to control how traffic flows between resources in the virtual network, the internet, and the on-premises network.</span></span>

> [!WARNING]
> <span data-ttu-id="e65a0-221">HDInsight richiede l'accesso in ingresso da indirizzi IP specifici nel cloud Azure e l'accesso in uscita senza restrizioni.</span><span class="sxs-lookup"><span data-stu-id="e65a0-221">HDInsight requires inbound access from specific IP addresses in the Azure cloud, and unrestricted outbound access.</span></span> <span data-ttu-id="e65a0-222">Quando si usano NSG o route definite dall'utente per controllare il traffico, è necessario eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e65a0-222">When using NSGs or UDRs to control traffic, you must perform the following steps:</span></span>
>
> 1. <span data-ttu-id="e65a0-223">Trovare gli indirizzi IP per la località contenente la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-223">Find the IP addresses for the location that contains your virtual network.</span></span> <span data-ttu-id="e65a0-224">Per un elenco di indirizzi IP necessari in base alla località, vedere [Indirizzi IP richiesti](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="e65a0-224">For a list of required IPs by location, see [Required IP addresses](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span></span>
>
> 2. <span data-ttu-id="e65a0-225">Consentire il traffico in ingresso dagli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="e65a0-225">Allow inbound traffic from the IP addresses.</span></span>
>
>    * <span data-ttu-id="e65a0-226">__NSG__: consentire il traffico __in ingresso__ sulla porta __443__ da __Internet__.</span><span class="sxs-lookup"><span data-stu-id="e65a0-226">__NSG__: Allow __inbound__ traffic on port __443__ from the __Internet__.</span></span>
>    * <span data-ttu-id="e65a0-227">__Route definita dall'utente__: impostare il tipo di __Hop successivo__ della route su __Internet__.</span><span class="sxs-lookup"><span data-stu-id="e65a0-227">__UDR__: Set the __Next Hop__ type of the route to __Internet__.</span></span>

<span data-ttu-id="e65a0-228">Per un esempio di utilizzo di Azure PowerShell o dell'interfaccia della riga di comando di Azure per creare gruppi NSG, vedere il documento [Estendere le funzionalità di HDInsight usando Rete virtuale di Azure](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg).</span><span class="sxs-lookup"><span data-stu-id="e65a0-228">For an example of using Azure PowerShell or the Azure CLI to create NSGs, see the [Extend HDInsight with Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span></span>

## <a name="create-the-hdinsight-cluster"></a><span data-ttu-id="e65a0-229">Creare il cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="e65a0-229">Create the HDInsight cluster</span></span>

> [!WARNING]
> <span data-ttu-id="e65a0-230">È necessario configurare il server DNS personalizzato prima di installare HDInsight nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-230">You must configure the custom DNS server before installing HDInsight in the virtual network.</span></span>

<span data-ttu-id="e65a0-231">Seguire i passaggi riportati in [Creare un cluster HDInsight tramite il portale di Azure](./hdinsight-hadoop-create-linux-clusters-portal.md) per creare un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e65a0-231">Use the steps in the [Create an HDInsight cluster using the Azure portal](./hdinsight-hadoop-create-linux-clusters-portal.md) document to create an HDInsight cluster.</span></span>

> [!WARNING]
> * <span data-ttu-id="e65a0-232">Durante la creazione del cluster, è necessario scegliere la posizione per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e65a0-232">During cluster creation, you must choose the location that contains your virtual network.</span></span>
>
> * <span data-ttu-id="e65a0-233">Nella sezione __Impostazioni avanzate__ della configurazione, è necessario selezionare la rete virtuale e la subnet create in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e65a0-233">In the __Advanced settings__ part of configuration, you must select the virtual network and subnet that you created earlier.</span></span>

## <a name="connecting-to-hdinsight"></a><span data-ttu-id="e65a0-234">Connessione a HDInsight</span><span class="sxs-lookup"><span data-stu-id="e65a0-234">Connecting to HDInsight</span></span>

<span data-ttu-id="e65a0-235">La maggior parte delle documentazione in HDInsight presuppone che sia disponibile l'accesso al cluster tramite internet.</span><span class="sxs-lookup"><span data-stu-id="e65a0-235">Most documentation on HDInsight assumes that you have access to the cluster over the internet.</span></span> <span data-ttu-id="e65a0-236">Verificare ad esempio che sia possibile connettersi al cluster all'indirizzo https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="e65a0-236">For example, that you can connect to the cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="e65a0-237">Questo indirizzo usa il gateway pubblico, che non è disponibile se sono stati usati NSG o route definite dall'utente per limitare l'accesso da Internet.</span><span class="sxs-lookup"><span data-stu-id="e65a0-237">This address uses the public gateway, which is not available if you have used NSGs or UDRs to restrict access from the internet.</span></span>

<span data-ttu-id="e65a0-238">Per connettersi direttamente a HDInsight attraverso la rete virtuale, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e65a0-238">To directly connect to HDInsight through the virtual network, use the following steps:</span></span>

1. <span data-ttu-id="e65a0-239">Per individuare i nomi di dominio completi interni dei nodi del cluster HDInsight, usare uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e65a0-239">To discover the internal fully qualified domain names of the HDInsight cluster nodes, use one of the following methods:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

2. <span data-ttu-id="e65a0-240">Per determinare la porta su cui un servizio è disponibile, vedere il documento [Porte usate dai servizi Hadoop su HDInsight](./hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="e65a0-240">To determine the port that a service is available on, see the [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e65a0-241">Alcuni servizi ospitati nei nodi head sono attivi solo in un nodo per volta.</span><span class="sxs-lookup"><span data-stu-id="e65a0-241">Some services hosted on the head nodes are only active on one node at a time.</span></span> <span data-ttu-id="e65a0-242">Se si prova ad accedere a un servizio in un nodo head e si verifica un errore, passare all'altro nodo head.</span><span class="sxs-lookup"><span data-stu-id="e65a0-242">If you try accessing a service on one head node and it fails, switch to the other head node.</span></span>
    >
    > <span data-ttu-id="e65a0-243">Ambari, ad esempio, è attivo solo in un nodo head per volta.</span><span class="sxs-lookup"><span data-stu-id="e65a0-243">For example, Ambari is only active on one head node at a time.</span></span> <span data-ttu-id="e65a0-244">Se si prova ad accedere ad Ambari in un nodo head e viene restituito un errore 404, significa che è in esecuzione nell'altro nodo head.</span><span class="sxs-lookup"><span data-stu-id="e65a0-244">If you try accessing Ambari on one head node and it returns a 404 error, then it is running on the other head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e65a0-245">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e65a0-245">Next steps</span></span>

* <span data-ttu-id="e65a0-246">Per altre informazioni sull'uso HDInsight in una rete virtuale, vedere [Estendere le funzionalità di HDInsight usando Rete virtuale di Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="e65a0-246">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

* <span data-ttu-id="e65a0-247">Per altre informazioni sulle reti virtuali di Azure, vedere [Rete virtuale di Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e65a0-247">For more information on Azure virtual networks, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="e65a0-248">Per altre informazioni sui gruppi di sicurezza di rete, vedere [Gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="e65a0-248">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="e65a0-249">Per altre informazioni sulle route definite dall'utente, vedere [Route definite dall'utente e inoltro IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e65a0-249">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>
