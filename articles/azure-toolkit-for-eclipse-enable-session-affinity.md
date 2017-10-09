---
title: "utilizzo di affinità di sessione aaaEnable hello Azure Toolkit per Eclipse"
description: "Informazioni su come l'affinità di sessione tooenable utilizzando hello Azure Toolkit per Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 523e728c58bda95e7af4b242e831694eb6d75cb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-session-affinity"></a>Abilitare l'affinità di sessione
All'interno di hello Azure Toolkit per Eclipse, è possibile abilitare l'affinità di sessione HTTP, o "sessioni permanenti", per i ruoli. Hello immagine seguente viene illustrato hello **il bilanciamento del carico** funzionalità affinità di sessione di proprietà finestra di dialogo utilizzata tooenable hello:

![][ic719492]

## <a name="tooenable-session-affinity-for-your-role"></a>tooenable l'affinità di sessione per il ruolo
1. Fare doppio clic su ruolo hello in Project Explorer di Eclipse, fare clic su **Azure**, quindi fare clic su **il bilanciamento del carico**.

2. In hello **proprietà per il bilanciamento del carico WorkerRole1** finestra di dialogo:

   a. Controllare **Abilita l'affinità di sessione attiva HTTP (sessioni permanenti) per questo ruolo.**

   b. Per **toouse endpoint di Input**, selezionare toouse un endpoint di input, ad esempio, **http (public: 80, private: 8080)**. L'applicazione deve usare questo endpoint come l’endpoint HTTP. È possibile abilitare più endpoint per il ruolo, ma è possibile selezionare solo uno di essi toosupport sessioni permanenti.

   c. Ricompilare l'applicazione

Una volta abilitato, se si dispone di più istanze di ruolo, le richieste HTTP provenienti da un client specifico continuerà gestita da hello stessa istanza del ruolo.

Hello Eclipse Toolkit lo consente installando un modulo IIS speciale denominato Application Request Routing (ARR) in ognuna delle istanze del ruolo. ARR reindirizza l'istanza del ruolo appropriata toohello le richieste HTTP. Hello toolkit riconfigura automaticamente l'endpoint hello selezionata in modo che il traffico HTTP in ingresso hello è primo toohello indirizzato ARR software. Hello toolkit crea anche un nuovo endpoint interno che toolisten configurato per il server Java. Ovvero endpoint hello utilizzato dall'istanza di ruolo appropriato di ARR tooreroute hello HTTP traffico toohello. In questo modo, ogni istanza del ruolo nella distribuzione multi-istanza funge da proxy inverso per tutti hello altri casi, l'abilitazione di sessioni permanenti.

## <a name="notes-about-session-affinity"></a>Note sull'affinità di sessione
* Affinità di sessione non funziona nell'emulatore di calcolo hello. Hello impostazioni possono essere applicate nell'emulatore di calcolo hello senza interferire con il processo di compilazione o dell'esecuzione dell'emulatore di calcolo, ma non funziona nell'emulatore di calcolo hello funzionalità hello stessa.

* Abilitazione di affinità di sessione comporterà un aumento della quantità di hello di spazio su disco occupato dalla distribuzione in Azure, come verrà scaricato e installato nelle istanze del ruolo quando il servizio viene avviato nel cloud di Azure hello software aggiuntivo.

* Hello ora tooinitialize ogni ruolo richiederà più tempo.

* Verrà aggiunto un endpoint interno, toofunction come rerouter un traffico, come indicato in precedenza.


## <a name="see-also"></a>Vedere anche
[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]

[Creare un'applicazione Hello World per Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

[L'installazione di hello Azure Toolkit per Eclipse][Installing hello Azure Toolkit for Eclipse] 

Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How tooMaintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
