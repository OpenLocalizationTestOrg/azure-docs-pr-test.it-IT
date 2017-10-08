---
title: aaaAccessing cloud privati di Azure con Visual Studio | Documenti Microsoft
description: Informazioni su come privato tooaccess risorse cloud con Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/19/2017
ms.author: kraigb
ms.openlocfilehash: 5cfd6439afdcf98c6f7d7f29ab6c4256ed02533a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a>Accesso ai cloud privati di Azure con Visual Studio
Per impostazione predefinita, Visual Studio supporta gli endpoint REST del cloud pubblico di Azure. In questo argomento, è illustrato toouse cloud il privata del certificato tooaccess - e interagire con: hello cloud privato da Visual Studio.

## <a name="tooaccess-a-private-azure-cloud-in-visual-studio"></a>tooaccess un Azure privato cloud in Visual Studio
1. In hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885) per cloud privato hello, scaricare il file di impostazioni di pubblicazione o contattare l'amministratore per un file di impostazioni di pubblicazione. Nella versione pubblica di hello di Azure, hello toodownload collegamento si tratta di [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/). (file scaricato hello deve avere l'estensione `.publishsettings`)

1. Aprire Visual Studio.

1. In **Esplora Server**, hello rapida **Azure** nodo e selezionare il menu di scelta rapida hello **Gestisci e filtra sottoscrizioni**.
   
    ![Comando Gestisci sottoscrizioni](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. In hello **Gestione sottoscrizioni Microsoft Azure** finestra di dialogo, seleziona hello **certificati** scheda e quindi selezionare **importazione**.
   
    ![Importazione di certificati di Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. In hello **Importa sottoscrizioni di Microsoft Azure** finestra di dialogo Seleziona **Sfoglia**.

    ![Pulsante nella finestra di dialogo Importa sottoscrizioni di Microsoft Azure hello Sfoglia](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. In hello **aprire** finestra di dialogo Sfoglia toohello directory in cui è salvato hello impostazioni di pubblicazione file, selezionare hello file e quindi seleziona **aprire**.

    ![Selezionare il file di impostazioni di pubblicazione hello](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. Quando restituito toohello **Importa sottoscrizioni di Microsoft Azure** finestra di dialogo Seleziona **importazione**.

    ![Importare il file di impostazioni di pubblicazione hello](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    Hello certificati sono importati dal file di impostazioni di pubblicazione hello in Visual Studio e ora è possibile interagire con le risorse di cloud privato.
   
## <a name="next-steps"></a>Passaggi successivi
- [Tooan pubblicazione servizio Cloud di Azure da Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- [Procedura: Scaricare e importare le impostazioni di pubblicazione e le informazioni sulla sottoscrizione](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)
