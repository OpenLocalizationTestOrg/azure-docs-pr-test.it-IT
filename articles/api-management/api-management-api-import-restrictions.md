---
title: importare aaaRestrictions e problemi noti in Azure API di gestione | Documenti Microsoft
description: Dettagli di problemi noti e le restrizioni sull'importazione in Gestione API di Azure mediante i formati di API aperta, WSDL o WADL hello.
services: api-management
documentationcenter: 
author: mattfarm
manager: vlvinogr
editor: 
ms.assetid: 7a5a63f0-3e72-49d3-a28c-1bb23ab495e2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: apipm
ms.openlocfilehash: 0bed5ace47de6ccbfbecba25ea6b69c5329de089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="api-import-restrictions-and-known-issues"></a>Problemi noti e limitazioni dell'importazione dell'API
## <a name="about-this-list"></a>Informazioni sull'elenco
Mentre ogni impegno tooensure che l'API di importazione in Gestione API di Azure non è più semplice e senza problemi possibili, è talvolta imporre restrizioni o identificare i problemi che saranno necessario toobe alla correzione dell'errore prima di poter importare correttamente. Questo articolo sono descritti questi elementi, organizzate dal formato di importazione hello di hello API.

## <a name="open-api"></a>Aprire l'API/Swagger
In generale, se si ricevono errori durante l'importazione del documento API aperta, verificare - sia stato convalidato utilizzando Progettazione hello in hello nuovo portale di Azure (progettazione - Front-End - Apri Editor di API specifica) oppure con un 3rd party strumento, ad esempio <a href="http://www.swagger.io"> Swagger Editor</a>.

* **Nome host** è necessario un attributo per il nome host.
* **Percorso base** è necessario un attributo per il percorso base.
* **Schemi** è necessaria una matrice di schemi. 

## <a name="wsdl"></a>WSDL
File WSDL sono toogenerate utilizzate le API SOAP di pass-through o fungono hello back-end di un'API SOAP-a-REST.

* **WSDL:Import**: le API che usano questo attributo non sono attualmente supportate. I clienti è necessario unire gli elementi importato hello in un unico documento.
* **Messaggi con più parti**: non sono attualmente supportati.
* I servizi SOAP **wsHttpBinding di WCF** creati con Windows Communication Foundation devono usare basicHttpBinding in quanto wsHttpBinding non è supportato.
* **MTOM**: i servizi che usano MTOM <em>potrebbero</em> funzionare. Al momento il supporto ufficiale non è previsto.
* **Ricorsione** tipi che sono definiti in modo ricorsivo (ad esempio, fare riferimento la matrice tooan di per sé) non sono supportati.

## <a name="wadl"> </a>WADL
Attualmente non sono noti problemi di importazione del formato WADL.


[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
