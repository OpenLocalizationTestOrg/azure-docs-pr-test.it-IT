---
title: Creare un cluster autonomo con macchine virtuale di Azure che eseguono Windows| Microsoft Docs
description: Informazioni su come creare e gestire un cluster di Azure Service Fabric su macchine virtuali di Azure che eseguono Windows Server.
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
ms.openlocfilehash: f8a0305a22c00f9bdbdb1bdb06dc299cccee23dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a><span data-ttu-id="920e4-103">Creare un cluster di Service Fabric autonomo a tre nodi con macchine virtuali di Azure che eseguono Windows Server</span><span class="sxs-lookup"><span data-stu-id="920e4-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server</span></span>
<span data-ttu-id="920e4-104">Questo articolo descrive come creare un cluster su macchine virtuali (VM) di Windows Azure usando il programma di installazione di Service Fabric autonomo per Windows Server.</span><span class="sxs-lookup"><span data-stu-id="920e4-104">This article describes how to create a cluster on Windows-based Azure virtual machines (VMs), using the standalone Service Fabric installer for Windows Server.</span></span> <span data-ttu-id="920e4-105">Lo scenario è un caso speciale di [creazione e gestione di un cluster che esegue Windows Server](service-fabric-cluster-creation-for-windows-server.md) in cui le VM sono [VM di Azure che eseguono Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Non si crea tuttavia [un cluster di Azure Service Fabric basato su cloud](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="920e4-105">The scenario is a special case of [Create and manage a cluster running on Windows Server](service-fabric-cluster-creation-for-windows-server.md) where the VMs are [Azure VMs running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), however you are not creating [an Azure cloud-based Service Fabric cluster](service-fabric-cluster-creation-via-portal.md).</span></span> <span data-ttu-id="920e4-106">La differenza nel seguire questo schema è che il cluster di Service Fabric autonomo creato dai passaggi seguenti è interamente gestito dall'utente, mentre i cluster di Service Fabric di Azure basati su cloud vengono gestiti e aggiornati dal provider di risorse di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="920e4-106">The distinction in following this pattern is that the standalone Service Fabric cluster created by the following steps is entirely managed by you, whereas the Azure cloud-based Service Fabric clusters are managed and upgraded by the Service Fabric resource provider.</span></span>

## <a name="steps-to-create-the-standalone-cluster"></a><span data-ttu-id="920e4-107">Passaggi per creare il cluster autonomo</span><span class="sxs-lookup"><span data-stu-id="920e4-107">Steps to create the standalone cluster</span></span>
1. <span data-ttu-id="920e4-108">Accedere al portale di Azure e creare una nuova VM Windows Server 2012 R2 Datacenter o Windows Server 2016 Datacenter in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="920e4-108">Sign in to the Azure portal and create a new Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM in a resource group.</span></span> <span data-ttu-id="920e4-109">Per altre informazioni, leggere l'articolo [Creare una VM Windows nel portale di Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="920e4-109">Read the article [Create a Windows VM in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more details.</span></span>
2. <span data-ttu-id="920e4-110">Aggiungere altre due VM allo stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="920e4-110">Add a couple more VMs to the same resource group.</span></span> <span data-ttu-id="920e4-111">Assicurarsi che ogni VM abbia al momento della creazione lo stesso nome utente e la stessa password di amministratore.</span><span class="sxs-lookup"><span data-stu-id="920e4-111">Ensure that each of the VMs has the same administrator user name and password when created.</span></span> <span data-ttu-id="920e4-112">Al termine della creazione, tutte e tre le VM dovrebbero essere visualizzate nella stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="920e4-112">Once created you should see all three VMs in the same virtual network.</span></span>
3. <span data-ttu-id="920e4-113">Connettersi a ogni VM e disattivare Windows Firewall con il [dashboard Server locale di Server Manager](https://technet.microsoft.com/library/jj134147.aspx).</span><span class="sxs-lookup"><span data-stu-id="920e4-113">Connect to each of the VMs and turn off the Windows Firewall using the [Server Manager, Local Server dashboard](https://technet.microsoft.com/library/jj134147.aspx).</span></span> <span data-ttu-id="920e4-114">Ciò garantisce la comunicazione del traffico di rete tra le macchine.</span><span class="sxs-lookup"><span data-stu-id="920e4-114">This ensures that the network traffic can communicate between the machines.</span></span> <span data-ttu-id="920e4-115">Durante la connessione a ogni macchina, ottenere l'indirizzo IP aprendo un prompt dei comandi e digitando `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="920e4-115">While connected to each machine, get the IP address by opening a command prompt and typing `ipconfig`.</span></span> <span data-ttu-id="920e4-116">In alternativa è possibile visualizzare l'indirizzo IP di ogni computer nel portale, selezionando la risorsa di rete virtuale per il gruppo di risorse e verificando le interfacce di rete create per ogni computer.</span><span class="sxs-lookup"><span data-stu-id="920e4-116">Alternatively you can see the IP address of each machine on the portal, by selecting the virtual network resource for the resource group and checking the network interfaces created for each of these machines.</span></span>
4. <span data-ttu-id="920e4-117">Connettersi a una delle VM e verificare di poter effettuare correttamente il ping delle altre due.</span><span class="sxs-lookup"><span data-stu-id="920e4-117">Connect to one of the VMs and test that you can ping the other two VMs successfully.</span></span>
5. <span data-ttu-id="920e4-118">Connettersi a una delle VM, [scaricare il pacchetto Service Fabric autonomo per Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) in una nuova cartella nella macchina ed estrarre il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="920e4-118">Connect to one of the VMs and [download the standalone Service Fabric package for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) into a new folder on the machine and extract the package.</span></span>
6. <span data-ttu-id="920e4-119">Aprire il file *ClusterConfig.Unsecure.MultiMachine.json* nel Blocco note e quindi modificare ogni nodo con i tre indirizzi IP delle macchine.</span><span class="sxs-lookup"><span data-stu-id="920e4-119">Open the *ClusterConfig.Unsecure.MultiMachine.json* file in Notepad and edit each node with the three IP addresses of the machines.</span></span> <span data-ttu-id="920e4-120">Cambiare il nome del cluster nella parte superiore e salvare il file.</span><span class="sxs-lookup"><span data-stu-id="920e4-120">Change the cluster name at the top and save the file.</span></span>  <span data-ttu-id="920e4-121">Di seguito è riportato un esempio parziale del manifesto del cluster.</span><span class="sxs-lookup"><span data-stu-id="920e4-121">A partial example of the cluster manifest is shown below.</span></span>
   
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
7. <span data-ttu-id="920e4-122">Se si vuole che questo sia un cluster protetto, decidere la misura di sicurezza da usare e seguire i passaggi disponibili al collegamento associato: [certificato X509](service-fabric-windows-cluster-x509-security.md) o [protezione di Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="920e4-122">If you intend this to be a secure cluster, decide the security measure you would like to use and follow the steps at the associated link: [X509 Certificate](service-fabric-windows-cluster-x509-security.md) or [Windows Security](service-fabric-windows-cluster-windows-security.md).</span></span> <span data-ttu-id="920e4-123">Se si configura il cluster con la sicurezza di Windows, è necessario configurare un controller di dominio per gestire Active Directory.</span><span class="sxs-lookup"><span data-stu-id="920e4-123">If setting up the cluster using Windows Security, you will need to set up a domain controller to manage Active Directory.</span></span> <span data-ttu-id="920e4-124">Si noti che l'uso di un computer controller di dominio come nodo di Service Fabric non è supportato.</span><span class="sxs-lookup"><span data-stu-id="920e4-124">Note that using a domain controller machine as a Service Fabric node is not supported.</span></span>
8. <span data-ttu-id="920e4-125">Aprire una [finestra di PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span><span class="sxs-lookup"><span data-stu-id="920e4-125">Open a [PowerShell ISE window](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span> <span data-ttu-id="920e4-126">Passare alla cartella in cui è stato estratto il pacchetto di installazione autonomo scaricato e salvato il file di configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="920e4-126">Navigate to the folder where you extracted the downloaded standalone installer package and saved the cluster configuration file.</span></span> <span data-ttu-id="920e4-127">Eseguire il comando di PowerShell seguente per distribuire il cluster:</span><span class="sxs-lookup"><span data-stu-id="920e4-127">Run the following PowerShell command to deploy the cluster:</span></span>
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

<span data-ttu-id="920e4-128">Lo script configurerà in modalità remota il cluster Service Fabric e segnalerà lo stato di avanzamento durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="920e4-128">The script will remotely configure the Service Fabric cluster and should report progress as deployment rolls through.</span></span>

9. <span data-ttu-id="920e4-129">Dopo circa un minuto è possibile controllare che il cluster sia operativo connettendosi a Service Fabric Explorer mediante uno degli indirizzi IP delle macchine, ad esempio usando `http://10.1.0.5:19080/Explorer/index.html`.</span><span class="sxs-lookup"><span data-stu-id="920e4-129">After about a minute, you can check if the cluster is operational by connecting to the Service Fabric Explorer using one of the machine's IP addresses, for example by using `http://10.1.0.5:19080/Explorer/index.html`.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="920e4-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="920e4-130">Next steps</span></span>
* [<span data-ttu-id="920e4-131">Creare cluster autonomi di Service Fabric in Windows Server o Linux</span><span class="sxs-lookup"><span data-stu-id="920e4-131">Create standalone Service Fabric clusters on Windows Server or Linux</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="920e4-132">Aggiungere o rimuovere nodi in un cluster di Service Fabric autonomo</span><span class="sxs-lookup"><span data-stu-id="920e4-132">Add or remove nodes to a standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="920e4-133">Impostazioni di configurazione per un cluster autonomo in Windows</span><span class="sxs-lookup"><span data-stu-id="920e4-133">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="920e4-134">Proteggere un cluster autonomo in Windows tramite la funzionalità di sicurezza di Windows</span><span class="sxs-lookup"><span data-stu-id="920e4-134">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="920e4-135">Proteggere un cluster autonomo in Windows con certificati X.509</span><span class="sxs-lookup"><span data-stu-id="920e4-135">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

