---
title: connettore di Informix hello aaaAdd nelle App logica | Documenti Microsoft
description: Panoramica del connettore Informix con i parametri dell'API REST
services: 
documentationcenter: 
author: gplarsen
manager: anneta
editor: 
tags: connectors
ms.assetid: ca2393f0-3073-4dc2-8438-747f5bc59689
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/26/2016
ms.author: plarsen; ladocs
ms.openlocfilehash: 7a163e2ebf00fa3109b93e34845d922c2174a48d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-informix-connector"></a>Iniziare con il connettore di Informix hello
Microsoft connector per Informix connette tooresources logica App archiviati in un database IBM Informix. il connettore di Informix Hello comprende un computer server di Microsoft client toocommunicate tooremote Informix attraverso una rete TCP/IP. Questo include database cloud, ad esempio IBM Informix per Windows in esecuzione in Azure virtualizzazione e i database che utilizzano gateway dati locale di hello locale. Vedere hello [supportati elenco](connectors-create-api-informix.md#supported-informix-platforms-and-versions) di IBM Informix piattaforme e le versioni (in questo argomento).

connettore Hello supporta hello operazioni di database seguenti:

* Visualizzazione di un elenco delle tabelle di database
* Lettura di una riga con SELECT
* Lettura di tutte le righe con SELECT
* Aggiunta di una riga con INSERT
* Modifica di una riga con UPDATE
* Rimozione di una riga con DELETE

Questo argomento viene illustrato come le operazioni del database in un tooprocess app logica del connettore hello toouse.

toolearn informazioni sulle App per la logica, vedere [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="available-actions"></a>Azioni disponibili
Questo connettore supporta hello azioni di app la logica seguente:

* GetTables
* GetRow
* GetRows
* InsertRow
* UpdateRow
* DeleteRow

## <a name="list-tables"></a>Visualizzazione di un elenco di tabelle
Creazione di un'app di logica per qualsiasi operazione è costituita da numerosi passaggi, eseguiti tramite il portale di Microsoft Azure hello.

All'interno di hello logica app, è possibile aggiungere le tabelle toolist un'azione in un database di Informix. Questa azione indica hello connettore tooprocess un'istruzione di schema, Informix, ad esempio `CALL SYSIBM.SQLTABLES`.

### <a name="create-a-logic-app"></a>Creare un'app per la logica
1. In hello **Azure avviare discussioni**selezionare  **+**  (segno), **Web e dispositivi mobili**e quindi **logica App**.
2. Immettere hello **nome**, ad esempio `InformixgetTables`, **sottoscrizione**, **gruppo di risorse**, **percorso**, e **App Piano di servizio**. Selezionare **Pin toodashboard**, quindi selezionare **crea**.

### <a name="add-a-trigger-and-action"></a>Aggiungere un trigger e un'azione
1. In hello **logica App progettazione**selezionare **LogicApp vuoto** in hello **modelli** elenco.
2. In hello **trigger** elenco, selezionare **ricorrenza**. 
3. In hello **ricorrenza** trigger, selezionare **modifica**selezionare **frequenza** tooselect elenco a discesa **giorno**, quindi selezionare  **Intervallo** tootype **7**.  
4. Seleziona hello **+ nuovo passaggio** e quindi selezionare **aggiungere un'azione**.
5. In hello **azioni** elenco, digitare **informix** in hello **cercare altre azioni** casella di modifica e quindi selezionare **Informix - Get tabelle (anteprima)**.
   
   ![](./media/connectors-create-api-informix/InformixconnectorActions.png)  
6. In hello **Informix - Get tabelle** riquadro configurazione, selezionare **casella di controllo** tooenable **Connetti tramite il gateway dati locale**. Si noti che le impostazioni di hello cambiano da cloud tooon locale.
   
   * Tipo di valore per **Server**, nel formato hello indirizzo o alias virgola numero di porta. Ad esempio digitare `ibmserver01:9089`.
   * Digitare un valore in **Database**. Ad esempio digitare `nwind`.
   * Selezionare un valore in **Autenticazione**, ad esempio **Basic**.
   * Digitare un valore in **Nome utente**. Ad esempio digitare `informix`.
   * Digitare un valore in **Password**. Ad esempio digitare `Password1`.
   * Selezionare un valore in **Gateway**, ad esempio, selezionare **datagateway01**.
7. Selezionare **Crea** e quindi **Salva**. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorOnPremisesDataGatewayConnection.png)
8. In hello **InformixgetTables** pannello all'interno di hello **tutte le esecuzioni** elenco sotto **riepilogo**, selezionare hello elencate al primo elemento (esecuzione più recente).
9. In hello **app per eseguire la logica** pannello seleziona **Dettagli esecuzione**. All'interno di hello **azione** elenco, selezionare **Get_tables**. Visualizzare il valore hello **stato**, che deve essere **Succeeded**. Seleziona hello **collegamento di input** input hello tooview. Seleziona hello **collegamento di output**e restituisce hello visualizzazione, che deve includere un elenco di tabelle.
   
   ![](./media/connectors-create-api-informix/InformixconnectorGetTablesLogicAppRunOutputs.png)

## <a name="create-hello-connections"></a>Creare connessioni hello
Questo connettore supporta connessioni toodatabase locale e nel cloud hello utilizzando hello seguenti proprietà di connessione. 

| Proprietà | Descrizione |
| --- | --- |
| server |Obbligatorio. Accetta un valore stringa che rappresenta un alias o un indirizzo TCP/IP, in formato IPv4 o IPv6, delimitato da due punti e seguito da un numero di porta TCP/IP. |
| database |Obbligatorio. Accetta un valore stringa che rappresenta un nome di database relazionale (RDBNAM) DRDA. Informix accetta una stringa di 128 byte (il database è definito come nome di database IBM Informix, ovvero come dbname). |
| authentication |facoltativo. Accetta un valore elemento di elenco, ovvero Basic o Windows (kerberos). |
| username |Obbligatorio. Accetta il valore della stringa. |
| password |Obbligatorio. Accetta il valore della stringa. |
| gateway |Obbligatorio. Accetta un valore di elemento di elenco, che rappresenta hello locale dati gateway definito tooLogic App del gruppo di archiviazione hello. |

## <a name="create-hello-on-premises-gateway-connection"></a>Creare hello locale connessione gateway
Questo connettore può accedere a un database di Informix locale tramite gateway dati locale di hello. Per altre informazioni, vedere gli argomenti relativi al gateway. 

1. In hello **gateway** riquadro configurazione, selezionare **casella di controllo** tooenable **connessione tramite gateway**. Vedere hello modifica delle impostazioni dal cloud tooon locale.
2. Tipo di valore per **Server**, nel formato hello indirizzo o alias virgola numero di porta. Ad esempio digitare `ibmserver01:9089`.
3. Digitare un valore in **Database**. Ad esempio digitare `nwind`.
4. Selezionare un valore in **Autenticazione**, ad esempio **Basic**.
5. Digitare un valore in **Nome utente**. Ad esempio digitare `informix`.
6. Digitare un valore in **Password**. Ad esempio digitare `Password1`.
7. Selezionare un valore in **Gateway**, ad esempio, selezionare **datagateway01**.
8. Selezionare **crea** toocontinue. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorOnPremisesDataGatewayConnection.png)

