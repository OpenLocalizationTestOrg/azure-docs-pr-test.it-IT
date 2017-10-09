---
title: imposta una scala di macchina virtuale di Azure tooa aaaConvert | Documenti Microsoft
description: "Creare e distribuire un scalabilità della macchina virtuale Linux Azure impostato con hello CLI di Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a>Convertire un set di scalabilità tooa macchina virtuale di Azure esistente

Questa esercitazione viene illustrato come tooconvert toouse CLI di Azure 2.0 scalabilità della macchina virtuale una macchina virtuale tooa impostare. Verrà inoltre descritto come set di configurazione di hello tooautomate delle macchine virtuali hello in scala di hello. Per ulteriori informazioni su come tooinstall CLI di Azure 2.0, vedere [Introduzione a Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md). Per altre informazioni sui set di scalabilità, vedere [Set di scalabilità di macchine virtuali](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).

## <a name="step-1---deprovision-hello-vm"></a>Passaggio 1: eseguire il deprovisioning hello VM

Usare SSH tooconnect toohello macchina virtuale.

Hello deprovisioning VM utilizzando hello Azure VM agente toodelete file e i dati. Per una panoramica dettagliata sul deprovisioning, vedere [Come generalizzare e acquisire una macchina virtuale Linux](capture-image.md).

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a>Passaggio 2: acquisire un'immagine di hello VM

Per una panoramica dettagliata sull'acquisizione, vedere [Come generalizzare e acquisire una macchina virtuale Linux](capture-image.md).

Deallocare hello macchina virtuale con [az vm deallocare](/cli/azure/vm#deallocate):

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Generalizzare hello macchina virtuale con [generalizzare la macchina virtuale az](/cli/azure/vm#generalize):

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

Creare un'immagine dalla risorsa di macchina virtuale hello con [immagine az creare](/cli/azure/image#create):

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a>Passaggio 3: creare set di scalabilità hello

Ottenere hello **id** dell'immagine di hello.

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

Creare una macchina virtuale dalla risorsa di immagine con [az vm create](/cli/azure/vmss#create):

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

Questo comando associa anche un disco dati di 10 GB. Tenere presente che, a seconda di hello VM dimensioni definite (utilizzassimo **Standard_DS1_v2**), hello numero di dischi dati è diverso. Per ulteriori informazioni, esaminare hello [dimensioni delle macchine virtuali](sizes.md).

Una volta al termine di set di scalabilità di hello, connettersi tooit. Ottenere un elenco di indirizzi IP per le istanze di hello per SSH con [az vmss elenco--connessione-informazioni sull'istanza](/cli/azure/vmss#list-instance-connection-info):

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

Ora è possibile connettersi disco della macchina virtuale istanza tooinitialize hello dati toohello

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a>Passaggio 4: disco dati di inizializzazione hello

Durante la macchina virtuale connessa toohello, partizione disco hello con `fdisk`:

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

Scrittura di una partizione toohello con hello `mkfs` comando:

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Montare il disco nuovo hello in modo che siano accessibile nel sistema operativo hello:

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

disco Hello è ora possibile accede tramite hello datadrive puntoMontaggio, che può essere verificato con `ls /datadrive/`.

Terminare la sessione SSH hello.


## <a name="step-5---configure-firewall"></a>Passaggio 5: configurare il firewall

Punto di entrata breccia hello firewall toohello webserver ospitato dal set di scalabilità hello. Quando è stato creato il set di scalabilità di hello ed è stato creato anche un servizio di bilanciamento del carico è stato utilizzato **SSH** toohello singole macchine virtuali. tooopen una porta, è necessario che due tipi di informazioni, che è possibile ottenere mediante Azure CLI.

* **Pool di indirizzi IP front-end**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* **Pool di indirizzi IP back-end**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

Con questi due nomi, è possibile aprire la porta **80**.

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a>Passaggio 6: automatizzare la configurazione

disco dati Hello deve toobe configurato in ogni istanza di macchina virtuale. È possibile automatizzare la configurazione di hello della macchina virtuale hello con hello **CustomScript** estensione.

Creare innanzitutto un *sh* script che include comandi di formato di disco hello.

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

Successivamente, caricare tale hello toowhere file di script **CustomScript** estensione può accedervi. Una copia è disponibile [qui](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).

Creare un file locale denominato **Settings** e put hello in seguito il blocco JSON in essa contenuti. Hello `flieUris` proprietà deve essere impostata toowhere caricato il file di script.

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

Distribuire questo comando tooyour set di scalabilità con hello **CustomScript** estensione, che fanno riferimento a hello **Settings** file appena creato.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

Questa estensione viene eseguita automaticamente in tutte le istanze correnti e in tutte le istanze create successivamente tramite scalabilità.

## <a name="step-7---configure-autoscale-rules"></a>Passaggio 7: configurare le regole di scalabilità automatica

Attualmente non è possibile impostare le regole di scalabilità automatica nell'interfaccia della riga di comando di Azure. Hello utilizzare [portale di Azure](https://portal.azure.com) scalabilità automatica tooconfigure.

## <a name="step-8---management-tasks"></a>Passaggio 8: attività di gestione

Nel ciclo di vita hello del set di scalabilità di hello, potrebbe essere necessario toorun uno o più attività di gestione. Inoltre, è opportuno toocreate script che automatizzano le varie attività di ciclo di vita e hello CLI di Azure fornisce un toodo rapidamente le attività. Di seguito vengono illustrate alcune attività comuni.

### <a name="get-connection-info"></a>Ottenere informazioni sulla connessione

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a>Impostare il conteggio delle istanze (scalabilità manuale)

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a>Eliminare un gruppo di risorse

Se si elimina un gruppo di risorse, vengono eliminate anche tutte le risorse in esso contenute.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni su alcune delle scalabilità della macchina virtuale hello impostare funzionalità introdotte in questa esercitazione, vedere hello le seguenti informazioni:

- [Informazioni sui set di scalabilità di macchine virtuali in Azure](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [Panoramica di Azure Load Balancer](../../load-balancer/load-balancer-overview.md)
- [Controllare il flusso del traffico di rete con i gruppi di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md)