---
title: connessioni aaaITSM in connettore di gestione del servizio IT OMS | Documenti Microsoft
description: Connettere i prodotti e servizi ITSM con connettore di gestione del servizio IT in OMS toocentrally monitoraggio e gestire gli elementi di lavoro ITSM hello.
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 8231b7ce-d67f-4237-afbf-465e2e397105
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: v-jysur
ms.openlocfilehash: 53ef51bf75fb8ed15ea3ce5072d9365c221f9f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-itsm-productsservices-with-it-service-management-connector-preview"></a>Connettere i servizi/prodotti ITSM con IT Service Management Connector (Anteprima)
In questo articolo fornisce informazioni su come tooconnect tooIT di prodotti o servizi connettore di gestione del servizio in OMS e in modo centralizzato il ITSM gestire gli elementi di lavoro. Per altre informazioni su IT Service Management Connector, vedere [Panoramica](log-analytics-itsmc-overview.md).

è supportato i seguenti prodotti e servizi Hello:

- [System Center Service Manager](#connect-system-center-service-manager-to-it-service-management-connector-in-oms)
- [ServiceNow](#connect-servicenow-to-it-service-management-connector-in-oms)
- [Provance](#connect-provance-to-it-service-management-connector-in-oms)
- [Cherwell](#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="connect-system-center-service-manager-tooit-service-management-connector-in-oms"></a>Connettersi a System Center Service Manager tooIT connettore del servizio di gestione di OMS

Hello nelle sezioni seguenti vengono fornite informazioni dettagliate tooconnect il toohello prodotto System Center Service Manager connettore di gestione del servizio IT in OMS.

### <a name="prerequisites"></a>Prerequisiti

Verificare di che aver seguito i prerequisiti soddisfatti hello:

- IT Service Management Connector è stato installato.
Per altre informazioni, vedere [Configuration](log-analytics-itsmc-overview.md#configuration) (Configurazione).
- applicazione Web di Service Manager (app Web) Hello è distribuito e configurato. Per informazioni sull'app Web, vedere[qui](#create-and-deploy-service-manager-web-app-service).
- Connessione ibrida è stata creata e configurata. Altre informazioni: [ibrida hello Configura connessione](#configure-the-hybrid-connection).
- Versioni supportate di Service Manager: 2012 R2 o 2016.
- Ruolo utente: [Operatore avanzato](https://technet.microsoft.com/library/ff461054.aspx).

### <a name="connection-procedure"></a>Procedura di connessione

Utilizzare hello seguendo procedure tooconnect il toohello di istanza di System Center Service Manager connettore di gestione del servizio IT:

1. Andare troppo**OMS** >**impostazioni** > **Connected Sources**.
2. Selezionare **ITSM Connector** e fare clic su **Aggiungi nuova connessione**.

    ![Service Manager ](./media/log-analytics-itsmc/itsmc-service-manager-connection.png)
3. Fornire informazioni hello, come descritto in hello nella tabella seguente e fare clic su **salvare** connessione hello toocreate:

> [!NOTE]
> Tutti questi parametri sono obbligatori.

| **Campo** | **Descrizione** |
| --- | --- |
| **Nome**   | Digitare un nome per l'istanza di System Center Service Manager hello che si desidera tooconnect con hello connettore di gestione del servizio IT.  Questo nome viene usato in seguito durante la configurazione degli elementi di lavoro in questa istanza o quando si visualizzano analisi del log dettagliate. |
| **Seleziona tipo di connessione**   | Selezionare **System Center Service Manager**. |
| **URL del server**   | Digitare l'URL hello di hello app Web di Service Manager. Per altre informazioni sull'app Web Service Manager, vedere [qui](#create-and-deploy-service-manager-web-app-service).
| **ID client**   | Digitare l'ID client hello generato (tramite script automatico hello) per autenticare l'app Web hello. Per ulteriori informazioni sull'utilizzo di script automatizzato hello [qui.](log-analytics-itsmc-service-manager-script.md)|
| **Segreto client**   | Segreto del client di tipo hello, generato per questo ID.   |
| **Ambito sincronizzazione dati**   | Selezionare gli elementi di lavoro di hello Service Manager che si desidera toosync tramite hello connettore di gestione del servizio IT.  Questi elementi di lavoro vengono importati in Log Analytics. **Opzioni:** Eventi imprevisti, Richieste di modifica.|
| **Sincronizza dati** | Digitare hello numero di giorni che si desidera che i dati hello da. **Limite massimo**: 120 giorni. |
| **Create new configuration item in ITSM solution** (Crea nuovo elemento di configurazione nella soluzione ITSM) | Selezionare questa opzione se si desidera toocreate prodotto ITSM hello gli elementi di configurazione hello. Se selezionata, OMS crea gli elementi di configurazione interessato hello come elementi di configurazione (in caso di elementi di configurazione non esistente) in hello supportate sistema ITSM. **Impostazione predefinita**: disabilitata. |

Dopo la connessione e la sincronizzazione:

- Gli elementi di lavoro selezionati da Service Manager vengono importati in OMS **Log Analytics.** È possibile visualizzare il riepilogo di hello di questi elementi di lavoro nella tessera di hello connettore di gestione del servizio IT.

- Da OMS è possibile creare eventi imprevisti dagli avvisi di OMS o dalla ricerca log in questa istanza di Service Manager.

Per altre informazioni, vedere [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) (Creare elementi di lavoro ITSM per avvisi di OMS) e [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs) (Creare elementi di lavoro ITSM da log di OMS).

### <a name="create-and-deploy-service-manager-web-app-service"></a>Creare e distribuire il servizio app Web di Service Manager

tooconnect hello locale Service Manager con hello connettore di gestione del servizio IT in OMS, Microsoft ha creato un'app Web di Service Manager su hello GitHub.

tooset backup hello ITSM Web app per il gestore del servizio, hello seguenti:

- **Distribuisci hello Web app** : distribuire l'app Web hello, impostare le proprietà di hello e l'autenticazione con Azure AD. È possibile distribuire l'app web hello utilizzando hello [automatizzata script](log-analytics-itsmc-service-manager-script.md) che Microsoft sono stati forniti.
- **Configurare la connessione ibrida hello** - [configurare la connessione](#configure-the-hybrid-connection)manualmente.

#### <a name="deploy-hello-web-app"></a>Distribuire l'app web hello
Hello utilizzare automatizzata [script](log-analytics-itsmc-service-manager-script.md) toodeploy hello app Web, impostare le proprietà di hello e l'autenticazione con Azure AD.

Eseguire script hello fornendo hello seguito i dettagli richiesti:

- Dettagli della sottoscrizione di Azure
- Nome del gruppo di risorse
- Località
- Dettagli del server di Service Manager (nome del server, dominio, nome utente e password)
- Prefisso del nome del sito per l'app Web
- Spazio dei nomi ServiceBus.

lo script Hello crea hello Web app con nome hello specificato (insieme alcuni ulteriori stringhe toomake è univoco). Genera hello **URL app Web**, **ID client** e **segreto client**.

Salvare i valori hello, utilizzarli quando si crea una connessione con connettore di gestione del servizio IT.

**Verificare l'installazione dell'app Web hello**

1. Andare troppo**portale di Azure** > **risorse**.
2. Selezionare l'app Web hello, fare clic su **impostazioni** > **le impostazioni dell'applicazione**.
3. Verificare le informazioni di hello sull'istanza di Service Manager hello forniti in fase di hello della distribuzione di app hello tramite script hello.

### <a name="configure-hello-hybrid-connection"></a>Configurare la connessione ibrida hello

Utilizzare hello dopo la connessione procedure tooconfigure hello ibrida che connette l'istanza di Service Manager hello con hello connettore di gestione del servizio IT in OMS.

1. Trovare hello app Web di Service Manager, in **le risorse di Azure**.
2. Fare clic su **Impostazioni** > **Rete**.
3. In **Connessioni ibride** fare clic su **Configurare gli endpoint della connessione ibrida**.

    ![Rete per la connessione ibrida](./media/log-analytics-itsmc/itsmc-hybrid-connection-networking-and-end-points.png)
4. In hello **connessioni ibride** pannello, fare clic su **aggiungere la connessione ibrida**.

    ![Aggiunta di una connessione ibrida](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-add.png)

5. In hello **aggiungere connessioni ibride** pannello, fare clic su **ibrida nuova Crea connessione**.

    ![Nuova connessione ibrida](./media/log-analytics-itsmc/itsmc-create-new-hybrid-connection.png)

6. Digitare hello seguenti valori:

    - **Nome dell'endPoint**: specificare un nome per la connessione ibrida nuova hello.
    -  **Host endPoint**: nome FQDN del server di gestione di Service Manager hello.
    - **Porta endpoint**: digitare 5724.
    - **Spazio dei nomi del bus di servizio**: usare uno spazio dei nomi del bus di servizio esistente o crearne uno nuovo.
    - **Percorso**: selezionare il percorso di hello.
    -  **Nome**: specificare un bus di servizio toohello nome se si crea.

    ![Valori della connessione ibrida](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-values.png)
6. Fare clic su **OK** tooclose hello **creare la connessione ibrida** blade e avviare la creazione di connessione ibrida hello.

    Dopo aver creata la connessione ibrida hello, viene visualizzato sotto il pannello hello.

7. Dopo aver creata la connessione ibrida hello, selezionare la connessione hello e fare clic su **Add selected connessione ibrida**.

    ![Nuova connessione ibrida](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-added.png)

#### <a name="configure-hello-listener-setup"></a>Configurare le impostazioni listener hello

Utilizzare procedura di installazione di procedure tooconfigure hello listener per la connessione ibrida hello hello.

1. In hello **connessioni ibride** pannello, fare clic su **Download hello Connection Manager** e installarlo nel computer di hello in cui viene eseguita l'istanza di System Center Service Manager.

    Dopo aver completato l'installazione di hello **UI Hybrid Connection Manager** opzione è disponibile in **avviare** menu.

2. Fare clic su **Hybrid Connection Manager UI** (Interfaccia utente ibrida di Gestione connessioni). Verranno richieste le credenziali di Azure.

3. Account di accesso con le credenziali di Azure e selezionare la sottoscrizione in cui è stata creata la connessione ibrida hello.

4. Fare clic su **Salva**.

La connessione ibrida è stata completata.

![Connessione ibrida completata](./media/log-analytics-itsmc/itsmc-hybrid-connection-listener-set-up-successful.png)
> [!NOTE]

> Dopo aver creata la connessione ibrida hello, verificare e test della connessione hello visitando hello distribuiti app Web di Service Manager. Verificare la connessione hello ha esito positivo prima di provare tooconnect toohello connettore di gestione del servizio IT in OMS.

Hello immagine seguente mostra i dettagli di hello di una connessione ha esito positivo:

![Test della connessione ibrida](./media/log-analytics-itsmc/itsmc-hybrid-connection-test.png)

## <a name="connect-servicenow-tooit-service-management-connector-in-oms"></a>Connettere ServiceNow tooIT connettore del servizio di gestione di OMS

Hello nelle sezioni seguenti vengono fornite informazioni dettagliate tooconnect il toohello prodotto ServiceNow connettore di gestione del servizio IT in OMS.

### <a name="prerequisites"></a>Prerequisiti

Verificare di che aver seguito i prerequisiti soddisfatti hello:

- IT Service Management Connector è stato installato. Per altre informazioni, vedere [Configuration](log-analytics-itsmc-overview.md#configuration) (Configurazione).
- Versioni supportate di ServiceNow: Fuji, Geneva, Helsinki.

Eseguire ServiceNow Admins hello nella propria istanza di ServiceNow seguente:
- Generare l'ID client e il segreto client per il prodotto di ServiceNow hello. Per informazioni su come toogenerate client ID e segreto, vedere [l'installazione di OAuth](http://wiki.servicenow.com/index.php?title=OAuth_Setup).
- Installare hello utente App per l'integrazione con Microsoft OMS (ServiceNow app). [Altre informazioni](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0 )
- Creare ruolo utente di integrazione per hello utente app installata. Informazioni su come ruolo utente di integrazione hello toocreate [qui](#create-integration-user-role-in-servicenow-app).


### <a name="connection-procedure"></a>**Procedura di connessione**

Utilizzare hello seguendo procedure toocreate una connessione di ServiceNow:

1. Andare troppo**OMS** > **impostazioni** > **Connected Sources**.
2. Selezionare **ITSM Connector** e fare clic su **Aggiungi nuova connessione**.

    ![Connessione ServiceNow](./media/log-analytics-itsmc/itsmc-servicenow-connection.png)

3. Fornire informazioni hello, come descritto in hello nella tabella seguente e fare clic su **salvare** connessione hello toocreate:

> [!NOTE]
> Tutti questi parametri sono obbligatori.

| **Campo** | **Descrizione** |
| --- | --- |
| **Nome**   | Digitare un nome per l'istanza di ServiceNow hello che si desidera tooconnect con hello connettore di gestione del servizio IT.  Questo nome viene usato in seguito in OMS durante la configurazione degli elementi di lavoro in questa istanza di ITSM o quando si visualizzano analisi del log dettagliate. |
| **Seleziona tipo di connessione**   | Selezionare **ServiceNow**. |
| **Nome utente**   | Digitare nome utente di integrazione hello creati in hello ServiceNow app toosupport hello connessione toohello connettore di gestione del servizio IT. Per altre informazioni, vedere [Create ServiceNow app user role](#create-integration-user-role-in-servicenow-app) (Creare il ruolo utente dell'app ServiceNow).|
| **Password**   | Digitare la password hello associata a questo nome utente. **Nota**: nome utente e password vengono utilizzate per generare solo i token di autenticazione e non vengono archiviate in un punto qualsiasi all'interno del servizio OMS hello.  |
| **URL del server**   | Digitare l'URL di hello dell'istanza di ServiceNow hello che si desidera tooconnect tooIT connettore del servizio di gestione. |
| **ID client**   | Digitare l'ID client hello che si desidera toouse per l'autenticazione OAuth2, che è stato generato in precedenza.  Per altre informazioni sulla generazione dell'ID client e del segreto, vedere [OAuth Setup](http://wiki.servicenow.com/index.php?title=OAuth_Setup) (Configurazione di OAuth). |
| **Segreto client**   | Segreto del client di tipo hello, generato per questo ID.   |
| **Ambito sincronizzazione dati**   | Selezionare gli elementi di lavoro ServiceNow hello che si desidera tooOMS toosync, tramite hello connettore di gestione del servizio IT.  i valori Hello selezionato vengono importati in analitica di log.   **Opzioni:** Eventi imprevisti e Richieste di modifica.|
| **Sincronizza dati** | Digitare hello numero di giorni che si desidera che i dati hello da. **Limite massimo**: 120 giorni. |
| **Create new configuration item in ITSM solution** (Crea nuovo elemento di configurazione nella soluzione ITSM) | Selezionare questa opzione se si desidera toocreate prodotto ITSM hello gli elementi di configurazione hello. Se selezionata, OMS crea gli elementi di configurazione interessato hello come elementi di configurazione (in caso di elementi di configurazione non esistente) in hello supportate sistema ITSM. **Impostazione predefinita**: disabilitata. |


Dopo la connessione e la sincronizzazione:

- Gli elementi di lavoro selezionati dalla connessione ServiceNow vengono importati in OMS Log Analytics.  È possibile visualizzare il riepilogo di hello di questi elementi di lavoro nella tessera di hello connettore di gestione del servizio IT.
- È possibile creare eventi imprevisti, avvisi ed eventi da Avvisi OMS o dalla ricerca log nell'istanza di ServiceNow.  


Per altre informazioni, vedere [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) (Creare elementi di lavoro ITSM per avvisi di OMS) e [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs) (Creare elementi di lavoro ITSM da log di OMS).

### <a name="create-integration-user-role-in-servicenow-app"></a>Creare un ruolo utente di integrazione nell'app ServiceNow

Hello utente seguente procedura:

1.  Visitare hello [ServiceNow archivio](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0) e installare hello **utente App per l'integrazione di OMS di Microsoft e ServiceNow** nell'istanza ServiceNow.
2.  Dopo l'installazione, visitare hello barra di spostamento dell'istanza di ServiceNow hello, ricerca e selezionare Microsoft OMS integrator a sinistra.  
3.  Fare clic su **Installation Checklist** (Elenco di controllo installazione).

    stato Hello viene visualizzato come **non completare** se il ruolo di utente hello è ancora toobe creato.

4.  Testo hello caselle accanto troppo**Crea utente integrazione**, immettere il nome utente hello per utente hello in grado di connettersi toohello connettore di gestione del servizio IT in OMS.
5.  Immettere la password di hello per questo utente e fare clic su **OK**.  

>[!NOTE]

> Utilizzi queste credenziali toomake hello ServiceNow in OMS.

Hello utente appena creato viene visualizzato con i ruoli predefiniti di hello assegnati.

Ruoli predefiniti:
- personalize_choices
- import_transformer
-   x_mioms_microsoft.user
-   itil
-   template_editor
-   view_changer

Una volta hello utente creato correttamente, hello stato **verifica dell'installazione** Sposta tooCompleted, dettagli hello del ruolo utente hello creato per l'applicazione hello elenco.

> [!NOTE]

> un utente di toocreate tooallow **avvisi** e **eventi** in ServiceNow da OMS:

> - Assicurarsi di disporre di modulo di gestione degli eventi hello installato sull'istanza ServiceNow.

> - Aggiungere hello utente di integrazione toohello ruoli seguenti:
>      - evt_mgmt_integration
>      - evt_mgmt_operator  


## <a name="connect-provance-tooit-service-management-connector-in-oms"></a>Connettersi Provance tooIT connettore del servizio di gestione di OMS

Hello nelle sezioni seguenti vengono fornite informazioni dettagliate tooconnect il toohello prodotto Provance connettore di gestione del servizio IT in OMS.

### <a name="prerequisites"></a>Prerequisiti

Verificare di che aver seguito i prerequisiti soddisfatti hello:

- IT Service Management Connector è stato installato. Per altre informazioni, vedere [Configuration](log-analytics-itsmc-overview.md#configuration) (Configurazione).
- L'app Provance deve essere registrata in Azure AD e l'ID client deve essere stato reso disponibile. Per informazioni dettagliate, vedere [come l'autenticazione di active directory tooconfigure](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).
- Ruolo utente: amministratore.

### <a name="connection-procedure"></a>Procedura di connessione

Utilizzare hello procedure toocreate una connessione Provance seguenti:

1. Andare troppo**OMS** > **impostazioni** > **Connected Sources**.
2. Selezionare **ITSM Connector** e fare clic su **Aggiungi nuova connessione**.  

    ![Connessione Provance](./media/log-analytics-itsmc/itsmc-provance-connection.png)
3. Fornire informazioni hello, come descritto in hello nella tabella seguente e fare clic su **salvare** connessione hello toocreate.

> [!NOTE]
> Tutti questi parametri sono obbligatori.

| **Campo** | **Descrizione** |
| --- | --- |
| **Nome**   | Digitare un nome di istanza Provance hello che si desidera tooconnect con hello connettore di gestione del servizio IT.  Questo nome viene usato in seguito in OMS durante la configurazione degli elementi di lavoro in questa istanza di ITSM o quando si visualizzano analisi del log dettagliate. |
| **Seleziona tipo di connessione**   | Selezionare **Provance**. |
| **Nome utente**   | Digitare nome utente hello in grado di connettersi toohello connettore di gestione del servizio IT.    |
| **Password**   | Digitare la password hello associata a questo nome utente. **Nota:** nome utente e password vengono utilizzate per generare solo i token di autenticazione e non vengono archiviate in un punto qualsiasi all'interno del servizio OMS hello. _|
| **URL del server**   | Digitare l'URL hello dell'istanza Provance che si desidera tooconnect tooIT connettore del servizio di gestione. |
| **ID client**   | ID tipo hello client per autenticare la connessione, che è stato generato nell'istanza di Provance.  Ulteriori informazioni sull'ID client, vedere [come l'autenticazione di active directory tooconfigure](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). |
| **Ambito sincronizzazione dati**   | Selezionare gli elementi di lavoro Provance hello che si desidera tooOMS toosync, tramite hello connettore di gestione del servizio IT.  Questi elementi di lavoro vengono importati in Log Analytics.   **Opzioni:** Eventi imprevisti, Richieste di modifica.|
| **Sincronizza dati** | Digitare hello numero di giorni che si desidera che i dati hello da. **Limite massimo**: 120 giorni. |
| **Create new configuration item in ITSM solution** (Crea nuovo elemento di configurazione nella soluzione ITSM) | Selezionare questa opzione se si desidera toocreate prodotto ITSM hello gli elementi di configurazione hello. Se selezionata, OMS crea gli elementi di configurazione interessato hello come elementi di configurazione (in caso di elementi di configurazione non esistente) in hello supportate sistema ITSM. **Impostazione predefinita**: disabilitata.|

Dopo la connessione e la sincronizzazione:

- Gli elementi di lavoro selezionati dalla connessione Provance vengono importati in OMS **Log Analytics**.  È possibile visualizzare il riepilogo di hello di questi elementi di lavoro nella tessera di hello connettore di gestione del servizio IT.
- È possibile creare eventi imprevisti ed eventi da Avvisi OMS o dalla ricerca log nell'istanza di Provance.

Per altre informazioni, vedere [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) (Creare elementi di lavoro ITSM per avvisi di OMS) e [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs) (Creare elementi di lavoro ITSM da log di OMS).

## <a name="connect-cherwell-tooit-service-management-connector-in-oms"></a>Connettersi a Cherwell tooIT connettore del servizio di gestione di OMS

Hello nelle sezioni seguenti vengono fornite informazioni dettagliate tooconnect il toohello prodotto Cherwell connettore di gestione del servizio IT in OMS.

### <a name="prerequisites"></a>Prerequisiti

Verificare di che aver seguito i prerequisiti soddisfatti hello:

- IT Service Management Connector è stato installato. Per altre informazioni, vedere [Configuration](log-analytics-itsmc-overview.md#configuration) (Configurazione).
- L'ID client è stato generato. Per altre informazioni, vedere [Generare l'ID client per Cherwell](#generate-client-id-for-cherwell).
- Ruolo utente: amministratore.

### <a name="connection-procedure"></a>Procedura di connessione

Utilizzare hello seguendo procedure toocreate una connessione di Cherwell:

1. Andare troppo**OMS** >  **impostazioni** > **Connected Sources**.
2. Selezionare **ITSM Connector** e fare clic su **Aggiungi nuova connessione**.  

    ![ID utente di Cherwell](./media/log-analytics-itsmc/itsmc-cherwell-connection.png)

3. Fornire informazioni hello, come descritto in hello nella tabella seguente e fare clic su **salvare** connessione hello toocreate.

> [!NOTE]
> Tutti questi parametri sono obbligatori.

| **Campo** | **Descrizione** |
| --- | --- |
| **Nome**   | Digitare un nome per l'istanza di Cherwell hello che si desidera tooconnect toohello connettore di gestione del servizio IT.  Questo nome viene usato in seguito in OMS durante la configurazione degli elementi di lavoro in questa istanza di ITSM o quando si visualizzano analisi del log dettagliate. |
| **Seleziona tipo di connessione**   | Selezionare **Cherwell**. |
| **Nome utente**   | Digitare nome utente di Cherwell hello in grado di connettersi toohello connettore di gestione del servizio IT. |
| **Password**   | Digitare la password hello associata a questo nome utente. **Nota:** nome utente e password vengono utilizzate per generare solo i token di autenticazione e non vengono archiviate in un punto qualsiasi all'interno del servizio OMS hello.|
| **URL del server**   | Digitare l'URL hello dell'istanza di Cherwell che si desidera tooconnect tooIT connettore del servizio di gestione. |
| **ID client**   | ID tipo hello client per autenticare la connessione, che è stato generato nell'istanza di Cherwell.   |
| **Ambito sincronizzazione dati**   | Selezionare gli elementi di lavoro Cherwell hello che si desidera toosync tramite hello connettore di gestione del servizio IT.  Questi elementi di lavoro vengono importati in Log Analytics.   **Opzioni:** Eventi imprevisti, Richieste di modifica. |
| **Sincronizza dati** | Digitare hello numero di giorni che si desidera che i dati hello da. **Limite massimo**: 120 giorni. |
| **Create new configuration item in ITSM solution** (Crea nuovo elemento di configurazione nella soluzione ITSM) | Selezionare questa opzione se si desidera toocreate prodotto ITSM hello gli elementi di configurazione hello. Se selezionata, OMS crea gli elementi di configurazione interessato hello come elementi di configurazione (in caso di elementi di configurazione non esistente) in hello supportate sistema ITSM. **Impostazione predefinita**: disabilitata. |

Dopo la connessione e la sincronizzazione:

- Gli elementi di lavoro selezionati dalla connessione Cherwell vengono importati in OMS Log Analytics. È possibile visualizzare il riepilogo di hello di questi elementi di lavoro nella tessera di hello connettore di gestione del servizio IT.
- È possibile creare eventi imprevisti ed eventi in questa istanza di Cherwell da OMS. Per altre informazioni, vedere "Create ITSM work items for OMS alerts" (Creare elementi di lavoro ITSM per avvisi di OMS) e "Create ITSM work items from OMS logs" (Creare elementi di lavoro ITSM da log di OMS).

Per altre informazioni, vedere [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) (Creare elementi di lavoro ITSM per avvisi di OMS) e [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs) (Creare elementi di lavoro ITSM da log di OMS).

### <a name="generate-client-id-for-cherwell"></a>Generare l'ID client per Cherwell

toogenerate hello client ID/chiave per Cherwell, usare hello seguente procedura:

1. Accedi tooyour Cherwell istanza come amministratore.
2. Fare clic su **Security** (Sicurezza)  > **Edit REST API client settings** (Modifica le impostazioni client dell'API REST).
3. Selezionare **Create new client** (Crea nuovo client)  > **client secret** (segreto client).

    ![ID utente di Cherwell](./media/log-analytics-itsmc/itsmc-cherwell-client-id.png)


## <a name="next-steps"></a>Passaggi successivi
 - [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) (Creare elementi di lavoro ITSM per avvisi di OMS)

 - [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs) (Creare elementi di lavoro ITSM da log di OMS)

- [View log analytics for your connection](log-analytics-itsmc-overview.md#using-the-solution) (Visualizzare Log Analytics per la connessione)
