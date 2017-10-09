---
title: aaaWeb la clonazione di App tramite il portale di Azure
description: Informazioni su come tooclone il toonew App Web App Web tramite il portale di Azure.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: 605c4879f34d568e9981c34109f9496731c9ed18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a><span data-ttu-id="653c7-103">Clonazione di app del servizio app di Azure con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="653c7-103">Azure App Service App Cloning Using Azure Portal</span></span>
<span data-ttu-id="653c7-104">la funzionalità di clonazione Hello [App Web di servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) consente di eseguire facilmente la clonazione app web esistente App tooa appena creato in un'area diversa o in hello stessa area.</span><span class="sxs-lookup"><span data-stu-id="653c7-104">hello cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps tooa newly created app in a different region or in hello same region.</span></span> <span data-ttu-id="653c7-105">In questo modo i clienti toodeploy un numero di App in aree geografiche diverse in modo semplice e rapido.</span><span class="sxs-lookup"><span data-stu-id="653c7-105">This will enable customers toodeploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="653c7-106">La clonazione di app è attualmente supportata solo per i piani di servizio app Premium.</span><span class="sxs-lookup"><span data-stu-id="653c7-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="653c7-107">Usa funzionalità nuova Hello hello stesso limitazioni delle funzionalità di Backup di applicazioni Web, vedere [eseguire il backup di un'app web in Azure App Service](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="653c7-107">hello new feature uses hello same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="653c7-108">Clonazione di un'app esistente</span><span class="sxs-lookup"><span data-stu-id="653c7-108">Cloning an existing App</span></span>
<span data-ttu-id="653c7-109">app web Hello deve essere eseguita in hello **Premium** modalità affinché si toocreate un duplicato per l'app web hello.</span><span class="sxs-lookup"><span data-stu-id="653c7-109">hello web app must be running in hello **Premium** mode in order for you toocreate a clone for hello web app.</span></span>

1. <span data-ttu-id="653c7-110">In hello [portale Azure](https://portal.azure.com/), aprire il pannello dell'app web.</span><span class="sxs-lookup"><span data-stu-id="653c7-110">In hello [Azure Portal](https://portal.azure.com/), open your web app's blade.</span></span>
2. <span data-ttu-id="653c7-111">Fare clic su **Strumenti**.</span><span class="sxs-lookup"><span data-stu-id="653c7-111">Click **Tools**.</span></span> <span data-ttu-id="653c7-112">Quindi, nel hello **strumenti** pannello, fare clic su **Clone App**.</span><span class="sxs-lookup"><span data-stu-id="653c7-112">Then, in hello **Tools** blade, click **Clone App**.</span></span>
   
    ![][1]
   
   > [!NOTE]
   > <span data-ttu-id="653c7-113">Se hello web app non è già in hello **Premium** modalità, si riceverà un messaggio che indica la modalità di hello è supportato per la clonazione di app.</span><span class="sxs-lookup"><span data-stu-id="653c7-113">If hello web app is not already in hello **Premium** mode, you will receive a message indicating hello supported modes for app cloning.</span></span> <span data-ttu-id="653c7-114">A questo punto, si dispone di hello opzione tooselect **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="653c7-114">At this point, you have hello option tooselect **Upgrade**.</span></span>
   > 
   > 
3. <span data-ttu-id="653c7-115">In hello **Clone App** pannello consente di specificare un nome di hello nuova app web, gruppo di risorse e piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="653c7-115">In hello **Clone App** blade provide a name of hello new web app, Resource Group, and App Service Plan.</span></span> <span data-ttu-id="653c7-116">Anche hello utente sarà in grado di toochoose se tooclone una serie di impostazioni app web di origine o non.</span><span class="sxs-lookup"><span data-stu-id="653c7-116">Also hello user will be able toochoose whether tooclone a number of source web app settings or not.</span></span>
   
    ![][2]
4. <span data-ttu-id="653c7-117">Dopo aver fatto clic **creare** piattaforma hello inizierà a funzionare per la creazione di un clone di hello app web di origine.</span><span class="sxs-lookup"><span data-stu-id="653c7-117">After clicking **create** hello platform will start working on creating a clone of hello source web app.</span></span>

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a><span data-ttu-id="653c7-118">La clonazione di un tooan App esistenti di ambiente del servizio App</span><span class="sxs-lookup"><span data-stu-id="653c7-118">Cloning an existing App tooan App Service Environment</span></span>
<span data-ttu-id="653c7-119">In hello **Clone App** cliente hello pannello avrà hello opzione toochoose un pool di applicazioni in un ambiente di servizio App esistente.</span><span class="sxs-lookup"><span data-stu-id="653c7-119">In hello **Clone App** blade hello customer will have hello option toochoose an app pool in an existing App Service Environment.</span></span>

## <a name="current-restrictions"></a><span data-ttu-id="653c7-120">Restrizioni attuali</span><span class="sxs-lookup"><span data-stu-id="653c7-120">Current Restrictions</span></span>
<span data-ttu-id="653c7-121">Questa funzionalità è attualmente in anteprima, Microsoft è impegnata tooadd nuove funzionalità nel tempo, hello seguente elenco sono hello restrizioni note sul supporto corrente hello di clonazione app nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="653c7-121">This feature is currently in preview, we are working tooadd new capabilities over time, hello following list are hello known restrictions on hello current support of app cloning in Azure Portal:</span></span>

* <span data-ttu-id="653c7-122">Le impostazioni di Gestione traffico di Azure non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="653c7-122">Azure Traffic Manager settings are not cloned</span></span>
* <span data-ttu-id="653c7-123">Le impostazioni di ridimensionamento automatico non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="653c7-123">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="653c7-124">Le impostazioni di pianificazione del backup non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="653c7-124">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="653c7-125">Le impostazioni della rete virtuale non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="653c7-125">VNET settings are not cloned</span></span>
* <span data-ttu-id="653c7-126">App Insights non automaticamente impostate nell'applicazione web di destinazione hello</span><span class="sxs-lookup"><span data-stu-id="653c7-126">App Insights are not automatically set up on hello destination web app</span></span>
* <span data-ttu-id="653c7-127">Le impostazioni di Easy Auth non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="653c7-127">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="653c7-128">L'estensione Kudu non viene clonata.</span><span class="sxs-lookup"><span data-stu-id="653c7-128">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="653c7-129">Le regole TiP non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="653c7-129">TiP rules are not cloned</span></span>
* <span data-ttu-id="653c7-130">Il contenuto di database non viene clonato.</span><span class="sxs-lookup"><span data-stu-id="653c7-130">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="653c7-131">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="653c7-131">References</span></span>
* [<span data-ttu-id="653c7-132">Clonazione di app Web con PowerShell</span><span class="sxs-lookup"><span data-stu-id="653c7-132">Web App Cloning using PowerShell</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="653c7-133">Eseguire il backup di un'app Web nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="653c7-133">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="653c7-134">Come tooCreate un ambiente del servizio App</span><span class="sxs-lookup"><span data-stu-id="653c7-134">How tooCreate an App Service Environment</span></span>](app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="653c7-135">Creare un'app Web in un ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="653c7-135">Create a web app in an App Service Environment</span></span>](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="653c7-136">Introduzione tooApp ambiente del servizio</span><span class="sxs-lookup"><span data-stu-id="653c7-136">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
