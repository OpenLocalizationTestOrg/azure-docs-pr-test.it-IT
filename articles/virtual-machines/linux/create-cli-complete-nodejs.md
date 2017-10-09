---
title: un ambiente completo di Linux con hello Azure CLI 1.0 aaaCreate | Documenti Microsoft
description: Creare archiviazione, una VM Linux, una rete virtuale e subnet, un bilanciamento del carico, una scheda di rete, un indirizzo IP pubblico e un gruppo di sicurezza di rete, tutti da hello messa a terra tramite hello Azure CLI 1.0.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 7fe00e138704fe9c9a1c9b87a7dd1afd6174e527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-environment-with-hello-azure-cli-10"></a>Creare un ambiente completo di Linux con hello Azure CLI 1.0
In questo articolo viene spiegato come creare una semplice rete con un servizio di bilanciamento del carico e un paio di VM utili per lo sviluppo e per calcoli semplici. Esaminare il processo di hello dal comando, fino a quando non si dispone di due funzionante, proteggere le macchine virtuali Linux toowhich che è possibile connettersi da un punto qualsiasi in hello Internet. È quindi possibile spostare su ambienti e reti complesse toomore.

Lungo il percorso di hello, conoscere gerarchia delle dipendenze hello che offre modello di distribuzione di gestione risorse di hello e su quanta capacità fornisce. Dopo aver visualizzato la modalità di compilazione sistema hello, è possibile ricompilare molto più rapidamente utilizzando [modelli di Azure Resource Manager](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Inoltre, dopo aver appreso come hello parti dell'ambiente montate, creazione di modelli tooautomate li diventa più facile.

ambiente di Hello contiene:

* Due VM all'interno di un set di disponibilità.
* Un servizio di bilanciamento del carico con una regola di bilanciamento del carico sulla porta 80.
* Rete gruppo di sicurezza (), le regole per la macchina virtuale dal traffico indesiderato tooprotect.

toocreate questo ambiente personalizzato, è necessario più recente hello [CLI di Azure 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in modalità di gestione risorse (`azure config mode arm`). È inoltre necessario uno strumento di analisi JSON. In questo esempio viene utilizzato [jq](https://stedolan.github.io/jq/).


## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- [Azure CLI 1.0](#quick-commands) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello


## <a name="quick-commands"></a>Comandi rapidi
Se è necessario tooquickly attività hello, hello seguente hello dettagli sezione base tooupload comandi tooAzure una macchina virtuale. Ulteriori informazioni e il contesto per ogni passaggio è reperibile nel resto di hello del documento hello, a partire [qui](#detailed-walkthrough).

Assicurarsi di aver [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) effettuato l'accesso e utilizzo della modalità di gestione delle risorse:

```azurecli
azure config mode arm
```

In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `myVM`.

Creare il gruppo di risorse hello. esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `westeurope` percorso:

```azurecli
azure group create -n myResourceGroup -l westeurope
```

Verificare che il gruppo di risorse hello utilizzando parser JSON hello:

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Creare account di archiviazione hello. esempio Hello crea un account di archiviazione denominato `mystorageaccount`. (nome di account di archiviazione hello deve essere univoco, quindi fornire il proprio nome univoco.)

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

Verificare l'account di archiviazione hello utilizzando parser JSON hello:

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

Creare la rete virtuale hello. esempio Hello crea una rete virtuale denominata `myVnet`:

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

Creare una subnet. esempio Hello crea una subnet denominata `mySubnet`:

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

Verificare la rete virtuale hello e subnet utilizzando parser JSON hello:

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

Creare un indirizzo IP pubblico. esempio Hello crea un indirizzo IP pubblico denominato `myPublicIP` con nome DNS hello `mypublicdns`. (nome DNS hello deve essere univoco, quindi fornire il proprio nome univoco.)

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

Creazione di bilanciamento del carico hello. esempio Hello crea un bilanciamento del carico denominato `myLoadBalancer`:

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

Creare un pool IP front-end di bilanciamento del carico hello e associare l'indirizzo IP pubblico hello. esempio Hello crea un pool IP front-end denominato `mySubnetPool`:

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

Creare pool IP hello back-end di bilanciamento del carico hello. esempio Hello crea un pool IP back-end denominato `myBackEndPool`:

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

Creare la rete in ingresso SSH regole translation (NAT) indirizzo di bilanciamento del carico hello. esempio Hello crea due regole di bilanciamento del carico, `myLoadBalancerRuleSSH1` e `myLoadBalancerRuleSSH2`:

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

Creare web hello regole NAT in ingresso per hello bilanciamento del carico. esempio Hello crea una regola di bilanciamento del carico denominata `myLoadBalancerRuleWeb`:

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

Creare i probe di integrità bilanciamento del carico hello. esempio Hello crea un probe TCP denominato `myHealthProbe`:

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

Verificare le regole NAT bilanciamento del carico hello e pool IP utilizzando parser JSON hello:

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

Creare hello prima scheda di rete (NIC). Sostituire hello `#####-###-###` sezioni con il proprio ID sottoscrizione Azure. La sottoscrizione con ID è riportato un output di hello **jq** quando si esaminano le risorse di hello si sta creando. È anche possibile visualizzare l'ID sottoscrizione con `azure account list`.

esempio Hello crea una scheda di rete denominata `myNic1`:

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

Creare hello seconda scheda di rete. esempio Hello crea una scheda di rete denominata `myNic2`:

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

Verificare hello due schede di rete utilizzando il parser JSON hello:

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

Creare un gruppo di sicurezza di rete hello. esempio Hello crea un gruppo di sicurezza di rete denominato `myNetworkSecurityGroup`:

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

Aggiungere due regole in entrata per il gruppo di sicurezza di rete hello. esempio Hello crea due regole, `myNetworkSecurityGroupRuleSSH` e `myNetworkSecurityGroupRuleHTTP`:

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

Verificare le regole in entrata e gruppo di sicurezza di rete hello utilizzando parser JSON hello:

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

Associazione di sicurezza di rete hello toohello due schede di rete di gruppo:

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

Creare set di disponibilità hello. esempio Hello crea un set denominato di disponibilità `myAvailabilitySet`:

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

Creare hello prima VM Linux. esempio Hello crea una macchina virtuale denominata `myVM1`:

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

Creare hello secondo VM Linux. esempio Hello crea una macchina virtuale denominata `myVM2`:

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

Utilizzare hello JSON parser tooverify che tutto ciò che è stato compilato:

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

Esportare il nuovo ambiente tooa tooquickly ricreare nuove istanze di modello:

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a>Procedura dettagliata
Hello dettagliati passaggi che seguono illustrano ogni comando operazioni eseguite durante la compilazione orizzontale dell'ambiente. Questi concetti torneranno utili in fase di creazione degli ambienti personalizzati per lo sviluppo o per la produzione.

Assicurarsi di aver [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) effettuato l'accesso e utilizzo della modalità di gestione delle risorse:

```azurecli
azure config mode arm
```

In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `myVM`.

## <a name="create-resource-groups-and-choose-deployment-locations"></a>Creare i gruppi di risorse e scegliere i percorsi di distribuzione
I gruppi di risorse di Azure sono entità logica di distribuzione che contengono informazioni e i metadati tooenable hello logica gestione della configurazione di distribuzioni di risorse. esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `westeurope` percorso:

```azurecli
azure group create --name myResourceGroup --location westeurope
```

Output:

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a>Creare un account di archiviazione
È necessario l'account di archiviazione per i dischi di macchina virtuale e per qualsiasi disco dati aggiuntivo che si desidera tooadd. Si creano account di archiviazione quasi subito dopo la creazione di gruppi di risorse.

In questo caso si usa hello `azure storage account create` comando, passando il percorso di hello dell'account di hello, gruppo di risorse hello che controlla e tipo hello di supporto di archiviazione desiderato. esempio Hello crea un account di archiviazione denominato `mystorageaccount`:

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

Output:

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

la risorsa gruppo mediante hello tooexamine `azure group show` comando, è possibile utilizzare hello [jq](https://stedolan.github.io/jq/) strumento insieme hello `--json` opzione CLI di Azure. (È possibile utilizzare **jsawk** o qualsiasi libreria linguaggio si preferisce tooparse hello JSON.)

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Output:

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

account di archiviazione tooinvestigate hello utilizzando hello CLI, è necessario innanzitutto le chiavi e nomi di account tooset hello. Sostituire il nome di hello hello dell'account di archiviazione nel seguente esempio con un nome che si sceglie di hello:

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

Dopodiché è possibile visualizzare facilmente le informazioni di archiviazione:

```azurecli
azure storage container list
```

Output:

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a>Creare una rete virtuale e una subnet
Successivamente sarà tooneed toocreate una rete virtuale in esecuzione in Azure e una subnet in cui è possibile creare le macchine virtuali. esempio Hello crea una rete virtuale denominata `myVnet` con hello `192.168.0.0/16` prefisso dell'indirizzo:

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

Output:

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

Nuovamente, consente di usare il possibilità - json hello di `azure group show` e `jq` toosee come svilupperemo le risorse. Ora sono disponibili una risorsa `storageAccounts` e una risorsa `virtualNetworks`.  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Output:

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

Ora è possibile crearne una subnet in hello `myVnet` rete virtuale in cui hello sono distribuite macchine virtuali. Utilizziamo hello `azure network vnet subnet create` comando, insieme a risorse hello abbiamo creato: hello `myResourceGroup` gruppo di risorse e hello `myVnet` rete virtuale. Nell'esempio seguente di hello, aggiungiamo subnet hello denominata `mySubnet` con prefisso dell'indirizzo di subnet hello `192.168.1.0/24`:

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

Output:

```azurecli
info:    Executing command network vnet subnet create
+ Looking up hello subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up hello subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

Poiché subnet hello è logicamente all'interno di rete virtuale hello, cercare informazioni sulla subnet hello con un comando leggermente diverso. comando Hello utilizziamo `azure network vnet show`, ma si continua l'output JSON hello tooexamine utilizzando `jq`.

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

Output:

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a>Creare un indirizzo IP pubblico
Ora è possibile crearne hello indirizzo IP pubblico (PIP) che vengono assegnati tooyour servizio di bilanciamento del carico. La procedura permette tooconnect tooyour, le macchine virtuali da Internet hello utilizzando hello `azure network public-ip create` comando. Poiché l'indirizzo predefinito hello è dinamico, non è creare una voce DNS denominata in hello **cloudapp.azure.com** dominio utilizzando hello `--domain-name-label` opzione. esempio Hello crea un indirizzo IP pubblico denominato `myPublicIP` con nome DNS hello `mypublicdns`. Poiché il nome DNS hello deve essere univoco, è fornire il proprio nome DNS univoco:

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

Output:

```azurecli
info:    Executing command network public-ip create
+ Looking up hello public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up hello public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

Hello indirizzo IP pubblico è anche una risorsa di primo livello, in modo da visualizzare con `azure group show`.

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Output:

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

È possibile esaminare ulteriori dettagli di risorse, inclusi il nome di dominio completo hello (FQDN) del sottodominio hello, utilizzando hello completo `azure network public-ip show` comando. risorsa di indirizzo IP pubblica Hello è stata allocata in modo logico, ma non è ancora stato assegnato un indirizzo specifico. tooobtain un indirizzo IP, sarà tooneed un bilanciamento del carico, non è stato ancora creato.

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

Output:

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a>Creare un servizio di bilanciamento del carico e i pool di indirizzi IP
Quando si crea un bilanciamento del carico, consente il traffico toodistribute tra più macchine virtuali. Fornisce inoltre l'applicazione tooyour ridondanza tramite l'esecuzione di più macchine virtuali che rispondono a richieste toouser nell'evento di hello di manutenzione o di notevoli carichi di lavoro. esempio Hello crea un bilanciamento del carico denominato `myLoadBalancer`:

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

Output:

```azurecli
info:    Executing command network lb create
+ Looking up hello load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

Il servizio di bilanciamento del carico è piuttosto vuoto, per cui si creeranno alcuni pool di indirizzi IP. Vogliamo toocreate due pool IP per il bilanciamento del carico, una per i componenti front-end hello e uno per back-end hello. il pool IP front-end di Hello è visibile pubblicamente. È inoltre toowhich percorso hello che assegniamo hello PIP creati in precedenza. Quindi utilizziamo pool back-end hello come un percorso per il nostro tooconnect macchine virtuali per. In questo modo, hello il traffico tramite toohello di bilanciamento carico di hello macchine virtuali.

Prima di tutto si creerà il pool di indirizzi IP front-end. esempio Hello crea un pool di server front-end denominato `myFrontEndPool`:

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

Output:

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up hello load balancer "myLoadBalancer"
+ Looking up hello public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

Si noti come è possibile usare hello `--public-ip-name` attivare toopass hello `myPublicIP` creati in precedenza. Assegnazione indirizzo IP pubblico hello servizio di bilanciamento del carico indirizzo toohello consente tooreach le macchine virtuali tra hello Internet.

Quindi si creerà il secondo pool di indirizzi IP, questa volta per il traffico back-end. esempio Hello crea un pool back-end denominato `myBackEndPool`:

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

Output:

```azurecli
info:    Executing command network lb address-pool create
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

È possibile osservare come il bilanciamento del carico procede esaminando con `azure network lb show` ed esaminando l'output JSON hello:

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

Output:

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a>Creare le regole NAT per il servizio di bilanciamento del carico
traffico tooget che passano attraverso il servizio di bilanciamento del carico, è necessario la regole toocreate network address translation (NAT) che specificano le azioni in ingresso o in uscita. È possibile specificare hello protocollo toouse, quindi eseguire il mapping di porte toointernal porte esterne come desiderato. Per l'ambiente, creare alcune regole che consentono di SSH tramite il nostro tooour del servizio di bilanciamento carico di macchine virtuali. È necessario impostare la porta TCP porte 4222 e 4223 toodirect tooTCP 22 nel nostro macchine virtuali (che si creano più avanti). esempio Hello crea una regola denominata `myLoadBalancerRuleSSH1` toomap TCP porta 4222 tooport 22:

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

Output:

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

Ripetere la procedura hello per la seconda regola NAT per SSH. esempio Hello crea una regola denominata `myLoadBalancerRuleSSH2` toomap TCP porta 4223 tooport 22:

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

Verrà inoltre proseguo e creare una regola NAT per la porta TCP 80 per il traffico web, l'associazione di pool IP tooour regola hello. Se è collegare hello regola tooan pool IP, anziché l'associazione di hello regola tooour macchine virtuali singolarmente, è possibile aggiungere o rimuovere le macchine virtuali dal pool IP hello. servizio di bilanciamento del carico Hello regola automaticamente il flusso di hello del traffico. esempio Hello crea una regola denominata `myLoadBalancerRuleWeb` toomap TCP porta 80 tooport 80:

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

Output:

```azurecli
info:    Executing command network lb rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a>Creare un probe di integrità per il servizio di bilanciamento del carico
Integrità di probe periodicamente controlli sulle macchine virtuali che si trovano dietro il nostro toomake bilanciamento di carico che è operativo e risponde toorequests come definito hello. Se non vengono rimossi dal tooensure operazione che gli utenti non vengono indirizzate toothem. È possibile definire controlli personalizzati per il probe di integrità hello, insieme a intervalli e i valori di timeout. Per altre informazioni sui probe di integrità, vedere [Probe di integrità del servizio di bilanciamento del carico](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). esempio Hello crea un TCP integrità sondati denominata `myHealthProbe`:

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

Output:

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

In questo caso è stato specificato un intervallo di 15 secondi per i controlli di integrità. È possibile perdere un massimo di quattro probe (un minuto) prima di bilanciamento del carico hello considera che ospitano hello non funziona più.

## <a name="verify-hello-load-balancer"></a>Verificare di bilanciamento del carico hello
Dopo l'operazione di configurazione di bilanciamento del carico hello viene eseguita. Di seguito sono hello passaggi:

1. È stato creato un bilanciamento del carico.
2. È stato creato un pool IP front-end e un tooit IP pubblico assegnato.
3. È stato creato un pool IP back-end a cui possono connettersi le VM.
4. Le regole NAT che consentono di macchine virtuali toohello SSH per la gestione, insieme a una regola che consenta la porta TCP 80 per l'app web creata.
5. È stato aggiunto un hello di integrità probe tooperiodically controllo macchine virtuali. Questo probe di integrità garantisce che gli utenti non tentano tooaccess una macchina virtuale che non è più funzionante o del contenuto.

Ecco il bilanciamento del carico risultante:

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

Output:

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-toouse-with-hello-linux-vm"></a>Creare un toouse NIC con hello VM Linux
Schede di rete disponibili a livello di codice in quanto è possibile applicare regole tootheir utilizzare. È inoltre possibile averne più di una. In seguito hello `azure network nic create` dei comandi, si agganciare i pool IP hello NIC toohello carico back-end e associarlo a hello traffico SSH toopermit di regole NAT.

Sostituire hello `#####-###-###` sezioni con il proprio ID sottoscrizione Azure. La sottoscrizione con ID è riportato un output di hello `jq` quando si esaminano le risorse di hello si sta creando. È anche possibile visualizzare l'ID sottoscrizione con `azure account list`.

esempio Hello crea una scheda di rete denominata `myNic1`:

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

Output:

```azurecli
info:    Executing command network nic create
+ Looking up hello subnet "mySubnet"
+ Looking up hello network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

È possibile visualizzare i dettagli di hello esaminando risorse hello direttamente. Si esamina la risorsa hello utilizzando hello `azure network nic show` comando:

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

Output:

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

Ora è creare hello seconda scheda di rete, collegare nuovamente nel pool IP tooour back-end. Questa regola NAT secondo tempo hello consenta il traffico SSH. esempio Hello crea una scheda di rete denominata `myNic2`:

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a>Creare un gruppo di sicurezza di rete e le regole corrispondenti
Ora verrà creato un gruppo di sicurezza di rete e hello per le regole in entrata che regolano l'accesso toohello scheda di rete. Un gruppo di sicurezza di rete può essere applicato tooa NIC o subnet. Definire un flusso di hello toocontrol regole del traffico da e verso le macchine virtuali. esempio Hello crea un gruppo di sicurezza di rete denominato `myNetworkSecurityGroup`:

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

Aggiungere la regola in ingresso di hello per hello NSG tooallow connessioni sulla porta 22 (toosupport SSH) in ingresso. esempio Hello crea una regola denominata `myNetworkSecurityGroupRuleSSH` tooallow TCP sulla porta 22:

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

A questo punto aggiungere la regola in ingresso di hello per hello NSG tooallow connessioni sulla porta 80 (traffico web toosupport) in ingresso. esempio Hello crea una regola denominata `myNetworkSecurityGroupRuleHTTP` tooallow TCP sulla porta 80:

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> regola connessioni in entrata Hello è un filtro per le connessioni di rete in ingresso. In questo esempio viene eseguita l'associazione hello NSG toohello NIC virtuale le macchine virtuali, il che significa che qualsiasi tooport richiesta 22 è passato toohello NIC la macchina virtuale. Questa regola è relativa alla connessione di rete anziché all'endpoint, come invece sarebbe nelle distribuzioni classiche. tooopen una porta, è necessario lasciare hello `--source-port-range` impostare troppo '\*' tooaccept (valore predefinito di hello) in entrata delle richieste da **qualsiasi** porta richiesta. Le porte sono solitamente dinamiche.
>
>

## <a name="bind-toohello-nic"></a>Associare toohello NIC
Associare hello toohello di gruppo NIC. È necessario tooconnect nostri NIC con il gruppo di sicurezza di rete. Eseguire entrambi i comandi, toohook di entrambi i nostri schede di rete:

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a>Creare un set di disponibilità
I set di disponibilità agevolano la distribuzione delle VM nei domini di errore e domini di aggiornamento. Si creerà un set di disponibilità per le VM. esempio Hello crea un set denominato di disponibilità `myAvailabilitySet`:

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

I domini di errore definiscono un gruppo di macchine virtuali che condividono una fonte di alimentazione e uno switch di rete comuni. Per impostazione predefinita, hello le macchine virtuali configurate all'interno del set di disponibilità sono separate tra i domini di errore toothree. l'idea Hello è un problema hardware in uno di questi domini di errore non influisce sulla ogni macchina virtuale che esegue l'app. Durante il posizionamento in un set di disponibilità, Azure distribuisce automaticamente le macchine virtuali in domini di errore hello.

Indicano i domini di aggiornamento gruppi di macchine virtuali e l'hardware fisico sottostante che può essere riavviata in hello contemporaneamente. ordine di Hello in cui vengono riavviati i domini di aggiornamento potrebbe non essere sequenziale durante la manutenzione pianificata, ma solo un aggiornamento è stato riavviato alla volta. D nuovo, Azure distribuisce automaticamente le VM tra i domini di aggiornamento durante il posizionamento in un sito di disponibilità.

Altre informazioni sui [la gestione della disponibilità di hello di macchine virtuali](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="create-hello-linux-vms"></a>Creare le macchine virtuali Linux hello
Risorse di archiviazione e rete hello aver creato le macchine virtuali toosupport accessibile tramite Internet. Ora è possibile creare quelle VM e proteggerle con una chiave SSH priva di password. In questo caso, verrà toocreate una VM Ubuntu in base a hello LTS più recente. Per trovare le informazioni sull'immagine si usa `azure vm image list`, come descritto nell'articolo relativo alla [ricerca di immagini di VM di Azure](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

È stata selezionata un'immagine utilizzando il comando hello `azure vm image list westeurope canonical | grep LTS`. In questo caso, si usa `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`. Ultimo campo hello, passiamo `latest` in modo che in futuro hello è ottenere sempre la compilazione più recente di hello. (stringa hello utilizziamo `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).

Il passaggio successivo è familiare tooanyone che ha già creato un ssh chiave pubblica e privata rsa associare in Linux o Mac usando **ssh-keygen - t rsa -b 2048**. Se non si dispone di alcuna coppia di chiavi del certificato nella directory `~/.ssh` , è possibile crearle:

* Automaticamente, tramite hello `azure vm create --generate-ssh-keys` opzione.
* Manualmente, utilizzando [toocreate istruzioni hello li manualmente](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

In alternativa, è possibile utilizzare hello `--admin-password` metodo tooauthenticate le connessioni SSH dopo hello macchina virtuale viene creato. Di solito, questo metodo risulta essere meno sicuro.

Creiamo hello VM riportando tutti i risorse e informazioni insieme hello `azure vm create` comando:

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

Output:

```azurecli
info:    Executing command vm create
+ Looking up hello VM "myVM1"
info:    Verifying hello public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using hello VM Size "Standard_DS1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Looking up hello storage account mystorageaccount
+ Looking up hello availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up hello NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in hello NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    hello storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by hello parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

È possibile connettersi immediatamente tooyour VM utilizzando le chiavi SSH predefinito. Assicurarsi di specificare la porta appropriata hello poiché passaggio tramite bilanciamento del carico hello. (Per la prima macchina virtuale, è necessario impostare hello NAT regola tooforward porta 4222 tooour VM.)

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

Output:

```bash
hello authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

Vado avanti e creare la seconda macchina virtuale in hello allo stesso modo:

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

Ed è ora possibile usare hello `azure vm show myResourceGroup myVM1` comando tooexamine è stato creato. A questo punto le VM Ubuntu sono in esecuzione dietro al bilanciamento del carico in Azure a cui è possibile accedere solo con la coppia di chiavi SSH, dal momento che le password sono disabilitate. È possibile installare nginx o httpd, distribuire un'app web e visualizzare il traffico hello scorrono tooboth del servizio di bilanciamento carico di hello di macchine virtuali hello.

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

Output:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "TestVM1"
+ Looking up hello NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-hello-environment-as-a-template"></a>Esportazione hello ambiente come modello
Dopo aver creato questo ambiente, cosa accade se si desidera toocreate un ambiente di sviluppo aggiuntive con hello stessi parametri o un ambiente di produzione a esso corrispondente? Gestione risorse Usa i modelli JSON che definiscono tutti i parametri di hello per l'ambiente. È possibile creare interi ambienti facendo riferimento a questo modello JSON. È possibile [creare manualmente modelli JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o esportare un modello JSON hello di toocreate ambiente esistente per l'utente:

```azurecli
azure group export --name myResourceGroup
```

Questo comando Crea hello `myResourceGroup.json` file nella directory di lavoro corrente. Quando si crea un ambiente da questo modello, viene chiesto di tutti i nomi risorsa hello, inclusi i nomi di hello per le macchine virtuali, le interfacce di rete o bilanciamento del carico hello. È possibile popolare questi nomi nel file di modello aggiungendo hello `-p` o `--includeParameterDefaultValue` parametro toohello `azure group export` comando illustrata in precedenza. Modifica i nome di risorsa hello JSON modelli toospecify, o [creare un file parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) che specifica i nomi delle risorse hello.

toocreate un ambiente in base al modello:

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

Potrebbe essere necessario tooread [altre informazioni su come toodeploy dai modelli](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Informazioni su come utilizzare i file dei parametri hello tooincrementally aggiornamento ambienti e accedere ai modelli da un unico percorso di archiviazione.

## <a name="next-steps"></a>Passaggi successivi
Ora si è pronti toobegin utilizzo di più componenti di rete e le macchine virtuali. È possibile utilizzare questo toobuild ambiente di esempio dell'applicazione utilizzando i componenti di base hello introdotti in questa sezione.
