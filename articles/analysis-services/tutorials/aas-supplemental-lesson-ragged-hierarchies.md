---
titolo: aaa "lezione supplementare esercitazione Azure Analysis Services: gerarchie incomplete | Descrizione di "Microsoft Docs: viene descritto come toofix gerarchie incomplete nell'esercitazione di hello Azure Analysis Services.
servizi: documentationcenter di analysis services: ' autore: manager minewiskan: erikre editor: ' tag: '

ms. AssetID: ms. Service: ms. DevLang analysis services: ms. topic NA: ms. tgt_pltfrm get-started-article: Workload NA: ms. date na: author 26/05/2017: owend
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>Lezione supplementare: gerarchie incomplete

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Questa lezione supplementare spiega come risolvere un problema comune che si verifica quando si applica il calcolo pivot sulle gerarchie che contengono valori (membri) vuoti a livelli diversi. Per fare un esempio, un'organizzazione in cui un responsabile di alto livello ha sia responsabili di reparto sia non responsabili come dipendenti diretti. Un altro esempio è rappresentato dalle gerarchie geografiche composte da paese-regione-città, in cui alcune città non dispongono di uno stato o una provincia, ad esempio Washington D.C. e la Città del Vaticano. Quando si dispone di una gerarchia di membri vuoti, è spesso discende toodifferent o incompleta, livelli.

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

I modelli tabulari a livello di compatibilità hello 1400 presentano un ulteriore **Nascondi membri** proprietà per le gerarchie. Hello **predefinito** impostazione presuppone che non esistono membri vuoti a qualsiasi livello. Hello **nascondere i membri vuoti** impostazione consente di escludere i membri vuoti dalla gerarchia di hello quando aggiunto tooa tabella pivot o un report.  
  
Stimato toocomplete ora questa lezione: **20 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
L'argomento di questa lezione supplementare fa parte di un'esercitazione sulla creazione di modelli tabulari. Prima di eseguire attività di hello in questa lezione supplementare, è necessario avere completato tutte le lezioni precedenti o dispone di un progetto di modello di esempio Adventure Works Internet Sales completato. 

Se sono stati creati progetto AW Internet Sales hello come parte dell'esercitazione hello, il modello non contiene ancora dati o gerarchie incomplete. toocomplete questa lezione supplementare, è necessario innanzitutto toocreate hello problema mediante l'aggiunta di alcune tabelle aggiuntive, creare relazioni, colonne calcolate, una misura e una nuova gerarchia organizzativa. Questa operazione richiede circa 15 minuti. Quindi, si ottiene toosolve in pochi minuti.  

## <a name="add-tables-and-objects"></a>Aggiungere tabelle e oggetti
  
### <a name="tooadd-new-tables-tooyour-model"></a>nuovo modello di tooyour tabelle tooadd
  
1.  In Esplora modelli tabulari espandere **Origini dati** e quindi fare clic con il pulsante destro del mouse sulla connessione > **Importa nuove tabelle**.
  
2.  Nello strumento di spostamento selezionare **DimEmployee** e **FactResellerSales** e quindi fare clic su **OK**.

3.  Nell'Editor di query fare clic su **Importa**.

4.  Creare i seguenti hello [relazioni](../tutorials/aas-lesson-4-create-relationships.md):

    | Tabella 1           | Colonna       | Direzione del filtro   | Tabella 2     | Colonna      | Attivo |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | Default            | DimDate     | Data        | Sì    |
    | FactResellerSales | DueDate      | Default            | DimDate     | Data        | No     |
    | FactResellerSales | ShipDateKey  | Default            | DimDate     | Data        | No     |
    | FactResellerSales | ProductKey   | Default            | DimProduct  | ProductKey  | Sì    |
    | FactResellerSales | EmployeeKey  | Tabelle tooBoth | DimEmployee | EmployeeKey | Sì    |

5. In hello **DimEmployee** tabella, creare i seguenti hello [le colonne calcolate](../tutorials/aas-lesson-5-create-calculated-columns.md): 

    **Percorso** 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    **FullName** 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    **Level1** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    **Level2** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    **Level3** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    **Level4** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    **Level5** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  In hello **DimEmployee** tabella, creare un [gerarchia](../tutorials/aas-lesson-9-create-hierarchies.md) denominato **organizzazione**. Aggiungere hello colonne nell'ordine seguente: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.

7.  In hello **FactResellerSales** tabella, creare i seguenti hello [misura](../tutorials/aas-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  Utilizzare [analizza in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel e creare automaticamente una tabella pivot.

9.  In **PivotTable Fields**, aggiungere hello **organizzazione** gerarchia da hello **DimEmployee** tabella troppo**righe**e hello **ResellerTotalSales** misura dalla hello **FactResellerSales** tabella troppo**valori**.

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    Come si vede nella tabella pivot hello, hello gerarchia consente di visualizzare le righe che sono incomplete. Sono presenti molte righe con membri vuoti.

## <a name="toofix-hello-ragged-hierarchy-by-setting-hello-hide-members-property"></a>gerarchia incompleta di hello toofix impostando la proprietà membri Nascondi hello

1.  In **Esplora modelli tabulari** espandere **Tabelle** > **DimEmployee** > **Gerarchie** > **Organizzazione**.

2.  In **Proprietà** > **Nascondi membri** selezionare **Nascondi membri vuoti**. 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  In Excel, aggiornare hello tabella pivot. 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    La tabella è ora completa.

## <a name="see-also"></a>Vedere anche   
[Lezione 9: Creare gerarchie](../tutorials/aas-lesson-9-create-hierarchies.md)  
[Lezione supplementare: Sicurezza dinamica](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[Lezione supplementare: Righe di dettaglio](../tutorials/aas-supplemental-lesson-detail-rows.md)  