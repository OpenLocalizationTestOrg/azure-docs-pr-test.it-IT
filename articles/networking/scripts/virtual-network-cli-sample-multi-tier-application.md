---
title: 'script CLI aaaAzure di esempio: creare una rete per applicazioni multilivello | Documenti Microsoft'
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una rete virtuale per applicazioni multilivello
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: deeb3f459499cebd1b8ded6a299eb759d49cf08d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a>Creare una rete per applicazioni multilivello

Questo script di esempio crea una rete virtuale con subnet front-end e back-end. Subnet con traffico toohello front-end è limitato tooHTTP e SSH, mentre il traffico toohello subnet back-end è limitato tooMySQL, porta 3306. Dopo l'esecuzione dello script hello, si avrà a disposizione due macchine virtuali, una in ogni subnet che è possibile distribuire server web e software MySQL.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a>Script di esempio


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello toocreate i comandi seguenti a un gruppo di risorse, rete virtuale e gruppi di sicurezza di rete. Ogni comando nella documentazione di hello tabella collegamenti toocommand specifica.

| Comando | Note |
|---|---|
| [az group create](/cli/azure/group#create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az network vnet create](/cli/azure/network/vnet#create) | Consente di creare una rete virtuale e una subnet front-end di Azure. |
| [az network subnet create](/cli/azure/network/vnet/subnet#create) | Consente di creare una subnet back-end. |
| [az network public-ip create](/cli/azure/network/public-ip#create) | Crea un hello VM tooaccess indirizzo pubblico di IP da Internet hello. |
| [az network nic create](/cli/azure/network/nic#create) | Consente di creare interfacce di rete virtuale e lo connette le subnet front-end e back-end della rete virtuale toohello. |
| [az network nsg create](/cli/azure/network/nsg#create) | Crea gruppi di sicurezza di rete (gruppo) che sono subnet front-end e back-end di toohello associato. |
| [az network nsg rule create](/cli/azure/network/nsg/rule#create) |Crea regole del gruppo che consentono o Blocca subnet toospecific porte specifiche. |
| [az vm create](/cli/azure/vm#create) | Crea le macchine virtuali e la collega tooeach una scheda di rete VM. Questo comando specifica inoltre toouse immagine di macchina virtuale hello e le credenziali amministrative. |
| [az group delete](/cli/azure/group#delete) | Consente di eliminare un gruppo di risorse e tutte le risorse in esso contenute. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](/cli/azure/overview).

Ulteriori esempi di script CLI rete sono reperibili hello [documentazione Cenni preliminari sulle reti di Azure](../cli-samples.md)
