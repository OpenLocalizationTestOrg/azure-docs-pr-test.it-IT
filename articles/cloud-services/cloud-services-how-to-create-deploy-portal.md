---
title: Come creare e distribuire un servizio Cloud | Documentazione Microsoft
description: Informazioni su come creare e distribuire un servizio cloud mediante il portale di Azure.
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
ms.openlocfilehash: e5ce666f1d826c7901c9fd5e7fafe6171139c3ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-deploy-a-cloud-service"></a><span data-ttu-id="4a160-103">Come creare e distribuire un servizio Cloud</span><span class="sxs-lookup"><span data-stu-id="4a160-103">How to create and deploy a cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4a160-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4a160-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="4a160-105">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="4a160-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
>
>

<span data-ttu-id="4a160-106">Nel portale di Azure sono disponibili due modi per creare e distribuire un servizio cloud: *Creazione rapida* e *Creazione personalizzata*.</span><span class="sxs-lookup"><span data-stu-id="4a160-106">The Azure portal provides two ways for you to create and deploy a cloud service: *Quick Create* and *Custom Create*.</span></span>

<span data-ttu-id="4a160-107">In questo argomento viene descritto come usare il metodo di creazione rapida di un nuovo servizio cloud e come caricare e distribuire un pacchetto del servizio cloud in Azure tramite l'opzione **Carica** .</span><span class="sxs-lookup"><span data-stu-id="4a160-107">This article explains how to use the Quick Create method to create a new cloud service and then use **Upload** to upload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="4a160-108">Quando si usa questo metodo, il portale di Azure rende disponibili comodi collegamenti per completare tutti i requisiti man mano che si procede.</span><span class="sxs-lookup"><span data-stu-id="4a160-108">When you use this method, the Azure portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="4a160-109">Se si è pronti per distribuire il servizio cloud durante la creazione, è possibile effettuare contemporaneamente entrambe le operazioni usando Creazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="4a160-109">If you're ready to deploy your cloud service when you create it, you can do both at the same time using Custom Create.</span></span>

> [!NOTE]
> <span data-ttu-id="4a160-110">Se si prevede di pubblicare il servizio cloud da Visual Studio Team Services (VSTS), usare Creazione rapida, quindi configurare la pubblicazione VSTS da Azure Quickstart o dal dashboard.</span><span class="sxs-lookup"><span data-stu-id="4a160-110">If you plan to publish your cloud service from Visual Studio Team Services (VSTS), use Quick Create, and then set up VSTS publishing from the Azure Quickstart or the dashboard.</span></span> <span data-ttu-id="4a160-111">Per altre informazioni, vedere [Recapito continuo in Azure tramite Visual Studio Team Services][TFSTutorialForCloudService] o la guida alla pagina **Avvio rapido**.</span><span class="sxs-lookup"><span data-stu-id="4a160-111">For more information, see [Continuous Delivery to Azure by Using Visual Studio Team Services][TFSTutorialForCloudService], or see help for the **Quick Start** page.</span></span>
>
>

## <a name="concepts"></a><span data-ttu-id="4a160-112">Concetti</span><span class="sxs-lookup"><span data-stu-id="4a160-112">Concepts</span></span>
<span data-ttu-id="4a160-113">Per distribuire un'applicazione come servizio cloud in Azure, sono necessari tre componenti:</span><span class="sxs-lookup"><span data-stu-id="4a160-113">Three components are required to deploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="4a160-114">**Definizione del servizio**</span><span class="sxs-lookup"><span data-stu-id="4a160-114">**Service Definition**</span></span>  
  <span data-ttu-id="4a160-115">Il file di definizione del servizio cloud (con estensione csdef) definisce il modello di servizio, compreso il numero di ruoli.</span><span class="sxs-lookup"><span data-stu-id="4a160-115">The cloud service definition file (.csdef) defines the service model, including the number of roles.</span></span>
