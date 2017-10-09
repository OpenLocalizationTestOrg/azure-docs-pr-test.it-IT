---
title: soluzioni di gestione di Azure Log Analitica aaaAdd | Documenti Microsoft
description: Le soluzioni di gestione di Operations Management Suite (OMS)/Log Analytics sono una raccolta di regole per la logica, la visualizzazione e l'acquisizione dei dati che forniscono le metriche specifiche per una particolare area problematica.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f029dd6d-58ae-42c5-ad27-e6cc92352b3b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5a232d20e144b800387b09adb5248505d801944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-log-analytics-management-solutions-tooyour-workspace"></a>Aggiungere l'area di lavoro di Azure Log Analitica Gestione soluzioni tooyour

Le soluzioni di gestione di Log Analytics sono una raccolta di regole per la **logica**, la **visualizzazione** e l'**acquisizione dei dati** che forniscono le metriche specifiche per una particolare area problematica. In questo articolo sono elencate le soluzioni di gestione supportate da Analitica di Log e Mostra come tooadd e remove per un'area di lavoro utilizzando hello portale di Azure. È anche possibile aggiungere soluzioni nel portale OMS hello usando la raccolta di soluzioni hello.

Le soluzioni di gestione consentono di ottenere informazioni più approfondite per:

* Individuare e risolvere i problemi operativi più rapidamente
* Raccogliere e correlare diversi tipi di dati del computer
* Migliorare la proattività grazie ad attività che espone la soluzione hello.

> [!NOTE]
> Log Analitica include funzionalità di ricerca nei Log, pertanto non è necessario tooinstall un tooenable soluzione di gestione è. Invece, si ottiene visualizzazioni dei dati, ricerche suggerite e approfondimenti aggiungendo area tooyour soluzioni di gestione.

In questo articolo è utilizzare per aggiungere Gestione soluzioni tooa dell'area di lavoro tramite il portale di Azure Marketplace hello. Dopo aver aggiunto una soluzione, i dati vengono raccolti dai server hello nell'infrastruttura e inviati servizio OMS toohello. Elaborazione per hello servizio OMS richiede in genere l'ora di tooan pochi minuti. Dopo che il servizio di hello elaborato dati hello, è possibile visualizzarli in OMS.

Le soluzioni di gestione non più necessarie possono essere rimosse facilmente. Quando si rimuove una soluzione di gestione, i dati non vengono inviati tooOMS. Se si utilizza hello a livello di prezzo gratuito, la rimozione di una soluzione può ridurre hello di dati utilizzato, consentono di superare la quota giornaliera di dati.

## <a name="view-available-management-solutions"></a>Visualizzare le soluzioni di gestione disponibili

