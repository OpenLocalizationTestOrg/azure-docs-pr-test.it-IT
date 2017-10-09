---
title: aaaSet di avvisi di fatturazione o carta di credito per le sottoscrizioni di Azure | Documenti Microsoft
description: "Viene descritto come è possibile impostare gli avvisi di fatturazione di Azure per evitare sorprese fatturazione."
keywords: avviso di credito, avviso di fatturazione
services: 
documentationcenter: 
author: vikdesai
manager: tonguyen
editor: 
tags: billing
ms.assetid: 9b7b3eeb-cd9d-4690-86a3-51b1e2a8974f
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: vikdesai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 711b9c72c59874792b0e229cdc5ec0fa517c24c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a>Impostare avvisi di fatturazione o di credito per le sottoscrizioni di Microsoft Azure
Se si è amministratore dell'Account di hello per una sottoscrizione di Azure, è possibile utilizzare hello Azure fatturazione avviso servizio avvisi di fatturazione toocreate personalizzati che consentono di monitorare e gestire attività di fatturazione per l'account di Azure.

Questo servizio è in anteprima, pertanto è necessario tooenable nella pagina di funzionalità di anteprima hello prima.

## <a name="set-hello-alert-threshold-and-email-recipients"></a>Impostare i destinatari di posta elettronica e di soglia avviso hello
1. Visitare [pagina di funzionalità di anteprima hello](https://account.windowsazure.com/PreviewFeatures) e abilitare **servizio di avvisi di fatturazione**.

1. Dopo aver ricevuto una conferma tramite posta elettronica hello che servizio di fatturazione hello è attivata per la sottoscrizione, visitare [pagina sottoscrizioni hello](https://account.windowsazure.com/Subscriptions) nel portale di account hello. Fare clic su sottoscrizione hello desidera toomonitor e quindi fare clic su **avvisi**.

    ![Schermata di vista delle sottoscrizioni hello del centro Account Azure, con gli avvisi evidenziato][Image1]

2. Successivamente, fare clic su **Aggiungi avviso** toocreate uno. È possibile impostare su un totale di cinque avvisi di fatturazione per sottoscrizione, con un'altra soglia e dei destinatari di posta elettronica tootwo per ogni avviso.

    ![Schermata di visualizzazione di avvisi, in cui è possibile aggiungere avviso hello][Image2]

3. Quando si aggiunge un avviso, assegnare un nome univoco, scegliere una soglia di spesa e scegliere hello indirizzi di posta elettronica in cui gli avvisi vengono inviati. Quando si imposta la soglia hello, è possibile scegliere un **totale fattura** o **credito monetario** da hello **avviso per** elenco. Per un totale di fatturazione, viene inviato un avviso quando spesa per la sottoscrizione supera la soglia di hello. Per un credito monetario, viene inviato un avviso quando il credito monetario scende sotto il limite di hello. I crediti monetari in genere applicano tooFree le sottoscrizioni di valutazione e Visual Studio.

    ![Schermata della visualizzazione di avvisi aggiunta hello, in cui è possibile configurare destinatari][Image3]

Azure supporta qualsiasi indirizzo di posta elettronica, ma non verificare il funzionamento dell'indirizzo di posta elettronica hello, pertanto si consiglia di controllare gli errori di battitura.

## <a name="check-on-your-alerts"></a>Controllare gli avvisi
Dopo aver impostato gli avvisi, hello centro Account li elenca e illustra il numero è più possibile configurare. Per ogni avviso, vedere hello data e l'ora di invio, se si tratta di un avviso per totale fattura o a crediti monetari e limite hello impostati. il formato di data e ora Hello è 24 ore coordinare UTC (Universal Time) e data hello è formato aaaa-mm-gg. Scegliere hello e firmarlo per un avviso in hello elenco tooedit o toodelete Cestino hello è.

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a>Avvisi di fatturazione per i clienti con contratto Enterprise (EA, Enterprise Agreement)
Nell'ambito di una registrazione i clienti EA possono usufruire di avvisi per ogni reparto, impostando le quote di spesa. Vedere [reparto spesa quote](https://ea.azure.com/helpdocs/departmentSpendingQuotas) nel portale tooget EA hello avviato.

## <a name="learn-more-about-azure-cost-management"></a>Altre informazioni sulla gestione dei costi in Azure
- Stima dei costi mediante hello [calcolatore dei costi](https://azure.microsoft.com/pricing/calculator/), [costo totale di calcolatrice di proprietà](https://aka.ms/azure-tco-calculator), e quando si aggiunge un servizio.
- [Verificare regolarmente uso e costi nel portale di Azure](billing-getting-started.md#costs).
- Attivare i [consigli di Azure Advisor sui costi](../advisor/advisor-cost-recommendations.md).

vedere, più toolearn [Guida alla gestione dei costi Azure](billing-getting-started.md).

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
