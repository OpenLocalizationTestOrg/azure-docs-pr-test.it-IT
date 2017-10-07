---
titolo: aaa "lezione dell'esercitazione di Azure Analysis Services 3: contrassegna come tabella data | Descrizione di "Microsoft Docs: viene descritto come toomark tabella di una data nel progetto di esercitazione di hello Azure Analysis Services. servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '

ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 01/06/2017: owend
---
# <a name="lesson-3-mark-as-date-table"></a>Lezione 3: Contrassegnare come tabella data

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Nella lezione 2: Ottenere i dati è stata importata una tabella delle dimensioni denominata DimDate. Anche se nel modello questa tabella è denominata DimDate, è anche nota come *tabella data*, perché contiene dati di data e ora.  
  
Quando si usano funzioni di Business Intelligence per le gerarchie temporali DAX, è necessario specificare alcune proprietà, tra cui una *tabella data* e una *colonna data* che funge da identificatore univoco nella tabella.
  
In questa lezione si contrassegna tabella DimDate hello come hello *tabella data* e una colonna di Date hello (nella tabella Date hello) come hello *colonna Data* (identificatore univoco).  

Prima di contrassegnare una colonna di tabella e la data di date hello, è un toodo tempestivamente un po' di manutenzione toomake toounderstand di più facile del modello. Si noti che nella tabella DimDate hello una colonna denominata **FullDateAlternateKey**. Questa colonna contiene una riga per ogni giorno in ogni anno di calendario incluso nella tabella hello. Questa colonna viene usata molto spesso nelle formule per le misure e nei report, ma FullDateAlternateKey non è in realtà un buon identificatore per questa colonna. Si rinomina troppo**data**, rendendo più semplice tooidentify e includere nelle formule. Quando possibile, è una buona idea toorename oggetti quali tabelle e colonne toomake li tooidentify più semplice in SSDT e client di creazione report di applicazioni, quali Power BI ed Excel. 
  
Stimato toocomplete ora questa lezione: **tre minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 2: ottenere dati](../tutorials/aas-lesson-2-get-data.md). 

### <a name="toorename-hello-fulldatealternatekey-column"></a>colonna FullDateAlternateKey di hello toorename

1.  In Progettazione modelli di hello, fare clic su hello **DimDate** tabella.

2.  Doppio clic sull'intestazione di hello per hello **FullDateAlternateKey** colonna, quindi rinominare troppo**data**.

  
### <a name="tooset-mark-as-date-table"></a>tooset contrassegna come tabella data  
  
1.  Seleziona hello **data** colonna, quindi nel hello **proprietà** finestra, in **tipo di dati**, assicurarsi che **data** è selezionata.  
  
2.  Fare clic su hello **tabella** menu, quindi fare clic su **data**, quindi fare clic su **contrassegna come tabella data**.  
  
3.  In hello **contrassegna come tabella data** della finestra di dialogo hello **data** casella di riepilogo Seleziona hello **data** colonna come identificatore univoco di hello. In genere, è selezionata per impostazione predefinita. Fare clic su **OK**. 

    ![aas-lesson3-date-table](../tutorials/media/aas-lesson3-date-table.png)
  

## <a name="whats-next"></a>Passaggi successivi
[Lezione 4: Creare relazioni](../tutorials/aas-lesson-4-create-relationships.md).
  
