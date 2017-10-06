---
title: aaaAzure CLI Script di esempio - creare una VM Linux con NGINX | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una VM Linux con NGINX
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9166ccfd4f2e6eea731a8dc6956575d9f8f85488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-nginx"></a>Creare una VM con NGINX

Questo script crea una macchina virtuale di Azure e Usa l'estensione Script personalizzata della macchina virtuale Azure di hello tooinstall NGINX. Dopo l'esecuzione di script hello, è possibile accedere a un sito Web demo sull'indirizzo IP pubblico di hello della macchina virtuale hello.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]

## <a name="custom-script-extension"></a>Estensione di script personalizzati

estensione script personalizzata Hello copia questo script nella macchina virtuale hello. script di Hello viene quindi eseguito tooinstall e configurare un server web NGINX. 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

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
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Crea macchina virtuale hello. Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.  |
| [az vm open-port](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Crea un tooallow di regola gruppo di sicurezza rete il traffico in ingresso. In questo esempio, la porta 80 è aperta al traffico HTTP. |
| [azure vm extension set](https://docs.microsoft.com/cli/azure/vm/extension#set) | Aggiunge e viene eseguito un tooa di estensione della macchina virtuale macchina virtuale. In questo esempio, un'estensione personalizzata hello è usato tooinstall NGINX.|
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
