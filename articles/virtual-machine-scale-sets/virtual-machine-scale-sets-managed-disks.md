---
title: aaaUsing gestiti dischi con Azure scala set di macchine virtuali | Documenti Microsoft
description: "Informazioni su come e perché toouse gestiti dischi con il set di scalabilità di macchine virtuali"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/01/2017
ms.author: negat
ms.openlocfilehash: 0e2a21e9f8b114ae1c8b81e1e6124621366f5643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a>Set di scalabilità VM di Azure e dischi gestiti

I [set di scalabilità di macchine virtuali](/azure/virtual-machine-scale-sets/) di Azure supportano macchine virtuali con dischi gestiti. L'uso di dischi gestiti con i set di scalabilità presenta diversi vantaggi, tra cui:

* Non è più necessario toopre-creare e gestire i dischi di archiviazione account toostore hello del sistema operativo per le macchine virtuali del set di scalabilità di hello.

* È possibile collegare i set di scalabilità toohello dischi di dati gestiti.

* Grazie al disco gestito, un set di scalabilità può contenere fino a un massimo di 1.000 macchine virtuali se basato su un'immagine di piattaforma o di 100 macchine virtuali se basato su un'immagine personalizzata.

## <a name="get-started"></a>Attività iniziali

Un modo semplice tooget avviato con il set di scalabilità di un disco gestito è toodeploy da hello portale di Azure. Per altre informazioni, vedere [questo articolo](./virtual-machine-scale-sets-portal-create.md). Un altro modo semplice tooget avviato è toouse [CLI di Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy una scala impostata. Hello seguente illustra un Ubuntu toocreate basati su set di scalabilità con 10 macchine virtuali, ognuno con un disco da 50 GB e 100 GB di dati:

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

In alternativa, è possibile cercare in hello [repository GitHub modelli Guida introduttiva di Azure](https://github.com/Azure/azure-quickstart-templates) per le cartelle che contengono `vmss` toosee predefinite esempi di modelli di distribuire i set di scalabilità. tootell i modelli sono già in uso dischi gestiti, è possibile fare riferimento troppo[questo elenco](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sui dischi gestiti in generale, vedere [questo articolo](../virtual-machines/windows/managed-disks-overview.md).

toosee su una scala di gestione risorse modello tooprovision imposta con tooconvert gestiti dischi, vedere [questo articolo](./virtual-machine-scale-sets-convert-template-to-md.md). Hello stessi modelli di gestione risorse toohello modifiche si applicano toohello API REST di Azure.

toolearn ulteriori informazioni sull'utilizzo di dischi di dati gestiti con il set di scalabilità, vedere [questo articolo](./virtual-machine-scale-sets-attached-disks.md).

toobegin lavora con set su larga scala, fare riferimento troppo[questo articolo](./virtual-machine-scale-sets-placement-groups.md).


