---
title: toouse aaaHow con REST di Power BI Embedded | Documenti Microsoft
description: 'Informazioni su come toouse con REST di Power BI Embedded '
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 8bcef780-cca0-4f30-9a9b-9daa1a7ae865
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 02/06/2017
ms.author: asaxton
ms.openlocfilehash: 98057724e60ba868f9c93de8c50383569eb8852d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-power-bi-embedded-with-rest"></a>Come toouse con REST di Power BI Embedded

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a>Power BI Embedded: che cos'è e a cosa serve

Una panoramica di Power BI Embedded descritto ufficiale hello [sito Power BI Embedded](https://azure.microsoft.com/services/power-bi-embedded/), ma verrà esaminata rapidamente prima di passare in dettaglio hello per utilizzarlo con REST.

È davvero semplice. potrebbe essere visualizzazioni di dati dinamica hello toouse di [Power BI](https://powerbi.microsoft.com) nella propria applicazione.

La maggior parte delle applicazioni personalizzate necessario dati hello toodeliver ai propri clienti, non necessariamente gli utenti nella propria organizzazione. Ad esempio, se si sta offrendo alcuni servizi per la società e la società B, gli utenti nella società dovrebbero visualizzare solo dati per la propria società A. Vale a dire, multi-tenancy hello è necessaria per il recapito di hello.

applicazione personalizzata Hello potrebbe anche essere offerta propri metodi di autenticazione, ad esempio l'autenticazione form, autenticazione di base, e così via... Quindi, hello incorporamento soluzione deve collaborare in modo sicuro con questo metodo di autenticazione esistente. È inoltre necessario per gli utenti toobe in grado di toouse tali applicazioni di ISV senza hello acquisto aggiuntiva o licenze di una sottoscrizione di Power BI.

 **Power BI Embedded** è progettato esattamente per questi tipi di scenari. In tal caso, ora che è disponibile tale introduzione fuori modo hello, iniziamo in dettaglio

È possibile usare .NET hello \(c#) o Node.js SDK, tooeasily compilare l'applicazione con Power BI Embedded. Tuttavia, in questo articolo verrà illustrato il flusso HTTP \(tra cui AuthN) di Power BI senza SDK. Questo flusso, è possibile compilare l'applicazione **con qualsiasi linguaggio di programmazione**, e si possono comprendere eccessivamente le tracce di hello di Power BI Embedded.

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a>Creare una raccolta di aree di lavoro di Power BI e ottenere la chiave di accesso \(provisioning)

Power BI incorporato è uno dei hello servizi di Azure. Solo hello ISV che usa il portale di Azure verrà addebitato i costi di utilizzo \(per la sessione utente di ogni ora), e gli utenti hello report hello viste non viene addebitato o persino richiede una sottoscrizione di Azure.
Prima di iniziare lo sviluppo di applicazioni, è necessario creare hello **raccolta dell'area di lavoro di Power BI** tramite il portale di Azure.

Ogni area di lavoro di Power BI Embedded è l'area di lavoro di hello per ogni cliente (tenant) e possiamo aggiungere molte aree di lavoro in ogni raccolta di area di lavoro. Hello stessa chiave di accesso viene utilizzato in ogni raccolta di area di lavoro. In concreto, raccolta di area di lavoro hello è il limite di sicurezza hello per Power BI Embedded.

![](media/power-bi-embedded-iframe/create-workspace.png)

Dopo il completamento di creazione della raccolta di hello dell'area di lavoro, copiare la chiave di accesso hello dal portale di Azure.

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> È anche possibile eseguire il provisioning hello dell'area di lavoro raccolta e ottenere la chiave di accesso tramite l'API REST. vedere, più toolearn [API del Provider di risorse di Power BI](https://msdn.microsoft.com/library/azure/mt712306.aspx).

## <a name="create-pbix-file-with-power-bi-desktop"></a>Creare file con estensione pbix con Power BI Desktop

Successivamente, è necessario creare connessione dati hello e toobe report incorporato.
Per questa attività, non è disponibile alcun codice o programmazione. È sufficiente usare Power BI Desktop.
In questo articolo non verranno esaminate tramite informazioni dettagliate hello toouse Power BI Desktop. Per assistenza, vedere [Introduzione a Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/). Per questo esempio, si userà solo hello [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a>Creare un'area di lavoro di Power BI

Ora che hello tutti il completamento del provisioning, iniziamo creazione dell'area di lavoro di un cliente nella raccolta di hello dell'area di lavoro tramite le API REST. Hello seguente HTTP POST richiesta (REST) è creazione hello nuova area di lavoro dell'insieme di area di lavoro esistente. Si tratta di hello [API dell'area di lavoro POST](https://msdn.microsoft.com/library/azure/mt711503.aspx). In questo esempio, nome della raccolta dell'area di lavoro hello è **mypbiapp**. È sufficiente impostare chiave di accesso hello, che viene copiati in precedenza, come **AppKey**. L'autenticazione è molto semplice.

**Richiesta HTTP**

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

**Risposta HTTP**

```
HTTP/1.1 201 Created
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces
RequestId: 4220d385-2fb3-406b-8901-4ebe11a5f6da

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/$metadata#workspaces/$entity",
  "workspaceId": "32960a09-6366-4208-a8bb-9e0678cdbb9d",
  "workspaceCollectionName": "mypbiapp"
}
```

Hello restituito **Idareadilavoro** viene utilizzato per hello dopo le chiamate API successive. L'applicazione deve mantenere questo valore.

## <a name="import-pbix-file-into-hello-workspace"></a>Importare i file con estensione pbix nell'area di lavoro hello

Ogni report in un'area di lavoro corrisponde tooa singolo file di Power BI Desktop con un set di dati \(incluse le impostazioni di origine dati). È possibile importare l'area toohello file pbix come illustrato nel seguente codice hello. Come si può notare, è possibile caricare file binario hello del file con estensione pbix usando multipart MIME in http.

frammento dell'uri Hello **32960a09-6366-4208-a8bb-9e0678cdbb9d** è Idareadilavoro hello e parametro di query **datasetDisplayName** è toocreate nome set di dati di hello. set di dati creato Hello contiene tutti i dati relativi elementi nel file con estensione pbix, ad esempio i dati importati, hello origine dati toohello di puntatore e così via...

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{hello content (binary) of .pbix file}
--A300testx--
```

Questa attività di importazione potrebbe richiedere qualche minuto. Al termine, l'applicazione può richiedere lo stato delle attività hello usando un id di importazione. In questo esempio, id di importazione hello è **4eec64dd-533b-47c3-a72c-6508ad854659**.

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

esempio Hello richiede lo stato utilizzando questo id di importazione:

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

Se l'attività hello non è stato completato, hello risposta HTTP potrebbe essere simile al seguente:

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: 614a13a5-4de7-43e8-83c9-9cd225535136

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Publishing",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "name": "mydataset01"
}
```

Se l'attività hello è stata completata, hello risposta HTTP può essere analogo al seguente:

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: eb2c5a85-4d7d-4cc2-b0aa-0bafee4b1606

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Succeeded",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "reports": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://app.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c"
    }
  ],
  "datasets": [
    {
      "id": "458e0451-7215-4029-80b3-9627bf3417b0",
      "name": "mydataset01",
      "tables": [
      ],
      "webUrl": "https://app.powerbi.com/datasets/458e0451-7215-4029-80b3-9627bf3417b0"
    }
  ],
  "name": "mydataset01"
}
```

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a>Connettività dell'origine dati \(e multi-tenancy dei dati)

Quasi tutti gli elementi di hello in file con estensione pbix vengono importati l'area di lavoro, le credenziali di hello per le origini dati non sono. Di conseguenza, quando si utilizza **modalità DirectQuery**, hello report incorporato non può essere visualizzato correttamente. Ma, quando si usano **la modalità di importazione**, è possibile visualizzare report hello utilizzando i dati importati esistenti hello. In tal caso, è necessario impostare credenziali hello utilizzando hello tramite chiamate REST come segue.

Innanzitutto, è necessario ottenere hello gateway datasource. Sappiamo hello dataset **id** è hello in precedenza ha restituito un id.

**Richiesta HTTP**

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

**Risposta HTTP**

```
GET HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: 574b0b18-a6fa-46a6-826c-e65840cf6e15

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#gatewayDatasources",
  "value": [
    {
      "id": "5f7ee2e7-4851-44a1-8b75-3eb01309d0ea",
      "gatewayId": "ca17e77f-1b51-429b-b059-6b3e3e9685d1",
      "datasourceType": "Sql",
      "connectionDetails": "{\"server\":\"testserver.database.windows.net\",\"database\":\"testdb01\"}"
    }
  ]
}
```

Usando hello restituiti id gateway e l'id origine dati \(vedere hello precedente **gatewayId** e **id** in hello restituito), è possibile modificare le credenziali di hello dell'origine dati, come indicato di seguito:

**Richiesta HTTP**

```
PATCH https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/gateways/ca17e77f-1b51-429b-b059-6b3e3e9685d1/datasources/5f7ee2e7-4851-44a1-8b75-3eb01309d0ea
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "credentialType": "Basic",
  "basicCredentials": {
    "username": "demouser",
    "password": "P@ssw0rd"
  }
}
```

**Risposta HTTP**

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

Nell'ambiente di produzione, è anche possibile impostare la stringa di connessione diversa hello per ogni area di lavoro tramite l'API REST. \(ad esempio, è possibile separare hello database per ciascun cliente.)

esempio Hello sta modificando la stringa di connessione hello dell'origine dati tramite REST.

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

In alternativa, è possibile utilizzare una sicurezza a livello di riga in Power BI Embedded ed è possibile separare i dati di hello per ciascun utente in un unico report. Di conseguenza, è possibile eseguire il provisioning di ogni report cliente con lo stesso file con estensione pbix \(interfaccia utente e così via) e origini dati diverse.

> [!NOTE]
> Se si utilizza **la modalità di importazione** anziché **modalità DirectQuery**, non vi è Nessun modello toorefresh modo tramite l'API. Inoltre, le origini dati locali mediante gateway di Power BI non sono ancora supportate in Power BI Embedded. Tuttavia, è opportuno effettivamente tookeep sotto controllo hello [blog di Power BI](https://powerbi.microsoft.com/blog/) per le novità e Novità nelle future versioni.

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a>Autenticazione e hosting (incorporamento) dei report nella pagina Web

In hello precedente API REST, è possibile usare la chiave di accesso hello **AppKey** stesso come intestazione di autorizzazione hello. Poiché queste chiamate possono essere gestite sul lato server back-end di hello, è sicuro.

Ma, quando si incorporano report hello nella nostra pagina web, verrebbe gestito di questo tipo di informazioni di sicurezza utilizzando JavaScript \(front-end). Valore dell'intestazione di autorizzazione hello deve quindi essere protetto. Se un utente malintenzionato o un codice dannoso individua la chiave di accesso, la può usare per chiamare qualsiasi operazione.

Quando si incorporano report hello nella nostra pagina web, è necessario utilizzare token calcolata hello anziché chiave di accesso **AppKey**. L'applicazione deve creare Token Web Json OAuth hello \(JWT) che include le attestazioni hello e firma digitale calcolata hello. Come illustrato di seguito, questo token JTW OAuth è il token di stringa con codifica delimitato da punti.

![](media/power-bi-embedded-iframe/oauth-jwt.png)

In primo luogo, è necessario preparare hello valore di input, che viene firmato in un secondo momento. Questo valore è hello base64 codificati nell'url (rfc4648) stringa hello seguente json e queste sono delimitate da punto hello \(.) caratteri. Successivamente, verrà illustrato come tooget hello id del report.

> [!NOTE]
> Se si desidera toouse a livello di sicurezza di riga con Power BI incorporato, è necessario specificare anche **username** e **ruoli** nelle attestazioni hello.

```
{
  "typ":"JWT",
  "alg":"HS256"
}
```

```
{
  "wid":"{workspace id}",
  "rid":"{report id}",
  "wcn":"{workspace collection name}",
  "iss":"PowerBISDK",
  "ver":"0.2.0",
  "aud":"https://analysis.windows.net/powerbi/api",
  "nbf":{start time of token expiration},
  "exp":{end time of token expiration}
}
```

Successivamente, è necessario creare stringa con codificata base64 hello del codice HMAC \(firma hello) con l'algoritmo SHA256. Questo valore di input con segno è stringa precedente hello.

Ultimo, sarà necessario combinare valore di input hello e stringa di firma utilizzando periodo \(.) caratteri. la stringa Hello completata è token app hello per hello incorporamento di report. Anche se il token di app hello viene individuato da un utente malintenzionato, è Impossibile ottenere chiave di accesso originale hello. Questo token dell'applicazione scadrà rapidamente.

Ecco un esempio di codice PHP per questi passaggi:

```
<?php
// 1. power bi access key
$accesskey = "MpaUgrTv5e...";

