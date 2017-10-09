---
title: "aaaVM con più indirizzi IP mediante Azure CLI 2.0 hello | Documenti Microsoft"
description: "Informazioni su come tooassign più gli indirizzi IP tooa macchina virtuale utilizzando hello Azure CLI 2.0 | Gestore delle risorse."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 15efd853cc7c31bacb64ed052dabedd3fe4d3079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-cli-20"></a>Assegnare più indirizzi IP macchine toovirtual utilizzando hello Azure CLI 2.0

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

In questo articolo viene illustrato come una macchina virtuale (VM) tramite il modello di distribuzione Azure Resource Manager hello utilizzando toocreate hello CLI di Azure 2.0. Impossibile assegnare più indirizzi IP tooresources creato tramite il modello di distribuzione classica hello. ulteriori informazioni sui modelli di distribuzione di Azure, leggere hello toolearn [comprendere i modelli di distribuzione](../resource-manager-deployment-model.md) articolo.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Creare una macchina virtuale con più indirizzi IP

È possibile completare questa attività usando hello Azure CLI 2.0 (in questo articolo) o hello [CLI di Azure 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md). Modificare i valori hello, come appropriato, per l'ambiente. passaggi di Hello che seguono viene illustrato come toocreate un esempio di macchina virtuale con più IP risolve, come descritto nello scenario di hello. Modificare i valori delle variabili e i tipi di indirizzi IP come richiesto per l'implementazione. 

