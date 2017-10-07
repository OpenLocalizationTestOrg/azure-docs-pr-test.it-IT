---
title: aaaResources per batch e HPC nel cloud di Azure hello | Documenti Microsoft
description: Elenca le risorse tecniche toohelp si eseguono i paralleli su larga scala, batch e ad alte prestazioni (HPC) carichi di lavoro in Azure.
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
ms.openlocfilehash: ab8ba24678bd7ec090306b501d29ca63c4fb83ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a>Big Compute in Azure: risorse tecniche per Batch e High Performance Computing
Si tratta di un toohelp risorse tootechnical di Guida si esegue il paralleli su larga scala, batch e i carichi di lavoro ad alte prestazioni (HPC computing) in Azure. Estendere il batch esistenti o toohello i carichi di lavoro HPC cloud di Azure oppure creare nuove soluzioni Big Compute utilizzando un intervallo di Azure servizi.

## <a name="solutions-options"></a>Opzioni di soluzioni
Informazioni sulle opzioni di Big Compute in Azure e scegliere l'approccio corretto di hello alle esigenze del carico di lavoro e business.

* [Batch e soluzioni HPC](batch-hpc-solutions.md)
* [Video: Big Compute nel cloud hello con Azure e HPC](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a>Azure Batch
[Batch](https://azure.microsoft.com/services/batch/) è un servizio di piattaforma che consente di abilitare toocloud facilmente applicazioni Linux e Windows e i processi di esecuzione senza impostare e gestire un cluster e processi dell'utilità di pianificazione. Utilizzare le applicazioni client SDK toointegrate hello con Azure Batch tramite diverse lingue, fase dati tooAzure e la pipeline di esecuzione processo di compilazione.

* [Documentazione](https://azure.microsoft.com/documentation/services/batch/)
* Informazioni di riferimento su [.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/) e API [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx)
* [libreria Batch management .NET](https://msdn.microsoft.com/library/mt463120.aspx)
* [Esercitazione: Introduzione alla libreria di Azure Batch per .NET](batch-dotnet-get-started.md) e al [client Python di Batch](batch-python-tutorial.md)
* [Forum di Batch](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [Video su Batch](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a>Soluzioni cluster di HPC
Distribuire o estendere l'esistente Windows o Linux HPC cluster tooAzure toorun i carichi di lavoro con utilizzo intensivo di calcolo.  

### <a name="microsoft-hpc-pack"></a>Microsoft HPC Pack
HPC Pack è la soluzione HPC gratuita di Microsoft basata sulle tecnologie di Microsoft Azure e Windows Server, in grado di eseguire carichi di lavoro sia di Windows che di Linux HPC.  

* [Scaricare HPC Pack 2016](https://www.microsoft.com/download/details.aspx?id=54507)
* [Scaricare HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49922)
* [Documentazione](https://technet.microsoft.com/library/jj899572.aspx)
* Opzioni per il cluster HPC Pack in Azure: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) e [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 
* [Potenziamento tooAzure istanze di lavoro con HPC Pack](https://technet.microsoft.com/library/gg481749.aspx)
* [Potenziamento tooAzure Batch con HPC Pack](https://technet.microsoft.com/library/mt612877.aspx)
* [Forum di Windows HPC](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a>Soluzioni cluster Linux e OSS
Utilizzare questi modelli di Azure di toodeploy cluster HPC Linux.

* [Avviare un cluster SLURM](https://azure.microsoft.com/documentation/templates/slurm/) e un [post di blog](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)
* [Avviare un cluster Torque](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [Modelli di griglia di calcolo con PBS Professional](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a>Archiviazione HPC
* [File system paralleli per l'archiviazione HPC in Azure](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [Intel Cloud Edition per software Lustre - Valutazione](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [Modello BeeGFS su CentOS 7.2](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a>Microsoft MPI
[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) è un'implementazione Microsoft di hello messaggio passando interfaccia standard per lo sviluppo e l'esecuzione di applicazioni parallele nella piattaforma Windows hello.

* [Scaricare MS-MPI](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [Informazioni di riferimento su MS-MPI](https://msdn.microsoft.com/library/dn473458.aspx)
* [Forum di MPI](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a>Istanze a elevato uso di calcolo
Azure offre un [intervallo di dimensioni](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), tra cui [serie H complesse](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) istanze in grado di connessione di rete RDMA di back-end tooa, toorun i carichi di lavoro di Linux e Windows HPC. 

* [Impostare un applicazioni MPI toorun di Linux RDMA cluster](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Configurare un cluster di Windows RDMA con applicazioni MPI di Microsoft HPC Pack toorun](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

Per carichi di lavoro con elevato uso della GPU, vedere [NC e NV sizes](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/) (Dimensioni NC e NV).

## <a name="samples-and-demos"></a>Esempi e demo
* [Esempi di codice di Azure Batch C# e Python](https://github.com/Azure/azure-batch-samples)
* [Batch ambientali](https://azure.github.io/batch-shipyard/) toolkit per facilitarne la distribuzione di tipo batch Dockerized i carichi di lavoro tooAzure Batch
* Pacchetto [doAzureParallel](http://www.github.com/Azure/doAzureParallel) R, basato su Azure Batch
* [Versione di test di SUSE Linux Enterprise Server per HPC](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a>Servizi Azure correlati
* [Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)
* [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)
* [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/)
* [Macchine virtuali](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Set di scalabilità di macchine virtuali](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [Servizi cloud](https://azure.microsoft.com/documentation/services/cloud-services/)
* [Servizio app](https://azure.microsoft.com/documentation/services/app-service/)
* [Servizi multimediali](https://azure.microsoft.com/documentation/services/media-services/)
* [Funzioni](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a>Progetti dell'architettura
* [Orchestrazione di HPC e dati con Azure Batch e Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) e [articolo](../data-factory/data-factory-data-processing-using-batch.md)

## <a name="industry-solutions"></a>Soluzioni di settore
* [Banche e mercati finanziari](https://finance.azure.com/)
* [Simulazioni di progettazione](https://simulation.azure.com/) 

## <a name="customer-stories"></a>Casi di successo dei clienti
* [ANEO](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [d3View](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [Ludwig Institute of Cancer Research](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [Microsoft Research](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [Milliman](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [Mitsubishi UFJ Securities International](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [Schlumberger](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [Towers Watson](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [UberCloud](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a>Passaggi successivi
* Per gli annunci più recenti di hello, vedere hello [blog del team di Microsoft HPC e Batch](http://blogs.technet.com/b/windowshpc/) hello e [blog di Azure](https://azure.microsoft.com/blog/tag/hpc/).
* Vedere anche [novità in Batch](https://azure.microsoft.com/updates/?service=batch) o la sottoscrizione toohello [feed RSS](https://azure.microsoft.com/updates/feed/?service=batch).

