---
title: aaaMove un tooAzure macchine virtuali di Windows AWS | Documenti Microsoft
description: Spostare un tooAzure istanza Amazon Web Services (AWS) EC2 Windows macchine virtuali tramite Azure PowerShell.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: cynthn
ms.openlocfilehash: f912c28d3ffe585162c3add715a1318ac3cd4643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a><span data-ttu-id="409c2-103">Spostare una macchina virtuale Windows da tooAzure Amazon Web Services (AWS) tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="409c2-103">Move a Windows VM from Amazon Web Services (AWS) tooAzure using PowerShell</span></span>

<span data-ttu-id="409c2-104">Se si siano valutando macchine virtuali di Azure per ospitare i carichi di lavoro, è possibile esportare un'istanza esistente di Amazon Web Services (AWS) EC2 macchina virtuale di Windows, quindi caricare hello tooAzure di disco rigido virtuale (VHD).</span><span class="sxs-lookup"><span data-stu-id="409c2-104">If you are evaluating Azure virtual machines for hosting your workloads, you can export an existing Amazon Web Services (AWS) EC2 Windows VM instance then upload hello virtual hard disk (VHD) tooAzure.</span></span> <span data-ttu-id="409c2-105">Una volta è hello che disco rigido virtuale viene caricato, è possibile creare una nuova macchina virtuale in Azure da hello disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="409c2-105">Once hello VHD is uploaded, you can create a new VM in Azure from hello VHD.</span></span> 

