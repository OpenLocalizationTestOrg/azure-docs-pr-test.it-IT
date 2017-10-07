---
title: connettore DB2 hello aaaAdd nelle App logica | Documenti Microsoft
description: Panoramica del connettore DB2 con i parametri dell'API REST
services: 
documentationcenter: 
author: gplarsen
manager: erikre
editor: 
tags: connectors
ms.assetid: 1c6b010c-beee-496d-943a-a99e168c99aa
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/26/2016
ms.author: plarsen; ladocs
ms.openlocfilehash: d836c61231d3c9cfdb30ff9c40a48b1718f3ffb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-db2-connector"></a>Iniziare con connettore DB2 hello
Connettore Microsoft per DB2 si connette tooresources logica App archiviati in un database IBM DB2. Questo connettore include un toocommunicate client di Microsoft con il computer server DB2 remoti attraverso una rete TCP/IP. Questo include database cloud, ad esempio dashDB IBM Bluemix o IBM DB2 per Windows in esecuzione in Azure virtualizzazione e i database che utilizzano gateway dati locale di hello locale. Vedere hello [supportati elenco](connectors-create-api-db2.md#supported-db2-platforms-and-versions) di piattaforme IBM DB2 e le versioni (in questo argomento).

connettore DB2 Hello supporta hello operazioni di database seguenti:

* Visualizzazione di un elenco delle tabelle di database
* Lettura di una riga con SELECT
* Lettura di tutte le righe con SELECT
* Aggiunta di una riga con INSERT
* Modifica di una riga con UPDATE
* Rimozione di una riga con DELETE

Questo argomento viene illustrato come le operazioni del database in un tooprocess app logica del connettore hello toouse.

toolearn informazioni sulle App per la logica, vedere [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="available-actions"></a>Azioni disponibili
connettore DB2 Hello supporta hello azioni di app la logica seguente:

* GetTables
* GetRow
* GetRows
* InsertRow
* UpdateRow
* DeleteRow

## <a name="list-tables"></a>Visualizzazione di un elenco di tabelle
Creazione di un'app di logica per qualsiasi operazione è costituita da numerosi passaggi, eseguiti tramite il portale di Microsoft Azure hello.

All'interno di hello logica app, è possibile aggiungere le tabelle toolist un'azione in un database DB2. Hello azione indica hello connettore tooprocess un DB2 schema-istruzione, ad esempio `CALL SYSIBM.SQLTABLES`.

### <a name="create-a-logic-app"></a>Creare un'app per la logica
1. In hello **Azure avviare discussioni**selezionare  **+**  (segno), **Web e dispositivi mobili**e quindi **logica App**.
2. Immettere hello **nome**, ad esempio `Db2getTables`, **sottoscrizione**, **gruppo di risorse**, **percorso**, e **App Piano di servizio**. Selezionare **Pin toodashboard**, quindi selezionare **crea**.

### <a name="add-a-trigger-and-action"></a>Aggiungere un trigger e un'azione
1. In hello **logica App progettazione**selezionare **LogicApp vuoto** in hello **modelli** elenco.
2. In hello **trigger** elenco, selezionare **ricorrenza**. 
3. In hello **ricorrenza** trigger, selezionare **modifica**selezionare **frequenza** elenco a discesa tooselect **giorno**, quindi impostare hello **Intervallo** tootype **7**.  
4. Seleziona hello **+ nuovo passaggio** e quindi selezionare **aggiungere un'azione**.
5. In hello **azioni** elenco, digitare `db2` in hello **cercare altre azioni** casella di modifica e quindi selezionare **DB2 - Get tabelle (anteprima)**.
   
   ![](./media/connectors-create-api-db2/Db2connectorActions.png)  
6. In hello **DB2 - Get tabelle** riquadro configurazione, selezionare **casella di controllo** tooenable **Connetti tramite il gateway dati locale**. Si noti che le impostazioni di hello cambiano da cloud tooon locale.
   
   * Tipo di valore per **Server**, nel formato hello indirizzo o alias virgola numero di porta. Ad esempio digitare `ibmserver01:50000`.
   * Digitare un valore in **Database**. Ad esempio digitare `nwind`.
   * Selezionare un valore in **Autenticazione**, ad esempio **Basic**.
   * Digitare un valore in **Nome utente**. Ad esempio digitare `db2admin`.
   * Digitare un valore in **Password**. Ad esempio digitare `Password1`.
   * Selezionare un valore in **Gateway**, ad esempio, selezionare **datagateway01**.
7. Selezionare **Crea** e quindi **Salva**. 
   
    ![](./media/connectors-create-api-db2/Db2connectorOnPremisesDataGatewayConnection.png)
8. In hello **Db2getTables** pannello all'interno di hello **tutte le esecuzioni** elenco sotto **riepilogo**, selezionare hello elencate al primo elemento (esecuzione più recente).
9. In hello **app per eseguire la logica** pannello seleziona **Dettagli esecuzione**. All'interno di hello **azione** elenco, selezionare **Get_tables**. Visualizzare il valore hello **stato**, che deve essere **Succeeded**. Seleziona hello **collegamento di input** input hello tooview. Seleziona hello **collegamento di output**e restituisce hello visualizzazione, che deve includere un elenco di tabelle.
   
   ![](./media/connectors-create-api-db2/Db2connectorGetTablesLogicAppRunOutputs.png)

## <a name="create-hello-connections"></a>Creare connessioni hello
Questo connettore supporta connessioni toodatabases ospitato locale e nel cloud hello utilizzando hello seguenti proprietà di connessione. 

| Proprietà | Descrizione |
| --- | --- |
| server |Obbligatorio. Accetta un valore stringa che rappresenta un alias o un indirizzo TCP/IP, in formato IPv4 o IPv6, delimitato da due punti e seguito da un numero di porta TCP/IP. |
| database |Obbligatorio. Accetta un valore stringa che rappresenta un nome di database relazionale (RDBNAM) DRDA. DB2 per z/OS accetta una stringa di 16 byte (il database è definito come posizione di IBM DB2 per z/OS). DB2 per i5/OS accetta una stringa di 18 byte (il database è definito come database relazionale IBM DB2 per i). DB2 per LUW accetta una stringa di 8 byte. |
| authentication |facoltativo. Accetta un valore elemento di elenco, ovvero Basic o Windows (kerberos). |
| username |Obbligatorio. Accetta il valore della stringa. DB2 per z/OS accetta una stringa di 8 byte. DB2 per i accetta una stringa di 10 byte. DB2 per Linux o UNIX accetta una stringa di 8 byte. DB2 per Windows accetta una stringa di 30 byte. |
| password |Obbligatorio. Accetta il valore della stringa. |
| gateway |Obbligatorio. Accetta un valore di elemento di elenco, che rappresenta hello locale dati gateway definito tooLogic App del gruppo di archiviazione hello. |

## <a name="create-hello-on-premises-gateway-connection"></a>Creare hello locale connessione gateway
Questo connettore può accedere a un database DB2 locale tramite gateway locale hello. Per altre informazioni, vedere gli argomenti relativi al gateway. 

1. In hello **gateway** riquadro configurazione, selezionare **casella di controllo** tooenable **connessione tramite gateway**. Si noti che le impostazioni di hello cambiano da cloud tooon locale.
2. Tipo di valore per **Server**, nel formato hello indirizzo o alias virgola numero di porta. Ad esempio digitare `ibmserver01:50000`.
3. Digitare un valore in **Database**. Ad esempio digitare `nwind`.
4. Selezionare un valore in **Autenticazione**, ad esempio **Basic**.
5. Digitare un valore in **Nome utente**. Ad esempio digitare `db2admin`.
6. Digitare un valore in **Password**. Ad esempio digitare `Password1`.
7. Selezionare un valore in **Gateway**, ad esempio, selezionare **datagateway01**.
8. Selezionare **crea** toocontinue. 
   
    ![](./media/connectors-create-api-db2/Db2connectorOnPremisesDataGatewayConnection.png)

## <a name="create-hello-cloud-connection"></a>Creare una connessione di cloud hello
Il connettore può accedere a un database DB2 cloud. 

1. In hello **gateway** riquadro configurazione, lasciare hello **casella di controllo** disabilitato (collegamento) **connessione tramite gateway**. 
2. Digitare un valore in **Nome connessione**. Ad esempio digitare `hisdemo2`.
3. Tipo di valore per **nome del server DB2**, nel formato hello indirizzo o alias virgola numero di porta. Ad esempio digitare `hisdemo2.cloudapp.net:50000`.
4. Digitare un valore per il nome del database DB2 in **Database**. Ad esempio digitare `nwind`.
5. Digitare un valore in **Nome utente**. Ad esempio digitare `db2admin`.
6. Digitare un valore in **Password**. Ad esempio digitare `Password1`.
7. Selezionare **crea** toocontinue. 
   
    ![](./media/connectors-create-api-db2/Db2connectorCloudConnection.png)

## <a name="fetch-all-rows-using-select"></a>Recuperare tutte le righe con SELECT
È possibile definire un toofetch di azione logica app tutte le righe in una tabella DB2. Indica al connettore di hello tooprocess un'istruzione SELECT di DB2, ad esempio `SELECT * FROM AREA`.

### <a name="create-a-logic-app"></a>Creare un'app per la logica
1. In hello **Azure avviare discussioni**selezionare  **+**  (segno), **Web e dispositivi mobili**e quindi **logica App**.
2. Immettere hello **nome**, ad esempio `Db2getRows`, **sottoscrizione**, **gruppo di risorse**, **percorso**, e **App Piano di servizio**. Selezionare **Pin toodashboard**, quindi selezionare **crea**.

### <a name="add-a-trigger-and-action"></a>Aggiungere un trigger e un'azione
1. In hello **logica App progettazione**selezionare **LogicApp vuoto** in hello **modelli** elenco.
2. In hello **trigger** elenco, selezionare **ricorrenza**. 
3. In hello **ricorrenza** trigger, selezionare **modifica**selezionare **frequenza** tooselect elenco a discesa **giorno**, quindi selezionare  **Intervallo** tootype **7**. 
4. Seleziona hello **+ nuovo passaggio** e quindi selezionare **aggiungere un'azione**.
5. In hello **azioni** elenco, digitare `db2` in hello **cercare altre azioni** casella di modifica e quindi selezionare **DB2 - Get righe (anteprima)**.
6. In hello **ottenere righe (anteprima)** azione, selezionare **Cambia connessione**.
7. In hello **connessioni** riquadro configurazione, selezionare **Crea nuovo**. 
   
    ![](./media/connectors-create-api-db2/Db2connectorNewConnection.png)
8. In hello **gateway** riquadro configurazione, lasciare hello **casella di controllo** disabilitato (collegamento) **connessione tramite gateway**.
   
   * Digitare un valore in **Nome connessione**. Ad esempio digitare `HISDEMO2`.
   * Tipo di valore per **nome del server DB2**, nel formato hello indirizzo o alias virgola numero di porta. Ad esempio digitare `HISDEMO2.cloudapp.net:50000`.
   * Digitare un valore per il nome del database DB2 in **Database**. Ad esempio digitare `NWIND`.
   * Digitare un valore in **Nome utente**. Ad esempio digitare `db2admin`.
   * Digitare un valore in **Password**. Ad esempio digitare `Password1`.
9. Selezionare **crea** toocontinue.
   
    ![](./media/connectors-create-api-db2/Db2connectorCloudConnection.png)
10. In hello **nome tabella** elenco, seleziona hello **freccia giù**, quindi selezionare **AREA**.
11. Facoltativamente, selezionare **Visualizza le opzioni avanzate** toospecify opzioni di query.
12. Selezionare **Salva**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowsTableName.png)
13. In hello **Db2getRows** pannello all'interno di hello **tutte le esecuzioni** elenco sotto **riepilogo**, selezionare hello elencate al primo elemento (esecuzione più recente).
14. In hello **app per eseguire la logica** pannello seleziona **Dettagli esecuzione**. All'interno di hello **azione** elenco, selezionare **Get_rows**. Visualizzare il valore hello **stato**, che deve essere **Succeeded**. Seleziona hello **collegamento di input** input hello tooview. Seleziona hello **collegamento di output**e restituisce hello visualizzazione, che deve includere un elenco di righe.
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowsOutputs.png)

