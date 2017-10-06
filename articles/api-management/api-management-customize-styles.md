---
title: stili aaaCustomize nel portale per sviluppatori hello in Gestione API di Azure | Documenti Microsoft
description: Informazioni sull'utilizzo degli stili hello toomodify per qualsiasi pagina nel portale per sviluppatori hello in Gestione API di Azure.
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
ms.openlocfilehash: aaaa86527992ba43e64eab5fd35c7f57b573c812
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-styling-of-hello-developer-portal-in-azure-api-management"></a>Personalizzare lo stile di hello del portale per sviluppatori hello in Gestione API di Azure
In Gestione API di Azure sono disponibili tre modi principali toocustomize hello portale:

* [Modificare il contenuto di hello di pagine statiche e gli elementi di layout di pagina][modify-content-layout]
* [Aggiornare gli stili di hello utilizzati per gli elementi di pagina tra il portale per sviluppatori di hello] [ customize-styles] (descritto in questa Guida)
* [Modificare modelli di hello utilizzati per le pagine generate dal portale hello] [ portal-templates] (ad esempio documenti di API, prodotti, l'autenticazione utente e così via)

## <a name="change-headers-styling"></a>Modificare lo stile di hello degli elementi di pagina

Hello colori, tipi di carattere, dimensioni, spaziature avanzamento e altri elementi correlate allo stile di qualsiasi pagina del portale hello sono definiti da regole di stile. 

Modifica delle regole di stile hello avviene da hello **portale per sviluppatori** mentre viene effettuato l'accesso come amministratore. tooget esiste prima di tutto aprire hello portale di Azure e fare clic su **portale di pubblicazione** dalla barra degli strumenti del servizio hello dell'istanza di gestione API.

![Portale di pubblicazione][api-management-management-console]

Fare clic su **portale per sviluppatori** in alto a destra di hello. 

![Collegamento del portale per sviluppatori sul portale di pubblicazione hello][api-management-pp-dp-link]

barra degli strumenti personalizzazione di hello tooopen spostare il puntatore del mouse sull'icona della personalizzazione hello (o selezionarlo) e quindi fare clic su "stili" dalla barra degli strumenti hello.

![Pulsante della barra degli strumenti di personalizzazione][api-management-customization-toolbar-button]

Esistono due modi principali di modifica delle regole di stile: è possibile esaminare hello l'elenco di tutte le regole di stile hello utilizzate in qualsiasi punto in cui viene visualizzato per impostazione predefinita e modificare uno stile in base alle esigenze o è possibile scegliere **selezionare un elemento nella pagina hello** e quindi Fare clic su hello pagina toosee solo hello stili per quell'elemento.

![Barra degli strumenti Personalizzazione][api-management-customization-toolbar]

Fare clic su hello **selezionare un elemento nella pagina hello** opzione per questo esempio.  A questo punto, gli elementi diventano evidenziati al passaggio del mouse su di essi con hello mouse toosignify stili dell'elemento, quale iniziare la modifica se è stato selezionato. Spostamento hello passa il mouse sul testo hello nell'intestazione di hello (in genere è necessario il nome di società hello qui) e quindi fare clic su e. Un set di regole di stile denominata e categoria viene visualizzata nell'editor di applicazione di stili hello. Ogni regola rappresenta una proprietà di stile dell'elemento selezionato hello. Ad esempio, per il testo di intestazione hello selezionato in precedenza, la dimensione di hello del testo hello è @font-size-h1 mentre è il nome di hello del tipo di carattere hello con alternative in @headings-font-family.

> Se si ha familiarità con [bootstrap][bootstrap], queste regole sono in realtà [variabili LESS] [ LESS variables] in tema di bootstrap hello usato da hello portale per sviluppatori.
> 
> 

Modificare i colori hello del testo titolo hello. Selezionare la voce hello hello  **@headings-color**  campo e tipo **#000000**. Questo è hello codice esadecimale per il colore di hello nero. In questo caso, vedrai che alla fine di hello hello della casella di testo viene visualizzato un indicatore di quadrato di colore. Se si fa clic su questo indicatore, una selezione colori consente si toochoose un colore.

![Selezione colori][api-management-customization-toolbar-color-picker]

Vengono visualizzati in anteprima le modifiche in tempo reale renderli, ma sono visibili tooadministrators solo. toomake queste modifiche sono state tooeveryone visibile, fare clic su hello **pubblica** pulsante nell'editor di applicazione di stili hello e confermare le modifiche di hello.

![Menu Pubblica][api-management-customization-toolbar-publish-form]

> hello toochange le regole di stile che si applicano tooany altri elementi nella pagina di hello, seguire hello stessa stored procedure come in precedenza per intestazione hello. Fare clic su **selezionare un elemento nella pagina hello** da editor stile hello elemento selezionare hello si è interessati e inizio modifica dei valori hello hello delle regole di stile visualizzate sullo schermo hello.
> 
> 


## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come contenuto di hello toocustomize del portale per sviluppatori di pagine con [modelli portali per sviluppatori](api-management-developer-portal-templates.md).

[Change hello styling of hello headers]: #change-headers-styling
[Next steps]: #next-steps

[Azure Classic Portal]: https://manage.windowsazure.com/

[api-management-management-console]: ./media/api-management-customize-styles/api-management-management-console.png
[api-management-pp-dp-link]: ./media/api-management-customize-styles/api-management-pp-dp-link.png
[api-management-customization-toolbar-button]: ./media/api-management-customize-styles/api-management-customization-toolbar-button.png
[api-management-customization-toolbar]: ./media/api-management-customize-styles/api-management-customization-toolbar.png
[api-management-customization-toolbar-color-picker]: ./media/api-management-customize-styles/api-management-customization-toolbar-color-picker.png
[api-management-customization-toolbar-publish-form]: ./media/api-management-customize-styles/api-management-customization-toolbar-publish-form.png

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[bootstrap]: http://getbootstrap.com/
[LESS variables]: http://getbootstrap.com/css/
