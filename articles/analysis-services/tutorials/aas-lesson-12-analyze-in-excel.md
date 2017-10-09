---
titolo: aaa "lezione dell'esercitazione di Azure Analysis Services 12: analizza in Excel | Descrizione di Microsoft Docs": descrive come toouse analizza in Excel in hello Azure Analysis Services tutorial progetto. servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '

ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 26/05/2017: owend
---
# <a name="lesson-12-analyze-in-excel"></a>Lezione 12: Analizzare in Excel

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In questa lezione, utilizzare hello analizza in Excel funzionalità tooopen Microsoft Excel, creare automaticamente un'area di lavoro modello toohello connessione e aggiunge automaticamente un foglio di lavoro toohello di tabella pivot. Hello analizza nella funzionalità di Excel deve tooprovide efficacia di hello tootest un modo semplice e rapido del modello di progettazione toodeploying precedente del modello. In questa lezione non si esegue alcuna analisi dei dati. scopo di Hello in questa lezione è toofamiliarize, creare il modello di hello, con gli strumenti di hello è possibile utilizzare tootest la progettazione del modello.   
  
in questa lezione, Excel deve essere installata in hello toocomplete SSDT nello stesso computer.
  
Stimato toocomplete ora questa lezione: **cinque minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 11: creare ruoli](../tutorials/aas-lesson-11-create-roles.md).  
  
## <a name="browse-using-hello-default-and-internet-sales-perspectives"></a>Sfogliare il modello utilizzando le prospettive di hello predefinito e le vendite Internet  
In queste prime attività, esplorare il modello utilizzando la prospettiva predefinita entrambi hello, che include tutti gli oggetti modello, e prospettiva Internet Sales hello è in precedenza. Hello prospettiva Internet Sales esclude l'oggetto hello Customer table.  
  
#### <a name="toobrowse-by-using-hello-default-perspective"></a>toobrowse usando la prospettiva predefinita hello  
  
1.  Fare clic su hello **modello** menu > **analizza in Excel**.  
  
2.  In hello **analizza in Excel** la finestra di dialogo, fare clic su **OK**.  
  
    Excel verrà aperto con una nuova cartella di lavoro. Una connessione all'origine dati viene creata utilizzando l'account utente corrente hello e hello prospettiva predefinita è campi visualizzabili toodefine utilizzato. Una tabella pivot viene aggiunta automaticamente toohello foglio di lavoro.  
  
3.  Nella finestra Excel hello **elenco campi tabella pivot**, hello preavviso **DimDate** e **FactInternetSales** vengono visualizzati i gruppi di misure. Hello **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, e **FactInternetSales** vengono visualizzati anche le tabelle con le rispettive colonne.  
  
4.  Chiudere Excel senza salvare una cartella di lavoro hello.  
  
#### <a name="toobrowse-by-using-hello-internet-sales-perspective"></a>toobrowse usando la prospettiva Internet Sales hello  
  
1.  Fare clic su hello **modello** menu e quindi fare clic su **analizza in Excel**.  
  
2.  In hello **analizza in Excel** la finestra di dialogo, lasciare **utente Windows corrente** selezionata, quindi hello **prospettiva** listbox elenco a discesa, selezionare **Internet Sales** , quindi fare clic su **OK**. 
    
    ![aas-lesson12-perspective](../tutorials/media/aas-lesson12-perspective.png)
    
3.  In Excel, in **PivotTable Fields**, si noti tabella DimCustomer hello viene escluso dall'elenco di campi hello.  
    
    ![aas-lesson12-fields](../tutorials/media/aas-lesson12-fields.png)
    
4.  Chiudere Excel senza salvare una cartella di lavoro hello.  
  
## <a name="browse-by-using-roles"></a>Esplorare il modello tramite i ruoli  
I ruoli sono una parte fondamentale di qualsiasi modello tabulare. Senza almeno un ruolo toowhich utenti vengono aggiunti come membri, gli utenti non possono accedere e analizzare i dati utilizzando il modello. Hello analizza nella funzionalità di Excel fornisce un modo per si ruoli hello tootest definiti.  
  
#### <a name="toobrowse-by-using-hello-sales-manager-user-role"></a>toobrowse con ruolo utente Sales Manager di hello  
  
1.  In SSDT, fare clic su hello **modello** menu e quindi fare clic su **analizza in Excel**.  
  
2.  In **specificare hello nome o ruolo toouse tooconnect toohello modello utente**selezionare **ruolo**, quindi nella casella di riepilogo discesa hello **Sales Manager**e quindi fare clic su  **OK**.  
  
    Excel verrà aperto con una nuova cartella di lavoro. Viene creata automaticamente una tabella pivot. Hello elenco campi tabella Pivot include tutti i campi dati hello disponibili nel nuovo modello.  
      
3.  Chiudere Excel senza salvare una cartella di lavoro hello.  
  
## <a name="whats-next"></a>Passaggi successivi
Lezione successiva passare toohello: [lezione 13: distribuire](../tutorials/aas-lesson-13-deploy.md).

  
  
  
