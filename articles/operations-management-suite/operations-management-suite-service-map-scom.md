---
title: integrazione di mappa con System Center Operations Manager aaaService | Documenti Microsoft
description: "Mappa del servizio è una soluzione di Operations Management Suite che individua automaticamente i componenti dell'applicazione in Windows e mappe e i sistemi Linux hello la comunicazione tra servizi. In questo articolo viene illustrato l'utilizzo di mapping servizio tooautomatically creare diagrammi di applicazione distribuita in Operations Manager."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: cff9cce2559448ec3a5fd14087b867f314716560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a>Integrazione di Elenco dei servizi con System Center Operations Manager
  > [!NOTE]
  > Questa funzionalità è disponibile in anteprima pubblica.
  > 
  
Mappa del servizio Operations Management Suite consente di individuare i componenti dell'applicazione nei sistemi Windows e Linux e automaticamente la comunicazione tra servizi hello viene eseguito il mapping. Mappa del servizio consente tooview intralcio hello server immaginano, come sistemi interconnessi che offrono servizi critici. Mappa del servizio Mostra le connessioni tra server, i processi e le porte attraverso qualsiasi architettura connesso TCP, senza alcuna configurazione oltre all'installazione di hello di un agente. Per ulteriori informazioni, vedere hello [documentazione mappa del servizio](operations-management-suite-service-map.md).

L'integrazione tra System Center Operations Manager e di mappa del servizio, è possibile creare automaticamente i diagrammi di applicazione distribuita in Operations Manager che si basano sulle mappe di dipendenze dinamiche hello nella mappa del servizio.

