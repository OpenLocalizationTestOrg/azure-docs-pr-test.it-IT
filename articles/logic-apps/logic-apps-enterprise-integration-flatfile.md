---
title: aaaEncode o decodificare file flat in App per la logica di Azure | Documenti Microsoft
description: Come toouse hello file file codificatore o un decodificatore in hello Enterprise Integration Pack nelle app di logica
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 82152dab-c7ad-43df-b721-596559703be8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 2c295586625fd84366ec7cbafdcebf0489ba234d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-enterprise-integration-with-flat-files"></a>Informazioni generali sull'integrazione aziendale con file flat

È opportuno tooencode XML contenuto prima di inviare il partner commerciale tooa in uno scenario business-to-business (B2B). In un'app di logica, è possibile utilizzare file flat di hello codifica questo connettore toodo. Hello logica app che crei può ottenere il codice XML contenuto da un'ampia gamma di origini, ad esempio da un trigger di richiesta HTTP, da un'altra applicazione o anche da una delle hello molti [connettori](../connectors/apis-list.md). Per ulteriori informazioni sulle App per la logica, vedere hello [documentazione App logica](logic-apps-what-are-logic-apps.md "altre informazioni sulle App logica").  

## <a name="create-hello-flat-file-encoding-connector"></a>Creare hello connettore di codifica file flat
Seguire questi passaggi tooadd un file flat codifica connettore tooyour logica app.

1. Creare un'app di logica e [collegarlo account integrazione tooyour](logic-apps-enterprise-integration-accounts.md "informazioni toolink un'app di logica di integrazione account tooa"). L'account contiene schema hello si utilizzerà tooencode hello dati XML.  
2. Aggiungere un **richiesta - viene ricevuta la richiesta HTTP quando** trigger tooyour logica app.  
   ![Schermata di trigger tooselect](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)    
3. Aggiungere file flat di hello codifica azione, come indicato di seguito:
   
    a. Seleziona hello **più** sign.
   
    b. Seleziona hello **aggiungere un'azione** collegamento (viene visualizzato dopo aver selezionato hello sul segno più).
   
    c. Nella casella di ricerca hello, immettere *Flat* toofilter tutti hello toohello azioni uno che si desidera toouse.
   
    d. Seleziona hello **codifica File Flat** opzione dall'elenco di hello.   
   ![Screenshot dell'opzione Codifica file flat](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)   
4. In hello **codifica File Flat** la finestra di dialogo, seleziona hello **contenuto** casella di testo.  
   ![Screenshot della casella di testo Contenuto](media/logic-apps-enterprise-integration-flatfile/flatfile-3.png)  
5. Selezionare i tag body hello come contenuto che si desidera tooencode hello. tag body Hello popolerà campo contenuto hello.     
   ![Screenshot del tag body](media/logic-apps-enterprise-integration-flatfile/flatfile-4.png)  
6. Seleziona hello **nome dello Schema** nella casella di riepilogo, quindi scegliere il contenuto di input schema hello desiderato toouse tooencode hello.    
   ![Screenshot della casella di riepilogo Nome schema](media/logic-apps-enterprise-integration-flatfile/flatfile-5.png)  
7. Salvare il lavoro.   
   ![Screenshot dell'icona Salva](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)  

A questo punto la configurazione del connettore di codifica del file flat è completa. In un'applicazione reale, si consiglia di dati con codifica hello toostore in un'applicazione line-of-business, ad esempio Salesforce. Oppure è possibile inviare tale tooa dati codificati partner commerciale. È possibile aggiungere facilmente un output di hello azione toosend di hello codifica azione tooSalesforce o tooyour partner commerciale, utilizzando uno qualsiasi di hello altri connettori forniti.

È ora possibile testare il connettore effettua un endpoint HTTP toohello di richiesta e includere contenuto XML hello nel corpo di hello di hello richiesta.  

## <a name="create-hello-flat-file-decoding-connector"></a>Creare file flat di hello decodifica connettore

> [!NOTE]
> toocomplete questi passaggi, è necessario toohave conto di integrazione è già caricato un file di schema.

1. Aggiungere un **richiesta - viene ricevuta la richiesta HTTP quando** trigger tooyour logica app.  
   ![Schermata di trigger tooselect](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)    
2. Aggiungere file flat di hello decodifica azione, come indicato di seguito:
   
    a. Seleziona hello **più** sign.
   
    b. Seleziona hello **aggiungere un'azione** collegamento (viene visualizzato dopo aver selezionato hello sul segno più).
   
    c. Nella casella di ricerca hello, immettere *Flat* toofilter tutti hello toohello azioni uno che si desidera toouse.
   
    d. Seleziona hello **decodifica del File Flat** opzione dall'elenco di hello.   
   ![Screenshot dell'opzione Decodifica file flat](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)   
3. Seleziona hello **contenuto** controllo. Viene prodotto un elenco di contenuti di hello dai passaggi precedenti che è possibile utilizzare come toodecode contenuto hello. Si noti che hello *corpo* da hello richiesta HTTP in ingresso è disponibile toobe utilizzato come hello toodecode contenuto. È inoltre possibile immettere toodecode contenuto hello direttamente in hello **contenuto** controllo.     
4. Seleziona hello *corpo* tag. Tag body hello di notifica è ora in hello **contenuto** controllo.
5. Selezionare il nome di hello dello schema hello che si desidera di toouse toodecode hello contenuto. Hello cattura di schermata seguente mostra che *OrderFile* è il nome di schema selezionato hello. Questo nome di schema era stato caricato in precedenza conto integrazione hello.
   
   ![Screenshot della finestra di dialogo Decodifica file flat](media/logic-apps-enterprise-integration-flatfile/flatfile-decode-1.png)    
6. Salvare il lavoro.  
   ![Screenshot dell'icona Salva](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)    

A questo punto la configurazione del connettore di decodifica file flat è completa. In un'applicazione reale, è consigliabile dati decodificato hello toostore in un'applicazione line-of-business, ad esempio Salesforce. È possibile aggiungere facilmente un output di hello azione toosend di hello decodifica tooSalesforce di azione.

È ora possibile testare il connettore, eseguendo un endpoint HTTP toohello di richiesta e tra il contenuto XML hello desiderato toodecode nel corpo di hello di hello richiesta.  

## <a name="next-steps"></a>Passaggi successivi
* [Altre informazioni su Enterprise Integration Pack hello](logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack").  

