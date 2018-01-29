---
title: 'Lezione supplementare dell''esercitazione su Azure Analysis Services: gerarchie incomplete | Microsoft Docs'
description: Questo articolo descrive come correggere le gerarchie incomplete nell'esercitazione di Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 01/08/2018
ms.author: owend
ms.openlocfilehash: c5c4a687ffe512b15372d152b517834771e46328
ms.sourcegitcommit: 176c575aea7602682afd6214880aad0be6167c52
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2018
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>Lezione supplementare: gerarchie incomplete

Questa lezione supplementare spiega come risolvere un problema comune che si verifica quando si applica il calcolo pivot sulle gerarchie che contengono valori (membri) vuoti a livelli diversi. Per fare un esempio, un'organizzazione in cui un responsabile di alto livello ha sia responsabili di reparto sia non responsabili come dipendenti diretti. Un altro esempio è rappresentato dalle gerarchie geografiche composte da paese-regione-città, in cui alcune città non dispongono di uno stato o una provincia, ad esempio Washington D.C. e la Città del Vaticano. Quando una gerarchia include membri vuoti, spesso finisce per includere livelli diversi o incompleti.

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

I modelli tabulari a livello di compatibilità 1400 offrono un'altra proprietà **Nascondi membri** per le gerarchie. L'impostazione **Default** (Predefinito) presuppone che non vi siamo membri vuoti ad alcun livello. L'impostazione **Nascondi membri vuoti** esclude i membri vuoti dalla gerarchia quando la si aggiunge a una tabella pivot o a un report.  
  
Tempo previsto per il completamento dell'esercitazione:**20 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
L'argomento di questa lezione supplementare fa parte di un'esercitazione sulla creazione di modelli tabulari. Prima di eseguire le attività di questa lezione supplementare, è necessario avere completato tutte le lezioni precedenti o avere completato il progetto modello di esempio Adventure Works Internet Sales. 

Se il progetto Adventure Works Internet Sales è stato creato nell'ambito dell'esercitazione, non contiene ancora dati o gerarchie incomplete. Per completare questa lezione supplementare, è quindi necessario creare prima il problema aggiungendo alcune tabelle, creare relazioni, colonne calcolate, una misura e una nuova gerarchia organizzativa. Questa operazione richiede circa 15 minuti. Basteranno poi pochi minuti per risolvere il problema.  

## <a name="add-tables-and-objects"></a>Aggiungere tabelle e oggetti
  
### <a name="to-add-new-tables-to-your-model"></a>Per aggiungere nuove tabelle al modello
  
1.  In Esplora modelli tabulari espandere **Origini dati** e quindi fare clic con il pulsante destro del mouse sulla connessione > **Importa nuove tabelle**.
  
2.  Nello strumento di spostamento selezionare **DimEmployee** e **FactResellerSales** e quindi fare clic su **OK**.

3.  Nell'Editor di query fare clic su **Importa**.

4.  Creare le [relazioni](../tutorials/aas-lesson-4-create-relationships.md) seguenti:

    | Tabella 1           | Colonna       | Direzione del filtro   | Tabella 2     | Colonna      | Attivo |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | Impostazione predefinita            | DimDate     | Data        | Sì    |
    | FactResellerSales | DueDate      | Impostazione predefinita            | DimDate     | Data        | No     |
    | FactResellerSales | ShipDateKey  | Impostazione predefinita            | DimDate     | Data        | No     |
    | FactResellerSales | ProductKey   | Impostazione predefinita            | DimProduct  | ProductKey  | Sì    |
    | FactResellerSales | EmployeeKey  | A entrambe le tabelle | DimEmployee | EmployeeKey | Sì    |

5. Nella tabella **DimEmployee** creare le [colonne calcolate](../tutorials/aas-lesson-5-create-calculated-columns.md) seguenti: 

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
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],2,1)) 
    ```

    **Level3** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],3,1)) 
    ```

    **Level4** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],4,1)) 
    ```

    **Level5** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],5,1)) 
    ```

6.  Nella tabella **DimEmployee** creare una [gerarchia](../tutorials/aas-lesson-9-create-hierarchies.md) denominata **Organizzazione**. Aggiungere le colonne seguenti nell'ordine: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.

7.  Nella tabella **FactResellerSales** creare la [misura](../tutorials/aas-lesson-6-create-measures.md) seguente:

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  Usare [Analizza in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) per aprire Excel e creare automaticamente una tabella pivot.

9.  In **Campi tabella pivot** aggiungere la gerarchia **Organizzazione** dalla tabella **DimEmployee** in **Righe** e la misura **ResellerTotalSales** dalla tabella **FactResellerSales** in **Valori**.

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    Come si può vedere nella tabella pivot, la gerarchia mostra righe incomplete. Sono presenti molte righe con membri vuoti.

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a>Per correggere la gerarchia incompleta impostando la proprietà Nascondi membri

1.  In **Esplora modelli tabulari** espandere **Tabelle** > **DimEmployee** > **Gerarchie** > **Organizzazione**.

2.  In **Proprietà** > **Nascondi membri** selezionare **Nascondi membri vuoti**. 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  In Excel aggiornare la tabella pivot. 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    La tabella è ora completa.

## <a name="see-also"></a>Vedere anche   
[Lezione 9: Creare gerarchie](../tutorials/aas-lesson-9-create-hierarchies.md)  
[Lezione supplementare: Sicurezza dinamica](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[Lezione supplementare: Righe di dettaglio](../tutorials/aas-supplemental-lesson-detail-rows.md)  