## <a name="prerequisites"></a>Prerequisiti
* Gruppo di gestione di Operations Manager che gestisce un set di server.
* Un'area di lavoro Operations Management Suite con hello soluzione mappa del servizio abilitata.
* Un set di server (almeno) che sono gestiti da Operations Manager e tooService l'invio di dati della mappa. Sono supportati server Windows e Linux.
* Un'entità servizio con accesso toohello sottoscrizione di Azure associato dell'area di lavoro di hello Operations Management Suite. Per ulteriori informazioni, visitare troppo[creare un'entità servizio](#creating-a-service-principal).

## <a name="install-hello-service-map-management-pack"></a>Installare il management pack di hello mappa del servizio
Abilitare l'integrazione di hello tra Operations Manager e di mapping servizio importando il bundle hello Microsoft.SystemCenter.ServiceMap management pack (Microsoft.SystemCenter.ServiceMap.mpb). bundle Hello contiene hello seguenti management pack:
* Microsoft Service Map Application Views
* Microsoft System Center Service Map Internal
* Microsoft System Center Service Map Overrides
* Microsoft System Center Service Map

## <a name="configure-hello-service-map-integration"></a>Configurare l'integrazione di hello mappa del servizio
Dopo l'installazione di management pack di hello mappa del servizio, un nuovo nodo **mappa del servizio**, viene visualizzato in **Operations Management Suite** in hello **amministrazione** riquadro. 

integrazione di mappa del servizio, tooconfigure hello seguenti:

1. tooopen hello configurazione guidata, in hello **Cenni preliminari sulla mappa servizio** riquadro, fare clic su **aggiunta area di lavoro**.  

    ![Riquadro Service Map Overview (Panoramica di Elenco dei servizi)](media/oms-service-map/scom-configuration.png)

2. In hello **configurazione della connessione** , immettere il nome di tenant hello o ID, ID dell'applicazione (noto anche come nome utente hello o clientID) e la password dell'entità servizio hello e quindi fare clic su **Avanti**. Per ulteriori informazioni, visitare troppo[creare un'entità servizio](#creating-a-service-principal).

    ![finestra di configurazione della connessione Hello](media/oms-service-map/scom-config-spn.png)

3. In hello **selezione sottoscrizione** , selezionare hello sottoscrizione di Azure, il gruppo di risorse di Azure (Buongiorno uno che contiene l'area di lavoro Operations Management Suite hello) e dell'area di lavoro di Operations Management Suite e quindi fare clic su **Avanti**.

    ![area di lavoro di Operations Manager configurazione Hello](media/oms-service-map/scom-config-workspace.png)

4. In hello **selezione gruppo di computer** finestra, si sceglie di quali gruppi di computer mappa servizio desiderato toosync tooOperations Manager. Fare clic su **Aggiungi/Rimuovi gruppi di computer**, scegliere i gruppi dall'elenco di hello di **gruppi di computer disponibili**, fare clic su **Aggiungi**.  Dopo aver selezionato i gruppi, fare clic su **Ok** toofinish.
    
    ![Hello gruppi di computer configurazione di Operations Manager](media/oms-service-map/scom-config-machine-groups.png)
    
5. In hello **selezione Server** finestra configuri hello gruppo di server mappa servizio con server hello che si desidera toosync tra Operations Manager e mappa del servizio. Fare clic su **Aggiungi/Rimuovi server**.   
    
    Per hello integrazione toobuild un diagramma applicazioni distribuite per un server, devono essere server hello:

    * Gestito da Operations Manager
    * Gestito da Mapping dei servizi
    * Elencato nel gruppo di server mappa servizio hello

    ![Hello il gruppo di configurazione di Operations Manager](media/oms-service-map/scom-config-group.png)

6. Facoltativo: Selezionare hello toocommunicate pool risorse di Server di gestione con Operations Management Suite e quindi fare clic su **Aggiungi area di lavoro**.

    ![Hello Pool di risorse configurazione di Operations Manager](media/oms-service-map/scom-config-pool.png)

    Potrebbe richiedere un minuto tooconfigure e registrare l'area di lavoro di hello Operations Management Suite. Una volta configurato, Operations Manager Avvia sincronizzazione mappa del servizio prima di hello da Operations Management Suite.

    ![Hello Pool di risorse configurazione di Operations Manager](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a>Monitorare le metriche del servizio
Dopo la connessione dell'area di lavoro di hello Operations Management Suite, una nuova cartella, mappa del servizio, viene visualizzata in hello **monitoraggio** riquadro della console di Operations Manager hello.

![riquadro monitoraggio di Operations Manager Hello](media/oms-service-map/scom-monitoring.png)

cartella di mapping servizio Hello con quattro nodi:
* **Gli avvisi attivi**: Elenca tutti gli avvisi attivi hello sulla comunicazione hello tra Operations Manager e mappa del servizio.  Si noti che questi avvisi non viene sincronizzata tooOperations Manager gli avvisi di Operations Management Suite. 

* **Server**: Elenca i server monitorato hello che sono configurati toosync dalla mappa del servizio.

    ![riquadro server di monitoraggio di Operations Manager Hello](media/oms-service-map/scom-monitoring-servers.png)

* **Machine Group Dependency Views** (Visualizzazioni dipendenze gruppi di computer): elenca tutti i gruppi di computer sincronizzati da Mapping dei servizi. È possibile scegliere qualsiasi tooview gruppo diagramma relativa applicazione distribuita.

    ![diagramma di applicazione distribuita di Operations Manager Hello](media/oms-service-map/scom-group-dad.png)

* **Server Dependency Views** (Visualizzazioni dipendenze server): elenca tutti i server sincronizzati da Elenco dei servizi. È possibile scegliere qualsiasi tooview server diagramma relativa applicazione distribuita.

    ![diagramma di applicazione distribuita di Operations Manager Hello](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-hello-workspace"></a>Modificare o eliminare l'area di lavoro hello
È possibile modificare o eliminare workspace hello configurato mediante hello **Cenni preliminari sulla mappa servizio** riquadro (**amministrazione** riquadro > **Operations Management Suite**  >  **Mappa del servizio**). Attualmente è possibile configurare una sola area di lavoro di Operations Management Suite.

![riquadro area di modifica di Operations Manager Hello](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a>Configurare regole e override
Una regola, _Microsoft.SystemCenter.ServiceMapImport.Rule_, viene creato le informazioni di recupero tooperiodically dalla mappa del servizio. gli intervalli di tempo di sincronizzazione toochange, è possibile configurare gli override della regola hello (**Authoring** riquadro > **regole** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).

![finestra proprietà di Operations Manager esegue l'override di Hello](media/oms-service-map/scom-overrides.png)

* **Enabled**: abilita/disabilita gli aggiornamenti automatici. 
* **IntervalMinutes**: hello tempo tra gli aggiornamenti di ripristino. intervallo predefinito di Hello è un'ora. Se si desidera toosync server mappe più di frequente, è possibile modificare il valore di hello.
* **Valori di TimeoutSeconds**: reimpostare lunghezza hello del tempo prima del timeout della richiesta hello. 
* **TimeWindowMinutes**: reimpostazione hello di intervallo di tempo per eseguire query sui dati. Il valore predefinito è una finestra temporale di 60 minuti. valore di Hello massimo consentito dalla mappa del servizio è 60 minuti.

## <a name="known-issues-and-limitations"></a>Problemi noti e limitazioni

progettazione corrente Hello presenta la seguente hello problemi e limitazioni:
* È possibile connettersi solo tooa singola area di lavoro di Operations Management Suite.
* Sebbene sia possibile aggiungere server toohello, gruppo di server mappa servizio manualmente tramite hello **Authoring** riquadro hello mappe per tali server non vengono sincronizzate immediatamente.  Essi verranno sincronizzate dalla mappa del servizio durante il successivo ciclo di sincronizzazione hello.
* Se si apportano modifiche toohello Distributed diagrammi applicazioni creati dal management pack di hello, tali modifiche verranno sovrascritte probabilmente nella sincronizzazione successiva di hello con mappa del servizio.

## <a name="create-a-service-principal"></a>Creare un’entità servizio
Per la documentazione ufficiale di Azure sulla creazione di un'entità servizio, vedere:
* [Create a service principal by using PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal) (Creare un'entità servizio usando PowerShell)
* [Create a service principal by using Azure CLI](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli) (Creare un'entità servizio usando Azure CLI)
* [Creare un'entità servizio utilizzando hello portale di Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a>Commenti e suggerimenti
Per inviare commenti su Mapping dei servizi e sulla relativa documentazione, Vedere la [pagina per i suggerimenti degli utenti](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), in cui è possibile suggerire funzionalità o votare i suggerimenti esistenti.
