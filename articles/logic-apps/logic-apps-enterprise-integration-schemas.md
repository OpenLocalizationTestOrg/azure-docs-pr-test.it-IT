---
title: aaaSchemas per la convalida XML - App Azure per la logica | Documenti Microsoft
description: Convalida dei documenti XML con gli schemi per le app per la logica di Azure ed Enterprise Integration Pack
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 56c5846c-5d8c-4ad4-9652-60b07aa8fc3b
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 87cf92741e10ff7cccd260f27442909e34928903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-hello-enterprise-integration-pack"></a>Convalida XML con schemi per le app di logica di Azure e hello Enterprise Integration Pack

Schemi confermare che si riceve i documenti XML hello siano validi e sia hello previsto i dati in un formato predefinito. Gli schemi vengono usati inoltre per convalidare i messaggi scambiati in uno scenario B2B.

## <a name="add-a-schema"></a>Aggiungere uno schema

1. Nel portale di Azure hello, selezionare **più servizi**.

    ![Portale di Azure, "More services" (Altri servizi)](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. Nella casella di ricerca hello filtro immettere **integrazione**e selezionare **account di integrazione** dall'elenco dei risultati di hello.

    ![Casella di ricerca del filtro](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. Seleziona hello **account integrazione** in cui si desidera schema hello tooadd.

    ![Elenco degli account di integrazione](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. Scegliere hello **schemi** riquadro.

    ![Esempio di account di integrazione, "Schemi"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a>Aggiungere un file di schema di dimensioni inferiori a 2 MB

1. In hello **schemi** blade che viene visualizzata (da hello passaggi precedenti), scegliere **Aggiungi**.

    ![Pannello Schemi, "Aggiungi"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. Immettere un nome per lo schema. Caricare il file di schema hello selezionando hello cartella icona Avanti toohello **Schema** casella. Al termine del processo di caricamento hello, **OK**.

    ![Screenshot di "Aggiungi schema", con "File piccolo" evidenziato](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-too8-mb-maximum"></a>Aggiungere un file di schema maggiore di 2 MB (backup di un massimo di too8 MB)

Questi passaggi sono diversi in base ai livelli di accesso di contenitore blob hello: **pubblica** o **Nessun accesso anonimo**.

**toodetermine questo livello di accesso**

1.  Aprire **Azure Storage Explorer** (Esplora archivi di Azure). 

2.  In **contenitori Blob**, selezionare il contenitore di blob hello desiderato. 

3.  Selezionare **Sicurezza**, **Livello di accesso**.

Se è a livello di accesso di sicurezza blob hello **pubblica**, seguire questi passaggi.

![Azure Storage Explorer con evidenziate le opzioni "Contenitori BLOB", "Sicurezza" e "Pubblico"](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. Caricare l'account di archiviazione tooyour schema hello e copiare hello URI.

    ![Account di archiviazione con URI evidenziato](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. In **Aggiungi Schema**selezionare **file di grandi dimensioni**e fornire Ciao URI hello **URI contenuto** casella di testo.

    ![Schemi con evidenziati il pulsante "Aggiungi" e l'opzione "Large file" (File grande)](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

Se è a livello di accesso di sicurezza blob hello **Nessun accesso anonimo**, seguire questi passaggi.

![Azure Storage Explorer, con evidenziate le opzioni "Contenitori BLOB", "Sicurezza" e "No anonymous access" (Nessun accesso anonimo)](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. Caricare l'account di archiviazione tooyour hello dello schema.

    ![Account di archiviazione](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. Generare una firma di accesso condiviso per lo schema di hello.

    ![Account di archiviazione con evidenziata la scheda delle firme di accesso condiviso](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. In **Aggiungi Schema**selezionare **file di grandi dimensioni**e fornire una firma di accesso condiviso hello URI in hello **URI contenuto** casella di testo.

    ![Schemi con evidenziati il pulsante "Aggiungi" e l'opzione "Large file" (File grande)](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. In hello **schemi** pannello dell'account di integrazione, dovrebbe essere visualizzato il nuovo schema.

    ![L'account di integrazione, con "Schemi" e il nuovo schema hello evidenziato](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a>Modificare gli schemi

1. Scegliere hello **schemi** riquadro.

2. Dopo aver hello **schemi** pannello consente di aprire, schema selezionare hello che si desidera tooedit.

3. In hello **schemi** pannello, scegliere **modifica**.

    ![Pannello Schemi](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. File di schema selezionare hello che si desidera tooedit, quindi selezionare **aprire**.

    ![Apri schema file tooedit](media/logic-apps-enterprise-integration-schemas/edit-31.png)

Azure Visualizza un messaggio che hello schema caricato correttamente.

## <a name="delete-schemas"></a>Eliminare gli schemi

1. Scegliere hello **schemi** riquadro.

2. Dopo aver hello **schemi** pannello consente di aprire, schema selezionare hello desiderato toodelete.

3. In hello **schemi** pannello, scegliere **eliminare**.

    ![Pannello Schemi](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. tooconfirm che si desidera toodelete hello selezionata dello schema, scegliere **Sì**.

    ![Messaggio di conferma "Elimina schema"](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    In hello **schemi** pannello elenco schema hello viene aggiornata e non include più schema hello che è stato eliminato.

    ![Account di integrazione con il riquadro "Schemi" evidenziato](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a>Passaggi successivi
* [Altre informazioni su Enterprise Integration Pack hello](logic-apps-enterprise-integration-overview.md "informazioni sul pacchetto di integrazione di enterprise hello").  

