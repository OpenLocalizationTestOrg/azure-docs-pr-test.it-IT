---
title: aaaView hello mensile stimato del lab tendenza dei costi in Azure DevTest Labs | Documenti Microsoft
description: Informazioni sul grafico di tendenza mensile costo stimato di hello Azure DevTest Labs.
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 47c7dd4cf91b76de74b502c50f05e79cd501ee35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="view-hello-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a>Visualizzazione hello mensile stimato del lab tendenza dei costi in Azure DevTest Labs
funzionalità di gestione dei costi Hello di DevTest Labs consente di tenere traccia dei costi di hello del lab. Questo articolo illustra come hello toouse **mensile tendenza costo stimato** tooview grafico hello stimato costo-to-date del mese di calendario corrente e hello costo del mese di fine per hello mese di calendario corrente. In questo articolo viene illustrato come tooview hello grafico di tendenza mensile costo stimato in hello portale di Azure.

## <a name="viewing-hello-monthly-estimated-cost-trend-chart"></a>Visualizzazione grafico di tendenza di costo stimato mensile hello
hello tooview grafico di tendenza di costo stimato mensile, seguire questi passaggi: 

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.
3. Elenco dei laboratori hello selezionare lab desiderato hello.   
4. Nel pannello del lab hello, selezionare **costo impostazioni**.
5. Nel lab di hello **costo impostazioni** pannello seleziona **Lab costo tendenza**.
6. Hello schermata riportata di seguito viene illustrato un esempio di un grafico di costo. 
   
    ![Grafico dei costi](./media/devtest-lab-configure-cost-management/graph.png)

Hello **costo stimato** valore è hello stimato costo-to-date del mese di calendario corrente. Hello **costo previsto** hello costo stimato per hello intero mese di calendario corrente, calcolato utilizzando costo lab hello per hello cinque giorni precedenti.

gli importi di costo Hello vengono arrotondati toohello successivo numero intero. ad esempio: 

* 5.01 Arrotonda too6 
* 5,50 Arrotonda too6
* 5.99 Arrotonda too6

, Come indicato sopra il grafico hello costi hello viene visualizzato nel grafico hello sono *stimato* costi utilizzando [consumo](https://azure.microsoft.com/offers/ms-azr-0003p/) offrono tariffe.
Sono inoltre seguente hello *non* incluso nel calcolo del costo hello:

* CSP e Dreamspark sottoscrizioni attualmente non sono supportate in Azure DevTest Labs utilizza hello [Azure API fatturazione](../billing/billing-usage-rate-card-overview.md) lab hello toocalculate costo, che non supporta le sottoscrizioni Dreamspark o di CSP.
* Le tariffe della propria offerta. Attualmente, non è in grado di toouse (mostrate sotto della sottoscrizione) che hanno negoziate con Microsoft o Microsoft partner per le tariffe di offerta. Vengono usate tariffe a consumo.
* Le imposte
* Gli sconti
* La valuta di fatturazione Attualmente, il costo di lab hello viene visualizzato solo nella valuta USD.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Post di blog correlati
* [Due altre tookeep di operazioni dei costi in modo corretto in DevTest Labs](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [Why Cost Thresholds? (Perché usare le soglie dei costi?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a>Passaggi successivi
Ecco alcuni aspetti tootry accanto:

* [Definire i criteri di lab](devtest-lab-set-lab-policy.md) -informazioni su come tooset hello vari criteri utilizzati toogovern come vengono usati nel lab e delle relative macchine virtuali. 
* [Creare un'immagine personalizzata](devtest-lab-create-template.md): quando si crea una VM, si specifica una base, che può essere un'immagine personalizzata o un'immagine del Marketplace. Questo articolo illustra come toocreate immagine personalizzata da un file VHD.
* [Configurare le immagini del Marketplace](devtest-lab-configure-marketplace-images.md): DevTest Labs supporta la creazione di VM basate su immagini di Azure Marketplace. Questo articolo illustra come toospecify che, se presente, le immagini di Azure Marketplace possono essere utilizzati durante la creazione di macchine virtuali in un ambiente lab.
* [Creare una macchina virtuale in un ambiente lab](devtest-lab-add-vm-with-artifacts.md) -illustra come toocreate una macchina virtuale da un'immagine di base (entrambi personalizzato o Marketplace) e come toowork con gli elementi di una macchina virtuale.

