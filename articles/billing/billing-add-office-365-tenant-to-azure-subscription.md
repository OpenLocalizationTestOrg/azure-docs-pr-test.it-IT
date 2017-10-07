---
title: tenant di Office 365 aaaUse con una sottoscrizione di Azure | Documenti Microsoft
description: Informazioni su come Office 365 tooadd directory (tenant) tooan sottoscrizione di Azure.
services: 
documentationcenter: 
author: JiangChen79
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: cc9c57c6-7bfd-4dea-9027-c75ef3737589
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: cjiang
ms.openlocfilehash: e560370417bd074a7e37ceb7c60da45dbbbcf775
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="associate-an-office-365-tenant-tooan-azure-subscription"></a><span data-ttu-id="12e10-103">Associare un tooan tenant di Office 365 sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="12e10-103">Associate an Office 365 tenant tooan Azure subscription</span></span>
<span data-ttu-id="12e10-104">Collegare le sottoscrizioni di Azure e Office 365 separate in modo che è possibile accedere a tenant di Office 365 hello dalla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="12e10-104">Link your separate Azure and Office 365 subscriptions so that you can access hello Office 365 tenant from your Azure subscription.</span></span> <span data-ttu-id="12e10-105">toolink delle sottoscrizioni, accedi tooAzure con hello account amministratore del servizio di Azure, aggiungere una directory e aggiungere il tenant di Azure Active Directory toohello account aziendali hello Office 365.</span><span class="sxs-lookup"><span data-stu-id="12e10-105">toolink your subscriptions, sign in tooAzure with hello Azure service administrator account, add a directory, and add hello Office 365 organizational accounts toohello Azure Active Directory tenant.</span></span>

