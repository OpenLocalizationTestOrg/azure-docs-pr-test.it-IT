---
title: un computer autonomo aaaCreate cluster con macchine virtuali di Azure che eseguono Windows | Documenti Microsoft
description: Informazioni su come toocreate e gestire un cluster di Azure Service Fabric in macchine virtuali di Azure che esegue Windows Server.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: ryanwi;chackdan
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: 8900204fe69887a7a0ca54b06e0d32534421bcfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a><span data-ttu-id="a6893-103">Creare un cluster di Service Fabric autonomo a tre nodi con macchine virtuali di Azure che eseguono Windows Server</span><span class="sxs-lookup"><span data-stu-id="a6893-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server</span></span>
<span data-ttu-id="a6893-104">In questo articolo viene descritto come toocreate un cluster basato su Windows Azure macchine virtuali (VM), utilizzando hello programma di installazione autonomo Service Fabric per Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a6893-104">This article describes how toocreate a cluster on Windows-based Azure virtual machines (VMs), using hello standalone Service Fabric installer for Windows Server.</span></span> <span data-ttu-id="a6893-105">scenario Hello è un caso speciale di [creare e gestire un cluster che esegue Windows Server](service-fabric-cluster-creation-for-windows-server.md) in cui le macchine virtuali hello sono [macchine virtuali di Azure che esegue Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), anche se non si sta creando [un Azure cluster basato su cloud di Service Fabric](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a6893-105">hello scenario is a special case of [Create and manage a cluster running on Windows Server](service-fabric-cluster-creation-for-windows-server.md) where hello VMs are [Azure VMs running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), however you are not creating [an Azure cloud-based Service Fabric cluster](service-fabric-cluster-creation-via-portal.md).</span></span> <span data-ttu-id="a6893-106">distinzione di Hello nei seguenti di questo modello è tale cluster di Service Fabric autonomo hello creati hello alla procedura seguente viene gestito interamente dall'utente, mentre hello Azure basato su cloud Service Fabric cluster gestiti e aggiornata da hello Service Fabric provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="a6893-106">hello distinction in following this pattern is that hello standalone Service Fabric cluster created by hello following steps is entirely managed by you, whereas hello Azure cloud-based Service Fabric clusters are managed and upgraded by hello Service Fabric resource provider.</span></span>

