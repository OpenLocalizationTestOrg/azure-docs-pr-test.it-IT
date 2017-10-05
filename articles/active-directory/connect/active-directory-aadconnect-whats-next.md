---
title: 'Azure AD Connect: passaggi successivi e come gestire Azure AD Connect | Microsoft Docs'
description: "Informazioni su come estendere la configurazione predefinita e attività operative per Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: beace24fa00c85a5038a3c39ae8f76af5fd12111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="next-steps-and-how-to-manage-azure-ad-connect"></a><span data-ttu-id="c12e2-103">Passaggi successivi e come gestire Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="c12e2-103">Next steps and how to manage Azure AD Connect</span></span>
<span data-ttu-id="c12e2-104">Usare le procedure operative descritte in questo articolo per personalizzare Azure Active Directory Connect al fine di soddisfare le esigenze e i requisiti dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="c12e2-104">Use the operational procedures in this article to customize Azure Active Directory (Azure AD) Connect to meet your organization's needs and requirements.</span></span>  

## <a name="add-additional-sync-admins"></a><span data-ttu-id="c12e2-105">Aggiungere altri amministratori di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="c12e2-105">Add additional sync admins</span></span>
<span data-ttu-id="c12e2-106">Per impostazione predefinita, solo l'utente che ha eseguito l'installazione e gli amministratori locali possono gestire il motore di sincronizzazione installato.</span><span class="sxs-lookup"><span data-stu-id="c12e2-106">By default, only the user who did the installation and local admins are able to manage the installed sync engine.</span></span> <span data-ttu-id="c12e2-107">Per fare in modo che altre persone possano accedere al motore di sincronizzazione e gestirlo, trovare il gruppo denominato ADSyncAdmins nel server locale e aggiungere gli utenti desiderati a questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="c12e2-107">For additional people to be able to access and manage the sync engine, locate the group named ADSyncAdmins on the local server and add them to this group.</span></span>

## <a name="assign-licenses-to-azure-ad-premium-and-enterprise-mobility-suite-users"></a><span data-ttu-id="c12e2-108">Assegnare licenze agli utenti di Azure AD Premium ed Enterprise Mobility Suite</span><span class="sxs-lookup"><span data-stu-id="c12e2-108">Assign licenses to Azure AD Premium and Enterprise Mobility Suite users</span></span>
<span data-ttu-id="c12e2-109">Dopo avere sincronizzato gli utenti nel cloud, occorre assegnare loro una licenza in modo che possano usare le app cloud come Office 365.</span><span class="sxs-lookup"><span data-stu-id="c12e2-109">Now that your users have been synchronized to the cloud, you need to assign them a license so they can get going with cloud apps such as Office 365.</span></span>

### <a name="to-assign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a><span data-ttu-id="c12e2-110">Per assegnare una licenza Azure AD Premium o Enterprise Mobility Suite</span><span class="sxs-lookup"><span data-stu-id="c12e2-110">To assign an Azure AD Premium or Enterprise Mobility Suite License</span></span>

1. <span data-ttu-id="c12e2-111">Accedere al portale di Azure come amministratore.</span><span class="sxs-lookup"><span data-stu-id="c12e2-111">Sign in to the Azure portal as an admin.</span></span>
2. <span data-ttu-id="c12e2-112">A sinistra, selezionare **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c12e2-112">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="c12e2-113">Nella pagina **Active Directory** fare doppio clic sulla directory con gli utenti da configurare.</span><span class="sxs-lookup"><span data-stu-id="c12e2-113">On the **Active Directory** page, double-click the directory that has the users you want to set up.</span></span>
4. <span data-ttu-id="c12e2-114">Nella parte superiore della pagina della directory selezionare **Licenses**.</span><span class="sxs-lookup"><span data-stu-id="c12e2-114">At the top of the directory page, select **Licenses**.</span></span>
5. <span data-ttu-id="c12e2-115">Nella pagina **Licenze** selezionare **Active Directory Premium** o **Enterprise Mobility Suite** e quindi fare clic su **Assegna**.</span><span class="sxs-lookup"><span data-stu-id="c12e2-115">On the **Licenses** page, select **Active Directory Premium** or **Enterprise Mobility Suite**, and then click **Assign**.</span></span>
6. <span data-ttu-id="c12e2-116">Nella finestra di dialogo selezionare gli utenti a cui assegnare le licenze, quindi fare clic sull'icona con il segno di spunta per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="c12e2-116">In the dialog box, select the users you want to assign licenses to, and then click the check mark icon to save the changes.</span></span>

