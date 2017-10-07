---
titolo: aaa "lezione dell'esercitazione di Azure Analysis Services 5: creare colonne calcolate | Descrizione di Microsoft Docs": descrive toocreate calcolo di colonne nel progetto di esercitazione di hello Azure Analysis Services. servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '

ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 01/06/2017: owend
---
# <a name="lesson-5-create-calculated-columns"></a>Lezione 5: Creare colonne calcolate

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In questa lezione vengono creati dati nel modello aggiungendo colonne calcolate. È possibile creare colonne calcolate (come le colonne personalizzate) quando si usa recupera dati, utilizzando hello Editor di Query o nel tipo di finestra di progettazione modello hello eseguire qui. vedere, più toolearn [le colonne calcolate](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).
  
Vengono create cinque nuove colonne calcolate in tre tabelle diverse. Hello passaggi sono leggermente diversi per ogni attività che mostra esistono diversi modi toocreate colonne, rinominarle e posizionarli in diverse posizioni in una tabella.  

Questa è anche la prima lezione in cui si usano espressioni DAX (Data Analysis Expressions). DAX è un linguaggio speciale per la creazione di espressioni per formule altamente personalizzabili per i modelli tabulari. In questa esercitazione, utilizzare le colonne calcolate toocreate DAX, misure e filtri di ruolo. vedere, più toolearn [DAX nei modelli tabulari](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular). 
  
Stimato toocomplete ora questa lezione: **15 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 4: creare relazioni](../tutorials/aas-lesson-4-create-relationships.md). 
  
## <a name="create-calculated-columns"></a>Creare colonne calcolate  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a>Creare una colonna calcolata di MonthCalendar tabella DimDate hello  
  
1.  Fare clic su hello **modello** menu > **vista modello** > **vista dati**.  
  
    Le colonne calcolate possono essere create solo tramite Progettazione modelli di hello in vista dati.  
  
2.  In Progettazione modelli di hello, fare clic su hello **DimDate** tabella (scheda).  
  
3.  Pulsante destro del mouse hello **CalendarQuarter** intestazione di colonna e quindi fare clic su **Inserisci colonna**.  
  
    Una nuova colonna denominata **calcolato 1 colonna** è toohello inserito a sinistra di hello **Calendar Quarter** colonna.  
  
4.  Nella barra della formula hello sopra la tabella hello, digitare hello seguente formula DAX: consente il completamento automatico si digita hello nomi completi di colonne e tabelle e gli elenchi di hello funzioni disponibili.  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    I valori vengono quindi popolati per tutte le righe di hello nella colonna calcolata hello. È possibile scorrere verso il basso nella tabella hello, vedrai che le righe possono avere valori diversi per questa colonna, in base ai dati hello in ogni riga.    
  
5.  Rinominare questa colonna troppo**MonthCalendar**. 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
colonna calcolata di MonthCalendar Hello fornisce un nome ordinabile per mese.  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a>Creare una colonna calcolata DayOfWeek tabella DimDate hello  
  
1.  Con hello **DimDate** ancora attiva, fare clic sul hello **colonna** menu e quindi fare clic su **Aggiungi colonna**.  
  
2.  Nella barra della formula hello, digitare hello formula seguente:  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    Al termine della compilazione hello formula, premere INVIO. Hello nuova colonna viene aggiunta a destra della tabella hello toohello.  
  
3.  Rinominare la colonna hello troppo**DayOfWeek**.  
  
4.  Fare clic sull'intestazione di colonna hello e quindi trascinare la colonna hello tra hello **EnglishDayNameOfWeek** colonna e hello **DayNumberOfMonth** colonna.  
  
    > [!TIP]  
    > Lo spostamento delle colonne nella tabella rende più semplice toonavigate.  
  
colonna calcolata di Hello DayOfWeek fornisce un nome ordinabile per giorno hello della settimana.  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a>Creare una colonna calcolata ProductSubcategoryName nella tabella DimProduct hello  
  
  
1.  In hello **DimProduct** tabella, toohello a destra della tabella di hello di scorrimento. Colonna più a destra di preavviso hello è denominata **Aggiungi colonna** (in corsivo), fare clic sull'intestazione di colonna hello.  
  
2.  Nella barra della formula hello, digitare hello formula seguente:  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  Rinominare la colonna hello troppo**ProductSubcategoryName**.  
  
colonna calcolata di Hello ProductSubcategoryName è toocreate utilizzata una gerarchia nella tabella DimProduct hello, che include i dati dalla colonna EnglishProductSubcategoryName hello nella tabella DimProductSubcategory hello. Le gerarchie non possono essere estese a più di una tabella. Le gerarchie verranno create più avanti nella lezione 9.  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a>Creare una colonna calcolata ProductCategoryName nella tabella DimProduct hello  
  
1.  Con hello **DimProduct** ancora attiva, fare clic sul hello **colonna** menu e quindi fare clic su **Aggiungi colonna**.  
  
2.  Nella barra della formula hello, digitare hello formula seguente:  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  Rinominare la colonna hello troppo**ProductCategoryName**.  
  
colonna calcolata di ProductCategoryName Hello è toocreate utilizzata una gerarchia nella tabella DimProduct hello, che include dati dalla colonna EnglishProductCategoryName hello hello DimProductCategory tabella. Le gerarchie non possono essere estese a più di una tabella.  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a>Creare una colonna calcolata Margin nella tabella FactInternetSales hello  
  
1.  In Progettazione modelli di hello, selezionare hello **FactInternetSales** tabella.  
  
2.  Creare una nuova colonna calcolata tra hello **SalesAmount** colonna e hello **TaxAmt** colonna.  
  
3.  Nella barra della formula hello, digitare hello formula seguente:  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  Rinominare la colonna hello troppo**margine**.  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    colonna calcolata Margin Hello è tooanalyze utilizzati i margini di profitto per ogni vendita.  
  
## <a name="whats-next"></a>Passaggi successivi
[Lezione 6: Creare misure](../tutorials/aas-lesson-6-create-measures.md).
  
  
  
