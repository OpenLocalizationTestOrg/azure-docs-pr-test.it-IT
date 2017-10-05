---
title: Risorse per batch e HPC nel cloud di Azure | Microsoft Docs
description: Questo articolo fornisce un elenco delle risorse tecniche che permettono di eseguire carichi di lavoro paralleli, batch e HPC (High Performance Computing) su larga scala in Azure.
services: batch, cloud-services, virtual-machines
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 6f8be911-c841-41ae-88d3-3bcfc029eb7f
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 03/17/2017
ms.author: danlep
ms.openlocfilehash: 18be9f503b57117a7e8f5f0a4e9c93614cc7755b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a><span data-ttu-id="b9923-103">Big Compute in Azure: risorse tecniche per Batch e High Performance Computing</span><span class="sxs-lookup"><span data-stu-id="b9923-103">Big Compute in Azure: Technical resources for batch and high-performance computing</span></span>
<span data-ttu-id="b9923-104">Si tratta di una guida alle risorse tecniche che permettono di eseguire carichi di lavoro paralleli, batch e HPC (High Performance Computing) su larga scala in Azure.</span><span class="sxs-lookup"><span data-stu-id="b9923-104">This is a guide to technical resources to help you run your large-scale parallel, batch, and high-performance computing (HPC) workloads in Azure.</span></span> <span data-ttu-id="b9923-105">La vasta gamma di servizi Azure consente di estendere il batch esistente o i carichi di lavoro HPC nel cloud Azure o creare nuove soluzioni Big Compute.</span><span class="sxs-lookup"><span data-stu-id="b9923-105">Extend your existing batch or HPC workloads to the Azure cloud, or build new Big Compute solutions using a range of Azure services.</span></span>

## <a name="solutions-options"></a><span data-ttu-id="b9923-106">Opzioni di soluzioni</span><span class="sxs-lookup"><span data-stu-id="b9923-106">Solutions options</span></span>
<span data-ttu-id="b9923-107">Informazioni sulle opzioni Big Compute in Azure e sulla scelta dell'approccio più adatto a soddisfare le esigenze del carico di lavoro e dell'azienda.</span><span class="sxs-lookup"><span data-stu-id="b9923-107">Learn about Big Compute options in Azure, and choose the right approach for your workload and business need.</span></span>

