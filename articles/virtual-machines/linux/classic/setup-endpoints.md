---
title: aaaSet degli endpoint in una VM Linux classico | Documenti Microsoft
description: Informazioni su tooset degli endpoint per una VM Linux di hello Azure tooallow portale classico comunicazione con una macchina virtuale di Linux in Azure
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a>Come tooset degli endpoint in una macchina virtuale di Linux classica in Azure
Tutte le macchine virtuali Linux create in Azure utilizzando il modello di distribuzione classica hello possono comunicare automaticamente tramite un canale di rete privata con altre macchine virtuali in hello che stesso servizio o della rete virtuale del cloud. Tuttavia, i computer su Internet hello o altre reti virtuali richiedono endpoint toodirect hello rete in ingresso traffico tooa computer macchina virtuale. Questo articolo è disponibile anche per le [macchine virtuali Windows](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

In hello **Gestione risorse** modello di distribuzione, gli endpoint vengono configurati tramite **rete sicurezza gruppi**. Per altre informazioni, vedere [Apertura di porte e di endpoint](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Quando si crea una macchina virtuale Linux nel portale di Azure hello, un endpoint per SSH (Secure Shell) è in genere creato automaticamente. È possibile configurare altri endpoint durante la creazione della macchina virtuale hello o in un secondo momento all'occorrenza.

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>Passaggi successivi
* È anche possibile creare un endpoint della macchina virtuale utilizzando hello [interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2). Eseguire hello **creare endpoint di macchina virtuale di azure** comando.
* Se una macchina virtuale è stato creato nel modello di distribuzione di gestione risorse di hello, è possibile utilizzare anche hello CLI di Azure in modalità di gestione risorse[creare gruppi di sicurezza di rete](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol traffico toohello macchina virtuale.
