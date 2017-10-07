---
title: aaaAuthenticate con le API REST di Engagement Mobile
description: Viene descritto come tooauthenticate con le API REST di Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: da82cb36-957a-4e19-a805-b44733cf6597
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 9b54aa5ec3da4bcf55ffe5b7e8d1759095d0c486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a>Eseguire l'autenticazione con le API REST di Mobile Engagement
## <a name="overview"></a>Panoramica
Questo documento descrive come un Oauth di AAD valido di tooget token tooauthenticate con hello API REST di Engagement Mobile. 

Si presuppone che l'utente abbia una sottoscrizione di Azure valida e che abbia creato un'app Mobile Engagement usando una delle [Esercitazioni per sviluppatori](mobile-engagement-windows-store-dotnet-get-started.md).

## <a name="authentication"></a>Autenticazione
È necessario usare per l'autenticazione un token OAuth basato su Microsoft Azure Active Directory. 

Nella richiesta di ordine tooauthentication un'API, un'intestazione di autorizzazione deve essere aggiunto richiesta tooevery di hello seguente formato:

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> I token di Azure Active Directory scadono in un'ora.
> 
> 

Esistono diversi modi tooget un token. Poiché hello che API vengono in genere chiamate da un servizio cloud, si desidera toouse una chiave API. Nella terminologia di Azure una chiave API è una password dell'entità servizio. Hello procedura seguente viene illustrato un modo toosetting il backup manualmente.

### <a name="one-time-setup-using-script"></a>Installazione singola (mediante script)
È consigliabile seguire il set di hello di istruzioni che seguono il programma di installazione di tooperform hello tramite uno script di PowerShell che richiede hello tempo minimo per l'installazione, ma vengono utilizzati valori predefiniti più ammissibili hello. Facoltativamente, è possibile inoltre seguire le istruzioni hello hello [installazione manuale](mobile-engagement-api-authentication-manual.md) per eseguire questa operazione da hello direttamente portale di Azure e configurazione di eseguire più preciso. 