## <a name="verify-the-scheduled-synchronization-task"></a><span data-ttu-id="c12e2-117">Verificare l'attività di sincronizzazione pianificata</span><span class="sxs-lookup"><span data-stu-id="c12e2-117">Verify the scheduled synchronization task</span></span>
<span data-ttu-id="c12e2-118">Usare il portale di Azure per controllare lo stato di una sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="c12e2-118">Use the Azure portal to check the status of a synchronization.</span></span>

### <a name="to-verify-the-scheduled-synchronization-task"></a><span data-ttu-id="c12e2-119">Per verificare l'attività di sincronizzazione pianificata</span><span class="sxs-lookup"><span data-stu-id="c12e2-119">To verify the scheduled synchronization task</span></span>
1. <span data-ttu-id="c12e2-120">Accedere al portale di Azure come amministratore.</span><span class="sxs-lookup"><span data-stu-id="c12e2-120">Sign in to the Azure portal as an admin.</span></span>
2. <span data-ttu-id="c12e2-121">A sinistra, selezionare **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c12e2-121">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="c12e2-122">Nella pagina **Active Directory** fare doppio clic sulla directory con gli utenti da configurare.</span><span class="sxs-lookup"><span data-stu-id="c12e2-122">On the **Active Directory** page, double-click the directory that has the users you want to set up.</span></span>
4. <span data-ttu-id="c12e2-123">Nella parte superiore della pagina della directory selezionare **Integrazione directory**.</span><span class="sxs-lookup"><span data-stu-id="c12e2-123">At the top of the directory page, select **Directory Integration**.</span></span>
5. <span data-ttu-id="c12e2-124">Nella sezione **integration with local active directory** (integrazione con Active Directory locale) prendere nota dell'ora dell'ultima sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="c12e2-124">Under **integration with local active directory**, note the last sync time.</span></span>

<span data-ttu-id="c12e2-125"><center>![Ora sincronizzazione directory](./media/active-directory-aadconnect-whats-next/verify.png)</center></span><span class="sxs-lookup"><span data-stu-id="c12e2-125"><center>![Directory sync time](./media/active-directory-aadconnect-whats-next/verify.png)</center></span></span>

## <a name="start-a-scheduled-synchronization-task"></a><span data-ttu-id="c12e2-126">Avviare un'attività di sincronizzazione pianificata</span><span class="sxs-lookup"><span data-stu-id="c12e2-126">Start a scheduled synchronization task</span></span>
<span data-ttu-id="c12e2-127">Se è necessario eseguire un'attività di sincronizzazione, è possibile eseguire nuovamente la procedura guidata di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c12e2-127">If you need to run a synchronization task, you can do this by running through the Azure AD Connect wizard again.</span></span>  <span data-ttu-id="c12e2-128">È necessario fornire le credenziali di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c12e2-128">You need to provide your Azure AD credentials.</span></span>  <span data-ttu-id="c12e2-129">Nella procedura guidata selezionare l'attività **Personalizzazione delle opzioni di sincronizzazione** e fare clic su **Avanti** nella procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="c12e2-129">In the wizard, select the **Customize synchronization options** task, and click **Next** to move through the wizard.</span></span> <span data-ttu-id="c12e2-130">Al termine, verificare che la casella **Avviare il processo di sincronizzazione non appena viene completata la configurazione iniziale.** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="c12e2-130">At the end, ensure that the **Start the synchronization process as soon as the initial configuration completes** box is selected.</span></span>

