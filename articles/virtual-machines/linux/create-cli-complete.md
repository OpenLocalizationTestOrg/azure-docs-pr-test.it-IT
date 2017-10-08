---
title: un ambiente Linux con hello Azure CLI 2.0 aaaCreate | Documenti Microsoft
description: Creare archiviazione, una VM Linux, una rete virtuale e subnet, un bilanciamento del carico, una scheda di rete, un indirizzo IP pubblico e un gruppo di sicurezza di rete, tutti da hello messa a terra tramite hello CLI di Azure 2.0.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 7287ea178e76001b84dade628ead04a59dc27f40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-hello-azure-cli"></a>Creare una macchina virtuale di Linux completezza con hello CLI di Azure
tooquickly creare una macchina virtuale (VM) in Azure, è possibile utilizzare un singolo comando CLI di Azure che utilizza l'impostazione predefinita i valori toocreate qualsiasi necessarie risorse di supporto. Le risorse, ad esempio una rete virtuale, l'indirizzo IP pubblico e regole del gruppo di sicurezza di rete, vengono create automaticamente. Per un maggiore controllo dell'ambiente di produzione, utilizzare, è possibile creare queste risorse anticipo e quindi aggiungere toothem le macchine virtuali. In questo articolo descrive come toocreate una macchina virtuale e ogni hello risorse di supporto uno alla volta.

Assicurarsi di avere installato più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) e l'account connesso tooan Azure con [accesso az](/cli/azure/#login).

In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono *myResourceGroup*, *myVnet* e *myVM*.

