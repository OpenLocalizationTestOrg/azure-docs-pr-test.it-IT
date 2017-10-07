---
title: controllo delle versioni SDK aaaClient e server in App per dispositivi mobili e i servizi mobili | Documenti Microsoft
description: "Elenco degli SDK del client e compatibilità con versioni SDK del server per Servizi mobili e App per dispositivi mobili di Azure"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5874b7455ea407ca8c77fb1bd03d97d0767ebb47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a>Controllo delle versioni client e server in App per dispositivi mobili e Servizi mobili
versione più recente di Hello di servizi mobili di Azure è hello **App per dispositivi mobili** funzionalità di servizio App di Azure.

Hello client App per dispositivi mobili e server SDK originariamente sono basate su quelle di servizi mobili, ma sono *non* compatibili tra loro.
È infatti necessario usare un SDK del client di *App per dispositivi mobili* con un SDK del server di *App per dispositivi mobili* e lo stesso vale per *Servizi mobili*. Il presente contratto verrà applicato tramite un valore di intestazione speciale utilizzato dalle hello client e server SDK, `ZUMO-API-VERSION`.

Nota: ogni volta che questo documento si riferisce tooa *servizi mobili* back-end, non devono necessariamente toobe ospitati in servizi mobili. È ora possibile toomigrate toorun un servizio mobile nel servizio App senza alcuna modifica al codice, ma è comunque possibile utilizzare servizio hello *servizi mobili* versioni del SDK.

toolearn altre informazioni sulla migrazione tooApp servizio senza alcuna modifica al codice, vedere l'articolo hello [tooAzure un servizio Mobile servizio App di eseguire la migrazione].

## <a name="header-specification"></a>Specifica di intestazione
chiave Hello `ZUMO-API-VERSION` può essere specificato nell'intestazione HTTP hello o stringa di query hello. il valore di Hello è una stringa di versione in formato hello **x.y.z**.

ad esempio:

GET https://service.azurewebsites.net/tables/TodoItem

HEADERS: ZUMO-API-VERSION: 2.0.0

POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0

## <a name="opting-out-of-version-checking"></a>Esclusione del controllo della versione
È possibile rifiutare esplicitamente la verifica della impostando un valore di versione **true** per l'impostazione di app hello **MS_SkipVersionCheck**. Specificare questo file Web. config o nella sezione impostazioni dell'applicazione del portale di Azure hello hello.

> [!NOTE]
> Esistono una serie di modifiche di comportamento tra servizi mobili e App per dispositivi mobili, in particolare nelle aree di hello di sincronizzazione non in linea, autenticazione e le notifiche push. È solo necessario rifiutare esplicitamente versione controllo dopo tooensure test completo che queste modifiche del comportamento non interrompe l'esecuzione funzionalità dell'app.
>
>

## <a name="summary-of-compatibility-for-all-versions"></a>Riepilogo della compatibilità per tutte le versioni
Hello grafico mostra la compatibilità di hello tra tutti i tipi di client e server. Un back-end viene classificato come entrambi Mobile **servizi** o Mobile **app** basata su server hello SDK che utilizza.

|  | **Servizi mobili** | **App per dispositivi mobili** |
| --- | --- | --- |
| [Client di Servizi mobili] |OK |Errore\* |
| [Client di App per dispositivi mobili] |Errore\* |OK |

\*Può essere controllato specificando **MS_SkipVersionCheck**.

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <a name="1.0.0"></a>Client e server di Servizi mobili
SDK per applicazioni client Hello in tabella hello riportata di seguito sono compatibili con **servizi mobili**.

Nota: hello SDK client Servizi mobili *non* per inviare un valore di intestazione `ZUMO-API-VERSION`. Se il servizio di hello riceve questa intestazione o un valore di stringa di query, verrà restituito un errore, a meno che non si è scelto in modo esplicito come descritto in precedenza.

### <a name="MobileServicesClients"></a> SDK del client di *Servizi* mobili
| Piattaforma client | Versione | Valore dell'intestazione della versione |
| --- | --- | --- |
| Client gestito (Windows, Xamarin) |[1.3.2](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |n/d |
| iOS |[2.2.2](http://aka.ms/gc6fex) |n/d |
| Android |[2.0.3](https://go.microsoft.com/fwLink/?LinkID=280126) |n/d |
| HTML |[1.2.7](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |n/d |

### <a name="mobile-services-server-sdks"></a>SDK del server di *Servizi* mobili
| Piattaforma server | Versione | Intestazione della versione accettata |
| --- | --- | --- |
| .NET |[WindowsAzure.MobileServices.Backend.* Versione 1.0.x](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |* * Nessuna intestazione di versione * * |
| Node.js |(Presto disponibile) |**Nessuna intestazione di versione** |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a>Comportamento dei back-end di Servizi mobili
| ZUMO-API-VERSION | Valore di MS_SkipVersionCheck | Response |
| --- | --- | --- |
| Non specificato |Qualsiasi |200 - OK |
| Qualsiasi valore |True |200 - OK |
| Qualsiasi valore |False/Non specificato |400 - Richiesta non valida |

## <a name="2.0.0"></a>Client e server di App per dispositivi mobili di Azure
### <a name="MobileAppsClients"></a> SDK del client di *App* per dispositivi mobili
Il controllo della versione è stato introdotto a partire da hello seguenti versioni del client hello SDK per **App mobili di Azure**:

| Piattaforma client | Versione | Valore dell'intestazione della versione |
| --- | --- | --- |
| Client gestito (Windows, Xamarin) |[2.0.0](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |2.0.0 |
| iOS |[3.0.0](http://go.microsoft.com/fwlink/?LinkID=529823) |2.0.0 |
| Android |[3.0.0](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |3.0.0 |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a>SDK del server di *App* per dispositivi mobili
Il controllo della versione è incluso nelle seguenti versioni dell’SDK del server:

| Piattaforma server | SDK | Intestazione della versione accettata |
| --- | --- | --- |
| .NET |[Microsoft.Azure.Mobile.Server](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |2.0.0 |
| Node.js |[azure-mobile-apps)](https://www.npmjs.com/package/azure-mobile-apps) |2.0.0 |

### <a name="behavior-of-mobile-apps-backends"></a>Comportamento dei back-end di app per dispositivi mobili
| ZUMO-API-VERSION | Valore di MS_SkipVersionCheck | Response |
| --- | --- | --- |
| x.y.z o Null |True |200 - OK |
| Null |False/Non specificato |400 - Richiesta non valida |
| 1.x.y |False/Non specificato |400 - Richiesta non valida |
| 2.0.0-2.x.y |False/Non specificato |200 - OK |
| 3.0.0-3.x.y |False/Non specificato |400 - Richiesta non valida |

## <a name="next-steps"></a>Passaggi successivi
* [tooAzure un servizio Mobile servizio App di eseguire la migrazione]

[Client di Servizi mobili]: #MobileServicesClients
[Client di App per dispositivi mobili]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[tooAzure un servizio Mobile servizio App di eseguire la migrazione]: app-service-mobile-migrating-from-mobile-services.md
