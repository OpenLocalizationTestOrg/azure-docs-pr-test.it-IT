---
title: Prerequisiti aaaNon-tecnici per la creazione di un'offerta per hello Azure Marketplace | Documenti Microsoft
description: Comprendere i requisiti di hello per la creazione e distribuzione di un toohello offerta Azure Marketplace per altri utenti toopurchase.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3dae463b-8f48-4f52-8fa8-4e3975f09f43
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 08/18/2016
ms.author: hascipio
ms.openlocfilehash: 472096863084cc58dc921313419ab60b1a08a3bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="general-prerequisites-for-creating-an-offer-for-hello-azure-marketplace"></a>Prerequisiti generali per la creazione di un'offerta per hello Azure Marketplace
Comprendere i prerequisiti hello generale business-incentrato sui processi che sono necessari toomove avanti con hello offrono il processo di creazione.

## <a name="ensure-that-you-are-registered-as-a-seller-with-microsoft"></a>Assicurarsi di essere registrati come venditore con Microsoft
Per istruzioni dettagliate su come registrare un account del venditore con Microsoft, visitare troppo[creazione di Account e la registrazione](marketplace-publishing-accounts-creation-registration.md).

* **Se l'azienda è già registrata come un venditore in hello Dev Center e si desidera una nuova offerta toocreate** quindi account di accesso toohello pubblicazione portale con hello stesso id con il centro per sviluppatori viene eseguita la registrazione di posta elettronica. Questo passaggio è obbligatorio in modo che hello portale Dev Center e la pubblicazione sono collegate tra loro.
* **Se l'azienda è già registrata come un venditore in hello Dev Center e si desidera un'offerta esistente, tooedit** quindi entrambi toohello accesso pubblicazione portale con account di amministratore hello o con un account che viene aggiunto come co-amministratore in hello portale di pubblicazione . Passaggi tooadd un account di co-amministratore è indicato di seguito.

## <a name="steps-tooadd-a-co-admin-in-hello-publishing-portal"></a>Passaggi tooadd co-amministratore in hello portale di pubblicazione
Gli amministratori di hello pubblicazione portale è possibile aggiungere altri membri della società hello, che lavorano su un'applicazione hello, come co-amministratore in hello hello portale di pubblicazione. **Supponendo che siano salve,** riportati di seguito vengono hello passaggi tooadd un co-amministratore.

> [!NOTE]
> Per i nuovi utenti, prima è necessario aggiungere un coamministratore hello pubblicazione portale, assicurarsi di avere creato almeno un'applicazione in hello portale di pubblicazione. Questa operazione è necessaria come hello **EDITORI** scheda viene visualizzata solo dopo la creazione di almeno un'applicazione in hello portale di pubblicazione.
> 
> 

1. Verificare che l'id di posta elettronica hello co-amministratore sia un account(MSA) Microsoft. In caso contrario, registrarlo come MSA mediante questo [collegamento](https://signup.live.com/signup?uaid=0089f09ccae94043a0f07c2aaf928831&lic=1).
2. Verificare che sia presente almeno un'applicazione con account di amministratore hello prima di tentare di tooadd un co-amministratore.
3. Dopo aver hello sopra i passaggi dell'operazione, account di accesso toohello pubblicazione portale con id di posta elettronica hello co-amministratore e quindi disconnettersi.
4. Ora di accesso toohello pubblicazione portale con id di posta elettronica amministratore hello.
5. Passare tooPublishers -> -> account selezionare amministratori -> Aggiungi co-salve (schermata specificato di seguito)
   
    ![disegno](media/marketplace-publishing-pre-requisites/imgAddAdmin_05.png)
6. Verificare che posta elettronica ID fornito in hello varie fasi del processo (ad esempio Dev Center, portale di pubblicazione) di pubblicazione hello vengono monitorate per qualsiasi comunicazione da Microsoft.
7. Per la registrazione in Dev Center, evitare di usare un account associato a una singola persona. Si consiglia di procedere in questo modo per eliminare la dipendenza da una singola persona.
8. In caso di problemi durante la registrazione in Dev Center, creare un ticket mediante questo [collegamento](https://developer.microsoft.com/en-us/windows/support).

## <a name="steps-toodelete-a-co-admin-in-hello-publishing-portal"></a>Passaggi toodelete co-amministratore in hello portale di pubblicazione
**Supponendo che siano salve,** riportati di seguito viene hello passaggi toodelete un co-amministratore.

1. Account di accesso toohello pubblicazione portale con id di posta elettronica amministratore hello.
2. Passare troppo**editori** -> account -> Seleziona **amministratori** -> **coamministratori**.
3. Fare clic su hello **X** pulsante Avanti toohello coamministratore si desidera eliminare tot (schermata specificato di seguito).
   
    ![disegno](media/marketplace-publishing-pre-requisites/imgDeleteAdmin_03.png)

> [!IMPORTANT]
> Non si dispone informazioni fiscali e bank società toocomplete se si intendono offerte gratis toopublish (o porta la propria licenza).
> 
> registrazione di società Hello deve essere completato tooget avviato. Tuttavia, quando viene utilizzato l'azienda alle informazioni di imposte e bank hello nell'account di Microsoft Developer hello, gli sviluppatori di hello possono iniziare a lavorare sulla creazione di immagini di macchina virtuale hello in hello [portale pubblicazione](https://publish.windowsazure.com), ottenere il certificato, e verificata nell'ambiente di gestione temporanea Azure hello. Sarà necessario hello venditore completo account approvazione solo per l'ultimo passaggio di hello della pubblicazione il toohello offerta Azure Marketplace.
> 
> 

## <a name="acquire-an-azure-pay-as-you-go-subscription"></a>Acquisire una sottoscrizione di Azure con pagamento in base al consumo
Si tratta di sottoscrizione hello che consentono di utilizzare toocreate le immagini di macchina virtuale e mano su hello immagini toohello [Azure Marketplace](https://azure.microsoft.com/marketplace/). Se non si dispone di una sottoscrizione esistente, iscriversi su https://account.windowsazure.com/signup?offer=ms-azr-0003p.

## <a name="sell-from-countries"></a>Paesi di origine della vendita
> [!WARNING]
> In ordine toosell dei servizi sul hello Azure Marketplace, è necessario assicurarsi che l'entità registrato è uno dei paesi hello approvato "vendere-from". Questa limitazione viene applicata per motivi legati ai proventi e alla tassazione. Si sta impegnando nella ricerca tooexpand questo elenco di paesi in hello prossimo futuro, pertanto in futuro. Per l'elenco completo di hello, vedere sezione 1b di hello [criteri la partecipazione di Azure Marketplace](http://go.microsoft.com/fwlink/?LinkID=526833).
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Quando vengono soddisfatti i prerequisiti non tecnico hello, accanto è offerta hello prerequisiti tecnici specifici. Fare clic hello collegamento toohello articolo per il tipo di offerta rispettivi hello che si desidera toocreate per hello Azure Marketplace.

* [Prerequisiti tecnici per le macchine virtuali](marketplace-publishing-vm-image-creation-prerequisites.md)
* [Prerequisiti tecnici per il modello di soluzione](marketplace-publishing-solution-template-creation-prerequisites.md)

## <a name="see-also"></a>Vedere anche
* [Guida introduttiva: come toopublish un toohello offerta Azure Marketplace](marketplace-publishing-getting-started.md)

