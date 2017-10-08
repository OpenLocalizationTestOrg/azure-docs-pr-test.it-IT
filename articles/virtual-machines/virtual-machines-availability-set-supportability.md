---
title: "aaaSupportability di aggiunta di set di disponibilità esistente tooan di macchine virtuali di Azure | Documenti Microsoft"
description: "Supporto di aggiunta di macchine virtuali di Azure tooan set di disponibilità esistente."
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a>Supporto di aggiunta di macchine virtuali di Azure tooan set di disponibilità esistente

In alcuni casi, è possibile riscontrare limitazioni quando si aggiungono nuove macchine virtuali (VM) tooan set di disponibilità esistente. Hello seguenti dettagli grafico le serie di macchina virtuale in cui è possibile combinare hello stesso set di disponibilità.

Ecco hello supportabilità matrice toomix diversi tipi di macchine virtuali:

Serie e set di disponibilità|Seconda macchina virtuale|Una |Av2|D|Dv2|Dv3|
|---|---|---|---|---|---|---|
|Prima macchina virtuale|||||||
|Una ||OK|OK|OK|OK|OK|
|Av2||OK|OK|OK|OK|OK|
|D||OK|OK|OK|OK|OK|
|Dv2||OK|OK|OK|OK|OK|
|Dv3||OK|OK|OK|OK|OK|

Tutte le altre serie non è stato in hello stesso disponibilità impostata perché richiedono un hardware specifico.
