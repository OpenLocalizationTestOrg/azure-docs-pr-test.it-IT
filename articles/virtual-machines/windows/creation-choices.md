---
title: aaaDifferent modi toocreate una macchina virtuale Windows in Azure | Documenti Microsoft
description: Elenca i diversi modi di hello toocreate una macchina virtuale di Windows con Gestione risorse.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a>Modi diversi toocreate una macchina virtuale Windows

Azure offre modi toocreate una macchina virtuale perché le macchine virtuali sono adatti per scopi e utenti diversi. Ciò significa che è necessario toomake elencate alcune scelte sulla macchina virtuale hello e come toocreate è. In questo articolo offre un riepilogo di queste opzioni e i collegamenti tooinstructions.

## <a name="azure-portal"></a>Portale di Azure
Tramite il portale di Azure hello è tootry un modo semplice out di una macchina virtuale, in particolare se si inizia con Azure. 

[Creare una macchina virtuale che esegue Windows usando il portale di hello](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a>Modello
Le macchine virtuali richiedono una combinazione di risorse (come set di disponibilità e account di archiviazione). Invece di distribuire e gestire separatamente ogni risorsa, è possibile creare un modello di gestione risorse di Azure che distribuisce ed esegue il provisioning di tutte le risorse di hello in un'operazione singola, coordinata.

* [Creare una macchina virtuale Windows con un modello di Gestione risorse](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a>Azure PowerShell
Se si preferisce lavorare in una shell dei comandi, è possibile utilizzare Azure PowerShell.

* [Creare una VM Windows tramite PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a>Visual Studio
Utilizzare Visual Studio toobuild, gestire, distribuire le macchine virtuali con hello Azure Tools per Visual Studio e hello Azure SDK.

[Strumenti di Azure per Visual Studio](https://www.visualstudio.com/features/azure-tools-vs)

