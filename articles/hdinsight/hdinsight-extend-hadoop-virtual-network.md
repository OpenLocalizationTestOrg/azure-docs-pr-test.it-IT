---
title: HDInsight con rete virtuale di Azure - aaaExtend | Documenti Microsoft
description: Informazioni su come toouse rete virtuale di Azure tooconnect HDInsight tooother cloud risorse o le risorse nel Data Center
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: ba80be4d9f280c6c62fa8acc996ef5f921acdbbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a><span data-ttu-id="74f5d-103">Estendere Azure HDInsight usando Rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="74f5d-103">Extend Azure HDInsight using an Azure Virtual Network</span></span>

<span data-ttu-id="74f5d-104">Informazioni su come toouse HDInsight con un [rete virtuale di Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="74f5d-104">Learn how toouse HDInsight with an [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="74f5d-105">L'utilizzo di una rete virtuale di Azure consente hello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="74f5d-105">Using an Azure Virtual Network enables hello following scenarios:</span></span>

* <span data-ttu-id="74f5d-106">Connessione tooHDInsight direttamente da una rete locale.</span><span class="sxs-lookup"><span data-stu-id="74f5d-106">Connecting tooHDInsight directly from an on-premises network.</span></span>

* <span data-ttu-id="74f5d-107">Connessione toodata HDInsight vengono archiviati in una rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="74f5d-107">Connecting HDInsight toodata stores in an Azure Virtual network.</span></span>

* <span data-ttu-id="74f5d-108">L'accesso ai servizi di Hadoop che non sono disponibili pubblicamente in salve direttamente a internet.</span><span class="sxs-lookup"><span data-stu-id="74f5d-108">Directly accessing Hadoop services that are not available publicly over hello internet.</span></span> <span data-ttu-id="74f5d-109">Ad esempio, le API Kafka o hello API Java HBase.</span><span class="sxs-lookup"><span data-stu-id="74f5d-109">For example, Kafka APIs or hello HBase Java API.</span></span>

> [!WARNING]
> <span data-ttu-id="74f5d-110">informazioni di Hello in questo documento richiedono la comprensione delle reti TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="74f5d-110">hello information in this document requires an understanding of TCP/IP networking.</span></span> <span data-ttu-id="74f5d-111">Se non si ha familiarità con la rete TCP/IP, è necessario collaborare con un utente prima di apportare modifiche tooproduction reti.</span><span class="sxs-lookup"><span data-stu-id="74f5d-111">If you are not familiar with TCP/IP networking, you should partner with someone who is before making modifications tooproduction networks.</span></span>

## <a name="planning"></a><span data-ttu-id="74f5d-112">Pianificazione</span><span class="sxs-lookup"><span data-stu-id="74f5d-112">Planning</span></span>

<span data-ttu-id="74f5d-113">di seguito Hello sono domande hello che è necessario rispondere durante la pianificazione tooinstall HDInsight in una rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="74f5d-113">hello following are hello questions that you must answer when planning tooinstall HDInsight in a virtual network:</span></span>

* <span data-ttu-id="74f5d-114">È necessario tooinstall HDInsight in una rete virtuale esistente?</span><span class="sxs-lookup"><span data-stu-id="74f5d-114">Do you need tooinstall HDInsight into an existing virtual network?</span></span> <span data-ttu-id="74f5d-115">Oppure si intende creare una rete nuova?</span><span class="sxs-lookup"><span data-stu-id="74f5d-115">Or are you creating a new network?</span></span>

    <span data-ttu-id="74f5d-116">Se si utilizza una rete virtuale esistente, potrebbe essere la configurazione di rete hello toomodify prima di poter installare HDInsight.</span><span class="sxs-lookup"><span data-stu-id="74f5d-116">If you are using an existing virtual network, you may need toomodify hello network configuration before you can install HDInsight.</span></span> <span data-ttu-id="74f5d-117">Per ulteriori informazioni, vedere hello [aggiungere la rete virtuale esistente di HDInsight tooan](#existingvnet) sezione.</span><span class="sxs-lookup"><span data-stu-id="74f5d-117">For more information, see hello [add HDInsight tooan existing virtual network](#existingvnet) section.</span></span>

* <span data-ttu-id="74f5d-118">Si desidera rete virtuale hello tooconnect contenente una rete virtuale di HDInsight tooanother o la rete locale?</span><span class="sxs-lookup"><span data-stu-id="74f5d-118">Do you want tooconnect hello virtual network containing HDInsight tooanother virtual network or your on-premises network?</span></span>

    <span data-ttu-id="74f5d-119">lavoro tooeasily con risorse tra le reti, è possibile necessario toocreate un DNS personalizzato e configurare l'inoltro di DNS.</span><span class="sxs-lookup"><span data-stu-id="74f5d-119">tooeasily work with resources across networks, you may need toocreate a custom DNS and configure DNS forwarding.</span></span> <span data-ttu-id="74f5d-120">Per ulteriori informazioni, vedere hello [la connessione di più reti](#multinet) sezione.</span><span class="sxs-lookup"><span data-stu-id="74f5d-120">For more information, see hello [connecting multiple networks](#multinet) section.</span></span>

* <span data-ttu-id="74f5d-121">Si desidera toorestrict/reindirizzamento del traffico in ingresso o in uscita tooHDInsight?</span><span class="sxs-lookup"><span data-stu-id="74f5d-121">Do you want toorestrict/redirect inbound or outbound traffic tooHDInsight?</span></span>

    <span data-ttu-id="74f5d-122">HDInsight deve avere la comunicazione con indirizzi IP specifici nel hello data center di Azure senza restrizioni.</span><span class="sxs-lookup"><span data-stu-id="74f5d-122">HDInsight must have unrestricted communication with specific IP addresses in hello Azure data center.</span></span> <span data-ttu-id="74f5d-123">Sono presenti anche diverse porte che devono essere abilitate attraverso i firewall per la comunicazione client.</span><span class="sxs-lookup"><span data-stu-id="74f5d-123">There are also several ports that must be allowed through firewalls for client communication.</span></span> <span data-ttu-id="74f5d-124">Per ulteriori informazioni, vedere hello [controllare il traffico di rete](#networktraffic) sezione.</span><span class="sxs-lookup"><span data-stu-id="74f5d-124">For more information, see hello [controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="74f5d-125"><a id="existingvnet"></a>Aggiungere la rete virtuale esistente tooan a HDInsight</span><span class="sxs-lookup"><span data-stu-id="74f5d-125"><a id="existingvnet"></a>Add HDInsight tooan existing virtual network</span></span>

<span data-ttu-id="74f5d-126">Utilizzare i passaggi di hello in questa sezione di toodiscover come tooadd un tooan HDInsight nuova rete virtuale di Azure esistente.</span><span class="sxs-lookup"><span data-stu-id="74f5d-126">Use hello steps in this section toodiscover how tooadd a new HDInsight tooan existing Azure Virtual Network.</span></span>

> [!NOTE]
> <span data-ttu-id="74f5d-127">È possibile aggiungere un cluster HDInsight esistente in una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="74f5d-127">You cannot add an existing HDInsight cluster into a virtual network.</span></span>

1. <span data-ttu-id="74f5d-128">Si sta utilizzando un classico o il modello di distribuzione di gestione risorse per la rete virtuale hello?</span><span class="sxs-lookup"><span data-stu-id="74f5d-128">Are you using a classic or Resource Manager deployment model for hello virtual network?</span></span>

    <span data-ttu-id="74f5d-129">HDInsight 3.4 e versione successiva richiedono l'utilizzo di una rete virtuale di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="74f5d-129">HDInsight 3.4 and greater requires a Resource Manager virtual network.</span></span> <span data-ttu-id="74f5d-130">Le versioni precedenti di HDInsight richiedono una rete virtuale classica.</span><span class="sxs-lookup"><span data-stu-id="74f5d-130">Earlier versions of HDInsight required a classic virtual network.</span></span>

    <span data-ttu-id="74f5d-131">Se la rete esistente è una rete virtuale classica, è necessario creare una rete virtuale di gestione delle risorse e quindi connettersi hello due.</span><span class="sxs-lookup"><span data-stu-id="74f5d-131">If your existing network is a classic virtual network, then you must create a Resource Manager virtual network and then connect hello two.</span></span> <span data-ttu-id="74f5d-132">[Connessione toonew reti virtuali classiche reti virtuali](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span><span class="sxs-lookup"><span data-stu-id="74f5d-132">[Connecting classic VNets toonew VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

    <span data-ttu-id="74f5d-133">Una volta inserito, HDInsight installato nella rete di gestione risorse di hello possibile interagire con le risorse di rete classiche hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-133">Once joined, HDInsight installed in hello Resource Manager network can interact with resources in hello classic network.</span></span>

2. <span data-ttu-id="74f5d-134">Si usa il tunneling forzato?</span><span class="sxs-lookup"><span data-stu-id="74f5d-134">Do you use forced tunneling?</span></span> <span data-ttu-id="74f5d-135">Il tunneling forzato è impostata una subnet che forza una periferica di tooa il traffico Internet in uscita per l'ispezione e la registrazione.</span><span class="sxs-lookup"><span data-stu-id="74f5d-135">Forced tunneling is a subnet setting that forces outbound Internet traffic tooa device for inspection and logging.</span></span> <span data-ttu-id="74f5d-136">HDInsight non supporta il tunneling forzato.</span><span class="sxs-lookup"><span data-stu-id="74f5d-136">HDInsight does not support forced tunneling.</span></span> <span data-ttu-id="74f5d-137">Occorre quindi rimuovere questa funzionalità prima di installare HDInsight in una subnet oppure si può creare una nuova subnet per HDInsight.</span><span class="sxs-lookup"><span data-stu-id="74f5d-137">Either remove forced tunneling before installing HDInsight into a subnet, or create a new subnet for HDInsight.</span></span>

3. <span data-ttu-id="74f5d-138">Si usano gruppi di sicurezza di rete, le route definite dall'utente o il traffico toorestrict ai dispositivi di rete virtuale da o verso la rete virtuale hello?</span><span class="sxs-lookup"><span data-stu-id="74f5d-138">Do you use network security groups, user-defined routes, or Virtual Network Appliances toorestrict traffic into or out of hello virtual network?</span></span>

    <span data-ttu-id="74f5d-139">Come servizio gestito, HDInsight richiede l'accesso illimitato tooseveral degli indirizzi IP in hello data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="74f5d-139">As a managed service, HDInsight requires unrestricted access tooseveral IP addresses in hello Azure data center.</span></span> <span data-ttu-id="74f5d-140">tooallow comunicazione con questi indirizzi IP, aggiornare eventuali gruppi di sicurezza di rete esistente o di una route definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="74f5d-140">tooallow communication with these IP addresses, update any existing network security groups or user-defined routes.</span></span>

    <span data-ttu-id="74f5d-141">HDInsight ospita più servizi, che usano porte diverse.</span><span class="sxs-lookup"><span data-stu-id="74f5d-141">HDInsight  hosts multiple services, which use a variety of ports.</span></span> <span data-ttu-id="74f5d-142">Non bloccare le porte toothese di traffico.</span><span class="sxs-lookup"><span data-stu-id="74f5d-142">Do not block traffic toothese ports.</span></span> <span data-ttu-id="74f5d-143">Per un elenco di porte tooallow attraverso i firewall appliance virtuale, vedere hello [sicurezza](#security) sezione.</span><span class="sxs-lookup"><span data-stu-id="74f5d-143">For a list of ports tooallow through virtual appliance firewalls, see hello [Security](#security) section.</span></span>

    <span data-ttu-id="74f5d-144">toofind la configurazione di protezione esistente, utilizzare hello seguenti comandi di Azure PowerShell o l'interfaccia CLI di Azure:</span><span class="sxs-lookup"><span data-stu-id="74f5d-144">toofind your existing security configuration, use hello following Azure PowerShell or Azure CLI commands:</span></span>

    * <span data-ttu-id="74f5d-145">Gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="74f5d-145">Network security groups</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="74f5d-146">Per ulteriori informazioni, vedere hello [risolvere i problemi relativi a gruppi di sicurezza di rete](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) documento.</span><span class="sxs-lookup"><span data-stu-id="74f5d-146">For more information, see hello [Troubleshoot network security groups](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="74f5d-147">Le regole di gruppo di sicurezza di rete vengono applicate seguendo un ordine basato sulla priorità delle regole.</span><span class="sxs-lookup"><span data-stu-id="74f5d-147">Network security group rules are applied in order based on rule priority.</span></span> <span data-ttu-id="74f5d-148">viene applicata Hello prima regola corrispondente a modello di traffico hello e non da altri vengono applicate per il traffico.</span><span class="sxs-lookup"><span data-stu-id="74f5d-148">hello first rule that matches hello traffic pattern is applied, and no others are applied for that traffic.</span></span> <span data-ttu-id="74f5d-149">Ordine delle regole da tooleast più permissivo.</span><span class="sxs-lookup"><span data-stu-id="74f5d-149">Order rules from most permissive tooleast permissive.</span></span> <span data-ttu-id="74f5d-150">Per ulteriori informazioni, vedere hello [filtrare il traffico di rete con gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md) documento.</span><span class="sxs-lookup"><span data-stu-id="74f5d-150">For more information, see hello [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    * <span data-ttu-id="74f5d-151">Route definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="74f5d-151">User-defined routes</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="74f5d-152">Per ulteriori informazioni, vedere hello [risolvere route](../virtual-network/virtual-network-routes-troubleshoot-portal.md) documento.</span><span class="sxs-lookup"><span data-stu-id="74f5d-152">For more information, see hello [Troubleshoot routes](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span></span>

4. <span data-ttu-id="74f5d-153">Creare un cluster HDInsight e selezionare la rete virtuale di Azure hello durante la configurazione.</span><span class="sxs-lookup"><span data-stu-id="74f5d-153">Create an HDInsight cluster and select hello Azure Virtual Network during configuration.</span></span> <span data-ttu-id="74f5d-154">Usare i passaggi di hello in hello successivo processo di creazione di documenti toounderstand hello cluster:</span><span class="sxs-lookup"><span data-stu-id="74f5d-154">Use hello steps in hello following documents toounderstand hello cluster creation process:</span></span>

    * [<span data-ttu-id="74f5d-155">Creare utilizzando hello portale di Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="74f5d-155">Create HDInsight using hello Azure portal</span></span>](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [<span data-ttu-id="74f5d-156">Creare cluster HDInsight tramite Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="74f5d-156">Create HDInsight using Azure PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [<span data-ttu-id="74f5d-157">Creare cluster HDInsight tramite l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="74f5d-157">Create HDInsight using Azure CLI 1.0</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [<span data-ttu-id="74f5d-158">Creare cluster HDInsight tramite un modello Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="74f5d-158">Create HDInsight using an Azure Resource Manager template</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > <span data-ttu-id="74f5d-159">Aggiunta di HDInsight tooa di rete virtuale è un passaggio di configurazione facoltativa.</span><span class="sxs-lookup"><span data-stu-id="74f5d-159">Adding HDInsight tooa virtual network is an optional configuration step.</span></span> <span data-ttu-id="74f5d-160">Essere la rete virtuale che tooselect hello durante la configurazione cluster hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-160">Be sure tooselect hello virtual network when configuring hello cluster.</span></span>

## <span data-ttu-id="74f5d-161"><a id="multinet"></a>Connessione a più reti</span><span class="sxs-lookup"><span data-stu-id="74f5d-161"><a id="multinet"></a>Connecting multiple networks</span></span>

<span data-ttu-id="74f5d-162">sfida Hello con una configurazione di multi-rete è la risoluzione dei nomi tra reti hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-162">hello biggest challenge with a multi-network configuration is name resolution between hello networks.</span></span>

<span data-ttu-id="74f5d-163">Azure assicura la risoluzione dei nomi per i servizi di Azure che vengono installati in una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="74f5d-163">Azure provides name resolution for Azure services that are installed in a virtual network.</span></span> <span data-ttu-id="74f5d-164">La risoluzione dei nomi predefinito consente di HDInsight tooconnect toohello seguenti risorse utilizzando un nome di dominio completo (FQDN):</span><span class="sxs-lookup"><span data-stu-id="74f5d-164">This built-in name resolution allows HDInsight tooconnect toohello following resources by using a fully qualified domain name (FQDN):</span></span>

* <span data-ttu-id="74f5d-165">Qualsiasi risorsa che è disponibile in hello internet.</span><span class="sxs-lookup"><span data-stu-id="74f5d-165">Any resource that is available on hello internet.</span></span> <span data-ttu-id="74f5d-166">ad esempio microsoft.com, google.com.</span><span class="sxs-lookup"><span data-stu-id="74f5d-166">For example, microsoft.com, google.com.</span></span>

* <span data-ttu-id="74f5d-167">Qualsiasi risorsa che è in hello stessa rete virtuale di Azure tramite hello __nomi DNS interni__ della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-167">Any resource that is in hello same Azure Virtual Network, by using hello __internal DNS name__ of hello resource.</span></span> <span data-ttu-id="74f5d-168">Ad esempio, quando si utilizza la risoluzione dei nomi predefinito di hello, hello di seguito è esempio interno DNS nomi tooHDInsight assegnati i nodi di lavoro:</span><span class="sxs-lookup"><span data-stu-id="74f5d-168">For example, when using hello default name resolution, hello following are example internal DNS names assigned tooHDInsight worker nodes:</span></span>

    * <span data-ttu-id="74f5d-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="74f5d-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>
    * <span data-ttu-id="74f5d-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="74f5d-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>

    <span data-ttu-id="74f5d-171">Entrambi questi nodi possono comunicare direttamente tra loro e con altri nodi in HDInsight, usando i nomi DNS interni.</span><span class="sxs-lookup"><span data-stu-id="74f5d-171">Both these nodes can communicate directly with each other, and other nodes in HDInsight, by using internal DNS names.</span></span>

<span data-ttu-id="74f5d-172">risoluzione dei nomi predefinito Hello __non__ consentire HDInsight tooresolve nomi hello delle risorse nella rete virtuale toohello unita in join le reti.</span><span class="sxs-lookup"><span data-stu-id="74f5d-172">hello default name resolution does __not__ allow HDInsight tooresolve hello names of resources in networks that are joined toohello virtual network.</span></span> <span data-ttu-id="74f5d-173">Ad esempio, è comune toojoin toohello di rete virtuale di rete locale.</span><span class="sxs-lookup"><span data-stu-id="74f5d-173">For example, it is common toojoin your on-premises network toohello virtual network.</span></span> <span data-ttu-id="74f5d-174">Con solo hello risoluzione dei nomi predefiniti, HDInsight non è possibile accedere alle risorse nella rete locale hello in base al nome.</span><span class="sxs-lookup"><span data-stu-id="74f5d-174">With only hello default name resolution, HDInsight cannot access resources in hello on-premises network by name.</span></span> <span data-ttu-id="74f5d-175">Hello opposto è anche true, le risorse nella rete locale non è possibile accedere alle risorse nella rete virtuale hello in base al nome.</span><span class="sxs-lookup"><span data-stu-id="74f5d-175">hello opposite is also true, resources in your on-premises network cannot access resources in hello virtual network by name.</span></span>

> [!WARNING]
> <span data-ttu-id="74f5d-176">È necessario creare un server DNS personalizzato hello e configurare hello toouse di rete virtuale, prima di creare hello cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="74f5d-176">You must create hello custom DNS server and configure hello virtual network toouse it before creating hello HDInsight cluster.</span></span>

<span data-ttu-id="74f5d-177">risoluzione dei nomi tooenable tra la rete virtuale hello e risorse in reti unita in join, è necessario eseguire hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="74f5d-177">tooenable name resolution between hello virtual network and resources in joined networks, you must perform hello following actions:</span></span>

1. <span data-ttu-id="74f5d-178">Creare un server DNS personalizzato nella rete virtuale di Azure in cui si prevede di tooinstall HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-178">Create a custom DNS server in hello Azure Virtual Network where you plan tooinstall HDInsight.</span></span>

2. <span data-ttu-id="74f5d-179">Configurare hello rete virtuale toouse hello server DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="74f5d-179">Configure hello virtual network toouse hello custom DNS server.</span></span>

3. <span data-ttu-id="74f5d-180">Trovare hello che Azure viene assegnato il suffisso DNS per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="74f5d-180">Find hello Azure assigned DNS suffix for your virtual network.</span></span> <span data-ttu-id="74f5d-181">Questo valore è troppo simile`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="74f5d-181">This value is similar too`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span></span> <span data-ttu-id="74f5d-182">Per informazioni sulla ricerca suffisso DNS hello, vedere hello [esempio: DNS personalizzato](#example-dns) sezione.</span><span class="sxs-lookup"><span data-stu-id="74f5d-182">For information on finding hello DNS suffix, see hello [Example: Custom DNS](#example-dns) section.</span></span>

4. <span data-ttu-id="74f5d-183">Configurare l'inoltro tra i server DNS hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-183">Configure forwarding between hello DNS servers.</span></span> <span data-ttu-id="74f5d-184">configurazione di Hello dipende dal tipo di hello della rete remota.</span><span class="sxs-lookup"><span data-stu-id="74f5d-184">hello configuration depends on hello type of remote network.</span></span>

    * <span data-ttu-id="74f5d-185">Se la rete remota hello è una rete locale, configurare il DNS come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="74f5d-185">If hello remote network is an on-premises network, configure DNS as follows:</span></span>
        
        * <span data-ttu-id="74f5d-186">__DNS personalizzato__ (in rete virtuale hello):</span><span class="sxs-lookup"><span data-stu-id="74f5d-186">__Custom DNS__ (in hello virtual network):</span></span>

            * <span data-ttu-id="74f5d-187">Inoltrare le richieste per il suffisso DNS hello del sistema di risoluzione ricorsiva Azure di hello rete virtuale toohello (168.63.129.16).</span><span class="sxs-lookup"><span data-stu-id="74f5d-187">Forward requests for hello DNS suffix of hello virtual network toohello Azure recursive resolver (168.63.129.16).</span></span> <span data-ttu-id="74f5d-188">Azure gestisce le richieste di risorse nella rete virtuale hello</span><span class="sxs-lookup"><span data-stu-id="74f5d-188">Azure handles requests for resources in hello virtual network</span></span>

            * <span data-ttu-id="74f5d-189">Tutte le altre richieste toohello locale servizio DNS di inoltro.</span><span class="sxs-lookup"><span data-stu-id="74f5d-189">Forward all other requests toohello on-premises DNS server.</span></span> <span data-ttu-id="74f5d-190">Hello locale DNS gestisce tutte le altre richieste di risoluzione nome, anche le richieste per le risorse internet, ad esempio Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="74f5d-190">hello on-premises DNS handles all other name resolution requests, even requests for internet resources such as Microsoft.com.</span></span>

        * <span data-ttu-id="74f5d-191">__DNS locale__: inoltrare le richieste per hello rete virtuale DNS suffisso toohello server DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="74f5d-191">__On-premises DNS__: Forward requests for hello virtual network DNS suffix toohello custom DNS server.</span></span> <span data-ttu-id="74f5d-192">un server DNS personalizzato Hello inoltra quindi toohello ricorsiva Azure resolver.</span><span class="sxs-lookup"><span data-stu-id="74f5d-192">hello custom DNS server then forwards toohello Azure recursive resolver.</span></span>

        <span data-ttu-id="74f5d-193">Richieste di route questa configurazione per i nomi di dominio che contengono il suffisso DNS hello del server DNS personalizzato di hello rete virtuale toohello completo.</span><span class="sxs-lookup"><span data-stu-id="74f5d-193">This configuration routes requests for fully qualified domain names that contain hello DNS suffix of hello virtual network toohello custom DNS server.</span></span> <span data-ttu-id="74f5d-194">Tutte le altre richieste (anche per gli indirizzi internet pubblici) vengono gestiti dal server DNS locale di hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-194">All other requests (even for public internet addresses) are handled by hello on-premises DNS server.</span></span>

    * <span data-ttu-id="74f5d-195">Se la rete remota hello è un'altra rete virtuale di Azure, configurare il DNS come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="74f5d-195">If hello remote network is another Azure Virtual Network, configure DNS as follows:</span></span>

        * <span data-ttu-id="74f5d-196">__DNS personalizzato__ (in ogni rete virtuale):</span><span class="sxs-lookup"><span data-stu-id="74f5d-196">__Custom DNS__ (in each virtual network):</span></span>

            * <span data-ttu-id="74f5d-197">Le richieste per il suffisso DNS hello di reti virtuali hello vengono inoltrate toohello i server DNS personalizzati.</span><span class="sxs-lookup"><span data-stu-id="74f5d-197">Requests for hello DNS suffix of hello virtual networks are forwarded toohello custom DNS servers.</span></span> <span data-ttu-id="74f5d-198">Hello DNS in ogni rete virtuale è responsabile per la risoluzione delle risorse all'interno della rete.</span><span class="sxs-lookup"><span data-stu-id="74f5d-198">hello DNS in each virtual network is responsible for resolving resources within its network.</span></span>

            * <span data-ttu-id="74f5d-199">Inoltrare tutti gli altri resolver ricorsivo Azure toohello di richieste.</span><span class="sxs-lookup"><span data-stu-id="74f5d-199">Forward all other requests toohello Azure recursive resolver.</span></span> <span data-ttu-id="74f5d-200">resolver ricorsivo Hello è responsabile della risoluzione locale e alle risorse internet.</span><span class="sxs-lookup"><span data-stu-id="74f5d-200">hello recursive resolver is responsible for resolving local and internet resources.</span></span>

        <span data-ttu-id="74f5d-201">server DNS Hello per ogni rete inoltra le richieste toohello altri, basata sul suffisso DNS.</span><span class="sxs-lookup"><span data-stu-id="74f5d-201">hello DNS server for each network forwards requests toohello other, based on DNS suffix.</span></span> <span data-ttu-id="74f5d-202">Le altre richieste vengono risolti mediante resolver ricorsivo Azure hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-202">Other requests are resolved using hello Azure recursive resolver.</span></span>

    <span data-ttu-id="74f5d-203">Per un esempio di ogni configurazione, vedere hello [esempio: DNS personalizzato](#example-dns) sezione.</span><span class="sxs-lookup"><span data-stu-id="74f5d-203">For an example of each configuration, see hello [Example: Custom DNS](#example-dns) section.</span></span>

<span data-ttu-id="74f5d-204">Per ulteriori informazioni, vedere hello [risoluzione dei nomi per le macchine virtuali e istanze del ruolo](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) documento.</span><span class="sxs-lookup"><span data-stu-id="74f5d-204">For more information, see hello [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span></span>

## <a name="directly-connect-toohadoop-services"></a><span data-ttu-id="74f5d-205">Connettersi direttamente servizi tooHadoop</span><span class="sxs-lookup"><span data-stu-id="74f5d-205">Directly connect tooHadoop services</span></span>

<span data-ttu-id="74f5d-206">La maggior parte delle documentazione su HDInsight si presuppone la presenza di cluster di accesso toohello su hello internet.</span><span class="sxs-lookup"><span data-stu-id="74f5d-206">Most documentation on HDInsight assumes that you have access toohello cluster over hello internet.</span></span> <span data-ttu-id="74f5d-207">Ad esempio, che è possibile connettersi cluster toohello https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="74f5d-207">For example, that you can connect toohello cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="74f5d-208">Questo indirizzo Usa gateway hello pubblico, non è disponibile se è stato utilizzato NSGs o UDRs toorestrict accesso da hello internet.</span><span class="sxs-lookup"><span data-stu-id="74f5d-208">This address uses hello public gateway, which is not available if you have used NSGs or UDRs toorestrict access from hello internet.</span></span>

<span data-ttu-id="74f5d-209">tooconnect tooAmbari e le altre pagine web attraverso la rete virtuale di hello, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="74f5d-209">tooconnect tooAmbari and other web pages through hello virtual network, use hello following steps:</span></span>

1. <span data-ttu-id="74f5d-210">toodiscover nomi di dominio completo interno hello (FQDN) dei nodi del cluster HDInsight hello, utilizzare uno dei seguenti metodi hello:</span><span class="sxs-lookup"><span data-stu-id="74f5d-210">toodiscover hello internal fully qualified domain names (FQDN) of hello HDInsight cluster nodes, use one of hello following methods:</span></span>

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

    <span data-ttu-id="74f5d-211">Nell'elenco di nodi restituiti hello trovare hello FQDN per hello nodi head e utilizzare hello FQDN tooconnect tooAmbari e altri servizi web.</span><span class="sxs-lookup"><span data-stu-id="74f5d-211">In hello list of nodes returned, find hello FQDN for hello head nodes and use hello FQDNs tooconnect tooAmbari and other web services.</span></span> <span data-ttu-id="74f5d-212">Ad esempio, utilizzare `http://<headnode-fqdn>:8080` tooaccess Ambari.</span><span class="sxs-lookup"><span data-stu-id="74f5d-212">For example, use `http://<headnode-fqdn>:8080` tooaccess Ambari.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="74f5d-213">Alcuni servizi ospitate nei nodi head hello attivi solo in un nodo alla volta.</span><span class="sxs-lookup"><span data-stu-id="74f5d-213">Some services hosted on hello head nodes are only active on one node at a time.</span></span> <span data-ttu-id="74f5d-214">Se si tenta di accedere al servizio in un nodo head e viene restituito un errore 404, passare toohello altro nodo head.</span><span class="sxs-lookup"><span data-stu-id="74f5d-214">If you try accessing a service on one head node and it returns a 404 error, switch toohello other head node.</span></span>

2. <span data-ttu-id="74f5d-215">nodo hello toodetermine e la porta di un servizio è disponibile, vedere hello [porte utilizzate da servizi di Hadoop in HDInsight](./hdinsight-hadoop-port-settings-for-services.md) documento.</span><span class="sxs-lookup"><span data-stu-id="74f5d-215">toodetermine hello node and port that a service is available on, see hello [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

## <span data-ttu-id="74f5d-216"><a id="networktraffic"></a> Controllo del traffico di rete</span><span class="sxs-lookup"><span data-stu-id="74f5d-216"><a id="networktraffic"></a> Controlling network traffic</span></span>

<span data-ttu-id="74f5d-217">Traffico di rete in un reti virtuali di Azure può essere controllato utilizzando hello dei seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="74f5d-217">Network traffic in an Azure Virtual Networks can be controlled using hello following methods:</span></span>

* <span data-ttu-id="74f5d-218">**Gruppi di sicurezza di rete** (gruppo) consentono di rete di toohello toofilter traffico in entrata e in uscita.</span><span class="sxs-lookup"><span data-stu-id="74f5d-218">**Network security groups** (NSG) allow you toofilter inbound and outbound traffic toohello network.</span></span> <span data-ttu-id="74f5d-219">Per ulteriori informazioni, vedere hello [filtrare il traffico di rete con gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md) documento.</span><span class="sxs-lookup"><span data-stu-id="74f5d-219">For more information, see hello [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    > [!WARNING]
    > <span data-ttu-id="74f5d-220">HDInsight non supporta la limitazione del traffico in uscita.</span><span class="sxs-lookup"><span data-stu-id="74f5d-220">HDInsight does not support restricting outbound traffic.</span></span>

* <span data-ttu-id="74f5d-221">**Le route definite dall'utente** (UDR) definiscono il flusso di traffico tra le risorse nella rete hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-221">**User-defined routes** (UDR) define how traffic flows between resources in hello network.</span></span> <span data-ttu-id="74f5d-222">Per ulteriori informazioni, vedere hello [le route definite dall'utente e l'inoltro IP](../virtual-network/virtual-networks-udr-overview.md) documento.</span><span class="sxs-lookup"><span data-stu-id="74f5d-222">For more information, see hello [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md) document.</span></span>

* <span data-ttu-id="74f5d-223">**Dispositivi di rete virtuale** replicare hello le funzionalità dei dispositivi, ad esempio router e firewall.</span><span class="sxs-lookup"><span data-stu-id="74f5d-223">**Network virtual appliances** replicate hello functionality of devices such as firewalls and routers.</span></span> <span data-ttu-id="74f5d-224">Per ulteriori informazioni, vedere hello [ai dispositivi di rete](https://azure.microsoft.com/solutions/network-appliances) documento.</span><span class="sxs-lookup"><span data-stu-id="74f5d-224">For more information, see hello [Network Appliances](https://azure.microsoft.com/solutions/network-appliances) document.</span></span>

<span data-ttu-id="74f5d-225">Come servizio gestito, HDInsight richiede l'accesso illimitato tooAzure integrità e la gestione servizi in cloud di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-225">As a managed service, HDInsight requires unrestricted access tooAzure health and management services in hello Azure cloud.</span></span> <span data-ttu-id="74f5d-226">Quando si usano i gruppi di sicurezza di rete e le route definite dall'utente, è necessario assicurarsi che questi servizi possano ancora comunicare con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="74f5d-226">When using NSGs and UDRs, you must ensure that HDInsight these services can still communicate with HDInsight.</span></span>

<span data-ttu-id="74f5d-227">HDInsight espone i servizi su porte diverse.</span><span class="sxs-lookup"><span data-stu-id="74f5d-227">HDInsight exposes services on several ports.</span></span> <span data-ttu-id="74f5d-228">Quando si utilizza un firewall appliance virtuale, è necessario consentire il traffico su hello porte usate per questi servizi.</span><span class="sxs-lookup"><span data-stu-id="74f5d-228">When using a virtual appliance firewall, you must allow traffic on hello ports used for these services.</span></span> <span data-ttu-id="74f5d-229">Per ulteriori informazioni, vedere la sezione hello [porte necessarie].</span><span class="sxs-lookup"><span data-stu-id="74f5d-229">For more information, see hello [Required ports] section.</span></span>

### <span data-ttu-id="74f5d-230"><a id="hdinsight-ip"></a>HDInsight con gruppi di sicurezza di rete e route definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="74f5d-230"><a id="hdinsight-ip"></a> HDInsight with network security groups and user-defined routes</span></span>

<span data-ttu-id="74f5d-231">Se si intende usare **gruppi di sicurezza di rete** o **le route definite dall'utente** toocontrol il traffico di rete, eseguire hello seguenti azioni prima di installare HDInsight:</span><span class="sxs-lookup"><span data-stu-id="74f5d-231">If you plan on using **network security groups** or **user-defined routes** toocontrol network traffic, perform hello following actions before installing HDInsight:</span></span>

1. <span data-ttu-id="74f5d-232">Identificare hello regione di Azure che si prevede di toouse per HDInsight.</span><span class="sxs-lookup"><span data-stu-id="74f5d-232">Identify hello Azure region that you plan toouse for HDInsight.</span></span>

2. <span data-ttu-id="74f5d-233">Identificare gli indirizzi IP hello necessari da HDInsight.</span><span class="sxs-lookup"><span data-stu-id="74f5d-233">Identify hello IP addresses required by HDInsight.</span></span> <span data-ttu-id="74f5d-234">Per ulteriori informazioni, vedere hello [indirizzi IP richiesti da HDInsight](#hdinsight-ip) sezione.</span><span class="sxs-lookup"><span data-stu-id="74f5d-234">For more information, see hello [IP Addresses required by HDInsight](#hdinsight-ip) section.</span></span>

3. <span data-ttu-id="74f5d-235">Creare o modificare gruppi di sicurezza di rete hello o le route definite dall'utente per la subnet hello pianificare tooinstall HDInsight in.</span><span class="sxs-lookup"><span data-stu-id="74f5d-235">Create or modify hello network security groups or user-defined routes for hello subnet that you plan tooinstall HDInsight into.</span></span>

    * <span data-ttu-id="74f5d-236">__Gruppi di sicurezza di rete__: Consenti __in ingresso__ il traffico sulla porta __443__ da indirizzi IP hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-236">__Network security groups__: allow __inbound__ traffic on port __443__ from hello IP addresses.</span></span>
    * <span data-ttu-id="74f5d-237">__Le route definite dall'utente__: creare un indirizzo IP tooeach di route e impostare hello __tipo dell'hop successivo__ too__Internet__.</span><span class="sxs-lookup"><span data-stu-id="74f5d-237">__User-defined routes__: create a route tooeach IP address and set hello __Next hop type__ too__Internet__.</span></span>

<span data-ttu-id="74f5d-238">Per ulteriori informazioni su gruppi di sicurezza di rete o le route definite dall'utente, vedere hello seguente documentazione:</span><span class="sxs-lookup"><span data-stu-id="74f5d-238">For more information on network security groups or user-defined routes, see hello following documentation:</span></span>

* [<span data-ttu-id="74f5d-239">Gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="74f5d-239">Network security group</span></span>](../virtual-network/virtual-networks-nsg.md)

* [<span data-ttu-id="74f5d-240">Route definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="74f5d-240">User-defined routes</span></span>](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a><span data-ttu-id="74f5d-241">Tunneling forzato</span><span class="sxs-lookup"><span data-stu-id="74f5d-241">Forced tunneling</span></span>

<span data-ttu-id="74f5d-242">Il tunneling forzato è una configurazione di routing definite dall'utente in cui tutto il traffico da una subnet è forzato tooa specifici di rete o posizione, ad esempio la rete locale.</span><span class="sxs-lookup"><span data-stu-id="74f5d-242">Forced tunneling is a user-defined routing configuration where all traffic from a subnet is forced tooa specific network or location, such as your on-premises network.</span></span> <span data-ttu-id="74f5d-243">HDInsight __non__ supporta il tunneling forzato.</span><span class="sxs-lookup"><span data-stu-id="74f5d-243">HDInsight does __not__ support forced tunneling.</span></span>

## <span data-ttu-id="74f5d-244"><a id="hdinsight-ip"></a> Indirizzi IP richiesti</span><span class="sxs-lookup"><span data-stu-id="74f5d-244"><a id="hdinsight-ip"></a> Required IP addresses</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74f5d-245">Hello Azure integrità e servizi di gestione devono essere in grado di toocommunicate con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="74f5d-245">hello Azure health and management services must be able toocommunicate with HDInsight.</span></span> <span data-ttu-id="74f5d-246">Se si utilizzano gruppi di sicurezza di rete o le route definite dall'utente, consentire il traffico dal hello gli indirizzi IP per questi tooreach servizi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="74f5d-246">If you use network security groups or user-defined routes, allow traffic from hello IP addresses for these services tooreach HDInsight.</span></span>
>
> <span data-ttu-id="74f5d-247">Se non si utilizza gruppi di sicurezza di rete o il traffico toocontrol le route definite dall'utente, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="74f5d-247">If you do not use network security groups or user-defined routes toocontrol traffic, you can ignore this section.</span></span>

<span data-ttu-id="74f5d-248">Se si utilizzano gruppi di sicurezza di rete o le route definite dall'utente, è necessario consentire il traffico proveniente da hello Azure health e Gestione servizi tooreach HDInsight.</span><span class="sxs-lookup"><span data-stu-id="74f5d-248">If you use network security groups or user-defined routes, you must allow traffic from hello Azure health and management services tooreach HDInsight.</span></span> <span data-ttu-id="74f5d-249">Utilizzare hello seguendo i passaggi toofind hello indirizzi IP devono essere consentiti:</span><span class="sxs-lookup"><span data-stu-id="74f5d-249">Use hello following steps toofind hello IP addresses that must be allowed:</span></span>

1. <span data-ttu-id="74f5d-250">È sempre necessario consentire il traffico proveniente da hello seguenti indirizzi IP:</span><span class="sxs-lookup"><span data-stu-id="74f5d-250">You must always allow traffic from hello following IP addresses:</span></span>

    | <span data-ttu-id="74f5d-251">Indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="74f5d-251">IP address</span></span> | <span data-ttu-id="74f5d-252">Porta consentita</span><span class="sxs-lookup"><span data-stu-id="74f5d-252">Allowed port</span></span> | <span data-ttu-id="74f5d-253">Direzione</span><span class="sxs-lookup"><span data-stu-id="74f5d-253">Direction</span></span> |
    | ---- | ----- | ----- |
    | <span data-ttu-id="74f5d-254">168.61.49.99</span><span class="sxs-lookup"><span data-stu-id="74f5d-254">168.61.49.99</span></span> | <span data-ttu-id="74f5d-255">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-255">443</span></span> | <span data-ttu-id="74f5d-256">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-256">Inbound</span></span> |
    | <span data-ttu-id="74f5d-257">23.99.5.239</span><span class="sxs-lookup"><span data-stu-id="74f5d-257">23.99.5.239</span></span> | <span data-ttu-id="74f5d-258">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-258">443</span></span> | <span data-ttu-id="74f5d-259">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-259">Inbound</span></span> |
    | <span data-ttu-id="74f5d-260">168.61.48.131</span><span class="sxs-lookup"><span data-stu-id="74f5d-260">168.61.48.131</span></span> | <span data-ttu-id="74f5d-261">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-261">443</span></span> | <span data-ttu-id="74f5d-262">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-262">Inbound</span></span> |
    | <span data-ttu-id="74f5d-263">138.91.141.162</span><span class="sxs-lookup"><span data-stu-id="74f5d-263">138.91.141.162</span></span> | <span data-ttu-id="74f5d-264">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-264">443</span></span> | <span data-ttu-id="74f5d-265">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-265">Inbound</span></span> |

2. <span data-ttu-id="74f5d-266">Se il cluster HDInsight è in uno dei seguenti aree hello, è necessario consentire il traffico proveniente da indirizzi IP di hello elencati per area hello:</span><span class="sxs-lookup"><span data-stu-id="74f5d-266">If your HDInsight cluster is in one of hello following regions, then you must allow traffic from hello IP addresses listed for hello region:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="74f5d-267">Se non è elencato hello regione di Azure in uso, quindi utilizzare solo quattro indirizzi IP hello dal passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="74f5d-267">If hello Azure region you are using is not listed, then only use hello four IP addresses from step 1.</span></span>

    | <span data-ttu-id="74f5d-268">Paese</span><span class="sxs-lookup"><span data-stu-id="74f5d-268">Country</span></span> | <span data-ttu-id="74f5d-269">Region</span><span class="sxs-lookup"><span data-stu-id="74f5d-269">Region</span></span> | <span data-ttu-id="74f5d-270">Indirizzi IP consentiti</span><span class="sxs-lookup"><span data-stu-id="74f5d-270">Allowed IP addresses</span></span> | <span data-ttu-id="74f5d-271">Porta consentita</span><span class="sxs-lookup"><span data-stu-id="74f5d-271">Allowed port</span></span> | <span data-ttu-id="74f5d-272">Direzione</span><span class="sxs-lookup"><span data-stu-id="74f5d-272">Direction</span></span> |
    | ---- | ---- | ---- | ---- | ----- |
    | <span data-ttu-id="74f5d-273">Asia</span><span class="sxs-lookup"><span data-stu-id="74f5d-273">Asia</span></span> | <span data-ttu-id="74f5d-274">Asia orientale</span><span class="sxs-lookup"><span data-stu-id="74f5d-274">East Asia</span></span> | <span data-ttu-id="74f5d-275">23.102.235.122</span><span class="sxs-lookup"><span data-stu-id="74f5d-275">23.102.235.122</span></span></br><span data-ttu-id="74f5d-276">52.175.38.134</span><span class="sxs-lookup"><span data-stu-id="74f5d-276">52.175.38.134</span></span> | <span data-ttu-id="74f5d-277">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-277">443</span></span> | <span data-ttu-id="74f5d-278">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-278">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="74f5d-279">Asia sudorientale</span><span class="sxs-lookup"><span data-stu-id="74f5d-279">Southeast Asia</span></span> | <span data-ttu-id="74f5d-280">13.76.245.160</span><span class="sxs-lookup"><span data-stu-id="74f5d-280">13.76.245.160</span></span></br><span data-ttu-id="74f5d-281">13.76.136.249</span><span class="sxs-lookup"><span data-stu-id="74f5d-281">13.76.136.249</span></span> | <span data-ttu-id="74f5d-282">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-282">443</span></span> | <span data-ttu-id="74f5d-283">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-283">Inbound</span></span> |
    | <span data-ttu-id="74f5d-284">Australia</span><span class="sxs-lookup"><span data-stu-id="74f5d-284">Australia</span></span> | <span data-ttu-id="74f5d-285">Australia orientale</span><span class="sxs-lookup"><span data-stu-id="74f5d-285">Australia East</span></span> | <span data-ttu-id="74f5d-286">104.210.84.115</span><span class="sxs-lookup"><span data-stu-id="74f5d-286">104.210.84.115</span></span></br><span data-ttu-id="74f5d-287">13.75.152.195</span><span class="sxs-lookup"><span data-stu-id="74f5d-287">13.75.152.195</span></span> | <span data-ttu-id="74f5d-288">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-288">443</span></span> | <span data-ttu-id="74f5d-289">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-289">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="74f5d-290">Australia sudorientale</span><span class="sxs-lookup"><span data-stu-id="74f5d-290">Australia Southeast</span></span> | <span data-ttu-id="74f5d-291">13.77.2.56</span><span class="sxs-lookup"><span data-stu-id="74f5d-291">13.77.2.56</span></span></br><span data-ttu-id="74f5d-292">13.77.2.94</span><span class="sxs-lookup"><span data-stu-id="74f5d-292">13.77.2.94</span></span> | <span data-ttu-id="74f5d-293">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-293">443</span></span> | <span data-ttu-id="74f5d-294">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-294">Inbound</span></span> |
    | <span data-ttu-id="74f5d-295">Brasile</span><span class="sxs-lookup"><span data-stu-id="74f5d-295">Brazil</span></span> | <span data-ttu-id="74f5d-296">Brasile meridionale</span><span class="sxs-lookup"><span data-stu-id="74f5d-296">Brazil South</span></span> | <span data-ttu-id="74f5d-297">191.235.84.104</span><span class="sxs-lookup"><span data-stu-id="74f5d-297">191.235.84.104</span></span></br><span data-ttu-id="74f5d-298">191.235.87.113</span><span class="sxs-lookup"><span data-stu-id="74f5d-298">191.235.87.113</span></span> | <span data-ttu-id="74f5d-299">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-299">443</span></span> | <span data-ttu-id="74f5d-300">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-300">Inbound</span></span> |
    | <span data-ttu-id="74f5d-301">Canada</span><span class="sxs-lookup"><span data-stu-id="74f5d-301">Canada</span></span> | <span data-ttu-id="74f5d-302">Canada orientale</span><span class="sxs-lookup"><span data-stu-id="74f5d-302">Canada East</span></span> | <span data-ttu-id="74f5d-303">52.229.127.96</span><span class="sxs-lookup"><span data-stu-id="74f5d-303">52.229.127.96</span></span></br><span data-ttu-id="74f5d-304">52.229.123.172</span><span class="sxs-lookup"><span data-stu-id="74f5d-304">52.229.123.172</span></span> | <span data-ttu-id="74f5d-305">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-305">443</span></span> | <span data-ttu-id="74f5d-306">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-306">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="74f5d-307">Canada centrale</span><span class="sxs-lookup"><span data-stu-id="74f5d-307">Canada Central</span></span> | <span data-ttu-id="74f5d-308">52.228.37.66</span><span class="sxs-lookup"><span data-stu-id="74f5d-308">52.228.37.66</span></span></br><span data-ttu-id="74f5d-309">52.228.45.222</span><span class="sxs-lookup"><span data-stu-id="74f5d-309">52.228.45.222</span></span> | <span data-ttu-id="74f5d-310">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-310">443</span></span> | <span data-ttu-id="74f5d-311">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-311">Inbound</span></span> |
    | <span data-ttu-id="74f5d-312">Cina</span><span class="sxs-lookup"><span data-stu-id="74f5d-312">China</span></span> | <span data-ttu-id="74f5d-313">Cina settentrionale</span><span class="sxs-lookup"><span data-stu-id="74f5d-313">China North</span></span> | <span data-ttu-id="74f5d-314">42.159.96.170</span><span class="sxs-lookup"><span data-stu-id="74f5d-314">42.159.96.170</span></span></br><span data-ttu-id="74f5d-315">139.217.2.219</span><span class="sxs-lookup"><span data-stu-id="74f5d-315">139.217.2.219</span></span> | <span data-ttu-id="74f5d-316">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-316">443</span></span> | <span data-ttu-id="74f5d-317">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-317">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="74f5d-318">Cina orientale</span><span class="sxs-lookup"><span data-stu-id="74f5d-318">China East</span></span> | <span data-ttu-id="74f5d-319">42.159.198.178</span><span class="sxs-lookup"><span data-stu-id="74f5d-319">42.159.198.178</span></span></br><span data-ttu-id="74f5d-320">42.159.234.157</span><span class="sxs-lookup"><span data-stu-id="74f5d-320">42.159.234.157</span></span> | <span data-ttu-id="74f5d-321">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-321">443</span></span> | <span data-ttu-id="74f5d-322">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-322">Inbound</span></span> |
    | <span data-ttu-id="74f5d-323">Europa</span><span class="sxs-lookup"><span data-stu-id="74f5d-323">Europe</span></span> | <span data-ttu-id="74f5d-324">Europa settentrionale</span><span class="sxs-lookup"><span data-stu-id="74f5d-324">North Europe</span></span> | <span data-ttu-id="74f5d-325">52.164.210.96</span><span class="sxs-lookup"><span data-stu-id="74f5d-325">52.164.210.96</span></span></br><span data-ttu-id="74f5d-326">13.74.153.132</span><span class="sxs-lookup"><span data-stu-id="74f5d-326">13.74.153.132</span></span> | <span data-ttu-id="74f5d-327">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-327">443</span></span> | <span data-ttu-id="74f5d-328">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-328">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="74f5d-329">Europa occidentale</span><span class="sxs-lookup"><span data-stu-id="74f5d-329">West Europe</span></span>| <span data-ttu-id="74f5d-330">52.166.243.90</span><span class="sxs-lookup"><span data-stu-id="74f5d-330">52.166.243.90</span></span></br><span data-ttu-id="74f5d-331">52.174.36.244</span><span class="sxs-lookup"><span data-stu-id="74f5d-331">52.174.36.244</span></span> | <span data-ttu-id="74f5d-332">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-332">443</span></span> | <span data-ttu-id="74f5d-333">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-333">Inbound</span></span> |
    | <span data-ttu-id="74f5d-334">Germania</span><span class="sxs-lookup"><span data-stu-id="74f5d-334">Germany</span></span> | <span data-ttu-id="74f5d-335">Germania centrale</span><span class="sxs-lookup"><span data-stu-id="74f5d-335">Germany Central</span></span> | <span data-ttu-id="74f5d-336">51.4.146.68</span><span class="sxs-lookup"><span data-stu-id="74f5d-336">51.4.146.68</span></span></br><span data-ttu-id="74f5d-337">51.4.146.80</span><span class="sxs-lookup"><span data-stu-id="74f5d-337">51.4.146.80</span></span> | <span data-ttu-id="74f5d-338">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-338">443</span></span> | <span data-ttu-id="74f5d-339">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-339">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="74f5d-340">Germania nord-orientale</span><span class="sxs-lookup"><span data-stu-id="74f5d-340">Germany Northeast</span></span> | <span data-ttu-id="74f5d-341">51.5.150.132</span><span class="sxs-lookup"><span data-stu-id="74f5d-341">51.5.150.132</span></span></br><span data-ttu-id="74f5d-342">51.5.144.101</span><span class="sxs-lookup"><span data-stu-id="74f5d-342">51.5.144.101</span></span> | <span data-ttu-id="74f5d-343">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-343">443</span></span> | <span data-ttu-id="74f5d-344">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-344">Inbound</span></span> |
    | <span data-ttu-id="74f5d-345">India</span><span class="sxs-lookup"><span data-stu-id="74f5d-345">India</span></span> | <span data-ttu-id="74f5d-346">India centrale</span><span class="sxs-lookup"><span data-stu-id="74f5d-346">Central India</span></span> | <span data-ttu-id="74f5d-347">52.172.153.209</span><span class="sxs-lookup"><span data-stu-id="74f5d-347">52.172.153.209</span></span></br><span data-ttu-id="74f5d-348">52.172.152.49</span><span class="sxs-lookup"><span data-stu-id="74f5d-348">52.172.152.49</span></span> | <span data-ttu-id="74f5d-349">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-349">443</span></span> | <span data-ttu-id="74f5d-350">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-350">Inbound</span></span> |
    | <span data-ttu-id="74f5d-351">Giappone</span><span class="sxs-lookup"><span data-stu-id="74f5d-351">Japan</span></span> | <span data-ttu-id="74f5d-352">Giappone orientale</span><span class="sxs-lookup"><span data-stu-id="74f5d-352">Japan East</span></span> | <span data-ttu-id="74f5d-353">13.78.125.90</span><span class="sxs-lookup"><span data-stu-id="74f5d-353">13.78.125.90</span></span></br><span data-ttu-id="74f5d-354">13.78.89.60</span><span class="sxs-lookup"><span data-stu-id="74f5d-354">13.78.89.60</span></span> | <span data-ttu-id="74f5d-355">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-355">443</span></span> | <span data-ttu-id="74f5d-356">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-356">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="74f5d-357">Giappone occidentale</span><span class="sxs-lookup"><span data-stu-id="74f5d-357">Japan West</span></span> | <span data-ttu-id="74f5d-358">40.74.125.69</span><span class="sxs-lookup"><span data-stu-id="74f5d-358">40.74.125.69</span></span></br><span data-ttu-id="74f5d-359">138.91.29.150</span><span class="sxs-lookup"><span data-stu-id="74f5d-359">138.91.29.150</span></span> | <span data-ttu-id="74f5d-360">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-360">443</span></span> | <span data-ttu-id="74f5d-361">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-361">Inbound</span></span> |
    | <span data-ttu-id="74f5d-362">Corea</span><span class="sxs-lookup"><span data-stu-id="74f5d-362">Korea</span></span> | <span data-ttu-id="74f5d-363">Corea centrale</span><span class="sxs-lookup"><span data-stu-id="74f5d-363">Korea Central</span></span> | <span data-ttu-id="74f5d-364">52.231.39.142</span><span class="sxs-lookup"><span data-stu-id="74f5d-364">52.231.39.142</span></span></br><span data-ttu-id="74f5d-365">52.231.36.209</span><span class="sxs-lookup"><span data-stu-id="74f5d-365">52.231.36.209</span></span> | <span data-ttu-id="74f5d-366">433</span><span class="sxs-lookup"><span data-stu-id="74f5d-366">433</span></span> | <span data-ttu-id="74f5d-367">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-367">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="74f5d-368">Corea meridionale</span><span class="sxs-lookup"><span data-stu-id="74f5d-368">Korea South</span></span> | <span data-ttu-id="74f5d-369">52.231.203.16</span><span class="sxs-lookup"><span data-stu-id="74f5d-369">52.231.203.16</span></span></br><span data-ttu-id="74f5d-370">52.231.205.214</span><span class="sxs-lookup"><span data-stu-id="74f5d-370">52.231.205.214</span></span> | <span data-ttu-id="74f5d-371">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-371">443</span></span> | <span data-ttu-id="74f5d-372">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-372">Inbound</span></span>
    | <span data-ttu-id="74f5d-373">Regno Unito</span><span class="sxs-lookup"><span data-stu-id="74f5d-373">United Kingdom</span></span> | <span data-ttu-id="74f5d-374">Regno Unito occidentale</span><span class="sxs-lookup"><span data-stu-id="74f5d-374">UK West</span></span> | <span data-ttu-id="74f5d-375">51.141.13.110</span><span class="sxs-lookup"><span data-stu-id="74f5d-375">51.141.13.110</span></span></br><span data-ttu-id="74f5d-376">51.141.7.20</span><span class="sxs-lookup"><span data-stu-id="74f5d-376">51.141.7.20</span></span> | <span data-ttu-id="74f5d-377">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-377">443</span></span> | <span data-ttu-id="74f5d-378">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-378">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="74f5d-379">Regno Unito meridionale</span><span class="sxs-lookup"><span data-stu-id="74f5d-379">UK South</span></span> | <span data-ttu-id="74f5d-380">51.140.47.39</span><span class="sxs-lookup"><span data-stu-id="74f5d-380">51.140.47.39</span></span></br><span data-ttu-id="74f5d-381">51.140.52.16</span><span class="sxs-lookup"><span data-stu-id="74f5d-381">51.140.52.16</span></span> | <span data-ttu-id="74f5d-382">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-382">443</span></span> | <span data-ttu-id="74f5d-383">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-383">Inbound</span></span> |
    | <span data-ttu-id="74f5d-384">Stati Uniti</span><span class="sxs-lookup"><span data-stu-id="74f5d-384">United States</span></span> | <span data-ttu-id="74f5d-385">Stati Uniti centrali</span><span class="sxs-lookup"><span data-stu-id="74f5d-385">Central US</span></span> | <span data-ttu-id="74f5d-386">13.67.223.215</span><span class="sxs-lookup"><span data-stu-id="74f5d-386">13.67.223.215</span></span></br><span data-ttu-id="74f5d-387">40.86.83.253</span><span class="sxs-lookup"><span data-stu-id="74f5d-387">40.86.83.253</span></span> | <span data-ttu-id="74f5d-388">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-388">443</span></span> | <span data-ttu-id="74f5d-389">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-389">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="74f5d-390">Stati Uniti centro-settentrionali</span><span class="sxs-lookup"><span data-stu-id="74f5d-390">North Central US</span></span> | <span data-ttu-id="74f5d-391">157.56.8.38</span><span class="sxs-lookup"><span data-stu-id="74f5d-391">157.56.8.38</span></span></br><span data-ttu-id="74f5d-392">157.55.213.99</span><span class="sxs-lookup"><span data-stu-id="74f5d-392">157.55.213.99</span></span> | <span data-ttu-id="74f5d-393">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-393">443</span></span> | <span data-ttu-id="74f5d-394">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-394">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="74f5d-395">Stati Uniti centro-occidentali</span><span class="sxs-lookup"><span data-stu-id="74f5d-395">West Central US</span></span> | <span data-ttu-id="74f5d-396">52.161.23.15</span><span class="sxs-lookup"><span data-stu-id="74f5d-396">52.161.23.15</span></span></br><span data-ttu-id="74f5d-397">52.161.10.167</span><span class="sxs-lookup"><span data-stu-id="74f5d-397">52.161.10.167</span></span> | <span data-ttu-id="74f5d-398">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-398">443</span></span> | <span data-ttu-id="74f5d-399">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-399">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="74f5d-400">Stati Uniti occidentali 2</span><span class="sxs-lookup"><span data-stu-id="74f5d-400">West US 2</span></span> | <span data-ttu-id="74f5d-401">52.175.211.210</span><span class="sxs-lookup"><span data-stu-id="74f5d-401">52.175.211.210</span></span></br><span data-ttu-id="74f5d-402">52.175.222.222</span><span class="sxs-lookup"><span data-stu-id="74f5d-402">52.175.222.222</span></span> | <span data-ttu-id="74f5d-403">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-403">443</span></span> | <span data-ttu-id="74f5d-404">In ingresso</span><span class="sxs-lookup"><span data-stu-id="74f5d-404">Inbound</span></span> |

    <span data-ttu-id="74f5d-405">Per informazioni su IP hello indirizzi toouse per Azure per enti pubblici, vedere hello [Azure per enti pubblici Intelligence + Analitica](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) documento.</span><span class="sxs-lookup"><span data-stu-id="74f5d-405">For information on hello IP addresses toouse for Azure Government, see hello [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span></span>

3. <span data-ttu-id="74f5d-406">Se si usa un server DNS personalizzato con la rete virtuale, è anche necessario consentire l'accesso da __168.63.129.16__.</span><span class="sxs-lookup"><span data-stu-id="74f5d-406">If you use a custom DNS server with your virtual network, you must also allow access from __168.63.129.16__.</span></span> <span data-ttu-id="74f5d-407">Questo è l'indirizzo del sistema di risoluzione ricorsiva di Azure.</span><span class="sxs-lookup"><span data-stu-id="74f5d-407">This address is Azure's recursive resolver.</span></span> <span data-ttu-id="74f5d-408">Per ulteriori informazioni, vedere hello [la risoluzione dei nomi per le macchine virtuali e il ruolo istanze](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) documento.</span><span class="sxs-lookup"><span data-stu-id="74f5d-408">For more information, see hello [Name resolution for VMs and Role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span></span>

<span data-ttu-id="74f5d-409">Per ulteriori informazioni, vedere hello [controllare il traffico di rete](#networktraffic) sezione.</span><span class="sxs-lookup"><span data-stu-id="74f5d-409">For more information, see hello [Controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="74f5d-410"><a id="hdinsight-ports"></a> Porte richieste</span><span class="sxs-lookup"><span data-stu-id="74f5d-410"><a id="hdinsight-ports"></a> Required ports</span></span>

<span data-ttu-id="74f5d-411">Se si intende usare una rete **firewall appliance virtuale** toosecure la rete virtuale hello, è necessario consentire il traffico in uscita hello seguenti porte:</span><span class="sxs-lookup"><span data-stu-id="74f5d-411">If you plan on using a network **virtual appliance firewall** toosecure hello virtual network, you must allow outbound traffic on hello following ports:</span></span>

* <span data-ttu-id="74f5d-412">53</span><span class="sxs-lookup"><span data-stu-id="74f5d-412">53</span></span>
* <span data-ttu-id="74f5d-413">443</span><span class="sxs-lookup"><span data-stu-id="74f5d-413">443</span></span>
* <span data-ttu-id="74f5d-414">1433</span><span class="sxs-lookup"><span data-stu-id="74f5d-414">1433</span></span>
* <span data-ttu-id="74f5d-415">11000-11999</span><span class="sxs-lookup"><span data-stu-id="74f5d-415">11000-11999</span></span>
* <span data-ttu-id="74f5d-416">14000-14999</span><span class="sxs-lookup"><span data-stu-id="74f5d-416">14000-14999</span></span>

<span data-ttu-id="74f5d-417">Per un elenco di porte per servizi specifici, vedere hello [porte utilizzate da servizi di Hadoop in HDInsight](hdinsight-hadoop-port-settings-for-services.md) documento.</span><span class="sxs-lookup"><span data-stu-id="74f5d-417">For a list of ports for specific services, see hello [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

<span data-ttu-id="74f5d-418">Per ulteriori informazioni sulle regole firewall per i dispositivi virtuali, vedere hello [scenario appliance virtuale](../virtual-network/virtual-network-scenario-udr-gw-nva.md) documento.</span><span class="sxs-lookup"><span data-stu-id="74f5d-418">For more information on firewall rules for virtual appliances, see hello [virtual appliance scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span></span>

## <span data-ttu-id="74f5d-419"><a id="hdinsight-nsg"></a>Ad esempio: gruppi di sicurezza di rete con HDInsight</span><span class="sxs-lookup"><span data-stu-id="74f5d-419"><a id="hdinsight-nsg"></a>Example: network security groups with HDInsight</span></span>

<span data-ttu-id="74f5d-420">esempi di Hello in questa sezione illustrano come gruppo di sicurezza di rete toocreate regole che consentono di HDInsight toocommunicate con hello servizi di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="74f5d-420">hello examples in this section demonstrate how toocreate network security group rules that allow HDInsight toocommunicate with hello Azure management services.</span></span> <span data-ttu-id="74f5d-421">Prima di usare esempi di hello regolare hello IP indirizzi toomatch hello quelli per hello regione di Azure in uso.</span><span class="sxs-lookup"><span data-stu-id="74f5d-421">Before using hello examples, adjust hello IP addresses toomatch hello ones for hello Azure region you are using.</span></span> <span data-ttu-id="74f5d-422">È possibile trovare queste informazioni in hello [HDInsight con gruppi di sicurezza di rete e le route definite dall'utente](#hdinsight-ip) sezione.</span><span class="sxs-lookup"><span data-stu-id="74f5d-422">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-resource-management-template"></a><span data-ttu-id="74f5d-423">Modello di Resource Manager di Azure</span><span class="sxs-lookup"><span data-stu-id="74f5d-423">Azure Resource Management template</span></span>

<span data-ttu-id="74f5d-424">Hello seguente modello di gestione delle risorse consente di creare una rete virtuale che consente di limitare il traffico in ingresso, ma consente il traffico proveniente da indirizzi IP hello necessario da HDInsight.</span><span class="sxs-lookup"><span data-stu-id="74f5d-424">hello following Resource Management template creates a virtual network that restricts inbound traffic, but allows traffic from hello IP addresses required by HDInsight.</span></span> <span data-ttu-id="74f5d-425">Questo modello crea anche un cluster HDInsight nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-425">This template also creates an HDInsight cluster in hello virtual network.</span></span>

* <span data-ttu-id="74f5d-426">[Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/) (Distribuire una rete virtuale di Azure protetta e un cluster Hadoop HDInsight)</span><span class="sxs-lookup"><span data-stu-id="74f5d-426">[Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74f5d-427">Modificare gli indirizzi IP hello utilizzati in questo hello toomatch esempio regione di Azure in uso.</span><span class="sxs-lookup"><span data-stu-id="74f5d-427">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="74f5d-428">È possibile trovare queste informazioni in hello [HDInsight con gruppi di sicurezza di rete e le route definite dall'utente](#hdinsight-ip) sezione.</span><span class="sxs-lookup"><span data-stu-id="74f5d-428">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="74f5d-429">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="74f5d-429">Azure PowerShell</span></span>

<span data-ttu-id="74f5d-430">Utilizzare hello seguente script di PowerShell toocreate una rete virtuale che consente di limitare il traffico in ingresso e consente il traffico proveniente da hello gli indirizzi IP per l'area Europa settentrionale hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-430">Use hello following PowerShell script toocreate a virtual network that restricts inbound traffic and allows traffic from hello IP addresses for hello North Europe region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74f5d-431">Modificare gli indirizzi IP hello utilizzati in questo hello toomatch esempio regione di Azure in uso.</span><span class="sxs-lookup"><span data-stu-id="74f5d-431">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="74f5d-432">È possibile trovare queste informazioni in hello [HDInsight con gruppi di sicurezza di rete e le route definite dall'utente](#hdinsight-ip) sezione.</span><span class="sxs-lookup"><span data-stu-id="74f5d-432">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with hello resource group hello virtual network is in"
$subnetName = "Replace with hello name of hello subnet that you plan toouse for HDInsight"
# Get hello Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get hello region hello Virtual network is in.
$location = $vnet.Location
# Get hello subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for hello HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 52.164.210.96" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "52.164.210.96" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 13.74.153.132" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "13.74.153.132" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 304 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 305 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "blockeverything" `
        -Description "Block everything else" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "*" `
        -SourceAddressPrefix "Internet" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Deny `
        -Priority 500 `
        -Direction Inbound
# Set hello changes toohello security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply hello NSG toohello subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> <span data-ttu-id="74f5d-433">In questo esempio viene illustrato come tooadd tooallow di regole in entrata traffico sugli indirizzi IP hello necessario.</span><span class="sxs-lookup"><span data-stu-id="74f5d-433">This example demonstrates how tooadd rules tooallow inbound traffic on hello required IP addresses.</span></span> <span data-ttu-id="74f5d-434">Non contiene una regola toorestrict accesso in entrata da altre origini.</span><span class="sxs-lookup"><span data-stu-id="74f5d-434">It does not contain a rule toorestrict inbound access from other sources.</span></span>
>
> <span data-ttu-id="74f5d-435">Hello di esempio seguente viene illustrato come accedere tooenable SSH da hello Internet:</span><span class="sxs-lookup"><span data-stu-id="74f5d-435">hello following example demonstrates how tooenable SSH access from hello Internet:</span></span>
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a><span data-ttu-id="74f5d-436">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="74f5d-436">Azure CLI</span></span>

<span data-ttu-id="74f5d-437">Utilizzare i seguenti passaggi toocreate una rete virtuale che consente di limitare il traffico in ingresso, ma consente il traffico proveniente da indirizzi IP hello necessario da HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-437">Use hello following steps toocreate a virtual network that restricts inbound traffic, but allows traffic from hello IP addresses required by HDInsight.</span></span>

1. <span data-ttu-id="74f5d-438">Hello utilizzo successivo comando toocreate un nuovo gruppo di sicurezza di rete denominato `hdisecure`.</span><span class="sxs-lookup"><span data-stu-id="74f5d-438">Use hello following command toocreate a new network security group named `hdisecure`.</span></span> <span data-ttu-id="74f5d-439">Sostituire **RESOURCEGROUPNAME** con gruppo di risorse hello contenente hello rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="74f5d-439">Replace **RESOURCEGROUPNAME** with hello resource group that contains hello Azure Virtual Network.</span></span> <span data-ttu-id="74f5d-440">Sostituire **percorso** con percorso hello (area) creato in quel gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-440">Replace **LOCATION** with hello location (region) that hello group was created in.</span></span>

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    <span data-ttu-id="74f5d-441">Dopo aver creato il gruppo di hello, vengono visualizzate informazioni sul nuovo gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-441">Once hello group has been created, you receive information on hello new group.</span></span>

2. <span data-ttu-id="74f5d-442">Utilizzare hello seguente tooadd regole toohello nuovo gruppo di sicurezza rete che consentono le comunicazioni in ingresso sulla porta 443 da hello servizio integrità e la gestione di Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="74f5d-442">Use hello following tooadd rules toohello new network security group that allow inbound communication on port 443 from hello Azure HDInsight health and management service.</span></span> <span data-ttu-id="74f5d-443">Sostituire **RESOURCEGROUPNAME** con nome hello hello del gruppo di risorse contenente hello rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="74f5d-443">Replace **RESOURCEGROUPNAME** with hello name of hello resource group that contains hello Azure Virtual Network.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="74f5d-444">Modificare gli indirizzi IP hello utilizzati in questo hello toomatch esempio regione di Azure in uso.</span><span class="sxs-lookup"><span data-stu-id="74f5d-444">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="74f5d-445">È possibile trovare queste informazioni in hello [HDInsight con gruppi di sicurezza di rete e le route definite dall'utente](#hdinsight-ip) sezione.</span><span class="sxs-lookup"><span data-stu-id="74f5d-445">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. <span data-ttu-id="74f5d-446">tooretrieve hello identificatore univoco per questo gruppo di sicurezza di rete, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="74f5d-446">tooretrieve hello unique identifier for this network security group, use hello following command:</span></span>

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    <span data-ttu-id="74f5d-447">Questo comando restituisce un toohello simile valore testo seguente:</span><span class="sxs-lookup"><span data-stu-id="74f5d-447">This command returns a value similar toohello following text:</span></span>

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    <span data-ttu-id="74f5d-448">Utilizzare virgolette doppie id comando hello se non si ottengono risultati hello previsto.</span><span class="sxs-lookup"><span data-stu-id="74f5d-448">Use double-quotes around id in hello command if you don't get hello expected results.</span></span>

4. <span data-ttu-id="74f5d-449">Utilizzare hello successivo comando tooapply hello rete sicurezza gruppo tooa subnet.</span><span class="sxs-lookup"><span data-stu-id="74f5d-449">Use hello following command tooapply hello network security group tooa subnet.</span></span> <span data-ttu-id="74f5d-450">Sostituire hello __GUID__ e __RESOURCEGROUPNAME__ valori con quelli hello restituito dal passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-450">Replace hello __GUID__ and __RESOURCEGROUPNAME__ values with hello ones returned from hello previous step.</span></span> <span data-ttu-id="74f5d-451">Sostituire __VNETNAME__ e __SUBNETNAME__ con il nome di rete virtuale hello e subnet che si desidera toocreate.</span><span class="sxs-lookup"><span data-stu-id="74f5d-451">Replace __VNETNAME__ and __SUBNETNAME__ with hello virtual network name and subnet name that you want toocreate.</span></span>

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    <span data-ttu-id="74f5d-452">Dopo il completamento del comando, è possibile installare HDInsight in hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="74f5d-452">Once this command completes, you can install HDInsight into hello Virtual Network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74f5d-453">Questi passaggi aprire solo accesso toohello HDInsight integrità e la gestione del servizio nel cloud di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-453">These steps only open access toohello HDInsight health and management service on hello Azure cloud.</span></span> <span data-ttu-id="74f5d-454">Qualsiasi altro accesso toohello cluster HDInsight da hello di fuori rete virtuale è bloccata.</span><span class="sxs-lookup"><span data-stu-id="74f5d-454">Any other access toohello HDInsight cluster from outside hello Virtual Network is blocked.</span></span> <span data-ttu-id="74f5d-455">accesso tooenable da rete virtuale esterna hello, è necessario aggiungere regole aggiuntive di gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="74f5d-455">tooenable access from outside hello virtual network, you must add additional Network Security Group rules.</span></span>
>
> <span data-ttu-id="74f5d-456">Hello di esempio seguente viene illustrato come accedere tooenable SSH da hello Internet:</span><span class="sxs-lookup"><span data-stu-id="74f5d-456">hello following example demonstrates how tooenable SSH access from hello Internet:</span></span>
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <span data-ttu-id="74f5d-457"><a id="example-dns"></a> Esempio: configurazione DNS</span><span class="sxs-lookup"><span data-stu-id="74f5d-457"><a id="example-dns"></a> Example: DNS configuration</span></span>

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a><span data-ttu-id="74f5d-458">Risoluzione dei nomi tra una rete virtuale e una rete locale connessa</span><span class="sxs-lookup"><span data-stu-id="74f5d-458">Name resolution between a virtual network and a connected on-premises network</span></span>

<span data-ttu-id="74f5d-459">In questo esempio viene hello seguenti presupposti:</span><span class="sxs-lookup"><span data-stu-id="74f5d-459">This example makes hello following assumptions:</span></span>

* <span data-ttu-id="74f5d-460">Si dispone di una rete virtuale di Azure che è una rete locale tooan connessi tramite un gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="74f5d-460">You have an Azure Virtual Network that is connected tooan on-premises network using a VPN gateway.</span></span>

* <span data-ttu-id="74f5d-461">server DNS personalizzato Hello nella rete virtuale hello è in esecuzione Linux o Unix come sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-461">hello custom DNS server in hello virtual network is running Linux or Unix as hello operating system.</span></span>

* <span data-ttu-id="74f5d-462">[Associare](https://www.isc.org/downloads/bind/) è installato nel server DNS personalizzato hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-462">[Bind](https://www.isc.org/downloads/bind/) is installed on hello custom DNS server.</span></span>

<span data-ttu-id="74f5d-463">Nel server DNS personalizzato hello nella rete virtuale hello:</span><span class="sxs-lookup"><span data-stu-id="74f5d-463">On hello custom DNS server in hello virtual network:</span></span>

1. <span data-ttu-id="74f5d-464">Utilizza Azure PowerShell o Azure CLI toofind hello il suffisso DNS della rete virtuale hello:</span><span class="sxs-lookup"><span data-stu-id="74f5d-464">Use either Azure PowerShell or Azure CLI toofind hello DNS suffix of hello virtual network:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="74f5d-465">Nel server DNS personalizzato hello per la rete virtuale hello, utilizzare hello segue testo come contenuto di hello di hello `/etc/bind/named.conf.local` file:</span><span class="sxs-lookup"><span data-stu-id="74f5d-465">On hello custom DNS server for hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.local` file:</span></span>

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    <span data-ttu-id="74f5d-466">Sostituire hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` valore con il suffisso DNS hello della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="74f5d-466">Replace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with hello DNS suffix of your virtual network.</span></span>

    <span data-ttu-id="74f5d-467">Questa configurazione consente di indirizzare tutte le richieste DNS per il suffisso DNS hello del sistema di risoluzione ricorsiva Azure toohello di hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="74f5d-467">This configuration routes all DNS requests for hello DNS suffix of hello virtual network toohello Azure recursive resolver.</span></span>

2. <span data-ttu-id="74f5d-468">Nel server DNS personalizzato hello per la rete virtuale hello, utilizzare hello segue testo come contenuto di hello di hello `/etc/bind/named.conf.options` file:</span><span class="sxs-lookup"><span data-stu-id="74f5d-468">On hello custom DNS server for hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients tooaccept requests from
    // TODO: Add hello IP range of hello joined network toothis list
    acl goodclients {
        10.0.0.0/16; # IP address range of hello virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent toohello following
            forwarders {
                192.168.0.1; # Replace with hello IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="74f5d-469">Sostituire hello `10.0.0.0/16` valore con l'intervallo di indirizzi IP hello della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="74f5d-469">Replace hello `10.0.0.0/16` value with hello IP address range of your virtual network.</span></span> <span data-ttu-id="74f5d-470">Questa voce consente l'indirizzamento delle richieste di risoluzione dei nomi all'interno di questo intervallo.</span><span class="sxs-lookup"><span data-stu-id="74f5d-470">This entry allows name resolution requests addresses within this range.</span></span>

    * <span data-ttu-id="74f5d-471">Aggiungi intervallo di indirizzi IP hello di hello locale rete toohello `acl goodclients { ... }` sezione.</span><span class="sxs-lookup"><span data-stu-id="74f5d-471">Add hello IP address range of hello on-premises network toohello `acl goodclients { ... }` section.</span></span>  <span data-ttu-id="74f5d-472">voce consente le richieste di risoluzione nome dalle risorse nella rete locale hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-472">entry allows name resolution requests from resources in hello on-premises network.</span></span>
    
    * <span data-ttu-id="74f5d-473">Sostituire il valore di hello `192.168.0.1` con indirizzo IP di hello del server DNS locale.</span><span class="sxs-lookup"><span data-stu-id="74f5d-473">Replace hello value `192.168.0.1` with hello IP address of your on-premises DNS server.</span></span> <span data-ttu-id="74f5d-474">Questa voce indirizza tutte le altre richieste toohello locale DNS server DNS.</span><span class="sxs-lookup"><span data-stu-id="74f5d-474">This entry routes all other DNS requests toohello on-premises DNS server.</span></span>

3. <span data-ttu-id="74f5d-475">configurazione di hello toouse, riavviare l'operazione di binding.</span><span class="sxs-lookup"><span data-stu-id="74f5d-475">toouse hello configuration, restart Bind.</span></span> <span data-ttu-id="74f5d-476">ad esempio `sudo service bind9 restart`.</span><span class="sxs-lookup"><span data-stu-id="74f5d-476">For example, `sudo service bind9 restart`.</span></span>

4. <span data-ttu-id="74f5d-477">Aggiungere un server DNS di server d'inoltro condizionale toohello locale.</span><span class="sxs-lookup"><span data-stu-id="74f5d-477">Add a conditional forwarder toohello on-premises DNS server.</span></span> <span data-ttu-id="74f5d-478">Configurare le richieste di hello server d'inoltro condizionale toosend per il suffisso DNS hello dal passaggio 1 toohello un server DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="74f5d-478">Configure hello conditional forwarder toosend requests for hello DNS suffix from step 1 toohello custom DNS server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="74f5d-479">Consultare la documentazione hello per il DNS per informazioni dettagliate su come tooadd un server d'inoltro condizionale.</span><span class="sxs-lookup"><span data-stu-id="74f5d-479">Consult hello documentation for your DNS software for specifics on how tooadd a conditional forwarder.</span></span>

<span data-ttu-id="74f5d-480">Dopo aver completato questi passaggi, è possibile connettersi tooresources in una rete tramite nomi di dominio completo (FQDN).</span><span class="sxs-lookup"><span data-stu-id="74f5d-480">After completing these steps, you can connect tooresources in either network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="74f5d-481">È ora possibile installare HDInsight in rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-481">You can now install HDInsight into hello virtual network.</span></span>

### <a name="name-resolution-between-two-connected-virtual-networks"></a><span data-ttu-id="74f5d-482">Risoluzione dei nomi tra due reti virtuali connesse</span><span class="sxs-lookup"><span data-stu-id="74f5d-482">Name resolution between two connected virtual networks</span></span>

<span data-ttu-id="74f5d-483">In questo esempio viene hello seguenti presupposti:</span><span class="sxs-lookup"><span data-stu-id="74f5d-483">This example makes hello following assumptions:</span></span>

* <span data-ttu-id="74f5d-484">Si dispone di due reti virtuali di Azure connesse tramite gateway VPN o peering.</span><span class="sxs-lookup"><span data-stu-id="74f5d-484">You have two Azure Virtual Networks that are connected using either a VPN gateway or peering.</span></span>

* <span data-ttu-id="74f5d-485">server DNS personalizzato Hello in entrambe le reti è in esecuzione Linux o Unix come sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-485">hello custom DNS server in both networks is running Linux or Unix as hello operating system.</span></span>

* <span data-ttu-id="74f5d-486">[Associare](https://www.isc.org/downloads/bind/) è installato nel server DNS personalizzati hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-486">[Bind](https://www.isc.org/downloads/bind/) is installed on hello custom DNS servers.</span></span>

1. <span data-ttu-id="74f5d-487">Utilizza Azure PowerShell o Azure CLI toofind hello il suffisso DNS di entrambe le reti virtuali:</span><span class="sxs-lookup"><span data-stu-id="74f5d-487">Use either Azure PowerShell or Azure CLI toofind hello DNS suffix of both virtual networks:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="74f5d-488">Hello utilizzo successivo di testo come contenuto di hello di hello `/etc/bind/named.config.local` file in un server DNS personalizzato hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-488">Use hello following text as hello contents of hello `/etc/bind/named.config.local` file on hello custom DNS server.</span></span> <span data-ttu-id="74f5d-489">Apportare questa modifica nel server DNS personalizzato hello in entrambe le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="74f5d-489">Make this change on hello custom DNS server in both virtual networks.</span></span>

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello IP address of hello DNS server in hello other virtual network
    };
    ```

    <span data-ttu-id="74f5d-490">Sostituire hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` valore con il suffisso DNS hello hello __altri__ rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="74f5d-490">Replace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with hello DNS suffix of hello __other__ virtual network.</span></span> <span data-ttu-id="74f5d-491">Questa voce instrada le richieste per il suffisso DNS hello di hello rete remota toohello personalizzato DNS nella rete.</span><span class="sxs-lookup"><span data-stu-id="74f5d-491">This entry routes requests for hello DNS suffix of hello remote network toohello custom DNS in that network.</span></span>

3. <span data-ttu-id="74f5d-492">Nei server DNS personalizzato hello di entrambe le reti virtuali, utilizzare hello segue testo come contenuto di hello di hello `/etc/bind/named.conf.options` file:</span><span class="sxs-lookup"><span data-stu-id="74f5d-492">On hello custom DNS servers in both virtual networks, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients tooaccept requests from
    acl goodclients {
        10.1.0.0/16; # hello IP address range of one virtual network
        10.0.0.0/16; # hello IP address range of hello other virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            forwarders {
            168.63.129.16;   # Azure recursive resolver         
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="74f5d-493">Sostituire hello `10.0.0.0/16` e `10.1.0.0/16` valori con IP hello intervalli della rete virtuale di indirizzi.</span><span class="sxs-lookup"><span data-stu-id="74f5d-493">Replace hello `10.0.0.0/16` and `10.1.0.0/16` values with hello IP address ranges of your virtual networks.</span></span> <span data-ttu-id="74f5d-494">Questa voce consente le risorse in ogni rete toomake le richieste dei server DNS hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-494">This entry allows resources in each network toomake requests of hello DNS servers.</span></span>

    <span data-ttu-id="74f5d-495">Tutte le richieste che non sono per i suffissi DNS hello di reti virtuali hello (ad esempio microsoft.com) viene gestita dal sistema di risoluzione ricorsiva Azure hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-495">Any requests that are not for hello DNS suffixes of hello virtual networks (for example, microsoft.com) is handled by hello Azure recursive resolver.</span></span>

4. <span data-ttu-id="74f5d-496">configurazione di hello toouse, riavviare l'operazione di binding.</span><span class="sxs-lookup"><span data-stu-id="74f5d-496">toouse hello configuration, restart Bind.</span></span> <span data-ttu-id="74f5d-497">Ad esempio `sudo service bind9 restart` su entrambi i server DNS.</span><span class="sxs-lookup"><span data-stu-id="74f5d-497">For example, `sudo service bind9 restart` on both DNS servers.</span></span>

<span data-ttu-id="74f5d-498">Dopo aver completato questi passaggi, è possibile connettersi tooresources nella rete virtuale di hello utilizzando nomi di dominio completo (FQDN).</span><span class="sxs-lookup"><span data-stu-id="74f5d-498">After completing these steps, you can connect tooresources in hello virtual network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="74f5d-499">È ora possibile installare HDInsight in rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="74f5d-499">You can now install HDInsight into hello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74f5d-500">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="74f5d-500">Next steps</span></span>

* <span data-ttu-id="74f5d-501">Per un esempio end-to-end di configurazione di rete locale tooan tooconnect di HDInsight, vedere [rete locale di connettersi a HDInsight tooan](./connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="74f5d-501">For an end-to-end example of configuring HDInsight tooconnect tooan on-premises network, see [Connect HDInsight tooan on-premises network](./connect-on-premises-network.md).</span></span>

* <span data-ttu-id="74f5d-502">Per ulteriori informazioni su reti virtuali di Azure, vedere hello [Cenni preliminari sulla rete virtuale di Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="74f5d-502">For more information on Azure virtual networks, see hello [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="74f5d-503">Per altre informazioni sui gruppi di sicurezza di rete, vedere [Gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="74f5d-503">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="74f5d-504">Per altre informazioni sulle route definite dall'utente, vedere [Route definite dall'utente e inoltro IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="74f5d-504">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>