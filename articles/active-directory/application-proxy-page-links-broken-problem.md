---
title: aaaLinks nella pagina di hello non funzionano per un'applicazione Proxy dell'applicazione | Documenti Microsoft
description: "Come tootroubleshoot genera collegamenti interrotti in applicazioni di Proxy dell'applicazione che è stata integrata con Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 77c1e22d27c7a6436d8e57e105037c2328180481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="links-on-hello-page-dont-work-for-an-application-proxy-application"></a>I collegamenti nella pagina di hello non funzionano per un'applicazione Proxy dell'applicazione

Questo articolo è utile tootroubleshoot perché l'applicazione Proxy dell'applicazione Azure Active Directory i collegamenti non funzionano correttamente.

## <a name="overview"></a>Panoramica 
Dopo la pubblicazione di un'app di Proxy dell'applicazione, hello solo i collegamenti che lavoro per impostazione predefinita in un'applicazione hello siano toodestinations collegamenti contenuti all'interno di hello pubblicati URL radice. non sono in uso Hello collegamenti all'interno delle applicazioni di hello, hello URL interno per un'applicazione hello non includono tutte le destinazioni di hello dei collegamenti all'interno di un'applicazione hello.

**Perché si verifica questo problema?** Quando un collegamento in un'applicazione, URL del Proxy di applicazione tentativi tooresolve hello come l'URL interno all'interno di hello stessa applicazione o come un URL disponibile esternamente. Hello stesso collegamento hello punta tooan l'URL interno che non è all'interno dell'applicazione, non appartengono tooeither questi bucket e provocare un errore non è stato trovato.

## <a name="ways-you-can-resolve-broken-links"></a>Come correggere i collegamenti interrotti

Esistono tre modi tooresolve questo problema. scelte Hello sottostanti sono elencati nella complessità crescente.

1.  Verificare che l'URL interno hello è una radice che contiene tutti i collegamenti rilevanti hello per un'applicazione hello. In questo modo tutti i collegamenti toobe, risolto come contenuto pubblicato all'interno di hello stessa applicazione.

    Se si modifica l'URL interno hello senza hello toochange pagina per gli utenti di destinazione, modifica hello URL della Home page toohello pubblicato in precedenza URL interno. Questa operazione può essere eseguita passando troppo "Azure Active Directory -"&gt; registrazioni di App -&gt; selezionare un'applicazione hello -&gt; proprietà. In questa scheda proprietà, viene visualizzato il campo di hello "URL della Home Page" che è possibile modificare toobe hello desiderato pagina di destinazione.

2.  Se le applicazioni utilizzano nomi di dominio completo (FQDN), utilizzare [domini personalizzati](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) toopublish delle applicazioni. Questa funzionalità consente hello stesso URL toobe utilizzato sia internamente ed esternamente.

    Questa opzione garantisce che hello collegamenti nell'applicazione siano accessibili tramite il Proxy di applicazione poiché i collegamenti di hello nei toointernal URL dell'applicazione hello sono inoltre riconosciuti esternamente. Si noti che tutti i collegamenti è comunque necessario toobelong tooa pubblicata l'applicazione. Tuttavia, con hello questa opzione i collegamenti non è necessario toobelong toohello applicazione stessa e può appartenere toomultiple applicazioni.

3.  Se nessuna di queste opzioni sono applicabili, si join anteprima hello per una nuova funzionalità di riscrittura URL traduzione /. Con questa opzione, essere interno URL o i collegamenti esistenti nel corpo HTML hello le applicazioni convertite, o "mappata", toohello pubblicati URL esterni Proxy di applicazione. Questo metodo funziona solo per i collegamenti in hello HTML o CSS e questo è utile quando viene generato il collegamento tramite JS. 

Di conseguenza, è consigliabile utilizzare hello [domini personalizzati](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) soluzione se possibile. Se si desidera anteprima hello toojoin, inviare tramite posta elettronica < aadapfeedback@microsoft.com > con applicationId(s) hello.

## <a name="next-steps"></a>Passaggi successivi
[Usare server proxy locali esistenti](application-proxy-working-with-proxy-servers.md)

