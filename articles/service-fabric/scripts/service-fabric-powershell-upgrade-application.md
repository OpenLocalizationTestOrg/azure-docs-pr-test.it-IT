---
title: Esempio di Script di PowerShell - aaaAzure aggiornare un'applicazione di Service Fabric | Documenti Microsoft
description: Esempio di script di Azure PowerShell - Aggiornare un'applicazione di Service Fabric.
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
ms.date: 08/23/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 4f4777607bd6b35a76029e09ddb441006565d4cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-service-fabric-application"></a>Aggiornare un'applicazione di Service Fabric

Questo script di esempio aggiorna un tooversion 1.3.0 istanza dell'applicazione in esecuzione di Service Fabric. script Hello copia hello nuovo applicazione toohello cluster immagine archivio pacchetti, registra il tipo di applicazione hello, avvia un aggiornamento monitorato e controlla continuamente lo stato dell'aggiornamento hello fino a quando non viene completato l'aggiornamento di hello o il rollback. Personalizzare i parametri di hello in base alle esigenze. 

Se necessario, installare il modulo di PowerShell di Service Fabric hello con hello [Service Fabric SDK](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Script di esempio

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello i comandi seguenti. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | Ottiene tutte le applicazioni in cluster di Service Fabric hello hello o un'applicazione specifica.  |
| [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | Ottiene lo stato di hello di un aggiornamento dell'applicazione di Service Fabric. |
| [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | Ottiene i tipi di applicazioni di Service Fabric hello registrati nel cluster di Service Fabric hello. |
| [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | Annulla la registrazione del tipo di applicazione di Service Fabric.  |
| [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | Copia un'immagine di toohello Service Fabric pacchetto dell'applicazione nell'archivio.  |
| [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | Registra un tipo di applicazione di Service Fabric. |
| [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | Consente di aggiornare una versione di tipo Service Fabric applicazione toohello applicazione specificata. |


## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sul modulo PowerShell di Service Fabric hello, vedere [documentazione di Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Ulteriori esempi di Powershell per Azure Service Fabric sono reperibile in hello [esempi di Azure PowerShell](../service-fabric-powershell-samples.md).