Azure marketplace Hello contiene elenco hello di [soluzioni di gestione per Log Analitica](https://azuremarketplace.microsoft.com/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).

È possibile installare le soluzioni di gestione da Azure marketplace facendo hello **Scarica adesso** collegamento nella parte inferiore di hello di ciascuna soluzione.

## <a name="add-a-management-solution"></a>Aggiungere una soluzione di gestione
1. Se non già stato fatto, accedere toohello [portale di Azure](https://portal.azure.com) tramite la sottoscrizione di Azure.
2. In hello **New** pannello **Marketplace**selezionare **monitoraggio + gestione**.
3. In hello **monitoraggio + gestione** pannello, fare clic su **tutti**.  
    Pannello ![Monitoraggio e gestione](./media/log-analytics-add-solutions/monitoring-management-blade.png)  
4. toohello destra **soluzioni di gestione**, fare clic su **più**.
5. In hello **soluzioni di gestione** pannello, selezionare una soluzione di gestione che si desidera tooadd tooa area di lavoro.  
    Pannello ![Monitoraggio e gestione](./media/log-analytics-add-solutions/management-solutions.png)  
6. Nel Pannello di soluzione di gestione di hello, esaminare le informazioni sulla soluzione di gestione di hello e quindi fare clic su **crea**.
7. In hello *Nome soluzione di gestione* pannello, selezionare un'area di lavoro che si desidera tooassociate con la soluzione di gestione hello.
8. Facoltativamente, modificare le impostazioni dell'area per sottoscrizione Azure hello, gruppo di risorse e il percorso. È anche possibile scegliere **Opzioni di automazione**. Fare clic su **Crea**.  
    ![area di lavoro della soluzione](./media/log-analytics-add-solutions/solution-workspace.png)  
9. toostart utilizzando una soluzione di gestione di hello aggiunti tooyour dell'area di lavoro, passare troppo**Log Analitica** > **sottoscrizioni** > ***nome area di lavoro ***  >  **Panoramica**. Verrà visualizzato un nuovo riquadro per la soluzione di gestione. Fare clic su tooopen riquadro hello e iniziare a utilizzare la soluzione hello dopo aver raccolto i dati per la soluzione hello.

## <a name="remove-a-management-solution"></a>Rimuovere una soluzione di gestione

1. In hello [portale di Azure](https://portal.azure.com), passare troppo**Log Analitica** > **sottoscrizioni** > ***nome area di lavoro*** e quindi in hello ***nome area di lavoro*** pannello, fare clic su **soluzioni**.
2. Nell'elenco di hello di soluzioni di gestione, selezionare soluzione hello che si desidera tooremove.
3. Nel Pannello di soluzione hello dell'area di lavoro, fare clic su **eliminare**.  
    ![elimina soluzione](./media/log-analytics-add-solutions/solution-delete.png)  
4. Nella finestra di dialogo Conferma hello, fare clic su **Sì**.

## <a name="offers-and-pricing-tiers"></a>Offerte e piani tariffari

Hello nella tabella seguente identifica le soluzioni di gestione appartengono tooeach offerta di Operations Management Suite.
tabella Hello identifica anche hello livelli disponibili per ogni soluzione di gestione di prezzo.
Tutte le soluzioni in hello nella tabella seguente sono disponibili dall'interno hello portale e hello soluzioni raccolta di Azure nel portale di hello Analitica di Log.

| Soluzione di gestione                                                                       | Offerta                                                                     | Piani tariffari<sup>1</sup>                                                 | Note |
| ---                                                                                       | ---                                                                       | ---                                                                                                       | ---   |
| [Activity Log Analytics](log-analytics-activity.md)                                                                   | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | Sono disponibili 90 giorni gratuiti di traffico dati<br>Dati di interesse non toohello estremità di livello gratuito |
| [Valutazione di AD](log-analytics-ad-assessment.md)                                           | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [Stato della replica di AD](log-analytics-ad-replication-status.md)                           | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | Non è disponibile tooadd dal portale di Azure/marketplace. |
| [Integrità agente](../operations-management-suite/oms-solution-agenthealth.md)                                                                                | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | Dati di interesse non toohello estremità di livello gratuito<br> Non è disponibile tooadd dal portale di Azure/marketplace. |
| [Gestione degli avvisi](log-analytics-solution-alert-management.md)                            | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | Non è disponibile tooadd dal portale di Azure/marketplace. |
| [Connettore di Application Insights (anteprima)](log-analytics-app-insights-connector.md)                                               | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [Ruolo di lavoro ibrido per runbook di Automazione](../automation/automation-hybrid-runbook-worker.md)                                                                     | <ul><li>Automation & Control</li></ul>                                  | Gratuito<br> Per&nbsp;nodo&nbsp;(OMS)                                                                         | Richiede il tooan toobe collegato dell'area di lavoro di Log Analitica account di automazione |
| [Analisi dei gateway applicazione di Azure](log-analytics-azure-networking-analytics.md)    | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [Analisi del gruppo di sicurezza di rete di Azure](log-analytics-azure-networking-analytics.md)     | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [Azure SQL Analytics (Anteprima)](log-analytics-azure-sql.md)                                                       | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br>Per&nbsp;nodo&nbsp;(OMS)                                                                          | Richiede il tooan toobe collegato dell'area di lavoro di Log Analitica account di automazione|
| [Analisi app Web di Azure](log-analytics-azure-web-apps-analytics.md)     | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
|[Backup](../backup/backup-introduction-to-azure-backup.md)                                                                                 | <ul><li>Insight & Analytics</li></ul>                                   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)                                                                       | È necessario un insieme di credenziali di backup classico.<br> Non è disponibile tooadd dal portale di Azure/marketplace. |
| [Capacità e prestazioni (anteprima)](log-analytics-capacity.md)                                                   | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [Rilevamento delle modifiche](log-analytics-change-tracking.md)                                       | <ul><li>Automation & Control</li></ul>                                  | Gratuito<br> Per&nbsp;nodo&nbsp;(OMS)                                                                         | Richiede il tooan toobe collegato dell'area di lavoro di Log Analitica account di automazione |
| [Contenitori](log-analytics-containers.md)                                                 | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [IT Service Management Connector (anteprima)](log-analytics-itsmc-overview.md)                                              | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Per&nbsp;nodo&nbsp;(OMS)     | |
| Monitoraggio per HDInsight HBase <br>(Anteprima)                                                  | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [Analisi dell'insieme di credenziali delle chiavi](log-analytics-azure-key-vault.md)                   | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [App per la logica B2B](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)                    | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | Non è disponibile tooadd dal portale di Azure/marketplace. |
| [Valutazione di malware](log-analytics-malware.md)                                            | <ul><li>Sicurezza e conformità</li></ul>                                 | Gratuito<br> Autonoma<br>Per&nbsp;nodo&nbsp;(OMS)                                                                           | Se si aggiungono le soluzioni di sicurezza e conformità hello dopo il 19 giugno 2017 [fatturazione è per ogni nodo](https://azure.microsoft.com/pricing/details/security-compliance/), indipendentemente dall'area di lavoro hello piano tariffario. Hello primi 60 giorni sono gratuiti.  |
| [Monitoraggio delle prestazioni di rete](log-analytics-network-performance-monitor.md) <br>  | <ul><li>Insight & Analytics</li></ul>                                   | Gratuito<br> Per&nbsp;nodo&nbsp;(OMS)                                                                         | |
| [Analisi Office 365 (anteprima)](../operations-management-suite/oms-solution-office-365.md)                                                       | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [Sicurezza e controllo](../operations-management-suite/oms-security-getting-started.md)      | <ul><li>Sicurezza &nbsp;e&nbsp;conformità</li></ul>                       | Gratuito<br> Autonoma<br>Per&nbsp;nodo&nbsp;(OMS)                                                                           | Questa soluzione è necessaria per la raccolta dei log eventi di sicurezza<br>Se si aggiungono le soluzioni di sicurezza e conformità hello dopo il 19 giugno 2017 [fatturazione è per ogni nodo](https://azure.microsoft.com/pricing/details/security-compliance/), indipendentemente dall'area di lavoro hello piano tariffario. Hello primi 60 giorni sono gratuiti. |
| [Service Fabric Analytics (anteprima)](log-analytics-service-fabric.md)                     | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [Mapping dei servizi (anteprima)](../operations-management-suite/operations-management-suite-service-map.md) | <ul><li>Insight & Analytics</li></ul>                      | Gratuito<br> Per&nbsp;nodo&nbsp;(OMS)                                                                         | Disponibile in Europa orientale, Europa occidentale e Stati Uniti centro-occidentali    |
| [Site Recovery](../site-recovery/site-recovery-overview.md)                                                                               | <ul><li>Insight & Analytics</li></ul>                                   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)                                                                       | Richiede un insieme di credenziali di ripristino sito classico.<br> Non è disponibile tooadd dal portale di Azure/marketplace. |
| [SQL Assessment](log-analytics-sql-assessment.md)                                         | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| Avviare/arrestare VM durante gli orari di minore attività<br>(Anteprima)                                              | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Per&nbsp;nodo&nbsp;(OMS)                                                                         | Richiede il tooan toobe collegato dell'area di lavoro di Log Analitica account di automazione |
| [SurfaceHub](log-analytics-surface-hubs.md)                                               | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | Non è disponibile tooadd dal portale di Azure/marketplace. |
| [Valutazione System Center Operations Manager (anteprima)](log-analytics-scom-assessment.md)  | <ul><li>Insight & Analytics</li><li>Log Analytics</li></ul>        | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [Gestione degli aggiornamenti](../operations-management-suite/oms-solution-update-management.md)                                                                         | <ul><li>Automation & Control</li></ul>                                  | Gratuito<br> Per&nbsp;nodo&nbsp;(OMS)                                                                         | Richiede il tooan toobe collegato dell'area di lavoro di Log Analitica account di automazione |
| [Conformità aggiornamenti (anteprima)](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started)                                                             | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | Non sono previsti addebiti per i dati o i nodi<br>Dati di interesse non toohello estremità di livello gratuito.<br> Non è disponibile tooadd dal portale di Azure/marketplace. |
| [Preparazione dell'aggiornamento](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started)                                                          | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | Non sono previsti addebiti per i dati o i nodi<br>Dati di interesse non toohello estremità di livello gratuito.<br> Non è disponibile tooadd dal portale di Azure/marketplace. |
| [Monitoraggio VMware (anteprima)](log-analytics-vmware.md)                                | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [Wire Data 2.0 (anteprima)](log-analytics-wire-data.md)                                                                 | <ul><li>Insight & Analytics</li></ul>                                   | Gratuito<br> Per&nbsp;nodo&nbsp;(OMS)                                                                         | Disponibile in Europa orientale, Europa occidentale e Stati Uniti centro-occidentali |

<sup>1</sup> hello *Standard* e *Premium (OMS)* piani tariffari disponibili solo per i clienti che ha creato i relativi Log Analitica dell'area di lavoro precedente tooSeptember 21, 2016.

### <a name="community-provided-management-solutions"></a>Soluzioni di gestione offerte dalla community

Sono disponibili da hello community fornite soluzioni [raccolta di modelli di Azure](https://azure.microsoft.com/resources/templates/?term=Per&nbsp;Node&nbsp;(OMS)) e diretto da autori hello.

| Soluzione di gestione               | Offerta                                                                     | Piani tariffari                         | Note |
| ---                               | ---                                                                       | ---                                   | ---   |
| Tutte le soluzioni offerte dalla community  | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Per&nbsp;nodo&nbsp;(OMS)     |   Richiede il tooan toobe collegato dell'area di lavoro di Log Analitica account di automazione |




## <a name="data-collection-details"></a>Informazioni dettagliate sulla raccolta di dati
Hello tabelle seguenti illustrano i metodi di raccolta dati e altri dettagli sulla modalità di raccolta dati per le origini di dati e le soluzioni gestione Analitica di Log. Hello tabelle vengono suddivise le offerte di soluzioni, equivalgono troppo[sottoscrizione ai livelli di prezzo](https://go.microsoft.com/fwlink/?linkid=827926). soluzione Analitica Log attività Hello è tooall disponibile gratuitamente i livelli di prezzo.

agente Log Analitica Windows Hello e System Center Operations Manager agent sono essenzialmente hello stesso. agente di Windows Hello include funzionalità aggiuntive tooallow è tooconnect toohello OMS workspace e route tramite un proxy. Se si utilizza un agente Operations Manager, deve essere indirizzato come un toocommunicate agente OMS con OMS. Agenti di Operations Manager in questa tabella sono gli agenti OMS connesso tooOperations Manager. Vedere [tooLog connettere Operations Manager Analitica](log-analytics-om-agents.md) per informazioni sulla connessione del tooOMS di ambiente esistente di Operations Manager.

> [!NOTE]
> tipo di Hello di agente in uso determina come i dati vengono inviati tooOMS, con hello seguenti condizioni:
> - Utilizzare dell'agente di Windows hello o un agente OMS associati a Operations Manager.
> - Quando Operations Manager è necessario, i dati dell'agente Operations Manager per la soluzione hello viene sempre inviati tooOMS utilizza hello gruppo di gestione di Operations Manager. Inoltre, quando Operations Manager è necessario, solo agente di Operations Manager di hello viene utilizzato dalla soluzione hello.
> - Quando Operations Manager non è obbligatorio e tabella hello mostra che i dati dell'agente Operations Manager vengono inviati tooOMS utilizzando il gruppo di gestione di hello, quindi i dati dell'agente Operations Manager viene sempre inviato tooOMS utilizzando i gruppi di gestione. Gli agenti Windows ignora il gruppo di gestione di hello e invia i dati direttamente tooOMS.
> - Quando i dati dell'agente Operations Manager non viene inviati tramite un gruppo di gestione, quindi hello dati vengono inviati direttamente tooOMS, ignorando il gruppo di gestione di hello.

### <a name="insight--analytics--log-analytics"></a>Insight & Analytics/Log Analytics

| Soluzione di gestione | Piattaforma | Microsoft Monitoring Agent | Agente di Operations Manager | Archiviazione di Azure | È necessario Operations Manager? | Dati dell'agente Operations Manager inviati con il gruppo di gestione | Frequenza della raccolta |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Activity Log Analytics | Azure |   |   |   |   |   | su notifica |
| AD Assessment |Windows |&#8226; |&#8226; |  |  |&#8226; |7 giorni |
| Stato della replica di AD |Windows |&#8226; |&#8226; |  |  |&#8226; |5 giorni |
| Integrità agente | Windows e Linux | &#8226; | &#8226; |   |   | &#8226; | 1 minuto |
| Alert Management (Nagios) |Linux |&#8226; |  |  |  |  |all'arrivo |
| Alert Management (Zabbix) |Linux |&#8226; |  |  |  |  |1 minuto |
| Gestione avvisi (Operations Manager) |Windows |  |&#8226; |  |&#8226; |&#8226; |3 minuti |
| Application Insights Connector (anteprima) | Azure |   |   |   |   |   | su notifica |
| Analisi dei gateway applicazione di Azure | Azure |   |   |   |   |   | su notifica |
| Analisi del gruppo di sicurezza di rete di Azure | Azure |   |   |   |   |   | su notifica |
| Azure SQL Analytics (Anteprima) |Windows |  |  |  |  |  | 10 minuti |
| Capacity Management |Windows |&#8226; |&#8226; |  |  |&#8226; |all'arrivo |
| Contenitori | Windows e Linux | &#8226; | &#8226; |   |   |   | 3 minuti |
| Analisi dell'insieme di credenziali delle chiavi |Windows |  |  |  |  |  |su notifica |
| Monitoraggio delle prestazioni di rete | Windows | &#8226; | &#8226; |   |   |   | TCP esegue handshake ogni 5 secondi e i dati vengono inviati ogni 3 minuti |
| Office 365 Analytics (anteprima) |Windows |  |  |  |  |  |su notifica |
| Service Fabric Analytics |Windows |  |  |&#8226; |  |  |5 minuti |
| Elenco dei servizi | Windows e Linux | &#8226; | &#8226; |   |   |   | 5 secondi |
| SQL Assessment |Windows |&#8226; |&#8226; |  |  |&#8226; |7 giorni |
| SurfaceHub |Windows |&#8226; |  |  |  |  |all'arrivo |
| System Center Operations Manager Assessment (anteprima) | Windows | &#8226; | &#8226; |   |   | &#8226; | 7 giorni |
| Upgrade Analytics (anteprima) | Windows | &#8226; |   |   |   |   | 2 giorni |
| VMware Monitoring (anteprima) | Linux | &#8226; |   |   |   |   | 3 minuti |
| Trasferimento dati |Windows (2012 R2 / 8.1 o versioni successive) |&#8226; |&#8226; |  |  |  | 1 minuto |


### <a name="automation--control"></a>Automation & Control

| Soluzione di gestione | Piattaforma | Microsoft Monitoring Agent | Agente di Operations Manager | Archiviazione di Azure | È necessario Operations Manager? | Dati dell'agente Operations Manager inviati con il gruppo di gestione | Frequenza della raccolta |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Ruolo di lavoro ibrido di Automazione | Windows | &#8226; | &#8226; |   |   |   | n/d |
| Change Tracking |Windows |&#8226; |&#8226; |  |  |&#8226; |ogni ora |
| Change Tracking |Linux |&#8226; |  |  |  |  |ogni ora |
| Gestione degli aggiornamenti | Windows |&#8226; |&#8226; |  |  |&#8226; |almeno 2 volte al giorno e 15 minuti dopo l'installazione di un aggiornamento |

### <a name="security--compliance"></a>Sicurezza e conformità

| Soluzione di gestione | Piattaforma | Microsoft Monitoring Agent | Agente di Operations Manager | Archiviazione di Azure | È necessario Operations Manager? | Dati dell'agente Operations Manager inviati con il gruppo di gestione | Frequenza della raccolta |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Antimalware Assessment |Windows |&#8226; |&#8226; |  |  |&#8226; |ogni ora |
| Security and Audit<sup>1</sup> | Windows e Linux | parziale | parziale | parziale |   | parziale | variabile |

<sup>1</sup> hello sicurezza e di soluzione di controllo può raccogliere log da agenti Operations Manager, di Windows e Linux. Vedere la tabella [Origini dati](#data-sources) per informazioni sulla raccolta dati relativa a:

- syslog
- Registri eventi della sicurezza di Windows
- Registri firewall di Windows
- Registri eventi di Windows



### <a name="protection--recovery"></a>Protezione e ripristino

| Soluzione di gestione | Piattaforma | Microsoft Monitoring Agent | Agente di Operations Manager | Archiviazione di Azure | È necessario Operations Manager? | Dati dell'agente Operations Manager inviati con il gruppo di gestione | Frequenza della raccolta |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Backup | Azure |   |   |   |   |   | n/d |
| Azure Site Recovery | Azure |   |   |   |   |   | n/d |


### <a name="data-sources"></a>Origini dati


| Origine dati | Piattaforma | Microsoft Monitoring Agent | Agente di Operations Manager | Archiviazione di Azure | È necessario Operations Manager? | Dati dell'agente Operations Manager inviati con il gruppo di gestione | Frequenza della raccolta |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Log di attività di Azure |Windows |  |  |  |  |  |su notifica |
| Log di diagnostica di Azure |Windows |  |  |  |  |  |su notifica |
| Metrica di diagnostica di Azure |Windows |  |  |  |  |  |su notifica |
| ETW |Windows |  |  |&#8226; |  |  |5 minuti |
| Log di IIS |Windows |&#8226; |&#8226; |&#8226; |  |  |5 minuti |
| Contatori delle prestazioni |Windows |&#8226; |&#8226; |  |  |  |come pianificato, almeno 10 secondi |
| Contatori delle prestazioni |Linux |&#8226; |  |  |  |  |come pianificato, almeno 10 secondi |
| syslog |Linux |&#8226; |  |  |  |  |dall'Archiviazione di Azure: 10 minuti; dall'agente: all'arrivo |
| Registri eventi della sicurezza di Windows |Windows |&#8226; |&#8226; |&#8226; |  |  |per l'archiviazione di Azure: 10 minuti; per l'agente di hello: all'arrivo |
| Registri firewall di Windows |Windows |&#8226; |&#8226; |  |  |  |all'arrivo |
| Registri eventi di Windows |Windows |&#8226; |&#8226; |&#8226; |  |&#8226; |per l'archiviazione di Azure: 10 minuti; per l'agente di hello: all'arrivo |



## <a name="preview-management-solutions-and-features"></a>Soluzioni di gestione e funzionalità in anteprima
Esecuzione di un servizio e seguendo devops consigliate, siamo in grado di toopartner con i clienti toodevelop funzionalità e soluzioni.

Durante l'anteprima privata, è fornire un piccolo gruppo di clienti accesso tooan implementazione anticipata del feedback toogain funzionalità o una soluzione di hello e apportare miglioramenti. Questa implementazione preliminare è dotata di funzionalità e capacità operative minime.

L'obiettivo è tootry operazioni rapidamente, pertanto è possibile trovare ciò che funziona e cosa non funziona. Abbiamo scorrere questo processo fino a quando i commenti e suggerimenti hello dai clienti anteprima privata hello è indicato che si è pronti per l'anteprima pubblica.

Durante l'anteprima pubblica di hello, è rendere funzionalità hello o soluzioni disponibili per tutti gli utenti tooget ulteriori commenti e suggerimenti e convalidare la scalabilità e l'efficienza. In questa fase:

* Le funzionalità di anteprima vengono visualizzati nella scheda Impostazioni hello e possono essere attivate da qualsiasi utente.
* Soluzioni di anteprima vengono aggiunti tramite la raccolta di hello o tramite uno script.

### <a name="what-should-i-know-about-preview-features-and-solutions"></a>Cosa occorre sapere sulle funzionalità e le soluzioni in anteprima
Siamo entusiasti sulle nuove funzionalità e le soluzioni di gestione e noi piace utilizzo si toodevelop li.

Le funzionalità e le soluzioni in anteprima non sono adatte a tutti. Prima di chiedere toojoin un'anteprima privata o l'abilitazione di un'anteprima pubblica, assicurarsi che OK si lavora con un elemento che è in fase di sviluppo.

Quando si abilita una funzionalità di anteprima tramite il portale di hello, viene visualizzato un avviso per ricordare che hello funzionalità è disponibile in anteprima.

#### <a name="for-both-private-and-public-preview"></a>Per l'anteprima sia *privata* che *pubblica*
Hello informazioni seguenti si applicano tooboth pubbliche e private Preview:

* Non sempre tutto potrebbe funzionare correttamente.
  * Rilascia l'intervallo di diventare un fastidio secondario tramite toosomething non funziona in tutti.
* È possibile inserire hello anteprima toohave un impatto negativo sui sistemi / ambiente.
  * Si tenta di aspetti negativi di tooavoid sistemi toohello problema che si sta utilizzando con OMS, ma in alcuni casi imprevisti operazioni si verificano.
* Può verificarsi la perdita o il danneggiamento dei dati.
* Potrebbe essere richiesto di log di diagnostica toocollect o toohelp altri dati, risoluzione dei problemi.
* funzionalità di Hello o una soluzione potrebbe venire rimosso (temporaneamente o definitivamente).
  * Basate su nostri informazioni durante l'anteprima di hello si potrebbe decidere funzionalità di hello toonot versione o una soluzione.
* Le anteprime potrebbero non funzionare o non essere testate con tutte le configurazioni e Microsoft potrebbe pertanto limitare:
  * Hello sistemi operativi che può essere utilizzati (ad esempio, una funzionalità solo valere tooLinux mentre è in anteprima).
  * Hello tipo di agente (MMA, Operations Manager) che può essere utilizzato (ad esempio, una funzionalità potrebbe non funzionare con Operations Manager in anteprima).  
* Funzionalità e soluzioni di anteprima non rientrano hello Service Level Agreement.
* L'utilizzo di funzionalità in anteprima dà luogo ad addebiti.
* Caratteristiche o funzionalità che è necessario per la funzionalità di hello o toobe soluzione utile potrebbe essere mancanti o incomplete.
* Alcune funzionalità/soluzioni potrebbero non essere disponibili in tutte le aree.
* Alcune funzionalità/soluzioni potrebbero non essere localizzate.
* Funzionalità / soluzioni possono presentare un limite sul numero di hello dei clienti o i dispositivi che è possono utilizzarlo.
* Potrebbe essere necessario toouse tooperform tooenable e configurazione hello soluzione/funzionalità script.
* interfaccia utente di Hello (UI) è completo e può variare da tooday giorno.
* Le anteprime pubbliche potrebbero non essere appropriate per sistemi di produzione o critici.

#### <a name="for-private-preview"></a>Per l’anteprima *privata*
Negli elementi toohello addizione precedenti, le seguenti informazioni hello è anteprime tooprivate specifico:

* Prevediamo tooprovide ci con commenti e suggerimenti sull'esperienza in modo da poter apportare hello funzionalità o la soluzione migliore.
* Potrebbe quindi chiedere agli utenti di fornire tali commenti e suggerimenti rispondendo a questionari, chiamate telefoniche o messaggi di posta elettronica.
* Non sempre tutto funziona correttamente.
* Potrebbe essere richiesta la sottoscrizione di un accordo di riservatezza per la partecipazione o potrebbe essere incluso contenuto riservato.
  * Prima di blogging, utilizzo di tweet o in caso contrario, la comunicazione con terze parti, verificare con hello Program Manager responsabile hello anteprima toounderstand eventuali restrizioni alla comunicazione.
* Non eseguire l'anteprima in sistemi di produzione o critici.

### <a name="how-do-i-get-access-tooprivate-preview-features-and-solutions"></a>Come ottenere le funzionalità di anteprima tooprivate di accesso e le soluzioni?
Microsoft invita anteprime tooprivate clienti attraverso diversi modi a seconda di anteprima di hello.

* Rispondendo indagine mensile hello e rinunciare ci toofollow autorizzazione con l'utente migliora le possibilità di essere invitati tooa anteprima privata.
* I partecipanti possono essere proposti dal team degli account Microsoft.
* È possibile effettuare l'iscrizione in base alle informazioni pubblicate sulla pagina Twitter [msopsmgmt](https://twitter.com/msopsmgmt).
* È possibile effettuare l'iscrizione in base alle informazioni condivise in occasione di eventi della community, come raduni, conferenze e community online.

## <a name="next-steps"></a>Passaggi successivi
* [Ricerca dei registri](log-analytics-log-searches.md) tooview informazioni raccolte da soluzioni di gestione.
