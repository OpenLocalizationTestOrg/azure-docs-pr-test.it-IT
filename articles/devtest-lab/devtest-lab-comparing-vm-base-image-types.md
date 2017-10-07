---
title: aaaComparing immagini personalizzate e le formule di DevTest Labs | Documenti Microsoft
description: "Informazioni sulle differenze hello immagini personalizzate e le formule come macchina virtuale si basa in modo è possibile scegliere quella più appropriata per l'ambiente."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tarcher
ms.openlocfilehash: 3c1d88dfe0ff94b8e825bb7a0b4aca3341c9330d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a>Confronto tra immagini personalizzate e formule nei lab di sviluppo/test
Sia le [immagini personalizzate](devtest-lab-create-template.md) che le [formule](devtest-lab-manage-formulas.md) possono essere usate come basi per [creare nuove macchine virtuali](devtest-lab-add-vm-with-artifacts.md). Tuttavia, hello chiave per distinguere le immagini personalizzate e le formule è che un'immagine personalizzata è semplicemente un'immagine basata su un disco rigido virtuale, mentre una formula è un'immagine basata su un disco rigido virtuale *oltre a* preconfigurato impostazioni - ad esempio dimensioni delle macchine Virtuali, rete virtuale, subnet e gli elementi. Queste impostazioni preconfigurate vengono configurate con i valori predefiniti che possono essere sostituiti in fase di hello di creazione della macchina virtuale. In questo articolo illustra alcuni dei vantaggi di hello (Pro) e immagini personalizzate di toousing (cons) piuttosto che utilizzare formule svantaggi.

## <a name="custom-image-pros-and-cons"></a>Vantaggi e svantaggi delle immagini personalizzate
Immagini personalizzate forniscono un metodo statico e non modificabile di toocreate macchine virtuali da un ambiente desiderato. 

**Vantaggi**

* VM provisioning da un'immagine personalizzata è veloce, non vengono apportate modifiche dopo la macchina virtuale viene riattivata hello dall'immagine hello. Sono non disponibili in altre parole, tooapply impostazioni come immagine personalizzata hello è solo un'immagine senza le impostazioni. 
* Le macchine virtuali create da un'unica immagine personalizzata sono identiche.

**Svantaggi**

* Se è necessario tooupdate alcuni aspetti dell'immagine personalizzata hello, è necessario ricreare l'immagine di hello.  

## <a name="formula-pros-and-cons"></a>Vantaggi e svantaggi delle formule
Le formule forniscono un toocreate dinamico modo macchine virtuali dalle impostazioni di configurazione/hello desiderato.

**Vantaggi**

* È possibile acquisire le modifiche nell'ambiente di hello hello volo tramite gli elementi. Ad esempio, se si desidera che una macchina virtuale installata con i bit più recenti di hello dalla pipeline di rilascio o integra codice più recente di hello dal repository, è possibile specificare semplicemente un elemento che distribuisce i bit più recenti hello o inserisce il codice più recente di hello nella formula hello insieme a un immagine di base di destinazione. Ogni volta che questa formula macchine virtuali utilizzate toocreate, codice o i bit più recente hello sono distribuiti integrata toohello macchina virtuale. 
* A differenza delle immagini personalizzate, le formule possono definire impostazioni predefinite come le dimensioni delle macchine virtuali e le impostazioni della rete virtuale. 
* le impostazioni di Hello salvate in una formula vengono visualizzate come valori predefiniti, ma possono essere modificate quando viene creato hello macchina virtuale. 

**Svantaggi**

* La creazione di una macchina virtuale da una formula può richiedere più tempo rispetto alla creazione da un'immagine personalizzata.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Post di blog correlati
* [Custom images or formulas? (Immagini personalizzate o formule?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a>Passaggi successivi
- [Domande frequenti su DevTest Labs](devtest-lab-faq.md)