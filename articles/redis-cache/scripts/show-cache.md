---
title: 'aaaAzure CLI Script di esempio: recupero delle informazioni dettagliate di Cache Redis di Azure | Documenti Microsoft'
description: Esempio di script dell'interfaccia della riga di comando di Azure - Ottenere i dettagli di un'istanza di Cache Redis di Azure
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 155924e6-00d5-4a8c-ba99-5189f300464a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: a3ad1fdf000bbab52e84dbf9f002a5e9fa6d347a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-details-of-an-azure-redis-cache"></a>Ottiene i dettagli di una Cache Redis di Azure

In questo scenario viene illustrato come istanza dettagli hello tooretrieve di Cache Redis di Azure, incluso il relativo stato di provisioning.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Script di esempio

[!code-azurecli[main](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "Azure Redis Cache")]

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello seguenti comandi tooretrieve hello dettagli di un'istanza di Cache Redis di Azure. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [az redis show](https://docs.microsoft.com/cli/azure/redis#show) | Recupera i dettagli di un'istanza di Cache Redis di Azure. |


## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Ulteriori esempi di script di Azure Redis Cache CLI sono reperibile in hello [documentazione Cache Redis di Azure](../cli-samples.md).
