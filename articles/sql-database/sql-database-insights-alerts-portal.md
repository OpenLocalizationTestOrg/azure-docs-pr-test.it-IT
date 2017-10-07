---
title: gli avvisi di Database SQL di Azure toocreate portale aaaUse | Documenti Microsoft
description: Utilizzare hello toocreate portale Azure SQL Database gli avvisi che possono attivare notifiche o automazione quando vengono soddisfatte le condizioni di hello specificate.
author: aamalvea
manager: jhubbard
editor: 
services: sql-database
documentationcenter: 
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: sql-database
ms.custom: monitor and tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: aamalvea
ms.openlocfilehash: 4e494b130a26c4cdf42445cb49648fce9bf4d300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-toocreate-alerts-for-azure-sql-database-and-data-warehouse"></a>Utilizzare gli avvisi di Azure toocreate portale per Database SQL di Azure e Data Warehouse

## <a name="overview"></a>Panoramica
Questo articolo illustra come tooset di avvisi di Database SQL di Azure e Data Warehouse utilizzando hello portale di Azure. Questo articolo include anche le procedure consigliate per impostare i periodi di avviso.    

È possibile ricevere avvisi basati su metriche di monitoraggio o eventi nei servizi Azure.

* **Valori della metrica** : hello trigger un avviso quando il valore di hello di una specifica metrica supera una soglia è assegnare in entrambe le direzioni. Ovvero, entrambi attiva quando hello prima condizione e quindi successivamente non condizione when che è non è più in grado di soddisfare.    
* **Eventi del log attività** : è possibile attivare un avviso per *ogni* evento o solo quando si verifica un determinato numero di eventi.

È possibile configurare un avviso toodo hello seguenti attiva:

* inviare coamministratore e amministratore del servizio toohello le notifiche tramite posta elettronica
* Invia messaggio di posta elettronica tooadditional messaggi di posta elettronica specificato.
* chiamare un webhook

È possibile configurare e ottenere informazioni sulle regole degli avvisi tramite

