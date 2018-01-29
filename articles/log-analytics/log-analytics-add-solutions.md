---
title: Aggiungere soluzioni di gestione di Log Analytics di Azure| Microsoft Docs
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
ms.date: 01/23/2018
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d951387882a5a8f5e0ebdc01841bb8384e4848ee
ms.sourcegitcommit: 28178ca0364e498318e2630f51ba6158e4a09a89
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/24/2018
---
# <a name="add-azure-log-analytics-management-solutions-to-your-workspace"></a>Aggiungere soluzioni di gestione di Log Analytics di Azure all'area di lavoro

Le soluzioni di gestione di Log Analytics sono una raccolta di regole per la **logica**, la **visualizzazione** e l'**acquisizione dei dati** che forniscono le metriche specifiche per una particolare area problematica. Questo articolo contiene un elenco delle soluzioni di gestione supportate da Log Analytics e illustra come aggiungerle e rimuoverle da un'area di lavoro usando il portale di Azure. È anche possibile aggiungere soluzioni nel portale di OMS tramite Raccolta soluzioni.

Le soluzioni di gestione consentono di ottenere informazioni più approfondite per:

* Individuare e risolvere i problemi operativi più rapidamente
* Raccogliere e correlare diversi tipi di dati del computer
* Assicurare reazioni proattive con attività esposte dalla soluzione.

> [!NOTE]
> Log Analytics include funzionalità di ricerca nei log, non è quindi necessario installare una soluzione di gestione per abilitarla. È tuttavia possibile ottenere visualizzazioni dei dati, ricerche suggerite e informazioni dettagliate aggiungendo soluzioni di gestione all'area di lavoro.

Le informazioni contenute in questo articolo permettono di aggiungere soluzioni di gestione a un'area di lavoro tramite il Marketplace del portale di Azure. Dopo aver aggiunto una soluzione, i dati vengono raccolti dai server nell'infrastruttura e inviati al servizio OMS. L’elaborazione da parte del servizio OMS richiede in genere da alcuni minuti a un’ora. Dopo che il servizio ha elaborato i dati, è possibile visualizzarli in OMS.

Le soluzioni di gestione non più necessarie possono essere rimosse facilmente. Quando si rimuove una soluzione di gestione, i dati non vengono inviati a OMS. Se è stato adottato il piano tariffario Gratuito, la rimozione di una soluzione può ridurre la quantità di dati usati, consentendo di rimanere al di sotto della quota giornaliera di dati.

## <a name="view-available-management-solutions"></a>Visualizzare le soluzioni di gestione disponibili

Azure Marketplace contiene l'elenco di [soluzioni di gestione per Log Analytics](https://azuremarketplace.microsoft.com/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).

È possibile installare le soluzioni di gestione da Azure Marketplace facendo clic sul collegamento **Get it now** (Scarica adesso) nella parte inferiore di ogni soluzione.

