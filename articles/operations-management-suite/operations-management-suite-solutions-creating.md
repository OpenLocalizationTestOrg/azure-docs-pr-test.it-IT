---
title: una soluzione di gestione in OMS aaaBuild | Documenti Microsoft
description: "Soluzioni di gestione estendono le funzionalità di hello di Operations Management Suite (OMS), fornendo gli scenari di gestione di pacchetti che è possibile aggiungere l'area di lavoro OMS tootheir.  Questo articolo fornisce informazioni dettagliate su come creare toobe di soluzioni di gestione utilizzato nel proprio ambiente o resi disponibili tooyour clienti."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dea4c0d9e608d9fe4aa41088705958c9fe999372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-build-a-management-solution-in-operations-management-suite-oms-preview"></a>Progettare e creare una soluzione di gestione in Operations Management Suite (OMS) (anteprima)
> [!NOTE]
> Questa è una documentazione preliminare per la creazione di soluzioni di gestione in OMS attualmente disponibili in versione di anteprima. Qualsiasi schema descritto di seguito è soggetto toochange.

[Soluzioni di gestione](operations-management-suite-solutions.md) estendere le funzionalità di hello di Operations Management Suite (OMS), fornendo gli scenari di gestione di pacchetti che è possibile aggiungere l'area di lavoro OMS tootheir.  In questo articolo presenta toodesign un processo di base e compilare una soluzione di gestione che è adatta per i requisiti più comuni.  Se sei nuove soluzioni di gestione toobuilding è possibile utilizzare questo processo come punto di partenza e quindi sfruttare i concetti di hello per le soluzioni più complesse come l'evolversi delle esigenze.

## <a name="what-is-a-management-solution"></a>Che cos'è una soluzione di gestione?

Soluzioni di gestione contenuto OMS e risorse di Azure che interagiscono tra di loro tooachieve un particolare scenario di monitoraggio.  Sono implementati come [modelli di gestione delle risorse](../azure-resource-manager/resource-manager-template-walkthrough.md) che contengono informazioni dettagliate su come tooinstall e configurare le risorse contenute, quando si installa la soluzione hello.

Hello strategia di base è la soluzione di gestione di toostart compilando i singoli componenti di hello nell'ambiente Azure.  Dopo aver creato la funzionalità di hello funziona correttamente, quindi iniziare a creare il pacchetto in un [file di soluzione di gestione](operations-management-suite-solutions-solution-file.md). 


## <a name="design-your-solution"></a>Progettare la soluzione
modello più comune di Hello per una soluzione di gestione viene illustrata nel seguente diagramma hello.  diversi componenti di Hello in questo modello sono descritti nella seguente hello.

![Panoramica della soluzione OMS](media/operations-management-suite-solutions/solution-overview.png)


