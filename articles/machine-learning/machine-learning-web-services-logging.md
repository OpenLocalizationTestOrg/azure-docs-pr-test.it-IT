---
title: aaaLogging per servizi web Machine Learning | Documenti Microsoft
description: Informazioni su come servizi web registrazione tooenable per Machine Learning. Registrazione fornisce informazioni aggiuntive toohelp risolvere hello API.
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: ed23933d52d2151af658af2307d7df8743071f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a>Abilitare la registrazione per i servizi Web di Machine Learning
Questo documento vengono fornite informazioni su hello registrazione delle funzionalità di servizi web Machine Learning. Registrazione fornisce informazioni aggiuntive, oltre a un numero di errore e un messaggio, che consentono di risolvere i problemi del toohello chiamate API di Machine Learning.  

## <a name="how-tooenable-logging-for-a-web-service"></a>La modalità registrazione tooenable per un servizio Web

Abilitare la registrazione da hello [servizi Web di Azure Machine Learning](https://services.azureml.net) portale. 

1. Accedi al portale di servizi Web di Azure Machine Learning toohello all'indirizzo [https://services.azureml.net](https://services.azureml.net). Per un servizio web classica, è inoltre possibile ottenere toohello portale facendo **nuova esperienza di servizi Web** nella pagina servizi Web di Machine Learning hello in Machine Learning Studio.

   ![Collegamento New Web Services Experience](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. Nella barra dei menu superiore hello, fare clic su **servizi Web** per un nuovo servizio web oppure fare clic su **classico servizi Web** per un classico servizio web.

   ![Selezione di servizi Web nuovi o classici](media/machine-learning-web-services-logging/select-web-service.png)

3. Per un nuovo servizio web, fare clic sul nome del servizio web hello. Per un servizio web classica, fare clic sul nome del servizio web di hello e quindi fare clic su endpoint appropriato hello nella pagina successiva di hello.

4. Nella barra dei menu superiore hello, fare clic su **configura**.

5. Set hello **Abilita registrazione** opzione troppo*errore* (toolog solo gli errori) o *tutti* (per la registrazione completa).

   ![Selezione del livello di registrazione](media/machine-learning-web-services-logging/enable-logging.png)

6. Fare clic su **Salva**.

7. Per i servizi web classica creare hello **ml diagnostica** contenitore.

   Tutti i log di servizio web vengono conservati in un contenitore blob denominato **ml diagnostica** nell'account di archiviazione hello associato al servizio web hello. Per i nuovi servizi web, questo contenitore viene creato hello primo accesso del servizio web di hello. Per i servizi web classica, è necessario contenitore hello toocreate se non esiste già. 

   1. In hello [portale di Azure](https://portal.azure.com), visitare toohello account di archiviazione associato al servizio web hello.

   2. In **Servizio BLOB** fare clic su **Contenitori**.

   3. Se il contenitore di hello **ml diagnostica** non esiste, fare clic su **+ contenitore**, assegnare hello contenitore hello nome "ml diagnostica" e selezionare hello **tipo di accesso** come "Blob". Fare clic su **OK**.

      ![Selezione del livello di registrazione](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> Per un servizio web classica, hello del Dashboard di servizi Web in Machine Learning Studio dispone anche di registrazione tooenable commutatore. Tuttavia, poiché la registrazione è ora gestita tramite il portale di servizi Web hello, è necessario tooenable registrazione tramite il portale di hello come descritto in questo articolo. Se è già abilitata la registrazione in Studio, nel portale dei servizi Web hello, disabilitare la registrazione e abilitarlo di nuovo.


## <a name="hello-effects-of-enabling-logging"></a>effetti Hello dell'abilitazione della registrazione
Quando è abilitata la registrazione, diagnostica hello ed errori restituiti dall'endpoint del servizio web hello vengono registrate in hello **ml diagnostica** contenitore blob nell'Account di archiviazione Azure hello collegate con area di lavoro dell'utente hello. Questo contenitore contiene tutte le informazioni di diagnostica di hello per tutti gli endpoint servizio web hello per tutte le aree di lavoro di hello associate a questo account di archiviazione.

Hello registri possono essere visualizzati utilizzando uno dei hello diversi strumenti disponibili tooexplore un Account di archiviazione di Azure. Hello più semplice può essere toonavigate toohello account di archiviazione nel portale di Azure hello, fare clic su **contenitori**e quindi fare clic sul contenitore di hello **ml diagnostica**.  

## <a name="log-blob-detail-information"></a>Informazioni dettagliate dei BLOB dei log
Ogni blob nel contenitore hello contiene le informazioni di diagnostica hello esattamente per una delle seguenti azioni hello:

* Un'esecuzione del metodo hello esecuzione Batch  
* Un'esecuzione del metodo hello richiesta-risposta  
* Inizializzazione di un contenitore Request-Response

nome Hello di ciascun blob ha un prefisso di hello seguente formato: 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


Dove _tipo Log_ è uno dei seguenti valori hello:  

* o batch  
* punteggio/richieste  
* punteggio/init  

