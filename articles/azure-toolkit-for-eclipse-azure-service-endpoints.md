---
title: aaaAzure gli endpoint del servizio
description: Descrive le impostazioni di Endpoint del servizio Azure hello in hello Azure Toolkit per Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 357aa56409a894719077f2c8f302575c8ebb6883
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-endpoints"></a>Endpoint del servizio di Azure
Gli endpoint del servizio Azure determinano che se l'applicazione è distribuita tooand gestita dalla piattaforma Azure globale hello, Azure gestito da 21Vianet in Cina o una privata piattaforma Azure. Hello **gli endpoint del servizio** finestra di dialogo consente toospecify che si desidera toouse endpoint del servizio. hello tooopen **gli endpoint del servizio** finestra di dialogo, in Eclipse, fare clic su **finestra**, fare clic su **preferenze**, espandere **Azure**, quindi fare clic su **Gli endpoint del servizio**. Hello impostazione **Active Set** campo determina quale servizio di Azure verranno utilizzati l'endpoint per hello Azure progetti nell'area di lavoro corrente.

Hello seguente illustra la hello **gli endpoint del servizio** finestra di dialogo.

![][ic719493]

## <a name="tooset-hello-service-endpoints"></a>endpoint del servizio hello tooset
In hello **gli endpoint del servizio** finestra di dialogo, eseguire una di hello seguenti azioni:

* Se si desidera toouse hello piattaforma Azure globale, da hello **Active Set** elenco a discesa, seleziona **windowsazure.com** e fare clic su **OK**.

* Se si desidera toouse Azure gestito da 21Vianet in Cina, da hello **Active Set** elenco a discesa, seleziona **windowsazure.cn (China)** e fare clic su **OK**.

* Se si desidera toouse una piattaforma Azure privata:

  1. Fare clic su **Modifica**.

  2. Verrà visualizzata una finestra di dialogo che informa che hello **gli endpoint del servizio** finestra di dialogo verrà chiusa e verranno aperto hello preferenza set di file. Fare clic su **OK**.

  3. Nel file preferencesets.xml hello, creare un nuovo `preferenceset` elemento. Per questo nuovo elemento, creare `name`, `blob`, `management`, `portalURL` e `publishsettings` gli attributi e aggiungere i valori per tale piattaforma Azure privata tooyour corrispondono. È possibile utilizzare i valori hello forniti hello esistenti `preferenceset` elementi come modelli. **Nota**: hello valore utilizzato per hello `blob` attributo deve contenere il testo hello "blob" nell'URL hello.

  4. Salvare e chiudere preferencesets.xml.

  5. Riaprire hello **gli endpoint del servizio** finestra di dialogo.

  6. Da hello **Active Set** dall'elenco a discesa selezionare hello attivo imposta creata e fare clic su **OK**.

  7. Dopo aver creato la piattaforma Azure privata `preferenceset` elemento, è possibile modificare hello tooit di valori assegnati facendo hello **modifica** pulsante hello **Endpoint dei servizi** finestra di dialogo. È inoltre possibile creare più elementi `preferenceset` della piattaforma Azure privata, se lo si desidera.

## <a name="see-also"></a>Vedere anche
[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]

[L'installazione di hello Azure Toolkit per Eclipse][Installing hello Azure Toolkit for Eclipse] 

[Creare un'applicazione Hello World per Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
