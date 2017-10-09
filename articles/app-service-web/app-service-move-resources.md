---
title: Risorse dell'App Web di aaaMove tooanother gruppo di risorse
description: "Vengono descritti gli scenari di hello in cui è possibile spostare le applicazioni Web e servizi App da un gruppo di risorse tooanother."
services: app-service
documentationcenter: 
author: ZainRizvi
manager: erikre
editor: 
ms.assetid: 22f97607-072e-4d1f-a46f-8d500420c33c
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: zarizvi
ms.openlocfilehash: 931012fee656b7f8a4b2c225c38739a9171d3b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="supported-move-configurations"></a>Configurazioni di spostamento supportate
È possibile spostare le risorse di App Web di Azure utilizzando hello [risorsa gestore di spostare risorse API](../azure-resource-manager/resource-group-move-resources.md).

Le app Web di Azure supporta attualmente hello seguenti scenari di spostamento:

* Spostare hello l'intero contenuto di un gruppo di risorse (app web, i piani di servizio app e i certificati) tooanother gruppo di risorse. 
   > [!Note]
   > gruppo di risorse di destinazione Hello non può contenere tutte le risorse di Microsoft in questo scenario.

* Gruppo di risorse diverso tooa App web singoli, può essere spostato mentre ancora all'hosting in al piano di servizio app (hello app servizio piano rimane nel gruppo di risorse precedente hello) corrente.


