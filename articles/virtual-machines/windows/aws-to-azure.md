---
title: Spostare macchine virtuali AWS Windows in Azure | Microsoft Docs
description: Spostare un'istanza Windows di Amazon Web Services (AWS) EC2 in Macchine virtuali di Azure usando Azure PowerShell.
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
ms.openlocfilehash: 7d2b498d3f84c4fd6cccf97c6d7781f293f5b395
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-to-azure-using-powershell"></a><span data-ttu-id="41300-103">Spostare una VM Windows da Amazon Web Services (AWS) ad Azure usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="41300-103">Move a Windows VM from Amazon Web Services (AWS) to Azure using PowerShell</span></span>

<span data-ttu-id="41300-104">Se si stanno valutando le macchine virtuali di Azure per l'hosting dei carichi di lavoro, è possibile esportare un'istanza di VM Windows di Amazon Web Services (AWS) EC2 esistente e quindi caricare il disco rigido virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="41300-104">If you are evaluating Azure virtual machines for hosting your workloads, you can export an existing Amazon Web Services (AWS) EC2 Windows VM instance then upload the virtual hard disk (VHD) to Azure.</span></span> <span data-ttu-id="41300-105">Dopo il caricamento del disco rigido virtuale è possibile creare una nuova VM in Azure dal disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="41300-105">Once the VHD is uploaded, you can create a new VM in Azure from the VHD.</span></span> 

