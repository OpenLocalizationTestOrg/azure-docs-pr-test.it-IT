---
title: aaaUsing DNS interno per la macchina virtuale la risoluzione dei nomi in Azure | Documenti Microsoft
description: Uso del DNS interno per la risoluzione dei nomi di macchine virtuali in Azure.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: 94fd6577aa51ce5db4dc26649b415ddeeb410eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a>Uso del DNS interno per la risoluzione dei nomi di macchine virtuali in Azure

Questo articolo illustra come tooset nomi DNS interni statici per le macchine virtuali Linux con schede di rete virtuale (VNic) e i nomi DNS con etichetta. Si ricorre ai nomi DNS statici per i servizi di infrastruttura permanenti, ad esempio per un server di compilazione Jenkins, usato per questo documento, o un server Git.

requisiti di Hello sono:

* [Un account di Azure](https://azure.microsoft.com/pricing/free-trial/)
* [File di chiavi SSH pubbliche e private](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- [Azure CLI 1.0](#quick-commands) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello


## <a name="quick-commands"></a>Comandi rapidi

Se è necessario tooquickly attività hello, hello successiva sezione Dettagli comandi hello necessari. Ulteriori informazioni e il contesto per ogni passaggio è reperibile rest hello del documento hello, [avvio qui](#detailed-walkthrough).  

Prerequisiti: gruppo di risorse, rete virtuale, gruppo di sicurezza di rete con SSH in ingresso, subnet.

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a>Creare una scheda di interfaccia di rete virtuale con un nome DNS interno statico

Hello `-r` flag cli è per l'etichetta DNS di impostazione hello, che fornisce nome DNS statico hello per hello scheda di rete virtuale.

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-hello-vm-into-hello-vnet-nsg-and-connect-hello-vnic"></a>Distribuire hello VM in hello rete virtuale, gruppo e, connettersi hello VNic

Hello `-N` si connette hello VNic toohello nuova macchina virtuale durante hello tooAzure di distribuzione.

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a>Procedura dettagliata

Un'integrazione completa continua e distribuzione continua (CiCd) infrastruttura di Azure richiede alcuni server server toobe statico o di lunga durata.  È consigliabile che le risorse di Azure come le reti virtuali (Vnet) hello e rete sicurezza gruppi, deve essere statiche e le risorse distribuite raramente di lunga durata.  Dopo la distribuzione di una rete virtuale, può essere riutilizzato per nuove distribuzioni senza alcuna infrastruttura toohello effetto negativo.  Aggiunta di rete statica toothis un Git repository server e un server di automazione di Jenkins offre CiCd tooyour gli ambienti di sviluppo o test.  

I nomi DNS interni sono risolvibili solo all'interno di una rete virtuale di Azure.  I nomi DNS hello sono interni, pertanto non sono toohello risolvibile all'esterno di internet, offre un'infrastruttura toohello aggiuntiva di sicurezza.

_Sostituire i nomi nell'esempio con nomi personalizzati._

## <a name="create-hello-resource-group"></a>Creare il gruppo di risorse hello

Un gruppo di risorse è necessario tooorganize tutto ciò che viene creata nella procedura dettagliata.  Per altre informazioni sui gruppi di risorse di Azure, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-hello-vnet"></a>Creare hello rete virtuale

primo passaggio Hello è toobuild toolaunch una rete virtuale hello macchine virtuali in.  Hello rete virtuale contiene una subnet per questa procedura dettagliata.  Per ulteriori informazioni sulle reti virtuali di Azure, vedere [creare una rete virtuale tramite hello CLI di Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-hello-nsg"></a>Creare hello NSG

Hello Subnet si basa dietro a un gruppo di sicurezza di rete esistente, creata hello NSG prima hello Subnet.  Azure NSGs sono equivalenti tooa firewall a livello di rete hello.  Per ulteriori informazioni su Azure NSGs, vedere [come NSGs toocreate in hello CLI di Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Aggiungere una regola di assenso SSH in ingresso

Hello VM Linux richiede l'accesso da hello internet in modo da una regola che consente di porta in ingresso traffico 22 toobe passati tramite hello rete tooport 22 hello VM Linux è necessaria.

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>Aggiungere un toohello subnet rete virtuale

Macchine virtuali all'interno di hello rete virtuale devono trovarsi in una subnet.  Ogni rete virtuale può avere più subnet.  Creare subnet hello e associare subnet hello hello NSG tooadd una subnet toohello firewall.

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

Hello Subnet è ora aggiunto all'interno di reti virtuali hello e associata a hello gruppo e regola gruppo hello.

## <a name="creating-static-dns-names"></a>Creazione di nomi DNS statici

Azure è molto flessibile, ma toouse i nomi DNS per la risoluzione dei nomi di macchine virtuali, è necessario toocreate come virtuale schede (VNics) tramite l'assegnazione di etichette DNS di rete.  VNics sono importanti per poterli usare di nuovo connettendo le macchine virtuali toodifferent, che consente di mantenere hello VNic come una risorsa statica hello macchine virtuali può essere temporaneo.  Tramite l'assegnazione di etichette in hello VNic DNS, siamo tooenable in grado di risoluzione dei nomi semplici da altre macchine virtuali nella rete virtuale hello.  Utilizzo dei nomi di risolvibili consente altri server di automazione hello tooaccess macchine virtuali in base al nome DNS hello `Jenkins` o di server di Git hello `gitrepo`.  Creare una scheda di rete virtuale e associarlo a hello che subnet creato nel passaggio precedente hello.

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Distribuire hello VM nella rete virtuale hello e gruppo

È ora disponibile una rete virtuale, una subnet all'interno di tale rete virtuale e un gruppo che agisce come un tooprotect firewall la subnet bloccare tutto il traffico in ingresso, ad eccezione di porta 22 per SSH.  è ora possibile distribuire Hello VM all'interno di questa infrastruttura di rete esistente.

Utilizzando hello Azure CLI e hello `azure vm create` comando hello VM Linux è toohello distribuito esistente al gruppo di risorse di Azure, rete virtuale, Subnet e scheda di rete virtuale.  Per ulteriori informazioni sull'utilizzo di hello CLI toodeploy una VM completezza, vedere [creare un ambiente completo di Linux mediante hello CLI di Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

Utilizzando hello CLI flag toocall risorse esistente, è indicare hello toodeploy Azure VM all'interno di una rete esistente hello.  tooreiterate, dopo una rete virtuale e subnet sono stati distribuiti, essi possono essere lasciati come statiche o permanente di risorse all'interno di propria area di Azure.  

## <a name="next-steps"></a>Passaggi successivi
* [Creare un ambiente Linux completo mediante l'interfaccia della riga di comando di Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Creare una VM Linux in Azure usando i modelli](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
