---
title: un hub eventi Azure aaaCreate | Documenti Microsoft
description: Creare uno spazio dei nomi dell'hub eventi di Azure e un hub di eventi utilizzando hello portale di Azure
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: sethm
ms.openlocfilehash: 9a8b7711e2ca7d112e24be19353d43c365ff6935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-hello-azure-portal"></a>Creare uno spazio dei nomi dell'hub eventi e un hub di eventi utilizzando hello portale di Azure

## <a name="create-an-event-hubs-namespace"></a>Creare uno spazio dei nomi di Hub eventi
1. Accesso toohello [portale di Azure][Azure portal], fare clic su **New** in hello in alto a sinistra della schermata di hello.
1. Fare clic su **Internet delle cose** e quindi su **Hub eventi**.
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. In hello **Crea spazio dei nomi** pannello, immettere un nome di spazio dei nomi. sistema di Hello controlla immediatamente toosee se nome hello è disponibile.
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. Dopo il nome di spazio dei nomi che hello è disponibile, scegliere hello tariffario (Standard o Basic). Inoltre, è possibile scegliere una sottoscrizione di Azure, un gruppo di risorse e una posizione nella quale risorsa hello toocreate. 
1. Fare clic su **crea** dello spazio dei nomi di toocreate hello. È possibile toowait per le risorse hello di effettuare il provisioning di hello sistema toofully qualche minuto.
2. Hello portale selezionare nell'elenco degli spazi dei nomi hello appena creato spazio dei nomi.
2. Fare clic su **Criteri di accesso condivisi** e quindi su **RootManageSharedAccessKey**.
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. Fare clic su hello toocopy pulsante Copia di hello **RootManageSharedAccessKey** Appunti toohello stringa di connessione. Salvare la stringa di connessione in un percorso temporaneo, ad esempio Blocco note, toouse in un secondo momento.
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a>Creare un hub eventi

1. Nell'elenco dello spazio dei nomi di hub eventi hello, fare clic su spazio dei nomi hello appena creato.      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. Nel Pannello di hello dello spazio dei nomi, fare clic su **hub eventi**.
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. Nella parte superiore di hello del Pannello di hello, fare clic su **aggiungere Hub eventi**.
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. Digitare un nome per l'hub eventi e quindi fare clic su **Crea**.
   
    ![](./media/event-hubs-create/create-event-hub5.png)

È stato creato l'hub di eventi e disporre le stringhe di connessione hello è necessario toosend eventi e di ricezione.

## <a name="next-steps"></a>Passaggi successivi
toolearn più sugli hub di eventi, visitare i collegamenti:

* [Panoramica di Hub eventi](event-hubs-what-is-event-hubs.md)
* [Panoramica dell'API di Hub eventi](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/