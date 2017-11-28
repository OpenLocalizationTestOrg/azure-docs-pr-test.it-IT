---
title: Aggiungere un dominio personalizzato e un certificato SSL a un'app Web di Azure | Microsoft Docs
description: "Informazioni su come preparare l'app Web di Azure per l'ambiente di produzione aggiungendo il marchio della società. Eseguire il mapping del nome di dominio personalizzato (dominio personale) all'app Web e proteggerlo con un certificato SSL personalizzato."
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
ms.openlocfilehash: c9d00f678b6257a8aafb35acd2d5a2292703a2dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="add-custom-domain-and-ssl-to-an-azure-web-app"></a><span data-ttu-id="d2b84-104">Aggiungere un dominio personalizzato e un certificato SSL a un'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="d2b84-104">Add custom domain and SSL to an Azure web app</span></span>

<span data-ttu-id="d2b84-105">Questa esercitazione illustra come eseguire rapidamente il mapping di un nome di dominio personalizzato all'app Web di Azure e quindi garantirne la sicurezza con un certificato SSL personalizzato.</span><span class="sxs-lookup"><span data-stu-id="d2b84-105">This tutorial shows you how to quickly map a custom domain name to your Azure web app and then secure it with a custom SSL certificate.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="d2b84-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="d2b84-106">Before you begin</span></span>

<span data-ttu-id="d2b84-107">Prima di eseguire l'esempio, installare l'[interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) in locale.</span><span class="sxs-lookup"><span data-stu-id="d2b84-107">Before running this sample, install the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) locally.</span></span>

<span data-ttu-id="d2b84-108">È anche necessario l'accesso amministrativo alla pagina di configurazione DNS per il provider di dominio pertinente.</span><span class="sxs-lookup"><span data-stu-id="d2b84-108">You also need administrative access to the DNS configuration page for your respective domain provider.</span></span> <span data-ttu-id="d2b84-109">Per aggiungere, ad esempio, `www.contoso.com`, è necessario essere in grado di configurare voci DNS per `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="d2b84-109">For example, to add `www.contoso.com`, you need to be able to configure DNS entries for `contoso.com`.</span></span>

<span data-ttu-id="d2b84-110">Infine, sono necessari un file PFX valido _e_ la relativa password per il certificato SSL da caricare e di cui eseguire il binding.</span><span class="sxs-lookup"><span data-stu-id="d2b84-110">Lastly, you need a valid .PFX file _and_ its password for the SSL certificate you want to upload and bind.</span></span> <span data-ttu-id="d2b84-111">Il certificato SSL deve essere configurato per proteggere il nome di dominio personalizzato desiderato.</span><span class="sxs-lookup"><span data-stu-id="d2b84-111">This SSL certificate should be configured to secure the custom domain name you want.</span></span> <span data-ttu-id="d2b84-112">Nell'esempio precedente il certificato SSL deve proteggere `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="d2b84-112">In the above example, your SSL certificate should secure `www.contoso.com`.</span></span> 

## <a name="step-1---create-an-azure-web-app"></a><span data-ttu-id="d2b84-113">Passaggio 1 - Creare un'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="d2b84-113">Step 1 - Create an Azure web app</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="d2b84-114">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="d2b84-114">Log in to Azure</span></span>

