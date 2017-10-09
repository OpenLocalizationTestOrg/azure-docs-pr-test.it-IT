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
# <a name="add-custom-domain-and-ssl-tooan-azure-web-app"></a><span data-ttu-id="8f8f7-104">Aggiungi dominio personalizzato e SSL tooan Azure web app</span><span class="sxs-lookup"><span data-stu-id="8f8f7-104">Add custom domain and SSL tooan Azure web app</span></span>

<span data-ttu-id="8f8f7-105">Questa esercitazione viene illustrato come eseguire il mapping di un'app di web Azure tooyour nome di dominio personalizzato e come proteggere con un certificato SSL personalizzato tooquickly.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-105">This tutorial shows you how tooquickly map a custom domain name tooyour Azure web app and then secure it with a custom SSL certificate.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="8f8f7-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="8f8f7-106">Before you begin</span></span>

<span data-ttu-id="8f8f7-107">Prima di eseguire questo esempio, installare hello [CLI di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) localmente.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-107">Before running this sample, install hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) locally.</span></span>

<span data-ttu-id="8f8f7-108">È necessario anche la pagina di configurazione di accesso amministrativo toohello DNS per il provider del rispettivo dominio.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-108">You also need administrative access toohello DNS configuration page for your respective domain provider.</span></span> <span data-ttu-id="8f8f7-109">Ad esempio, tooadd `www.contoso.com`, è necessario toobe tooconfigure in grado di ottenere voci DNS per `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-109">For example, tooadd `www.contoso.com`, you need toobe able tooconfigure DNS entries for `contoso.com`.</span></span>

<span data-ttu-id="8f8f7-110">Infine, è necessario un valore valido. Il file PFX _e_ la relativa password per il certificato SSL hello desiderato tooupload ed eseguire l'associazione.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-110">Lastly, you need a valid .PFX file _and_ its password for hello SSL certificate you want tooupload and bind.</span></span> <span data-ttu-id="8f8f7-111">Questo certificato SSL deve essere configurato toosecure nome di dominio personalizzato di hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-111">This SSL certificate should be configured toosecure hello custom domain name you want.</span></span> <span data-ttu-id="8f8f7-112">In hello esempio precedente, è necessario proteggere il certificato SSL `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-112">In hello above example, your SSL certificate should secure `www.contoso.com`.</span></span> 

## <a name="step-1---create-an-azure-web-app"></a><span data-ttu-id="8f8f7-113">Passaggio 1 - Creare un'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="8f8f7-113">Step 1 - Create an Azure web app</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="8f8f7-114">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="8f8f7-114">Log in tooAzure</span></span>

<span data-ttu-id="8f8f7-115">Ci sono ora corso toouse hello Azure CLI 2.0 nelle risorse di hello toocreate finestra terminale necessari toohost nostra app Node.js in Azure.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-115">We are now going toouse hello Azure CLI 2.0 in a terminal window toocreate hello resources needed toohost our Node.js app in Azure.</span></span>  <span data-ttu-id="8f8f7-116">Accedere alla sottoscrizione di Azure con hello tooyour [accesso az](/cli/azure/#login) comando e seguire hello le direzioni.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-116">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="8f8f7-117">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="8f8f7-117">Create a resource group</span></span>   
<span data-ttu-id="8f8f7-118">Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="8f8f7-118">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="8f8f7-119">Un gruppo di risorse di Azure è un contenitore logico in cui vengono distribuite e gestite risorse di Azure come app Web, database e account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-119">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

<span data-ttu-id="8f8f7-120">toosee i possibili valori da utilizzare per `---location`, utilizzare hello `az appservice list-locations` comando CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-120">toosee what possible values you can use for `---location`, use hello `az appservice list-locations` Azure CLI command.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="8f8f7-121">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="8f8f7-121">Create an App Service plan</span></span>

