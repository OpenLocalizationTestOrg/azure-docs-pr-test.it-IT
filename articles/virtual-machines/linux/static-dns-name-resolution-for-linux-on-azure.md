---
title: aaaUse DNS interno per la macchina virtuale la risoluzione dei nomi con hello Azure CLI 2.0 | Documenti Microsoft
description: Come la rete virtuale toocreate schede di interfaccia e utilizzare DNS interno per la risoluzione dei nomi di macchina virtuale in Azure con hello Azure CLI 2.0
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
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: b3c4bfd3ab698f7b25d763ba9e60dd7984f6269d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a>Creare schede di interfaccia di rete virtuale e usare DNS interni per la risoluzione dei nomi di VM in Azure
Questo articolo illustra come tooset statici nomi DNS interni per le macchine virtuali Linux mediante rete schede di interfaccia (vNics) e i nomi DNS con etichetta con hello CLI di Azure 2.0. È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Si ricorre ai nomi DNS statici per i servizi di infrastruttura permanenti, ad esempio per un server di compilazione Jenkins, usato per questo documento, o un server Git.

requisiti di Hello sono:

* [Un account di Azure](https://azure.microsoft.com/pricing/free-trial/)
* [File di chiavi SSH pubbliche e private](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a>Comandi rapidi
Se è necessario tooquickly attività hello, hello successiva sezione Dettagli comandi hello necessari. Ulteriori informazioni e il contesto per ogni passaggio è reperibile nel resto di hello del documento hello, [avvio qui](#detailed-walkthrough). tooperform questi passaggi, è necessario hello più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).

Pre-requisiti: gruppo di risorse, rete virtuale e subnet, gruppo di sicurezza di rete con SSH in ingresso.

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a>Creare una scheda di interfaccia di rete virtuale con un nome DNS interno statico
Creare una scheda di rete virtuale hello con [az rete nic creare](/cli/azure/network/nic#create). Hello `--internal-dns-name` flag CLI è per l'etichetta DNS di impostazione hello, che fornisce nome DNS statico hello per scheda di interfaccia di rete virtuale hello (vNic). esempio Hello crea una scheda di rete virtuale denominata `myNic`, connetterla toohello `myVnet` rete virtuale e viene creato un record di nome DNS interno denominato `jenkins`:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-hello-vnic"></a>Distribuire una macchina virtuale e connettersi hello vNic
Creare una VM con il comando [az vm create](/cli/azure/vm#create). Hello `--nics` flag si connette hello vNic toohello VM durante hello tooAzure di distribuzione. esempio Hello crea una macchina virtuale denominata `myVM` con i dischi di Azure gestita e collega hello vNic denominato `myNic` da hello passaggio precedente:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a>Procedura dettagliata

Un'integrazione completa continua e distribuzione continua (CiCd) infrastruttura di Azure richiede alcuni server server toobe statico o di lunga durata. È consigliabile che le risorse di Azure come hello reti virtuali e i gruppi di sicurezza di rete sono statiche e le risorse distribuite raramente di lunga durata. Dopo la distribuzione di una rete virtuale, può essere riutilizzato per nuove distribuzioni senza alcuna infrastruttura toohello effetto negativo. È quindi possibile aggiungere un server di repository Git o un server di automazione di Jenkins recapita CiCd toothis di rete virtuale per gli ambienti di sviluppo o test.  

I nomi DNS interni sono risolvibili solo all'interno di una rete virtuale di Azure. I nomi DNS hello sono interni, pertanto non sono toohello risolvibile all'esterno di internet, offre un'infrastruttura toohello aggiuntiva di sicurezza.

In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono `myResourceGroup`, `myNic` e `myVM`.

## <a name="create-hello-resource-group"></a>Creare il gruppo di risorse hello
Innanzitutto, creare il gruppo di risorse hello con [gruppo az creare](/cli/azure/group#create). esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `westus` percorso:

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-hello-virtual-network"></a>Creare una rete virtuale hello

passaggio successivo Hello è toobuild toolaunch una rete virtuale hello macchine virtuali in. rete virtuale Hello contiene una subnet per questa procedura dettagliata. Per ulteriori informazioni su reti virtuali di Azure, vedere [creare una rete virtuale mediante Azure CLI hello](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Creare una rete virtuale di hello con [creazione della rete virtuale di rete az](/cli/azure/network/vnet#create). esempio Hello crea una rete virtuale denominata `myVnet` e subnet denominata `mySubnet`:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-hello-network-security-group"></a>Creare il gruppo di sicurezza di rete hello
Azure i gruppi di sicurezza di rete sono equivalenti tooa firewall a livello di rete hello. Per ulteriori informazioni sui gruppi di sicurezza di rete, vedere [come NSGs toocreate in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Creare un gruppo di sicurezza di rete hello con [rete az creare](/cli/azure/network/nsg#create). esempio Hello crea un gruppo di sicurezza di rete denominato `myNetworkSecurityGroup`:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-tooallow-ssh"></a>Aggiungere un tooallow regola in entrata SSH
Aggiungere una regola in ingresso per il gruppo di sicurezza di rete hello con [creare una regola gruppo rete az](/cli/azure/network/nsg/rule#create). esempio Hello crea una regola denominata `myRuleAllowSSH`:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-hello-subnet-with-hello-network-security-group"></a>Associare subnet hello hello il gruppo di sicurezza di rete
subnet hello tooassociate hello gruppo di sicurezza di rete, utilizzare [aggiornare subnet rete virtuale di rete az](/cli/azure/network/vnet/subnet#update). esempio Hello associa il nome di subnet hello `mySubnet` con il gruppo di sicurezza di rete denominata hello `myNetworkSecurityGroup`:

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-hello-virtual-network-interface-card-and-static-dns-names"></a>Creare una scheda di interfaccia di rete virtuale hello e i nomi DNS statici
Azure è molto flessibile, ma toouse i nomi DNS per la risoluzione dei nomi di macchina virtuale, è necessario toocreate virtuale schede di rete (vNics) che includono un'etichetta DNS. vNics sono importanti per poterli usare di nuovo connettendo le macchine virtuali toodifferent sul ciclo di vita di hello infrastruttura. Questo approccio consente di mantenere hello vNic come una risorsa statica durante hello macchine virtuali può essere temporaneo. Tramite l'assegnazione di etichette su NIC virtuale hello DNS, siamo tooenable in grado di risoluzione dei nomi semplici da altre macchine virtuali nella rete virtuale hello. Utilizzo dei nomi di risolvibili consente altri server di automazione hello tooaccess macchine virtuali in base al nome DNS hello `Jenkins` o di server di Git hello `gitrepo`.  

Creare una scheda di rete virtuale hello con [az rete nic creare](/cli/azure/network/nic#create). esempio Hello crea una scheda di rete virtuale denominata `myNic`, connetterla toohello `myVnet` rete virtuale denominata `myVnet`e viene creato un record di nome DNS interno denominato `jenkins`:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Distribuire hello VM nell'infrastruttura di rete virtuale hello
È ora disponibile una rete virtuale e una subnet, un gruppo di sicurezza di rete che agisce come un tooprotect firewall la subnet bloccare tutto il traffico in ingresso, ad eccezione di porta 22 per SSH e una scheda di rete virtuale. Ora è possibile distribuire una VM all'interno di questa infrastruttura di rete esistente.

Creare una VM con il comando [az vm create](/cli/azure/vm#create). esempio Hello crea una macchina virtuale denominata `myVM` con i dischi di Azure gestita e collega hello vNic denominato `myNic` da hello passaggio precedente:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

Utilizzando hello CLI flag toocall risorse esistente, è indicare hello toodeploy Azure VM all'interno di una rete esistente hello. tooreiterate, dopo una rete virtuale e subnet sono stati distribuiti, essi possono essere lasciati come statiche o permanente di risorse all'interno di propria area di Azure.  

## <a name="next-steps"></a>Passaggi successivi
* [Creare un ambiente Linux completo mediante l'interfaccia della riga di comando di Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Creare una VM Linux in Azure usando i modelli](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
