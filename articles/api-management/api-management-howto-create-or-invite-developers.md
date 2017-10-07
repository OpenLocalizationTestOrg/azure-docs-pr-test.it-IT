---
title: aaaHow gestire gli account utente in Gestione API di Azure | Documenti Microsoft
description: Informazioni su come toocreate o invita gli utenti in Gestione API di Azure
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 078abfa5-1e4f-4c9d-b9c7-a172bd19c1a2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3966f4454e29621d7c615beefee352ec91b48b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-user-accounts-in-azure-api-management"></a>La modalità di account utente di toomanage in Gestione API di Azure
In Gestione API, gli sviluppatori sono utenti hello di hello API esposta tramite Gestione API. Questa guida Mostra toohow toocreate e invita gli sviluppatori toouse hello API e i prodotti che si apportano toothem disponibili con l'istanza di gestione API. Per informazioni sulla gestione degli account utente a livello di codice, vedere hello [entità utente](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentazione in hello [API REST di gestione](https://msdn.microsoft.com/library/azure/dn776326.aspx) riferimento.

## <a name="create-developer"> </a>Creare un nuovo sviluppatore
toocreate uno sviluppatore di nuovo, fare clic su **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API. Consente di procedere toohello portale di pubblicazione di gestione API. Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.

![Portale di pubblicazione][api-management-management-console]

Fare clic su **utenti** da hello **gestione API** menu hello a sinistra e quindi fare clic su **aggiungere utente**.

![Create developer][api-management-create-developer]

Immettere hello **posta elettronica**, **Password**, e **nome** nuovo sviluppatore hello e fare clic su **salvare**.

![Create developer][api-management-add-new-user]

Per impostazione predefinita, gli account appena creato per sviluppatori sono **Active**e associati hello **sviluppatori** gruppo.

![New developer][api-management-new-developer]

Gli account sviluppatore in un **active** lo stato può essere utilizzato tooaccess tutte le API di hello per le quali sono le sottoscrizioni. sviluppatore di tooassociate hello appena creato con altri gruppi aggiuntivi, vedere [come i gruppi con gli sviluppatori tooassociate][How tooassociate groups with developers].

## <a name="invite-developer"> </a>Invitare uno sviluppatore
tooinvite uno sviluppatore, fare clic su **utenti** da hello **gestione API** menu hello a sinistra e quindi fare clic su **invitare utente**.

![Invite developer][api-management-invite-developer]

Immettere l'indirizzo di posta elettronica e nome hello dello sviluppatore hello e fare clic su **invitare**.

![Invite developer][api-management-invite-developer-window]

Viene visualizzato un messaggio di conferma, ma developer hello appena invito non è disponibile nell'elenco di hello fino a dopo aver accettato l'invito hello. 

![Invite confirmation][api-management-invite-developer-confirmation]

Quando uno sviluppatore è visualizzato un messaggio, viene inviato un messaggio toohello developer. generato con un modello e personalizzabile. Per altre informazioni, vedere [Configurare modelli di posta elettronica][Configure email templates].

Dopo aver accettato hello invito, account hello diventa attivo.

## <a name="block-developer"></a> Disattivare o riattivare un account sviluppatore
Per impostazione predefinita, un nuovo account sviluppatore creato o invitato è **Attivo**. Fare clic su un account sviluppatore, toodeactivate **blocco**. Fare clic su un account sviluppatore bloccati, tooreactivate **attiva**. Un account sviluppatore bloccati non possa accedere al portale per sviluppatori hello o chiamare le API. Fare clic su un account utente, toodelete **eliminare**.

![Block developer][api-management-new-developer]

## <a name="reset-a-user-password"></a>Reimpostare la password di un utente
password di hello tooreset per un account utente, fare clic su nome hello dell'account di hello.

![Reimpostazione delle password][api-management-view-developer]

Fare clic su **reimpostazione password** toosend tooreset di utente toohello un collegamento la propria password.

![Reimpostazione delle password][api-management-reset-password]

tooprogrammatically gestire account utente, vedere hello [entità utente](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentazione in hello [API REST di gestione](https://msdn.microsoft.com/library/azure/dn776326.aspx) riferimento. un valore specifico utente account password tooa tooreset, è possibile utilizzare hello [aggiornare un utente](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operazione e specificare la password desiderata hello.

## <a name="pending-verification"></a>Verifica in sospeso
![Verifica in sospeso][api-management-pending-verification]

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato un account sviluppatore, è possibile associarlo a ruoli ed effettuare la sottoscrizione tooproducts e API. Per ulteriori informazioni, vedere [come toocreate e utilizzare gruppi][How toocreate and use groups].

[api-management-management-console]: ./media/api-management-howto-create-or-invite-developers/api-management-management-console.png
[api-management-add-new-user]: ./media/api-management-howto-create-or-invite-developers/api-management-add-new-user.png
[api-management-create-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-create-developer.png
[api-management-invite-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer.png
[api-management-new-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-new-developer.png
[api-management-invite-developer-window]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-window.png
[api-management-invite-developer-confirmation]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-confirmation.png
[api-management-pending-verification]: ./media/api-management-howto-create-or-invite-developers/api-management-pending-verification.png
[api-management-view-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-view-developer.png
[api-management-reset-password]: ./media/api-management-howto-create-or-invite-developers/api-management-reset-password.png


[Create a new developer]: #create-developer
[Invite a developer]: #invite-developer
[Deactivate or reactivate a developer account]: #block-developer
[Next steps]: #next-steps
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
