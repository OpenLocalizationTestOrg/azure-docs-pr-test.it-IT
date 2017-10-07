---
title: "soluzione di integrità in OMS aaaAgent | Documenti Microsoft"
description: "Questo articolo è toohelp previsto è comprendere come toouse toomonitor questa soluzione hello integrità di agenti di reporting direttamente tooOMS o System Center Operations Manager."
services: operations-management-suite
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: magoedte
ms.openlocfilehash: 071b14b4ab7af6680ae458eaa331246755c5bb56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
#  <a name="agent-health-solution-in-oms"></a>Soluzione Integrità agente in OMS
soluzione di integrità agente Hello in OMS consente di comprendere, per tutti gli agenti di hello reporting direttamente l'area di lavoro OMS toohello o un tooOMS gruppo connesso gestione di System Center Operations Manager, ovvero che non risponde e l'invio dati operativi.  È possibile anche tenere traccia dei numero di agenti viene distribuito, in cui sono distribuiti geograficamente ed eseguire altri consapevolezza toomaintain query della distribuzione hello degli agenti distribuiti in Azure, gli altri ambienti cloud o locale.    

## <a name="prerequisites"></a>Prerequisiti
Prima di distribuire questa soluzione, confermare è supportato [degli agenti Windows](../log-analytics/log-analytics-windows-agents.md) reporting toohello area di lavoro OMS o reporting tooan [il gruppo di gestione di Operations Manager](../log-analytics/log-analytics-om-agents.md) integrato con il Area di lavoro OMS.    

## <a name="solution-components"></a>Componenti della soluzione
Questa soluzione è costituita da hello seguendo le risorse che vengono aggiunti tooyour dell'area di lavoro e gli agenti direttamente connessi o gruppo di gestione connesso Operations Manager.

### <a name="management-packs"></a>Management Pack
Se il gruppo di gestione di System Center Operations Manager è l'area di lavoro OMS tooan connesso, hello seguenti management pack viene installato in Operations Manager.  Questi Management Pack vengono installati anche su computer Windows direttamente connessi dopo l'aggiunta di questa soluzione. Non c'è niente tooconfigure o gestiranno con questi management pack.

* Microsoft System Center Advisor HealthAssessment Direct Channel Intelligence Pack (Microsoft.IntelligencePacks.HealthAssessmentDirect)
* Microsoft System Center Advisor HealthAssessment Server Channel Intelligence Pack (Microsoft.IntelligencePacks.HealthAssessmentViaServer).  

Per ulteriori informazioni sulla modalità di aggiornamento dei management pack di soluzione, vedere [tooLog connettere Operations Manager Analitica](../log-analytics/log-analytics-om-agents.md).

## <a name="configuration"></a>Configurazione
Aggiungere hello integrità agente soluzione tooyour all'area di lavoro OMS tramite il processo di hello [aggiungere soluzioni](../log-analytics/log-analytics-add-solutions.md). Non è richiesta alcuna ulteriore configurazione.


## <a name="data-collection"></a>Raccolta dei dati
### <a name="supported-agents"></a>Agenti supportati
Hello nella tabella seguente descrive hello connesso origini supportate da questa soluzione.

| Origine connessa | Supportato | Descrizione |
| --- | --- | --- |
| Agenti di Windows | Sì | Gli eventi di heartbeat vengono raccolti dagli agenti di Windows diretti.|
| Gruppo di gestione di System Center Operations Manager | Sì | Eventi di heartbeat vengono raccolti dagli agenti reporting toohello gruppo di gestione ogni 60 secondi e quindi vengono inoltrati tooLog Analitica. Una connessione diretta da tooLog gli agenti di Operations Manager non è necessario Analitica. Dati dell'evento heartbeat viene inoltrati dal repository di hello gestione gruppo toohello Analitica di Log.|

## <a name="using-hello-solution"></a>Utilizzo di soluzione hello
Quando si aggiunge l'area di lavoro OMS tooyour soluzione hello, hello **integrità agente** riquadro verrà aggiunto il dashboard OMS tooyour. Questo riquadro mostra il numero totale di hello degli agenti e il numero di hello degli agenti che non risponde in hello ultime 24 ore.<br><br> ![Riquadro della soluzione Integrità agente nel dashboard](./media/oms-solution-agenthealth/agenthealth-solution-tile-homepage.png)

