---
title: aaaSetup emulatore express toodebug applicazioni di servizi Cloud in Visual Studio | Documenti Microsoft
description: Viene illustrato come tooinstall hello tooenable di C++ ridistribuibili Emulator Express in Visual Studio
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 22b20f7a-23f4-4f7f-b536-3bf1e01adcd1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 6fb506f0b1384f2e52310799eb5ae2a102d777bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-emulator-express-toodebug-cloud-services-application-in-vs-2017"></a><span data-ttu-id="0cc2a-103">Utilizzare Emulator Express toodebug servizi Cloud applicazione in Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="0cc2a-103">Use Emulator Express toodebug Cloud Services application in VS 2017</span></span>
<span data-ttu-id="0cc2a-104">Questo articolo viene illustrato come toouse Emulator Express toodebug servizi Cloud le applicazioni in VS 2017.</span><span class="sxs-lookup"><span data-stu-id="0cc2a-104">This article explains how toouse Emulator Express toodebug Cloud Services applications in VS 2017.</span></span>

## <a name="background-context"></a><span data-ttu-id="0cc2a-105">Contesto di fondo</span><span class="sxs-lookup"><span data-stu-id="0cc2a-105">Background context</span></span>
<span data-ttu-id="0cc2a-106">L'emulatore Express viene usato per impostazione predefinita per il debug di ruoli Web e di lavoro di Servizi cloud in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0cc2a-106">Emulator Express is used by default for debugging Cloud Services Web and Worker roles in Visual Studio.</span></span> <span data-ttu-id="0cc2a-107">Questa impostazione è specificata nella pagina delle proprietà di progetto servizi Cloud hello.</span><span class="sxs-lookup"><span data-stu-id="0cc2a-107">This setting is specified in hello Cloud Services project properties page.</span></span>

![Aprire le proprietà del progetto][0]

![L'emulatore Express è selezionato per impostazione predefinita][1]

<span data-ttu-id="0cc2a-110">Hello [Visual C++ Redistributable] [ Visual C++ Redistributable] per Visual Studio è richiesto dall'emulatore express.</span><span class="sxs-lookup"><span data-stu-id="0cc2a-110">hello [Visual C++ Redistributable][Visual C++ Redistributable] for Visual Studio is required by Emulator express.</span></span> <span data-ttu-id="0cc2a-111">Attualmente non è installato con hello del carico di lavoro di Azure.</span><span class="sxs-lookup"><span data-stu-id="0cc2a-111">Currently it is not installed with hello Azure workload.</span></span> <span data-ttu-id="0cc2a-112">Al momento F5 movimento toodebug applicazioni di servizi Cloud, Visual Studio verrà richiesto tooinstall questo componente e procedere con il debug.</span><span class="sxs-lookup"><span data-stu-id="0cc2a-112">Upon F5 gesture toodebug a Cloud Services applications, Visual Studio would prompt tooinstall this component and proceed with debugging.</span></span>

![Prompt per l'installazione di C++ Redistributable][2]

<span data-ttu-id="0cc2a-114">Fare clic su Sì tooinstall C++ Redistributable.</span><span class="sxs-lookup"><span data-stu-id="0cc2a-114">Click Yes tooinstall C++ Redistributable.</span></span>

![Installare C++ Redistributable][3]

<span data-ttu-id="0cc2a-116">Premere F5 nuovamente toolaunch le sessioni di debug.</span><span class="sxs-lookup"><span data-stu-id="0cc2a-116">Press F5 again toolaunch debugging sessions.</span></span>

![Avviare il debug][4]

![Debug completato][5]

> <span data-ttu-id="0cc2a-119">Nota: l'installazione di Visual C++ Redistributable viene eseguita una sola volta.</span><span class="sxs-lookup"><span data-stu-id="0cc2a-119">Note: Installing Visual C++ Redistributable is a onetime effort.</span></span> <span data-ttu-id="0cc2a-120">Se venisse effettuato l'aggiornamento da una versione precedente di Azure SDK e l'emulatore Express fosse già installato, questo problema non si verificherebbe.</span><span class="sxs-lookup"><span data-stu-id="0cc2a-120">If you were upgrading from an older version of Azure SDK and have installed Emulator Express, then you won’t encounter this problem.</span></span>
> 
> 

## <a name="manual-workaround"></a><span data-ttu-id="0cc2a-121">Soluzione alternativa manuale</span><span class="sxs-lookup"><span data-stu-id="0cc2a-121">Manual workaround</span></span>
<span data-ttu-id="0cc2a-122">È inoltre possibile installare hello [Visual C++ Redistributable] [ Visual C++ Redistributable] manualmente ed equivale verrà applicato come come Visual Studio installato nel sistema.</span><span class="sxs-lookup"><span data-stu-id="0cc2a-122">You can also install hello [Visual C++ Redistributable][Visual C++ Redistributable] manually and same effect will be applied as how Visual Studio installed it on your system.</span></span>

<span data-ttu-id="0cc2a-123">[vcredist_x86.exe][vcredist_x86.exe]</span><span class="sxs-lookup"><span data-stu-id="0cc2a-123">[vcredist_x86.exe][vcredist_x86.exe]</span></span>

<span data-ttu-id="0cc2a-124">[VCRedist_x64.exe][vcredist_x64.exe]</span><span class="sxs-lookup"><span data-stu-id="0cc2a-124">[vcredist_x64.exe][vcredist_x64.exe]</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cc2a-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0cc2a-125">Next Steps</span></span>
<span data-ttu-id="0cc2a-126">Ulteriori informazioni sull'utilizzo toodebug emulatore di calcolo di Azure le applicazioni di servizi Cloud in Visual Studio: [toorun uso di Emulator Express e debug di un servizio cloud in un computer locale][Using Emulator Express toorun and debug a cloud service on a local machine]</span><span class="sxs-lookup"><span data-stu-id="0cc2a-126">Learn more about using Azure Computer Emulator toodebug your Cloud Services applications in Visual Studio: [Using Emulator Express toorun and debug a cloud service on a local machine][Using Emulator Express toorun and debug a cloud service on a local machine]</span></span>

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express toorun and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
