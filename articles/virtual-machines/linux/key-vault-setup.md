---
title: aaaSet di insieme di credenziali chiave di Azure per le macchine virtuali Linux | Documenti Microsoft
description: Come tooset di insieme di credenziali chiave per l'utilizzo con una macchina virtuale di gestione risorse di Azure con hello CLI 2.0.
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: a5dc1fbe59a71b4456ba5b9bbacdb90440064757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-key-vault-for-virtual-machines-with-hello-azure-cli-20"></a>Come tooset di insieme di credenziali chiave per le macchine virtuali con hello Azure CLI 2.0

Nello stack di gestione risorse di Azure hello, segreti/certificati vengono modellati come risorse fornite dall'insieme di credenziali chiave. toolearn ulteriori informazioni sull'insieme di credenziali chiave di Azure, vedere [che cos'è l'insieme di credenziali chiave di Azure?](../../key-vault/key-vault-whatis.md) Affinché toobe insieme di credenziali chiave utilizzato con le macchine virtuali di Azure Resource Manager, hello *EnabledForDeployment* in insieme di credenziali chiave deve essere impostata tootrue. Questo articolo illustra come tooset di insieme di credenziali chiave per l'utilizzo con macchine virtuali di Azure (VM) utilizzando hello CLI di Azure 2.0. È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

tooperform questi passaggi, è necessario hello più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).

## <a name="create-a-key-vault"></a>Creare un insieme di credenziali delle chiavi
Creare un insieme di credenziali chiave e assegnare criteri di distribuzione hello con [keyvault az creare](/cli/azure/keyvault#create). esempio Hello crea un insieme di credenziali chiave denominata `myKeyVault` in hello `myResourceGroup` gruppo di risorse:

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a>Aggiornare un insieme di credenziali delle chiavi per l'uso con le macchine virtuali
Impostare i criteri di distribuzione hello in un insieme di credenziali chiave esistente con [aggiornamento keyvault az](/cli/azure/keyvault#update). gli aggiornamenti seguenti Hello hello chiave dell'insieme di credenziali denominato `myKeyVault` in hello `myResourceGroup` gruppo di risorse:

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-tooset-up-key-vault"></a>Utilizzare tooset di modelli di insieme di credenziali chiave
Quando si utilizza un modello, è necessario hello tooset `enabledForDeployment` proprietà troppo`true` per la risorsa di hello insieme di credenziali chiave come indicato di seguito:

```json
{
    "type": "Microsoft.KeyVault/vaults",
    "name": "ContosoKeyVault",
    "apiVersion": "2015-06-01",
    "location": "<location-of-key-vault>",
    "properties": {
    "enabledForDeployment": "true",
    ....
    ....
    }
}
```

## <a name="next-steps"></a>Passaggi successivi
Per altre opzioni che è possibile configurare quando si crea un insieme di credenziali delle chiavi usando i modelli vedere [Crea un insieme di credenziali delle chiavi](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).
