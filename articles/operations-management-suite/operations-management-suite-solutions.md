---
title: aaaSolutions Operations Management Suite (OMS) | Documenti Microsoft
description: "Soluzioni di estendono le funzionalità di hello di Operations Management Suite (OMS), fornendo gli scenari di gestione di pacchetti che è possibile aggiungere l'area di lavoro OMS tootheir.  Questo articolo fornisce informazioni dettagliate sulle soluzioni personalizzate create dai clienti e dai partner."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5b5a538f1bc4b5577bec94db08bd43668bc6584a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-management-solutions-in-operations-management-suite-oms-preview"></a>Utilizzo di soluzioni di gestione in Operations Management Suite (OMS) (anteprima)
> [!NOTE]
> Questa è una documentazione preliminare per le soluzioni di gestione in OMS attualmente disponibili in versione di anteprima.    
> 
> 

Soluzioni di gestione estendono le funzionalità di hello di Operations Management Suite (OMS), fornendo gli scenari di gestione di pacchetti che è possibile aggiungere tootheir ambiente.  Inoltre troppo[soluzioni fornite da Microsoft](../log-analytics/log-analytics-add-solutions.md), partner e i clienti possono creare toobe soluzioni di gestione utilizzato nel proprio ambiente o resi disponibili toocustomers tramite community hello.

## <a name="finding-and-installing-management-solutions"></a>Ricerca e installazione di soluzioni di gestione
Sono disponibili più metodi per l'individuazione e l'installazione di soluzioni di gestione, come descritto in hello le sezioni seguenti.

### <a name="azure-marketplace"></a>Azure Marketplace
Soluzioni di gestione fornito da Microsoft e partner attendibili possono essere installati da hello Azure Marketplace in hello portale di Azure.