<span data-ttu-id="41300-106">Questo argomento illustra lo spostamento di una singola VM da AWS ad Azure.</span><span class="sxs-lookup"><span data-stu-id="41300-106">This topic covers moving a single VM from AWS to Azure.</span></span> <span data-ttu-id="41300-107">Per spostare VM da AWS ad Azure su larga scala, vedere [Eseguire la migrazione delle macchine virtuali in Amazon Web Services (AWS) ad Azure con Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="41300-107">If you want to move VMs from AWS to Azure at scale, see [Migrate virtual machines in Amazon Web Services (AWS) to Azure with Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span></span>

## <a name="prepare-the-vm"></a><span data-ttu-id="41300-108">Preparare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="41300-108">Prepare the VM</span></span> 
 
<span data-ttu-id="41300-109">È possibile caricare dischi rigidi virtuali generalizzati e specializzati in Azure.</span><span class="sxs-lookup"><span data-stu-id="41300-109">You can upload both generalized and specialized VHDs to Azure.</span></span> <span data-ttu-id="41300-110">Entrambi i tipi richiedono prima di tutto la preparazione della macchina virtuale prima dell'esportazione da AWS.</span><span class="sxs-lookup"><span data-stu-id="41300-110">Each type requires that you prepare the VM before exporting from AWS.</span></span> 

- <span data-ttu-id="41300-111">**Disco rigido virtuale generalizzato**: tutte le informazioni sull'account personale sono state rimosse dal disco rigido virtuale generalizzato usando Sysprep.</span><span class="sxs-lookup"><span data-stu-id="41300-111">**Generalized VHD** - a generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="41300-112">Se si vuole usare il disco rigido virtuale come immagine dalla quale creare nuove macchine virtuali, è necessario:</span><span class="sxs-lookup"><span data-stu-id="41300-112">If you intend to use the VHD as an image to create new VMs from, you should:</span></span> 
 
    * <span data-ttu-id="41300-113">[Preparare una VM Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="41300-113">[Prepare a Windows VM](prepare-for-upload-vhd-image.md).</span></span>  
    * <span data-ttu-id="41300-114">Generalizzare una macchina virtuale Windows con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="41300-114">Generalize the virtual machine using Sysprep.</span></span>  

 
- <span data-ttu-id="41300-115">**Disco rigido virtuale specializzato**: un disco rigido virtuale specializzato gestisce gli account utente, le applicazioni e altri dati di stato dalla macchina virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="41300-115">**Specialized VHD** - a specialized VHD maintains the user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="41300-116">Se si intende usare il disco rigido virtuale così come è per creare una nuova macchina virtuale, assicurare il completamento delle operazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="41300-116">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span></span>  
    * <span data-ttu-id="41300-117">[Preparare un disco rigido virtuale (VHD) di Windows per il caricamento in Azure](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="41300-117">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md).</span></span> <span data-ttu-id="41300-118">**Non** generalizzare la macchina Virtuale con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="41300-118">**Do not** generalize the VM using Sysprep.</span></span> 
    * <span data-ttu-id="41300-119">Rimuovere tutti gli strumenti di virtualizzazione guest e gli agenti installati nella macchina virtuale, ad esempio gli strumenti VMware.</span><span class="sxs-lookup"><span data-stu-id="41300-119">Remove any guest virtualization tools and agents that are installed on the VM (i.e. VMware tools).</span></span> 
    * <span data-ttu-id="41300-120">Assicurarsi che la macchina virtuale sia configurata per eseguire il pull dell'indirizzo IP e delle impostazioni DNS tramite DHCP.</span><span class="sxs-lookup"><span data-stu-id="41300-120">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="41300-121">In questo modo il server ottiene un indirizzo IP all'interno della rete virtuale all'avvio.</span><span class="sxs-lookup"><span data-stu-id="41300-121">This ensures that the server obtains an IP address within the VNet when it starts up.</span></span>  


## <a name="export-and-download-the-vhd"></a><span data-ttu-id="41300-122">Esportare e scaricare il disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="41300-122">Export and download the VHD</span></span> 

<span data-ttu-id="41300-123">Esportare l'istanza EC2 in un disco rigido virtuale in un bucket Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="41300-123">Export the EC2 instance to a VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="41300-124">Seguire la procedura illustrata nell'argomento [Exporting an Instance as a VM Using VM Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) (Esportazione di un'istanza come VM tramite l'importazione/esportazione della VM) della documentazione di Amazon ed eseguire il comando [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) per esportare l'istanza EC2 in un file di disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="41300-124">Follow the steps described in the Amazon documentation topic [Exporting an Instance as a VM Using VM Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) and run the [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) command to export the EC2 instance to a VHD file.</span></span> 

<span data-ttu-id="41300-125">Il file di disco rigido virtuale esportato viene salvato nel bucket Amazon S3 indicato.</span><span class="sxs-lookup"><span data-stu-id="41300-125">The exported VHD file is saved in the Amazon S3 bucket you specify.</span></span> <span data-ttu-id="41300-126">La sintassi di base per l'esportazione del disco rigido virtuale viene riportata di seguito. È sufficiente sostituire il testo segnaposto in <brackets> con le informazioni specifiche.</span><span class="sxs-lookup"><span data-stu-id="41300-126">The basic syntax for exporting the VHD is below, just replace the placeholder text in <brackets> with your information.</span></span>

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

<span data-ttu-id="41300-127">Dopo l'esportazione del disco rigido virtuale, seguire le istruzioni disponibili in [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) (Come scaricare un oggetto da un bucket S3) per scaricare il file disco rigido virtuale dal bucket S3.</span><span class="sxs-lookup"><span data-stu-id="41300-127">Once the VHD has been exported, follow the instructions in [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) to download the VHD file from the S3 bucket.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="41300-128">AWS applica addebiti per il trasferimento di dati per il download del disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="41300-128">AWS charges data transfer fees for downloading the VHD.</span></span> <span data-ttu-id="41300-129">Per altre informazioni, vedere [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/) (Prezzi di Amazon S3).</span><span class="sxs-lookup"><span data-stu-id="41300-129">See [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/) for more information.</span></span>


## <a name="next-steps"></a><span data-ttu-id="41300-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="41300-130">Next steps</span></span>

<span data-ttu-id="41300-131">È ora possibile caricare il disco rigido virtuale in Azure e creare una nuova VM.</span><span class="sxs-lookup"><span data-stu-id="41300-131">Now you can upload the VHD to Azure and create a new VM.</span></span> 

- <span data-ttu-id="41300-132">Se è stato eseguito Sysprep nell'origine per la **generalizzazione** prima dell'esportazione, vedere [Caricare un disco rigido virtuale generalizzato e usarlo per creare una nuova VM in Azure](upload-generalized-managed.md)</span><span class="sxs-lookup"><span data-stu-id="41300-132">If you ran Sysprep on your source to **generalize** it before exporting, see [Upload a generalized VHD and use it to create a new VMs in Azure](upload-generalized-managed.md)</span></span>
- <span data-ttu-id="41300-133">Se non è stato eseguito Sysprep prima dell'esportazione, il disco rigido virtuale viene considerato **specializzato**. Vedere [Caricare un disco rigido virtuale specializzato in Azure e creare una nuova VM](create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="41300-133">If you did not run Sysprep before exporting, the VHD is considered **specialized**, see [Upload a specialized VHD to Azure and create a new VM](create-vm-specialized.md)</span></span>

 