* [<span data-ttu-id="b9923-108">Batch e soluzioni HPC</span><span class="sxs-lookup"><span data-stu-id="b9923-108">Batch and HPC solutions</span></span>](batch-hpc-solutions.md)
* [<span data-ttu-id="b9923-109">Video: Big Compute nel cloud con Azure e HPC</span><span class="sxs-lookup"><span data-stu-id="b9923-109">Video: Big Compute in the cloud with Azure and HPC</span></span>](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a><span data-ttu-id="b9923-110">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="b9923-110">Azure Batch</span></span>
<span data-ttu-id="b9923-111">[Batch](https://azure.microsoft.com/services/batch/) è un servizio piattaforma che semplifica l'abilitazione cloud delle applicazioni Linux e Windows e l'esecuzione dei processi senza che sia necessario impostare e gestire un cluster e un'utilità di pianificazione dei processi.</span><span class="sxs-lookup"><span data-stu-id="b9923-111">[Batch](https://azure.microsoft.com/services/batch/) is a platform service that makes it easy to cloud-enable your Linux and Windows applications and run jobs without setting up and managing a cluster and job scheduler.</span></span> <span data-ttu-id="b9923-112">Usare l'SDK per integrare le applicazioni client con Azure Batch in vari linguaggi, organizzare i dati in Azure e creare le pipeline di esecuzione del processo.</span><span class="sxs-lookup"><span data-stu-id="b9923-112">Use the SDK to integrate client applications with Azure Batch through various languages, stage data to Azure, and build job execution pipelines.</span></span>

* [<span data-ttu-id="b9923-113">Documentazione</span><span class="sxs-lookup"><span data-stu-id="b9923-113">Documentation</span></span>](https://azure.microsoft.com/documentation/services/batch/)
* <span data-ttu-id="b9923-114">Informazioni di riferimento su [.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/) e API [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx)</span><span class="sxs-lookup"><span data-stu-id="b9923-114">[.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), and [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API reference</span></span>
* <span data-ttu-id="b9923-115">[libreria Batch management .NET](https://msdn.microsoft.com/library/mt463120.aspx) </span><span class="sxs-lookup"><span data-stu-id="b9923-115">[Batch management .NET library](https://msdn.microsoft.com/library/mt463120.aspx) reference</span></span>
* <span data-ttu-id="b9923-116">[Esercitazione: Introduzione alla libreria di Azure Batch per .NET](batch-dotnet-get-started.md) e al [client Python di Batch](batch-python-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="b9923-116">Tutorials: Get started with [Azure Batch library for .NET](batch-dotnet-get-started.md) and [Batch Python client](batch-python-tutorial.md)</span></span>
* [<span data-ttu-id="b9923-117">Forum di Batch</span><span class="sxs-lookup"><span data-stu-id="b9923-117">Batch forum</span></span>](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [<span data-ttu-id="b9923-118">Video su Batch</span><span class="sxs-lookup"><span data-stu-id="b9923-118">Batch videos</span></span>](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a><span data-ttu-id="b9923-119">Soluzioni cluster di HPC</span><span class="sxs-lookup"><span data-stu-id="b9923-119">HPC cluster solutions</span></span>
<span data-ttu-id="b9923-120">Distribuire o estendere il cluster HPC Windows o Linux esistente in Azure per eseguire carichi di lavoro a elevato utilizzo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="b9923-120">Deploy or extend your existing Windows or Linux HPC cluster to Azure to run your compute intensive workloads.</span></span>  

### <a name="microsoft-hpc-pack"></a><span data-ttu-id="b9923-121">Microsoft HPC Pack</span><span class="sxs-lookup"><span data-stu-id="b9923-121">Microsoft HPC Pack</span></span>
<span data-ttu-id="b9923-122">HPC Pack è la soluzione HPC gratuita di Microsoft basata sulle tecnologie di Microsoft Azure e Windows Server, in grado di eseguire carichi di lavoro sia di Windows che di Linux HPC.</span><span class="sxs-lookup"><span data-stu-id="b9923-122">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies, capable of running Windows and Linux HPC workloads.</span></span>  

* [<span data-ttu-id="b9923-123">Scaricare HPC Pack 2016</span><span class="sxs-lookup"><span data-stu-id="b9923-123">Download HPC Pack 2016</span></span>](https://www.microsoft.com/download/details.aspx?id=54507)
* [<span data-ttu-id="b9923-124">Scaricare HPC Pack 2012 R2 Update 3</span><span class="sxs-lookup"><span data-stu-id="b9923-124">Download HPC Pack 2012 R2 Update 3</span></span>](https://www.microsoft.com/download/details.aspx?id=49922)
* [<span data-ttu-id="b9923-125">Documentazione</span><span class="sxs-lookup"><span data-stu-id="b9923-125">Documentation</span></span>](https://technet.microsoft.com/library/jj899572.aspx)
* <span data-ttu-id="b9923-126">Opzioni per il cluster HPC Pack in Azure: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) e [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="b9923-126">HPC Pack cluster options in Azure: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span> 
* [<span data-ttu-id="b9923-127">Potenziare le istanze del ruolo di lavoro di Azure con HPC Pack</span><span class="sxs-lookup"><span data-stu-id="b9923-127">Burst to Azure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="b9923-128">Potenziare Azure Batch con HPC Pack</span><span class="sxs-lookup"><span data-stu-id="b9923-128">Burst to Azure  Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)
* [<span data-ttu-id="b9923-129">Forum di Windows HPC</span><span class="sxs-lookup"><span data-stu-id="b9923-129">Windows HPC forums</span></span>](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a><span data-ttu-id="b9923-130">Soluzioni cluster Linux e OSS</span><span class="sxs-lookup"><span data-stu-id="b9923-130">Linux and OSS cluster solutions</span></span>
<span data-ttu-id="b9923-131">Usare questi modelli di Azure per distribuire cluster HPC Linux.</span><span class="sxs-lookup"><span data-stu-id="b9923-131">Use these Azure templates to deploy Linux HPC clusters.</span></span>

* <span data-ttu-id="b9923-132">[Avviare un cluster SLURM](https://azure.microsoft.com/documentation/templates/slurm/) e un [post di blog](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="b9923-132">[Spin up a SLURM cluster](https://azure.microsoft.com/documentation/templates/slurm/) and [blog post](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span></span>
* [<span data-ttu-id="b9923-133">Avviare un cluster Torque</span><span class="sxs-lookup"><span data-stu-id="b9923-133">Spin up a Torque cluster</span></span>](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [<span data-ttu-id="b9923-134">Modelli di griglia di calcolo con PBS Professional</span><span class="sxs-lookup"><span data-stu-id="b9923-134">Compute grid templates with PBS Professional</span></span>](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a><span data-ttu-id="b9923-135">Archiviazione HPC</span><span class="sxs-lookup"><span data-stu-id="b9923-135">HPC storage</span></span>
* [<span data-ttu-id="b9923-136">File system paralleli per l'archiviazione HPC in Azure</span><span class="sxs-lookup"><span data-stu-id="b9923-136">Parallel file systems for HPC storage on Azure</span></span>](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [<span data-ttu-id="b9923-137">Intel Cloud Edition per software Lustre - Valutazione</span><span class="sxs-lookup"><span data-stu-id="b9923-137">Intel Cloud Edition for Lustre Software - Eval</span></span>](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [<span data-ttu-id="b9923-138">Modello BeeGFS su CentOS 7.2</span><span class="sxs-lookup"><span data-stu-id="b9923-138">BeeGFS on CentOS 7.2 template</span></span>](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a><span data-ttu-id="b9923-139">Microsoft MPI</span><span class="sxs-lookup"><span data-stu-id="b9923-139">Microsoft MPI</span></span>
<span data-ttu-id="b9923-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) è un'implementazione Microsoft dello standard Message Passing Interface per lo sviluppo e l'esecuzione di applicazioni parallele sulla piattaforma Windows.</span><span class="sxs-lookup"><span data-stu-id="b9923-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) is a Microsoft implementation of the Message Passing Interface standard for developing and running parallel applications on the Windows platform.</span></span>

* [<span data-ttu-id="b9923-141">Scaricare MS-MPI</span><span class="sxs-lookup"><span data-stu-id="b9923-141">Download MS-MPI</span></span>](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [<span data-ttu-id="b9923-142">Informazioni di riferimento su MS-MPI</span><span class="sxs-lookup"><span data-stu-id="b9923-142">MS-MPI reference</span></span>](https://msdn.microsoft.com/library/dn473458.aspx)
* [<span data-ttu-id="b9923-143">Forum di MPI</span><span class="sxs-lookup"><span data-stu-id="b9923-143">MPI forum</span></span>](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a><span data-ttu-id="b9923-144">Istanze a elevato uso di calcolo</span><span class="sxs-lookup"><span data-stu-id="b9923-144">Compute-intensive instances</span></span>
<span data-ttu-id="b9923-145">Azure offre [varie dimensioni di macchine virtuali](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), tra cui istanze [a elevato uso di calcolo serie H](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) che consentono di connettersi a una rete RDMA di back-end per eseguire carichi di lavoro HPC Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="b9923-145">Azure offers a [range of VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), including [compute-intensive H-series](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) instances capable of connecting to a back-end RDMA network, to run your Linux and Windows HPC workloads.</span></span> 

* [<span data-ttu-id="b9923-146">Configurazione di un cluster Linux RDMA per eseguire applicazioni MPI</span><span class="sxs-lookup"><span data-stu-id="b9923-146">Set up a Linux RDMA cluster to run MPI applications</span></span>](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="b9923-147">Configurare un cluster di Windows RDMA con Microsoft HPC Pack per eseguire applicazioni MPI</span><span class="sxs-lookup"><span data-stu-id="b9923-147">Set up a Windows RDMA cluster with Microsoft HPC Pack to run MPI applications</span></span>](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

<span data-ttu-id="b9923-148">Per carichi di lavoro con elevato uso della GPU, vedere [NC e NV sizes](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/) (Dimensioni NC e NV).</span><span class="sxs-lookup"><span data-stu-id="b9923-148">For GPU-intensive workloads, check out [NC and NV sizes](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).</span></span>

## <a name="samples-and-demos"></a><span data-ttu-id="b9923-149">Esempi e demo</span><span class="sxs-lookup"><span data-stu-id="b9923-149">Samples and demos</span></span>
* [<span data-ttu-id="b9923-150">Esempi di codice di Azure Batch C# e Python</span><span class="sxs-lookup"><span data-stu-id="b9923-150">Azure Batch C# and Python code samples</span></span>](https://github.com/Azure/azure-batch-samples)
* <span data-ttu-id="b9923-151">Toolkit [Batch Shipyard](https://azure.github.io/batch-shipyard/) per semplificare la distribuzione dei carichi di lavoro Docker di tipo batch in Azure Batch</span><span class="sxs-lookup"><span data-stu-id="b9923-151">[Batch Shipyard](https://azure.github.io/batch-shipyard/) toolkit for easy deployment of batch-style Dockerized workloads to Azure Batch</span></span>
* <span data-ttu-id="b9923-152">Pacchetto [doAzureParallel](http://www.github.com/Azure/doAzureParallel) R, basato su Azure Batch</span><span class="sxs-lookup"><span data-stu-id="b9923-152">[doAzureParallel](http://www.github.com/Azure/doAzureParallel) R package, built on top of Azure Batch</span></span>
* [<span data-ttu-id="b9923-153">Versione di test di SUSE Linux Enterprise Server per HPC</span><span class="sxs-lookup"><span data-stu-id="b9923-153">Test drive SUSE Linux Enterprise Server for HPC</span></span>](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a><span data-ttu-id="b9923-154">Servizi Azure correlati</span><span class="sxs-lookup"><span data-stu-id="b9923-154">Related Azure services</span></span>
* [<span data-ttu-id="b9923-155">Data Factory</span><span class="sxs-lookup"><span data-stu-id="b9923-155">Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)
* [<span data-ttu-id="b9923-156">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="b9923-156">Machine Learning</span></span>](https://azure.microsoft.com/documentation/services/machine-learning/)
* [<span data-ttu-id="b9923-157">HDInsight</span><span class="sxs-lookup"><span data-stu-id="b9923-157">HDInsight</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="b9923-158">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="b9923-158">Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="b9923-159">Set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="b9923-159">Virtual Machine Scale Sets</span></span>](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [<span data-ttu-id="b9923-160">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="b9923-160">Cloud Services</span></span>](https://azure.microsoft.com/documentation/services/cloud-services/)
* [<span data-ttu-id="b9923-161">Servizio app</span><span class="sxs-lookup"><span data-stu-id="b9923-161">App Service</span></span>](https://azure.microsoft.com/documentation/services/app-service/)
* [<span data-ttu-id="b9923-162">Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="b9923-162">Media Services</span></span>](https://azure.microsoft.com/documentation/services/media-services/)
* [<span data-ttu-id="b9923-163">Funzioni</span><span class="sxs-lookup"><span data-stu-id="b9923-163">Functions</span></span>](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a><span data-ttu-id="b9923-164">Progetti dell'architettura</span><span class="sxs-lookup"><span data-stu-id="b9923-164">Architecture blueprints</span></span>
* <span data-ttu-id="b9923-165">[Orchestrazione di HPC e dati con Azure Batch e Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) e [articolo](../data-factory/data-factory-data-processing-using-batch.md)</span><span class="sxs-lookup"><span data-stu-id="b9923-165">[HPC and data orchestration using Azure Batch and Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) and [article](../data-factory/data-factory-data-processing-using-batch.md)</span></span>

## <a name="industry-solutions"></a><span data-ttu-id="b9923-166">Soluzioni di settore</span><span class="sxs-lookup"><span data-stu-id="b9923-166">Industry solutions</span></span>
* [<span data-ttu-id="b9923-167">Banche e mercati finanziari</span><span class="sxs-lookup"><span data-stu-id="b9923-167">Banking and capital markets</span></span>](https://finance.azure.com/)
* [<span data-ttu-id="b9923-168">Simulazioni di progettazione</span><span class="sxs-lookup"><span data-stu-id="b9923-168">Engineering simulations</span></span>](https://simulation.azure.com/) 

## <a name="customer-stories"></a><span data-ttu-id="b9923-169">Casi di successo dei clienti</span><span class="sxs-lookup"><span data-stu-id="b9923-169">Customer stories</span></span>
* [<span data-ttu-id="b9923-170">ANEO</span><span class="sxs-lookup"><span data-stu-id="b9923-170">ANEO</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [<span data-ttu-id="b9923-171">d3View</span><span class="sxs-lookup"><span data-stu-id="b9923-171">d3View</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [<span data-ttu-id="b9923-172">Ludwig Institute of Cancer Research</span><span class="sxs-lookup"><span data-stu-id="b9923-172">Ludwig Institute of Cancer Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [<span data-ttu-id="b9923-173">Microsoft Research</span><span class="sxs-lookup"><span data-stu-id="b9923-173">Microsoft Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [<span data-ttu-id="b9923-174">Milliman</span><span class="sxs-lookup"><span data-stu-id="b9923-174">Milliman</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [<span data-ttu-id="b9923-175">Mitsubishi UFJ Securities International</span><span class="sxs-lookup"><span data-stu-id="b9923-175">Mitsubishi UFJ Securities International</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [<span data-ttu-id="b9923-176">Schlumberger</span><span class="sxs-lookup"><span data-stu-id="b9923-176">Schlumberger</span></span>](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [<span data-ttu-id="b9923-177">Towers Watson</span><span class="sxs-lookup"><span data-stu-id="b9923-177">Towers Watson</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [<span data-ttu-id="b9923-178">UberCloud</span><span class="sxs-lookup"><span data-stu-id="b9923-178">UberCloud</span></span>](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a><span data-ttu-id="b9923-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b9923-179">Next steps</span></span>
* <span data-ttu-id="b9923-180">Per gli annunci più recenti, vedere il [blog del team di Microsoft HPC e Batch](http://blogs.technet.com/b/windowshpc/) e il [blog di Azure](https://azure.microsoft.com/blog/tag/hpc/).</span><span class="sxs-lookup"><span data-stu-id="b9923-180">For the latest announcements, see the [Microsoft HPC and Batch team blog](http://blogs.technet.com/b/windowshpc/) and the [Azure blog](https://azure.microsoft.com/blog/tag/hpc/).</span></span>
* <span data-ttu-id="b9923-181">Vedere anche le [novità di Batch](https://azure.microsoft.com/updates/?service=batch) o eseguire la sottoscrizione al [feed RSS](https://azure.microsoft.com/updates/feed/?service=batch).</span><span class="sxs-lookup"><span data-stu-id="b9923-181">Also see [what's new in Batch](https://azure.microsoft.com/updates/?service=batch) or subscribe to the [RSS feed](https://azure.microsoft.com/updates/feed/?service=batch).</span></span>

