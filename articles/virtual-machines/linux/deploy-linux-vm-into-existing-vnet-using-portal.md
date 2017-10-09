---
title: aaaDeploy le macchine virtuali Linux in una rete esistente con il portale di Azure | Documenti Microsoft
description: Distribuire una VM Linux in una rete virtuale esistente a Azure tramite il portale di hello.
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 51272b8cdb1dc7f3fe768d2ebbf4ebe0d754cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-portal"></a>Come toodeploy una macchina virtuale di Linux in una rete virtuale di Azure esistente con hello portale di Azure

In questo articolo illustra come toodeploy una macchina virtuale (VM) in una rete virtuale esistente (VNet). Gli asset di Azure, come le reti virtuali e i gruppi di sicurezza di rete, devono essere risorse statiche, ovvero di lunga durata e distribuite raramente. Dopo la distribuzione di una rete virtuale, può essere riutilizzato da ridistribuzioni costante senza alcuna infrastruttura toohello effetto negativo. Pensa a una rete virtuale come un tradizionale commutatore di rete hardware - non è necessario passare un nuovo hardware per ciascuna distribuzione tooconfigure.  

Con una rete virtuale è configurata correttamente, è possibile continuare toodeploy nuovi server in tale rete virtuale a più volte con alcuni, se presente, le modifiche richieste per la durata hello di hello rete virtuale.

## <a name="create-hello-resource-group"></a>Creare il gruppo di risorse hello

Creare innanzitutto un tooorganize gruppo di risorse tutti gli oggetti creati in questa procedura dettagliata. Per altre informazioni sui gruppi di risorse di Azure, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-hello-vnet"></a>Creare hello rete virtuale

Successivamente, compilare un hello toolaunch di rete virtuale le macchine virtuali in. Hello rete virtuale contiene una subnet e associato al gruppo di sicurezza di rete hello con questa subnet in un passaggio successivo.

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-toohello-subnet"></a>Aggiungere una subnet toohello VNic

Schede di rete virtuale (VNics) sono importanti, come è possibile collegare le macchine virtuali toodifferent. Questo approccio consente di mantenere hello VNic come una risorsa statica durante hello macchine virtuali può essere temporaneo. Creare una scheda di rete virtuale e associarlo a subnet hello creato nel passaggio precedente hello.

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-hello-network-security-group"></a>Creare un gruppo di sicurezza di rete hello

Gruppi di sicurezza di rete di Azure sono equivalenti tooa firewall a livello di rete hello. Per altre informazioni sui gruppi di sicurezza di rete di Azure, vedere [Che cos'è un gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md).

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a>Aggiungere una regola di assenso SSH in ingresso

Hello VM richiede l'accesso da hello internet, in modo da una regola che consente la porta in ingresso 22 traffico toobe passati tramite hello rete tooport 22 hello viene creata la VM.

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-hello-nsg-with-hello-subnet"></a>Associare subnet hello hello NSG

Con rete virtuale hello e una subnet hello creato, associare il gruppo di sicurezza rete hello subnet hello. È possibile associare i gruppi di sicurezza di rete a un'intera subnet o a una scheda di rete virtuale singola. Con il filtro di traffico a livello di subnet hello firewall di hello, tutti VNics e hello macchine virtuali all'interno di subnet hello sono protetti dal gruppo di sicurezza di rete hello. Hello altri approcci è hello gruppo di sicurezza di rete viene associato solo un singolo VNic e protegge solo una macchina virtuale.

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Distribuire hello VM nella rete virtuale hello e gruppo

Utilizzo di hello portale di Azure, hello VM Linux è toohello distribuito esistente al gruppo di risorse di Azure, rete virtuale, Subnet e scheda di rete virtuale.

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

Utilizzando le risorse esistenti di hello toochoose portale, è possibile indicare hello toodeploy Azure VM all'interno di una rete esistente hello. Una volta distribuite la rete virtuale e la subnet possono essere usate come risorse statiche o permanenti nell'area di Azure.  

## <a name="next-steps"></a>Passaggi successivi

* [Utilizzare un toocreate modello di gestione risorse di Azure una distribuzione specifica](../windows/cli-deploy-templates.md)
* [Creare un ambiente Linux completo mediante l'interfaccia della riga di comando di Azure](create-cli-complete.md)
* [Creare una VM Linux in Azure usando i modelli](create-ssh-secured-vm-from-template.md)
