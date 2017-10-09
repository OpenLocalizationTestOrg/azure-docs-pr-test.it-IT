---
title: scala aaaVertically macchina virtuale di Azure con automazione di Azure | Documenti Microsoft
description: Come toovertically ridimensionare una macchina virtuale Linux negli avvisi toomonitoring risposta con automazione di Azure
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dcee199e-fa25-44d5-9b25-df564cee9b45
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: singhkay
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee4c1c33a588bd907d107f1828380a8afdaa725e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-azure-linux-virtual-machine-with-azure-automation"></a>Scalabilità verticale di macchine virtuali di Linux in Azure tramite Automazione di Azure
La scalabilità verticale è il processo di hello di aumento o diminuzione risorse hello di un computer nel carico di lavoro di risposta toohello. In Azure può essere eseguita mediante la modifica delle dimensioni hello di hello macchina virtuale. Ciò consente in hello seguenti scenari

* Se non viene utilizzato spesso hello macchina virtuale, è possibile ridimensionarla verso il basso tooreduce dimensioni più piccole tooa i costi mensili
* Se hello macchina virtuale viene visualizzato un carico di picco, può essere ridimensionato tooa tooincrease di dimensioni maggiori capacità

struttura Hello per hello passaggi tooaccomplish si tratta di seguito

1. Programma di installazione tooaccess di automazione di Azure le macchine virtuali
2. Importazione dei runbook di hello scalabilità verticale di automazione di Azure alla sottoscrizione di
3. Aggiungere un runbook tooyour webhook
4. Aggiungere un avviso tooyour macchina virtuale

> [!NOTE]
> A causa delle dimensioni di hello hello prima macchina virtuale, le dimensioni di hello possono essere ridimensionato, potrebbe risultare limitato a causa della disponibilità toohello di hello altre dimensioni cluster hello macchina virtuale corrente viene distribuito. In hello pubblicato il runbook di automazione usato in questo articolo si occuperà del case e applicare la scalabilità solo all'interno di hello di sotto di coppie di dimensioni di macchina virtuale. Ciò significa che una macchina virtuale Standard_D1v2 verranno non improvvisamente ridimensionati tooStandard_G5 o scalabilità verso il basso tooBasic_A0.
> 
> | coppie di ridimensionamento di dimensioni delle macchine virtuali |  |
> | --- | --- |
> | Basic_A0 |Basic_A4 |
> | Standard_A0 |Standard_A4 |
> | Standard_A5 |Standard_A7 |
> | Standard_A8 |Standard_A9 |
> | Standard_A10 |Standard_A11 |
> | Standard_D1 |Standard_D4 |
> | Standard_D11 |Standard_D14 |
> | Standard_DS1 |Standard_DS4 |
> | Standard_DS11 |Standard_DS14 |
> | Standard_D1v2 |Standard_D5v2 |
> | Standard_D11v2 |Standard_D14v2 |
> | Standard_G1 |Standard_G5 |
> | Standard_GS1 |Standard_GS5 |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a>Programma di installazione tooaccess di automazione di Azure le macchine virtuali
Hello occorre innanzitutto toodo è creare un account di automazione di Azure che ospiterà hello runbook utilizzato tooscale hello Set di scalabilità della macchina virtuale istanze. Servizio automazione hello introdotto di recente funzionalità "Esegui come account" hello che rende impostazione hello dell'entità servizio per l'esecuzione automatica hello runbook per conto dell'utente hello molto semplice. È possibile leggere altre informazioni nell'articolo hello riportato di seguito:

* [Autenticare runbook con account RunAs di Azure](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>Importazione dei runbook di hello scalabilità verticale di automazione di Azure alla sottoscrizione di
runbook Hello che sono necessari per la scalabilità verticale della macchina virtuale sono già pubblicati in hello raccolta di Runbook di automazione di Azure. Sarà necessario tooimport nella sottoscrizione. È possibile apprendere come tooimport runbook leggendo hello articolo seguente.

* [Raccolte di runbook e moduli per l'automazione di Azure](../../automation/automation-runbook-gallery.md)

i runbook Hello necessario toobe importati sono illustrati nella figura hello seguente

![Importazione runbook](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a>Aggiungere un runbook tooyour webhook
Dopo aver importato i runbook hello è necessario un runbook toohello webhook tooadd in modo che può essere attivata da un avviso da una macchina virtuale. dettagli di Hello per la creazione di un webhook per i Runbook possono essere letti qui

* [Webhook di Automazione di Azure](../../automation/automation-webhooks.md)

Assicurarsi di copiare hello webhook prima della chiusura di finestra di dialogo webhook hello perché sarà necessaria nella sezione successiva hello.

## <a name="add-an-alert-tooyour-virtual-machine"></a>Aggiungere un avviso tooyour macchina virtuale
1. Selezionare le impostazioni della macchina virtuale
2. Selezionare "Regole di avviso"
3. Selezionare "Aggiungi avviso"
4. Selezionare un avviso di hello toofire metrica in
5. Selezionare una condizione, che una volta soddisfatti verrà causare toofire avviso hello
6. Selezionare una soglia per la condizione hello nel passaggio 5. toobe soddisfatte
7. Selezionare un periodo di su quale hello monitoraggio del servizio verrà verificato per la condizione di hello e soglia in passaggi 5 e 6
8. Incollare in webhook hello copiato dalla sezione precedente hello.

![Aggiungere avvisi tooVirtual 1 computer](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Aggiungere avvisi tooVirtual Machine 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

