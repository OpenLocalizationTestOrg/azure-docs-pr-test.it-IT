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
# <a name="use-emulator-express-toodebug-cloud-services-application-in-vs-2017"></a>Utilizzare Emulator Express toodebug servizi Cloud applicazione in Visual Studio 2017
Questo articolo viene illustrato come toouse Emulator Express toodebug servizi Cloud le applicazioni in VS 2017.

## <a name="background-context"></a>Contesto di fondo
L'emulatore Express viene usato per impostazione predefinita per il debug di ruoli Web e di lavoro di Servizi cloud in Visual Studio. Questa impostazione è specificata nella pagina delle proprietà di progetto servizi Cloud hello.

![Aprire le proprietà del progetto][0]

![L'emulatore Express è selezionato per impostazione predefinita][1]

Hello [Visual C++ Redistributable] [ Visual C++ Redistributable] per Visual Studio è richiesto dall'emulatore express. Attualmente non è installato con hello del carico di lavoro di Azure. Al momento F5 movimento toodebug applicazioni di servizi Cloud, Visual Studio verrà richiesto tooinstall questo componente e procedere con il debug.

![Prompt per l'installazione di C++ Redistributable][2]

Fare clic su Sì tooinstall C++ Redistributable.

![Installare C++ Redistributable][3]

Premere F5 nuovamente toolaunch le sessioni di debug.

![Avviare il debug][4]

![Debug completato][5]

> Nota: l'installazione di Visual C++ Redistributable viene eseguita una sola volta. Se venisse effettuato l'aggiornamento da una versione precedente di Azure SDK e l'emulatore Express fosse già installato, questo problema non si verificherebbe.
> 
> 

## <a name="manual-workaround"></a>Soluzione alternativa manuale
È inoltre possibile installare hello [Visual C++ Redistributable] [ Visual C++ Redistributable] manualmente ed equivale verrà applicato come come Visual Studio installato nel sistema.

[vcredist_x86.exe][vcredist_x86.exe]

[VCRedist_x64.exe][vcredist_x64.exe]

## <a name="next-steps"></a>Passaggi successivi
Ulteriori informazioni sull'utilizzo toodebug emulatore di calcolo di Azure le applicazioni di servizi Cloud in Visual Studio: [toorun uso di Emulator Express e debug di un servizio cloud in un computer locale][Using Emulator Express toorun and debug a cloud service on a local machine]

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
