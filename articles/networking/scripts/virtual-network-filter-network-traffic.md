---
title: esempio di script CLI aaaAzure - il traffico di rete VM filtro | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Filtrare il traffico di rete della VM in ingresso e in uscita.
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
ms.openlocfilehash: c2f14e54bc96c99420b4300d1c24a457ac8c948c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a>Filtrare il traffico della VM in ingresso e in uscita

Questo script di esempio crea una rete virtuale con subnet front-end e back-end. Il traffico di rete in ingresso subnet front-end toohello è limitato tooHTTP, toohello Internet dalla subnet di back-end hello non è consentito il traffico HTTPS e SSH, mentre in uscita. Dopo l'esecuzione di script hello, si disporrà di una macchina virtuale con due schede di rete. Ogni scheda è connessa tooa diverse subnet.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]

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
| [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) | Associa NSGs toosubnets. |
| [az network public-ip create](/cli/azure/network/public-ip#create) | Crea un hello VM tooaccess indirizzo pubblico di IP da Internet hello. |
| [az network nic create](/cli/azure/network/nic#create) | Consente di creare interfacce di rete virtuale e lo connette le subnet front-end e back-end della rete virtuale toohello. |
| [az network nsg create](/cli/azure/network/nsg#create) | Crea gruppi di sicurezza di rete (gruppo) che sono subnet front-end e back-end di toohello associato. |
| [az network nsg rule create](/cli/azure/network/nsg/rule#create) |Crea regole del gruppo che consentono o Blocca subnet toospecific porte specifiche. |
| [az vm create](/cli/azure/vm#create) | Crea le macchine virtuali e la collega tooeach una scheda di rete VM. Questo comando specifica inoltre toouse immagine di macchina virtuale hello e le credenziali amministrative. |
| [az group delete](/cli/azure/group#delete) | Consente di eliminare un gruppo di risorse e tutte le risorse in esso contenute. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](/cli/azure/overview).

Ulteriori esempi di script CLI rete sono reperibili hello [documentazione Cenni preliminari sulle reti di Azure](../cli-samples.md)
