---
title: aaaNAMD con Microsoft HPC Pack nelle macchine virtuali Linux | Documenti Microsoft
description: "Informazioni su come distribuire un cluster Microsoft HPC Pack in Azure e come eseguire una simulazione NAMD con charmrun in più nodi di calcolo Linux"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 76072c6b-ac35-4729-ba67-0d16f9443bd7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/13/2016
ms.author: danlep
ms.openlocfilehash: 90c722f66b494335a62c0613079366ae99002076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a><span data-ttu-id="a2f5c-103">Eseguire NAMD con Microsoft HPC Pack su nodi di calcolo Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="a2f5c-103">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>
<span data-ttu-id="a2f5c-104">Questo articolo illustra un modo toorun un carico di lavoro (HPC) high-performance computing Linux su macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-104">This article shows you one way toorun a Linux high-performance computing (HPC) workload on Azure virtual machines.</span></span> <span data-ttu-id="a2f5c-105">In questo caso, impostare un [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure con nodi di calcolo Linux ed eseguire un [NAMD](http://www.ks.uiuc.edu/Research/namd/) toocalculate simulazione e visualizzare hello struttura di un sistema biomolecular di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-105">Here, you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster on Azure with Linux compute nodes and run a [NAMD](http://www.ks.uiuc.edu/Research/namd/) simulation toocalculate and visualize hello structure of a large biomolecular system.</span></span>  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* <span data-ttu-id="a2f5c-106">**NAMD** (per il programma di Dynamics molecolare Nanoscale) è un pacchetto parallelo dynamics molecolare progettato per la simulazione dei sistemi di grandi dimensioni biomolecular ad alte prestazioni che contengono backup toomillions atomi di.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-106">**NAMD** (for Nanoscale Molecular Dynamics program) is a parallel molecular dynamics package designed for high-performance simulation of large biomolecular systems containing up toomillions of atoms.</span></span> <span data-ttu-id="a2f5c-107">Esempi di questi sistemi includono virus, strutture di celle e proteine di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-107">Examples of these systems include viruses, cell structures, and large proteins.</span></span> <span data-ttu-id="a2f5c-108">NAMD scala toohundreds di core per tipico simulazioni e toomore di 500.000 core per simulazioni di hello più grande.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-108">NAMD scales toohundreds of cores for typical simulations and toomore than 500,000 cores for hello largest simulations.</span></span>
* <span data-ttu-id="a2f5c-109">**Microsoft HPC Pack** fornisce funzionalità toorun HPC su larga scala e le applicazioni parallele in cluster di computer locali o di macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-109">**Microsoft HPC Pack** provides features toorun large-scale HPC and parallel applications in clusters of on-premises computers or Azure virtual machines.</span></span> <span data-ttu-id="a2f5c-110">Sviluppato originariamente come soluzione per i carichi di lavoro HPC di Windows, HPC Pack supporta ora le applicazioni HPC che eseguono Linux su macchine virtuali del nodo di calcolo Linux distribuite in un cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-110">Originally developed as a solution for Windows HPC workloads, HPC Pack now supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="a2f5c-111">Per una panoramica, vedere [Introduzione all'uso di nodi di calcolo Linux in un cluster HPC Pack in Azure](hpcpack-cluster.md) .</span><span class="sxs-lookup"><span data-stu-id="a2f5c-111">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction.</span></span>

<span data-ttu-id="a2f5c-112">Per altre toorun opzioni HPC Linux carichi di lavoro in Azure, vedere [risorse tecniche per batch e high performance computing](../../../batch/batch-hpc-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="a2f5c-112">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/batch-hpc-solutions.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2f5c-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a2f5c-113">Prerequisites</span></span>
* <span data-ttu-id="a2f5c-114">**Cluster HPC Pack con nodi di calcolo Linux**: distribuire un cluster HPC Pack con nodi di calcolo Linux in Azure usando un [modello di Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) o uno [script di Azure PowerShell](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="a2f5c-114">**HPC Pack cluster with Linux compute nodes** - Deploy an HPC Pack cluster with Linux compute nodes on Azure using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="a2f5c-115">Vedere [Introduzione a Linux nodi di calcolo in un cluster HPC Pack in Azure](hpcpack-cluster.md) per hello prerequisiti e i passaggi per entrambe le opzioni.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-115">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for hello prerequisites and steps for either option.</span></span> <span data-ttu-id="a2f5c-116">Se si sceglie l'opzione di distribuzione di script di PowerShell hello, vedere file di configurazione di esempio hello nei file di esempio hello alla fine di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-116">If you choose hello PowerShell script deployment option, see hello sample configuration file in hello sample files at hello end of this article.</span></span> <span data-ttu-id="a2f5c-117">Questo file consente di configurare un cluster HPC Pack basato su Azure costituito da un nodo head di Windows Server 2012 R2 e quattro nodi di calcolo CentOS 6.6 di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-117">This file configures an Azure-based HPC Pack cluster consisting of a Windows Server 2012 R2 head node and four size Large CentOS 6.6 compute nodes.</span></span> <span data-ttu-id="a2f5c-118">Personalizzare questo file in base all'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-118">Customize this file as needed for your environment.</span></span>
* <span data-ttu-id="a2f5c-119">**File di esercitazione e software NAMD** -software scaricare NAMD per Linux da hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) sito (è richiesta la registrazione).</span><span class="sxs-lookup"><span data-stu-id="a2f5c-119">**NAMD software and tutorial files** - Download NAMD software for Linux from hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registration required).</span></span> <span data-ttu-id="a2f5c-120">In questo articolo si basa sul NAMD versione 2.10 e utilizza hello [Linux-x86_64 (64 bit Intel o AMD con Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archivio.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-120">This article is based on NAMD version 2.10, and uses hello [Linux-x86_64 (64-bit Intel/AMD with Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive.</span></span> <span data-ttu-id="a2f5c-121">Inoltre scaricare hello [file delle esercitazioni NAMD](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span><span class="sxs-lookup"><span data-stu-id="a2f5c-121">Also download hello [NAMD tutorial files](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span></span> <span data-ttu-id="a2f5c-122">download Hello sono file con estensione tar, sono necessari un file hello tooextract dello strumento di Windows nel nodo head del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-122">hello downloads are .tar files, and you need a Windows tool tooextract hello files on hello cluster head node.</span></span> <span data-ttu-id="a2f5c-123">file hello tooextract, seguire le istruzioni di hello più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-123">tooextract hello files, follow hello instructions later in this article.</span></span> 
* <span data-ttu-id="a2f5c-124">**VMD** (facoltativo): risultati hello toosee del processo NAMD, scaricare e installare il programma di visualizzazione molecolare hello [VMD](http://www.ks.uiuc.edu/Research/vmd/) in un computer di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-124">**VMD** (optional) - toosee hello results of your NAMD job, download and install hello molecular visualization program [VMD](http://www.ks.uiuc.edu/Research/vmd/) on a computer of your choice.</span></span> <span data-ttu-id="a2f5c-125">la versione corrente di Hello è 1.9.2.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-125">hello current version is 1.9.2.</span></span> <span data-ttu-id="a2f5c-126">Vedere hello VMD scaricare tooget sito avviata.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-126">See hello VMD download site tooget started.</span></span>  

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="a2f5c-127">Configurare il trust reciproco tra i nodi di calcolo</span><span class="sxs-lookup"><span data-stu-id="a2f5c-127">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="a2f5c-128">Esecuzione di un processo tra nodi in più nodi di Linux richiede hello nodi tootrust tra loro (da **rsh** o **ssh**).</span><span class="sxs-lookup"><span data-stu-id="a2f5c-128">Running a cross-node job on multiple Linux nodes requires hello nodes tootrust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="a2f5c-129">Quando si crea il cluster di HPC Pack hello con script di distribuzione IaaS di Microsoft HPC Pack hello, script hello imposta automaticamente permanente reciproca relazione di trust per l'account amministratore hello specificato.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-129">When you create hello HPC Pack cluster with hello Microsoft HPC Pack IaaS deployment script, hello script automatically sets up permanent mutual trust for hello administrator account you specify.</span></span> <span data-ttu-id="a2f5c-130">Per gli utenti non amministratori creati nel dominio del cluster di hello, è necessario tooset temporaneo reciproca relazione di trust tra i nodi di hello quando un processo viene allocato toothem.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-130">For non-administrator users you create in hello cluster's domain, you have tooset up temporary mutual trust among hello nodes when a job is allocated toothem.</span></span> <span data-ttu-id="a2f5c-131">Infine, l'eliminazione di relazione hello al termine il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-131">Then, destroy hello relationship after hello job is complete.</span></span> <span data-ttu-id="a2f5c-132">toodo, per ogni utente, fornire un cluster di toohello coppia di chiavi RSA quali HPC Pack usa una relazione di trust tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-132">toodo this for each user, provide an RSA key pair toohello cluster which HPC Pack uses tooestablish hello trust relationship.</span></span> <span data-ttu-id="a2f5c-133">Di seguito sono riportate le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-133">Instructions follow.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="a2f5c-134">Generare una coppia di chiavi RSA</span><span class="sxs-lookup"><span data-stu-id="a2f5c-134">Generate an RSA key pair</span></span>
<span data-ttu-id="a2f5c-135">È facile toogenerate una coppia di chiavi RSA, che contiene una chiave pubblica e una chiave privata, eseguendo hello Linux **ssh-keygen** comando.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-135">It's easy toogenerate an RSA key pair, which contains a public key and a private key, by running hello Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="a2f5c-136">Accedere tooa computer Linux.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-136">Log on tooa Linux computer.</span></span>
2. <span data-ttu-id="a2f5c-137">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a2f5c-137">Run hello following command:</span></span>
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="a2f5c-138">Premere **invio** toouse impostazioni predefinite di hello fino a quando non viene completato hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-138">Press **Enter** toouse hello default settings until hello command is completed.</span></span> <span data-ttu-id="a2f5c-139">Non immettere una passphrase. Quando viene richiesta una password, è sufficiente premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-139">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Generare una coppia di chiavi RSA][keygen]
3. <span data-ttu-id="a2f5c-141">Cambiare directory toohello ~/.ssh directory.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-141">Change directory toohello ~/.ssh directory.</span></span> <span data-ttu-id="a2f5c-142">la chiave privata di Hello viene archiviata nella chiave pubblica id_rsa e hello id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-142">hello private key is stored in id_rsa and hello public key in id_rsa.pub.</span></span>
   
   ![Chiavi pubbliche e private][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a><span data-ttu-id="a2f5c-144">Aggiungere cluster HPC Pack toohello di hello coppia di chiavi</span><span class="sxs-lookup"><span data-stu-id="a2f5c-144">Add hello key pair toohello HPC Pack cluster</span></span>
1. <span data-ttu-id="a2f5c-145">[Connessione Desktop remoto](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello nodo head VM utilizzando hello le credenziali di dominio fornito al momento della distribuzione cluster hello (ad esempio, hpc\clusteradmin).</span><span class="sxs-lookup"><span data-stu-id="a2f5c-145">[Connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, hpc\clusteradmin).</span></span> <span data-ttu-id="a2f5c-146">Gestire i cluster di hello dal nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-146">You manage hello cluster from hello head node.</span></span>
2. <span data-ttu-id="a2f5c-147">Usare toocreate procedure di Windows Server standard account utente di dominio nel dominio di Active Directory del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-147">Use standard Windows Server procedures toocreate a domain user account in hello cluster's Active Directory domain.</span></span> <span data-ttu-id="a2f5c-148">Ad esempio, è possibile utilizzare hello utente di Active Directory e lo strumento di computer nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-148">For example, use hello Active Directory User and Computers tool on hello head node.</span></span> <span data-ttu-id="a2f5c-149">esempi di Hello in questo articolo presuppongono che crei un utente di dominio denominato hpcuser nel dominio hpclab hello (hpclab\hpcuser).</span><span class="sxs-lookup"><span data-stu-id="a2f5c-149">hello examples in this article assume you create a domain user named hpcuser in hello hpclab domain (hpclab\hpcuser).</span></span>
3. <span data-ttu-id="a2f5c-150">Aggiungere il cluster HPC Pack toohello di hello dominio utente come un utente del cluster.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-150">Add hello domain user toohello HPC Pack cluster as a cluster user.</span></span> <span data-ttu-id="a2f5c-151">Per le istruzioni, vedere [Aggiungere o rimuovere utenti del cluster](https://technet.microsoft.com/library/ff919330.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2f5c-151">For instructions, see [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).</span></span>
4. <span data-ttu-id="a2f5c-152">Creare un file denominato C:\cred.xml e copia hello RSA dati della chiave al suo interno.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-152">Create a file named C:\cred.xml and copy hello RSA key data into it.</span></span> <span data-ttu-id="a2f5c-153">È possibile trovare un esempio in hello file di esempio alla fine di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-153">You can find an example in hello sample files at hello end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. <span data-ttu-id="a2f5c-154">Aprire un prompt dei comandi e immettere hello comando hello tooset credenziali dati per conto di hello hpclab\hpcuser seguente.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-154">Open a Command Prompt and enter hello following command tooset hello credentials data for hello hpclab\hpcuser account.</span></span> <span data-ttu-id="a2f5c-155">Utilizzare hello **extendeddata** toopass parametro hello Nome file hello C:\cred.xml creato per i dati chiave hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-155">You use hello **extendeddata** parameter toopass hello name of hello C:\cred.xml file you created for hello key data.</span></span>
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="a2f5c-156">Questo comando viene completato correttamente senza output.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-156">This command completes successfully without output.</span></span> <span data-ttu-id="a2f5c-157">Dopo aver impostato le credenziali di hello per gli account utente di hello che è necessario toorun processi, archiviare file cred.xml hello in un percorso sicuro o eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-157">After setting hello credentials for hello user accounts you need toorun jobs, store hello cred.xml file in a secure location, or delete it.</span></span>
6. <span data-ttu-id="a2f5c-158">Se è stato generato hello coppia di chiavi RSA in uno dei nodi di Linux, tenere presente le chiavi di hello toodelete dopo aver terminato di utilizzare tali.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-158">If you generated hello RSA key pair on one of your Linux nodes, remember toodelete hello keys after you finish using them.</span></span> <span data-ttu-id="a2f5c-159">HPC Pack non configura il trust reciproco se rileva un file id_rsa o id_rsa.pub esistente.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-159">HPC Pack does not set up mutual trust if it finds an existing id_rsa file or id_rsa.pub file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a2f5c-160">Non è consigliabile eseguendo un processo di Linux come amministratore del cluster in un cluster condiviso, poiché viene eseguito un processo inviato da un amministratore account radice hello in nodi di Linux hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-160">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under hello root account on hello Linux nodes.</span></span> <span data-ttu-id="a2f5c-161">Un processo inviato da un utente non amministratore viene eseguito con un account utente locale di Linux con stesso nome utente di un processo di hello hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-161">A job submitted by a non-administrator user runs under a local Linux user account with hello same name as hello job user.</span></span> <span data-ttu-id="a2f5c-162">In questo caso, HPC Pack imposta reciproca relazione di trust per questo utente di Linux in tutti i nodi di hello allocati toohello processo.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-162">In this case, HPC Pack sets up mutual trust for this Linux user across all hello nodes allocated toohello job.</span></span> <span data-ttu-id="a2f5c-163">È possibile impostare l'utente di Linux hello manualmente nei nodi di Linux hello prima di eseguire il processo di hello o HPC Pack Crea utente hello automaticamente quando il processo di hello viene inviato.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-163">You can set up hello Linux user manually on hello Linux nodes before running hello job, or HPC Pack creates hello user automatically when hello job is submitted.</span></span> <span data-ttu-id="a2f5c-164">HPC Pack Crea utente hello, HPC Pack eliminata dopo il completamento del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-164">If HPC Pack creates hello user, HPC Pack deletes it after hello job completes.</span></span> <span data-ttu-id="a2f5c-165">tooreduce minaccia alla sicurezza, le chiavi vengono rimosse al termine del processo di hello nei nodi hello hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-165">tooreduce security threat, hello keys are removed after hello job completes on hello nodes.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="a2f5c-166">Configurare una condivisione di file per i nodi Linux</span><span class="sxs-lookup"><span data-stu-id="a2f5c-166">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="a2f5c-167">Ora configurare una condivisione file SMB e montare una cartella condivisa di hello in tutti i nodi tooallow hello Linux nodi tooaccess NAMD file Linux con un percorso comune.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-167">Now set up an SMB file share, and mount hello shared folder on all Linux nodes tooallow hello Linux nodes tooaccess NAMD files with a common path.</span></span> <span data-ttu-id="a2f5c-168">Di seguito sono passaggi toomount una cartella condivisa nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-168">Following are steps toomount a shared folder on hello head node.</span></span> <span data-ttu-id="a2f5c-169">Una condivisione è consigliata per le distribuzioni, ad esempio CentOS 6.6 che attualmente non supportano il servizio di Azure File hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-169">A share is recommended for distributions such as CentOS 6.6 that currently don’t support hello Azure File service.</span></span> <span data-ttu-id="a2f5c-170">Se i nodi di Linux supportano una condivisione di File di Azure, vedere [come archiviazione di File di Azure con Linux toouse](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a2f5c-170">If your Linux nodes support an Azure File share, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="a2f5c-171">Per altre opzioni di condivisione dei file con HPC Pack, vedere [Introduzione ai nodi di calcolo Linux in un cluster HPC Pack in Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="a2f5c-171">For additional file sharing options with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="a2f5c-172">Creare una cartella nel nodo head hello e condividerlo tooEveryone impostando i privilegi di lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-172">Create a folder on hello head node, and share it tooEveryone by setting Read/Write privileges.</span></span> <span data-ttu-id="a2f5c-173">In questo esempio, \\ \\CentOS66HN\Namd è il nome di hello della cartella di hello, dove CentOS66HN è il nome host hello del nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-173">In this example, \\\\CentOS66HN\Namd is hello name of hello folder, where CentOS66HN is hello host name of hello head node.</span></span>
2. <span data-ttu-id="a2f5c-174">Creare una sottocartella denominata namd2 nella cartella condivisa hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-174">Create a subfolder named namd2 in hello shared folder.</span></span> <span data-ttu-id="a2f5c-175">All'interno di namd2, creare un'altra sottocartella namdsample.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-175">In namd2, create another subfolder named namdsample.</span></span>
3. <span data-ttu-id="a2f5c-176">Estrarre i file NAMD hello nella cartella hello utilizzando una versione di Windows di **tar** o un'altra utilità di Windows che opera su tar archivi.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-176">Extract hello NAMD files in hello folder by using a Windows version of **tar** or another Windows utility that operates on .tar archives.</span></span> 
   
   * <span data-ttu-id="a2f5c-177">Estrarre troppo archivio tar di hello NAMD\\\\CentOS66HN\Namd\namd2.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-177">Extract hello NAMD tar archive too\\\\CentOS66HN\Namd\namd2.</span></span>
   * <span data-ttu-id="a2f5c-178">Estrarre i file delle esercitazioni hello in \\ \\CentOS66HN\Namd\namd2\namdsample.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-178">Extract hello tutorial files under \\\\CentOS66HN\Namd\namd2\namdsample.</span></span>
4. <span data-ttu-id="a2f5c-179">Aprire una finestra di Windows PowerShell ed eseguire i seguenti comandi toomount hello cartella condivisa in nodi di Linux hello hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-179">Open a Windows PowerShell window and run hello following commands toomount hello shared folder on hello Linux nodes.</span></span>
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="a2f5c-180">Hello primo comando crea una cartella denominata /namd2 in tutti i nodi nel gruppo LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-180">hello first command creates a folder named /namd2 on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="a2f5c-181">comando secondo Hello Monta //CentOS66HN/Namd/namd2 cartella hello condivise nella cartella hello con dir_mode e file_mode too777 di set di bit.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-181">hello second command mounts hello shared folder //CentOS66HN/Namd/namd2 onto hello folder with dir_mode and file_mode bits set too777.</span></span> <span data-ttu-id="a2f5c-182">Hello *username* e *password* in hello comando deve essere credenziali hello di un utente nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-182">hello *username* and *password* in hello command should be hello credentials of a user on hello head node.</span></span>

> [!NOTE]
> <span data-ttu-id="a2f5c-183">Hello "\\`" simbolo nel secondo comando hello è un simbolo di escape per PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-183">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="a2f5c-184">"\\`,"significa hello"," (carattere virgola) è una parte del comando hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-184">“\\`,” means hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

## <a name="create-a-bash-script-toorun-a-namd-job"></a><span data-ttu-id="a2f5c-185">Creare un toorun script Bash un processo NAMD</span><span class="sxs-lookup"><span data-stu-id="a2f5c-185">Create a Bash script toorun a NAMD job</span></span>
<span data-ttu-id="a2f5c-186">Il processo NAMD richiede un *nodelist* file per **charmrun** toouse nodi all'avvio di processi NAMD svariate hello toodetermine.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-186">Your NAMD job needs a *nodelist* file for **charmrun** toodetermine hello number of nodes toouse when starting NAMD processes.</span></span> <span data-ttu-id="a2f5c-187">Utilizzare uno script Bash che genera file nodelist hello e viene eseguito **charmrun** con questo file nodelist.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-187">You use a Bash script that generates hello nodelist file and runs **charmrun** with this nodelist file.</span></span> <span data-ttu-id="a2f5c-188">È quindi possibile inviare un processo NAMD in HPC Cluster Manager per chiamare questo script.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-188">You can then submit a NAMD job in HPC Cluster Manager that calls this script.</span></span>

<span data-ttu-id="a2f5c-189">Utilizzando un editor di testo di propria scelta, è possibile creare uno script Bash nella cartella /namd2 hello contenente i file di programma NAMD hello e denominarlo hpccharmrun.sh. Per una rapida modello di prova, copiare script hpccharmrun.sh di esempio hello fornito alla fine di hello di questo articolo e andare troppo[invia un processo NAMD](#submit-a-namd-job).</span><span class="sxs-lookup"><span data-stu-id="a2f5c-189">Using a text editor of your choice, create a Bash script in hello /namd2 folder containing hello NAMD program files and name it hpccharmrun.sh. For a quick proof of concept, copy hello example hpccharmrun.sh script provided at hello end of this article and go too[Submit a NAMD job](#submit-a-namd-job).</span></span>

> [!TIP]
> <span data-ttu-id="a2f5c-190">Salvare lo script come file di testo con terminazioni riga Linux (solo LF, non CR LF),</span><span class="sxs-lookup"><span data-stu-id="a2f5c-190">Save your script as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="a2f5c-191">In questo modo si garantisce il corretto funzionamento in nodi di Linux hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-191">This ensures that it runs properly on hello Linux nodes.</span></span>
> 
> 

<span data-ttu-id="a2f5c-192">Di seguito sono descritte nel dettaglio le operazioni eseguite dallo script Bash.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-192">Following are details about what this bash script does.</span></span> 

1. <span data-ttu-id="a2f5c-193">Definire alcune variabili.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-193">Define some variables.</span></span>
   
   ```bash
   #!/bin/bash
   
   # hello path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. <span data-ttu-id="a2f5c-194">Ottenere informazioni sul nodo dalle variabili di ambiente hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-194">Get node information from hello environment variables.</span></span> <span data-ttu-id="a2f5c-195">$NODESCORES archivia un elenco di parole suddivise da $CCP_NODES_CORES.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-195">$NODESCORES stores a list of split words from $CCP_NODES_CORES.</span></span> <span data-ttu-id="a2f5c-196">$COUNT è pari a hello $NODESCORES.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-196">$COUNT is hello size of $NODESCORES.</span></span>
   
   ```
   # Get node information from hello environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   <span data-ttu-id="a2f5c-197">formato di Hello per hello $CCP_NODES_CORES variabile è il seguente:</span><span class="sxs-lookup"><span data-stu-id="a2f5c-197">hello format for hello $CCP_NODES_CORES variable is as follows:</span></span>
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   <span data-ttu-id="a2f5c-198">Questa variabile Elenca numero totale di hello di nodi, i nomi dei nodi e numero di core in ogni nodo allocati toohello processo.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-198">This variable lists hello total number of nodes, node names, and number of cores on each node that are allocated toohello job.</span></span> <span data-ttu-id="a2f5c-199">Ad esempio, se il processo di hello deve 10 core toorun, valore hello $CCP_NODES_CORES è simile a:</span><span class="sxs-lookup"><span data-stu-id="a2f5c-199">For example, if hello job needs 10 cores toorun, hello value of $CCP_NODES_CORES is similar to:</span></span>
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. <span data-ttu-id="a2f5c-200">Se non è una variabile di hello $CCP_NODES_CORES, avviare **charmrun** direttamente.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-200">If hello $CCP_NODES_CORES variable is not set, start **charmrun** directly.</span></span> <span data-ttu-id="a2f5c-201">È consigliabile seguire questa procedura solo quando si esegue lo script direttamente nei nodi Linux.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-201">(This should only occur when you run this script directly on your Linux nodes.)</span></span>
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. <span data-ttu-id="a2f5c-202">In alternativa, creare un file nodelist per **charmrun**.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-202">Or create a nodelist file for **charmrun**.</span></span>
   
   ```
   else
     # Create hello nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write hello head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into hello nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. <span data-ttu-id="a2f5c-203">Eseguire **charmrun** con file nodelist hello, ottenere lo stato restituito e rimuovere file nodelist hello alla fine di hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-203">Run **charmrun** with hello nodelist file, get its return status, and remove hello nodelist file at hello end.</span></span>
   
   <span data-ttu-id="a2f5c-204">${CCP_NUMCPUS} è impostata dal nodo head di HPC Pack hello un'altra variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-204">${CCP_NUMCPUS} is another environment variable set by hello HPC Pack head node.</span></span> <span data-ttu-id="a2f5c-205">Archivia il numero di hello di core totale allocato toothis processo.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-205">It stores hello number of total cores allocated toothis job.</span></span> <span data-ttu-id="a2f5c-206">Usato da numero hello toospecify di processi per charmrun.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-206">We use it toospecify hello number of processes for charmrun.</span></span>
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. <span data-ttu-id="a2f5c-207">Uscita con hello **charmrun** restituiscono lo stato.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-207">Exit with hello **charmrun** return status.</span></span>
   
   ```
   exit ${RTNSTS}
   ```

<span data-ttu-id="a2f5c-208">Di seguito è informazioni hello nel file hello nodelist quale script hello genera l'errore:</span><span class="sxs-lookup"><span data-stu-id="a2f5c-208">Following is hello information in hello nodelist file, which hello script generates:</span></span>

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

<span data-ttu-id="a2f5c-209">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a2f5c-209">For example:</span></span>

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a><span data-ttu-id="a2f5c-210">Inviare un processo NAMD</span><span class="sxs-lookup"><span data-stu-id="a2f5c-210">Submit a NAMD job</span></span>
<span data-ttu-id="a2f5c-211">Si è ora pronto toosubmit un processo NAMD in Gestione Cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-211">Now you are ready toosubmit a NAMD job in HPC Cluster Manager.</span></span>

1. <span data-ttu-id="a2f5c-212">Connettersi tooyour nodo head del cluster e avviare HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-212">Connect tooyour cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="a2f5c-213">In **la gestione delle risorse**, assicurarsi che i nodi di calcolo di hello Linux hello **Online** stato.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-213">In **Resource Management**, ensure that hello Linux compute nodes are in hello **Online** state.</span></span> <span data-ttu-id="a2f5c-214">Se lo stato è diverso, selezionarli e fare clic su **Portare Online**.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-214">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="a2f5c-215">In **Job Management** (Gestione processi) fare clic su **New Job** (Nuovo processo).</span><span class="sxs-lookup"><span data-stu-id="a2f5c-215">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="a2f5c-216">Immettere un nome per il processo, ad esempio *hpccharmrun*.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-216">Enter a name for job such as *hpccharmrun*.</span></span>
   
   ![Nuovo processo HPC][namd_job]
5. <span data-ttu-id="a2f5c-218">In hello **i dettagli dei processi** nella pagina **risorse di processo**, selezionare il tipo di hello di risorsa come **nodo** e set hello **minimo** too3.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-218">On hello **Job Details** page, under **Job Resources**, select hello type of resource as **Node** and set hello **Minimum** too3.</span></span> <span data-ttu-id="a2f5c-219">, si esegue il processo di hello in tre nodi di Linux e ogni nodo dispone di quattro core.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-219">, we run hello job on three Linux nodes and each node has four cores.</span></span>
   
   ![Risorse del processo][job_resources]
6. <span data-ttu-id="a2f5c-221">Fare clic su **modifica attività** in hello spostamento a sinistra e quindi fare clic su **Aggiungi** tooadd un processo toohello di attività.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-221">Click **Edit Tasks** in hello left navigation, and then click **Add** tooadd a task toohello job.</span></span>    
7. <span data-ttu-id="a2f5c-222">In hello **i dettagli delle attività e il reindirizzamento i/o** pagina hello set seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="a2f5c-222">On hello **Task Details and I/O Redirection** page, set hello following values:</span></span>
   
   * <span data-ttu-id="a2f5c-223">**Riga di comando** -
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span><span class="sxs-lookup"><span data-stu-id="a2f5c-223">**Command line** -
`/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span></span>
     
     > [!TIP]
     > <span data-ttu-id="a2f5c-224">Hello riga di comando precedente è un comando singolo senza interruzioni di riga.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-224">hello preceding command line is a single command without line breaks.</span></span> <span data-ttu-id="a2f5c-225">Esegue il wrapping tooappear su più righe in **riga di comando**.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-225">It wraps tooappear on several lines under **Command line**.</span></span>
     > 
     > 
   * <span data-ttu-id="a2f5c-226">**Working directory** - /namd2</span><span class="sxs-lookup"><span data-stu-id="a2f5c-226">**Working directory** - /namd2</span></span>
   * <span data-ttu-id="a2f5c-227">**Minimum** - 3</span><span class="sxs-lookup"><span data-stu-id="a2f5c-227">**Minimum** - 3</span></span>
     
     ![Dettagli dell'attività][task_details]
     
     > [!NOTE]
     > <span data-ttu-id="a2f5c-229">Impostare la directory di lavoro hello qui perché **charmrun** tenta toonavigate toohello stessa directory di lavoro in ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-229">You set hello working directory here because **charmrun** tries toonavigate toohello same working directory on each node.</span></span> <span data-ttu-id="a2f5c-230">Se non è impostata, la directory di lavoro hello HPC Pack inizia comando hello in una cartella denominata in modo casuale creata su uno dei nodi di Linux hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-230">If hello working directory isn't set, HPC Pack starts hello command in a randomly named folder created on one of hello Linux nodes.</span></span> <span data-ttu-id="a2f5c-231">In questo modo l'errore seguente in hello hello altri nodi: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid questo problema, specificare un percorso di cartella accessibile da tutti i nodi come directory di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-231">This causes hello following error on hello other nodes: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid this problem, specify a folder path that can be accessed by all nodes as hello working directory.</span></span>
     > 
     > 
8. <span data-ttu-id="a2f5c-232">Fare clic su **OK** e quindi fare clic su **Invia** toorun questo processo.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-232">Click **OK** and then click **Submit** toorun this job.</span></span>
   
   <span data-ttu-id="a2f5c-233">Per impostazione predefinita, HPC Pack invia il processo di hello come account utente corrente.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-233">By default, HPC Pack submits hello job as your current logged-on user account.</span></span> <span data-ttu-id="a2f5c-234">Una finestra di dialogo è possibile che richieda nome utente di tooenter hello e una password dopo aver fatto clic **Invia**.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-234">A dialog box might prompt you tooenter hello user name and password after you click **Submit**.</span></span>
   
   ![Credenziali del processo][creds]
   
   <span data-ttu-id="a2f5c-236">In alcune condizioni, HPC Pack memorizza informazioni utente di hello prima di input e non visualizza questa finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-236">Under some conditions, HPC Pack remembers hello user information you input before and doesn't show this dialog box.</span></span> <span data-ttu-id="a2f5c-237">toomake HPC Pack visualizzarlo nuovamente, immettere hello comando al Prompt di comando seguente e quindi inviare il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-237">toomake HPC Pack show it again, enter hello following command at a Command Prompt and then submit hello job.</span></span>
   
   ```command
   hpccred delcreds
   ```
9. <span data-ttu-id="a2f5c-238">il processo di Hello richiede diversi minuti toofinish.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-238">hello job takes several minutes toofinish.</span></span>
10. <span data-ttu-id="a2f5c-239">Trovare i log di processi hello in \\ <headnodeName>\Namd\namd2\namd2_hpccharmrun.log e hello output file \\ <headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-239">Find hello job log at \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log and hello output files in \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span></span>
11. <span data-ttu-id="a2f5c-240">Facoltativamente, avviare VMD tooview i risultati del processo.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-240">Optionally, start VMD tooview your job results.</span></span> <span data-ttu-id="a2f5c-241">passaggi di Hello per la visualizzazione dei file di output di hello NAMD (in questo caso, una molecola proteine ubiquitin in una sfera di acqua) esulano dall'ambito hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a2f5c-241">hello steps for visualizing hello NAMD output files (in this case, a ubiquitin protein molecule in a water sphere) are beyond hello scope of this article.</span></span> <span data-ttu-id="a2f5c-242">Per informazioni dettagliate, vedere l' [esercitazione relativa a NAMD](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) .</span><span class="sxs-lookup"><span data-stu-id="a2f5c-242">See [NAMD Tutorial](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) for details.</span></span>
    
    ![Risultati del processo][vmd_view]

## <a name="sample-files"></a><span data-ttu-id="a2f5c-244">File di esempio</span><span class="sxs-lookup"><span data-stu-id="a2f5c-244">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="a2f5c-245">File di configurazione XML di esempio per la distribuzione di cluster tramite script PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2f5c-245">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
      <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS66HN</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS66LN-%00%</VMNamePattern>
    <ServiceName>MyLnxCNService</ServiceName>
     <VMSize>Large</VMSize>
     <NodeCount>4</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-66-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>    
```

### <a name="sample-credxml-file"></a><span data-ttu-id="a2f5c-246">File cred.xml di esempio</span><span class="sxs-lookup"><span data-stu-id="a2f5c-246">Sample cred.xml file</span></span>
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

### <a name="sample-hpccharmrunsh-script"></a><span data-ttu-id="a2f5c-247">Script hpccharmrun.sh di esempio</span><span class="sxs-lookup"><span data-stu-id="a2f5c-247">Sample hpccharmrun.sh script</span></span>
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
# Charmrun command
CHARMRUN=${SCRIPT_PATH}/charmrun
# Argument of ++nodelist
NODELIST_OPT="++nodelist"
# Argument of ++p
NUMPROCESS="+p"

# Get node information from ENVs
# CCP_NODES_CORES=3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 4
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # If CCP_NODES_CORES is not found or is empty, just run hello charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create hello nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write hello head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into hello nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello charmrun with nodelist arg
    #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
    ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}
```

 

<!--Image references-->
[keygen]:media/hpcpack-cluster-namd/keygen.png
[keys]:media/hpcpack-cluster-namd/keys.png
[namd_job]:media/hpcpack-cluster-namd/namd_job.png
[job_resources]:media/hpcpack-cluster-namd/job_resources.png
[creds]:media/hpcpack-cluster-namd/creds.png
[task_details]:media/hpcpack-cluster-namd/task_details.png
[vmd_view]:media/hpcpack-cluster-namd/vmd_view.png
