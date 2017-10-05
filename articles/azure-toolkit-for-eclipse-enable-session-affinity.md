---
title: "Abilitare l'affinità di sessione tramite il Toolkit di Azure per Eclipse"
description: "Informazioni su come abilitare l'affinità di sessione tramite il Toolkit di Azure per Eclipse"
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
ms.openlocfilehash: ab8623d6f9751ed6d71d9a5b1c0d5e939c442862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enable-session-affinity"></a>Abilitare l'affinità di sessione
Nel Toolkit di Azure per Eclipse, è possibile abilitare l'affinità di sessione HTTP, o "sessioni permanenti", per i ruoli. La figura seguente mostra la finestra di dialogo delle proprietà di **Bilanciamento del carico** utilizzata per abilitare la funzionalità di affinità di sessione:

![][ic719492]

## <a name="to-enable-session-affinity-for-your-role"></a>Per abilitare l'affinità di sessione per il ruolo
1. Fare clic con il tasto destro del mouse sul ruolo in (Esplora progetti) di Eclipse, scegliere **Azure**, quindi fare clic su **Load Balancing** (Bilanciamento del carico).

2. Nella finestra di dialogo **Proprietà per il bilanciamento del carico del WorkerRole1** :

   a. Controllare **Abilita l'affinità di sessione attiva HTTP (sessioni permanenti) per questo ruolo.**

   b. Per gli **Input endpoint to use** (Endpoint di input da usare) selezionare un endpoint di input da usare, ad esempio, **http (public:80, private:8080)**. L'applicazione deve usare questo endpoint come l’endpoint HTTP. È possibile abilitare più endpoint per il ruolo, ma è possibile selezionare solo uno di essi per supportare le sessioni permanenti.

   c. Ricompilare l'applicazione

Una volta abilitato, se si dispone di più di un'istanza del ruolo, le richieste HTTP provenienti da un determinato client continueranno ad essere gestite dalla stessa istanza del ruolo.

Il Toolkit di Eclipse lo consente installando un modulo IIS speciale denominato Application Request Routing (ARR) in tutte le istanze del ruolo. ARR reindirizza le richieste HTTP all'istanza del ruolo appropriato. Il toolkit riconfigura automaticamente l'endpoint selezionato in modo che il traffico HTTP in ingresso viene instradato al software ARR. Il toolkit crea anche un nuovo endpoint interno al quale server Java deve stare attenti per configurazione. Si tratta dell'endpoint usato da ARR per reindirizzare il traffico HTTP all'istanza del ruolo appropriato. In questo modo, ogni istanza del ruolo nella distribuzione multi-istanza funge da proxy inverso per tutte le altre istanze, abilitando le sessioni permanenti.

## <a name="notes-about-session-affinity"></a>Note sull'affinità di sessione
* L’affinità di sessione non funziona nell'emulatore di calcolo. Le impostazioni possono essere applicate nell'emulatore di calcolo senza interferire con il processo di compilazione o con l’esecuzione dell'emulatore di calcolo, ma la funzionalità di per sé non funziona nell'emulatore di calcolo.

* L’abilitazione dell’affinità di sessione comporterà un aumento della quantità di spazio nel disco preso dalla distribuzione in Azure, come software aggiuntivo verrà scaricato e installato nelle istanze del ruolo quando il servizio viene avviato nel cloud di Azure.

* Il tempo necessario per inizializzare ogni ruolo sarà maggiore.

* Verrà aggiunto un endpoint interno, che fungerà da rerouter di traffico, come indicato in precedenza.


## <a name="see-also"></a>Vedere anche
[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]

[Creare un'applicazione Hello World per Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Installazione di Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse] 

Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How to Maintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