## <a name="add-one-row-using-insert"></a>Aggiunta di una riga con INSERT
È possibile definire una logica app azione tooadd una riga in una tabella DB2. Questa azione indica hello connettore tooprocess un'istruzione INSERT di DB2, ad esempio `INSERT INTO AREA (AREAID, AREADESC, REGIONID) VALUES ('99999', 'Area 99999', 102)`.

### <a name="create-a-logic-app"></a>Creare un'app per la logica
1. In hello **Azure avviare discussioni**selezionare  **+**  (segno), **Web e dispositivi mobili**e quindi **logica App**.
2. Immettere hello **nome**, ad esempio `Db2insertRow`, **sottoscrizione**, **gruppo di risorse**, **percorso**, e **App Piano di servizio**. Selezionare **Pin toodashboard**, quindi selezionare **crea**.

### <a name="add-a-trigger-and-action"></a>Aggiungere un trigger e un'azione
1. In hello **logica App progettazione**selezionare **LogicApp vuoto** in hello **modelli** elenco.
2. In hello **trigger** elenco, selezionare **ricorrenza**. 
3. In hello **ricorrenza** trigger, selezionare **modifica**selezionare **frequenza** tooselect elenco a discesa **giorno**, quindi selezionare  **Intervallo** tootype **7**. 
4. Seleziona hello **+ nuovo passaggio** e quindi selezionare **aggiungere un'azione**.
5. In hello **azioni** elenco, digitare **db2** in hello **cercare altre azioni** casella di modifica e quindi selezionare **DB2 - riga di inserimento (anteprima)**.
6. In hello **DB2 - riga di inserimento (anteprima)** azione, selezionare **Cambia connessione**. 
7. In hello **connessioni** riquadro configurazione, selezionare una connessione. ad esempio, selezionare **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. In hello **nome tabella** elenco, seleziona hello **freccia giù**, quindi selezionare **AREA**.
9. Immettere valori per tutte le colonne obbligatorie (asterisco rosso). Ad esempio digitare `99999` per **AREAID** e `Area 99999``102` per **REGIONID**. 
10. Selezionare **Salva**.
    
    ![](./media/connectors-create-api-db2/Db2connectorInsertRowValues.png)
