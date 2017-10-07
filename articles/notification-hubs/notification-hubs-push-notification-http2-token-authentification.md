---
title: Autenticazione basata su aaaToken di (HTTP/2) per il servizio APN nell'hub di notifica di Azure | Documenti Microsoft
description: Questo argomento viene illustrato come tooleverage hello nuova autenticazione del token per il servizio APN
services: notification-hubs
documentationcenter: .net
author: kpiteira
manager: erikre
editor: 
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 05/17/2017
ms.author: kapiteir
ms.openlocfilehash: 3353d7f16033ce0b68edec9ee9aeb98f47faa1fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="token-based-http2-authentication-for-apns"></a>Autenticazione basata su token (HTTP/2) per il servizio APN
## <a name="overview"></a>Panoramica
In questo articolo illustra in dettaglio come l'autenticazione basata su protocollo nuovo APN HTTP/2 toouse hello con token.

vantaggi principali di Hello dell'utilizzo di nuovo protocollo di hello includono:
-   Generazione dei token è relativamente semplice disponibile (confrontati toocertificates)
-   Non sono previste scadenze: l'utente ha il controllo completo dei token di autenticazione e della rispettiva revoca.
-   È ora possibile payload too4 KB
- Commenti e suggerimenti sincroni
-   Si è sul protocollo più recente di Apple – i certificati utilizzano ancora protocollo binario hello, che è contrassegnato per l'eliminazione

Per usare questo nuovo meccanismo sono sufficienti due passaggi che richiedono pochi minuti:
1.  Ottenere le informazioni necessarie hello dal portale di Account per sviluppatori Apple hello
2.  Configurare l'hub di notifica con le nuove informazioni hello

Gli hub di notifica è ora tutti i set toouse hello nuovo sistema di autenticazione con il servizio APN. 

Se è stata eseguita la migrazione dall'uso delle credenziali del certificato per il servizio APN, si noti quanto segue:
- proprietà token Hello sovrascrivere il certificato nel sistema,
- ma l'applicazione continua tooreceive notifiche senza problemi.

## <a name="obtaining-authentication-information-from-apple"></a>Recupero delle informazioni di autenticazione da Apple
l'autenticazione basata su token tooenable, è necessario hello le proprietà seguenti dal tuo Account sviluppatore Apple:
### <a name="key-identifier"></a>Identificatore di chiave
Identificatore di chiave Hello può essere ottenuti dalla pagina "Chiavi" hello nell'Account per sviluppatori di Apple

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a>Identificatore dell'applicazione e nome dell'applicazione
nome dell'applicazione Hello è disponibile nella pagina di ID App hello in hello Account sviluppatore. 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

Identificatore dell'applicazione Hello è disponibile nella pagina dettagli di appartenenza hello in hello Account sviluppatore.
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a>Token di autenticazione
è possibile scaricare il token di autenticazione Hello dopo la generazione di un token per l'applicazione. Per informazioni dettagliate su come toogenerate questo token, vedere troppo[documentazione per sviluppatori di Apple](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).

## <a name="configuring-your-notification-hub-toouse-token-based-authentication"></a>Configurazione dell'autenticazione basata su token toouse la notifica hub
### <a name="configure-via-hello-azure-portal"></a>Configurare tramite hello portale di Azure
token tooenable in base l'autenticazione nel portale di hello, accedi toohello portale di Azure e passare tooyour Hub di notifica > Notification Services > Pannello APN. 

È disponibile una nuova proprietà, ovvero *Modalità di autenticazione*. Se si seleziona Token sarà tooupdate l'hub con tutte hello token le proprietà rilevanti.

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- Immettere proprietà hello recuperato dal tuo account sviluppatore di Apple, 
- Scegliere la modalità dell'applicazione (produzione o sandbox). 
- Fare clic su Salva tooupdate le credenziali APNS. 

### <a name="configure-via-management-api-rest"></a>Configurazione tramite API Gestione (REST)

È possibile utilizzare il nostro [le API di gestione](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate l'autenticazione basata su token di notifica hub toouse.
A seconda se si sta configurando un'applicazione hello è un'applicazione di produzione o Sandbox (specificata nell'Account per sviluppatori di Apple), utilizzare uno degli endpoint corrispondente hello:

- Endpoint sandbox: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)
- Endpoint di produzione: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)

> [!IMPORTANT]
> L'autenticazione basata su token richiede una versione **2017-04 o successiva** dell'API.
> 
> 

Di seguito è riportato un esempio di un tooupdate richiesta PUT un hub con l'autenticazione basata su token:


        PUT https://{namespace}.servicebus.windows.net/{Notification Hub}?api-version=2017-04
          "Properties": {
            "ApnsCredential": {
              "Properties": {
                "KeyId": "<Your Key Id>",
                "Token": "<Your Authentication Token>",
                "AppName": "<Your Application Name>",
                "AppId": "<Your Application Id>",
                "Endpoint":"<Sandbox/Production Endpoint>"
              }
            }
          }
        

### <a name="configure-via-hello-net-sdk"></a>Configurare tramite hello .NET SDK
È possibile configurare l'autenticazione basata su token toouse hub utilizzando il nostro [client più recente SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8). 

Di seguito è riportato un esempio di codice che descrive l'utilizzo corretto di hello:


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH tooYOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-toousing-certificate-based-authentication"></a>Autenticazione basata su certificato toousing ripristino
È possibile ripristinare in qualsiasi autenticazione basata sui certificati di tempo toousing utilizzando qualsiasi certificato di hello (metodo) e il passaggio precedente anziché le proprietà token hello. Le credenziali che l'azione sovrascrive hello precedentemente archiviate.