## <a name="create-resource-group"></a>Creare un gruppo di risorse
Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite. Il gruppo di risorse deve essere creato prima della macchina virtuale e delle risorse della rete virtuale di supporto. Creare il gruppo di risorse hello con [gruppo az creare](/cli/azure/group#create). esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:

```azurecli
az group create --name myResourceGroup --location eastus
```

Per impostazione predefinita, l'output di hello di comandi CLI di Azure è in JSON (JavaScript Object Notation). toochange hello predefinito output tooa elenco o una tabella, ad esempio, utilizzare [az configurare - output](/cli/azure/#configure). È inoltre possibile aggiungere `--output` comando tooany per un periodo di una modifica in formato di output. Hello esempio seguente viene illustrato l'output JSON hello da hello `az group create` comando:

```json                       
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "location": "eastus",
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-a-virtual-network-and-subnet"></a>Creare una rete virtuale e una subnet
Successivamente si crea una rete virtuale in Azure e una subnet in toowhich è possibile creare le macchine virtuali. Utilizzare [creazione della rete virtuale di rete az](/cli/azure/network/vnet#create) toocreate una rete virtuale denominata *myVnet* con hello *192.168.0.0/16* prefisso dell'indirizzo. È inoltre aggiungere una subnet denominata *mySubnet* con prefisso di indirizzo hello *192.168.1.0/24*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

output di Hello Mostra subnet hello come punto di vista logico creato all'interno di rete virtuale hello:

```json
{
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "location": "eastus",
  "name": "myVnet",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "ed62fd03-e9de-430b-84df-8a3b87cacdbb",
  "subnets": [
    {
      "addressPrefix": "192.168.1.0/24",
      "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
      "ipConfigurations": null,
      "name": "mySubnet",
      "networkSecurityGroup": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  "tags": {},
  "type": "Microsoft.Network/virtualNetworks",
  "virtualNetworkPeerings": null
}
```


## <a name="create-a-public-ip-address"></a>Creare un indirizzo IP pubblico
Creare ora un indirizzo IP pubblico con [az network public-ip create](/cli/azure/network/public-ip#create). Questo indirizzo IP pubblico consente si tooconnect tooyour macchine virtuali da hello Internet. Poiché l'indirizzo predefinito hello è dinamica, è inoltre creare una voce DNS denominata con hello `--domain-name-label` opzione. esempio Hello crea un indirizzo IP pubblico denominato *myPublicIP* con nome DNS hello *mypublicdns*. Poiché il nome DNS hello deve essere univoco, fornire il proprio nome DNS univoco:

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

Output:

```json
{
  "publicIp": {
    "dnsSettings": {
      "domainNameLabel": "mypublicdns",
      "fqdn": "mypublicdns.eastus.cloudapp.azure.com",
      "reverseFqdn": null
    },
    "etag": "W/\"2632aa72-3d2d-4529-b38e-b622b4202925\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "idleTimeoutInMinutes": 4,
    "ipAddress": null,
    "ipConfiguration": null,
    "location": "eastus",
    "name": "myPublicIP",
    "provisioningState": "Succeeded",
    "publicIpAddressVersion": "IPv4",
    "publicIpAllocationMethod": "Dynamic",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "4c65de38-71f5-4684-be10-75e605b3e41f",
    "tags": null,
    "type": "Microsoft.Network/publicIPAddresses"
  }
}
```


## <a name="create-a-network-security-group"></a>Creare un gruppo di sicurezza di rete
flusso di hello toocontrol del traffico da e verso le macchine virtuali, creare un gruppo di sicurezza di rete. Un gruppo di sicurezza di rete può essere applicato tooa NIC o subnet. Hello seguente utilizza [rete az creare](/cli/azure/network/nsg#create) toocreate un gruppo di sicurezza di rete denominato *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

Si definiscono regole che consentono o negano il traffico specifico hello. tooallow le connessioni in ingresso sulla porta 22 (toosupport SSH), creare una regola in ingresso per il gruppo di sicurezza di rete hello con [creare una regola gruppo rete az](/cli/azure/network/nsg/rule#create). esempio Hello crea una regola denominata *myNetworkSecurityGroupRuleSSH*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 22 \
    --access allow
```

tooallow le connessioni in ingresso sulla porta 80 (il traffico web toosupport), aggiungere un'altra regola di gruppo di sicurezza di rete. esempio Hello crea una regola denominata *myNetworkSecurityGroupRuleHTTP*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleWeb \
    --protocol tcp \
    --priority 1001 \
    --destination-port-range 80 \
    --access allow
```

Esaminare il gruppo di sicurezza rete hello e le regole con [Mostra nsg di rete az](/cli/azure/network/nsg#show):

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

Output:

```json
{
  "defaultSecurityRules": [
    {
      "access": "Allow",
      "description": "Allow inbound traffic from all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetInBound",
      "name": "AllowVnetInBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow inbound traffic from azure load balancer",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowAzureLoadBalancerInBou
      "name": "AllowAzureLoadBalancerInBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "AzureLoadBalancer",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all inbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllInBound",
      "name": "DenyAllInBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs tooall VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetOutBound",
      "name": "AllowVnetOutBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs tooInternet",
      "destinationAddressPrefix": "Internet",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowInternetOutBound",
      "name": "AllowInternetOutBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all outbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllOutBound",
      "name": "DenyAllOutBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
  "location": "eastus",
  "name": "myNetworkSecurityGroup",
  "networkInterfaces": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "47a9964e-23a3-438a-a726-8d60ebbb1c3c",
  "securityRules": [
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "22",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleSSH",
      "name": "myNetworkSecurityGroupRuleSSH",
      "priority": 1000,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "80",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleWeb",
      "name": "myNetworkSecurityGroupRuleWeb",
      "priority": 1001,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "subnets": null,
  "tags": null,
  "type": "Microsoft.Network/networkSecurityGroups"
}
```

## <a name="create-a-virtual-nic"></a>Creare una scheda di rete virtuale
Schede di interfaccia di rete virtuale (NIC) disponibili a livello di codice in quanto è possibile applicare regole tootheir utilizzare. È inoltre possibile averne più di una. In seguito hello [az rete nic creare](/cli/azure/network/nic#create) comando, si crea una scheda di rete denominata *myNic* e associarlo a gruppo di sicurezza di rete hello. indirizzo IP pubblico Hello *myPublicIP* è inoltre associata a una scheda di rete virtuale. hello

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

Output:

```json
{
  "NewNIC": {
    "dnsSettings": {
      "appliedDnsServers": [],
      "dnsServers": [],
      "internalDnsNameLabel": null,
      "internalDomainNameSuffix": "brqlt10lvoxedgkeuomc4pm5tb.bx.internal.cloudapp.net",
      "internalFqdn": null
    },
    "enableAcceleratedNetworking": false,
    "enableIpForwarding": false,
    "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic",
    "ipConfigurations": [
      {
        "applicationGatewayBackendAddressPools": null,
        "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic/ipConfigurations/ipconfig1",
        "loadBalancerBackendAddressPools": null,
        "loadBalancerInboundNatRules": null,
        "name": "ipconfig1",
        "primary": true,
        "privateIpAddress": "192.168.1.4",
        "privateIpAddressVersion": "IPv4",
        "privateIpAllocationMethod": "Dynamic",
        "provisioningState": "Succeeded",
        "publicIpAddress": {
          "dnsSettings": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
          "idleTimeoutInMinutes": null,
          "ipAddress": null,
          "ipConfiguration": null,
          "location": null,
          "name": null,
          "provisioningState": null,
          "publicIpAddressVersion": null,
          "publicIpAllocationMethod": null,
          "resourceGroup": "myResourceGroup",
          "resourceGuid": null,
          "tags": null,
          "type": null
        },
        "resourceGroup": "myResourceGroup",
        "subnet": {
          "addressPrefix": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
          "ipConfigurations": null,
          "name": null,
          "networkSecurityGroup": null,
          "provisioningState": null,
          "resourceGroup": "myResourceGroup",
          "resourceNavigationLinks": null,
          "routeTable": null
        }
      }
    ],
    "location": "eastus",
    "macAddress": null,
    "name": "myNic",
    "networkSecurityGroup": {
      "defaultSecurityRules": null,
      "etag": null,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
      "location": null,
      "name": null,
      "networkInterfaces": null,
      "provisioningState": null,
      "resourceGroup": "myResourceGroup",
      "resourceGuid": null,
      "securityRules": null,
      "subnets": null,
      "tags": null,
      "type": null
    },
    "primary": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "b3dbaa0e-2cf2-43be-a814-5cc49fea3304",
    "tags": null,
    "type": "Microsoft.Network/networkInterfaces",
    "virtualMachine": null
  }
}
```


## <a name="create-an-availability-set"></a>Creare un set di disponibilità
I set di disponibilità agevolano la distribuzione delle macchine virtuali nei domini di errore e nei domini di aggiornamento. Anche se è solo creare una macchina virtuale al momento, si tratta di best practice toouse disponibilità set toomake è più facile tooexpand in hello future. 

I domini di errore definiscono un gruppo di macchine virtuali che condividono una fonte di alimentazione e uno switch di rete comuni. Per impostazione predefinita, hello le macchine virtuali configurate all'interno del set di disponibilità sono separate tra i domini di errore toothree. Un problema hardware in uno di questi domini di errore non influenza tutte le macchine virtuali che eseguono l'app.

Indicano i domini di aggiornamento gruppi di macchine virtuali e l'hardware fisico sottostante che può essere riavviata in hello contemporaneamente. Durante la manutenzione pianificata, ordine di hello in aggiornamento vengono riavviati domini potrebbe non essere sequenziale, ma riavvio del dominio di aggiornamento solo una alla volta.

Azure distribuisce automaticamente le macchine virtuali tra i domini di errore e l'aggiornamento di hello durante il posizionamento in un set di disponibilità. Per ulteriori informazioni, vedere [la gestione della disponibilità di hello di macchine virtuali](manage-availability.md).

Creare un set di disponibilità per la macchina virtuale con [az vm availability-set create](/cli/azure/vm/availability-set#create). esempio Hello crea un set denominato di disponibilità *myAvailabilitySet*:

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

Hello output note domini di errore e domini di aggiornamento:

```json
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet",
  "location": "eastus",
  "managed": null,
  "name": "myAvailabilitySet",
  "platformFaultDomainCount": 2,
  "platformUpdateDomainCount": 5,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": null,
    "managed": true,
    "tier": null
  },
  "statuses": null,
  "tags": {},
  "type": "Microsoft.Compute/availabilitySets",
  "virtualMachines": []
}
```


## <a name="create-hello-linux-vms"></a>Creare le macchine virtuali Linux hello
Si è creato toosupport risorse di rete hello macchine virtuali accessibile tramite Internet. A questo punto, creare una macchina virtuale e proteggerla con la chiave SSH. In questo caso, verrà toocreate una VM Ubuntu in base a hello LTS più recente. È possibile trovare immagini aggiuntive con [az vm image list](/cli/azure/vm/image#list), come descritto nell'articolo sulla [ricerca di immagini della macchina virtuale di Azure](cli-ps-findimage.md).

È inoltre possibile specificare un toouse chiave SSH per l'autenticazione. Se non si dispone di una coppia di chiavi pubblica SSH, è possibile [crearli](mac-create-ssh-keys.md) o utilizzare hello `--generate-ssh-keys` toocreate parametro usarle per l'utente. Se si dispone già di una coppia di chiavi, questo parametro usa le chiavi esistenti in `~/.ssh`.

Creare VM hello riportando tutti i risorse e informazioni insieme hello [creare vm az](/cli/azure/vm#create) comando. esempio Hello crea una macchina virtuale denominata *myVM*:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --availability-set myAvailabilitySet \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour VM con hello voce DNS specificato durante la creazione di indirizzo IP pubblico hello. Questo `fqdn` è illustrato nell'output di hello durante la creazione di una macchina virtuale:

```json
{
  "fqdns": "mypublicdns.eastus.cloudapp.azure.com",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-13-71-C8",
  "powerState": "VM running",
  "privateIpAddress": "192.168.1.5",
  "publicIpAddress": "13.90.94.252",
  "resourceGroup": "myResourceGroup"
}
```

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

Output:

```bash
hello authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

toorun a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

È possibile installare NGINX e vedere hello traffico flusso toohello macchina virtuale. Installare NGINX come indicato di seguito:

```bash
sudo apt-get install -y nginx
```

toosee sito NGINX predefinito di hello in azione, aprire il web browser e immettere il nome FQDN:

![Sito NGINX predefinito nella macchina virtuale](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a>Esportare come modello
È ora possibile toocreate un ambiente di sviluppo aggiuntive con hello stessi parametri o un ambiente di produzione a esso corrispondente? Gestione risorse Usa i modelli JSON che definiscono tutti i parametri di hello per l'ambiente. È possibile creare interi ambienti facendo riferimento a questo modello JSON. È possibile [creare manualmente modelli JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o esportare un modello JSON hello di toocreate ambiente esistente per l'utente. Utilizzare [esportazione gruppo az](/cli/azure/group#export) tooexport la risorsa gruppo come indicato di seguito:

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

Questo comando Crea hello `myResourceGroup.json` file nella directory di lavoro corrente. Quando si crea un ambiente da questo modello, viene chiesto di tutti i nomi di risorsa hello. È possibile popolare questi nomi nel file di modello aggiungendo hello `--include-parameter-default-value` parametro toohello `az group export` comando. Modifica i nome di risorsa hello JSON modelli toospecify, o [creare un file parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) che specifica i nomi delle risorse hello.

un ambiente nel modello di utilizzo toocreate [distribuzione gruppo az creare](/cli/azure/group/deployment#create) come indicato di seguito:

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

Potrebbe essere necessario tooread [altre informazioni su come toodeploy dai modelli](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Informazioni su come utilizzare i file dei parametri hello tooincrementally aggiornamento ambienti e accedere ai modelli da un unico percorso di archiviazione.

## <a name="next-steps"></a>Passaggi successivi
Ora si è pronti toobegin utilizzo di più componenti di rete e le macchine virtuali. È possibile utilizzare questo toobuild ambiente di esempio dell'applicazione utilizzando i componenti di base hello introdotti in questa sezione.