11. In hello **Db2insertRow** pannello all'interno di hello **tutte le esecuzioni** elenco sotto **riepilogo**, selezionare hello elencate al primo elemento (esecuzione più recente).
12. In hello **app per eseguire la logica** pannello seleziona **Dettagli esecuzione**. All'interno di hello **azione** elenco, selezionare **Get_rows**. Visualizzare il valore hello **stato**, che deve essere **Succeeded**. Seleziona hello **collegamento di input** input hello tooview. Seleziona hello **collegamento di output**e restituisce hello di visualizzazione, che deve includere una nuova riga hello.
    
    ![](./media/connectors-create-api-db2/Db2connectorInsertRowOutputs.png)

## <a name="fetch-one-row-using-select"></a>Recuperare una riga con SELECT
È possibile definire una logica app azione toofetch una riga in una tabella DB2. Questa azione indica hello connettore tooprocess un'istruzione DB2 selezionare in cui, ad esempio `SELECT FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Creare un'app per la logica
1. In hello **Azure avviare discussioni**selezionare  **+**  (segno), **Web e dispositivi mobili**e quindi **logica App**.
2. Immettere hello **nome** (ad esempio, "**Db2getRow**"), **Sottoscrizione**, **Gruppo di risorse**, **Località**, **Piano di servizio app**. Selezionare **Pin toodashboard**, quindi selezionare **crea**.

