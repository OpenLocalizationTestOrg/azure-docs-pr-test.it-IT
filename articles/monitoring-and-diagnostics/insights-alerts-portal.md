---
title: gli avvisi aaaCreate per servizi di Azure - portale di Azure | Documenti Microsoft
description: Attivare l'automazione, notifiche, gli URL di siti Web di chiamata (webhook) o messaggi di posta elettronica quando vengono soddisfatte le condizioni di hello specificate.
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/23/2016
ms.author: robb
ms.openlocfilehash: 78d862d25255cda9fdfe347329e908a471c39846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a>Creare avvisi sulle metriche in Monitoraggio di Azure per i servizi di Azure: portale di Azure
> [!div class="op_single_selector"]
> * [Portale](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Panoramica
Questo articolo illustra come tooset di Azure avvisi metrica utilizzando hello portale di Azure.   

È possibile ricevere avvisi basati su metriche di monitoraggio o eventi nei servizi Azure.

* **Valori della metrica** : hello trigger un avviso quando il valore di hello di una specifica metrica supera una soglia è assegnare in entrambe le direzioni. Ovvero, entrambi attiva quando hello prima condizione e quindi successivamente non condizione when che è non è più in grado di soddisfare.    
* **Eventi del log attività**: è possibile attivare un avviso per *ogni* evento o solo quando si verifica un determinato evento. ulteriori informazioni sugli avvisi di log attività toolearn [fare clic qui](monitoring-activity-log-alerts.md)

È possibile configurare una metrica toodo avviso hello seguenti attiva:

* inviare coamministratore e amministratore del servizio toohello le notifiche tramite posta elettronica
* Invia messaggio di posta elettronica tooadditional messaggi di posta elettronica specificato.
* chiamare un webhook
* avviare l'esecuzione di un runbook di Azure (solo da hello portale di Azure)

È possibile configurare e ottenere informazioni sulle regole degli avvisi sulle metriche tramite

* [Portale di Azure](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [interfaccia della riga di comando](insights-alerts-command-line-interface.md)
* [API REST di Monitoraggio di Azure](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a>Creare una regola di avviso su una metrica con hello portale di Azure
1. In hello [portale](https://portal.azure.com/)individuare risorse hello si è interessati a monitoraggio e selezionarlo.

2. Selezionare **avvisi** o **regole di avviso** nella sezione monitoraggio hello. icona e il testo hello possono variare leggermente a diverse risorse.  

    ![Monitoraggio](./media/insights-alerts-portal/AlertRulesButton.png)

3. Seleziona hello **Aggiungi avviso** comando e compilare i campi di hello.

    ![Aggiungi avviso](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. Assegnare alla regola di avviso un **Nome** e scegliere una **Descrizione**, che viene visualizzata anche nella notifica inviata tramite posta elettronica.

5. Seleziona hello **metrica** toomonitor desiderato, quindi scegliere un **condizione** e **soglia** valore per la misurazione hello. Anche scelta hello **periodo** di tempo che hello metrica regola deve essere soddisfatti prima di allarmi hello. Ad esempio, se si utilizza il periodo di hello "PT5M" e l'avviso Cerca della CPU superiore all'80%, avviso hello attiva quando hello della CPU è stata costantemente sopra l'80% per 5 minuti. Quando si verifica primo trigger hello, nuovamente attiva quando hello della CPU rimane sotto l'80% per 5 minuti. Hello misura della CPU si verifica a intervalli di 1 minuto.   

6. Controllare **proprietari di posta elettronica...**  se si desidera che gli amministratori e i coamministratori toobe inviato tramite posta elettronica quando hello avviso generato.

7. Se si desidera che altri messaggi di posta elettronica tooreceive una notifica quando hello viene generato un avviso, aggiungerle in hello **email(s) amministratore aggiuntive** campo. Separare gli indirizzi di posta elettronica con punti e virgola: *email@contoso.com;email2@contoso.com*

8. Inserire in un URI valido in hello **Webhook** campo se si desidera che chiamato hello quando avviso generato.

9. Se si utilizza l'automazione di Azure, è possibile selezionare un toobe Runbook eseguito quando viene generato l'avviso hello.

10. Selezionare **OK** quando toocreate done hello avviso.   

Entro pochi minuti, l'avviso hello è attivo e attiva come descritto in precedenza.

## <a name="managing-your-alerts"></a>Gestione degli avvisi
Dopo aver creato un avviso, è possibile selezionarlo e:

* Consente di visualizzare un grafico che mostra soglia hello per le metriche e i valori effettivi da hello hello giorno precedente.
* Modificarlo o eliminarlo.
* **Disabilitare** o **abilitare** se si desidera tootemporarily arrestare o riprendere la ricezione di notifiche relative a questo avviso.

## <a name="next-steps"></a>Passaggi successivi
* [Panoramica di Azure monitoring](monitoring-overview.md) inclusi i tipi di informazioni è possibile raccogliere e monitorare hello.
* Altre informazioni sulla [configurazione dei webhook negli avvisi](insights-webhooks-alerts.md).
* Altre informazioni sulla [configurazione di avvisi sugli eventi del log attività](monitoring-activity-log-alerts.md).
* Altre informazioni sui [runbook di automazione di Azure](../automation/automation-starting-a-runbook.md).
* Leggere una [panoramica dei log di diagnostica](monitoring-overview-of-diagnostic-logs.md) e sulla raccolta di metriche dettagliate e ad alta frequenza sul servizio.
* Ottenere un [Panoramica della raccolta di metriche](insights-how-to-customize-monitoring.md) toomake che il servizio sia disponibile e reattiva.
