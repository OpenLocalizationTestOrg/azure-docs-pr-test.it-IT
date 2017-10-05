---
title: Creare un contenitore del servizio cloud con PowerShell | Documentazione Microsoft
description: Questo articolo illustra come creare un contenitore del servizio cloud con PowerShell. Il contenitore ospita il ruolo Web e il ruolo di lavoro.
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
ms.openlocfilehash: 2023fa7b318f9f76ce1e1ea0a46110297be9a001
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-an-azure-powershell-command-to-create-an-empty-cloud-service-container"></a><span data-ttu-id="d164e-104">Usare un prompt dei comandi di Azure PowerShell per creare un contenitore del servizio cloud vuoto</span><span class="sxs-lookup"><span data-stu-id="d164e-104">Use an Azure PowerShell command to create an empty cloud service container</span></span>
<span data-ttu-id="d164e-105">Questo articolo illustra come creare velocemente un contenitore di Servizi cloud usando i cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d164e-105">This article explains how to quickly create a Cloud Services container using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="d164e-106">Eseguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d164e-106">Please follow the steps below:</span></span>

1. <span data-ttu-id="d164e-107">Installare i cmdlet di Microsoft Azure PowerShell dalla pagina dei [download di Azure PowerShell](http://aka.ms/webpi-azps) .</span><span class="sxs-lookup"><span data-stu-id="d164e-107">Install the Microsoft Azure PowerShell cmdlet from the [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.</span></span>
2. <span data-ttu-id="d164e-108">Aprire il prompt dei comandi di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d164e-108">Open the PowerShell command prompt.</span></span>
3. <span data-ttu-id="d164e-109">Usare [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) per accedere.</span><span class="sxs-lookup"><span data-stu-id="d164e-109">Use the [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) to sign in.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d164e-110">Per altre istruzioni sull'installazione del cmdlet di Azure PowerShell e sulla connessione alla sottoscrizione di Azure, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d164e-110">For further instruction on installing the Azure PowerShell cmdlet and connecting to your Azure subscription, refer to [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
   >
   >
4. <span data-ttu-id="d164e-111">Usare il cmdlet **New-AzureService** per creare un contenitore del servizio cloud vuoto.</span><span class="sxs-lookup"><span data-stu-id="d164e-111">Use the **New-AzureService** cmdlet to create an empty Azure cloud service container.</span></span>

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. <span data-ttu-id="d164e-112">Per richiamare il cmdlet, seguire questo esempio:</span><span class="sxs-lookup"><span data-stu-id="d164e-112">Follow this example to invoke the cmdlet:</span></span>

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

<span data-ttu-id="d164e-113">Per altre informazioni sulla creazione del servizio cloud di Azure, eseguire:</span><span class="sxs-lookup"><span data-stu-id="d164e-113">For more information about creating the Azure cloud service, run:</span></span>

```
Get-help New-AzureService
```

### <a name="next-steps"></a><span data-ttu-id="d164e-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d164e-114">Next steps</span></span>
* <span data-ttu-id="d164e-115">Per gestire la distribuzione del servizio cloud, vedere i comandi [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx) e [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx).</span><span class="sxs-lookup"><span data-stu-id="d164e-115">To manage the cloud service deployment, refer to the [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands.</span></span> <span data-ttu-id="d164e-116">Per altre informazioni, è anche possibile vedere [Come configurare i servizi cloud](cloud-services-how-to-configure.md) .</span><span class="sxs-lookup"><span data-stu-id="d164e-116">You may also refer to [How to configure cloud services](cloud-services-how-to-configure.md) for further information.</span></span>
* <span data-ttu-id="d164e-117">Per pubblicare il progetto servizio cloud in Azure, vedere l'esempio di codice **PublishCloudService.ps1** riportato nell'articolo [Recapito continuo per Servizi cloud in Azure](cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="d164e-117">To publish your cloud service project to Azure, refer to the  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).</span></span>
