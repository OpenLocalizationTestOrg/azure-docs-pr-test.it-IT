---
titolo: aaa "lezione supplementare di Azure Analysis Services tutorial: righe di dettaglio | Descrizione di "Microsoft Docs: viene descritto come toocreate un espressione di righe di dettaglio in hello Azure Analysis Services tutorial.
servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '

ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 26/05/2017: owend
---
# <a name="supplemental-lesson---detail-rows"></a>Lezione supplementare: Righe di dettaglio

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In questa lezione supplementare, utilizzare Editor DAX toodefine hello un'espressione di righe di dettaglio personalizzata. Un'espressione di righe di dettaglio è una proprietà su una misura, fornendo agli utenti finali di ulteriori informazioni sui risultati di hello aggregato di una misura. 
  
Stimato toocomplete ora questa lezione: **10 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
L'argomento di questa lezione supplementare fa parte di un'esercitazione sulla creazione di modelli tabulari. Prima di eseguire attività di hello in questa lezione supplementare, è necessario avere completato tutte le lezioni precedenti o dispone di un progetto di modello di esempio Adventure Works Internet Sales completato.  
  
## <a name="what-do-we-need-toosolve"></a>Che cosa dobbiamo toosolve?
Esaminiamo i dettagli di hello della misura InternetTotalSales, prima di aggiungere un'espressione di righe di dettaglio.

1.  In SSDT, fare clic su hello **modello** menu > **analizza in Excel** tooopen Excel e creare una tabella pivot vuota.
  
2.  In **PivotTable Fields**, aggiungere hello **InternetTotalSales** misure da tabella FactInternetSales hello troppo**valori**, **CalendarYear**dalla hello DimDate tabella troppo**colonne**, e **EnglishCountryRegionName** troppo**righe**. La tabella pivot subito produce risultati aggregati da misure InternetTotalSales hello per le aree e anno. 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. Nella tabella pivot hello, fare doppio clic su un valore aggregato per un anno e un nome di area. Di seguito si fa doppio clic sul valore hello per l'Australia e hello anno 2014. Viene aperto un nuovo foglio contenente alcuni dati, ma non molto utili.

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
Ciò che si desidera toosee qui è una tabella contenente colonne e righe di dati che contribuiscono toohello aggregati i risultati di una misura InternetTotalSales. toodo, che è possibile aggiungere un'espressione di righe di dettaglio come proprietà della misura hello.

## <a name="add-a-detail-rows-expression"></a>Aggiungere un'espressione di righe di dettaglio

#### <a name="toocreate-a-detail-rows-expression"></a>toocreate un'espressione di righe di dettaglio 
  
1. In SSDT, nella griglia delle misure della tabella FactInternetSales hello, fare clic su hello **InternetTotalSales** misura. 

2. In **proprietà** > **espressione righe di dettaglio**, fare clic su prova editor pulsante tooopen prova Editor DAX.

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. Nell'Editor DAX immettere hello espressione seguente:

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    Questa espressione consente di specificare i nomi, le colonne e misure da tabella FactInternetSales hello e le tabelle correlate vengono restituiti quando un utente fa doppio clic su un risultato aggregato in una tabella pivot o un report.

4. In Excel, Elimina foglio hello creato nel passaggio 3, quindi fare doppio clic su un valore aggregato. Questa volta, con una proprietà di espressione di righe di dettaglio definita per la misura hello, un nuovo foglio apre che contiene dati molto più utili.

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. Ridistribuire il modello.

  
## <a name="see-also"></a>Vedere anche  
[SELECTCOLUMNS Function (DAX) (Funzione DAX SELECTCOLUMNS)](https://msdn.microsoft.com/library/mt761759.aspx)   
[Lezione supplementare: Sicurezza dinamica](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[Lezione supplementare: Gerarchie incomplete](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