## <a name="create-hello-cloud-connection"></a>Creare una connessione di cloud hello
Il connettore può accedere a un database Informix cloud. 

1. In hello **gateway** riquadro configurazione, lasciare hello **casella di controllo** disabilitato (collegamento) **connessione tramite gateway**. 
2. Digitare un valore in **Nome connessione**. Ad esempio digitare `hisdemo2`.
3. Tipo di valore per **nome del server Informix**, nel formato hello indirizzo o alias virgola numero di porta. Ad esempio digitare `hisdemo2.cloudapp.net:9089`.
4. Digitare un valore per il nome del database Informix in **Database**. Ad esempio digitare `nwind`.
5. Digitare un valore in **Nome utente**. Ad esempio digitare `informix`.
6. Digitare un valore in **Password**. Ad esempio digitare `Password1`.
7. Selezionare **crea** toocontinue. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorCloudConnection.png)

## <a name="fetch-all-rows-using-select"></a>Recuperare tutte le righe con SELECT
È possibile creare un toofetch di azione logica app tutte le righe nella tabella di Informix hello. Questa azione indica hello connettore tooprocess un'istruzione SELECT di Informix, ad esempio `SELECT * FROM AREA`.

### <a name="create-a-logic-app"></a>Creare un'app per la logica
1. In hello **Azure avviare discussioni**selezionare  **+**  (segno), **Web e dispositivi mobili**e quindi **logica App**.
2. Immettere hello **nome** (ad esempio, "**InformixgetRows**"), **Sottoscrizione**, **Gruppo di risorse**, **Località** e **Piano di servizio app**. Selezionare **Pin toodashboard**, quindi selezionare **crea**.

