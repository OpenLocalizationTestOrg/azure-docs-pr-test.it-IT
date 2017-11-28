---
title: 'Azure Active Directory Domain Services: Crea gruppo di amministratori di controller di dominio hello Azure AD | Documenti Microsoft'
description: Abilitare Azure Active Directory Domain Services utilizzando hello portale di Azure classico
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
ms.date: 07/13/2017
ms.author: maheshu
ms.openlocfilehash: d629ab9632ef6a45b549630999ff9a122d60c040
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a><span data-ttu-id="f1c9a-103">Abilitare Azure Active Directory Domain Services utilizzando hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="f1c9a-103">Enable Azure Active Directory Domain Services using hello Azure classic portal</span></span>
<span data-ttu-id="f1c9a-104">Questo articolo descrive e illustra le attività di configurazione hello necessarie tooenable Azure Active Directory servizi di dominio (Azure AD DS) per il tenant di Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f1c9a-104">This article describes and walks through hello configuration tasks that are required for you tooenable Azure Active Directory Domain Services (Azure AD DS) for your Azure Active Directory (Azure AD) tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="f1c9a-105">[**Provare esperienza del portale Azure (anteprima) nuovo hello**](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="f1c9a-105">[**Try hello new (preview) Azure portal experience instead**](active-directory-ds-getting-started.md).</span></span> 
>

## <a name="task-1-create-hello-azure-ad-dc-administrators-group"></a><span data-ttu-id="f1c9a-106">Attività 1: creare gruppo di amministratori di controller di dominio hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f1c9a-106">Task 1: create hello Azure AD DC administrators group</span></span>
<span data-ttu-id="f1c9a-107">Hello prima attività è toocreate un gruppo amministrativo nel tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-107">hello first task is toocreate an administrative group in your Azure AD tenant.</span></span> <span data-ttu-id="f1c9a-108">Questo gruppo amministrativo speciale è chiamato *AAD DC Administrators*.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-108">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="f1c9a-109">Membri di questo gruppo vengono concesse le autorizzazioni amministrative nei computer che sono toohello appartenenti a un dominio gestito di Azure Active Directory Domain Services dominio.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-109">Members of this group are granted administrative permissions on machines that are domain-joined toohello Azure Active Directory Domain Services-managed domain.</span></span> <span data-ttu-id="f1c9a-110">In computer appartenenti a un dominio, questo gruppo viene aggiunto il gruppo di amministratori toohello.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-110">On domain-joined machines, this group is added toohello administrators group.</span></span> <span data-ttu-id="f1c9a-111">Inoltre, i membri di questo gruppo è possono utilizzare Desktop remoto tooconnect in modalità remota toodomain computer appartenenti a un.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-111">Additionally, members of this group can use Remote Desktop tooconnect remotely toodomain-joined machines.</span></span>  

> [!NOTE]
> <span data-ttu-id="f1c9a-112">Non si dispone delle autorizzazioni di amministratore dell'organizzazione o di amministratore di dominio nel dominio gestito hello creato tramite Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-112">You do not have Domain Administrator or Enterprise Administrator permissions on hello managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="f1c9a-113">Nei domini gestiti, queste autorizzazioni sono riservate dal servizio hello e non vengono resi disponibili toousers nel tenant di hello.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-113">On managed domains, these permissions are reserved by hello service and are not made available toousers within hello tenant.</span></span> <span data-ttu-id="f1c9a-114">Tuttavia, è possibile utilizzare gruppo amministrativo di hello speciale creato in questa tooperform di attività di configurazione alcune operazioni privilegiate.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-114">However, you can use hello special administrative group created in this configuration task tooperform some privileged operations.</span></span> <span data-ttu-id="f1c9a-115">Tali operazioni includono l'aggiunta a dominio toohello computer appartenenti toohello gruppo di amministrazione nei computer appartenenti a un dominio e la configurazione dei criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-115">These operations include joining computers toohello domain, belonging toohello administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="f1c9a-116">In questa attività di configurazione, si crea il gruppo amministrativo di hello e aggiungere uno o più utenti del gruppo toohello directory.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-116">In this configuration task, you create hello administrative group and add one or more users in your directory toohello group.</span></span> <span data-ttu-id="f1c9a-117">gruppo amministrativo di hello toocreate per Azure Active Directory Domain Services hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="f1c9a-117">toocreate hello administrative group for Azure Active Directory Domain Services, do hello following:</span></span>

