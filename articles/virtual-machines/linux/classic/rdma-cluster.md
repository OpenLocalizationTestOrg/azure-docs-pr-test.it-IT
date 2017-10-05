---
title: Configurare un cluster Linux RDMA per eseguire applicazioni MPI | Microsoft Docs
description: Creare un cluster Linux con macchine virtuali di dimensioni H16r, H16mr, A8 o A9 per usare la rete RDMA di Azure per l'esecuzione di app MPI
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 01834bad-c8e6-48a3-b066-7f1719047dd2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.openlocfilehash: 4b2ceb64b1737918458f6d5c692fc2bfbc0f12ed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-a-linux-rdma-cluster-to-run-mpi-applications"></a><span data-ttu-id="749ea-103">Configurazione di un cluster Linux RDMA per eseguire applicazioni MPI</span><span class="sxs-lookup"><span data-stu-id="749ea-103">Set up a Linux RDMA cluster to run MPI applications</span></span>
<span data-ttu-id="749ea-104">Informazioni su come configurare un cluster Linux RDMA in Azure con [Dimensioni delle VM High Performance Computing (HPC)](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per eseguire applicazioni MPI (Message Passing Interface) in parallelo.</span><span class="sxs-lookup"><span data-stu-id="749ea-104">Learn how to set up a Linux RDMA cluster in Azure with [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to run parallel Message Passing Interface (MPI) applications.</span></span> <span data-ttu-id="749ea-105">Questo articolo illustra la procedura per preparare un'immagine Linux HPC per l'esecuzione di Intel MPI in un cluster.</span><span class="sxs-lookup"><span data-stu-id="749ea-105">This article provides steps to prepare a Linux HPC image to run Intel MPI on a cluster.</span></span> <span data-ttu-id="749ea-106">Dopo la preparazione viene distribuito un cluster di macchine virtuali usando questa immagine e una delle dimensioni di macchina virtuale di Azure con supporto per RDMA (attualmente H16r, H16mr, A8 o A9).</span><span class="sxs-lookup"><span data-stu-id="749ea-106">After preparation, you deploy a cluster of VMs using this image and one of the RDMA-capable Azure VM sizes (currently H16r, H16mr, A8, or A9).</span></span> <span data-ttu-id="749ea-107">Usare il cluster per eseguire applicazioni MPI in grado di comunicare in modo efficiente tramite una rete a bassa latenza e velocità effettiva elevata basata sulla tecnologia di accesso diretto a memoria remota (RDMA).</span><span class="sxs-lookup"><span data-stu-id="749ea-107">Use the cluster to run MPI applications that communicate efficiently over a low-latency, high-throughput network based on remote direct memory access (RDMA) technology.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="749ea-108">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="749ea-108">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="749ea-109">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="749ea-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="749ea-110">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="749ea-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

## <a name="cluster-deployment-options"></a><span data-ttu-id="749ea-111">Opzioni di distribuzione del cluster</span><span class="sxs-lookup"><span data-stu-id="749ea-111">Cluster deployment options</span></span>
<span data-ttu-id="749ea-112">Di seguito vengono riportati i metodi utilizzabili per creare un cluster Linux RDMA con o senza un'utilità di pianificazione del processo.</span><span class="sxs-lookup"><span data-stu-id="749ea-112">Following are methods you can use to create a Linux RDMA cluster with or without a job scheduler.</span></span>

* <span data-ttu-id="749ea-113">**Script dell'interfaccia della riga di comando di Azure**: come illustrato più avanti in questo articolo, usare l'[interfaccia della riga di comando di Azure](../../../cli-install-nodejs.md) per eseguire lo script della distribuzione di un cluster di macchine virtuali con supporto per RDMA.</span><span class="sxs-lookup"><span data-stu-id="749ea-113">**Azure CLI scripts**: As shown later in this article, use the [Azure command-line interface](../../../cli-install-nodejs.md) (CLI) to script the deployment of a cluster of RDMA-capable VMs.</span></span> <span data-ttu-id="749ea-114">L'interfaccia della riga di comando in modalità Service Management crea i nodi del cluster in modo seriale nel modello di distribuzione classica, quindi la distribuzione di molti nodi di calcolo potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="749ea-114">The CLI in Service Management mode creates the cluster nodes serially in the classic deployment model, so deploying many compute nodes might take several minutes.</span></span> <span data-ttu-id="749ea-115">Per abilitare la connessione di rete RDMA quando si usa il modello di distribuzione classico, distribuire le macchine virtuali nello stesso servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="749ea-115">To enable the RDMA network connection when you use the classic deployment model, deploy the VMs in the same cloud service.</span></span>
* <span data-ttu-id="749ea-116">**Modelli di Azure Resource Manager**: è possibile anche usare il modello di distribuzione di Resource Manager per distribuire un cluster di macchine virtuali con supporto per RDMA che si connette alla rete RDMA.</span><span class="sxs-lookup"><span data-stu-id="749ea-116">**Azure Resource Manager templates**: You can also use the Resource Manager deployment model to deploy a cluster of RDMA-capable VMs that connects to the RDMA network.</span></span> <span data-ttu-id="749ea-117">Per distribuire la soluzione desiderata, è possibile [creare un modello personalizzato](../../../resource-group-authoring-templates.md) o vedere la [Modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/) per accedere ai modelli forniti da Microsoft o dalla community.</span><span class="sxs-lookup"><span data-stu-id="749ea-117">You can [create your own template](../../../resource-group-authoring-templates.md), or check the [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/) for templates contributed by Microsoft or the community to deploy the solution you want.</span></span> <span data-ttu-id="749ea-118">I modelli di Gestione risorse riescono a fornire un modo veloce e affidabile per distribuire un cluster Linux.</span><span class="sxs-lookup"><span data-stu-id="749ea-118">Resource Manager templates can provide a fast and reliable way to deploy a Linux cluster.</span></span> <span data-ttu-id="749ea-119">Per abilitare la connessione di rete RDMA quando si usa il modello di distribuzione di Resource Manager, distribuire le macchine virtuali nello stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="749ea-119">To enable the RDMA network connection when you use the Resource Manager deployment model, deploy the VMs in the same availability set.</span></span>
* <span data-ttu-id="749ea-120">**HPC Pack**: creare un cluster Microsoft HPC Pack in Azure e aggiungere nodi di calcolo con supporto per RDMA che eseguono una distribuzione Linux supportata per accedere alla rete RDMA.</span><span class="sxs-lookup"><span data-stu-id="749ea-120">**HPC Pack**: Create a Microsoft HPC Pack cluster in Azure and add RDMA-capable compute nodes that run a supported Linux distribution to access the RDMA network.</span></span> <span data-ttu-id="749ea-121">Per ulteriori informazioni, vedere [Introduzione all’uso di nodi di calcolo Linux in un cluster HPC Pack in Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="749ea-121">For more information, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="sample-deployment-steps-in-the-classic-model"></a><span data-ttu-id="749ea-122">Procedura per una distribuzione di esempio nel modello classico</span><span class="sxs-lookup"><span data-stu-id="749ea-122">Sample deployment steps in the classic model</span></span>
<span data-ttu-id="749ea-123">I passaggi seguenti mostrano come usare l'interfaccia della riga di comando di Azure per distribuire una macchina virtuale HPC SUSE Linux Enterprise Server (SLES) 12 SP1 da Azure Marketplace, personalizzarla e creare un'immagine di macchina virtuale personalizzata.</span><span class="sxs-lookup"><span data-stu-id="749ea-123">The following steps show how to use the Azure CLI to deploy a SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM from the Azure Marketplace, customize it, and create a custom VM image.</span></span> <span data-ttu-id="749ea-124">È quindi possibile usare l'immagine per lo script della distribuzione di un cluster di macchine virtuali con supporto per RDMA.</span><span class="sxs-lookup"><span data-stu-id="749ea-124">Then you can use the image to script the deployment of a cluster of RDMA-capable VMs.</span></span>

> [!TIP]
> <span data-ttu-id="749ea-125">Usare una procedura simile per distribuire un cluster di macchine virtuali con supporto per RDMA basate su immagini HPC basate su CentOS in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="749ea-125">Use similar steps to deploy a cluster of RDMA-capable VMs based on CentOS-based HPC images in the Azure Marketplace.</span></span> <span data-ttu-id="749ea-126">Come indicato, alcuni passaggi variano leggermente.</span><span class="sxs-lookup"><span data-stu-id="749ea-126">Some steps differ slightly, as noted.</span></span> 
>
>

### <a name="prerequisites"></a><span data-ttu-id="749ea-127">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="749ea-127">Prerequisites</span></span>
* <span data-ttu-id="749ea-128">**Computer client**: è necessario un computer client Mac, Linux o Windows per comunicare con Azure.</span><span class="sxs-lookup"><span data-stu-id="749ea-128">**Client computer**: You need a Mac, Linux, or Windows client computer to communicate with Azure.</span></span> <span data-ttu-id="749ea-129">Nella procedura si presuppone che venga usato un client Linux.</span><span class="sxs-lookup"><span data-stu-id="749ea-129">These steps assume you are using a Linux client.</span></span>
* <span data-ttu-id="749ea-130">**Sottoscrizione di Azure**: se non è disponibile una sottoscrizione, è possibile creare un [account gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="749ea-130">**Azure subscription**: If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span> <span data-ttu-id="749ea-131">Per cluster di maggiori dimensioni, prendere in considerazione una sottoscrizione con pagamento in base al consumo o altre opzioni di acquisto.</span><span class="sxs-lookup"><span data-stu-id="749ea-131">For larger clusters, consider a pay-as-you-go subscription or other purchase options.</span></span>
* <span data-ttu-id="749ea-132">**Disponibilità delle dimensioni di macchina virtuale**: offrono supporto per RDMA le dimensioni di istanza seguenti: H16r, H16mr, A8 e A9.</span><span class="sxs-lookup"><span data-stu-id="749ea-132">**VM size availability**: The following instance sizes are RDMA capable: H16r, H16mr, A8, and A9.</span></span> <span data-ttu-id="749ea-133">Per informazioni sulla disponibilità nelle aree di Azure, vedere [Prodotti disponibili in base all'area](https://azure.microsoft.com/regions/services/) .</span><span class="sxs-lookup"><span data-stu-id="749ea-133">Check [Products available by region](https://azure.microsoft.com/regions/services/) for availability in Azure regions.</span></span>
* <span data-ttu-id="749ea-134">**Quota di core**: può essere necessario aumentare la quota di core per distribuire un cluster di macchine virtuali a elevato uso di calcolo.</span><span class="sxs-lookup"><span data-stu-id="749ea-134">**Cores quota**: You might need to increase the quota of cores to deploy a cluster of compute-intensive VMs.</span></span> <span data-ttu-id="749ea-135">Ad esempio, se si desidera distribuire 8 VM A9 come illustrato in questo articolo, è necessario disporre di almeno 128 core.</span><span class="sxs-lookup"><span data-stu-id="749ea-135">For example, you need at least 128 cores if you want to deploy 8 A9 VMs as shown in this article.</span></span> <span data-ttu-id="749ea-136">La sottoscrizione può anche limitare il numero di core che è possibile distribuire in alcune famiglie di dimensioni di macchina virtuale, inclusa la serie H.</span><span class="sxs-lookup"><span data-stu-id="749ea-136">Your subscription might also limit the number of cores you can deploy in certain VM size families, including the H-series.</span></span> <span data-ttu-id="749ea-137">Per richiedere un aumento della quota, è possibile [aprire una richiesta di assistenza clienti online](../../../azure-supportability/how-to-create-azure-support-request.md) senza alcun addebito.</span><span class="sxs-lookup"><span data-stu-id="749ea-137">To request a quota increase, [open an online customer support request](../../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
* <span data-ttu-id="749ea-138">**Interfaccia della riga di comando di Azure**: [installare](../../../cli-install-nodejs.md) l'interfaccia della riga di comando di Azure e [connetterla alla sottoscrizione di Azure](../../../xplat-cli-connect.md) dal computer client.</span><span class="sxs-lookup"><span data-stu-id="749ea-138">**Azure CLI**: [Install](../../../cli-install-nodejs.md) the Azure CLI and [connect to your Azure subscription](../../../xplat-cli-connect.md) from the client computer.</span></span>

### <a name="provision-an-sles-12-sp1-hpc-vm"></a><span data-ttu-id="749ea-139">Provisioning di una macchina virtuale HPC SLES 12 SP1</span><span class="sxs-lookup"><span data-stu-id="749ea-139">Provision an SLES 12 SP1 HPC VM</span></span>
<span data-ttu-id="749ea-140">Dopo l'accesso ad Azure con l'interfaccia della riga di comando di Azure, eseguire `azure config list` per verificare che l'output indichi la modalità Azure Service Management.</span><span class="sxs-lookup"><span data-stu-id="749ea-140">After signing in to Azure with the Azure CLI, run `azure config list` to confirm that the output shows Service Management mode.</span></span> <span data-ttu-id="749ea-141">In caso contrario, impostare la modalità eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="749ea-141">If it does not, set the mode by running this command:</span></span>

    azure config mode asm


<span data-ttu-id="749ea-142">Digitare il comando seguente per elencare tutte le sottoscrizioni per le quali si dispone dell'autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="749ea-142">Type the following to list all the subscriptions you are authorized to use:</span></span>

    azure account list

<span data-ttu-id="749ea-143">La sottoscrizione attualmente attiva sarà identificata da `Current` impostato su `true`.</span><span class="sxs-lookup"><span data-stu-id="749ea-143">The current active subscription is identified with `Current` set to `true`.</span></span> <span data-ttu-id="749ea-144">Se questa sottoscrizione non è quella che si desidera usare per creare il cluster, impostare l'ID sottoscrizione appropriato come sottoscrizione attiva:</span><span class="sxs-lookup"><span data-stu-id="749ea-144">If this subscription isn't the one you want to use to create the cluster, set the appropriate subscription ID as the active subscription:</span></span>

    azure account set <subscription-Id>

<span data-ttu-id="749ea-145">Per visualizzare le immagini HPC SLES 12 SP1 disponibili pubblicamente in Azure, eseguire un comando simile al seguente, presupponendo che l'ambiente shell supporti **grep**:</span><span class="sxs-lookup"><span data-stu-id="749ea-145">To see the publicly available SLES 12 SP1 HPC images in Azure, run a command like the following, assuming your shell environment supports **grep**:</span></span>

    azure vm image list | grep "suse.*hpc"

<span data-ttu-id="749ea-146">Eseguire il provisioning di una macchina virtuale con supporto per RDMA con un'immagine HPC SLES 12 SP1 eseguendo un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="749ea-146">Provision an RDMA-capable VM with a SLES 12 SP1 HPC image by running a command like the following:</span></span>

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

<span data-ttu-id="749ea-147">Dove:</span><span class="sxs-lookup"><span data-stu-id="749ea-147">Where:</span></span>

* <span data-ttu-id="749ea-148">La dimensione (A9 in questo esempio) è una delle dimensioni di macchina virtuale con supporto per RDMA.</span><span class="sxs-lookup"><span data-stu-id="749ea-148">The size (A9 in this example) is one of the RDMA-capable VM sizes.</span></span>
* <span data-ttu-id="749ea-149">Il numero della porta SSH esterna (22 in questo esempio, ovvero la porta SSH predefinita) può essere qualsiasi numero di porta valido.</span><span class="sxs-lookup"><span data-stu-id="749ea-149">The external SSH port number (22 in this example, which is the SSH default) is any valid port number.</span></span> <span data-ttu-id="749ea-150">Il numero della porta SSH interna è impostato su 22.</span><span class="sxs-lookup"><span data-stu-id="749ea-150">The internal SSH port number is set to 22.</span></span>
* <span data-ttu-id="749ea-151">viene creato un nuovo servizio cloud nell'area di Azure specificata dalla località</span><span class="sxs-lookup"><span data-stu-id="749ea-151">A new cloud service is created in the Azure region specified by the location.</span></span> <span data-ttu-id="749ea-152">Specificare una posizione in cui sia disponibile la dimensione di macchina virtuale scelta.</span><span class="sxs-lookup"><span data-stu-id="749ea-152">Specify a location in which the VM size you choose is available.</span></span>
* <span data-ttu-id="749ea-153">Attualmente il nome dell'immagine SLES 12 SP1 può essere una delle due opzioni seguenti per il supporto SUSE prioritario (sono previsti costi aggiuntivi).</span><span class="sxs-lookup"><span data-stu-id="749ea-153">For SUSE priority support (which incurs additional charges), the SLES 12 SP1 image name currently can be one of these two options:</span></span> 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-the-vm"></a><span data-ttu-id="749ea-154">Personalizzazione della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="749ea-154">Customize the VM</span></span>
<span data-ttu-id="749ea-155">Quando la macchina virtuale completa il provisioning, assegnare una porta SSH alla macchina virtuale usando l'indirizzo IP esterno della macchina virtuale (o nome DNS) e il numero della porta esterna configurata, quindi personalizzarla.</span><span class="sxs-lookup"><span data-stu-id="749ea-155">After the VM finishes provisioning, SSH to the VM by using the VM's external IP address (or DNS name) and the external port number you configured, and then customize it.</span></span> <span data-ttu-id="749ea-156">Per informazioni dettagliate sulla connessione, vedere [Come accedere a una macchina virtuale che esegue Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="749ea-156">For connection details, see [How to log on to a virtual machine running Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="749ea-157">Eseguire i comandi come l'utente configurato nella VM, a meno che non sia necessario l'accesso alla radice per eseguire un passaggio.</span><span class="sxs-lookup"><span data-stu-id="749ea-157">Perform commands as the user you configured on the VM, unless root access is required to complete a step.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="749ea-158">Microsoft Azure non fornisce l'accesso alla directory principale per le macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="749ea-158">Microsoft Azure does not provide root access to Linux VMs.</span></span> <span data-ttu-id="749ea-159">Per ottenere l'accesso amministrativo quando si è connessi come utente alla macchina virtuale, eseguire i comandi con `sudo`.</span><span class="sxs-lookup"><span data-stu-id="749ea-159">To gain administrative access when connected as a user to the VM, run commands by using `sudo`.</span></span>
>
>

* <span data-ttu-id="749ea-160">**Aggiornamenti**: installare gli aggiornamenti usando zypper.</span><span class="sxs-lookup"><span data-stu-id="749ea-160">**Updates**: Install updates by using zypper.</span></span> <span data-ttu-id="749ea-161">È anche possibile decidere di installare le utilità NFS.</span><span class="sxs-lookup"><span data-stu-id="749ea-161">You might also want to install NFS utilities.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="749ea-162">In una macchina virtuale HPC SLES 12 SP1 è consigliabile non applicare gli aggiornamenti del kernel, che possono causare problemi con i driver Linux RDMA.</span><span class="sxs-lookup"><span data-stu-id="749ea-162">In a SLES 12 SP1 HPC VM, we recommend that you don't apply kernel updates, which can cause issues with the Linux RDMA drivers.</span></span>
  >
  >
* <span data-ttu-id="749ea-163">**Intel MPI**: completare l'installazione di Intel MPI nella macchina virtuale HPC SLES 12 SP1 eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="749ea-163">**Intel MPI**: Complete the installation of Intel MPI on the SLES 12 SP1 HPC VM by running the following command:</span></span>

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* <span data-ttu-id="749ea-164">**Blocco della memoria**: affinché i codici MPI blocchino la memoria disponibile per RDMA, aggiungere o modificare le impostazioni seguenti nel file /etc/security/limits.conf.</span><span class="sxs-lookup"><span data-stu-id="749ea-164">**Lock memory**: For MPI codes to lock the memory available for RDMA, add or change the following settings in the /etc/security/limits.conf file.</span></span> <span data-ttu-id="749ea-165">Per modificare questo file è necessario l'accesso alla radice.</span><span class="sxs-lookup"><span data-stu-id="749ea-165">You need root access to edit this file.</span></span>

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > <span data-ttu-id="749ea-166">A scopo di test, è inoltre possibile impostare memlock su illimitato.</span><span class="sxs-lookup"><span data-stu-id="749ea-166">For testing purposes, you can also set memlock to unlimited.</span></span> <span data-ttu-id="749ea-167">Ad esempio: `<User or group name>    hard    memlock unlimited`.</span><span class="sxs-lookup"><span data-stu-id="749ea-167">For example: `<User or group name>    hard    memlock unlimited`.</span></span> <span data-ttu-id="749ea-168">Per altre informazioni, vedere [Metodi noti per l'impostazione delle dimensioni della memoria bloccata](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span><span class="sxs-lookup"><span data-stu-id="749ea-168">For more information, see [Best known methods for setting locked memory size](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span></span>
  >
  >
* <span data-ttu-id="749ea-169">**Chiavi SSH per VM SLES**: generare chiavi SSH per stabilire una relazione di trust per il proprio account utente tra i nodi di calcolo del cluster SLES quando vengono eseguiti processi MPI.</span><span class="sxs-lookup"><span data-stu-id="749ea-169">**SSH keys for SLES VMs**: Generate SSH keys to establish trust for your user account among the compute nodes in the SLES cluster when running MPI jobs.</span></span> <span data-ttu-id="749ea-170">Se è stata distribuita una macchina virtuale HPC basata su CentOS, non seguire questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="749ea-170">If you deployed a CentOS-based HPC VM, don't follow this step.</span></span> <span data-ttu-id="749ea-171">Vedere le istruzioni più avanti nell'articolo per configurare un trust SSH senza password tra i nodi del cluster dopo aver acquisito l'immagine e distribuito il cluster.</span><span class="sxs-lookup"><span data-stu-id="749ea-171">See instructions later in this article to set up passwordless SSH trust among the cluster nodes after you capture the image and deploy the cluster.</span></span>

    <span data-ttu-id="749ea-172">Usare il comando seguente per creare chiavi SSH.</span><span class="sxs-lookup"><span data-stu-id="749ea-172">To create SSH keys, run the following command.</span></span> <span data-ttu-id="749ea-173">Quando viene richiesto, premere **INVIO** per generare le chiavi nel percorso predefinito senza impostare una password.</span><span class="sxs-lookup"><span data-stu-id="749ea-173">When you are prompted for input, select **Enter** to generate the keys in the default location without setting a password.</span></span>

        ssh-keygen

    <span data-ttu-id="749ea-174">Aggiungere la chiave pubblica alla fine del file authorized_keys per le chiavi pubbliche note.</span><span class="sxs-lookup"><span data-stu-id="749ea-174">Append the public key to the authorized_keys file for known public keys.</span></span>

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    <span data-ttu-id="749ea-175">Nella directory ~/.ssh modificare o creare il file config.</span><span class="sxs-lookup"><span data-stu-id="749ea-175">In the ~/.ssh directory, edit or create the config file.</span></span> <span data-ttu-id="749ea-176">Specificare l'intervallo di indirizzi IP della rete privata che si prevede di usare in Azure (10.32.0.0/16 in questo esempio):</span><span class="sxs-lookup"><span data-stu-id="749ea-176">Provide the IP address range of the private network that you plan to use in Azure (10.32.0.0/16 in this example):</span></span>

        host 10.32.0.*
        StrictHostKeyChecking no

    <span data-ttu-id="749ea-177">In alternativa, elencare l'indirizzo IP di rete privata di ogni macchina virtuale del cluster come segue:</span><span class="sxs-lookup"><span data-stu-id="749ea-177">Alternatively, list the private network IP address of each VM in your cluster as follows:</span></span>

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > <span data-ttu-id="749ea-178">La configurazione di `StrictHostKeyChecking no` può creare un potenziale rischio di sicurezza quando non viene specificato un intervallo o un indirizzo IP specifico.</span><span class="sxs-lookup"><span data-stu-id="749ea-178">Configuring `StrictHostKeyChecking no` can create a potential security risk when a specific IP address or range is not specified.</span></span>
  >
  >
* <span data-ttu-id="749ea-179">**Applicazioni**: installare le applicazioni necessarie in questa macchina virtuale o eseguire altre personalizzazioni prima di acquisire l'immagine.</span><span class="sxs-lookup"><span data-stu-id="749ea-179">**Applications**: Install any applications you need or perform other customizations before you capture the image.</span></span>

### <a name="capture-the-image"></a><span data-ttu-id="749ea-180">Acquisire l'immagine</span><span class="sxs-lookup"><span data-stu-id="749ea-180">Capture the image</span></span>
<span data-ttu-id="749ea-181">Per acquisire l'immagine, eseguire prima il comando seguente nella macchina virtuale Linux.</span><span class="sxs-lookup"><span data-stu-id="749ea-181">To capture the image, first run the following command on the Linux VM.</span></span> <span data-ttu-id="749ea-182">Questo comando esegue il deprovisioning della VM, ma mantiene gli account utente e le chiavi SSH configurati.</span><span class="sxs-lookup"><span data-stu-id="749ea-182">This command deprovisions the VM but maintains user accounts and SSH keys that you set up.</span></span>

```
sudo waagent -deprovision
```

<span data-ttu-id="749ea-183">Dal computer client, usare i seguenti comandi dell'interfaccia della riga di comando di Azure per acquisire l'immagine.</span><span class="sxs-lookup"><span data-stu-id="749ea-183">From your client computer, run the following Azure CLI commands to capture the image.</span></span> <span data-ttu-id="749ea-184">Per ulteriori informazioni, vedere [Come acquisire una macchina virtuale Linux classica come immagine](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="749ea-184">For more information, see [How to capture a classic Linux virtual machine as an image](capture-image.md).</span></span>  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

<span data-ttu-id="749ea-185">Dopo l'esecuzione di questi comandi, l'immagine della macchina virtuale viene acquisita per l'uso e la macchina virtuale viene eliminata.</span><span class="sxs-lookup"><span data-stu-id="749ea-185">After you run these commands, the VM image is captured for your use and the VM is deleted.</span></span> <span data-ttu-id="749ea-186">Ora si dispone dell'immagine personalizzata pronta per distribuire un cluster.</span><span class="sxs-lookup"><span data-stu-id="749ea-186">Now you have your custom image ready to deploy a cluster.</span></span>

### <a name="deploy-a-cluster-with-the-image"></a><span data-ttu-id="749ea-187">Distribuzione di un cluster con l'immagine</span><span class="sxs-lookup"><span data-stu-id="749ea-187">Deploy a cluster with the image</span></span>
<span data-ttu-id="749ea-188">Modificare lo script Bash seguente con i valori appropriati per il proprio ambiente ed eseguirlo dal computer client.</span><span class="sxs-lookup"><span data-stu-id="749ea-188">Modify the following Bash script with appropriate values for your environment and run it from your client computer.</span></span> <span data-ttu-id="749ea-189">Poiché Azure distribuisce le VM in modo seriale nel modello di distribuzione classica, sono necessari alcuni minuti per distribuire le otto macchine virtuali A9 suggerite in questo script.</span><span class="sxs-lookup"><span data-stu-id="749ea-189">Because Azure deploys the VMs serially in the classic deployment model, it takes a few minutes to deploy the eight A9 VMs suggested in this script.</span></span>

```
#!/bin/bash -x
# Script to create a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where the VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All the compute-intensive instances need to be in the same cloud service for Linux RDMA to work across InfiniBand.
# Note: The current maximum number of VMs in a cloud service is 50. If you need to provision more than 50 VMs in the same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want to turn off external ports and use only internal ports to communicate between compute nodes via port 22, don’t use this option. Since port numbers up to 10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 to cluster18. Specify your captured image in <image-name>. Specify the username and password you used when creating the SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment to provision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a><span data-ttu-id="749ea-190">Considerazioni per un cluster HPC CentOS</span><span class="sxs-lookup"><span data-stu-id="749ea-190">Considerations for a CentOS HPC cluster</span></span>
<span data-ttu-id="749ea-191">Se si vuole impostare un cluster in base a una delle immagini HPC basate su CentOS in Azure Marketplace anziché SLES 12 per HPC, seguire la procedura generale riportata nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="749ea-191">If you want to set up a cluster based on one of the CentOS-based HPC images in the Azure Marketplace instead of SLES 12 for HPC, follow the general steps in the preceding section.</span></span> <span data-ttu-id="749ea-192">Durante il provisioning e la configurazione della macchina virtuale, tenere presenti le differenze seguenti:</span><span class="sxs-lookup"><span data-stu-id="749ea-192">Note the following differences when you provision and configure the VM:</span></span>

- <span data-ttu-id="749ea-193">Intel MPI è già installato in una macchina virtuale con provisioning da un'immagine HPC basata su CentOS.</span><span class="sxs-lookup"><span data-stu-id="749ea-193">Intel MPI is already installed on a VM provisioned from a CentOS-based HPC image.</span></span>
- <span data-ttu-id="749ea-194">Le impostazioni di blocco della memoria sono già state aggiunte al file /etc/security/limits.conf della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="749ea-194">Lock memory settings are already added in the VM's /etc/security/limits.conf file.</span></span>
- <span data-ttu-id="749ea-195">Non generare chiavi SSH sulla macchina virtuale di cui viene effettuato il provisioning per l'acquisizione.</span><span class="sxs-lookup"><span data-stu-id="749ea-195">Do not generate SSH keys on the VM you provision for capture.</span></span> <span data-ttu-id="749ea-196">È invece consigliabile impostare l'autenticazione basata sull'utente dopo la distribuzione del cluster.</span><span class="sxs-lookup"><span data-stu-id="749ea-196">Instead, we recommend setting up user-based authentication after you deploy the cluster.</span></span> <span data-ttu-id="749ea-197">Per altre informazioni, vedere la sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="749ea-197">For more information, see the following section.</span></span>  

### <a name="set-up-passwordless-ssh-trust-on-the-cluster"></a><span data-ttu-id="749ea-198">Impostare il trust SSH senza password nel cluster</span><span class="sxs-lookup"><span data-stu-id="749ea-198">Set up passwordless SSH trust on the cluster</span></span>
<span data-ttu-id="749ea-199">In un cluster HPC basato su CentOS sono disponibili due metodi per stabilire relazioni di trust tra i nodi di calcolo: autenticazione basata sull'host e autenticazione basata sull'utente.</span><span class="sxs-lookup"><span data-stu-id="749ea-199">On a CentOS-based HPC cluster, there are two methods for establishing trust between the compute nodes: host-based authentication and user-based authentication.</span></span> <span data-ttu-id="749ea-200">L'autenticazione basata sull'host non rientra nell'ambito di questo articolo e in genere deve essere eseguita tramite uno script di estensione durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="749ea-200">Host-based authentication is outside of the scope of this article and generally must be done through an extension script during deployment.</span></span> <span data-ttu-id="749ea-201">L'autenticazione basata sull'utente è utile per stabilire un trust dopo la distribuzione e richiede la generazione e la condivisione di chiavi SSH tra i nodi di calcolo nel cluster.</span><span class="sxs-lookup"><span data-stu-id="749ea-201">User-based authentication is convenient for establishing trust after deployment and requires the generation and sharing of SSH keys among the compute nodes in the cluster.</span></span> <span data-ttu-id="749ea-202">Questo metodo è comunemente noto come accesso SSH senza password ed è obbligatorio quando si eseguono processi MPI.</span><span class="sxs-lookup"><span data-stu-id="749ea-202">This method is commonly known as passwordless SSH login and is required when running MPI jobs.</span></span>

<span data-ttu-id="749ea-203">In [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) è disponibile uno script di esempio fornito dalla community per abilitare l'autenticazione utente semplice in un cluster HPC basato su CentOS.</span><span class="sxs-lookup"><span data-stu-id="749ea-203">A sample script contributed from the community is available on [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) to enable easy user authentication on a CentOS-based HPC cluster.</span></span> <span data-ttu-id="749ea-204">Scaricare e usare questo script con la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="749ea-204">Download and use this script by using the following steps.</span></span> <span data-ttu-id="749ea-205">È anche possibile modificare lo script o usare qualsiasi altro metodo per stabilire l'autenticazione SSH senza password tra i nodi di calcolo del cluster.</span><span class="sxs-lookup"><span data-stu-id="749ea-205">You can also modify this script or use any other method to establish passwordless SSH authentication between the cluster compute nodes.</span></span>

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

<span data-ttu-id="749ea-206">Per eseguire lo script, è necessario conoscere il prefisso degli indirizzi IP della subnet.</span><span class="sxs-lookup"><span data-stu-id="749ea-206">To run the script, you need to know the prefix for your subnet IP addresses.</span></span> <span data-ttu-id="749ea-207">È possibile ottenere il prefisso con il comando seguente in uno dei nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="749ea-207">Get the prefix by running the following command on one of the cluster nodes.</span></span> <span data-ttu-id="749ea-208">L'output sarà essere simile a 10.1.3.5 e il prefisso è la parte 10.1.3.</span><span class="sxs-lookup"><span data-stu-id="749ea-208">Your output should look something like 10.1.3.5, and the prefix is the 10.1.3 portion.</span></span>

    ifconfig eth0 | grep -w inet | awk '{print $2}'

<span data-ttu-id="749ea-209">Eseguire lo script con tre parametri: il nome utente comune nei nodi di calcolo, la password comune per tale utente nei nodi di calcolo e il prefisso della subnet restituito dal comando precedente.</span><span class="sxs-lookup"><span data-stu-id="749ea-209">Now run the script using three parameters: the common user name on the compute nodes, the common password for that user on the compute nodes, and the subnet prefix that was returned from the previous command.</span></span>

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

<span data-ttu-id="749ea-210">Lo script esegue queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="749ea-210">This script does the following:</span></span>

* <span data-ttu-id="749ea-211">Crea una directory nel nodo host denominata SSH, necessaria per l'accesso senza password.</span><span class="sxs-lookup"><span data-stu-id="749ea-211">Creates a directory on the host node named .ssh, which is required for passwordless login.</span></span>
* <span data-ttu-id="749ea-212">Crea un file di configurazione nella directory .ssh che indica di consentire l'accesso senza password da qualsiasi nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="749ea-212">Creates a configuration file in the .ssh directory that instructs passwordless login to allow login from any node in the cluster.</span></span>
* <span data-ttu-id="749ea-213">Crea file contenenti i nomi dei nodi e gli indirizzi IP dei nodi per tutti i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="749ea-213">Creates files containing the node names and node IP addresses for all the nodes in the cluster.</span></span> <span data-ttu-id="749ea-214">Questi file vengono lasciati dopo l'esecuzione dello script come riferimento futuro.</span><span class="sxs-lookup"><span data-stu-id="749ea-214">These files are left after the script is run for later reference.</span></span>
* <span data-ttu-id="749ea-215">Crea una coppia di chiavi pubblica e privata per ogni nodo del cluster, incluso il nodo host, e crea una voce nel file authorized_keys.</span><span class="sxs-lookup"><span data-stu-id="749ea-215">Creates a private and public key pair for each cluster node (including the host node) and creates entries in the authorized_keys file.</span></span>

> [!WARNING]
> <span data-ttu-id="749ea-216">L'esecuzione di questo script può creare un potenziale rischio per la sicurezza.</span><span class="sxs-lookup"><span data-stu-id="749ea-216">Running this script can create a potential security risk.</span></span> <span data-ttu-id="749ea-217">Assicurarsi che le informazioni sulla chiave pubblica in ~/.ssh non vengano distribuite.</span><span class="sxs-lookup"><span data-stu-id="749ea-217">Ensure that the public key information in ~/.ssh is not distributed.</span></span>
>
>

## <a name="configure-intel-mpi"></a><span data-ttu-id="749ea-218">Configurare Intel MPI</span><span class="sxs-lookup"><span data-stu-id="749ea-218">Configure Intel MPI</span></span>
<span data-ttu-id="749ea-219">Per eseguire applicazioni MPI su Azure Linux RDMA, è necessario configurare determinate variabili di ambiente specifiche di Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="749ea-219">To run MPI applications on Azure Linux RDMA, you need to configure certain environment variables specific to Intel MPI.</span></span> <span data-ttu-id="749ea-220">Di seguito è riportato uno script Bash di esempio per la configurazione delle variabili necessarie per eseguire un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="749ea-220">Here is a sample Bash script to configure the variables needed to run an application.</span></span> <span data-ttu-id="749ea-221">Modificare il percorso in mpivars.sh secondo le esigenze per l'installazione di Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="749ea-221">Change the path to mpivars.sh as needed for your installation of Intel MPI.</span></span>

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting the variable to shm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line to run the job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path to the application exe> <arguments specific to the application>

#end
```

<span data-ttu-id="749ea-222">Il formato del file host è indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="749ea-222">The format of the host file is as follows.</span></span> <span data-ttu-id="749ea-223">Aggiungere una riga per ciascun nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="749ea-223">Add one line for each node in your cluster.</span></span> <span data-ttu-id="749ea-224">Specificare gli indirizzi IP privati dalla rete virtuale definita in precedenza, non i nomi DNS.</span><span class="sxs-lookup"><span data-stu-id="749ea-224">Specify private IP addresses from the virtual network defined earlier, not DNS names.</span></span> <span data-ttu-id="749ea-225">Ad esempio, per due host con gli indirizzi IP 10.32.0.1 e 10.32.0.2 il file contiene quanto segue:</span><span class="sxs-lookup"><span data-stu-id="749ea-225">For example, for two hosts with IP addresses 10.32.0.1 and 10.32.0.2, the file contains the following:</span></span>

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a><span data-ttu-id="749ea-226">Eseguire MPI su un cluster di base a due nodi</span><span class="sxs-lookup"><span data-stu-id="749ea-226">Run MPI on a basic two-node cluster</span></span>
<span data-ttu-id="749ea-227">Se non si è ancora provveduto, prima configurare l'ambiente per Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="749ea-227">If you haven't already done so, first set up the environment for Intel MPI.</span></span>

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a><span data-ttu-id="749ea-228">Eseguire un comando MPI</span><span class="sxs-lookup"><span data-stu-id="749ea-228">Run an MPI command</span></span>
<span data-ttu-id="749ea-229">Eseguire un comando MPI su uno dei nodi di calcolo per vedere che MPI è installato correttamente e può comunicare tra almeno due nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="749ea-229">Run an MPI command on one of the compute nodes to show that MPI is installed properly and can communicate between at least two compute nodes.</span></span> <span data-ttu-id="749ea-230">Il comando **mpirun** seguente esegue il comando **hostname** su due nodi.</span><span class="sxs-lookup"><span data-stu-id="749ea-230">The following **mpirun** command runs the **hostname** command on two nodes.</span></span>

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
<span data-ttu-id="749ea-231">L'output dovrebbe elencare i nomi di tutti i nodi passati come input per `-hosts`.</span><span class="sxs-lookup"><span data-stu-id="749ea-231">Your output should list the names of all the nodes that you passed as input for `-hosts`.</span></span> <span data-ttu-id="749ea-232">Ad esempio, un comando **mpirun** con due nodi restituisce un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="749ea-232">For example, an **mpirun** command with two nodes returns output like the following:</span></span>

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a><span data-ttu-id="749ea-233">Eseguire un benchmark MPI</span><span class="sxs-lookup"><span data-stu-id="749ea-233">Run an MPI benchmark</span></span>
<span data-ttu-id="749ea-234">Il comando Intel MPI seguente esegue un benchmark pingpong per verificare la configurazione del cluster e la connessione alla rete RDMA.</span><span class="sxs-lookup"><span data-stu-id="749ea-234">The following Intel MPI command runs a pingpong benchmark to verify the cluster configuration and connection to the RDMA network.</span></span>

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

<span data-ttu-id="749ea-235">In un cluster funzionante con due nodi dovrebbe essere visualizzato un output simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="749ea-235">On a working cluster with two nodes, you should see output like the following.</span></span> <span data-ttu-id="749ea-236">Nella rete RDMA di Azure è prevista una latenza pari o inferiore a 3 microsecondi per i messaggi con una dimensione massima di 512 byte.</span><span class="sxs-lookup"><span data-stu-id="749ea-236">On the Azure RDMA network, expect latency at or below 3 microseconds for message sizes up to 512 bytes.</span></span>

```
#------------------------------------------------------------
#    Intel (R) MPI Benchmarks 4.0 Update 1, MPI-1 part
#------------------------------------------------------------
# Date                  : Fri Jul 17 23:16:46 2015
# Machine               : x86_64
# System                : Linux
# Release               : 3.12.39-44-default
# Version               : #5 SMP Thu Jun 25 22:45:24 UTC 2015
# MPI Version           : 3.0
# MPI Thread Environment:
# New default behavior from Version 3.2 on:
# the number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected to be exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through the flag => -time

# Calling sequence was:
# /opt/intel/impi_latest/bin64/IMB-MPI1 pingpong
# Minimum message length in bytes:   0
# Maximum message length in bytes:   4194304
#
# MPI_Datatype                   :   MPI_BYTE
# MPI_Datatype for reductions    :   MPI_FLOAT
# MPI_Op                         :   MPI_SUM
#
#
# List of Benchmarks to run:
# PingPong
#---------------------------------------------------
# Benchmarking PingPong
# #processes = 2
#---------------------------------------------------
       #bytes #repetitions      t[usec]   Mbytes/sec
            0         1000         2.23         0.00
            1         1000         2.26         0.42
            2         1000         2.26         0.85
            4         1000         2.26         1.69
            8         1000         2.26         3.38
           16         1000         2.36         6.45
           32         1000         2.57        11.89
           64         1000         2.36        25.81
          128         1000         2.64        46.19
          256         1000         2.73        89.30
          512         1000         3.09       157.99
         1024         1000         3.60       271.53
         2048         1000         4.46       437.57
         4096         1000         6.11       639.23
         8192         1000         7.49      1043.47
        16384         1000         9.76      1600.76
        32768         1000        14.98      2085.77
        65536          640        25.99      2405.08
       131072          320        50.68      2466.64
       262144          160        80.62      3101.01
       524288           80       145.86      3427.91
      1048576           40       279.06      3583.42
      2097152           20       543.37      3680.71
      4194304           10      1082.94      3693.63

# All processes entering MPI_Finalize

```



## <a name="next-steps"></a><span data-ttu-id="749ea-237">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="749ea-237">Next steps</span></span>
* <span data-ttu-id="749ea-238">Distribuire ed eseguire le applicazioni MPI Linux nel cluster Linux.</span><span class="sxs-lookup"><span data-stu-id="749ea-238">Deploy and run your Linux MPI applications on your Linux cluster.</span></span>
* <span data-ttu-id="749ea-239">Per istruzioni su Intel MPI, vedere la [documentazione relativa a Intel MPI Library](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/).</span><span class="sxs-lookup"><span data-stu-id="749ea-239">See the [Intel MPI Library documentation](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) for guidance on Intel MPI.</span></span>
* <span data-ttu-id="749ea-240">Provare un [modello di avvio rapido](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) per creare un cluster Intel Lustre usando un'immagine basata HPC su CentOS.</span><span class="sxs-lookup"><span data-stu-id="749ea-240">Try a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) to create an Intel Lustre cluster by using a CentOS-based HPC image.</span></span> <span data-ttu-id="749ea-241">Per informazioni dettagliate, vedere [Distribuzione di Intel Cloud Edition per Lustre in Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span><span class="sxs-lookup"><span data-stu-id="749ea-241">For details, see [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span></span>
