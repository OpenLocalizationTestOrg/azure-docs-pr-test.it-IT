---
title: Estendere HDInsight con Rete virtuale - Azure | Microsoft Docs
description: Informazioni su come usare Rete virtuale di Azure per la connessione di HDInsight ad altre risorse cloud o risorse nel proprio data center
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
ms.openlocfilehash: 380423ec42ad4905c73fcd57501102e9f7062e81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a><span data-ttu-id="9dc1f-103">Estendere Azure HDInsight usando Rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="9dc1f-103">Extend Azure HDInsight using an Azure Virtual Network</span></span>

<span data-ttu-id="9dc1f-104">Informazioni su come usare HDInsight con [Rete virtuale di Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-104">Learn how to use HDInsight with an [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="9dc1f-105">Il servizio Rete virtuale di Azure consente di implementare gli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-105">Using an Azure Virtual Network enables the following scenarios:</span></span>

* <span data-ttu-id="9dc1f-106">Connessione a HDInsight direttamente da una rete locale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-106">Connecting to HDInsight directly from an on-premises network.</span></span>

* <span data-ttu-id="9dc1f-107">Connessione di HDInsight ad archivi dati in una rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-107">Connecting HDInsight to data stores in an Azure Virtual network.</span></span>

* <span data-ttu-id="9dc1f-108">Accesso diretto ai servizi Hadoop che non sono disponibili pubblicamente su Internet,</span><span class="sxs-lookup"><span data-stu-id="9dc1f-108">Directly accessing Hadoop services that are not available publicly over the internet.</span></span> <span data-ttu-id="9dc1f-109">ad esempio le API Kafka o l'API Java HBase.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-109">For example, Kafka APIs or the HBase Java API.</span></span>

> [!WARNING]
> <span data-ttu-id="9dc1f-110">Le informazioni contenute in questo documento richiedono la conoscenza delle reti TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-110">The information in this document requires an understanding of TCP/IP networking.</span></span> <span data-ttu-id="9dc1f-111">Se non si ha familiarità con le reti TCP/IP, è consigliabile collaborare con qualcuno che ne abbia conoscenza se si intende apportare modifiche alle reti di produzione.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-111">If you are not familiar with TCP/IP networking, you should partner with someone who is before making modifications to production networks.</span></span>

## <a name="planning"></a><span data-ttu-id="9dc1f-112">Pianificazione</span><span class="sxs-lookup"><span data-stu-id="9dc1f-112">Planning</span></span>

<span data-ttu-id="9dc1f-113">Di seguito sono elencate le domande che è necessario porsi quando si intende installare HDInsight in una rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-113">The following are the questions that you must answer when planning to install HDInsight in a virtual network:</span></span>

* <span data-ttu-id="9dc1f-114">Occorre installare HDInsight in una rete virtuale esistente?</span><span class="sxs-lookup"><span data-stu-id="9dc1f-114">Do you need to install HDInsight into an existing virtual network?</span></span> <span data-ttu-id="9dc1f-115">Oppure si intende creare una rete nuova?</span><span class="sxs-lookup"><span data-stu-id="9dc1f-115">Or are you creating a new network?</span></span>

    <span data-ttu-id="9dc1f-116">Se si usa una rete virtuale esistente, potrebbe essere necessario modificare la configurazione di rete prima di poter installare HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-116">If you are using an existing virtual network, you may need to modify the network configuration before you can install HDInsight.</span></span> <span data-ttu-id="9dc1f-117">Per altre informazioni, vedere la sezione [Aggiungere HDInsight a una rete virtuale esistente](#existingvnet).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-117">For more information, see the [add HDInsight to an existing virtual network](#existingvnet) section.</span></span>

* <span data-ttu-id="9dc1f-118">La rete virtuale che contiene HDInsight deve essere connessa a un'altra rete virtuale o alla rete locale?</span><span class="sxs-lookup"><span data-stu-id="9dc1f-118">Do you want to connect the virtual network containing HDInsight to another virtual network or your on-premises network?</span></span>

    <span data-ttu-id="9dc1f-119">Per usare facilmente le risorse tra più reti, potrebbe essere necessario creare un DNS personalizzato e configurare l'inoltro DNS.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-119">To easily work with resources across networks, you may need to create a custom DNS and configure DNS forwarding.</span></span> <span data-ttu-id="9dc1f-120">Per altre informazioni, vedere la sezione [Connessione a più reti](#multinet).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-120">For more information, see the [connecting multiple networks](#multinet) section.</span></span>

* <span data-ttu-id="9dc1f-121">Si vuole limitare/reindirizzare il traffico in ingresso o in uscita a HDInsight?</span><span class="sxs-lookup"><span data-stu-id="9dc1f-121">Do you want to restrict/redirect inbound or outbound traffic to HDInsight?</span></span>

    <span data-ttu-id="9dc1f-122">HDInsight deve disporre di una comunicazione senza restrizioni con indirizzi IP specifici nel data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-122">HDInsight must have unrestricted communication with specific IP addresses in the Azure data center.</span></span> <span data-ttu-id="9dc1f-123">Sono presenti anche diverse porte che devono essere abilitate attraverso i firewall per la comunicazione client.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-123">There are also several ports that must be allowed through firewalls for client communication.</span></span> <span data-ttu-id="9dc1f-124">Per altre informazioni, vedere la sezione [Controllo del traffico di rete](#networktraffic).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-124">For more information, see the [controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="9dc1f-125"><a id="existingvnet"></a>Aggiungere HDInsight a una rete virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="9dc1f-125"><a id="existingvnet"></a>Add HDInsight to an existing virtual network</span></span>

<span data-ttu-id="9dc1f-126">Seguire la procedura in questa sezione per aggiungere un nuovo cluster HDInsight a una rete virtuale di Azure esistente.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-126">Use the steps in this section to discover how to add a new HDInsight to an existing Azure Virtual Network.</span></span>

> [!NOTE]
> <span data-ttu-id="9dc1f-127">È possibile aggiungere un cluster HDInsight esistente in una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-127">You cannot add an existing HDInsight cluster into a virtual network.</span></span>

1. <span data-ttu-id="9dc1f-128">Si intende usare un modello di distribuzione classico o di Resource Manager per la rete virtuale?</span><span class="sxs-lookup"><span data-stu-id="9dc1f-128">Are you using a classic or Resource Manager deployment model for the virtual network?</span></span>

    <span data-ttu-id="9dc1f-129">HDInsight 3.4 e versione successiva richiedono l'utilizzo di una rete virtuale di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-129">HDInsight 3.4 and greater requires a Resource Manager virtual network.</span></span> <span data-ttu-id="9dc1f-130">Le versioni precedenti di HDInsight richiedono una rete virtuale classica.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-130">Earlier versions of HDInsight required a classic virtual network.</span></span>

    <span data-ttu-id="9dc1f-131">Se la rete virtuale esistente è un modello classico, è necessario creare una rete virtuale di Resource Manager e successivamente connettere le due reti.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-131">If your existing network is a classic virtual network, then you must create a Resource Manager virtual network and then connect the two.</span></span> <span data-ttu-id="9dc1f-132">[Connessione di reti virtuali classiche a reti virtuali nuove](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-132">[Connecting classic VNets to new VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

    <span data-ttu-id="9dc1f-133">Dopo che le due reti sono state unite, HDInsight installato nella rete di Resource Manager può interagire con le risorse della rete classica.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-133">Once joined, HDInsight installed in the Resource Manager network can interact with resources in the classic network.</span></span>

2. <span data-ttu-id="9dc1f-134">Si usa il tunneling forzato?</span><span class="sxs-lookup"><span data-stu-id="9dc1f-134">Do you use forced tunneling?</span></span> <span data-ttu-id="9dc1f-135">Il tunneling forzato è un'impostazione di subnet che spinge il traffico Internet in uscita verso un dispositivo per l'ispezione e la registrazione.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-135">Forced tunneling is a subnet setting that forces outbound Internet traffic to a device for inspection and logging.</span></span> <span data-ttu-id="9dc1f-136">HDInsight non supporta il tunneling forzato.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-136">HDInsight does not support forced tunneling.</span></span> <span data-ttu-id="9dc1f-137">Occorre quindi rimuovere questa funzionalità prima di installare HDInsight in una subnet oppure si può creare una nuova subnet per HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-137">Either remove forced tunneling before installing HDInsight into a subnet, or create a new subnet for HDInsight.</span></span>

3. <span data-ttu-id="9dc1f-138">Si usano gruppi di sicurezza di rete, route definite dall'utente o appliance di rete virtuali per limitare il traffico all'interno o all'esterno della rete virtuale?</span><span class="sxs-lookup"><span data-stu-id="9dc1f-138">Do you use network security groups, user-defined routes, or Virtual Network Appliances to restrict traffic into or out of the virtual network?</span></span>

    <span data-ttu-id="9dc1f-139">In qualità di servizio gestito, HDInsight richiede l'accesso senza restrizioni a vari indirizzi IP nel data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-139">As a managed service, HDInsight requires unrestricted access to several IP addresses in the Azure data center.</span></span> <span data-ttu-id="9dc1f-140">Per consentire la comunicazione con questi indirizzi IP, aggiornare tutti i gruppi di sicurezza di rete o le route definite dall'utente esistenti.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-140">To allow communication with these IP addresses, update any existing network security groups or user-defined routes.</span></span>

    <span data-ttu-id="9dc1f-141">HDInsight ospita più servizi, che usano porte diverse.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-141">HDInsight  hosts multiple services, which use a variety of ports.</span></span> <span data-ttu-id="9dc1f-142">Non bloccare il traffico indirizzato a queste porte.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-142">Do not block traffic to these ports.</span></span> <span data-ttu-id="9dc1f-143">Per un elenco di porte da abilitare attraverso i firewall dell'appliance virtuale, vedere la sezione [Sicurezza](#security).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-143">For a list of ports to allow through virtual appliance firewalls, see the [Security](#security) section.</span></span>

    <span data-ttu-id="9dc1f-144">Per trovare la configurazione di sicurezza esistente, usare i comandi di Azure PowerShell o dell'interfaccia della riga di comando di Azure che seguono:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-144">To find your existing security configuration, use the following Azure PowerShell or Azure CLI commands:</span></span>

    * <span data-ttu-id="9dc1f-145">Gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="9dc1f-145">Network security groups</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="9dc1f-146">Per altre informazioni, vedere il documento [Risolvere i problemi relativi ai gruppi di sicurezza di rete](../virtual-network/virtual-network-nsg-troubleshoot-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-146">For more information, see the [Troubleshoot network security groups](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="9dc1f-147">Le regole di gruppo di sicurezza di rete vengono applicate seguendo un ordine basato sulla priorità delle regole.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-147">Network security group rules are applied in order based on rule priority.</span></span> <span data-ttu-id="9dc1f-148">Viene applicata la prima regola che corrisponde al modello di traffico, dopodiché non vengono applicate altre regole per quel traffico.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-148">The first rule that matches the traffic pattern is applied, and no others are applied for that traffic.</span></span> <span data-ttu-id="9dc1f-149">Ordinare le regole dalla più permissiva alla più restrittiva.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-149">Order rules from most permissive to least permissive.</span></span> <span data-ttu-id="9dc1f-150">Per altre informazioni, vedere il documento [Filtrare il traffico di rete con gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-150">For more information, see the [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    * <span data-ttu-id="9dc1f-151">Route definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="9dc1f-151">User-defined routes</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="9dc1f-152">Per altre informazioni, vedere il documento [Risolvere i problemi relativi alle route](../virtual-network/virtual-network-routes-troubleshoot-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-152">For more information, see the [Troubleshoot routes](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span></span>

4. <span data-ttu-id="9dc1f-153">Creare un cluster HDInsight e selezionare la rete virtuale di Azure durante la configurazione.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-153">Create an HDInsight cluster and select the Azure Virtual Network during configuration.</span></span> <span data-ttu-id="9dc1f-154">Per comprendere il processo di creazione del cluster, attenersi alla procedura nei documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-154">Use the steps in the following documents to understand the cluster creation process:</span></span>

    * [<span data-ttu-id="9dc1f-155">Creare cluster HDInsight tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9dc1f-155">Create HDInsight using the Azure portal</span></span>](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [<span data-ttu-id="9dc1f-156">Creare cluster HDInsight tramite Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9dc1f-156">Create HDInsight using Azure PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [<span data-ttu-id="9dc1f-157">Creare cluster HDInsight tramite l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="9dc1f-157">Create HDInsight using Azure CLI 1.0</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [<span data-ttu-id="9dc1f-158">Creare cluster HDInsight tramite un modello Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9dc1f-158">Create HDInsight using an Azure Resource Manager template</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > <span data-ttu-id="9dc1f-159">L'aggiunta di un cluster HDInsight a una rete virtuale è un passaggio di configurazione facoltativo.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-159">Adding HDInsight to a virtual network is an optional configuration step.</span></span> <span data-ttu-id="9dc1f-160">Assicurarsi di selezionare la rete virtuale quando si configura il cluster.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-160">Be sure to select the virtual network when configuring the cluster.</span></span>

## <span data-ttu-id="9dc1f-161"><a id="multinet"></a>Connessione a più reti</span><span class="sxs-lookup"><span data-stu-id="9dc1f-161"><a id="multinet"></a>Connecting multiple networks</span></span>

<span data-ttu-id="9dc1f-162">Il problema più grande con una configurazione con più reti è la risoluzione dei nomi tra le reti.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-162">The biggest challenge with a multi-network configuration is name resolution between the networks.</span></span>

<span data-ttu-id="9dc1f-163">Azure assicura la risoluzione dei nomi per i servizi di Azure che vengono installati in una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-163">Azure provides name resolution for Azure services that are installed in a virtual network.</span></span> <span data-ttu-id="9dc1f-164">La risoluzione dei nomi integrata consente a HDInsight di connettersi alle risorse seguenti usando un nome di dominio completo (FQDN):</span><span class="sxs-lookup"><span data-stu-id="9dc1f-164">This built-in name resolution allows HDInsight to connect to the following resources by using a fully qualified domain name (FQDN):</span></span>

* <span data-ttu-id="9dc1f-165">Qualsiasi risorsa disponibile in Internet,</span><span class="sxs-lookup"><span data-stu-id="9dc1f-165">Any resource that is available on the internet.</span></span> <span data-ttu-id="9dc1f-166">ad esempio microsoft.com, google.com.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-166">For example, microsoft.com, google.com.</span></span>

* <span data-ttu-id="9dc1f-167">Qualsiasi risorsa che si trovi nella stessa rete virtuale di Azure tramite l'utilizzo del __nome DNS interno__ della risorsa.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-167">Any resource that is in the same Azure Virtual Network, by using the __internal DNS name__ of the resource.</span></span> <span data-ttu-id="9dc1f-168">Quando ad esempio si usa la risoluzione dei nomi predefinita, i seguenti sono nomi DNS interni di esempio assegnati a nodi del ruolo di lavoro di HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-168">For example, when using the default name resolution, the following are example internal DNS names assigned to HDInsight worker nodes:</span></span>

    * <span data-ttu-id="9dc1f-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="9dc1f-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>
    * <span data-ttu-id="9dc1f-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="9dc1f-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>

    <span data-ttu-id="9dc1f-171">Entrambi questi nodi possono comunicare direttamente tra loro e con altri nodi in HDInsight, usando i nomi DNS interni.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-171">Both these nodes can communicate directly with each other, and other nodes in HDInsight, by using internal DNS names.</span></span>

<span data-ttu-id="9dc1f-172">La risoluzione dei nomi predefinita __non__ consente a HDInsight di risolvere i nomi di risorse in reti che sono aggiunte alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-172">The default name resolution does __not__ allow HDInsight to resolve the names of resources in networks that are joined to the virtual network.</span></span> <span data-ttu-id="9dc1f-173">È ad esempio pratica diffusa unire la rete locale alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-173">For example, it is common to join your on-premises network to the virtual network.</span></span> <span data-ttu-id="9dc1f-174">Con la semplice risoluzione dei nomi predefinita, HDInsight non può accedere alle risorse della rete locale in base al nome.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-174">With only the default name resolution, HDInsight cannot access resources in the on-premises network by name.</span></span> <span data-ttu-id="9dc1f-175">È vero anche il contrario. Le risorse nella rete locale non possono accedere alle risorse della rete virtuale in base al nome.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-175">The opposite is also true, resources in your on-premises network cannot access resources in the virtual network by name.</span></span>

> [!WARNING]
> <span data-ttu-id="9dc1f-176">È necessario creare il server DNS personalizzato e configurare la rete virtuale per il suo utilizzo prima di creare il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-176">You must create the custom DNS server and configure the virtual network to use it before creating the HDInsight cluster.</span></span>

<span data-ttu-id="9dc1f-177">Per abilitare la risoluzione dei nomi tra la rete virtuale e le risorse in reti aggiunte, è necessario eseguire le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-177">To enable name resolution between the virtual network and resources in joined networks, you must perform the following actions:</span></span>

1. <span data-ttu-id="9dc1f-178">Creare un server DNS personalizzato nella rete virtuale di Azure in cui si intende installare HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-178">Create a custom DNS server in the Azure Virtual Network where you plan to install HDInsight.</span></span>

2. <span data-ttu-id="9dc1f-179">Configurare la rete virtuale per l'utilizzo del server DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-179">Configure the virtual network to use the custom DNS server.</span></span>

3. <span data-ttu-id="9dc1f-180">Trovare il suffisso DNS assegnato da Azure per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-180">Find the Azure assigned DNS suffix for your virtual network.</span></span> <span data-ttu-id="9dc1f-181">Questo valore è simile a `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-181">This value is similar to `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span></span> <span data-ttu-id="9dc1f-182">Per informazioni sulla ricerca del suffisso DNS, vedere la sezione [Esempio: DNS personalizzato](#example-dns).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-182">For information on finding the DNS suffix, see the [Example: Custom DNS](#example-dns) section.</span></span>

4. <span data-ttu-id="9dc1f-183">Configurare l'inoltro tra i server DNS.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-183">Configure forwarding between the DNS servers.</span></span> <span data-ttu-id="9dc1f-184">La configurazione dipende dal tipo di rete remota.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-184">The configuration depends on the type of remote network.</span></span>

    * <span data-ttu-id="9dc1f-185">Se la rete remota è una rete locale, configurare il DNS come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-185">If the remote network is an on-premises network, configure DNS as follows:</span></span>
        
        * <span data-ttu-id="9dc1f-186">__DNS personalizzato__ (nella rete virtuale):</span><span class="sxs-lookup"><span data-stu-id="9dc1f-186">__Custom DNS__ (in the virtual network):</span></span>

            * <span data-ttu-id="9dc1f-187">Inoltrare le richieste per il suffisso DNS della rete virtuale al sistema di risoluzione ricorsiva di Azure (168.63.129.16).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-187">Forward requests for the DNS suffix of the virtual network to the Azure recursive resolver (168.63.129.16).</span></span> <span data-ttu-id="9dc1f-188">Azure gestisce le richieste per le risorse nella rete virtuale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-188">Azure handles requests for resources in the virtual network</span></span>

            * <span data-ttu-id="9dc1f-189">Inoltrare tutte le altre richieste al server DNS locale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-189">Forward all other requests to the on-premises DNS server.</span></span> <span data-ttu-id="9dc1f-190">Il server DNS locale gestisce tutte le altre richieste di risoluzione dei nomi, persino le richieste per le risorse Internet quali Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-190">The on-premises DNS handles all other name resolution requests, even requests for internet resources such as Microsoft.com.</span></span>

        * <span data-ttu-id="9dc1f-191">__DNS locale__: inoltrare le richieste per il suffisso DNS di rete virtuale al server DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-191">__On-premises DNS__: Forward requests for the virtual network DNS suffix to the custom DNS server.</span></span> <span data-ttu-id="9dc1f-192">Il server DNS personalizzato le inoltra quindi al sistema di risoluzione ricorsiva di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-192">The custom DNS server then forwards to the Azure recursive resolver.</span></span>

        <span data-ttu-id="9dc1f-193">Questa configurazione indirizza le richieste di nomi di dominio completi che contengono il suffisso DNS della rete virtuale al server DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-193">This configuration routes requests for fully qualified domain names that contain the DNS suffix of the virtual network to the custom DNS server.</span></span> <span data-ttu-id="9dc1f-194">Tutte le altre richieste (anche per gli indirizzi Internet pubblici) vengono gestite dal server DNS locale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-194">All other requests (even for public internet addresses) are handled by the on-premises DNS server.</span></span>

    * <span data-ttu-id="9dc1f-195">Se la rete remota è un'altra rete virtuale di Azure, configurare il DNS come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-195">If the remote network is another Azure Virtual Network, configure DNS as follows:</span></span>

        * <span data-ttu-id="9dc1f-196">__DNS personalizzato__ (in ogni rete virtuale):</span><span class="sxs-lookup"><span data-stu-id="9dc1f-196">__Custom DNS__ (in each virtual network):</span></span>

            * <span data-ttu-id="9dc1f-197">Le richieste per il suffisso DNS delle reti virtuali vengono inoltrate ai server DNS personalizzati.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-197">Requests for the DNS suffix of the virtual networks are forwarded to the custom DNS servers.</span></span> <span data-ttu-id="9dc1f-198">Il DNS in ogni rete virtuale è responsabile della risoluzione delle risorse all'interno della propria rete.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-198">The DNS in each virtual network is responsible for resolving resources within its network.</span></span>

            * <span data-ttu-id="9dc1f-199">Inoltrare tutte le altre richieste al sistema di risoluzione ricorsiva di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-199">Forward all other requests to the Azure recursive resolver.</span></span> <span data-ttu-id="9dc1f-200">Il sistema di risoluzione ricorsiva è responsabile della risoluzione delle risorse Internet e locali.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-200">The recursive resolver is responsible for resolving local and internet resources.</span></span>

        <span data-ttu-id="9dc1f-201">Il server DNS per ogni rete inoltra le richieste all'altro, in base al suffisso DNS.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-201">The DNS server for each network forwards requests to the other, based on DNS suffix.</span></span> <span data-ttu-id="9dc1f-202">Le altre richieste vengono risolte usando il sistema di risoluzione ricorsiva di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-202">Other requests are resolved using the Azure recursive resolver.</span></span>

    <span data-ttu-id="9dc1f-203">Per un esempio di ogni configurazione, vedere la sezione [Esempio: DNS personalizzato](#example-dns).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-203">For an example of each configuration, see the [Example: Custom DNS](#example-dns) section.</span></span>

<span data-ttu-id="9dc1f-204">Per altre informazioni, vedere il documento [Risoluzione dei nomi per le macchine virtuali e le istanze del ruolo](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-204">For more information, see the [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span></span>

## <a name="directly-connect-to-hadoop-services"></a><span data-ttu-id="9dc1f-205">Connettersi direttamente ai servizi Hadoop</span><span class="sxs-lookup"><span data-stu-id="9dc1f-205">Directly connect to Hadoop services</span></span>

<span data-ttu-id="9dc1f-206">La maggior parte della documentazione in HDInsight presuppone che sia disponibile l'accesso al cluster tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-206">Most documentation on HDInsight assumes that you have access to the cluster over the internet.</span></span> <span data-ttu-id="9dc1f-207">Verificare ad esempio che sia possibile connettersi al cluster all'indirizzo https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-207">For example, that you can connect to the cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="9dc1f-208">Questo indirizzo usa il gateway pubblico, che non è disponibile se sono stati usati gruppi di sicurezza di rete o route definite dall'utente per limitare l'accesso da Internet.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-208">This address uses the public gateway, which is not available if you have used NSGs or UDRs to restrict access from the internet.</span></span>

<span data-ttu-id="9dc1f-209">Per connettersi alle pagine Ambari e ad altre pagine Web tramite la rete virtuale, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-209">To connect to Ambari and other web pages through the virtual network, use the following steps:</span></span>

1. <span data-ttu-id="9dc1f-210">Per individuare i nomi di dominio completi (FQDN) interni dei nodi del cluster HDInsight, usare uno dei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-210">To discover the internal fully qualified domain names (FQDN) of the HDInsight cluster nodes, use one of the following methods:</span></span>

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

    <span data-ttu-id="9dc1f-211">Nell'elenco di nodi restituito, trovare i nomi di dominio completi dei nodi head e usarli per connettersi ad Ambari e altri servizi Web.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-211">In the list of nodes returned, find the FQDN for the head nodes and use the FQDNs to connect to Ambari and other web services.</span></span> <span data-ttu-id="9dc1f-212">Usare ad esempio `http://<headnode-fqdn>:8080` per accedere ad Ambari.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-212">For example, use `http://<headnode-fqdn>:8080` to access Ambari.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9dc1f-213">Alcuni servizi ospitati nei nodi head sono attivi solo in un nodo alla volta.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-213">Some services hosted on the head nodes are only active on one node at a time.</span></span> <span data-ttu-id="9dc1f-214">Se nel tentativo di accedere a un servizio in un nodo head si riceve un messaggio di errore 404, passare al nodo head successivo.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-214">If you try accessing a service on one head node and it returns a 404 error, switch to the other head node.</span></span>

2. <span data-ttu-id="9dc1f-215">Per determinare il nodo e la porta su cui un servizio è disponibile, vedere il documento [Porte usate dai servizi Hadoop su HDInsight](./hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-215">To determine the node and port that a service is available on, see the [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

## <span data-ttu-id="9dc1f-216"><a id="networktraffic"></a> Controllo del traffico di rete</span><span class="sxs-lookup"><span data-stu-id="9dc1f-216"><a id="networktraffic"></a> Controlling network traffic</span></span>

<span data-ttu-id="9dc1f-217">Il traffico di rete nelle reti virtuali di Azure può essere controllato usando i modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-217">Network traffic in an Azure Virtual Networks can be controlled using the following methods:</span></span>

* <span data-ttu-id="9dc1f-218">i **gruppi di sicurezza di rete** (NSG) consentono di filtrare il traffico di rete in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-218">**Network security groups** (NSG) allow you to filter inbound and outbound traffic to the network.</span></span> <span data-ttu-id="9dc1f-219">Per altre informazioni, vedere il documento [Filtrare il traffico di rete con gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-219">For more information, see the [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    > [!WARNING]
    > <span data-ttu-id="9dc1f-220">HDInsight non supporta la limitazione del traffico in uscita.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-220">HDInsight does not support restricting outbound traffic.</span></span>

* <span data-ttu-id="9dc1f-221">Le **route definite dall'utente** definiscono il flusso del traffico tra le risorse nella rete.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-221">**User-defined routes** (UDR) define how traffic flows between resources in the network.</span></span> <span data-ttu-id="9dc1f-222">Per altre informazioni, vedere il documento [Route definite dall'utente e inoltro IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-222">For more information, see the [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md) document.</span></span>

* <span data-ttu-id="9dc1f-223">Le **appliance virtuali di rete** replicano le funzionalità di dispositivi come i firewall e i router.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-223">**Network virtual appliances** replicate the functionality of devices such as firewalls and routers.</span></span> <span data-ttu-id="9dc1f-224">Per altre informazioni, vedere il documento relativo alle [Appliance di rete](https://azure.microsoft.com/solutions/network-appliances).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-224">For more information, see the [Network Appliances](https://azure.microsoft.com/solutions/network-appliances) document.</span></span>

<span data-ttu-id="9dc1f-225">In qualità di servizio gestito, HDInsight richiede l'accesso senza restrizioni a servizi di gestione e integrità di Azure nel cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-225">As a managed service, HDInsight requires unrestricted access to Azure health and management services in the Azure cloud.</span></span> <span data-ttu-id="9dc1f-226">Quando si usano i gruppi di sicurezza di rete e le route definite dall'utente, è necessario assicurarsi che questi servizi possano ancora comunicare con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-226">When using NSGs and UDRs, you must ensure that HDInsight these services can still communicate with HDInsight.</span></span>

<span data-ttu-id="9dc1f-227">HDInsight espone i servizi su porte diverse.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-227">HDInsight exposes services on several ports.</span></span> <span data-ttu-id="9dc1f-228">Quando si usa un firewall di appliance virtuale, è necessario consentire il traffico sulle porte usate per questi servizi.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-228">When using a virtual appliance firewall, you must allow traffic on the ports used for these services.</span></span> <span data-ttu-id="9dc1f-229">Per altre informazioni, vedere la sezione [Porte richieste].</span><span class="sxs-lookup"><span data-stu-id="9dc1f-229">For more information, see the [Required ports] section.</span></span>

### <span data-ttu-id="9dc1f-230"><a id="hdinsight-ip"></a>HDInsight con gruppi di sicurezza di rete e route definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="9dc1f-230"><a id="hdinsight-ip"></a> HDInsight with network security groups and user-defined routes</span></span>

<span data-ttu-id="9dc1f-231">Se si intende usare **gruppi di sicurezza di rete** o **route definite dall'utente** per controllare il traffico di rete, eseguire le azioni seguenti prima di installare HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-231">If you plan on using **network security groups** or **user-defined routes** to control network traffic, perform the following actions before installing HDInsight:</span></span>

1. <span data-ttu-id="9dc1f-232">Identificare l'area di Azure che si intende usare per HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-232">Identify the Azure region that you plan to use for HDInsight.</span></span>

2. <span data-ttu-id="9dc1f-233">Identificare gli indirizzi IP richiesti da HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-233">Identify the IP addresses required by HDInsight.</span></span> <span data-ttu-id="9dc1f-234">Per altre informazioni, vedere la sezione [Indirizzi IP richiesti da HDInsight](#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-234">For more information, see the [IP Addresses required by HDInsight](#hdinsight-ip) section.</span></span>

3. <span data-ttu-id="9dc1f-235">Creare o modificare i gruppi di sicurezza di rete o le route definite dall'utente per la subnet in cui si intende installare HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-235">Create or modify the network security groups or user-defined routes for the subnet that you plan to install HDInsight into.</span></span>

    * <span data-ttu-id="9dc1f-236">__Gruppi di sicurezza di rete__: consentono il traffico __in ingresso__ sulla porta __443__ dagli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-236">__Network security groups__: allow __inbound__ traffic on port __443__ from the IP addresses.</span></span>
    * <span data-ttu-id="9dc1f-237">__Route definite dall'utente__: creare una route per ogni indirizzo IP e impostare __Tipo hop successivo__ su __Internet__.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-237">__User-defined routes__: create a route to each IP address and set the __Next hop type__ to __Internet__.</span></span>

<span data-ttu-id="9dc1f-238">Per altre informazioni sui gruppi di sicurezza di rete o sulle route definite dall'utente, vedere la documentazione seguente:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-238">For more information on network security groups or user-defined routes, see the following documentation:</span></span>

* [<span data-ttu-id="9dc1f-239">Gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="9dc1f-239">Network security group</span></span>](../virtual-network/virtual-networks-nsg.md)

* [<span data-ttu-id="9dc1f-240">Route definite dall'utente</span><span class="sxs-lookup"><span data-stu-id="9dc1f-240">User-defined routes</span></span>](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a><span data-ttu-id="9dc1f-241">Tunneling forzato</span><span class="sxs-lookup"><span data-stu-id="9dc1f-241">Forced tunneling</span></span>

<span data-ttu-id="9dc1f-242">Il tunneling forzato è una configurazione di routing definita dall'utente in cui tutto il traffico da una subnet viene spinto verso una rete o un percorso specifico, ad esempio la rete locale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-242">Forced tunneling is a user-defined routing configuration where all traffic from a subnet is forced to a specific network or location, such as your on-premises network.</span></span> <span data-ttu-id="9dc1f-243">HDInsight __non__ supporta il tunneling forzato.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-243">HDInsight does __not__ support forced tunneling.</span></span>

## <span data-ttu-id="9dc1f-244"><a id="hdinsight-ip"></a> Indirizzi IP richiesti</span><span class="sxs-lookup"><span data-stu-id="9dc1f-244"><a id="hdinsight-ip"></a> Required IP addresses</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9dc1f-245">I servizi di gestione e integrità di Azure devono poter comunicare con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-245">The Azure health and management services must be able to communicate with HDInsight.</span></span> <span data-ttu-id="9dc1f-246">Se si usano gruppi di sicurezza di rete o route definite dall'utente, consentire il traffico dagli indirizzi IP in modo che tali servizi possano raggiungere HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-246">If you use network security groups or user-defined routes, allow traffic from the IP addresses for these services to reach HDInsight.</span></span>
>
> <span data-ttu-id="9dc1f-247">Se non si usano gruppi di sicurezza di rete o route definite dall'utente per controllare il traffico, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-247">If you do not use network security groups or user-defined routes to control traffic, you can ignore this section.</span></span>

<span data-ttu-id="9dc1f-248">Se si usano gruppi di sicurezza di rete o route definite dall'utente, è necessario consentire il traffico dai servizi di gestione e integrità di Azure per raggiungere HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-248">If you use network security groups or user-defined routes, you must allow traffic from the Azure health and management services to reach HDInsight.</span></span> <span data-ttu-id="9dc1f-249">Usare la procedura seguente per trovare gli indirizzi IP che devono essere consentiti:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-249">Use the following steps to find the IP addresses that must be allowed:</span></span>

1. <span data-ttu-id="9dc1f-250">È sempre necessario consentire il traffico dagli indirizzi IP seguenti:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-250">You must always allow traffic from the following IP addresses:</span></span>

    | <span data-ttu-id="9dc1f-251">Indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="9dc1f-251">IP address</span></span> | <span data-ttu-id="9dc1f-252">Porta consentita</span><span class="sxs-lookup"><span data-stu-id="9dc1f-252">Allowed port</span></span> | <span data-ttu-id="9dc1f-253">Direzione</span><span class="sxs-lookup"><span data-stu-id="9dc1f-253">Direction</span></span> |
    | ---- | ----- | ----- |
    | <span data-ttu-id="9dc1f-254">168.61.49.99</span><span class="sxs-lookup"><span data-stu-id="9dc1f-254">168.61.49.99</span></span> | <span data-ttu-id="9dc1f-255">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-255">443</span></span> | <span data-ttu-id="9dc1f-256">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-256">Inbound</span></span> |
    | <span data-ttu-id="9dc1f-257">23.99.5.239</span><span class="sxs-lookup"><span data-stu-id="9dc1f-257">23.99.5.239</span></span> | <span data-ttu-id="9dc1f-258">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-258">443</span></span> | <span data-ttu-id="9dc1f-259">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-259">Inbound</span></span> |
    | <span data-ttu-id="9dc1f-260">168.61.48.131</span><span class="sxs-lookup"><span data-stu-id="9dc1f-260">168.61.48.131</span></span> | <span data-ttu-id="9dc1f-261">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-261">443</span></span> | <span data-ttu-id="9dc1f-262">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-262">Inbound</span></span> |
    | <span data-ttu-id="9dc1f-263">138.91.141.162</span><span class="sxs-lookup"><span data-stu-id="9dc1f-263">138.91.141.162</span></span> | <span data-ttu-id="9dc1f-264">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-264">443</span></span> | <span data-ttu-id="9dc1f-265">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-265">Inbound</span></span> |

2. <span data-ttu-id="9dc1f-266">Se il cluster HDInsight si trova in una delle seguenti aree, è necessario consentire il traffico proveniente dagli indirizzi IP elencati per l'area:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-266">If your HDInsight cluster is in one of the following regions, then you must allow traffic from the IP addresses listed for the region:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9dc1f-267">Se si usa un'area di Azure non inclusa nell'elenco, usare solo i quattro IP riportati nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-267">If the Azure region you are using is not listed, then only use the four IP addresses from step 1.</span></span>

    | <span data-ttu-id="9dc1f-268">Paese</span><span class="sxs-lookup"><span data-stu-id="9dc1f-268">Country</span></span> | <span data-ttu-id="9dc1f-269">Region</span><span class="sxs-lookup"><span data-stu-id="9dc1f-269">Region</span></span> | <span data-ttu-id="9dc1f-270">Indirizzi IP consentiti</span><span class="sxs-lookup"><span data-stu-id="9dc1f-270">Allowed IP addresses</span></span> | <span data-ttu-id="9dc1f-271">Porta consentita</span><span class="sxs-lookup"><span data-stu-id="9dc1f-271">Allowed port</span></span> | <span data-ttu-id="9dc1f-272">Direzione</span><span class="sxs-lookup"><span data-stu-id="9dc1f-272">Direction</span></span> |
    | ---- | ---- | ---- | ---- | ----- |
    | <span data-ttu-id="9dc1f-273">Asia</span><span class="sxs-lookup"><span data-stu-id="9dc1f-273">Asia</span></span> | <span data-ttu-id="9dc1f-274">Asia orientale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-274">East Asia</span></span> | <span data-ttu-id="9dc1f-275">23.102.235.122</span><span class="sxs-lookup"><span data-stu-id="9dc1f-275">23.102.235.122</span></span></br><span data-ttu-id="9dc1f-276">52.175.38.134</span><span class="sxs-lookup"><span data-stu-id="9dc1f-276">52.175.38.134</span></span> | <span data-ttu-id="9dc1f-277">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-277">443</span></span> | <span data-ttu-id="9dc1f-278">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-278">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="9dc1f-279">Asia sudorientale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-279">Southeast Asia</span></span> | <span data-ttu-id="9dc1f-280">13.76.245.160</span><span class="sxs-lookup"><span data-stu-id="9dc1f-280">13.76.245.160</span></span></br><span data-ttu-id="9dc1f-281">13.76.136.249</span><span class="sxs-lookup"><span data-stu-id="9dc1f-281">13.76.136.249</span></span> | <span data-ttu-id="9dc1f-282">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-282">443</span></span> | <span data-ttu-id="9dc1f-283">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-283">Inbound</span></span> |
    | <span data-ttu-id="9dc1f-284">Australia</span><span class="sxs-lookup"><span data-stu-id="9dc1f-284">Australia</span></span> | <span data-ttu-id="9dc1f-285">Australia orientale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-285">Australia East</span></span> | <span data-ttu-id="9dc1f-286">104.210.84.115</span><span class="sxs-lookup"><span data-stu-id="9dc1f-286">104.210.84.115</span></span></br><span data-ttu-id="9dc1f-287">13.75.152.195</span><span class="sxs-lookup"><span data-stu-id="9dc1f-287">13.75.152.195</span></span> | <span data-ttu-id="9dc1f-288">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-288">443</span></span> | <span data-ttu-id="9dc1f-289">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-289">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="9dc1f-290">Australia sudorientale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-290">Australia Southeast</span></span> | <span data-ttu-id="9dc1f-291">13.77.2.56</span><span class="sxs-lookup"><span data-stu-id="9dc1f-291">13.77.2.56</span></span></br><span data-ttu-id="9dc1f-292">13.77.2.94</span><span class="sxs-lookup"><span data-stu-id="9dc1f-292">13.77.2.94</span></span> | <span data-ttu-id="9dc1f-293">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-293">443</span></span> | <span data-ttu-id="9dc1f-294">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-294">Inbound</span></span> |
    | <span data-ttu-id="9dc1f-295">Brasile</span><span class="sxs-lookup"><span data-stu-id="9dc1f-295">Brazil</span></span> | <span data-ttu-id="9dc1f-296">Brasile meridionale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-296">Brazil South</span></span> | <span data-ttu-id="9dc1f-297">191.235.84.104</span><span class="sxs-lookup"><span data-stu-id="9dc1f-297">191.235.84.104</span></span></br><span data-ttu-id="9dc1f-298">191.235.87.113</span><span class="sxs-lookup"><span data-stu-id="9dc1f-298">191.235.87.113</span></span> | <span data-ttu-id="9dc1f-299">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-299">443</span></span> | <span data-ttu-id="9dc1f-300">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-300">Inbound</span></span> |
    | <span data-ttu-id="9dc1f-301">Canada</span><span class="sxs-lookup"><span data-stu-id="9dc1f-301">Canada</span></span> | <span data-ttu-id="9dc1f-302">Canada orientale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-302">Canada East</span></span> | <span data-ttu-id="9dc1f-303">52.229.127.96</span><span class="sxs-lookup"><span data-stu-id="9dc1f-303">52.229.127.96</span></span></br><span data-ttu-id="9dc1f-304">52.229.123.172</span><span class="sxs-lookup"><span data-stu-id="9dc1f-304">52.229.123.172</span></span> | <span data-ttu-id="9dc1f-305">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-305">443</span></span> | <span data-ttu-id="9dc1f-306">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-306">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="9dc1f-307">Canada centrale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-307">Canada Central</span></span> | <span data-ttu-id="9dc1f-308">52.228.37.66</span><span class="sxs-lookup"><span data-stu-id="9dc1f-308">52.228.37.66</span></span></br><span data-ttu-id="9dc1f-309">52.228.45.222</span><span class="sxs-lookup"><span data-stu-id="9dc1f-309">52.228.45.222</span></span> | <span data-ttu-id="9dc1f-310">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-310">443</span></span> | <span data-ttu-id="9dc1f-311">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-311">Inbound</span></span> |
    | <span data-ttu-id="9dc1f-312">Cina</span><span class="sxs-lookup"><span data-stu-id="9dc1f-312">China</span></span> | <span data-ttu-id="9dc1f-313">Cina settentrionale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-313">China North</span></span> | <span data-ttu-id="9dc1f-314">42.159.96.170</span><span class="sxs-lookup"><span data-stu-id="9dc1f-314">42.159.96.170</span></span></br><span data-ttu-id="9dc1f-315">139.217.2.219</span><span class="sxs-lookup"><span data-stu-id="9dc1f-315">139.217.2.219</span></span> | <span data-ttu-id="9dc1f-316">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-316">443</span></span> | <span data-ttu-id="9dc1f-317">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-317">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="9dc1f-318">Cina orientale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-318">China East</span></span> | <span data-ttu-id="9dc1f-319">42.159.198.178</span><span class="sxs-lookup"><span data-stu-id="9dc1f-319">42.159.198.178</span></span></br><span data-ttu-id="9dc1f-320">42.159.234.157</span><span class="sxs-lookup"><span data-stu-id="9dc1f-320">42.159.234.157</span></span> | <span data-ttu-id="9dc1f-321">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-321">443</span></span> | <span data-ttu-id="9dc1f-322">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-322">Inbound</span></span> |
    | <span data-ttu-id="9dc1f-323">Europa</span><span class="sxs-lookup"><span data-stu-id="9dc1f-323">Europe</span></span> | <span data-ttu-id="9dc1f-324">Europa settentrionale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-324">North Europe</span></span> | <span data-ttu-id="9dc1f-325">52.164.210.96</span><span class="sxs-lookup"><span data-stu-id="9dc1f-325">52.164.210.96</span></span></br><span data-ttu-id="9dc1f-326">13.74.153.132</span><span class="sxs-lookup"><span data-stu-id="9dc1f-326">13.74.153.132</span></span> | <span data-ttu-id="9dc1f-327">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-327">443</span></span> | <span data-ttu-id="9dc1f-328">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-328">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="9dc1f-329">Europa occidentale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-329">West Europe</span></span>| <span data-ttu-id="9dc1f-330">52.166.243.90</span><span class="sxs-lookup"><span data-stu-id="9dc1f-330">52.166.243.90</span></span></br><span data-ttu-id="9dc1f-331">52.174.36.244</span><span class="sxs-lookup"><span data-stu-id="9dc1f-331">52.174.36.244</span></span> | <span data-ttu-id="9dc1f-332">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-332">443</span></span> | <span data-ttu-id="9dc1f-333">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-333">Inbound</span></span> |
    | <span data-ttu-id="9dc1f-334">Germania</span><span class="sxs-lookup"><span data-stu-id="9dc1f-334">Germany</span></span> | <span data-ttu-id="9dc1f-335">Germania centrale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-335">Germany Central</span></span> | <span data-ttu-id="9dc1f-336">51.4.146.68</span><span class="sxs-lookup"><span data-stu-id="9dc1f-336">51.4.146.68</span></span></br><span data-ttu-id="9dc1f-337">51.4.146.80</span><span class="sxs-lookup"><span data-stu-id="9dc1f-337">51.4.146.80</span></span> | <span data-ttu-id="9dc1f-338">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-338">443</span></span> | <span data-ttu-id="9dc1f-339">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-339">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="9dc1f-340">Germania nord-orientale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-340">Germany Northeast</span></span> | <span data-ttu-id="9dc1f-341">51.5.150.132</span><span class="sxs-lookup"><span data-stu-id="9dc1f-341">51.5.150.132</span></span></br><span data-ttu-id="9dc1f-342">51.5.144.101</span><span class="sxs-lookup"><span data-stu-id="9dc1f-342">51.5.144.101</span></span> | <span data-ttu-id="9dc1f-343">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-343">443</span></span> | <span data-ttu-id="9dc1f-344">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-344">Inbound</span></span> |
    | <span data-ttu-id="9dc1f-345">India</span><span class="sxs-lookup"><span data-stu-id="9dc1f-345">India</span></span> | <span data-ttu-id="9dc1f-346">India centrale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-346">Central India</span></span> | <span data-ttu-id="9dc1f-347">52.172.153.209</span><span class="sxs-lookup"><span data-stu-id="9dc1f-347">52.172.153.209</span></span></br><span data-ttu-id="9dc1f-348">52.172.152.49</span><span class="sxs-lookup"><span data-stu-id="9dc1f-348">52.172.152.49</span></span> | <span data-ttu-id="9dc1f-349">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-349">443</span></span> | <span data-ttu-id="9dc1f-350">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-350">Inbound</span></span> |
    | <span data-ttu-id="9dc1f-351">Giappone</span><span class="sxs-lookup"><span data-stu-id="9dc1f-351">Japan</span></span> | <span data-ttu-id="9dc1f-352">Giappone orientale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-352">Japan East</span></span> | <span data-ttu-id="9dc1f-353">13.78.125.90</span><span class="sxs-lookup"><span data-stu-id="9dc1f-353">13.78.125.90</span></span></br><span data-ttu-id="9dc1f-354">13.78.89.60</span><span class="sxs-lookup"><span data-stu-id="9dc1f-354">13.78.89.60</span></span> | <span data-ttu-id="9dc1f-355">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-355">443</span></span> | <span data-ttu-id="9dc1f-356">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-356">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="9dc1f-357">Giappone occidentale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-357">Japan West</span></span> | <span data-ttu-id="9dc1f-358">40.74.125.69</span><span class="sxs-lookup"><span data-stu-id="9dc1f-358">40.74.125.69</span></span></br><span data-ttu-id="9dc1f-359">138.91.29.150</span><span class="sxs-lookup"><span data-stu-id="9dc1f-359">138.91.29.150</span></span> | <span data-ttu-id="9dc1f-360">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-360">443</span></span> | <span data-ttu-id="9dc1f-361">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-361">Inbound</span></span> |
    | <span data-ttu-id="9dc1f-362">Corea</span><span class="sxs-lookup"><span data-stu-id="9dc1f-362">Korea</span></span> | <span data-ttu-id="9dc1f-363">Corea centrale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-363">Korea Central</span></span> | <span data-ttu-id="9dc1f-364">52.231.39.142</span><span class="sxs-lookup"><span data-stu-id="9dc1f-364">52.231.39.142</span></span></br><span data-ttu-id="9dc1f-365">52.231.36.209</span><span class="sxs-lookup"><span data-stu-id="9dc1f-365">52.231.36.209</span></span> | <span data-ttu-id="9dc1f-366">433</span><span class="sxs-lookup"><span data-stu-id="9dc1f-366">433</span></span> | <span data-ttu-id="9dc1f-367">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-367">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="9dc1f-368">Corea meridionale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-368">Korea South</span></span> | <span data-ttu-id="9dc1f-369">52.231.203.16</span><span class="sxs-lookup"><span data-stu-id="9dc1f-369">52.231.203.16</span></span></br><span data-ttu-id="9dc1f-370">52.231.205.214</span><span class="sxs-lookup"><span data-stu-id="9dc1f-370">52.231.205.214</span></span> | <span data-ttu-id="9dc1f-371">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-371">443</span></span> | <span data-ttu-id="9dc1f-372">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-372">Inbound</span></span>
    | <span data-ttu-id="9dc1f-373">Regno Unito</span><span class="sxs-lookup"><span data-stu-id="9dc1f-373">United Kingdom</span></span> | <span data-ttu-id="9dc1f-374">Regno Unito occidentale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-374">UK West</span></span> | <span data-ttu-id="9dc1f-375">51.141.13.110</span><span class="sxs-lookup"><span data-stu-id="9dc1f-375">51.141.13.110</span></span></br><span data-ttu-id="9dc1f-376">51.141.7.20</span><span class="sxs-lookup"><span data-stu-id="9dc1f-376">51.141.7.20</span></span> | <span data-ttu-id="9dc1f-377">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-377">443</span></span> | <span data-ttu-id="9dc1f-378">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-378">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="9dc1f-379">Regno Unito meridionale</span><span class="sxs-lookup"><span data-stu-id="9dc1f-379">UK South</span></span> | <span data-ttu-id="9dc1f-380">51.140.47.39</span><span class="sxs-lookup"><span data-stu-id="9dc1f-380">51.140.47.39</span></span></br><span data-ttu-id="9dc1f-381">51.140.52.16</span><span class="sxs-lookup"><span data-stu-id="9dc1f-381">51.140.52.16</span></span> | <span data-ttu-id="9dc1f-382">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-382">443</span></span> | <span data-ttu-id="9dc1f-383">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-383">Inbound</span></span> |
    | <span data-ttu-id="9dc1f-384">Stati Uniti</span><span class="sxs-lookup"><span data-stu-id="9dc1f-384">United States</span></span> | <span data-ttu-id="9dc1f-385">Stati Uniti centrali</span><span class="sxs-lookup"><span data-stu-id="9dc1f-385">Central US</span></span> | <span data-ttu-id="9dc1f-386">13.67.223.215</span><span class="sxs-lookup"><span data-stu-id="9dc1f-386">13.67.223.215</span></span></br><span data-ttu-id="9dc1f-387">40.86.83.253</span><span class="sxs-lookup"><span data-stu-id="9dc1f-387">40.86.83.253</span></span> | <span data-ttu-id="9dc1f-388">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-388">443</span></span> | <span data-ttu-id="9dc1f-389">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-389">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="9dc1f-390">Stati Uniti centro-settentrionali</span><span class="sxs-lookup"><span data-stu-id="9dc1f-390">North Central US</span></span> | <span data-ttu-id="9dc1f-391">157.56.8.38</span><span class="sxs-lookup"><span data-stu-id="9dc1f-391">157.56.8.38</span></span></br><span data-ttu-id="9dc1f-392">157.55.213.99</span><span class="sxs-lookup"><span data-stu-id="9dc1f-392">157.55.213.99</span></span> | <span data-ttu-id="9dc1f-393">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-393">443</span></span> | <span data-ttu-id="9dc1f-394">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-394">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="9dc1f-395">Stati Uniti centro-occidentali</span><span class="sxs-lookup"><span data-stu-id="9dc1f-395">West Central US</span></span> | <span data-ttu-id="9dc1f-396">52.161.23.15</span><span class="sxs-lookup"><span data-stu-id="9dc1f-396">52.161.23.15</span></span></br><span data-ttu-id="9dc1f-397">52.161.10.167</span><span class="sxs-lookup"><span data-stu-id="9dc1f-397">52.161.10.167</span></span> | <span data-ttu-id="9dc1f-398">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-398">443</span></span> | <span data-ttu-id="9dc1f-399">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-399">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="9dc1f-400">Stati Uniti occidentali 2</span><span class="sxs-lookup"><span data-stu-id="9dc1f-400">West US 2</span></span> | <span data-ttu-id="9dc1f-401">52.175.211.210</span><span class="sxs-lookup"><span data-stu-id="9dc1f-401">52.175.211.210</span></span></br><span data-ttu-id="9dc1f-402">52.175.222.222</span><span class="sxs-lookup"><span data-stu-id="9dc1f-402">52.175.222.222</span></span> | <span data-ttu-id="9dc1f-403">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-403">443</span></span> | <span data-ttu-id="9dc1f-404">In ingresso</span><span class="sxs-lookup"><span data-stu-id="9dc1f-404">Inbound</span></span> |

    <span data-ttu-id="9dc1f-405">Per informazioni sugli indirizzi IP da usare per Azure per enti pubblici, vedere il documento [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) (Intelligence e Analisi di Azure per enti pubblici).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-405">For information on the IP addresses to use for Azure Government, see the [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span></span>

3. <span data-ttu-id="9dc1f-406">Se si usa un server DNS personalizzato con la rete virtuale, è anche necessario consentire l'accesso da __168.63.129.16__.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-406">If you use a custom DNS server with your virtual network, you must also allow access from __168.63.129.16__.</span></span> <span data-ttu-id="9dc1f-407">Questo è l'indirizzo del sistema di risoluzione ricorsiva di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-407">This address is Azure's recursive resolver.</span></span> <span data-ttu-id="9dc1f-408">Per altre informazioni, vedere il documento [Risoluzione dei nomi per macchine virtuali e istanze del ruolo](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-408">For more information, see the [Name resolution for VMs and Role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span></span>

<span data-ttu-id="9dc1f-409">Per altre informazioni, vedere la sezione [Controllo del traffico di rete](#networktraffic).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-409">For more information, see the [Controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="9dc1f-410"><a id="hdinsight-ports"></a> Porte richieste</span><span class="sxs-lookup"><span data-stu-id="9dc1f-410"><a id="hdinsight-ports"></a> Required ports</span></span>

<span data-ttu-id="9dc1f-411">Se si intende usare un **firewall di appliance virtuale** di rete per proteggere la rete virtuale, è necessario abilitare il traffico in uscita sulle porte seguenti:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-411">If you plan on using a network **virtual appliance firewall** to secure the virtual network, you must allow outbound traffic on the following ports:</span></span>

* <span data-ttu-id="9dc1f-412">53</span><span class="sxs-lookup"><span data-stu-id="9dc1f-412">53</span></span>
* <span data-ttu-id="9dc1f-413">443</span><span class="sxs-lookup"><span data-stu-id="9dc1f-413">443</span></span>
* <span data-ttu-id="9dc1f-414">1433</span><span class="sxs-lookup"><span data-stu-id="9dc1f-414">1433</span></span>
* <span data-ttu-id="9dc1f-415">11000-11999</span><span class="sxs-lookup"><span data-stu-id="9dc1f-415">11000-11999</span></span>
* <span data-ttu-id="9dc1f-416">14000-14999</span><span class="sxs-lookup"><span data-stu-id="9dc1f-416">14000-14999</span></span>

<span data-ttu-id="9dc1f-417">Per un elenco di porte per servizi specifici, vedere il documento [Porte usate dai servizi Hadoop su HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-417">For a list of ports for specific services, see the [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

<span data-ttu-id="9dc1f-418">Per altre informazioni sulle regole del firewall per le appliance virtuali, vedere il documento [Scenario dell'appliance virtuale](../virtual-network/virtual-network-scenario-udr-gw-nva.md).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-418">For more information on firewall rules for virtual appliances, see the [virtual appliance scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span></span>

## <span data-ttu-id="9dc1f-419"><a id="hdinsight-nsg"></a>Ad esempio: gruppi di sicurezza di rete con HDInsight</span><span class="sxs-lookup"><span data-stu-id="9dc1f-419"><a id="hdinsight-nsg"></a>Example: network security groups with HDInsight</span></span>

<span data-ttu-id="9dc1f-420">Gli esempi in questa sezione illustrano come creare regole per i gruppi di sicurezza di rete che consentano a HDInsight di comunicare con i servizi di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-420">The examples in this section demonstrate how to create network security group rules that allow HDInsight to communicate with the Azure management services.</span></span> <span data-ttu-id="9dc1f-421">Prima di usare gli esempi, modificare gli indirizzi IP in modo che corrispondano a quelli per l'area di Azure in uso.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-421">Before using the examples, adjust the IP addresses to match the ones for the Azure region you are using.</span></span> <span data-ttu-id="9dc1f-422">Queste informazioni sono disponibili nella sezione [HDInsight con gruppi di sicurezza di rete e route definite dall'utente](#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-422">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-resource-management-template"></a><span data-ttu-id="9dc1f-423">Modello di Resource Manager di Azure</span><span class="sxs-lookup"><span data-stu-id="9dc1f-423">Azure Resource Management template</span></span>

<span data-ttu-id="9dc1f-424">Il modello di Resource Manager seguente crea una rete virtuale che limita il traffico in ingresso, ma consente il traffico dagli indirizzi IP richiesti da HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-424">The following Resource Management template creates a virtual network that restricts inbound traffic, but allows traffic from the IP addresses required by HDInsight.</span></span> <span data-ttu-id="9dc1f-425">Questo modello crea anche un cluster HDInsight nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-425">This template also creates an HDInsight cluster in the virtual network.</span></span>

* <span data-ttu-id="9dc1f-426">[Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/) (Distribuire una rete virtuale di Azure protetta e un cluster Hadoop HDInsight)</span><span class="sxs-lookup"><span data-stu-id="9dc1f-426">[Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9dc1f-427">Modificare gli indirizzi IP usati in questo esempio in modo che corrispondano all'area di Azure in uso.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-427">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="9dc1f-428">Queste informazioni sono disponibili nella sezione [HDInsight con gruppi di sicurezza di rete e route definite dall'utente](#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-428">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="9dc1f-429">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9dc1f-429">Azure PowerShell</span></span>

<span data-ttu-id="9dc1f-430">Usare lo script di PowerShell seguente per creare una rete virtuale che limita il traffico in ingresso e consente il traffico dagli indirizzi IP per l'area Europa settentrionale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-430">Use the following PowerShell script to create a virtual network that restricts inbound traffic and allows traffic from the IP addresses for the North Europe region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9dc1f-431">Modificare gli indirizzi IP usati in questo esempio in modo che corrispondano all'area di Azure in uso.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-431">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="9dc1f-432">Queste informazioni sono disponibili nella sezione [HDInsight con gruppi di sicurezza di rete e route definite dall'utente](#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-432">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with the resource group the virtual network is in"
$subnetName = "Replace with the name of the subnet that you plan to use for HDInsight"
# Get the Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get the region the Virtual network is in.
$location = $vnet.Location
# Get the subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for the HDInsight health and management services.
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
# Set the changes to the security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply the NSG to the subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> <span data-ttu-id="9dc1f-433">Questo esempio illustra come aggiungere le regole per consentire il traffico in ingresso sugli indirizzi IP richiesti.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-433">This example demonstrates how to add rules to allow inbound traffic on the required IP addresses.</span></span> <span data-ttu-id="9dc1f-434">Non contiene regole per limitare l'accesso in ingresso da altre origini.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-434">It does not contain a rule to restrict inbound access from other sources.</span></span>
>
> <span data-ttu-id="9dc1f-435">L'esempio seguente dimostra come abilitare l'accesso SSH da Internet:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-435">The following example demonstrates how to enable SSH access from the Internet:</span></span>
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a><span data-ttu-id="9dc1f-436">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="9dc1f-436">Azure CLI</span></span>

<span data-ttu-id="9dc1f-437">Seguire questa procedura per creare una rete virtuale che limita il traffico in ingresso, ma consente il traffico dagli indirizzi IP richiesti da HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-437">Use the following steps to create a virtual network that restricts inbound traffic, but allows traffic from the IP addresses required by HDInsight.</span></span>

1. <span data-ttu-id="9dc1f-438">Usare il comando seguente per creare un nuovo gruppo di sicurezza di rete denominato `hdisecure`.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-438">Use the following command to create a new network security group named `hdisecure`.</span></span> <span data-ttu-id="9dc1f-439">Sostituire **RESOURCEGROUPNAME** con il gruppo di risorse che contiene la rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-439">Replace **RESOURCEGROUPNAME** with the resource group that contains the Azure Virtual Network.</span></span> <span data-ttu-id="9dc1f-440">Sostituire **LOCATION** con la posizione (area geografica) in cui è stato creato il gruppo.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-440">Replace **LOCATION** with the location (region) that the group was created in.</span></span>

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    <span data-ttu-id="9dc1f-441">Dopo aver creato il gruppo si ricevono informazioni sul nuovo gruppo.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-441">Once the group has been created, you receive information on the new group.</span></span>

2. <span data-ttu-id="9dc1f-442">Usare le informazioni seguenti per aggiungere regole al nuovo gruppo di sicurezza di rete che ammettono la comunicazione in ingresso sulla porta 443 dal servizio integrità e gestione di Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-442">Use the following to add rules to the new network security group that allow inbound communication on port 443 from the Azure HDInsight health and management service.</span></span> <span data-ttu-id="9dc1f-443">Sostituire **RESOURCEGROUPNAME** con il nome del gruppo di risorse che contiene la rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-443">Replace **RESOURCEGROUPNAME** with the name of the resource group that contains the Azure Virtual Network.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9dc1f-444">Modificare gli indirizzi IP usati in questo esempio in modo che corrispondano all'area di Azure in uso.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-444">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="9dc1f-445">Queste informazioni sono disponibili nella sezione [HDInsight con gruppi di sicurezza di rete e route definite dall'utente](#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-445">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. <span data-ttu-id="9dc1f-446">Per recuperare l'identificatore univoco per questo gruppo di sicurezza di rete, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-446">To retrieve the unique identifier for this network security group, use the following command:</span></span>

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    <span data-ttu-id="9dc1f-447">Il comando restituisce un valore simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-447">This command returns a value similar to the following text:</span></span>

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    <span data-ttu-id="9dc1f-448">Se non si ottengono i risultati previsti, nel comando inserire l'ID tra virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-448">Use double-quotes around id in the command if you don't get the expected results.</span></span>

4. <span data-ttu-id="9dc1f-449">Usare il comando seguente per applicare il gruppo di sicurezza di rete a una subnet.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-449">Use the following command to apply the network security group to a subnet.</span></span> <span data-ttu-id="9dc1f-450">Sostituire i valori __GUID__ e __RESOURCEGROUPNAME__ con quelli restituiti nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-450">Replace the __GUID__ and __RESOURCEGROUPNAME__ values with the ones returned from the previous step.</span></span> <span data-ttu-id="9dc1f-451">Sostituire __VNETNAME__ e __SUBNETNAME__ con il nome della rete virtuale e il nome della subnet che si intende creare.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-451">Replace __VNETNAME__ and __SUBNETNAME__ with the virtual network name and subnet name that you want to create.</span></span>

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    <span data-ttu-id="9dc1f-452">Dopo il completamento del comando, è possibile installare HDInsight nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-452">Once this command completes, you can install HDInsight into the Virtual Network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9dc1f-453">Questa procedura consente di accedere solo al servizio di gestione e integrità di HDInsight nel cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-453">These steps only open access to the HDInsight health and management service on the Azure cloud.</span></span> <span data-ttu-id="9dc1f-454">Qualsiasi altro accesso al cluster HDInsight dall'esterno della rete virtuale è bloccato.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-454">Any other access to the HDInsight cluster from outside the Virtual Network is blocked.</span></span> <span data-ttu-id="9dc1f-455">Per abilitare l'accesso dall'esterno della rete virtuale è necessario aggiungere altre regole del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-455">To enable access from outside the virtual network, you must add additional Network Security Group rules.</span></span>
>
> <span data-ttu-id="9dc1f-456">L'esempio seguente dimostra come abilitare l'accesso SSH da Internet:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-456">The following example demonstrates how to enable SSH access from the Internet:</span></span>
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <span data-ttu-id="9dc1f-457"><a id="example-dns"></a> Esempio: configurazione DNS</span><span class="sxs-lookup"><span data-stu-id="9dc1f-457"><a id="example-dns"></a> Example: DNS configuration</span></span>

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a><span data-ttu-id="9dc1f-458">Risoluzione dei nomi tra una rete virtuale e una rete locale connessa</span><span class="sxs-lookup"><span data-stu-id="9dc1f-458">Name resolution between a virtual network and a connected on-premises network</span></span>

<span data-ttu-id="9dc1f-459">Questo esempio si basa sui presupposti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-459">This example makes the following assumptions:</span></span>

* <span data-ttu-id="9dc1f-460">Si dispone di una rete virtuale di Azure che è connessa a una rete locale tramite un gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-460">You have an Azure Virtual Network that is connected to an on-premises network using a VPN gateway.</span></span>

* <span data-ttu-id="9dc1f-461">Il server DNS personalizzato nella rete virtuale esegue il sistema operativo Linux o Unix.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-461">The custom DNS server in the virtual network is running Linux or Unix as the operating system.</span></span>

* <span data-ttu-id="9dc1f-462">Nel server DNS personalizzato è installato [Bind](https://www.isc.org/downloads/bind/).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-462">[Bind](https://www.isc.org/downloads/bind/) is installed on the custom DNS server.</span></span>

<span data-ttu-id="9dc1f-463">Nel server DNS personalizzato nella rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-463">On the custom DNS server in the virtual network:</span></span>

1. <span data-ttu-id="9dc1f-464">Usare Azure PowerShell o l'interfaccia della riga di comando di Azure per individuare il suffisso DNS della rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-464">Use either Azure PowerShell or Azure CLI to find the DNS suffix of the virtual network:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="9dc1f-465">Nel server DNS personalizzato per la rete virtuale, usare il testo seguente come contenuto del file `/etc/bind/named.conf.local`:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-465">On the custom DNS server for the virtual network, use the following text as the contents of the `/etc/bind/named.conf.local` file:</span></span>

    ```
    // Forward requests for the virtual network suffix to Azure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    <span data-ttu-id="9dc1f-466">Sostituire il valore `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` con il suffisso DNS della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-466">Replace the `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with the DNS suffix of your virtual network.</span></span>

    <span data-ttu-id="9dc1f-467">Questa configurazione indirizza tutte le richieste DNS per il suffisso DNS della rete virtuale al sistema di risoluzione ricorsiva di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-467">This configuration routes all DNS requests for the DNS suffix of the virtual network to the Azure recursive resolver.</span></span>

2. <span data-ttu-id="9dc1f-468">Nel server DNS personalizzato per la rete virtuale, usare il testo seguente come contenuto del file `/etc/bind/named.conf.options`:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-468">On the custom DNS server for the virtual network, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients to accept requests from
    // TODO: Add the IP range of the joined network to this list
    acl goodclients {
        10.0.0.0/16; # IP address range of the virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent to the following
            forwarders {
                192.168.0.1; # Replace with the IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform to RFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="9dc1f-469">Sostituire il valore `10.0.0.0/16` con l'intervallo di indirizzi IP della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-469">Replace the `10.0.0.0/16` value with the IP address range of your virtual network.</span></span> <span data-ttu-id="9dc1f-470">Questa voce consente l'indirizzamento delle richieste di risoluzione dei nomi all'interno di questo intervallo.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-470">This entry allows name resolution requests addresses within this range.</span></span>

    * <span data-ttu-id="9dc1f-471">Aggiungere l'intervallo di indirizzi IP della rete locale alla sezione `acl goodclients { ... }`.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-471">Add the IP address range of the on-premises network to the `acl goodclients { ... }` section.</span></span>  <span data-ttu-id="9dc1f-472">Questa voce consente le richieste di risoluzione dei nomi dalle risorse nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-472">entry allows name resolution requests from resources in the on-premises network.</span></span>
    
    * <span data-ttu-id="9dc1f-473">Sostituire il valore `192.168.0.1` con l'indirizzo IP del server DNS locale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-473">Replace the value `192.168.0.1` with the IP address of your on-premises DNS server.</span></span> <span data-ttu-id="9dc1f-474">Questa voce indirizza tutte le altre richieste DNS al server DNS locale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-474">This entry routes all other DNS requests to the on-premises DNS server.</span></span>

3. <span data-ttu-id="9dc1f-475">Per usare la configurazione, riavviare Bind.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-475">To use the configuration, restart Bind.</span></span> <span data-ttu-id="9dc1f-476">Ad esempio, `sudo service bind9 restart`.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-476">For example, `sudo service bind9 restart`.</span></span>

4. <span data-ttu-id="9dc1f-477">Aggiungere un server d'inoltro condizionale al server DNS locale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-477">Add a conditional forwarder to the on-premises DNS server.</span></span> <span data-ttu-id="9dc1f-478">Configurare il server d'inoltro condizionale per l'invio di richieste del suffisso DNS del passaggio 1 al server DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-478">Configure the conditional forwarder to send requests for the DNS suffix from step 1 to the custom DNS server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9dc1f-479">Per informazioni dettagliate su come aggiungere un server d'inoltro condizionale, consultare la documentazione del software del DNS.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-479">Consult the documentation for your DNS software for specifics on how to add a conditional forwarder.</span></span>

<span data-ttu-id="9dc1f-480">Dopo avere completato questi passaggi, è possibile connettersi alle risorse in entrambe le reti usando i nomi di dominio completi (FQDN).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-480">After completing these steps, you can connect to resources in either network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="9dc1f-481">È ora possibile installare HDInsight nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-481">You can now install HDInsight into the virtual network.</span></span>

### <a name="name-resolution-between-two-connected-virtual-networks"></a><span data-ttu-id="9dc1f-482">Risoluzione dei nomi tra due reti virtuali connesse</span><span class="sxs-lookup"><span data-stu-id="9dc1f-482">Name resolution between two connected virtual networks</span></span>

<span data-ttu-id="9dc1f-483">Questo esempio si basa sui presupposti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-483">This example makes the following assumptions:</span></span>

* <span data-ttu-id="9dc1f-484">Si dispone di due reti virtuali di Azure connesse tramite gateway VPN o peering.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-484">You have two Azure Virtual Networks that are connected using either a VPN gateway or peering.</span></span>

* <span data-ttu-id="9dc1f-485">Il server DNS personalizzato in entrambe le reti esegue il sistema operativo Linux o Unix.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-485">The custom DNS server in both networks is running Linux or Unix as the operating system.</span></span>

* <span data-ttu-id="9dc1f-486">Nei server DNS personalizzati è installato [Bind](https://www.isc.org/downloads/bind/).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-486">[Bind](https://www.isc.org/downloads/bind/) is installed on the custom DNS servers.</span></span>

1. <span data-ttu-id="9dc1f-487">Usare Azure PowerShell o l'interfaccia della riga di comando di Azure per individuare il suffisso DNS di entrambe le reti virtuali:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-487">Use either Azure PowerShell or Azure CLI to find the DNS suffix of both virtual networks:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="9dc1f-488">Usare il testo seguente come contenuto del file `/etc/bind/named.config.local` nel server DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-488">Use the following text as the contents of the `/etc/bind/named.config.local` file on the custom DNS server.</span></span> <span data-ttu-id="9dc1f-489">Apportare questa modifica al server DNS personalizzato in entrambe le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-489">Make this change on the custom DNS server in both virtual networks.</span></span>

    ```
    // Forward requests for the virtual network suffix to Azure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # The IP address of the DNS server in the other virtual network
    };
    ```

    <span data-ttu-id="9dc1f-490">Sostituire il valore `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` con il suffisso DNS dell'__altra__ rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-490">Replace the `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with the DNS suffix of the __other__ virtual network.</span></span> <span data-ttu-id="9dc1f-491">Questa voce indirizza le richieste per il suffisso DNS della rete remota al DNS personalizzato di quella rete.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-491">This entry routes requests for the DNS suffix of the remote network to the custom DNS in that network.</span></span>

3. <span data-ttu-id="9dc1f-492">Nei server DNS personalizzati in entrambe le reti virtuali, usare il testo seguente come contenuto del file `/etc/bind/named.conf.options`:</span><span class="sxs-lookup"><span data-stu-id="9dc1f-492">On the custom DNS servers in both virtual networks, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients to accept requests from
    acl goodclients {
        10.1.0.0/16; # The IP address range of one virtual network
        10.0.0.0/16; # The IP address range of the other virtual network
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

            auth-nxdomain no;    # conform to RFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="9dc1f-493">Sostituire i valori `10.0.0.0/16` e `10.1.0.0/16` all'interno degli intervalli di indirizzi IP delle reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-493">Replace the `10.0.0.0/16` and `10.1.0.0/16` values with the IP address ranges of your virtual networks.</span></span> <span data-ttu-id="9dc1f-494">Questa voce consente alle risorse in ogni rete di eseguire richieste dei server DNS.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-494">This entry allows resources in each network to make requests of the DNS servers.</span></span>

    <span data-ttu-id="9dc1f-495">Tutte le richieste che non riguardano i suffissi DNS delle reti virtuali (ad esempio microsoft.com) vengono gestite dal sistema di risoluzione ricorsiva di Azure.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-495">Any requests that are not for the DNS suffixes of the virtual networks (for example, microsoft.com) is handled by the Azure recursive resolver.</span></span>

4. <span data-ttu-id="9dc1f-496">Per usare la configurazione, riavviare Bind.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-496">To use the configuration, restart Bind.</span></span> <span data-ttu-id="9dc1f-497">Ad esempio `sudo service bind9 restart` su entrambi i server DNS.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-497">For example, `sudo service bind9 restart` on both DNS servers.</span></span>

<span data-ttu-id="9dc1f-498">Dopo avere completato questi passaggi, è possibile connettersi alle risorse nella rete virtuale usando i nomi di dominio completi (FQDN).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-498">After completing these steps, you can connect to resources in the virtual network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="9dc1f-499">È ora possibile installare HDInsight nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9dc1f-499">You can now install HDInsight into the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9dc1f-500">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9dc1f-500">Next steps</span></span>

* <span data-ttu-id="9dc1f-501">Per un esempio completo di configurazione di HDInsight per la connessione a una rete locale, vedere [Connettere HDInsight alla rete locale](./connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-501">For an end-to-end example of configuring HDInsight to connect to an on-premises network, see [Connect HDInsight to an on-premises network](./connect-on-premises-network.md).</span></span>

* <span data-ttu-id="9dc1f-502">Per altre informazioni sulle reti virtuali di Azure, vedere la [panoramica sulle reti virtuali di Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-502">For more information on Azure virtual networks, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="9dc1f-503">Per altre informazioni sui gruppi di sicurezza di rete, vedere [Gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-503">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="9dc1f-504">Per altre informazioni sulle route definite dall'utente, vedere [Route definite dall'utente e inoltro IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9dc1f-504">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>