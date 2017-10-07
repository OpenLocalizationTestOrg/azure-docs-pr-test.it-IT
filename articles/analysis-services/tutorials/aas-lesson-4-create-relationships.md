---
titolo: aaa "lezione dell'esercitazione di Azure Analysis Services 4: creare relazioni | Descrizione di "Microsoft Docs: viene descritto come relazioni toocreate in hello progetto tutorial Azure Analysis Services. servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '

ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 26/05/2017: owend
---
# <a name="lesson-4-create-relationships"></a>Lezione 4: Creare relazioni

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In questa lezione si verificare hello relazioni create automaticamente durante l'importazione dei dati e aggiungono nuove relazioni tra tabelle diverse. Una relazione è una connessione tra due tabelle che stabilisce la modalità dati hello in tali tabelle devono essere correlati. Ad esempio, nella tabella DimProduct hello e tabella DimProductSubcategory hello hanno una relazione basata su fatti hello che ogni prodotto appartiene tooa subcategory. vedere, più toolearn [relazioni](https://docs.microsoft.com/sql/analysis-services/tabular-models/relationships-ssas-tabular).
  
Stimato toocomplete ora questa lezione: **10 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 3: contrassegna come tabella data](../tutorials/aas-lesson-3-mark-as-date-table.md). 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Esaminare le relazioni esistenti e aggiungere nuove relazioni  
Quando sono stati importati dati usando recupera dati, sarà possibile ottenere sette tabelle dal database AdventureWorksDW2014 hello. In genere, quando si importano dati da un'origine relazionale, le relazioni esistenti vengono importate automaticamente insieme ai dati hello. Tuttavia, prima di procedere alla creazione del modello è necessario verificare che le relazioni create tra le tabelle siano appropriate. Per gli scopi di questa esercitazione vengono aggiunte tre nuove relazioni.  
  
#### <a name="tooreview-existing-relationships"></a>relazioni esistenti tooreview  
  
1.  Fare clic su hello **modello** menu > **vista modello** > **vista diagramma**.  

    Hello Progettazione modelli viene ora visualizzato nella vista diagramma, un formato grafico la visualizzazione di tutte le tabelle di hello importate, con linee tra di essi. linee di Hello tra le tabelle indicano le relazioni di hello che sono state create automaticamente durante l'importazione dei dati hello.
    
    ![aas-lesson4-diagram](../tutorials/media/aas-lesson4-diagram.png)
  
    Includere la maggior parte delle tabelle di hello possibile tramite i controlli della mini mappa nell'angolo inferiore destro hello di progettazione di modelli di hello. È possibile anche fare clic su e trascinare posizioni toodifferent tabelle, riunire più vicino a tabelle o inserirli in un ordine particolare. Spostamento di tabelle non influenza le relazioni di hello già tra le tabelle di hello. tooview tutte le colonne di hello in una determinata tabella, fare clic e trascinare un tooexpand bordo di tabella o renderla più piccola.  
  
2.  Fare clic hello linea continua tra hello **DimCustomer** tabella e hello **DimGeography** tabella. linea continua di Hello tra queste due tabelle viene illustrata che questa relazione è attiva, vale a dire, che viene utilizzato per impostazione predefinita durante il calcolo delle formule DAX.  
  
    Hello preavviso **GeographyKey** colonna hello **DimCustomer** tabella e hello **GeographyKey** colonna hello **DimGeography** tabella appaiono ora entrambe all'interno di una casella. Queste colonne vengono utilizzate nella relazione hello. Hello proprietà della relazione sono ora visualizzate nella hello **proprietà** finestra.  
  
    > [!TIP]  
    > Inoltre toousing hello Progettazione modelli in vista diagramma, è inoltre possibile utilizzare hello Gestisci relazioni della finestra di dialogo tooshow hello le relazioni tra tutte le tabelle in un formato di tabella. In Esplora modelli tabulari fare clic con il pulsante destro del mouse su **Relazioni** > **Gestisci relazioni**.
  