* [Portale di Azure](../monitoring-and-diagnostics/insights-alerts-portal.md)
* [PowerShell](../monitoring-and-diagnostics/insights-alerts-powershell.md)
* [interfaccia della riga di comando](../monitoring-and-diagnostics/insights-alerts-command-line-interface.md)
* [API REST di Monitoraggio di Azure](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a>Creare una regola di avviso su una metrica con hello portale di Azure
1. In hello [portale](https://portal.azure.com/)individuare risorse hello si è interessati a monitoraggio e selezionarlo.
2. Questo passaggio per il database SQL e i pool elastici è diverso rispetto a quello per SQL Data Warehouse: 

   - **Database di SQL Server & solo pool elastico**: selezionare **avvisi** o **regole di avviso** nella sezione monitoraggio hello. icona e il testo hello possono variare leggermente a diverse risorse.  
   
     ![Monitoraggio](../monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButton.png)
  
   - **SOLO data Warehouse SQL**: selezionare **monitoraggio** in hello sezione attività comuni. Fare clic su hello **DWU utilizzo** grafico.

     ![ATTIVITÀ COMUNI](../monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButtonDW.png)

3. Seleziona hello **Aggiungi avviso** comando e compilare i campi di hello.
   
    ![Aggiungi avviso](../monitoring-and-diagnostics/media/insights-alerts-portal/AddDBAlertPage.png)
4. Assegnare alla regola di avviso un **Nome** e scegliere una **Descrizione**, che viene visualizzata anche nella notifica inviata tramite posta elettronica.
5. Seleziona hello **metrica** toomonitor desiderato, quindi scegliere un **condizione** e **soglia** valore per la misurazione hello. Anche scelta hello **periodo** di tempo che hello metrica regola deve essere soddisfatti prima di allarmi hello. Ad esempio, se si utilizza il periodo di hello "PT5M" e l'avviso Cerca della CPU superiore all'80%, avviso hello attiva quando hello della CPU è stata costantemente sopra l'80% per 5 minuti. Quando si verifica primo trigger hello, nuovamente attiva quando hello della CPU rimane sotto l'80% per 5 minuti. Hello misura della CPU si verifica a intervalli di 1 minuto.   
6. Controllare **proprietari di posta elettronica...**  se si desidera che gli amministratori e i coamministratori toobe inviato tramite posta elettronica quando hello avviso generato.
7. Se si desidera che altri messaggi di posta elettronica tooreceive una notifica quando hello viene generato un avviso, aggiungerle in hello **email(s) amministratore aggiuntive** campo. Separare gli indirizzi di posta elettronica con punti e virgola: *email@contoso.com;email2@contoso.com*
8. Inserire in un URI valido in hello **Webhook** campo se si desidera che chiamato hello quando avviso generato.
9. Selezionare **OK** quando toocreate done hello avviso.   

Entro pochi minuti, l'avviso hello è attivo e attiva come descritto in precedenza.

## <a name="managing-your-alerts"></a>Gestione degli avvisi
Dopo aver creato un avviso, è possibile selezionarlo e:

* Consente di visualizzare un grafico che mostra soglia hello per le metriche e i valori effettivi da hello hello giorno precedente.
* Modificarlo o eliminarlo.
* **Disabilitare** o **abilitare** se si desidera tootemporarily arrestare o riprendere la ricezione di notifiche relative a questo avviso.


## <a name="sql-database-alert-values"></a>Valori degli avvisi per il database SQL

| Tipo di risorsa | Nome della metrica | Nome descrittivo | Tipo di aggregazione | Intervallo di tempo minimo per l'avviso|
| --- | --- | --- | --- | --- |
| Database SQL | cpu_percent | Percentuale CPU | Media | 5 minuti |
| Database SQL | physical_data_read_percent | Percentuale di I/O di dati | Media | 5 minuti |
| Database SQL | log_write_percent | Percentuale I/O registro | Media | 5 minuti |
| Database SQL | dtu_consumption_percent | Percentuale di DTU | Media | 5 minuti |
| Database SQL | storage | Dimensioni totali database | Massima | 30 minuti |
| Database SQL | connection_successful | Connessioni riuscite | Totale | 10 minuti |
| Database SQL | connection_failed | Connessioni non riuscite | Totale | 10 minuti |
| Database SQL | blocked_by_firewall | Blocco da parte del firewall | Totale | 10 minuti |
| Database SQL | deadlock | Deadlock | Totale | 10 minuti |
| Database SQL | storage_percent | Percentuale di dimensioni del database | Massima | 30 minuti |
| Database SQL | xtp_storage_percent | Percentuale archiviazione OLTP interna alla memoria (anteprima) | Media | 5 minuti |
| Database SQL | workers_percent | Percentuale ruoli di lavoro | Media | 5 minuti |
| Database SQL | sessions_percent | Percentuale sessioni | Media | 5 minuti |
| Database SQL | dtu_limit | Limite DTU | Media | 5 minuti |
| Database SQL | dtu_used | Uso DTU | Media | 5 minuti |
||||||
| Pool elastico | cpu_percent | Percentuale CPU | Media | 10 minuti |
| Pool elastico | physical_data_read_percent | Percentuale di I/O di dati | Media | 10 minuti |
| Pool elastico | log_write_percent | Percentuale I/O registro | Media | 10 minuti |
| Pool elastico | dtu_consumption_percent | Percentuale di DTU | Media | 10 minuti |
| Pool elastico | storage_percent | Percentuale archiviazione | Media | 10 minuti |
| Pool elastico | workers_percent | Percentuale ruoli di lavoro | Media | 10 minuti |
| Pool elastico | eDTU_limit | Limite eDTU | Media | 10 minuti |
| Pool elastico | storage_limit | Limite archiviazione | Media | 10 minuti |
| Pool elastico | eDTU_used | Uso eDTU | Media | 10 minuti |
| Pool elastico | storage_used | Uso archiviazione | Media | 10 minuti |
||||||               
| SQL Data Warehouse | cpu_percent | Percentuale CPU | Media | 10 minuti |
| SQL Data Warehouse | physical_data_read_percent | Percentuale di I/O di dati | Media | 10 minuti |
| SQL Data Warehouse | storage | Dimensioni totali database | Massima | 10 minuti |
| SQL Data Warehouse | connection_successful | Connessioni riuscite | Totale | 10 minuti |
| SQL Data Warehouse | connection_failed | Connessioni non riuscite | Totale | 10 minuti |
| SQL Data Warehouse | blocked_by_firewall | Blocco da parte del firewall | Totale | 10 minuti |
| SQL Data Warehouse | service_level_objective | Obiettivo del livello di servizio del database hello | Totale | 10 minuti |
| SQL Data Warehouse | dwu_limit | Limite DWU | Massima | 10 minuti |
| SQL Data Warehouse | dwu_consumption_percent | Percentuale DWU | Media | 10 minuti |
| SQL Data Warehouse | dwu_used | Uso DWU | Media | 10 minuti |
||||||


## <a name="next-steps"></a>Passaggi successivi
* [Panoramica di Azure monitoring](../monitoring-and-diagnostics/monitoring-overview.md) inclusi i tipi di informazioni è possibile raccogliere e monitorare hello.
* Altre informazioni sulla [configurazione dei webhook negli avvisi](../monitoring-and-diagnostics/insights-webhooks-alerts.md).
* Leggere una [panoramica dei log di diagnostica](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) e sulla raccolta di metriche dettagliate e ad alta frequenza sul servizio.
* Ottenere un [Panoramica della raccolta di metriche](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake che il servizio sia disponibile e reattiva.