### <a name="data-sources"></a>Origini dati
primo passaggio di Hello nella progettazione di una soluzione consiste nel determinare dati hello necessari dal repository Log Analitica hello.  Questi dati possono essere raccolti da un [origine dati](../log-analytics/log-analytics-data-sources.md) o [un'altra soluzione](operations-management-suite-solutions.md), o la soluzione potrebbe essere necessario tooprovide hello processo toocollect è.

Sono presenti origini dati che possono essere raccolti nell'archivio di Log Analitica hello, come descritto in diversi modi [origini dati nel Log Analitica](../log-analytics/log-analytics-data-sources.md).  Ciò include gli eventi nel registro eventi di Windows hello o generati da Syslog inoltre tooperformance contatori per i client Windows e Linux.  È possibile anche raccogliere dati dalle risorse di Azure raccolte da Monitoraggio di Azure.  

Se si richiedono dati che non sono accessibili tramite una delle origini dati disponibili hello, quindi è possibile utilizzare hello [API dell'agente di raccolta dati di HTTP](../log-analytics/log-analytics-data-collector-api.md) che consentono di toowrite repository Analitica Log toohello dei dati da qualsiasi client che è possibile chiamare un resto API.  Hello viene in genere di raccolta dati personalizzati in una soluzione di gestione toocreate un [runbook in automazione di Azure](../automation/automation-runbook-types.md) che raccoglie i dati di hello richiesto dalle risorse di Azure o esterne e Usa hello toowrite API dell'agente di raccolta dati toohello repository.  

### <a name="log-searches"></a>Ricerche log
[Log delle ricerche](../log-analytics/log-analytics-log-searches.md) vengono utilizzati tooextract e analizzare i dati nel repository di hello Analitica di Log.  Vengono utilizzati per le visualizzazioni e avvisi in aggiunta tooallowing hello utente tooperform analisi ad hoc dei dati nel repository di hello.  

È necessario definire le query che si ritiene risulteranno utili toohello utente anche se non vengono usati da tutte le viste o avvisi.  Questi saranno disponibili toothem come ricerche salvate nel portale di hello ed è anche possibile includere in un [parte di visualizzazione elenco di query](../log-analytics/log-analytics-view-designer-parts.md#list-of-queries-part) nella propria visualizzazione personalizzata.

### <a name="alerts"></a>Avvisi
[Gli avvisi nel registro Analitica](../log-analytics/log-analytics-alerts.md) identificare i problemi tramite [log ricerche](#log-searches) rispetto ai dati hello nel repository di hello.  Si notifica utente hello o eseguire automaticamente un'azione in risposta. Occorre identificare le diverse condizioni di avviso per l'applicazione e includere le regole di avviso corrispondenti nel file della soluzione.

Se il problema di hello possa potenzialmente essere risolto con un processo automatizzato, quindi in genere creerai un runbook in automazione di Azure tooperform questa correzione.  È possono gestire con servizi di Azure più [cmdlet](/powershell/azure/overview) quali runbook hello utilizzare tooperform tale funzionalità.

Se la soluzione richiede funzionalità esterne nell'avviso tooan risposta, quindi è possibile utilizzare un [webhook risposta](../log-analytics/log-analytics-alerts-actions.md).  In questo modo si toocall un servizio web esterno, l'invio di informazioni da avviso hello.

### <a name="views"></a>Visualizzazioni
Le visualizzazioni nel Log Analitica sono dati toovisualize utilizzati dall'archivio di Log Analitica hello.  Ogni soluzione conterrà in genere una singola visualizzazione con un [riquadro](../log-analytics/log-analytics-view-designer-tiles.md) visualizzato nel dashboard principale dell'utente hello.  visualizzazione di Hello può contenere un numero qualsiasi di [parti visualizzazione](../log-analytics/log-analytics-view-designer-parts.md) tooprovide visualizzazioni diverse dell'utente di toohello hello i dati raccolti.

Si [creare visualizzazioni personalizzate utilizzando Progettazione vista hello](../log-analytics/log-analytics-view-designer.md) che è possibile esportare in un secondo momento per l'inclusione nel file di soluzione.  


## <a name="create-solution-file"></a>Creare il file di soluzione
Dopo aver configurato e testato i componenti di hello che faranno parte della soluzione, è possibile [creare il file di soluzione](operations-management-suite-solutions-solution-file.md).  Si implementerà i componenti della soluzione hello in un [modello di gestione risorse](../azure-resource-manager/resource-group-authoring-templates.md) che include un [risorse della soluzione](operations-management-suite-solutions-solution-file.md#solution-resource) con toohello relazioni tra le altre risorse hello file.  


## <a name="test-your-solution"></a>Testare la soluzione personalizzata
Mentre si sviluppa la soluzione, sarà anche necessario tooinstall e testarlo nell'area di lavoro.  È possibile farlo usando uno dei metodi disponibili hello troppo[verificare e installare i modelli di gestione risorse](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="publish-your-solution"></a>Pubblicare la soluzione
Dopo aver completato e testare la soluzione, è possibile renderlo disponibile toocustomers tramite entrambe le seguenti origini di hello.

- **Modelli di avvio rapido di Azure**.  [Modelli di avvio rapido di Azure](https://azure.microsoft.com/resources/templates/) è un set di modelli di gestione risorse fornito dalla community di hello tramite GitHub.  È possibile rendere disponibile la soluzione per le informazioni seguenti in hello [Guida alla collaborazione su](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE).
- **Azure Marketplace**.  Hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/) consente toodistribute e vendere la soluzione tooother sviluppatori, fornitori di software indipendenti e i professionisti IT.  È possibile ottenere informazioni come toopublish il tooAzure Esplora Marketplace in [come toopublish e gestire un'offerta in hello Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md).



## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[creare un file di soluzione](operations-management-suite-solutions-solution-file.md) per la soluzione di gestione.
* Informazioni sul supporto di hello [modelli Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).
* Cercare i [modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates) per esempi di modelli di Resource Manager.