### <a name="add-a-trigger-and-action"></a>Aggiungere un trigger e un'azione
1. In hello **logica App progettazione**selezionare **LogicApp vuoto** in hello **modelli** elenco.
2. In hello **trigger** elenco, selezionare **ricorrenza**. 
3. In hello **ricorrenza** trigger, selezionare **modifica**selezionare **frequenza** tooselect elenco a discesa **giorno**, quindi selezionare  **Intervallo** tootype **7**. 
4. Seleziona hello **+ nuovo passaggio** e quindi selezionare **aggiungere un'azione**.
5. In hello **azioni** elenco, digitare **informix** in hello **cercare altre azioni** casella di modifica e quindi selezionare **Informix - Get righe (anteprima)** .
6. In hello **ottenere righe (anteprima)** azione, selezionare **Cambia connessione**.
7. In hello **connessioni** riquadro configurazione, selezionare **Crea nuovo**. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorNewConnection.png)
8. In hello **gateway** riquadro configurazione, lasciare hello **casella di controllo** disabilitato (collegamento) **connessione tramite gateway**.
   
   * Digitare un valore in **Nome connessione**. Ad esempio digitare `HISDEMO2`.
   * Tipo di valore per **nome del server Informix**, nel formato hello indirizzo o alias virgola numero di porta. Ad esempio digitare `HISDEMO2.cloudapp.net:9089`.
   * Digitare un valore per il nome del database Informix in **Database**. Ad esempio digitare `NWIND`.
   * Digitare un valore in **Nome utente**. Ad esempio digitare `informix`.
   * Digitare un valore in **Password**. Ad esempio digitare `Password1`.
9. Selezionare **crea** toocontinue.
   
    ![](./media/connectors-create-api-informix/InformixconnectorCloudConnection.png)
10. In hello **nome tabella** elenco, seleziona hello **freccia giù**, quindi selezionare **AREA**.
11. Facoltativamente, selezionare **Visualizza le opzioni avanzate** toospecify opzioni di query.
12. Selezionare **Salva**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowsTableName.png)
13. In hello **InformixgetRows** pannello all'interno di hello **tutte le esecuzioni** elenco sotto **riepilogo**, selezionare hello elencate al primo elemento (esecuzione più recente).
14. In hello **app per eseguire la logica** pannello seleziona **Dettagli esecuzione**. All'interno di hello **azione** elenco, selezionare **Get_rows**. Visualizzare il valore hello **stato**, che deve essere **Succeeded**. Seleziona hello **collegamento di input** input hello tooview. Seleziona hello **collegamento di output**e restituisce hello visualizzazione, che deve includere un elenco di righe.
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowsOutputs.png)

