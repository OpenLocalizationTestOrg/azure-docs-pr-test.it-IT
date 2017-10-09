---
title: aaaExport Log Analitica dati tooPower BI | Documenti Microsoft
description: "Power BI è un servizio di analisi business basato sul cloud di Microsoft che fornisce report e visualizzazioni dettagliate per l'analisi di diversi set di dati.  Log Analitica può continuamente esportare dati dal repository OMS hello in Power BI in modo che è possibile sfruttare le visualizzazioni e gli strumenti di analisi.  Questo articolo descrive la modalità di query tooconfigure in Analitica di Log che esportano automaticamente tooPower BI a intervalli regolari."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 83edc411-6886-4de1-aadd-33982147b9c3
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: bwren
ms.openlocfilehash: 4822f99677e5d1080c72e95cda410da81615bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="export-log-analytics-data-toopower-bi"></a>Esportare i dati di Log Analitica tooPower BI

>[!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi questo processo per l'esportazione di dati di Log Analitica tooPower BI non funzionerà più.  Le pianificazioni esistenti create prima dell'aggiornamento verranno disabilitate. 
>
> Dopo l'aggiornamento, viene utilizzato Azure Log Analitica hello stessa piattaforma come Application Insights e si utilizza hello stessa procedura adottata tooexport Analitica Log query tooPower BI come [tooexport processo hello Application Insights query tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).  È possibile esportare query hello utilizzando console Analitica hello, come descritto nell'articolo oppure è possibile selezionare hello **Power BI** pulsante nella parte superiore di hello della schermata Ciao nel portale di ricerca nei Log hello.



[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) è un servizio di analisi business basato sul cloud di Microsoft che fornisce visualizzazioni dettagliate e report per l'analisi di differenti set di dati.  Log Analitica può automaticamente esportare dati dal repository OMS hello in Power BI in modo che è possibile sfruttare le visualizzazioni e gli strumenti di analisi.

Quando si configura Power BI con Log Analitica, creare query di log che esporta i set di risultati toocorresponding dati in Power BI.  esportazione e query hello continua tooautomatically eseguita in una pianificazione che si definisce il set di dati di tookeep hello backup toodate con dati più recenti di hello raccolti da Log Analitica.

![Log Analitica tooPower BI](media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a>Pianificazioni di Power BI
Oggetto *Power BI pianificazione* include una ricerca di log che consente di esportare un set di dati da hello OMS repository tooa corrispondente set di dati in Power BI e una pianificazione che definisce la frequenza con cui questa ricerca viene eseguita tookeep hello dataset corrente.

i campi nel set di dati hello Hello corrisponderà proprietà hello dei record di hello restituito dalla ricerca log hello.  Se ricerca hello restituisce i record di diversi tipi di set di dati hello includerà tutte le proprietà di hello da ognuno di hello incluse tipi di record.  

> [!NOTE]
> Si tratta di un migliore toouse pratica una query di ricerca di log che restituisce dati non elaborati anziché tooperforming qualsiasi consolidamento utilizzando i comandi, ad esempio [misura](log-analytics-search-reference.md#measure).  È possibile eseguire qualsiasi delle aggregazioni e calcoli in Power BI da dati non elaborati hello.
>
>

## <a name="connecting-oms-workspace-toopower-bi"></a>Connessione dell'area di lavoro OMS tooPower BI
Prima di poter esportare dal Log Analitica tooPower BI, è necessario connettersi all'account di Power BI tooyour dell'area di lavoro OMS utilizzando hello seguente procedura.  

1. Nella console OMS hello fare clic su hello **impostazioni** riquadro.
2. Selezionare **Account**.
3. In hello **Workspace Information** fare clic su sezione **connettersi tooPower Account BI**.
4. Immettere le credenziali di hello per l'account di Power BI.

## <a name="create-a-power-bi-schedule"></a>Creare una pianificazione di Power BI
Creare una pianificazione di Power BI per ogni set di dati utilizzando hello seguente procedura.

1. Nella console OMS hello fare clic su hello **ricerca nei Log** riquadro.
2. Digitare una nuova query o selezionare una ricerca salvata, che restituisce hello dati che si desidera tooexport troppo**Power BI**.  
3. Fare clic su hello **Power BI** pulsante nella parte superiore di hello di hello di hello pagina tooopen **Power BI** finestra di dialogo.
4. Fornire le informazioni di hello in hello seguente tabella, fare clic **salvare**.

| Proprietà | Descrizione |
|:--- |:--- |
| Nome |Nome tooidentify hello pianificazione quando si visualizza l'elenco di hello di pianificazioni di Power BI. |
| Ricerca salvata |Hello toorun di ricerca log.  È possibile selezionare la query corrente hello o selezionare una ricerca salvata dalla casella a discesa hello. |
| Pianificazione |La frequenza con cui hello toorun salvato ricerca e l'esportazione di set di dati toohello Power BI.  il valore di Hello deve essere compreso tra 15 minuti e 24 ore. |
| Nome del set di dati |nome Hello del set di dati di hello in Power BI.  Verrà creato se non esiste e aggiornato se esiste. |

## <a name="viewing-and-removing-power-bi-schedules"></a>Visualizzazione e rimozione di pianificazioni di Power BI
Hello visualizzazione esistente le pianificazioni di Power BI con hello seguente procedura.

1. Nella console OMS hello fare clic su hello **impostazioni** riquadro.
2. Selezionare **Power BI**.

Inoltre di pianificare i dettagli di toohello di hello, quante volte hello pianificazione hello è stato eseguito in hello settimana scorsa e vengono visualizzati lo stato di hello dell'ultima sincronizzazione hello.  Se si verificano errori di sincronizzazione hello, è possibile fare clic su hello collegamento toorun una ricerca di log per i record con i dettagli dell'errore hello.

È possibile rimuovere una pianificazione facendo clic su hello **X** in hello **Rimuovi colonna**.  È possibile disabilitare una pianificazione selezionando **No**.  toomodify una pianificazione è necessario rimuoverla e ricrearla con le nuove impostazioni hello.

![Pianificazioni di Power BI](media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a>Procedura dettagliata di esempio
Hello nella sezione seguente vengono illustrati un esempio di creazione di una pianificazione di Power BI e toocreate il set di dati utilizzando un report semplice.  In questo esempio, tutti i dati sulle prestazioni per un insieme di computer viene esportato tooPower BI e quindi viene creato l'utilizzo del processore toodisplay un grafico a linee.

### <a name="create-log-search"></a>Creare una ricerca dei log
Si inizierà creando una ricerca di log per i dati di hello che si desidera toosend toohello set di dati.  In questo esempio si userà una query che restituisce tutti i dati sulle prestazioni per i computer con un nome che inizia con *srv*.  

![Pianificazioni di Power BI](media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a>Creare una ricerca di Power BI
Si fa clic hello **Power BI** pulsante finestra di dialogo tooopen hello Power BI e fornire informazioni di hello necessario.  Si desidera questo toorun ricerca una volta ogni ora e creare un set di dati denominato *Contoso Perf*.  Poiché è già aperta hello ricerca che consente di creare dati hello desiderato, è mantenere predefinito hello *query di ricerca corrente utilizzare* per **ricerca salvata**.

![Ricerca di Power BI](media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a>Verificare la ricerca di Power BI
tooverify di pianificazione di hello è stato creato correttamente, è elenco hello delle ricerche di Power BI in hello **impostazioni** riquadro nel dashboard OMS hello.  È attendere qualche minuto e aggiornare la visualizzazione finché non vengono segnalati che sia stata eseguita la sincronizzazione hello.

![Ricerca di Power BI](media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-hello-dataset-in-power-bi"></a>Verificare dataset hello in Power BI
Vengono registrate in conto in [pagina powerbi.microsoft.com](http://powerbi.microsoft.com/) e scorrere troppo**set di dati** nella parte inferiore di hello del riquadro di sinistra hello.  Possiamo vedere che hello *Contoso Perf* set di dati elencato che indica che l'esportazione è stata eseguita correttamente.

![Set di dati di Power BI](media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a>Creare report basato sul set di dati
Selezionare hello **Contoso Perf** set di dati e quindi fare clic su **risultati** in hello **campi** riquadro campi di hello tooview destra hello che fanno parte di questo set di dati.  toocreate utilizzo del processore che mostra grafico una riga per ogni computer, eseguire hello seguenti azioni.

1. Selezionare la visualizzazione grafico di riga hello.
2. Trascinare **ObjectName** troppo**filtro del livello Report** e controllare **processore**.
3. Trascinare **CounterName** troppo**filtro del livello Report** e controllare **% tempo processore**.
4. Trascinare **CounterValue** troppo**valori**.
5. Trascinare **Computer** troppo**legenda**.
6. Trascinare **TimeGenerated** troppo**asse**.

È possibile osservare che il grafico a linee hello risultante viene visualizzato con dati hello il set di dati.

![Grafico a linee di Power BI](media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-hello-report"></a>Salvare il report hello
Si salva il rapporto hello facendo clic su hello pulsante in alto hello hello Salva e convalida che è ora elencato nella sezione report hello nel riquadro di sinistra hello.

![Report di Power BI](media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su [log ricerche](log-analytics-log-searches.md) toobuild query che possono essere esportati tooPower BI.
* Altre informazioni, vedere [Power BI](http://powerbi.microsoft.com) toobuild visualizzazioni in base alle esportazioni Analitica di Log.
