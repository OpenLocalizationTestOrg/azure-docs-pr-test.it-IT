---
title: aaaAuthenticating e l'autorizzazione a Power BI Embedded
description: Autenticazione e autorizzazione con Power BI Embedded
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a>Autenticazione e autorizzazione con Power BI Embedded

Usa servizio Power BI Embedded Hello **chiavi** e **App token** per l'autenticazione e autorizzazione, anziché l'autenticazione degli utenti finali esplicita. In questo modello è l'applicazione a gestire l'autenticazione e l'autorizzazione degli utenti finali. Se necessario, l'app crea e invia i token App hello indicante il nostro toorender servizio hello report richiesto. Questa soluzione non richiede il toouse app Azure Active Directory per l'autenticazione e autorizzazione, anche se è ancora possibile.

## <a name="two-ways-tooauthenticate"></a>Due modi tooauthenticate

**Chiave** : è possibile usare le chiavi per tutte le chiamate API REST di Power BI Embedded. le chiavi di Hello sono reperibile in hello **portale di Azure** facendo clic su **tutte le impostazioni** e quindi **le chiavi di accesso**. Occorre gestire sempre la chiave come se fosse una password. Queste chiavi hanno autorizzazioni toomake chiamare qualsiasi API REST su un insieme specifico dell'area di lavoro.

toouse una chiave in una chiamata REST, aggiungere hello intestazione di autorizzazione seguente:            

    Authorization: AppKey {your key}

**Token dell'app** : i token dell'app vengono usati per tutte le richieste di incorporamento. Si toobe progettato eseguire sul lato client, in modo che siano limitati tooa singoli report e le relative procedure consigliate tooset un'ora di scadenza.

I token dell'app sono token JSON Web (JWT, JSON Web Token) firmati da una delle chiavi dell'utente.

Il token di app può contenere hello seguenti attestazioni:

| Attestazione | Descrizione |
| --- | --- |
| **ver** |versione di Hello del token app hello. 0.2.0 è la versione corrente di hello. |
| **aud** |Hello destinatario del token hello. Per Power BI Embedded usare: "https://analysis.windows.net/powerbi/api". |
| **iss** |Stringa che indica un'applicazione hello che ha rilasciato il token hello. |
| **type** |tipo di Hello del token di app che viene creato. Tipo di hello è supportato solo corrente è **incorporare**. |
| **wcn** |Token hello del nome dell'area di lavoro insieme viene emessa per. |
| **wid** |Token di hello ID area di lavoro viene emessa per. |
| **rid** |Report è rilasciato per il token hello ID. |
| **username** (facoltativa) |Utilizzato con una riga, questa è una stringa che consenta di identificare l'utente hello quando l'applicazione delle regole di riga. |
| **roles** (facoltativa) |Stringa contenente hello ruoli tooselect quando l'applicazione delle regole di sicurezza a livello di riga. Se si passa più di un ruolo, è consigliabile passarli come matrice di stringhe. |
| **scp** (facoltativo) |Stringa contenente gli ambiti delle autorizzazioni hello. Se si passa più di un ruolo, è consigliabile passarli come matrice di stringhe. |
| **exp** (facoltativa) |Indica il tempo di hello in cui hello token scadrà. Questi valori devono essere passati come timestamp Unix. |
| **nbf** (facoltativa) |Indica il tempo di hello in cui hello token inizia validi. Questi valori devono essere passati come timestamp Unix. |

Un token dell'app di esempio avrà un aspetto analogo al seguente:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

Quando viene decodificato, avrà un aspetto analogo al seguente:

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

Sono disponibili metodi all'interno di hello SDK che consentono di semplificare la creazione di apptokens. Ad esempio, per .NET è possibile esaminare hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) classe e hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) metodi.

Per hello .NET SDK, è possibile fare riferimento troppo[ambiti](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).

## <a name="scopes"></a>Ambiti

Quando si utilizza il token di incorporamento, è consigliabile toorestrict utilizzo delle risorse di hello a che si concede l'accesso. Per questo motivo, è possibile generare un token con autorizzazioni con ambito.

di seguito Hello sono gli ambiti disponibili hello per Power BI Embedded.

|Scope|Descrizione|
|---|---|
|Dataset.Read|Sono disponibili autorizzazioni hello tooread specificato set di dati.|
|Dataset.Write|Fornisce l'autorizzazione toowrite toohello specificato set di dati.|
|Dataset.ReadWrite|Fornisce l'autorizzazione tooread e scrittura toohello specificato set di dati.|
|Report.Read|Sono disponibili autorizzazioni hello tooview specificato report.|
|Report.ReadWrite|Fornisce la modifica e dell'autorizzazione tooview hello report specificato.|
|Workspace.Report.Create|Fornisce un nuovo report all'interno di hello specificato di autorizzazione toocreate dell'area di lavoro.|
|Workspace.Report.Copy|Fornisce un report esistente all'interno di hello specificato di autorizzazione tooclone dell'area di lavoro.|

È possibile fornire più ambiti mediante uno spazio tra gli ambiti di hello hello seguente.

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

**Attestazioni e ambiti necessari**

SCP: scopesClaim {scopesClaim} può essere una stringa o una matrice di stringhe, notando hello consentito autorizzazioni risorse tooworkspace (Report, set di dati e così via)

Un token decodificato, con gli ambiti definiti, avrà un aspetto simile toohello seguente.

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a>Operazioni e ambiti

|Operazione|Risorsa di destinazione|Autorizzazioni del token|
|---|---|---|
|Creare (in memoria) un nuovo report basato su un set di dati.|Set di dati|Dataset.Read|
|Creare un nuovo report basato su un set di dati di (in memoria) e salvare report hello.|Set di dati|* Dataset.Read<br>* Workspace.Report.Create|
|Visualizzare ed esplorare/modificare (in memoria) un report esistente. Report.Read implica Dataset.Read. In questo modo non autorizzazioni toosave modifiche.|Report|Report.Read|
|Modificare e salvare un report esistente.|Report|Report.ReadWrite|
|Salvare una copia di un report (Salva con nome).|Report|* Report.Read<br>* Workspace.Report.Copy|

## <a name="heres-how-hello-flow-works"></a>Ecco il funzionamento del flusso di hello
1. Copiare un'applicazione hello API chiavi tooyour. È possibile ottenere le chiavi di hello in **portale Azure**.
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. Il token esegue l'asserzione di un'attestazione e ha una scadenza.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. Con le chiavi di accesso API si accede al token.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. L'utente richiede tooview un report.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. Il token viene convalidato con chiavi di accesso API.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. Power BI Embedded invia toouser un report.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

Dopo aver **Power BI Embedded** invia un utente, toohello hello visualizzare i report di hello nell'applicazione personalizzata. Ad esempio, se è stata importata hello [esempio di analisi delle vendite dati PBIX](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), app web di esempio hello è analogo al seguente:

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a>Vedere anche

[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Introduzione all'esempio di Microsoft Power BI Embedded](power-bi-embedded-get-started-sample.md)  
[Scenari comuni di Microsoft Power BI Embedded](power-bi-embedded-scenarios.md)  
[Introduzione a Microsoft Power BI Embedded](power-bi-embedded-get-started.md)  
[Repository Git PowerBI-CSharp](https://github.com/Microsoft/PowerBI-CSharp)  
Altre domande? [Provare a hello Community di Power BI](http://community.powerbi.com/)