## <a name="add-one-row-using-insert"></a>Aggiunta di una riga con INSERT
È possibile creare una logica app azione tooadd una riga in una tabella di Informix. Questa azione indica hello connettore tooprocess un'istruzione INSERT Informix, ad esempio `INSERT INTO AREA (AREAID, AREADESC, REGIONID) VALUES ('99999', 'Area 99999', 102)`.

### <a name="create-a-logic-app"></a>Creare un'app per la logica
1. In hello **Azure avviare discussioni**selezionare  **+**  (segno), **Web e dispositivi mobili**e quindi **logica App**.
2. Immettere hello **nome**, ad esempio `InformixinsertRow`, **sottoscrizione**, **gruppo di risorse**, **percorso**, e **App Piano di servizio**. Selezionare **Pin toodashboard**, quindi selezionare **crea**.

### <a name="add-a-trigger-and-action"></a>Aggiungere un trigger e un'azione
1. In hello **logica App progettazione**selezionare **LogicApp vuoto** in hello **modelli** elenco.
2. In hello **trigger** elenco, selezionare **ricorrenza**. 
3. In hello **ricorrenza** trigger, selezionare **modifica**selezionare **frequenza** tooselect elenco a discesa **giorno**, quindi selezionare  **Intervallo** tootype **7**. 
4. Seleziona hello **+ nuovo passaggio** e quindi selezionare **aggiungere un'azione**.
5. In hello **azioni** elenco, digitare **informix** in hello **cercare altre azioni** casella di modifica e quindi selezionare **Informix - riga di inserimento (anteprima)**.
6. In hello **ottenere righe (anteprima)** azione, selezionare **Cambia connessione**. 
7. In hello **connessioni** riquadro Configurazione tooselect selezionare una connessione. ad esempio, selezionare **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. In hello **nome tabella** elenco, seleziona hello **freccia giù**, quindi selezionare **AREA**.
9. Immettere valori per tutte le colonne obbligatorie (asterisco rosso). Ad esempio digitare `99999` per **AREAID** e `Area 99999``102` per **REGIONID**. 
10. Selezionare **Salva**.
    
    ![](./media/connectors-create-api-informix/InformixconnectorInsertRowValues.png)
11. In hello **InformixinsertRow** pannello all'interno di hello **tutte le esecuzioni** elenco sotto **riepilogo**, selezionare hello elencate al primo elemento (esecuzione più recente).
12. In hello **app per eseguire la logica** pannello seleziona **Dettagli esecuzione**. All'interno di hello **azione** elenco, selezionare **Get_rows**. Visualizzare il valore hello **stato**, che deve essere **Succeeded**. Seleziona hello **collegamento di input** input hello tooview. Seleziona hello **collegamento di output**e restituisce hello di visualizzazione, che deve includere una nuova riga hello.
    
    ![](./media/connectors-create-api-informix/InformixconnectorInsertRowOutputs.png)

## <a name="fetch-one-row-using-select"></a>Recuperare una riga con SELECT
È possibile creare una logica app azione toofetch una riga in una tabella di Informix. Questa azione indica hello connettore tooprocess un'istruzione Informix selezionare in cui, ad esempio `SELECT FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Creare un'app per la logica
1. In hello **Azure avviare discussioni**selezionare  **+**  (segno), **Web e dispositivi mobili**e quindi **logica App**.
2. Immettere hello **nome**, ad esempio `InformixgetRow`, **sottoscrizione**, **gruppo di risorse**, **percorso**, e **App Piano di servizio**. Selezionare **Pin toodashboard**, quindi selezionare **crea**.

