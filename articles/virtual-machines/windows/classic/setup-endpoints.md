---
title: aaaSet degli endpoint in una macchina virtuale Windows classica | Documenti Microsoft
description: Informazioni tooset degli endpoint per una macchina virtuale Windows hello Azure tooallow portale classico comunicazione con una macchina virtuale Windows in Azure.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a>Come tooset degli endpoint in una macchina virtuale di Windows classica in Azure
Tutte le finestre di macchine virtuali create in Azure utilizzando il modello di distribuzione classica hello possono comunicare automaticamente tramite un canale di rete privata con altre macchine virtuali in hello nello stesso servizio cloud o rete virtuale. Tuttavia, i computer su Internet hello o altre reti virtuali richiedono endpoint toodirect hello rete in ingresso traffico tooa computer macchina virtuale. Questo articolo è disponibile anche per le [macchine virtuali Linux](../../linux/classic/setup-endpoints.md).

> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

In hello **Gestione risorse** modello di distribuzione, gli endpoint vengono configurati tramite **rete sicurezza gruppi**. Per ulteriori informazioni, vedere [Consenti accesso esterno tooyour VM utilizzando hello Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Quando si crea una macchina virtuale Windows in hello portale di Azure, gli endpoint comuni come quelli per Desktop remoto e comunicazione remota di Windows PowerShell sono in genere creati automaticamente. È possibile configurare altri endpoint durante la creazione della macchina virtuale hello o in un secondo momento all'occorrenza.

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>Passaggi successivi
* toouse un tooset cmdlet PowerShell di Azure di un endpoint di macchina virtuale, vedere [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).
* toouse un toomanage cmdlet PowerShell di Azure un ACL su un endpoint, vedere [il controllo di accesso di gestione elenchi (ACL) per gli endpoint tramite PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).
* Se una macchina virtuale è stato creato nel modello di distribuzione di gestione risorse di hello, è possibile usare Azure PowerShell troppo[creare gruppi di sicurezza di rete](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol traffico toohello macchina virtuale.
