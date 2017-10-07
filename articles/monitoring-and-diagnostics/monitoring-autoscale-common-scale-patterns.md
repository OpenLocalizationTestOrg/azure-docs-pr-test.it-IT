---
title: "aaaOverview dei modelli di scalabilità automatica comuni | Documenti Microsoft"
description: Informazioni su che alcune delle tooauto modelli comuni hello ridimensionare la risorsa in Azure.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: fc5bd97852e0af01aa32940c99721ab8e21033ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-common-autoscale-patterns"></a>Panoramica di modelli comuni di scalabilità automatica
In questo articolo vengono descritte alcune tooscale modelli comuni hello la risorsa in Azure.

Azure ridimensionamento automatico di monitoraggio si applica solo tooVirtual set di scalabilità macchina (VMSS), servizi cloud, piani di servizio app e gli ambienti del servizio app. 

# <a name="lets-get-started"></a>Introduzione

Questo articolo presuppone che l'utente abbia familiarità con la scalabilità automatica. È possibile [ottenere avviata tooscale qui la risorsa][1]. di seguito Hello sono alcuni dei modelli di scala comune hello.

## <a name="scale-based-on-cpu"></a>Scalabilità in base alla CPU

È presente un'app Web (VMSS/ruolo del servizio cloud) e 

- Si desidera tooscale out e della scala in base alle CPU.
- Inoltre, si desidera tooensure è un numero minimo di istanze. 
- Inoltre, si desidera tooensure che si imposta un numero di toohello limite massimo di istanze che per cui è possibile scalare.

![Scalabilità in base alla CPU][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a>Scalabilità diversa per giorni feriali e fine settimana

È presente un'app Web (VMSS/ruolo del servizio cloud) e

- Si vogliono 3 istanze per impostazione predefinita nei giorni feriali
- Non si prevede che il traffico nei fine settimana e pertanto si desidera tooscale verso il basso too1 istanza nei fine settimana.

![Scalabilità diversa per giorni feriali e fine settimana][3]

## <a name="scale-differently-during-holidays"></a>Scalabilità diversa durante le festività

È presente un'app Web (VMSS/ruolo del servizio cloud) e 

- Si desidera tooscale su/giù in base all'utilizzo della CPU per impostazione predefinita
- Tuttavia, durante le feste natalizie (o i giorni specifici che sono importanti per l'azienda) desiderato toooverride hello predefinite che dispone di maggiore capacità.

![Scalabilità diversa nelle festività][4]

## <a name="scale-based-on-custom-metric"></a>Scalabilità in base a metriche personalizzate

È necessario un front-end web e un livello di API che comunica con hello di back-end. 

- Si desidera il livello di API hello tooscale basato sugli eventi personalizzati nel front-end hello (esempio: si desidera tooscale il processo di estrazione in base al numero di hello di elementi nel carrello degli acquisti hello)

![Scalabilità in base a metriche personalizzate][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png