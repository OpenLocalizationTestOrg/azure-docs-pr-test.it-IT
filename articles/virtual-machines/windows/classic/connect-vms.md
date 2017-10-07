---
title: aaaConnect macchine virtuali di Windows in un servizio cloud | Documenti Microsoft
description: Connettere le macchine virtuali di Windows create con tooan modello di distribuzione classica hello servizio cloud di Azure o rete virtuale.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c1cbc802-4352-4d2e-9e49-4ccbd955324b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: cynthn
ms.openlocfilehash: d19dc555694eab8a7e790c970cfb5e6a53aa7a7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-virtual-machines-created-with-hello-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a>Connettere le macchine virtuali di Windows create con il modello di distribuzione classica hello con un servizio cloud o di rete virtuale
> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

Macchine virtuali di Windows create con il modello di distribuzione classica hello sono sempre incluse in un servizio cloud. servizio cloud Hello funge da contenitore e fornisce un nome DNS pubblico univoco, un indirizzo IP pubblico e un set di macchina virtuale di endpoint tooaccess hello hello Internet. servizio cloud Hello può essere in una rete virtuale, ma che non è un requisito. È inoltre possibile [connettere le macchine virtuali Linux con una rete virtuale o un servizio cloud](../../linux/classic/connect-vms.md).

Se un servizio cloud non si trova in una rete virtuale, è detto servizio cloud *autonomo* . macchine virtuali Hello in un servizio cloud autonomo comunicare con altre macchine virtuali tramite hello nomi DNS pubblici altre macchine virtuali e traffico hello viene trasmessa hello Internet. Se un servizio cloud è in una rete virtuale, le macchine virtuali hello in servizio cloud può comunicare con tutte le altre macchine virtuali nella rete virtuale hello senza inviare tutto il traffico attraverso hello Internet.

Se si inseriscono delle macchine virtuali in hello nello stesso servizio cloud autonomo, è comunque possibile usare il bilanciamento del carico e set di disponibilità. Per informazioni dettagliate, vedere [il bilanciamento del carico delle macchine virtuali](../../virtual-machines-windows-load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [gestione hello disponibilità delle macchine virtuali](../../virtual-machines-windows-manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Tuttavia, non è possibile organizzare le macchine virtuali hello in subnet o connettere una rete locale tooyour di autonomo cloud del servizio. Ad esempio:

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato una macchina virtuale, è buona norma troppo[aggiungere un disco dati](attach-disk.md) in modo che i servizi e i carichi di lavoro dati toostore percorso.
