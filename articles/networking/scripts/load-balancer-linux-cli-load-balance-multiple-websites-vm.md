---
title: "bilanciamento del carico aaaAzure CLI Script di esempio - più siti Web con hello CLI di Azure | Documenti Microsoft"
description: "Esempio di Script di Azure CLI - più siti Web toohello il bilanciamento del carico stessa macchina virtuale"
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 136da5d1783fb9f9dc87f1ffad8eec7b95c6bd7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a>Eseguire il bilanciamento del carico per più siti Web

Questo esempio di script crea una rete virtuale con due macchine virtuali che fanno parte di un set di disponibilità. Un servizio di bilanciamento del carico indirizza il traffico di due macchine virtuali toohello due indirizzi IP. Dopo l'esecuzione dello script hello, è possibile distribuire toohello software tramite server web le macchine virtuali e ospitare più siti web, ciascuno con il proprio indirizzo IP.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, la rete virtuale, bilanciamento del carico e tutte le relative risorse. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | Consente di creare una rete virtuale e una subnet di Azure. |
| [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Consente di creare un indirizzo IP pubblico con un indirizzo IP statico e un nome DNS associato. |
| [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#create) | Crea un servizio di bilanciamento del carico di Azure. |
| [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Crea un probe di bilanciamento del carico. Un probe di bilanciamento del carico è toomonitor usato ogni macchina virtuale nel set di bilanciamento carico di hello. Se qualsiasi macchina virtuale non è accessibile, il traffico non è indirizzato toohello macchina virtuale. |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Crea una regola di bilanciamento del carico. In questo esempio viene creata una regola per la porta 80. Come il traffico HTTP arriva al servizio di bilanciamento del carico hello, è indirizzato tooport 80 una delle macchine virtuali di hello nel set di bilanciamento carico di hello. |
| [az network lb frontend-ip create](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | Creare un indirizzo IP di front-end per hello bilanciamento del carico. |
| [az network lb address-pool create](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | Crea un pool di indirizzi back-end. |
| [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#create) | Crea una scheda di rete virtuale e la collega toohello di rete virtuale e la subnet. |
| [az vm availability-set create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Consente di creare un set di disponibilità. Set di disponibilità la distribuzione di macchine virtuali hello tra risorse fisiche in modo che se si verifica l'errore, non è stato eseguito alcun set intero di hello assicurare la disponibilità dell'applicazione. |
| [az network nic ip-config create](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | Crea una configurazione IP. È necessario disporre di funzionalità Microsoft.Network/AllowMultipleIpConfigurationsPerNic hello abilitata per la sottoscrizione. Solo una configurazione può essere definita come configurazione IP primaria hello per ogni scheda di rete, utilizzando hello - flag di creazione primario. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Crea macchina virtuale hello e lo connette la scheda di rete toohello, rete virtuale, subnet e gruppo. Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.  |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Ulteriori esempi di script CLI rete sono reperibili hello [documentazione Cenni preliminari sulle reti di Azure](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
