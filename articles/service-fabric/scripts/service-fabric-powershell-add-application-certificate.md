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
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a><span data-ttu-id="c512f-103">Aggiungere un cluster di Service Fabric application tooa certificato</span><span class="sxs-lookup"><span data-stu-id="c512f-103">Add an application certificate tooa Service Fabric cluster</span></span>

<span data-ttu-id="c512f-104">Questo script di esempio crea un certificato autofirmato nell'insieme di credenziali chiave di Azure specificato hello e lo installa tooall i nodi del cluster di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="c512f-104">This sample script creates a self-signed certificate in hello specified Azure key vault and installs it tooall nodes of hello Service Fabric cluster.</span></span> <span data-ttu-id="c512f-105">certificato Hello scarica anche tooa di cartella locale.</span><span class="sxs-lookup"><span data-stu-id="c512f-105">hello certificate also downloads tooa local folder.</span></span> <span data-ttu-id="c512f-106">nome di Hello del certificato scaricata hello è hello corrisponde al nome hello del certificato hello nell'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="c512f-106">hello name of hello downloaded certificate is hello same as hello name of hello certificate in hello key vault.</span></span> <span data-ttu-id="c512f-107">Personalizzare i parametri di hello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="c512f-107">Customize hello parameters as needed.</span></span>

<span data-ttu-id="c512f-108">Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](/powershell/azure/overview) e quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="c512f-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c512f-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="c512f-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a><span data-ttu-id="c512f-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="c512f-110">Script explanation</span></span>

<span data-ttu-id="c512f-111">Questo script utilizza hello seguenti comandi: ogni comando in una tabella di hello collega la documentazione specifica toocommand.</span><span class="sxs-lookup"><span data-stu-id="c512f-111">This script uses hello following commands: Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c512f-112">Comando</span><span class="sxs-lookup"><span data-stu-id="c512f-112">Command</span></span> | <span data-ttu-id="c512f-113">Note</span><span class="sxs-lookup"><span data-stu-id="c512f-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c512f-114">Add-AzureRmServiceFabricApplicationCertificate</span><span class="sxs-lookup"><span data-stu-id="c512f-114">Add-AzureRmServiceFabricApplicationCertificate</span></span>](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | <span data-ttu-id="c512f-115">Aggiungere che set di scalabilità della macchina virtuale toohello una nuova applicazione certificato che costituiscono il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c512f-115">Add a new application certificate toohello virtual machine scale set that make up hello cluster.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="c512f-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c512f-116">Next steps</span></span>

<span data-ttu-id="c512f-117">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c512f-117">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c512f-118">Esempi aggiuntivi di Azure Powershell per Azure Service Fabric sono reperibile in hello [esempi di Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c512f-118">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
