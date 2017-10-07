---
title: "aaaIssuer nome e la chiave dell'autorità di certificazione nei servizi BizTalk | Documenti Microsoft"
description: "Informazioni su come nome dell'autorità di certificazione tooretrieve e la chiave dell'autorità di certificazione per il Bus di servizio o Access Control (ACS) nei servizi BizTalk. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a>Servizi BizTalk: nome e chiave dell'autorità emittente

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Servizi BizTalk di Azure Usa hello nome dell'autorità di certificazione del Bus di servizio e la chiave dell'autorità emittente e hello nome di accesso controllo dell'autorità emittente e chiave dell'autorità emittente. In particolare:

| Attività | Nome e chiave dell'autorità emittente da utilizzare |
| --- | --- |
| Distribuzione dell'applicazione da Visual Studio |Nome e chiave dell'autorità emittente del Controllo di accesso |
| Configurazione hello portale servizi BizTalk di Azure |Nome e chiave dell'autorità emittente del Controllo di accesso |
| Creazione di inoltro LOB con hello servizi dell'Adapter BizTalk in Visual Studio |Nome e chiave dell'autorità emittente del bus di servizio |

Questo argomento elenca hello passaggi tooretrieve hello nome dell'autorità emittente e chiave dell'autorità emittente. 

## <a name="access-control-issuer-name-and-issuer-key"></a>Nome e chiave dell'autorità emittente del Controllo di accesso
Hello nome di accesso controllo dell'autorità emittente e la chiave dell'autorità di certificazione vengono utilizzati dal seguente hello:

* L'applicazione di servizio BizTalk di Azure creata in Visual Studio: toosuccessfully distribuire l'applicazione BizTalk Service in tooAzure di Visual Studio, si immette hello nome di accesso controllo dell'autorità emittente e chiave dell'autorità emittente. 
* Hello portale servizi BizTalk di Azure: quando si crea un BizTalk Service e apre hello portale dei servizi BizTalk, il nome di autorità di certificazione di controllo di accesso e la chiave dell'autorità di certificazione vengono registrati automaticamente per le distribuzioni con hello stessi valori di controllo di accesso.

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a>Ottenere hello nome di accesso controllo dell'autorità emittente e la chiave dell'autorità di certificazione

toouse ACS per l'autenticazione e get hello i valori di nome dell'autorità emittente e la chiave dell'autorità di certificazione, includono hello passaggi generali:

1. Installare hello [cmdlet di Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
2. Aggiungere il proprio Account Azure: `Add-AzureAccount`
3. Restituire il nome della sottoscrizione: `get-azuresubscription`
4. Selezionare la propria sottoscrizione: `select-azuresubscription <name of your subscription>` 
5. Creare un nuovo spazio dei nomi: `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`

    Esempio:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`
      
5. Creazione di hello nuovo spazio dei nomi ACS (che può richiedere alcuni minuti), sono elencati i valori di nome dell'autorità emittente e chiave dell'autorità emittente hello nella stringa di connessione hello: 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

toosummarize:  
Nome dell'autorità emittente = SharedSecretIssuer  
Chiave dell'autorità emittente = SharedSecretKey

Altre informazioni sul hello [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet. 

## <a name="service-bus-issuer-name-and-issuer-key"></a>Nome e chiave dell'autorità emittente del bus di servizio
Il nome e la chiave dell'autorità emittente del bus di servizio vengono utilizzati dai servizi dell'adapter di BizTalk. Nel progetto servizi BizTalk in Visual Studio, utilizzare il sistema Line-of-Business (LOB) locale tooan di hello servizi dell'Adapter BizTalk tooconnect. tooconnect, si crea hello inoltro LOB e immettere i dettagli del sistema LOB. In tal caso, è anche possibile immettere hello nome dell'autorità di certificazione del Bus di servizio e la chiave dell'autorità di certificazione.

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a>hello tooretrieve nome dell'autorità di certificazione del Bus di servizio e la chiave dell'autorità di certificazione
1. Accedi toohello [portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Nel riquadro di spostamento a sinistra di hello, selezionare **Bus di servizio**.
3. Selezionare lo spazio dei nomi. Nella barra delle applicazioni hello, selezionare **informazioni di connessione**. Consente di visualizzare hello **autorità di certificazione predefinita** (nome dell'autorità emittente) e **chiave predefinita** (chiave dell'autorità di certificazione). Questi valori possono essere copiati.  

toosummarize:  
Nome dell'autorità di certificazione = Autorità di certificazione predefinita  
Chiave autorità di certificazione = Chiave predefinita

## <a name="next"></a>Avanti
Altri argomenti relativi a Servizi BizTalk di Azure:

* [L'installazione di hello Azure BizTalk Services SDK](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [Servizi BizTalk: Esercitazioni ed esempi](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [Come è possibile utilizzare hello Azure BizTalk Services SDK](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Servizi BizTalk di Azure](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>Vedere anche
* [Procedura: tooConfigure servizio di gestione ACS di usare le identità del servizio](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [Servizi BizTalk: Grafico edizioni Developer, Basic, Standard e Premium](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [Servizi BizTalk: effettuare il provisioning di un servizio BizTalk mediante il portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [Servizi BizTalk: Tabella degli stati del servizio](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [Servizi BizTalk: Schede Dashboard, Monitoraggio, Scalabilità](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [Servizi BizTalk: backup e ripristino](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [Servizi BizTalk: limitazione](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

