---
title: aaa "prospettive di Azure Analysis Services tutorial lezione 8 crea | Documenti di Microsoft"
description: Viene descritto come toocreate prospettive in hello progetto tutorial Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 25391813e1969ecb22af4d6f9c1ccd8358d812fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-8-create-perspectives"></a>Lezione 8: Creare prospettive

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

In questa lezione verrà creata una prospettiva Internet Sales. Una prospettiva definisce un subset visualizzabile di un modello che offre punti di vista mirati, specifici di un'azienda o specifici di un'applicazione. Quando un utente si connette tooa modello utilizzando una prospettiva, vengono visualizzati solo gli oggetti modello (tabelle, colonne, misure, gerarchie e indicatori KPI) come campi definiti in tale prospettiva. vedere, più toolearn [prospettive](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).
  
Hello prospettiva Internet Sales è stato creato in questa lezione esclude l'oggetto della tabella DimCustomer hello. Quando si crea una prospettiva che esclude determinati oggetti dalla visualizzazione, l'oggetto esiste ancora nel modello di hello. ma non è visibile in un elenco di campi del client per la creazione di report. Le colonne e le misure calcolate, indipendentemente dal fatto che siano incluse o meno in una prospettiva, possono comunque essere calcolate in base ai dati degli oggetti esclusi.  
  
scopo di Hello in questa lezione è toodescribe come toocreate prospettive e acquisire familiarità con gli strumenti di creazione di modelli tabulari hello. Se successivamente si espande questo tabelle aggiuntive tooinclude di modello, è possibile creare ulteriori prospettive toodefine diversi punti di vista del modello di hello, ad esempio, vendite e inventario.  
  
Stimato toocomplete ora questa lezione: **cinque minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire attività di hello in questa lezione, è necessario avere completato la lezione precedente hello: [lezione 7: creare indicatori di prestazioni chiave](../tutorials/aas-lesson-7-create-key-performance-indicators.md).  
  
## <a name="create-perspectives"></a>Creare prospettive  
  
#### <a name="toocreate-an-internet-sales-perspective"></a>toocreate una prospettiva Internet Sales  
  
1.  Fare clic su hello **modello** menu > **prospettive** > **crea e Gestisci**.  
  
2.  In hello **prospettive** la finestra di dialogo, fare clic su **nuova prospettiva**.  
  
3.  Fare doppio clic su hello **nuova prospettiva** intestazione di colonna e quindi rinominare **Internet Sales**.  
  
4.  Selezionare hello tutte le tabelle di hello *tranne* **DimCustomer**.  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    In una lezione successiva, utilizzare hello analizza in Excel funzionalità tootest questa prospettiva. Hello elenco campi tabella pivot di Excel include ogni tabella ad eccezione di tabella DimCustomer hello.  

## <a name="whats-next"></a>Passaggi successivi
[Lezione 9: Creare gerarchie](../tutorials/aas-lesson-9-create-hierarchies.md).
  
  
  
  