* <span data-ttu-id="4a160-116">**Configurazione del servizio**</span><span class="sxs-lookup"><span data-stu-id="4a160-116">**Service Configuration**</span></span>  
  <span data-ttu-id="4a160-117">l file di configurazione del servizio cloud (con estensione cscfg) specifica le impostazioni di configurazione per il servizio cloud e i singoli ruoli, incluso il numero di istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="4a160-117">The cloud service configuration file (.cscfg) provides configuration settings for the cloud service and individual roles, including the number of role instances.</span></span>
* <span data-ttu-id="4a160-118">**Pacchetto del servizio**</span><span class="sxs-lookup"><span data-stu-id="4a160-118">**Service Package**</span></span>  
  <span data-ttu-id="4a160-119">Il pacchetto del servizio (con estensione cspkg) contiene il codice dell'applicazione, le configurazioni e il file di definizione del servizio.</span><span class="sxs-lookup"><span data-stu-id="4a160-119">The service package (.cspkg) contains the application code and configurations and the service definition file.</span></span>

<span data-ttu-id="4a160-120">Per altre informazioni in proposito e su come creare un pacchetto, fare clic [qui](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="4a160-120">You can learn more about these and how to create a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="4a160-121">Preparare l'app</span><span class="sxs-lookup"><span data-stu-id="4a160-121">Prepare your app</span></span>
<span data-ttu-id="4a160-122">Per poter distribuire un servizio cloud, è necessario creare il pacchetto di servizio cloud (.cspkg) dal codice dell'applicazione e un file di configurazione del servizio cloud (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="4a160-122">Before you can deploy a cloud service, you must create the cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="4a160-123">Azure SDK offre strumenti per la preparazione dei file necessari alla distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4a160-123">The Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="4a160-124">È possibile installare l'SDK dalla pagina di [download](https://azure.microsoft.com/downloads/) di Azure, nel linguaggio in cui si preferisce sviluppare il codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4a160-124">You can install the SDK from the [Azure Downloads](https://azure.microsoft.com/downloads/) page, in the language in which you prefer to develop your application code.</span></span>

<span data-ttu-id="4a160-125">Per poter esportare un pacchetto di servizio, è necessario configurare tre funzionalità del servizio cloud:</span><span class="sxs-lookup"><span data-stu-id="4a160-125">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="4a160-126">Se si vuole distribuire un servizio cloud che usa SSL (Secure Sockets Layer) per la crittografia dei dati, [configurare l'applicazione](cloud-services-configure-ssl-certificate-portal.md#modify) per SSL.</span><span class="sxs-lookup"><span data-stu-id="4a160-126">If you want to deploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate-portal.md#modify) for SSL.</span></span>
* <span data-ttu-id="4a160-127">Se si vogliono configurare connessioni Desktop remoto a istanze del ruolo, [configurare i ruoli](cloud-services-role-enable-remote-desktop-new-portal.md) per Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="4a160-127">If you want to configure Remote Desktop connections to role instances, [configure the roles](cloud-services-role-enable-remote-desktop-new-portal.md) for Remote Desktop.</span></span>
* <span data-ttu-id="4a160-128">Se si desidera configurare il monitoraggio dettagliato per il servizio cloud, abilitare la Diagnostica Azure per il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="4a160-128">If you want to configure verbose monitoring for your cloud service, enable Azure Diagnostics for the cloud service.</span></span> <span data-ttu-id="4a160-129">*Monitoraggio minimo* (livello di monitoraggio predefinito) ricorre a contatori delle prestazioni raccolti dai sistemi operativi host per istanze del ruolo (macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="4a160-129">*Minimal monitoring* (the default monitoring level) uses performance counters gathered from the host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="4a160-130">*Il* monitoraggio dettagliato raccoglie metriche supplementari in base ai dati delle prestazioni all'interno delle istanze del ruolo per consentire un'analisi più accurata dei problemi che si verificano durante l'elaborazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4a160-130">*Verbose monitoring* gathers additional metrics based on performance data within the role instances to enable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="4a160-131">Per scoprire come abilitare la Diagnostica Azure, vedere [Abilitazione della diagnostica in Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="4a160-131">To find out how to enable Azure Diagnostics, see [Enabling diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="4a160-132">Per creare un servizio cloud con le distribuzioni dei ruoli Web o dei ruoli di lavoro, è necessario [creare il pacchetto del servizio](cloud-services-model-and-package.md#servicepackagecspkg).</span><span class="sxs-lookup"><span data-stu-id="4a160-132">To create a cloud service with deployments of web roles or worker roles, you must [create the service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4a160-133">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="4a160-133">Before you begin</span></span>
* <span data-ttu-id="4a160-134">Se Azure SDK non è stato installato, fare clic su **Install Azure SDK** per aprire la pagina di [download](https://azure.microsoft.com/downloads/)di Azure e quindi scaricare l'SDK nel linguaggio in cui si preferisce sviluppare il codice.</span><span class="sxs-lookup"><span data-stu-id="4a160-134">If you haven't installed the Azure SDK, click **Install Azure SDK** to open the [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download the SDK for the language in which you prefer to develop your code.</span></span> <span data-ttu-id="4a160-135">(È possibile eseguire questa operazione in seguito).</span><span class="sxs-lookup"><span data-stu-id="4a160-135">(You'll have an opportunity to do this later.)</span></span>
* <span data-ttu-id="4a160-136">Se un'istanza del ruolo lo richiede, creare i certificati.</span><span class="sxs-lookup"><span data-stu-id="4a160-136">If any role instances require a certificate, create the certificates.</span></span> <span data-ttu-id="4a160-137">I servizi cloud richiedono un file con estensione pfx con una chiave privata.</span><span class="sxs-lookup"><span data-stu-id="4a160-137">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="4a160-138">È possibile caricare i certificati in Azure nel corso della creazione e della distribuzione del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="4a160-138">You can upload the certificates to Azure as you create and deploy the cloud service.</span></span>

## <a name="create-and-deploy"></a><span data-ttu-id="4a160-139">Creazione e distribuzione</span><span class="sxs-lookup"><span data-stu-id="4a160-139">Create and deploy</span></span>
1. <span data-ttu-id="4a160-140">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4a160-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4a160-141">Fare clic su **Nuovo > Calcolo**, quindi scorrere verso il basso e fare clic su **Servizio cloud**.</span><span class="sxs-lookup"><span data-stu-id="4a160-141">Click **New > Compute**, and then scroll down to and click **Cloud Service**.</span></span>

    ![Pubblicare il servizio cloud](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. <span data-ttu-id="4a160-143">Nel nuovo pannello **Servizio cloud** immettere un valore per il **nome DNS**.</span><span class="sxs-lookup"><span data-stu-id="4a160-143">In the new **Cloud Service** blade, enter a value for the **DNS name**.</span></span>
4. <span data-ttu-id="4a160-144">Creare un nuovo **Gruppo di risorse** o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="4a160-144">Create a new **Resource Group** or select an existing one.</span></span>
5. <span data-ttu-id="4a160-145">Selezionare un **percorso**.</span><span class="sxs-lookup"><span data-stu-id="4a160-145">Select a **Location**.</span></span>
6. <span data-ttu-id="4a160-146">Fare clic su **Pacchetto**.</span><span class="sxs-lookup"><span data-stu-id="4a160-146">Click **Package**.</span></span> <span data-ttu-id="4a160-147">Verrà visualizzato il pannello **Carica un pacchetto** .</span><span class="sxs-lookup"><span data-stu-id="4a160-147">This will open the **Upload a package** blade.</span></span> <span data-ttu-id="4a160-148">Compilare i campi obbligatori.</span><span class="sxs-lookup"><span data-stu-id="4a160-148">Fill in the required fields.</span></span> <span data-ttu-id="4a160-149">Se sono presenti ruoli contenenti una singola istanza, assicurarsi che l'opzione **Distribuisci anche se uno o più ruoli contengono una singola istanza** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="4a160-149">If any of your roles contain a single instance, ensure **Deploy even if one or more roles contain a single instance** is selected.</span></span>
7. <span data-ttu-id="4a160-150">Assicurarsi che l'opzione **Avvia distribuzione** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="4a160-150">Make sure that **Start deployment** is selected.</span></span>
8. <span data-ttu-id="4a160-151">Fare clic su **OK** per chiudere il pannello **Carica un pacchetto**.</span><span class="sxs-lookup"><span data-stu-id="4a160-151">Click **OK** which will close the **Upload a package** blade.</span></span>
9. <span data-ttu-id="4a160-152">Se non è disponibile un certificato da aggiungere, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4a160-152">If you do not have any certificates to add, click **Create**.</span></span>

    ![Pubblicare il servizio cloud](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a><span data-ttu-id="4a160-154">Caricamento di un certificato</span><span class="sxs-lookup"><span data-stu-id="4a160-154">Upload a certificate</span></span>
<span data-ttu-id="4a160-155">Se il pacchetto di distribuzione è stato [configurato per usare i certificati](cloud-services-configure-ssl-certificate-portal.md#modify), a questo punto è possibile caricare il certificato.</span><span class="sxs-lookup"><span data-stu-id="4a160-155">If your deployment package was [configured to use certificates](cloud-services-configure-ssl-certificate-portal.md#modify), you can upload the certificate now.</span></span>

1. <span data-ttu-id="4a160-156">Selezionare **Certificati** e nel pannello **Aggiungi certificati** selezionare il file con estensione pfx del certificato SSL e fornire la **password** per il certificato.</span><span class="sxs-lookup"><span data-stu-id="4a160-156">Select **Certificates**, and on the **Add certificates** blade, select the SSL certificate .pfx file, and then provide the **Password** for the certificate,</span></span>
2. <span data-ttu-id="4a160-157">Fare clic su **Collega certificato** e quindi su **OK** nel pannello **Aggiungi certificati**.</span><span class="sxs-lookup"><span data-stu-id="4a160-157">Click **Attach certificate**, and then click **OK** on the **Add certificates** blade.</span></span>
3. <span data-ttu-id="4a160-158">Fare clic su **Crea** nel pannello **Servizio cloud**.</span><span class="sxs-lookup"><span data-stu-id="4a160-158">Click **Create** on the **Cloud Service** blade.</span></span> <span data-ttu-id="4a160-159">Quando la distribuzione ha raggiunto lo stato **Ready** , è possibile procedere con i passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="4a160-159">When the deployment has reached the **Ready** status, you can proceed to the next steps.</span></span>

    ![Pubblicare il servizio cloud](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="4a160-161">Verificare che la distribuzione sia stata completata correttamente</span><span class="sxs-lookup"><span data-stu-id="4a160-161">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="4a160-162">Fare clic sull'istanza del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="4a160-162">Click the cloud service instance.</span></span>

    <span data-ttu-id="4a160-163">Lo stato del servizio dovrebbe ora essere **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="4a160-163">The status should show that the service is **Running**.</span></span>
2. <span data-ttu-id="4a160-164">In **Informazioni di base** fare clic su **URL sito** per aprire il servizio cloud in un Web browser.</span><span class="sxs-lookup"><span data-stu-id="4a160-164">Under **Essentials**, click the **Site URL** to open your cloud service in a web browser.</span></span>

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a><span data-ttu-id="4a160-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4a160-166">Next steps</span></span>
* <span data-ttu-id="4a160-167">[Configurazione generale del servizio cloud](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4a160-167">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="4a160-168">Configurare un [nome di dominio personalizzato](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4a160-168">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="4a160-169">[Gestire il servizio cloud](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4a160-169">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="4a160-170">Configurare i [certificati ssl](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4a160-170">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