<span data-ttu-id="409c2-106">Questo argomento illustra lo spostamento di una singola macchina virtuale da AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="409c2-106">This topic covers moving a single VM from AWS tooAzure.</span></span> <span data-ttu-id="409c2-107">Se si desidera toomove macchine virtuali da AWS tooAzure su larga scala, vedere [eseguire la migrazione di macchine virtuali in tooAzure Amazon Web Services (AWS) con Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="409c2-107">If you want toomove VMs from AWS tooAzure at scale, see [Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="409c2-108">Preparare hello VM</span><span class="sxs-lookup"><span data-stu-id="409c2-108">Prepare hello VM</span></span> 
 
<span data-ttu-id="409c2-109">È possibile caricare specializzate e generalizzate tooAzure dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="409c2-109">You can upload both generalized and specialized VHDs tooAzure.</span></span> <span data-ttu-id="409c2-110">Ogni tipo è necessario preparare hello VM prima dell'esportazione da AWS.</span><span class="sxs-lookup"><span data-stu-id="409c2-110">Each type requires that you prepare hello VM before exporting from AWS.</span></span> 

- <span data-ttu-id="409c2-111">**Disco rigido virtuale generalizzato**: tutte le informazioni sull'account personale sono state rimosse dal disco rigido virtuale generalizzato usando Sysprep.</span><span class="sxs-lookup"><span data-stu-id="409c2-111">**Generalized VHD** - a generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="409c2-112">Se si prevede di hello toouse toocreate un'immagine disco rigido virtuale nuove macchine virtuali da, è necessario:</span><span class="sxs-lookup"><span data-stu-id="409c2-112">If you intend toouse hello VHD as an image toocreate new VMs from, you should:</span></span> 
 
    * <span data-ttu-id="409c2-113">[Preparare una VM Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="409c2-113">[Prepare a Windows VM](prepare-for-upload-vhd-image.md).</span></span>  
    * <span data-ttu-id="409c2-114">Generalizzare una macchina virtuale hello tramite Sysprep.</span><span class="sxs-lookup"><span data-stu-id="409c2-114">Generalize hello virtual machine using Sysprep.</span></span>  

 
- <span data-ttu-id="409c2-115">**Disco rigido virtuale specializzato** -un disco rigido virtuale specializzato gestisce gli account utente di hello, applicazioni e altri dati di stato dalla macchina virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="409c2-115">**Specialized VHD** - a specialized VHD maintains hello user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="409c2-116">Se si intende toouse hello file VHD come-è toocreate una nuova macchina virtuale, verificare hello operazioni viene completata.</span><span class="sxs-lookup"><span data-stu-id="409c2-116">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span>  
    * <span data-ttu-id="409c2-117">[Preparare un tooAzure tooupload disco rigido virtuale di Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="409c2-117">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span></span> <span data-ttu-id="409c2-118">**Non** generalizzare hello macchina virtuale con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="409c2-118">**Do not** generalize hello VM using Sysprep.</span></span> 
    * <span data-ttu-id="409c2-119">Rimuovere eventuali strumenti di virtualizzazione guest e gli agenti installati in hello VM (ad esempio strumenti di VMware).</span><span class="sxs-lookup"><span data-stu-id="409c2-119">Remove any guest virtualization tools and agents that are installed on hello VM (i.e. VMware tools).</span></span> 
    * <span data-ttu-id="409c2-120">Assicurarsi di hello macchina virtuale è configurata toopull il relativo indirizzo IP e le impostazioni DNS attraverso DHCP.</span><span class="sxs-lookup"><span data-stu-id="409c2-120">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="409c2-121">Ciò garantisce che il server hello ottenga un indirizzo IP all'interno di hello rete virtuale al momento dell'avvio.</span><span class="sxs-lookup"><span data-stu-id="409c2-121">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span>  


## <a name="export-and-download-hello-vhd"></a><span data-ttu-id="409c2-122">Esportare e scaricare hello disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="409c2-122">Export and download hello VHD</span></span> 

<span data-ttu-id="409c2-123">Esportare hello EC2 istanza tooa disco rigido virtuale in un bucket S3 Amazon.</span><span class="sxs-lookup"><span data-stu-id="409c2-123">Export hello EC2 instance tooa VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="409c2-124">Seguire i passaggi di hello descritti nell'argomento della documentazione di Amazon hello [l'esportazione di un'istanza di una macchina virtuale utilizzando VM importazione/esportazione](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) esecuzione hello e [creare-istanza--attività di esportazione](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) comando tooexport hello EC2 file di disco rigido virtuale tooa istanza.</span><span class="sxs-lookup"><span data-stu-id="409c2-124">Follow hello steps described in hello Amazon documentation topic [Exporting an Instance as a VM Using VM Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) and run hello [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) command tooexport hello EC2 instance tooa VHD file.</span></span> 

<span data-ttu-id="409c2-125">file disco rigido virtuale esportato Hello viene salvato nel bucket S3 Amazon hello specificate.</span><span class="sxs-lookup"><span data-stu-id="409c2-125">hello exported VHD file is saved in hello Amazon S3 bucket you specify.</span></span> <span data-ttu-id="409c2-126">Hello sintassi di base per l'esportazione hello disco rigido virtuale è inferiore, è sufficiente sostituire il testo segnaposto hello in <brackets> con le informazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="409c2-126">hello basic syntax for exporting hello VHD is below, just replace hello placeholder text in <brackets> with your information.</span></span>

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

<span data-ttu-id="409c2-127">Una volta hello disco rigido virtuale è stata esportata, seguire le istruzioni hello [come scaricare un oggetto da un Bucket S3?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) bucket S3 hello file hello toodownload disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="409c2-127">Once hello VHD has been exported, follow hello instructions in [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) toodownload hello VHD file from hello S3 bucket.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="409c2-128">AWS pagare una tariffa di trasferimento dati per il download di hello disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="409c2-128">AWS charges data transfer fees for downloading hello VHD.</span></span> <span data-ttu-id="409c2-129">Per altre informazioni, vedere [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/) (Prezzi di Amazon S3).</span><span class="sxs-lookup"><span data-stu-id="409c2-129">See [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/) for more information.</span></span>


## <a name="next-steps"></a><span data-ttu-id="409c2-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="409c2-130">Next steps</span></span>

<span data-ttu-id="409c2-131">È ora possibile caricare tooAzure VHD hello e creare una nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="409c2-131">Now you can upload hello VHD tooAzure and create a new VM.</span></span> 

- <span data-ttu-id="409c2-132">Se è stato eseguito Sysprep in origine troppo**generalizzare** , prima dell'esportazione, vedere [caricare un disco rigido virtuale generalizzato e usarlo toocreate un nuove macchine virtuali in Azure](upload-generalized-managed.md)</span><span class="sxs-lookup"><span data-stu-id="409c2-132">If you ran Sysprep on your source too**generalize** it before exporting, see [Upload a generalized VHD and use it toocreate a new VMs in Azure](upload-generalized-managed.md)</span></span>
- <span data-ttu-id="409c2-133">Se non è stato eseguito Sysprep prima dell'esportazione, hello disco rigido virtuale viene considerato **specializzato**, vedere [caricare un specializzato tooAzure VHD e creare una nuova macchina virtuale](create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="409c2-133">If you did not run Sysprep before exporting, hello VHD is considered **specialized**, see [Upload a specialized VHD tooAzure and create a new VM](create-vm-specialized.md)</span></span>

 
