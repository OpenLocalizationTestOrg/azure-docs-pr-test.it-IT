---
title: aaaScale quote e limiti nell'ambiente lab in Azure DevTest Labs | Documenti Microsoft
description: Informazioni su come tooscale un laboratorio di Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a>Ridimensionare i limiti e le quote in DevTest Labs
Mentre si lavora in DevTest Labs, è possibile notare che esistono determinati toosome limiti predefinito risorse di Azure, che possono influire sul servizio di DevTest Labs hello. Questi limiti sono cui tooas **quote**.

> [!NOTE]
> servizio di DevTest Labs Hello non imporre le quote. Le quote che possono verificarsi sono vincoli predefiniti di hello sottoscrizione globale di Azure.

È possibile usare ogni risorsa di Azure finché non si raggiunge la quota. Ogni sottoscrizione dispone di quote separate il cui uso viene controllato per ogni sottoscrizione.

Ad esempio, ogni sottoscrizione ha una quota predefinita di 20 core. Pertanto, se si siano creano macchine virtuali nel lab con quattro core, è possibile creare solo cinque macchine virtuali. 

[Sottoscrizione di Azure e limiti dei servizi](https://docs.microsoft.com/azure/azure-subscription-service-limits) vengono elencate alcune delle quote più comuni di hello per le risorse di Azure. Hello le risorse usate più di frequente in un ambiente lab e per cui potrebbero verificarsi le quote, includere core VM, gli indirizzi IP pubblici, l'interfaccia di rete, dischi gestiti, assegnazione di ruolo RBAC e circuiti ExpressRoute.

## <a name="view-your-usage-and-quotas"></a>Visualizzare le quote e l'uso
Questi passaggi mostrano come tooview hello quote corrente nella sottoscrizione per le risorse di Azure specifiche e toosee la percentuale di ogni quota utilizzata.

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selezionare **più servizi**, quindi selezionare **fatturazione** dall'elenco di hello.
1. Nel pannello fatturazione hello, selezionare una sottoscrizione.
4. Selezionare **Utilizzo e quote**.

   ![Pulsante Utilizzo e quote](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   Hello utilizzo + quote pannello verrà visualizzata, varie risorse disponibili in tale sottoscrizione e hello percentuale della quota di hello che viene utilizzato per ogni risorsa.

   ![Utilizzo e quote](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a>Richiesta di altre risorse nella sottoscrizione
Se si raggiunge un limite di quota, il limite predefinito hello di una risorsa in una sottoscrizione può essere aumentato di limite massimo tooa, come descritto in [sottoscrizione di Azure e limiti dei servizi](https://docs.microsoft.com/azure/azure-subscription-service-limits).

La procedura mostra come toorequest aumentare di una quota tramite hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selezionare **Altri servizi**, quindi **Fatturazione** e **Utilizzo e quote**.
1. In utilizzo hello + pannello quote, selezionare hello **richiesta aumentare** pulsante.

   ![Pulsante Richiedi aumento](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. toocomplete e inviare la richiesta di hello, immettere le informazioni necessarie hello in tutte e tre le schede di hello **nuova richiesta di assistenza** form.

   ![Modulo Richiedi aumento](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

[Informazioni sui limiti di Azure e di aumentare](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) fornisce ulteriori informazioni su come contattare il supporto di Azure toorequest una quota aumento.



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>Passaggi successivi
* Esplorare hello [raccolta di modelli di DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/Samples).
