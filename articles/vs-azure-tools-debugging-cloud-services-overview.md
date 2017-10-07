---
title: servizi cloud aaaOptions per il debug di Azure | Documenti Microsoft
description: Debug dei servizi cloud di Azure
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 80755da7-8350-4f5c-97ce-2962beabb36d
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/18/2017
ms.author: kraigb
ms.openlocfilehash: 8b7779ca33cfd82fd5fbccf229ea822c311bdea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="learn-hello-various-ways-toodebug-an-azure-cloud-service"></a>Informazioni su hello vari modi toodebug un servizio cloud di Azure
In questo articolo fornisce collegamenti toohello varie modi toodebug un servizio cloud di Azure. 

## <a name="debugging-an-azure-cloud-service-in-visual-studio"></a>Debug di un servizio cloud di Azure in Visual Studio
È possibile risparmiare tempo e denaro utilizzando toodebug emulatore di calcolo di Azure hello il servizio cloud in un computer locale. Eseguendo il debug di un servizio in locale prima della distribuzione, è possibile migliorare l'affidabilità e le prestazioni senza pagare per il tempo di calcolo. È tuttavia possibile che si verifichino alcuni errori solo quando si esegue un servizio cloud in Azure. Il debug di errori che si verificano solo quando si esegue un servizio cloud in Azure possono essere eseguiti abilitando il debug remoto quando si pubblica il servizio e connettendo quindi l'istanza del ruolo tooa debugger hello. Per ulteriori informazioni, vedere il [Debug del servizio cloud nel computer locale](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer).

## <a name="using-azure-diagnostics"></a>Uso di Diagnostica di Azure 
È possibile utilizzare diagnostica Azure toolog informazioni dall'esecuzione di codice all'interno di ruoli, ruoli hello esecuzione nell'ambiente di sviluppo hello o in Azure. Per altre informazioni, vedere [Abilitazione di Diagnostica di Azure in servizi cloud di Azure](http://go.microsoft.com/fwlink/p/?LinkId=400450).

## <a name="using-intellitrace"></a>Uso di IntelliTrace 
Se si utilizza ruoli di Visual Studio Enterprise toowrite destinati a .NET Framework 4.5, è possibile abilitare IntelliTrace nel momento in hello che si distribuisce un servizio cloud di Azure da Visual Studio. IntelliTrace fornisce un log che è possibile utilizzare con Visual Studio toodebug l'applicazione come se fosse in esecuzione in Azure. Per altre informazioni, vedere [Debug di un servizio cloud pubblicato con IntelliTrace e Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623016).

## <a name="remote-debugging"></a>Debug remoto 
È possibile abilitare il debug remoto nei servizi cloud in fase di hello quando si distribuisce il servizio cloud hello da Visual Studio. Se si sceglie tooenable il debug remoto per una distribuzione, i servizi di debug remoti vengono installati nelle macchine virtuali hello che eseguono ogni istanza del ruolo. Questi servizi, ad esempio `msvsmon.exe`, non influiscono sulle prestazioni né producono costi aggiuntivi. Per ulteriori informazioni, vedere [il Debug di un servizio cloud in Azure](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure).

## <a name="next-steps"></a>Passaggi successivi
- [Debug di un servizio cloud di Azure o una macchina virtuale in Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md) -informazioni sul supporto hello di toodebug Azure come i servizi cloud.