1. Accedi toohello portale di Azure.
2. Nel riquadro sinistro hello selezionare **più servizi**.
3. Uno scorrere verso il basso troppo**soluzioni** o tipo *soluzioni* in hello **filtro** finestra di dialogo.
4. Fare clic su hello **+ Aggiungi** pulsante.
5. Cercare le soluzioni che si sono interessati tramite esplorazione, fare clic su hello **filtro** pulsante o la digitazione hello **ricerca tutto** casella.
6. Fare clic su un tooview elemento marketplace, le informazioni dettagliate.
7. Fare clic su **crea** tooopen hello **Aggiungi soluzione** riquadro.
8. Sarà toorequired richiesta informazioni, ad esempio hello [OMS dell'area di lavoro e account di automazione](#oms-workspace-and-automation-account) inoltre toovalues per i parametri in hello soluzione.
9. Fare clic su **crea** soluzione hello tooinstall.

### <a name="oms-portal"></a>Portale di OMS
Soluzioni di gestione fornite da Microsoft possono essere installate da hello Solutions Gallery nel portale OMS hello.

1. Accedi toohello portale di OMS.
2. Fare clic su hello **Solutions Gallery** riquadro.
3. Nella pagina Solutions Gallery di OMS hello ottenere informazioni su ogni soluzione disponibile. Fare clic su nome hello della soluzione di hello che si desidera tooadd tooOMS.
4. Nella pagina hello soluzione hello scelto, verranno visualizzate informazioni dettagliate sulla soluzione hello. Fare clic su **Aggiungi**.
5. Un nuovo riquadro per la soluzione hello aggiunto viene visualizzato nella pagina Overview di OMS hello e iniziare a usarla dopo che il servizio OMS hello elabora i dati.

### <a name="azure-quickstart-templates"></a>Modelli di Guida introduttiva di Azure
I membri della community di hello possono inviare tooAzure soluzioni di gestione modelli di avvio rapido.  È possibile scaricare questi modelli per l'installazione di versioni successive o verificarli toolearn come troppo[creare soluzioni personalizzate](#creating-a-solution).

1. Seguire il processo di hello descritto in [OMS dell'area di lavoro e account di automazione](#oms-workspace-and-automation-account) toolink un'area di lavoro e account.
2. Andare troppo[modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/).  
3. Cercare una soluzione adatta alle proprie esigenze.
4. Selezionare soluzione hello hello risultati tooview i dettagli.
5. Fare clic su hello **distribuire tooAzure** pulsante.
6. Sarà tooprovide richiesta informazioni, ad esempio il gruppo di risorse hello e il percorso nella toovalues aggiunta per i parametri nella soluzione hello.
7. Fare clic su **acquisto** soluzione hello tooinstall.

### <a name="deploy-azure-resource-manager-template"></a>Distribuire un modello di Azure Resource Manager
Soluzioni che si ottiene dalla community di hello o che sono stati [creare autonomamente](#creating-a-solution) vengono implementati come un modello di gestione risorse ed è possibile utilizzare uno dei metodi standard di hello per [distribuzione di un modello](../azure-resource-manager/resource-group-template-deploy-portal.md).  Si noti che prima di installare la soluzione hello, è necessario creare e collegare hello [OMS dell'area di lavoro e account di automazione](#oms-workspace-and-automation-account).

## <a name="oms-workspace-and-automation-account"></a>Area di lavoro OMS e account di Automazione
La maggior parte delle soluzioni di gestione richiedono un [area di lavoro OMS](../log-analytics/log-analytics-manage-access.md) toocontain viste e un [account di automazione](../automation/automation-security-overview.md#automation-account-overview) toocontain runbook e le relative risorse. Hello dell'area di lavoro e l'account deve soddisfare i seguenti requisiti hello.

* Una soluzione può usare solo un'area di lavoro OMS e un account di Automazione.  
* Hello area di lavoro OMS e account di automazione utilizzato da una soluzione devono essere tooone collegato un altro. Un'area di lavoro OMS può essere solo account di automazione di tooone collegato e un account di automazione può essere solo l'area di lavoro OMS tooone collegato.
* toobe collegato, hello area di lavoro OMS e account deve trovarsi in automazione hello allo stesso gruppo di risorse e area.  eccezione di Hello è un'area di lavoro OMS nell'area Stati Uniti orientali ed e l'account di automazione in Stati Uniti orientali 2.

### <a name="creating-a-link-between-an-oms-workspace-and-automation-account"></a>Creazione di un collegamento tra un'area di lavoro OMS e un account di Automazione
Come specificare l'area di lavoro OMS hello e account di automazione dipende dal metodo di installazione di hello per la soluzione.

* Quando si installa una soluzione Microsoft tramite il portale di OMS hello, viene installato nell'area di lavoro OMS corrente hello e nessun account di automazione è obbligatorio.
* Quando si installa una soluzione attraverso hello Azure Marketplace, richiesto per un'area di lavoro OMS e account di automazione e viene creato il collegamento hello tra di essi.  
* Per le soluzioni di fuori di hello Azure Marketplace, è necessario collegare l'area di lavoro OMS hello e account di automazione prima di installare la soluzione hello.  Tale scopo, è possibile selezionare qualsiasi soluzione in hello Azure Marketplace e area di lavoro OMS hello e account di automazione.  Non è necessario tooactually installare soluzione hello in quanto verrà creato il collegamento hello come area di lavoro OMS hello e account di automazione sono selezionati.  Una volta creato il collegamento hello, è possibile utilizzare tale area di lavoro OMS e account di automazione per una soluzione. 

### <a name="verifying-hello-link-between-an-oms-workspace-and-automation-account"></a>Verifica collegamento hello tra un'area di lavoro OMS e account di automazione
È possibile verificare hello collegamento tra un'area di lavoro OMS e un account di automazione mediante hello seguente procedura.

1. Selezionare l'account di automazione hello in hello portale di Azure.
2. Scorri toohello alla fine di hello **impostazioni** riquadro.
3. Se è presente una sezione denominata **le risorse di OMS** in hello **impostazioni** riquadro, questo account è l'area di lavoro OMS tooan associata.
4. Selezionare **dell'area di lavoro** dettagli hello tooview dell'area di lavoro OMS hello collegato toothis account di automazione.

## <a name="listing-management-solutions"></a>Creazione di un elenco delle soluzioni di gestione
Utilizzare hello seguenti soluzioni di gestione di procedure tootooview hello in hello aree di lavoro collegato tooyour sottoscrizione di Azure.

1. Accedi toohello portale di Azure.
2. Nel riquadro sinistro hello selezionare **più servizi**.
3. Uno scorrere verso il basso troppo**soluzioni** o tipo *soluzioni* in hello **filtro** finestra di dialogo.
4. Verranno elencate le soluzioni installate in tutte le aree di lavoro.

Si noti che è possibile visualizzare solo le soluzioni Microsoft hello installate hello nell'area di lavoro tramite il portale di OMS hello.

## <a name="removing-a-management-solution"></a>Rimozione di una soluzione di gestione
Quando una soluzione di gestione viene rimosso, vengono rimosse anche tutte le risorse nella soluzione hello.  

1. Individuare la soluzione hello in hello Azure portale utilizzando la procedura hello in [elenco soluzioni](#listing-solutions).
2. Selezionare soluzione hello da tooremove.
3. Fare clic su hello **eliminare** pulsante.

## <a name="creating-a-management-solution"></a>Creazione di una soluzione di gestione
Istruzioni complete sulla creazione di soluzioni di gestione sono disponibili nell'articolo [Creazione di soluzioni in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md). 

## <a name="next-steps"></a>Passaggi successivi
* Cercare i [modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates) per esempi di modelli di Resource Manager.
* Creare [soluzioni di gestione](operations-management-suite-solutions-creating.md) personalizzate.

