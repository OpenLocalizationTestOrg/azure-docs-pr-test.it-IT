---
title: soluzione di gestione in OMS aaaUpdate | Documenti Microsoft
description: "Questo articolo è toohelp previsto è comprendere come toouse toomanage questa soluzione gli aggiornamenti per i computer Windows e Linux."
services: operations-management-suite
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: e33ce6f9-d9b0-4a03-b94e-8ddedcc595d2
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 2dd321913bf049ab1996fd60a2f74b8417084dcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="update-management-solution-in-oms"></a>Soluzione Gestione aggiornamenti in OMS

![Simbolo Gestione aggiornamenti](./media/oms-solution-update-management/update-management-symbol.png)

soluzione di gestione degli aggiornamenti in OMS Hello consente aggiornamenti della sicurezza del sistema operativo toomanage per i computer Windows e Linux distribuiti in Azure, locale ambienti o altri provider di cloud.  Rapidamente, è possibile valutare lo stato di hello degli aggiornamenti disponibili in tutti i computer agente e gestire il processo di hello di installazione degli aggiornamenti necessari per i server.


## <a name="solution-overview"></a>Panoramica della soluzione
I computer gestiti da OMS usare hello seguente tabella per la distribuzione di valutazione e aggiornamento:

* Agente OMS per Windows o Linux
* PowerShell DSC (Desired State Configuration) per Linux
* Ruolo di lavoro ibrido per runbook di Automazione
* Microsoft Update o Windows Server Update Services per computer Windows

Hello diagrammi seguente mostra una visualizzazione concettuale del flusso di dati e comportamento hello con come soluzione hello valuta e Applica protezione aggiornamenti tooall connessi a Windows Server e i computer Linux in un'area di lavoro.    

