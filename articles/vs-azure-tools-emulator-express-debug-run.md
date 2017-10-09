---
title: servizio in un computer locale di cloud aaaUsing Emulator Express toorun ed eseguire il debug di Azure | Documenti Microsoft
description: Con Emulator Express toorun e debug di un servizio cloud in un computer locale
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
ms.openlocfilehash: d89a0fc2dce42b4a2d2f93f9c4ff0482af924ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a><span data-ttu-id="487cd-103">Con Emulator Express toorun ed eseguire il debug di Azure servizio cloud in un computer locale</span><span class="sxs-lookup"><span data-stu-id="487cd-103">Using Emulator Express toorun and debug an Azure cloud service on a local machine</span></span>
<span data-ttu-id="487cd-104">Con l'emulatore Express, è possibile testare ed eseguire il debug di un servizio cloud senza eseguire Visual Studio come amministratore.</span><span class="sxs-lookup"><span data-stu-id="487cd-104">By using Emulator Express, you can test and debug a cloud service without running Visual Studio as an administrator.</span></span> <span data-ttu-id="487cd-105">È possibile impostare il toouse impostazioni progetto entrambi Emulator Express o hello emulatore completo, a seconda dei requisiti di hello del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="487cd-105">You can set your project settings toouse either Emulator Express or hello full emulator, depending on hello requirements of your cloud service.</span></span> <span data-ttu-id="487cd-106">Per ulteriori informazioni sull'emulatore completo hello, vedere [eseguire un'applicazione Azure nell'emulatore di calcolo hello](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="487cd-106">For more information about hello full emulator, see [Run an Azure Application in hello Compute Emulator](storage/common/storage-use-emulator.md).</span></span>

## <a name="using-emulator-express-in-visual-studio"></a><span data-ttu-id="487cd-107">Uso dell'emulatore Express in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="487cd-107">Using Emulator Express in Visual Studio</span></span>
<span data-ttu-id="487cd-108">Quando si crea un progetto di Azure in Azure SDK 2.3 o versione successiva, l'emulatore Express è selezionato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="487cd-108">When you create an Azure project in Azure SDK 2.3 or later, Emulator Express is automatically used.</span></span> <span data-ttu-id="487cd-109">Per i progetti esistenti creati con una versione precedente di hello Azure SDK, usare hello seguendo i passaggi tooselect Emulator Express:</span><span class="sxs-lookup"><span data-stu-id="487cd-109">For existing projects that were created with an earlier version of hello Azure SDK, use hello following steps tooselect Emulator Express:</span></span>

1. <span data-ttu-id="487cd-110">Creare o aprire un progetto del servizio cloud di Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="487cd-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="487cd-111">In **Esplora**, fare clic sul progetto hello e selezionare il menu di scelta rapida hello **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="487cd-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>

1. <span data-ttu-id="487cd-112">Nelle pagine delle proprietà progetti hello, selezionare hello **Web** scheda.</span><span class="sxs-lookup"><span data-stu-id="487cd-112">In hello projects properties pages, select hello **Web** tab.</span></span>

    ![Proprietà di un progetto di servizio cloud di Azure](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. <span data-ttu-id="487cd-114">In **Server di sviluppo locale**, scegliere **Usa l'opzione IIS Express**.</span><span class="sxs-lookup"><span data-stu-id="487cd-114">Under **Local Development Server**, select **Use IIS Express option**.</span></span>

1. <span data-ttu-id="487cd-115">In **Emulatore**selezionare **Usa emulatore Express**.</span><span class="sxs-lookup"><span data-stu-id="487cd-115">Under **Emulator**, select **Use Emulator Express**.</span></span>
   
1. <span data-ttu-id="487cd-116">toolaunch hello Emulator Express, eseguire hello comando al prompt di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="487cd-116">toolaunch hello Emulator Express, run hello following command at a command prompt:</span></span> 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a><span data-ttu-id="487cd-117">Limitazioni dell'emulatore Express</span><span class="sxs-lookup"><span data-stu-id="487cd-117">Emulator Express limitations</span></span>
<span data-ttu-id="487cd-118">limitazioni di Emulator Express è note Hello seguenti problemi:</span><span class="sxs-lookup"><span data-stu-id="487cd-118">hello following issues are known limitations of Emulator Express:</span></span> 

- <span data-ttu-id="487cd-119">L'emulatore Express non è compatibile con il Server Web IIS.</span><span class="sxs-lookup"><span data-stu-id="487cd-119">Emulator Express is not compatible with IIS Web Server.</span></span>
- <span data-ttu-id="487cd-120">Il servizio cloud può contenere più ruoli, ma ogni ruolo è limitato tooone istanza.</span><span class="sxs-lookup"><span data-stu-id="487cd-120">Your cloud service can contain multiple roles, but each role is limited tooone instance.</span></span>
- <span data-ttu-id="487cd-121">È possibile accedere ai numeri di porta inferiori a 1000.</span><span class="sxs-lookup"><span data-stu-id="487cd-121">You can't access port numbers below 1000.</span></span> <span data-ttu-id="487cd-122">Se si utilizza un provider di autenticazione che in genere utilizza una porta inferiore a 1000, potrebbe essere necessario toochange questo numero di porta tooa valore di sopra di 1000.</span><span class="sxs-lookup"><span data-stu-id="487cd-122">If you use an authentication provider that normally uses a port below 1000, you might need toochange this value tooa port number that's above 1000.</span></span>
- <span data-ttu-id="487cd-123">Qualsiasi limitazione applicabile toohello emulatore di calcolo di Azure si applicano anche tooEmulator Express.</span><span class="sxs-lookup"><span data-stu-id="487cd-123">Any limitations that apply toohello Azure Compute Emulator also apply tooEmulator Express.</span></span> <span data-ttu-id="487cd-124">Ad esempio, non si può disporre di più di 50 istanze del ruolo per ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="487cd-124">For example, you can't have more than 50 role instances per deployment.</span></span> <span data-ttu-id="487cd-125">Per ulteriori informazioni su hello emulatore di calcolo di Azure, vedere [eseguire un'applicazione Azure nell'emulatore di calcolo hello](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span><span class="sxs-lookup"><span data-stu-id="487cd-125">For more information about hello Azure Compute Emulator, see [Run an Azure Application in hello Compute Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span></span>

## <a name="next-steps"></a><span data-ttu-id="487cd-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="487cd-126">Next steps</span></span>
[<span data-ttu-id="487cd-127">Debug dei servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="487cd-127">Debugging Azure cloud services</span></span>](https://msdn.microsoft.com/library/azure/ee405479.aspx)