1. <span data-ttu-id="f1c9a-118">Passare toohello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="f1c9a-118">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="f1c9a-119">Nel riquadro sinistro hello selezionare hello **Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-119">In hello left pane, select hello **Active Directory** button.</span></span>
3. <span data-ttu-id="f1c9a-120">Selezionare tenant di Azure AD hello (directory) per il quale si desidera tooenable Azure servizi di dominio Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-120">Select hello Azure AD tenant (directory) for which you want tooenable Azure Active Directory Domain Services.</span></span> <span data-ttu-id="f1c9a-121">È possibile creare solo un dominio per ogni directory di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-121">You can create only one domain for each Azure AD directory.</span></span>

    ![Selezionare la directory di Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="f1c9a-123">In hello **directory anteprima** pagina, fare clic su hello **gruppi** scheda.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-123">On hello **preview directory** page, click hello **Groups** tab.</span></span>
5. <span data-ttu-id="f1c9a-124">Fare clic su un tenant di Azure AD tooyour gruppo, nel riquadro attività hello nella parte inferiore di hello della finestra hello, tooadd **Aggiungi gruppo**.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-124">tooadd a group tooyour Azure AD tenant, on hello task pane at hello bottom of hello window, click **Add Group**.</span></span>

    ![pulsante Aggiungi gruppo Hello](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. <span data-ttu-id="f1c9a-126">In hello **Aggiungi gruppo** finestra di dialogo casella, creare un gruppo denominato **gli amministratori di controller di dominio di AAD**, quindi impostare **tipo di gruppo** troppo**sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-126">In hello **Add Group** dialog box, create a group named **AAD DC Administrators**, and then set **Group Type** too**Security**.</span></span>

   > [!WARNING]
   > <span data-ttu-id="f1c9a-127">accesso tooenable all'interno del dominio gestito di Azure Active Directory Domain Services, creare un gruppo con lo stesso nome.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-127">tooenable access within your Azure Active Directory Domain Services-managed domain, create a group with this exact name.</span></span>
   >
   >

    ![finestra di dialogo Aggiungi gruppo Hello](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. <span data-ttu-id="f1c9a-129">In hello **descrizione** , immettere una descrizione che consente ad altri utenti toounderstand che questo gruppo concede le autorizzazioni amministrative all'interno di servizi di dominio di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-129">In hello **Description** box, enter a description that enables others toounderstand that this group grants administrative permissions within Azure Active Directory Domain Services.</span></span>
8. <span data-ttu-id="f1c9a-130">Dopo aver creato il gruppo di hello, fare clic su tooview nome gruppo di hello le relative proprietà.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-130">After you've created hello group, click hello group name tooview its properties.</span></span>
9. <span data-ttu-id="f1c9a-131">tooadd utenti come membri del gruppo di hello, nella parte inferiore di hello della finestra hello, fare clic su hello **Aggiungi membri** pulsante.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-131">tooadd users as members of hello group, at hello bottom of hello window, click hello **Add Members** button.</span></span>

    ![Pulsate Aggiungi membri gruppo](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. <span data-ttu-id="f1c9a-133">In hello **aggiungere membri** nella finestra di dialogo hello selezionare gli utenti devono essere membri del gruppo e quindi fare clic sull'icona di segno di spunta hello in hello in basso a destra.</span><span class="sxs-lookup"><span data-stu-id="f1c9a-133">In hello **Add members** dialog box, select hello users who should be members of this group, and then click hello checkmark icon at hello lower right.</span></span>

    ![Aggiungere il gruppo di utenti tooadministrators](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a><span data-ttu-id="f1c9a-135">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="f1c9a-135">Next step</span></span>
[<span data-ttu-id="f1c9a-136">Attività 2: creare o selezionare una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="f1c9a-136">Task 2: create or select an Azure virtual network</span></span>](active-directory-ds-getting-started-vnet.md)
