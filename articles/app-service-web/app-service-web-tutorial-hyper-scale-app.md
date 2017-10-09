---
title: aaaBuild un'app con in Azure | Documenti Microsoft
description: Informazioni su come toouse diversi servizi Azure toomaximize hello delle prestazioni di un'applicazione ASP.NET in Azure.
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: erikre
editor: 
ms.assetid: a4d49ac7-0f97-4997-84c5-cdb9c4465757
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/23/2017
ms.author: cephalin
ms.openlocfilehash: 7952647b49a82c286c6a737eb41a7f23a13fd75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a>Creare un'app Web con iperscalabilità in Azure

Questa esercitazione viene illustrato come tooscale un'App web ASP.NET in Azure toomaximize utente richieste.

Prima di iniziare questa esercitazione, assicurarsi che [hello CLI di Azure è installato](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) nel computer. Inoltre, è necessario [Visual Studio](https://www.visualstudio.com/vs/) sull'applicazione di esempio hello toorun computer locale.

## <a name="step-1---get-sample-application"></a>Passaggio 1: applicazione di esempio
In questo passaggio, impostare il progetto ASP.NET locale di hello.

### <a name="clone-hello-application-repository"></a>Repository di applicazione hello clone

Terminal della riga di comando di hello aperto di propria scelta e `CD` tooa directory di lavoro. Quindi, seguente hello esecuzione comandi tooclone l'applicazione di esempio hello. 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-hello-sample-application-in-visual-studio"></a>Eseguire l'applicazione di esempio hello in Visual Studio

Aprire la soluzione hello in Visual Studio.

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

Tipo `F5` toorun un'applicazione hello.

Questa applicazione web ASP.NET di esempio proviene dal modello predefinito hello e persiste utente sessioni e utilizza hello cache di output. Vedere `HighScaleApp\Controllers\HomeController.cs`. Hello `Index()` metodo aggiunge una parte della sessione toohello dati.

```csharp
Session.Add("visited", "true"); 
```

Hello e `About()` e `Contact()` metodi di memorizzare nella cache l'output.

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-tooazure"></a>Passaggio 2: distribuire tooAzure
In questo passaggio, creare un'app web di Azure e distribuire il tooit applicazione ASP.NET di esempio.

### <a name="create-a-resource-group"></a>Creare un gruppo di risorse   
Utilizzare [gruppo az creare](https://docs.microsoft.com/cli/azure/group#create) toocreate un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) nell'area Europa occidentale hello. È di un gruppo di risorse in cui inserire tutti hello risorse di Azure che si desidera toomanage insieme, ad esempio hello web app e tutti i Database SQL back-end.

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

toosee i possibili valori da utilizzare per `---location`, utilizzare hello [az appservice elenco posizioni](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) comando.

### <a name="create-an-app-service-plan"></a>Creare un piano di servizio app
Utilizzare [crea piano di servizio App az](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate "B1" [piano di servizio App](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

Un piano di servizio App è un'unità di scala, che può includere qualsiasi numero di applicazioni che si desidera tooscale o out over insieme hello stessa infrastruttura di servizio App. A ogni piano viene inoltre assegnato un [piano tariffario](https://azure.microsoft.com/en-us/pricing/details/app-service/). I piani tariffari superiori includono un hardware migliore e più caratteristiche, ad esempio un numero maggiore di istanze di scalabilità orizzontale.

Per questa esercitazione, B1 è livello minimo di hello che consente la scalabilità orizzontale toothree istanze. È sempre possibile spostare l'app verso l'alto o verso il basso hello piano tariffario in un secondo momento eseguendo [aggiornamento piani di az appservice](https://docs.microsoft.com/cli/azure/appservice/plan#update). 

### <a name="create-a-web-app"></a>Creare un'app Web
Utilizzare [web appservice az creare](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate un'app web con un nome univoco in `$appName`.

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a>Reimpostare le credenziali di distribuzione
Utilizzare [az appservice web distribuzione utente set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset credenziali la distribuzione a livello di account di servizio App.

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a>Configurare la distribuzione Git
Utilizzare [az appservice web controllo del codice sorgente config-locale-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) distribuzione Git locale tooconfigure.

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

Questo comando consente un output simile al seguente hello:

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

Hello utilizzare restituito tooconfigure URL il Git remote. Hello comando che segue utilizza hello precedente esempio di output.

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-hello-sample-application"></a>Distribuire l'applicazione di esempio hello
Si sono ora pronti toodeploy l'applicazione di esempio. Eseguire `git push`.

```powershell
git push azure master
```

Quando viene richiesta la password, utilizzare password hello specificato al momento dell'esecuzione `az appservice web deployment user set`.

### <a name="browse-tooazure-web-app"></a>Sfoglia tooAzure web app
Utilizzare [Sfoglia web di servizio App az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee l'app in esecuzione in tempo reale in Azure, eseguire questo comando.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-tooredis"></a>Passaggio 3: connettere tooRedis
In questo passaggio è Cache Redis di Azure come applicazione web di Azure tooyour cache esterna, con percorso condiviso. È possibile utilizzare rapidamente Redis toocache l'output delle pagine. In più, quando si scalano orizzontalmente le app Web in un secondo momento, Redis aiuta a mantenere le sessioni degli utenti su più istanze in maniera affidabile.

### <a name="create-an-azure-redis-cache"></a>Creare una cache Redis di Azure
Utilizzare [redis az creare](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate un Azure Redis Cache e di salvataggio hello output JSON. Usare un nome univoco in `$cacheName`.

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-hello-application-toouse-redis"></a>Configurare l'applicazione di hello toouse Redis
Formato stringa di connessione hello per la cache.

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

seconda riga Hello deve fornire un output simile al seguente:

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

In Visual Studio, creare un file di configurazione web nella radice del progetto denominato `redis.config` e Incolla hello seguente codice al suo interno. In `value`, utilizzare la stringa di connessione hello da hello output di PowerShell.

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

Se si osserva hello `.gitignore` file del repository Git, si noterà che il file è stato escluso dal controllo del codice sorgente. In questo modo le informazioni riservate vengono protette. 

Aprire `Web.config`. Hello preavviso `<appSettings file="redis.config">` elemento, che ottiene l'impostazione di hello è stato creato in `redis.config`. 

Trovare hello commentato sezione che include `<sessionState>` e `<caching>`. Rimuovere il commento in questa sezione.

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

Questo codice esegue la ricerca di stringa di connessione Redis hello è definito in `RedisConnection`. 

A questo punto l'applicazione utilizza le sessioni toomanage di Redis e la memorizzazione nella cache. Tipo `F5` toorun un'applicazione hello. Se si desidera, è possibile scaricare un Redis gestione client toovisualize hello dati ora salvati toohello cache.

### <a name="configure-hello-connection-string-in-azure"></a>Configurare la stringa di connessione hello in Azure

Per toowork l'applicazione in Azure, è necessario tooconfigure hello stessa stringa di connessione Redis nell'app web di Azure. Poiché `redis.config` non viene mantenuto nel controllo del codice sorgente, non è distribuito tooAzure quando si esegue la distribuzione Git.

Utilizzare [az appservice web configurazione appsettings aggiornare](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) stringa di connessione hello tooadd con hello stesso nome (`RedisConnection`).

az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup

Tenere presente che `$connstring` contiene la stringa di connessione hello formattato.

### <a name="redeploy-hello-application-tooazure"></a>Ridistribuire tooAzure applicazione hello
Utilizzare toopush comandi Git tooAzure le modifiche

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

Quando viene richiesta la password, utilizzare password hello specificato al momento dell'esecuzione `az appservice web deployment user set`.

### <a name="browse-toohello-azure-web-app"></a>Sfoglia toohello Azure web app
Utilizzare [Sfoglia web di servizio App az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) modifiche hello toosee risiedono in Azure.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-toomultiple-instances"></a>Passaggio 4: istanze toomultiple scala
piano di servizio App Hello è l'unità di scala hello per le app web di Azure. tooscale all'app web, è la scalabilità hello piano di servizio App.

Utilizzare [aggiornamento piani di az appservice](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale istanze di toothree piano di servizio App hello, che è il numero massimo consentito dal piano tariffario di hello B1 di hello. Tenere presente che B1 hello tariffario scelto al momento della creazione piano di servizio App in precedenza hello. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a>Passaggio 5: scalare geograficamente
Quando si ridimensiona geograficamente, si esegue l'app in più aree di hello cloud di Azure. Questo programma di installazione di bilanciamento del carico dell'app ulteriormente in base a geography e riduce il tempo di risposta hello inserendo browser tooclient più vicino di app.

In questo passaggio si modifica la scala ASP.NET web app tooa secondo paese con [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/). Alla fine di hello del passaggio di hello, si avrà un'app web in esecuzione in Europa occidentale (già creato) e un'app web in esecuzione in Asia sudorientale (non ancora creato). Verranno utilizzate entrambe le app da hello stesso URL di gestione traffico.

### <a name="scale-up-hello-europe-app-toostandard-tier"></a>Applicare la scalabilità verticale hello livello tooStandard di app Europa
Nel servizio App, integrazione con gestione traffico di Azure richiede il livello di prezzo Standard di hello. Utilizzare [aggiornamento piani di az appservice](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale backup il tooS1 piano di servizio App. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a>Creare un profilo di Gestione traffico 
Utilizzare [Crea profilo di gestione traffico di rete az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate un traffico di gestione del profilo e aggiungere il gruppo di risorse tooyour. Usare un nome DNS univoco in $dnsName.

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> `--routing-method Performance`Specifica che il profilo [instrada endpoint più vicino di utente traffico toohello](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="get-hello-resource-id-of-hello-europe-app"></a>Ottenere l'ID di risorsa hello di hello Europa app
Utilizzare [per web di servizio App az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello ID di risorsa dell'app web.

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-europe-app"></a>Aggiungere un endpoint di gestione traffico per app di hello Europa
Utilizzare [creare endpoint di gestione traffico di rete az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd un profilo di gestione traffico di tooyour endpoint e l'ID di risorsa di hello di utilizzo dell'app web come destinazione di hello.

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-hello-traffic-manager-endpoint-url"></a>Ottenere l'URL dell'endpoint di gestione traffico hello
Profilo di Traffic Manager dispone ora di un endpoint che punti tooyour esistente web app. Utilizzare [az rete gestione traffico profilo visualizzare](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget il relativo URL. 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

Copia output di hello nel browser. Dovrebbe essere visualizzata nuovamente l'app Web.

### <a name="create-an-azure-redis-cache-in-asia"></a>Creare una cache Redis di Azure in Asia
A questo punto, si replica l'area geografica di Azure web app toohello Asia sudorientale. toostart, utilizzare [redis az creare](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate un secondo Cache Redis di Azure in Asia sudorientale. Questa cache deve toobe installato con l'app in Asia.

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

`--name $cacheName-asia`Consente di hello Nome hello della cache di hello cache Europa occidentale, con hello `-asia` suffisso.

### <a name="create-an-app-service-plan-in-asia"></a>Creare un piano di servizio app in Asia
Utilizzare [crea piano di servizio App az](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate un servizio App secondo piano nell'area Asia sudorientale hello, utilizzando hello S1 stesso livello del piano di hello Europa occidentale.

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a>Creare un'app Web in Asia
Utilizzare [web appservice az creare](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate un'app web di secondo.

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

`--name $appName-asia`Consente di hello Nome hello app di app hello Europa occidentale, con hello `-asia` suffisso.

### <a name="configure-hello-connection-string-for-redis"></a>Configurare la stringa di connessione hello per Redis
Utilizzare [az appservice web configurazione appsettings aggiornare](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello web app hello connessione per hello cache Asia sudorientale.

az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup

### <a name="configure-git-deployment-for-hello-asia-app"></a>Configurare la distribuzione Git per app Asia hello.
Utilizzare [az appservice web controllo del codice sorgente config-locale-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure la distribuzione Git locale per l'app web secondo hello.

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

Questo comando consente un output simile al seguente hello:

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

Hello utilizzare restituito tooconfigure URL un secondo Git remoto per il repository locale. Hello comando che segue utilizza hello precedente esempio di output.

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a>Distribuire l'applicazione di esempio
Eseguire `git push` toodeploy remoto Git secondo l'esempio applicazione toohello. 

```bash
git push azure-asia master
```

Quando viene richiesta la password, utilizzare password hello specificato al momento dell'esecuzione `az appservice web deployment user set`.

### <a name="browse-toohello-asia-app"></a>Esplorare app Asia toohello
Utilizzare [Sfoglia web di servizio App az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify l'app è in esecuzione in tempo reale in Azure.

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-hello-resource-id-of-hello-asia-app"></a>Ottenere l'ID di risorsa hello di hello Asia app
Utilizzare [per web di servizio App az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello ID di risorsa dell'app web in Asia sudorientale.

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-asia-app"></a>Aggiungere un endpoint di gestione traffico per app Asia hello
Utilizzare [creare endpoint di gestione traffico di rete az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd un toohello endpoint secondo profilo di gestione traffico.

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-tooweb-apps"></a>Aggiungere App tooweb identificatore di area
Utilizzare [az appservice web configurazione appsettings aggiornare](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd una variabile di ambiente specifiche.

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

Il codice dell'applicazione usa già questa impostazione. Vedere `HighScaleApp\Views\Home\Index.cshtml`.

### <a name="complete"></a>Operazione completata

A questo punto, provare a tooaccess hello URL del profilo di Traffic Manager da parte dei browser in aree geografiche diverse. I browser client situati in Europa dovrebbero mostrare "ASP.NET Europa occidentale", mentre quelli in Asia dovrebbero mostrare "ASP.NET Asia sud-orientale".

## <a name="more-resources"></a>Altre risorse
