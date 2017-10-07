---
title: Esempio di Script di PowerShell - aaaAzure distribuire cluster di applicazione tooa | Documenti Microsoft
description: 'Script di Azure PowerShell di esempio: distribuire un cluster di Service Fabric application tooa.'
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: b417c9908c72f016e930c43ff2d13e0cc5451f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a>Distribuire un cluster di Service Fabric tooa applicazione

Questo script di esempio copia di un archivio di immagini dell'applicazione pacchetto tooa cluster, registra il tipo di applicazione hello cluster hello e crea un'istanza di applicazione dal tipo di applicazione hello.  Se servizi predefiniti sono stati definiti nel manifesto dell'applicazione hello del tipo di applicazione di destinazione hello, tali servizi vengono creati in questo momento. Personalizzare i parametri di hello in base alle esigenze. 

Se necessario, installare il modulo di PowerShell di Service Fabric hello con hello [Service Fabric SDK](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Script di esempio

[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Dopo l'esecuzione di script di esempio hello, hello script [rimuovere un'applicazione](service-fabric-powershell-remove-application.md) possono essere utilizzati tooremove istanza dell'applicazione hello, annullare la registrazione del tipo di applicazione hello ed eliminare il pacchetto di applicazione hello dall'archivio immagini hello.

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello i comandi seguenti. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | Copiare un archivio di immagini dell'applicazione pacchetto toohello cluster.  |
|[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| Registra un tipo di applicazione e la versione in cluster hello. |
|[New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| Crea un'applicazione da un tipo di applicazione registrata. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sul modulo PowerShell di Service Fabric hello, vedere [documentazione di Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Ulteriori esempi di Powershell per Azure Service Fabric sono reperibile in hello [esempi di Azure PowerShell](../service-fabric-powershell-samples.md).