// 2. construct input value
$token1 = "{" .
  "\"typ\":\"JWT\"," .
  "\"alg\":\"HS256\"" .
  "}";
$token2 = "{" .
  "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
  "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
  "\"wcn\":\"mypbiapp\"," . // workspace collection name
  "\"iss\":\"PowerBISDK\"," .
  "\"ver\":\"0.2.0\"," .
  "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
  "\"nbf\":" . date("U") . "," .
  "\"exp\":" . date("U" , strtotime("+1 hour")) .
  "}";
$inputval = rfc4648_base64_encode($token1) .
  "." .
  rfc4648_base64_encode($token2);

// 3. get encoded signature
$hash = hash_hmac("sha256",
    $inputval,
    $accesskey,
    true);
$sig = rfc4648_base64_encode($hash);

// 4. show result (which is hello apptoken)
$apptoken = $inputval . "." . $sig;
echo($apptoken);

// helper functions
function rfc4648_base64_encode($arg) {
  $res = $arg;
  $res = base64_encode($res);
  $res = str_replace("/", "_", $res);
  $res = str_replace("+", "-", $res);
  $res = rtrim($res, "=");
  return $res;
}
?>
```

## <a name="finally-embed-hello-report-into-hello-web-page"></a>Infine, incorporare report hello pagina web hello

Per incorporare il report, è necessario ottenere hello incorporare url e report **id** utilizzando hello seguenti API REST.

**Richiesta HTTP**

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

**Risposta HTTP**

```
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: d4099022-405b-49d3-b3b7-3c60cf675958

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#reports",
  "value": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c",
      "isFromPbix": false
    }
  ]
}
```

È possibile incorporare report hello nella nostra app web con token app precedente hello.
Se si esamina il codice di esempio successivo hello, parte precedente hello è hello stesso esempio hello precedente. Nella parte di quest'ultimo hello, in questo esempio viene hello **embedUrl** \(vedere risultato precedente hello) in hello iframe, quindi esegue l'invio token app hello in iframe hello.

> [!NOTE]
> È necessario toochange hello report id valore tooone personalizzati. Inoltre, a causa di bug tooa nel nostro sistema di gestione dei contenuti, hello iframe nell'esempio di codice hello lettura tag letteralmente. Rimuovere testo hello delimitata da tag hello se si copia e incolla questo codice di esempio.

```
    <?php
    // 1. power bi access key
    $accesskey = "MpaUgrTv5e...";

    // 2. construct input value
    $token1 = "{" .
      "\"typ\":\"JWT\"," .
      "\"alg\":\"HS256\"" .
      "}";
    $token2 = "{" .
      "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
      "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
      "\"wcn\":\"mypbiapp\"," . // workspace collection name
      "\"iss\":\"PowerBISDK\"," .
      "\"ver\":\"0.2.0\"," .
      "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
      "\"nbf\":" . date("U") . "," .
      "\"exp\":" . date("U" , strtotime("+1 hour")) .
      "}";
    $inputval = rfc4648_base64_encode($token1) .
      "." .
      rfc4648_base64_encode($token2);

    // 3. get encoded signature value
    $hash = hash_hmac("sha256",
        $inputval,
        $accesskey,
        true);
    $sig = rfc4648_base64_encode($hash);

    // 4. get apptoken
    $apptoken = $inputval . "." . $sig;

    // helper functions
    function rfc4648_base64_encode($arg) {
      $res = $arg;
      $res = base64_encode($res);
      $res = str_replace("/", "_", $res);
      $res = str_replace("+", "-", $res);
      $res = rtrim($res, "=");
      return $res;
    }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Test page</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
      <button id="btnView">View Report !</button>
      <div id="divView">
        <**REMOVE THIS CAPPED TEXT IF COPIED** iframe id="ifrTile" width="100%" height="400"></iframe>
      </div>
      <script>
        (function () {
          document.getElementById('btnView').onclick = function() {
            var iframe = document.getElementById('ifrTile');
            iframe.src = 'https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c';
            iframe.onload = function() {
              var msgJson = {
                action: "loadReport",
                accessToken: "<?=$apptoken?>",
                height: 500,
                width: 722
              };
              var msgTxt = JSON.stringify(msgJson);
              iframe.contentWindow.postMessage(msgTxt, "*");
            };
          };
        }());
      </script>
    </body>
```

Ed ecco il risultato:

![](media/power-bi-embedded-iframe/view-report.png)

In questo momento, Power BI Embedded vengono visualizzati solo report hello in iframe hello. Tuttavia, è consigliabile monitorare hello [Blog di Power BI](https://powerbi.microsoft.com/blog/). Miglioramenti futuri utilizzi lato client nuova API che verranno possiamo inviare informazioni in iframe hello, nonché ottenere informazioni. Ci sono tanti aspetti interessanti.

## <a name="see-also"></a>Vedere anche
* [Autenticazione e autorizzazione con Power BI Embedded](power-bi-embedded-app-token-flow.md)

Altre domande? [Provare a hello Community di Power BI](http://community.powerbi.com/)

