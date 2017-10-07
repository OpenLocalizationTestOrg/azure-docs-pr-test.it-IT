---
titolo: aaa "lezione dell'esercitazione di Azure Analysis Services 2: ottenere i dati | Descrizione di "Microsoft Docs: viene descritto come tooget e Importa dati in hello progetto tutorial Azure Analysis Services. servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '

ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 01/06/2017: owend
---

# <a name="lesson-2-get-data"></a>Lezione 2: Ottenere i dati

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In questa lezione, Usa Recupera dati in database di esempio tooconnect toohello AdventureWorksDW2014 SSDT, i dati selezionati, anteprima e filtro e quindi importare nell'area di lavoro modello.  
  
Con Recupera dati è possibile importare dati da un'ampia gamma di origini: database SQL di Azure, Oracle, Sybase, feed OData, Teradata, file e altro ancora. I dati possono essere recuperati anche tramite query, usando un'espressione di formula Power Query M.
  
Stimato toocomplete ora questa lezione: **10 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 1: creare un nuovo progetto di modello tabulare](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Creare una connessione  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a>un database toohello AdventureWorksDW2014 connessione toocreate  
  
1.  In Esplora modelli tabulari fare doppio clic su **Origini dati** > **Importa da origine dati**.  
  
    Verrà avviata recupera dati, che ti assisterà connessione origine dati di tooa. Se non viene visualizzato Esplora modelli tabulari, **Esplora**, fare doppio clic su **Model.bim** modello hello tooopen nella finestra di progettazione hello. 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  In Recupera dati fare clic su **Database** > **Database di SQL Server** > **Connetti**.  
  
3.  In hello **Database di SQL Server** finestra di dialogo, nella **Server**, digitare il nome di hello del server di hello in cui è installato il database di hello AdventureWorksDW2014 e quindi fare clic su **Connetti**.  

4.  Quando richiesto tooenter credenziali, è necessario che le credenziali di hello toospecify Analysis Services utilizza l'origine dei dati toohello tooconnect durante l'importazione e l'elaborazione dei dati. In **Modalità di rappresentazione** selezionare **Rappresenta account**, immettere le credenziali e quindi fare clic su **Connetti**. È consigliabile che utilizzare un account in cui è senza scadenza password hello.

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > Utilizzando un account utente di Windows e una password fornisce un metodo più sicuro hello di connessione origine dati di tooa.
  
5.  Nel Pannello di navigazione, selezionare hello **AdventureWorksDW2014** database e quindi fare clic su **OK**. Crea database toohello di connessione hello. 
  
6.  Nel Pannello di navigazione, selezionare hello casella di controllo per le tabelle seguenti hello: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, e **FactInternetSales**.  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
Dopo aver fatto clic su OK verrà aperto l'Editor di query. Nella sezione successiva hello, si seleziona solo i dati di hello desiderati tooimport.

  
## <a name="filter-hello-table-data"></a>Filtrare i dati della tabella hello  
Le tabelle nel database di esempio hello AdventureWorksDW2014 contengono dati non sono necessario tooinclude nel modello. Quando possibile, è opportuno toofilter out spazio in memoria di dati non necessari toosave utilizzato dal modello hello. Filtrare determinati hello le colonne di tabelle in modo non si importati nel database dell'area di lavoro hello o database modello hello dopo che è stato distribuito. 
  
#### <a name="toofilter-hello-table-data-before-importing"></a>dati della tabella hello toofilter prima dell'importazione  
  
1.  Nell'Editor di Query selezionare hello **DimCustomer** tabella. Verrà visualizzata una vista della tabella DimCustomer hello in datasource hello (il database di esempio AdventureWorksDWQ2014). 
  
2.  Effettuare una selezione multipla con CTRL+clic di **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, fare clic con il pulsante destro del mouse e quindi scegliere **Rimuovi colonne**. 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    Poiché i valori hello per le colonne selezionate non sono rilevanti tooInternet analisi delle vendite, non è alcuna necessità tooimport queste colonne. L'eliminazione delle colonne superflue consente di ridurre le dimensioni del modello e di aumentarne l'efficienza.  
  
4.  Filtrare hello rimanenti tabelle rimuovendo hello colonne in ogni tabella di seguito:  
    
    **DimDate**
    
      |Colonna|  
      |--------|  
      |DateKey|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |Colonna|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |Colonna|  
      |-----------|  
      |**SpanishProductName**|  
      |**FrenchProductName**|  
      |**FrenchDescription**|  
      |**ChineseDescription**|  
      |**ArabicDescription**|  
      |**HebrewDescription**|  
      |**ThaiDescription**|  
      |**GermanDescription**|  
      |**JapaneseDescription**|  
      |**TurkishDescription**|  
  
    **DimProductCategory**
  
      |Colonna|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |Colonna|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      |Colonna|  
      |------------------|  
      |**OrderDateKey**|  
      |**DueDateKey**|  
      |**ShipDateKey**|   
  
## <a name="Import"></a>Importare i dati delle colonne e tabelle hello selezionato  
Ora che è stato visualizzato in anteprima e filtrati i dati non necessari, è possibile importare rest hello hello di dati. Hello importazione dei dati di tabella hello insieme a tutte le relazioni tra tabelle. Vengono create nuove tabelle e colonne nel modello hello e non è possibile importare i dati esclusi tramite filtro.  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a>hello tooimport selezionate tabelle e i dati della colonna  
  
1.  Controllare le selezioni. Se è tutto corretto, fare clic su **Importa**. finestra di dialogo l'elaborazione dati Hello Mostra stato hello di dati da importare dall'origine dati nel database dell'area di lavoro.
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  Fare clic su **Close**.  

  
## <a name="save-your-model-project"></a>Salvare il progetto del modello  
È importante toofrequently salvare il progetto di modello.  
  
#### <a name="toosave-hello-model-project"></a>progetto di modello hello toosave  
  
-   Fare clic su **File** > **Salva tutti**.  
  
## <a name="whats-next"></a>Passaggi successivi
[Lezione 3: Contrassegnare come tabella data](../tutorials/aas-lesson-3-mark-as-date-table.md).

  
  
