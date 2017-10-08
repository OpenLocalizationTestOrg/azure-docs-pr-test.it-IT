---
title: aaaAdd archiviazione di Azure tramite i servizi connessi in Visual Studio | Documenti Microsoft
description: Aggiungere app tooyour di archiviazione di Azure tramite la finestra di dialogo di Visual Studio aggiungere servizi connessi hello
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 56b42063d86510b330e405108e28d50e6ba4da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a>Aggiunta dell’archiviazione di Azure tramite Servizi connessi di Visual Studio
Con Visual Studio, è possibile connettere uno qualsiasi dei seguenti tooAzure archiviazione utilizzando hello hello **aggiungere servizi connessi** finestra di dialogo:

- Servizio cloud C#
- Servizio mobile back-end .NET
- Sito Web ASP.NET
- Servizio ASP.NET Core
- Servizio Processo Web di Azure 

Hello funzionalità servizio connesso aggiunge tutti i riferimenti necessita hello e il progetto tooyour codice di connessione e modifica i file di configurazione in modo appropriato. 

Dopo il completamento, hello **aggiungere servizi connessi** finestra di dialogo viene visualizzata automaticamente la documentazione che riporta in dettaglio hello passaggi necessari toostart utilizzo di archiviazione blob, code e tabelle.

## <a name="connect-tooazure-storage-using-hello-connected-services-dialog"></a>La connessione di archiviazione tramite servizi connessi hello tooAzure finestra di dialogo
1. Aprire il progetto in Visual Studio

1. In **Esplora soluzioni**, hello rapida **servizi connessi** nodo, quindi scegliere il menu di scelta rapida hello e selezionare **Aggiungi servizio connesso**.
   
    ![Aggiunta di un servizio connesso di Azure](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. In hello **servizi connessi** selezionare **archiviazione Cloud con l'archiviazione di Azure**.
   
    ![Aggiungi Archiviazione di Azure](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. In hello **di archiviazione di Azure** finestra di dialogo, selezionare un account di archiviazione esistente e selezionare **Aggiungi**.
   
    Se è necessario un account di archiviazione toocreate, andare toohello successivo. In caso contrario, andare toostep 6.
    
    ![Aggiungere tooproject di account di archiviazione esistente](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. toocreate un account di archiviazione: 
   
   1. Selezionare **creare un nuovo Account di archiviazione** nella parte inferiore di hello della finestra di dialogo hello.

   1. Compilare hello **crea Account di archiviazione** finestra di dialogo e selezionare **crea**.
      
       ![Nuovo account di archiviazione di Azure](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. Quando hello **di archiviazione di Azure** viene visualizzata una finestra di dialogo, il nuovo account di archiviazione hello viene visualizzato nell'elenco di hello. Selezionare il nuovo account di archiviazione hello nell'elenco di hello e selezionare **Aggiungi**.

1. Hello archiviazione servizio connesso viene visualizzato sotto hello **riferimenti al servizio** nodo del progetto.
   
## <a name="how-your-project-is-modified"></a>Come viene modificato il progetto
Quando si termina dialogo hello, Visual Studio aggiunge i riferimenti e modifica alcuni file di configurazione. modifiche specifiche Hello dipendono dal tipo di progetto hello: 

- Progetti ASP.NET - [Risultati – Progetti ASP.NET](http://go.microsoft.com/fwlink/p/?LinkId=513126).
- Progetti ASP.NET 5 - [Risultati – Progetti ASP.NET 5](http://go.microsoft.com/fwlink/p/?LinkId=513124). 
- Progetti del servizio cloud (ruoli Web e ruoli di lavoro) [Risultati - Progetti del servizio cloud](http://go.microsoft.com/fwlink/p/?LinkId=516965).
- Progetti di tipo processo Web - [Risultati - Progetti di tipo processo Web](visual-studio/vs-storage-webjobs-what-happened.md).

## <a name="next-steps"></a>Passaggi successivi
- [Forum MSDN: Archiviazione di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [Blog del team di Archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage/).
- [Documentazione di Archiviazione di Azure](https://docs.microsoft.com/azure/storage/)
