---
title: aaaRun OpenFOAM con HPC Pack nelle macchine virtuali Linux | Documenti Microsoft
description: "Informazioni su come distribuire un cluster Microsoft HPC Pack in Azure ed eseguire un processo OpenFOAM in più nodi di calcolo Linux su una rete RDMA."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: 1a51ffe6804abb5156f01d580c9b7a4a9649377a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="32c1b-103">Eseguire OpenFoam con Microsoft HPC Pack in un cluster Linux RDMA in Azure</span><span class="sxs-lookup"><span data-stu-id="32c1b-103">Run OpenFoam with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="32c1b-104">Questo articolo illustra un modo toorun OpenFoam macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="32c1b-104">This article shows you one way toorun OpenFoam in Azure virtual machines.</span></span> <span data-ttu-id="32c1b-105">Viene distribuito un cluster Microsoft HPC Pack con nodi di calcolo Linux in Azure e viene eseguito un processo [OpenFoam](http://openfoam.com/) con Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="32c1b-105">Here, you deploy a Microsoft HPC Pack cluster with Linux compute nodes on Azure and run an [OpenFoam](http://openfoam.com/) job with Intel MPI.</span></span> <span data-ttu-id="32c1b-106">È possibile utilizzare macchine virtuali di Azure che supportano RDMA per nodi di calcolo hello, in modo che i nodi di calcolo hello comunicano su hello rete RDMA di Azure.</span><span class="sxs-lookup"><span data-stu-id="32c1b-106">You can use RDMA-capable Azure VMs for hello compute nodes, so that hello compute nodes communicate over hello Azure RDMA network.</span></span> <span data-ttu-id="32c1b-107">Altre opzioni toorun OpenFoam in Azure includono completamente configurato commerciale immagini disponibili in Marketplace, ad esempio del UberCloud hello [OpenFoam 2.3 CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/)e mediante l'esecuzione su [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span><span class="sxs-lookup"><span data-stu-id="32c1b-107">Other options toorun OpenFoam in Azure include fully configured commercial images available in hello Marketplace, such as UberCloud's [OpenFoam 2.3 on CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), and by running on [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="32c1b-108">OpenFOAM (Open Field Operation and Manipulation) è un pacchetto software di fluidodinamica computazionale (CFD) open source ampiamente usato in ambito ingegneristico e scientifico, in organizzazioni sia di tipo commerciale che accademico.</span><span class="sxs-lookup"><span data-stu-id="32c1b-108">OpenFOAM (for Open Field Operation and Manipulation) is an open-source computational fluid dynamics (CFD) software package that is used widely in engineering and science, in both commercial and academic organizations.</span></span> <span data-ttu-id="32c1b-109">Include strumenti per la generazione di mesh, ad esempio snappyHexMesh, uno strumento di generazione mesh parallelizzato per geometrie CAD complesse, per la pre e la post-elaborazione.</span><span class="sxs-lookup"><span data-stu-id="32c1b-109">It includes tools for meshing, notably snappyHexMesh, a parallelized mesher for complex CAD geometries, and for pre- and post-processing.</span></span> <span data-ttu-id="32c1b-110">Quasi tutti i processi eseguiti in parallelo, consentendo agli utenti tootake appieno hardware del computer a loro disposizione.</span><span class="sxs-lookup"><span data-stu-id="32c1b-110">Almost all processes run in parallel, enabling users tootake full advantage of computer hardware at their disposal.</span></span>  

<span data-ttu-id="32c1b-111">Microsoft HPC Pack fornisce funzionalità toorun HPC su larga scala e applicazioni parallele, incluse le applicazioni MPI, nei cluster di macchine virtuali di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="32c1b-111">Microsoft HPC Pack provides features toorun large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="32c1b-112">HPC Pack supporta anche applicazioni HPC che eseguono Linux su macchine virtuali del nodo di calcolo Linux distribuite in un cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="32c1b-112">HPC Pack also supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="32c1b-113">Vedere [Introduzione a Linux nodi di calcolo in un cluster HPC Pack in Azure](hpcpack-cluster.md) per un'introduzione toousing Linux nodi di calcolo di HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="32c1b-113">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction toousing Linux compute nodes with HPC Pack.</span></span>

> [!NOTE]
> <span data-ttu-id="32c1b-114">Questo articolo illustra come toorun un carico di lavoro Linux MPI con HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="32c1b-114">This article illustrates how toorun a Linux MPI workload with HPC Pack.</span></span> <span data-ttu-id="32c1b-115">e presuppone che l'utente abbia familiarità con l'amministrazione del sistema Linux e con l'esecuzione di carichi di lavoro MPI in cluster Linux.</span><span class="sxs-lookup"><span data-stu-id="32c1b-115">It assumes you have some familiarity with Linux system administration and with running MPI workloads on Linux clusters.</span></span> <span data-ttu-id="32c1b-116">Se si utilizzano versioni di MPI e OpenFOAM diversi da quelli illustrati in questo articolo hello, potrebbe essere toomodify alcuni passaggi di installazione e configurazione.</span><span class="sxs-lookup"><span data-stu-id="32c1b-116">If you use versions of MPI and OpenFOAM different from hello ones shown in this article, you might have toomodify some installation and configuration steps.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="32c1b-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="32c1b-117">Prerequisites</span></span>
* <span data-ttu-id="32c1b-118">**Cluster HPC Pack con nodi di calcolo con supporto per RDMA**: distribuire un cluster HPC Pack con nodi di calcolo Linux di dimensione A8, A9, H16r o H16rm usando un [modello di Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) o uno [script di Azure PowerShell](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="32c1b-118">**HPC Pack cluster with RDMA-capable Linux compute nodes** - Deploy an HPC Pack cluster with size A8, A9, H16r, or H16rm Linux compute nodes using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="32c1b-119">Vedere [Introduzione a Linux nodi di calcolo in un cluster HPC Pack in Azure](hpcpack-cluster.md) per hello prerequisiti e i passaggi per entrambe le opzioni.</span><span class="sxs-lookup"><span data-stu-id="32c1b-119">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for hello prerequisites and steps for either option.</span></span> <span data-ttu-id="32c1b-120">Se si sceglie l'opzione di distribuzione di script di PowerShell hello, vedere file di configurazione di esempio hello nei file di esempio hello alla fine di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="32c1b-120">If you choose hello PowerShell script deployment option, see hello sample configuration file in hello sample files at hello end of this article.</span></span> <span data-ttu-id="32c1b-121">Utilizzare questo cluster di HPC Pack toodeploy un basati su Azure configurazione costituito da un nodo head di dimensioni A8 Windows Server 2012 R2 e 2 dimensioni A8 SUSE Linux Enterprise Server 12 nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="32c1b-121">Use this configuration toodeploy an Azure-based HPC Pack cluster consisting of a size A8 Windows Server 2012 R2 head node and 2 size A8 SUSE Linux Enterprise Server 12 compute nodes.</span></span> <span data-ttu-id="32c1b-122">Sostituire i valori dell'esempio con i valori appropriati per la sottoscrizione e i nomi dei servizi.</span><span class="sxs-lookup"><span data-stu-id="32c1b-122">Substitute appropriate values for your subscription and service names.</span></span> 
  
  <span data-ttu-id="32c1b-123">**Ulteriori operazioni tooknow**</span><span class="sxs-lookup"><span data-stu-id="32c1b-123">**Additional things tooknow**</span></span>
  
  * <span data-ttu-id="32c1b-124">Per i prerequisiti della rete RDMA Linux in Azure, vedere [Dimensioni delle VM High Performance Computing (HPC)](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="32c1b-124">For Linux RDMA networking prerequisites in Azure, see [High performance compute VM sizes](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  * <span data-ttu-id="32c1b-125">Se si utilizza l'opzione di distribuzione di script di Powershell hello, distribuire tutti i nodi di calcolo di Linux hello all'interno di connessione di rete RDMA di un cloud servizio toouse hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-125">If you use hello Powershell script deployment option, deploy all hello Linux compute nodes within one cloud service toouse hello RDMA network connection.</span></span>
  * <span data-ttu-id="32c1b-126">Dopo aver distribuito i nodi di Linux hello, connessione SSH tooperform qualsiasi attività amministrative aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="32c1b-126">After deploying hello Linux nodes, connect by SSH tooperform any additional administrative tasks.</span></span> <span data-ttu-id="32c1b-127">Trovare i dettagli della connessione SSH hello per ogni VM Linux nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-127">Find hello SSH connection details for each Linux VM in hello Azure portal.</span></span>  
* <span data-ttu-id="32c1b-128">**Intel MPI** -toorun OpenFOAM su SLES 12 HPC nodi di calcolo in Azure, è necessario tooinstall hello Intel MPI libreria 5 runtime da hello [Intel.com sito](https://software.intel.com/en-us/intel-mpi-library/).</span><span class="sxs-lookup"><span data-stu-id="32c1b-128">**Intel MPI** - toorun OpenFOAM on SLES 12 HPC compute nodes in Azure, you need tooinstall hello Intel MPI Library 5 runtime from hello [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span></span> <span data-ttu-id="32c1b-129">(Intel MPI 5 è preinstallato nelle immagini HPC basate su CentOS).  Se necessario, in un passaggio successivo installare Intel MPI nei nodi di calcolo Linux.</span><span class="sxs-lookup"><span data-stu-id="32c1b-129">(Intel MPI 5 is preinstalled on CentOS-based HPC images.)  In a later step, if necessary, install Intel MPI on your Linux compute nodes.</span></span> <span data-ttu-id="32c1b-130">tooprepare per questo passaggio, dopo aver registrato con Intel, seguire il collegamento di hello in hello conferma tramite posta elettronica toohello correlati pagina web.</span><span class="sxs-lookup"><span data-stu-id="32c1b-130">tooprepare for this step, after you register with Intel, follow hello link in hello confirmation email toohello related web page.</span></span> <span data-ttu-id="32c1b-131">Quindi, hello Copia collegamento per il download per il file .tgz hello hello appropriata per versione di Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="32c1b-131">Then, copy hello download link for hello .tgz file for hello appropriate version of Intel MPI.</span></span> <span data-ttu-id="32c1b-132">Questo articolo si riferisce a Intel MPI versione 5.0.3.048.</span><span class="sxs-lookup"><span data-stu-id="32c1b-132">This article is based on Intel MPI version 5.0.3.048.</span></span>
* <span data-ttu-id="32c1b-133">**Service Pack di origine OpenFOAM** -scaricare il software di Service Pack di origine OpenFOAM hello per Linux da hello [sito OpenFOAM Foundation](http://openfoam.org/download/2-3-1-source/).</span><span class="sxs-lookup"><span data-stu-id="32c1b-133">**OpenFOAM Source Pack** - Download hello OpenFOAM Source Pack software for Linux from hello [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span></span> <span data-ttu-id="32c1b-134">In questo articolo viene usato Source Pack versione 2.3.1, disponibile per il download come OpenFOAM 2.3.1.tgz.</span><span class="sxs-lookup"><span data-stu-id="32c1b-134">This article is based on Source Pack version 2.3.1, available for download as OpenFOAM-2.3.1.tgz.</span></span> <span data-ttu-id="32c1b-135">Seguire le istruzioni di hello più avanti in questo articolo di toounpack e compilare OpenFOAM sui nodi di calcolo di hello Linux.</span><span class="sxs-lookup"><span data-stu-id="32c1b-135">Follow hello instructions later in this article toounpack and compile OpenFOAM on hello Linux compute nodes.</span></span>
* <span data-ttu-id="32c1b-136">**EnSight** (facoltativo): risultati hello toosee della simulazione di OpenFOAM, scaricare e installare hello [EnSight](https://www.ceisoftware.com/download/) programma di analisi e visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="32c1b-136">**EnSight** (optional) - toosee hello results of your OpenFOAM simulation, download and install hello [EnSight](https://www.ceisoftware.com/download/) visualization and analysis program.</span></span> <span data-ttu-id="32c1b-137">Informazioni sulla gestione delle licenze e download sono presso EnSight hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-137">Licensing and download information are at hello EnSight site.</span></span>

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="32c1b-138">Configurare il trust reciproco tra i nodi di calcolo</span><span class="sxs-lookup"><span data-stu-id="32c1b-138">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="32c1b-139">Esecuzione di un processo tra nodi in più nodi di Linux richiede hello nodi tootrust tra loro (da **rsh** o **ssh**).</span><span class="sxs-lookup"><span data-stu-id="32c1b-139">Running a cross-node job on multiple Linux nodes requires hello nodes tootrust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="32c1b-140">Quando si crea il cluster di HPC Pack hello con script di distribuzione IaaS di Microsoft HPC Pack hello, script hello imposta automaticamente permanente reciproca relazione di trust per l'account amministratore hello specificato.</span><span class="sxs-lookup"><span data-stu-id="32c1b-140">When you create hello HPC Pack cluster with hello Microsoft HPC Pack IaaS deployment script, hello script automatically sets up permanent mutual trust for hello administrator account you specify.</span></span> <span data-ttu-id="32c1b-141">Per gli utenti non amministratori creati nel dominio del cluster di hello, è possibile tooset temporaneo reciproca relazione di trust tra i nodi di hello quando un processo viene allocato toothem ed Elimina relazione hello dopo che viene completato il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-141">For non-administrator users you create in hello cluster's domain, you have tooset up temporary mutual trust among hello nodes when a job is allocated toothem, and destroy hello relationship after hello job is complete.</span></span> <span data-ttu-id="32c1b-142">trust tooestablish per ogni utente, fornire un cluster di toohello coppia di chiavi RSA utilizzata per la relazione di trust hello HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="32c1b-142">tooestablish trust for each user, provide an RSA key pair toohello cluster that HPC Pack uses for hello trust relationship.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="32c1b-143">Generare una coppia di chiavi RSA</span><span class="sxs-lookup"><span data-stu-id="32c1b-143">Generate an RSA key pair</span></span>
<span data-ttu-id="32c1b-144">È facile toogenerate una coppia di chiavi RSA, che contiene una chiave pubblica e una chiave privata, eseguendo hello Linux **ssh-keygen** comando.</span><span class="sxs-lookup"><span data-stu-id="32c1b-144">It's easy toogenerate an RSA key pair, which contains a public key and a private key, by running hello Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="32c1b-145">Accedere tooa computer Linux.</span><span class="sxs-lookup"><span data-stu-id="32c1b-145">Log on tooa Linux computer.</span></span>
2. <span data-ttu-id="32c1b-146">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="32c1b-146">Run hello following command:</span></span>
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="32c1b-147">Premere **invio** toouse impostazioni predefinite di hello fino a quando non viene completato hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-147">Press **Enter** toouse hello default settings until hello command is completed.</span></span> <span data-ttu-id="32c1b-148">Non immettere una passphrase. Quando viene richiesta una password, è sufficiente premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="32c1b-148">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Generare una coppia di chiavi RSA][keygen]
3. <span data-ttu-id="32c1b-150">Cambiare directory toohello ~/.ssh directory.</span><span class="sxs-lookup"><span data-stu-id="32c1b-150">Change directory toohello ~/.ssh directory.</span></span> <span data-ttu-id="32c1b-151">la chiave privata di Hello viene archiviata nella chiave pubblica id_rsa e hello id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="32c1b-151">hello private key is stored in id_rsa and hello public key in id_rsa.pub.</span></span>
   
   ![Chiavi pubbliche e private][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a><span data-ttu-id="32c1b-153">Aggiungere cluster HPC Pack toohello di hello coppia di chiavi</span><span class="sxs-lookup"><span data-stu-id="32c1b-153">Add hello key pair toohello HPC Pack cluster</span></span>
1. <span data-ttu-id="32c1b-154">Verificare un nodo head di tooyour connessione Desktop remoto con l'account administrator di HPC Pack (hello amministratore account configurato durante l'esecuzione di script di distribuzione hello).</span><span class="sxs-lookup"><span data-stu-id="32c1b-154">Make a Remote Desktop connection tooyour head node with your HPC Pack administrator account (hello administrator account you set up when you ran hello deployment script).</span></span>
2. <span data-ttu-id="32c1b-155">Usare toocreate procedure di Windows Server standard account utente di dominio nel dominio di Active Directory del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-155">Use standard Windows Server procedures toocreate a domain user account in hello cluster's Active Directory domain.</span></span> <span data-ttu-id="32c1b-156">Ad esempio, è possibile utilizzare hello utente di Active Directory e lo strumento di computer nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-156">For example, use hello Active Directory User and Computers tool on hello head node.</span></span> <span data-ttu-id="32c1b-157">esempi di Hello in questo articolo presuppongono che crei un utente di dominio denominato hpclab\hpcuser.</span><span class="sxs-lookup"><span data-stu-id="32c1b-157">hello examples in this article assume you create a domain user named hpclab\hpcuser.</span></span>
3. <span data-ttu-id="32c1b-158">Creare un file denominato C:\cred.xml e copia hello RSA dati della chiave al suo interno.</span><span class="sxs-lookup"><span data-stu-id="32c1b-158">Create a file named C:\cred.xml and copy hello RSA key data into it.</span></span> <span data-ttu-id="32c1b-159">Un file di esempio cred.xml è alla fine di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="32c1b-159">A sample cred.xml file is at hello end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. <span data-ttu-id="32c1b-160">Aprire un prompt dei comandi e immettere hello comando hello tooset credenziali dati per conto di hello hpclab\hpcuser seguente.</span><span class="sxs-lookup"><span data-stu-id="32c1b-160">Open a Command Prompt and enter hello following command tooset hello credentials data for hello hpclab\hpcuser account.</span></span> <span data-ttu-id="32c1b-161">Utilizzare hello **extendeddata** toopass parametro hello nome del file C:\cred.xml creato per i dati chiave hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-161">You use hello **extendeddata** parameter toopass hello name of C:\cred.xml file you created for hello key data.</span></span>
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="32c1b-162">Questo comando viene completato correttamente senza output.</span><span class="sxs-lookup"><span data-stu-id="32c1b-162">This command completes successfully without output.</span></span> <span data-ttu-id="32c1b-163">Dopo aver impostato le credenziali di hello per gli account utente di hello che è necessario toorun processi, archiviare file cred.xml hello in un percorso sicuro o eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="32c1b-163">After setting hello credentials for hello user accounts you need toorun jobs, store hello cred.xml file in a secure location, or delete it.</span></span>
5. <span data-ttu-id="32c1b-164">Se è stato generato hello coppia di chiavi RSA in uno dei nodi di Linux, tenere presente le chiavi di hello toodelete dopo aver terminato di utilizzare tali.</span><span class="sxs-lookup"><span data-stu-id="32c1b-164">If you generated hello RSA key pair on one of your Linux nodes, remember toodelete hello keys after you finish using them.</span></span> <span data-ttu-id="32c1b-165">Se HPC Pack rileva un file id_rsa o id_rsa.pub esistente, non configura il trust reciproco.</span><span class="sxs-lookup"><span data-stu-id="32c1b-165">If HPC Pack finds an existing id_rsa file or id_rsa.pub file, it does not set up mutual trust.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32c1b-166">Non è consigliabile eseguendo un processo di Linux come amministratore del cluster in un cluster condiviso, poiché viene eseguito un processo inviato da un amministratore account radice hello in nodi di Linux hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-166">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under hello root account on hello Linux nodes.</span></span> <span data-ttu-id="32c1b-167">Tuttavia, un processo inviato da un utente non amministratore viene eseguito con un account utente locale di Linux con hello stesso nome utente di un processo di hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-167">However, a job submitted by a non-administrator user runs under a local Linux user account with hello same name as hello job user.</span></span> <span data-ttu-id="32c1b-168">In questo caso, HPC Pack imposta reciproca relazione di trust per questo utente Linux tra nodi hello allocati toohello processo.</span><span class="sxs-lookup"><span data-stu-id="32c1b-168">In this case, HPC Pack sets up mutual trust for this Linux user across hello nodes allocated toohello job.</span></span> <span data-ttu-id="32c1b-169">È possibile impostare l'utente di Linux hello manualmente nei nodi di Linux hello prima di eseguire il processo di hello o HPC Pack Crea utente hello automaticamente quando il processo di hello viene inviato.</span><span class="sxs-lookup"><span data-stu-id="32c1b-169">You can set up hello Linux user manually on hello Linux nodes before running hello job, or HPC Pack creates hello user automatically when hello job is submitted.</span></span> <span data-ttu-id="32c1b-170">HPC Pack Crea utente hello, HPC Pack eliminata dopo il completamento del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-170">If HPC Pack creates hello user, HPC Pack deletes it after hello job completes.</span></span> <span data-ttu-id="32c1b-171">minacce per la sicurezza tooreduce, HPC Pack rimuove le chiavi di hello dopo il completamento del processo.</span><span class="sxs-lookup"><span data-stu-id="32c1b-171">tooreduce security threats, HPC Pack removes hello keys after job completion.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="32c1b-172">Configurare una condivisione di file per i nodi Linux</span><span class="sxs-lookup"><span data-stu-id="32c1b-172">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="32c1b-173">Ora si consiglia di configurare una condivisione SMB standard in una cartella nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-173">Now set up a standard SMB share on a folder on hello head node.</span></span> <span data-ttu-id="32c1b-174">tooallow hello Linux nodi tooaccess file dell'applicazione con un percorso comune, hello montaggio cartella nei nodi Linux hello condivisa.</span><span class="sxs-lookup"><span data-stu-id="32c1b-174">tooallow hello Linux nodes tooaccess application files with a common path, mount hello shared folder on hello Linux nodes.</span></span> <span data-ttu-id="32c1b-175">In alternativa, è possibile usare un'altra opzione di condivisione, ad esempio una condivisione File di Azure, consigliata per molti scenari, oppure una condivisione NFS.</span><span class="sxs-lookup"><span data-stu-id="32c1b-175">If you want, you can use another file sharing option, such as an Azure Files share - recommended for many scenarios - or an NFS share.</span></span> <span data-ttu-id="32c1b-176">Vedere il file hello condivisione di informazioni e procedure dettagliate per [Introduzione a Linux nodi di calcolo in un Cluster HPC Pack in Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="32c1b-176">See hello file sharing information and detailed steps in [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="32c1b-177">Creare una cartella nel nodo head hello e condividerlo tooEveryone impostando i privilegi di lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="32c1b-177">Create a folder on hello head node, and share it tooEveryone by setting Read/Write privileges.</span></span> <span data-ttu-id="32c1b-178">Ad esempio condividere C:\OpenFOAM nel nodo head di hello come \\ \\SUSE12RDMA HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="32c1b-178">For example, share C:\OpenFOAM on hello head node as \\\\SUSE12RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="32c1b-179">In questo caso, *SUSE12RDMA HN* è il nome host hello del nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-179">Here, *SUSE12RDMA-HN* is hello host name of hello head node.</span></span>
2. <span data-ttu-id="32c1b-180">Aprire una finestra di Windows PowerShell ed eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="32c1b-180">Open a Windows PowerShell window and run hello following commands:</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

<span data-ttu-id="32c1b-181">Hello primo comando crea una cartella denominata /openfoam in tutti i nodi nel gruppo LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-181">hello first command creates a folder named /openfoam on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="32c1b-182">comando secondo Hello Monta //SUSE12RDMA-HN/OpenFOAM cartella hello condiviso in nodi di Linux hello con dir_mode e file_mode too777 di set di bit.</span><span class="sxs-lookup"><span data-stu-id="32c1b-182">hello second command mounts hello shared folder //SUSE12RDMA-HN/OpenFOAM on hello Linux nodes with dir_mode and file_mode bits set too777.</span></span> <span data-ttu-id="32c1b-183">Hello *username* e *password* in hello comando deve essere credenziali hello di un utente nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-183">hello *username* and *password* in hello command should be hello credentials of a user on hello head node.</span></span>

> [!NOTE]
> <span data-ttu-id="32c1b-184">Hello "\\`" simbolo nel secondo comando hello è un simbolo di escape per PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32c1b-184">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="32c1b-185">"\\`,"significa hello"," (carattere virgola) è una parte del comando hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-185">“\\`,” means hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

## <a name="install-mpi-and-openfoam"></a><span data-ttu-id="32c1b-186">Installare MPI e OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="32c1b-186">Install MPI and OpenFOAM</span></span>
<span data-ttu-id="32c1b-187">toorun OpenFOAM come un processo MPI su rete RDMA hello, è necessario toocompile OpenFOAM con le librerie di Intel MPI hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-187">toorun OpenFOAM as an MPI job on hello RDMA network, you need toocompile OpenFOAM with hello Intel MPI libraries.</span></span> 

<span data-ttu-id="32c1b-188">In primo luogo, eseguire vari **clusrun** comandi OpenFOAM e librerie di Intel MPI tooinstall (se non è già installato) sui nodi di Linux.</span><span class="sxs-lookup"><span data-stu-id="32c1b-188">First, run several **clusrun** commands tooinstall Intel MPI libraries (if not already installed) and OpenFOAM on your Linux nodes.</span></span> <span data-ttu-id="32c1b-189">Condivisione di un nodo head hello utilizzare configurata in precedenza i file di installazione hello tooshare tra i nodi di Linux hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-189">Use hello head node share configured previously tooshare hello installation files among hello Linux nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32c1b-190">Questi passaggi di installazione e compilazione sono riportati come esempio</span><span class="sxs-lookup"><span data-stu-id="32c1b-190">These installation and compiling steps are examples.</span></span> <span data-ttu-id="32c1b-191">È necessario una discreta conoscenza di Linux tooensure di amministrazione di sistema che dipendenti compilatori e librerie siano installate correttamente.</span><span class="sxs-lookup"><span data-stu-id="32c1b-191">You need some knowledge of Linux system administration tooensure that dependent compilers and libraries are installed correctly.</span></span> <span data-ttu-id="32c1b-192">Potrebbe essere necessario toomodify alcune variabili di ambiente o altre impostazioni per le versioni di Intel MPI e OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="32c1b-192">You might need toomodify certain environment variables or other settings for your versions of Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="32c1b-193">Per informazioni dettagliate, vedere [Guida all'installazione di Intel MPI Library per Linux](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) e [Installazione del pacchetto di origine di OpenFOAM](http://openfoam.org/download/2-3-1-source/) per l'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="32c1b-193">For details, see [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) and [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) for your environment.</span></span>
> 
> 

### <a name="install-intel-mpi"></a><span data-ttu-id="32c1b-194">Installare Intel MPI</span><span class="sxs-lookup"><span data-stu-id="32c1b-194">Install Intel MPI</span></span>
<span data-ttu-id="32c1b-195">Salvare il pacchetto di installazione scaricato hello per Intel MPI (l_mpi_p_5.0.3.048.tgz in questo esempio) in C:\OpenFoam nel nodo head hello in modo che i nodi di Linux hello possono accedere a questo file da /openfoam.</span><span class="sxs-lookup"><span data-stu-id="32c1b-195">Save hello downloaded installation package for Intel MPI (l_mpi_p_5.0.3.048.tgz in this example) in C:\OpenFoam on hello head node so that hello Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="32c1b-196">Eseguire quindi **clusrun** libreria Intel MPI tooinstall in tutti i nodi di Linux hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-196">Then run **clusrun** tooinstall Intel MPI library on all hello Linux nodes.</span></span>

1. <span data-ttu-id="32c1b-197">di seguito Hello comandi pacchetto di installazione copia hello e decomprimerlo troppo/rifiutare/intel in ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="32c1b-197">hello following commands copy hello installation package and extract it too/opt/intel on each node.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. <span data-ttu-id="32c1b-198">Libreria MPI Intel tooinstall invisibile all'utente, utilizzare un file di silent.cfg.</span><span class="sxs-lookup"><span data-stu-id="32c1b-198">tooinstall Intel MPI Library silently, use a silent.cfg file.</span></span> <span data-ttu-id="32c1b-199">È possibile trovare un esempio in hello file di esempio alla fine di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="32c1b-199">You can find an example in hello sample files at hello end of this article.</span></span> <span data-ttu-id="32c1b-200">Inserire questo file in hello condivisa /openfoam cartella.</span><span class="sxs-lookup"><span data-stu-id="32c1b-200">Place this file in hello shared folder /openfoam.</span></span> <span data-ttu-id="32c1b-201">Per informazioni dettagliate sul file silent.cfg hello, vedere [Intel MPI libreria per la Guida all'installazione di Linux - installazione invisibile all'utente](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span><span class="sxs-lookup"><span data-stu-id="32c1b-201">For details about hello silent.cfg file, see [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="32c1b-202">Assicurarsi di salvare il file silent.cfg come file di testo con terminazioni di riga Linux (solo LF, non CR LF),</span><span class="sxs-lookup"><span data-stu-id="32c1b-202">Make sure that you save your silent.cfg file as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="32c1b-203">Questo passaggio garantisce che venga eseguito correttamente in nodi di Linux hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-203">This step ensures that it runs properly on hello Linux nodes.</span></span>
   > 
   > 
3. <span data-ttu-id="32c1b-204">Installare Intel MPI Library in modalità invisibile all'utente.</span><span class="sxs-lookup"><span data-stu-id="32c1b-204">Install Intel MPI Library in silent mode.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a><span data-ttu-id="32c1b-205">Configurare MPI</span><span class="sxs-lookup"><span data-stu-id="32c1b-205">Configure MPI</span></span>
<span data-ttu-id="32c1b-206">Per il test, è consigliabile aggiungere hello seguenti righe toohello /etc/security/limits.conf in ognuno dei nodi di Linux hello:</span><span class="sxs-lookup"><span data-stu-id="32c1b-206">For testing, you should add hello following lines toohello /etc/security/limits.conf on each of hello Linux nodes:</span></span>

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


<span data-ttu-id="32c1b-207">Riavviare i nodi di Linux hello dopo l'aggiornamento di file limits.conf hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-207">Restart hello Linux nodes after you update hello limits.conf file.</span></span> <span data-ttu-id="32c1b-208">Ad esempio, utilizzare la seguente hello **clusrun** comando:</span><span class="sxs-lookup"><span data-stu-id="32c1b-208">For example, use hello following **clusrun** command:</span></span>

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

<span data-ttu-id="32c1b-209">Dopo il riavvio, verificare che tale cartella hello viene montata come /openfoam.</span><span class="sxs-lookup"><span data-stu-id="32c1b-209">After restarting, ensure that hello shared folder is mounted as /openfoam.</span></span>

### <a name="compile-and-install-openfoam"></a><span data-ttu-id="32c1b-210">Compilare e installare OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="32c1b-210">Compile and install OpenFOAM</span></span>
<span data-ttu-id="32c1b-211">Salvare il pacchetto di installazione scaricato hello per hello tooC:\OpenFoam OpenFOAM Source Pack (OpenFOAM 2.3.1.tgz in questo esempio) nel nodo head hello in modo che i nodi di Linux hello possono accedere a questo file da /openfoam.</span><span class="sxs-lookup"><span data-stu-id="32c1b-211">Save hello downloaded installation package for hello OpenFOAM Source Pack (OpenFOAM-2.3.1.tgz in this example) tooC:\OpenFoam on hello head node so that hello Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="32c1b-212">Eseguire quindi **clusrun** comandi hello di toocompile OpenFOAM in tutti i nodi di Linux.</span><span class="sxs-lookup"><span data-stu-id="32c1b-212">Then run **clusrun** commands toocompile OpenFOAM on all hello Linux nodes.</span></span>

1. <span data-ttu-id="32c1b-213">Creare una cartella /opt/OpenFOAM in ogni nodo di Linux, Copia cartella toothis hello origine pacchetto ed estrarre i file non esiste.</span><span class="sxs-lookup"><span data-stu-id="32c1b-213">Create a folder /opt/OpenFOAM on each Linux node, copy hello source package toothis folder, and extract it there.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. <span data-ttu-id="32c1b-214">toocompile OpenFOAM con hello libreria MPI Intel, innanzitutto impostare alcune variabili di ambiente per Intel MPI e OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="32c1b-214">toocompile OpenFOAM with hello Intel MPI Library, first set up some environment variables for both Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="32c1b-215">Utilizzare uno script bash denominato settings.sh tooset hello variabili.</span><span class="sxs-lookup"><span data-stu-id="32c1b-215">Use a bash script called settings.sh tooset hello variables.</span></span> <span data-ttu-id="32c1b-216">È possibile trovare un esempio in hello file di esempio alla fine di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="32c1b-216">You can find an example in hello sample files at hello end of this article.</span></span> <span data-ttu-id="32c1b-217">Inserire questo file (salvato con terminazioni di riga di Linux) in hello condivisa /openfoam cartella.</span><span class="sxs-lookup"><span data-stu-id="32c1b-217">Place this file (saved with Linux line endings) in hello shared folder /openfoam.</span></span> <span data-ttu-id="32c1b-218">Questo file contiene inoltre le impostazioni per hello MPI e OpenFOAM runtime utilizzare successive toorun un processo OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="32c1b-218">This file also contains settings for hello MPI and OpenFOAM runtimes that you use later toorun an OpenFOAM job.</span></span>
3. <span data-ttu-id="32c1b-219">Installare pacchetti dipendenti necessiti toocompile OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="32c1b-219">Install dependent packages needed toocompile OpenFOAM.</span></span> <span data-ttu-id="32c1b-220">A seconda di distribuzione di Linux, è necessario innanzitutto tooadd un repository.</span><span class="sxs-lookup"><span data-stu-id="32c1b-220">Depending on your Linux distribution, you might first need tooadd a repository.</span></span> <span data-ttu-id="32c1b-221">Eseguire **clusrun** comandi simili toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="32c1b-221">Run **clusrun** commands similar toohello following:</span></span>
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    <span data-ttu-id="32c1b-222">Se necessario, hello toorun SSH tooeach Linux nodo comandi tooconfirm cui vengono eseguite correttamente.</span><span class="sxs-lookup"><span data-stu-id="32c1b-222">If necessary, SSH tooeach Linux node toorun hello commands tooconfirm that they run properly.</span></span>
4. <span data-ttu-id="32c1b-223">Comando che segue di esecuzione hello toocompile OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="32c1b-223">Run hello following command toocompile OpenFOAM.</span></span> <span data-ttu-id="32c1b-224">il processo di compilazione Hello accetta alcuni toocomplete ora e genera una grande quantità di informazioni toostandard dell'output di log, pertanto usare hello **/ interleaved** l'opzione di output di hello toodisplay interfogliati.</span><span class="sxs-lookup"><span data-stu-id="32c1b-224">hello compilation process takes some time toocomplete and generates a large amount of log information toostandard output, so use hello **/interleaved** option toodisplay hello output interleaved.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > <span data-ttu-id="32c1b-225">Hello "\\`" simbolo nel comando hello è un simbolo di escape per PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32c1b-225">hello “\\`” symbol in hello command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="32c1b-226">"\\`&" significa hello "e" è una parte del comando hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-226">“\\`&” means hello “&” is a part of hello command.</span></span>
   > 
   > 

## <a name="prepare-toorun-an-openfoam-job"></a><span data-ttu-id="32c1b-227">Preparazione di un processo OpenFOAM toorun</span><span class="sxs-lookup"><span data-stu-id="32c1b-227">Prepare toorun an OpenFOAM job</span></span>
<span data-ttu-id="32c1b-228">Ora get ready toorun un processo MPI chiamato sloshingTank3D, che è uno degli esempi OpenFoam hello, in due nodi di Linux.</span><span class="sxs-lookup"><span data-stu-id="32c1b-228">Now get ready toorun an MPI job called sloshingTank3D, which is one of hello OpenFoam samples, on two Linux nodes.</span></span> 

### <a name="set-up-hello-runtime-environment"></a><span data-ttu-id="32c1b-229">Configurare un ambiente di runtime hello</span><span class="sxs-lookup"><span data-stu-id="32c1b-229">Set up hello runtime environment</span></span>
<span data-ttu-id="32c1b-230">tooset ambienti di runtime hello OpenFOAM relative MPI in nodi di Linux hello, Esegui comando in una finestra di Windows PowerShell seguente nel nodo head hello hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-230">tooset up hello runtime environments for MPI and OpenFOAM on hello Linux nodes, run hello following command in a Windows PowerShell window on hello head node.</span></span> <span data-ttu-id="32c1b-231">(Questo comando è valido solamente per SUSE Linux).</span><span class="sxs-lookup"><span data-stu-id="32c1b-231">(This command is valid for SUSE Linux only.)</span></span>

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a><span data-ttu-id="32c1b-232">Preparare i dati di esempio</span><span class="sxs-lookup"><span data-stu-id="32c1b-232">Prepare sample data</span></span>
<span data-ttu-id="32c1b-233">Condivisione di un nodo head hello utilizzare configurate in precedenza i file tooshare tra i nodi di Linux hello (montati come /openfoam).</span><span class="sxs-lookup"><span data-stu-id="32c1b-233">Use hello head node share you configured previously tooshare files among hello Linux nodes (mounted as /openfoam).</span></span>

1. <span data-ttu-id="32c1b-234">Nodi di calcolo SSH tooone del Linux.</span><span class="sxs-lookup"><span data-stu-id="32c1b-234">SSH tooone of your Linux compute nodes.</span></span>
2. <span data-ttu-id="32c1b-235">Se non hai già fatto, eseguire hello tooset di comando di ambiente di runtime OpenFOAM hello, di seguito.</span><span class="sxs-lookup"><span data-stu-id="32c1b-235">Run hello following command tooset up hello OpenFOAM runtime environment, if you haven’t already done this.</span></span>
   
   ```
   $ source /openfoam/settings.sh
   ```
3. <span data-ttu-id="32c1b-236">Copiare una cartella condivisa toohello esempio sloshingTank3D hello e passare tooit.</span><span class="sxs-lookup"><span data-stu-id="32c1b-236">Copy hello sloshingTank3D sample toohello shared folder and navigate tooit.</span></span>
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. <span data-ttu-id="32c1b-237">Quando si utilizzano parametri predefiniti hello di questo esempio, può richiedere decine di toorun minuti, pertanto è opportuno toomodify toomake alcuni parametri eseguito più velocemente.</span><span class="sxs-lookup"><span data-stu-id="32c1b-237">When you use hello default parameters of this sample, it can take tens of minutes toorun, so you might want toomodify some parameters toomake it run faster.</span></span> <span data-ttu-id="32c1b-238">Una semplice scelta è toomodify hello ora passaggio variabili deltaT e writeInterval nel file di sistema/controlDict hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-238">One simple choice is toomodify hello time step variables deltaT and writeInterval in hello system/controlDict file.</span></span> <span data-ttu-id="32c1b-239">Questo file contiene tutti i dati di input relativi controllo toohello di tempo e di lettura e scrittura di dati della soluzione.</span><span class="sxs-lookup"><span data-stu-id="32c1b-239">This file stores all input data relating toohello control of time and reading and writing solution data.</span></span> <span data-ttu-id="32c1b-240">Ad esempio, è possibile modificare il valore di hello di deltaT da too0.5 0,05 e il valore di hello di writeInterval da too0.5 0,05.</span><span class="sxs-lookup"><span data-stu-id="32c1b-240">For example, you could change hello value of deltaT from 0.05 too0.5 and hello value of writeInterval from 0.05 too0.5.</span></span>
   
   ![Modificare le variabili delle fasi][step_variables]
5. <span data-ttu-id="32c1b-242">Specificare i valori desiderati per le variabili di hello nel file di sistema/decomposeParDict hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-242">Specify desired values for hello variables in hello system/decomposeParDict file.</span></span> <span data-ttu-id="32c1b-243">In questo esempio vengono utilizzati due nodi di Linux ogni con 8 core, quindi impostare numberOfSubdomains too16 e n di hierarchicalCoeffs too(1 1 16), vale a dire che eseguire OpenFOAM in parallelo con i processi di 16.</span><span class="sxs-lookup"><span data-stu-id="32c1b-243">This example uses two Linux nodes each with 8 cores, so set numberOfSubdomains too16 and n of hierarchicalCoeffs too(1 1 16), which means run OpenFOAM in parallel with 16 processes.</span></span> <span data-ttu-id="32c1b-244">Per altre informazioni, vedere la sezione [3.4 del manuale dell'utente di OpenFOAM relativa all'esecuzione di applicazioni in parallelo](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span><span class="sxs-lookup"><span data-stu-id="32c1b-244">For more information, see [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span></span>
   
   ![Scomporre i processi][decompose]
6. <span data-ttu-id="32c1b-246">Eseguire hello dopo i comandi da dati di esempio hello tooprepare directory sloshingTank3D hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-246">Run hello following commands from hello sloshingTank3D directory tooprepare hello sample data.</span></span>
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. <span data-ttu-id="32c1b-247">Nel nodo head hello, dovrebbe essere vengono copiati i file di dati di esempio hello in C:\OpenFoam\sloshingTank3D.</span><span class="sxs-lookup"><span data-stu-id="32c1b-247">On hello head node, you should see hello sample data files are copied into C:\OpenFoam\sloshingTank3D.</span></span> <span data-ttu-id="32c1b-248">(C:\OpenFoam è una cartella condivisa di hello nel nodo head hello.)</span><span class="sxs-lookup"><span data-stu-id="32c1b-248">(C:\OpenFoam is hello shared folder on hello head node.)</span></span>
   
   ![File di dati sul nodo head hello][data_files]

### <a name="host-file-for-mpirun"></a><span data-ttu-id="32c1b-250">File host per mpirun</span><span class="sxs-lookup"><span data-stu-id="32c1b-250">Host file for mpirun</span></span>
<span data-ttu-id="32c1b-251">In questo passaggio è creare un file di host (un elenco di nodi di calcolo) quale hello **mpirun** comando Usa.</span><span class="sxs-lookup"><span data-stu-id="32c1b-251">In this step, you create a host file (a list of compute nodes) which hello **mpirun** command uses.</span></span>

1. <span data-ttu-id="32c1b-252">In uno dei nodi di Linux hello, creare un file denominato file host in /openfoam, pertanto questo file può essere raggiunto al /openfoam/hostfile in tutti i nodi di Linux.</span><span class="sxs-lookup"><span data-stu-id="32c1b-252">On one of hello Linux nodes, create a file named hostfile under /openfoam, so this file can be reached at /openfoam/hostfile on all Linux nodes.</span></span>
2. <span data-ttu-id="32c1b-253">Scrivere i nomi dei nodi Linux in questo file.</span><span class="sxs-lookup"><span data-stu-id="32c1b-253">Write your Linux node names into this file.</span></span> <span data-ttu-id="32c1b-254">In questo esempio, file hello contiene hello i nomi seguenti:</span><span class="sxs-lookup"><span data-stu-id="32c1b-254">In this example, hello file contains hello following names:</span></span>
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > <span data-ttu-id="32c1b-255">È anche possibile creare questo file in C:\OpenFoam\hostfile nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-255">You can also create this file at C:\OpenFoam\hostfile on hello head node.</span></span> <span data-ttu-id="32c1b-256">Se si sceglie questa opzione, è necessario salvare lo script come file di testo con terminazioni di riga Linux (solo LF, non CR LF),</span><span class="sxs-lookup"><span data-stu-id="32c1b-256">If you choose this option, save it as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="32c1b-257">In questo modo si garantisce il corretto funzionamento in nodi di Linux hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-257">This ensures that it runs properly on hello Linux nodes.</span></span>
   > 
   > 
   
   <span data-ttu-id="32c1b-258">**Wrapper di script bash**</span><span class="sxs-lookup"><span data-stu-id="32c1b-258">**Bash script wrapper**</span></span>
   
   <span data-ttu-id="32c1b-259">Se si dispongano di molti nodi di Linux e si desidera toorun il processo solo per alcune di esse, non è un toouse buona un host predefinito di file, perché non si conoscono i nodi che verranno allocati tooyour processo.</span><span class="sxs-lookup"><span data-stu-id="32c1b-259">If you have many Linux nodes and you want your job toorun on only some of them, it’s not a good idea toouse a fixed host file, because you don’t know which nodes will be allocated tooyour job.</span></span> <span data-ttu-id="32c1b-260">In questo caso, scrivere un wrapper di script bash per **mpirun** toocreate hello automaticamente i file di host.</span><span class="sxs-lookup"><span data-stu-id="32c1b-260">In this case, write a bash script wrapper for **mpirun** toocreate hello host file automatically.</span></span> <span data-ttu-id="32c1b-261">È possibile trovare un wrapper di script di esempio bash chiamato hpcimpirun.sh alla fine di hello di questo articolo e salvarlo come /openfoam/hpcimpirun.sh. Questo script di esempio hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="32c1b-261">You can find an example bash script wrapper called hpcimpirun.sh at hello end of this article, and save it as /openfoam/hpcimpirun.sh. This example script does hello following:</span></span>
   
   1. <span data-ttu-id="32c1b-262">Consente di impostare le variabili di ambiente hello **mpirun**e un processo MPI hello toorun di addizione comando parametri tramite rete RDMA hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-262">Sets up hello environment variables for **mpirun**, and some addition command parameters toorun hello MPI job through hello RDMA network.</span></span> <span data-ttu-id="32c1b-263">In questo caso, imposta hello seguenti variabili:</span><span class="sxs-lookup"><span data-stu-id="32c1b-263">In this case, it sets hello following variables:</span></span>
      
      * <span data-ttu-id="32c1b-264">I_MPI_FABRICS=shm:dapl</span><span class="sxs-lookup"><span data-stu-id="32c1b-264">I_MPI_FABRICS=shm:dapl</span></span>
      * <span data-ttu-id="32c1b-265">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span><span class="sxs-lookup"><span data-stu-id="32c1b-265">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span></span>
      * <span data-ttu-id="32c1b-266">I_MPI_DYNAMIC_CONNECTION=0</span><span class="sxs-lookup"><span data-stu-id="32c1b-266">I_MPI_DYNAMIC_CONNECTION=0</span></span>
   2. <span data-ttu-id="32c1b-267">Crea un file di host in base a toohello $ variabile di ambiente CCP_NODES_CORES, che viene impostato dal nodo head HPC hello quando il processo di hello è attivato.</span><span class="sxs-lookup"><span data-stu-id="32c1b-267">Creates a host file according toohello environment variable $CCP_NODES_CORES, which is set by hello HPC head node when hello job is activated.</span></span>
      
      <span data-ttu-id="32c1b-268">formato Hello $CCP_NODES_CORES segue questo modello:</span><span class="sxs-lookup"><span data-stu-id="32c1b-268">hello format of $CCP_NODES_CORES follows this pattern:</span></span>
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      <span data-ttu-id="32c1b-269">dove</span><span class="sxs-lookup"><span data-stu-id="32c1b-269">where</span></span>
      
      * <span data-ttu-id="32c1b-270">`<Number of nodes>`-numero di nodi di hello allocata toothis processo.</span><span class="sxs-lookup"><span data-stu-id="32c1b-270">`<Number of nodes>` - hello number of nodes allocated toothis job.</span></span>  
      * <span data-ttu-id="32c1b-271">`<Name of node_n_...>`-nome hello di ogni nodo allocata toothis processo.</span><span class="sxs-lookup"><span data-stu-id="32c1b-271">`<Name of node_n_...>` - hello name of each node allocated toothis job.</span></span>
      * <span data-ttu-id="32c1b-272">`<Cores of node_n_...>`-numero di core nel processo di hello nodo toothis allocato hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-272">`<Cores of node_n_...>` - hello number of cores on hello node allocated toothis job.</span></span>
      
      <span data-ttu-id="32c1b-273">Ad esempio, se il processo di hello necessita di due nodi toorun, $CCP_NODES_CORES è simile a</span><span class="sxs-lookup"><span data-stu-id="32c1b-273">For example, if hello job needs two nodes toorun, $CCP_NODES_CORES is similar to</span></span>
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. <span data-ttu-id="32c1b-274">Hello chiamate **mpirun** comando e accoda riga di comando di due parametri toohello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-274">Calls hello **mpirun** command and appends two parameters toohello command line.</span></span>
      
      * <span data-ttu-id="32c1b-275">`--hostfile <hostfilepath>: <hostfilepath>`-Crea il percorso di hello di hello host file hello script</span><span class="sxs-lookup"><span data-stu-id="32c1b-275">`--hostfile <hostfilepath>: <hostfilepath>` - hello path of hello host file hello script creates</span></span>
      * <span data-ttu-id="32c1b-276">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`-una variabile di ambiente impostata dal nodo head HPC Pack, hello che archivia il numero di hello di core totale allocato toothis processo.</span><span class="sxs-lookup"><span data-stu-id="32c1b-276">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - an environment variable set by hello HPC Pack head node, which stores hello number of total cores allocated toothis job.</span></span> <span data-ttu-id="32c1b-277">In questo caso, specifica il numero di hello dei processi di **mpirun**.</span><span class="sxs-lookup"><span data-stu-id="32c1b-277">In this case, it specifies hello number of processes for **mpirun**.</span></span>

## <a name="submit-an-openfoam-job"></a><span data-ttu-id="32c1b-278">Inviare un processo OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="32c1b-278">Submit an OpenFOAM job</span></span>
<span data-ttu-id="32c1b-279">A questo punto è possibile inviare un processo in HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="32c1b-279">Now you can submit a job in HPC Cluster Manager.</span></span> <span data-ttu-id="32c1b-280">È necessario toopass hello script hpcimpirun.sh nelle righe di comando hello per alcune delle attività di processo hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-280">You need toopass hello script hpcimpirun.sh in hello command lines for some of hello job tasks.</span></span>

1. <span data-ttu-id="32c1b-281">Connettersi tooyour nodo head del cluster e avviare HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="32c1b-281">Connect tooyour cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="32c1b-282">**Gestione delle risorse**, assicurarsi che i nodi di calcolo di hello Linux hello **Online** stato.</span><span class="sxs-lookup"><span data-stu-id="32c1b-282">**In Resource Management**, ensure that hello Linux compute nodes are in hello **Online** state.</span></span> <span data-ttu-id="32c1b-283">Se lo stato è diverso, selezionarli e fare clic su **Portare Online**.</span><span class="sxs-lookup"><span data-stu-id="32c1b-283">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="32c1b-284">In **Job Management** (Gestione processi) fare clic su **New Job** (Nuovo processo).</span><span class="sxs-lookup"><span data-stu-id="32c1b-284">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="32c1b-285">Immettere un nome per il processo, ad esempio *sloshingTank3D*.</span><span class="sxs-lookup"><span data-stu-id="32c1b-285">Enter a name for job such as *sloshingTank3D*.</span></span>
   
   ![Dettagli del processo][job_details]
5. <span data-ttu-id="32c1b-287">In **risorse di processo**, scegliere il tipo di hello di risorsa come "Nodo" e impostare too2 minimo hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-287">In **Job resources**, choose hello type of resource as “Node” and set hello Minimum too2.</span></span> <span data-ttu-id="32c1b-288">Questa configurazione esegue il processo di hello in due nodi di Linux, ognuno dei quali presenta otto core in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="32c1b-288">This configuration runs hello job on two Linux nodes, each of which has eight cores in this example.</span></span>
   
   ![Risorse del processo][job_resources]
6. <span data-ttu-id="32c1b-290">Fare clic su **modifica attività** in hello spostamento a sinistra e quindi fare clic su **Aggiungi** tooadd un processo toohello di attività.</span><span class="sxs-lookup"><span data-stu-id="32c1b-290">Click **Edit Tasks** in hello left navigation, and then click **Add** tooadd a task toohello job.</span></span> <span data-ttu-id="32c1b-291">Aggiungere quattro processo toohello di attività con hello seguenti righe di comando e le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="32c1b-291">Add four tasks toohello job with hello following command lines and settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="32c1b-292">Esecuzione `source /openfoam/settings.sh` imposta hello OpenFOAM e MPI gli ambienti di runtime, in modo ciascuna delle seguenti attività hello chiama prima hello OpenFOAM comando.</span><span class="sxs-lookup"><span data-stu-id="32c1b-292">Running `source /openfoam/settings.sh` sets up hello OpenFOAM and MPI runtime environments, so each of hello following tasks calls it before hello OpenFOAM command.</span></span>
   > 
   > 
   
   * <span data-ttu-id="32c1b-293">**Attività 1**.</span><span class="sxs-lookup"><span data-stu-id="32c1b-293">**Task 1**.</span></span> <span data-ttu-id="32c1b-294">Eseguire **decomposePar** toogenerate i file di dati per l'esecuzione **interDyMFoam** in parallelo.</span><span class="sxs-lookup"><span data-stu-id="32c1b-294">Run **decomposePar** toogenerate data files for running **interDyMFoam** in parallel.</span></span>
     
     * <span data-ttu-id="32c1b-295">Assegnare un nodo toohello attività</span><span class="sxs-lookup"><span data-stu-id="32c1b-295">Assign one node toohello task</span></span>
     * <span data-ttu-id="32c1b-296">**Riga di comando** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="32c1b-296">**Command line** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="32c1b-297">**Directory di lavoro** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="32c1b-297">**Working directory** - /openfoam/sloshingTank3D</span></span>
     
     <span data-ttu-id="32c1b-298">Vedere hello seguente illustrazione.</span><span class="sxs-lookup"><span data-stu-id="32c1b-298">See hello following figure.</span></span> <span data-ttu-id="32c1b-299">Configurare le attività rimanenti hello in modo analogo.</span><span class="sxs-lookup"><span data-stu-id="32c1b-299">You configure hello remaining tasks similarly.</span></span>
     
     ![Dettagli dell'attività 1][task_details1]
   * <span data-ttu-id="32c1b-301">**Attività 2**.</span><span class="sxs-lookup"><span data-stu-id="32c1b-301">**Task 2**.</span></span> <span data-ttu-id="32c1b-302">Eseguire **interDyMFoam** nell'esempio hello toocompute parallelo.</span><span class="sxs-lookup"><span data-stu-id="32c1b-302">Run **interDyMFoam** in parallel toocompute hello sample.</span></span>
     
     * <span data-ttu-id="32c1b-303">Assegnare due nodi toohello attività</span><span class="sxs-lookup"><span data-stu-id="32c1b-303">Assign two nodes toohello task</span></span>
     * <span data-ttu-id="32c1b-304">**Riga di comando** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="32c1b-304">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="32c1b-305">**Directory di lavoro** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="32c1b-305">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="32c1b-306">**Attività 3**.</span><span class="sxs-lookup"><span data-stu-id="32c1b-306">**Task 3**.</span></span> <span data-ttu-id="32c1b-307">Eseguire **reconstructPar** toomerge hello imposta delle directory ora da ogni directory processor_N_ in un unico gruppo.</span><span class="sxs-lookup"><span data-stu-id="32c1b-307">Run **reconstructPar** toomerge hello sets of time directories from each processor_N_ directory into a single set.</span></span>
     
     * <span data-ttu-id="32c1b-308">Assegnare un nodo toohello attività</span><span class="sxs-lookup"><span data-stu-id="32c1b-308">Assign one node toohello task</span></span>
     * <span data-ttu-id="32c1b-309">**Riga di comando** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="32c1b-309">**Command line** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="32c1b-310">**Directory di lavoro** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="32c1b-310">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="32c1b-311">**Attività 4**.</span><span class="sxs-lookup"><span data-stu-id="32c1b-311">**Task 4**.</span></span> <span data-ttu-id="32c1b-312">Eseguire **foamToEnsight** in parallelo tooconvert file dei risultati OpenFOAM hello in EnSight formattare e hello EnSight file in una directory denominata Ensight nella directory case hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-312">Run **foamToEnsight** in parallel tooconvert hello OpenFOAM result files into EnSight format and place hello EnSight files in a directory named Ensight in hello case directory.</span></span>
     
     * <span data-ttu-id="32c1b-313">Assegnare due nodi toohello attività</span><span class="sxs-lookup"><span data-stu-id="32c1b-313">Assign two nodes toohello task</span></span>
     * <span data-ttu-id="32c1b-314">**Riga di comando** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="32c1b-314">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="32c1b-315">**Directory di lavoro** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="32c1b-315">**Working directory** - /openfoam/sloshingTank3D</span></span>
7. <span data-ttu-id="32c1b-316">Aggiungere le dipendenze toothese attività in attività ordine crescente.</span><span class="sxs-lookup"><span data-stu-id="32c1b-316">Add dependencies toothese tasks in ascending task order.</span></span>
   
   ![Dipendenze dell'attività][task_dependencies]
8. <span data-ttu-id="32c1b-318">Fare clic su **Invia** toorun questo processo.</span><span class="sxs-lookup"><span data-stu-id="32c1b-318">Click **Submit** toorun this job.</span></span>
   
   <span data-ttu-id="32c1b-319">Per impostazione predefinita, HPC Pack invia il processo di hello come account utente corrente.</span><span class="sxs-lookup"><span data-stu-id="32c1b-319">By default, HPC Pack submits hello job as your current logged-on user account.</span></span> <span data-ttu-id="32c1b-320">Dopo aver fatto clic **Invia**, si potrebbe visualizzare una finestra di dialogo che richiede nome utente di tooenter hello e una password.</span><span class="sxs-lookup"><span data-stu-id="32c1b-320">After you click **Submit**, you might see a dialog box prompting you tooenter hello user name and password.</span></span>
   
   ![Credenziali del processo][creds]
   
   <span data-ttu-id="32c1b-322">In alcune condizioni, HPC Pack memorizza informazioni utente di hello prima di input e non visualizza questa finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="32c1b-322">Under some conditions, HPC Pack remembers hello user information you input before and doesn’t show this dialog box.</span></span> <span data-ttu-id="32c1b-323">toomake HPC Pack visualizzarlo nuovamente, immettere hello comando al prompt di comando seguente e quindi inviare il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-323">toomake HPC Pack show it again, enter hello following command at a Command prompt and then submit hello job.</span></span>
   
   ```
   hpccred delcreds
   ```
9. <span data-ttu-id="32c1b-324">processo Hello accetta da decine di minuti tooseveral ore in base a parametri toohello che sono stati impostati per l'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-324">hello job takes from tens of minutes tooseveral hours according toohello parameters you have set for hello sample.</span></span> <span data-ttu-id="32c1b-325">Nella mappa di calore hello, vedrai il processo di hello in esecuzione in nodi di Linux hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-325">In hello heat map, you see hello job running on hello Linux nodes.</span></span> 
   
   ![Mappa termica][heat_map]
   
   <span data-ttu-id="32c1b-327">In ogni nodo vengono avviati otto processi.</span><span class="sxs-lookup"><span data-stu-id="32c1b-327">On each node, eight processes are started.</span></span>
   
   ![Processi Linux][linux_processes]
10. <span data-ttu-id="32c1b-329">Al termine del processo di hello, è possibile trovare i risultati del processo hello nelle cartelle in C:\OpenFoam\sloshingTank3D e file di log hello C:\OpenFoam.</span><span class="sxs-lookup"><span data-stu-id="32c1b-329">When hello job finishes, find hello job results in folders under C:\OpenFoam\sloshingTank3D, and hello log files at C:\OpenFoam.</span></span>

## <a name="view-results-in-ensight"></a><span data-ttu-id="32c1b-330">Visualizzare i risultati in EnSight</span><span class="sxs-lookup"><span data-stu-id="32c1b-330">View results in EnSight</span></span>
<span data-ttu-id="32c1b-331">Se si desidera utilizzare [EnSight](https://www.ceisoftware.com/) toovisualize e analisi dei risultati del processo OpenFOAM hello hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-331">Optionally use [EnSight](https://www.ceisoftware.com/) toovisualize and analyze hello results of hello OpenFOAM job.</span></span> <span data-ttu-id="32c1b-332">Per altre informazioni sulla visualizzazione e l'animazione in EnSight, vedere questa [guida video](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span><span class="sxs-lookup"><span data-stu-id="32c1b-332">For more about visualization and animation in EnSight, see this [video guide](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span></span>

1. <span data-ttu-id="32c1b-333">Dopo aver installato EnSight nel nodo head hello, avviarlo.</span><span class="sxs-lookup"><span data-stu-id="32c1b-333">After you install EnSight on hello head node, start it.</span></span>
2. <span data-ttu-id="32c1b-334">Aprire C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span><span class="sxs-lookup"><span data-stu-id="32c1b-334">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span></span>
   
   <span data-ttu-id="32c1b-335">Viene visualizzato un serbatoio nel Visualizzatore hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-335">You see a tank in hello viewer.</span></span>
   
   ![Serbatoio in EnSight][tank]
3. <span data-ttu-id="32c1b-337">Creare un **Isosurface** da **internalMesh**, quindi scegliere variabile hello **alpha_water**.</span><span class="sxs-lookup"><span data-stu-id="32c1b-337">Create an **Isosurface** from **internalMesh**, and then choose hello variable **alpha_water**.</span></span>
   
   ![Creare un oggetto isosurface][isosurface]
4. <span data-ttu-id="32c1b-339">Impostare il colore di hello per **Isosurface_part** creato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-339">Set hello color for **Isosurface_part** created in hello previous step.</span></span> <span data-ttu-id="32c1b-340">Ad esempio, impostarla toowater blu.</span><span class="sxs-lookup"><span data-stu-id="32c1b-340">For example, set it toowater blue.</span></span>
   
   ![Modificare il colore dell'oggetto isosurface][isosurface_color]
5. <span data-ttu-id="32c1b-342">Creare un **Iso volume** da **pareti** selezionando **pareti** in hello **parti** pannello e fare clic su hello **Isosurfaces**  pulsante nella barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-342">Create an **Iso-volume** from **walls** by selecting **walls** in hello **Parts** panel and click hello **Isosurfaces** button in hello toolbar.</span></span>
6. <span data-ttu-id="32c1b-343">Nella finestra di dialogo hello selezionare **tipo** come **Isovolume** e impostare Min di hello **Isovolume intervallo** too0.5.</span><span class="sxs-lookup"><span data-stu-id="32c1b-343">In hello dialog box, select **Type** as **Isovolume** and set hello Min of **Isovolume range** too0.5.</span></span> <span data-ttu-id="32c1b-344">toocreate hello isovolume, fare clic su **crea con parti selezionate**.</span><span class="sxs-lookup"><span data-stu-id="32c1b-344">toocreate hello isovolume, click **Create with selected parts**.</span></span>
7. <span data-ttu-id="32c1b-345">Impostare il colore di hello per **Iso_volume_part** creato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-345">Set hello color for **Iso_volume_part** created in hello previous step.</span></span> <span data-ttu-id="32c1b-346">Ad esempio, impostarla acqua toodeep blu.</span><span class="sxs-lookup"><span data-stu-id="32c1b-346">For example, set it toodeep water blue.</span></span>
8. <span data-ttu-id="32c1b-347">Impostare il colore di hello per **pareti**.</span><span class="sxs-lookup"><span data-stu-id="32c1b-347">Set hello color for **walls**.</span></span> <span data-ttu-id="32c1b-348">Ad esempio, impostarla tootransparent bianco.</span><span class="sxs-lookup"><span data-stu-id="32c1b-348">For example, set it tootransparent white.</span></span>
9. <span data-ttu-id="32c1b-349">Fare clic su **riprodurre** risultati hello toosee di simulazione hello.</span><span class="sxs-lookup"><span data-stu-id="32c1b-349">Now click **Play** toosee hello results of hello simulation.</span></span>
   
    ![Risultato per il serbatoio][tank_result]

## <a name="sample-files"></a><span data-ttu-id="32c1b-351">File di esempio</span><span class="sxs-lookup"><span data-stu-id="32c1b-351">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="32c1b-352">File di configurazione XML di esempio per la distribuzione di cluster tramite script PowerShell</span><span class="sxs-lookup"><span data-stu-id="32c1b-352">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

### <a name="sample-credxml-file"></a><span data-ttu-id="32c1b-353">File cred.xml di esempio</span><span class="sxs-lookup"><span data-stu-id="32c1b-353">Sample cred.xml file</span></span>
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```
### <a name="sample-silentcfg-file-tooinstall-mpi"></a><span data-ttu-id="32c1b-354">Esempio silent.cfg file tooinstall MPI</span><span class="sxs-lookup"><span data-stu-id="32c1b-354">Sample silent.cfg file tooinstall MPI</span></span>
```
# Patterns used toocheck silent configuration file
#
# anythingpat - any string
# filepat     - hello file location pattern (/file/location/to/license.lic)
# lspat       - hello license server address pattern (0123@hostname)
# snpat       - hello serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components tooinstall, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path toohello cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes tooenable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes tooupdate ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a><span data-ttu-id="32c1b-355">Script settings.sh di esempio</span><span class="sxs-lookup"><span data-stu-id="32c1b-355">Sample settings.sh script</span></span>
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a><span data-ttu-id="32c1b-356">Script hpccharmrun.sh di esempio</span><span class="sxs-lookup"><span data-stu-id="32c1b-356">Sample hpcimpirun.sh script</span></span>
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run hello mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into hello hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png
