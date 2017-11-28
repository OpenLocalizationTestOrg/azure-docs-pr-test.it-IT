---
title: Risorse, ruoli e controllo di accesso in Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: c979a8bfbeecacc7c0bbc112e02a4b68e874c219
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a><span data-ttu-id="d61a2-103">Risorse, ruoli e controllo di accesso in Application Insights</span><span class="sxs-lookup"><span data-stu-id="d61a2-103">Resources, roles, and access control in Application Insights</span></span>
<span data-ttu-id="d61a2-104">È possibile controllare chi ha eseguito la lettura e aggiornare l'accesso ai dati in Azure [Application Insights][start] mediante il [controllo degli accessi in base al ruolo in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d61a2-104">You can control who has read and update access to your data in Azure [Application Insights][start], by using [Role-based access control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d61a2-105">Assegnare l'accesso agli utenti nella **sottoscrizione o nel gruppo di risorse** a cui la risorsa dell'applicazione appartiene, non nella risorsa stessa.</span><span class="sxs-lookup"><span data-stu-id="d61a2-105">Assign access to users in the **resource group or subscription** to which your application resource belongs - not in the resource itself.</span></span> <span data-ttu-id="d61a2-106">Assegnare il ruolo **collaboratore componente di Application Insights** .</span><span class="sxs-lookup"><span data-stu-id="d61a2-106">Assign the **Application Insights component contributor** role.</span></span> <span data-ttu-id="d61a2-107">In tal modo si garantisce un controllo di accesso uniforme ai test Web e agli avvisi nonché alla risorsa dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d61a2-107">This ensures uniform control of access to web tests and alerts along with your application resource.</span></span> <span data-ttu-id="d61a2-108">[Altre informazioni](#access)</span><span class="sxs-lookup"><span data-stu-id="d61a2-108">[Learn more](#access).</span></span>
> 
> 

## <a name="resources-groups-and-subscriptions"></a><span data-ttu-id="d61a2-109">Risorse, gruppi e sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="d61a2-109">Resources, groups and subscriptions</span></span>
<span data-ttu-id="d61a2-110">Innanzitutto prendere nota di alcune definizioni:</span><span class="sxs-lookup"><span data-stu-id="d61a2-110">First, some definitions:</span></span>

