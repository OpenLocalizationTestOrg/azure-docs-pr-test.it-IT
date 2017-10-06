---
title: un servizio Web di Machine Learning da Excel aaaConsume | Documenti Microsoft
description: Utilizzo di un servizio Web Azure Machine Learning da Excel | Azure
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a>Utilizzo di un servizio Web Azure Machine Learning da Excel
 Azure Machine Learning Studio rende facile toocall servizi web direttamente da Excel senza hello necessario toowrite qualsiasi codice.

Se si utilizza Excel 2013 (o versioni successive) o Excel Online, si consiglia di utilizzare Excel hello [aggiuntivo di Excel](machine-learning-excel-add-in-for-web-services.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a>Passi
Pubblicazione di un servizio Web. [Questa pagina](machine-learning-walkthrough-5-publish-web-service.md) spiega come toodo è. Funzionalità di cartella di lavoro di Excel hello è attualmente supportata solo per servizi di richiesta/risposta che dispongono di un singolo output (ovvero, un punteggio etichetta singola). 

Dopo aver creato un servizio web, fare clic su hello **servizi WEB** sezione sinistra hello di studio hello e quindi selezionare hello web servizio tooconsume da Excel.

**Servizio Web classico**

1. In hello **DASHBOARD** scheda per il servizio web hello è una riga per hello **richiesta/risposta** servizio. Se questo servizio dispone di un singolo output, dovrebbe essere hello **cartella di lavoro di Excel scaricare** collegamento in tale riga.
   
    ![][1]
2. Fare clic su **Download Excel Workbook**(Scarica cartella di lavoro Excel).

**Nuovo servizio Web**

1. Nel portale del servizio Web di Azure Machine Learning hello, selezionare **consumare**.
2. Nella pagina di consumare, hello hello **opzioni di utilizzo del servizio Web** sezione fare clic sull'icona di Excel hello.

**Utilizzare hello cartella di lavoro**

1. Cartella di lavoro aperto hello.
2. Viene visualizzato un avviso di sicurezza; Fare clic su hello **Abilita modifica** pulsante.
   
    ![][2]
3. Viene visualizzato un avviso di sicurezza. Fare clic su hello **Abilita contenuto** pulsante toorun macro del foglio di calcolo.
   
    ![][3]
4. Una volta attivate le macro, viene generata una tabella. Le colonne sono blu richiesto come input per hello servizio web di record di risorse, o **parametri**. Notare l'output di hello di hello servizio RR, **PREDICTED VALUES** in verde. Quando tutte le colonne per una determinata riga sono riempite, cartella di lavoro hello automaticamente chiama l'API di punteggio hello e Visualizza risultati con punteggio hello.
   
    ![][4]
5. tooscore più di una riga, la seconda riga hello riempimento hello e dati stimati vengono prodotti i valori. È anche possibile incollare più righe contemporaneamente.

È possibile utilizzare una delle caratteristiche di Excel hello (grafici, mappa power, condizionale formattazione e così via) con hello stimato valori toohelp visualizzare i dati di hello.    

## <a name="sharing-your-workbook"></a>Condivisione della cartella di lavoro
Per hello macro toowork, la chiave API deve essere parte del foglio di calcolo hello. Ciò significa che Condividi cartella di lavoro hello solo con le entità utenti singoli che è attendibile.

## <a name="automatic-updates"></a>Aggiornamenti automatici
Una chiamata RRS viene effettuata nei due casi seguenti:

1. Hello prima volta che una riga è contenuto in tutti i relativi **parametri**
2. Ogni volta che uno qualsiasi dei hello **parametri** modifiche in una riga che contiene tutti i relativi **parametri** immesso.

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
