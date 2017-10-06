---
title: aaaDeploy il tooAzure app servizio App utilizzando FTP/S | Documenti Microsoft
description: Informazioni su come toodeploy tooAzure l'app App Service tramite FTP o FTPS.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a><span data-ttu-id="fddd3-103">Distribuire il servizio App utilizzando FTP/S di tooAzure app</span><span class="sxs-lookup"><span data-stu-id="fddd3-103">Deploy your app tooAzure App Service using FTP/S</span></span>

<span data-ttu-id="fddd3-104">In questo articolo illustra come toouse FTP o FTPS toodeploy l'app web back-end dell'app mobile o app per le API troppo[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="fddd3-104">This article shows you how toouse FTP or FTPS toodeploy your web app, mobile app backend, or API app too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="fddd3-105">endpoint di Hello FTP/S per l'app è già attivo.</span><span class="sxs-lookup"><span data-stu-id="fddd3-105">hello FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="fddd3-106">Non è distribuzione FTP/S tooenable necessaria alcuna configurazione.</span><span class="sxs-lookup"><span data-stu-id="fddd3-106">No configuration is necessary tooenable FTP/S deployment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fddd3-107">Si sta eseguendo in modo continuo passaggi tooimprove sicurezza piattaforma Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fddd3-107">We are continuously taking steps tooimprove Microsoft Azure Platform security.</span></span> <span data-ttu-id="fddd3-108">Nell'ambito di questa attività in corso un aggiornamento delle applicazioni Web è pianificato per le aree della Germania centrale e nord-orientale.</span><span class="sxs-lookup"><span data-stu-id="fddd3-108">As part of this ongoing effort an upgrade of Web Applications is planned for Germany Central and Germany Northeast regions.</span></span> <span data-ttu-id="fddd3-109">Durante l'esecuzione dell'App Web verrà la disabilitazione della utilizzare hello del protocollo di testo normale FTP per le distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="fddd3-109">During this Web Apps will be disabling hello use of plain text FTP protocol for deployments.</span></span> <span data-ttu-id="fddd3-110">I clienti tooour raccomandazione è tooFTPS tooswitch per le distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="fddd3-110">Our recommendation tooour customers is tooswitch tooFTPS for deployments.</span></span> <span data-ttu-id="fddd3-111">Non Prevediamo qualsiasi servizio tooyour interruzioni durante l'aggiornamento a cui è pianificato per 9/5.</span><span class="sxs-lookup"><span data-stu-id="fddd3-111">We do not expect any disruption tooyour service during this upgrade which is planned for 9/5.</span></span> <span data-ttu-id="fddd3-112">Grazie per il sostegno per il lavoro richiesto.</span><span class="sxs-lookup"><span data-stu-id="fddd3-112">We appreciate you support in this effort.</span></span>

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="fddd3-113">Passaggio 1: Impostare le credenziali per la distribuzione</span><span class="sxs-lookup"><span data-stu-id="fddd3-113">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="fddd3-114">server di tooaccess hello FTP per l'app, è necessario innanzitutto le credenziali di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fddd3-114">tooaccess hello FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="fddd3-115">tooset o Reimposta le credenziali di distribuzione, vedere [le credenziali di distribuzione di Azure App Service](app-service-deployment-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="fddd3-115">tooset or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="fddd3-116">Questa esercitazione viene illustrato l'utilizzo di hello delle credenziali a livello di utente.</span><span class="sxs-lookup"><span data-stu-id="fddd3-116">This tutorial demonstrates hello use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="fddd3-117">Passaggio 2: Ottenere informazioni di connessione a FTP</span><span class="sxs-lookup"><span data-stu-id="fddd3-117">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="fddd3-118">In hello [portale di Azure](https://portal.azure.com), Apri l'app [pannello della risorsa](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="fddd3-118">In hello [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="fddd3-119">Selezionare **Panoramica** nel menu a sinistra di hello, quindi annotare i valori hello per **utente FTP/distribuzione**, **nome Host FTP**, e **il nome Host FTPS**.</span><span class="sxs-lookup"><span data-stu-id="fddd3-119">Select **Overview** in hello left menu, then note hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![Informazioni di connessione a FTP](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="fddd3-121">Hello **utente FTP/distribuzione** valore utente come visualizzato dal portale di Azure, incluso il nome dell'app hello contesto appropriato tooprovide di ordine per il server FTP hello hello.</span><span class="sxs-lookup"><span data-stu-id="fddd3-121">hello **FTP/Deployment User** user value as displayed by hello Azure Portal including hello app name in order tooprovide proper context for hello FTP server.</span></span>
    > <span data-ttu-id="fddd3-122">È possibile trovare hello stesse informazioni quando si seleziona **proprietà** nel menu a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="fddd3-122">You can find hello same information when you select **Properties** in hello left menu.</span></span> 
    >
    > <span data-ttu-id="fddd3-123">Inoltre, la password di hello distribuzione non viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="fddd3-123">Also, hello deployment password is never shown.</span></span> <span data-ttu-id="fddd3-124">Se si dimentica la password di distribuzione, tornare troppo[passaggio 1](#step1) e reimpostare la password di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fddd3-124">If you forget your deployment password, go back too[step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-tooazure"></a><span data-ttu-id="fddd3-125">Passaggio 3: Distribuire file tooAzure</span><span class="sxs-lookup"><span data-stu-id="fddd3-125">Step 3: Deploy files tooAzure</span></span>

1. <span data-ttu-id="fddd3-126">Dal client FTP ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client)e così via), utilizzare le informazioni di connessione hello raccolte tooconnect tooyour app.</span><span class="sxs-lookup"><span data-stu-id="fddd3-126">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use hello connection information you gathered tooconnect tooyour app.</span></span>
3. <span data-ttu-id="fddd3-127">Copiare i file e i relativi toohello struttura rispettive directory [ **/sito/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (o hello **/sito/wwwroot/App_Data/processi/** directory per Processi Web).</span><span class="sxs-lookup"><span data-stu-id="fddd3-127">Copy your files and their respective directory structure toohello [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or hello **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="fddd3-128">App di hello tooverify URL dell'app tooyour Sfoglia viene eseguito correttamente.</span><span class="sxs-lookup"><span data-stu-id="fddd3-128">Browse tooyour app's URL tooverify hello app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="fddd3-129">A differenza di [le distribuzioni basate su Git](app-service-deploy-local-git.md), la distribuzione FTP non supporta hello automazioni di distribuzione seguenti:</span><span class="sxs-lookup"><span data-stu-id="fddd3-129">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support hello following deployment automations:</span></span> 
>
> - <span data-ttu-id="fddd3-130">Ripristino delle dipendenze (ad esempio, automazioni NuGet, NPM, PIP e Composer)</span><span class="sxs-lookup"><span data-stu-id="fddd3-130">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="fddd3-131">Compilazione di file binari .NET</span><span class="sxs-lookup"><span data-stu-id="fddd3-131">compilation of .NET binaries</span></span>
> - <span data-ttu-id="fddd3-132">Generazione di web.config ([esempio di Node.js](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span><span class="sxs-lookup"><span data-stu-id="fddd3-132">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="fddd3-133">Questi file necessari devono essere ripristinati, compilati e generati manualmente nel computer locale e distribuiti con l'app.</span><span class="sxs-lookup"><span data-stu-id="fddd3-133">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="fddd3-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fddd3-134">Next steps</span></span>

<span data-ttu-id="fddd3-135">Per gli scenari più avanzati, provare a [distribuzione tooAzure con Git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="fddd3-135">For more advanced deployment scenarios, try [deploying tooAzure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="fddd3-136">Distribuzione basati su GIT tooAzure consente il controllo della versione, ripristino del pacchetto, MSBuild e molto altro.</span><span class="sxs-lookup"><span data-stu-id="fddd3-136">Git-based deployment tooAzure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="fddd3-137">Altre risorse</span><span class="sxs-lookup"><span data-stu-id="fddd3-137">More Resources</span></span>

* <span data-ttu-id="fddd3-138">[Creare un'app Web PHP-MySQL e distribuirla tramite FTP](web-sites-php-mysql-deploy-use-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="fddd3-138">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="fddd3-139">Credenziali per la distribuzione del Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="fddd3-139">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
