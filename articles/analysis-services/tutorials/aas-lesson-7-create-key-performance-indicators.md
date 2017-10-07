---
titolo: aaa "lezione dell'esercitazione di Azure Analysis Services 7: creare indicatori di prestazioni chiave | Descrizione di "Microsoft Docs: viene descritto come indicatori di prestazioni chiave toocreate in hello progetto tutorial Azure Analysis Services. servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '

ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 26/05/2017: owend
---
# <a name="lesson-7-create-key-performance-indicators"></a>Lezione 7: Creare indicatori di prestazioni chiave

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In questa lezione verranno creati alcuni indicatori di prestazioni chiave (KPI). Gli indicatori KPI sono utilizzati toogauge prestazioni di un valore definito da un *Base* misura, contro un *destinazione* definito anch'esso da una misura o da un valore assoluto. In applicazioni client di reporting, gli indicatori KPI possono fornire ai professionisti di business toounderstand un modo semplice e rapido un riepilogo delle tendenze di esito positivo o tooidentify business. vedere, più toolearn [gli indicatori KPI](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)
  
Stimato toocomplete ora questa lezione: **15 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 6: creare misure](../tutorials/aas-lesson-6-create-measures.md).   
  
## <a name="create-key-performance-indicators"></a>Creare indicatori di prestazioni chiave  
  
#### <a name="toocreate-an-internetcurrentquartersalesperformance-kpi"></a>un KPI InternetCurrentQuarterSalesPerformance toocreate  
  
1.  In Progettazione modelli di hello, fare clic su hello **FactInternetSales** tabella.  
  
2.  Nella griglia delle misure hello, fare clic su una cella vuota.  
  
3.  Nella barra della formula hello, sopra la tabella hello, digitare hello formula seguente: 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    Questa misura viene utilizzata come misura di Base hello per hello indicatore KPI.  
  
4.  Fare clic con il pulsante destro del mouse su **InternetCurrentQuarterSalesPerformance** > **Crea KPI**.   
  
5.  Nella finestra di dialogo indicatore di prestazioni chiave (KPI) hello in **destinazione** selezionare **valore assoluto**, quindi digitare **1.1**.  
  
7.  Nel campo hello dispositivo di scorrimento sinistro (in basso) digitare **1**, quindi nel dispositivo di scorrimento destro (in alto) hello digitare **1.07**.  
  
8.  In **Seleziona stile icona**, selezionare triangolo a rombo (rosso), hello (giallo) o cerchio tipo di icona (verde).
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > Hello avviso espandibile **descrizioni** etichetta di sotto di stili di icona disponibili hello. Utilizzare le descrizioni per hello vari KPI elementi toomake li facilitare l'identificazione nelle applicazioni client.  
  
9. Fare clic su **OK** toocomplete hello indicatore KPI.  
  
    Nella griglia delle misure hello, si noti hello icona Avanti toohello **InternetCurrentQuarterSalesPerformance** misura. Questa icona indica che la misura funge da valore di base per un indicatore KPI.  
  
#### <a name="toocreate-an-internetcurrentquartermarginperformance-kpi"></a>un KPI InternetCurrentQuarterMarginPerformance toocreate  
  
1.  Nella griglia delle misure hello hello **FactInternetSales** tabella, fare clic su una cella vuota.  
  
2.  Nella barra della formula hello, sopra la tabella hello, digitare hello formula seguente:  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  Fare clic con il pulsante destro del mouse su **InternetCurrentQuarterMarginPerformance** > **Crea KPI**.  
  
4.  Nella finestra di dialogo indicatore di prestazioni chiave (KPI) hello in **destinazione** selezionare **valore assoluto**, quindi digitare **1.25**.   
  
5.  Nel campo del dispositivo di scorrimento sinistro (in basso) hello, scorrere fino a quando non viene visualizzato il campo hello **0,8**, e quindi hello diapositiva destro campo dispositivo di scorrimento (alto), fino a quando non viene visualizzato il campo hello **1.03**.  
  
6.  In **Seleziona stile icona**selezionare hello a forma di rombo (rosso), triangolo (giallo), il tipo di icona cerchio (verde) e quindi fare clic su **OK**.  
  
## <a name="whats-next"></a>Passaggi successivi
[Lezione 8: Creare prospettive](../tutorials/aas-lesson-8-create-perspectives.md).
  
  
