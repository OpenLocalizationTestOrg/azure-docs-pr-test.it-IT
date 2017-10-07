---
titolo: aaa "lezione dell'esercitazione di Azure Analysis Services 9: creare gerarchie | Descrizione di Microsoft Docs": servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '

ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 26/05/2017: owend
---
# <a name="lesson-9-create-hierarchies"></a>Lezione 9: Creare gerarchie

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In questa lezione verranno create gerarchie. Le gerarchie sono gruppi di colonne disposti in livelli. Ad esempio, una gerarchia Geografia può includere i sottolivelli Paese, Stato, Regione e Città. Le gerarchie possono verificarsi separatamente dalle altre colonne in un elenco di campi dell'applicazione client reporting, agevolando client toonavigate gli utenti e includere in un report. vedere, più toolearn [gerarchie](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)
  
gerarchie toocreate, utilizzare Progettazione modelli di hello in *vista diagramma*. La creazione e la gestione delle gerarchie non è supportata in vista dati.  
  
Stimato toocomplete ora questa lezione: **20 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 8: creare prospettive](../tutorials/aas-lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Creare gerarchie  
  
#### <a name="toocreate-a-category-hierarchy-in-hello-dimproduct-table"></a>una gerarchia Category nella tabella DimProduct hello toocreate  
  
1.  In Progettazione modelli hello (vista diagramma) fare doppio clic su hello **DimProduct** tabella > **crea gerarchia**. Nella parte inferiore della finestra di tabella hello hello disponibile per una nuova gerarchia. Rinominare la gerarchia hello **categoria**.  
  
2.  Fare clic e trascinare hello **ProductCategoryName** toohello colonna nuova **categoria** gerarchia.  
  
3.  In hello **categoria** gerarchia, hello rapida **ProductCategoryName** > **rinominare**, quindi digitare **categoria**.  
  
    > [!NOTE]  
    > Ridenominazione di una colonna in una gerarchia non comporta la ridenominazione di tale colonna nella tabella hello. Una colonna in una gerarchia è semplicemente una rappresentazione della colonna hello nella tabella di hello.  
  
4.  Fare clic e trascinare hello **ProductSubcategoryName** colonna toohello **categoria** gerarchia. Rinominarla **Subcategory**. 
  
5.  Pulsante destro del mouse hello **ModelName** colonna > **aggiungere toohierarchy**, quindi selezionare **categoria**. Rinominarla **Model**.

6.  Infine, aggiungere **EnglishProductName** toohello gerarchia di categorie. Rinominarla **Product**.  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="toocreate-hierarchies-in-hello-dimdate-table"></a>gerarchie toocreate tabella DimDate hello  
  
1.  In hello **DimDate** tabella, creare una gerarchia denominata **calendario**.  
  
3.  Aggiungere hello colonne nell'ordine seguente:

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  In hello **DimDate** tabella, creare un **fiscale** gerarchia. Includere hello colonne nell'ordine seguente:  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  Infine, in hello **DimDate** tabella, creare un **ProductionCalendar** gerarchia. Includere hello colonne nell'ordine seguente:  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>Passaggi successivi
[Lezione 10: Creare partizioni](../tutorials/aas-lesson-10-create-partitions.md). 
  
  
