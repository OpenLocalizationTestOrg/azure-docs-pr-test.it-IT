---
title: aaaAzure CLI Script di esempio - creare una VM Linux con bilanciamento carico di rete | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una VM Linux con bilanciamento del carico di rete
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 79b245c1268734fead313b34c120f74ab2330d4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-highly-available-vm"></a>Creare una VM a disponibilità elevata

In questo esempio di script crea tutti gli elementi necessari toorun diverse macchine virtuali Ubuntu configurati a disponibilità elevata e carico bilanciato di configurazione. Tre macchine virtuali, tooan aggiunti a un Set di disponibilità di Azure, sarà necessario dopo l'esecuzione dello script, hello e accessibile tramite un servizio di bilanciamento del carico di Azure. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, macchina virtuale, set di disponibilità, bilanciamento del carico e tutte le relative risorse. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | Consente di creare una rete virtuale e una subnet di Azure. |
| [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Consente di creare un indirizzo IP pubblico con un indirizzo IP statico e un nome DNS associato. |
| [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#create) | Consente di creare un bilanciamento del carico di rete di Azure (NLB). |
| [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Consente di creare un probe di bilanciamento del carico di rete. Un probe di bilanciamento carico di rete viene utilizzato toomonitor ogni macchina virtuale nel set di bilanciamento carico di rete hello. Se qualsiasi macchina virtuale non è accessibile, il traffico non è indirizzato toohello macchina virtuale. |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Consente di creare una regola di bilanciamento del carico di rete. In questo esempio viene creata una regola per la porta 80. Come il traffico HTTP riceve hello bilanciamento carico di rete, è indirizzato tooport 80 una delle macchine virtuali di hello nel set di bilanciamento carico di rete hello. |
| [az network lb inbound-nat-rule create](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | Consente di creare una regola Network Address Translation (NAT) di bilanciamento del carico di rete.  Le regole NAT mapping di una porta di hello porta tooa bilanciamento carico di rete in una macchina virtuale. In questo esempio, viene creata una regola NAT per il traffico SSH tooeach macchina virtuale nel set di bilanciamento carico di rete hello.  |
| [az network nsg create](https://docs.microsoft.com/cli/azure/network/nsg#create) | Crea un gruppo di sicurezza di rete (gruppo), ovvero un limite di sicurezza tra le macchine virtuali internet e hello hello. |
| [az network nsg rule create](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Crea un tooallow regola NSG il traffico in ingresso. In questo esempio, la porta 22 è aperta al traffico SSH. |
| [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#create) | Crea una scheda di rete virtuale e la collega toohello di rete virtuale, subnet e gruppo. |
| [az vm availability-set create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Consente di creare un set di disponibilità. Set di disponibilità la distribuzione di macchine virtuali hello tra risorse fisiche in modo che se si verifica l'errore, non è stato eseguito alcun set intero di hello assicurare la disponibilità dell'applicazione. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Crea macchina virtuale hello e lo connette la scheda di rete toohello, rete virtuale, subnet e gruppo. Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.  |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
