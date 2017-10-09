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
ms.openlocfilehash: 0e99ea66a87b7e00eb21a2f72dd2bce8673778dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a>Come tootag una macchina virtuale di Linux in Azure
Questo articolo descrive diversi modi tootag una macchina virtuale di Linux in Azure tramite il modello di distribuzione del hello Gestione risorse. I tag sono coppie chiave/valore definite dall'utente che possono essere inserite direttamente in una risorsa o un gruppo di risorse. Azure supporta attualmente i tag too15 per ogni risorsa e gruppo di risorse. Tag possono essere inseriti su una risorsa in fase di hello della creazione o aggiunta di risorse esistente tooan. Si noti, tag sono supportati per le risorse create tramite solo modello di distribuzione di gestione delle risorse hello.

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a>Assegnazione di tag con Azure CLI
toobegin, [installare e configurare hello Azure CLI](../../xplat-cli-azure-resource-manager.md) e assicurarsi che si è in modalità di gestione risorse (`azure config mode arm`).

È possibile visualizzare tutte le proprietà per una determinata macchina virtuale, inclusi tag hello, questo comando:

        azure vm show -g MyResourceGroup -n MyTestVM

tooadd un nuovo tag VM tramite hello CLI di Azure, è possibile utilizzare hello `azure vm set` comando insieme al parametro tag hello **-t**:

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

tooremove tutti i tag, è possibile utilizzare hello **– T** parametro hello `azure vm set` comando.

        azure vm set – g MyResourceGroup –n MyTestVM -T


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