1. Installare hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) se non ne è già installata.
2. Creare una coppia chiave SSH pubblica e privata per le macchine virtuali Linux completando i passaggi hello hello [creare una coppia chiave SSH pubblica e privata per le macchine virtuali Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. Da una shell dei comandi, accedere con il comando hello `az login` selezionare hello sottoscrizione in uso.
4. Creare VM hello eseguendo script hello che segue in un computer Linux o Mac. script Hello crea un gruppo di risorse, una rete virtuale (VNet), una scheda di rete con tre configurazioni IP e una macchina virtuale con tooit di hello due schede di rete associate. Hello scheda di rete, indirizzo IP pubblico, rete virtuale e risorse macchina virtuale devono esistere in hello stesso percorso e sottoscrizione. Anche se le risorse di hello non hanno tooexist in hello stesso gruppo di risorse, in hello avviene script seguente.

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using hello `--allocation-method Static` option. If you
# do not specify this option, hello address is allocated dynamically. hello address is assigned toohello resource from a pool
# of IP adresses unique tooeach Azure region. Download and view hello file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists hello ranges for each region.

PipName="myPublicIP"

# This name must be unique within an Azure location.
DnsName="myDNSName"

az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--dns-name $DnsName\
--allocation-method Static

# Create a virtual network with one subnet

VnetName="myVnet"
VnetPrefix="10.0.0.0/16"
VnetSubnetName="mySubnet"
VnetSubnetPrefix="10.0.0.0/24"

az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnetName \
--subnet-prefix $VnetSubnetPrefix

# Create a network interface connected toohello subnet and associate hello public IP address tooit. Azure will create the
# first IP configuration with a static private IP address and will associate hello public IP address resource tooit.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it toohello NIC. This configuration has a
# static public IP address and a static private IP address.

az network public-ip create \
--resource-group $RgName \
--location $Location \
--name myPublicIP2 \
--dns-name mypublicdns2 \
--allocation-method Static

az network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--name IPConfig-2 \
--private-ip-address 10.0.0.5 \
--public-ip-name myPublicIP2

# Create a third IP configuration, and associate it toohello NIC. This configuration has  static private IP address and # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations
# tooany NIC in a VM. toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach hello NIC.

VmName="myVm"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. hello script fails if hello VM size
# is not supported in hello location you select. Run hello `azure vm sizes --location estcentralus` command tooget a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file. If you're creating a Windows VM, remove hello following
# line and you'll be prompted for hello password you want tooconfigure for hello VM.

SshKeyValue="~/.ssh/id_rsa.pub"

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $NicName \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

Una macchina virtuale con una scheda NIC con 3 configurazioni IP toocreating, script hello crea inoltre:

- Un unico premio gestito disco per impostazione predefinita, ma sono disponibili altre opzioni per il tipo di disco hello che è possibile creare. Hello lettura [creare una VM Linux di Azure 2.0 CLI hello](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo per informazioni dettagliate.
- Una rete virtuale con una subnet e due indirizzi IP pubblici. In alternativa, è possibile usare le risorse *esistenti* di rete virtuale, subnet, scheda di interfaccia di rete o indirizzo IP pubblico. toolearn come toouse esistente alle risorse di rete anziché la creazione di altre risorse, immettere `az vm create -h`.

Per gli indirizzi IP pubblici è prevista una tariffa nominale. ulteriori informazioni su IP indirizzo sui prezzi, toolearn leggere hello [dei prezzi di indirizzo IP](https://azure.microsoft.com/pricing/details/ip-addresses) pagina. È un toohello limita il numero di indirizzi IP pubblici che può essere usato in una sottoscrizione. informazioni sui limiti di hello, leggere hello toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo.

Dopo la creazione di VM hello immettere hello `az network nic show --name MyNic1 --resource-group myResourceGroup` configurazione NIC hello tooview del comando. Immettere hello `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview un elenco di configurazioni IP hello associata toohello scheda di rete.

Toohello macchina virtuale del sistema operativo di indirizzi IP privati di Aggiungi hello completando i passaggi di hello del sistema operativo in hello [aggiungere indirizzi del sistema operativo VM tooa](#os-config) sezione di questo articolo.

## <a name="add"></a>Aggiungere tooa di indirizzi IP VM

È possibile aggiungere ulteriori pubbliche e private IP indirizzi tooan esistente NIC completando i passaggi di hello che seguono. esempi di Hello si basano su hello [scenario](#Scenario) descritto in questo articolo.

1. Aprire una shell dei comandi e completa hello rimanenti passaggi in questa sezione all'interno di una singola sessione. Se si dispone già di Azure CLI installato e configurato, hello completato i passaggi in hello [CLI di Azure 2.0 installazione](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) tooyour articolo e account di accesso account Azure con hello `az-login` comando.

2. Completare i passaggi di hello in uno di hello le sezioni, in base ai requisiti seguenti:

    **Aggiungere un indirizzo IP privato**
    
    tooadd un tooa di indirizzo IP privato NIC, è necessario creare una configurazione IP hello comando che segue. indirizzo IP statico Hello deve essere un indirizzo per subnet hello inutilizzato.

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    Creare tutte le configurazioni usando nomi di configurazione univoci e indirizzi IP privati (per le configurazioni con indirizzi IP statici).

    **Aggiungere un indirizzo IP pubblico**
    
    Viene aggiunto un indirizzo IP pubblico associandolo tooeither una nuova configurazione IP o una configurazione IP esistente. Completare i passaggi di hello nelle sezioni che seguono, hello necessari.

    Per gli indirizzi IP pubblici è prevista una tariffa nominale. ulteriori informazioni su IP indirizzo sui prezzi, toolearn leggere hello [dei prezzi di indirizzo IP](https://azure.microsoft.com/pricing/details/ip-addresses) pagina. È un toohello limita il numero di indirizzi IP pubblici che può essere usato in una sottoscrizione. informazioni sui limiti di hello, leggere hello toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo.

    - **Associare hello risorsa tooa nuova configurazione IP**
    
        Ogni volta che si aggiunge un indirizzo IP pubblico a una nuova configurazione IP, è necessario aggiungere anche un indirizzo IP privato, perché tutte le configurazioni IP devono avere un indirizzo IP privato. È possibile aggiungere una risorsa indirizzo IP pubblico esistente o crearne una nuova. toocreate uno nuovo, immettere hello comando seguente:
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        una nuova configurazione IP con un indirizzo IP privato statico e hello associata toocreate *myPublicIP3* indirizzo IP pubblico risorsa degli indirizzi, immettere hello comando seguente:

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - **Configurazione IP esistente di hello associare risorse tooan** una risorsa di indirizzo IP pubblica può essere solo la configurazione IP tooan associato che non ha ancora associata. È possibile determinare se una configurazione IP è un indirizzo IP pubblico associato immettendo hello comando seguente:

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        Output restituito:
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        Poiché hello **PublicIpAddressId** colonna per *IpConfig 3* è vuoto in hello output, alcuna risorsa di indirizzo IP pubblica non è tooit attualmente associato. È possibile aggiungere un esistente pubblica IP indirizzo risorsa tooIpConfig-3 o immettere hello toocreate comando uno di seguito:

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        Immettere hello comando risorsa toohello configurazione IP esistente denominato di indirizzo IP pubblico di tooassociate hello seguente *IPConfig 3*:
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. Gli indirizzi IP privati di visualizzazione hello e hello pubblica di indirizzi IP assegnati toohello NIC immettendo hello comando seguente ID di risorsa:

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    Output restituito: <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. Aggiungere indirizzi IP privati hello è stato aggiunto il sistema operativo VM di toohello NIC toohello seguendo le istruzioni hello hello [aggiungere indirizzi del sistema operativo VM tooa](#os-config) sezione di questo articolo. Non aggiungere hello pubblica IP indirizzi toohello del sistema operativo.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