* <span data-ttu-id="d61a2-111">**Risorse** : un'istanza di un servizio di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d61a2-111">**Resource** - An instance of a Microsoft Azure service.</span></span> <span data-ttu-id="d61a2-112">La risorsa di Application Insights raccoglie, analizza e visualizza i dati di telemetria inviati dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d61a2-112">Your Application Insights resource collects, analyzes and displays the telemetry data sent from your application.</span></span>  <span data-ttu-id="d61a2-113">Altri tipi di risorse di Azure includono app Web, database e macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="d61a2-113">Other types of Azure resources include web apps, databases, and VMs.</span></span>
  
    <span data-ttu-id="d61a2-114">Per vedere le risorse, aprire il [portale di Azure][portal], eseguire l'accesso e fare clic su Tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="d61a2-114">To see your resources, open the [Azure Portal][portal], sign in, and click All Resources.</span></span> <span data-ttu-id="d61a2-115">Per trovare una risorsa, digitare parte del nome nel campo del filtro.</span><span class="sxs-lookup"><span data-stu-id="d61a2-115">To find a resource, type part of its name in the filter field.</span></span>
  
    ![Elenco di risorse di Azure](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* <span data-ttu-id="d61a2-117">[**Gruppo di risorse**][group]: ogni risorsa appartiene a un gruppo.</span><span class="sxs-lookup"><span data-stu-id="d61a2-117">[**Resource group**][group] - Every resource belongs to one group.</span></span> <span data-ttu-id="d61a2-118">Un gruppo è un modo pratico per gestire risorse correlate, in particolare per il controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="d61a2-118">A group is a convenient way to manage related resources, particularly for access control.</span></span> <span data-ttu-id="d61a2-119">In un gruppo di risorse, ad esempio, è possibile inserire un'app Web, una risorsa di Application Insights per monitorare l'app e una risorsa di archiviazione per conservare i dati esportati.</span><span class="sxs-lookup"><span data-stu-id="d61a2-119">For example, into one resource group you could put a Web App, an Application Insights resource to monitor the app, and a Storage resource to keep exported data.</span></span>

    ![Scegliere Sfoglia, gruppi di risorse e quindi scegliere un gruppo](./media/app-insights-resources-roles-access-control/11-group.png)

* <span data-ttu-id="d61a2-121">[**Sottoscrizione**](https://manage.windowsazure.com): per usare Application Insights o altre risorse di Azure, si accede a una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d61a2-121">[**Subscription**](https://manage.windowsazure.com) - To use Application Insights or other Azure resources, you sign in to an Azure subscription.</span></span> <span data-ttu-id="d61a2-122">Ogni gruppo di risorse appartiene a una sottoscrizione di Azure, dove si sceglie il pacchetto di prezzo e, se è la sottoscrizione di un'organizzazione, si scelgono i membri e le relative autorizzazioni di accesso.</span><span class="sxs-lookup"><span data-stu-id="d61a2-122">Every resource group belongs to one Azure subscription, where you choose your price package and, if it's an organization subscription, choose the members and their access permissions.</span></span>
* <span data-ttu-id="d61a2-123">[**Account Microsoft**][account]: il nome utente e la password usati per accedere alle sottoscrizioni di Microsoft Azure, XBox Live, Outlook.com e altri servizi Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d61a2-123">[**Microsoft account**][account] - The username and password that you use to sign in to Microsoft Azure subscriptions, XBox Live, Outlook.com, and other Microsoft services.</span></span>

## <span data-ttu-id="d61a2-124"><a name="access"></a> Controllare l'accesso nel gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="d61a2-124"><a name="access"></a> Control access in the resource group</span></span>
<span data-ttu-id="d61a2-125">È importante comprendere che oltre la risorsa creata per l'applicazione, sono disponibili anche risorse nascoste distinte per avvisi e i test Web.</span><span class="sxs-lookup"><span data-stu-id="d61a2-125">It's important to understand that in addition to the resource you created for your application, there are also separate hidden resources for alerts and web tests.</span></span> <span data-ttu-id="d61a2-126">Vengono collegati allo stesso [gruppo di risorse](#resource-group) dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d61a2-126">They are attached to the same [resource group](#resource-group) as your application.</span></span> <span data-ttu-id="d61a2-127">È anche possibile che siano stati inseriti altri servizi di Azure in tale posizione, ad esempio siti Web o risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d61a2-127">You might also have put other Azure services in there, such as websites or storage.</span></span>

![Risorse in Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

<span data-ttu-id="d61a2-129">Per controllare l'accesso a queste risorse, è quindi consigliabile:</span><span class="sxs-lookup"><span data-stu-id="d61a2-129">To control access to these resources it's therefore recommended to:</span></span>

* <span data-ttu-id="d61a2-130">Controllare l'accesso al livello della **sottoscrizione o del gruppo di risorse** .</span><span class="sxs-lookup"><span data-stu-id="d61a2-130">Control access at the **resource group or subscription** level.</span></span>
* <span data-ttu-id="d61a2-131">Assegnare il ruolo **collaboratore componente di Application Insights** agli utenti.</span><span class="sxs-lookup"><span data-stu-id="d61a2-131">Assign the **Application Insights Component contributor** role to users.</span></span> <span data-ttu-id="d61a2-132">In tal modo si consente loro di modificare i test Web, gli avvisi e le risorse di Application Insights, senza fornire l'accesso a tutti gli altri servizi del gruppo.</span><span class="sxs-lookup"><span data-stu-id="d61a2-132">This allows them to edit web tests, alerts, and Application Insights resources, without providing access to any other services in the group.</span></span>

## <a name="to-provide-access-to-another-user"></a><span data-ttu-id="d61a2-133">Per fornire l'accesso a un altro utente</span><span class="sxs-lookup"><span data-stu-id="d61a2-133">To provide access to another user</span></span>
<span data-ttu-id="d61a2-134">È necessario disporre dei diritti di proprietario per la sottoscrizione o per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="d61a2-134">You must have Owner rights to the subscription or the resource group.</span></span>

<span data-ttu-id="d61a2-135">L'utente deve avere un [account Microsoft][account] o l'accesso all'[account Microsoft aziendale](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="d61a2-135">The user must have a [Microsoft Account][account], or access to their [organizational Microsoft Account](../active-directory/sign-up-organization.md).</span></span> <span data-ttu-id="d61a2-136">È possibile fornire l'accesso a utenti e anche a gruppi di utenti definiti in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d61a2-136">You can provide access to individuals, and also to user groups defined in Azure Active Directory.</span></span>

#### <a name="navigate-to-the-resource-group"></a><span data-ttu-id="d61a2-137">Passare al gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="d61a2-137">Navigate to the resource group</span></span>
<span data-ttu-id="d61a2-138">Aggiungere l'utente da quella posizione.</span><span class="sxs-lookup"><span data-stu-id="d61a2-138">Add the user there.</span></span>

![Nel pannello di risorse dell'applicazione, aprire Essentials, aprire il gruppo di risorse e quindi selezionare Impostazioni/Utenti.](./media/app-insights-resources-roles-access-control/01-add-user.png)

<span data-ttu-id="d61a2-141">oppure è possibile spostarsi ad un altro livello e aggiungere l'utente alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d61a2-141">Or you could go up another level and add the user to the Subscription.</span></span>

#### <a name="select-a-role"></a><span data-ttu-id="d61a2-142">Selezionare un ruolo</span><span class="sxs-lookup"><span data-stu-id="d61a2-142">Select a role</span></span>
![Selezionare un ruolo per il nuovo utente](./media/app-insights-resources-roles-access-control/03-role.png)

| <span data-ttu-id="d61a2-144">Ruolo</span><span class="sxs-lookup"><span data-stu-id="d61a2-144">Role</span></span> | <span data-ttu-id="d61a2-145">Nel gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="d61a2-145">In the resource group</span></span> |
| --- | --- |
| <span data-ttu-id="d61a2-146">Proprietario</span><span class="sxs-lookup"><span data-stu-id="d61a2-146">Owner</span></span> |<span data-ttu-id="d61a2-147">È possibile modificare qualsiasi oggetto, incluso l'accesso utente</span><span class="sxs-lookup"><span data-stu-id="d61a2-147">Can change anything, including user access</span></span> |
| <span data-ttu-id="d61a2-148">Collaboratore</span><span class="sxs-lookup"><span data-stu-id="d61a2-148">Contributor</span></span> |<span data-ttu-id="d61a2-149">È possibile modificare qualsiasi oggetto, incluse tutte le risorse</span><span class="sxs-lookup"><span data-stu-id="d61a2-149">Can edit anything, including all resources</span></span> |
| <span data-ttu-id="d61a2-150">collaboratore componente di Application Insights </span><span class="sxs-lookup"><span data-stu-id="d61a2-150">Application Insights Component contributor</span></span> |<span data-ttu-id="d61a2-151">Può modificare risorse, test Web e avvisi di Application Insights</span><span class="sxs-lookup"><span data-stu-id="d61a2-151">Can edit Application Insights resources, web tests and alerts</span></span> |
| <span data-ttu-id="d61a2-152">Reader</span><span class="sxs-lookup"><span data-stu-id="d61a2-152">Reader</span></span> |<span data-ttu-id="d61a2-153">È possibile visualizzare qualsiasi oggetto ma non apportare alcuna modifica</span><span class="sxs-lookup"><span data-stu-id="d61a2-153">Can view but not change anything</span></span> |

<span data-ttu-id="d61a2-154">'Modifica' include la creazione, l'eliminazione e l'aggiornamento:</span><span class="sxs-lookup"><span data-stu-id="d61a2-154">'Editing' includes creating, deleting and updating:</span></span>

* <span data-ttu-id="d61a2-155">Risorse</span><span class="sxs-lookup"><span data-stu-id="d61a2-155">Resources</span></span>
* <span data-ttu-id="d61a2-156">Test Web</span><span class="sxs-lookup"><span data-stu-id="d61a2-156">Web tests</span></span>
* <span data-ttu-id="d61a2-157">Avvisi</span><span class="sxs-lookup"><span data-stu-id="d61a2-157">Alerts</span></span>
* <span data-ttu-id="d61a2-158">Esportazione continua</span><span class="sxs-lookup"><span data-stu-id="d61a2-158">Continuous export</span></span>

#### <a name="select-the-user"></a><span data-ttu-id="d61a2-159">Selezionare l'utente</span><span class="sxs-lookup"><span data-stu-id="d61a2-159">Select the user</span></span>

<span data-ttu-id="d61a2-160">Se l'utente desiderato non è nella directory, è possibile invitare chiunque disponga di un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d61a2-160">If the user you want isn't in the directory, you can invite anyone with a Microsoft account.</span></span>
<span data-ttu-id="d61a2-161">Se si usano servizi come Outlook.com, OneDrive, Windows Phone o XBox Live, hanno un account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d61a2-161">(If they use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, they have a Microsoft account.)</span></span>

## <a name="related-content"></a><span data-ttu-id="d61a2-162">Contenuti correlati</span><span class="sxs-lookup"><span data-stu-id="d61a2-162">Related content</span></span>

* [<span data-ttu-id="d61a2-163">Controllo di accesso basato sui ruoli in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d61a2-163">Role based access control in Azure</span></span>](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
