---
title: 'Azure Active Directory Domain Services: creare il gruppo di amministratori Azure AD DC | Microsoft Docs'
description: Abilitare Azure Active Directory Domain Services tramite il portale di Azure classico
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
ms.openlocfilehash: 5ed0125e05928cf0f6d9941e099b433ecb46e6e2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-classic-portal"></a><span data-ttu-id="d383f-103">Abilitare Azure Active Directory Domain Services tramite il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="d383f-103">Enable Azure Active Directory Domain Services using the Azure classic portal</span></span>
<span data-ttu-id="d383f-104">Questo articolo descrive e illustra le attività di configurazione necessarie per abilitare Azure Active Directory Domain Services (Azure AD DS) per il tenant di Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d383f-104">This article describes and walks through the configuration tasks that are required for you to enable Azure Active Directory Domain Services (Azure AD DS) for your Azure Active Directory (Azure AD) tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="d383f-105">[**Provare invece la nuova (anteprima) esperienza del portale di Azure**](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="d383f-105">[**Try the new (preview) Azure portal experience instead**](active-directory-ds-getting-started.md).</span></span> 
>

## <a name="task-1-create-the-azure-ad-dc-administrators-group"></a><span data-ttu-id="d383f-106">Attività 1: creare il gruppo di amministratori Azure AD DC</span><span class="sxs-lookup"><span data-stu-id="d383f-106">Task 1: create the Azure AD DC administrators group</span></span>
<span data-ttu-id="d383f-107">La prima attività consiste nel creare un gruppo amministrativo nel tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d383f-107">The first task is to create an administrative group in your Azure AD tenant.</span></span> <span data-ttu-id="d383f-108">Questo gruppo amministrativo speciale è chiamato *AAD DC Administrators*.</span><span class="sxs-lookup"><span data-stu-id="d383f-108">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="d383f-109">Ai membri di questo gruppo vengono concesse autorizzazioni amministrative per i computer aggiunti al dominio gestito di Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="d383f-109">Members of this group are granted administrative permissions on machines that are domain-joined to the Azure Active Directory Domain Services-managed domain.</span></span> <span data-ttu-id="d383f-110">Nei computer appartenenti a un dominio viene aggiunto al gruppo degli amministratori.</span><span class="sxs-lookup"><span data-stu-id="d383f-110">On domain-joined machines, this group is added to the administrators group.</span></span> <span data-ttu-id="d383f-111">Inoltre, i membri di questo gruppo possono usare Desktop remoto per connettersi ai computer del dominio da remoto.</span><span class="sxs-lookup"><span data-stu-id="d383f-111">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span></span>  

> [!NOTE]
> <span data-ttu-id="d383f-112">Non sarà possibile esercitare i privilegi di amministratore di dominio o amministratore dell'organizzazione all'interno del dominio gestito creato con Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="d383f-112">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="d383f-113">Nei domini gestiti questi privilegi sono riservati dal servizio e non vengono resi disponibili agli utenti all'interno del tenant.</span><span class="sxs-lookup"><span data-stu-id="d383f-113">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span></span> <span data-ttu-id="d383f-114">Per poter eseguire alcune operazioni con privilegi, sarà tuttavia possibile usare il gruppo amministrativo speciale creato in questa attività di configurazione.</span><span class="sxs-lookup"><span data-stu-id="d383f-114">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span></span> <span data-ttu-id="d383f-115">Queste operazioni prevedono l'aggiunta di computer al dominio, l'appartenenza al gruppo di amministrazione su computer aggiunti al dominio e la configurazione di Criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="d383f-115">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="d383f-116">In questa attività di configurazione verrà creato il gruppo amministrativo al quale verranno aggiunti uno o più utenti nella directory.</span><span class="sxs-lookup"><span data-stu-id="d383f-116">In this configuration task, you create the administrative group and add one or more users in your directory to the group.</span></span> <span data-ttu-id="d383f-117">Per creare il gruppo amministrativo per Azure Active Directory Domain Services, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d383f-117">To create the administrative group for Azure Active Directory Domain Services, do the following:</span></span>

