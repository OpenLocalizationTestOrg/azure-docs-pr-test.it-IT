---
titolo: aaa "lezione supplementare di Azure Analysis Services tutorial: sicurezza dinamica | Descrizione di "Microsoft Docs: viene descritto come toouse sicurezza dinamica mediante riga filtri nell'esercitazione di hello Azure Analysis Services.
servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '

ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 26/05/2017: owend
---
# <a name="supplemental-lesson---dynamic-security"></a>Lezione supplementare: Sicurezza dinamica

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In questa lezione supplementare si creerà un ruolo aggiuntivo che implementa la sicurezza dinamica. Sicurezza dinamica offre sicurezza a livello di riga in base alle hello Nome account di accesso o l'id di hello utente attualmente connesso. 
  
sicurezza dinamica tooimplement, si aggiunge un modello di tooyour di tabella contenente i nomi utente hello degli utenti che possono connettersi toohello modello e visualizzare dati e oggetti modello. modello di Hello creato in questa esercitazione è nel contesto di hello di Adventure Works; Tuttavia, toocomplete questa lezione, è necessario aggiungere una tabella contenente gli utenti del proprio dominio. Le password hello non è necessario per i nomi utente hello che vengono aggiunti. toocreate una tabella EmployeeSecurity, con una piccola parte degli utenti del proprio dominio, utilizzare funzionalità Incolla hello, incollare i dati dei dipendenti da un foglio di calcolo di Excel. In uno scenario reale, tabella hello contenente i nomi utente in genere sarebbe una tabella da un database effettivo come un'origine dati. ad esempio, una tabella DimEmployee reale.  
  
