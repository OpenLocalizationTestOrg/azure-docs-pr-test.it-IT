---
title: aaaCreate una VM Linux di Azure da un modello | Documenti Microsoft
description: Come toouse hello Azure CLI 2.0 toocreate una VM Linux da un modello di gestione risorse
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a>Come toocreate una macchina virtuale Linux con modelli di gestione risorse di Azure
Questo articolo illustra come tooquickly distribuire una macchina virtuale Linux (VM) con i modelli di gestione risorse di Azure e hello CLI di Azure 2.0. È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](create-ssh-secured-vm-from-template-nodejs.md).


## <a name="templates-overview"></a>Panoramica dei modelli
Modelli di gestione risorse di Azure sono i file JSON che definiscono l'infrastruttura di hello e configurazione della soluzione Azure. Usando il modello è possibile distribuire ripetutamente la soluzione nel corso del ciclo di vita garantendo al contempo che le risorse vengano distribuite in uno stato coerente. toolearn ulteriori informazioni sui formati di hello del modello hello e come creare l'oggetto, vedere [creare il primo modello di gestione risorse di Azure](../../azure-resource-manager/resource-manager-create-first-template.md). hello tooview sintassi JSON per i tipi di risorse, vedere [definire le risorse nei modelli di Azure Resource Manager](/azure/templates/).


## <a name="create-resource-group"></a>Creare un gruppo di risorse
Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite. Il gruppo di risorse deve essere creato prima della macchina virtuale. esempio Hello crea un gruppo di risorse denominato *myResourceGroupVM* in hello *eastus* area:

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Crea macchina virtuale
esempio Hello crea una macchina virtuale da [questo modello di gestione risorse di Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) con [distribuzione gruppo az creare](/cli/azure/group/deployment#create). Fornire la propria chiave pubblica SSH, ad esempio contenuto hello del valore hello *~/.ssh/id_rsa.pub*. Se è necessario toocreate una coppia di chiavi SSH, vedere [come toocreate e utilizzare un SSH coppia di chiavi per le macchine virtuali Linux in Azure](mac-create-ssh-keys.md).

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

In questo esempio è stato specificato un modello archiviato in GitHub. È anche possibile scaricare o creare un modello e specificare un percorso locale della hello con hello stesso `--template-file` parametro.

tooSSH tooyour macchina virtuale, ottenere l'indirizzo IP pubblico hello con [Mostra public-ip di rete az](/cli/azure/network/public-ip#show):

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

È quindi possibile SSH tooyour VM come di consueto:

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a>Passaggi successivi
In questo esempio è stata creata una VM Linux di base. Per ulteriori modelli di gestione risorse per l'inclusione di Framework applicazioni o creare ambienti più complessi, visitare hello [raccolta di modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/).
