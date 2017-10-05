---
title: 'Azure Active Directory Domain Services: Introduzione | Microsoft Docs'
description: Abilitare Azure Active Directory Domain Services tramite il portale di Azure (anteprima)
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: f87bcf33d3b1eb21c7d84814e4c4086f664e293d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="da359-103">Abilitare Azure Active Directory Domain Services tramite il portale di Azure (Anteprima)</span><span class="sxs-lookup"><span data-stu-id="da359-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="da359-104">Attività 3: Configurare un gruppo amministrativo</span><span class="sxs-lookup"><span data-stu-id="da359-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="da359-105">In questa attività di configurazione si crea un gruppo amministrativo nella directory di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da359-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="da359-106">Questo gruppo amministrativo speciale è chiamato *AAD DC Administrators*.</span><span class="sxs-lookup"><span data-stu-id="da359-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="da359-107">Ai membri di questo gruppo vengono concesse autorizzazioni amministrative per i computer aggiunti al dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="da359-107">Members of this group are granted administrative permissions on machines that are domain-joined to the managed domain.</span></span> <span data-ttu-id="da359-108">Nei computer appartenenti a un dominio viene aggiunto al gruppo degli amministratori.</span><span class="sxs-lookup"><span data-stu-id="da359-108">On domain-joined machines, this group is added to the administrators group.</span></span> <span data-ttu-id="da359-109">Inoltre, i membri di questo gruppo possono usare Desktop remoto per connettersi ai computer del dominio da remoto.</span><span class="sxs-lookup"><span data-stu-id="da359-109">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="da359-110">Non sarà possibile esercitare i privilegi di amministratore di dominio o amministratore dell'organizzazione all'interno del dominio gestito creato con Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="da359-110">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="da359-111">Nei domini gestiti questi privilegi sono riservati dal servizio e non vengono resi disponibili agli utenti all'interno del tenant.</span><span class="sxs-lookup"><span data-stu-id="da359-111">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span></span> <span data-ttu-id="da359-112">Per poter eseguire alcune operazioni con privilegi, sarà tuttavia possibile usare il gruppo amministrativo speciale creato in questa attività di configurazione.</span><span class="sxs-lookup"><span data-stu-id="da359-112">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span></span> <span data-ttu-id="da359-113">Queste operazioni prevedono l'aggiunta di computer al dominio, l'appartenenza al gruppo di amministrazione su computer aggiunti al dominio e la configurazione di Criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="da359-113">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="da359-114">La procedura guidata crea automaticamente il gruppo amministrativo nella directory di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da359-114">The wizard automatically creates the administrative group in your Azure AD directory.</span></span> <span data-ttu-id="da359-115">Il gruppo viene chiamato "Amministratori di AAD DC".</span><span class="sxs-lookup"><span data-stu-id="da359-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="da359-116">Se si dispone di un gruppo esistente con questo nome nella directory di Azure AD, la procedura guidata seleziona questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="da359-116">If you have an existing group with this name in your Azure AD directory, the wizard selects this group.</span></span> <span data-ttu-id="da359-117">È possibile configurare l'appartenenza al gruppo usando la pagina **Gruppo Amministratori** della procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="da359-117">You can configure group membership using the **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="da359-118">Per configurare l'appartenenza al gruppo, fare clic su **Amministratori di AAD DC**.</span><span class="sxs-lookup"><span data-stu-id="da359-118">To configure group membership, click **AAD DC Administrators**.</span></span>

    ![Configurare l'appartenenza al gruppo](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="da359-120">Fare clic su **Aggiungi membri** per aggiungere gli utenti dalla directory di Azure AD al gruppo di amministratori.</span><span class="sxs-lookup"><span data-stu-id="da359-120">Click the **Add members** button to add users from your Azure AD directory to the administrator group.</span></span>

3. <span data-ttu-id="da359-121">Al termine, fare clic su **OK** per passare alla pagina **Riepilogo** della procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="da359-121">When you are done, click **OK** to move on to the **Summary** page of the wizard.</span></span>

4. <span data-ttu-id="da359-122">Nella pagina **Riepilogo** della procedura guidata controllare le impostazioni di configurazione per il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="da359-122">On the **Summary** page of the wizard, review the configuration settings for the managed domain.</span></span> <span data-ttu-id="da359-123">Se necessario, è possibile tornare a qualsiasi passaggio precedente della procedura guidata per eseguire le modifiche desiderate.</span><span class="sxs-lookup"><span data-stu-id="da359-123">You can go back to any step of the wizard to make changes, if necessary.</span></span> <span data-ttu-id="da359-124">Al termine, fare clic su **OK** per creare il nuovo dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="da359-124">When you are done, click **OK** to create the new managed domain.</span></span>

    ![Riepilogo](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="da359-126">Viene visualizzata una notifica che mostra lo stato di avanzamento della distribuzione di Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="da359-126">You see a notification that shows the progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="da359-127">Fare clic sulla notifica per visualizzare lo stato di avanzamento dettagliato del processo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="da359-127">Click the notification to see detailed progress for the deployment.</span></span>

    ![Notifica - Distribuzione in corso](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="da359-129">Effettuare il provisioning del dominio gestito</span><span class="sxs-lookup"><span data-stu-id="da359-129">Provision your managed domain</span></span>
<span data-ttu-id="da359-130">Il processo di provisioning del dominio gestito può richiedere fino a un'ora.</span><span class="sxs-lookup"><span data-stu-id="da359-130">The process of provisioning your managed domain can take up to an hour.</span></span>

1. <span data-ttu-id="da359-131">Mentre è in corso la distribuzione, è possibile cercare "domain services" nella casella di ricerca **Cerca risorse**.</span><span class="sxs-lookup"><span data-stu-id="da359-131">While your deployment is in progress, you can search for 'domain services' in the **Search resources** search box.</span></span> <span data-ttu-id="da359-132">Selezionare **Azure AD Domain Services** dai risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="da359-132">Select **Azure AD Domain Services** from the search result.</span></span> <span data-ttu-id="da359-133">Nel pannello **Azure AD Domain Services** viene elencato il dominio gestito di cui viene effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="da359-133">The **Azure AD Domain Services** blade lists the managed domain that is being provisioned.</span></span>

    ![Trovare il dominio gestito di cui viene effettuato il provisioning](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="da359-135">Fare clic sul nome del dominio gestito (ad esempio, "contoso100.com") per visualizzare altre informazioni sul dominio.</span><span class="sxs-lookup"><span data-stu-id="da359-135">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the domain.</span></span>

    ![Domain Services - Stato del provisioning](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="da359-137">La scheda **Panoramica** indica che il dominio è attualmente sottoposto a provisioning.</span><span class="sxs-lookup"><span data-stu-id="da359-137">The **Overview** tab shows that the domain is currently being provisioned.</span></span> <span data-ttu-id="da359-138">Non è possibile configurare il dominio gestito fino a quando non ne è stato completato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="da359-138">You cannot configure the managed domain until it is fully provisioned.</span></span> <span data-ttu-id="da359-139">Per completare il provisioning del dominio gestito può essere necessaria fino a un'ora.</span><span class="sxs-lookup"><span data-stu-id="da359-139">It may take up to an hour for your managed domain to be fully provisioned.</span></span>

    ![<span data-ttu-id="da359-140">Domain Services - Scheda Panoramica durante lo stato di provisioning</span><span class="sxs-lookup"><span data-stu-id="da359-140">Domain Services - Overview tab during the provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="da359-141">Al termine del provisioning del dominio gestito, nella scheda **Panoramica** il dominio gestito è impostato su **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="da359-141">When the managed domain is fully provisioned, the **Overview** tab shows the domain status as **Running**.</span></span>

    ![Domain Services - Scheda Panoramica al termine del provisioning](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="da359-143">Nella scheda **Proprietà** vengono visualizzati i due indirizzi IP in cui sono disponibili i controller di dominio per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="da359-143">On the **Properties** tab, you see two IP addresses at which domain controllers are available for the virtual network.</span></span>

    ![Domain Services - Scheda Proprietà al termine del provisioning](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="da359-145">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="da359-145">Next step</span></span>
[<span data-ttu-id="da359-146">Attività 4: Aggiornare le impostazioni DNS per la rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="da359-146">Task 4: update the DNS settings for the Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