## <a name="add-a-management-solution"></a>Aggiungere una soluzione di gestione
1. Se questa operazione non è già stata eseguita, accedere al [portale di Azure](https://portal.azure.com), usando la sottoscrizione di Azure.
2. Nel pannello **Nuovo** in **Marketplace** selezionare **Monitoraggio e gestione**.
3. Nel pannello **Monitoraggio e gestione** fare clic su **Visualizza tutto**.  
    Pannello ![Monitoraggio e gestione](./media/log-analytics-add-solutions/monitoring-management-blade.png)  
4. A destra di **Soluzioni di gestione** fare clic su **Altro**.
5. Nel pannello **Soluzioni di gestione** selezionare una soluzione di gestione da aggiungere a un'area di lavoro.  
    Pannello ![Monitoraggio e gestione](./media/log-analytics-add-solutions/management-solutions.png)  
6. Nel pannello Soluzioni di gestione esaminare le informazioni sulla soluzione di gestione e quindi fare clic su **Crea**.
7. Nel pannello relativo al *nome della soluzione di gestione* selezionare un'area di lavoro da associare alla soluzione di gestione.
8. Facoltativamente, è possibile modificare le impostazioni dell'area di lavoro per la sottoscrizione di Azure, il gruppo di risorse e la località. È anche possibile scegliere **Opzioni di automazione**. Fare clic su **Crea**.  
    ![area di lavoro della soluzione](./media/log-analytics-add-solutions/solution-workspace.png)  
9. Per iniziare a usare la soluzione di gestione aggiunta all'area di lavoro, passare a **Log Analytics** > **Sottoscrizioni** > ***nome dell'area di lavoro*** > **Panoramica**. Verrà visualizzato un nuovo riquadro per la soluzione di gestione. Fare clic sul riquadro per aprirlo e iniziare a usare la soluzione dopo aver raccolto i dati per la soluzione.

## <a name="remove-a-management-solution"></a>Rimuovere una soluzione di gestione

1. Nel [portale di Azure](https://portal.azure.com) passare a **Log Analytics** > **Sottoscrizioni** > ***nome dell'area di lavoro*** e quindi nel pannello relativo al ***nome dell'area di lavoro*** fare clic su **Soluzioni**.
2. Selezionare la soluzione da rimuovere dall'elenco delle soluzioni di gestione.
3. Nel pannello della soluzione per l'area di lavoro, fare clic su **Elimina**.  
    ![elimina soluzione](./media/log-analytics-add-solutions/solution-delete.png)  
4. Nella finestra di dialogo di conferma fare clic su **Sì**.

## <a name="offers-and-pricing-tiers"></a>Offerte e piani tariffari

La tabella seguente indica le soluzioni di gestione pertinenti a ogni offerta di Operations Management Suite.
La tabella indica anche i piani tariffari disponibili per ogni soluzione di gestione.
Tutte le soluzioni della tabella seguente sono disponibili nel portale di Azure e nella raccolta di soluzioni nel portale di Log Analytics.

| Soluzione di gestione                                                                       | Offerta                                                                     | Piani tariffari<sup>1</sup>                                                 | Note |
| ---                                                                                       | ---                                                                       | ---                                                                                                       | ---   |
| [Activity Log Analytics](log-analytics-activity.md)                                                                   | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | Sono disponibili 90 giorni gratuiti di traffico dati<br>Dati non soggetti al limite del livello gratuito |
| [Valutazione di AD](log-analytics-ad-assessment.md)                                           | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [Stato della replica di AD](log-analytics-ad-replication-status.md)                           | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | Non disponibile per essere aggiunto dal portale di Azure/marketplace. |
| [Integrità agente](../operations-management-suite/oms-solution-agenthealth.md)                                                                                | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | Dati non soggetti al limite del livello gratuito<br> Non disponibile per essere aggiunto dal portale di Azure/marketplace. |
| [Gestione degli avvisi](log-analytics-solution-alert-management.md)                            | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | Non disponibile per essere aggiunto dal portale di Azure/marketplace. |
| [Connettore di Application Insights (anteprima)](log-analytics-app-insights-connector.md)                                               | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [Ruolo di lavoro ibrido per runbook di Automazione](../automation/automation-hybrid-runbook-worker.md)                                                                     | <ul><li>Automation & Control</li></ul>                                  | Gratuito<br> Per&nbsp;nodo&nbsp;(OMS)                                                                         | È necessario che l'area di lavoro di Log Analytics sia collegata a un account di Automazione |
| [Analisi dei gateway applicazione di Azure](log-analytics-azure-networking-analytics.md)    | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [Analisi del gruppo di sicurezza di rete di Azure](log-analytics-azure-networking-analytics.md)     | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [Azure SQL Analytics (Anteprima)](log-analytics-azure-sql.md)                                                       | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br>Per&nbsp;nodo&nbsp;(OMS)                                                                          | È necessario che l'area di lavoro di Log Analytics sia collegata a un account di Automazione|
| [Analisi app Web di Azure](log-analytics-azure-web-apps-analytics.md)     | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
|[Backup](../backup/backup-introduction-to-azure-backup.md)                                                                                 | <ul><li>Insight & Analytics</li></ul>                                   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)                                                                       | È necessario un insieme di credenziali di backup classico.<br> Non disponibile per essere aggiunto dal portale di Azure/marketplace. |
| [Capacità e prestazioni (anteprima)](log-analytics-capacity.md)                                                   | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [Rilevamento delle modifiche](log-analytics-change-tracking.md)                                       | <ul><li>Automation & Control</li></ul>                                  | Gratuito<br> Per&nbsp;nodo&nbsp;(OMS)                                                                         | È necessario che l'area di lavoro di Log Analytics sia collegata a un account di Automazione |
| [Contenitori](log-analytics-containers.md)                                                 | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [IT Service Management Connector](log-analytics-itsmc-overview.md)                                                | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Per&nbsp;nodo&nbsp;(OMS)     | |
| Monitoraggio per HDInsight HBase <br>(Anteprima)                                                  | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [Analisi dell'insieme di credenziali delle chiavi](log-analytics-azure-key-vault.md)                   | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [App per la logica B2B](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)                    | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | Non disponibile per essere aggiunto dal portale di Azure/marketplace. |
| [Valutazione di malware](log-analytics-malware.md)                                            | <ul><li>Sicurezza e conformità</li></ul>                                 | Gratuito<br> Autonoma<br>Per&nbsp;nodo&nbsp;(OMS)                                                                           | Se si aggiungono le soluzioni Sicurezza e conformità dopo il 19 giugno 2017, queste verranno [fatturate per nodo](https://azure.microsoft.com/pricing/details/security-compliance/) indipendentemente dal piano tariffario dell'area di lavoro. I primi 60 giorni sono gratuiti.  |
| [Monitoraggio delle prestazioni di rete](log-analytics-network-performance-monitor.md) <br>  | <ul><li>Insight & Analytics</li></ul>                                   | Gratuito<br> Per&nbsp;nodo&nbsp;(OMS)                                                                         | |
| [Analisi Office 365 (anteprima)](../operations-management-suite/oms-solution-office-365.md)                                                       | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [Sicurezza e controllo](../operations-management-suite/oms-security-getting-started.md)      | <ul><li>Sicurezza &nbsp;e&nbsp;conformità</li></ul>                       | Gratuito<br> Autonoma<br>Per&nbsp;nodo&nbsp;(OMS)                                                                           | Questa soluzione è necessaria per la raccolta dei log eventi di sicurezza<br>Se si aggiungono le soluzioni Sicurezza e conformità dopo il 19 giugno 2017, queste verranno [fatturate per nodo](https://azure.microsoft.com/pricing/details/security-compliance/) indipendentemente dal piano tariffario dell'area di lavoro. I primi 60 giorni sono gratuiti. |
| [Service Fabric Analytics (anteprima)](log-analytics-service-fabric.md)                     | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [Mapping dei servizi (anteprima)](../operations-management-suite/operations-management-suite-service-map.md) | <ul><li>Insight & Analytics</li></ul>                      | Gratuito<br> Per&nbsp;nodo&nbsp;(OMS)                                                                         | Disponibile in Europa orientale, Europa occidentale e Stati Uniti centro-occidentali    |
| [Site Recovery](../site-recovery/site-recovery-overview.md)                                                                               | <ul><li>Insight & Analytics</li></ul>                                   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)                                                                       | Richiede un insieme di credenziali di ripristino sito classico.<br> Non disponibile per essere aggiunto dal portale di Azure/marketplace. |
| [SQL Assessment](log-analytics-sql-assessment.md)                                         | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| Avviare/arrestare VM durante gli orari di minore attività<br>(Anteprima)                                              | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Per&nbsp;nodo&nbsp;(OMS)                                                                         | È necessario che l'area di lavoro di Log Analytics sia collegata a un account di Automazione |
| [SurfaceHub](log-analytics-surface-hubs.md)                                               | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | Non disponibile per essere aggiunto dal portale di Azure/marketplace. |
| [Valutazione System Center Operations Manager (anteprima)](log-analytics-scom-assessment.md)  | <ul><li>Insight & Analytics</li><li>Log Analytics</li></ul>        | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [Gestione degli aggiornamenti](../operations-management-suite/oms-solution-update-management.md)                                                                         | <ul><li>Automation & Control</li></ul>                                  | Gratuito<br> Per&nbsp;nodo&nbsp;(OMS)                                                                         | È necessario che l'area di lavoro di Log Analytics sia collegata a un account di Automazione |
| [Conformità aggiornamenti (anteprima)](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started)                                                             | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | Non sono previsti addebiti per i dati o i nodi<br>Dati non soggetti al limite del livello gratuito.<br> Non disponibile per essere aggiunto dal portale di Azure/marketplace. |
| [Preparazione dell'aggiornamento](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started)                                                          | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | Non sono previsti addebiti per i dati o i nodi<br>Dati non soggetti al limite del livello gratuito.<br> Non disponibile per essere aggiunto dal portale di Azure/marketplace. |
| [Monitoraggio VMware (anteprima)](log-analytics-vmware.md)                                | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(autonomo)<br> Per&nbsp;nodo&nbsp;(OMS)   | |
| [Wire Data 2.0 (anteprima)](log-analytics-wire-data.md)                                                                 | <ul><li>Insight & Analytics</li></ul>                                   | Gratuito<br> Per&nbsp;nodo&nbsp;(OMS)                                                                         | Disponibile in Europa orientale, Europa occidentale e Stati Uniti centro-occidentali |

<sup>1</sup> I piani tariffari *Standard* e *Premium (OMS)* sono disponibili solo per i clienti che hanno creato l'area di lavoro di Log Analytics prima del 21 settembre 2016.

### <a name="community-provided-management-solutions"></a>Soluzioni di gestione offerte dalla community

Le soluzioni offerte dalla community sono disponibili nella [raccolta di modelli di Azure](https://azure.microsoft.com/resources/templates/?term=Per&nbsp;Node&nbsp;(OMS)) e direttamente dagli autori.

| Soluzione di gestione               | Offerta                                                                     | Piani tariffari                         | Note |
| ---                               | ---                                                                       | ---                                   | ---   |
| Tutte le soluzioni offerte dalla community  | <ul><li>Insight&nbsp;&&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratuito<br> Per&nbsp;nodo&nbsp;(OMS)     |   È necessario che l'area di lavoro di Log Analytics sia collegata a un account di Automazione |




## <a name="data-collection-details"></a>Informazioni dettagliate sulla raccolta di dati
Le tabelle seguenti illustrano i metodi di raccolta dei dati e altre informazioni dettagliate sul modo in cui i dati vengono raccolti per le origini dati e le soluzioni di gestione di Log Analytics. Le tabelle sono classificate in base alle soluzioni offerte, che equivalgono ai [piani tariffari delle sottoscrizioni](https://go.microsoft.com/fwlink/?linkid=827926). La soluzione Activity Log Analytics è disponibile gratuitamente per tutti i piani tariffari.

L'agente Windows per Log Analytics e l'agente System Center Operations Manager sono essenzialmente uguali. L'agente Windows include funzionalità aggiuntive che ne consentono la connessione all'area di lavoro di OMS e l'indirizzamento tramite un proxy. Se si usa un agente Operations Manager, è necessario impostarlo come agente OMS per consentire la comunicazione con OMS. Gli agenti Operations Manager in questa tabella sono agenti OMS connessi a Operations Manager. Per informazioni sulla connessione dell'ambiente Operations Manager esistente a OMS, vedere [Connettere Operations Manager a Log Analytics](log-analytics-om-agents.md).

> [!NOTE]
> Il tipo di agente usato determina il modo in cui i dati vengono inviati a OMS, con le condizioni seguenti:
> - Si usa l'agente Windows o un agente OMS associato a Operations Manager.
> - Quando è necessario Operations Manager, i dati dell'agente Operations Manager per la soluzione vengono sempre inviati a OMS usando il gruppo di gestione di Operations Manager. Inoltre, quando è necessario Operations Manager, viene usato dalla soluzione solo l'agente Operations Manager.
> - Quando Operations Manager non è necessario e la tabella mostra che i dati dell'agente Operations Manager vengono inviati a OMS usando il gruppo di gestione, i dati dell'agente Operations Manager vengono inviati sempre a OMS usando i gruppi di gestione. Gli agenti Windows ignorano il gruppo di gestione e inviano i dati direttamente a OMS.
> - Quando i dati dell'agente Operations Manager non vengono inviati usando un gruppo di gestione, i dati vengono inviati direttamente a OMS, ignorando il gruppo di gestione.

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
| Trasferimento dati |Windows (2012 R2/8.1 o versioni successive) |&#8226; |&#8226; |  |  |  | 1 minuto |


### <a name="automation--control"></a>Automation & Control

| Soluzione di gestione | Piattaforma | Microsoft Monitoring Agent | Agente di Operations Manager | Archiviazione di Azure | È necessario Operations Manager? | Dati dell'agente Operations Manager inviati con il gruppo di gestione | Frequenza della raccolta |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Ruolo di lavoro ibrido di Automazione | Windows | &#8226; | &#8226; |   |   |   | n/d |
| Change Tracking |Windows |&#8226; |&#8226; |  |  |&#8226; |Ogni ora |
| Change Tracking |Linux |&#8226; |  |  |  |  |Ogni ora |
| Gestione degli aggiornamenti | Windows |&#8226; |&#8226; |  |  |&#8226; |almeno 2 volte al giorno e 15 minuti dopo l'installazione di un aggiornamento |

### <a name="security--compliance"></a>Sicurezza e conformità

| Soluzione di gestione | Piattaforma | Microsoft Monitoring Agent | Agente di Operations Manager | Archiviazione di Azure | È necessario Operations Manager? | Dati dell'agente Operations Manager inviati con il gruppo di gestione | Frequenza della raccolta |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Antimalware Assessment |Windows |&#8226; |&#8226; |  |  |&#8226; |Ogni ora |
| Security and Audit<sup>1</sup> | Windows e Linux | parziale | parziale | parziale |   | parziale | variabile |

<sup>1</sup>La soluzione Sicurezza e controllo può raccogliere log da agenti Windows, Operations Manager e Linux. Vedere la tabella [Origini dati](#data-sources) per informazioni sulla raccolta dati relativa a:

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
| log di IIS |Windows |&#8226; |&#8226; |&#8226; |  |  |5 minuti |
| Contatori delle prestazioni |Windows |&#8226; |&#8226; |  |  |  |come pianificato, almeno 10 secondi |
| Contatori delle prestazioni |Linux |&#8226; |  |  |  |  |come pianificato, almeno 10 secondi |
| syslog |Linux |&#8226; |  |  |  |  |dall'Archiviazione di Azure: 10 minuti; dall'agente: all'arrivo |
| Registri eventi della sicurezza di Windows |Windows |&#8226; |&#8226; |&#8226; |  |  |per l'Archiviazione di Azure: 10 min.; per l'agente: all'arrivo |
| Registri firewall di Windows |Windows |&#8226; |&#8226; |  |  |  |all'arrivo |
| Registri eventi di Windows |Windows |&#8226; |&#8226; |&#8226; |  |&#8226; |per l'Archiviazione di Azure: 10 min.; per l'agente: all'arrivo |



## <a name="preview-management-solutions-and-features"></a>Soluzioni di gestione e funzionalità in anteprima
Eseguendo un servizio e seguendo procedure DevOps, Microsoft può collaborare con i clienti per sviluppare funzionalità e soluzioni.

Durante l'anteprima privata, a un piccolo gruppo di clienti viene fornito l'accesso a un'implementazione preliminare della funzionalità o della soluzione per ottenere commenti e apportare miglioramenti. Questa implementazione preliminare è dotata di funzionalità e capacità operative minime.

L’obiettivo è eseguire una rapida prova per vedere cosa funziona e cosa non funziona. Questo processo viene iterato più volte fino a quando, sulla base dei commenti dei clienti dell’anteprima privata, non è possibile passare all’anteprima pubblica.

Durante l’anteprima pubblica, la funzionalità o la soluzione viene resa disponibile per tutti gli utenti per ottenere più commenti e convalidarne il ridimensionamento e l’efficienza. In questa fase:

* Le funzionalità in anteprima vengono visualizzate nella scheda Impostazioni e possono essere abilitate da qualsiasi utente.
* Le soluzioni in anteprima vengono aggiunte tramite la raccolta o uno script.

### <a name="what-should-i-know-about-preview-features-and-solutions"></a>Cosa occorre sapere sulle funzionalità e le soluzioni in anteprima
Microsoft è molto interessata alle nuove funzionalità e soluzioni di gestione ed è lieta di collaborare al loro sviluppo.

Le funzionalità e le soluzioni in anteprima non sono adatte a tutti. Prima di chiedere di partecipare a un'anteprima privata o di passare a un'anteprima pubblica, è quindi necessario verificare di sentirsi a proprio agio nell'affrontare elementi ancora in fase di sviluppo.

Quando si abilita una funzionalità di anteprima tramite il portale, viene visualizzato un avviso che ricorda che si tratta di un'anteprima.

#### <a name="for-both-private-and-public-preview"></a>Per l'anteprima sia *privata* che *pubblica*
Le informazioni seguenti si applicano alle anteprime sia private che pubbliche:

* Non sempre tutto potrebbe funzionare correttamente.
  * I problemi vanno da aspetti di minor rilievo a elementi che non funzionano affatto.
* L'anteprima potrebbe influire negativamente sui sistemi o l'ambiente usato.
  * Microsoft cerca di evitare che accada qualcosa di negativo ai sistemi usati con OMS, ma a volte si verificano imprevisti.
* Può verificarsi la perdita o il danneggiamento dei dati.
* È possibile che venga richiesto di raccogliere i log di diagnostica o altri dati per agevolare la risoluzione dei problemi.
* La funzionalità o la soluzione potrebbe essere rimossa, in via temporanea o definitiva.
  * In base a quanto appreso durante l'anteprima, Microsoft può decidere di non rilasciare la funzionalità o la soluzione.
* Le anteprime potrebbero non funzionare o non essere testate con tutte le configurazioni e Microsoft potrebbe pertanto limitare:
  * I sistemi operativi utilizzabili, ad esempio una funzionalità potrebbe essere applicabile solo a Linux in fase di anteprima.
  * Il tipo di agente (MMA, Operations Manager) utilizzabile, ad esempio una funzionalità potrebbe non funzionare con Operations Manager durante l'anteprima.  
* Le soluzioni e le funzionalità in anteprima non sono coperte dal Contratto di servizio.
* L'utilizzo di funzionalità in anteprima dà luogo ad addebiti.
* Funzionalità o capacità necessarie per l'utilità della funzione o della soluzione potrebbero mancare o essere incomplete.
* Alcune funzionalità/soluzioni potrebbero non essere disponibili in tutte le aree.
* Alcune funzionalità/soluzioni potrebbero non essere localizzate.
* Alcune funzionalità/soluzioni potrebbero presentare un limite al numero di clienti o dispositivi che possono usarle.
* Potrebbe essere necessario usare script per eseguire la configurazione e per abilitare la soluzione/funzionalità.
* L'interfaccia utente si presenta incompleta e potrebbe cambiare di giorno in giorno.
* Le anteprime pubbliche potrebbero non essere appropriate per sistemi di produzione o critici.

#### <a name="for-private-preview"></a>Per l’anteprima *privata*
Oltre alle considerazioni precedenti, le informazioni seguenti sono specifiche per le anteprime private:

* Microsoft prevede di ricevere commenti e suggerimenti sull'esperienza di anteprima per poter migliorare la funzionalità/soluzione.
* Potrebbe quindi chiedere agli utenti di fornire tali commenti e suggerimenti rispondendo a questionari, chiamate telefoniche o messaggi di posta elettronica.
* Non sempre tutto funziona correttamente.
* Potrebbe essere richiesta la sottoscrizione di un accordo di riservatezza per la partecipazione o potrebbe essere incluso contenuto riservato.
  * Prima di comunicare informazioni a terze parti tramite blog, tweet o in altro modo, verificare con il Program Manager responsabile dell'anteprima la presenza di eventuali restrizioni alla divulgazione.
* Non eseguire l'anteprima in sistemi di produzione o critici.

### <a name="how-do-i-get-access-to-private-preview-features-and-solutions"></a>Come si ottiene l’accesso alle soluzioni e alle funzionalità di anteprima?
Microsoft invita i clienti alle anteprime private in diversi modi a seconda dell'anteprima.

* Rispondendo al sondaggio clienti mensile e autorizzando Microsoft a restare in contatto, aumentano le possibilità di essere invitati a un'anteprima privata.
* I partecipanti possono essere proposti dal team degli account Microsoft.
* È possibile effettuare l'iscrizione in base alle informazioni pubblicate sulla pagina Twitter [msopsmgmt](https://twitter.com/msopsmgmt).
* È possibile effettuare l'iscrizione in base alle informazioni condivise in occasione di eventi della community, come raduni, conferenze e community online.

## <a name="next-steps"></a>Passaggi successivi
* [Eseguire ricerche nei log](log-analytics-log-searches.md) per visualizzare le informazioni dettagliate raccolte dalle soluzioni di gestione.