### <a name="add-a-trigger-and-action"></a>Aggiungere un trigger e un'azione
1. In hello **logica App progettazione**selezionare **LogicApp vuoto** in hello **modelli** elenco.
2. In hello **trigger** elenco, selezionare **ricorrenza**. 
3. In hello **ricorrenza** trigger, selezionare **modifica**selezionare **frequenza** tooselect elenco a discesa **giorno**, quindi selezionare  **Intervallo** tootype **7**. 
4. Seleziona hello **+ nuovo passaggio** e quindi selezionare **aggiungere un'azione**.
5. In hello **azioni** elenco, digitare **informix** in hello **cercare altre azioni** casella di modifica e quindi selezionare **Informix - Get righe (anteprima)** .
6. In hello **ottenere righe (anteprima)** azione, selezionare **Cambia connessione**. 
7. In hello **connessioni** riquadro configurazioni, selezionare tooselect una connessione esistente. ad esempio, selezionare **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. In hello **nome tabella** elenco, seleziona hello **freccia giù**, quindi selezionare **AREA**.
9. Immettere valori per tutte le colonne obbligatorie (asterisco rosso). Ad esempio digitare `99999` per **AREAID**. 
10. Facoltativamente, selezionare **Visualizza le opzioni avanzate** toospecify opzioni di query.
11. Selezionare **Salva**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowValues.png)
12. In hello **InformixgetRow** pannello all'interno di hello **tutte le esecuzioni** elenco sotto **riepilogo**, selezionare hello elencate al primo elemento (esecuzione più recente).
13. In hello **app per eseguire la logica** pannello seleziona **Dettagli esecuzione**. All'interno di hello **azione** elenco, selezionare **Get_rows**. Visualizzare il valore hello **stato**, che deve essere **Succeeded**. Seleziona hello **collegamento di input** input hello tooview. Seleziona hello **collegamento di output**e restituisce hello visualizzazione, che deve includere una riga.
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowOutputs.png)

## <a name="change-one-row-using-update"></a>Modificare una riga con UPDATE
È possibile creare una logica app azione toochange una riga in una tabella di Informix. Questa azione indica hello connettore tooprocess un'istruzione UPDATE Informix, ad esempio `UPDATE AREA SET AREAID = '99999', AREADESC = 'Area 99999', REGIONID = 102)`.

### <a name="create-a-logic-app"></a>Creare un'app per la logica
1. In hello **Azure avviare discussioni**selezionare  **+**  (segno), **Web e dispositivi mobili**e quindi **logica App**.
2. Immettere hello **nome**, ad esempio `InformixupdateRow`, **sottoscrizione**, **gruppo di risorse**, **percorso**, e **App Piano di servizio**. Selezionare **Pin toodashboard**, quindi selezionare **crea**.

### <a name="add-a-trigger-and-action"></a>Aggiungere un trigger e un'azione
1. In hello **logica App progettazione**selezionare **LogicApp vuoto** in hello **modelli** elenco.
2. In hello **trigger** elenco, selezionare **ricorrenza**. 
3. In hello **ricorrenza** trigger, selezionare **modifica**selezionare **frequenza** tooselect elenco a discesa **giorno**, quindi selezionare  **Intervallo** tootype **7**. 
4. Seleziona hello **+ nuovo passaggio** e quindi selezionare **aggiungere un'azione**.
5. In hello **azioni** elenco, digitare **informix** in hello **cercare altre azioni** casella di modifica e quindi selezionare **Informix - riga aggiornamento (anteprima)**.
6. In hello **ottenere righe (anteprima)** azione, selezionare **Cambia connessione**. 
7. In hello **connessioni** riquadro configurazioni, selezionare tooselect una connessione esistente. ad esempio, selezionare **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. In hello **nome tabella** elenco, seleziona hello **freccia giù**, quindi selezionare **AREA**.
9. Immettere valori per tutte le colonne obbligatorie (asterisco rosso). Ad esempio digitare `99999` per **AREAID** e `Updated 99999``102` per **REGIONID**. 
10. Selezionare **Salva**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorUpdateRowValues.png)
11. In hello **InformixupdateRow** pannello all'interno di hello **tutte le esecuzioni** elenco sotto **riepilogo**, selezionare hello elencate al primo elemento (esecuzione più recente).
12. In hello **app per eseguire la logica** pannello seleziona **Dettagli esecuzione**. All'interno di hello **azione** elenco, selezionare **Get_rows**. Visualizzare il valore hello **stato**, che deve essere **Succeeded**. Seleziona hello **collegamento di input** input hello tooview. Seleziona hello **collegamento di output**e restituisce hello di visualizzazione, che deve includere una nuova riga hello.
    
    ![](./media/connectors-create-api-informix/InformixconnectorUpdateRowOutputs.png)

