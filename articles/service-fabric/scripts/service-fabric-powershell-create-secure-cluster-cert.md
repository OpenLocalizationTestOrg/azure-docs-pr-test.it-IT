---
title: aaaAzure Script di PowerShell di esempio - creare un cluster di Service Fabric | Documenti Microsoft
description: Esempio di script di Azure PowerShell - Creare un cluster di Service Fabric.
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 12fdc201bd51688cb850cd456b1e00442b79c22d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster"></a>Creare un cluster di Service Fabric

Questo script di esempio crea un cluster con cinque nodi di Service Fabric protetto con un certificato X.509.  comando Hello crea un certificato autofirmato e caricarlo tooa nuovo insieme di credenziali chiave. certificato Hello è anche la directory locale tooa copiato.  Set hello *-OS* versione di hello toochoose parametri di Windows o Linux, che viene eseguito sui nodi del cluster hello.  Personalizzare i parametri di hello in base alle esigenze.

Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](/powershell/azure/overview) e quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure. 

## <a name="sample-script"></a>Script di esempio

[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello, cluster e tutte le relative risorse.

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello i comandi seguenti. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [New-AzureRmServiceFabricCluster](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | Crea un nuovo cluster di Service Fabric. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).

Esempi aggiuntivi di Azure Powershell per Azure Service Fabric sono reperibile in hello [esempi di Azure PowerShell](../service-fabric-powershell-samples.md).
