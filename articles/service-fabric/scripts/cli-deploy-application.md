---
title: aaaAzure esempio distribuire uno Script del servizio dell'infrastruttura CLI
description: Distribuire un cluster di Azure Service Fabric tooan applicazione utilizzando hello CLI di Azure Service Fabric
services: service-fabric
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.openlocfilehash: aaec7042a4fd7ed32ad706cde70361f23d18fb48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a>Distribuire un cluster di Service Fabric tooa applicazione

Questo script di esempio copia di un archivio di immagini dell'applicazione pacchetto tooa cluster, registra il tipo di applicazione hello cluster hello e crea un'istanza di applicazione dal tipo di applicazione hello. Anche i servizi predefiniti vengono creati in questa fase.

Se necessario, installare hello [servizio infrastruttura CLI](../service-fabric-cli.md).

## <a name="sample-script"></a>Script di esempio

[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione

Al termine, hello [rimuovere](cli-remove-application.md) script può essere un'applicazione hello tooremove utilizzato. script di rimozione Hello Elimina istanza dell'applicazione hello, Annulla la registrazione di tipo di applicazione hello e pacchetto dell'applicazione hello dall'archivio immagini.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni, vedere hello [documentazione servizio infrastruttura CLI](../service-fabric-cli.md).

Esempi aggiuntivi di servizio dell'infrastruttura CLI per Azure Service Fabric sono reperibile in hello [esempi del servizio dell'infrastruttura CLI](../samples-cli.md).
