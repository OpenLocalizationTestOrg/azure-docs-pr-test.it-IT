---
title: dominio personalizzato aaaAdd e tooan SSL Azure web app | Documenti Microsoft
description: "Informazioni su come tooprepare di Azure web produzione toogo app aggiungendo il marchio della società. Eseguire il mapping di app web tooyour di hello dominio personalizzato nome (dominio personale) e proteggerla con un certificato SSL personalizzato."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 03/29/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2679ed8b2dbbeba0b128c1a3ec01148f97c35342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-domain-and-ssl-tooan-azure-web-app"></a>Aggiungi dominio personalizzato e SSL tooan Azure web app

Questa esercitazione viene illustrato come eseguire il mapping di un'app di web Azure tooyour nome di dominio personalizzato e come proteggere con un certificato SSL personalizzato tooquickly. 

## <a name="before-you-begin"></a>Prima di iniziare

Prima di eseguire questo esempio, installare hello [CLI di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) localmente.

È necessario anche la pagina di configurazione di accesso amministrativo toohello DNS per il provider del rispettivo dominio. Ad esempio, tooadd `www.contoso.com`, è necessario toobe tooconfigure in grado di ottenere voci DNS per `contoso.com`.

Infine, è necessario un valore valido. Il file PFX _e_ la relativa password per il certificato SSL hello desiderato tooupload ed eseguire l'associazione. Questo certificato SSL deve essere configurato toosecure nome di dominio personalizzato di hello desiderato. In hello esempio precedente, è necessario proteggere il certificato SSL `www.contoso.com`. 

## <a name="step-1---create-an-azure-web-app"></a>Passaggio 1 - Creare un'app Web di Azure

### <a name="log-in-tooazure"></a>Accedi tooAzure

Ci sono ora corso toouse hello Azure CLI 2.0 nelle risorse di hello toocreate finestra terminale necessari toohost nostra app Node.js in Azure.  Accedere alla sottoscrizione di Azure con hello tooyour [accesso az](/cli/azure/#login) comando e seguire hello le direzioni. 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a>Creare un gruppo di risorse   
Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create). Un gruppo di risorse di Azure è un contenitore logico in cui vengono distribuite e gestite risorse di Azure come app Web, database e account di archiviazione. 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

toosee i possibili valori da utilizzare per `---location`, utilizzare hello `az appservice list-locations` comando CLI di Azure.

## <a name="create-an-app-service-plan"></a>Creare un piano di servizio app

