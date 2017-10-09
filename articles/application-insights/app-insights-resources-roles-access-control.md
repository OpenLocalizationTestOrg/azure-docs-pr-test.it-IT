---
title: controllo di accesso, ruoli e aaaResources in Azure Application Insights | Documenti Microsoft
description: Proprietari, collaboratori e lettori di informazioni dell'organizzazione.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: a6f6ca0443b5f60239f094606e124f856967d8ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a><span data-ttu-id="f834d-103">Risorse, ruoli e controllo di accesso in Application Insights</span><span class="sxs-lookup"><span data-stu-id="f834d-103">Resources, roles, and access control in Application Insights</span></span>
<span data-ttu-id="f834d-104">È possibile controllare chi ha letto e aggiornare i dati di accesso tooyour in Azure [Application Insights][start], utilizzando [controllo di accesso basato sui ruoli in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f834d-104">You can control who has read and update access tooyour data in Azure [Application Insights][start], by using [Role-based access control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f834d-105">Assegnare l'accesso toousers in hello **gruppo di risorse o sottoscrizione** toowhich appartiene la risorsa di applicazione - non nella risorsa hello stessa.</span><span class="sxs-lookup"><span data-stu-id="f834d-105">Assign access toousers in hello **resource group or subscription** toowhich your application resource belongs - not in hello resource itself.</span></span> <span data-ttu-id="f834d-106">Assegnare hello **collaboratore di componenti di Application Insights** ruolo.</span><span class="sxs-lookup"><span data-stu-id="f834d-106">Assign hello **Application Insights component contributor** role.</span></span> <span data-ttu-id="f834d-107">In questo modo uniform controllo di accesso tooweb test e gli avvisi con la risorsa di applicazione.</span><span class="sxs-lookup"><span data-stu-id="f834d-107">This ensures uniform control of access tooweb tests and alerts along with your application resource.</span></span> <span data-ttu-id="f834d-108">[Altre informazioni](#access)</span><span class="sxs-lookup"><span data-stu-id="f834d-108">[Learn more](#access).</span></span>
> 
> 

## <a name="resources-groups-and-subscriptions"></a><span data-ttu-id="f834d-109">Risorse, gruppi e sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="f834d-109">Resources, groups and subscriptions</span></span>
<span data-ttu-id="f834d-110">Innanzitutto prendere nota di alcune definizioni:</span><span class="sxs-lookup"><span data-stu-id="f834d-110">First, some definitions:</span></span>

* <span data-ttu-id="f834d-111">**Risorse** : un'istanza di un servizio di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f834d-111">**Resource** - An instance of a Microsoft Azure service.</span></span> <span data-ttu-id="f834d-112">La risorsa di Application Insights consente di raccogliere, analizza e visualizza i dati di telemetria hello inviati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f834d-112">Your Application Insights resource collects, analyzes and displays hello telemetry data sent from your application.</span></span>  <span data-ttu-id="f834d-113">Altri tipi di risorse di Azure includono app Web, database e macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f834d-113">Other types of Azure resources include web apps, databases, and VMs.</span></span>
  
    <span data-ttu-id="f834d-114">Aprire le risorse, toosee hello [portale Azure][portal], accedere e fare clic su tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="f834d-114">toosee your resources, open hello [Azure Portal][portal], sign in, and click All Resources.</span></span> <span data-ttu-id="f834d-115">toofind una risorsa, tipo di parte del nome nel campo filtro hello.</span><span class="sxs-lookup"><span data-stu-id="f834d-115">toofind a resource, type part of its name in hello filter field.</span></span>
  
    ![Elenco di risorse di Azure](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* <span data-ttu-id="f834d-117">[**Gruppo di risorse** ] [ group] -tutte le risorse appartiene tooone gruppo.</span><span class="sxs-lookup"><span data-stu-id="f834d-117">[**Resource group**][group] - Every resource belongs tooone group.</span></span> <span data-ttu-id="f834d-118">Un gruppo è un modo toomanage relative risorse, in particolare per il controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="f834d-118">A group is a convenient way toomanage related resources, particularly for access control.</span></span> <span data-ttu-id="f834d-119">Ad esempio, in una risorsa del gruppo, è possibile inserire un'App Web, un'app di Application Insights risorse toomonitor hello e una tookeep risorse di archiviazione dati esportati.</span><span class="sxs-lookup"><span data-stu-id="f834d-119">For example, into one resource group you could put a Web App, an Application Insights resource toomonitor hello app, and a Storage resource tookeep exported data.</span></span>

    ![Scegliere Sfoglia, gruppi di risorse e quindi scegliere un gruppo](./media/app-insights-resources-roles-access-control/11-group.png)

* <span data-ttu-id="f834d-121">[**Sottoscrizione** ](https://manage.windowsazure.com) -toouse Application Insights o altre risorse di Azure, accedi tooan sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f834d-121">[**Subscription**](https://manage.windowsazure.com) - toouse Application Insights or other Azure resources, you sign in tooan Azure subscription.</span></span> <span data-ttu-id="f834d-122">Ogni gruppo di risorse appartiene tooone sottoscrizione di Azure, in cui si sceglie il pacchetto di prezzi e, se si tratta di una sottoscrizione di organizzazione, scegliere i membri di hello e le relative autorizzazioni di accesso.</span><span class="sxs-lookup"><span data-stu-id="f834d-122">Every resource group belongs tooone Azure subscription, where you choose your price package and, if it's an organization subscription, choose hello members and their access permissions.</span></span>
* <span data-ttu-id="f834d-123">[**Account Microsoft** ] [ account] -hello nome utente e password utilizzare toosign tooMicrosoft Azure sottoscrizioni, XBox Live, Outlook.com e altri servizi Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f834d-123">[**Microsoft account**][account] - hello username and password that you use toosign in tooMicrosoft Azure subscriptions, XBox Live, Outlook.com, and other Microsoft services.</span></span>

## <span data-ttu-id="f834d-124"><a name="access"></a>Controllare l'accesso nel gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="f834d-124"><a name="access"></a> Control access in hello resource group</span></span>
<span data-ttu-id="f834d-125">È importante toounderstand in risorsa toohello aggiunta creato per l'applicazione, sono presenti inoltre di separare risorse nascoste per gli avvisi e i test web.</span><span class="sxs-lookup"><span data-stu-id="f834d-125">It's important toounderstand that in addition toohello resource you created for your application, there are also separate hidden resources for alerts and web tests.</span></span> <span data-ttu-id="f834d-126">Sono collegato toohello stesso [gruppo di risorse](#resource-group) dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f834d-126">They are attached toohello same [resource group](#resource-group) as your application.</span></span> <span data-ttu-id="f834d-127">È anche possibile che siano stati inseriti altri servizi di Azure in tale posizione, ad esempio siti Web o risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f834d-127">You might also have put other Azure services in there, such as websites or storage.</span></span>

![Risorse in Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

<span data-ttu-id="f834d-129">risorse di toothese accesso toocontrol che è pertanto consigliabile:</span><span class="sxs-lookup"><span data-stu-id="f834d-129">toocontrol access toothese resources it's therefore recommended to:</span></span>

* <span data-ttu-id="f834d-130">Controllare l'accesso a hello **gruppo di risorse o sottoscrizione** livello.</span><span class="sxs-lookup"><span data-stu-id="f834d-130">Control access at hello **resource group or subscription** level.</span></span>
* <span data-ttu-id="f834d-131">Assegnare hello **collaboratore di componenti di Application Insights** toousers ruolo.</span><span class="sxs-lookup"><span data-stu-id="f834d-131">Assign hello **Application Insights Component contributor** role toousers.</span></span> <span data-ttu-id="f834d-132">In questo modo i test web tooedit, avvisi e le risorse di Application Insights, senza fornire accesso tooany altri servizi nel gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="f834d-132">This allows them tooedit web tests, alerts, and Application Insights resources, without providing access tooany other services in hello group.</span></span>

## <a name="tooprovide-access-tooanother-user"></a><span data-ttu-id="f834d-133">tooprovide accesso tooanother utente</span><span class="sxs-lookup"><span data-stu-id="f834d-133">tooprovide access tooanother user</span></span>
<span data-ttu-id="f834d-134">È necessario disporre di sottoscrizione toohello diritti di proprietario o il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="f834d-134">You must have Owner rights toohello subscription or hello resource group.</span></span>

<span data-ttu-id="f834d-135">Hello utente deve disporre di un [Account Microsoft][account], o accesso tootheir [Account aziendale di Microsoft](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="f834d-135">hello user must have a [Microsoft Account][account], or access tootheir [organizational Microsoft Account](../active-directory/sign-up-organization.md).</span></span> <span data-ttu-id="f834d-136">È possibile fornire accesso tooindividuals e toouser gruppi definiti in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f834d-136">You can provide access tooindividuals, and also toouser groups defined in Azure Active Directory.</span></span>

#### <a name="navigate-toohello-resource-group"></a><span data-ttu-id="f834d-137">Passare il gruppo di risorse toohello</span><span class="sxs-lookup"><span data-stu-id="f834d-137">Navigate toohello resource group</span></span>
<span data-ttu-id="f834d-138">Aggiungere hello utente non esiste.</span><span class="sxs-lookup"><span data-stu-id="f834d-138">Add hello user there.</span></span>

![Nel pannello della risorsa dell'applicazione, aprire Essentials, aprire il gruppo di risorse hello e vi selezionare impostazioni o gli utenti.](./media/app-insights-resources-roles-access-control/01-add-user.png)

<span data-ttu-id="f834d-141">Oppure è possibile passare ad un livello e aggiungere hello utente toohello sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f834d-141">Or you could go up another level and add hello user toohello Subscription.</span></span>

#### <a name="select-a-role"></a><span data-ttu-id="f834d-142">Selezionare un ruolo</span><span class="sxs-lookup"><span data-stu-id="f834d-142">Select a role</span></span>
![Selezionare un ruolo per hello nuovo utente](./media/app-insights-resources-roles-access-control/03-role.png)

| <span data-ttu-id="f834d-144">Ruolo</span><span class="sxs-lookup"><span data-stu-id="f834d-144">Role</span></span> | <span data-ttu-id="f834d-145">Nel gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="f834d-145">In hello resource group</span></span> |
| --- | --- |
| <span data-ttu-id="f834d-146">Proprietario</span><span class="sxs-lookup"><span data-stu-id="f834d-146">Owner</span></span> |<span data-ttu-id="f834d-147">È possibile modificare qualsiasi oggetto, incluso l'accesso utente</span><span class="sxs-lookup"><span data-stu-id="f834d-147">Can change anything, including user access</span></span> |
| <span data-ttu-id="f834d-148">Collaboratore</span><span class="sxs-lookup"><span data-stu-id="f834d-148">Contributor</span></span> |<span data-ttu-id="f834d-149">È possibile modificare qualsiasi oggetto, incluse tutte le risorse</span><span class="sxs-lookup"><span data-stu-id="f834d-149">Can edit anything, including all resources</span></span> |
| <span data-ttu-id="f834d-150">collaboratore componente di Application Insights </span><span class="sxs-lookup"><span data-stu-id="f834d-150">Application Insights Component contributor</span></span> |<span data-ttu-id="f834d-151">Può modificare risorse, test Web e avvisi di Application Insights</span><span class="sxs-lookup"><span data-stu-id="f834d-151">Can edit Application Insights resources, web tests and alerts</span></span> |
| <span data-ttu-id="f834d-152">Reader</span><span class="sxs-lookup"><span data-stu-id="f834d-152">Reader</span></span> |<span data-ttu-id="f834d-153">È possibile visualizzare qualsiasi oggetto ma non apportare alcuna modifica</span><span class="sxs-lookup"><span data-stu-id="f834d-153">Can view but not change anything</span></span> |

<span data-ttu-id="f834d-154">'Modifica' include la creazione, l'eliminazione e l'aggiornamento:</span><span class="sxs-lookup"><span data-stu-id="f834d-154">'Editing' includes creating, deleting and updating:</span></span>

* <span data-ttu-id="f834d-155">Risorse</span><span class="sxs-lookup"><span data-stu-id="f834d-155">Resources</span></span>
* <span data-ttu-id="f834d-156">Test Web</span><span class="sxs-lookup"><span data-stu-id="f834d-156">Web tests</span></span>
* <span data-ttu-id="f834d-157">Avvisi</span><span class="sxs-lookup"><span data-stu-id="f834d-157">Alerts</span></span>
* <span data-ttu-id="f834d-158">Esportazione continua</span><span class="sxs-lookup"><span data-stu-id="f834d-158">Continuous export</span></span>

#### <a name="select-hello-user"></a><span data-ttu-id="f834d-159">Selezionare utente hello</span><span class="sxs-lookup"><span data-stu-id="f834d-159">Select hello user</span></span>

<span data-ttu-id="f834d-160">Se non è utente hello desiderato nella directory di hello, è possibile invitare tutti gli utenti con un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f834d-160">If hello user you want isn't in hello directory, you can invite anyone with a Microsoft account.</span></span>
<span data-ttu-id="f834d-161">Se si usano servizi come Outlook.com, OneDrive, Windows Phone o XBox Live, hanno un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f834d-161">(If they use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, they have a Microsoft account.)</span></span>

## <a name="related-content"></a><span data-ttu-id="f834d-162">Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="f834d-162">Related content</span></span>

* [<span data-ttu-id="f834d-163">Controllo di accesso basato sui ruoli in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f834d-163">Role based access control in Azure</span></span>](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
