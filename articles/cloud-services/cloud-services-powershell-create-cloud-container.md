---
title: un contenitore del servizio cloud con PowerShell aaaCreate | Documenti Microsoft
description: Questo articolo spiega come toocreate un cloud servizio contenitore con PowerShell. contenitore Hello ospita i ruoli web e di lavoro.
services: cloud-services
documentationcenter: .net
author: cawaMS
manager: timlt
editor: 
ms.assetid: c8f32469-610e-4f37-a3aa-4fac5c714e13
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 4c47b10b5ba1f9cc39594a45cd869bf04fcaadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-azure-powershell-command-toocreate-an-empty-cloud-service-container"></a><span data-ttu-id="2a0a2-104">Utilizzare un toocreate di comando di PowerShell di Azure un contenitore del servizio cloud vuoto</span><span class="sxs-lookup"><span data-stu-id="2a0a2-104">Use an Azure PowerShell command toocreate an empty cloud service container</span></span>
<span data-ttu-id="2a0a2-105">Questo articolo spiega come tooquickly creare un contenitore di servizi Cloud utilizzando i cmdlet PowerShell di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a0a2-105">This article explains how tooquickly create a Cloud Services container using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="2a0a2-106">Eseguire le operazioni di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a0a2-106">Please follow hello steps below:</span></span>

1. <span data-ttu-id="2a0a2-107">Installare i cmdlet di Microsoft Azure PowerShell hello da hello [Scarica Azure PowerShell](http://aka.ms/webpi-azps) pagina.</span><span class="sxs-lookup"><span data-stu-id="2a0a2-107">Install hello Microsoft Azure PowerShell cmdlet from hello [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.</span></span>
2. <span data-ttu-id="2a0a2-108">Aprire il prompt dei comandi di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="2a0a2-108">Open hello PowerShell command prompt.</span></span>
3. <span data-ttu-id="2a0a2-109">Hello utilizzare [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign in.</span><span class="sxs-lookup"><span data-stu-id="2a0a2-109">Use hello [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign in.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2a0a2-110">Per ulteriori istruzioni sull'installazione di cmdlet di Azure PowerShell hello e connessione tooyour sottoscrizione di Azure, vedere troppo[come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2a0a2-110">For further instruction on installing hello Azure PowerShell cmdlet and connecting tooyour Azure subscription, refer too[How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
   >
   >
4. <span data-ttu-id="2a0a2-111">Hello utilizzare **New-AzureService** toocreate cmdlet un contenitore di servizi cloud di Azure vuoto.</span><span class="sxs-lookup"><span data-stu-id="2a0a2-111">Use hello **New-AzureService** cmdlet toocreate an empty Azure cloud service container.</span></span>

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. <span data-ttu-id="2a0a2-112">Eseguire questo cmdlet hello tooinvoke di esempio:</span><span class="sxs-lookup"><span data-stu-id="2a0a2-112">Follow this example tooinvoke hello cmdlet:</span></span>

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

<span data-ttu-id="2a0a2-113">Per ulteriori informazioni sulla creazione del servizio cloud di Azure hello, eseguire:</span><span class="sxs-lookup"><span data-stu-id="2a0a2-113">For more information about creating hello Azure cloud service, run:</span></span>

```
Get-help New-AzureService
```

### <a name="next-steps"></a><span data-ttu-id="2a0a2-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2a0a2-114">Next steps</span></span>
* <span data-ttu-id="2a0a2-115">hello toomanage distribuzione del servizio cloud, vedere toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), e [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) comandi.</span><span class="sxs-lookup"><span data-stu-id="2a0a2-115">toomanage hello cloud service deployment, refer toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands.</span></span> <span data-ttu-id="2a0a2-116">È possibile anche fare riferimento troppo[come servizi cloud tooconfigure](cloud-services-how-to-configure.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="2a0a2-116">You may also refer too[How tooconfigure cloud services](cloud-services-how-to-configure.md) for further information.</span></span>
* <span data-ttu-id="2a0a2-117">toopublish il servizio cloud tooAzure del progetto, fare riferimento toohello **PublishCloudService.ps1** nell'esempio di codice da [la distribuzione continua per il servizio cloud in Azure](cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="2a0a2-117">toopublish your cloud service project tooAzure, refer toohello  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).</span></span>
