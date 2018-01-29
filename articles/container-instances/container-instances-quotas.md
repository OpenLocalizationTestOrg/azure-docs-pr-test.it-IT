---
title: Quote e aree disponibili per Istanze di contenitore di Azure
description: Quote predefinite e aree disponibili per il servizio Istanze di contenitore di Azure.
services: container-instances
author: mmacy
manager: timlt
ms.service: container-instances
ms.topic: overview
ms.date: 01/11/2018
ms.author: marsma
ms.openlocfilehash: baf93d4a2a4ba1e05bbf558d0c056fa3aa833fef
ms.sourcegitcommit: 562a537ed9b96c9116c504738414e5d8c0fd53b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/12/2018
---
# <a name="quotas-and-region-availability-for-azure-container-instances"></a>Quote e aree disponibili per Istanze di contenitore di Azure

Tutti i servizi di Azure prevedono determinati limiti predefiniti e quote per le risorse e le funzionalità. Le sezioni seguenti illustrano in modo dettagliato i limiti predefiniti per alcune risorse di Istanze di contenitore di Azure e la disponibilità di questo servizio nelle aree di Azure.

## <a name="service-quotas-and-limits"></a>Quote e limiti del servizio

[!INCLUDE [container-instances-limits](../../includes/container-instances-limits.md)]

## <a name="region-availability"></a>Aree di disponibilità

Istanze di contenitore di Azure è disponibile nelle aree seguenti con i limiti di CPU e memoria specificati.

| Località | OS | CPU | Memoria (GB) |
| -------- | -- | :---: | :-----------: |
| Europa occidentale, Stati Uniti occidentali, Stati Uniti orientali, Asia sud-orientale | Linux | 4 | 14 |
| Europa occidentale, Stati Uniti occidentali, Stati Uniti orientali, Asia sud-orientale  | Windows | 4 | 14 |

La disponibilità di Istanze di contenitore con questi limiti di risorse dipende dell'area di distribuzione. Quando un'area ha un carico elevato, può verificarsi un errore durante la distribuzione delle istanze. Per mitigare tale errore di distribuzione, provare a distribuire le istanze con impostazioni di memoria e CPU inferiori oppure provare a eseguire la distribuzione in un secondo momento.

Per altre informazioni sulla risoluzione dei problemi di distribuzione di Istanze di contenitore, vedere [Risolvere i problemi di distribuzione di Istanze di contenitore di Azure](container-instances-troubleshooting.md).

## <a name="next-steps"></a>Passaggi successivi

È possibile aumentare alcune quote e alcuni limiti predefiniti. Per richiedere un aumento di una o più risorse che lo consentono, inviare una [richiesta di supporto di Azure][azure-support] (selezionare "Quota" per **Tipo di problema**).

<!-- LINKS - External -->
[azure-support]: https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest
