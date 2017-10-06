---
title: aaaAzure CLI Script di esempio - eliminare una Cache Redis di Azure | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Eliminare una cache Redis di Azure
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 7beded7a-d2c9-43a6-b3b4-b8079c11de4a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: 788277f6464d40fedc597ce7f3041130312c07a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-azure-redis-cache"></a>Eliminare una cache Redis di Azure

In questo scenario viene illustrato come toodelete un Redis di Azure memorizzano nella Cache.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Script di esempio

[!code-azurecli[main](../../../cli_scripts/redis-cache/delete-cache/delete-cache.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello seguenti comandi toodelete un'istanza di Cache Redis di Azure. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [eliminazione di redis az](https://docs.microsoft.com/cli/azure/redis#delete) | Eliminare un'istanza della cache Redis. |


## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Ulteriori esempi di script di Azure Redis Cache CLI sono reperibile in hello [documentazione Cache Redis di Azure](../cli-samples.md).
