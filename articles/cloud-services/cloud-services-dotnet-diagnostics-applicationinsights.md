---
title: Servizi Cloud con Application Insights aaaTroubleshoot | Documenti Microsoft
description: Informazioni su come servizio cloud tootroubleshoot problemi utilizzando i dati di Application Insights tooprocess da diagnostica di Azure.
services: cloud-services
documentationcenter: .net
author: sbtron
manager: timlt
editor: tysonn
ms.assetid: e93f387b-ef29-4731-ae41-0676722accb6
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: saurabh
ms.openlocfilehash: 972924d9e6d1fe33d5c19b006d482de52ffb0ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-services-using-application-insights"></a>Risoluzione dei problemi di Servizi Cloud tramite Application Insights
Con [Azure SDK 2.8](https://azure.microsoft.com/downloads/) ed estensione di diagnostica di Azure 1.5, è possibile inviare i dati di diagnostica di Azure per il servizio Cloud direttamente tooApplication Insights. Hello log raccolti da diagnostica di Azure&mdash;inclusi i log applicazioni, registri eventi di Windows, i log ETW e i contatori delle prestazioni&mdash;possono essere inviati tooApplication Insights. È quindi possibile visualizzare queste informazioni nell'interfaccia utente del portale Application Insights hello. È quindi possibile utilizzare hello Application Insights SDK tooget approfondite metriche e i registri che provengono da dell'applicazione, nonché sistema hello e a livello di infrastruttura, i dati provenienti da diagnostica di Azure.

## <a name="configure-azure-diagnostics-toosend-data-tooapplication-insights"></a>Configurare diagnostica Azure toosend dati tooApplication Insights
Seguire questi tooset passaggi backup il tooApplication dati relativo a cloud service progetto toosend diagnostica di Azure Insights.

1. In Esplora soluzioni di Visual Studio, fare doppio clic su un ruolo e scegliere **proprietà** progettazione ruoli di hello tooopen.

    ![Proprietà del ruolo di Esplora soluzioni][1]

2. In hello **diagnostica** sezione di progettazione ruoli hello, seleziona hello **inviare dati di diagnostica tooApplication Insights** opzione.

    ![Progettazione ruoli invia la diagnostica tooapplication comprensione dei dati][2]

3. In hello finestra di dialogo visualizzata selezionare risorsa di Application Insights hello che si desidera toosend hello Azure dati di diagnostica. la finestra di dialogo Hello consente tooselect una risorsa di Application Insights esistente dalla sottoscrizione o toomanually specificare una chiave di strumentazione per una risorsa di Application Insights. Per altre informazioni sulla creazione di una risorsa di Application Insights, vedere [Creare una nuova risorsa di Application Insights](../application-insights/app-insights-create-new-resource.md).

    ![selezionare una risorsa di Application Insights][3]

    Dopo aver aggiunto la risorsa di Application Insights hello, chiave di strumentazione hello per la risorsa viene archiviata come impostazione di configurazione del servizio con nome hello **APPINSIGHTS_INSTRUMENTATIONKEY**. È possibile modificare questa impostazione di configurazione per ogni configurazione del servizio o ambiente. toodo in tal caso, selezionare una configurazione diversa da hello **configurazione del servizio** elenco e specificare una nuova chiave di strumentazione per la configurazione.

    ![selezionare una configurazione del servizio][4]

    Hello **APPINSIGHTS_INSTRUMENTATIONKEY** impostazione di configurazione viene utilizzata dall'estensione di diagnostica di Visual Studio tooconfigure hello hello appropriato Application Insights informazioni sulle risorse durante la pubblicazione. impostazione di configurazione di Hello è un modo pratico di definizione di chiavi di strumentazione diversi per le configurazioni di servizio diverso. Visual Studio verrà convertire tale impostazione e inserirlo hello diagnostica configurazione pubblica dell'estensione hello durante il processo di pubblicazione. processo di hello toosimplify di configurazione dell'estensione di diagnostica hello con PowerShell, output del pacchetto hello da Visual Studio contiene anche hello pubblico XML di configurazione con chiave appropriata di strumentazione di Application Insights hello. file di configurazione pubblica Hello vengono creati nella cartella estensioni hello e seguire pattern hello *PaaSDiagnostics.&lt; RoleName&gt;. Paasdiagnostics.<NomeRuolo>.pubconfig.XML*. Tutte le distribuzioni basate su PowerShell possono usare toomap questo modello ogni ruolo di tooa di configurazione.

4) tooconfigure diagnostica Windows Azure toosend tutti i log a livello di errore e i contatori delle prestazioni raccolti da hello diagnostica Windows Azure agente tooApplication informazioni dettagliate, abilitare hello **inviare dati di diagnostica tooApplication Insights** opzione. 

    Se si desidera toofurther configurare quali dati vengono inviati tooApplication Insights, è necessario modificare manualmente hello *wadcfgx* file per ogni ruolo. Vedere [tooApplication dati di diagnostica di Azure configurare toosend Insights](#configure-azure-diagnostics-to-send-data-to-application-insights) toolearn ulteriori informazioni sull'aggiornamento manuale configurazione hello.

Quando il servizio di cloud hello è configurato toosend diagnostica Windows Azure dati tooapplication insights, è possibile distribuirlo tooAzure in genere, assicurandosi di hello estensione diagnostica di Azure è abilitata. Per altre informazioni, vedere [Pubblicazione di un servizio cloud di Azure con Visual Studio](../vs-azure-tools-publishing-a-cloud-service.md).  

## <a name="viewing-azure-diagnostics-data-in-application-insights"></a>Visualizzazione dei dati del servizio Diagnostica di Azure in Application Insights
Hello telemetria di diagnostica Azure viene visualizzato nella hello Application Insights risorsa configurata per il servizio cloud.

Mapping tra tipi di log di diagnostica Windows Azure concetti Insights tooApplication nei modi seguenti:

* I contatori delle prestazioni vengono visualizzati come metriche personalizzate in Application Insights.
* I registri eventi di Windows vengono visualizzati come tracce ed eventi personalizzati in Application Insights.
* I log applicazioni, i log ETW e gli eventuali log dell'infrastruttura di diagnostica vengono visualizzati come tracce in Application Insights.

tooview dati di diagnostica di Azure in Application Insights, effettuare una delle seguenti hello:

* Utilizzare [Esplora metriche](../application-insights/app-insights-metrics-explorer.md) toovisualize un miglioramento delle prestazioni personalizzato contatori o i conteggi di diversi tipi di eventi di registro eventi di Windows.

    ![Metriche personalizzate in Esplora metriche][5]

* Utilizzare [ricerca](../application-insights/app-insights-diagnostic-search.md) toosearch attraverso i registri di traccia hello inviato da diagnostica di Azure. Ad esempio, se un'eccezione non gestita ha causato toocrash ruolo hello e riciclo, informazioni sull'eccezione hello dell'elenco di hello *applicazione* canale di *registro eventi di Windows*. È possibile utilizzare ricerca toolook hello errore registro eventi di Windows e ottenere hello completo dello stack per determinare causa hello eccezione toohelp trova hello del problema hello.

    ![Cerca tracce][6]

## <a name="next-steps"></a>Passaggi successivi
* [Aggiungere il servizio cloud di hello Application Insights SDK tooyour](../application-insights/app-insights-cloudservices.md) toosend dati sulle richieste, eccezioni, dipendenze e qualsiasi telemetria personalizzata dall'applicazione. In combinazione con dati di diagnostica Azure hello, queste informazioni è possibile ottenere una visione completa dell'applicazione e del sistema, tutto in hello stessa risorsa di Application Insights.  

<!--Image references-->
[1]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/solution-explorer-properties.png
[2]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-sendtoappinsights.png
[3]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/select-appinsights-resource.png
[4]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-appinsights-serviceconfig.png
[5]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/metrics-explorer-custom-metrics.png
[6]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/search-windowseventlog-error.png