<span data-ttu-id="8f8f7-122">Creare un piano di servizio App con hello [crea piano di servizio App az](/cli/azure/appservice/plan#create) comando.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-122">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="8f8f7-123">esempio Hello crea un piano di servizio App denominato `myAppServicePlan` utilizzando hello **base** piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-123">hello following example creates an App Service plan named `myAppServicePlan` using hello **Basic** pricing tier.</span></span>

<span data-ttu-id="8f8f7-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span><span class="sxs-lookup"><span data-stu-id="8f8f7-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span></span>

<span data-ttu-id="8f8f7-125">Dopo aver creato il piano di servizio App hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-125">When hello App Service plan has been created, hello Azure CLI shows information similar toohello following example.</span></span> 

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

## <a name="create-a-web-app"></a><span data-ttu-id="8f8f7-126">Creare un'app Web</span><span class="sxs-lookup"><span data-stu-id="8f8f7-126">Create a web app</span></span>

<span data-ttu-id="8f8f7-127">Ora che è stato creato un piano di servizio App, creare un'app web all'interno di hello `myAppServicePlan` piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-127">Now that an App Service plan has been created, create a web app within hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="8f8f7-128">Consente di app web Hello è in un host toodeploy spazio il codice, nonché fornisce un URL per l'utente tooview hello applicazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-128">hello web app gives your a hosting space toodeploy your code as well as provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="8f8f7-129">Hello utilizzare [web appservice az creare](/cli/azure/appservice/web#create) comando toocreate hello web app.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-129">Use hello [az appservice web create](/cli/azure/appservice/web#create) command toocreate hello web app.</span></span> 

<span data-ttu-id="8f8f7-130">Nel comando hello seguente, sostituire con il proprio nome univoco di app in cui si vedere hello `<app_name>` segnaposto.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-130">In hello command below, please substitute your own unique app name where you see hello `<app_name>` placeholder.</span></span> <span data-ttu-id="8f8f7-131">Questo nome verrà usato come parte di hello hello predefinito del nome di dominio per l'app web hello, quindi nome hello deve toobe univoco tra tutte le App in Azure.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-131">This unique name will be used as hello part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="8f8f7-132">È possibile mappare qualsiasi app web toohello di voce DNS personalizzato in un secondo momento per esporre gli utenti tooyour.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-132">You can later map any custom DNS entry toohello web app before you expose it tooyour users.</span></span> 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

<span data-ttu-id="8f8f7-133">Quando è stato creato l'app web hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-133">When hello web app has been created, hello Azure CLI shows information similar toohello following example.</span></span> 

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

<span data-ttu-id="8f8f7-134">Dall'output JSON, hello `defaultHostName` Mostra nome di dominio dell'applicazione web predefinita.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-134">From hello JSON output, `defaultHostName` shows your web app's default domain name.</span></span> <span data-ttu-id="8f8f7-135">Nel browser, passare l'indirizzo toothis.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-135">In your browser, navigate toothis address.</span></span>

```
http://<app_name>.azurewebsites.net 
``` 
 
![App Web creata nel servizio app](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a><span data-ttu-id="8f8f7-137">Passaggio 2 - Configurare il mapping DNS</span><span class="sxs-lookup"><span data-stu-id="8f8f7-137">Step 2 - Configure DNS mapping</span></span>

<span data-ttu-id="8f8f7-138">In questo passaggio, è possibile aggiungere un mapping dal nome di dominio predefinito dell'app web un dominio personalizzato tooyour, `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-138">In this step, you add a mapping from a custom domain tooyour web app's default domain name, `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="8f8f7-139">In genere si esegue questo passaggio nel sito Web del provider del dominio.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-139">Typically, you perform this step in your domain provider's website.</span></span> <span data-ttu-id="8f8f7-140">Il sito Web di ogni registrar di dominio è leggermente diverso, quindi è consigliabile vedere la documentazione del provider.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-140">Every domain registrar's website is slightly different, so you should consult your provider's documentation.</span></span> <span data-ttu-id="8f8f7-141">Di seguito sono tuttavia indicate alcune linee guida generali.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-141">However, here are some general guidelines.</span></span> 

### <a name="navigate-tootoodns-management-page"></a><span data-ttu-id="8f8f7-142">Passare la pagina di gestione tootooDNS</span><span class="sxs-lookup"><span data-stu-id="8f8f7-142">Navigate tootooDNS management page</span></span>

<span data-ttu-id="8f8f7-143">Innanzitutto, effettuare l'accesso del sito Web del registrar di dominio tooyour.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-143">First, log in tooyour domain registrar's website.</span></span>  

<span data-ttu-id="8f8f7-144">Quindi, individuare pagina hello per la gestione dei record DNS.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-144">Then, find hello page for managing DNS records.</span></span> <span data-ttu-id="8f8f7-145">Cercare i collegamenti o aree del sito hello etichettata **nome di dominio**, **DNS**, o **denomina Gestione Server**.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-145">Look for links or areas of hello site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="8f8f7-146">Spesso, è possibile trovare il collegamento hello visualizzando le informazioni sull'account, e quindi cercare, ad esempio un collegamento **My domains**.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-146">Often, you can find hello link by viewing your account information, and then looking for a link such as **My domains**.</span></span>

<span data-ttu-id="8f8f7-147">Una volta trovata la pagina, cercare un collegamento che consenta di aggiungere o modificare i record DNS.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-147">Once you find this page, look for a link that lets you add or edit DNS records.</span></span> <span data-ttu-id="8f8f7-148">Potrebbe trattarsi di un collegamento a un **file di zona** o a **record DNS** oppure di un collegamento a una **configurazione avanzata**.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-148">This might be a **Zone file** or **DNS Records** link, or an **Advanced configuration** link.</span></span>

### <a name="create-a-cname-record"></a><span data-ttu-id="8f8f7-149">Creare un record CNAME</span><span class="sxs-lookup"><span data-stu-id="8f8f7-149">Create a CNAME record</span></span>

<span data-ttu-id="8f8f7-150">Aggiungere un record CNAME che associa il nome di dominio predefinito hello sottodominio desiderato nome tooyour dell'applicazione web (`<app_name>.azurewebsites.net`, dove `<app_name>` è nome univoco dell'applicazione).</span><span class="sxs-lookup"><span data-stu-id="8f8f7-150">Add a CNAME record that maps hello desired subdomain name tooyour web app's default domain name (`<app_name>.azurewebsites.net`, where `<app_name>` is your app's unique name).</span></span>

<span data-ttu-id="8f8f7-151">Per hello `www.contoso.com` esempio, si crea un record CNAME che esegue il mapping hello `www` nome host troppo`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-151">For hello `www.contoso.com` example, you create a CNAME that maps hello `www` hostname too`<app_name>.azurewebsites.net`.</span></span>

## <a name="step-3---configure-hello-custom-domain-on-your-web-app"></a><span data-ttu-id="8f8f7-152">Passaggio 3: configurare dominio personalizzato hello nell'app web</span><span class="sxs-lookup"><span data-stu-id="8f8f7-152">Step 3 - Configure hello custom domain on your web app</span></span>

<span data-ttu-id="8f8f7-153">Al termine della configurazione di mapping hostname hello nel sito Web del provider di dominio, si è pronti tooconfigure dominio personalizzato di hello nell'app web.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-153">When you finish configuring hello hostname mapping in your domain provider's website, you're ready tooconfigure hello custom domain on your web app.</span></span> <span data-ttu-id="8f8f7-154">Hello utilizzare [az appservice web configurazione hostname aggiungere](/cli/azure/appservice/web/config/hostname#add) comando tooadd questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-154">Use hello [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) command tooadd this configuration.</span></span> 

<span data-ttu-id="8f8f7-155">Nel comando hello seguente, sostituire `<app_name>` con il nome univoco dell'app e < your_custom_domain > con il nome di dominio personalizzato completo hello (ad esempio `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="8f8f7-155">In hello command below, please substitute `<app_name>` with your unique app name, and <your_custom_domain> with hello fully qualified custom domain name (e.g. `www.contoso.com`).</span></span> 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

<span data-ttu-id="8f8f7-156">dominio personalizzato Hello è ora completamente mappato tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-156">hello custom domain now is fully mapped tooyour web app.</span></span> <span data-ttu-id="8f8f7-157">Nel browser, passare il nome di dominio personalizzato toohello.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-157">In your browser, navigate toohello custom domain name.</span></span> <span data-ttu-id="8f8f7-158">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8f8f7-158">For example:</span></span>

```
http://www.contoso.com 
``` 

![App Web creata nel servizio app](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-tooyour-web-app"></a><span data-ttu-id="8f8f7-160">Passaggio 4: associare un'app web tooyour di certificati SSL personalizzata</span><span class="sxs-lookup"><span data-stu-id="8f8f7-160">Step 4 - Bind a custom SSL certificate tooyour web app</span></span>

<span data-ttu-id="8f8f7-161">È ora disponibile un'app web di Azure, con il nome di dominio hello desiderato nella barra degli indirizzi del browser hello.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-161">You now have an Azure web app, with hello domain name you want in hello browser's address bar.</span></span> <span data-ttu-id="8f8f7-162">Tuttavia, se si passa toohello `https://<your_custom_domain>` a questo punto, si verifica un errore di certificato.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-162">However, if you navigate toohello `https://<your_custom_domain>` now, you get a certificate error.</span></span> 

![App Web creata nel servizio app](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

<span data-ttu-id="8f8f7-164">Questo errore si verifica perché l'app Web non ha ancora un binding a un certificato SSL corrispondente al nome del dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-164">This error occurs because your web app doesn't yet have an SSL certificate binding that matches your custom domain name.</span></span> <span data-ttu-id="8f8f7-165">Tuttavia, non si verifica un errore se si passa troppo`https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-165">However, you don't get an error if you navigate too`https://<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="8f8f7-166">In questo modo l'app, nonché tutte le applicazioni di servizio App di Azure, è protetto con il certificato SSL hello per hello `*.azurewebsites.net` dominio con caratteri jolly per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-166">This is because your app, as well as all Azure App Service apps, is secured with hello SSL certificate for hello `*.azurewebsites.net` wildcard domain by default.</span></span> 

<span data-ttu-id="8f8f7-167">In Ordina tooaccess app web per il nome di dominio personalizzato, è necessario certificato SSL di toobind hello per le app web toohello di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-167">In order tooaccess your web app by your custom domain name, you need toobind hello SSL certificate for your custom domain toohello web app.</span></span> <span data-ttu-id="8f8f7-168">Questa operazione verrà eseguita in questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-168">You will do it in this step.</span></span> 

### <a name="upload-hello-ssl-certificate"></a><span data-ttu-id="8f8f7-169">Caricare il certificato SSL hello</span><span class="sxs-lookup"><span data-stu-id="8f8f7-169">Upload hello SSL certificate</span></span>

<span data-ttu-id="8f8f7-170">Caricare il certificato SSL hello per le app web tooyour di dominio personalizzato tramite hello [az appservice configurazione ssl caricamento](/cli/azure/appservice/web/config/ssl#upload) comando.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-170">Upload hello SSL certificate for your custom domain tooyour web app by using hello [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload) command.</span></span>

<span data-ttu-id="8f8f7-171">Nel comando hello seguente, sostituire `<app_name>` con il nome univoco di app, `<path_to_ptx_file>` con tooyour percorso hello. Il file PFX, e `<password>` con la password del certificato.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-171">In hello command below, please substitute `<app_name>` with your unique app name, `<path_to_ptx_file>` with hello path tooyour .PFX file, and `<password>` with your certificate's password.</span></span> 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

<span data-ttu-id="8f8f7-172">Quando viene caricato il certificato di hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="8f8f7-172">When hello certificate is uploaded, hello Azure CLI shows information similar toohello following example:</span></span>

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

<span data-ttu-id="8f8f7-173">Dall'output JSON, hello `thumbprint` Mostra l'identificazione personale del certificato caricato.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-173">From hello JSON output, `thumbprint` shows your uploaded certificate's thumbprint.</span></span> <span data-ttu-id="8f8f7-174">Copiare il valore per il passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-174">Copy its value for hello next step.</span></span>

### <a name="bind-hello-uploaded-ssl-certificate-toohello-web-app"></a><span data-ttu-id="8f8f7-175">Associare l'applicazione web di hello caricato SSL certificati toohello</span><span class="sxs-lookup"><span data-stu-id="8f8f7-175">Bind hello uploaded SSL certificate toohello web app</span></span>

<span data-ttu-id="8f8f7-176">L'app web ha ora il nome di dominio personalizzato hello desiderato e include anche un certificato SSL che protegge il dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-176">Your web app now has hello custom domain name you want, and it also has a SSL certificate that secures that custom domain.</span></span> <span data-ttu-id="8f8f7-177">Hello solo toodo a sinistra di cosa è toobind hello certificato caricato toohello web app.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-177">hello only thing left toodo is toobind hello uploaded certificate toohello web app.</span></span> <span data-ttu-id="8f8f7-178">Farlo tramite hello [il binding ssl az appservice web configurazione](/cli/azure/appservice/web/config/ssl#bind) comando.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-178">You do this by using hello [az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind) command.</span></span>

<span data-ttu-id="8f8f7-179">Nel comando hello seguente, sostituire `<app_name>` con il nome univoco di app e `<thumbprint-from-previous-output>` con identificazione personale del certificato hello che vengono recuperate dal comando precedente hello.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-179">In hello command below, please substitute `<app_name>` with your unique app name and `<thumbprint-from-previous-output>` with hello certificate thumbprint that you get from hello previous command.</span></span> 

<span data-ttu-id="8f8f7-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span><span class="sxs-lookup"><span data-stu-id="8f8f7-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span></span>

<span data-ttu-id="8f8f7-181">Quando hello certificato associate tooyour web app, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="8f8f7-181">When hello certificate is bound tooyour web app, hello Azure CLI shows information similar toohello following example:</span></span>

<span data-ttu-id="8f8f7-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span><span class="sxs-lookup"><span data-stu-id="8f8f7-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span></span>

<span data-ttu-id="8f8f7-183">Nel browser passare endpoint tooHTTPS del nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="8f8f7-183">In your browser, navigate tooHTTPS endpoint of your custom domain name.</span></span> <span data-ttu-id="8f8f7-184">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8f8f7-184">For example:</span></span>

```
https://www.contoso.com 
``` 

![App Web creata nel servizio app](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a><span data-ttu-id="8f8f7-186">Altre risorse</span><span class="sxs-lookup"><span data-stu-id="8f8f7-186">More resources</span></span>

<span data-ttu-id="8f8f7-187">[Acquistare e configurare un nome di dominio personalizzato in Servizio app di Azure](custom-dns-web-site-buydomains-web-app.md)
[Acquistare e configurare un certificato SSL per il servizio app di Azure](web-sites-purchase-ssl-web-site.md)</span><span class="sxs-lookup"><span data-stu-id="8f8f7-187">[Buy and Configure a custom domain name in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[Buy and Configure an SSL Certificate for your Azure App Service](web-sites-purchase-ssl-web-site.md)</span></span>
