---
title: Clonazione di app Web con il portale di Azure
description: Come clonare le app Web in nuove app Web con il portale di Azure.
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
ms.openlocfilehash: 9ebfa91c7972ab3c264032ead8376c23c1197a4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a><span data-ttu-id="b67ea-103">Clonazione di app del servizio app di Azure con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b67ea-103">Azure App Service App Cloning Using Azure Portal</span></span>
<span data-ttu-id="b67ea-104">La funzionalità di clonazione nelle [app Web del servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) consente facilmente di clonare app Web esistenti in un'app appena creata in un'area diversa o nella stessa area.</span><span class="sxs-lookup"><span data-stu-id="b67ea-104">The cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="b67ea-105">In questo modo i clienti possono distribuire una quantità di app in aree geografiche diverse rapidamente e con facilità.</span><span class="sxs-lookup"><span data-stu-id="b67ea-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="b67ea-106">La clonazione di app è attualmente supportata solo per i piani di servizio app Premium.</span><span class="sxs-lookup"><span data-stu-id="b67ea-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="b67ea-107">La nuova funzionalità usa le stesse limitazioni della funzionalità di backup di App Web. Vedere [Eseguire il backup di un'app Web nel servizio app di Azure](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="b67ea-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="b67ea-108">Clonazione di un'app esistente</span><span class="sxs-lookup"><span data-stu-id="b67ea-108">Cloning an existing App</span></span>
<span data-ttu-id="b67ea-109">L'app Web deve essere in esecuzione in modalità **Premium** per poter creare un clone per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="b67ea-109">The web app must be running in the **Premium** mode in order for you to create a clone for the web app.</span></span>

1. <span data-ttu-id="b67ea-110">Nel [portale di Azure](https://portal.azure.com/), aprire il pannello dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="b67ea-110">In the [Azure Portal](https://portal.azure.com/), open your web app's blade.</span></span>
2. <span data-ttu-id="b67ea-111">Fare clic su **Strumenti**.</span><span class="sxs-lookup"><span data-stu-id="b67ea-111">Click **Tools**.</span></span> <span data-ttu-id="b67ea-112">Quindi, nel pannello **Strumenti** selezionare **Clona app**.</span><span class="sxs-lookup"><span data-stu-id="b67ea-112">Then, in the **Tools** blade, click **Clone App**.</span></span>
   
    ![][1]
   
   > [!NOTE]
   > <span data-ttu-id="b67ea-113">Se l'app Web non è già in modalità **Standard** , si riceverà un messaggio che indica le modalità supportate per la clonazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="b67ea-113">If the web app is not already in the **Premium** mode, you will receive a message indicating the supported modes for app cloning.</span></span> <span data-ttu-id="b67ea-114">A questo punto è possibile selezionare **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="b67ea-114">At this point, you have the option to select **Upgrade**.</span></span>
   > 
   > 
3. <span data-ttu-id="b67ea-115">Nel pannello **Clona app** specificare un nome per la nuova app Web, il gruppo di risorse e il piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="b67ea-115">In the **Clone App** blade provide a name of the new web app, Resource Group, and App Service Plan.</span></span> <span data-ttu-id="b67ea-116">Inoltre, l'utente sarà in grado di scegliere se clonare un numero di impostazioni dell'app Web di origine o meno.</span><span class="sxs-lookup"><span data-stu-id="b67ea-116">Also the user will be able to choose whether to clone a number of source web app settings or not.</span></span>
   
    ![][2]
4. <span data-ttu-id="b67ea-117">Dopo aver selezionato **Crea** , la piattaforma inizierà a creare un clone per l'app Web di origine.</span><span class="sxs-lookup"><span data-stu-id="b67ea-117">After clicking **create** the platform will start working on creating a clone of the source web app.</span></span>

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="b67ea-118">Clonazione di un'app esistente in un ambiente del servizio App</span><span class="sxs-lookup"><span data-stu-id="b67ea-118">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="b67ea-119">Nel pannello **Clona app** il cliente ha la possibilità di selezionare un pool di app in un ambiente del servizio app esistente.</span><span class="sxs-lookup"><span data-stu-id="b67ea-119">In the **Clone App** blade the customer will have the option to choose an app pool in an existing App Service Environment.</span></span>

## <a name="current-restrictions"></a><span data-ttu-id="b67ea-120">Restrizioni attuali</span><span class="sxs-lookup"><span data-stu-id="b67ea-120">Current Restrictions</span></span>
<span data-ttu-id="b67ea-121">Questa funzionalità è attualmente in anteprima e sono allo studio nuove funzionalità che saranno aggiunte con il tempo. L'elenco seguente include le restrizioni note riguardanti l'attuale supporto per la clonazione di app nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="b67ea-121">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current support of app cloning in Azure Portal:</span></span>

* <span data-ttu-id="b67ea-122">Le impostazioni di Gestione traffico di Azure non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="b67ea-122">Azure Traffic Manager settings are not cloned</span></span>
* <span data-ttu-id="b67ea-123">Le impostazioni di ridimensionamento automatico non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="b67ea-123">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="b67ea-124">Le impostazioni di pianificazione del backup non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="b67ea-124">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="b67ea-125">Le impostazioni della rete virtuale non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="b67ea-125">VNET settings are not cloned</span></span>
* <span data-ttu-id="b67ea-126">Le informazioni sull'app non vengono configurate automaticamente nell'app Web di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b67ea-126">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="b67ea-127">Le impostazioni di Easy Auth non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="b67ea-127">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="b67ea-128">L'estensione Kudu non viene clonata.</span><span class="sxs-lookup"><span data-stu-id="b67ea-128">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="b67ea-129">Le regole TiP non vengono clonate.</span><span class="sxs-lookup"><span data-stu-id="b67ea-129">TiP rules are not cloned</span></span>
* <span data-ttu-id="b67ea-130">Il contenuto di database non viene clonato.</span><span class="sxs-lookup"><span data-stu-id="b67ea-130">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="b67ea-131">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="b67ea-131">References</span></span>
* [<span data-ttu-id="b67ea-132">Clonazione di app Web con PowerShell</span><span class="sxs-lookup"><span data-stu-id="b67ea-132">Web App Cloning using PowerShell</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="b67ea-133">Eseguire il backup di un'app Web nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="b67ea-133">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="b67ea-134">Come creare un ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="b67ea-134">How to Create an App Service Environment</span></span>](app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="b67ea-135">Creare un'app Web in un ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="b67ea-135">Create a web app in an App Service Environment</span></span>](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="b67ea-136">Introduzione all'ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="b67ea-136">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
