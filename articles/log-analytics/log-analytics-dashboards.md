---
title: un dashboard personalizzato in Azure Log Analitica aaaCreate | Documenti Microsoft
description: Questa Guida consente di comprendere come i dashboard di Log Analitica possono visualizzare tutte le ricerche log salvate, offrendo una singola obiettivo tooview l'ambiente.
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 73fcf131a91c743d473f37d5a40d52eaf78a7ba3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a>Creare un dashboard personalizzato da usare in Log Analytics

>[!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi è possibile creare nuovi dashboard o modificare dashboard esistenti. 

Questa Guida consente di comprendere come i dashboard di Log Analitica possono visualizzare tutte le ricerche log salvate, offrendo una singola obiettivo tooview l'ambiente.

![Dashboard di esempio](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

Tutti i dashboard personalizzati hello creati nel portale OMS hello sono disponibili anche in App per dispositivi mobili OMS hello. Vedere hello seguenti pagine per altre informazioni sulle App hello.

* [App per dispositivi mobili OMS da hello Microsoft Store](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [App OMS per dispositivi mobili in Apple iTunes](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![dashboard mobile](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a>Come si crea un dashboard?
toobegin, pagina Overview di OMS toohello passare. Si noterà hello **My Dashboard** riquadro a sinistra di hello. Fare clic toodrill verso il basso nel dashboard.

![Panoramica](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a>Aggiunta di un riquadro
I riquadri dei dashboard vengono compilati in base alle ricerche log salvate. OMS offre diverse ricerche nei log salvate predefinite che ne consentono un utilizzo immediato. Tale struttura i passaggi seguenti hello utilizzare come toobegin.

Nella visualizzazione My Dashboard hello, fare semplicemente clic **Personalizza** tooenter la modalità di personalizzazione.

![Illustrazione](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 Pannello Hello visualizzato sul lato destro hello della pagina hello Mostra tutte le ricerche log salvate dell'area di lavoro. toovisualize ricerca di un registro salvato come un riquadro, passare il mouse su una ricerca salvata e quindi fare clic su hello **più** simbolo.

![Aggiunta di riquadri 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

Quando si fa clic su hello **più** symbol, un nuovo riquadro viene visualizzato nella visualizzazione My Dashboard hello.

![Aggiunta di riquadri 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a>Modifica di un riquadro
Nella visualizzazione My Dashboard hello, fare semplicemente clic **Personalizza** tooenter la modalità di personalizzazione. Fare clic su riquadro hello da tooedit. riquadro di destra Hello diventa tooedit e fornisce diverse opzioni:

![Modifica di un riquadro](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Modifica di un riquadro](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a>Tipi di visualizzazione dei riquadri
Esistono tre tipi di riquadro visualizzazioni toochoose da:

| tipo di grafico | funzione |
| --- | --- |
| ![Grafico a barre](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |Visualizza una sequenza temporale dei risultati della ricerca log salvata sotto forma di grafico a barre o un elenco dei risultati per campo, a seconda che i risultati vengano aggregati o meno in base a un campo. |
| ![metrica](./media/log-analytics-dashboards/oms-dashboards-metric.png) |Il risultato totale della ricerca nei log viene visualizzato sotto forma di numero in un riquadro. Metrica riquadri consentono di tooset una soglia che, quando viene raggiunta la soglia hello evidenziazione hello riquadro. |
| ![line](./media/log-analytics-dashboards/oms-dashboards-line.png) |Visualizza una sequenza temporale dei risultati della ricerca log salvata con i relativi valori sotto forma di grafico a linee. |

### <a name="threshold"></a>Soglia
È possibile creare una soglia in un riquadro usando la visualizzazione Metrica hello. Scegliere toocreate un valore di soglia nel riquadro di hello. Scegliere se il riquadro hello toohighlight quando il valore di hello è sopra o sotto la soglia di hello scelto, quindi impostare valore soglia hello.

## <a name="organizing-hello-dashboard"></a>Organizzazione hello dashboard
tooorganize dashboard, passare a visualizzazione My Dashboard toohello e fare clic su **Personalizza** tooenter la modalità di personalizzazione. Fare clic e trascinare riquadro hello desiderato toomove e spostarlo toowhere desiderato toobe del riquadro.

![Organizzazione del dashboard](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a>Rimozione di un riquadro
tooremove un riquadro, passare a visualizzazione My Dashboard toohello e fare clic su **Personalizza** tooenter la modalità di personalizzazione. Riquadro hello selezionare tooremove desiderato, quindi nel riquadro di destra hello selezionare **Remove Tile**.

![Rimozione di un riquadro](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a>Passaggi successivi
* Creare [avvisi](log-analytics-alerts.md) notifiche toogenerate Log Analitica e tooremediate problemi.
