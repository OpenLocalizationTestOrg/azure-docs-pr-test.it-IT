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
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a>Spostare una macchina virtuale Windows da tooAzure Amazon Web Services (AWS) tramite PowerShell

Se si siano valutando macchine virtuali di Azure per ospitare i carichi di lavoro, è possibile esportare un'istanza esistente di Amazon Web Services (AWS) EC2 macchina virtuale di Windows, quindi caricare hello tooAzure di disco rigido virtuale (VHD). Una volta è hello che disco rigido virtuale viene caricato, è possibile creare una nuova macchina virtuale in Azure da hello disco rigido virtuale. 

Questo argomento illustra lo spostamento di una singola macchina virtuale da AWS tooAzure. Se si desidera toomove macchine virtuali da AWS tooAzure su larga scala, vedere [eseguire la migrazione di macchine virtuali in tooAzure Amazon Web Services (AWS) con Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).

## <a name="prepare-hello-vm"></a>Preparare hello VM 
 
È possibile caricare specializzate e generalizzate tooAzure dischi rigidi virtuali. Ogni tipo è necessario preparare hello VM prima dell'esportazione da AWS. 

- **Disco rigido virtuale generalizzato**: tutte le informazioni sull'account personale sono state rimosse dal disco rigido virtuale generalizzato usando Sysprep. Se si prevede di hello toouse toocreate un'immagine disco rigido virtuale nuove macchine virtuali da, è necessario: 
 
    * [Preparare una VM Windows](prepare-for-upload-vhd-image.md).  
    * Generalizzare una macchina virtuale hello tramite Sysprep.  

 
- **Disco rigido virtuale specializzato** -un disco rigido virtuale specializzato gestisce gli account utente di hello, applicazioni e altri dati di stato dalla macchina virtuale originale. Se si intende toouse hello file VHD come-è toocreate una nuova macchina virtuale, verificare hello operazioni viene completata.  
    * [Preparare un tooAzure tooupload disco rigido virtuale di Windows](prepare-for-upload-vhd-image.md). **Non** generalizzare hello macchina virtuale con Sysprep. 
    * Rimuovere eventuali strumenti di virtualizzazione guest e gli agenti installati in hello VM (ad esempio strumenti di VMware). 
    * Assicurarsi di hello macchina virtuale è configurata toopull il relativo indirizzo IP e le impostazioni DNS attraverso DHCP. Ciò garantisce che il server hello ottenga un indirizzo IP all'interno di hello rete virtuale al momento dell'avvio.  


## <a name="export-and-download-hello-vhd"></a>Esportare e scaricare hello disco rigido virtuale 

Esportare hello EC2 istanza tooa disco rigido virtuale in un bucket S3 Amazon. Seguire i passaggi di hello descritti nell'argomento della documentazione di Amazon hello [l'esportazione di un'istanza di una macchina virtuale utilizzando VM importazione/esportazione](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) esecuzione hello e [creare-istanza--attività di esportazione](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) comando tooexport hello EC2 file di disco rigido virtuale tooa istanza. 

file disco rigido virtuale esportato Hello viene salvato nel bucket S3 Amazon hello specificate. Hello sintassi di base per l'esportazione hello disco rigido virtuale è inferiore, è sufficiente sostituire il testo segnaposto hello in <brackets> con le informazioni necessarie.

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

Una volta hello disco rigido virtuale è stata esportata, seguire le istruzioni hello [come scaricare un oggetto da un Bucket S3?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) bucket S3 hello file hello toodownload disco rigido virtuale. 

> [!IMPORTANT]
> AWS pagare una tariffa di trasferimento dati per il download di hello disco rigido virtuale. Per altre informazioni, vedere [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/) (Prezzi di Amazon S3).


## <a name="next-steps"></a>Passaggi successivi

È ora possibile caricare tooAzure VHD hello e creare una nuova macchina virtuale. 

- Se è stato eseguito Sysprep in origine troppo**generalizzare** , prima dell'esportazione, vedere [caricare un disco rigido virtuale generalizzato e usarlo toocreate un nuove macchine virtuali in Azure](upload-generalized-managed.md)
- Se non è stato eseguito Sysprep prima dell'esportazione, hello disco rigido virtuale viene considerato **specializzato**, vedere [caricare un specializzato tooAzure VHD e creare una nuova macchina virtuale](create-vm-specialized.md)

 
