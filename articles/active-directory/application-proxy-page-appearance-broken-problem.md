---
title: pagina aaaApplication non viene visualizzato correttamente per un'applicazione Proxy dell'applicazione | Documenti Microsoft
description: "Quando la pagina hello non vengono visualizzati correttamente in un'applicazione di Proxy di applicazione è stata integrata con Azure AD"
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
ms.openlocfilehash: f4abaa4e94c512868f2085affe59cac443784a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a>La pagina dell'applicazione non viene visualizzata correttamente per un'applicazione proxy di applicazione

Questo articolo è utile tootroubleshoot problemi con applicazioni di Proxy dell'applicazione Azure Active Directory quando si passa toohello pagina, ma un elemento nella pagina di hello non sembra corretto.

## <a name="overview"></a>Panoramica
Quando si pubblica un'app di Proxy dell'applicazione, solo le pagine nella cartella principale sono accessibili quando si accede a un'applicazione hello. Se non è la corretta visualizzazione pagina hello, hello radice URL interno utilizzato per un'applicazione hello potrebbero mancare alcune risorse di pagina. tooresolve, assicurarsi di aver pubblicato *tutti* hello risorse per la pagina hello come parte dell'applicazione.

È possibile verificare questo problema hello aprendo l'individuazione di rete (ad esempio Fiddler o F12 strumenti in Internet Explorer o Edge), il caricamento della pagina hello e cercare 404 errori. Che indica le pagine di hello che attualmente non è state trovate e potrebbe essere ancora necessario toobe pubblicato.

Si supponga ad esempio di questo caso, è stata pubblicata un'applicazione di spese utilizzando un URL interno di <http://myapps/expenses>, ma hello app utilizza hello stylesheet <http://myapps/style.css>. In questo caso, hello foglio di stile non è pubblicato nell'applicazione, pertanto il caricamento delle app spese hello generano un errore durante il tentativo tooload style.css 404. In questo esempio, hello problema potrebbe essere risolto tramite la pubblicazione di un URL interno di un'applicazione hello <http://myapp/> invece.

## <a name="problems-with-publishing-as-one-application"></a>Problemi relativi alla pubblicazione come singola applicazione

Se non è possibile toopublish tutte le risorse all'interno di hello stessa applicazione, è necessario toopublish più applicazioni e abilitare i collegamenti tra di essi.

toodo in tal caso, si consiglia di utilizzare hello [domini personalizzati](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) soluzione. Tuttavia, questa soluzione richiede che il certificato di hello si è proprietari del dominio e le applicazioni utilizzano nomi di dominio completo (FQDN). Per altre opzioni, vedere hello [risolvere collegamenti non funzionanti documentazione](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).

## <a name="next-steps"></a>Passaggi successivi
[Pubblicare applicazioni mediante il proxy di applicazione AD Azure](application-proxy-publish-azure-portal.md)
