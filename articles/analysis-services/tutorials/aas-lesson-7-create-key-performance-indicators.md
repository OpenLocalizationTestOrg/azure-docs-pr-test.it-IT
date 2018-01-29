---
title: 'Esercitazione su Azure Analysis Services - Lezione 7: Creare indicatori di prestazioni chiave | Microsoft Docs'
description: Descrive come creare indicatori di prestazioni chiave nel progetto per l'esercitazione su Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 01/08/2018
ms.author: owend
ms.openlocfilehash: 8f25773541deba2a94d3adc0c9b61c1b90a90aa6
ms.sourcegitcommit: 176c575aea7602682afd6214880aad0be6167c52
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2018
---
# <a name="create-key-performance-indicators"></a>Creare indicatori di prestazioni chiave

In questa lezione verranno creati alcuni indicatori di prestazioni chiave (KPI). Gli indicatori KPI vengono usati per misurare le prestazioni di un valore, definito da una misura di *base*, rispetto a un valore di *destinazione*, anch'esso definito da una misura o da un valore assoluto. Nelle applicazioni client per la creazione di report, gli indicatori KPI possono fornire ai professionisti aziendali un modo rapido e semplice per comprendere i risultati aziendali positivi nel loro complesso o per identificare tendenze significative. Per altre informazioni, vedere [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular) (Indicatori di prestazioni chiave).
  
Tempo previsto per il completamento della lezione: **15 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 6: Creare misure](../tutorials/aas-lesson-6-create-measures.md).   
  
## <a name="create-key-performance-indicators"></a>Creare indicatori di prestazioni chiave  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a>Per creare un KPI InternetCurrentQuarterSalesPerformance  
  
1.  Nella finestra di progettazione dei modelli fare clic sulla tabella **FactInternetSales**.  
  
2.  Nella griglia delle misure fare clic su una cella vuota.  
  
3.  Nella barra della formula sopra la tabella digitare la formula seguente: 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    Questa misura viene usata come misura di base per l'indicatore KPI.  
  
4.  Nella griglia delle misure fare clic con il pulsante destro del mouse su **InternetCurrentQuarterSalesPerformance** > **Crea KPI**.   
  
5.  Nella finestra di dialogo Indicatore di prestazioni chiave (KPI) selezionare **Valore assoluto** in **Destinazione** e quindi digitare **1,1**.  
  
7.  Nel campo del dispositivo di scorrimento a sinistra (in basso), digitare **1** e quindi nel campo del dispositivo di scorrimento a destra (in alto) digitare **1,07**.  
  
8.  In **Seleziona stile icona** selezionare l'icona a forma di rombo (rossa), di triangolo (gialla) o di cerchio (verde).
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > Si noti l'etichetta **Descrizioni** espandibile sotto gli stili di icona disponibili. Usare descrizioni per i vari elementi KPI, in modo che siano più facilmente identificabili nelle applicazioni client.  
  
9. Fare clic su **OK** per completare l'indicatore KPI.  
  
    Nella griglia delle misure notare l'icona accanto alla misura **InternetCurrentQuarterSalesPerformance**. Questa icona indica che la misura funge da valore di base per un indicatore KPI.  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a>Per creare un KPI InternetCurrentQuarterMarginPerformance  
  
1.  Nella griglia delle misure per la tabella **FactInternetSales** fare clic su una cella vuota.  
  
2.  Nella barra della formula sopra la tabella digitare la formula seguente:  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  Fare clic con il pulsante destro del mouse su **InternetCurrentQuarterMarginPerformance** > **Crea KPI**.  
  
4.  Nella finestra di dialogo Indicatore di prestazioni chiave (KPI) selezionare **Valore assoluto** in **Destinazione** e quindi digitare **1,25**.   
  
5.  Nel campo del dispositivo di scorrimento a sinistra (in basso) scorrere fino a quando non viene visualizzato il valore **0,8** e quindi fare scorrere il dispositivo di scorrimento a destra (in alto) fino a quando non viene visualizzato il valore **1,03** nel campo.  
  
6.  In **Seleziona stile icona** selezionare l'icona a forma di rombo (rossa), di triangolo (gialla) o di cerchio (verde) e quindi fare clic su **OK**.  
  
## <a name="whats-next"></a>Passaggi successivi
[Lezione 8: Creare prospettive](../tutorials/aas-lesson-8-create-perspectives.md).
  
  
