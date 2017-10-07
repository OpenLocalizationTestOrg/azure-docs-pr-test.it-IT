---
title: 'Azure Active Directory Domain Services: Introduzione | Microsoft Docs'
description: Abilitare Azure Active Directory Domain Services utilizzando hello del portale di Azure (anteprima)
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
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="6d0d4-103">Abilitare Azure Active Directory Domain Services utilizzando hello del portale di Azure (anteprima)</span><span class="sxs-lookup"><span data-stu-id="6d0d4-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="6d0d4-104">Attività 3: Configurare un gruppo amministrativo</span><span class="sxs-lookup"><span data-stu-id="6d0d4-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="6d0d4-105">In questa attività di configurazione si crea un gruppo amministrativo nella directory di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="6d0d4-106">Questo gruppo amministrativo speciale è chiamato *AAD DC Administrators*.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="6d0d4-107">Membri di questo gruppo vengono concesse le autorizzazioni amministrative nei computer di dominio gestiti toohello appartenenti a un dominio.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-107">Members of this group are granted administrative permissions on machines that are domain-joined toohello managed domain.</span></span> <span data-ttu-id="6d0d4-108">In computer appartenenti a un dominio, questo gruppo viene aggiunto il gruppo di amministratori toohello.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-108">On domain-joined machines, this group is added toohello administrators group.</span></span> <span data-ttu-id="6d0d4-109">Inoltre, i membri di questo gruppo è possono utilizzare Desktop remoto tooconnect in modalità remota toodomain computer appartenenti a un.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-109">Additionally, members of this group can use Remote Desktop tooconnect remotely toodomain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="6d0d4-110">Non si dispone delle autorizzazioni di amministratore dell'organizzazione o di amministratore di dominio nel dominio gestito hello creato tramite Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-110">You do not have Domain Administrator or Enterprise Administrator permissions on hello managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="6d0d4-111">Nei domini gestiti, queste autorizzazioni sono riservate dal servizio hello e non vengono resi disponibili toousers nel tenant di hello.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-111">On managed domains, these permissions are reserved by hello service and are not made available toousers within hello tenant.</span></span> <span data-ttu-id="6d0d4-112">Tuttavia, è possibile utilizzare gruppo amministrativo di hello speciale creato in questa tooperform di attività di configurazione alcune operazioni privilegiate.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-112">However, you can use hello special administrative group created in this configuration task tooperform some privileged operations.</span></span> <span data-ttu-id="6d0d4-113">Tali operazioni includono l'aggiunta a dominio toohello computer appartenenti toohello gruppo di amministrazione nei computer appartenenti a un dominio e la configurazione dei criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-113">These operations include joining computers toohello domain, belonging toohello administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="6d0d4-114">procedura guidata di Hello crea automaticamente il gruppo amministrativo di hello nella directory di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-114">hello wizard automatically creates hello administrative group in your Azure AD directory.</span></span> <span data-ttu-id="6d0d4-115">Il gruppo viene chiamato "Amministratori di AAD DC".</span><span class="sxs-lookup"><span data-stu-id="6d0d4-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="6d0d4-116">Se si dispone di un gruppo esistente con lo stesso nome nella directory di Azure AD, la procedura guidata hello seleziona questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-116">If you have an existing group with this name in your Azure AD directory, hello wizard selects this group.</span></span> <span data-ttu-id="6d0d4-117">È possibile configurare l'appartenenza al gruppo usando hello **gruppo amministratore** pagina della procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-117">You can configure group membership using hello **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="6d0d4-118">l'appartenenza al gruppo tooconfigure, fare clic su **gli amministratori di controller di dominio di AAD**.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-118">tooconfigure group membership, click **AAD DC Administrators**.</span></span>

    ![Configurare l'appartenenza al gruppo](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="6d0d4-120">Fare clic su hello **aggiungere membri** pulsante tooadd gli utenti del gruppo dell'amministratore toohello directory Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-120">Click hello **Add members** button tooadd users from your Azure AD directory toohello administrator group.</span></span>

3. <span data-ttu-id="6d0d4-121">Al termine, fare clic su **OK** toomove su toohello **riepilogo** pagina della procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-121">When you are done, click **OK** toomove on toohello **Summary** page of hello wizard.</span></span>

4. <span data-ttu-id="6d0d4-122">In hello **riepilogo** pagina della procedura guidata hello, rivedere le impostazioni di configurazione di hello per il dominio gestito hello.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-122">On hello **Summary** page of hello wizard, review hello configuration settings for hello managed domain.</span></span> <span data-ttu-id="6d0d4-123">È possibile tornare tooany passaggio delle modifiche di toomake hello procedura guidata, se necessario.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-123">You can go back tooany step of hello wizard toomake changes, if necessary.</span></span> <span data-ttu-id="6d0d4-124">Al termine, fare clic su **OK** toocreate hello gestiti nuovo dominio.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-124">When you are done, click **OK** toocreate hello new managed domain.</span></span>

    ![Riepilogo](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="6d0d4-126">Viene visualizzata una notifica che mostra lo stato di avanzamento hello della distribuzione di servizi di dominio Active Directory di Azure.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-126">You see a notification that shows hello progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="6d0d4-127">Fare clic su notifica hello toosee dettagliate per la distribuzione di hello lo stato di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-127">Click hello notification toosee detailed progress for hello deployment.</span></span>

    ![Notifica - Distribuzione in corso](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="6d0d4-129">Effettuare il provisioning del dominio gestito</span><span class="sxs-lookup"><span data-stu-id="6d0d4-129">Provision your managed domain</span></span>
<span data-ttu-id="6d0d4-130">Hello processo di provisioning del dominio gestito può richiedere tooan ora.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-130">hello process of provisioning your managed domain can take up tooan hour.</span></span>

1. <span data-ttu-id="6d0d4-131">Durante la distribuzione è in corso, è possibile cercare "servizi di dominio' in hello **individuare risorse** casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-131">While your deployment is in progress, you can search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="6d0d4-132">Selezionare **servizi di dominio Active Directory di Azure** dai risultati di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-132">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="6d0d4-133">Hello **servizi di dominio Active Directory di Azure** pannello elenca hello un dominio gestito che viene eseguito il provisioning.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-133">hello **Azure AD Domain Services** blade lists hello managed domain that is being provisioned.</span></span>

    ![Trovare il dominio gestito di cui viene effettuato il provisioning](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="6d0d4-135">Fare clic su nome hello di hello gestito dominio (ad esempio, ' contoso100.com') toosee ulteriori dettagli su dominio hello.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-135">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Domain Services - Stato del provisioning](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="6d0d4-137">Hello **Panoramica** scheda Mostra il dominio hello è attualmente in corso il provisioning.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-137">hello **Overview** tab shows that hello domain is currently being provisioned.</span></span> <span data-ttu-id="6d0d4-138">È possibile configurare dominio gestito hello fino a quando non è completamente disponibile.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-138">You cannot configure hello managed domain until it is fully provisioned.</span></span> <span data-ttu-id="6d0d4-139">Potrebbe richiedere fino a ora tooan per toobe il dominio gestito eseguito il provisioning completo.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-139">It may take up tooan hour for your managed domain toobe fully provisioned.</span></span>

    ![<span data-ttu-id="6d0d4-140">Servizi di dominio - scheda Panoramica durante hello lo stato di provisioning</span><span class="sxs-lookup"><span data-stu-id="6d0d4-140">Domain Services - Overview tab during hello provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="6d0d4-141">Quando è stato effettuato il provisioning dominio gestito hello, hello **Panoramica** scheda Mostra stato dominio hello come **esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-141">When hello managed domain is fully provisioned, hello **Overview** tab shows hello domain status as **Running**.</span></span>

    ![Domain Services - Scheda Panoramica al termine del provisioning](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="6d0d4-143">In hello **proprietà** scheda, viene visualizzato due indirizzi IP del dominio sono disponibili per la rete virtuale hello controller.</span><span class="sxs-lookup"><span data-stu-id="6d0d4-143">On hello **Properties** tab, you see two IP addresses at which domain controllers are available for hello virtual network.</span></span>

    ![Domain Services - Scheda Proprietà al termine del provisioning](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="6d0d4-145">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="6d0d4-145">Next step</span></span>
[<span data-ttu-id="6d0d4-146">Attività 4: aggiornare le impostazioni DNS di hello per hello rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="6d0d4-146">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
