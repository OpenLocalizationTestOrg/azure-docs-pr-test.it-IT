---
titolo: aaa "lezione dell'esercitazione di Azure Analysis Services 10: creare partizioni | Descrizione di "Microsoft Docs: viene descritto come toocreate partizioni nel progetto di esercitazione di hello Azure Analysis Services. servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '

ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 26/05/2017: owend
---
# <a name="lesson-10-create-partitions"></a>Lezione 10: Creare partizioni

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In questa lezione è creare partizioni toodivide hello FactInternetSales tabella in parti logiche più piccole che possono essere elaborate (aggiornate) indipendentemente dalle altre partizioni. Per impostazione predefinita, ogni tabella che inclusa nel modello dispone di una partizione, che include colonne e righe della tabella di hello tutti. Per la tabella FactInternetSales hello vogliamo dati hello toodivide per anno; una partizione per ognuno dei cinque anni della tabella hello. Ogni partizione può quindi essere elaborata in modo indipendente. vedere, più toolearn [partizioni](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular). 
  
Stimato toocomplete ora questa lezione: **15 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 9: creare gerarchie](../tutorials/aas-lesson-9-create-hierarchies.md).  
  
## <a name="create-partitions"></a>Creare partizioni  
  
#### <a name="toocreate-partitions-in-hello-factinternetsales-table"></a>toocreate partizioni nella tabella FactInternetSales hello  
  
1.  In Esplora modelli tabulari espandere **Tabelle** e quindi fare clic con il pulsante destro del mouse su **FactInternetSales** > **Partizioni**.  
  
2.  In Gestione partizioni, fare clic su **copia**e quindi modificare il nome di hello troppo**FactInternetSales2010**.
  
    Poiché si desidera hello partizione tooinclude solo le righe all'interno di un determinato periodo, per l'anno hello 2010, è necessario modificare l'espressione di query hello.
  
4.  Fare clic su **progettazione** tooopen Editor di Query e quindi fare clic su hello **FactInternetSales2010** query.

5.  Nell'anteprima, fare clic su hello freccia giù in hello **OrderDate** intestazione di colonna e quindi fare clic su **filtri data/ora** > **tra**.

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  Nella finestra di dialogo Filtra righe hello, in **Mostra righe in cui: OrderDate**, lasciare **è dopo o uguale a**, quindi immettere nel campo Data hello **1/1/2010**. Lasciare hello **e** operatore selezionato, quindi selezionare **prima**, quindi immettere nel campo Data hello **1/1/2011**e quindi fare clic su **OK**.

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    Si noti che nell'Editor di query, in Passaggi applicati, è visualizzato un altro passaggio denominato Filtrate righe. Questo filtro è tooselect solo date di ordini da 2010.

8.  Fare clic su **Importa**.

    In Gestione partizioni, si noti query hello ora l'espressione contiene una clausola di filtrare le righe aggiuntiva.

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    Questa istruzione consente di specificare che la partizione deve includere solo i dati di hello in tali righe in cui è hello OrderDate in hello anno di calendario 2010 come specificato nella clausola di hello righe filtrate.  
  
  
#### <a name="toocreate-a-partition-for-hello-2011-year"></a>una partizione per l'anno 2011 hello toocreate  
  
1.  Nell'elenco di partizioni hello, fare clic su hello **FactInternetSales2010** partizione creata e quindi fare clic su **copia**.  Modificare il nome di partizione hello troppo**FactInternetSales2011**. 

    Non è necessario toouse Editor di Query toocreate una nuova clausola di righe filtrate. Poiché una copia della query hello è stato creato per 2010, è sufficiente toodo effettuano una lieve modifica in query di hello per 2011.
  
2.  In **espressione di Query**, affinché questo tooinclude partizione solo le righe per hello anno 2011, sostituire gli anni di hello nella clausola righe filtrate hello con **2011** e **2012**, rispettivamente, ad esempio:  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="toocreate-partitions-for-2012-2013-and-2014"></a>partizioni toocreate per 2012, 2013 e 2014.  
  
- Seguire i passaggi precedenti hello, creazione di partizioni per 2012, 2013 e 2014, la modifica di anni hello in hello righe filtrate clausola tooinclude solo le righe per tale anno. 
  

## <a name="delete-hello-factinternetsales-partition"></a>Eliminare hello FactInternetSales partizione
Dopo aver creato le partizioni per ogni anno, è possibile eliminare partizione FactInternetSales hello; Quando si sceglie elabora tutte durante l'elaborazione di partizioni, impedendo si sovrappongono.

#### <a name="toodelete-hello-factinternetsales-partition"></a>hello toodelete FactInternetSales partizione
-  Fare clic sulla partizione FactInternetSales hello e quindi fare clic su **eliminare**.



## <a name="process-partitions"></a>Elaborare le partizioni  
In Gestione partizioni notare hello **elaborati ultimo** per ognuna delle nuove partizioni hello creato mostra queste partizioni non sono mai state elaborate. Quando si creano partizioni, è consigliabile eseguire un elabora partizioni o una tabella del processo operazione toorefresh hello dati nelle partizioni.  
  
#### <a name="tooprocess-hello-factinternetsales-partitions"></a>tooprocess hello FactInternetSales partizioni  
  
1.  Fare clic su **OK** tooclose gestione partizioni.  
  
2.  Fare clic su hello **FactInternetSales** tabella, quindi fare clic su hello **modello** menu > **processo** > **elabora partizioni**.  
  
3.  Nella finestra di dialogo Elabora partizioni hello verificare **modalità** è troppo**elaborazione predefinita**.  
  
4.  Selezionare la casella di controllo di hello in hello **processo** per ognuna delle cinque hello partizioni creato e quindi fare clic su **OK**.  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    Se viene chiesto di immettere le credenziali di rappresentazione, immettere nome utente di Windows hello e la password specificati nella lezione 2.  
  
    Hello **l'elaborazione dati** verrà visualizzata la finestra di dialogo con informazioni dettagliate sul processo per ogni partizione. Si noti che viene trasferito un numero diverso di righe per ogni partizione, Ogni partizione include solo le righe per anno hello specificato nella clausola WHERE nell'istruzione SQL hello hello. Al termine dell'elaborazione, vado avanti e chiudere la finestra di dialogo di elaborazione dei dati hello.  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>Passaggi successivi
Lezione successiva passare toohello: [lezione 11: creare ruoli](../tutorials/aas-lesson-11-create-roles.md). 
