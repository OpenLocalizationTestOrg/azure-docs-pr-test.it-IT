---
title: aaaAzure CLI Script di esempio - creare una macchina virtuale con un disco rigido virtuale | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una macchina virtuale Linux usando un disco rigido virtuale.
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
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a>Creare una macchina virtuale con un disco rigido virtuale

In questo esempio viene creata una macchina virtuale usando un disco rigido virtuale.
Crea un gruppo di risorse, un account di archiviazione e un contenitore, quindi crea una macchina virtuale caricando contenitore toohello di hello disco rigido virtuale.
Sostituisce hello ssh pubblica della chiave con la chiave pubblica in modo da disporre di accesso toohello macchina virtuale.

È necessario un disco rigido virtuale di avvio.
È possibile scaricare hello disco rigido virtuale che è stato usato da https://azclisamples.blob.core.windows.net/vhds/sample.vhd o utilizzare un disco rigido virtuale. Cerca script Hello `~/sample.vhd`.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, macchina virtuale, set di disponibilità, bilanciamento del carico e tutte le relative risorse. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az storage account list](https://docs.microsoft.com/cli/azure/storage/account#list) | Elenca gli account di archiviazione |
| [az storage account check-name](https://docs.microsoft.com/cli/azure/storage/account#check-name) | Verifica che un nome di account di archiviazione sia valido e che non esista già |
| [az storage account keys list](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | Elenca le chiavi per gli account di archiviazione hello |
| [az storage blob exists](https://docs.microsoft.com/cli/azure/storage/blob#exists) | Verifica l'esistenza di blob hello |
| [az storage container create](https://docs.microsoft.com/cli/azure/storage/container#create) | Crea un contenitore in un account di archiviazione. |
| [az storage blob upload](https://docs.microsoft.com/cli/azure/storage/blob#upload) | Crea un blob nel contenitore hello hello il caricamento del disco rigido virtuale. |
| [az vm list](https://docs.microsoft.com/cli/azure/vm#list) | Utilizzato con `--query` controllare se il nome di macchina virtuale hello è in uso. | 
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Crea le macchine virtuali hello. |
| [az vm access set-linux-user](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | Reimposta hello SSH toogive chiave hello corrente utente accesso toohello macchina virtuale. |
| [az vm list-ip-addresses](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | Ottiene l'indirizzo IP hello di hello macchina virtuale che è stato creato. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