### <a name="add-a-trigger-and-action"></a>Aggiungere un trigger e un'azione
1. In hello **logica App progettazione**selezionare **LogicApp vuoto** in hello **modelli** elenco. 
2. In hello **trigger** elenco, selezionare **ricorrenza**. 
3. In hello **ricorrenza** trigger, selezionare **modifica**selezionare **frequenza** tooselect elenco a discesa **giorno**, quindi selezionare  **Intervallo** tootype **7**. 
4. Seleziona hello **+ nuovo passaggio** e quindi selezionare **aggiungere un'azione**.
5. In hello **azioni** elenco, digitare **db2** in hello **cercare altre azioni** casella di modifica e quindi selezionare **DB2 - Get righe (anteprima)**.
6. In hello **ottenere righe (anteprima)** azione, selezionare **Cambia connessione**. 
7. In hello **connessioni** riquadro configurazioni, selezionare una connessione esistente. ad esempio, selezionare **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. In hello **nome tabella** elenco, seleziona hello **freccia giù**, quindi selezionare **AREA**.
9. Immettere valori per tutte le colonne obbligatorie (asterisco rosso). Ad esempio digitare `99999` per **AREAID**. 
10. Facoltativamente, selezionare **Visualizza le opzioni avanzate** toospecify opzioni di query.
11. Selezionare **Salva**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowValues.png)
12. In hello **Db2getRow** pannello all'interno di hello **tutte le esecuzioni** elenco sotto **riepilogo**, selezionare hello elencate al primo elemento (esecuzione più recente).
13. In hello **app per eseguire la logica** pannello seleziona **Dettagli esecuzione**. All'interno di hello **azione** elenco, selezionare **Get_rows**. Visualizzare il valore hello **stato**, che deve essere **Succeeded**. Seleziona hello **collegamento di input** input hello tooview. Seleziona hello **collegamento di output**e restituisce hello visualizzazione, che deve includere una riga.
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowOutputs.png)

