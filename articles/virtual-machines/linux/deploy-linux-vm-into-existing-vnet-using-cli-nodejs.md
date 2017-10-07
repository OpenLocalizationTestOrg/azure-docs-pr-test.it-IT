---
title: aaaDeploy le macchine virtuali Linux in una rete esistente con 1.0 CLI di Azure | Documenti Microsoft
description: Come toodeploy una VM Linux in una rete virtuale esistente usando hello Azure CLI 1.0
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a>Come una macchina virtuale di Linux in una rete virtuale di Azure esistente con hello Azure CLI 1.0 toodeploy

In questo articolo illustra come toouse CLI di Azure 1.0 toodeploy una macchina virtuale (VM) in una rete virtuale esistente (VNet). requisiti di Hello sono:

- [Un account di Azure](https://azure.microsoft.com/pricing/free-trial/)
- [File di chiavi SSH pubbliche e private](mac-create-ssh-keys.md)


## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- [Azure CLI 1.0](#quick-commands) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello


## <a name="quick-commands"></a>Comandi rapidi

Se è necessario tooquickly attività hello, hello successiva sezione Dettagli comandi hello necessari. Ulteriori informazioni e il contesto per ogni passaggio è reperibile rest hello del documento hello, [avvio qui](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).

Prerequisiti: gruppo di risorse, rete virtuale, gruppo di sicurezza di rete con SSH in ingresso, subnet. Sostituire gli esempi con le impostazioni desiderate.

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Distribuire hello VM nell'infrastruttura di rete virtuale hello

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a>Procedura dettagliata

Risorse di Azure come hello reti virtuali e i gruppi di sicurezza di rete devono essere statici e le risorse distribuite raramente di lunga durata. Dopo la distribuzione di una rete virtuale, può essere riutilizzato per nuove distribuzioni senza alcuna infrastruttura toohello effetto negativo. Si pensi a una rete virtuale come se fosse uno switch di rete hardware tradizionale. Non è necessario passare un nuovo hardware per ciascuna distribuzione tooconfigure. Con una rete virtuale è configurata correttamente, è possibile continuare toodeploy nuovi server in tale rete virtuale a più volte con alcuni, se presente, le modifiche richieste per la durata hello di hello rete virtuale.

## <a name="create-hello-resource-group"></a>Creare il gruppo di risorse hello

Creare innanzitutto un tooorganize gruppo di risorse tutti gli oggetti creati in questa procedura dettagliata. Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a>Creare hello rete virtuale

primo passaggio Hello è toobuild toolaunch una rete virtuale hello macchine virtuali in. Hello rete virtuale contiene una subnet per questa procedura dettagliata. Per ulteriori informazioni sulle reti virtuali di Azure, vedere [creare una rete virtuale tramite hello CLI di Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a>Creare un gruppo di sicurezza di rete hello

subnet Hello viene compilato dietro a un gruppo di sicurezza di rete esistente pertanto creare gruppi di sicurezza di rete hello prima subnet hello. Gruppi di sicurezza di rete di Azure sono equivalenti tooa firewall a livello di rete hello. Per ulteriori informazioni sui gruppi di sicurezza di rete di Azure, vedere [come i gruppi di sicurezza di rete toocreate in hello CLI di Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Aggiungere una regola di assenso SSH in ingresso

Hello VM richiede l'accesso da hello internet in modo da una regola che consente la porta in ingresso 22 traffico toobe passati tramite hello rete tooport 22 hello macchina virtuale è necessaria.

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>Aggiungere un toohello subnet rete virtuale

Macchine virtuali all'interno di hello rete virtuale devono trovarsi in una subnet. Ogni rete virtuale può avere più subnet. Creare subnet hello e associare al gruppo di sicurezza di rete hello.

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

Hello Subnet è ora aggiunto all'interno di reti virtuali hello e associata alla regola e gruppo di sicurezza di rete hello.


## <a name="add-a-vnic-toohello-subnet"></a>Aggiungere una subnet toohello VNic

Schede di rete virtuale (VNics) sono importanti, come è possibile riutilizzare gli connettendo le macchine virtuali toodifferent. Questo approccio consente di mantenere hello VNic come una risorsa statica durante hello macchine virtuali può essere temporaneo. Creare una scheda di rete virtuale e associarlo a subnet hello creato nel passaggio precedente hello.

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Distribuire hello VM nella rete virtuale hello e gruppo

È ora disponibile una rete virtuale e una subnet all'interno di tale rete virtuale e un gruppo di sicurezza di rete che agisce subnet hello tooprotect bloccare tutto il traffico in ingresso, ad eccezione di porta 22 per SSH. è ora possibile distribuire Hello VM all'interno di questa infrastruttura di rete esistente.

Utilizzando hello Azure CLI e hello `azure vm create` comando hello VM Linux è toohello distribuito esistente al gruppo di risorse di Azure, rete virtuale, Subnet e scheda di rete virtuale. Per ulteriori informazioni sull'utilizzo di hello CLI toodeploy una VM completezza, vedere [creare un ambiente completo di Linux mediante hello CLI di Azure](create-cli-complete.md)

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

Utilizzando hello CLI flag toocall risorse esistente, indicando hello toodeploy Azure VM all'interno di una rete esistente hello. Una volta distribuite la rete virtuale e la subnet possono essere usate come risorse statiche o permanenti nell'area di Azure.  

## <a name="next-steps"></a>Passaggi successivi

* [Utilizzare un toocreate modello di gestione risorse di Azure una distribuzione specifica](../windows/cli-deploy-templates.md)
* [Creare un ambiente Linux completo mediante l'interfaccia della riga di comando di Azure](create-cli-complete.md)
* [Creare una VM Linux in Azure usando i modelli](create-ssh-secured-vm-from-template.md)
