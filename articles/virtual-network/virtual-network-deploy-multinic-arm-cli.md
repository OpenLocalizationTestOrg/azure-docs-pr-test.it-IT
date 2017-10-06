---
title: "una macchina virtuale con più schede di rete - CLI di Azure 2.0 aaaCreate | Documenti Microsoft"
description: "Informazioni su come una macchina virtuale con più schede di rete utilizzando toocreate hello CLI di Azure 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac0291a978e2c8682c69104915196cc6c4fcf8dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-20"></a>Creare una macchina virtuale con più schede di rete utilizzando hello Azure CLI 2.0

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).  In questo articolo viene illustrato l'utilizzo modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché hello [modello di distribuzione classica](virtual-network-deploy-multinic-classic-cli.md).
>

## <a name="create"></a>Creare VM hello

È possibile completare questa attività usando hello Azure CLI 2.0 (in questo articolo) o hello [CLI di Azure 1.0](virtual-network-deploy-multinic-cli-nodejs.md). valori Hello "" per le variabili di hello nei passaggi hello che seguono creano risorse con le impostazioni da uno scenario di hello. Modificare i valori hello, come appropriato, per l'ambiente.

1. Installare hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) se non ne è già installata.
2. Creare una coppia chiave SSH pubblica e privata per le macchine virtuali Linux completando i passaggi hello hello [creare una coppia chiave SSH pubblica e privata per le macchine virtuali Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. Da una shell dei comandi, accedere con il comando hello `az login`.
4. Creare VM hello eseguendo script hello che segue in un computer Linux o Mac. script di Hello crea un gruppo di risorse, una rete virtuale (VNet) con due subnet, due schede di rete e una macchina virtuale con hello due schede di rete associata tooit. Una delle schede di rete hello subnet tooone connesso e viene assegnata un indirizzo IP pubblico e privato. Hello altro NIC è connessa toohello altre subnet e viene assegnato un indirizzo IP privato statico e alcun indirizzo IP pubblico. Hello scheda di rete, indirizzo IP pubblico, rete virtuale e risorse macchina virtuale devono esistere in hello stesso percorso e sottoscrizione. Anche se le risorse di hello non hanno tooexist in hello stesso gruppo di risorse, in hello avviene script seguente.

```bash
#!/bin/sh

RgName="Multi-NIC-VM"
Location="westus"

# Create a resource group.
az group create \
--name $RgName \
--location $Location

# hello address is assigned toohello resource from a pool of IP adresses unique tooeach Azure region. 
# Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists
# hello ranges for each region.

PipName="PIP-WEB"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static

# Create a virtual network with one subnet

VnetName="VNet1"
VnetPrefix="10.0.0.0/16"
VnetSubnet1Name="Front-End"
VnetSubnet1Prefix="10.0.0.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnet1Name \
--subnet-prefix $VnetSubnet1Prefix

# Create a second subnet within hello VNet

VnetSubnet2Name="Back-end"
VnetSubnet2Prefix="10.0.1.0/24"
az network vnet subnet create \
--vnet-name $VnetName \
--resource-group $RgName \
--name $VnetSubnet2Name \
--address-prefix $VnetSubnet2Prefix

# Create a network interface connected tooone of hello subnets. hello NIC is assigned a single dynamic private and
# public IP address by default, but you can instead, assign static addresses, or no public IP address at all.
# You can also assign multiple private or public IP addresses tooeach NIC. toolearn more about IP addressing
# options for NICs, enter hello az network nic create -h command.

Nic1Name="NIC-FE"
PrivateIpAddress1="10.0.0.5"

az network nic create \
--name $Nic1Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress1 \
--public-ip-address $PipName

# Create a second network interface and connect it toohello other subnet. Though multiple NICs attached toohello same
# VM can be connected toodifferent subnets, hello subnets must all be within hello same VNet. Add additional NICs as necessary.

Nic2Name="NIC-BE"
PrivateIpAddress2="10.0.1.5"

az network nic create \
--name $Nic2Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet2Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress2

# Create a VM and attach hello two NICs.

VmName="WEB"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article. Not all VM sizes support
# more than one NIC, so be sure tooselect a VM size that supports hello number of NICs you want tooattach toohello VM.
# You must create hello VM with at least two NICs if you want tooadd more after VM creation. If you create a VM with
# only one NIC, you can't add additional NICs toohello VM after VM creation, regardless of how many NICs hello VM supports.
# hello VM size specified in hello following variable supports two NICs.

VmSize="Standard_DS2"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello output returned by entering the
# az vm image list command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file.

SshKeyValue="~/.ssh/id_rsa.pub"

# Before executing hello following command, add variable names of additional NICs you may have added toohello script that
# you want tooattach toohello VM. If creating a Windows VM, remove hello **ssh-key-value** line and you'll be prompted for
# hello password you want tooconfigure for hello VM.

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $Nic1Name $Nic2Name \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

Inoltre toocreating una macchina virtuale con due schede di rete, consente di creare script hello:
- Un unico premio gestito disco per impostazione predefinita, ma sono disponibili altre opzioni per il tipo di disco hello che è possibile creare. Hello lettura [creare una VM Linux di Azure 2.0 CLI hello](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo per informazioni dettagliate.
- Una rete virtuale con due subnet e un singolo indirizzo IP pubblico. In alternativa, è possibile usare le risorse *esistenti* di rete virtuale, subnet, scheda di interfaccia di rete o indirizzo IP pubblico. toolearn come toouse esistente alle risorse di rete anziché la creazione di altre risorse, immettere `az vm create -h`.

## <a name = "validate"></a>Convalidare la creazione di VM e le schede di interfacce di rete

1. Immettere il comando hello `az resource list --resouce-group Multi-NIC-VM --output table` toosee un elenco di risorse hello creato dallo script hello. Deve essere presente sei risorse nell'output restituito hello: due schede di rete, un disco, un indirizzo IP pubblico, una rete virtuale e una macchina virtuale.
2. Immettere il comando hello `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`. In hello restituito l'output, annotare il valore di hello del **IpAddress** e tale valore hello **PublicIpAllocationMethod** è *statico*.
3. Prima di eseguire hello comando seguente, rimuovere <> hello, sostituire *Username* con nome hello utilizzato per hello **Username** variabile script hello e sostituire *ipAddress* con hello **ipAddress** dal passaggio precedente hello. Comando che segue hello esecuzione tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`. 
4. Una volta connessi toohello macchina virtuale, eseguire hello `sudo ifconfig` comando toosee *eth0* e *scheda eth1* interfacce. Ogni scheda di rete è stata assegnata hello privati indirizzi IP statici specificati nello script hello dai server DHCP di Azure hello. Hello indirizzi IP e MAC assegnati toohello NIC non cambiano finché hello che macchina virtuale è stata eliminata. È consigliabile non modificare gli indirizzi IP all'interno di un sistema operativo, come è possibile disabilitare computer toohello di connettività. Gli indirizzi IP pubblici non sono presenti nel sistema operativo hello, come se fossero tooand convertita indirizzo di rete dall'indirizzo IP privato hello da hello dell'infrastruttura di Azure.

## <a name= "clean-up"></a>Rimuovere hello macchina virtuale e le risorse associate

Si consiglia di eliminare le risorse di hello create in questo esercizio, se non vengono usati nell'ambiente di produzione. Le risorse di VM, indirizzo IP pubblico e disco comportano spese finché si esegue il provisioning. risorse di hello tooremove create durante questo esercizio, hello completo alla procedura seguente:
1. risorse di hello tooview nel gruppo di risorse hello, eseguire hello `az resource list --resource-group Multi-NIC-VM` comando.
2. Verificare che non sono presenti risorse nel gruppo di risorse hello, diverso da risorse hello create dallo script hello in questo articolo. 
3. tutte le risorse create in questo esercizio, eseguire hello toodelete `az group delete --name Multi-NIC-VM` comando. comando Hello Elimina gruppo di risorse hello e tutte le risorse di hello che contiene.

## <a name="next-steps"></a>Passaggi successivi

Traffico di rete può propagare tooand da hello che macchina virtuale creata in questo articolo. È possibile definire regole in entrata e in uscita all'interno di un gruppo che consentono di limitare il traffico di hello che possano essere scambiate tooand da ogni interfaccia di rete, ogni subnet o entrambi. ulteriori informazioni sulla NSGs, leggere hello toolearn [Panoramica gruppo](virtual-networks-nsg.md) articolo.