<span data-ttu-id="d2b84-115">Verrà ora usata l'interfaccia della riga di comando di Azure 2.0 in una finestra del terminale per creare le risorse necessarie per ospitare l'app Node.js in Azure.</span><span class="sxs-lookup"><span data-stu-id="d2b84-115">We are now going to use the Azure CLI 2.0 in a terminal window to create the resources needed to host our Node.js app in Azure.</span></span>  <span data-ttu-id="d2b84-116">Accedere alla sottoscrizione di Azure con il comando [az login](/cli/azure/#login) e seguire le istruzioni visualizzate.</span><span class="sxs-lookup"><span data-stu-id="d2b84-116">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="d2b84-117">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="d2b84-117">Create a resource group</span></span>   
<span data-ttu-id="d2b84-118">Creare un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d2b84-118">Create a resource group with the [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="d2b84-119">Un gruppo di risorse di Azure è un contenitore logico in cui vengono distribuite e gestite risorse di Azure come app Web, database e account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d2b84-119">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

<span data-ttu-id="d2b84-120">Per visualizzare i possibili valori utilizzabili per `---location`, usare il comando `az appservice list-locations` dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="d2b84-120">To see what possible values you can use for `---location`, use the `az appservice list-locations` Azure CLI command.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="d2b84-121">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="d2b84-121">Create an App Service plan</span></span>

<span data-ttu-id="d2b84-122">Creare un piano di servizio app con il comando [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="d2b84-122">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="d2b84-123">L'esempio seguente crea un piano di servizio app denominato `myAppServicePlan` usando il piano tariffario **Basic**.</span><span class="sxs-lookup"><span data-stu-id="d2b84-123">The following example creates an App Service plan named `myAppServicePlan` using the **Basic** pricing tier.</span></span>

<span data-ttu-id="d2b84-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span><span class="sxs-lookup"><span data-stu-id="d2b84-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span></span>

<span data-ttu-id="d2b84-125">Dopo aver creato il piano di servizio app, l'interfaccia della riga di comando di Azure mostra informazioni simili a quelle dell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="d2b84-125">When the App Service plan has been created, the Azure CLI shows information similar to the following example.</span></span> 

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

## <a name="create-a-web-app"></a><span data-ttu-id="d2b84-126">Creare un'app Web</span><span class="sxs-lookup"><span data-stu-id="d2b84-126">Create a web app</span></span>

<span data-ttu-id="d2b84-127">Ora che il piano di servizio app è stato creato, creare un'app Web nel piano `myAppServicePlan`.</span><span class="sxs-lookup"><span data-stu-id="d2b84-127">Now that an App Service plan has been created, create a web app within the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="d2b84-128">L'app Web fornisce uno spazio di hosting per la distribuzione del codice e un URL per visualizzare l'applicazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="d2b84-128">The web app gives your a hosting space to deploy your code as well as provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="d2b84-129">Usare il comando [az appservice web create](/cli/azure/appservice/web#create) per creare l'app Web.</span><span class="sxs-lookup"><span data-stu-id="d2b84-129">Use the [az appservice web create](/cli/azure/appservice/web#create) command to create the web app.</span></span> 

<span data-ttu-id="d2b84-130">Nel comando seguente sostituire il segnaposto `<app_name>` con il nome univoco della propria app.</span><span class="sxs-lookup"><span data-stu-id="d2b84-130">In the command below, please substitute your own unique app name where you see the `<app_name>` placeholder.</span></span> <span data-ttu-id="d2b84-131">Questo nome univoco verrà usato come parte del nome di dominio predefinito per l'app Web, quindi è necessario che il nome sia univoco in tutte le app in Azure.</span><span class="sxs-lookup"><span data-stu-id="d2b84-131">This unique name will be used as the part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="d2b84-132">In un secondo momento è possibile eseguire il mapping di qualsiasi voce DNS personalizzata all'app Web prima di esporla agli utenti.</span><span class="sxs-lookup"><span data-stu-id="d2b84-132">You can later map any custom DNS entry to the web app before you expose it to your users.</span></span> 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

<span data-ttu-id="d2b84-133">Dopo aver creato l'app Web, l'interfaccia della riga di comando di Azure mostra informazioni simili a quelle dell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="d2b84-133">When the web app has been created, the Azure CLI shows information similar to the following example.</span></span> 

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

<span data-ttu-id="d2b84-134">Nell'output JSON `defaultHostName` indica il nome di dominio predefinito dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="d2b84-134">From the JSON output, `defaultHostName` shows your web app's default domain name.</span></span> <span data-ttu-id="d2b84-135">Nel browser passare a questo indirizzo.</span><span class="sxs-lookup"><span data-stu-id="d2b84-135">In your browser, navigate to this address.</span></span>

```
http://<app_name>.azurewebsites.net 
``` 
 
![App Web creata nel servizio app](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a><span data-ttu-id="d2b84-137">Passaggio 2 - Configurare il mapping DNS</span><span class="sxs-lookup"><span data-stu-id="d2b84-137">Step 2 - Configure DNS mapping</span></span>

<span data-ttu-id="d2b84-138">In questo passaggio si aggiunge un mapping da un dominio personalizzato al nome di dominio predefinito dell'app Web, `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="d2b84-138">In this step, you add a mapping from a custom domain to your web app's default domain name, `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="d2b84-139">In genere si esegue questo passaggio nel sito Web del provider del dominio.</span><span class="sxs-lookup"><span data-stu-id="d2b84-139">Typically, you perform this step in your domain provider's website.</span></span> <span data-ttu-id="d2b84-140">Il sito Web di ogni registrar di dominio è leggermente diverso, quindi è consigliabile vedere la documentazione del provider.</span><span class="sxs-lookup"><span data-stu-id="d2b84-140">Every domain registrar's website is slightly different, so you should consult your provider's documentation.</span></span> <span data-ttu-id="d2b84-141">Di seguito sono tuttavia indicate alcune linee guida generali.</span><span class="sxs-lookup"><span data-stu-id="d2b84-141">However, here are some general guidelines.</span></span> 

### <a name="navigate-to-to-dns-management-page"></a><span data-ttu-id="d2b84-142">Passare alla pagina di gestione DNS</span><span class="sxs-lookup"><span data-stu-id="d2b84-142">Navigate to to DNS management page</span></span>

<span data-ttu-id="d2b84-143">Accedere prima di tutto al sito Web del registrar del dominio.</span><span class="sxs-lookup"><span data-stu-id="d2b84-143">First, log in to your domain registrar's website.</span></span>  

<span data-ttu-id="d2b84-144">Individuare quindi la pagina relativa alla gestione dei record DNS.</span><span class="sxs-lookup"><span data-stu-id="d2b84-144">Then, find the page for managing DNS records.</span></span> <span data-ttu-id="d2b84-145">Individuare collegamenti o aree del sito denominate **Domain Name**, **DNS** o **Name Server Management**.</span><span class="sxs-lookup"><span data-stu-id="d2b84-145">Look for links or areas of the site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="d2b84-146">Spesso è possibile trovare il collegamento visualizzando le informazioni dell'account, cercando una voce simile a **Domini personali**.</span><span class="sxs-lookup"><span data-stu-id="d2b84-146">Often, you can find the link by viewing your account information, and then looking for a link such as **My domains**.</span></span>

<span data-ttu-id="d2b84-147">Una volta trovata la pagina, cercare un collegamento che consenta di aggiungere o modificare i record DNS.</span><span class="sxs-lookup"><span data-stu-id="d2b84-147">Once you find this page, look for a link that lets you add or edit DNS records.</span></span> <span data-ttu-id="d2b84-148">Potrebbe trattarsi di un collegamento a un **file di zona** o a **record DNS** oppure di un collegamento a una **configurazione avanzata**.</span><span class="sxs-lookup"><span data-stu-id="d2b84-148">This might be a **Zone file** or **DNS Records** link, or an **Advanced configuration** link.</span></span>

### <a name="create-a-cname-record"></a><span data-ttu-id="d2b84-149">Creare un record CNAME</span><span class="sxs-lookup"><span data-stu-id="d2b84-149">Create a CNAME record</span></span>

<span data-ttu-id="d2b84-150">Aggiungere un record CNAME che esegue il mapping del nome di sottodominio desiderato al nome di dominio predefinito dell'app Web (`<app_name>.azurewebsites.net`, dove `<app_name>` è il nome univoco dell'app).</span><span class="sxs-lookup"><span data-stu-id="d2b84-150">Add a CNAME record that maps the desired subdomain name to your web app's default domain name (`<app_name>.azurewebsites.net`, where `<app_name>` is your app's unique name).</span></span>

<span data-ttu-id="d2b84-151">Per l'esempio relativo a `www.contoso.com`, si crea un record CNAME che esegue il mapping del nome host `www` a `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="d2b84-151">For the `www.contoso.com` example, you create a CNAME that maps the `www` hostname to `<app_name>.azurewebsites.net`.</span></span>

## <a name="step-3---configure-the-custom-domain-on-your-web-app"></a><span data-ttu-id="d2b84-152">Passaggio 3 - Configurare il dominio personalizzato nell'app Web</span><span class="sxs-lookup"><span data-stu-id="d2b84-152">Step 3 - Configure the custom domain on your web app</span></span>

<span data-ttu-id="d2b84-153">Dopo aver configurato il mapping del nome host nel sito Web del provider di dominio, si è pronti per configurare il dominio personalizzato nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="d2b84-153">When you finish configuring the hostname mapping in your domain provider's website, you're ready to configure the custom domain on your web app.</span></span> <span data-ttu-id="d2b84-154">Usare il comando [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) per aggiungere questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="d2b84-154">Use the [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) command to add this configuration.</span></span> 

<span data-ttu-id="d2b84-155">Nel comando seguente sostituire `<app_name>` con il nome univoco dell'app e <your_custom_domain> con il nome di dominio personalizzato completo (ad esempio `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="d2b84-155">In the command below, please substitute `<app_name>` with your unique app name, and <your_custom_domain> with the fully qualified custom domain name (e.g. `www.contoso.com`).</span></span> 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

<span data-ttu-id="d2b84-156">Il dominio personalizzato è ora completamente mappato all'app Web.</span><span class="sxs-lookup"><span data-stu-id="d2b84-156">The custom domain now is fully mapped to your web app.</span></span> <span data-ttu-id="d2b84-157">Nel browser passare al nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="d2b84-157">In your browser, navigate to the custom domain name.</span></span> <span data-ttu-id="d2b84-158">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d2b84-158">For example:</span></span>

```
http://www.contoso.com 
``` 

![App Web creata nel servizio app](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-to-your-web-app"></a><span data-ttu-id="d2b84-160">Passaggio 4 - Eseguire il binding di un certificato SSL personalizzato all'app Web</span><span class="sxs-lookup"><span data-stu-id="d2b84-160">Step 4 - Bind a custom SSL certificate to your web app</span></span>

<span data-ttu-id="d2b84-161">A questo punto si ha un'app web di Azure con il nome di dominio desiderato nella barra degli indirizzi del browser.</span><span class="sxs-lookup"><span data-stu-id="d2b84-161">You now have an Azure web app, with the domain name you want in the browser's address bar.</span></span> <span data-ttu-id="d2b84-162">Se tuttavia si passa a `https://<your_custom_domain>`, si verifica un errore di certificato.</span><span class="sxs-lookup"><span data-stu-id="d2b84-162">However, if you navigate to the `https://<your_custom_domain>` now, you get a certificate error.</span></span> 

![App Web creata nel servizio app](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

<span data-ttu-id="d2b84-164">Questo errore si verifica perché l'app Web non ha ancora un binding a un certificato SSL corrispondente al nome del dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="d2b84-164">This error occurs because your web app doesn't yet have an SSL certificate binding that matches your custom domain name.</span></span> <span data-ttu-id="d2b84-165">Non viene invece generato un errore se si passa a `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="d2b84-165">However, you don't get an error if you navigate to `https://<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="d2b84-166">Questo accade perché l'app, come tutte le app di Servizio app di Azure, è protetta con il certificato SSL per il dominio con caratteri jolly `*.azurewebsites.net` per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d2b84-166">This is because your app, as well as all Azure App Service apps, is secured with the SSL certificate for the `*.azurewebsites.net` wildcard domain by default.</span></span> 

<span data-ttu-id="d2b84-167">Per accedere all'app Web dal nome di dominio personalizzato, è necessario eseguire il binding del certificato SSL per il dominio personalizzato all'app Web.</span><span class="sxs-lookup"><span data-stu-id="d2b84-167">In order to access your web app by your custom domain name, you need to bind the SSL certificate for your custom domain to the web app.</span></span> <span data-ttu-id="d2b84-168">Questa operazione verrà eseguita in questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="d2b84-168">You will do it in this step.</span></span> 

### <a name="upload-the-ssl-certificate"></a><span data-ttu-id="d2b84-169">Caricare il certificato SSL</span><span class="sxs-lookup"><span data-stu-id="d2b84-169">Upload the SSL certificate</span></span>

<span data-ttu-id="d2b84-170">Caricare il certificato SSL per il dominio personalizzato nell'app Web usando il comando [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload).</span><span class="sxs-lookup"><span data-stu-id="d2b84-170">Upload the SSL certificate for your custom domain to your web app by using the [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload) command.</span></span>

<span data-ttu-id="d2b84-171">Nel comando seguente sostituire `<app_name>` con il nome univoco dell'app, `<path_to_ptx_file>` con il percorso del file PFX e `<password>` con la password del certificato.</span><span class="sxs-lookup"><span data-stu-id="d2b84-171">In the command below, please substitute `<app_name>` with your unique app name, `<path_to_ptx_file>` with the path to your .PFX file, and `<password>` with your certificate's password.</span></span> 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

<span data-ttu-id="d2b84-172">Dopo aver caricato il certificato, l'interfaccia della riga di comando di Azure mostra informazioni simili a quelle dell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d2b84-172">When the certificate is uploaded, the Azure CLI shows information similar to the following example:</span></span>

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

<span data-ttu-id="d2b84-173">Nell'output JSON `thumbprint` indica l'identificazione personale del certificato caricato.</span><span class="sxs-lookup"><span data-stu-id="d2b84-173">From the JSON output, `thumbprint` shows your uploaded certificate's thumbprint.</span></span> <span data-ttu-id="d2b84-174">Copiare il valore per il passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="d2b84-174">Copy its value for the next step.</span></span>

### <a name="bind-the-uploaded-ssl-certificate-to-the-web-app"></a><span data-ttu-id="d2b84-175">Eseguire il binding del certificato SSL caricato all'app Web</span><span class="sxs-lookup"><span data-stu-id="d2b84-175">Bind the uploaded SSL certificate to the web app</span></span>

<span data-ttu-id="d2b84-176">L'app web ha ora il nome di dominio personalizzato desiderato, oltre che un certificato SSL che protegge il dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="d2b84-176">Your web app now has the custom domain name you want, and it also has a SSL certificate that secures that custom domain.</span></span> <span data-ttu-id="d2b84-177">L'unica operazione che rimane da fare è eseguire il binding del certificato caricato all'app Web.</span><span class="sxs-lookup"><span data-stu-id="d2b84-177">The only thing left to do is to bind the uploaded certificate to the web app.</span></span> <span data-ttu-id="d2b84-178">A tale scopo, usare il comando[az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind).</span><span class="sxs-lookup"><span data-stu-id="d2b84-178">You do this by using the [az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind) command.</span></span>

<span data-ttu-id="d2b84-179">Nel comando seguente sostituire `<app_name>` con il nome univoco dell'app e `<thumbprint-from-previous-output>` con l'identificazione personale del certificato ottenuta dal comando precedente.</span><span class="sxs-lookup"><span data-stu-id="d2b84-179">In the command below, please substitute `<app_name>` with your unique app name and `<thumbprint-from-previous-output>` with the certificate thumbprint that you get from the previous command.</span></span> 

<span data-ttu-id="d2b84-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span><span class="sxs-lookup"><span data-stu-id="d2b84-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span></span>

<span data-ttu-id="d2b84-181">Dopo aver eseguito il binding del certificato all'app Web, l'interfaccia della riga di comando di Azure mostra informazioni simili a quelle dell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d2b84-181">When the certificate is bound to your web app, the Azure CLI shows information similar to the following example:</span></span>

<span data-ttu-id="d2b84-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span><span class="sxs-lookup"><span data-stu-id="d2b84-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span></span>

<span data-ttu-id="d2b84-183">Nel browser passare all'endpoint HTTPS del nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="d2b84-183">In your browser, navigate to HTTPS endpoint of your custom domain name.</span></span> <span data-ttu-id="d2b84-184">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d2b84-184">For example:</span></span>

```
https://www.contoso.com 
``` 

![App Web creata nel servizio app](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a><span data-ttu-id="d2b84-186">Altre risorse</span><span class="sxs-lookup"><span data-stu-id="d2b84-186">More resources</span></span>

<span data-ttu-id="d2b84-187">[Acquistare e configurare un nome di dominio personalizzato in Servizio app di Azure](custom-dns-web-site-buydomains-web-app.md)
[Acquistare e configurare un certificato SSL per il servizio app di Azure](web-sites-purchase-ssl-web-site.md)</span><span class="sxs-lookup"><span data-stu-id="d2b84-187">[Buy and Configure a custom domain name in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[Buy and Configure an SSL Certificate for your Azure App Service](web-sites-purchase-ssl-web-site.md)</span></span>
