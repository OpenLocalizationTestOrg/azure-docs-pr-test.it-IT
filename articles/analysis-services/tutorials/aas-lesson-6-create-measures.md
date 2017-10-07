---
titolo: aaa "lezione dell'esercitazione di Azure Analysis Services 6: creare misure | Descrizione di "Microsoft Docs: viene descritto come toocreate misure nel progetto di esercitazione di hello Azure Analysis Services. servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '

ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 01/06/2017: owend
---
# <a name="lesson-6-create-measures"></a>Lezione 6: Creare misure

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In questa lezione, creare misure toobe inclusi nel modello. Toohello simile calcolata colonne che è stato creato, una misura è un calcolo creato utilizzando una formula DAX. Tuttavia, a differenza delle colonne calcolate, le misure vengono valutate in base a un *filtro* selezionato dall'utente, Ad esempio, una determinata colonna o sezionamento aggiunto campo etichette di riga toohello in una tabella pivot. Viene quindi calcolato un valore per ogni cella nel filtro hello dalla misura hello applicato. Le misure sono calcoli potenti e flessibili che si desidera tooinclude in quasi tutti i modelli tabulari tooperform i calcoli dinamici sui dati numerici. vedere, più toolearn [misure](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).
  
le misure toocreate, utilizzare hello *griglia delle misure*. Per impostazione predefinita, ogni tabella ha una griglia delle misure vuota, ma di solito non si creano misure per ogni tabella. la griglia delle misure Hello viene visualizzata sotto una tabella in Progettazione modelli di hello in vista dati. griglia delle misure hello toohide o Mostra per una tabella, fare clic su hello **tabella** menu e quindi fare clic su **Mostra griglia delle misure**.  
  
È possibile creare una misura facendo clic su una cella vuota nella griglia delle misure hello, e quindi digitando una formula DAX nella barra della formula hello. Quando fare clic su invio toocomplete hello formula, misura hello quindi viene visualizzato nella cella hello. È inoltre possibile creare misure utilizzando una funzione di aggregazione standard facendo clic su una colonna e quindi fare clic sul pulsante Somma automatica di hello (**∑**) sulla barra degli strumenti hello. Le misure create utilizzando funzionalità Somma automatica hello visualizzata nella cella della griglia di misure hello direttamente sotto la colonna hello, ma possono essere spostate.  
  
In questa lezione, creare misure sia immettendo una formula DAX nella barra della formula hello e la funzionalità Somma automatica hello.  
  
Stimato toocomplete ora questa lezione: **30 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 5: creare colonne calcolate](../tutorials/aas-lesson-5-create-calculated-columns.md).  
  
## <a name="create-measures"></a>Creare misure  
  
#### <a name="toocreate-a-dayscurrentquartertodate-measure-in-hello-dimdate-table"></a>una misura DaysCurrentQuarterToDate tabella DimDate hello toocreate  
  
1.  In Progettazione modelli di hello, fare clic su hello **DimDate** tabella.  
  
2.  Nella griglia delle misure hello, fare clic sulla cella vuota in alto a sinistra di hello.  
  
3.  Nella barra della formula hello, digitare hello formula seguente:  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    Cella superiore sinistra hello di notifica contiene ora un nome di misura, **DaysCurrentQuarterToDate**, seguito dal risultato di hello, **92**.
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    A differenza delle colonne calcolate, con le formule delle misure è possibile digitare il nome di misura hello, seguito da due punti, seguiti dall'espressione formula hello.

  
#### <a name="toocreate-a-daysincurrentquarter-measure-in-hello-dimdate-table"></a>una misura DaysInCurrentQuarter tabella DimDate hello toocreate  
  
1.  Con hello **DimDate** ancora attiva in Progettazione modelli di hello, nella griglia delle misure hello, fare clic sulla cella vuota di hello sotto misura hello creata.  
  
2.  Nella barra della formula hello, digitare hello formula seguente:  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    Quando si crea un rapporto di confronto tra un periodo incompleto e hello periodo precedente. formula Hello deve calcolare proporzione hello del periodo di hello trascorsa e confrontarla toohello stesso proporzioni in hello periodo precedente. In questo caso, [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] fornisce hello proporzione in hello, trascorso il periodo corrente.  
  
#### <a name="toocreate-an-internetdistinctcountsalesorder-measure-in-hello-factinternetsales-table"></a>una misura InternetDistinctCountSalesOrder nella tabella FactInternetSales hello toocreate  
  
1.  Fare clic su hello **FactInternetSales** tabella.   
  
2.  Fare clic su hello **SalesOrderNumber** intestazione di colonna.  
  
3.  Sulla barra degli strumenti hello, fare clic su hello sulla freccia avanti toohello Somma automatica (**∑**) e quindi selezionare **DistinctCount**.  
  
    funzionalità Somma automatica Hello automaticamente creata una misura per la colonna selezionata da hello utilizzando una formula di aggregazione standard DistinctCount hello.  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  Nella griglia delle misure hello, fare clic su nuova misura hello e quindi in hello **proprietà** finestra, in **nome misura**, rinominare la misura hello troppo**InternetDistinctCountSalesOrder**. 
 
  
#### <a name="toocreate-additional-measures-in-hello-factinternetsales-table"></a>toocreate misure aggiuntive nella tabella FactInternetSales hello  
  
1.  La funzionalità Somma automatica hello, creare e denominare hello seguenti misure:  

    |Colonna|Nome misura|Somma automatica (∑)|Formula|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|Numero|=COUNTA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|Somma|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|Somma|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|Somma|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|Somma|=SUM([SalesAmount])|  
    |Margin|InternetTotalMargin|Somma|=SUM([Margin])|  
    |TaxAmt|InternetTotalTaxAmt|Somma|=SUM([TaxAmt])|  
    |Freight|InternetTotalFreight|Somma|=SUM([Freight])|  
  
2.  Facendo clic su una cella vuota nella griglia delle misure hello e utilizzando la barra della formula hello, creare e le misure seguenti hello nome nell'ordine:  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
Le misure create per la tabella FactInternetSales hello possono essere utilizzato tooanalyze dati finanziari critici, ad esempio vendite, costi e margine di profitto per elementi definiti dal filtro selezionato di hello utente.  
  
## <a name="whats-next"></a>Passaggi successivi
[Lezione 7: Creare indicatori di prestazioni chiave](../tutorials/aas-lesson-7-create-key-performance-indicators.md).  

  
