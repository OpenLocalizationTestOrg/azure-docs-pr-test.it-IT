---
title: repository del Registro di sistema di contenitore aaaAzure | Documenti Microsoft
description: Il repository del Registro di sistema di Azure contenitore toouse per le immagini Docker
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: 06172a63465838a78a607f268da116d8158789ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a>Archivi di registri contenitori di Azure

I registri contenitori di Azure sono compatibili con una vasta gamma di servizi e agenti di orchestrazione. toomake è più facile tootrack hello origine i servizi e gli agenti da cui viene utilizzato ACR, abbiamo iniziato con campo di intestazione hello Docker nel file Docker.config hello.



## <a name="viewing-repositories-in-hello-portal"></a>Visualizzazione di repository in hello portale

intestazioni ACR Hello seguono il formato di hello:
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* Cloud: Azure, Azure Stack o altri cloud di Azure per enti pubblici o paesi specifici. Anche se Azure Stack e i cloud per enti pubblici non sono attualmente supportati, questo parametro consente il supporto futuro.
* Servizio: nome del servizio di hello.
* Optionalservicename: parametro facoltativo per i servizi con i servizi secondari o toospecify uno SKU (ex: corrispondono App web con Azure/app-servizio/web-App).

Orchestrators e servizi dei partner sono invitati toouse intestazione specifici valori toohelp con i dati di telemetria. Gli utenti possono inoltre modificare il valore di hello passato toohello intestazione se desiderano.

di seguito sono valori Hello si vuole creare ACR partner toouse toopopulate hello "X-Meta-origine-Client" campo:

| Nome servizio              | Intestazione                                |
| ------------------------- | ------------------------------------- |
| Servizio contenitore di Azure   | azure/compute/azure-container-service |
| Servizio app - App Web    | azure/app-service/web-apps            |
| Servizio app - App per la logica  | azure/app-service/logic-apps          |
| Batch                     | azure/compute/batch                   |
| Cloud Console             | azure/cloud-console                   |
| Funzioni                 | azure/compute/functions               |
| Internet delle cose - Hub  | azure/iot/hub                         |
| HDInsight                 | azure/data/hdinsight                  |
| Jenkins                   | azure/jenkins                         |
| Machine Learning          | azure/data/machile-learning           |
| Service Fabric            | azure/compute/service-fabric          |
| VSTS                      | azure/vsts                            |


## <a name="next-steps"></a>Passaggi successivi
[Altre informazioni sui registri e i servizi di hello è supportato e orchestrators](container-registry-intro.md)
