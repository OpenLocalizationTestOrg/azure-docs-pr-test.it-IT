---
titolo: aaa "lezione dell'esercitazione di Azure Analysis Services 11: creare ruoli | Descrizione di "Microsoft Docs: viene descritto come ruoli toocreate hello progetto tutorial Azure Analysis Services. servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '

ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 26/05/2017: owend
---
# <a name="lesson-11-create-roles"></a>Lezione 11: Creare ruoli

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In questa lezione verranno creati ruoli. I ruoli garantiscono protezione dati e oggetti di database modello, limitando l'accesso tooonly gli utenti che sono membri del ruolo. Ogni ruolo è definito con una sola autorizzazione: Nessuna, Lettura, Lettura ed elaborazione, Elaborazione o Amministratore. I ruoli possono essere definiti durante la creazione dei modelli tramite Gestione ruoli. Dopo avere distribuito un modello, è possibile gestire i ruoli con SQL Server Management Studio (SSMS). vedere, più toolearn [ruoli](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).
  
> [!NOTE]  
> Creazione di ruoli è toocomplete non necessari in questa esercitazione. Per impostazione predefinita, si è connessi con account di hello privilegi di amministratore nel modello di hello. Tuttavia, per altri utenti nella toobrowse organizzazione utilizzando uno strumento client, è necessario creare almeno un ruolo lettura autorizzazioni e aggiungere tali utenti come membri.  
  
Vengono creati tre ruoli:  
  
-   **Responsabile vendite** : questo ruolo può includere gli utenti dell'organizzazione per cui si desidera toohave lettura autorizzazione tooall modello a oggetti e dati.  
  
-   **Sales Analyst US** : questo ruolo può includere gli utenti dell'organizzazione per cui si desidera solo i dati in grado di toobrowse toobe toosales in Italia hello correlati. Per questo ruolo, utilizzare un toodefine formula DAX un *filtro di riga*, che limita i membri toobrowse solo i dati per hello Stati Uniti.  
  
-   **Amministratore** : questo ruolo può includere gli utenti per cui si desidera toohave amministratore le autorizzazioni, che consente accesso illimitato e autorizzazioni tooperform le attività amministrative sul database modello hello.  
  
Poiché gli account utente e gruppo di Windows nell'organizzazione sono univoci, è possibile aggiungere l'account da toomembers l'organizzazione. Tuttavia, per questa esercitazione, è possibile inoltre omettere i membri di hello. Testare l'effetto di hello di ogni ruolo in un secondo momento nella lezione 12: analizza in Excel.  
  
Stimato toocomplete ora questa lezione: **15 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 10: creare partizioni](../tutorials/aas-lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Creare ruoli  
  
#### <a name="toocreate-a-sales-manager-user-role"></a>un ruolo utente Sales Manager toocreate  
  
1.  In Esplora modelli tabulari fare clic con il pulsante destro del mouse su **Ruoli** > **Ruoli**.  
  
2.  In Gestione ruoli fare clic su **Nuovo**.  
  
3.  Fare clic su nuovo ruolo hello e quindi in hello **nome** colonna, rinominare il ruolo di hello troppo**Sales Manager**.  
  
4.  In hello **autorizzazioni** colonna, fare clic su elenco a discesa hello e quindi selezionare hello **lettura** autorizzazione. 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  Facoltativo: Fare clic su hello **membri** scheda e quindi fare clic su **Aggiungi**. In hello **Seleziona utenti o gruppi** finestra di dialogo, immettere gli utenti di Windows hello o i gruppi dell'organizzazione si desidera tooinclude ruolo hello.  
  
#### <a name="toocreate-a-sales-analyst-us-user-role"></a>un ruolo utente Sales Analyst US toocreate  
  
1.  In Gestione ruoli fare clic su **Nuovo**.    
  
2.  Rinominare il ruolo di hello troppo**Sales Analyst US**.  
  
3.  Assegnare a questo ruolo l'autorizzazione **Lettura**.  
  
4.  Fare clic sulla scheda filtri di riga hello e quindi per hello **DimGeography** tabella solo nella colonna filtro DAX hello hello di tipo formula seguente:  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    Formula di filtro di riga di un valore booleano (TRUE/FALSE) tooa deve essere risolto. Con questa formula, si specifica che solo le righe con valore Country Region Code hello "US" sono visibili toohello utente.  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  Facoltativo: Fare clic su hello **membri** scheda e quindi fare clic su **Aggiungi**. In hello **Seleziona utenti o gruppi** finestra di dialogo, immettere gli utenti di Windows hello o i gruppi dell'organizzazione si desidera tooinclude ruolo hello.  
  
#### <a name="toocreate-an-administrator-user-role"></a>toocreate un ruolo utente amministratore  
  
1.  Fare clic su **New**.  
  
2.  Rinominare il ruolo di hello troppo**amministratore**.  
  
3.  Assegnare a questo ruolo l'autorizzazione **Amministratore**.  
  
4.  Facoltativo: Fare clic su hello **membri** scheda e quindi fare clic su **Aggiungi**. In hello **Seleziona utenti o gruppi** finestra di dialogo, immettere gli utenti di Windows hello o i gruppi dell'organizzazione si desidera tooinclude ruolo hello. 
  
  
## <a name="whats-next"></a>Passaggi successivi
[Lezione 12: Analizzare in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).

  
  
