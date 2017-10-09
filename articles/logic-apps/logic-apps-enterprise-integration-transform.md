---
title: dati XML aaaConvert con trasformazioni - App Azure per la logica | Documenti Microsoft
description: Creare trasformazioni o mapps tooconvert dei dati XML tra formati di App per la logica tramite hello Enterprise Integration SDK
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: add01429-21bc-4bab-8b23-bc76ba7d0bde
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: b56ec1072c5058d3aefc7f88ac9b2748ebe56456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a>Enterprise Integration con trasformazioni XML
## <a name="overview"></a>Panoramica
connettore di trasformazione di Hello Enterprise integration converte i dati da un formato di tooanother di formato. Ad esempio, si dispone di un messaggio in arrivo che contiene la data corrente nel formato YearMonthDay hello di hello. È possibile utilizzare una data toobe di trasformazione tooreformat hello in formato MonthDayYear hello.

## <a name="what-does-a-transform-do"></a>Funzioni della trasformazione
Una trasformazione, è anche noto come una mappa, è costituito da uno schema di origine XML (Buongiorno input) e uno schema XML di destinazione (output di hello). È possibile utilizzare diverse funzioni predefinite toohelp modificare o controllare hello dati, quali stringhe, le assegnazioni condizionale, espressioni aritmetiche, formattatori ora data e anche i costrutti di ciclo.

## <a name="how-toocreate-a-transform"></a>Come una trasformazione toocreate?
È possibile creare una mappa di trasformazione o utilizzando Visual Studio hello [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas). Quando si è finito di creare e testare le trasformazione hello, caricare hello trasformazione all'account di integrazione. 

## <a name="how-toouse-a-transform"></a>Come toouse una trasformazione
Dopo aver caricato trasformazione hello/eseguire il mapping all'account di integrazione, è possibile utilizzare toocreate un'app di logica. Hello logica app esegue le trasformazioni, ogni volta che viene attivato l'app per la logica hello (e il contenuto di input non deve toobe trasformato viene).

**Ecco una trasformazione hello passaggi toouse**:

### <a name="prerequisites"></a>Prerequisiti

* Creare un account di integrazione e aggiungere una mappa tooit  

Ora che è stato preso in considerazione i prerequisiti di hello, è possibile ora toocreate app logica:  

1. Creare un'app di logica e [collegarlo account integrazione tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md "informazioni toolink un'app di logica di integrazione account tooa") che contiene la mappa hello.
2. Aggiungere un **richiesta** trigger tooyour logica app  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. Aggiungi hello **trasformare XML** azione selezionando prima **aggiungere un'azione**   
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. Immettere la parola hello *trasformare* in toofilter casella di ricerca hello tutti hello toohello azioni uno che si desidera toouse  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. Seleziona hello **trasformare XML** azione   
6. Aggiungere hello XML **contenuto** che è la trasformazione. È possibile utilizzare tutti i dati XML viene visualizzato nella richiesta HTTP hello come hello **contenuto**. In questo esempio, selezionare corpo hello della richiesta HTTP hello che ha attivato hello logica app.
7. Nome selezionare hello di hello **mappa** che si desidera che toouse tooperform hello trasformazione. mappa di Hello devono essere già nell'account di integrazione. In un passaggio precedente, è già assegnato la logica app tooyour integrazione account di accesso che contiene la mappa.      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. Salvare il lavoro   
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

A questo punto, la configurazione della mappa è completa. In un'applicazione reale, si consiglia di dati trasformato hello toostore in un'applicazione LOB, ad esempio SalesForce. È possibile trasformare facilmente come azione toosend hello output di hello tooSalesforce. 

È ora possibile testare la trasformazione, eseguendo un endpoint HTTP toohello di richiesta.  

## <a name="features-and-use-cases"></a>Funzionalità e casi d'uso
* trasformazione Hello creato in una mappa può essere semplice, ad esempio la copia di un nome e indirizzo da un documento tooanother. In alternativa, è possibile creare trasformazioni più complesse mediante operazioni di mapping della casella di hello.  
* Sono già disponibili più operazioni o funzioni di mapping, incluse stringhe, funzioni data/ora e così via.  
* È possibile eseguire una copia diretta dei dati tra schemi hello. In hello che Mapper è incluso in hello SDK, questo è semplice come disegnare una linea che collega gli elementi di hello nello schema di origine hello con le controparti nello schema di destinazione hello.  
* Quando si crea una mappa, si visualizza una rappresentazione grafica della mappa hello, che mostra tutte le relazioni di hello e collegamenti creati.
* Utilizzare hello Test mappa funzionalità tooadd un messaggio XML di esempio. Con un semplice clic, è possibile testare una mappa hello è stato creato e visualizzato un output di hello generato.  
* Caricare le mappe esistenti  
* Include il supporto per il formato XML hello.

## <a name="learn-more"></a>Altre informazioni
* [Altre informazioni su Enterprise Integration Pack hello](../logic-apps/logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack")  
* [Altre informazioni sulle mappe](../logic-apps/logic-apps-enterprise-integration-maps.md "Informazioni sulle mappe di Enterprise Integration")  

