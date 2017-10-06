---
title: aaaAzure CLI Script di esempio - riavviare le macchine virtuali | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Riavviare macchine virtuali in base al tag e all'ID
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a>Riavviare le VM

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

Questo esempio viene illustrato un paio di modi tooget alcune macchine virtuali e riavviarle.

Hello riavvia innanzitutto tutte le macchine virtuali hello nel gruppo di risorse hello.

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

secondo ottiene hello Hello tag macchine virtuali con `az resouce list` Filtra le risorse toohello macchine virtuali e riavvia tali macchine virtuali.

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

Questo esempio funziona in una shell Bash. Per opzioni all'esecuzione di script CLI di Azure su client Windows, vedere [in esecuzione hello CLI di Azure in Windows](../windows/cli-options.md).


## <a name="sample-script"></a>Script di esempio

esempio Hello ha tre script.
Hello macchine virtuali di un primo disposizioni hello.
Opzione no-wait hello viene utilizzato in modo comando hello viene restituita senza aspettare in ogni macchina virtuale toobe il provisioning.
Hello secondo rimane in attesa hello macchine virtuali toobe eseguito il provisioning completo.
script terzo Hello riavvia tutte le macchine virtuali hello che ha effettuato il provisioning e quindi hello solo tag macchine virtuali.

### <a name="provision-hello-vms"></a>Eseguire il provisioning di hello macchine virtuali

Questo script crea un gruppo di risorse e quindi crea tre toorestart macchine virtuali.
Due di queste vengono contrassegnate con tag.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a>Attesa

Questo script verifica su hello ogni 20 secondi finché non vengono effettuato il provisioning di tutti e tre macchine virtuali, o uno di essi non tooprovision lo stato del provisioning.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a>Riavviare le macchine virtuali hello

Questo script viene riavviato hello tutte le macchine virtuali nel gruppo di risorse hello e riavvia solo le macchine virtuali hello tag.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove hello gruppi di risorse, le macchine virtuali e tutte le relative risorse.

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, macchina virtuale, set di disponibilità, bilanciamento del carico e tutte le relative risorse. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Crea le macchine virtuali hello.  |
| [az vm list](https://docs.microsoft.com/cli/azure/vm#list) | Utilizzato con `--query` tooensure hello macchine virtuali viene effettuato il provisioning prima di riavviarli, e quindi tooget hello gli ID di hello toorestart di macchine virtuali di loro. |
| [az resource list](https://docs.microsoft.com/cli/azure/vm#list) | Utilizzato con `--query` tooget hello gli ID delle macchine virtuali hello mediante tag hello. |
| [az vm restart](https://docs.microsoft.com/cli/azure/vm#list) | Consente di riavviare le macchine virtuali hello. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