<span data-ttu-id="12e10-106">Se si desidera una sottoscrizione di Office 365 per gli utenti nell'istanza di Azure Active Directory o si dispone di un account Office 365 ma non di un account Azure, vedere [Sign up for Azure with Office 365 account](billing-use-existing-office-365-account-azure-subscription.md) (Iscriversi ad Azure con un account Office 365).</span><span class="sxs-lookup"><span data-stu-id="12e10-106">If you want an Office 365 subscription for users in your Azure Active Directory instance or you have an Office 365 account but not an Azure account, see [Sign up for Azure with Office 365 account](billing-use-existing-office-365-account-azure-subscription.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="12e10-107">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="12e10-107">Before you begin</span></span>
* <span data-ttu-id="12e10-108">È necessario disporre delle credenziali hello dell'amministratore del servizio hello sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="12e10-108">You must have hello credentials of hello Azure subscription service administrator.</span></span> <span data-ttu-id="12e10-109">Account di coamministratore non può eseguire alcuni passaggi hello in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="12e10-109">Co-administrator accounts can't do some of hello steps in this article.</span></span> <span data-ttu-id="12e10-110">toochange l'amministratore del servizio, vedere [come tooadd o modificare i ruoli di amministratore di Azure](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span><span class="sxs-lookup"><span data-stu-id="12e10-110">toochange your service administrator, see [How tooadd or change Azure administrator roles](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span></span>
* <span data-ttu-id="12e10-111">È necessario disporre di credenziali di hello di un amministratore globale del tenant di Office 365 hello.</span><span class="sxs-lookup"><span data-stu-id="12e10-111">You must have hello credentials of a global administrator of hello Office 365 tenant.</span></span>
* <span data-ttu-id="12e10-112">indirizzo di posta elettronica Hello del messaggio per l'amministratore del servizio non deve essere nel tenant di Office 365 hello.</span><span class="sxs-lookup"><span data-stu-id="12e10-112">hello email address of hello service administrator must not be in hello Office 365 tenant.</span></span>
* <span data-ttu-id="12e10-113">indirizzo di posta elettronica Hello del messaggio per l'amministratore del servizio deve corrisponde a quello di qualsiasi amministratore globale del tenant di Office 365 hello.</span><span class="sxs-lookup"><span data-stu-id="12e10-113">hello email address of hello service administrator must not match that of any global administrator of hello Office 365 tenant.</span></span>
* <span data-ttu-id="12e10-114">Se si utilizza un indirizzo di posta elettronica che è un account Microsoft sia un account aziendale, modificare temporaneamente amministratore del servizio hello di toouse la sottoscrizione di Azure un altro account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="12e10-114">If you use an email address that is both a Microsoft account and an organizational account, temporarily change hello service administrator of your Azure subscription toouse another Microsoft account.</span></span> <span data-ttu-id="12e10-115">È possibile creare un account Microsoft in hello [pagina account Microsoft](https://signup.live.com/).</span><span class="sxs-lookup"><span data-stu-id="12e10-115">You can create a Microsoft account at hello [Microsoft account signup page](https://signup.live.com/).</span></span>

## <a name="link-office-365-tenant-tooazure-subscription"></a><span data-ttu-id="12e10-116">Collegamento sottoscrizione tooAzure tenant di Office 365</span><span class="sxs-lookup"><span data-stu-id="12e10-116">Link Office 365 tenant tooAzure subscription</span></span>
<span data-ttu-id="12e10-117">toohello tenant di Office 365 hello tooassociate sottoscrizione di Azure, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="12e10-117">tooassociate hello Office 365 tenant toohello Azure subscription, follow these steps:</span></span>

### <a name="step-1-add-office-365-tenant-tooyour-azure-subscription"></a><span data-ttu-id="12e10-118">Passaggio 1: Aggiungere tooyour tenant di Office 365 sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="12e10-118">Step 1: Add Office 365 tenant tooyour Azure subscription</span></span>

1. <span data-ttu-id="12e10-119">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com/) con le credenziali di amministratore hello.</span><span class="sxs-lookup"><span data-stu-id="12e10-119">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with hello service administrator credentials.</span></span>

    ![Screenshot dell'accesso ad Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. <span data-ttu-id="12e10-121">Nel riquadro sinistro hello selezionare **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="12e10-121">In hello left pane, select **ACTIVE DIRECTORY**.</span></span> <span data-ttu-id="12e10-122">Non deve vedrai tenant hello Office 365.</span><span class="sxs-lookup"><span data-stu-id="12e10-122">You shouldn't see hello Office 365 tenant.</span></span> <span data-ttu-id="12e10-123">Se è visibile, andare troppo[passaggio 2: impostare la directory hello associata a una sottoscrizione di Azure hello](#Step2).</span><span class="sxs-lookup"><span data-stu-id="12e10-123">If you see it, skip too[Step 2: Change hello directory associated with hello Azure subscription](#Step2).</span></span>
   
   ![Screenshot della voce di Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. <span data-ttu-id="12e10-125">Selezionare **NUOVA** > **DIRECTORY** > **CREAZIONE PERSONALIZZATA**.</span><span class="sxs-lookup"><span data-stu-id="12e10-125">Select **NEW** > **DIRECTORY** > **CUSTOM CREATE**.</span></span>
   
    ![Screenshot di Creazione personalizzata di Azure Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. <span data-ttu-id="12e10-127">In hello **Aggiungi directory** pagina **DIRECTORY**selezionare **utilizza directory esistente**.</span><span class="sxs-lookup"><span data-stu-id="12e10-127">On hello **Add directory** page, under **DIRECTORY**, select **Use existing directory**.</span></span> <span data-ttu-id="12e10-128">Selezionare quindi **sono pronti toobe uscire ora**e selezionare **completa** ![icona completare](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="12e10-128">Then select **I am ready toobe signed out now**, and select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Screenshot di "Utilizza directory esistente"](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. <span data-ttu-id="12e10-130">Dopo essere disconnessi, accedere con le credenziali dell'amministratore di hello globale del tenant Office 365.</span><span class="sxs-lookup"><span data-stu-id="12e10-130">After you are signed out, sign in with hello global administrator’s credentials of your Office 365 tenant.</span></span>
   
    ![Screenshot dell'accesso come amministratore globale di Office 365](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. <span data-ttu-id="12e10-132">Selezionare **Continua**.</span><span class="sxs-lookup"><span data-stu-id="12e10-132">Select **Continue**.</span></span>
   
    ![Screenshot della verifica](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. <span data-ttu-id="12e10-134">Selezionare **Esci ora**.</span><span class="sxs-lookup"><span data-stu-id="12e10-134">Select **Sign out now**.</span></span>
   
    ![Screenshot della disconnessione](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. <span data-ttu-id="12e10-136">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com/) con le credenziali di amministratore hello.</span><span class="sxs-lookup"><span data-stu-id="12e10-136">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with hello service administrator credentials.</span></span>
   
    ![Screenshot dell'accesso ad Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. <span data-ttu-id="12e10-138">Verrà visualizzato il tenant di Office 365 in dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="12e10-138">You should see your Office 365 tenant in hello dashboard.</span></span>
   
    ![Screenshot del dashboard](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <span data-ttu-id="12e10-140"><a name="Step2"></a>Passaggio 2: Impostare la directory hello associato hello sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="12e10-140"><a name="Step2"></a>Step 2: Change hello directory associated with hello Azure subscription</span></span>
   
1. <span data-ttu-id="12e10-141">Selezionare **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="12e10-141">Select **Settings**.</span></span>
   
    ![Screenshot dell'icona delle impostazioni del portale classico di Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. <span data-ttu-id="12e10-143">Selezionare la sottoscrizione di Azure e quindi **MODIFICA DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="12e10-143">Select your Azure subscription, and then select **EDIT DIRECTORY**.</span></span>

    ![Screenshot di Modifica directory per la sottoscrizione di Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. <span data-ttu-id="12e10-145">Selezionare **Avanti** ![icona Avanti](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span><span class="sxs-lookup"><span data-stu-id="12e10-145">Select **Next** ![Next icon](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span></span>
   
    ![Schermata di "Modifica hello associate nella directory"](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. <span data-ttu-id="12e10-147">Esaminare gli account hello interessata.</span><span class="sxs-lookup"><span data-stu-id="12e10-147">Review hello affected accounts.</span></span> <span data-ttu-id="12e10-148">Tutti i coamministratori e [controllo di accesso basato sui ruoli (RBAC)](../active-directory/role-based-access-control-configure.md) gli utenti con accesso assegnato in gruppi di risorse esistente hello vengono rimossi.</span><span class="sxs-lookup"><span data-stu-id="12e10-148">All co-administrators and [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) users with assigned access in hello existing resource groups are removed.</span></span> <span data-ttu-id="12e10-149">avviso Hello ricevuto menziona solo la rimozione di hello dei coamministratori.</span><span class="sxs-lookup"><span data-stu-id="12e10-149">hello warning you receive only mentions hello removal of co-administrators.</span></span>
      
    ![Schermata che mostra hello account coamministratore toobe rimosso.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Schermata che mostra un toobe di account utente di esempio è stato rimosso.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. <span data-ttu-id="12e10-152">Selezionare **Completa** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="12e10-152">Select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-toohello-azure-active-directory-tenant"></a><span data-ttu-id="12e10-153">Passaggio 3: Aggiungere gli account aziendali di Office 365 come tenant di Azure Active Directory toohello coamministratori</span><span class="sxs-lookup"><span data-stu-id="12e10-153">Step 3: Add your Office 365 organizational accounts as co-administrators toohello Azure Active Directory tenant</span></span>
   
1. <span data-ttu-id="12e10-154">Seleziona hello **amministratori** scheda e quindi selezionare **aggiungere**.</span><span class="sxs-lookup"><span data-stu-id="12e10-154">Select hello **ADMINISTRATORS** tab, and then select **ADD**.</span></span>
   
    ![Screenshot della scheda Amministratori relativa alle impostazioni nel portale di Azure classico](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. <span data-ttu-id="12e10-156">Immettere un account aziendale di tenant di Office 365, selezionare hello sottoscrizione di Azure, quindi **completa** ![icona completare](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="12e10-156">Enter an organizational account of your Office 365 tenant, select hello Azure subscription, and then select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Screenshot della finestra di dialogo Aggiungi coamministratore di Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. <span data-ttu-id="12e10-158">Tornare indietro toohello **amministratori** scheda. Dovrebbe essere visualizzato come co-amministratore account aziendale di hello.</span><span class="sxs-lookup"><span data-stu-id="12e10-158">Go back toohello **ADMINISTRATORS** tab. You should see hello organizational account displayed as co-administrator.</span></span>
   
    ![Screenshot della scheda Amministratori](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  <span data-ttu-id="12e10-160">Test tooAzure di accesso con account di coamministratore hello.</span><span class="sxs-lookup"><span data-stu-id="12e10-160">Test access tooAzure with hello co-administrator account.</span></span>
   
    <span data-ttu-id="12e10-161">a.</span><span class="sxs-lookup"><span data-stu-id="12e10-161">a.</span></span> <span data-ttu-id="12e10-162">Uscire da hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="12e10-162">Sign out of hello Azure classic portal.</span></span>
   
    <span data-ttu-id="12e10-163">b.</span><span class="sxs-lookup"><span data-stu-id="12e10-163">b.</span></span> <span data-ttu-id="12e10-164">Aprire hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="12e10-164">Open hello [Azure portal](https://portal.azure.com/).</span></span>
   
    <span data-ttu-id="12e10-165">c.</span><span class="sxs-lookup"><span data-stu-id="12e10-165">c.</span></span> <span data-ttu-id="12e10-166">Immettere le credenziali di hello di CO-amministratore hello e quindi selezionare **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="12e10-166">Enter hello credentials of hello co-administrator, and then select **Sign in**.</span></span>
   
    ![Screenshot della pagina di accesso di Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a><span data-ttu-id="12e10-168">Richiesta di assistenza</span><span class="sxs-lookup"><span data-stu-id="12e10-168">Need help?</span></span> <span data-ttu-id="12e10-169">Contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="12e10-169">Contact support.</span></span>
<span data-ttu-id="12e10-170">Se è ancora necessario della Guida, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.</span><span class="sxs-lookup"><span data-stu-id="12e10-170">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>


