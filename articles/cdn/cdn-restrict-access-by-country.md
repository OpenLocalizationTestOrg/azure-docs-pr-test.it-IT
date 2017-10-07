---
title: contenuto della rete CDN di Azure in base al paese aaaRestrict | Documenti Microsoft
description: "Informazioni su come toorestrict accesso tooyour rete CDN di Azure contenuto mediante hello funzionalità filtro geografica."
services: cdn
documentationcenter: 
author: lichard
manager: akucer
editor: 
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: ffdd994612b6c9cfbf1a6e29d260709b4afa86e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a>Limitare il contenuto della rete CDN di Azure in base al paese

## <a name="overview"></a>Panoramica
Quando un utente richiede il contenuto, per impostazione predefinita, il contenuto di hello viene servito indipendentemente dalla effettuati di questa richiesta dall'utente hello. In alcuni casi, si consiglia di tooyour toorestrict accedere al contenuto in base al paese. Questo argomento viene illustrato come hello toouse **filtro geografica** funzionalità in ordine tooconfigure hello servizio tooallow o blocchi l'accesso in base al paese.

> [!IMPORTANT]
> Hello Verizon e Akamai offrono hello stessa funzionalità di filtro geografica ma presentare piccole differenze nei codici paese te supportano. Per le differenze toohello un collegamento, vedere il passaggio 3.


Per informazioni sulle considerazioni relative tooconfiguring questo tipo di restrizione, vedere hello [considerazioni](cdn-restrict-access-by-country.md#considerations) sezione alla fine di hello di hello argomento.  

![filtro di paese](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-hello-directory-path"></a>Passaggio 1: Definire il percorso di directory hello
Selezionare l'endpoint nel portale di hello e hello filtro geografica scheda toofind di navigazione a sinistra di hello questa funzionalità è disponibile.

Quando si configura un filtro di paese, è necessario specificare utenti toowhich toohello hello percorso relativo verranno consentiti o negati l'accesso. È possibile applicare il filtro geografico a tutti i file con "/" o alle cartelle selezionate specificando i percorsi di directory "/pictures/". È inoltre possibile applicare a file singolo filtro geografica tooa specificando file hello ed escludendo hello barra finale "/ Pictures/City.png".

Esempio di filtro di percorso di directory:

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-hello-action-block-or-allow"></a>Passaggio 2: Definire l'azione di hello: bloccare o consentire
**Blocco:** agli utenti di hello specificato paesi verranno negati l'accesso tooassets richiesto da tale percorso ricorsiva. Se non sono state definite altre opzioni di filtro di paese per tale percorso, tutti gli altri utenti saranno autorizzati ad accedere.

**Consenti:** solo gli utenti di hello specificato paesi potrà essere richiesto da tale percorso ricorsiva tooassets di accesso.

## <a name="step-3-define-hello-countries"></a>Passaggio 3: Definire paesi hello
Selezionare hello paesi che desidera tooblock o consentire per il percorso di hello. 

Ad esempio, la regola hello di blocco /Photos Strasburgo/filtrerà i file inclusi:

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a>Codici paese
Hello **filtro geografica** funzionalità utilizza paese codici toodefine hello i paesi da cui consentire o bloccare una richiesta per una directory protetta. Si noterà hello codici paese in [codici paese della rete CDN di Azure](https://msdn.microsoft.com/library/mt761717.aspx). 

## <a id="considerations"></a>Considerazioni
* Potrebbe richiedere fino a too90 minuti per Verizon, o un paio di minuti con Akamai, per le modifiche tooyour paese configurazione tootake effetto filtro.
* Questa funzionalità non supporta i caratteri jolly (ad esempio, ‘*’).
* configurazione di filtro geografica Hello associato hello relativo percorso sarà percorso toothat applicate in modo ricorsivo.
* Solo una regola può essere applicato toohello stesso percorso relativo (non è possibile creare più filtri paese toohello tale punto stesso percorso relativo. Tuttavia, una cartella potrebbe avere più filtri di paese. Questo è dovuto toohello ricorsiva natura dei filtri di paese. In altre parole, una sottocartella di una cartella configurata in precedenza può essere assegnata a un filtro di paese diverso.

