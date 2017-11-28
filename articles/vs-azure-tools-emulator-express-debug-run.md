---
title: Uso dell'emulatore Express per l'esecuzione e il debug di un servizio cloud di Azure in un computer locale | Documentazione Microsoft
description: Uso di Emulator Express per l'esecuzione e il debug di un servizio cloud in un computer locale
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: d7d87045569fdc473333deae05f95d1df343b68c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="using-emulator-express-to-run-and-debug-an-azure-cloud-service-on-a-local-machine"></a><span data-ttu-id="fb62e-103">Uso dell'emulatore Express per l'esecuzione e il debug di un servizio cloud di Azure in un computer locale</span><span class="sxs-lookup"><span data-stu-id="fb62e-103">Using Emulator Express to run and debug an Azure cloud service on a local machine</span></span>
<span data-ttu-id="fb62e-104">Con l'emulatore Express, è possibile testare ed eseguire il debug di un servizio cloud senza eseguire Visual Studio come amministratore.</span><span class="sxs-lookup"><span data-stu-id="fb62e-104">By using Emulator Express, you can test and debug a cloud service without running Visual Studio as an administrator.</span></span> <span data-ttu-id="fb62e-105">È possibile configurare le impostazioni del progetto per usare l'emulatore Express o l'emulatore completo, in base ai requisiti del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="fb62e-105">You can set your project settings to use either Emulator Express or the full emulator, depending on the requirements of your cloud service.</span></span> <span data-ttu-id="fb62e-106">Per altre informazioni sull'emulatore completo, vedere [Eseguire un'applicazione Azure nell'emulatore di calcolo](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="fb62e-106">For more information about the full emulator, see [Run an Azure Application in the Compute Emulator](storage/common/storage-use-emulator.md).</span></span>

## <a name="using-emulator-express-in-visual-studio"></a><span data-ttu-id="fb62e-107">Uso dell'emulatore Express in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fb62e-107">Using Emulator Express in Visual Studio</span></span>
<span data-ttu-id="fb62e-108">Quando si crea un progetto di Azure in Azure SDK 2.3 o versione successiva, l'emulatore Express è selezionato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="fb62e-108">When you create an Azure project in Azure SDK 2.3 or later, Emulator Express is automatically used.</span></span> <span data-ttu-id="fb62e-109">Per i progetti esistenti creati con una versione precedente dell'SDK di Azure, attenersi alla procedura seguente per selezionare l'emulatore Express:</span><span class="sxs-lookup"><span data-stu-id="fb62e-109">For existing projects that were created with an earlier version of the Azure SDK, use the following steps to select Emulator Express:</span></span>

1. <span data-ttu-id="fb62e-110">Creare o aprire un progetto del servizio cloud di Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb62e-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="fb62e-111">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e scegliere **Proprietà** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="fb62e-111">In **Solution Explorer**, right-click the project, and, from the context menu, select **Properties**.</span></span>

1. <span data-ttu-id="fb62e-112">Nelle pagine delle proprietà di progetti, selezionare la scheda **Web**.</span><span class="sxs-lookup"><span data-stu-id="fb62e-112">In the projects properties pages, select the **Web** tab.</span></span>

    ![Proprietà di un progetto di servizio cloud di Azure](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. <span data-ttu-id="fb62e-114">In **Server di sviluppo locale**, scegliere **Usa l'opzione IIS Express**.</span><span class="sxs-lookup"><span data-stu-id="fb62e-114">Under **Local Development Server**, select **Use IIS Express option**.</span></span>

1. <span data-ttu-id="fb62e-115">In **Emulatore**selezionare **Usa emulatore Express**.</span><span class="sxs-lookup"><span data-stu-id="fb62e-115">Under **Emulator**, select **Use Emulator Express**.</span></span>
   
1. <span data-ttu-id="fb62e-116">Per avviare l'emulatore Express, eseguire il comando seguente al prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="fb62e-116">To launch the Emulator Express, run the following command at a command prompt:</span></span> 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a><span data-ttu-id="fb62e-117">Limitazioni dell'emulatore Express</span><span class="sxs-lookup"><span data-stu-id="fb62e-117">Emulator Express limitations</span></span>
<span data-ttu-id="fb62e-118">Di seguito sono indicati alcuni problemi causati da limiti noti dell'emulatore Express:</span><span class="sxs-lookup"><span data-stu-id="fb62e-118">The following issues are known limitations of Emulator Express:</span></span> 

- <span data-ttu-id="fb62e-119">L'emulatore Express non è compatibile con il Server Web IIS.</span><span class="sxs-lookup"><span data-stu-id="fb62e-119">Emulator Express is not compatible with IIS Web Server.</span></span>
- <span data-ttu-id="fb62e-120">Il servizio cloud può contenere più ruoli, ma ogni ruolo è limitato a un'istanza.</span><span class="sxs-lookup"><span data-stu-id="fb62e-120">Your cloud service can contain multiple roles, but each role is limited to one instance.</span></span>
- <span data-ttu-id="fb62e-121">È possibile accedere ai numeri di porta inferiori a 1000.</span><span class="sxs-lookup"><span data-stu-id="fb62e-121">You can't access port numbers below 1000.</span></span> <span data-ttu-id="fb62e-122">Se si usa un provider di autenticazione che in genere usa una porta inferiore a 1000, potrebbe essere necessario modificare questo valore per i numeri di porta superiori a 1000.</span><span class="sxs-lookup"><span data-stu-id="fb62e-122">If you use an authentication provider that normally uses a port below 1000, you might need to change this value to a port number that's above 1000.</span></span>
- <span data-ttu-id="fb62e-123">Qualsiasi limitazione dell'emulatore di calcolo di Azure si applica anche all'emulatore Express.</span><span class="sxs-lookup"><span data-stu-id="fb62e-123">Any limitations that apply to the Azure Compute Emulator also apply to Emulator Express.</span></span> <span data-ttu-id="fb62e-124">Ad esempio, non si può disporre di più di 50 istanze del ruolo per ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fb62e-124">For example, you can't have more than 50 role instances per deployment.</span></span> <span data-ttu-id="fb62e-125">Per altre informazioni sull'emulatore completo di Azure, vedere [Eseguire un'applicazione Azure nell'emulatore di calcolo](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span><span class="sxs-lookup"><span data-stu-id="fb62e-125">For more information about the Azure Compute Emulator, see [Run an Azure Application in the Compute Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb62e-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fb62e-126">Next steps</span></span>
[<span data-ttu-id="fb62e-127">Debug dei servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="fb62e-127">Debugging Azure cloud services</span></span>](https://msdn.microsoft.com/library/azure/ee405479.aspx)
