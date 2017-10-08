---
title: una macchina virtuale con un indirizzo IP pubblico statico - CLI di Azure 2.0 aaaCreate | Documenti Microsoft
description: Informazioni su come una macchina virtuale con un indirizzo pubblico IP statico usando toocreate hello Azure interfaccia della riga di comando (CLI) 2.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486060463486462dd8336734a7ad23c4a2cba452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-cli-20"></a>Creare una macchina virtuale con un indirizzo IP pubblico statico utilizzando hello Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Portale di Azure](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Interfaccia della riga di comando di Azure 2.0](virtual-network-deploy-static-pip-arm-cli.md)
> * [Interfaccia della riga di comando di Azure 1.0](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [Modello](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (Classic)](virtual-networks-reserved-public-ip.md) (PowerShell (classico))

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). In questo articolo viene illustrato l'utilizzo di modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché il modello di distribuzione classica hello.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name = "create"></a>Creare VM hello

È possibile completare questa attività usando hello Azure CLI 2.0 (in questo articolo) o hello [CLI di Azure 1.0](virtual-network-deploy-static-pip-cli-nodejs.md). valori Hello "" per le variabili di hello nei passaggi hello che seguono creano risorse con le impostazioni da uno scenario di hello. Modificare i valori hello, come appropriato, per l'ambiente.

1. Installare hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) se non ne è già installata.
2. Creare una coppia chiave SSH pubblica e privata per le macchine virtuali Linux completando i passaggi hello hello [creare una coppia chiave SSH pubblica e privata per le macchine virtuali Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. Da una shell dei comandi, accedere con il comando hello `az login`.
4. Creare VM hello eseguendo script hello che segue in un computer Linux o Mac. Hello Azure indirizzo IP pubblico, rete virtuale, l'interfaccia di rete e risorse macchina virtuale devono esistere in hello stesso percorso. Anche se le risorse di hello non hanno tooexist in hello stesso gruppo di risorse, in hello avviene script seguente.

```bash
RgName="IaaSStory"
Location="westus"

# Create a resource group.

az group create \
--name $RgName \
--location $Location

# Create a public IP address resource with a static IP address using hello --allocation-method Static option.
# If you do not specify this option, hello address is allocated dynamically. hello address is assigned toothe
# resource from a pool of IP adresses unique tooeach Azure region. hello DnsName must be unique within the
# Azure location it's created in. Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653#
# that lists hello ranges for each region.

PipName="PIPWEB1"
DnsName="iaasstoryws1"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static \
--dns-name $DnsName

# Create a virtual network with one subnet

VnetName="TestVNet"
VnetPrefix="192.168.0.0/16"
SubnetName="FrontEnd"
SubnetPrefix="192.168.1.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $SubnetName \
--subnet-prefix $SubnetPrefix

# Create a network interface connected toohello VNet with a static private IP address and associate hello public IP address
# resource toohello NIC.

NicName="NICWEB1"
PrivateIpAddress="192.168.1.101"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $SubnetName \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress \
--public-ip-address $PipName

# Create a new VM with hello NIC

VmName="WEB1"

# Replace hello value for hello VmSize variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article.
VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable with a value for *urn* from hello output returned by entering
# hello `az vm image list` command. 

OsImage="credativ:Debian:8:latest"
Username='adminuser'

# Replace hello following value with hello path tooyour public key file.
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
# If creating a Windows VM, remove hello previous line and you'll be prompted for hello password you want tooconfigure for hello VM.
```

Inoltre toocreating una macchina virtuale, lo script hello crea:
- Un unico premio gestito disco per impostazione predefinita, ma sono disponibili altre opzioni per il tipo di disco hello che è possibile creare. Hello lettura [creare una VM Linux di Azure 2.0 CLI hello](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo per informazioni dettagliate.
- Risorse di rete virtuale, subnet, scheda di interfaccia di rete e indirizzo IP pubblico. In alternativa, è possibile usare le risorse *esistenti* di rete virtuale, subnet, scheda di interfaccia di rete o indirizzo IP pubblico. toolearn come toouse esistente alle risorse di rete anziché la creazione di altre risorse, immettere `az vm create -h`.

## <a name = "validate"></a>Convalidare la creazione della VM e l'indirizzo IP pubblico

1. Immettere il comando hello `az resource list --resouce-group IaaSStory --output table` toosee un elenco di risorse hello creato dallo script hello. Deve essere presente cinque risorse nell'output restituito hello: una macchina virtuale, rete virtuale, indirizzo IP pubblico, disco e interfaccia di rete.
2. Immettere il comando hello `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`. In hello restituito l'output, annotare il valore di hello del **IpAddress** e tale valore hello **PublicIpAllocationMethod** è *statico*.
3. Prima di eseguire hello comando seguente, rimuovere <> hello, sostituire *Username* con nome hello utilizzato per hello **Username** variabile script hello e sostituire *ipAddress* con hello **ipAddress** dal passaggio precedente hello. Comando che segue hello esecuzione tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`. 

## <a name= "clean-up"></a>Rimuovere hello macchina virtuale e le risorse associate

Si consiglia di eliminare le risorse di hello create in questo esercizio, se non vengono usati nell'ambiente di produzione. Le risorse di VM, indirizzo IP pubblico e disco comportano spese finché si esegue il provisioning. risorse di hello tooremove create durante questo esercizio, hello completo alla procedura seguente:

1. risorse di hello tooview nel gruppo di risorse hello, eseguire hello `az resource list --resource-group IaaSStory` comando.
2. Verificare che non sono presenti risorse nel gruppo di risorse hello, diverso da risorse hello create dallo script hello in questo articolo. 
3. tutte le risorse create in questo esercizio, eseguire hello toodelete `az group delete -n IaaSStory` comando. comando Hello Elimina gruppo di risorse hello e tutte le risorse di hello che contiene.

## <a name="next-steps"></a>Passaggi successivi

Traffico di rete può propagare tooand da hello che macchina virtuale creata in questo articolo. È possibile definire regole in entrata e in uscita all'interno di un gruppo che consentono di limitare il traffico di hello che possano essere scambiate tooand dall'interfaccia di rete hello, hello subnet o entrambi. ulteriori informazioni sulla NSGs, leggere hello toolearn [Panoramica gruppo](virtual-networks-nsg.md) articolo.