Fare clic su hello **integrità agente** riquadro tooopen hello **integrità agente** dashboard.  dashboard Hello sono incluse colonne hello hello nella tabella seguente. Ogni colonna elenca gli eventi di dieci superiore di hello dal conteggio che soddisfano i criteri della colonna per hello specificato intervallo di tempo. È possibile eseguire una ricerca di log che fornisce l'intero elenco hello selezionando **tutti** hello in basso a destra di ogni colonna, oppure facendo clic sull'intestazione di colonna hello.

| Colonna | Descrizione |
|--------|-------------|
| Agent count over time (Conteggio nel tempo) | Tendenza del conteggio dell'agente in un periodo di sette giorni per agenti di Linux e Windows.|
| Count of unresponsive agents (Conteggio di agenti che non rispondono) | Un elenco degli agenti che è ancora stato inviato un heartbeat in hello nelle ultime 24 ore.|
| Distribution by OS Type (Distribuzione per tipo di sistema operativo) | Indicazione del numero di agenti di Windows e Linux disponibili nell'ambiente.|
| Distribuzione per versione dell'agente | Una partizione hello diverse delle versioni dell'agente installato nel proprio ambiente e un conteggio di ciascuna di esse.|
| Distribuzione per categoria dell'agente | Una partizione di hello le diverse categorie di agenti che inviano eventi heartbeat: diretta degli agenti, gli agenti OpsMgr o hello Server di gestione di Operations Manager.|
| Distribuzione per gruppo di gestione | Una partizione hello diversi SCOM dei gruppi di gestione nell'ambiente in uso.|
| Posizione geografica degli agenti | Una partizione di diversi paesi hello in cui si dispone di agenti e il numero totale di numero hello di agenti che sono stati installati in ogni paese.|
| Count of Gateways Installed (Conteggio dei gateway installati) | numero di Hello del server che dispongono di hello installato il Gateway di OMS e un elenco di questi server.|

![Esempio di dashboard della soluzione Integrità agente](./media/oms-solution-agenthealth/agenthealth-solution-dashboard.png)  

## <a name="log-analytics-records"></a>Record di Log Analytics
soluzione Hello crea un tipo di record nel repository OMS hello.  

### <a name="heartbeat-records"></a>Record di heartbeat
Viene creato un record di tipo **Heartbeat**.  Questi record dispongono di proprietà di hello in hello nella tabella seguente.  

| Proprietà | Descrizione |
| --- | --- |
| Tipo | *Heartbeat*|
| Categoria | Il valore è *Agente diretto*, *SCOM Agent* (Agente SCOM) o *SCOM Management Server* (Server di gestione SCOM).|
| Computer | Nome del computer.|
| OSType | Sistema operativo Windows o Linux.|
| OSMajorVersion | Versione principale del sistema operativo.|
| OSMinorVersion | Versione secondaria del sistema operativo.|
| Versione | Versione dell'agente di OMS o dell'agente di Operations Manager.|
| SCAgentChannel | Il valore è *Direct* e/o *SCManagementServer*.|
| IsGatewayInstalled | Se il Gateway OMS è installato, il valore è *true*. In caso contrario, il valore è *false*.|
| ComputerIP | Indirizzo IP del computer hello.|
| RemoteIPCountry | Posizione geografica in cui è distribuito il computer.|
| ManagementGroupName | Nome del gruppo di gestione di Operations Manager.|
| SourceComputerId | ID univoco del computer.|
| RemoteIPLongitude | Longitudine della posizione geografica del computer.|
| RemoteIPLatitude | Latitudine della posizione geografica del computer.|

Ogni agente di reporting server di gestione di Operations Manager tooan invierà due heartbeat e includerà sia il valore della proprietà SCAgentChannel **diretto** e **SCManagementServer** a seconda di ciò Origini dati di log Analitica e le soluzioni che è stata abilitata nella sottoscrizione OMS. Se si ricorderà, dati da soluzioni vengono inviati direttamente da Operations Manager management server toohello OMS servizio web oppure a causa di hello volume dei dati raccolti sull'agente hello, vengono inviati direttamente dal servizio web di hello agente tooOMS. Per gli eventi di heartbeat il cui valore hello **SCManagementServer**, hello ComputerIP valore è l'indirizzo IP hello hello del server di gestione poiché dati hello viene effettivamente caricati da esso.  Per gli heartbeat in cui è impostato troppo SCAgentChannel**diretto**, è l'indirizzo IP pubblico hello dell'agente di hello.  