## <a name="change-one-row-using-update"></a>Modificare una riga con UPDATE
È possibile definire una logica app azione toochange una riga in una tabella DB2. Questa azione indica hello connettore tooprocess un'istruzione UPDATE di DB2, ad esempio `UPDATE AREA SET AREAID = '99999', AREADESC = 'Area 99999', REGIONID = 102)`.

### <a name="create-a-logic-app"></a>Creare un'app per la logica
1. In hello **Azure avviare discussioni**selezionare  **+**  (segno), **Web e dispositivi mobili**e quindi **logica App**.
2. Immettere hello **nome**, ad esempio `Db2updateRow`, **sottoscrizione**, **gruppo di risorse**, **percorso**, e **App Piano di servizio**. Selezionare **Pin toodashboard**, quindi selezionare **crea**.

### <a name="add-a-trigger-and-action"></a>Aggiungere un trigger e un'azione
1. In hello **logica App progettazione**selezionare **LogicApp vuoto** in hello **modelli** elenco.
2. In hello **trigger** elenco, selezionare **ricorrenza**. 
3. In hello **ricorrenza** trigger, selezionare **modifica**selezionare **frequenza** tooselect elenco a discesa **giorno**, quindi selezionare  **Intervallo** tootype **7**. 
4. Seleziona hello **+ nuovo passaggio** e quindi selezionare **aggiungere un'azione**.
5. In hello **azioni** elenco, digitare **db2** in hello **cercare altre azioni** casella di modifica e quindi selezionare **DB2 - riga aggiornamento (anteprima)**.
6. In hello **DB2 - riga aggiornamento (anteprima)** azione, selezionare **Cambia connessione**. 
7. In hello **connessioni** riquadro configurazioni, selezionare tooselect una connessione esistente. ad esempio, selezionare **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. In hello **nome tabella** elenco, seleziona hello **freccia giù**, quindi selezionare **AREA**.
9. Immettere valori per tutte le colonne obbligatorie (asterisco rosso). Ad esempio digitare `99999` per **AREAID** e `Updated 99999``102` per **REGIONID**. 
10. Selezionare **Salva**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorUpdateRowValues.png)
11. In hello **Db2updateRow** pannello all'interno di hello **tutte le esecuzioni** elenco sotto **riepilogo**, selezionare hello elencate al primo elemento (esecuzione più recente).
12. In hello **app per eseguire la logica** pannello seleziona **Dettagli esecuzione**. All'interno di hello **azione** elenco, selezionare **Get_rows**. Visualizzare il valore hello **stato**, che deve essere **Succeeded**. Seleziona hello **collegamento di input** input hello tooview. Seleziona hello **collegamento di output**e restituisce hello di visualizzazione, che deve includere una nuova riga hello.
    
    ![](./media/connectors-create-api-db2/Db2connectorUpdateRowOutputs.png)

