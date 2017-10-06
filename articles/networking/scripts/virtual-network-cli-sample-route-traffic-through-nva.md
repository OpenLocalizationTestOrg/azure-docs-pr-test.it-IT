---
title: esempio di script CLI aaaAzure - instradare il traffico attraverso un dispositivo di rete virtuale | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Instradare il traffico attraverso un'appliance virtuale di rete.
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
ms.openlocfilehash: 981d6073be04a7ebaf96b657fbab8a378e7a995e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a>Instradare il traffico attraverso un'appliance virtuale di rete

Questo script di esempio crea una rete virtuale con subnet front-end e back-end. Viene inoltre creata una macchina virtuale con IP inoltro del traffico tra due subnet hello tooroute abilitato. Dopo l'esecuzione di script hello è possibile distribuire il software di rete, ad esempio un'applicazione di firewall, toohello macchina virtuale.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a>Script di esempio


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]

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
| [az network subnet create](/cli/azure/network/vnet/subnet#create) | Consente di creare le subnet back-end e di rete perimetrale. |
| [az network public-ip create](/cli/azure/network/public-ip#create) | Crea un hello VM tooaccess indirizzo pubblico di IP da Internet hello. |
| [az network nic create](/cli/azure/network/nic#create) | Consente di creare un'interfaccia di rete virtuale e attiva l'inoltro IP. |
| [az network nsg create](/cli/azure/network/nsg#create) | Consente di creare un gruppo di sicurezza di rete. |
| [az network nsg rule create](/cli/azure/network/nsg/rule#create) | Crea regole del gruppo che consentono le porte HTTP e HTTPS in ingresso toohello macchina virtuale. |
| [az network vnet subnet update](/cli/azure/network/vnet/subnet#update)| Associa hello NSGs e toosubnets nelle tabelle di route. |
| [az network route-table create](/cli/azure/network/route-table#create)| Consente di creare una tabella di route per tutte le route. |
| [az network route-table route create](/cli/azure/network/route-table/route#create)| Crea route tooroute il traffico tra subnet e hello Internet tramite hello macchina virtuale. |
| [az vm create](/cli/azure/vm#create) | Crea una macchina virtuale e collega tooit NIC hello. Questo comando specifica inoltre toouse immagine di macchina virtuale hello e le credenziali amministrative. |
| [az group delete](/cli/azure/group#delete) | Consente di eliminare un gruppo di risorse e tutte le risorse in esso contenute. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](/cli/azure/overview).

Ulteriori esempi di script CLI rete sono reperibili hello [documentazione Cenni preliminari sulle reti di Azure](../cli-samples.md)
