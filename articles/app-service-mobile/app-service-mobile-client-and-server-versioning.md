---
title: Controllo delle versioni SDK di client e server in App per dispositivi mobili e Servizi mobili | Documentazione Microsoft
description: "Elenco degli SDK del client e compatibilità con versioni SDK del server per Servizi mobili e App per dispositivi mobili di Azure"
services: app-service\mobile
documentationcenter: 
author: conceptdev
manager: crdun
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: crdun
ms.openlocfilehash: 37bf36af535eb9b5c8b0ba38434b71f1a6686811
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/04/2018
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a>Controllo delle versioni client e server in App per dispositivi mobili e Servizi mobili
La versione più recente di Servizi mobili di Azure è la funzionalità **App per dispositivi mobili** del Servizio app di Azure.

Gli SDK del client e del server di App per dispositivi mobili in origine si basano su quelle in Servizi mobili, ma *non* sono compatibili tra loro.
È infatti necessario usare un SDK del client di *App per dispositivi mobili* con un SDK del server di *App per dispositivi mobili* e lo stesso vale per *Servizi mobili*. Questo contratto viene applicato tramite un valore di intestazione speciale utilizzato dagli SDK del client e del server, `ZUMO-API-VERSION`.

Nota: ogni volta che in questo documento si fa riferimento a un back-end di *Servizi mobili* , esso non deve necessariamente essere ospitato su Servizi mobili. È ora possibile eseguire la migrazione di un servizio mobile per l'esecuzione nel servizio app senza apportare modifiche al codice, ma il servizio continuerà a usare le versioni SDK di *Servizi mobili*.

Per ulteriori informazioni sulla migrazione al servizio app senza apportare modifiche al codice, vedere l'articolo [Eseguire la migrazione di un servizio mobile al servizio app di Azure].

## <a name="header-specification"></a>Specifica di intestazione
La chiave `ZUMO-API-VERSION` può essere specificata nell'intestazione HTTP o nella stringa di query. Il valore è una stringa di versione nel formato **x.y.z**.

Ad esempio: 

GET https://service.azurewebsites.net/tables/TodoItem

HEADERS: ZUMO-API-VERSION: 2.0.0

POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0

## <a name="opting-out-of-version-checking"></a>Esclusione del controllo della versione
È possibile rifiutare esplicitamente il controllo della versione impostando un valore **true** per l'impostazione dell'app **MS_SkipVersionCheck**. Specificarlo nel file web.config o nella sezione Impostazioni applicazione del portale di Azure.

> [!NOTE]
> Esistono una serie di modifiche di comportamento tra Servizi mobili e App per dispositivi mobili, in particolare per quanto riguarda la sincronizzazione offline, l’autenticazione e le notifiche push. È consigliabile rifiutare esplicitamente solo il controllo della versione dopo aver completato un test per assicurarsi che queste modifiche del comportamento non interferiscano con le funzionalità dell'applicazione.
>
>

## <a name="summary-of-compatibility-for-all-versions"></a>Riepilogo della compatibilità per tutte le versioni
Il grafico seguente illustra la compatibilità tra tutti i tipi di client e server. Un back-end viene classificato come **Servizi** mobili o **App** per dispositivi mobili in base all'SDK del server usato.

|  | **Servizi mobili** | **App per dispositivi mobili** |
| --- | --- | --- |
| [Client di Servizi mobili] |OK |Errore\* |
| [Client di App per dispositivi mobili] |Errore\* |OK |

\*Può essere controllato specificando **MS_SkipVersionCheck**.

<!-- IMPORTANT!  The anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: the fwlink to this document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <a name="1.0.0"></a>Client e server di Servizi mobili
Gli SDK del client nella tabella seguente sono compatibili con **Servizi mobili**.

Nota: gli SDK del client di Servizi mobili *non* inviano un valore di intestazione per `ZUMO-API-VERSION`. Se il servizio riceve questo valore di intestazione o di stringa di query, verrà restituito un errore, a meno che non lo si abbia rifiutato in modo esplicito come descritto sopra.

### <a name="MobileServicesClients"></a> SDK del client di *Servizi* mobili
| Piattaforma client | Version | Valore dell'intestazione della versione |
| --- | --- | --- |
| Client gestito (Windows, Xamarin) |[1.3.2](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |n/d |
| iOS |[2.2.2](http://aka.ms/gc6fex) |n/d |
| Android |[2.0.3](https://go.microsoft.com/fwLink/?LinkID=280126) |n/d |
| HTML |[1.2.7](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |n/d |

### <a name="mobile-services-server-sdks"></a>SDK del server di *Servizi* mobili
| Piattaforma server | Version | Intestazione della versione accettata |
| --- | --- | --- |
| .NET |[WindowsAzure.MobileServices.Backend.* Versione 1.0.x](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |**Nessuna intestazione di versione ** |
| Node.js |(Presto disponibile) |**Nessuna intestazione di versione** |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a>Comportamento dei back-end di Servizi mobili
| ZUMO-API-VERSION | Valore di MS_SkipVersionCheck | Risposta |
| --- | --- | --- |
| Non specificato |Qualsiasi |200 - OK |
| Qualsiasi valore |True  |200 - OK |
| Qualsiasi valore |False/Non specificato |400 - Richiesta non valida |

## <a name="2.0.0"></a>Client e server di App per dispositivi mobili di Azure
### <a name="MobileAppsClients"></a> SDK del client di *App* per dispositivi mobili
Il controllo della versione è stata introdotta a partire dalle seguenti versioni dell’SDK del client per **App per dispositivi mobili di Azure**:

| Piattaforma client | Version | Valore dell'intestazione della versione |
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
| ZUMO-API-VERSION | Valore di MS_SkipVersionCheck | Risposta |
| --- | --- | --- |
| x.y.z o Null |True  |200 - OK |
| Null |False/Non specificato |400 - Richiesta non valida |
| 1.x.y |False/Non specificato |400 - Richiesta non valida |
| 2.0.0-2.x.y |False/Non specificato |200 - OK |
| 3.0.0-3.x.y |False/Non specificato |400 - Richiesta non valida |

## <a name="next-steps"></a>Fasi successive
* [Eseguire la migrazione di un servizio mobile al servizio app di Azure]

[Client di Servizi mobili]: #MobileServicesClients
[Client di App per dispositivi mobili]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[Eseguire la migrazione di un servizio mobile al servizio app di Azure]: app-service-mobile-migrating-from-mobile-services.md