## <a name="remove-one-row-using-delete"></a>Rimozione di una riga con DELETE
È possibile definire una logica app azione tooremove una riga in una tabella DB2. Questa azione indica hello connettore tooprocess un'istruzione DELETE di DB2, ad esempio `DELETE FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Creare un'app per la logica
1. In hello **Azure avviare discussioni**selezionare  **+**  (segno), **Web e dispositivi mobili**e quindi **logica App**.
2. Immettere hello **nome**, ad esempio `Db2deleteRow`, **sottoscrizione**, **gruppo di risorse**, **percorso**, e **App Piano di servizio**. Selezionare **Pin toodashboard**, quindi selezionare **crea**.

### <a name="add-a-trigger-and-action"></a>Aggiungere un trigger e un'azione
1. In hello **logica App progettazione**selezionare **LogicApp vuoto** in hello **modelli** elenco. 
2. In hello **trigger** elenco, selezionare **ricorrenza**. 
3. In hello **ricorrenza** trigger, selezionare **modifica**selezionare **frequenza** tooselect elenco a discesa **giorno**, quindi selezionare  **Intervallo** tootype **7**. 
4. Seleziona hello **+ nuovo passaggio** e quindi selezionare **aggiungere un'azione**.
5. In hello **azioni** elenco, selezionare **db2** in hello **cercare altre azioni** casella di modifica e quindi selezionare **DB2 - Elimina riga (anteprima)**.
6. In hello **DB2 - Elimina riga (anteprima)** azione, selezionare **Cambia connessione**. 
7. In hello **connessioni** riquadro configurazioni, selezionare una connessione esistente. ad esempio, selezionare **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. In hello **nome tabella** elenco, seleziona hello **freccia giù**, quindi selezionare **AREA**.
9. Immettere valori per tutte le colonne obbligatorie (asterisco rosso). Ad esempio digitare `99999` per **AREAID**. 
10. Selezionare **Salva**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorDeleteRowValues.png)
11. In hello **Db2deleteRow** pannello all'interno di hello **tutte le esecuzioni** elenco sotto **riepilogo**, selezionare hello elencate al primo elemento (esecuzione più recente).
12. In hello **app per eseguire la logica** pannello seleziona **Dettagli esecuzione**. All'interno di hello **azione** elenco, selezionare **Get_rows**. Visualizzare il valore hello **stato**, che deve essere **Succeeded**. Seleziona hello **collegamento di input** input hello tooview. Seleziona hello **collegamento di output**e hello visualizzazione output, che deve includere la riga hello eliminato.
    
    ![](./media/connectors-create-api-db2/Db2connectorDeleteRowOutputs.png)

## <a name="supported-db2-platforms-and-versions"></a>Piattaforme e versioni di DB2 supportate
Questo connettore supporta hello seguenti piattaforme IBM DB2 e le versioni, nonché prodotti compatibili a IBM DB2 (ad esempio IBM Bluemix dashDB) che supportano Distributed Relational Database Architecture (DRDA) SQL Access Manager (SQLAM) versione 10 e 11:

* IBM DB2 per z/OS 11.1
* IBM DB2 per z/OS 10.1
* IBM DB2 per i 7.3
* IBM DB2 per i 7.2
* IBM DB2 per i 7.1
* IBM DB2 per LUW 11
* IBM DB2 per LUW 10.5

## <a name="connector-specific-details"></a>Dettagli specifici del connettore

Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/db2/). 

## <a name="next-steps"></a>Passaggi successivi
[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md). Esplorare hello altri connettori disponibile in App per la logica nel nostro [elenco API](apis-list.md).

