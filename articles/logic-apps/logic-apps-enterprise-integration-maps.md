---
title: aaaTransform XML con XSLT mappe - App Azure per la logica | Documenti Microsoft
description: Aggiungere che XSLT esegue il mapping di dati XML tootransform con le applicazioni di logica di Azure e hello Enterprise Integration Pack
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 90f5cfc4-46b2-4ef7-8ac4-486bb0e3f289
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 720e6f988b8542136dfcc402c3c463fcfb2f23cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-maps-for-xml-data-transform"></a>Aggiungere mappe per la trasformazione dei dati XML

Utilizza integrazione di Enterprise esegue il mapping dei dati XML tootransform tra formati. Una mappa è un documento XML che definisce i dati hello in un documento che deve essere trasformato in un altro formato. 

## <a name="why-use-maps"></a>Perché usare le mappe?

Si supponga che riceve regolarmente B2B ordini o fatture da un cliente che utilizza il formato YYYMMDD hello per le date. All'interno dell'organizzazione, tuttavia, archiviare le date nel formato MMDDYYY hello. È possibile utilizzare una mappa troppo*trasformare* formato di data YYYMMDD hello in hello MMDDYYY prima di archiviare i dettagli dell'ordine o una fattura hello nel database di attività dei clienti.

## <a name="how-do-i-create-a-map"></a>Come si crea una mappa?

È possibile creare progetti di integrazione di BizTalk con hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "informazioni sul pacchetto di integrazione di enterprise hello") per Visual Studio 2015. È quindi possibile creare un file Integration Map che consente di eseguire il mapping visivo degli elementi tra due file di schema XML. Dopo aver compilato il progetto, si disporrà di un documento XSLT.

## <a name="how-do-i-add-a-map"></a>Come si aggiunge una mappa?

1. Nel portale di Azure hello, selezionare **Sfoglia**.

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. Nella casella di ricerca hello filtro immettere **integrazione**, quindi selezionare **account di integrazione** dall'elenco dei risultati di hello.

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. Selezionare l'account di integrazione hello in cui si desidera mappa hello tooadd.

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Seleziona hello **mappe** riquadro.

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. Dopo l'apertura di blade mappe hello, scegliere **Aggiungi**.

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. Immettere un **nome** per la mappa. mappa di hello tooupload file, scegliere l'icona della cartella hello sul lato destro hello di hello **mappa** casella di testo. Al termine del processo di caricamento hello, scegliere **OK**.

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. Dopo che Azure aggiunge l'account di integrazione tooyour hello mappa, viene visualizzato un messaggio sullo schermo che mostra se il file di mapping è stato aggiunto. Dopo il messaggio viene visualizzato, scegliere hello **mappe** riquadro in modo da visualizzare hello appena aggiunto mappa.

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a>Come si modifica una mappa?

È necessario caricare un nuovo file di mappa con modifiche hello che si desidera. È possibile scaricare innanzitutto mappa hello per la modifica.

tooupload una nuova mappa che sostituisce una mappa esistente hello, seguire questi passaggi.

1. Scegliere hello **mappe** riquadro.

2. Dopo l'apertura di blade mappe hello, selezionare la mappa di hello che si desidera tooedit.

3. In hello **mappe** pannello, scegliere **aggiornamento**.

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. In selezione file hello, selezionare i file di mappa hello che si desidera tooupload, quindi selezionare **aprire**.

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-toodelete-a-map"></a>Come toodelete una mappa?

1. Scegliere hello **mappe** riquadro.

2. Dopo l'apertura di blade mappe hello, selezionare mappa hello che si desidera toodelete.

3. Scegliere **Elimina**.

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. Confermare che si desidera mappa hello toodelete.

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a>Passaggi successivi
* [Altre informazioni su Enterprise Integration Pack hello](logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack")  
* [Altre informazioni sui contratti](../logic-apps/logic-apps-enterprise-integration-agreements.md "Informazioni sui contratti di Enterprise Integration")  
* [Altre informazioni sulle trasformazioni](logic-apps-enterprise-integration-transform.md "Informazioni sulle trasformazioni di Enterprise Integration")  