## <a name="steps-toocreate-hello-standalone-cluster"></a><span data-ttu-id="a6893-107">Cluster di passaggi toocreate hello autonomo</span><span class="sxs-lookup"><span data-stu-id="a6893-107">Steps toocreate hello standalone cluster</span></span>
1. <span data-ttu-id="a6893-108">Accedi toohello portale di Azure e creare un nuovo Windows Server 2012 R2 Datacenter o macchina virtuale di Windows Server 2016 Data Center in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a6893-108">Sign in toohello Azure portal and create a new Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM in a resource group.</span></span> <span data-ttu-id="a6893-109">Leggere l'articolo hello [creare una macchina virtuale di Windows nel portale di Azure hello](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="a6893-109">Read hello article [Create a Windows VM in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more details.</span></span>
2. <span data-ttu-id="a6893-110">Aggiungere due ulteriori toohello di macchine virtuali nello stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a6893-110">Add a couple more VMs toohello same resource group.</span></span> <span data-ttu-id="a6893-111">Verificare che ciascuna delle macchine virtuali hello è hello stesso nome utente dell'amministratore e una password quando viene creato.</span><span class="sxs-lookup"><span data-stu-id="a6893-111">Ensure that each of hello VMs has hello same administrator user name and password when created.</span></span> <span data-ttu-id="a6893-112">Dopo la creazione, si noterà che tutte le tre macchine virtuali in hello stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="a6893-112">Once created you should see all three VMs in hello same virtual network.</span></span>
3. <span data-ttu-id="a6893-113">Connettersi tooeach di hello macchine virtuali e disattivare hello Windows Firewall utilizzando hello [Server Manager, il dashboard di Server locale](https://technet.microsoft.com/library/jj134147.aspx).</span><span class="sxs-lookup"><span data-stu-id="a6893-113">Connect tooeach of hello VMs and turn off hello Windows Firewall using hello [Server Manager, Local Server dashboard](https://technet.microsoft.com/library/jj134147.aspx).</span></span> <span data-ttu-id="a6893-114">In questo modo si garantisce che il traffico di rete hello può comunicare tra le macchine hello.</span><span class="sxs-lookup"><span data-stu-id="a6893-114">This ensures that hello network traffic can communicate between hello machines.</span></span> <span data-ttu-id="a6893-115">Durante la macchina tooeach connesso, ottenere l'indirizzo IP hello aprendo un prompt dei comandi e digitando `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="a6893-115">While connected tooeach machine, get hello IP address by opening a command prompt and typing `ipconfig`.</span></span> <span data-ttu-id="a6893-116">In alternativa è possibile visualizzare hello IP indirizzo di ogni computer nel portale di hello, selezionando hello risorsa di rete virtuale per il gruppo di risorse hello e controllando le interfacce di rete hello create per ognuno di questi computer.</span><span class="sxs-lookup"><span data-stu-id="a6893-116">Alternatively you can see hello IP address of each machine on hello portal, by selecting hello virtual network resource for hello resource group and checking hello network interfaces created for each of these machines.</span></span>
4. <span data-ttu-id="a6893-117">Connettersi tooone di hello macchine virtuali e i test che è possibile effettuare il ping hello altri due macchine virtuali correttamente.</span><span class="sxs-lookup"><span data-stu-id="a6893-117">Connect tooone of hello VMs and test that you can ping hello other two VMs successfully.</span></span>
5. <span data-ttu-id="a6893-118">Connettersi tooone di hello macchine virtuali e [download del pacchetto di Service Fabric di hello autonomo per Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) in una nuova cartella hello computer ed estrarre il pacchetto di hello.</span><span class="sxs-lookup"><span data-stu-id="a6893-118">Connect tooone of hello VMs and [download hello standalone Service Fabric package for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) into a new folder on hello machine and extract hello package.</span></span>
6. <span data-ttu-id="a6893-119">Aprire hello *ClusterConfig.Unsecure.MultiMachine.json* file nel blocco note e modificare ogni nodo con gli indirizzi IP hello tre macchine hello.</span><span class="sxs-lookup"><span data-stu-id="a6893-119">Open hello *ClusterConfig.Unsecure.MultiMachine.json* file in Notepad and edit each node with hello three IP addresses of hello machines.</span></span> <span data-ttu-id="a6893-120">Modificare il nome del cluster hello nella parte superiore di hello e salvare file hello.</span><span class="sxs-lookup"><span data-stu-id="a6893-120">Change hello cluster name at hello top and save hello file.</span></span>  <span data-ttu-id="a6893-121">Un esempio parziale hello del manifesto del cluster è illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="a6893-121">A partial example of hello cluster manifest is shown below.</span></span>
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. <span data-ttu-id="a6893-122">Se si prevede un cluster protetto questo toobe, decidere di misura di sicurezza hello desideri toouse e seguire i passaggi di hello in hello associata collegamento: [certificato X509](service-fabric-windows-cluster-x509-security.md) o [la sicurezza di Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="a6893-122">If you intend this toobe a secure cluster, decide hello security measure you would like toouse and follow hello steps at hello associated link: [X509 Certificate](service-fabric-windows-cluster-x509-security.md) or [Windows Security](service-fabric-windows-cluster-windows-security.md).</span></span> <span data-ttu-id="a6893-123">Se si imposta la sicurezza di Windows del cluster di hello, occorre tooset backup un toomanage di controller di dominio Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a6893-123">If setting up hello cluster using Windows Security, you will need tooset up a domain controller toomanage Active Directory.</span></span> <span data-ttu-id="a6893-124">Si noti che l'uso di un computer controller di dominio come nodo di Service Fabric non è supportato.</span><span class="sxs-lookup"><span data-stu-id="a6893-124">Note that using a domain controller machine as a Service Fabric node is not supported.</span></span>
8. <span data-ttu-id="a6893-125">Aprire una [finestra di PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span><span class="sxs-lookup"><span data-stu-id="a6893-125">Open a [PowerShell ISE window](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span> <span data-ttu-id="a6893-126">Passare toohello cartella in cui si estratti pacchetto di installazione autonomo scaricato hello e salvata i file di configurazione del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a6893-126">Navigate toohello folder where you extracted hello downloaded standalone installer package and saved hello cluster configuration file.</span></span> <span data-ttu-id="a6893-127">Eseguire hello cluster hello toodeploy comando di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="a6893-127">Run hello following PowerShell command toodeploy hello cluster:</span></span>
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

<span data-ttu-id="a6893-128">script di Hello configurerà in modalità remota i cluster di Service Fabric hello e devono segnalare lo stato di avanzamento come distribuzione transita in.</span><span class="sxs-lookup"><span data-stu-id="a6893-128">hello script will remotely configure hello Service Fabric cluster and should report progress as deployment rolls through.</span></span>

9. <span data-ttu-id="a6893-129">Dopo circa un minuto, è possibile verificare se il cluster hello è operativo connettendosi toohello Service Fabric Explorer utilizzando uno degli IP della macchina hello indirizzi, ad esempio tramite `http://10.1.0.5:19080/Explorer/index.html`.</span><span class="sxs-lookup"><span data-stu-id="a6893-129">After about a minute, you can check if hello cluster is operational by connecting toohello Service Fabric Explorer using one of hello machine's IP addresses, for example by using `http://10.1.0.5:19080/Explorer/index.html`.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a6893-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a6893-130">Next steps</span></span>
* [<span data-ttu-id="a6893-131">Creare cluster autonomi di Service Fabric in Windows Server o Linux</span><span class="sxs-lookup"><span data-stu-id="a6893-131">Create standalone Service Fabric clusters on Windows Server or Linux</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="a6893-132">Aggiungere o rimuovere nodi tooa autonoma dell'infrastruttura del servizio cluster</span><span class="sxs-lookup"><span data-stu-id="a6893-132">Add or remove nodes tooa standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="a6893-133">Impostazioni di configurazione per un cluster autonomo in Windows</span><span class="sxs-lookup"><span data-stu-id="a6893-133">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="a6893-134">Proteggere un cluster autonomo in Windows tramite la funzionalità di sicurezza di Windows</span><span class="sxs-lookup"><span data-stu-id="a6893-134">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="a6893-135">Proteggere un cluster autonomo in Windows con certificati X.509</span><span class="sxs-lookup"><span data-stu-id="a6893-135">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

