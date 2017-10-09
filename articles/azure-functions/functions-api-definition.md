---
title: metadati aaaOpenAPI nelle funzioni di Azure | Documenti Microsoft
description: Panoramica del supporto OpenAPI in Funzioni di Azure
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/23/2017
ms.author: alkarche
ms.openlocfilehash: fff8f14110469a002a6c9dca03f641672003a3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="openapi-20-metadata-support-in-azure-functions-preview"></a>Supporto per metadati OpenAPI 2.0 in Funzioni di Azure (anteprima)
OpenAPI 2.0 (in precedenza Swagger) supporto dei metadati nelle funzioni di Azure è una funzionalità di anteprima che è possibile utilizzare un 2.0 OpenAPI toowrite definizione all'interno di un'app di funzione. È quindi possibile ospitare tale file tramite app di funzione hello.

[Metadati OpenAPI](http://swagger.io/) consente a una funzione che ospita un toobe API REST utilizzato da un'ampia gamma di altri software. Il software include offerte Microsoft quali PowerApps e hello [funzionalità delle App per le API di Azure App Service](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), gli strumenti di sviluppo di terze parti come [Postman](https://www.getpostman.com/docs/importing_swagger), e [molti altri pacchetti](http://swagger.io/tools/).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

>[!TIP]
>È consigliabile iniziare con hello [esercitazione introduttiva](./functions-api-definition-getting-started.md) e restituendo quindi toothis documento toolearn ulteriori informazioni sulle funzionalità specifiche.

## <a name="enable"></a>Abilitare il supporto per la definizione OpenAPI
È possibile configurare tutte le impostazioni di OpenAPI su hello **di definizione dell'API** pagina dell'applicazione di funzione **funzionalità della piattaforma**.

generazione di hello tooenable di una definizione di OpenAPI ospitata e una definizione di avvio rapido, impostare **origine della definizione API** troppo**funzione (anteprima)**. **URL esterno** consente toouse la funzione di una definizione di OpenAPI che ha ospitato altrove.

## <a name="generate-definition"></a>Generare una struttura Swagger dai metadati della funzione
Per iniziare a scrivere la prima definizione OpenAPI può essere utile usare un modello. funzionalità di definizione del modello Hello crea una definizione di tipo sparse OpenAPI tramite tutti i metadati di hello nel file function.json hello per ognuna delle funzioni di trigger HTTP. È necessario toofill in ulteriori informazioni sull'API da hello [OpenAPI specifica](http://swagger.io/specification/), ad esempio i modelli di richiesta e risposta.

Per istruzioni dettagliate, vedere hello [esercitazione introduttiva](./functions-api-definition-getting-started.md).

### <a name="templates"></a>Modelli disponibili

|Nome| Descrizione |
|:-----|:-----|
|Definizione generata|Una definizione di OpenAPI con quantità massima di hello di informazioni che possono essere dedotto dai metadati esistenti della funzione hello.|

### <a name="quickstart-details"></a>Metadati inclusi nella definizione di hello generato

Hello seguente rappresenta tabella hello impostazioni del portale di Azure e i corrispondenti dati in function.json perché è mappato toohello generato Swagger scheletro.

|Swagger.json|Interfaccia utente del portale|Function.json|
|:----|:-----|:-----|
|[Host](http://swagger.io/specification/#fixed-fields-15)|**Impostazioni dell'app per le funzioni** > **Impostazioni del servizio app** > **Panoramica** > **URL**|*Non presente*
|[Percorsi](http://swagger.io/specification/#paths-object-29)|**Integrazione** > **Metodi HTTP selezionati**|Associazioni: Route
|[Elemento del percorso](http://swagger.io/specification/#path-item-object-32)|**Integrazione** > **Modello di route**|Associazioni: Metodi
|[Sicurezza](http://swagger.io/specification/#security-scheme-object-112)|**Chiavi**|*Non presente*|
|operationID*|**Route + Verbi consentiti**|Route + verbi consentiti|

\*ID operazione Hello è obbligatorio solo per l'integrazione con flusso e PowerApps.
> [!NOTE]
> estensione di x-ms-summary Hello fornisce un nome visualizzato flusso App per la logica e PowerApps.
>
> vedere, più toolearn [personalizzare la definizione Swagger per PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/).

## <a name="CICD"></a>Utilizzare definizione tooset un'API CI/CD-ROM

 È necessario abilitare l'API definizione hosting nel portale di hello prima di abilitare origine controllo toomodify la definizione dell'API dal controllo del codice sorgente. Seguire queste istruzioni:

1. Sfoglia troppo**(anteprima) di definizione dell'API** nelle impostazioni di app di funzione.
  1. Impostare **origine della definizione API** troppo**funzione**.
  1. Fare clic su **il modello di definizione API generare** e quindi **salvare** toocreate una definizione di modello per la modifica in un secondo momento.
  1. Prendere nota dell'URL di definizione dell'API e della chiave.
1. [Impostare l'integrazione continuata e la distribuzione continua (CI/CD)](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements).
2. Modificare il file swagger.json nel controllo del codice sorgente in \site\wwwroot\.azurefunctions\swagger\swagger.json.

A questo punto, le modifiche sono ospitati tooswagger.json nel repository dalla tua app di funzione all'URL di definizione API hello e chiave annotato nel passaggio 1.

## <a name="next-steps"></a>Passaggi successivi
* [Esercitazione introduttiva](functions-api-definition-getting-started.md). Provare il nostro toosee procedura dettagliata, una definizione di OpenAPI in azione.
* [Repository GitHub di Funzioni di Azure](https://github.com/Azure/Azure-Functions/). Estrarre hello funzioni repository toogive ci commenti e suggerimenti sull'anteprima del supporto definizione hello API. Crea un problema di GitHub per immettere le informazioni desiderate toosee aggiornato.
* [Informazioni di riferimento per sviluppatori su Funzioni di Azure](functions-reference.md). Informazioni sulla codifica delle funzioni e sulla definizione di trigger e associazioni.
