---
title: aaaAzure CLI Script di esempio - creare una VM Linux con OMS monitoraggio | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una VM Linux con il monitoraggio di OMS
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
ms.openlocfilehash: 7a329d4f90a20e0e11faa1f5cafd0701574dc440
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a>Monitorare una macchina virtuale con Operations Management Suite

Questo script crea una macchina virtuale di Azure, installa l'agente di Operations Management Suite (OMS) hello e registra sistema hello con un'area di lavoro OMS. Dopo l'esecuzione dello script di hello, macchina virtuale hello saranno visibile nella console OMS hello.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, la macchina virtuale, hello e tutte risorse correlate. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Crea macchina virtuale hello e lo connette la scheda di rete toohello, rete virtuale, subnet e gruppo. Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.  |
| [azure vm extension set](https://docs.microsoft.com/cli/azure/vm/extension#set) | Consente di eseguire un'estensione di VM in una macchina virtuale. In questo caso, hello estensione agente Operations Management Suite tooinstall utilizzati hello OMS agente e registrare hello macchina virtuale in un'area di lavoro OMS. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
