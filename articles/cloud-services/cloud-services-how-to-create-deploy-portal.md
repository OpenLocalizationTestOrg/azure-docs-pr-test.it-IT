---
title: aaaHow toocreate e distribuire un servizio cloud | Documenti Microsoft
description: Informazioni su come toocreate e distribuire un servizio cloud con hello portale di Azure.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: dc8b81a594f3514e662c49c9a46a33da8a551f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a><span data-ttu-id="61fb4-103">Come toocreate e distribuire un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="61fb4-103">How toocreate and deploy a cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="61fb4-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="61fb4-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="61fb4-105">portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="61fb4-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
>
>

<span data-ttu-id="61fb4-106">sono disponibili due metodi per l'utente toocreate Hello portale di Azure e distribuire un servizio cloud: *creazione rapida* e *creazione personalizzata*.</span><span class="sxs-lookup"><span data-stu-id="61fb4-106">hello Azure portal provides two ways for you toocreate and deploy a cloud service: *Quick Create* and *Custom Create*.</span></span>

<span data-ttu-id="61fb4-107">Questo articolo viene illustrato come toouse hello creazione rapida metodo toocreate un nuovo servizio cloud e quindi utilizzare **caricare** tooupload e distribuire un pacchetto del servizio cloud in Azure.</span><span class="sxs-lookup"><span data-stu-id="61fb4-107">This article explains how toouse hello Quick Create method toocreate a new cloud service and then use **Upload** tooupload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="61fb4-108">Quando si utilizza questo metodo, hello portale di Azure rende disponibili utili collegamenti per il completamento di tutti i requisiti man mano.</span><span class="sxs-lookup"><span data-stu-id="61fb4-108">When you use this method, hello Azure portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="61fb4-109">Se si è pronti toodeploy durante la creazione del servizio cloud, è possibile eseguire sia hello contemporaneamente utilizzando creazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="61fb4-109">If you're ready toodeploy your cloud service when you create it, you can do both at hello same time using Custom Create.</span></span>

> [!NOTE]
> <span data-ttu-id="61fb4-110">Se si intende toopublish il servizio cloud da Visual Studio Team Services (VSTS), usare creazione rapida e quindi impostare la pubblicazione di Visual Studio Team Services dal dashboard di avvio rapido di Azure o hello hello.</span><span class="sxs-lookup"><span data-stu-id="61fb4-110">If you plan toopublish your cloud service from Visual Studio Team Services (VSTS), use Quick Create, and then set up VSTS publishing from hello Azure Quickstart or hello dashboard.</span></span> <span data-ttu-id="61fb4-111">Per ulteriori informazioni, vedere [tooAzure la distribuzione continua da utilizzando Visual Studio Team Services][TFSTutorialForCloudService], vedere la Guida per hello o **avvio rapido** pagina.</span><span class="sxs-lookup"><span data-stu-id="61fb4-111">For more information, see [Continuous Delivery tooAzure by Using Visual Studio Team Services][TFSTutorialForCloudService], or see help for hello **Quick Start** page.</span></span>
>
>

## <a name="concepts"></a><span data-ttu-id="61fb4-112">Concetti</span><span class="sxs-lookup"><span data-stu-id="61fb4-112">Concepts</span></span>
<span data-ttu-id="61fb4-113">Tre componenti sono necessari toodeploy un'applicazione come servizio cloud in Azure:</span><span class="sxs-lookup"><span data-stu-id="61fb4-113">Three components are required toodeploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="61fb4-114">**Definizione del servizio**</span><span class="sxs-lookup"><span data-stu-id="61fb4-114">**Service Definition**</span></span>  
  <span data-ttu-id="61fb4-115">file di definizione del servizio cloud Hello (con estensione csdef) definisce il modello di servizio hello, incluso il numero di hello dei ruoli.</span><span class="sxs-lookup"><span data-stu-id="61fb4-115">hello cloud service definition file (.csdef) defines hello service model, including hello number of roles.</span></span>