1. Ottenere la versione più recente di hello di Azure PowerShell da [qui](http://aka.ms/webpi-azps). Per ulteriori informazioni sulle istruzioni di download di hello, è possibile visualizzare questo [collegamento](/powershell/azure/overview).  
2. Una volta installato Azure PowerShell, seguito hello utilizzare comandi tooensure di aver hello **modulo Azure** installato:
   
    a. Verificare che il modulo di Azure PowerShell hello è disponibile nell'elenco di hello dei moduli disponibili. 
   
        Get-Module –ListAvailable 
   
    ![Moduli di Azure disponibili][1]
   
    b. Se non si trova il modulo di Azure PowerShell hello in hello sopra l'elenco è necessario seguente hello toorun:
   
        Import-Module Azure 
3. Account di accesso toohello, Gestione risorse di Azure da PowerShell eseguendo hello comando seguente e di fornire il nome utente e la password per l'account di Azure: 
   
        Login-AzureRmAccount
4. Se sono presenti più sottoscrizioni, è consigliabile eseguire l'esempio hello:
   
    a. Ottenere un elenco di tutte le sottoscrizioni e hello copia SubscriptionId della sottoscrizione hello da toouse. Verificare che la sottoscrizione è quello che ha hello App Engagement Mobile che si prevede di hello toointeract con hello API. 
   
        Get-AzureRmSubscription
   
    b. Comando che segue di hello esecuzione fornendo hello SubscriptionId tooconfigure hello sottoscrizione toobe utilizzato.
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. Copiare il testo hello per hello [New AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) script tooyour locali e salvarlo come un cmdlet di PowerShell (ad esempio `APIAuth.ps1`) ed eseguirlo `.\APIAuth.ps1`. 
6. Hello script chiederà tooprovide un input per **nome dell'entità**. Fornire un nome appropriato che si desidera toouse toocreate l'applicazione di Active Directory (ad esempio APIAuth). 
7. Al termine dell'esecuzione dello script hello, verrà visualizzato hello seguenti quattro valori che è necessario tooauthenticate a livello di programmazione con Active Directory per rendere toocopy che li. 
   
    **TenantId**, **SubscriptionId**, **ApplicationId** e **Secret**.
   
    TenantId sarà usato come `{TENANT_ID}`, ApplicationId come `{CLIENT_ID}` e Secret come `{CLIENT_SECRET}`.
   
   > [!NOTE]
   > I criteri di sicurezza predefiniti possono bloccare l'esecuzione degli script PowerShell. In questo caso, configurare temporaneamente l'esecuzione di script tooallow dei criteri di esecuzione utilizzando hello comando seguente:
   > 
   > Set-ExecutionPolicy RemoteSigned
   > 
   > 
8. Ecco come set di hello di cmdlet di PS avrà un aspetto analogo. 
   
    ![][3]
9. Controllare nel portale di gestione di Azure hello che una nuova applicazione di Active Directory è stata creata con il nome di hello è fornito toohello script chiamato **nome dell'entità** in **applicazioni Mostra proprietà dell'azienda**.
   
    ![][4]

#### <a name="steps-tooget-a-valid-token"></a>Passaggi tooget un token valido
1. Chiamata API hello con hello seguenti parametri e verificare che tooreplace hello TENANT\_ID, i CLIENT\_ID e CLIENT\_segreto:
   
   * **URL richiesta** come *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*
   * **Intestazione Content-Type HTTP** come *application/x-www-form-urlencoded*
   * **Corpo richiesta HTTP** come *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*
     
     di seguito Hello è un esempio di richiesta:
     
       POST / {TENANT_ID} / oauth2/token Host HTTP/1.1: login.microsoftonline.com Content-Type: grant_type application/x-www-form-urlencoded = client_credentials & client_id = {CLIENT_ID} & client_secret = {CLIENT_SECRET} & reso urce=https%3A%2F%2Fmanagement.core.windows.net%2F
     
     Di seguito è riportata una risposta di esempio:
     
       HTTP/1.1 200 OK Content-Type: application/json; charset = utf-8. Content-Length: 1234
     
       {"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}
     
     In questo esempio è inclusa la codifica URL dei parametri POST hello, `resource` valore sia effettivamente `https://management.core.windows.net/`. Assicurarsi che la codifica URL tooalso `{CLIENT_SECRET}` , che potrebbe contenere caratteri speciali.
     
     > [!NOTE]
     > Per i test, è possibile usare uno strumento client HTTP come [Fiddler](http://www.telerik.com/fiddler) o [l'estensione Chrome Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop) 
     > 
     > 
2. In ogni chiamata API, includono ora intestazione di richiesta di autorizzazione hello:
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    Se viene visualizzato un codice di 401 stato restituito, corpo della risposta hello controllo, potrebbe indicare hello token è scaduto. In caso affermativo, ottenere un nuovo token.

## <a name="using-hello-apis"></a>Utilizzando le API di hello
Dopo aver creato un token valido, si è pronti toomake hello API chiamate.

1. In ogni richiesta di API, è necessario un token valido e non scaduto è ottenuto nella sezione precedente di hello toopass.
2. È necessario tooplug alcuni parametri nella richiesta di hello URI che identifica l'applicazione. URI della richiesta Hello è simile a hello seguente
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    parametri di hello tooget, fare clic sul nome dell'applicazione e fare clic su Dashboard per visualizzare una pagina come segue hello con tutte hello 3 parametri.
   
   * **1**`{subscription-id}`
   * **2**`{app-collection}`
   * **3**`{app-resource-name}`
   * **4** nome del gruppo di risorse sta toobe **MobileEngagement** a meno che non è stato creato uno nuovo. 
     
     ![Parametri URI API di Mobile Engagement][2]

> [!NOTE]
> <br/>
> 
> 1. Ignorare hello indirizzo radice API perché questo era per hello API precedente.<br/>
> 2. Se si hello app creata usando il portale di Azure classico è necessario nome di risorsa dell'applicazione hello toouse che è diverso dal nome dell'applicazione hello stesso. Se si crea l'applicazione hello in hello portale di Azure è necessario utilizzare hello Nome App stesso (non vi è alcuna differenza tra il nome di risorsa dell'applicazione e il nome dell'App per le app create nel nuovo portale di hello).  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