1. <span data-ttu-id="d383f-118">Passare al [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d383f-118">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="d383f-119">Selezionare il pulsante **Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="d383f-119">In the left pane, select the **Active Directory** button.</span></span>
3. <span data-ttu-id="d383f-120">Selezionare il tenant (directory) di Azure AD per il quale si desidera abilitare Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="d383f-120">Select the Azure AD tenant (directory) for which you want to enable Azure Active Directory Domain Services.</span></span> <span data-ttu-id="d383f-121">È possibile creare solo un dominio per ogni directory di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d383f-121">You can create only one domain for each Azure AD directory.</span></span>

    ![Selezionare la directory di Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="d383f-123">Nella pagina di **anteprima della directory** fare clic sulla scheda **Gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d383f-123">On the **preview directory** page, click the **Groups** tab.</span></span>
5. <span data-ttu-id="d383f-124">Per aggiungere un gruppo al tenant di Azure AD fare clic su **Aggiungi gruppo** nel riquadro attività nella parte inferiore della finestra.</span><span class="sxs-lookup"><span data-stu-id="d383f-124">To add a group to your Azure AD tenant, on the task pane at the bottom of the window, click **Add Group**.</span></span>

    ![Pulsante Aggiungi gruppo](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. <span data-ttu-id="d383f-126">Nella finestra di dialogo **Aggiungi gruppo** creare un gruppo denominato **AAD DC Administrators**, quindi impostare **Tipo di gruppo** su **Sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="d383f-126">In the **Add Group** dialog box, create a group named **AAD DC Administrators**, and then set **Group Type** to **Security**.</span></span>

   > [!WARNING]
   > <span data-ttu-id="d383f-127">Per consentire l'accesso al dominio gestito di Azure Active Directory Domain Services, è necessario creare un gruppo con questo nome esatto.</span><span class="sxs-lookup"><span data-stu-id="d383f-127">To enable access within your Azure Active Directory Domain Services-managed domain, create a group with this exact name.</span></span>
   >
   >

    ![Finestra di dialogo Aggiungi gruppo](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. <span data-ttu-id="d383f-129">Nella casella **Descrizione** immettere una descrizione che consenta ad altri utenti di comprendere che questo gruppo concede autorizzazioni amministrative all'interno di Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="d383f-129">In the **Description** box, enter a description that enables others to understand that this group grants administrative permissions within Azure Active Directory Domain Services.</span></span>
8. <span data-ttu-id="d383f-130">Dopo averlo creato, fare clic sul nome del gruppo per visualizzarne le proprietà.</span><span class="sxs-lookup"><span data-stu-id="d383f-130">After you've created the group, click the group name to view its properties.</span></span>
9. <span data-ttu-id="d383f-131">Per aggiungere utenti come membri di questo gruppo fare clic sul pulsante **Aggiungi membri** nella parte inferiore della finestra.</span><span class="sxs-lookup"><span data-stu-id="d383f-131">To add users as members of the group, at the bottom of the window, click the **Add Members** button.</span></span>

    ![Pulsate Aggiungi membri gruppo](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. <span data-ttu-id="d383f-133">Nella finestra di dialogo **Aggiungi membri** selezionare gli utenti da includere in questo gruppo e fare clic sul segno di spunta in basso a destra.</span><span class="sxs-lookup"><span data-stu-id="d383f-133">In the **Add members** dialog box, select the users who should be members of this group, and then click the checkmark icon at the lower right.</span></span>

    ![Aggiungere utenti al gruppo di amministratori](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a><span data-ttu-id="d383f-135">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="d383f-135">Next step</span></span>
[<span data-ttu-id="d383f-136">Attività 2: creare o selezionare una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="d383f-136">Task 2: create or select an Azure virtual network</span></span>](active-directory-ds-getting-started-vnet.md)