* <span data-ttu-id="61fb4-116">**Configurazione del servizio**</span><span class="sxs-lookup"><span data-stu-id="61fb4-116">**Service Configuration**</span></span>  
  <span data-ttu-id="61fb4-117">file di configurazione del servizio cloud Hello (. cscfg) fornisce le impostazioni di configurazione per servizio cloud hello e singoli ruoli, tra cui hello numero di istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="61fb4-117">hello cloud service configuration file (.cscfg) provides configuration settings for hello cloud service and individual roles, including hello number of role instances.</span></span>
* <span data-ttu-id="61fb4-118">**Pacchetto del servizio**</span><span class="sxs-lookup"><span data-stu-id="61fb4-118">**Service Package**</span></span>  
  <span data-ttu-id="61fb4-119">pacchetto del servizio Hello (con estensione cspkg) contiene il codice dell'applicazione hello e le configurazioni e file di definizione del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="61fb4-119">hello service package (.cspkg) contains hello application code and configurations and hello service definition file.</span></span>

<span data-ttu-id="61fb4-120">Sono disponibili ulteriori informazioni su questi e in che modo un pacchetto toocreate [qui](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="61fb4-120">You can learn more about these and how toocreate a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="61fb4-121">Preparare l'app</span><span class="sxs-lookup"><span data-stu-id="61fb4-121">Prepare your app</span></span>
<span data-ttu-id="61fb4-122">Prima di poter distribuire un servizio cloud, è necessario creare pacchetto del servizio cloud hello (con estensione cspkg) dal codice dell'applicazione e un file di configurazione del servizio cloud (. cscfg).</span><span class="sxs-lookup"><span data-stu-id="61fb4-122">Before you can deploy a cloud service, you must create hello cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="61fb4-123">Hello Azure SDK sono disponibili strumenti per la preparazione di questi file di distribuzione necessarie.</span><span class="sxs-lookup"><span data-stu-id="61fb4-123">hello Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="61fb4-124">È possibile installare SDK hello hello [download di Azure](https://azure.microsoft.com/downloads/) pagina, nella lingua hello in cui si preferisce toodevelop il codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="61fb4-124">You can install hello SDK from hello [Azure Downloads](https://azure.microsoft.com/downloads/) page, in hello language in which you prefer toodevelop your application code.</span></span>

<span data-ttu-id="61fb4-125">Per poter esportare un pacchetto di servizio, è necessario configurare tre funzionalità del servizio cloud:</span><span class="sxs-lookup"><span data-stu-id="61fb4-125">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="61fb4-126">Se si desidera che un servizio cloud che utilizza Secure Sockets Layer (SSL) per la crittografia dei dati, toodeploy [configurare l'applicazione](cloud-services-configure-ssl-certificate-portal.md#modify) per SSL.</span><span class="sxs-lookup"><span data-stu-id="61fb4-126">If you want toodeploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate-portal.md#modify) for SSL.</span></span>
* <span data-ttu-id="61fb4-127">Se si desidera tooconfigure istanze di toorole connessioni Desktop remoto, [configurare ruoli hello](cloud-services-role-enable-remote-desktop-new-portal.md) per Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="61fb4-127">If you want tooconfigure Remote Desktop connections toorole instances, [configure hello roles](cloud-services-role-enable-remote-desktop-new-portal.md) for Remote Desktop.</span></span>
* <span data-ttu-id="61fb4-128">Se si desidera tooconfigure dettagliato di monitoraggio per il servizio cloud, abilitare la diagnostica di Azure per il servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="61fb4-128">If you want tooconfigure verbose monitoring for your cloud service, enable Azure Diagnostics for hello cloud service.</span></span> <span data-ttu-id="61fb4-129">*Monitoraggio minimo* (impostazione predefinita hello monitoraggio livello) usa i contatori delle prestazioni raccolti dai sistemi operativi host di hello per le istanze del ruolo (macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="61fb4-129">*Minimal monitoring* (hello default monitoring level) uses performance counters gathered from hello host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="61fb4-130">*Monitoraggio dettagliato* raccoglie le metriche aggiuntive basate sui dati delle prestazioni all'interno di hello ruolo istanze tooenable analisi ravvicinata dei problemi che si verificano durante l'elaborazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="61fb4-130">*Verbose monitoring* gathers additional metrics based on performance data within hello role instances tooenable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="61fb4-131">toofind come tooenable diagnostica di Azure, vedere [abilitazione di diagnostica Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="61fb4-131">toofind out how tooenable Azure Diagnostics, see [Enabling diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="61fb4-132">toocreate un servizio cloud con distribuzioni di ruoli web o ruoli di lavoro, è necessario [Crea pacchetto del servizio hello](cloud-services-model-and-package.md#servicepackagecspkg).</span><span class="sxs-lookup"><span data-stu-id="61fb4-132">toocreate a cloud service with deployments of web roles or worker roles, you must [create hello service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="61fb4-133">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="61fb4-133">Before you begin</span></span>
* <span data-ttu-id="61fb4-134">Se non è stato installato hello Azure SDK, fare clic su **installare Azure SDK** tooopen hello [pagina di download di Azure](https://azure.microsoft.com/downloads/)e quindi scaricare hello SDK per la lingua di hello in cui si preferisce toodevelop il codice.</span><span class="sxs-lookup"><span data-stu-id="61fb4-134">If you haven't installed hello Azure SDK, click **Install Azure SDK** tooopen hello [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download hello SDK for hello language in which you prefer toodevelop your code.</span></span> <span data-ttu-id="61fb4-135">(Sarà necessario questo toodo un'opportunità in un secondo momento.)</span><span class="sxs-lookup"><span data-stu-id="61fb4-135">(You'll have an opportunity toodo this later.)</span></span>
* <span data-ttu-id="61fb4-136">Se tutte le istanze di ruolo richiedono un certificato, è possibile creare certificati hello.</span><span class="sxs-lookup"><span data-stu-id="61fb4-136">If any role instances require a certificate, create hello certificates.</span></span> <span data-ttu-id="61fb4-137">I servizi cloud richiedono un file con estensione pfx con una chiave privata.</span><span class="sxs-lookup"><span data-stu-id="61fb4-137">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="61fb4-138">È possibile caricare hello certificati tooAzure come creare e distribuire il servizio di cloud hello.</span><span class="sxs-lookup"><span data-stu-id="61fb4-138">You can upload hello certificates tooAzure as you create and deploy hello cloud service.</span></span>

## <a name="create-and-deploy"></a><span data-ttu-id="61fb4-139">Creazione e distribuzione</span><span class="sxs-lookup"><span data-stu-id="61fb4-139">Create and deploy</span></span>
1. <span data-ttu-id="61fb4-140">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="61fb4-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="61fb4-141">Fare clic su **nuovo > calcolo**e quindi scorrere verso il basso fare clic su tooand **servizio Cloud**.</span><span class="sxs-lookup"><span data-stu-id="61fb4-141">Click **New > Compute**, and then scroll down tooand click **Cloud Service**.</span></span>

    ![Pubblicare il servizio cloud](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. <span data-ttu-id="61fb4-143">Nella nuova hello **servizio Cloud** pannello, immettere un valore per hello **nome DNS**.</span><span class="sxs-lookup"><span data-stu-id="61fb4-143">In hello new **Cloud Service** blade, enter a value for hello **DNS name**.</span></span>
4. <span data-ttu-id="61fb4-144">Creare un nuovo **Gruppo di risorse** o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="61fb4-144">Create a new **Resource Group** or select an existing one.</span></span>
5. <span data-ttu-id="61fb4-145">Selezionare un **percorso**.</span><span class="sxs-lookup"><span data-stu-id="61fb4-145">Select a **Location**.</span></span>
6. <span data-ttu-id="61fb4-146">Fare clic su **Pacchetto**.</span><span class="sxs-lookup"><span data-stu-id="61fb4-146">Click **Package**.</span></span> <span data-ttu-id="61fb4-147">Verrà aperta hello **caricare un pacchetto** blade.</span><span class="sxs-lookup"><span data-stu-id="61fb4-147">This will open hello **Upload a package** blade.</span></span> <span data-ttu-id="61fb4-148">Compilare i campi necessario hello.</span><span class="sxs-lookup"><span data-stu-id="61fb4-148">Fill in hello required fields.</span></span> <span data-ttu-id="61fb4-149">Se sono presenti ruoli contenenti una singola istanza, assicurarsi che l'opzione **Distribuisci anche se uno o più ruoli contengono una singola istanza** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="61fb4-149">If any of your roles contain a single instance, ensure **Deploy even if one or more roles contain a single instance** is selected.</span></span>
7. <span data-ttu-id="61fb4-150">Assicurarsi che l'opzione **Avvia distribuzione** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="61fb4-150">Make sure that **Start deployment** is selected.</span></span>
8. <span data-ttu-id="61fb4-151">Fare clic su **OK** verranno chiusi hello **caricare un pacchetto** blade.</span><span class="sxs-lookup"><span data-stu-id="61fb4-151">Click **OK** which will close hello **Upload a package** blade.</span></span>
9. <span data-ttu-id="61fb4-152">Se non si dispone di qualsiasi tooadd certificati, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="61fb4-152">If you do not have any certificates tooadd, click **Create**.</span></span>

    ![Pubblicare il servizio cloud](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a><span data-ttu-id="61fb4-154">Caricamento di un certificato</span><span class="sxs-lookup"><span data-stu-id="61fb4-154">Upload a certificate</span></span>
<span data-ttu-id="61fb4-155">Se il pacchetto di distribuzione è stata [configurato i certificati toouse](cloud-services-configure-ssl-certificate-portal.md#modify), è possibile caricare il certificato di hello ora.</span><span class="sxs-lookup"><span data-stu-id="61fb4-155">If your deployment package was [configured toouse certificates](cloud-services-configure-ssl-certificate-portal.md#modify), you can upload hello certificate now.</span></span>

1. <span data-ttu-id="61fb4-156">Selezionare **certificati**e in hello **aggiungere certificati** pannello selezionare file pfx del certificato SSL hello e quindi fornire hello **Password** certificato hello,</span><span class="sxs-lookup"><span data-stu-id="61fb4-156">Select **Certificates**, and on hello **Add certificates** blade, select hello SSL certificate .pfx file, and then provide hello **Password** for hello certificate,</span></span>
2. <span data-ttu-id="61fb4-157">Fare clic su **certificato Connetti**, quindi fare clic su **OK** su hello **aggiungere certificati** blade.</span><span class="sxs-lookup"><span data-stu-id="61fb4-157">Click **Attach certificate**, and then click **OK** on hello **Add certificates** blade.</span></span>
3. <span data-ttu-id="61fb4-158">Fare clic su **crea** su hello **servizio Cloud** blade.</span><span class="sxs-lookup"><span data-stu-id="61fb4-158">Click **Create** on hello **Cloud Service** blade.</span></span> <span data-ttu-id="61fb4-159">Quando la distribuzione di hello ha raggiunto hello **pronto** stato, è possibile procedere toohello passaggi.</span><span class="sxs-lookup"><span data-stu-id="61fb4-159">When hello deployment has reached hello **Ready** status, you can proceed toohello next steps.</span></span>

    ![Pubblicare il servizio cloud](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="61fb4-161">Verificare che la distribuzione sia stata completata correttamente</span><span class="sxs-lookup"><span data-stu-id="61fb4-161">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="61fb4-162">Scegliere l'istanza del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="61fb4-162">Click hello cloud service instance.</span></span>

    <span data-ttu-id="61fb4-163">Hello stato risulterà che servizio hello è **esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="61fb4-163">hello status should show that hello service is **Running**.</span></span>
2. <span data-ttu-id="61fb4-164">In **Essentials**, fare clic su hello **URL del sito** tooopen del servizio cloud in un web browser.</span><span class="sxs-lookup"><span data-stu-id="61fb4-164">Under **Essentials**, click hello **Site URL** tooopen your cloud service in a web browser.</span></span>

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a><span data-ttu-id="61fb4-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="61fb4-166">Next steps</span></span>
* <span data-ttu-id="61fb4-167">[Configurazione generale del servizio cloud](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="61fb4-167">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="61fb4-168">Configurare un [nome di dominio personalizzato](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="61fb4-168">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="61fb4-169">[Gestire il servizio cloud](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="61fb4-169">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="61fb4-170">Configurare i [certificati ssl](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="61fb4-170">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
