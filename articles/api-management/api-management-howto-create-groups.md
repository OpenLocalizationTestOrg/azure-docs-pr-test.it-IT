---
title: gli account sviluppatore aaaManage usano i gruppi in Gestione API di Azure | Documenti Microsoft
description: Informazioni su come sviluppatore toomanage degli account con gruppi di gestione API di Azure
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 33660b45-442f-44be-9a4a-1899d7f699b0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c46e010e41d9705ae161dcd60d734a76d19c9e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-groups-toomanage-developer-accounts-in-azure-api-management"></a>Come per sviluppatori toomanage gruppi toocreate e utilizzare gli account in Gestione API di Azure
In Gestione API, i gruppi sono utilizzati toomanage hello visibilità dei prodotti toodevelopers. I prodotti sono primo toogroups visibile effettuata e gli sviluppatori di tali gruppi possono quindi visualizzare e sottoscrivere toohello prodotti che sono associati a gruppi di hello. 

Gestione API ha hello seguenti gruppi di sistema non modificabile.

* **Amministratori** : gli amministratori delle sottoscrizioni di Azure sono membri di questo gruppo. Gli amministratori di gestire le istanze del servizio Gestione API, la creazione di hello API, operazioni e i prodotti che vengono utilizzati dagli sviluppatori.
* **Sviluppatori** : gli utenti autenticati del portale per sviluppatori rientrano in questo gruppo. Gli sviluppatori hanno clienti hello che compilano applicazioni che utilizzano l'API. Gli sviluppatori sono concesse portale per sviluppatori di accesso toohello e compilare applicazioni che chiamano le operazioni di hello di un'API.
* **Gli utenti guest** -non autenticati gli utenti del portale per sviluppatori, ad esempio clienti potenziali, visitare il portale per sviluppatori hello di un passaggio di istanza di gestione API in questo gruppo. È possibile concedere alcuni accesso di sola lettura, ad esempio hello possibilità tooview API, ma li chiama.

Nei gruppi di sistema aggiunta toothese, gli amministratori possono creare gruppi personalizzati o [sfruttare gruppi esterni nel tenant di Azure Active Directory associato][leverage external groups in associated Azure Active Directory tenants]. Personalizzati e i gruppi esterni possono essere utilizzati insieme ai gruppi di sistema in fornendo agli sviluppatori di visibilità e accedere tooAPI prodotti. Ad esempio, è possibile creare un gruppo personalizzato per gli sviluppatori associati a uno specifico partner dell'organizzazione e consentono loro l'accesso toohello API da un prodotto che contiene solo le API pertinente. Un utente può essere un membro di più gruppi.

Questa guida illustra come gli amministratori di un'istanza di Gestione API possono aggiungere nuovi gruppi e associarli a prodotti e sviluppatori.

> [!NOTE]
> Inoltre toocreating e gestione di gruppi nel portale di pubblicazione hello, è possibile creare e gestire i gruppi tramite l'API REST gestione API hello [gruppo](https://msdn.microsoft.com/library/azure/dn776329.aspx) entità.
> 
> 

## <a name="create-group"></a>Creare un gruppo
Fare clic su un nuovo gruppo, toocreate **portale di pubblicazione** in hello portale di Azure per il servizio Gestione API. Consente di procedere toohello portale di pubblicazione di gestione API.

![Portale di pubblicazione][api-management-management-console]

> Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.
> 
> 

Fare clic su **gruppi** da hello **gestione API** menu hello a sinistra e quindi fare clic su **Aggiungi gruppo**.

![Aggiungere un nuovo gruppo][api-management-add-group]

Immettere un nome univoco per il gruppo di hello e una descrizione facoltativa e fare clic su **salvare**.

![Aggiungere un nuovo gruppo][api-management-add-group-window]

viene visualizzato il nuovo gruppo di Hello in hello tooedit scheda gruppi di hello **nome** o **descrizione** del gruppo di hello, fare clic sul nome di hello del gruppo di hello nell'elenco di hello. gruppo di hello toodelete, fare clic su **eliminare**.

![Gruppo aggiunto][api-management-new-group]

Dopo aver creato hello gruppo, può essere associata a prodotti e gli sviluppatori.

## <a name="associate-group-product"></a>Associare un gruppo a un prodotto
Fare clic su un gruppo con un prodotto, tooassociate **prodotti** da hello **gestione API** menu hello a sinistra e quindi fare clic su nome hello del prodotto desiderate hello.

![Visibilità dei prodotti][api-management-add-group-to-product]

Seleziona hello **visibilità** scheda tooadd e rimuovere gruppi e tooview hello corrente per il prodotto hello. tooadd o rimuovere i gruppi, selezionare o deselezionare le caselle di controllo di hello per hello desiderato di gruppi e fare clic su **salvare**.

![Visibilità dei prodotti][api-management-add-group-to-product-visibility]

> [!NOTE]
> gruppi di Azure Active Directory tooadd, vedere [modalità sviluppatore tooauthorize degli account con Azure Active Directory in Gestione API di Azure](api-management-howto-aad.md).
> 
> gruppi tooconfigure da hello **visibilità** per un prodotto, fare clic **Gestisci gruppi**.
> 
> 

Una volta associato a un gruppo di un prodotto, gli sviluppatori in tale gruppo possono visualizzare e sottoscrivere toohello prodotto.

## <a name="associate-group-developer"> </a>Associare gruppi a sviluppatori
gruppi tooassociate con gli sviluppatori, fare clic su **utenti** da hello **gestione API** menu hello a sinistra, quindi casella hello di controllo accanto agli sviluppatori di hello desiderato tooassociate con un gruppo.

![Aggiungere toogroup developer][api-management-add-group-to-developer]

Una volta hello lo si desidera che gli sviluppatori vengono controllati, fare clic su gruppo hello nella hello **aggiungere tooGroup** elenco a discesa. Gli sviluppatori possono essere rimossi dai gruppi tramite hello **rimuovere dal gruppo** elenco a discesa. 

![Sviluppatori][api-management-add-group-to-developer-saved]

Una volta tra developer hello e gruppo di hello viene aggiunta l'associazione di hello, è possibile visualizzarlo in hello **utenti** scheda.

## <a name="next-steps"></a>Passaggi successivi
* Dopo aver aggiunto il gruppo tooa uno sviluppatore, possono visualizzare e sottoscrivere toohello prodotti associati al gruppo. Per altre informazioni, vedere [Come creare e pubblicare un prodotto in Gestione API di Azure][How create and publish a product in Azure API Management],
* Inoltre toocreating e gestione di gruppi nel portale di pubblicazione hello, è possibile creare e gestire i gruppi tramite l'API REST gestione API hello [gruppo](https://msdn.microsoft.com/library/azure/dn776329.aspx) entità.

[api-management-management-console]: ./media/api-management-howto-create-groups/api-management-management-console.png
[api-management-add-group]: ./media/api-management-howto-create-groups/api-management-add-group.png
[api-management-add-group-window]: ./media/api-management-howto-create-groups/api-management-add-group-window.png
[api-management-new-group]: ./media/api-management-howto-create-groups/api-management-new-group.png
[api-management-add-group-to-product]: ./media/api-management-howto-create-groups/api-management-add-group-to-product.png
[api-management-add-group-to-product-visibility]: ./media/api-management-howto-create-groups/api-management-add-group-to-product-visibility.png
[api-management-add-group-to-developer]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer.png
[api-management-add-group-to-developer-saved]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer-saved.png

[api-management-]: ./media/api-management-howto-create-groups/api-management-.png

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group
