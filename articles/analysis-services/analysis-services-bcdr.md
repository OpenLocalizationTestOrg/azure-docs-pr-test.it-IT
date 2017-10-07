---
title: "disponibilità elevata di Analysis Services aaaAzure | Documenti Microsoft"
description: "Assicurare la disponibilità elevata di Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 6e09536c5bd7dc7f88f9b662e1a9f42d2b8c969b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analysis-services-high-availability"></a>Disponibilità elevata di Azure Analysis Services
Questo articolo descrive come garantire la disponibilità elevata dei server di Azure Analysis Services. 


## <a name="assuring-high-availability-during-a-service-disruption"></a>Garantire la disponibilità elevata durante un'interruzione del servizio
Sebbene accada raramente, un data center di Azure può subire un'interruzione del servizio. Quando si verifica un'interruzione, viene generata un'interruzione delle attività che può durare pochi minuti oppure alcune ore. La disponibilità elevata è ottenuta spesso con la ridondanza dei server. Azure Analysis Services consente di ottenere tale ridondanza tramite la creazione di server secondari e aggiuntivi in una o più aree. Quando la creazione di server ridondanti, tooassure hello dati e i metadati di tali server sia sincronizzato con il server di hello in un'area che è non in linea, è possibile:

* Distribuire modelli tooredundant server in altri paesi. Questo metodo richiede l'elaborazione dei dati in parallelo sia sul server primario sia sui server, assicurando così la sincronizzazione di tutti i server.

* Eseguire il backup dei database dal server primario e il ripristino nei server ridondanti. Ad esempio, automatizzare archiviazione tooAzure notturna backup e ripristino tooother server ridondanti in altre aree. 

In entrambi i casi, se il server principale si verifica un'interruzione, è necessario modificare le stringhe di connessione hello in client tooconnect toohello server in un altro Data Center regionale di report. Questa modifica deve essere presa in considerazione come soluzione estrema e solo quando si verifica un'interruzione del data center dell'area. È più probabile che un'interruzione del data center che ospita il server principale venga risolta prima che sia possibile aggiornare le connessioni in tutti i client. 



## <a name="related-information"></a>Informazioni correlate
[Backup e ripristino](analysis-services-backup.md)   
[Gestire Azure Analysis Services](analysis-services-manage.md) 

