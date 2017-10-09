---
title: contenuto della pagina aaaModify nel portale per sviluppatori hello in Gestione API di Azure | Documenti Microsoft
description: Informazioni su come contenuto della pagina tooedit nel portale per sviluppatori hello in Gestione API di Azure.
services: api-management
documentationcenter: 
author: antonba
manager: vlvinogr
editor: 
ms.assetid: 186128fe-41c0-4efb-9efe-2478ad4d103f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/09/2017
ms.author: antonba
ms.openlocfilehash: fd5a854e900d9512518643e593b1b59a0952621f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-content-and-layout-of-pages-on-hello-developer-portal-in-azure-api-management"></a>Modificare il contenuto di hello e layout delle pagine del portale per sviluppatori hello in Gestione API di Azure
In Gestione API di Azure sono disponibili tre modi principali toocustomize hello portale:

* [Modificare il contenuto di hello di pagine statiche e gli elementi di layout di pagina] [ modify-content-layout] (descritto in questa Guida)
* [Aggiornare gli stili di hello in portale per sviluppatori hello vengono utilizzati per gli elementi di pagina][customize-styles]
* [Modificare modelli di hello utilizzati per le pagine generate dal portale hello] [ portal-templates] (ad esempio documenti di API, prodotti, l'autenticazione utente e così via)

## <a name="page-structure"></a>Struttura delle pagine del portale per sviluppatori

portale per sviluppatori Hello è basato su un sistema di gestione dei contenuti. layout di Hello di ogni pagina si basa sul set di elementi di piccole dimensioni pagina widget:

![Struttura della pagina del portale per sviluppatori][api-management-customization-widget-structure]

Tutti i widget sono modificabili. 
* pagina singoli Hello core contenuto tooeach specifico si trovano nel widget "Contenuto" hello. Modifica di una pagina, significa che la modifica hello contenuto di questo widget.
* Tutti gli elementi di layout di pagina sono contenuti con i widget di hello rimanenti. Le modifiche apportate widget toothese applicherà tooall pagine. Saranno tooas cui "widget layout".

Nella pagina quotidiane solo una modifica in genere modifica i widget contenuto hello che conterrà un contenuto diverso per ogni pagina.

## <a name="modify-layout-widget"></a>Modifica hello contenuto di un widget di layout

Viene modificato il contenuto all'interno di portale per sviluppatori hello tramite portale di pubblicazione hello accessibile dal portale di Azure hello. tooreach, fare clic su **portale di pubblicazione** dalla barra degli strumenti del servizio hello dell'istanza di gestione API.

![Portale di pubblicazione][api-management-management-console]

Fare clic su contenuto hello tooedit di tale widget, **widget** da hello **portale per sviluppatori** menu di sinistra hello. Per questo esempio consente di modificare il contenuto di hello del widget intestazione hello. Seleziona hello **intestazione** widget dall'elenco di hello.

![Widget Intestazione][api-management-widgets-header]

contenuto di Hello dell'intestazione hello può essere modificata da in hello **corpo** campo. Modificare il testo hello come desiderato e quindi fare clic su **salvare** nella parte inferiore di hello della pagina hello.

Ora è necessario che la nuova intestazione hello in grado di toosee in ogni pagina portale per sviluppatori hello.

> portale per sviluppatori di hello tooopen mentre nel portale di pubblicazione hello, fare clic su **portale per sviluppatori** nella barra superiore hello.
> 
> 

## <a name="edit-page-contents"></a>Modificare hello contenuto di una pagina

elenco di hello toosee di tutte le pagine di contenuto esistente, fare clic su **contenuto** da hello **portale per sviluppatori** menu nel portale di pubblicazione hello.

![Gestione del contenuto][api-management-customization-manage-content]

Fare clic su hello **iniziale** pagina tooedit contenuto hello home page del portale per sviluppatori hello. Apportare modifiche hello desidera visualizzare in anteprima, se necessario e quindi fare clic su **pubblica** toomake li tooeveryone visibile.

> home page di Hello utilizza un layout speciale che ne consenta toodisplay un'intestazione nella parte superiore di hello. Questa intestazione non è modificabile dall'hello **contenuto** sezione. tooedit questo avvio, fare clic su **widget** da hello **portale per sviluppatori** dal menu **Home page** da hello **livello corrente** elenco a discesa elenco e quindi aprire hello **Banner** voce hello **in primo piano sezione**. il contenuto di Hello di questo widget è modificabile come qualsiasi altra pagina.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* [Aggiornare gli stili di hello in portale per sviluppatori hello vengono utilizzati per gli elementi di pagina][customize-styles]
* [Modificare modelli di hello utilizzati per le pagine generate dal portale hello] [ portal-templates] (ad esempio documenti di API, prodotti, l'autenticazione utente e così via)

[Structure of developer portal pages]: #page-structure
[Modifying hello contents of a layout widget]: #modify-layout-widget
[Edit hello contents of a page]: #edit-page-contents
[Next steps]: #next-steps

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customization-widget-structure]: ./media/api-management-modify-content-layout/portal-widget-structure.png
[api-management-management-console]: ./media/api-management-modify-content-layout/api-management-management-console.png
[api-management-widgets-header]: ./media/api-management-modify-content-layout/api-management-widgets-header.png
[api-management-customization-manage-content]: ./media/api-management-modify-content-layout/api-management-customization-manage-content.png
