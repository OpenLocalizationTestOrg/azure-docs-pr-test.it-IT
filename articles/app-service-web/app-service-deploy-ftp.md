---
title: Distribuire l'app nel servizio app di Azure usando FTP/S | Documentazione Microsoft
description: Informazioni su come distribuire l'app nel servizio app di Azure usando FTP o FTPS.
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
ms.openlocfilehash: 9078abbc4ed7eff6975201443992f7bbb84bf57c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-your-app-to-azure-app-service-using-ftps"></a><span data-ttu-id="b249f-103">Distribuire l'app nel servizio app di Azure usando FTP/S</span><span class="sxs-lookup"><span data-stu-id="b249f-103">Deploy your app to Azure App Service using FTP/S</span></span>

<span data-ttu-id="b249f-104">Questo articolo illustra come usare FTP o FTPS per distribuire l'app Web, il back-end dell'app per dispositivi mobili o l'app per le API nel [servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="b249f-104">This article shows you how to use FTP or FTPS to deploy your web app, mobile app backend, or API app to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="b249f-105">L'endpoint FTP/S per l'app è già attivo.</span><span class="sxs-lookup"><span data-stu-id="b249f-105">The FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="b249f-106">Non è necessaria alcuna configurazione per abilitare la distribuzione FTP/S.</span><span class="sxs-lookup"><span data-stu-id="b249f-106">No configuration is necessary to enable FTP/S deployment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b249f-107">Microsoft è costantemente impegnata per migliorare la protezione della piattaforma Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b249f-107">We are continuously taking steps to improve Microsoft Azure Platform security.</span></span> <span data-ttu-id="b249f-108">Nell'ambito di questa attività in corso un aggiornamento delle applicazioni Web è pianificato per le aree della Germania centrale e nord-orientale.</span><span class="sxs-lookup"><span data-stu-id="b249f-108">As part of this ongoing effort an upgrade of Web Applications is planned for Germany Central and Germany Northeast regions.</span></span> <span data-ttu-id="b249f-109">Durante tale aggiornamento le App Web disabiliteranno l'uso del protocollo di testo normale FTP per le distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="b249f-109">During this Web Apps will be disabling the use of plain text FTP protocol for deployments.</span></span> <span data-ttu-id="b249f-110">Si consiglia ai clienti per passare a FTPS per le distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="b249f-110">Our recommendation to our customers is to switch to FTPS for deployments.</span></span> <span data-ttu-id="b249f-111">Non sono previste interruzioni del servizio durante l'aggiornamento, pianificato per il 5/9.</span><span class="sxs-lookup"><span data-stu-id="b249f-111">We do not expect any disruption to your service during this upgrade which is planned for 9/5.</span></span> <span data-ttu-id="b249f-112">Grazie per il sostegno per il lavoro richiesto.</span><span class="sxs-lookup"><span data-stu-id="b249f-112">We appreciate you support in this effort.</span></span>

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="b249f-113">Passaggio 1: Impostare le credenziali per la distribuzione</span><span class="sxs-lookup"><span data-stu-id="b249f-113">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="b249f-114">Per accedere al server FTP per l'app, prima sono necessarie le credenziali per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b249f-114">To access the FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="b249f-115">Per impostare o reimpostare le credenziali per la distribuzione, vedere [Credenziali per la distribuzione del Servizio app di Azure](app-service-deployment-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="b249f-115">To set or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="b249f-116">Questa esercitazione illustra l'uso di credenziali a livello di utente.</span><span class="sxs-lookup"><span data-stu-id="b249f-116">This tutorial demonstrates the use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="b249f-117">Passaggio 2: Ottenere informazioni di connessione a FTP</span><span class="sxs-lookup"><span data-stu-id="b249f-117">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="b249f-118">Nel [portale di Azure](https://portal.azure.com) aprire il [pannello della risorsa](../azure-resource-manager/resource-group-portal.md#manage-resources) dell'app.</span><span class="sxs-lookup"><span data-stu-id="b249f-118">In the [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="b249f-119">Scegliere **Panoramica** dal menu a sinistra, quindi prendere nota dei valori per **Utente FTP/distribuzione**, **Nome host FTP** e **Nome host FTPS**.</span><span class="sxs-lookup"><span data-stu-id="b249f-119">Select **Overview** in the left menu, then note the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![Informazioni di connessione a FTP](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="b249f-121">Il valore di **Utente FTP/distribuzione** visualizzato dal portale di Azure include il nome dell'app per rendere disponibile un contesto appropriato al server FTP.</span><span class="sxs-lookup"><span data-stu-id="b249f-121">The **FTP/Deployment User** user value as displayed by the Azure Portal including the app name in order to provide proper context for the FTP server.</span></span>
    > <span data-ttu-id="b249f-122">È possibile trovare le stesse informazioni scegliendo **Proprietà** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="b249f-122">You can find the same information when you select **Properties** in the left menu.</span></span> 
    >
    > <span data-ttu-id="b249f-123">La password per la distribuzione inoltre non viene mai visualizzata.</span><span class="sxs-lookup"><span data-stu-id="b249f-123">Also, the deployment password is never shown.</span></span> <span data-ttu-id="b249f-124">Se si dimentica la password per la distribuzione, tornare al [passaggio 1](#step1) e reimpostarla.</span><span class="sxs-lookup"><span data-stu-id="b249f-124">If you forget your deployment password, go back to [step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-to-azure"></a><span data-ttu-id="b249f-125">Passaggio 3: Distribuire file in Azure</span><span class="sxs-lookup"><span data-stu-id="b249f-125">Step 3: Deploy files to Azure</span></span>

1. <span data-ttu-id="b249f-126">Dal client FTP ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client) e così via) usare le informazioni di connessione raccolte per connettersi all'app.</span><span class="sxs-lookup"><span data-stu-id="b249f-126">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use the connection information you gathered to connect to your app.</span></span>
3. <span data-ttu-id="b249f-127">Copiare i file e la struttura di directory corrispondente nella directory [**/site/wwwroot** ](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure o nella directory **/site/wwwroot/App_Data/Jobs/** per i processi Web.</span><span class="sxs-lookup"><span data-stu-id="b249f-127">Copy your files and their respective directory structure to the [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or the **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="b249f-128">Passare all'URL dell'app per verificare che l'applicazione venga eseguita correttamente.</span><span class="sxs-lookup"><span data-stu-id="b249f-128">Browse to your app's URL to verify the app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="b249f-129">Diversamente dalle [distribuzioni basate su Git](app-service-deploy-local-git.md), la distribuzione FTP non supporta le automazioni di distribuzione seguenti:</span><span class="sxs-lookup"><span data-stu-id="b249f-129">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support the following deployment automations:</span></span> 
>
> - <span data-ttu-id="b249f-130">Ripristino delle dipendenze (ad esempio, automazioni NuGet, NPM, PIP e Composer)</span><span class="sxs-lookup"><span data-stu-id="b249f-130">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="b249f-131">Compilazione di file binari .NET</span><span class="sxs-lookup"><span data-stu-id="b249f-131">compilation of .NET binaries</span></span>
> - <span data-ttu-id="b249f-132">Generazione di web.config ([esempio di Node.js](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span><span class="sxs-lookup"><span data-stu-id="b249f-132">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="b249f-133">Questi file necessari devono essere ripristinati, compilati e generati manualmente nel computer locale e distribuiti con l'app.</span><span class="sxs-lookup"><span data-stu-id="b249f-133">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="b249f-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b249f-134">Next steps</span></span>

<span data-ttu-id="b249f-135">Per scenari di distribuzione più avanzati, provare a eseguire la [distribuzione in Azure con Git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="b249f-135">For more advanced deployment scenarios, try [deploying to Azure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="b249f-136">La distribuzione basata su Git in Azure abilita il controllo della versione, il ripristino del pacchetto, MSBuild e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="b249f-136">Git-based deployment to Azure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="b249f-137">Altre risorse</span><span class="sxs-lookup"><span data-stu-id="b249f-137">More Resources</span></span>

* <span data-ttu-id="b249f-138">[Creare un'app Web PHP-MySQL e distribuirla tramite FTP](web-sites-php-mysql-deploy-use-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="b249f-138">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="b249f-139">Credenziali per la distribuzione del Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="b249f-139">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
