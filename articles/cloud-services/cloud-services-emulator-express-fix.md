---
title: Installare l'emulatore Express per eseguire il debug di applicazioni di Servizi cloud in Visual Studio | Documentazione Microsoft
description: Descrive come installare C++ Redistributable per abilitare l'emulatore Express in Visual Studio
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
ms.openlocfilehash: 05d672dcb1335c617bb8d8cae43947bcd5e9ab3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-emulator-express-to-debug-cloud-services-application-in-vs-2017"></a><span data-ttu-id="7ef08-103">Usare l'emulatore Express per eseguire il debug di applicazioni di Servizi cloud in Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="7ef08-103">Use Emulator Express to debug Cloud Services application in VS 2017</span></span>
<span data-ttu-id="7ef08-104">Questo articolo spiega come usare l'emulatore Express per eseguire il debug di applicazioni di Servizi cloud in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="7ef08-104">This article explains how to use Emulator Express to debug Cloud Services applications in VS 2017.</span></span>

## <a name="background-context"></a><span data-ttu-id="7ef08-105">Contesto di fondo</span><span class="sxs-lookup"><span data-stu-id="7ef08-105">Background context</span></span>
<span data-ttu-id="7ef08-106">L'emulatore Express viene usato per impostazione predefinita per il debug di ruoli Web e di lavoro di Servizi cloud in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7ef08-106">Emulator Express is used by default for debugging Cloud Services Web and Worker roles in Visual Studio.</span></span> <span data-ttu-id="7ef08-107">Questa impostazione viene specificata nella pagina delle proprietà del progetto di Servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="7ef08-107">This setting is specified in the Cloud Services project properties page.</span></span>

![Aprire le proprietà del progetto][0]

![L'emulatore Express è selezionato per impostazione predefinita][1]

<span data-ttu-id="7ef08-110">Il [Visual C++ Redistributable] [ Visual C++ Redistributable] per Visual Studio è richiesto dall'emulatore express.</span><span class="sxs-lookup"><span data-stu-id="7ef08-110">The [Visual C++ Redistributable][Visual C++ Redistributable] for Visual Studio is required by Emulator express.</span></span> <span data-ttu-id="7ef08-111">Non viene attualmente installato con il carico di lavoro di Azure.</span><span class="sxs-lookup"><span data-stu-id="7ef08-111">Currently it is not installed with the Azure workload.</span></span> <span data-ttu-id="7ef08-112">Quando si preme F5 per eseguire il debug di applicazioni di Servizi cloud, Visual Studio chiederà di installare il componente e procedere con il debug.</span><span class="sxs-lookup"><span data-stu-id="7ef08-112">Upon F5 gesture to debug a Cloud Services applications, Visual Studio would prompt to install this component and proceed with debugging.</span></span>

![Prompt per l'installazione di C++ Redistributable][2]

<span data-ttu-id="7ef08-114">Fare clic su Sì per installare C++ Redistributable.</span><span class="sxs-lookup"><span data-stu-id="7ef08-114">Click Yes to install C++ Redistributable.</span></span>

![Installare C++ Redistributable][3]

<span data-ttu-id="7ef08-116">Premere di nuovo F5 per avviare le sessioni di debug.</span><span class="sxs-lookup"><span data-stu-id="7ef08-116">Press F5 again to launch debugging sessions.</span></span>

![Avviare il debug][4]

![Debug completato][5]

> <span data-ttu-id="7ef08-119">Nota: l'installazione di Visual C++ Redistributable viene eseguita una sola volta.</span><span class="sxs-lookup"><span data-stu-id="7ef08-119">Note: Installing Visual C++ Redistributable is a onetime effort.</span></span> <span data-ttu-id="7ef08-120">Se venisse effettuato l'aggiornamento da una versione precedente di Azure SDK e l'emulatore Express fosse già installato, questo problema non si verificherebbe.</span><span class="sxs-lookup"><span data-stu-id="7ef08-120">If you were upgrading from an older version of Azure SDK and have installed Emulator Express, then you won’t encounter this problem.</span></span>
> 
> 

## <a name="manual-workaround"></a><span data-ttu-id="7ef08-121">Soluzione alternativa manuale</span><span class="sxs-lookup"><span data-stu-id="7ef08-121">Manual workaround</span></span>
<span data-ttu-id="7ef08-122">È inoltre possibile installare il [Visual C++ Redistributable] [ Visual C++ Redistributable] manualmente ed equivale verrà applicato come come Visual Studio installato nel sistema.</span><span class="sxs-lookup"><span data-stu-id="7ef08-122">You can also install the [Visual C++ Redistributable][Visual C++ Redistributable] manually and same effect will be applied as how Visual Studio installed it on your system.</span></span>

<span data-ttu-id="7ef08-123">[vcredist_x86.exe][vcredist_x86.exe]</span><span class="sxs-lookup"><span data-stu-id="7ef08-123">[vcredist_x86.exe][vcredist_x86.exe]</span></span>

<span data-ttu-id="7ef08-124">[VCRedist_x64.exe][vcredist_x64.exe]</span><span class="sxs-lookup"><span data-stu-id="7ef08-124">[vcredist_x64.exe][vcredist_x64.exe]</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ef08-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7ef08-125">Next Steps</span></span>
<span data-ttu-id="7ef08-126">Ulteriori informazioni sull'utilizzo di emulatore di calcolo di Azure per il debug delle applicazioni di servizi Cloud in Visual Studio: [usando Emulator Express per l'esecuzione e il debug di un servizio cloud in un computer locale][Using Emulator Express to run and debug a cloud service on a local machine]</span><span class="sxs-lookup"><span data-stu-id="7ef08-126">Learn more about using Azure Computer Emulator to debug your Cloud Services applications in Visual Studio: [Using Emulator Express to run and debug a cloud service on a local machine][Using Emulator Express to run and debug a cloud service on a local machine]</span></span>

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express to run and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
