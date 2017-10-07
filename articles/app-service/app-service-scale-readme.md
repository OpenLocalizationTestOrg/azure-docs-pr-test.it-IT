---
title: "Servizio app di Azure: scalabilità delle applicazioni nel servizio app"
description: "Informazioni su vantaggi e svantaggi hello di scalabilità dell'applicazione di servizio App."
keywords: servizio app, servizio app di azure, scala, scalabile, piano di servizio app, costo del servizio app
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: d8cd12f73915a916a75d46da2f751a40d567b189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a>Servizio app di Azure: scalabilità delle applicazioni nel servizio app
Le applicazioni ospitate nel servizio app di Azure possono [raggiungere un livello di scalabilità elevato](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).
Tuttavia, la scalabilità di un'applicazione è un problema complesso senza una soluzione valida per tutti i casi. toocorrectly ridimensionare l'applicazione sono presenti 3 aree chiave che contribuiranno tooyour esito positivo di applicazioni:

1. Comprendere l'architettura dell'applicazione e i relativi punti deboli.
   * Si tratta di un'applicazione con stato o senza stato?
   * Quali sono tutti i componenti dell'applicazione hello?
     * Dove si trovano i colli di bottiglia hello in un'applicazione hello?
   * Quando carico è applicato tooyour app, ciò che verrà interrotta prima?
2. Hello comprensione prevede requisiti di carico e delle prestazioni.
   * Un'applicazione hello necessita tooserve 1000 utenti? o di un milione?
   * Il traffico proviene da un'unica area geografica o a livello globale?
   * Sono presenti variazioni stagionali o picchi di traffico?
   * La velocità con cui deve rispondere l'applicazione hello? Un secondo? Un millisecondo?
3. Comprensione e correttamente sfruttano hello piattaforma che ospita l'app.
   * Quali funzionalità devono sfruttare appieno tooachieve miei obiettivi di scalabilità?

In questa sezione aiutano a comprendere tutti i fattori di hello e della Guida mettere a punto una strategia che sfrutta tooachieve funzionalità di servizio App necessarie hello gli obiettivi di scalabilità.

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

