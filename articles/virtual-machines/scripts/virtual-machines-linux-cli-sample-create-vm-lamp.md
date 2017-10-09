---
title: "aaaAzure CLI Script di esempio - distribuire hello Stack LAMP in un Set di scalabilità di Machin virtuale Load-Balanced | Documenti Microsoft"
description: "Utilizzare hello toodeploy estensione di uno script personalizzato Stack LAMP in un carico = scalabilità della macchina virtuale con bilanciamento impostato in Azure."
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
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a>Distribuire stack LAMP hello in un set di scalabilità della macchina virtuale di bilanciamento del carico

In questo esempio crea un set di scalabilità della macchina virtuale e si applica un'estensione che viene eseguito uno stack di luce hello toodeploy script personalizzato in ogni macchina virtuale nel set di scalabilità hello.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Script di esempio

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a>Connettere

Utilizzare questo codice toosee come impostare tooconnect tooyour macchine virtuali e la scala.

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Eseguire hello seguente gruppo di risorse di comando tooremove hello, hello set di scalabilità e le macchine virtuali e tutte le relative risorse.

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, macchina virtuale, set di disponibilità, bilanciamento del carico e tutte le relative risorse. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az vmss create](https://docs.microsoft.com/cli/azure/vmss#create) | Consente di creare un set di scalabilità di macchine virtuali |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Consente di aggiungere un endpoint con carico bilanciato |
| [az vmss extension set](https://docs.microsoft.com/cli/azure/vmss/extension#set) | Creare l'estensione hello che esegue uno script personalizzato hello sulla distribuzione di una macchina virtuale |
| [az vmss update-instances](https://docs.microsoft.com/cli/azure/vmss#update-instances) | Eseguire uno script personalizzato hello nelle istanze VM hello che sono state distribuite prima dell'applicazione di estensione hello toohello set di scalabilità. |
| [az vmss scale](https://docs.microsoft.com/cli/azure/vmss#scale) | La scalabilità verticale hello scala impostata tramite l'aggiunta di più istanze di macchina virtuale. script personalizzato Hello viene eseguito su questi quando vengono distribuiti. |
| [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) | Ottenere gli indirizzi IP di hello di macchine virtuali create da esempio hello hello. |
| [az network lb show](https://docs.microsoft.com/cli/azure/network/lb#show) | Porte utilizzate dal servizio di bilanciamento del carico hello ottenere back-end e front-end hello. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
