---
title: "aaaRules per la denominazione delle entità di Azure Data Factory | Documenti Microsoft"
description: "Descrive le regole di denominazione per le entità di Data factory."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: bc5e801d-0b3b-48ec-9501-bb4146ea17f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 98c5fc5fc932b72b65894afad438b4dc321c8aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---naming-rules"></a>Azure Data Factory - Regole di denominazione
Hello nella tabella seguente fornisce le regole di denominazione per gli elementi Data Factory.

| Nome | Univocità del nome | Controlli di convalida |
|:--- |:--- |:--- |
| Data factory |Univoco in Microsoft Azure. I nomi sono tra maiuscole e minuscole, vale a dire `MyDF` e `mydf` riferimento toohello stessa data factory. |<ul><li>Ogni data factory è abbinato tooexactly una sottoscrizione di Azure.</li><li>I nomi degli oggetti deve iniziare con una lettera o un numero e può contenere solo lettere, numeri e hello trattino (-).</li><li>Ogni carattere trattino (-) deve essere immediatamente preceduto e seguito da una lettera o un numero. Nei nomi di contenitori non sono consentiti trattini consecutivi.</li><li>Il nome può contenere da 3 a 63 caratteri.</li></ul> |
| Servizi collegati/Tabelle/Pipeline |Univoco in una data factory. Per i nomi viene fatta distinzione tra maiuscole e minuscole. |<ul><li>Numero massimo di caratteri nel nome di una tabella: 260.</li><li>I nomi degli oggetti devono iniziare con una lettera, un numero o un carattere di sottolineatura (_).</li><li>Non sono ammessi i caratteri seguenti: ".", "+", "?", "/", "<", ">", "*", "%", "&", ":", "\\".</li></ul> |
| Gruppo di risorse |Univoco in Microsoft Azure. Per i nomi viene fatta distinzione tra maiuscole e minuscole. |<ul><li>Numero massimo di caratteri: 1000.</li><li>Nome può contenere lettere, cifre e hello seguenti caratteri: "-", "_",","e"."</li></ul> |

