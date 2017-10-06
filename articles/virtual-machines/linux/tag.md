---
title: aaaHow tootag una macchina virtuale Linux di Azure | Documenti Microsoft
description: Informazioni sull'uso dei tag di una macchina virtuale di Linux di Azure creata in Azure tramite il modello di distribuzione di gestione risorse di hello.
services: virtual-machines-linux
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: memccror
ms.openlocfilehash: 456b226af4495c3b446cb79c99cf9494dde9fca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a>Come tootag una macchina virtuale di Linux in Azure
Questo articolo descrive diversi modi tootag una macchina virtuale di Linux in Azure tramite il modello di distribuzione del hello Gestione risorse. I tag sono coppie chiave/valore definite dall'utente che possono essere inserite direttamente in una risorsa o un gruppo di risorse. Azure supporta attualmente i tag too15 per ogni risorsa e gruppo di risorse. Tag possono essere inseriti su una risorsa in fase di hello della creazione o aggiunta di risorse esistente tooan. Si noti, tag sono supportati per le risorse create tramite solo modello di distribuzione di gestione delle risorse hello.

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a>Assegnazione di tag con Azure CLI
toobegin, è necessario hello più recente [2.0 CLI di Azure (anteprima)](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).

È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

È possibile visualizzare tutte le proprietà per una determinata macchina virtuale, inclusi tag hello, questo comando:

        az vm show --resource-group MyResourceGroup --name MyTestVM

tooadd un nuovo tag VM tramite hello CLI di Azure, è possibile utilizzare hello `azure vm update` comando insieme al parametro tag hello **-impostare**:

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

tag tooremove, è possibile utilizzare hello **-rimuovere** parametro hello `azure vm update` comando.

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


Ora che sono applicati tag tooour risorse CLI di Azure e hello portale, esaminiamo un hello utilizzo dettagli toosee tag hello nel portale di fatturazione hello.

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>Passaggi successivi
* toolearn ulteriori informazioni sull'assegnazione di tag delle risorse di Azure, vedere [Panoramica di gestione risorse di Azure] [ Azure Resource Manager Overview] e [tooorganize tag usando le risorse di Azure] [ Using Tags tooorganize your Azure Resources].
* toosee come tag consentono di gestire l'utilizzo delle risorse di Azure, vedere [comprendere la fattura di Azure] [ Understanding your Azure Bill] e [ottenere informazioni approfondite del consumo di risorse di Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
