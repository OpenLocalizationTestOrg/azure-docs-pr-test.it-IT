---
title: aaaAzure CLI Script di esempio - creare una macchina virtuale di Windows Server 2016 con IIS mediante DSC | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una macchina virtuale Windows Server 2016 con IIS usando DSC
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.custom: mvc
ms.openlocfilehash: 9883b5925dddca3dd53d083679a0e76d0fb982e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-iis-using-dsc"></a>Creare una macchina virtuale con IIS usando DSC

Questo script crea una macchina virtuale e utilizza tooinstall estensione script personalizzato di hello macchina virtuale di Azure DSC e configura IIS. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-windows-iis-using-dsc/create-windows-iis-using-dsc.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, la macchina virtuale, hello e tutte risorse correlate. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Crea macchina virtuale hello e lo connette la scheda di rete toohello, rete virtuale, subnet e gruppo. Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.  |
| [az vm extension set](https://docs.microsoft.com/cli/azure/vm#create) | Aggiungere la macchina hello estensione Script personalizzata toohello virtuale che richiama un tooinstall script IIS. |
| [az vm open-port](https://docs.microsoft.com/cli/azure/vm#open-port) | Crea un tooallow di regola gruppo di sicurezza rete il traffico in ingresso. In questo esempio, la porta 80 è aperta al traffico HTTP. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione macchina virtuale Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
