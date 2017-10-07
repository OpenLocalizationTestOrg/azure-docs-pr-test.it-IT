---
title: "aaaPower BI Dashboard di integrità veicolo e gestire abitudini - Azure | Documenti Microsoft"
description: "Utilizzare funzionalità di hello di insights di predittiva e in tempo reale toogain Intelligence Cortana sull'integrità del veicolo e abitudini di Guida."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: 0bd054d943387ecad7301236eebae22458173aba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a>Istruzioni di configurazione del dashboard di Power BI per il modello di soluzione per l'analisi dei dati di telemetria del veicolo
Questo **menu** capitoli toohello questo playbook è collegato. 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

Hello soluzione Analitica telemetria veicolo illustra come società di assicurazioni, produttori di automobili e settore automobilistico trae possono sfruttare le funzionalità di hello di Cortana Intelligence toogain predittive e in tempo reale informazioni dettagliate sui integrità veicolo e Guida miglioramenti di toodrive abitudini nell'area di hello del cliente verifica, R & D e campagne di marketing. Questo documento contiene istruzioni dettagliate su come configurare i report di Power BI hello e dashboard dopo aver distribuita la soluzione hello nella sottoscrizione. 

## <a name="prerequisites"></a>Prerequisiti
1. Distribuire hello [telemetria Analitica](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) soluzione  
2. [Installare Microsoft Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331)
3. Una [sottoscrizione di Azure](https://azure.microsoft.com/pricing/free-trial/). Se non si dispone di una sottoscrizione Azure, iniziare con una sottoscrizione gratuita di Azure.
4. Account di Microsoft Power BI

## <a name="cortana-intelligence-suite-components"></a>Componenti di Cortana Intelligence Suite
Come parte del modello di soluzione hello veicolo telemetria Analitica, hello seguenti Intelligence Cortana services viene distribuito nella sottoscrizione.

* **Hub eventi** per l'inserimento di milioni di eventi di telemetria del veicolo in Azure.
* **Analisi di flusso** per ottenere informazioni dettagliate in tempo reale sul funzionamento del veicolo e salvare i dati in modo permanente nello spazio di archiviazione a lungo termine per un'analisi batch avanzata.
* **Machine Learning** per il rilevamento di anomalie in tempo reale e approfondimenti predittiva toogain di elaborazione batch.
* **HDInsight** tootransform sfruttate dati su larga scala
* **Data Factory** gestisce l'orchestrazione, pianificazione, la gestione delle risorse e il monitoraggio della pipeline di elaborazione batch hello.

**Power BI** offre alla soluzione un dashboard completo per la visualizzazione di dati in tempo reale e di analisi predittiva. 

soluzione Hello utilizza due origini dati diverse: **simulato segnali veicolo e set di dati diagnostici** e **catalogo veicolo**.

Nella soluzione è incluso un simulatore di dati telematici relativi al veicolo. Genera informazioni di diagnostica ed segnala stato toohello corrispondente del veicolo hello e modello determinante in un determinato punto nel tempo. 

Hello veicolo catalogo è un mapping riferimento set di dati contenente VPN toomodel

## <a name="power-bi-dashboard-preparation"></a>Preparazione del dashboard di Power BI
### <a name="setup-power-bi-real-time-dashboard"></a>Configurare il dashboard in tempo reale di Power BI

**Avviare un'applicazione hello dashboard in tempo reale** al termine della distribuzione di hello, è necessario seguire le istruzioni di operazione manuale hello

* Scaricare l'applicazione dashboard in tempo reale RealtimeDashboardApp.zip e decomprimere il file.
*  Nella cartella decompresso hello, aprire file di configurazione app 'RealtimeDashboardApp.exe.config', sostituire appSettings per le connessioni di servizio hub eventi, l'archiviazione Blob e ML con i valori hello in istruzioni di operazione manuale hello e salvare le modifiche.
* Eseguire l'applicazione RealtimeDashboardApp.exe. Una finestra di dialogo di accesso popup, fornire le credenziali di Power BI valide e fare clic su hello **Accept** pulsante. Quindi l'applicazione hello inizierà toorun.

   ![Accedi tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Autorizzazioni per il dashboard di Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* Sito Web tooPowerBI account di accesso e creare dashboard in tempo reale.

A questo punto, si è pronti tooconfigure dashboard di Power BI hello con le visualizzazioni dettagliate toogain in tempo reale e abitudini predittive informazioni essenziali quanto a integrità veicolo e la Guida. Sono necessari circa 45 minuti tooan ora toocreate hello tutti i report e configurare hello dashboard. 

### <a name="configure-power-bi-reports"></a>Configurare i report di Power BI
i report in tempo reale di Hello e dashboard hello richiedere circa 30 a 45 minuti toocomplete. Sfoglia troppo[http://powerbi.com](http://powerbi.com) e account di accesso.

![Accedi tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

Viene generato un nuovo set di dati in Power BI. Fare clic su hello **ConnectedCarsRealtime** set di dati.

![Selezionare il set di dati in tempo reale delle automobili connesse](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

Salvare hello report vuoto utilizzando **Ctrl + s**.

![Salvare il report vuoto](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

Specificare il nome del report *Analisi dei dati di telemetria del veicolo in tempo reale - Report*.

![Specificare il nome del report](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a>Report in tempo reale
Questa soluzione include tre report in tempo reale:

1. Veicoli operativi
2. Veicoli che richiedono manutenzione
3. Statistiche sull'integrità dei veicoli

È possibile scegliere tooconfigure tutti i report in tempo reale tre hello o arrestarsi dopo qualsiasi fase e procedere toohello successiva sezione di configurazione dei report di batch hello. È consigliabile toocreate tutti hello tre riporta informazioni dettagliate completo toovisualize hello del percorso in tempo reale di hello di soluzione hello.  

### <a name="1-vehicles-in-operation"></a>1. Veicoli operativi
Fare doppio clic su **pagina 1** e rinominarlo troppo "Veicoli nell'operazione"  
    ![Automobili connesse: veicoli operativi](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)  

Selezionare il campo **vin** da **Fields** e scegliere **"Card"** come tipo di visualizzazione.  

Viene creata una visualizzazione di tipo scheda come illustrato nella figura.  
    ![Automobili connesse: seleziona vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

Fare clic su nuova visualizzazione tooadd area vuota hello.  

Selezionare **Città** e **vin** dai campi. Modificare anche le visualizzazione**"Mappa"**. Trascinare **vin** nell'area valori. Trascinare **Città** dai campi troppo**legenda** area.   
    ![Automobili connesse: visualizzazione scheda](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)

Selezionare **formato** sezione **visualizzazioni**, fare clic su **titolo** e modificare hello **testo** troppo**"veicoli operazione in base alla città"**.  
    ![Automobili connesse: veicoli operativi in base alla città](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)   

La visualizzazione finale è simile a quella illustrata nella figura.    
    ![Automobili connesse: visualizzazione finale](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

Fare clic su nuova visualizzazione tooadd area vuota hello.  

Selezionare **Città** e **VPN**, modificare il tipo di visualizzazione anche**istogramma a colonne raggruppate**. Verificare che il campo **Città** sia nell'**area Asse** e **vin** nell'**area Valore**  

Ordinare il grafico in base a **"Count of vin"**  
    ![Automobili connesse: conteggio di vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)  

Il grafico cambia **titolo** troppo**"Veicoli nell'operazione in base alla città"**  

Fare clic su hello **formato** sezione, quindi selezionare **colori dati**, fare clic su hello **"On"** troppo**Mostra tutto**  
    ![Automobili connesse: mostra tutti i colori dei dati](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)  

Modificare il colore di hello di singole città facendo clic sull'icona di colore.  
    ![Automobili connesse: modifica colori](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

Fare clic su nuova visualizzazione tooadd area vuota hello.  

Dalle visualizzazioni selezionare **Istogramma a colonne raggruppate**, trascinare il campo **città** nell'area **Asse**, **Modello** nell'area **Legenda** e **vin** nell'area **Valore**.  
    ![Automobili connesse: istogramma a colonne raggruppate](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)  
    ![Automobili connesse: rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)

Ridisporre la visualizzazione nella pagina come illustrato nella figura.  
    ![Automobili connesse: visualizzazioni](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

Report in tempo reale di hello "Veicoli nell'operazione" è stata configurata. È possibile procedere toocreate hello successivo in tempo reale report o interrompere la procedura e configurare hello dashboard. 

### <a name="2-vehicles-requiring-maintenance"></a>2. Veicoli che richiedono manutenzione
Fare clic su ![Aggiungi](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd un nuovo report, rinominare troppo**"Veicoli che richiedono manutenzione"**

![Automobili connesse: veicoli che richiedono manutenzione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

Selezionare **VPN** campo e modificare il tipo di visualizzazione troppo**scheda**.  
    ![Automobili connesse: visualizzazione scheda vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)  

Abbiamo un campo denominato "MaintenanceLabel" nel set di dati hello. Questo campo può avere un valore pari a "0" o "1". Viene impostato dal modello di Azure Machine Learning hello effettuato il provisioning come parte della soluzione e integrato con il percorso di hello in tempo reale. il valore di Hello "1" indica che un veicolo richiede attività di manutenzione. 

tooadd un **a livello di pagina** filtro per la visualizzazione dei dati veicoli, che richiedono manutenzione: 

1. Hello trascinare **"MaintenanceLabel"** campo in **filtri a livello di pagina**.  
   ![Automobili connesse: filtri del livello di pagina](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)  
2. Fare clic sul menu **Basic Filtering** presente in basso nella schermata del filtro MaintenanceLabel in Page Level Filter.  
   ![Automobili connesse: filtro base](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)  
3. Impostare il valore di filtro troppo**"1"**    
   ![Automobili connesse: valore di filtro](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)  

Fare clic su nuova visualizzazione tooadd area vuota hello.  

Dalle visualizzazioni selezionare **Istogramma a colonne raggruppate**  
![Automobili connesse: visualizzazione scheda vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)  
![Automobili connesse: istogramma a colonne raggruppate](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)

Campo trascinare **modello** in **asse** area **VPN** troppo**valore** area. Ordinare quindi la visualizzazione in base a **Count of vin**.  Il grafico cambia **titolo** troppo**"Veicoli richiesta dal modello di manutenzione"**  

Trascinare i campi **vin** in **Saturazione colore** presente nella sezione **Campi** ![Campi](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) della scheda **Visualizzazione**  
![Automobili connesse: saturazione dei colori](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)  

Modificare **Colori dati** nelle visualizzazioni dalla sezione **Formato**  
Cambiare il colore minimo in: **F2C812**  
Cambiare il colore minimo in: **FF6300**  
![Automobili connesse: modifiche dei colori](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)  
![Automobili connesse: nuovi colori di visualizzazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)  

Fare clic su nuova visualizzazione tooadd area vuota hello.  

Selezionare **Istogramma a colonne raggruppate** dalle visualizzazioni, trascinare il campo **vin** nell'area **Valore** e il campo **Città** nell'area **Asse**. Ordinare il grafico in base a **"Count of vin"**. Il grafico cambia **titolo** troppo**"Veicoli che richiedono manutenzione in base alla città"**   
![Automobili connesse: veicoli che richiedono manutenzione in base alla città](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)  

Fare clic su nuova visualizzazione tooadd area vuota hello.  

Selezionare **scheda con più righe** visualizzazione da visualizzazioni, trascinare **modello** e **VPN** in hello **campi** area.  
![Automobili connesse: scheda con più righe](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)    

Report finale hello ridisposizione tutti di visualizzazione hello, simile al seguente:  
![Automobili connesse: scheda con più righe](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

È stato configurato correttamente i report in tempo reale di hello "Veicoli che richiedono manutenzione". È possibile procedere toocreate hello successivo in tempo reale report o interrompere la procedura e configurare hello dashboard. 

### <a name="3-vehicles-health-statistics"></a>3. Statistiche sull'integrità dei veicoli
Fare clic su ![Aggiungi](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd nuovo report, rinominarla troppo**"Veicoli delle statistiche di integrità"**  

Selezionare **misuratore** visualizzazione da visualizzazioni, quindi trascinare hello **velocità** campo in **, valore minimo, massimo valore** aree.  
![Automobili connesse: scheda con più righe](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)  

Modificare l'aggregazione predefinita hello di **velocità** in **valore area** troppo**medio** 

Modificare l'aggregazione predefinita hello di **velocità** in **area minima** troppo**minimo**

Modificare l'aggregazione predefinita hello di **velocità** in **area massima** troppo**massimo**

![Automobili connesse: scheda con più righe](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

Rinominare hello **misuratore titolo** troppo**"Velocità media"** 

![Automobili connesse: misuratore](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

Fare clic su nuova visualizzazione tooadd area vuota hello.  

Allo stesso modo, aggiungere un **Misuratore** per **media olio motore**, **media carburante** e **media temperatura motore**.  

Modificare l'aggregazione predefinita hello di campi in ogni misuratore in base di sopra di passaggi **"Velocità media"** del misuratore.

![Automobili connesse: misuratori](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

Fare clic su nuova visualizzazione tooadd area vuota hello.

Selezionare **riga e istogramma a colonne raggruppate** visualizzazioni, quindi trascinare **Città** campo in **asse condiviso**, trascinare **velocità**, **campi tirepressure ed engineoil** in **i valori di colonna** area, modificare il tipo di aggregazione troppo**Media**. 

Hello trascinare **engineTemperature** campo in **valori riga** area, modificare il tipo di aggregazione di hello troppo**Media**. 

![Automobili connesse: campi di visualizzazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

Grafico hello modifica **titolo** troppo**"Media velocità, pressione tire, olio motore e temperatura del motore"**.  

![Automobili connesse: campi di visualizzazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

Fare clic su nuova visualizzazione tooadd area vuota hello.

Selezionare **Treemap** visualizzazione da visualizzazioni, trascinare hello **modello** campo in hello **gruppo** area e trascinare hello  **MaintenanceProbability** in hello **valori** area.

Grafico hello modifica **titolo** troppo**"Modelli veicolo che richiedono manutenzione"**.

![Automobili connesse: modifica titolo del grafico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

Fare clic su nuova visualizzazione tooadd area vuota hello.

Selezionare **barre del grafico in pila 100%** dalla visualizzazione, trascinare hello **Città** campo in hello **asse** area e trascinare hello **MaintenanceProbability**, **RecallProbability** campi hello **valore** area.

![Automobili connesse: aggiungi nuova visualizzazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

Fare clic su **formato**selezionare **colori dati**e set hello **MaintenanceProbability** toohello valore di colore **"F2C80F"**.

Hello modifica **titolo** di hello grafico troppo**"Probabilità del veicolo manutenzione e richiamare by City"**.

![Automobili connesse: aggiungi nuova visualizzazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

Fare clic su nuova visualizzazione tooadd area vuota hello.

Selezionare **grafico ad Area** dalla visualizzazione da visualizzazioni, trascinare hello **modello** campo in hello **asse** area e trascinare hello **engineOil, tirepressure, velocità e MaintenanceProbability** campi hello **valori** area. Modificare il tipo di aggregazione troppo**"Medio"**. 

![Automobili connesse: modifica tipo di aggregazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

Modificare il titolo di hello del grafico hello troppo**"Media olio motore, tire probabilità pressione, velocità e la manutenzione dal modello"**.

![Automobili connesse: modifica titolo del grafico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

Fare clic su nuova visualizzazione tooadd area vuota hello:

1. Nelle visualizzazioni selezionare **Scatter Chart** .
2. Hello trascinare **modello** campo in hello **dettagli** e **legenda** area.
3. Hello trascinare **carburante** campo in hello **asse x** area, modificare anche le aggregazioni hello**Media**.
4. Trascinare **engineTemparature** in **area asse y**, modificare anche le aggregazioni hello**medio**
5. Hello trascinare **VPN** campo in hello **dimensioni** area.

![Automobili connesse: aggiungi nuova visualizzazione](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

Grafico hello modifica **titolo** troppo**"Medie di carburante, temperatura motore dal modello"**.

![Automobili connesse: modifica titolo del grafico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

report finale Hello apparirà come illustrato di seguito.

![Automobili connesse: report finale](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-hello-reports-toohello-real-time-dashboard"></a>Visualizzazioni di pin di dashboard in tempo reale di hello report toohello
Creare un dashboard vuoto da facendo clic sull'icona di addizione hello tooDashboards successivo. È possibile denominarlo "Dashboard di analisi dei dati di telemetria di veicolo".

![Automobili connesse: dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

Visualizzazione di hello pin da hello sopra dashboard toohello di report. 

![Automobili connesse: dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

Quando tutti hello tre report vengono creati e hello corrispondente visualizzazioni dashboard toohello bloccati, dashboard Hello dovrebbe apparire come segue. Se non è stato creato tutti i report di hello, il dashboard potrebbe essere diverso. 

![Automobili connesse: dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

Congratulazioni. Dashboard in tempo reale hello è stato creato. Mentre si continua a tooexecute CarEventGenerator.exe e RealtimeDashboardApp.exe, vedrai aggiornamenti in tempo reale nel dashboard di hello. Occorrere hello di toocomplete too15 circa 10 minuti alla procedura seguente.

## <a name="setup-power-bi-batch-processing-dashboard"></a>Configurare il dashboard di elaborazione batch di PowerBI
> [!NOTE]
> Accetta circa due ore (da hello corretto completamento di distribuzione hello) per il batch di tooend fine hello esecuzione toofinish della pipeline di elaborazione e l'elaborazione di un valore di anno di dati generati. Pertanto si consiglia di attendere hello toofinish prima di procedere con passaggi successivi hello di elaborazione. 
> 
> 

**Scaricare il file della finestra di progettazione di Power BI hello**

* Un file della finestra di progettazione di Power BI configurati in precedenza è incluso come parte della distribuzione hello istruzioni operazione manuale
* Cercare 2. Dashboard di elaborazione batch di installazione Power BI è possibile scaricare il modello di Power BI hello per l'elaborazione batch dashboard denominate **ConnectedCarsPbiReport.pbix**.
* Salvare in locale

**Configurare i report di Power BI**

* File di progettazione aprire hello '**ConnectedCarsPbiReport.pbix**' con Power BI Desktop. Se non si dispone, installa hello Power BI Desktop dal [installare Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331). 
* Fare clic su hello **modifica query**.

![Modificare la query di Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* Fare doppio clic su hello **origine**.

![Impostare l'origine di Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* Aggiornare la stringa di connessione Server con hello Azure SQL server in cui è stato eseguito il provisioning come parte della distribuzione hello.  Cerca in istruzioni di operazione manuale hello in 

    4. Database SQL di Azure
    
    * Server: somethingsrv.database.windows.net
    * Database: connectedcar
    * Nome utente: nome utente
    * Password: è possibile gestire la password di SQL Server dal portale di Azure

* Lasciare **Database** come *connectedcar*.

![Impostare il database Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* Fare clic su **OK**.
* Si noterà **credenziale Windows** scheda selezionata per impostazione predefinita, modificarla troppo**le credenziali del Database** facendo clic su **Database** scheda nella parte destra.
* Fornire hello **Username** e **Password** di Database SQL di Azure che è stato specificato durante il programma di installazione di distribuzione.

![Ottenere le credenziali del database](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* Fare clic su **Connetti**
* Ripetere hello sopra i passaggi per ogni query hello tre rimanenti presenti nel riquadro destro e quindi aggiornare i dettagli di connessione origine dati hello.
* Fare clic su **Chiudi e carica**. Set di file di dati di Power BI Desktop sono tabelle di Database di Azure tooSQL connesso.
* **Chiudi** per chiudere il file Power BI Desktop.

![Chiudere Power BI Desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* Fare clic su **salvare** pulsante modifiche hello toosave. 

È stato configurato tutti i report di hello toohello percorso di elaborazione batch nella soluzione hello corrispondente. 

## <a name="upload-toopowerbicom"></a>Caricare troppo*powerbi.com*
1. Passare portale web di Power BI toohello http://powerbi.com e account di accesso.
2. Fare clic su **Recupera dati**  
3. Caricare il File di Power BI Desktop hello.  
4. tooupload, fare clic su **recupera dati -> ottenere file -> file locale**  
5. Passare toohello **"**ConnectedCarsPbiReport.pbix**"**  
6. Una volta caricato il file hello, sarà tooyour indietro spostarsi area di lavoro di Power BI.  

Verranno creati automaticamente un set di dati, un report e un dashboard vuoto.  

PIN grafici tooa nuovo dashboard chiamato **veicolo telemetria Analitica Dashboard** in **Power BI**. Fare clic su dashboard di hello vuoto creato in precedenza e quindi passare toohello **report** fare clic su sezione hello appena caricato report.  

![Vehicle Telemetry Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

**Nota hello report ha sei pagine:**  
Pagina 1: Densità veicolo  
Pagina 2: Integrità veicolo in tempo reale  
Pagina 3: Veicoli guidati in modo aggressivo   
Pagina 4: Veicoli richiamati  
Pagina 5: Veicoli con consumo di carburante efficiente  
Pagina 6: Logo di Contoso  

![Connected Cars Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

**Dalla pagina 3**, aggiungere il seguente hello:  

1. Count of vin  
   ![Connected Cars Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. Veicoli guidati in modo aggressivo in base al modello: grafico a cascata   
   ![Telemetria veicolo: aggiungi grafici 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

**Dalla pagina 5**, aggiungere il seguente hello: 

1. Count of vin    
   ![Telemetria veicolo: aggiungi grafici 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. Veicoli guidati con un consumo efficiente del carburante in base al modello: istogramma a colonne raggruppate   
   ![Telemetria veicolo: aggiungi grafici 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

**Dalla pagina 4**, aggiungere il seguente hello:  

1. Count of vin  
   ![Telemetria veicolo: aggiungi grafici 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. Veicoli richiamati in base alla città e al modello: grafico ad albero   
   ![Telemetria veicolo: aggiungi grafici 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

**Dalla pagina 6**, aggiungere il seguente hello:  

1. Logo Contoso Motors   
   ![Telemetria veicolo: aggiungi grafici 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

**Organizzare il dashboard di hello**  

1. Passare toohello dashboard
2. Passare il mouse su ogni grafico e rinominarlo in base a denominazione hello fornito nell'immagine di un dashboard completo hello riportato di seguito. Spostare anche i grafici di hello intorno toolook come dashboard hello riportato di seguito.  
   ![Telemetria veicolo: organizza dashboard 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Vehicle Telemetry Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. Se è stato creato tutti i report di hello, come indicato in questo documento, hello finale dashboard completato dovrebbe essere simile hello seguente illustrazione. 

![Telemetria veicolo: organizza dashboard 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

Congratulazioni. Sono stati creati correttamente i report di hello e hello toogain dashboard in tempo reale, predittiva e abitudini di insights di batch su integrità veicolo e la Guida.  