#### <a name="windows-server"></a>Windows Server
![Flusso del processo di gestione dell'aggiornamento di Windows Server](media/oms-solution-update-management/update-mgmt-windows-updateworkflow.png)

#### <a name="linux"></a>Linux
![Flusso del processo di gestione dell'aggiornamento di Linux](media/oms-solution-update-management/update-mgmt-linux-updateworkflow.png)

Dopo che il computer hello esegue un'analisi per la conformità degli aggiornamenti, l'agente OMS hello inoltra le informazioni di hello in tooOMS bulk. In un computer di finestra, analisi di conformità hello viene eseguita ogni 12 ore per impostazione predefinita.  Pianificazione analisi toohello, analisi hello conformità degli aggiornamenti viene inoltre avviato entro 15 minuti se hello Microsoft Monitoring Agent (MMA) viene riavviato, precedenti tooupdate installazione e dopo l'installazione dell'aggiornamento.  Con un computer Linux, analisi di conformità hello viene eseguita ogni 3 ore per impostazione predefinita e un'analisi di conformità viene avviata entro 15 minuti se hello MMA agent viene riavviato.  

Hello le informazioni di conformità viene quindi elaborate e riepilogate in dashboard hello inclusi nella soluzione hello Usa ricerca definito dall'utente o pre-definiti dal query.  soluzione Hello report di aggiornamento hello computer si basa l'origine si è configurato toosynchronize con.  Se il computer di Windows hello è tooWSUS tooreport configurato, a seconda di quando WSUS ultima sincronizzazione con Microsoft Update, i risultati di hello differiscano dalle quali Mostra Microsoft Updates.  Hello stesso per i computer Linux che sono configurati tooreport tooa di repository locale rispetto a un repository pubblico.   

È possibile distribuire e installare gli aggiornamenti software nei computer che richiedono aggiornamenti hello mediante la creazione di una distribuzione pianificata.  Gli aggiornamenti classificati come *facoltativo* non sono inclusi nell'ambito della distribuzione hello per i computer Windows, solo gli aggiornamenti necessari.  Hello distribuzione pianificata definisce quali computer di destinazione riceveranno gli aggiornamenti applicabili di hello, in base che specifica i computer in modo esplicito o selezionando un [gruppo di computer](../log-analytics/log-analytics-computer-groups.md) che è basato sul ricerche nei log di un set specifico di computer.  Inoltre, specificare una pianificazione tooapprove e designare un periodo di tempo quando gli aggiornamenti sono consentiti toobe installato all'interno.  Gli aggiornamenti vengono installati da runbook in Automazione di Azure.  Questi runbook non richiedono alcuna configurazione e non possono essere visualizzati.  Quando viene creata una distribuzione di aggiornamento, crea una pianificazione che avvia un runbook master di aggiornamento all'hello specificato per i computer incluso hello.  Questo runbook master avvia un runbook figlio in ogni agente che esegue l'installazione degli aggiornamenti necessari.       

Data di hello e un'ora specificata nella distribuzione degli aggiornamenti hello, il computer di destinazione hello esegue la distribuzione di hello in parallelo.  Un'analisi viene prima eseguita tooverify hello aggiornamenti sono ancora necessari e li installa.  È importante toonote per i computer client WSUS, se hello aggiornamenti non approvati in WSUS, la distribuzione di aggiornamenti hello avrà esito negativo.  risultati Hello di aggiornamenti applicato hello vengono inoltrati tooOMS toobe elaborati e riepilogati in dashboard hello o da ricerca di eventi di hello hello.     

## <a name="prerequisites"></a>Prerequisiti
* soluzione Hello supporta l'esecuzione le valutazioni degli aggiornamenti in Windows Server 2008 e versioni successive e aggiornare le distribuzioni in Windows Server 2008 R2 SP1 e versioni successive.  Le opzioni di installazione Server Core e Nano Server non sono supportate.

    > [!NOTE]
    > Supporto per la distribuzione di aggiornamenti tooWindows Server 2008 R2 SP1 richiede .NET Framework 4.5 e WMF 5.0 o versione successiva.
    >  
* I sistemi operativi client di Windows non sono supportati.  
* Gli agenti di Windows devono essere toocommunicate configurato con un server Windows Server Update Services (WSUS) o avere accesso tooMicrosoft aggiornamento.  

    > [!NOTE]
    > agente di Windows Hello non può essere gestito contemporaneamente da System Center Configuration Manager.  
    >
* CentOS 6 (x86/x64) e 7 (x64)  
* Red Hat Enterprise 6 (x86/x64) e 7 (x64)  
* SUSE Linux Enterprise Server 11 (x86/x64) e 12 (x64)  
* Ubuntu 12.04 LTS e versioni x86/x64 più recenti   
    > [!NOTE]  
    > aggiornamenti tooavoid viene applicati di fuori di una finestra di manutenzione in Ubuntu, riconfigurare aggiornamenti automatici toodisable pacchetto di aggiornamento automatico. Per informazioni su come tooconfigure questa operazione, vedere [argomento aggiornamenti automatici in hello Ubuntu Server Guida](https://help.ubuntu.com/lts/serverguide/automatic-updates.html).

* Gli agenti Linux devono avere repository degli aggiornamenti tooan accesso.  

    > [!NOTE]
    > Un agente OMS per Linux configurato aree di lavoro OMS toomultiple tooreport non è supportato con questa soluzione.  
    >

Per ulteriori informazioni su come tooinstall hello agente OMS per Linux e scaricare la versione più recente di hello, consultare troppo[agente Operations Management Suite per Linux](https://github.com/microsoft/oms-agent-for-linux).  Per informazioni su come tooinstall hello agente OMS per Windows, vedere [Operations Management Suite Agent for Windows](../log-analytics/log-analytics-windows-agents.md).  

### <a name="permissions"></a>Autorizzazioni
Aggiornare le distribuzioni in ordine toocreate, è necessario concedere il ruolo di collaboratore hello nell'account di automazione e l'area di lavoro Log Analitica toobe.  

## <a name="solution-components"></a>Componenti della soluzione
Questa soluzione è costituita da hello seguendo le risorse che vengono aggiunti account di automazione tooyour e agenti direttamente connessi o il gruppo di gestione connessi Operations Manager.

### <a name="management-packs"></a>Management Pack
Se il gruppo di gestione di System Center Operations Manager è l'area di lavoro OMS tooan connesso, hello seguenti management pack viene installato in Operations Manager.  Questi Management Pack vengono installati anche su computer Windows direttamente connessi dopo l'aggiunta di questa soluzione. Non c'è niente tooconfigure o gestiranno con questi management pack.

* Microsoft System Center Advisor Update Assessment Intelligence Pack (Microsoft.IntelligencePacks.UpdateAssessment)
* Microsoft.IntelligencePack.UpdateAssessment.Configuration (Microsoft.IntelligencePack.UpdateAssessment.Configuration)
* Update Deployment MP

Per ulteriori informazioni sulla modalità di aggiornamento dei management pack di soluzione, vedere [tooLog connettere Operations Manager Analitica](../log-analytics/log-analytics-om-agents.md).

### <a name="hybrid-worker-groups"></a>Gruppi di ruoli di lavoro ibridi
Dopo aver abilitato questa soluzione, tutti i computer Windows direttamente connessi tooyour area di lavoro OMS viene configurato automaticamente come un Runbook Worker ibrido toosupport hello incluso in questa soluzione.  Per ogni computer Windows gestiti da soluzione hello, verrà elencata nel Pannello di gruppi di lavoro ibridi Runbook hello dell'account di automazione hello hello convenzione di denominazione seguente *Hostname FQDN_GUID*.  Non è possibile applicare runbook a questi gruppi nell'account perché avranno esito negativo. Questi gruppi sono solo soluzioni di gestione hello toosupport desiderato.   

È tuttavia possibile aggiungere gruppo di lavoro ibridi per Runbook tooa i computer Windows hello nel toosupport di account di automazione runbook di automazione, purché si utilizza hello stesso account per la soluzione hello e l'appartenenza al gruppo di lavoro ibridi per Runbook.  Questa funzionalità è stata aggiunta tooversion 7.2.12024.0 di hello Runbook Worker ibrido.  

## <a name="configuration"></a>Configurazione
Eseguire i seguenti passaggi tooadd hello gestione aggiornamenti soluzione tooyour area di lavoro OMS hello e verificare i report di agenti. Area di lavoro già connesso tooyour agenti Windows vengono aggiunti automaticamente senza alcuna configurazione aggiuntiva.

È possibile distribuire una soluzione di hello utilizzando hello dei seguenti metodi:

* Da Azure Marketplace in hello portale di Azure selezionando l'offerta di automazione e controllo hello o soluzioni di gestione degli aggiornamenti
* Da hello OMS Solutions Gallery nell'area di lavoro OMS

Se si dispone già di un account di automazione e l'area di lavoro OMS collegato insieme in hello stesso gruppo di risorse e al paese, la selezione di automazione e controllo verrà verificare la configurazione solo installare la soluzione hello e configurarla in entrambi i servizi.  Selezione di soluzione di gestione degli aggiornamenti di hello da Azure Marketplace recapita hello stesso comportamento.  Se non si dispone di entrambi i servizi distribuiti nella sottoscrizione, seguire hello hello **Crea nuova soluzione** pannello e confermare il tooinstall hello altri preselezionate le soluzioni consigliate.  Facoltativamente, è possibile aggiungere tooyour soluzione di gestione degli aggiornamenti hello all'area di lavoro OMS attenendosi alla procedura hello [soluzioni OMS aggiungere](../log-analytics/log-analytics-add-solutions.md) da hello Solutions Gallery.  

### <a name="confirm-oms-agents-and-operations-manager-management-group-connected-toooms"></a>Verificare gli agenti OMS e Operations Manager Gestione gruppo connesso tooOMS

tooconfirm direttamente connessi agente OMS per Linux e Windows comunicano con OMS, dopo pochi minuti è possibile eseguire hello ricerca nei log seguenti:

* Linux - `Type=Heartbeat OSType=Linux | top 500000 | dedup SourceComputerId | Sort Computer | display Table`.  

* Windows - `Type=Heartbeat OSType=Windows | top 500000 | dedup SourceComputerId | Sort Computer | display Table`

In un computer Windows, è possibile esaminare hello tooverify connettività dell'agente con OMS seguenti:

1.  Aprire Microsoft Monitoring Agent nel Pannello di controllo, scegliere hello **Analitica Log di Azure (OMS)** scheda, hello agent viene visualizzato un messaggio che informa: **toohello Microsoft connesso hello Microsoft Monitoring Agent Servizio Operations Management Suite**.   
2.  Aprire hello registro eventi di Windows, passare troppo**applicazioni e servizi di Logs\Operations** e cercare 3000 ID evento e 5002 dall'origine connettore del servizio.  Questi eventi indicano computer hello è registrato con l'area di lavoro OMS hello e ricezione di configurazione.  

Se l'agente hello non è in grado di toocommunicate con hello servizio OMS ed è configurato toocommunicate con hello internet tramite un server proxy o firewall, verificare hello firewall o server proxy sia configurato correttamente, è consigliabile consultare [rete configurazione per l'agente di Windows](../log-analytics/log-analytics-windows-agents.md#network) o [configurazione di rete per l'agente Linux](../log-analytics/log-analytics-agent-linux.md#network).

> [!NOTE]
> Se i sistemi Linux toocommunicate configurato con un proxy o Gateway di OMS, l'onboarding di questa soluzione, eseguire l'aggiornamento hello *proxy.conf* omiuser gruppo di autorizzazioni toogrant hello autorizzazioni di lettura per il file hello eseguendo esecuzione di hello seguenti comandi:  
> `sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf`  
> `sudo chmod 644 /etc/opt/microsoft/omsagent/proxy.conf`


Gli agenti Linux appena aggiunti visualizzeranno lo stato **Aggiornato** dopo l'esecuzione di una valutazione.  Questo processo può richiedere ore too6.

gruppo di gestione comunica con OMS, vedere Operations Manager tooconfirm [convalidare di integrazione di Operations Manager con OMS](../log-analytics/log-analytics-om-agents.md#validate-operations-manager-integration-with-oms).

## <a name="data-collection"></a>Raccolta dei dati
### <a name="supported-agents"></a>Agenti supportati
Hello nella tabella seguente descrive hello connesso origini supportate da questa soluzione.

| Origine connessa | Supportato | Descrizione |
| --- | --- | --- |
| Agenti di Windows |Sì |soluzione Hello raccoglie informazioni sugli aggiornamenti del sistema dagli agenti di Windows e avvia l'installazione degli aggiornamenti richiesti. |
| Agenti Linux |Sì |soluzione Hello raccoglie informazioni sugli aggiornamenti del sistema dagli agenti Linux e avvia l'installazione degli aggiornamenti richiesti in distribuzioni supportate. |
| Gruppo di gestione di Operations Manager |Sì |soluzione Hello raccoglie informazioni sugli aggiornamenti del sistema di agenti in un gruppo di gestione connesso.<br>Una connessione diretta da tooLog agente di Operations Manager hello Analitica non è necessaria. Dati viene inoltrati dal repository OMS toohello di hello gestione gruppo. |
| Account di archiviazione di Azure |No |Archiviazione di Azure non include informazioni sugli aggiornamenti del sistema. |

### <a name="collection-frequency"></a>Frequenza della raccolta
Per ogni computer Windows gestito viene eseguita un'analisi due volte al giorno. Hello ogni 15 minuti Windows viene chiamata API tooquery per hello ultimo aggiornamento ora toodetermine se è stato modificato lo stato e in tal caso viene avviata un'analisi di conformità.  Per ogni computer Linux gestito viene eseguita un'analisi ogni 3 ore.

È possibile richiedere da 30 minuti too6 ore per i dati aggiornati toodisplay dashboard hello dai computer gestiti.   

## <a name="using-hello-solution"></a>Utilizzo di soluzione hello
Quando si aggiunge l'area di lavoro OMS hello gestione aggiornamenti soluzione tooyour, hello **gestione aggiornamenti** riquadro verrà aggiunto il dashboard OMS tooyour. Questo riquadro Visualizza un numero e la rappresentazione grafica del numero di hello del computer nel proprio ambiente e la conformità di aggiornamento.<br><br>
![Riquadro di riepilogo di Gestione aggiornamenti](media/oms-solution-update-management/update-management-summary-tile.png)  


## <a name="viewing-update-assessments"></a>Visualizzazione della valutazione degli aggiornamenti
Fare clic su hello **gestione aggiornamenti** riquadro tooopen hello **gestione aggiornamenti** dashboard.<br><br> ![Dashboard di riepilogo di Gestione aggiornamenti](./media/oms-solution-update-management/update-management-dashboard.png)<br>

Questo dashboard offre una descrizione dettagliata dello stato di aggiornamento in base al tipo di sistema operativo e alla classificazione dell'aggiornamento, ovvero critico, di sicurezza o altro, ad esempio un aggiornamento delle definizioni. risultati di Hello in ogni sezione in questo dashboard riflettono solo gli aggiornamenti approvati per la distribuzione, che si basa basata sull'origine di sincronizzazione di computer hello.   Hello **le distribuzioni di aggiornamenti** riquadro selezionato, si viene reindirizzati toohello pagina di distribuzioni di aggiornamenti in cui è possibile visualizzare le pianificazioni, le distribuzioni in esecuzione, le distribuzioni completate, o pianificare una nuova distribuzione.  

È possibile eseguire una ricerca di log che restituisce tutti i record facendo clic sul riquadro specifico hello o toorun una query di una determinata categoria e i criteri predefiniti, selezionarne uno dall'elenco di hello disponibile in hello **query comuni di aggiornamento** colonna.    

## <a name="installing-updates"></a>Installazione degli aggiornamenti
Dopo gli aggiornamenti sono stati valutati per tutti i computer Windows nell'area di lavoro e di hello Linux, è possibile avere gli aggiornamenti richiesti installati mediante la creazione di un *distribuzione degli aggiornamenti*.  Una distribuzione degli aggiornamenti è un'installazione pianificata di aggiornamenti necessari per uno o più computer.  Specificare hello data e ora non è per la distribuzione di hello inoltre tooa computer o gruppo di computer che devono essere incluse nell'ambito di hello di una distribuzione.  toolearn altre informazioni sui gruppi di computer, vedere [gruppi di Computer in Log Analitica](../log-analytics/log-analytics-computer-groups.md).  Quando si includono gruppi di computer nella distribuzione di aggiornamento, memnbership gruppo viene valutata una sola volta al momento di hello della creazione di pianificazione.  Non vengono applicate le modifiche successive tooa gruppo.  toowork il problema, eliminare la distribuzione di aggiornamenti pianificato hello e ricrearlo.

> [!NOTE]
> Macchine virtuali di Windows distribuite da hello Azure Marketplace per impostazione predefinita sono impostati gli aggiornamenti automatici tooreceive di servizio Windows Update.  Questo comportamento rimane invariato dopo l'aggiunta di questa soluzione o l'area di lavoro tooyour macchine virtuali di Windows.  In caso contrario, gli aggiornamenti non è attivamente gestiti con questa soluzione hello comportamento predefinito (applicare automaticamente gli aggiornamenti) verrà applicata.  

Per le macchine virtuali create da hello su richiesta Red Hat Enterprise Linux (RHEL) le immagini disponibili in Azure Marketplace, sono registrati tooaccess hello [Red Hat aggiornamento dell'infrastruttura (RHUI)](../virtual-machines/virtual-machines-linux-update-infrastructure-redhat.md) distribuito in Azure.  Distribuzioni Linux devono essere aggiornato dall'archivio di file online distribuzioni hello seguendo i metodi supportati.  

### <a name="viewing-update-deployments"></a>Visualizzazione delle distribuzioni degli aggiornamenti
Fare clic su hello **distribuzione degli aggiornamenti** riquadro tooview hello elenco esistente delle distribuzioni degli aggiornamenti.  Le distribuzioni sono raggruppate per stato, ovvero **Pianificato**, **In esecuzione** e **Completato**.<br><br> ![Pagina di pianificazione delle distribuzioni degli aggiornamenti](./media/oms-solution-update-management/update-updatedeployment-schedule-page.png)<br>  

in hello nella tabella seguente sono descritte le proprietà di Hello visualizzate per ogni distribuzione degli aggiornamenti.

| Proprietà | Descrizione |
| --- | --- |
| Nome |Nome della distribuzione degli aggiornamenti di hello. |
| Pianificazione |Tipo di pianificazione.  Le opzioni disponibili sono *Una sola volta*, *Ricorrenza settimanale* o *Ricorrenza mensile*. |
| Ora di inizio |Data e ora che hello distribuzione degli aggiornamenti è toostart pianificato. |
| Duration |Numero di minuti hello distribuzione degli aggiornamenti è consentito toorun.  Se tutti gli aggiornamenti non sono installati entro questo periodo di tempo, quindi hello rimanenti aggiornamenti è necessario attendere hello distribuzione dell'aggiornamento successivo. |
| Server |Numero di computer interessati da hello distribuzione degli aggiornamenti.  |
| Stato |Stato corrente di hello distribuzione degli aggiornamenti.<br><br>I valori possibili sono:<br>- Non avviato<br>- In esecuzione<br>- Operazione terminata |

Selezionare una distribuzione degli aggiornamenti tooview hello dettaglio schermata che include le colonne di hello hello nella tabella seguente.  Queste colonne verranno non essere popolate se hello distribuzione degli aggiornamenti non sono ancora state avviate.<br><br> ![Panoramica dei risultati della distribuzione degli aggiornamenti](./media/oms-solution-update-management/update-management-deploymentresults-dashboard.png)

| Colonna | Descrizione |
| --- | --- |
| **Vista Computer** | |
| Computer Windows |Elenca il numero di hello di computer Windows hello distribuzione degli aggiornamenti in base allo stato.  Fare clic su un toorun lo stato di restituzione di che tutti i record di aggiornamento con lo stato per hello Update Deployment una ricerca di log. |
| Computer Linux |Elenca il numero di hello di computer Linux in hello distribuzione degli aggiornamenti in base allo stato.  Fare clic su un toorun lo stato di restituzione di che tutti i record di aggiornamento con lo stato per hello Update Deployment una ricerca di log. |
| Stato di installazione del computer |Elenca i computer hello coinvolti nella distribuzione degli aggiornamenti hello e la percentuale di hello degli aggiornamenti che hanno installato correttamente. Fare clic su uno dei hello voci toorun una ricerca nei log la restituzione di tutti gli aggiornamenti mancanti e critici. |
| **Vista Aggiornamenti** | |
| Aggiornamenti di Windows |Elenca gli aggiornamenti di Windows inclusi in Update Deployment hello e il relativo stato di installazione per ogni aggiornamento.  Selezionare un aggiornamento toorun una ricerca dei registri di restituzione di tutte aggiornare i record per tale aggiornamento specifico o fare clic su hello stato toorun una ricerca dei registri di restituzione di che tutti i record per la distribuzione di hello di aggiornamento. |
| Aggiornamenti Linux |Elenca gli aggiornamenti di Linux inclusi in Update Deployment hello e il relativo stato di installazione per ogni aggiornamento.  Selezionare un aggiornamento toorun una ricerca dei registri di restituzione di tutte aggiornare i record per tale aggiornamento specifico o fare clic su hello stato toorun una ricerca dei registri di restituzione di che tutti i record per la distribuzione di hello di aggiornamento. |

### <a name="creating-an-update-deployment"></a>Creazione di una distribuzione degli aggiornamenti
Creare una nuova distribuzione di aggiornamento, fare clic su hello **Aggiungi** pulsante nella parte superiore di hello di hello tooopen schermata di hello **nuova distribuzione di aggiornamento** pagina.  È necessario fornire valori per le proprietà di hello in hello nella tabella seguente.

| Proprietà | Descrizione |
| --- | --- |
| Nome |Distribuzione degli aggiornamenti hello tooidentify nome univoco. |
| Fuso orario |Toouse fuso orario per l'ora di inizio hello. |
| Tipo di pianificazione | Tipo di pianificazione.  Le opzioni disponibili sono *Una sola volta*, *Ricorrenza settimanale* o *Ricorrenza mensile*.  
| Ora di inizio |Data e ora toostart hello distribuzione degli aggiornamenti. **Nota:** hello prima di eseguita una distribuzione è 30 minuti dall'ora corrente, se è necessario toodeploy immediatamente. |
| Duration |Numero di minuti hello distribuzione degli aggiornamenti è consentito toorun.  Se tutti gli aggiornamenti non sono installati entro questo periodo di tempo, quindi hello rimanenti aggiornamenti è necessario attendere hello distribuzione dell'aggiornamento successivo. |
| Computer |Nomi di computer o tooinclude di gruppi di computer e di destinazione in hello distribuzione degli aggiornamenti.  Selezionare una o più voci dall'elenco a discesa hello. |

<br><br> ![Pagina Nuova distribuzione aggiornamenti](./media/oms-solution-update-management/update-newupdaterun-page.png)

### <a name="time-range"></a>Intervallo di tempo
Per impostazione predefinita, l'ambito di hello di dati hello analizzati in hello soluzione di gestione degli aggiornamenti è da tutti i gruppi di gestione connessi generati all'interno di hello ultimo giorno.

intervallo di tempo hello toochange dei dati di hello, selezionare **i dati basati su** nella parte superiore di hello del dashboard hello. È possibile selezionare i record creata o aggiornata all'interno di hello ultimi 7 giorni, 1 giorno o 6 ore. In alternativa, è possibile selezionare **Personalizzato** e specificare un intervallo di date personalizzato.

## <a name="log-analytics-records"></a>Record di Log Analytics
soluzione di gestione degli aggiornamenti Hello crea due tipi di record nel repository OMS hello.

### <a name="update-records"></a>Record di aggiornamento
Viene creato un record di tipo **Aggiornamento** per ogni aggiornamento installato o necessario in ogni computer. Aggiornare i record dispongono di proprietà di hello in hello nella tabella seguente.

| Proprietà | Descrizione |
| --- | --- |
| Tipo |*Aggiornamento* |
| SourceSystem |origine Hello approvati installazione dell'aggiornamento hello.<br>I valori possibili sono:<br>- Microsoft Update<br>- Windows Update<br>- SCCM<br>- Server Linux recuperati da Gestione pacchetti |
| Approved |Specifica se l'aggiornamento di hello è stata approvata per l'installazione.<br> Per i server Linux è attualmente facoltativo perché l'applicazione di patch non è gestita da OMS. |
| Classificazione per Windows |Classificazione dell'aggiornamento hello.<br>I valori possibili sono:<br>- Applicazioni<br>- Aggiornamenti critici<br>- Aggiornamenti della definizione<br>- Feature Pack<br>- Aggiornamenti della sicurezza<br>- Service Pack<br>- Aggiornamenti cumulativi<br>- Aggiornamenti |
| Classificazione per Linux |Cassification dell'aggiornamento hello.<br>I valori possibili sono:<br>- Aggiornamenti critici<br>- Aggiornamenti della sicurezza<br>- Altri aggiornamenti |
| Computer |Nome del computer hello. |
| InstallTimeAvailable |Specifica se il tempo di installazione di hello è disponibile da altri agenti installati hello stesso aggiornamento. |
| InstallTimePredictionSeconds |Tempo previsto di installazione in secondi in base a altri agenti installati hello stesso aggiornamento. |
| KBID |ID dell'articolo hello KB che descrive l'aggiornamento di hello. |
| ManagementGroupName |Nome del gruppo di gestione di hello per gli agenti SCOM.  Per gli altri agenti corrisponde a AOI-<workspace ID>. |
| MSRCBulletinID |ID del bollettino Microsoft sulla hello descrizione aggiornamento hello. |
| MSRCSeverity |Gravità del bollettino Microsoft sulla sicurezza hello.<br>I valori possibili sono:<br>- Critico<br>- Importante<br>- Moderato |
| Facoltativo |Specifica se l'aggiornamento di hello è facoltativa. |
| Prodotto |Nome dell'aggiornamento hello hello è per.  Fare clic su **vista** articolo hello tooopen in un browser. |
| PackageSeverity |gravità Hello della vulnerabilità hello risolti in questo aggiornamento, come riportato da fornitori di distribuzione di Linux hello. |
| PublishDate |Data e ora di hello aggiornamento è stato installato. |
| RebootBehavior |Specifica se l'aggiornamento di hello impone un riavvio.<br>I valori possibili sono:<br>- canrequestreboot<br>- neverreboots |
| RevisionNumber |Numero di revisione dell'aggiornamento hello. |
| SourceComputerId |GUID toouniquely identificare computer hello. |
| TimeGenerated |Data e ora di hello record dell'ultimo aggiornamento. |
| Titolo |Titolo dell'aggiornamento hello. |
| UpdateID |GUID toouniquely identificare aggiornamento hello. |
| UpdateState |Specifica se l'aggiornamento di hello è installato nel computer.<br>I valori possibili sono:<br>-- Aggiornamento hello è installato nel computer.<br>-Necessari - hello aggiornamento non è installato è necessario in questo computer |

Quando si eseguono tutte le ricerche log che restituisce i record con un tipo di **aggiornamento** è possibile selezionare hello **aggiornamenti** visualizzazione che consente di visualizzare un set di sezioni di riepilogo degli aggiornamenti di hello restituiti dalla ricerca hello. È possibile fare clic sulle voci hello hello **mancanti e gli aggiornamenti applicati** e **gli aggiornamenti obbligatori e facoltativi** tooscope hello vista toothat più aggiornamenti di riquadri. Seleziona hello **elenco** o **tabella** visualizzare tooreturn hello singoli record.<br>

![Visualizzazione degli aggiornamenti con ricerca log per record di tipo Aggiornamento](./media/oms-solution-update-management/update-la-view-updates.png)  

In hello **tabella** vista, è possibile fare clic su hello **KBID** per qualsiasi record tooopen un browser con articolo hello KB. In questo modo si tooquickly leggere informazioni sui dettagli di hello di aggiornamento particolare hello.<br>

![Visualizzazione tabella con ricerca log per record di tipo Aggiornamento](./media/oms-solution-update-management/update-la-view-table.png)

In hello **elenco** vista, si fa clic su hello **vista** articolo tooopen KBID di collegamento successivo toohello hello KB.<br>

![Visualizzazione elenco con ricerca log per record di tipo Aggiornamento](./media/oms-solution-update-management/update-la-view-list.png)

### <a name="updatesummary-records"></a>UpdateSummary records
Viene creato un record di tipo **UpdateSummary** per ogni computer agente Windows. Questo record viene aggiornato ogni volta che viene analizzato il computer di hello per gli aggiornamenti. **UpdateSummary** record hanno proprietà hello in hello nella tabella seguente.

| Proprietà | Descrizione |
| --- | --- |
| Tipo |UpdateSummary |
| SourceSystem |OpsManager |
| Computer |Nome del computer hello. |
| CriticalUpdatesMissing |Numero di aggiornamenti critici mancanti nel computer di hello. |
| ManagementGroupName |Nome del gruppo di gestione di hello per gli agenti SCOM. Per gli altri agenti corrisponde a AOI-<workspace ID>. |
| NETRuntimeVersion |Versione di hello .NET runtime installato nel computer di hello. |
| OldestMissingSecurityUpdateBucket |Bucket toocategorize ora hello poiché hello meno recente mancante aggiornamento della sicurezza in questo computer è stato pubblicato.<br>I valori possibili sono:<br>- Meno recente<br>- 180 giorni fa<br>- 150 giorni fa<br>- 120 giorni fa<br>- 90 giorni fa<br>- 60 giorni fa<br>- 30 giorni fa<br>- Recente |
| OldestMissingSecurityUpdateInDays |Numero di giorni dopo la pubblicazione hello meno recente sicurezza aggiornamento mancante nel computer. |
| OsVersion |Versione del sistema operativo hello hello installato. |
| OtherUpdatesMissing |Numero di altri aggiornamenti mancanti nel computer di hello. |
| SecurityUpdatesMissing |Numero di aggiornamenti della sicurezza mancanti nel computer di hello. |
| SourceComputerId |GUID toouniquely identificare computer hello. |
| TimeGenerated |Data e ora di hello record dell'ultimo aggiornamento. |
| TotalUpdatesMissing |Numero totale di aggiornamenti mancanti nel computer di hello. |
| WindowsUpdateAgentVersion |Numero di versione dell'agente Windows Update hello computer hello. |
| WindowsUpdateSetting |Impostazione per il computer hello installerà gli aggiornamenti importanti.<br>I valori possibili sono:<br>- Disabilitato<br>- Notifica prima dell'installazione<br>- Installazione pianificata |
| WSUSServer |Server di URL di WSUS se hello computer è configurato toouse uno. |

## <a name="sample-log-searches"></a>Ricerche di log di esempio
Hello nella tabella seguente fornisce le ricerche log di esempio per aggiornare i record raccolti da questa soluzione.

| Query | Descrizione |
| --- | --- |
| Type:Update OSType!=Linux UpdateState=Needed Optional=false Approved!=false &#124; measure count() by Computer |Computer server basati su Windows che richiedono aggiornamenti |
| Type:Update OSType=Linux UpdateState!="Not needed" &#124; measure count() by Computer |Server Linux che richiedono aggiornamenti | 
| Type=Update UpdateState=Needed Optional=false &#124; select Computer,Title,KBID,Classification,UpdateSeverity,PublishedDate |Tutti i computer con aggiornamenti mancanti |
| Type=Update UpdateState=Needed Optional=false Computer="COMPUTER01.contoso.com" &#124; select Computer,Title,KBID,Product,UpdateSeverity,PublishedDate |Aggiornamenti mancanti per un computer specifico. Sostituire il valore con il nome computer.|
| Type=Update UpdateState=Needed Optional=false (Classification="Security Updates" OR Classification="Critical Updates") |Tutti i computer con aggiornamenti critici o della sicurezza mancanti | 
| Type=Update UpdateState=Needed Optional=false (Classification="Security Updates" OR Classification="Critical Updates") Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual &#124; Distinct Computer} &#124; Distinct KBID |Aggiornamenti critici o della sicurezza necessari nei computer in cui gli aggiornamenti vengono applicati manualmente |
| Type=Event EventLevelName=error Computer IN {Type=Update (Classification="Security Updates" OR Classification="Critical Updates") UpdateState=Needed Optional=false &#124; Distinct Computer} |Eventi di errore per computer con aggiornamenti critici o della sicurezza necessari mancanti |
| Type=Update Optional=false Classification="Update Rollups" UpdateState=Needed &#124; select Computer,Title,KBID,Classification,UpdateSeverity,PublishedDate |Tutti i computer con aggiornamenti cumulativi mancanti | 
| Type=Update UpdateState=Needed Optional=false &#124; Distinct Title |Aggiornamenti distinti mancanti tra tutti i computer | 
| Type:UpdateRunProgress InstallationStatus=failed &#124; measure count() by Computer, Title, UpdateRunName |Computer server basati su Windows con aggiornamenti non riusciti in un'operazione di aggiornamento | 
| Type:UpdateRunProgress InstallationStatus=failed &#124; measure count() by Computer, Product, UpdateRunName |Server Linux con aggiornamenti non riusciti in un'operazione di aggiornamento | 
| Type=UpdateSummary &#124; measure count() by WSUSServer |Appartenenza computer WSUS | 
| Type=UpdateSummary &#124; measure count() by WindowsUpdateSetting |Configurazione dell'aggiornamento automatico | 
| Type=UpdateSummary WindowsUpdateSetting=Manual |Computer con aggiornamento automatico disabilitato | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" &#124; measure count() by Computer |Elenco di tutti i computer Linux hello che è disponibile un aggiornamento di pacchetto | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" and (Classification="Critical Updates" OR Classification="Security Updates") &#124; measure count() by Computer |Elenco di tutti i computer Linux hello che è disponibile un aggiornamento di pacchetto che risolve la vulnerabilità critici o della sicurezza | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" |Elenco di tutti i pacchetti con un aggiornamento disponibile | 
| Type=Update  and OSType=Linux and UpdateState!="Not needed" and (Classification="Critical Updates" OR Classification="Security Updates") |Elenco di tutti i pacchetti con un aggiornamento critico o della sicurezza disponibile | 
| Type:UpdateRunProgress &#124; measure Count() by UpdateRunName |Elencare quali distribuzioni degli aggiornamenti hanno modificato i computer | 
| Type:UpdateRunProgress UpdateRunName="DeploymentName" &#124; measure Count() by Computer |Computer che sono stati aggiornati in questa operazione di aggiornamento. Sostituire il valore con il nome della distribuzione degli aggiornamenti | 
| Type=Update and OSType=Linux and OSName = Ubuntu &#124; measure count() by Computer |Elenco di tutte le macchine "Ubuntu" hello con gli aggiornamenti disponibili | 

## <a name="troubleshooting"></a>Risoluzione dei problemi

In questa sezione fornisce informazioni toohelp di risolvere i problemi con hello soluzione di gestione degli aggiornamenti.  

### <a name="how-do-i-troubleshoot-onboarding-issues"></a>Risoluzione dei problemi di onboarding
Se si verificano problemi durante il tentativo di soluzione hello tooonboard o una macchina virtuale, controllare hello **applicazioni e servizi di Logs\Operations** registro eventi per gli eventi con ID 4502 ed eventi messaggio contenente **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**.  Hello nella tabella seguente illustra i messaggi di errore specifico e una possibile risoluzione per ogni.  

| Message | Motivo | Soluzione |   
|----------|----------|----------|  
| Non è possibile tooRegister macchina per la gestione delle Patch,<br>Registration Failed with Exception<br>System.InvalidOperationException: {"Message":"Machine is already<br>tooa registrati account diverso. "} | Computer è già caricate tooanother dell'area di lavoro per la gestione degli aggiornamenti | Eseguire la pulizia degli elementi precedenti da [eliminazione gruppo di runbook hello ibridi](../automation/automation-hybrid-runbook-worker.md#remove-hybrid-worker-groups)|  
| Impossibile registrare troppo macchina per la gestione delle Patch,<br>Registration Failed with Exception<br>System.Net.Http.HttpRequestException: Si è verificato un errore durante l'invio della richiesta di hello. ---><br>System.NET. WebException: connessione sottostante hello<br>was closed: An unexpected error<br>occurred on a receive. ---> System.ComponentModel.Win32Exception:<br>non è possibile comunicare hello client e server,<br>because they do not possess a common algorithm | Proxy/Gateway/Firewall che blocca la comunicazione | [Esaminare i requisiti di rete](../automation/automation-offering-get-started.md#network-planning)|  
| Non è possibile tooRegister macchina per la gestione delle Patch,<br>Registration Failed with Exception<br>Newtonsoft.Json.JsonReaderException: Error parsing positive infinity value. | Proxy/Gateway/Firewall che blocca la comunicazione | [Esaminare i requisiti di rete](../automation/automation-offering-get-started.md#network-planning)| 
| certificato Hello presentato dal servizio hello <wsid>. c o m<br>was not issued by a certificate authority<br>used for Microsoft services. Please contact<br>l'amministratore di rete toosee se sono in esecuzione un proxy che intercetta<br>TLS/SSL communication. |Proxy/Gateway/Firewall che blocca la comunicazione | [Esaminare i requisiti di rete](../automation/automation-offering-get-started.md#network-planning)|  
| Non è possibile tooRegister macchina per la gestione delle Patch,<br>Registration Failed with Exception<br>AgentService.HybridRegistration.<br>PowerShell.Certificates.CertificateCreationException:<br>Non è stato possibile toocreate un certificato autofirmato. ---><br>System.UnauthorizedAccessException: Access is denied. | Errore di generazione del certificato autofirmato | Verificare che l'account di sistema abbia<br>accesso in lettura toofolder:<br>**C:\ProgramData\Microsoft\**<br>**Crypto\RSA**|  

### <a name="how-do-i-troubleshoot-update-deployments"></a>Come si risolvono i problemi con le distribuzioni degli aggiornamenti?
È possibile visualizzare i risultati di hello di runbook hello responsabile per la distribuzione degli aggiornamenti di hello inclusi nella distribuzione di aggiornamento pianificato hello dal pannello processi hello dell'account di automazione che è collegato con area di lavoro OMS hello supportano questa soluzione.  Hello runbook **Patch MicrosoftOMSComputer** è un runbook figlio che è destinato a un computer gestito specifico e l'analisi di flusso dettagliato hello offrirà informazioni dettagliate per la distribuzione.  output di Hello verrà visualizzato che richiedevano gli aggiornamenti sono applicabili, scaricare lo stato, lo stato di installazione e altri dettagli.<br><br> ![Stato del processo di distribuzione degli aggiornamenti](media/oms-solution-update-management/update-la-patchrunbook-outputstream.png)<br>

Per altre informazioni, vedere [Output e messaggi dei runbook in Automazione di Azure](../automation/automation-runbook-output-and-messages.md).   

## <a name="next-steps"></a>Passaggi successivi
* Usare le ricerche Log in [Log Analitica](../log-analytics/log-analytics-log-searches.md) tooview in dettaglio i dati di aggiornamento.
* [Creare dashboard personalizzati](../log-analytics/log-analytics-dashboards.md) che indicano la conformità degli aggiornamenti per i computer gestiti.
* [Creare avvisi](../log-analytics/log-analytics-alerts.md) quando aggiornamenti critici vengono rilevati come mancanti nei computer oppure quando gli aggiornamenti automatici sono disabilitati per un computer.  
