---
title: Esempio di Script di PowerShell - Rimuovi applicazione da un cluster aaaAzure | Documenti Microsoft
description: Esempio di script di Azure PowerShell - Rimuovere un'applicazione da un cluster di Service Fabric.
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
ms.openlocfilehash: 3fe2082c2fbeffbff1622f206021d4d907197d19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Rimuovere un'applicazione da un cluster di Service Fabric

Questo script di esempio elimina un'istanza di applicazione di Service Fabric in esecuzione, Annulla la registrazione di un tipo di applicazione e la versione dal cluster hello e pacchetto dell'applicazione hello dall'archivio di immagini cluster hello.  Istanza dell'applicazione hello eliminazione elimina inoltre hello tutte le istanze del servizio associata all'applicazione. Personalizzare i parametri di hello in base alle esigenze. 

Se necessario, installare il modulo di PowerShell di Service Fabric hello con hello [Service Fabric SDK](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Script di esempio

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello i comandi seguenti. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | Rimuove un'istanza di applicazione di Service Fabric in esecuzione dal cluster hello.  |
| [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | Annulla la registrazione di un tipo di applicazione di Service Fabric e una versione da cluster hello. |
| [Remove-ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | Rimuove un pacchetto di applicazione di Service Fabric dall'archivio immagini hello.|

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sul modulo PowerShell di Service Fabric hello, vedere [documentazione di Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Ulteriori esempi di Powershell per Azure Service Fabric sono reperibile in hello [esempi di Azure PowerShell](../service-fabric-powershell-samples.md).
