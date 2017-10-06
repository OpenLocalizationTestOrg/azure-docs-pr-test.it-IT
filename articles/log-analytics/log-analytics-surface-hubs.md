---
title: aaaMonitor Surface hub con Analitica di Log di Azure | Documenti Microsoft
description: "Utilizzare hello Surface Hub soluzione tootrack hello integrità gli hub di area e comprendere la modalità in uso."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 623d30e749cafdd4a34ba0c5b3408164f1b4a95b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-tootrack-their-health"></a>Monitorare Surface hub con Log Analitica tootrack lo stato di integrità

![Simbolo di Surface Hub](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

In questo articolo viene descritto come utilizzare soluzioni Surface Hub hello nei dispositivi di Microsoft Surface Hub toomonitor Log Analitica con hello Microsoft Operations Management Suite (OMS). Log consente di Analitica che verificare integrità hello degli hub di area nonché comprendere la modalità in uso.

Ogni Surface Hub è installato Microsoft Monitoring Agent hello. Relativo all'agente hello che è possibile inviare i dati dal tooOMS Surface Hub. File di log vengono letti dal Surface hub e vengono quindi inviati servizio OMS toohello. Problemi come i server in modalità offline, hello calendario non la sincronizzazione o se hello dispositivo account non è possibile toolog in Skype vengono visualizzati in OMS nel dashboard di hello Surface Hub. Utilizzando i dati di hello nel dashboard di hello, è possibile identificare i dispositivi che non sono in esecuzione o che hanno altri problemi e potenzialmente applicare correzioni a problemi di hello rilevato.

## <a name="installing-and-configuring-hello-solution"></a>Installazione e configurazione di soluzione hello
Utilizzare hello tooinstall le informazioni seguenti e configurare la soluzione hello. In ordine toomanage gli hub di superficie da hello Microsoft Operations Management Suite (OMS), è necessario hello seguenti:

* Una sottoscrizione valida troppo[OMS](http://www.microsoft.com/oms).
* Un [sottoscrizione OMS](https://azure.microsoft.com/pricing/details/log-analytics/) livello che sarà supportato hello numero di dispositivi desiderato toomonitor. I prezzi di OMS variano a seconda del numero dei dispositivi registrati e del volume di dati in elaborazione. È opportuno tootake questo in considerazione quando si pianifica l'implementazione di Surface Hub.

Successivamente, si verrà aggiunta una sottoscrizione di Microsoft Azure esistente OMS sottoscrizione tooyour o creare una nuova area di lavoro direttamente tramite il portale di OMS hello. le istruzioni dettagliate per usare uno di questi metodi sono fornite nella sezione [Introduzione a Log Analytics](log-analytics-get-started.md). Una volta configurato hello sottoscrizione OMS, sono disponibili due modi tooenroll dispositivi Surface Hub:

* Automaticamente tramite Intune
* Manualmente tramite **Impostazioni** sul dispositivo di Surface Hub.

## <a name="set-up-monitoring"></a>Configurare il monitoraggio
È possibile monitorare l'integrità di hello e l'attività di Hub area utilizzando Analitica di Log in OMS. È possibile registrare hello Surface Hub in OMS con Intune o localmente tramite **impostazioni** su hello Surface Hub.

## <a name="connect-surface-hubs-toooms-through-intune"></a>Connettersi tooOMS Surface hub tramite Intune
Sarà necessario hello ID area di lavoro e la chiave dell'area di lavoro per l'area di lavoro OMS hello che gestirà gli hub di area. È possibile ottenere quelle dal portale OMS hello.

Intune è un prodotto Microsoft che consente di toocentrally gestire impostazioni di configurazione di OMS hello tooone applicato sono più dei dispositivi. Seguire questi passaggi tooconfigure i dispositivi tramite Intune:

1. Accedi tooIntune.
2. Passare troppo**impostazioni** > **Connected Sources**.
3. Creare o modificare un criterio basato sul modello di hello Surface Hub.
4. Passare toohello sezione OMS (Azure Operational Insights) dei criteri di hello e aggiungere hello *ID area di lavoro* e *chiave dell'area di lavoro* toohello criteri.
5. Salvare il criterio di hello.
6. Consente di associare i criteri di hello gruppo di dispositivi appropriato hello.

   ![Criterio di Intune](./media/log-analytics-surface-hubs/intune.png)

Intune Sincronizza le impostazioni di OMS hello quindi dispositivi hello nel gruppo di destinazione hello, registrali nell'area di lavoro OMS.

## <a name="connect-surface-hubs-toooms-using-hello-settings-app"></a>Connettersi tooOMS Surface hub utilizzando hello impostazioni app
Sarà necessario hello ID area di lavoro e la chiave dell'area di lavoro per l'area di lavoro OMS hello che gestirà gli hub di area. È possibile ottenere quelle dal portale OMS hello.

Se non si usa Intune toomanage l'ambiente, è possibile registrare dispositivi manualmente tramiti **impostazioni** su ogni Hub area:

1. Da Surface Hub aprire **Impostazioni**.
2. Immettere credenziali di amministratore del dispositivo hello quando richiesto.
3. Fare clic su **questo dispositivo**e hello in **monitoraggio**, fare clic su **configurare le impostazioni di OMS**.
4. Selezionare **Abilita monitoraggio**.
5. Nella finestra di dialogo Impostazioni di OMS hello, digitare hello **ID area di lavoro** e hello tipo **chiave dell'area di lavoro**.  
   ![impostazioni](./media/log-analytics-surface-hubs/settings.png)
6. Fare clic su **OK** configurazione hello toocomplete.

Viene visualizzato un messaggio di conferma per richiedere è o meno hello configurazione di OMS è stato applicato toohello dispositivo. Se è stato, viene visualizzato un messaggio che informa che l'agente di hello stabilita servizio OMS toohello. dispositivo Hello inizia quindi a inviare dati tooOMS in cui è possibile visualizzare e agire su di esso.

## <a name="monitor-surface-hubs"></a>Monitorare Surface Hub
Monitorare Surface Hub con OMS è molto simile all'attività di monitoraggio di qualsiasi altro dispositivo registrato.

1. Accedi toohello portale di OMS.
2. Passare i dashboard del pacchetto di soluzione toohello Surface Hub.
3. Viene visualizzata l'integrità del dispositivo.

   ![Dashboard di Surface Hub](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

È possibile creare [avvisi](log-analytics-alerts.md) in base alle ricerche log esistenti o personalizzate. Utilizza hello dati hello che OMS raccoglie dagli hub di area, è possibile cercare i problemi e di avviso in condizioni hello definite per i dispositivi.

## <a name="next-steps"></a>Passaggi successivi
* Utilizzare [Accedi ricerche Log Analitica](log-analytics-log-searches.md) tooview in dettaglio i dati di Surface Hub.
* Creare [avvisi](log-analytics-alerts.md) toonotify quando si verificano problemi con gli hub di area.
