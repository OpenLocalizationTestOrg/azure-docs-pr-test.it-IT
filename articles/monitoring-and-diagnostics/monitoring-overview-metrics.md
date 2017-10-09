---
title: aaaOverview di metriche in Microsoft Azure | Documenti Microsoft
description: Panoramica delle metriche e dei casi d'uso in Microsoft Azure
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 405ec51c-0946-4ec9-b535-60f65c4a5bd1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: johnkem
ms.openlocfilehash: 2b97f51e0554dae95a929241ae1f0e25e5c215ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Panoramica delle metriche in Microsoft Azure
In questo articolo vengono descritte le metriche in Microsoft Azure, le prestazioni e come utilizzarle toostart.  

## <a name="what-are-metrics"></a>Cosa sono le metriche?
Monitoraggio di Azure consente tooconsume telemetria toogain visibilità hello prestazioni e l'integrità dei carichi di lavoro in Azure. Hello più importanti dei dati di telemetria di Azure è metriche hello (detto anche i contatori delle prestazioni) generate da Azure più risorse. Monitoraggio di Azure offre diversi modi tooconfigure e utilizzare queste metriche per il monitoraggio e risoluzione dei problemi.

## <a name="what-can-you-do-with-metrics"></a>A cosa servono le metriche?
Le metriche sono fonte utile di telemetria e consentono di hello toodo seguenti attività:

* **Tenere traccia delle prestazioni di hello** della risorsa (ad esempio un'app di macchina virtuale, sito Web o logica) per tracciare la metrica in un grafico del portale e blocco dashboard tooa grafico.
* **Ricevere notifiche di un problema** che impatti hello delle prestazioni della risorsa quando una metrica supera una determinata soglia.
* **Configurare le azioni automatiche**, ad esempio la scalabilità automatica di una risorsa o la generazione di un runbook quando una metrica supera una determinata soglia.
* **Eseguire analisi avanzate** o creare report relativi alle tendenze delle prestazioni o di uso della risorsa.
* **Archivio** hello cronologia delle prestazioni o l'integrità della risorsa **per il controllo o di conformità** scopi.

## <a name="what-are-hello-characteristics-of-metrics"></a>Quali sono le caratteristiche di hello delle metriche?
Le metriche sono hello seguenti caratteristiche:

* Tutte le metriche hanno **frequenza di un minuto**. Si riceve un valore della metrica al minuto dalla risorsa, fornendo quasi in tempo reale visibilità nello stato di hello e l'integrità della risorsa.
* Le metriche sono **disponibili immediatamente**. Non necessario tooopt in oppure configurare ulteriori operazioni di diagnostica.
* Per ogni metrica è possibile accedere alla **cronologia degli ultimi 30 giorni** . È possibile esaminare rapidamente le tendenze recenti e mensili hello in prestazioni hello o l'integrità della risorsa.

È anche possibile:

* Configurare una metrica **avviso regola invia una notifica o accetta azione automatica** quando la metrica hello supera soglia hello che è stata impostata. La scalabilità automatica è un'azione automatica speciale che abilita tooscale le richieste in ingresso di risorse toomeet o carica le risorse di elaborazione di un sito Web. È possibile configurare un'impostazione regola tooscale in o out in base a una metrica oltrepassare la soglia di scalabilità automatica.

* **Route** tutte le metriche Analitica Log (OMS) o Application Insights tooenable immediata analitica, ricerca e avvisi personalizzati in dati di metrica dalle risorse. È inoltre possibile trasmettere le metriche tooan Hub eventi, consentendo toothen indirizzarle tooAzure flusso Analitica o toocustom App per l'analisi in tempo quasi reale. Impostare il flusso di Hub eventi usando le impostazioni di diagnostica.

* **Archiviare le metriche toostorage** per la conservazione più lungo o utilizzarli per report offline. È possibile indirizzare il tooAzure di metriche di archiviazione Blob quando si configurano impostazioni strumenti diagnostici per la risorsa.

* Individuare facilmente, accedere, e **consente di visualizzare tutte le metriche** tramite hello portale di Azure quando si seleziona una risorsa e tracciare hello metriche in un grafico.

* **Utilizzare** metriche hello tramite hello nuove API REST monitoraggio di Azure.

* **Query** metriche utilizzando hello i cmdlet di PowerShell o hello API REST e multipiattaforma.

  ![Reindirizzamento delle metriche nel monitoraggio di Azure](./media/monitoring-overview-metrics/Metrics_Overview_v4.png)

## <a name="access-metrics-via-hello-portal"></a>Metriche di accesso tramite il portale di hello
Ecco una rapida procedura dettagliata di come toocreate un grafico utilizzando metrica hello portale di Azure.

### <a name="tooview-metrics-after-creating-a-resource"></a>metriche tooview dopo la creazione di una risorsa
1. Hello aprirlo portale di Azure.
2. Creare un sito Web per il Servizio app di Azure.
3. Dopo aver creato un sito Web, visitare toohello **Panoramica** pannello del sito Web di hello.
4. È possibile visualizzare nuove metriche come un riquadro **Monitoraggio**. È quindi possibile modificare il riquadro hello e selezionare altre metriche.

   ![Metriche su una risorsa nel monitoraggio di Azure](./media/monitoring-overview-metrics/MetricsOverview1.png)

### <a name="tooaccess-all-metrics-in-a-single-place"></a>tooaccess tutte le metriche in un'unica posizione
1. Hello aprirlo portale di Azure.
2. Passare di nuovo toohello **monitoraggio** scheda e quindi e seleziona hello **metriche** opzione disponibili al suo interno.
3. Selezionare la sottoscrizione, un gruppo di risorse e un nome hello della risorsa di hello dall'elenco a discesa hello.
4. Elenco di visualizzazione hello le metriche disponibili. Selezionare quindi metrica hello si è interessati e traccia il.
5. È possibile aggiungere dashboard toohello facendo hello pin nell'angolo superiore destro di hello.

   ![Accedere a tutte le metriche in un'unica posizione nel monitoraggio di Azure](./media/monitoring-overview-metrics/MetricsOverview2.png)

> [!NOTE]
> È possibile accedere alle metriche a livello di host dalle VM (basate su Azure Resource Manager) e dai set di scalabilità di macchine virtuali senza altre eventuali configurazioni di diagnostica. Queste nuove metriche a livello di host sono disponibili per le istanze di Windows e Linux. Queste metriche non sono toobe confusa con hello metriche a livello di sistema operativo Guest che si dispone di accesso toowhen che attivare la diagnostica di Azure nel set di scalabilità di macchine virtuali o le macchine virtuali. toolearn più sulla configurazione di diagnostica, vedere [che cos'è Microsoft Azure Diagnostics](../azure-diagnostics.md).
>
>

## <a name="access-metrics-via-hello-rest-api"></a>Accedere alle metriche tramite hello API REST
Le metriche di Azure sono accessibili tramite le API di monitoraggio di Azure hello. Sono due le API che consentono di rilevare le metriche e accedervi:

* Hello utilizzare [le definizioni di metrica di monitoraggio di Azure API REST](https://msdn.microsoft.com/library/mt743621.aspx) tooaccess hello elenco delle metriche disponibili per un servizio.
* Hello utilizzare [API REST di metriche di monitoraggio di Azure](https://msdn.microsoft.com/library/mt743622.aspx) tooaccess hello dati di metrica effettivo.

> [!NOTE]
> Questo articolo vengono illustrate le metriche di hello tramite hello [nuova API per le metriche](https://msdn.microsoft.com/library/dn931930.aspx) per le risorse di Azure. versione dell'API per definizioni di metrica nuovo hello API Hello è 2016-03-01 e versione di hello per le API di metriche è 01 / 09 / 2016. le metriche e definizioni di metrica legacy hello accessibili con hello API versione 2014-04-01.
>
>

Per una più dettagliata utilizzando hello API REST di monitoraggio di Azure, vedere [procedura dettagliata di API REST di Azure monitoraggio](monitoring-rest-api-walkthrough.md).

## <a name="export-metrics"></a>Esportare le metriche
È possibile passare toohello **le impostazioni di diagnostica** pannello hello **monitoraggio** scheda e visualizzazione opzioni di esportazione hello per le metriche. È possibile selezionare metriche (e i log di diagnostica) toobe indirizzato archiviazione tooBlob, hub eventi tooAzure o tooOMS per casi d'uso che sono stati indicati in precedenza in questo articolo.

 ![Opzioni di esportazione per le metriche nel monitoraggio di Azure](./media/monitoring-overview-metrics/MetricsOverview3.png)

È possibile configurare questa opzione tramite i modelli di Resource Manager, [PowerShell](insights-powershell-samples.md), l'[interfaccia della riga di comando di Azure](insights-cli-samples.md) o l'[API REST](https://msdn.microsoft.com/library/dn931943.aspx).

## <a name="take-action-on-metrics"></a>Eseguire operazioni sulle metriche
le notifiche tooreceive o intraprendere automatizzata azioni sui dati di metrica, è possibile configurare le regole di avviso o impostazioni di scalabilità automatica.

### <a name="configure-alert-rules"></a>Configurare regole di avviso
È possibile configurare le regole di avviso sulle metriche. Queste regole di avviso possono verificare se una metrica ha superato una determinata soglia. Possono quindi ricevere una notifica tramite posta elettronica o attivare un webhook che può essere utilizzati toorun qualsiasi script personalizzato. È possibile utilizzare anche le integrazioni di hello webhook tooconfigure prodotto di terze parti.

 ![Metriche e regole di avviso nel monitoraggio di Azure](./media/monitoring-overview-metrics/MetricsOverview4.png)

### <a name="autoscale-your-azure-resources"></a>Ridimensionare automaticamente le risorse di Azure
Alcune risorse di Azure supportano hello scala o di più istanze toohandle i carichi di lavoro. Scalabilità automatica applica tooApp servizio (app Web), il set di scalabilità di macchine virtuali e servizi Cloud di Azure classico. È possibile configurare tooscale regole di scalabilità automatica o l'estrazione quando una metrica determinata che influisce sul carico di lavoro supera una soglia specificata. Per ulteriori informazioni, vedere [Panoramica della scalabilità automatica](monitoring-overview-autoscale.md).

 ![Metriche e ridimensionamento automatico nel Monitoraggio di Azure](./media/monitoring-overview-metrics/MetricsOverview5.png)

## <a name="learn-about-supported-services-and-metrics"></a>Altre informazioni su metriche e servizi supportati
Il monitoraggio di Azure è una nuova infrastruttura di metriche. Supporta hello seguenti servizi di Azure in hello Azure portal e hello nuova versione di hello API di monitoraggio di Azure:

* VM (basate su Azure Resource Manager)
* set di scalabilità di macchine virtuali
* Batch
* Spazio dei nomi di Hub eventi
* Spazio dei nomi del bus di servizio (solo SKU premium)
* Database SQL (versione 12)
* Pool SQL elastico
* Siti Web
* Server farm Web
* App per la logica
* Hub IoT
* Cache Redis
* Rete: gateway applicazione
* Ricerca

È possibile visualizzare un elenco dettagliato di tutti i servizi di hello supportato e le metriche a [metriche di monitoraggio di Azure - metriche supportate per ogni tipo di risorsa](monitoring-supported-metrics.md).

## <a name="next-steps"></a>Passaggi successivi
Vedere i collegamenti toohello in questo articolo. In più, è possibile ottenere informazioni su:  

* [Metriche comuni per il ridimensionamento automatico](insights-autoscale-common-metrics.md)
* [Come le regole di avviso toocreate](insights-alerts-portal.md)
* [Analizzare i log di Archiviazione di Azure con Log Analytics](../log-analytics/log-analytics-azure-storage.md)