Creare un piano di servizio App con hello [crea piano di servizio App az](/cli/azure/appservice/plan#create) comando. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

esempio Hello crea un piano di servizio App denominato `myAppServicePlan` utilizzando hello **base** piano tariffario.

az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1

Dopo aver creato il piano di servizio App hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente. 

```json 
{ 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "kind": "app", 
    "location": "West Europe", 
    "sku": { 
    "capacity": 1, 
    "family": "B", 
    "name": "B1", 
    "tier": "Basic" 
    }, 
    "status": "Ready", 
    "type": "Microsoft.Web/serverfarms" 
} 
``` 

## <a name="create-a-web-app"></a>Creare un'app Web

Ora che è stato creato un piano di servizio App, creare un'app web all'interno di hello `myAppServicePlan` piano di servizio App. Consente di app web Hello è in un host toodeploy spazio il codice, nonché fornisce un URL per l'utente tooview hello applicazione distribuita. Hello utilizzare [web appservice az creare](/cli/azure/appservice/web#create) comando toocreate hello web app. 

Nel comando hello seguente, sostituire con il proprio nome univoco di app in cui si vedere hello `<app_name>` segnaposto. Questo nome verrà usato come parte di hello hello predefinito del nome di dominio per l'app web hello, quindi nome hello deve toobe univoco tra tutte le App in Azure. È possibile mappare qualsiasi app web toohello di voce DNS personalizzato in un secondo momento per esporre gli utenti tooyour. 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

Quando è stato creato l'app web hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente. 

```json 
{ 
    "clientAffinityEnabled": true, 
    "defaultHostName": "<app_name>.azurewebsites.net", 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<app_name>", 
    "isDefaultContainer": null, 
    "kind": "app", 
    "location": "West Europe", 
    "name": "<app_name>", 
    "repositorySiteName": "<app_name>", 
    "reserved": true, 
    "resourceGroup": "myResourceGroup", 
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "state": "Running", 
    "type": "Microsoft.Web/sites", 
} 
```

Dall'output JSON, hello `defaultHostName` Mostra nome di dominio dell'applicazione web predefinita. Nel browser, passare l'indirizzo toothis.

```
http://<app_name>.azurewebsites.net 
``` 
 
![App Web creata nel servizio app](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a>Passaggio 2 - Configurare il mapping DNS

In questo passaggio, è possibile aggiungere un mapping dal nome di dominio predefinito dell'app web un dominio personalizzato tooyour, `<app_name>.azurewebsites.net`. In genere si esegue questo passaggio nel sito Web del provider del dominio. Il sito Web di ogni registrar di dominio è leggermente diverso, quindi è consigliabile vedere la documentazione del provider. Di seguito sono tuttavia indicate alcune linee guida generali. 

### <a name="navigate-tootoodns-management-page"></a>Passare la pagina di gestione tootooDNS

Innanzitutto, effettuare l'accesso del sito Web del registrar di dominio tooyour.  

Quindi, individuare pagina hello per la gestione dei record DNS. Cercare i collegamenti o aree del sito hello etichettata **nome di dominio**, **DNS**, o **denomina Gestione Server**. Spesso, è possibile trovare il collegamento hello visualizzando le informazioni sull'account, e quindi cercare, ad esempio un collegamento **My domains**.

Una volta trovata la pagina, cercare un collegamento che consenta di aggiungere o modificare i record DNS. Potrebbe trattarsi di un collegamento a un **file di zona** o a **record DNS** oppure di un collegamento a una **configurazione avanzata**.

### <a name="create-a-cname-record"></a>Creare un record CNAME

Aggiungere un record CNAME che associa il nome di dominio predefinito hello sottodominio desiderato nome tooyour dell'applicazione web (`<app_name>.azurewebsites.net`, dove `<app_name>` è nome univoco dell'applicazione).

Per hello `www.contoso.com` esempio, si crea un record CNAME che esegue il mapping hello `www` nome host troppo`<app_name>.azurewebsites.net`.

## <a name="step-3---configure-hello-custom-domain-on-your-web-app"></a>Passaggio 3: configurare dominio personalizzato hello nell'app web

Al termine della configurazione di mapping hostname hello nel sito Web del provider di dominio, si è pronti tooconfigure dominio personalizzato di hello nell'app web. Hello utilizzare [az appservice web configurazione hostname aggiungere](/cli/azure/appservice/web/config/hostname#add) comando tooadd questa configurazione. 

Nel comando hello seguente, sostituire `<app_name>` con il nome univoco dell'app e < your_custom_domain > con il nome di dominio personalizzato completo hello (ad esempio `www.contoso.com`). 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

dominio personalizzato Hello è ora completamente mappato tooyour web app. Nel browser, passare il nome di dominio personalizzato toohello. ad esempio:

```
http://www.contoso.com 
``` 

![App Web creata nel servizio app](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-tooyour-web-app"></a>Passaggio 4: associare un'app web tooyour di certificati SSL personalizzata

È ora disponibile un'app web di Azure, con il nome di dominio hello desiderato nella barra degli indirizzi del browser hello. Tuttavia, se si passa toohello `https://<your_custom_domain>` a questo punto, si verifica un errore di certificato. 

![App Web creata nel servizio app](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

Questo errore si verifica perché l'app Web non ha ancora un binding a un certificato SSL corrispondente al nome del dominio personalizzato. Tuttavia, non si verifica un errore se si passa troppo`https://<app_name>.azurewebsites.net`. In questo modo l'app, nonché tutte le applicazioni di servizio App di Azure, è protetto con il certificato SSL hello per hello `*.azurewebsites.net` dominio con caratteri jolly per impostazione predefinita. 

In Ordina tooaccess app web per il nome di dominio personalizzato, è necessario certificato SSL di toobind hello per le app web toohello di dominio personalizzato. Questa operazione verrà eseguita in questo passaggio. 

### <a name="upload-hello-ssl-certificate"></a>Caricare il certificato SSL hello

Caricare il certificato SSL hello per le app web tooyour di dominio personalizzato tramite hello [az appservice configurazione ssl caricamento](/cli/azure/appservice/web/config/ssl#upload) comando.

Nel comando hello seguente, sostituire `<app_name>` con il nome univoco di app, `<path_to_ptx_file>` con tooyour percorso hello. Il file PFX, e `<password>` con la password del certificato. 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

Quando viene caricato il certificato di hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:

```json
{
  "cerBlob": null,
  "expirationDate": "2018-03-29T14:12:57+00:00",
  "friendlyName": "",
  "hostNames": [
    "www.contoso.com"
  ],
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/cert
ificates/9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "issueDate": "2017-03-29T14:12:57+00:00",
  "issuer": "www.contoso.com",
  "keyVaultId": null,
  "keyVaultSecretName": null,
  "keyVaultSecretStatus": "Initialized",
  "kind": null,
  "location": "West Europe",
  "name": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "password": null,
 "pfxBlob": null,
  "publicKeyHash": null,
  "resourceGroup": "myResourceGroup",
  "selfLink": null,
  "serverFarmId": null,
  "siteName": null,
  "subjectName": "www.contoso.com",
  "tags": null,
  "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00",
  "type": "Microsoft.Web/certificates",
  "valid": null
}
```

Dall'output JSON, hello `thumbprint` Mostra l'identificazione personale del certificato caricato. Copiare il valore per il passaggio successivo hello.

### <a name="bind-hello-uploaded-ssl-certificate-toohello-web-app"></a>Associare l'applicazione web di hello caricato SSL certificati toohello

L'app web ha ora il nome di dominio personalizzato hello desiderato e include anche un certificato SSL che protegge il dominio personalizzato. Hello solo toodo a sinistra di cosa è toobind hello certificato caricato toohello web app. Farlo tramite hello [il binding ssl az appservice web configurazione](/cli/azure/appservice/web/config/ssl#bind) comando.

Nel comando hello seguente, sostituire `<app_name>` con il nome univoco di app e `<thumbprint-from-previous-output>` con identificazione personale del certificato hello che vengono recuperate dal comando precedente hello. 

az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI

Quando hello certificato associate tooyour web app, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:

{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }

Nel browser passare endpoint tooHTTPS del nome di dominio personalizzato. ad esempio:

```
https://www.contoso.com 
``` 

![App Web creata nel servizio app](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a>Altre risorse

[Acquistare e configurare un nome di dominio personalizzato in Servizio app di Azure](custom-dns-web-site-buydomains-web-app.md)
[Acquistare e configurare un certificato SSL per il servizio app di Azure](web-sites-purchase-ssl-web-site.md)
