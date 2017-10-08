---
title: Esempio di Script di PowerShell - aaaAzure aggiungere applicazione cert tooa cluster | Documenti Microsoft
description: Script di Azure PowerShell di esempio - aggiunta di un cluster di Service Fabric application tooa certificato.
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
ms.openlocfilehash: aba62598e2e4775012f89b5070bef5e61aec64f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a>Aggiungere un cluster di Service Fabric application tooa certificato

Questo script di esempio crea un certificato autofirmato nell'insieme di credenziali chiave di Azure specificato hello e lo installa tooall i nodi del cluster di Service Fabric hello. certificato Hello scarica anche tooa di cartella locale. nome di Hello del certificato scaricata hello è hello corrisponde al nome hello del certificato hello nell'insieme di credenziali chiave hello. Personalizzare i parametri di hello in base alle esigenze.

Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](/powershell/azure/overview) e quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure. 

## <a name="sample-script"></a>Script di esempio

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello seguenti comandi: ogni comando in una tabella di hello collega la documentazione specifica toocommand.

| Comando | Note |
|---|---|
| [Add-AzureRmServiceFabricApplicationCertificate](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | Aggiungere che set di scalabilità della macchina virtuale toohello una nuova applicazione certificato che costituiscono il cluster hello.  |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).

Esempi aggiuntivi di Azure Powershell per Azure Service Fabric sono reperibile in hello [esempi di Azure PowerShell](../service-fabric-powershell-samples.md).
