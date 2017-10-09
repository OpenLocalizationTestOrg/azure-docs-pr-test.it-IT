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
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a>Con Emulator Express toorun ed eseguire il debug di Azure servizio cloud in un computer locale
Con l'emulatore Express, è possibile testare ed eseguire il debug di un servizio cloud senza eseguire Visual Studio come amministratore. È possibile impostare il toouse impostazioni progetto entrambi Emulator Express o hello emulatore completo, a seconda dei requisiti di hello del servizio cloud. Per ulteriori informazioni sull'emulatore completo hello, vedere [eseguire un'applicazione Azure nell'emulatore di calcolo hello](storage/common/storage-use-emulator.md).

## <a name="using-emulator-express-in-visual-studio"></a>Uso dell'emulatore Express in Visual Studio
Quando si crea un progetto di Azure in Azure SDK 2.3 o versione successiva, l'emulatore Express è selezionato automaticamente. Per i progetti esistenti creati con una versione precedente di hello Azure SDK, usare hello seguendo i passaggi tooselect Emulator Express:

1. Creare o aprire un progetto del servizio cloud di Azure in Visual Studio.

1. In **Esplora**, fare clic sul progetto hello e selezionare il menu di scelta rapida hello **proprietà**.

1. Nelle pagine delle proprietà progetti hello, selezionare hello **Web** scheda.

    ![Proprietà di un progetto di servizio cloud di Azure](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. In **Server di sviluppo locale**, scegliere **Usa l'opzione IIS Express**.

1. In **Emulatore**selezionare **Usa emulatore Express**.
   
1. toolaunch hello Emulator Express, eseguire hello comando al prompt di comando seguente: 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a>Limitazioni dell'emulatore Express
limitazioni di Emulator Express è note Hello seguenti problemi: 

- L'emulatore Express non è compatibile con il Server Web IIS.
- Il servizio cloud può contenere più ruoli, ma ogni ruolo è limitato tooone istanza.
- È possibile accedere ai numeri di porta inferiori a 1000. Se si utilizza un provider di autenticazione che in genere utilizza una porta inferiore a 1000, potrebbe essere necessario toochange questo numero di porta tooa valore di sopra di 1000.
- Qualsiasi limitazione applicabile toohello emulatore di calcolo di Azure si applicano anche tooEmulator Express. Ad esempio, non si può disporre di più di 50 istanze del ruolo per ogni distribuzione. Per ulteriori informazioni su hello emulatore di calcolo di Azure, vedere [eseguire un'applicazione Azure nell'emulatore di calcolo hello](http://go.microsoft.com/fwlink/p/?LinkId=623050).

## <a name="next-steps"></a>Passaggi successivi
[Debug dei servizi cloud di Azure](https://msdn.microsoft.com/library/azure/ee405479.aspx)
