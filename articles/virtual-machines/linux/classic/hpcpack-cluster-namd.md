---
title: Eseguire NAMD con Microsoft HPC Pack sulle VM Linux | Microsoft Docs
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
ms.openlocfilehash: e31845f3d7aa08357b0e8a1b3b77d97302442ac3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a><span data-ttu-id="1208d-103">Eseguire NAMD con Microsoft HPC Pack su nodi di calcolo Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="1208d-103">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>
<span data-ttu-id="1208d-104">In questo articolo viene illustrato un modo per eseguire un carico di lavoro high-performance computing (HPC) Linux in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="1208d-104">This article shows you one way to run a Linux high-performance computing (HPC) workload on Azure virtual machines.</span></span> <span data-ttu-id="1208d-105">Si configura un cluster [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) su Azure con nodi di calcolo Linux e si esegue una simulazione [NAMD](http://www.ks.uiuc.edu/Research/namd/) per calcolare e visualizzare la struttura di un sistema biomolecolare di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="1208d-105">Here, you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster on Azure with Linux compute nodes and run a [NAMD](http://www.ks.uiuc.edu/Research/namd/) simulation to calculate and visualize the structure of a large biomolecular system.</span></span>  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* <span data-ttu-id="1208d-106">**NAMD** (ovvero programma Nanoscale Molecular Dynamics) è un pacchetto di dinamica molecolare parallela progettato per una simulazione a prestazioni elevate di grandi sistemi biomolecolari contenenti fino a milioni di atomi.</span><span class="sxs-lookup"><span data-stu-id="1208d-106">**NAMD** (for Nanoscale Molecular Dynamics program) is a parallel molecular dynamics package designed for high-performance simulation of large biomolecular systems containing up to millions of atoms.</span></span> <span data-ttu-id="1208d-107">Esempi di questi sistemi includono virus, strutture di celle e proteine di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="1208d-107">Examples of these systems include viruses, cell structures, and large proteins.</span></span> <span data-ttu-id="1208d-108">NAMD è scalabile fino a centinaia di core per simulazioni tipiche e fino a più di 500.000 core per le simulazioni più grandi.</span><span class="sxs-lookup"><span data-stu-id="1208d-108">NAMD scales to hundreds of cores for typical simulations and to more than 500,000 cores for the largest simulations.</span></span>
* <span data-ttu-id="1208d-109">**Microsoft HPC Pack** fornisce le funzionalità necessarie per eseguire applicazioni HPC e parallele su larga scala in cluster di computer locali o macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="1208d-109">**Microsoft HPC Pack** provides features to run large-scale HPC and parallel applications in clusters of on-premises computers or Azure virtual machines.</span></span> <span data-ttu-id="1208d-110">Sviluppato originariamente come soluzione per i carichi di lavoro HPC di Windows, HPC Pack supporta ora le applicazioni HPC che eseguono Linux su macchine virtuali del nodo di calcolo Linux distribuite in un cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="1208d-110">Originally developed as a solution for Windows HPC workloads, HPC Pack now supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="1208d-111">Per una panoramica, vedere [Introduzione all'uso di nodi di calcolo Linux in un cluster HPC Pack in Azure](hpcpack-cluster.md) .</span><span class="sxs-lookup"><span data-stu-id="1208d-111">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction.</span></span>

<span data-ttu-id="1208d-112">Per altre opzioni relative all'esecuzione di carichi di lavoro HPC in Linux e in Azure, vedere [Risorse tecniche per batch e high performance computing](../../../batch/batch-hpc-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="1208d-112">For other options to run Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/batch-hpc-solutions.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1208d-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1208d-113">Prerequisites</span></span>
* <span data-ttu-id="1208d-114">**Cluster HPC Pack con nodi di calcolo Linux**: distribuire un cluster HPC Pack con nodi di calcolo Linux in Azure usando un [modello di Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) o uno [script di Azure PowerShell](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="1208d-114">**HPC Pack cluster with Linux compute nodes** - Deploy an HPC Pack cluster with Linux compute nodes on Azure using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="1208d-115">Per i prerequisiti e i passaggi di entrambe le opzioni, vedere [Introduzione all'uso di nodi di calcolo Linux in un cluster HPC Pack in Azure](hpcpack-cluster.md) .</span><span class="sxs-lookup"><span data-stu-id="1208d-115">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for the prerequisites and steps for either option.</span></span> <span data-ttu-id="1208d-116">Se si sceglie l'opzione di distribuzione mediante uno script di PowerShell, vedere il file di configurazione di esempio al termine dell'articolo.</span><span class="sxs-lookup"><span data-stu-id="1208d-116">If you choose the PowerShell script deployment option, see the sample configuration file in the sample files at the end of this article.</span></span> <span data-ttu-id="1208d-117">Questo file consente di configurare un cluster HPC Pack basato su Azure costituito da un nodo head di Windows Server 2012 R2 e quattro nodi di calcolo CentOS 6.6 di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="1208d-117">This file configures an Azure-based HPC Pack cluster consisting of a Windows Server 2012 R2 head node and four size Large CentOS 6.6 compute nodes.</span></span> <span data-ttu-id="1208d-118">Personalizzare questo file in base all'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="1208d-118">Customize this file as needed for your environment.</span></span>
* <span data-ttu-id="1208d-119">**Software e file per le esercitazioni NAMD**: scaricare il software NAMD per Linux dal sito [NAMD](http://www.ks.uiuc.edu/Research/namd/). È richiesta la registrazione.</span><span class="sxs-lookup"><span data-stu-id="1208d-119">**NAMD software and tutorial files** - Download NAMD software for Linux from the [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registration required).</span></span> <span data-ttu-id="1208d-120">Questo articolo è basato sulla versione NAMD 2.10 e usa l'archivio [Linux-x86_64 (64-bit Intel/AMD con Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310).</span><span class="sxs-lookup"><span data-stu-id="1208d-120">This article is based on NAMD version 2.10, and uses the [Linux-x86_64 (64-bit Intel/AMD with Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive.</span></span> <span data-ttu-id="1208d-121">Scaricare anche i [file per le esercitazioni NAMD](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span><span class="sxs-lookup"><span data-stu-id="1208d-121">Also download the [NAMD tutorial files](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span></span> <span data-ttu-id="1208d-122">I download includono file con estensione .tar ed è necessario uno strumento di Windows per estrarre i file nel nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="1208d-122">The downloads are .tar files, and you need a Windows tool to extract the files on the cluster head node.</span></span> <span data-ttu-id="1208d-123">Per estrarre i file, seguire le istruzioni indicate più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="1208d-123">To extract the files, follow the instructions later in this article.</span></span> 
* <span data-ttu-id="1208d-124">**VMD** (facoltativo) - Per visualizzare i risultati del processo NAMD, scaricare e installare il programma di visualizzazione molecolare [VMD](http://www.ks.uiuc.edu/Research/vmd/) nel computer desiderato.</span><span class="sxs-lookup"><span data-stu-id="1208d-124">**VMD** (optional) - To see the results of your NAMD job, download and install the molecular visualization program [VMD](http://www.ks.uiuc.edu/Research/vmd/) on a computer of your choice.</span></span> <span data-ttu-id="1208d-125">La versione corrente è 1.9.2.</span><span class="sxs-lookup"><span data-stu-id="1208d-125">The current version is 1.9.2.</span></span> <span data-ttu-id="1208d-126">Per iniziare, vedere il sito per il download di VMD.</span><span class="sxs-lookup"><span data-stu-id="1208d-126">See the VMD download site to get started.</span></span>  

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="1208d-127">Configurare il trust reciproco tra i nodi di calcolo</span><span class="sxs-lookup"><span data-stu-id="1208d-127">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="1208d-128">L'esecuzione di un processo su più nodi Linux richiede una relazione di trust tra i nodi (tramite **rsh** o **ssh**).</span><span class="sxs-lookup"><span data-stu-id="1208d-128">Running a cross-node job on multiple Linux nodes requires the nodes to trust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="1208d-129">Quando si crea il cluster HPC Pack con lo script di distribuzione IaaS di Microsoft HPC Pack, lo script configura automaticamente un trust reciproco permanente per l'account amministratore specificato.</span><span class="sxs-lookup"><span data-stu-id="1208d-129">When you create the HPC Pack cluster with the Microsoft HPC Pack IaaS deployment script, the script automatically sets up permanent mutual trust for the administrator account you specify.</span></span> <span data-ttu-id="1208d-130">Per gli utenti non amministratori creati nel dominio del cluster è necessario configurare una relazione di trust reciproco temporanea tra i nodi in caso di allocazione di un processo.</span><span class="sxs-lookup"><span data-stu-id="1208d-130">For non-administrator users you create in the cluster's domain, you have to set up temporary mutual trust among the nodes when a job is allocated to them.</span></span> <span data-ttu-id="1208d-131">Quindi, eliminare la relazione dopo il completamento del processo.</span><span class="sxs-lookup"><span data-stu-id="1208d-131">Then, destroy the relationship after the job is complete.</span></span> <span data-ttu-id="1208d-132">Per eseguire questa operazione per ogni utente, fornire una coppia di chiavi RSA al cluster usato da HPC Pack per stabilire la relazione di trust.</span><span class="sxs-lookup"><span data-stu-id="1208d-132">To do this for each user, provide an RSA key pair to the cluster which HPC Pack uses to establish the trust relationship.</span></span> <span data-ttu-id="1208d-133">Di seguito sono riportate le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="1208d-133">Instructions follow.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="1208d-134">Generare una coppia di chiavi RSA</span><span class="sxs-lookup"><span data-stu-id="1208d-134">Generate an RSA key pair</span></span>
<span data-ttu-id="1208d-135">Per generare con facilità una coppia di chiavi RSA, che contiene una chiave pubblica e una chiave privata, eseguire il comando **ssh-keygen** di Linux.</span><span class="sxs-lookup"><span data-stu-id="1208d-135">It's easy to generate an RSA key pair, which contains a public key and a private key, by running the Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="1208d-136">Accedere a un computer Linux.</span><span class="sxs-lookup"><span data-stu-id="1208d-136">Log on to a Linux computer.</span></span>
2. <span data-ttu-id="1208d-137">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1208d-137">Run the following command:</span></span>
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="1208d-138">Premere **Invio** per usare le impostazioni predefinite fino al completamento del comando.</span><span class="sxs-lookup"><span data-stu-id="1208d-138">Press **Enter** to use the default settings until the command is completed.</span></span> <span data-ttu-id="1208d-139">Non immettere una passphrase. Quando viene richiesta una password, è sufficiente premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="1208d-139">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Generare una coppia di chiavi RSA][keygen]
3. <span data-ttu-id="1208d-141">Passare alla directory ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="1208d-141">Change directory to the ~/.ssh directory.</span></span> <span data-ttu-id="1208d-142">La chiave privata viene archiviata in id_rsa e la chiave pubblica in id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="1208d-142">The private key is stored in id_rsa and the public key in id_rsa.pub.</span></span>
   
   ![Chiavi pubbliche e private][keys]

### <a name="add-the-key-pair-to-the-hpc-pack-cluster"></a><span data-ttu-id="1208d-144">Aggiungere la coppia di chiavi al cluster HPC Pack</span><span class="sxs-lookup"><span data-stu-id="1208d-144">Add the key pair to the HPC Pack cluster</span></span>
1. <span data-ttu-id="1208d-145">[Connettersi tramite Desktop remoto](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) alla VM con nodo head usando le credenziali del dominio specificate durante la distribuzione del cluster, ad esempio hpc\clusteradmin.</span><span class="sxs-lookup"><span data-stu-id="1208d-145">[Connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to the head node VM using the domain credentials you provided when you deployed the cluster (for example, hpc\clusteradmin).</span></span> <span data-ttu-id="1208d-146">Il cluster viene gestito dal nodo head.</span><span class="sxs-lookup"><span data-stu-id="1208d-146">You manage the cluster from the head node.</span></span>
2. <span data-ttu-id="1208d-147">Usare le procedure standard di Windows Server per creare un account utente di dominio nel dominio di Active Directory del cluster.</span><span class="sxs-lookup"><span data-stu-id="1208d-147">Use standard Windows Server procedures to create a domain user account in the cluster's Active Directory domain.</span></span> <span data-ttu-id="1208d-148">Ad esempio, usare lo strumento Utenti e computer di Active Directory sul nodo head.</span><span class="sxs-lookup"><span data-stu-id="1208d-148">For example, use the Active Directory User and Computers tool on the head node.</span></span> <span data-ttu-id="1208d-149">Gli esempi in questo articolo presuppongono che venga creato un utente di dominio denominato hpclab\hpcuser nel dominio hpclab (hpclab\hpcuser).</span><span class="sxs-lookup"><span data-stu-id="1208d-149">The examples in this article assume you create a domain user named hpcuser in the hpclab domain (hpclab\hpcuser).</span></span>
3. <span data-ttu-id="1208d-150">Aggiungere l'utente di dominio al cluster HPC Pack come utente del cluster.</span><span class="sxs-lookup"><span data-stu-id="1208d-150">Add the domain user to the HPC Pack cluster as a cluster user.</span></span> <span data-ttu-id="1208d-151">Per le istruzioni, vedere [Aggiungere o rimuovere utenti del cluster](https://technet.microsoft.com/library/ff919330.aspx).</span><span class="sxs-lookup"><span data-stu-id="1208d-151">For instructions, see [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).</span></span>
4. <span data-ttu-id="1208d-152">Creare un file con nome C:\cred.xml e copiarvi i dati della chiave RSA.</span><span class="sxs-lookup"><span data-stu-id="1208d-152">Create a file named C:\cred.xml and copy the RSA key data into it.</span></span> <span data-ttu-id="1208d-153">Un esempio è disponibile nei file di esempio alla fine dell'articolo.</span><span class="sxs-lookup"><span data-stu-id="1208d-153">You can find an example in the sample files at the end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy the contents of private key here</PrivateKey>
     <PublicKey>Copy the contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. <span data-ttu-id="1208d-154">Aprire un prompt dei comandi e immettere il comando seguente per impostare i dati delle credenziali per l'account hpclab\hpcuser.</span><span class="sxs-lookup"><span data-stu-id="1208d-154">Open a Command Prompt and enter the following command to set the credentials data for the hpclab\hpcuser account.</span></span> <span data-ttu-id="1208d-155">Usare il parametro **extendeddata** per passare il nome del file C:\cred.xml creato per i dati della chiave.</span><span class="sxs-lookup"><span data-stu-id="1208d-155">You use the **extendeddata** parameter to pass the name of the C:\cred.xml file you created for the key data.</span></span>
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="1208d-156">Questo comando viene completato correttamente senza output.</span><span class="sxs-lookup"><span data-stu-id="1208d-156">This command completes successfully without output.</span></span> <span data-ttu-id="1208d-157">Dopo avere configurato le credenziali per gli account utente necessari per l'esecuzione dei progetti, archiviare il file cred.xml in un percorso sicuro oppure eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="1208d-157">After setting the credentials for the user accounts you need to run jobs, store the cred.xml file in a secure location, or delete it.</span></span>
6. <span data-ttu-id="1208d-158">Se la coppia di chiavi RSA è stata generata in uno dei nodi Linux, ricordare di eliminare le chiavi dopo averle usate.</span><span class="sxs-lookup"><span data-stu-id="1208d-158">If you generated the RSA key pair on one of your Linux nodes, remember to delete the keys after you finish using them.</span></span> <span data-ttu-id="1208d-159">HPC Pack non configura il trust reciproco se rileva un file id_rsa o id_rsa.pub esistente.</span><span class="sxs-lookup"><span data-stu-id="1208d-159">HPC Pack does not set up mutual trust if it finds an existing id_rsa file or id_rsa.pub file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1208d-160">Non è consigliabile eseguire un processo di Linux come amministratore del cluster in un cluster condiviso, perché un processo inviato da un amministratore viene eseguito con l'account radice nei nodi Linux.</span><span class="sxs-lookup"><span data-stu-id="1208d-160">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under the root account on the Linux nodes.</span></span> <span data-ttu-id="1208d-161">Un processo inviato da un utente non amministratore viene eseguito con un account utente Linux locale, con lo stesso nome dell'utente del processo.</span><span class="sxs-lookup"><span data-stu-id="1208d-161">A job submitted by a non-administrator user runs under a local Linux user account with the same name as the job user.</span></span> <span data-ttu-id="1208d-162">In questo caso, HPC Pack configura la relazione di trust reciproco per questo utente Linux in tutti i nodi allocati per il processo.</span><span class="sxs-lookup"><span data-stu-id="1208d-162">In this case, HPC Pack sets up mutual trust for this Linux user across all the nodes allocated to the job.</span></span> <span data-ttu-id="1208d-163">È possibile configurare manualmente l'utente Linux nei nodi Linux prima di eseguire il processo. In alternativa, HPC Pack crea automaticamente l'utente quando viene inviato il processo.</span><span class="sxs-lookup"><span data-stu-id="1208d-163">You can set up the Linux user manually on the Linux nodes before running the job, or HPC Pack creates the user automatically when the job is submitted.</span></span> <span data-ttu-id="1208d-164">Se HPC Pack crea l'utente, HPC Pack lo eliminerà dopo il completamento del processo.</span><span class="sxs-lookup"><span data-stu-id="1208d-164">If HPC Pack creates the user, HPC Pack deletes it after the job completes.</span></span> <span data-ttu-id="1208d-165">Per ridurre le minacce alla sicurezza, le chiavi vengono rimosse dopo il completamento del processo sui nodi.</span><span class="sxs-lookup"><span data-stu-id="1208d-165">To reduce security threat, the keys are removed after the job completes on the nodes.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="1208d-166">Configurare una condivisione di file per i nodi Linux</span><span class="sxs-lookup"><span data-stu-id="1208d-166">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="1208d-167">Configurare ora una condivisione di file SMB e montare la cartella condivisa in tutti i nodi Linux per consentire ai nodi Linux di accedere ai file NAMD con un percorso comune.</span><span class="sxs-lookup"><span data-stu-id="1208d-167">Now set up an SMB file share, and mount the shared folder on all Linux nodes to allow the Linux nodes to access NAMD files with a common path.</span></span> <span data-ttu-id="1208d-168">Di seguito vengono descritti i passaggi per montare una cartella condivisa nel nodo head.</span><span class="sxs-lookup"><span data-stu-id="1208d-168">Following are steps to mount a shared folder on the head node.</span></span> <span data-ttu-id="1208d-169">Per le distribuzioni che attualmente non supportano il servizio File di Azure, come ad esempio CentOS 6.6, si consiglia di eseguire una condivisione.</span><span class="sxs-lookup"><span data-stu-id="1208d-169">A share is recommended for distributions such as CentOS 6.6 that currently don’t support the Azure File service.</span></span> <span data-ttu-id="1208d-170">Se i nodi Linux supportano la condivisione di file di Azure, vedere [Come usare Archiviazione file di Azure con Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1208d-170">If your Linux nodes support an Azure File share, see [How to use Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="1208d-171">Per altre opzioni di condivisione dei file con HPC Pack, vedere [Introduzione ai nodi di calcolo Linux in un cluster HPC Pack in Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="1208d-171">For additional file sharing options with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="1208d-172">Creare una cartella sul nodo head e condividerla con tutti gli utenti, configurando privilegi di lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="1208d-172">Create a folder on the head node, and share it to Everyone by setting Read/Write privileges.</span></span> <span data-ttu-id="1208d-173">In questo esempio \\\\CentOS66HN\Namd è il nome della cartella, dove CentOS66HN è il nome host del nodo head.</span><span class="sxs-lookup"><span data-stu-id="1208d-173">In this example, \\\\CentOS66HN\Namd is the name of the folder, where CentOS66HN is the host name of the head node.</span></span>
2. <span data-ttu-id="1208d-174">Creare una sottocartella denominata namd2 nella cartella condivisa.</span><span class="sxs-lookup"><span data-stu-id="1208d-174">Create a subfolder named namd2 in the shared folder.</span></span> <span data-ttu-id="1208d-175">All'interno di namd2, creare un'altra sottocartella namdsample.</span><span class="sxs-lookup"><span data-stu-id="1208d-175">In namd2, create another subfolder named namdsample.</span></span>
3. <span data-ttu-id="1208d-176">Estrarre i file NAMD nella cartella usando una versione Windows di **tar** o un'altra utilità Windows che gestisce gli archivi con estensione tar.</span><span class="sxs-lookup"><span data-stu-id="1208d-176">Extract the NAMD files in the folder by using a Windows version of **tar** or another Windows utility that operates on .tar archives.</span></span> 
   
   * <span data-ttu-id="1208d-177">Estrarre l'archivio .tar NAMD in \\\\CentOS66HN\Namd\namd2.</span><span class="sxs-lookup"><span data-stu-id="1208d-177">Extract the NAMD tar archive to \\\\CentOS66HN\Namd\namd2.</span></span>
   * <span data-ttu-id="1208d-178">Estrarre i file per le esercitazioni in \\\\CentOS66HN\Namd\namd2\namdsample.</span><span class="sxs-lookup"><span data-stu-id="1208d-178">Extract the tutorial files under \\\\CentOS66HN\Namd\namd2\namdsample.</span></span>
4. <span data-ttu-id="1208d-179">Aprire una finestra di Windows PowerShell ed eseguire i comandi seguenti per montare la cartella condivisa nei nodi Linux.</span><span class="sxs-lookup"><span data-stu-id="1208d-179">Open a Windows PowerShell window and run the following commands to mount the shared folder on the Linux nodes.</span></span>
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="1208d-180">Il primo comando crea una cartella denominata /namd2 su tutti i nodi del gruppo LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="1208d-180">The first command creates a folder named /namd2 on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="1208d-181">Il secondo comando monta la cartella condivisa //CentOS66HN/Namd/namd2 nella cartella con i bit dir_mode e file_mode impostati su 777.</span><span class="sxs-lookup"><span data-stu-id="1208d-181">The second command mounts the shared folder //CentOS66HN/Namd/namd2 onto the folder with dir_mode and file_mode bits set to 777.</span></span> <span data-ttu-id="1208d-182">I valori di *username* e *password* nel comando devono corrispondere alle credenziali di un utente nel nodo head.</span><span class="sxs-lookup"><span data-stu-id="1208d-182">The *username* and *password* in the command should be the credentials of a user on the head node.</span></span>

> [!NOTE]
> <span data-ttu-id="1208d-183">Il simbolo "\\`" nel secondo comando è un simbolo di escape per PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1208d-183">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="1208d-184">"\\`" significa "," (virgola) e fa parte del comando.</span><span class="sxs-lookup"><span data-stu-id="1208d-184">“\\`,” means the “,” (comma character) is a part of the command.</span></span>
> 
> 

## <a name="create-a-bash-script-to-run-a-namd-job"></a><span data-ttu-id="1208d-185">Creare uno script Bash per eseguire un processo NAMD</span><span class="sxs-lookup"><span data-stu-id="1208d-185">Create a Bash script to run a NAMD job</span></span>
<span data-ttu-id="1208d-186">Il processo NAMD richiede un file *nodelist* per consentire a **charmrun** di determinare il numero di nodi da usare quando vengono avviati i processi NAMD.</span><span class="sxs-lookup"><span data-stu-id="1208d-186">Your NAMD job needs a *nodelist* file for **charmrun** to determine the number of nodes to use when starting NAMD processes.</span></span> <span data-ttu-id="1208d-187">Viene usato uno script Bash che genera il file nodelist ed esegue **charmrun** con il file nodelist generato.</span><span class="sxs-lookup"><span data-stu-id="1208d-187">You use a Bash script that generates the nodelist file and runs **charmrun** with this nodelist file.</span></span> <span data-ttu-id="1208d-188">È quindi possibile inviare un processo NAMD in HPC Cluster Manager per chiamare questo script.</span><span class="sxs-lookup"><span data-stu-id="1208d-188">You can then submit a NAMD job in HPC Cluster Manager that calls this script.</span></span>

<span data-ttu-id="1208d-189">Usando l'editor di testo desiderato, creare uno script Bash nella cartella /namd2 contenente i file di programma NAMD e denominarlo hpccharmrun.sh. Per un rapido modello di prova, copiare lo script di esempio hpccharmrun.sh fornito alla fine di questo articolo e passare a [Inviare un processo NAMD](#submit-a-namd-job).</span><span class="sxs-lookup"><span data-stu-id="1208d-189">Using a text editor of your choice, create a Bash script in the /namd2 folder containing the NAMD program files and name it hpccharmrun.sh. For a quick proof of concept, copy the example hpccharmrun.sh script provided at the end of this article and go to [Submit a NAMD job](#submit-a-namd-job).</span></span>

> [!TIP]
> <span data-ttu-id="1208d-190">Salvare lo script come file di testo con terminazioni riga Linux (solo LF, non CR LF),</span><span class="sxs-lookup"><span data-stu-id="1208d-190">Save your script as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="1208d-191">in modo da assicurarne l'esecuzione corretta nei nodi Linux.</span><span class="sxs-lookup"><span data-stu-id="1208d-191">This ensures that it runs properly on the Linux nodes.</span></span>
> 
> 

<span data-ttu-id="1208d-192">Di seguito sono descritte nel dettaglio le operazioni eseguite dallo script Bash.</span><span class="sxs-lookup"><span data-stu-id="1208d-192">Following are details about what this bash script does.</span></span> 

1. <span data-ttu-id="1208d-193">Definire alcune variabili.</span><span class="sxs-lookup"><span data-stu-id="1208d-193">Define some variables.</span></span>
   
   ```bash
   #!/bin/bash
   
   # The path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. <span data-ttu-id="1208d-194">Ottenere le informazioni sul nodo dalle variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="1208d-194">Get node information from the environment variables.</span></span> <span data-ttu-id="1208d-195">$NODESCORES archivia un elenco di parole suddivise da $CCP_NODES_CORES.</span><span class="sxs-lookup"><span data-stu-id="1208d-195">$NODESCORES stores a list of split words from $CCP_NODES_CORES.</span></span> <span data-ttu-id="1208d-196">$COUNT corrisponde alle dimensioni di $NODESCORES.</span><span class="sxs-lookup"><span data-stu-id="1208d-196">$COUNT is the size of $NODESCORES.</span></span>
   
   ```
   # Get node information from the environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   <span data-ttu-id="1208d-197">Il formato della variabile $CCP_NODES_CORES è il seguente:</span><span class="sxs-lookup"><span data-stu-id="1208d-197">The format for the $CCP_NODES_CORES variable is as follows:</span></span>
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   <span data-ttu-id="1208d-198">Questa variabile consente di elencare il numero totale di nodi, i nomi dei nodi e il numero di core in ogni nodo allocati al processo.</span><span class="sxs-lookup"><span data-stu-id="1208d-198">This variable lists the total number of nodes, node names, and number of cores on each node that are allocated to the job.</span></span> <span data-ttu-id="1208d-199">Ad esempio, se per l'esecuzione del processo sono necessari 10 core, il valore di $CCP_NODES_CORES è simile a:</span><span class="sxs-lookup"><span data-stu-id="1208d-199">For example, if the job needs 10 cores to run, the value of $CCP_NODES_CORES is similar to:</span></span>
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. <span data-ttu-id="1208d-200">Se la variabile $CCP_NODES_CORES non è configurata, avviare direttamente **charmrun**.</span><span class="sxs-lookup"><span data-stu-id="1208d-200">If the $CCP_NODES_CORES variable is not set, start **charmrun** directly.</span></span> <span data-ttu-id="1208d-201">È consigliabile seguire questa procedura solo quando si esegue lo script direttamente nei nodi Linux.</span><span class="sxs-lookup"><span data-stu-id="1208d-201">(This should only occur when you run this script directly on your Linux nodes.)</span></span>
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. <span data-ttu-id="1208d-202">In alternativa, creare un file nodelist per **charmrun**.</span><span class="sxs-lookup"><span data-stu-id="1208d-202">Or create a nodelist file for **charmrun**.</span></span>
   
   ```
   else
     # Create the nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write the head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into the nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. <span data-ttu-id="1208d-203">Eseguire **charmrun** con il file nodelist, ottenere il relativo stato restituito e quindi rimuovere il file nodelist al termine delle operazioni.</span><span class="sxs-lookup"><span data-stu-id="1208d-203">Run **charmrun** with the nodelist file, get its return status, and remove the nodelist file at the end.</span></span>
   
   <span data-ttu-id="1208d-204">${CCP_NUMCPUS} è un'altra variabile di ambiente configurata dal nodo head HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="1208d-204">${CCP_NUMCPUS} is another environment variable set by the HPC Pack head node.</span></span> <span data-ttu-id="1208d-205">Archivia il numero totale di core allocati per questo processo.</span><span class="sxs-lookup"><span data-stu-id="1208d-205">It stores the number of total cores allocated to this job.</span></span> <span data-ttu-id="1208d-206">Viene usata per specificare il numero di processi per charmrun.</span><span class="sxs-lookup"><span data-stu-id="1208d-206">We use it to specify the number of processes for charmrun.</span></span>
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. <span data-ttu-id="1208d-207">Uscire con lo stato restituito di **charmrun** .</span><span class="sxs-lookup"><span data-stu-id="1208d-207">Exit with the **charmrun** return status.</span></span>
   
   ```
   exit ${RTNSTS}
   ```

<span data-ttu-id="1208d-208">Le informazioni seguenti sono disponibili nel file nodelist, che viene generato dallo script:</span><span class="sxs-lookup"><span data-stu-id="1208d-208">Following is the information in the nodelist file, which the script generates:</span></span>

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

<span data-ttu-id="1208d-209">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1208d-209">For example:</span></span>

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a><span data-ttu-id="1208d-210">Inviare un processo NAMD</span><span class="sxs-lookup"><span data-stu-id="1208d-210">Submit a NAMD job</span></span>
<span data-ttu-id="1208d-211">È ora possibile inviare un processo NAMD in HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="1208d-211">Now you are ready to submit a NAMD job in HPC Cluster Manager.</span></span>

1. <span data-ttu-id="1208d-212">Connettersi al nodo head del cluster e avviare HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="1208d-212">Connect to your cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="1208d-213">In **Resource Management** (Gestione risorsa) assicurarsi che lo stato dei nodi di calcolo Linux sia **Online**.</span><span class="sxs-lookup"><span data-stu-id="1208d-213">In **Resource Management**, ensure that the Linux compute nodes are in the **Online** state.</span></span> <span data-ttu-id="1208d-214">Se lo stato è diverso, selezionarli e fare clic su **Portare Online**.</span><span class="sxs-lookup"><span data-stu-id="1208d-214">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="1208d-215">In **Job Management** (Gestione processi) fare clic su **New Job** (Nuovo processo).</span><span class="sxs-lookup"><span data-stu-id="1208d-215">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="1208d-216">Immettere un nome per il processo, ad esempio *hpccharmrun*.</span><span class="sxs-lookup"><span data-stu-id="1208d-216">Enter a name for job such as *hpccharmrun*.</span></span>
   
   ![Nuovo processo HPC][namd_job]
5. <span data-ttu-id="1208d-218">Nella pagina **Job Details** (Dettagli processo) in **Job Resources** (Risorse processo) scegliere **Node** (Nodo) come tipo di risorsa, quindi impostare il valore **Minimum** (Minimo) su 3</span><span class="sxs-lookup"><span data-stu-id="1208d-218">On the **Job Details** page, under **Job Resources**, select the type of resource as **Node** and set the **Minimum** to 3.</span></span> <span data-ttu-id="1208d-219">per eseguire il processo su tre nodi di Linux con quattro core ciascuno.</span><span class="sxs-lookup"><span data-stu-id="1208d-219">, we run the job on three Linux nodes and each node has four cores.</span></span>
   
   ![Risorse del processo][job_resources]
6. <span data-ttu-id="1208d-221">Fare clic su **Edit Tasks** (Modifica attività) nel riquadro di spostamento sinistro e quindi fare clic su **Add** (Aggiungi) per aggiungere un'attività al processo.</span><span class="sxs-lookup"><span data-stu-id="1208d-221">Click **Edit Tasks** in the left navigation, and then click **Add** to add a task to the job.</span></span>    
7. <span data-ttu-id="1208d-222">Nella pagina **Task Details and I/O Redirection** (Dettagli attività e reindirizzamento I/O) impostare i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="1208d-222">On the **Task Details and I/O Redirection** page, set the following values:</span></span>
   
   * <span data-ttu-id="1208d-223">**Riga di comando**-
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span><span class="sxs-lookup"><span data-stu-id="1208d-223">**Command line** -
`/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span></span>
     
     > [!TIP]
     > <span data-ttu-id="1208d-224">La riga di comando precedente è costituita da un comando singolo senza interruzioni di riga.</span><span class="sxs-lookup"><span data-stu-id="1208d-224">The preceding command line is a single command without line breaks.</span></span> <span data-ttu-id="1208d-225">Nella **riga di comando** il testo appare suddiviso in più righe.</span><span class="sxs-lookup"><span data-stu-id="1208d-225">It wraps to appear on several lines under **Command line**.</span></span>
     > 
     > 
   * <span data-ttu-id="1208d-226">**Working directory** - /namd2</span><span class="sxs-lookup"><span data-stu-id="1208d-226">**Working directory** - /namd2</span></span>
   * <span data-ttu-id="1208d-227">**Minimum** - 3</span><span class="sxs-lookup"><span data-stu-id="1208d-227">**Minimum** - 3</span></span>
     
     ![Dettagli dell'attività][task_details]
     
     > [!NOTE]
     > <span data-ttu-id="1208d-229">È necessario configurare qui la directory di lavoro, perché **charmrun** prova a passare alla stessa directory di lavoro in ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="1208d-229">You set the working directory here because **charmrun** tries to navigate to the same working directory on each node.</span></span> <span data-ttu-id="1208d-230">Se la directory di lavoro non è configurata, HPC Pack avvia il comando in una cartella con nome casuale creata in uno dei nodi Linux.</span><span class="sxs-lookup"><span data-stu-id="1208d-230">If the working directory isn't set, HPC Pack starts the command in a randomly named folder created on one of the Linux nodes.</span></span> <span data-ttu-id="1208d-231">Ciò provoca l'errore seguente negli altri nodi: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` Per evitare questo problema, specificare un percorso di cartella accessibile a tutti i nodi come directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="1208d-231">This causes the following error on the other nodes: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` To avoid this problem, specify a folder path that can be accessed by all nodes as the working directory.</span></span>
     > 
     > 
8. <span data-ttu-id="1208d-232">Fare clic su **OK** e quindi su **Invia** per eseguire il processo.</span><span class="sxs-lookup"><span data-stu-id="1208d-232">Click **OK** and then click **Submit** to run this job.</span></span>
   
   <span data-ttu-id="1208d-233">Per impostazione predefinita, HPC Pack invia il processo usando l'account utente attualmente connesso.</span><span class="sxs-lookup"><span data-stu-id="1208d-233">By default, HPC Pack submits the job as your current logged-on user account.</span></span> <span data-ttu-id="1208d-234">È possibile che una finestra di dialogo richieda l'immissione del nome utente e della password dopo la selezione di **Submit**.</span><span class="sxs-lookup"><span data-stu-id="1208d-234">A dialog box might prompt you to enter the user name and password after you click **Submit**.</span></span>
   
   ![Credenziali del processo][creds]
   
   <span data-ttu-id="1208d-236">In alcune condizioni, HPC Pack ricorda le informazioni utente inserite in precedenza e non visualizza questa finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1208d-236">Under some conditions, HPC Pack remembers the user information you input before and doesn't show this dialog box.</span></span> <span data-ttu-id="1208d-237">Per tornare a visualizzarla in HPC Pack, immettere il comando seguente nel prompt dei comandi e quindi inviare il processo.</span><span class="sxs-lookup"><span data-stu-id="1208d-237">To make HPC Pack show it again, enter the following command at a Command Prompt and then submit the job.</span></span>
   
   ```command
   hpccred delcreds
   ```
9. <span data-ttu-id="1208d-238">Il completamento del processo richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="1208d-238">The job takes several minutes to finish.</span></span>
10. <span data-ttu-id="1208d-239">Il log del processo è disponibile in \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log e i file di output sono disponibili in \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\..</span><span class="sxs-lookup"><span data-stu-id="1208d-239">Find the job log at \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log and the output files in \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span></span>
11. <span data-ttu-id="1208d-240">Facoltativamente, avviare VMD per visualizzare i risultati del processo.</span><span class="sxs-lookup"><span data-stu-id="1208d-240">Optionally, start VMD to view your job results.</span></span> <span data-ttu-id="1208d-241">I passaggi per la visualizzazione dei file di output NAMD (in questo caso, una molecola proteica di ubiquitina in una sfera d'acqua) non rientrano nell'ambito di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="1208d-241">The steps for visualizing the NAMD output files (in this case, a ubiquitin protein molecule in a water sphere) are beyond the scope of this article.</span></span> <span data-ttu-id="1208d-242">Per informazioni dettagliate, vedere l' [esercitazione relativa a NAMD](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) .</span><span class="sxs-lookup"><span data-stu-id="1208d-242">See [NAMD Tutorial](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) for details.</span></span>
    
    ![Risultati del processo][vmd_view]

## <a name="sample-files"></a><span data-ttu-id="1208d-244">File di esempio</span><span class="sxs-lookup"><span data-stu-id="1208d-244">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="1208d-245">File di configurazione XML di esempio per la distribuzione di cluster tramite script PowerShell</span><span class="sxs-lookup"><span data-stu-id="1208d-245">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
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

### <a name="sample-credxml-file"></a><span data-ttu-id="1208d-246">File cred.xml di esempio</span><span class="sxs-lookup"><span data-stu-id="1208d-246">Sample cred.xml file</span></span>
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

### <a name="sample-hpccharmrunsh-script"></a><span data-ttu-id="1208d-247">Script hpccharmrun.sh di esempio</span><span class="sxs-lookup"><span data-stu-id="1208d-247">Sample hpccharmrun.sh script</span></span>
```
#!/bin/bash

# The path of this script
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
    # If CCP_NODES_CORES is not found or is empty, just run the charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create the nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write the head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into the nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run the charmrun with nodelist arg
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