sicurezza dinamica tooimplement, utilizzare due funzioni DAX: [funzione USERNAME (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f) e [funzione LOOKUPVALUE (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab). Queste funzioni, applicate in una formula di filtro di riga, vengono definite in un nuovo ruolo. Tramite la funzione LOOKUPVALUE hello, formula hello specifica un valore dalla tabella EmployeeSecurity hello. formula Hello passa quindi funzione USERNAME toohello di valore, che specifica il nome utente hello dell'utente hello connesso appartiene toothis ruolo. utente Hello possibile passare solo i dati specificati dai filtri di riga del ruolo hello. In questo scenario, si specifica che addetti alle vendite possono esplorare solo i dati delle vendite Internet per territori di vendita hello in cui sono membri.  
  
Le attività che sono univoci toothis scenario di modello tabulare Adventure Works, ma potrebbero non applicarsi necessariamente uno scenario reale tooa vengono identificate come tali. Ogni attività include informazioni aggiuntive che descrivono hello scopo hello.  
  
Stimato toocomplete ora questa lezione: **30 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
L'argomento di questa lezione supplementare fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire attività di hello in questa lezione supplementare, è necessario avere completato tutte le lezioni precedenti.  
  
## <a name="add-hello-dimsalesterritory-table-toohello-aw-internet-sales-tabular-model-project"></a>Aggiungere hello DimSalesTerritory tabella toohello progetto AW Internet Sales Tabular Model  
tooimplement sicurezza dinamica per questo scenario di Adventure Works, è necessario aggiungere due modelli di tooyour tabelle aggiuntive. prima tabella Hello aggiungere è DimSalesTerritory (come territorio vendita) da hello stesso database AdventureWorksDW. Successivamente, si applica una riga toohello SalesTerritory tabella dei filtri che definisce i dati specifici di hello hello utente connesso può esplorare.  
  
#### <a name="tooadd-hello-dimsalesterritory-table"></a>tabella DimSalesTerritory di hello tooadd  
  
1.  In Esplora modelli tabulari espandere **Origini dati**, fare clic con il pulsante destro del mouse sulla connessione e quindi scegliere **Importa nuove tabelle**.  

    Se viene visualizzata la finestra di dialogo credenziali di rappresentazione di hello, digitare le credenziali di rappresentazione hello è utilizzata nella lezione 2: aggiungere dati.
  
2.  Nel Pannello di navigazione, selezionare hello **DimSalesTerritory** tabella e quindi fare clic su **OK**.    
  
3.  Nell'Editor di Query, fare clic su hello **DimSalesTerritory** eseguire una query, quindi rimuovere **SalesTerritoryAlternateKey** colonna.  
  
7.  Fare clic su **Importa**.  
  
    Hello nuova tabella verrà aggiunta l'area di lavoro modello toohello. Oggetti e dati dalla tabella DimSalesTerritory di origine hello vengono quindi importati nel modello tabulare AW Internet Sales.  
  
9. Dopo la tabella hello è stata importata correttamente, fare clic su **Chiudi**.  

## <a name="add-a-table-with-user-name-data"></a>Aggiungere una tabella con i dati dei nomi utente  
tabella DimEmployee Hello nel database di esempio AdventureWorksDW hello contiene gli utenti del dominio AdventureWorks hello. Questo nomi utente, tuttavia, non esistono nel proprio ambiente. È necessario quindi creare una tabella nel modello che contenga un piccolo campione (almeno tre) di utenti reali dell'organizzazione. È quindi possibile aggiungere questi utenti come membri toohello nuovo ruolo. Non è necessario per i nomi utente di esempio hello password hello, ma è necessario nomi utente di Windows effettivi presenti nel proprio dominio.  
  
#### <a name="tooadd-an-employeesecurity-table"></a>una tabella EmployeeSecurity tooadd  
  
1.  Aprire Microsoft Excel per creare un foglio di lavoro.  
  
2.  Copiare hello seguente tabella, incluse le righe di intestazione hello e quindi incollarlo nel foglio di lavoro hello.  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  Sostituire hello nome, cognome e dominio omeutente con nomi di hello e gli ID di accesso dei tre utenti dell'organizzazione. Inserire hello stesso utente su hello prime due righe per EmployeeId 1, che mostra toomore rispetto a un territorio di vendita a cui appartiene questo utente. Lasciare hello campi EmployeeId e SalesTerritoryId così come sono.  
  
4.  Salvare il foglio di lavoro hello **SampleEmployee**.  
  
5.  Nel foglio di lavoro hello, selezionare tutte le celle di hello con i dati dei dipendenti, incluse le intestazioni di hello, quindi fare doppio clic su dati hello selezionata e quindi fare clic su **copia**.  
  
6.  In SSDT, fare clic su hello **modifica** menu e quindi fare clic su **Incolla**.  
  
    Se Incolla è disattivato, fare clic su qualsiasi colonna di qualsiasi tabella nella finestra di progettazione modelli di hello e riprovare.  
  
7.  In hello **anteprima Incolla** della finestra di dialogo **nome tabella**, tipo **EmployeeSecurity**.  
  
8.  In **toobe dati incollati**, verificare che i dati di hello includono tutti i dati utente hello e le intestazioni dal foglio di lavoro SampleEmployee hello.  
  
9. Verificare che l'opzione **Usa la prima riga per le intestazioni di colonna** sia selezionata e quindi fare clic su **Ok**.  
  
    Viene creata una nuova tabella denominata EmployeeSecurity con i dati dei dipendenti copiati dal foglio di lavoro SampleEmployee hello.  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>Creare relazioni tra le tabelle FactInternetSales, DimGeography e DimSalesTerritory  
Hello FactInternetSales e DimGeography DimSalesTerritory tabella tutti contenere una colonna comune, SalesTerritoryId. Hello SalesTerritoryId colonna tabella DimSalesTerritory hello contiene i valori con un Id diverso per ogni territorio di vendita.  
  
#### <a name="toocreate-relationships-between-hello-factinternetsales-dimgeography-and-hello-dimsalesterritory-table"></a>tabella DimSalesTerritory hello hello FactInternetSales e DimGeography toocreate relazioni  
  
1.  Nella visualizzazione Diagramma, hello **DimGeography** tabella, fare clic e tenere premuto hello **SalesTerritoryId** colonna, quindi trascinare hello cursore toohello **SalesTerritoryId** colonna hello **DimSalesTerritory** tabella e infine rilasciare.  
  
2.  In hello **FactInternetSales** tabella, fare clic e tenere premuto hello **SalesTerritoryId** colonna, quindi trascinare hello cursore toohello **SalesTerritoryId** colonna hello  **DimSalesTerritory** tabella e infine rilasciare.  
  
    Hello avviso proprietà Active di questa relazione è False, ovvero che non è attivo. tabella FactInternetSales Hello esiste già un'altra relazione attiva.  
  
## <a name="hide-hello-employeesecurity-table-from-client-applications"></a>Nascondere hello EmployeeSecurity tabella dalle applicazioni client  
In questa attività si nasconde tabella EmployeeSecurity hello, mantenendolo venga visualizzato nell'elenco di campi di un'applicazione client. Tenere presente che nascondere una tabella non significa proteggerla. Gli utenti possono comunque eseguire query per recuperare dati dalla tabella EmployeeSecurity, se sanno come farlo. toosecure hello EmployeeSecurity dati della tabella, impedendo agli utenti in grado di tooquery i relativi dati, si applica un filtro in un'attività successiva.  
  
#### <a name="toohide-hello-employeesecurity-table-from-client-applications"></a>Nella tabella EmployeeSecurity hello toohide dalle applicazioni client  
  
-   In Progettazione modelli di hello, in vista diagramma, fare doppio clic su hello **dipendente** sull'intestazione di tabella e quindi fare clic su **Nascondi a strumenti Client**.  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>Creare un ruolo utente Sales Employees by Territory  
In questa attività si creerà un ruolo utente. Questo ruolo include un filtro di riga che definisce quali righe della tabella DimSalesTerritory hello sono toousers visibile. Hello filtro viene applicato in relazione uno-a-molti hello direzione tooall altre tabelle correlate tooDimSalesTerritory. È inoltre possibile applicare un filtro che protegge l'intera tabella EmployeeSecurity hello impedendone da qualsiasi utente che è un membro del ruolo hello.  
  
> [!NOTE]  
> Hello addetti alle vendite dal ruolo territorio creato in questa lezione consente di limitare i membri toobrowse (o query) solo i dati di vendita per hello territorio di vendita toowhich che appartengono. Se si aggiunge un utente come un membro toohello addetti alle vendite, dal ruolo di territorio che esiste anche un membro di un ruolo creato nella [lezione 11: creare ruoli](../tutorials/aas-lesson-11-create-roles.md), si ottiene una combinazione di autorizzazioni. Quando un utente è un membro di più ruoli, autorizzazioni hello e i filtri di riga definiti per ogni ruolo sono cumulativi. Vale a dire hello autorizzazioni utente hello maggiore determinato dalla combinazione di hello dei ruoli.  
  
#### <a name="toocreate-a-sales-employees-by-territory-user-role"></a>toocreate un addetti alle vendite per il ruolo di utente territorio  
  
1.  In SSDT, fare clic su hello **modello** menu e quindi fare clic su **ruoli**.  
  
2.  In **Gestione ruoli** fare clic su **Nuovo**.  
  
    Un nuovo ruolo con hello Nessuna autorizzazione è stato aggiunto toohello elenco.  
  
3.  Fare clic su nuovo ruolo hello e quindi in hello **nome** colonna, rinominare il ruolo di hello troppo**addetti alle vendite per territorio**.  
  
4.  In hello **autorizzazioni** colonna, fare clic su elenco a discesa hello e quindi selezionare hello **lettura** autorizzazione.  
  
5.  Fare clic su hello **membri** scheda e quindi fare clic su **Aggiungi**.  
  
6.  In hello **Seleziona utente o gruppo** della finestra di dialogo **oggetto hello invio denominato tooselect**, digitare hello primo esempio il nome utente utilizzato per la creazione tabella EmployeeSecurity hello. Fare clic su **Controlla nomi** tooverify hello utente nome valido e quindi fare clic su **Ok**.  
  
    Ripetere questo passaggio, aggiunta di hello altri nomi utente di esempio utilizzati per la creazione tabella EmployeeSecurity hello.  
  
7.  Fare clic su hello **i filtri di riga** scheda.  
  
8.  Per hello **EmployeeSecurity** tabella, in hello **filtro DAX** colonna, hello di tipo formula seguente:  
  
    ```
      =FALSE()  
    ```
  
    Questa formula specifica che tutte le colonne vengono risolte condizione booleana false toohello. Nessuna colonna per tabella EmployeeSecurity hello è possibile eseguire query da un membro di hello addetti alle vendite dal ruolo utente di territorio.  
  
9. Per hello **DimSalesTerritory** tabella, hello di tipo formula seguente:  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    In questa formula, hello funzione LOOKUPVALUE restituisce tutti i valori per la colonna [SalesTerritoryId] DimEmployeeSecurity hello, in cui hello EmployeeSecurity [LoginId] è hello stesso come connesso nome utente di Windows ed EmployeeSecurity [hello corrente SalesTerritoryId] è hello come hello DimSalesTerritory [SalesTerritoryId].  
  
    Hello set di ID territorio vendita restituito da LOOKUPVALUE viene quindi utilizzato toorestrict hello righe visualizzate nella tabella DimSalesTerritory hello. Vengono visualizzate solo le righe in cui hello SalesTerritoryID per riga hello è nel set di hello di ID restituiti da lookupvalue hello.  
  
10. In Gestione ruoli fare clic su **OK**.  
  
## <a name="test-hello-sales-employees-by-territory-user-role"></a>Test addetti alle vendite hello dal ruolo utente territorio  
In questa attività, utilizzare hello analizza nella funzionalità di Excel efficacia hello tootest SSDT di hello addetti alle vendite dal ruolo utente di territorio. Specificare uno dei nomi utente hello è stata aggiunta toohello EmployeeSecurity tabella e come membro del ruolo hello. Questo nome utente viene quindi utilizzato come nome utente effettivo hello in connessione hello creata tra Excel e hello modello.  
  
#### <a name="tootest-hello-sales-employees-by-territory-user-role"></a>tootest hello addetti alle vendite dal ruolo utente territorio  
  
1.  In SSDT, fare clic su hello **modello** menu e quindi fare clic su **analizza in Excel**.  
  
2.  In hello **analizza in Excel** della finestra di dialogo **specificare hello nome o ruolo toouse tooconnect toohello modello utente**selezionare **altro utente di Windows**, quindi fare clic su **Sfoglia**.  
  
3.  In hello **Seleziona utente o gruppo** della finestra di dialogo **immettere hello oggetto nome tooselect**, digitare un nome utente incluso nella tabella EmployeeSecurity hello e quindi fare clic su **Controlla nomi**.  
  
4.  Fare clic su **Ok** tooclose hello **Seleziona utente o gruppo** la finestra di dialogo e quindi fare clic su **Ok** tooclose hello **analizza in Excel** la finestra di dialogo.  
  
    Excel verrà aperto con una nuova cartella di lavoro. Viene creata automaticamente una tabella pivot. Hello elenco PivotTable Fields include la maggior parte dei campi dati hello disponibile nel nuovo modello.  
  
    Tabella EmployeeSecurity hello di notifica non è visibile nell'elenco PivotTable Fields hello. perché è stata nascosta dagli strumenti client in un'attività precedente.  
  
5.  In hello **campi** elenco **∑ Internet Sales** (misure) Seleziona hello **InternetTotalSales** misura. misura Hello viene inserito hello **valori** campi.  
  
6.  Seleziona hello **SalesTerritoryId** colonna hello **DimSalesTerritory** tabella. colonna Hello viene inserito hello **etichette di riga** campi.  
  
    Avviso Internet cifre di vendita vengono visualizzate solo per hello una regione toowhich hello nome utente effettivo utilizzato appartiene. Se si seleziona un'altra colonna, ad esempio città dalla tabella DimGeography hello come campo etichette di riga, solo le città utente effettivo hello hello territorio di vendita toowhich appartiene vengono visualizzati.  
  
    Questo utente non è possibile individuare o query di dati delle vendite Internet per territori diversi da hello uno a che cui appartengono. Questa restrizione è dato che il filtro di riga definito per la tabella DimSalesTerritory hello in hello addetti alle vendite dal ruolo utente territorio, hello protegge tutti i dati correlati tooother i territori di vendita.  
  
## <a name="see-also"></a>Vedere anche  
[USERNAME Function (DAX) (Funzione DAX USERNAME)](https://msdn.microsoft.com/library/hh230954.aspx)  
[LOOKUPVALUE Function (DAX) (Funzione DAX LOOKUPVALUE)](https://msdn.microsoft.com/library/gg492170.aspx)  
[CUSTOMDATA Function (DAX) (Funzione DAX CUSTOMDATA)](https://msdn.microsoft.com/library/hh213140.aspx)  