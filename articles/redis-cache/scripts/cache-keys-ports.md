---
title: aaaAzure CLI Script di esempio - hostname hello Get, porte e le chiavi per Cache Redis di Azure | Documenti Microsoft
description: Azure CLI Script di esempio - hostname hello Get, porte e le chiavi per un'istanza di Cache Redis di Azure
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 761eb24e-2ba7-418d-8fc3-431153e69a90
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: e6e794558087d6568438c439e2bf99fc46eeb8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-hostname-ports-and-keys-for-azure-redis-cache"></a>Ottenere hello hostname, porte e le chiavi per Cache Redis di Azure

In questo scenario, si informazioni sull'utilizzo delle chiavi, porte e nome host hello tooretrieve istanza di Cache Redis di Azure tooan tooconnect.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Script di esempio

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello seguenti comandi tooretrieve hello hostname, chiavi e le porte di un'istanza di Cache Redis di Azure. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [az redis show](https://docs.microsoft.com/cli/azure/redis#show) | Recupera i dettagli di un'istanza di Cache Redis di Azure. |
| [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys) | Recupera le chiavi di accesso per un'istanza di Cache Redis di Azure. |


## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Ulteriori esempi di script di Azure Redis Cache CLI sono reperibile in hello [documentazione Cache Redis di Azure](../cli-samples.md).