3.  Verificare hello segue le relazioni siano stata creata quando ognuna delle tabelle di hello è stata importata dal database AdventureWorksDW hello:  
  
    |Attivo|Table|Tabella di ricerca correlata|  
    |----------|---------|------------------------|  
    |Sì|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |Sì|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |Sì|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |Sì|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |Sì|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    Se sono presenti relazioni hello mancante, verificare che il modello includa le tabelle seguenti hello: DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory e FactInternetSales. Se hello stessa connessione all'origine dati vengono importati in tabelle separano volte, tutte le relazioni tra tali tabelle non vengono create e devono essere create manualmente.  

### <a name="take-a-closer-look"></a>Dettagli del diagramma e delle relazioni
Nella vista diagramma, si noti una freccia, un asterisco e un numero di righe hello che mostrano la relazione hello tra tabelle.

![aas-lesson4-line](../tutorials/media/aas-lesson4-line.png)

freccia di Hello indica la direzione del filtro hello. asterisco Hello mostra che questa tabella è hello lato "molti" in cardinalità della relazione hello e hello viene illustrato in questa tabella è uno lato di hello di relazione hello. Se è necessario tooedit una relazione. ad esempio, modificare la direzione del filtro o la cardinalità della relazione hello, fare doppio clic sulla finestra di hello relazione riga tooopen hello Modifica relazione.

![aas-lesson4-edit](../tutorials/media/aas-lesson4-edit.png)

Queste funzionalità sono concepite per la modellazione dei dati avanzate e ambito hello all'esterno di questa esercitazione. vedere, più toolearn [bidirezionale tra i filtri per i modelli tabulari in Analysis Services](https://docs.microsoft.com/sql/analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services).

In alcuni casi, potrebbe essere toocreate relazioni aggiuntive tra le tabelle del modello di toosupport determinata logica di business. Per questa esercitazione, è necessario toocreate tre relazioni aggiuntive tra tabella FactInternetSales hello e la tabella DimDate hello.  
  
#### <a name="tooadd-new-relationships-between-tables"></a>tooadd nuove relazioni tra tabelle  
  
1.  In Progettazione modelli hello in hello **FactInternetSales** tabella, fare clic e tenere premuto hello **OrderDate** colonna, quindi trascinare hello cursore toohello **data** colonna hello  **DimDate** tabella e infine rilasciare.  

    Verrà visualizzata di una linea a tinta unita che è stata creata una relazione attiva tra hello **OrderDate** colonna hello **Internet Sales** tabella e hello **data** colonna hello **Data** tabella. 
  
      ![aas-lesson4-new](../tutorials/media/aas-lesson4-new.png) 
  
    > [!NOTE]  
    > Quando si creano relazioni, hello cardinalità e filtro la direzione tra la tabella primaria hello e tabella di ricerca correlata hello viene selezionata automaticamente.  
  
2.  In hello **FactInternetSales** tabella, fare clic e tenere premuto hello **DueDate** colonna, quindi trascinare hello cursore toohello **data** colonna hello **DimDate** tabella e infine rilasciare.  
  
    Viene visualizzato di una linea punteggiata che è stata creata una relazione inattiva tra hello **DueDate** colonna hello **FactInternetSales** tabella e hello **data** colonna Hello **DimDate** tabella. È possibile creare più relazioni tra le tabelle, ma può essere attiva una sola relazione alla volta. Relazioni inattive possono essere rese tooperform active speciali aggregazioni personalizzate espressioni DAX.  
  
3.  Creare infine un'ultima relazione. In hello **FactInternetSales** tabella, fare clic e tenere premuto hello **ShipDate** colonna, quindi trascinare hello cursore toohello **data** colonna hello **DimDate** tabella e infine rilasciare.  
    
     ![aas-lesson4-newinactive](../tutorials/media/aas-lesson4-newinactive.png)
  
## <a name="whats-next"></a>Passaggi successivi
[Lezione 5: Creare colonne calcolate](../tutorials/aas-lesson-5-create-calculated-columns.md).
  
  
  
