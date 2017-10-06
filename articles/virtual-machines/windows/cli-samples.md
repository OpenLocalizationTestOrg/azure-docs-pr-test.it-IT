---
title: aaaAzure CLI esempi di Windows | Documenti Microsoft
description: Esempi dell'interfaccia della riga di comando di Azure per Windows
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 1eef61a24d14897dd0a88a3f467854cc21b1938d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-windows-virtual-machines"></a>Esempi dell'interfaccia della riga di comando di Azure per macchine virtuali Windows

Hello nella tabella seguente sono inclusi collegamenti toobash script compilato utilizzando hello CLI di Azure che distribuire macchine virtuali di Windows.

| | |
|---|---|
|**Creare macchine virtuali**||
| [Creare una macchina virtuale](./../scripts/virtual-machines-windows-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | Consente di creare una macchina virtuale Windows con la configurazione minima. |
| [Creare una macchina virtuale completamente configurata](./../scripts/virtual-machines-windows-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | Consente di creare un gruppo di risorse, una macchina virtuale e tutte le risorse correlate.|
| [Creare macchine virtuali a disponibilità elevata](./../scripts/virtual-machines-windows-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | Consente di creare più macchine virtuali in una configurazione a disponibilità elevata e con bilanciamento del carico. |
| [Creare una macchina virtuale ed eseguire script di configurazione](./../scripts/virtual-machines-windows-cli-sample-create-vm-iis.md?toc=%2fcli%2fazure%2ftoc.json) | Crea una macchina virtuale e utilizza hello Azure Custom Script estensione tooinstall IIS. |
| [Creare una macchina virtuale ed eseguire la configurazione DSC](./../scripts/virtual-machines-windows-cli-sample-create-iis-using-dsc.md?toc=%2fcli%2fazure%2ftoc.json) | Crea una macchina virtuale e utilizza hello Azure configurazione DSC (Desired State) estensione tooinstall IIS. |
|**Macchine virtuali di rete**||
| [Proteggere il traffico di rete tra le macchine virtuali](./../scripts/virtual-machines-windows-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | Consente di creare due macchine virtuali, tutte le risorse correlate, un gruppo di sicurezza di rete interno e uno esterno. |
|**Proteggere le macchine virtuali**||
| [Crittografare una macchina virtuale e i dischi dati](./../scripts/virtual-machines-windows-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | Crea un'istanza di Azure Key Vault, una chiave di crittografia e un'entità servizio, quindi crittografa una macchina virtuale. |
|**Monitorare le macchine virtuali**||
| [Monitorare una macchina virtuale con Operations Management Suite](./../scripts/virtual-machines-windows-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | Crea una macchina virtuale, installa l'agente di Operations Management Suite hello e registra hello macchina virtuale in un'area di lavoro di OMS.  |
| | |