## <a name="remove-one-row-using-delete"></a>Rimozione di una riga con DELETE
È possibile creare una logica app azione tooremove una riga in una tabella di Informix. Questa azione indica hello connettore tooprocess un'istruzione DELETE Informix, ad esempio `DELETE FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Creare un'app per la logica
1. In hello **Azure avviare discussioni**selezionare  **+**  (segno), **Web e dispositivi mobili**e quindi **logica App**.
2. Immettere hello **nome**, ad esempio `InformixdeleteRow`, **sottoscrizione**, **gruppo di risorse**, **percorso**, e **App Piano di servizio**. Selezionare **Pin toodashboard**, quindi selezionare **crea**.

### <a name="add-a-trigger-and-action"></a>Aggiungere un trigger e un'azione
1. In hello **logica App progettazione**selezionare **LogicApp vuoto** in hello **modelli** elenco.
2. In hello **trigger** elenco, selezionare **ricorrenza**. 
3. In hello **ricorrenza** trigger, selezionare **modifica**selezionare **frequenza** tooselect elenco a discesa **giorno**, quindi selezionare  **Intervallo** tootype **7**. 
4. Seleziona hello **+ nuovo passaggio** e quindi selezionare **aggiungere un'azione**.
5. In hello **azioni** elenco, digitare **informix** in hello **cercare altre azioni** casella di modifica e quindi selezionare **Informix - Elimina riga (anteprima)**.
6. In hello **ottenere righe (anteprima)** azione, selezionare **Cambia connessione**. 
7. In hello **connessioni** riquadro configurazioni, selezionare una connessione esistente. ad esempio, selezionare **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. In hello **nome tabella** elenco, seleziona hello **freccia giù**, quindi selezionare **AREA**.
9. Immettere valori per tutte le colonne obbligatorie (asterisco rosso). Ad esempio digitare `99999` per **AREAID**. 
10. Selezionare **Salva**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorDeleteRowValues.png)
11. In hello **InformixdeleteRow** pannello all'interno di hello **tutte le esecuzioni** elenco sotto **riepilogo**, selezionare hello elencate al primo elemento (esecuzione più recente).
12. In hello **app per eseguire la logica** pannello seleziona **Dettagli esecuzione**. All'interno di hello **azione** elenco, selezionare **Get_rows**. Visualizzare il valore hello **stato**, che deve essere **Succeeded**. Seleziona hello **collegamento di input** input hello tooview. Seleziona hello **collegamento di output**e hello visualizzazione output, che deve includere la riga hello eliminato.
    
    ![](./media/connectors-create-api-informix/InformixconnectorDeleteRowOutputs.png)

## <a name="supported-informix-platforms-and-versions"></a>Piattaforme e versioni di Informix supportate
Questo connettore supporta hello seguenti versioni di IBM Informix, configurato le connessioni client toosupport Distributed Relational Database Architecture (DRDA).

* IBM Informix 12.1
* IBM Informix 11.7

## <a name="connector-specific-details"></a>Dettagli specifici del connettore

Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/informix/). 

## <a name="next-steps"></a>Passaggi successivi
[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md). Esplorare hello altri connettori disponibile in App per la logica nel nostro [elenco API](apis-list.md).

