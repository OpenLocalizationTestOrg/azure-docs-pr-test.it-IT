---
title: rete di on-premise di aaaConnect HDInsight tooyour - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toocreate un HDInsight cluster in una rete virtuale di Azure e quindi connetterla rete locale tooyour. Informazioni su come tooconfigure la risoluzione dei nomi tra HDInsight e la rete locale tramite un server DNS personalizzato.
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
ms.openlocfilehash: 8a3adf0e3df7726d8e6566d723700506baaf89a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-hdinsight-tooyour-on-premise-network"></a><span data-ttu-id="5864e-104">La connessione di rete locale tooyour di HDInsight</span><span class="sxs-lookup"><span data-stu-id="5864e-104">Connect HDInsight tooyour on-premise network</span></span>

<span data-ttu-id="5864e-105">Informazioni su come tooconnect HDInsight tooyour locale rete tramite reti virtuali di Azure e un gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="5864e-105">Learn how tooconnect HDInsight tooyour on-premises network by using Azure Virtual Networks and a VPN gateway.</span></span> <span data-ttu-id="5864e-106">Questo documento fornisce le informazioni di pianificazione su:</span><span class="sxs-lookup"><span data-stu-id="5864e-106">This document provides planning information on:</span></span>

* <span data-ttu-id="5864e-107">Utilizzo di HDInsight in una rete virtuale di Azure che si connette tooyour locale rete.</span><span class="sxs-lookup"><span data-stu-id="5864e-107">Using HDInsight in an Azure Virtual Network that connects tooyour on-premises network.</span></span>

* <span data-ttu-id="5864e-108">Configurazione di risoluzione dei nomi DNS tra la rete virtuale hello e la rete locale.</span><span class="sxs-lookup"><span data-stu-id="5864e-108">Configuring DNS name resolution between hello virtual network and your on-premises network.</span></span>

* <span data-ttu-id="5864e-109">Configurazione di rete sicurezza gruppi toorestrict internet access tooHDInsight.</span><span class="sxs-lookup"><span data-stu-id="5864e-109">Configuring network security groups toorestrict internet access tooHDInsight.</span></span>

* <span data-ttu-id="5864e-110">Porte fornite da HDInsight nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-110">Ports provided by HDInsight on hello virtual network.</span></span>

## <a name="create-hello-virtual-network-configuration"></a><span data-ttu-id="5864e-111">Creare una configurazione di rete virtuale hello</span><span class="sxs-lookup"><span data-stu-id="5864e-111">Create hello Virtual network configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5864e-112">Se si cercano informazioni aggiuntive dettagliate sulla connessione HDInsight tooyour locale rete tramite una rete virtuale di Azure, vedere hello [rete locale di connettersi a HDInsight tooyour](connect-on-premises-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="5864e-112">If you are looking for step by step guidance on connecting HDInsight tooyour on-premises network using an Azure Virtual Network, see hello [Connect HDInsight tooyour on-premise network](connect-on-premises-network.md) document.</span></span>

<span data-ttu-id="5864e-113">Seguente hello utilizzare documenti toolearn come una rete virtuale di Azure che è connesso tooyour toocreate locale rete:</span><span class="sxs-lookup"><span data-stu-id="5864e-113">Use hello following documents toolearn how toocreate an Azure Virtual Network that is connected tooyour on-premises network:</span></span>
    