<span data-ttu-id="c12e2-131"><center>![Avviare la sincronizzazione](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span><span class="sxs-lookup"><span data-stu-id="c12e2-131"><center>![Start synchronization](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span></span>

<span data-ttu-id="c12e2-132">Per altre informazioni sull'utilità di pianificazione della sincronizzazione di Azure AD Connect, vedere [Utilità di pianificazione di Azure AD Connect](active-directory-aadconnectsync-feature-scheduler.md).</span><span class="sxs-lookup"><span data-stu-id="c12e2-132">For more information on the Azure AD Connect sync Scheduler, see [Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

## <a name="additional-tasks-available-in-azure-ad-connect"></a><span data-ttu-id="c12e2-133">Attività aggiuntive disponibili in Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="c12e2-133">Additional tasks available in Azure AD Connect</span></span>
<span data-ttu-id="c12e2-134">Dopo l'installazione iniziale di Azure AD Connect è sempre possibile riavviare la procedura guidata dalla pagina iniziale di Azure AD Connect o dal collegamento sul dekstop.</span><span class="sxs-lookup"><span data-stu-id="c12e2-134">After your initial installation of Azure AD Connect, you can always start the wizard again from the Azure AD Connect start page or desktop shortcut.</span></span>  <span data-ttu-id="c12e2-135">Si noterà che la riesecuzione della procedura guidata fornisce alcune nuove opzioni sotto forma di Attività aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="c12e2-135">You will notice that going through the wizard again provides some new options in the form of additional tasks.</span></span>  

<span data-ttu-id="c12e2-136">La tabella seguente include un riepilogo di tali attività e una breve descrizione di ognuna di esse.</span><span class="sxs-lookup"><span data-stu-id="c12e2-136">The following table provides a summary of these tasks and a brief description of each task.</span></span>

![Elenco delle attività aggiuntive](./media/active-directory-aadconnect-whats-next/addtasks.png)

| <span data-ttu-id="c12e2-138">Attività aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c12e2-138">Additional task</span></span> | <span data-ttu-id="c12e2-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c12e2-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c12e2-140">**Visualizza lo scenario selezionato**</span><span class="sxs-lookup"><span data-stu-id="c12e2-140">**View the selected scenario**</span></span> |<span data-ttu-id="c12e2-141">Consente di visualizzare la soluzione Azure AD Connect corrente.</span><span class="sxs-lookup"><span data-stu-id="c12e2-141">View your current Azure AD Connect solution.</span></span>  <span data-ttu-id="c12e2-142">Include impostazioni generali, directory sincronizzate e impostazioni di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="c12e2-142">This includes general settings, synchronized directories, and sync settings.</span></span> |
| <span data-ttu-id="c12e2-143">**Personalizzazione delle opzioni di sincronizzazione**</span><span class="sxs-lookup"><span data-stu-id="c12e2-143">**Customize synchronization options**</span></span> |<span data-ttu-id="c12e2-144">Consente di modificare la configurazione corrente, come l'aggiunta di altre foreste di Active Directory alla configurazione o l'attivazione di opzioni di sincronizzazione, ad esempio writeback di utenti, gruppi, dispositivi o password.</span><span class="sxs-lookup"><span data-stu-id="c12e2-144">Change the current configuration like adding additional Active Directory forests to the configuration, or enabling sync options such as user, group, device, or password write-back.</span></span> |
| <span data-ttu-id="c12e2-145">**Abilitazione modalità di gestione temporanea**</span><span class="sxs-lookup"><span data-stu-id="c12e2-145">**Enable Staging Mode**</span></span> |<span data-ttu-id="c12e2-146">Informazioni relative alla gestione temporanea non vengono sincronizzate immediatamente e non vengono esportate in Azure AD o in Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="c12e2-146">Stage information that is not immediately synchronized and is not exported to Azure AD or on-premises Active Directory.</span></span>  <span data-ttu-id="c12e2-147">Con questa funzionalità è possibile visualizzare in anteprima le sincronizzazioni prima che si verifichino.</span><span class="sxs-lookup"><span data-stu-id="c12e2-147">With this feature, you can preview the synchronizations before they occur.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c12e2-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c12e2-148">Next steps</span></span>
<span data-ttu-id="c12e2-149">Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="c12e2-149">Learn more about [integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