## <a name="sample-log-searches"></a>Ricerche di log di esempio
Hello nella tabella seguente fornisce ricerche log di esempio per i record raccolti da questa soluzione.

| Query | Descrizione |
| --- | --- |
| Type=Heartbeat &#124; distinct Computer |Numero totale di agenti |
| Type=Heartbeat &#124; measure max(TimeGenerated) as LastCall by Computer &#124; where LastCall < NOW-24HOURS |Numero di agenti che non risponde in hello ultime 24 ore |
| Type=Heartbeat &#124; measure max(TimeGenerated) as LastCall by Computer &#124; where LastCall < NOW-15MINUTES |Numero di agenti che non risponde in hello ultimi 15 minuti |
| Type=Heartbeat TimeGenerated>NOW-24HOURS Computer IN {Type=Heartbeat TimeGenerated>NOW-24HOURS &#124; distinct Computer} &#124; measure max(TimeGenerated) as LastCall by Computer |Computer online (Buongiorno ultime 24 ore) |
| Type=Heartbeat TimeGenerated>NOW-24HOURS Computer NOT IN {Type=Heartbeat TimeGenerated>NOW-30MINUTES &#124; distinct Computer} &#124; measure max(TimeGenerated) as LastCall by Computer |Totale agenti Offline negli ultimi 30 minuti (per hello ultime 24 ore) |
| Type=Heartbeat &#124; measure countdistinct(Computer) by OSType |Tendenza del numero di agenti nel tempo per OSType|
| Type=Heartbeat&#124;measure countdistinct(Computer) by OSType |Distribuzione per tipo di sistema operativo |
| Type=Heartbeat&#124;measure countdistinct(Computer) by Version |Distribuzione per versione dell'agente |
| Type=Heartbeat&#124;measure count() by Category |Distribuzione per categoria dell'agente |
| Type=Heartbeat&#124;measure countdistinct(Computer) by ManagementGroupName | Distribuzione per gruppo di gestione |
| Type=Heartbeat&#124;measure countdistinct(Computer) by RemoteIPCountry |Posizione geografica degli agenti |
| Type=Heartbeat IsGatewayInstalled=true&#124;Distinct Computer |Numero di gateway OMS installati |


>[!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](../log-analytics/log-analytics-log-search-upgrade.md), quindi hello sopra query modificherebbe toohello seguente.
>
>| Query | Descrizione |
|:---|:---|
| Heartbeat &#124; distinct Computer |Numero totale di agenti |
| Heartbeat &#124; summarize LastCall = max(TimeGenerated) by Computer &#124; where LastCall < ago(24h) |Numero di agenti che non risponde in hello ultime 24 ore |
| Heartbeat &#124; summarize LastCall = max(TimeGenerated) by Computer &#124; where LastCall < ago(15m) |Numero di agenti che non risponde in hello ultimi 15 minuti |
| Heartbeat &#124; where TimeGenerated > ago(24h) and Computer in ((Heartbeat &#124; where TimeGenerated > ago(24h) &#124; distinct Computer)) &#124; summarize LastCall = max(TimeGenerated) by Computer |Computer online (Buongiorno ultime 24 ore) |
| Heartbeat &#124; where TimeGenerated > ago(24h) and Computer !in ((Heartbeat &#124; where TimeGenerated > ago(30m) &#124; distinct Computer)) &#124; summarize LastCall = max(TimeGenerated) by Computer |Totale agenti Offline negli ultimi 30 minuti (per hello ultime 24 ore) |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by OSType |Tendenza del numero di agenti nel tempo per OSType|
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by OSType |Distribution by OS Type (Distribuzione per tipo di sistema operativo) |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by Version |Distribuzione per versione dell'agente |
| Heartbeat &#124; summarize AggregatedValue = count() by Category |Distribuzione per categoria dell'agente |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by ManagementGroupName | Distribuzione per gruppo di gestione |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by RemoteIPCountry |Posizione geografica degli agenti |
| Heartbeat &#124; where iff(isnotnull(toint(IsGatewayInstalled)), IsGatewayInstalled == true, IsGatewayInstalled == "true") == true &#124; distinct Computer |Numero di gateway OMS installati |

## <a name="next-steps"></a>Passaggi successivi

* Leggere l'articolo [Avvisi in Log Analytics](../log-analytics/log-analytics-alerts.md) per informazioni dettagliate sulla generazione di avvisi di Log Analytics.
