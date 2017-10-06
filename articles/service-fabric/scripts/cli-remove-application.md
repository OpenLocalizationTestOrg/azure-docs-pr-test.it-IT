---
title: aaaAzure esempio rimuovere Script del servizio dell'infrastruttura CLI
description: Rimuovere un'applicazione da un cluster di Azure Service Fabric utilizzando hello CLI di Azure Service Fabric
services: service-fabric
documentationcenter: 
author: thraka
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
ms.openlocfilehash: 3ccefd4a04c5b7af71a2f959e11da6e402f25881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Rimuovere un'applicazione da un cluster di Service Fabric

Questo script di esempio elimina un'istanza di applicazione di Service Fabric in esecuzione, Annulla la registrazione di un tipo di applicazione e la versione dal cluster hello.  Istanza dell'applicazione hello eliminazione elimina inoltre hello tutte le istanze del servizio associata all'applicazione. Successivamente, i file dell'applicazione hello vengono eliminati dall'archivio immagini hello. 

Se necessario, installare hello [servizio infrastruttura CLI](../service-fabric-cli.md).

## <a name="sample-script"></a>Script di esempio

[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni, vedere hello [documentazione servizio infrastruttura CLI](../service-fabric-cli.md).

Esempi aggiuntivi di servizio dell'infrastruttura CLI per Azure Service Fabric sono reperibile in hello [esempi del servizio dell'infrastruttura CLI](../samples-cli.md).