* [<span data-ttu-id="5864e-114">Utilizzo di hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5864e-114">Using hello Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [<span data-ttu-id="5864e-115">Uso di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5864e-115">Using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [<span data-ttu-id="5864e-116">Uso dell'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="5864e-116">Using Azure CLI</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a><span data-ttu-id="5864e-117">Configurare la risoluzione dei nomi</span><span class="sxs-lookup"><span data-stu-id="5864e-117">Configure name resolution</span></span>

<span data-ttu-id="5864e-118">tooallow HDInsight e risorse in toocommunicate rete hello unita in join in base al nome, è necessario eseguire hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="5864e-118">tooallow HDInsight and resources in hello joined network toocommunicate by name, you must perform hello following actions:</span></span>

* <span data-ttu-id="5864e-119">Creare un server DNS personalizzato in hello rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5864e-119">Create a custom DNS server in hello Azure Virtual Network.</span></span>

* <span data-ttu-id="5864e-120">Configurare hello rete virtuale toouse hello server DNS personalizzato anziché predefinito hello Resolver ricorsivo di Azure.</span><span class="sxs-lookup"><span data-stu-id="5864e-120">Configure hello virtual network toouse hello custom DNS server instead of hello default Azure Recursive Resolver.</span></span>

* <span data-ttu-id="5864e-121">Configurare l'inoltro tra un server DNS personalizzato hello e il server DNS locale.</span><span class="sxs-lookup"><span data-stu-id="5864e-121">Configure forwarding between hello custom DNS server and your on-premises DNS server.</span></span>

<span data-ttu-id="5864e-122">Questa configurazione consente hello seguente comportamento:</span><span class="sxs-lookup"><span data-stu-id="5864e-122">This configuration enables hello following behavior:</span></span>

* <span data-ttu-id="5864e-123">Le richieste per i nomi di dominio completo che hanno il suffisso DNS hello __per la rete virtuale hello__ vengono inoltrati toohello un server DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="5864e-123">Requests for fully qualified domain names that have hello DNS suffix __for hello virtual network__ are forwarded toohello custom DNS server.</span></span> <span data-ttu-id="5864e-124">un server DNS personalizzato Hello inoltra quindi questi toohello richieste Resolver ricorsivo di Azure, che restituisce l'indirizzo IP hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-124">hello custom DNS server then forwards these requests toohello Azure Recursive Resolver, which returns hello IP address.</span></span>

* <span data-ttu-id="5864e-125">Tutte le altre richieste vengono inoltrate a server DNS di toohello locale.</span><span class="sxs-lookup"><span data-stu-id="5864e-125">All other requests are forwarded toohello on-premises DNS server.</span></span> <span data-ttu-id="5864e-126">Anche le richieste di risorse internet pubblici, ad esempio microsoft.com vengono inoltrate server DNS locale di toohello per la risoluzione dei nomi.</span><span class="sxs-lookup"><span data-stu-id="5864e-126">Even requests for public internet resources such as microsoft.com are forwarded toohello on-premises DNS server for name resolution.</span></span>

<span data-ttu-id="5864e-127">Nel seguente diagramma di hello, linee verdi sono richieste per le risorse che terminano con il suffisso DNS hello della rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-127">In hello following diagram, green lines are requests for resources that end in hello DNS suffix of hello virtual network.</span></span> <span data-ttu-id="5864e-128">Linee blu sono richieste per le risorse nella rete locale hello o nell'hello rete internet pubblica.</span><span class="sxs-lookup"><span data-stu-id="5864e-128">Blue lines are requests for resources in hello on-premises network or on hello public internet.</span></span>

![Diagramma della modalità di risoluzione delle richieste DNS nella configurazione di hello utilizzato in questo documento](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a><span data-ttu-id="5864e-130">Creare un server DNS personalizzato</span><span class="sxs-lookup"><span data-stu-id="5864e-130">Create a custom DNS server</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5864e-131">È necessario creare e configurare i server DNS hello prima di installare HDInsight in rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-131">You must create and configure hello DNS server before installing HDInsight into hello virtual network.</span></span>

<span data-ttu-id="5864e-132">una VM Linux che utilizza hello toocreate [associare](https://www.isc.org/downloads/bind/) software DNS, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5864e-132">toocreate a Linux VM that uses hello [Bind](https://www.isc.org/downloads/bind/) DNS software, use hello following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="5864e-133">i passaggi seguenti Hello usano hello [portale di Azure](https://portal.azure.com) toocreate una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5864e-133">hello following steps use hello [Azure portal](https://portal.azure.com) toocreate an Azure Virtual Machine.</span></span> <span data-ttu-id="5864e-134">Per altri modi toocreate una macchina virtuale, vedere hello [creare VM - CLI di Azure](../virtual-machines/linux/quick-create-cli.md) e [creare VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documenti.</span><span class="sxs-lookup"><span data-stu-id="5864e-134">For other ways toocreate a virtual machine, see hello [Create VM - Azure CLI](../virtual-machines/linux/quick-create-cli.md) and [Create VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documents.</span></span>

1. <span data-ttu-id="5864e-135">Da hello [portale di Azure](https://portal.azure.com)selezionare  __+__ , __calcolo__, e __Ubuntu Server 16.04 LTS__.</span><span class="sxs-lookup"><span data-stu-id="5864e-135">From hello [Azure portal](https://portal.azure.com), select __+__, __Compute__, and __Ubuntu Server 16.04 LTS__.</span></span>

    ![Creare una macchina virtuale Ubuntu](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. <span data-ttu-id="5864e-137">Da hello __nozioni di base__ immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="5864e-137">From hello __Basics__ section, enter hello following information:</span></span>

    * <span data-ttu-id="5864e-138">__Nome__: nome descrittivo che identifica questa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5864e-138">__Name__: A friendly name that identifies this virtual machine.</span></span> <span data-ttu-id="5864e-139">Ad esempio __DNSProxy__.</span><span class="sxs-lookup"><span data-stu-id="5864e-139">For example, __DNSProxy__.</span></span>
    * <span data-ttu-id="5864e-140">__Nome utente__: nome hello di hello account SSH.</span><span class="sxs-lookup"><span data-stu-id="5864e-140">__User name__: hello name of hello SSH account.</span></span>
    * <span data-ttu-id="5864e-141">__La chiave pubblica SSH__ o __Password__: hello metodo di autenticazione per hello account SSH.</span><span class="sxs-lookup"><span data-stu-id="5864e-141">__SSH public key__ or __Password__: hello authentication method for hello SSH account.</span></span> <span data-ttu-id="5864e-142">Si consiglia di usare le chiavi pubbliche, che sono più sicure.</span><span class="sxs-lookup"><span data-stu-id="5864e-142">We recommend using public keys, as they are more secure.</span></span> <span data-ttu-id="5864e-143">Per ulteriori informazioni, vedere hello [creare e usare le chiavi SSH per le macchine virtuali Linux](../virtual-machines/linux/mac-create-ssh-keys.md) documento.</span><span class="sxs-lookup"><span data-stu-id="5864e-143">For more information, see hello [Create and use SSH keys for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span></span>
    * <span data-ttu-id="5864e-144">__Gruppo di risorse__: selezionare __utilizzare esistente__, quindi selezionare gruppo di risorse hello che contiene hello di rete virtuale creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5864e-144">__Resource group__: Select __Use existing__, and then select hello resource group that contains hello virtual network created earlier.</span></span>
    * <span data-ttu-id="5864e-145">__Percorso__: selezionare hello stesso percorso di rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-145">__Location__: Select hello same location as hello virtual network.</span></span>

    ![Configurazione di base della macchina virtuale](./media/connect-on-premises-network/vm-basics.png)

    <span data-ttu-id="5864e-147">Lasciare le altre voci in hello valori predefiniti e quindi selezionare __OK__.</span><span class="sxs-lookup"><span data-stu-id="5864e-147">Leave other entries at hello default values and then select __OK__.</span></span>

3. <span data-ttu-id="5864e-148">Da hello __scegliere una dimensione__ sezione, dimensioni della macchina virtuale selezionare hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-148">From hello __Choose a size__ section, select hello VM size.</span></span> <span data-ttu-id="5864e-149">Per questa esercitazione, selezionare più piccolo hello e opzione di costo più basso.</span><span class="sxs-lookup"><span data-stu-id="5864e-149">For this tutorial, select hello smallest and lowest cost option.</span></span> <span data-ttu-id="5864e-150">toocontinue, utilizzare hello __selezionare__ pulsante.</span><span class="sxs-lookup"><span data-stu-id="5864e-150">toocontinue, use hello __Select__ button.</span></span>

4. <span data-ttu-id="5864e-151">Da hello __impostazioni__ immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="5864e-151">From hello __Settings__ section, enter hello following information:</span></span>

    * <span data-ttu-id="5864e-152">__Rete virtuale__: selezionare hello rete virtuale creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5864e-152">__Virtual network__: Select hello virtual network that you created earlier.</span></span>

    * <span data-ttu-id="5864e-153">__Subnet__: selezionare hello predefinito subnet per la rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-153">__Subnet__: Select hello default subnet for hello virtual network.</span></span> <span data-ttu-id="5864e-154">Eseguire __non__ selezionare hello subnet usata dal gateway VPN hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-154">Do __not__ select hello subnet used by hello VPN gateway.</span></span>

    * <span data-ttu-id="5864e-155">__Account di archiviazione di diagnostica__: selezionare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="5864e-155">__Diagnostics storage account__: Either select an existing storage account or create a new one.</span></span>

    ![Impostazioni della rete virtuale](./media/connect-on-premises-network/virtual-network-settings.png)

    <span data-ttu-id="5864e-157">Mantenere hello altre voci hello valore predefinito, quindi selezionare __OK__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="5864e-157">Leave hello other entries at hello default value, then select __OK__ toocontinue.</span></span>

5. <span data-ttu-id="5864e-158">Da hello __acquisto__ sezione, seleziona hello __acquisto__ macchina virtuale di hello toocreate pulsante.</span><span class="sxs-lookup"><span data-stu-id="5864e-158">From hello __Purchase__ section, select hello __Purchase__ button toocreate hello virtual machine.</span></span>

6. <span data-ttu-id="5864e-159">Dopo aver creato, macchina virtuale hello relativo __Panoramica__ sezione viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="5864e-159">Once hello virtual machine has been created, its __Overview__ section is displayed.</span></span> <span data-ttu-id="5864e-160">Selezionare nell'elenco a sinistra di hello hello __proprietà__.</span><span class="sxs-lookup"><span data-stu-id="5864e-160">From hello list on hello left, select __Properties__.</span></span> <span data-ttu-id="5864e-161">Salvare hello __indirizzo IP pubblico__ e __indirizzo IP privato__ valori.</span><span class="sxs-lookup"><span data-stu-id="5864e-161">Save hello __Public IP address__ and __Private IP address__ values.</span></span> <span data-ttu-id="5864e-162">Da utilizzare nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-162">It will be used in hello next section.</span></span>

    ![Indirizzi IP pubblico e privato](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a><span data-ttu-id="5864e-164">Installare e configurare Bind (software DNS)</span><span class="sxs-lookup"><span data-stu-id="5864e-164">Install and configure Bind (DNS software)</span></span>

1. <span data-ttu-id="5864e-165">Usare SSH tooconnect toohello __indirizzo IP pubblico__ della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-165">Use SSH tooconnect toohello __public IP address__ of hello virtual machine.</span></span> <span data-ttu-id="5864e-166">Hello di esempio seguente si connette a macchina virtuale tooa in 40.68.254.142:</span><span class="sxs-lookup"><span data-stu-id="5864e-166">hello following example connects tooa virtual machine at 40.68.254.142:</span></span>

    ```bash
    ssh sshuser@40.68.254.142
    ```

    <span data-ttu-id="5864e-167">Sostituire `sshuser` con account utente SSH hello specificata durante la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-167">Replace `sshuser` with hello SSH user account you specified when creating hello cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5864e-168">Sono disponibili un'ampia gamma di hello tooobtain modi `ssh` utilità.</span><span class="sxs-lookup"><span data-stu-id="5864e-168">There are a variety of ways tooobtain hello `ssh` utility.</span></span> <span data-ttu-id="5864e-169">Su Linux, Unix e macOS, viene fornito come parte del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-169">On Linux, Unix, and macOS, it is provided as part of hello operating system.</span></span> <span data-ttu-id="5864e-170">Se si utilizza Windows, è possibile utilizzare una delle seguenti opzioni hello:</span><span class="sxs-lookup"><span data-stu-id="5864e-170">If you are using Windows, consider one of hello following options:</span></span>
    >
    > * [<span data-ttu-id="5864e-171">Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="5864e-171">Azure Cloud Shell</span></span>](../cloud-shell/quickstart.md)
    > * [<span data-ttu-id="5864e-172">Bash in Ubuntu su Windows 10</span><span class="sxs-lookup"><span data-stu-id="5864e-172">Bash on Ubuntu on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/about)
    > * [<span data-ttu-id="5864e-173">Git (https://git-scm.com/)</span><span class="sxs-lookup"><span data-stu-id="5864e-173">Git (https://git-scm.com/)</span></span>](https://git-scm.com/)
    > * [<span data-ttu-id="5864e-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span><span class="sxs-lookup"><span data-stu-id="5864e-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. <span data-ttu-id="5864e-175">tooinstall Bind, utilizzare hello comandi dalla sessione SSH hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="5864e-175">tooinstall Bind, use hello following commands from hello SSH session:</span></span>

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. <span data-ttu-id="5864e-176">tooconfigure binding tooforward nome risoluzione richieste tooyour locale server DNS, utilizzare hello segue testo come contenuto di hello di hello `/etc/bind/named.conf.options` file:</span><span class="sxs-lookup"><span data-stu-id="5864e-176">tooconfigure Bind tooforward name resolution requests tooyour on-prem DNS server, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

        acl goodclients {
            10.0.0.0/16; # Replace with hello IP address range of hello virtual network
            10.1.0.0/16; # Replace with hello IP address range of hello on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with hello IP address of hello on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform tooRFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > <span data-ttu-id="5864e-177">Sostituire i valori hello in hello `goodclients` sezione con intervallo di indirizzi IP hello di rete virtuale hello e rete locale.</span><span class="sxs-lookup"><span data-stu-id="5864e-177">Replace hello values in hello `goodclients` section with hello IP address range of hello virtual network and on-premises network.</span></span> <span data-ttu-id="5864e-178">In questa sezione definisce gli indirizzi di hello che questo server DNS accetta richieste da.</span><span class="sxs-lookup"><span data-stu-id="5864e-178">This section defines hello addresses that this DNS server accepts requests from.</span></span>
    >
    > <span data-ttu-id="5864e-179">Sostituire hello `192.168.0.1` voce hello `forwarders` sezione con l'indirizzo IP hello del server DNS locale.</span><span class="sxs-lookup"><span data-stu-id="5864e-179">Replace hello `192.168.0.1` entry in hello `forwarders` section with hello IP address of your on-premises DNS server.</span></span> <span data-ttu-id="5864e-180">Questo tooyour di richieste DNS route voce DNS server locale per la risoluzione.</span><span class="sxs-lookup"><span data-stu-id="5864e-180">This entry routes DNS requests tooyour on-premises DNS server for resolution.</span></span>

    <span data-ttu-id="5864e-181">tooedit questo file, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5864e-181">tooedit this file, use hello following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    <span data-ttu-id="5864e-182">file hello toosave, usare __Ctrl + X__, __Y__e quindi __invio__.</span><span class="sxs-lookup"><span data-stu-id="5864e-182">toosave hello file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

4. <span data-ttu-id="5864e-183">Dalla sessione SSH hello, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5864e-183">From hello SSH session, use hello following command:</span></span>

    ```bash
    hostname -f
    ```

    <span data-ttu-id="5864e-184">Questo comando restituisce un toohello simile valore testo seguente:</span><span class="sxs-lookup"><span data-stu-id="5864e-184">This command returns a value similar toohello following text:</span></span>

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    <span data-ttu-id="5864e-185">Hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` testo è hello __suffisso DNS__ per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="5864e-185">hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is hello __DNS suffix__ for this virtual network.</span></span> <span data-ttu-id="5864e-186">Salvare questo valore, che verrà usato in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="5864e-186">Save this value, as it is used later.</span></span>

5. <span data-ttu-id="5864e-187">i nomi DNS di tooconfigure binding tooresolve delle risorse in rete virtuale hello, utilizzare hello segue testo come contenuto di hello di hello `/etc/bind/named.conf.local` file:</span><span class="sxs-lookup"><span data-stu-id="5864e-187">tooconfigure Bind tooresolve DNS names for resources within hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.local` file:</span></span>

        // Replace hello following with hello DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # hello Azure recursive resolver
        };

    > [!IMPORTANT]
    > <span data-ttu-id="5864e-188">È necessario sostituire hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` con il suffisso DNS hello recuperati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5864e-188">You must replace hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` with hello DNS suffix you retrieved earlier.</span></span>

    <span data-ttu-id="5864e-189">tooedit questo file, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5864e-189">tooedit this file, use hello following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    <span data-ttu-id="5864e-190">file hello toosave, usare __Ctrl + X__, __Y__e quindi __invio__.</span><span class="sxs-lookup"><span data-stu-id="5864e-190">toosave hello file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

6. <span data-ttu-id="5864e-191">toostart Bind, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5864e-191">toostart Bind, use hello following command:</span></span>

    ```bash
    sudo service bind9 restart
    ```

7. <span data-ttu-id="5864e-192">tooverify che associano può risolvere i nomi di hello delle risorse nella rete locale, hello di utilizzare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5864e-192">tooverify that bind can resolve hello names of resources in your on-premises network, use hello following commands:</span></span>

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="5864e-193">Sostituire `dns.mynetwork.net` con il nome di dominio completo hello (FQDN) di una risorsa nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="5864e-193">Replace `dns.mynetwork.net` with hello fully qualified domain name (FQDN) of a resource in your on-premises network.</span></span>
    >
    > <span data-ttu-id="5864e-194">Sostituire `10.0.0.4` con hello __indirizzo IP interno__ del server DNS nella rete virtuale hello personalizzato.</span><span class="sxs-lookup"><span data-stu-id="5864e-194">Replace `10.0.0.4` with hello __internal IP address__ of your custom DNS server in hello virtual network.</span></span>

    <span data-ttu-id="5864e-195">viene visualizzata la risposta di Hello toohello simile, il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="5864e-195">hello response appears similar toohello following text:</span></span>

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-hello-virtual-network-toouse-hello-custom-dns-server"></a><span data-ttu-id="5864e-196">Configurare hello toouse hello personalizzato DNS server di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="5864e-196">Configure hello virtual network toouse hello custom DNS server</span></span>

<span data-ttu-id="5864e-197">tooconfigure hello rete virtuale toouse hello server DNS personalizzato anziché hello resolver ricorsivo Azure, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5864e-197">tooconfigure hello virtual network toouse hello custom DNS server instead of hello Azure recursive resolver, use hello following steps:</span></span>

1. <span data-ttu-id="5864e-198">In hello [portale di Azure](https://portal.azure.com), selezionare la rete virtuale hello e quindi selezionare __server DNS__.</span><span class="sxs-lookup"><span data-stu-id="5864e-198">In hello [Azure portal](https://portal.azure.com), select hello virtual network, and then select __DNS Servers__.</span></span>

2. <span data-ttu-id="5864e-199">Selezionare __personalizzato__, quindi immettere hello __indirizzo IP interno__ del server DNS personalizzato hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-199">Select __Custom__, and enter hello __internal IP address__ of hello custom DNS server.</span></span> <span data-ttu-id="5864e-200">Infine, selezionare __Salva__.</span><span class="sxs-lookup"><span data-stu-id="5864e-200">Finally, select __Save__.</span></span>

    ![Impostare hello del server DNS personalizzato per la rete hello](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-hello-on-premises-dns-server"></a><span data-ttu-id="5864e-202">Configurare i server DNS locale di hello</span><span class="sxs-lookup"><span data-stu-id="5864e-202">Configure hello on-premises DNS server</span></span>

<span data-ttu-id="5864e-203">Nella sezione precedente hello è configurato hello DNS server tooforward richieste toohello locale server DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="5864e-203">In hello previous section, you configured hello custom DNS server tooforward requests toohello on-premises DNS server.</span></span> <span data-ttu-id="5864e-204">Successivamente, è necessario configurare hello locale DNS server tooforward richieste toohello server DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="5864e-204">Next, you must configure hello on-premises DNS server tooforward requests toohello custom DNS server.</span></span>

<span data-ttu-id="5864e-205">Per i passaggi specifici su come tooconfigure il server DNS, consultare la documentazione hello per il software del server DNS.</span><span class="sxs-lookup"><span data-stu-id="5864e-205">For specific steps on how tooconfigure your DNS server, consult hello documentation for your DNS server software.</span></span> <span data-ttu-id="5864e-206">Cercare la procedura di hello tooconfigure un __server d'inoltro condizionale__.</span><span class="sxs-lookup"><span data-stu-id="5864e-206">Look for hello steps on how tooconfigure a __conditional forwarder__.</span></span>

<span data-ttu-id="5864e-207">L'inoltro condizionale consente di inoltrare solo le richieste per un suffisso DNS specifico.</span><span class="sxs-lookup"><span data-stu-id="5864e-207">A conditional forward only forwards requests for a specific DNS suffix.</span></span> <span data-ttu-id="5864e-208">In questo caso, è necessario configurare un server d'inoltro per il suffisso DNS hello della rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-208">In this case, you must configure a forwarder for hello DNS suffix of hello virtual network.</span></span> <span data-ttu-id="5864e-209">Le richieste per questo suffisso devono essere inoltrate toohello di indirizzo IP del server DNS personalizzato hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-209">Requests for this suffix should be forwarded toohello IP address of hello custom DNS server.</span></span> 

<span data-ttu-id="5864e-210">testo Hello è riportato un esempio di una configurazione di server d'inoltro condizionale per hello **associare** software DNS:</span><span class="sxs-lookup"><span data-stu-id="5864e-210">hello following text is an example of a conditional forwarder configuration for hello **Bind** DNS software:</span></span>

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello custom DNS server's internal IP address
    };

<span data-ttu-id="5864e-211">Per informazioni sull'utilizzo di DNS in **Windows Server 2016**, vedere hello [Aggiungi DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentazione...</span><span class="sxs-lookup"><span data-stu-id="5864e-211">For information on using DNS on **Windows Server 2016**, see hello [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...</span></span>

<span data-ttu-id="5864e-212">Dopo aver configurato i server DNS di hello locale, è possibile utilizzare `nslookup` da tooverify di rete locale hello che è possibile risolvere i nomi nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-212">Once you have configured hello on-premises DNS server, you can use `nslookup` from hello on-premises network tooverify that you can resolve names in hello virtual network.</span></span> <span data-ttu-id="5864e-213">esempio di seguente Hello</span><span class="sxs-lookup"><span data-stu-id="5864e-213">hello following example</span></span> 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

<span data-ttu-id="5864e-214">In questo esempio utilizza hello server DNS locale in 196.168.0.4 tooresolve nome di hello del server DNS personalizzato hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-214">This example uses hello on-premises DNS server at 196.168.0.4 tooresolve hello name of hello custom DNS server.</span></span> <span data-ttu-id="5864e-215">Sostituire l'indirizzo IP hello con hello per il server DNS locale di hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-215">Replace hello IP address with hello one for hello on-premises DNS server.</span></span> <span data-ttu-id="5864e-216">Sostituire hello `dnsproxy` indirizzo con il nome di dominio completo hello del server DNS personalizzato hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-216">Replace hello `dnsproxy` address with hello fully qualified domain name of hello custom DNS server.</span></span>

## <a name="optional-control-network-traffic"></a><span data-ttu-id="5864e-217">Facoltativo: Controllare il traffico di rete</span><span class="sxs-lookup"><span data-stu-id="5864e-217">Optional: Control network traffic</span></span>

<span data-ttu-id="5864e-218">È possibile utilizzare gruppi di sicurezza di rete (gruppo) o il traffico di rete toocontrol route definite dall'utente (UDR).</span><span class="sxs-lookup"><span data-stu-id="5864e-218">You can use network security groups (NSG) or user-defined routes (UDR) toocontrol network traffic.</span></span> <span data-ttu-id="5864e-219">NSGs consentono di toofilter in ingresso e in uscita, il traffico e consentire o negare il traffico di hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-219">NSGs allow you toofilter inbound and outbound traffic, and allow or deny hello traffic.</span></span> <span data-ttu-id="5864e-220">UDRs consentono toocontrol come flussi di traffico tra le risorse nella rete virtuale hello hello internet e hello rete locale.</span><span class="sxs-lookup"><span data-stu-id="5864e-220">UDRs allow you toocontrol how traffic flows between resources in hello virtual network, hello internet, and hello on-premises network.</span></span>

> [!WARNING]
> <span data-ttu-id="5864e-221">HDInsight richiede l'accesso in ingresso da indirizzi IP specifici nel cloud di Azure hello e accesso in uscita senza restrizioni.</span><span class="sxs-lookup"><span data-stu-id="5864e-221">HDInsight requires inbound access from specific IP addresses in hello Azure cloud, and unrestricted outbound access.</span></span> <span data-ttu-id="5864e-222">Quando si utilizza il traffico di toocontrol NSGs o UDRs, è necessario eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5864e-222">When using NSGs or UDRs toocontrol traffic, you must perform hello following steps:</span></span>
>
> 1. <span data-ttu-id="5864e-223">Trovare hello gli indirizzi IP per il percorso di hello che contiene la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="5864e-223">Find hello IP addresses for hello location that contains your virtual network.</span></span> <span data-ttu-id="5864e-224">Per un elenco di indirizzi IP necessari in base alla località, vedere [Indirizzi IP richiesti](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="5864e-224">For a list of required IPs by location, see [Required IP addresses](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span></span>
>
> 2. <span data-ttu-id="5864e-225">Consentire il traffico in ingresso da indirizzi IP hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-225">Allow inbound traffic from hello IP addresses.</span></span>
>
>    * <span data-ttu-id="5864e-226">__GRUPPO__: Consenti __in ingresso__ il traffico sulla porta __443__ da hello __Internet__.</span><span class="sxs-lookup"><span data-stu-id="5864e-226">__NSG__: Allow __inbound__ traffic on port __443__ from hello __Internet__.</span></span>
>    * <span data-ttu-id="5864e-227">__UDR__: hello Set __Hop successivo__ tipo too__Internet__ route hello.</span><span class="sxs-lookup"><span data-stu-id="5864e-227">__UDR__: Set hello __Next Hop__ type of hello route too__Internet__.</span></span>

<span data-ttu-id="5864e-228">Per un esempio di utilizzo di Azure PowerShell o hello Azure CLI toocreate NSGs, vedere hello [estendere HDInsight con reti virtuali di Azure](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) documento.</span><span class="sxs-lookup"><span data-stu-id="5864e-228">For an example of using Azure PowerShell or hello Azure CLI toocreate NSGs, see hello [Extend HDInsight with Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span></span>

## <a name="create-hello-hdinsight-cluster"></a><span data-ttu-id="5864e-229">Creare cluster HDInsight hello</span><span class="sxs-lookup"><span data-stu-id="5864e-229">Create hello HDInsight cluster</span></span>

> [!WARNING]
> <span data-ttu-id="5864e-230">È necessario configurare un server DNS personalizzato hello prima di installare la rete virtuale hello HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5864e-230">You must configure hello custom DNS server before installing HDInsight in hello virtual network.</span></span>

<span data-ttu-id="5864e-231">Hello di utilizzare i passaggi in hello [creare un cluster HDInsight tramite il portale di Azure hello](./hdinsight-hadoop-create-linux-clusters-portal.md) toocreate documento un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5864e-231">Use hello steps in hello [Create an HDInsight cluster using hello Azure portal](./hdinsight-hadoop-create-linux-clusters-portal.md) document toocreate an HDInsight cluster.</span></span>

> [!WARNING]
> * <span data-ttu-id="5864e-232">Durante la creazione del cluster, è necessario scegliere il percorso hello contenente la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="5864e-232">During cluster creation, you must choose hello location that contains your virtual network.</span></span>
>
> * <span data-ttu-id="5864e-233">In hello __impostazioni avanzate__ parte della configurazione, è necessario selezionare la rete virtuale hello e subnet creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5864e-233">In hello __Advanced settings__ part of configuration, you must select hello virtual network and subnet that you created earlier.</span></span>

## <a name="connecting-toohdinsight"></a><span data-ttu-id="5864e-234">Connessione tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="5864e-234">Connecting tooHDInsight</span></span>

<span data-ttu-id="5864e-235">La maggior parte delle documentazione su HDInsight si presuppone la presenza di cluster di accesso toohello su hello internet.</span><span class="sxs-lookup"><span data-stu-id="5864e-235">Most documentation on HDInsight assumes that you have access toohello cluster over hello internet.</span></span> <span data-ttu-id="5864e-236">Ad esempio, che è possibile connettersi cluster toohello https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="5864e-236">For example, that you can connect toohello cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="5864e-237">Questo indirizzo Usa gateway hello pubblico, non è disponibile se è stato utilizzato NSGs o UDRs toorestrict accesso da hello internet.</span><span class="sxs-lookup"><span data-stu-id="5864e-237">This address uses hello public gateway, which is not available if you have used NSGs or UDRs toorestrict access from hello internet.</span></span>

<span data-ttu-id="5864e-238">toodirectly connessione tooHDInsight attraverso la rete virtuale hello, usare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5864e-238">toodirectly connect tooHDInsight through hello virtual network, use hello following steps:</span></span>

1. <span data-ttu-id="5864e-239">i nomi di dominio completo interno hello toodiscover hello HDInsight dei nodi del cluster, utilizzare uno dei seguenti metodi hello:</span><span class="sxs-lookup"><span data-stu-id="5864e-239">toodiscover hello internal fully qualified domain names of hello HDInsight cluster nodes, use one of hello following methods:</span></span>

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

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

2. <span data-ttu-id="5864e-240">porta hello toodetermine che un servizio è disponibile, vedere hello [porte utilizzate da servizi di Hadoop in HDInsight](./hdinsight-hadoop-port-settings-for-services.md) documento.</span><span class="sxs-lookup"><span data-stu-id="5864e-240">toodetermine hello port that a service is available on, see hello [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="5864e-241">Alcuni servizi ospitate nei nodi head hello attivi solo in un nodo alla volta.</span><span class="sxs-lookup"><span data-stu-id="5864e-241">Some services hosted on hello head nodes are only active on one node at a time.</span></span> <span data-ttu-id="5864e-242">Se si tenta di accedere al servizio in un nodo head e si verifica un errore, passare toohello altro nodo head.</span><span class="sxs-lookup"><span data-stu-id="5864e-242">If you try accessing a service on one head node and it fails, switch toohello other head node.</span></span>
    >
    > <span data-ttu-id="5864e-243">Ambari, ad esempio, è attivo solo in un nodo head per volta.</span><span class="sxs-lookup"><span data-stu-id="5864e-243">For example, Ambari is only active on one head node at a time.</span></span> <span data-ttu-id="5864e-244">Se si tenta l'accesso a un nodo head Ambari e viene restituito un errore 404, tramite cui viene eseguito hello altro nodo head.</span><span class="sxs-lookup"><span data-stu-id="5864e-244">If you try accessing Ambari on one head node and it returns a 404 error, then it is running on hello other head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5864e-245">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5864e-245">Next steps</span></span>

* <span data-ttu-id="5864e-246">Per altre informazioni sull'uso di HDInsight in una rete virtuale, vedere [Estendere le funzionalità di HDInsight usando Rete virtuale di Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="5864e-246">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

* <span data-ttu-id="5864e-247">Per ulteriori informazioni su reti virtuali di Azure, vedere hello [Cenni preliminari sulla rete virtuale di Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5864e-247">For more information on Azure virtual networks, see hello [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="5864e-248">Per altre informazioni sui gruppi di sicurezza di rete, vedere [Gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="5864e-248">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="5864e-249">Per altre informazioni sulle route definite dall'utente, vedere [Route definite dall'utente e inoltro IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5864e-249">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>
