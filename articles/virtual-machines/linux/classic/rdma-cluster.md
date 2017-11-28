---
title: aaaSet un applicazioni MPI di Linux RDMA cluster toorun | Documenti Microsoft
description: Creare un cluster Linux di toouse H16r, H16mr, A8 o A9 VM di dimensioni hello Azure RDMA rete toorun MPI App
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
ms.openlocfilehash: 3199317a37b095e80718d6724954687d30aea3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-linux-rdma-cluster-toorun-mpi-applications"></a><span data-ttu-id="6fbec-103">Impostare un applicazioni MPI toorun di Linux RDMA cluster</span><span class="sxs-lookup"><span data-stu-id="6fbec-103">Set up a Linux RDMA cluster toorun MPI applications</span></span>
<span data-ttu-id="6fbec-104">Informazioni su come tooset backup un RDMA Linux cluster in Azure con [dimensioni delle macchine Virtuali di calcolo ad alte prestazioni](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun le applicazioni parallele interfaccia MPI (Message Passing).</span><span class="sxs-lookup"><span data-stu-id="6fbec-104">Learn how tooset up a Linux RDMA cluster in Azure with [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun parallel Message Passing Interface (MPI) applications.</span></span> <span data-ttu-id="6fbec-105">Questo articolo fornisce passaggi tooprepare un toorun immagine HPC Linux MPI Intel in un cluster.</span><span class="sxs-lookup"><span data-stu-id="6fbec-105">This article provides steps tooprepare a Linux HPC image toorun Intel MPI on a cluster.</span></span> <span data-ttu-id="6fbec-106">Dopo la preparazione, si distribuisce un cluster di macchine virtuali usando questa immagine di dimensioni di macchina virtuale di Azure che supportano RDMA hello (attualmente H16r, H16mr, A8 o A9).</span><span class="sxs-lookup"><span data-stu-id="6fbec-106">After preparation, you deploy a cluster of VMs using this image and one of hello RDMA-capable Azure VM sizes (currently H16r, H16mr, A8, or A9).</span></span> <span data-ttu-id="6fbec-107">Utilizzare le applicazioni MPI toorun di cluster hello che comunicano in modo efficiente su una rete a bassa latenza, velocità effettiva elevata, basata sulla tecnologia di diretto a memoria remota (RDMA) di accesso.</span><span class="sxs-lookup"><span data-stu-id="6fbec-107">Use hello cluster toorun MPI applications that communicate efficiently over a low-latency, high-throughput network based on remote direct memory access (RDMA) technology.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6fbec-108">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="6fbec-108">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="6fbec-109">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="6fbec-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="6fbec-110">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="6fbec-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

## <a name="cluster-deployment-options"></a><span data-ttu-id="6fbec-111">Opzioni di distribuzione del cluster</span><span class="sxs-lookup"><span data-stu-id="6fbec-111">Cluster deployment options</span></span>
<span data-ttu-id="6fbec-112">Di seguito sono metodi è possibile usare un cluster Linux RDMA toocreate con o senza un'utilità di pianificazione del processo.</span><span class="sxs-lookup"><span data-stu-id="6fbec-112">Following are methods you can use toocreate a Linux RDMA cluster with or without a job scheduler.</span></span>

* <span data-ttu-id="6fbec-113">**Script di Azure CLI**: come illustrato più avanti in questo articolo, utilizzare hello [interfaccia della riga di comando di Azure](../../../cli-install-nodejs.md) distribuzione di hello tooscript (CLI) di un cluster di macchine virtuali che supportano RDMA.</span><span class="sxs-lookup"><span data-stu-id="6fbec-113">**Azure CLI scripts**: As shown later in this article, use hello [Azure command-line interface](../../../cli-install-nodejs.md) (CLI) tooscript hello deployment of a cluster of RDMA-capable VMs.</span></span> <span data-ttu-id="6fbec-114">Hello CLI in modalità di gestione del servizio crea hello i nodi del cluster in modo seriale nel modello di distribuzione classica hello, per consentire la distribuzione di molti nodi di calcolo potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="6fbec-114">hello CLI in Service Management mode creates hello cluster nodes serially in hello classic deployment model, so deploying many compute nodes might take several minutes.</span></span> <span data-ttu-id="6fbec-115">hello tooenable connessione di rete RDMA quando si utilizza il modello di distribuzione classica hello, distribuire le macchine virtuali hello in hello stesso servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="6fbec-115">tooenable hello RDMA network connection when you use hello classic deployment model, deploy hello VMs in hello same cloud service.</span></span>
* <span data-ttu-id="6fbec-116">**Modelli di Azure Resource Manager**: È anche possibile usare toodeploy modello di distribuzione di gestione delle risorse hello un cluster di macchine virtuali con supporto per RDMA che si connette rete RDMA toohello.</span><span class="sxs-lookup"><span data-stu-id="6fbec-116">**Azure Resource Manager templates**: You can also use hello Resource Manager deployment model toodeploy a cluster of RDMA-capable VMs that connects toohello RDMA network.</span></span> <span data-ttu-id="6fbec-117">È possibile [Crea modello personale](../../../resource-group-authoring-templates.md), o controllare hello [modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/) per i modelli forniti da Microsoft o hello community toodeploy hello soluzione desiderata.</span><span class="sxs-lookup"><span data-stu-id="6fbec-117">You can [create your own template](../../../resource-group-authoring-templates.md), or check hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/) for templates contributed by Microsoft or hello community toodeploy hello solution you want.</span></span> <span data-ttu-id="6fbec-118">Modelli di gestione risorse possono fornire un modo rapido e affidabile di toodeploy un cluster Linux.</span><span class="sxs-lookup"><span data-stu-id="6fbec-118">Resource Manager templates can provide a fast and reliable way toodeploy a Linux cluster.</span></span> <span data-ttu-id="6fbec-119">hello tooenable connessione di rete RDMA quando si Usa modello di distribuzione di gestione risorse hello, distribuire le macchine virtuali di hello in hello stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="6fbec-119">tooenable hello RDMA network connection when you use hello Resource Manager deployment model, deploy hello VMs in hello same availability set.</span></span>
* <span data-ttu-id="6fbec-120">**HPC Pack**: creare un cluster di Microsoft HPC Pack in Azure e aggiungere il supporto per RDMA nodi di calcolo che eseguono una rete RDMA di supportata di Linux distribuzione tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="6fbec-120">**HPC Pack**: Create a Microsoft HPC Pack cluster in Azure and add RDMA-capable compute nodes that run a supported Linux distribution tooaccess hello RDMA network.</span></span> <span data-ttu-id="6fbec-121">Per ulteriori informazioni, vedere [Introduzione all’uso di nodi di calcolo Linux in un cluster HPC Pack in Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="6fbec-121">For more information, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="sample-deployment-steps-in-hello-classic-model"></a><span data-ttu-id="6fbec-122">I passaggi di distribuzione di esempio nel modello classico hello</span><span class="sxs-lookup"><span data-stu-id="6fbec-122">Sample deployment steps in hello classic model</span></span>
<span data-ttu-id="6fbec-123">Hello passaggi seguenti mostrano come personalizzarlo, toouse hello Azure CLI toodeploy una VM di HPC SUSE Linux Enterprise Server (SLES) 12 SP1 da Azure Marketplace, hello e creare un'immagine di macchina virtuale personalizzata.</span><span class="sxs-lookup"><span data-stu-id="6fbec-123">hello following steps show how toouse hello Azure CLI toodeploy a SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM from hello Azure Marketplace, customize it, and create a custom VM image.</span></span> <span data-ttu-id="6fbec-124">È quindi possibile utilizzare hello immagine tooscript hello la distribuzione di un cluster di macchine virtuali che supportano RDMA.</span><span class="sxs-lookup"><span data-stu-id="6fbec-124">Then you can use hello image tooscript hello deployment of a cluster of RDMA-capable VMs.</span></span>

> [!TIP]
> <span data-ttu-id="6fbec-125">Utilizzare un cluster di macchine virtuali che supportano RDMA in base alle immagini basate su CentOS HPC in Azure Marketplace hello simile toodeploy di passaggi.</span><span class="sxs-lookup"><span data-stu-id="6fbec-125">Use similar steps toodeploy a cluster of RDMA-capable VMs based on CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="6fbec-126">Come indicato, alcuni passaggi variano leggermente.</span><span class="sxs-lookup"><span data-stu-id="6fbec-126">Some steps differ slightly, as noted.</span></span> 
>
>

### <a name="prerequisites"></a><span data-ttu-id="6fbec-127">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6fbec-127">Prerequisites</span></span>
* <span data-ttu-id="6fbec-128">**Computer client**: È necessario un toocommunicate di computer client di Windows, Linux o Mac con Azure.</span><span class="sxs-lookup"><span data-stu-id="6fbec-128">**Client computer**: You need a Mac, Linux, or Windows client computer toocommunicate with Azure.</span></span> <span data-ttu-id="6fbec-129">Nella procedura si presuppone che venga usato un client Linux.</span><span class="sxs-lookup"><span data-stu-id="6fbec-129">These steps assume you are using a Linux client.</span></span>
* <span data-ttu-id="6fbec-130">**Sottoscrizione di Azure**: se non è disponibile una sottoscrizione, è possibile creare un [account gratuito](https://azure.microsoft.com/free/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="6fbec-130">**Azure subscription**: If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span> <span data-ttu-id="6fbec-131">Per cluster di maggiori dimensioni, prendere in considerazione una sottoscrizione con pagamento in base al consumo o altre opzioni di acquisto.</span><span class="sxs-lookup"><span data-stu-id="6fbec-131">For larger clusters, consider a pay-as-you-go subscription or other purchase options.</span></span>
* <span data-ttu-id="6fbec-132">**Disponibilità di dimensioni VM**: hello seguendo le dimensioni di istanza è in grado di supportare RDMA: H16r, H16mr, A8 e A9.</span><span class="sxs-lookup"><span data-stu-id="6fbec-132">**VM size availability**: hello following instance sizes are RDMA capable: H16r, H16mr, A8, and A9.</span></span> <span data-ttu-id="6fbec-133">Per informazioni sulla disponibilità nelle aree di Azure, vedere [Prodotti disponibili in base all'area](https://azure.microsoft.com/regions/services/) .</span><span class="sxs-lookup"><span data-stu-id="6fbec-133">Check [Products available by region](https://azure.microsoft.com/regions/services/) for availability in Azure regions.</span></span>
* <span data-ttu-id="6fbec-134">**Quota di core**: potrebbe essere necessario quota hello tooincrease di core toodeploy un cluster di macchine virtuali con utilizzo intensivo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="6fbec-134">**Cores quota**: You might need tooincrease hello quota of cores toodeploy a cluster of compute-intensive VMs.</span></span> <span data-ttu-id="6fbec-135">Ad esempio, è necessario disporre di almeno 128 core se si desidera che le macchine virtuali A9 toodeploy 8 come illustrato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="6fbec-135">For example, you need at least 128 cores if you want toodeploy 8 A9 VMs as shown in this article.</span></span> <span data-ttu-id="6fbec-136">La sottoscrizione anche potrebbe limitare il numero di hello di core, che è possibile distribuire in determinati gruppi di dimensioni macchina virtuale incluso hello H serie.</span><span class="sxs-lookup"><span data-stu-id="6fbec-136">Your subscription might also limit hello number of cores you can deploy in certain VM size families, including hello H-series.</span></span> <span data-ttu-id="6fbec-137">aumentare la quota toorequest, [aprire una richiesta di supporto clienti online](../../../azure-supportability/how-to-create-azure-support-request.md) senza alcun costo.</span><span class="sxs-lookup"><span data-stu-id="6fbec-137">toorequest a quota increase, [open an online customer support request](../../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
* <span data-ttu-id="6fbec-138">**CLI di Azure**: [installare](../../../cli-install-nodejs.md) hello Azure CLI e [tooyour sottoscrizione di Azure connettersi](../../../xplat-cli-connect.md) da computer client hello.</span><span class="sxs-lookup"><span data-stu-id="6fbec-138">**Azure CLI**: [Install](../../../cli-install-nodejs.md) hello Azure CLI and [connect tooyour Azure subscription](../../../xplat-cli-connect.md) from hello client computer.</span></span>

### <a name="provision-an-sles-12-sp1-hpc-vm"></a><span data-ttu-id="6fbec-139">Provisioning di una macchina virtuale HPC SLES 12 SP1</span><span class="sxs-lookup"><span data-stu-id="6fbec-139">Provision an SLES 12 SP1 HPC VM</span></span>
<span data-ttu-id="6fbec-140">Dopo aver effettuato l'accesso tooAzure con hello CLI di Azure, eseguire `azure config list` tooconfirm che hello l'output mostra la modalità di gestione del servizio.</span><span class="sxs-lookup"><span data-stu-id="6fbec-140">After signing in tooAzure with hello Azure CLI, run `azure config list` tooconfirm that hello output shows Service Management mode.</span></span> <span data-ttu-id="6fbec-141">In caso contrario, impostare la modalità hello eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="6fbec-141">If it does not, set hello mode by running this command:</span></span>

    azure config mode asm


<span data-ttu-id="6fbec-142">Digitare hello seguente toolist tutte le sottoscrizioni di hello si è autorizzati toouse:</span><span class="sxs-lookup"><span data-stu-id="6fbec-142">Type hello following toolist all hello subscriptions you are authorized toouse:</span></span>

    azure account list

<span data-ttu-id="6fbec-143">sottoscrizione attiva corrente Hello viene identificato con `Current` impostare troppo`true`.</span><span class="sxs-lookup"><span data-stu-id="6fbec-143">hello current active subscription is identified with `Current` set too`true`.</span></span> <span data-ttu-id="6fbec-144">Se la sottoscrizione non hello quello che si desidera toouse toocreate hello cluster, impostare l'ID di sottoscrizione appropriata hello come sottoscrizione attiva hello:</span><span class="sxs-lookup"><span data-stu-id="6fbec-144">If this subscription isn't hello one you want toouse toocreate hello cluster, set hello appropriate subscription ID as hello active subscription:</span></span>

    azure account set <subscription-Id>

<span data-ttu-id="6fbec-145">toosee hello disponibile pubblicamente immagini SLES 12 SP1 HPC in Azure, eseguire un comando simile hello segue, presupponendo che l'ambiente della shell offre il supporto **grep**:</span><span class="sxs-lookup"><span data-stu-id="6fbec-145">toosee hello publicly available SLES 12 SP1 HPC images in Azure, run a command like hello following, assuming your shell environment supports **grep**:</span></span>

    azure vm image list | grep "suse.*hpc"

<span data-ttu-id="6fbec-146">Eseguire il provisioning di una macchina virtuale che supportano RDMA con un'immagine SLES 12 SP1 HPC eseguendo un comando simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="6fbec-146">Provision an RDMA-capable VM with a SLES 12 SP1 HPC image by running a command like hello following:</span></span>

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

<span data-ttu-id="6fbec-147">Dove:</span><span class="sxs-lookup"><span data-stu-id="6fbec-147">Where:</span></span>

* <span data-ttu-id="6fbec-148">Hello dimensioni (in questo esempio, A9) è una delle dimensioni delle macchine Virtuali che supportano RDMA hello.</span><span class="sxs-lookup"><span data-stu-id="6fbec-148">hello size (A9 in this example) is one of hello RDMA-capable VM sizes.</span></span>
* <span data-ttu-id="6fbec-149">numero di porta esterna SSH Hello (22 in questo esempio è hello SSH predefinito) è qualsiasi numero di porta valido.</span><span class="sxs-lookup"><span data-stu-id="6fbec-149">hello external SSH port number (22 in this example, which is hello SSH default) is any valid port number.</span></span> <span data-ttu-id="6fbec-150">numero di porta SSH interno Hello è impostato too22.</span><span class="sxs-lookup"><span data-stu-id="6fbec-150">hello internal SSH port number is set too22.</span></span>
* <span data-ttu-id="6fbec-151">Un nuovo servizio cloud viene creato in hello specificato dal percorso hello regione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6fbec-151">A new cloud service is created in hello Azure region specified by hello location.</span></span> <span data-ttu-id="6fbec-152">Specificare un percorso in cui hello VM dimensione che scelto è disponibile.</span><span class="sxs-lookup"><span data-stu-id="6fbec-152">Specify a location in which hello VM size you choose is available.</span></span>
* <span data-ttu-id="6fbec-153">Per il supporto per le priorità SUSE (che comporta costi aggiuntivi), nome dell'immagine hello SLES 12 SP1 attualmente può essere una di queste due opzioni:</span><span class="sxs-lookup"><span data-stu-id="6fbec-153">For SUSE priority support (which incurs additional charges), hello SLES 12 SP1 image name currently can be one of these two options:</span></span> 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-hello-vm"></a><span data-ttu-id="6fbec-154">Personalizzare hello VM</span><span class="sxs-lookup"><span data-stu-id="6fbec-154">Customize hello VM</span></span>
<span data-ttu-id="6fbec-155">Al termine hello VM provisioning, SSH toohello VM utilizzando hello l'indirizzo IP esterno della macchina virtuale (o nome DNS) e hello numero di porta esterna configurato e quindi personalizzarlo.</span><span class="sxs-lookup"><span data-stu-id="6fbec-155">After hello VM finishes provisioning, SSH toohello VM by using hello VM's external IP address (or DNS name) and hello external port number you configured, and then customize it.</span></span> <span data-ttu-id="6fbec-156">Per informazioni di connessione, vedere [come toolog nella macchina virtuale tooa che eseguono Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6fbec-156">For connection details, see [How toolog on tooa virtual machine running Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="6fbec-157">Eseguire i comandi come utente hello che è configurato su hello macchina virtuale, a meno che l'accesso alla directory radice è necessario toocomplete un passaggio.</span><span class="sxs-lookup"><span data-stu-id="6fbec-157">Perform commands as hello user you configured on hello VM, unless root access is required toocomplete a step.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6fbec-158">Microsoft Azure non fornisce accesso alla directory radice tooLinux VM.</span><span class="sxs-lookup"><span data-stu-id="6fbec-158">Microsoft Azure does not provide root access tooLinux VMs.</span></span> <span data-ttu-id="6fbec-159">toogain accesso amministrativo quando si è connessi come un toohello utente macchina virtuale, eseguita i comandi tramite `sudo`.</span><span class="sxs-lookup"><span data-stu-id="6fbec-159">toogain administrative access when connected as a user toohello VM, run commands by using `sudo`.</span></span>
>
>

* <span data-ttu-id="6fbec-160">**Aggiornamenti**: installare gli aggiornamenti usando zypper.</span><span class="sxs-lookup"><span data-stu-id="6fbec-160">**Updates**: Install updates by using zypper.</span></span> <span data-ttu-id="6fbec-161">È inoltre possibile utilità NFS tooinstall.</span><span class="sxs-lookup"><span data-stu-id="6fbec-161">You might also want tooinstall NFS utilities.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="6fbec-162">In una VM di HPC SLES 12 SP1, è consigliabile non applicare gli aggiornamenti del kernel, che possono causare problemi con hello Linux RDMA driver.</span><span class="sxs-lookup"><span data-stu-id="6fbec-162">In a SLES 12 SP1 HPC VM, we recommend that you don't apply kernel updates, which can cause issues with hello Linux RDMA drivers.</span></span>
  >
  >
* <span data-ttu-id="6fbec-163">**Intel MPI**: completare l'installazione di hello di Intel MPI su hello SLES 12 SP1 HPC VM eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6fbec-163">**Intel MPI**: Complete hello installation of Intel MPI on hello SLES 12 SP1 HPC VM by running hello following command:</span></span>

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* <span data-ttu-id="6fbec-164">**Bloccare la memoria**: per MPI codici toolock hello memoria disponibile per RDMA, aggiungere o modificare hello seguendo le impostazioni nel file /etc/security/limits.conf hello.</span><span class="sxs-lookup"><span data-stu-id="6fbec-164">**Lock memory**: For MPI codes toolock hello memory available for RDMA, add or change hello following settings in hello /etc/security/limits.conf file.</span></span> <span data-ttu-id="6fbec-165">È necessario tooedit accesso principale di questo file.</span><span class="sxs-lookup"><span data-stu-id="6fbec-165">You need root access tooedit this file.</span></span>

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > <span data-ttu-id="6fbec-166">A scopo di test, è anche possibile impostare memlock toounlimited.</span><span class="sxs-lookup"><span data-stu-id="6fbec-166">For testing purposes, you can also set memlock toounlimited.</span></span> <span data-ttu-id="6fbec-167">Ad esempio: `<User or group name>    hard    memlock unlimited`.</span><span class="sxs-lookup"><span data-stu-id="6fbec-167">For example: `<User or group name>    hard    memlock unlimited`.</span></span> <span data-ttu-id="6fbec-168">Per altre informazioni, vedere [Metodi noti per l'impostazione delle dimensioni della memoria bloccata](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span><span class="sxs-lookup"><span data-stu-id="6fbec-168">For more information, see [Best known methods for setting locked memory size](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span></span>
  >
  >
* <span data-ttu-id="6fbec-169">**Le chiavi SSH per le macchine virtuali SLES**: generare SSH chiavi tooestablish attendibilità per l'account utente di hello nodi di calcolo nel cluster SLES hello durante l'esecuzione di processi MPI.</span><span class="sxs-lookup"><span data-stu-id="6fbec-169">**SSH keys for SLES VMs**: Generate SSH keys tooestablish trust for your user account among hello compute nodes in hello SLES cluster when running MPI jobs.</span></span> <span data-ttu-id="6fbec-170">Se è stata distribuita una macchina virtuale HPC basata su CentOS, non seguire questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="6fbec-170">If you deployed a CentOS-based HPC VM, don't follow this step.</span></span> <span data-ttu-id="6fbec-171">Dopo aver acquisito immagine hello e distribuire hello cluster, vedere le istruzioni più avanti in questo articolo di tooset di passwordless SSH trust tra i nodi del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6fbec-171">See instructions later in this article tooset up passwordless SSH trust among hello cluster nodes after you capture hello image and deploy hello cluster.</span></span>

    <span data-ttu-id="6fbec-172">chiavi SSH toocreate, eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="6fbec-172">toocreate SSH keys, run hello following command.</span></span> <span data-ttu-id="6fbec-173">Quando viene richiesto per l'input, selezionare **invio** chiavi hello toogenerate nel percorso predefinito di hello senza impostare una password.</span><span class="sxs-lookup"><span data-stu-id="6fbec-173">When you are prompted for input, select **Enter** toogenerate hello keys in hello default location without setting a password.</span></span>

        ssh-keygen

    <span data-ttu-id="6fbec-174">Accodare il file authorized_keys toohello chiave pubblica di hello per le chiavi pubbliche note.</span><span class="sxs-lookup"><span data-stu-id="6fbec-174">Append hello public key toohello authorized_keys file for known public keys.</span></span>

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    <span data-ttu-id="6fbec-175">Nella directory ~/.ssh hello, modificare o creare file di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="6fbec-175">In hello ~/.ssh directory, edit or create hello config file.</span></span> <span data-ttu-id="6fbec-176">Fornire intervallo di indirizzi IP hello della rete privata hello pianificare toouse in Azure (10.32.0.0/16 in questo esempio):</span><span class="sxs-lookup"><span data-stu-id="6fbec-176">Provide hello IP address range of hello private network that you plan toouse in Azure (10.32.0.0/16 in this example):</span></span>

        host 10.32.0.*
        StrictHostKeyChecking no

    <span data-ttu-id="6fbec-177">In alternativa, elenco indirizzo IP di rete privata hello di ogni macchina virtuale del cluster come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6fbec-177">Alternatively, list hello private network IP address of each VM in your cluster as follows:</span></span>

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > <span data-ttu-id="6fbec-178">La configurazione di `StrictHostKeyChecking no` può creare un potenziale rischio di sicurezza quando non viene specificato un intervallo o un indirizzo IP specifico.</span><span class="sxs-lookup"><span data-stu-id="6fbec-178">Configuring `StrictHostKeyChecking no` can create a potential security risk when a specific IP address or range is not specified.</span></span>
  >
  >
* <span data-ttu-id="6fbec-179">**Applicazioni**: installare le applicazioni, è necessario o eseguire altre personalizzazioni prima di acquisire l'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="6fbec-179">**Applications**: Install any applications you need or perform other customizations before you capture hello image.</span></span>

### <a name="capture-hello-image"></a><span data-ttu-id="6fbec-180">Acquisire l'immagine di hello</span><span class="sxs-lookup"><span data-stu-id="6fbec-180">Capture hello image</span></span>
<span data-ttu-id="6fbec-181">immagine di hello toocapture, eseguire innanzitutto hello comando seguente in hello VM Linux.</span><span class="sxs-lookup"><span data-stu-id="6fbec-181">toocapture hello image, first run hello following command on hello Linux VM.</span></span> <span data-ttu-id="6fbec-182">Questo comando annullamento del provisioning hello VM ma mantiene gli account utente e le chiavi SSH impostati.</span><span class="sxs-lookup"><span data-stu-id="6fbec-182">This command deprovisions hello VM but maintains user accounts and SSH keys that you set up.</span></span>

```
sudo waagent -deprovision
```

<span data-ttu-id="6fbec-183">Dal computer client eseguire hello seguente immagine di hello toocapture comandi CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="6fbec-183">From your client computer, run hello following Azure CLI commands toocapture hello image.</span></span> <span data-ttu-id="6fbec-184">Per ulteriori informazioni, vedere [come una macchina virtuale di Linux classica come immagine toocapture](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="6fbec-184">For more information, see [How toocapture a classic Linux virtual machine as an image](capture-image.md).</span></span>  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

<span data-ttu-id="6fbec-185">Dopo aver eseguito questi comandi, immagine di macchina virtuale hello viene acquisito per l'uso e hello VM viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="6fbec-185">After you run these commands, hello VM image is captured for your use and hello VM is deleted.</span></span> <span data-ttu-id="6fbec-186">Ora è disponibile il toodeploy pronto immagine personalizzata un cluster.</span><span class="sxs-lookup"><span data-stu-id="6fbec-186">Now you have your custom image ready toodeploy a cluster.</span></span>

### <a name="deploy-a-cluster-with-hello-image"></a><span data-ttu-id="6fbec-187">Distribuire un cluster con immagine di hello</span><span class="sxs-lookup"><span data-stu-id="6fbec-187">Deploy a cluster with hello image</span></span>
<span data-ttu-id="6fbec-188">Modificare lo script Bash con valori appropriati per l'ambiente seguente hello ed eseguirlo dal computer client.</span><span class="sxs-lookup"><span data-stu-id="6fbec-188">Modify hello following Bash script with appropriate values for your environment and run it from your client computer.</span></span> <span data-ttu-id="6fbec-189">Poiché Azure consente di distribuire macchine virtuali di hello in sequenza nel modello di distribuzione classica hello, sono necessari alcuni minuti toodeploy hello otto macchine virtuali A9 suggerite in questo script.</span><span class="sxs-lookup"><span data-stu-id="6fbec-189">Because Azure deploys hello VMs serially in hello classic deployment model, it takes a few minutes toodeploy hello eight A9 VMs suggested in this script.</span></span>

```
#!/bin/bash -x
# Script toocreate a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where hello VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All hello compute-intensive instances need toobe in hello same cloud service for Linux RDMA toowork across InfiniBand.
# Note: hello current maximum number of VMs in a cloud service is 50. If you need tooprovision more than 50 VMs in hello same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want tooturn off external ports and use only internal ports toocommunicate between compute nodes via port 22, don’t use this option. Since port numbers up too10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 toocluster18. Specify your captured image in <image-name>. Specify hello username and password you used when creating hello SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment tooprovision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a><span data-ttu-id="6fbec-190">Considerazioni per un cluster HPC CentOS</span><span class="sxs-lookup"><span data-stu-id="6fbec-190">Considerations for a CentOS HPC cluster</span></span>
<span data-ttu-id="6fbec-191">Se si vuole tooset di un cluster basato su una delle immagini basate su CentOS HPC hello in hello Azure Marketplace anziché SLES 12 per HPC, seguire i passaggi generali hello hello precedente sezione.</span><span class="sxs-lookup"><span data-stu-id="6fbec-191">If you want tooset up a cluster based on one of hello CentOS-based HPC images in hello Azure Marketplace instead of SLES 12 for HPC, follow hello general steps in hello preceding section.</span></span> <span data-ttu-id="6fbec-192">Si noti hello seguenti differenze. effettuare il provisioning e configurare hello VM:</span><span class="sxs-lookup"><span data-stu-id="6fbec-192">Note hello following differences when you provision and configure hello VM:</span></span>

- <span data-ttu-id="6fbec-193">Intel MPI è già installato in una macchina virtuale con provisioning da un'immagine HPC basata su CentOS.</span><span class="sxs-lookup"><span data-stu-id="6fbec-193">Intel MPI is already installed on a VM provisioned from a CentOS-based HPC image.</span></span>
- <span data-ttu-id="6fbec-194">Le impostazioni della memoria di blocco già aggiunti nel file /etc/security/limits.conf hello della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6fbec-194">Lock memory settings are already added in hello VM's /etc/security/limits.conf file.</span></span>
- <span data-ttu-id="6fbec-195">Non generare le chiavi SSH in hello VM viene effettuato il provisioning per l'acquisizione.</span><span class="sxs-lookup"><span data-stu-id="6fbec-195">Do not generate SSH keys on hello VM you provision for capture.</span></span> <span data-ttu-id="6fbec-196">È invece consigliabile configurare l'autenticazione basata su utente dopo la distribuzione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6fbec-196">Instead, we recommend setting up user-based authentication after you deploy hello cluster.</span></span> <span data-ttu-id="6fbec-197">Per ulteriori informazioni, vedere hello seguente sezione.</span><span class="sxs-lookup"><span data-stu-id="6fbec-197">For more information, see hello following section.</span></span>  

### <a name="set-up-passwordless-ssh-trust-on-hello-cluster"></a><span data-ttu-id="6fbec-198">Configurare passwordless trust SSH nel cluster hello</span><span class="sxs-lookup"><span data-stu-id="6fbec-198">Set up passwordless SSH trust on hello cluster</span></span>
<span data-ttu-id="6fbec-199">In un cluster HPC basato su CentOS, sono disponibili due metodi per stabilire il trust tra i nodi di calcolo hello: l'autenticazione basata su host e l'autenticazione basata sull'utente.</span><span class="sxs-lookup"><span data-stu-id="6fbec-199">On a CentOS-based HPC cluster, there are two methods for establishing trust between hello compute nodes: host-based authentication and user-based authentication.</span></span> <span data-ttu-id="6fbec-200">L'autenticazione basata su host esula dall'ambito di hello di questo articolo e in genere deve essere eseguita tramite uno script di estensione durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="6fbec-200">Host-based authentication is outside of hello scope of this article and generally must be done through an extension script during deployment.</span></span> <span data-ttu-id="6fbec-201">L'autenticazione basata su utente è utile per stabilire il trust dopo la distribuzione e richiede la generazione di hello e la condivisione di chiavi SSH tra hello nodi di calcolo nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6fbec-201">User-based authentication is convenient for establishing trust after deployment and requires hello generation and sharing of SSH keys among hello compute nodes in hello cluster.</span></span> <span data-ttu-id="6fbec-202">Questo metodo è comunemente noto come accesso SSH senza password ed è obbligatorio quando si eseguono processi MPI.</span><span class="sxs-lookup"><span data-stu-id="6fbec-202">This method is commonly known as passwordless SSH login and is required when running MPI jobs.</span></span>

<span data-ttu-id="6fbec-203">È disponibile in uno script di esempio fornito dalla community di hello [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable l'autenticazione utente semplice in un cluster basato su CentOS HPC.</span><span class="sxs-lookup"><span data-stu-id="6fbec-203">A sample script contributed from hello community is available on [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable easy user authentication on a CentOS-based HPC cluster.</span></span> <span data-ttu-id="6fbec-204">Scaricare e usare questo script usando hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="6fbec-204">Download and use this script by using hello following steps.</span></span> <span data-ttu-id="6fbec-205">È inoltre possibile modificare lo script o usare qualsiasi altro metodo tooestablish passwordless autenticazione SSH tra i nodi di calcolo cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6fbec-205">You can also modify this script or use any other method tooestablish passwordless SSH authentication between hello cluster compute nodes.</span></span>

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

<span data-ttu-id="6fbec-206">script di hello toorun, è necessario prefisso hello tooknow per gli indirizzi IP di subnet.</span><span class="sxs-lookup"><span data-stu-id="6fbec-206">toorun hello script, you need tooknow hello prefix for your subnet IP addresses.</span></span> <span data-ttu-id="6fbec-207">Ottenere il prefisso hello eseguendo hello comando seguente in uno dei nodi del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6fbec-207">Get hello prefix by running hello following command on one of hello cluster nodes.</span></span> <span data-ttu-id="6fbec-208">L'output dovrebbe essere simile al seguente 10.1.3.5 e prefisso hello è parte di hello 10.1.3.</span><span class="sxs-lookup"><span data-stu-id="6fbec-208">Your output should look something like 10.1.3.5, and hello prefix is hello 10.1.3 portion.</span></span>

    ifconfig eth0 | grep -w inet | awk '{print $2}'

<span data-ttu-id="6fbec-209">A questo punto eseguire script hello utilizzando tre parametri: hello comuni nel nome utente hello nodi di calcolo, di password comuni hello per nodi di calcolo di tale utente per hello e prefisso di subnet di hello che è stata restituita dal comando precedente hello.</span><span class="sxs-lookup"><span data-stu-id="6fbec-209">Now run hello script using three parameters: hello common user name on hello compute nodes, hello common password for that user on hello compute nodes, and hello subnet prefix that was returned from hello previous command.</span></span>

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

<span data-ttu-id="6fbec-210">Questo script hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="6fbec-210">This script does hello following:</span></span>

* <span data-ttu-id="6fbec-211">Crea una directory nel nodo host hello denominato .ssh, che è necessario per l'account di accesso passwordless.</span><span class="sxs-lookup"><span data-stu-id="6fbec-211">Creates a directory on hello host node named .ssh, which is required for passwordless login.</span></span>
* <span data-ttu-id="6fbec-212">Crea un file di configurazione nella directory .ssh hello che indica l'account di accesso tooallow passwordless account di accesso da qualsiasi nodo nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6fbec-212">Creates a configuration file in hello .ssh directory that instructs passwordless login tooallow login from any node in hello cluster.</span></span>
* <span data-ttu-id="6fbec-213">Crea i file contenenti i nomi dei nodi di hello e gli indirizzi IP di nodo per tutti i nodi nel cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="6fbec-213">Creates files containing hello node names and node IP addresses for all hello nodes in hello cluster.</span></span> <span data-ttu-id="6fbec-214">Questi file vengono lasciati dopo l'esecuzione di script hello per riferimento futuro.</span><span class="sxs-lookup"><span data-stu-id="6fbec-214">These files are left after hello script is run for later reference.</span></span>
* <span data-ttu-id="6fbec-215">Crea una coppia di chiavi pubblica e privata per ogni nodo del cluster (inclusi nodo host hello) e crea voci nel file authorized_keys hello.</span><span class="sxs-lookup"><span data-stu-id="6fbec-215">Creates a private and public key pair for each cluster node (including hello host node) and creates entries in hello authorized_keys file.</span></span>

> [!WARNING]
> <span data-ttu-id="6fbec-216">L'esecuzione di questo script può creare un potenziale rischio per la sicurezza.</span><span class="sxs-lookup"><span data-stu-id="6fbec-216">Running this script can create a potential security risk.</span></span> <span data-ttu-id="6fbec-217">Verificare che informazioni sulle chiavi pubbliche hello in ~/.ssh non viene distribuite.</span><span class="sxs-lookup"><span data-stu-id="6fbec-217">Ensure that hello public key information in ~/.ssh is not distributed.</span></span>
>
>

## <a name="configure-intel-mpi"></a><span data-ttu-id="6fbec-218">Configurare Intel MPI</span><span class="sxs-lookup"><span data-stu-id="6fbec-218">Configure Intel MPI</span></span>
<span data-ttu-id="6fbec-219">toorun di applicazioni MPI in Azure Linux RDMA, è necessario tooconfigure determinati tooIntel specifico MPI variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="6fbec-219">toorun MPI applications on Azure Linux RDMA, you need tooconfigure certain environment variables specific tooIntel MPI.</span></span> <span data-ttu-id="6fbec-220">Ecco un toorun hello variabili necessite tooconfigure script di esempio Bash un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6fbec-220">Here is a sample Bash script tooconfigure hello variables needed toorun an application.</span></span> <span data-ttu-id="6fbec-221">Modificare toompivars.sh percorso hello in base alle esigenze per l'installazione di Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="6fbec-221">Change hello path toompivars.sh as needed for your installation of Intel MPI.</span></span>

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting hello variable tooshm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line toorun hello job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path toohello application exe> <arguments specific toohello application>

#end
```

<span data-ttu-id="6fbec-222">formato di Hello del file host hello è come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="6fbec-222">hello format of hello host file is as follows.</span></span> <span data-ttu-id="6fbec-223">Aggiungere una riga per ciascun nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="6fbec-223">Add one line for each node in your cluster.</span></span> <span data-ttu-id="6fbec-224">Specificare gli indirizzi IP privati da rete virtuale hello definita in precedenza, non i nomi DNS.</span><span class="sxs-lookup"><span data-stu-id="6fbec-224">Specify private IP addresses from hello virtual network defined earlier, not DNS names.</span></span> <span data-ttu-id="6fbec-225">Ad esempio, per due host con gli indirizzi IP 10.32.0.1 e 10.32.0.2, file hello contiene seguente hello:</span><span class="sxs-lookup"><span data-stu-id="6fbec-225">For example, for two hosts with IP addresses 10.32.0.1 and 10.32.0.2, hello file contains hello following:</span></span>

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a><span data-ttu-id="6fbec-226">Eseguire MPI su un cluster di base a due nodi</span><span class="sxs-lookup"><span data-stu-id="6fbec-226">Run MPI on a basic two-node cluster</span></span>
<span data-ttu-id="6fbec-227">Se non già stato fatto, innanzitutto impostare hello ambiente per Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="6fbec-227">If you haven't already done so, first set up hello environment for Intel MPI.</span></span>

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a><span data-ttu-id="6fbec-228">Eseguire un comando MPI</span><span class="sxs-lookup"><span data-stu-id="6fbec-228">Run an MPI command</span></span>
<span data-ttu-id="6fbec-229">Eseguire un comando MPI in uno dei tooshow di nodi di calcolo hello MPI sia installato correttamente e possono comunicare tra almeno due nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="6fbec-229">Run an MPI command on one of hello compute nodes tooshow that MPI is installed properly and can communicate between at least two compute nodes.</span></span> <span data-ttu-id="6fbec-230">esempio Hello **mpirun** comando esegue hello **hostname** comando due nodi.</span><span class="sxs-lookup"><span data-stu-id="6fbec-230">hello following **mpirun** command runs hello **hostname** command on two nodes.</span></span>

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
<span data-ttu-id="6fbec-231">L'output deve includere nomi di hello di tutti i nodi di hello che è stato passato come input per `-hosts`.</span><span class="sxs-lookup"><span data-stu-id="6fbec-231">Your output should list hello names of all hello nodes that you passed as input for `-hosts`.</span></span> <span data-ttu-id="6fbec-232">Ad esempio, un **mpirun** comando con due nodi restituisce un output simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="6fbec-232">For example, an **mpirun** command with two nodes returns output like hello following:</span></span>

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a><span data-ttu-id="6fbec-233">Eseguire un benchmark MPI</span><span class="sxs-lookup"><span data-stu-id="6fbec-233">Run an MPI benchmark</span></span>
<span data-ttu-id="6fbec-234">Hello Intel MPI comando seguente esegue una pingpong benchmark tooverify hello configurazione e connessione toohello RDMA rete cluster.</span><span class="sxs-lookup"><span data-stu-id="6fbec-234">hello following Intel MPI command runs a pingpong benchmark tooverify hello cluster configuration and connection toohello RDMA network.</span></span>

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

<span data-ttu-id="6fbec-235">In un cluster di lavoro con due nodi, si dovrebbe vedere l'output seguente hello.</span><span class="sxs-lookup"><span data-stu-id="6fbec-235">On a working cluster with two nodes, you should see output like hello following.</span></span> <span data-ttu-id="6fbec-236">In hello rete RDMA di Azure, prevede latenza inferiore o uguale a 3 microsecondi per le dimensioni dei messaggi too512 byte.</span><span class="sxs-lookup"><span data-stu-id="6fbec-236">On hello Azure RDMA network, expect latency at or below 3 microseconds for message sizes up too512 bytes.</span></span>

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
# hello number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected toobe exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through hello flag => -time

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
# List of Benchmarks toorun:
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



## <a name="next-steps"></a><span data-ttu-id="6fbec-237">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6fbec-237">Next steps</span></span>
* <span data-ttu-id="6fbec-238">Distribuire ed eseguire le applicazioni MPI Linux nel cluster Linux.</span><span class="sxs-lookup"><span data-stu-id="6fbec-238">Deploy and run your Linux MPI applications on your Linux cluster.</span></span>
* <span data-ttu-id="6fbec-239">Vedere hello [documentazione libreria MPI Intel](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) per informazioni aggiuntive sul Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="6fbec-239">See hello [Intel MPI Library documentation](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) for guidance on Intel MPI.</span></span>
* <span data-ttu-id="6fbec-240">Provare un [modello delle Guide rapide](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate un lucentezza Intel cluster mediante un'immagine basata su CentOS HPC.</span><span class="sxs-lookup"><span data-stu-id="6fbec-240">Try a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate an Intel Lustre cluster by using a CentOS-based HPC image.</span></span> <span data-ttu-id="6fbec-241">Per informazioni dettagliate, vedere [Distribuzione di Intel Cloud Edition per Lustre in Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span><span class="sxs-lookup"><span data-stu-id="6fbec-241">For details, see [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span></span>
