---
title: aaaGet avviato con l'accesso condizionale in Azure Active Directory | Documenti Microsoft
description: "Verificare l'accesso condizionale usando una condizione della località."
services: active-directory
keywords: accesso condizionale tooapps, l'accesso condizionale con Azure AD, proteggere l'accesso alle risorse toocompany, criteri di accesso condizionale
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4521f5a34f5882e026f5e58a7127d8c55cba2f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a><span data-ttu-id="e04ae-104">Introduzione all'accesso condizionale in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e04ae-104">Get started with conditional access in Azure Active Directory</span></span>

<span data-ttu-id="e04ae-105">Accesso condizionale è una funzionalità di Azure Active Directory che consente di toodefine condizioni in cui gli utenti autorizzati possono accedere le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="e04ae-105">Conditional access is a capability of Azure Active Directory that enables you toodefine conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="e04ae-106">Questo argomento fornisce istruzioni per testare un accesso condizionale in base a una condizione della località nell'ambiente usato.</span><span class="sxs-lookup"><span data-stu-id="e04ae-106">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="e04ae-107">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="e04ae-107">Scenario description</span></span>

<span data-ttu-id="e04ae-108">Un requisito comune in molte organizzazioni è tooonly richiedono l'autenticazione a più fattori per tooapps di accesso che non viene eseguita dalla rete intranet aziendale hello.</span><span class="sxs-lookup"><span data-stu-id="e04ae-108">One common requirement in many organizations is tooonly require multi-factor authentication for access tooapps that is not performed from hello corporate intranet.</span></span> <span data-ttu-id="e04ae-109">Azure Active Directory permette di ottenere facilmente questo risultato mediante la configurazione di criteri di accesso condizionale basati sulla località.</span><span class="sxs-lookup"><span data-stu-id="e04ae-109">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="e04ae-110">Questo argomento fornisce istruzioni dettagliate per la configurazione di criteri correlati,</span><span class="sxs-lookup"><span data-stu-id="e04ae-110">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="e04ae-111">si basa su criteri Hello [gli indirizzi IP attendibili](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish tra i tentativi di accesso da hello aziendale della rete intranet e tutti gli altri percorsi.</span><span class="sxs-lookup"><span data-stu-id="e04ae-111">hello policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish between access attempts made from hello corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e04ae-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e04ae-112">Prerequisites</span></span>

<span data-ttu-id="e04ae-113">Hello scenario descritto in questo argomento si presuppone che si ha familiarità con concetti hello descritti nella [accesso condizionale di Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e04ae-113">hello scenario outlined in this topic assumes that you are familiar with hello concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="e04ae-114">tootest questo scenario, è necessario:</span><span class="sxs-lookup"><span data-stu-id="e04ae-114">tootest this scenario, you need to:</span></span>

- <span data-ttu-id="e04ae-115">Creare un utente test.</span><span class="sxs-lookup"><span data-stu-id="e04ae-115">Create a test user</span></span> 

- <span data-ttu-id="e04ae-116">Assegnare un utente di test toohello licenza Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="e04ae-116">Assign an Azure AD Premium license toohello test user</span></span>

- <span data-ttu-id="e04ae-117">Configurare un'app gestita e assegnare il tooit utente test</span><span class="sxs-lookup"><span data-stu-id="e04ae-117">Configure a managed app and assign your test user tooit</span></span>

- <span data-ttu-id="e04ae-118">Configurare indirizzi IP attendibili.</span><span class="sxs-lookup"><span data-stu-id="e04ae-118">Configure trusted IPs</span></span>

<span data-ttu-id="e04ae-119">Per altre informazioni sull'argomento, vedere [Indirizzi IP attendibili](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="e04ae-119">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="e04ae-120">Procedura di configurazione dei criteri</span><span class="sxs-lookup"><span data-stu-id="e04ae-120">Policy configuration steps</span></span>

<span data-ttu-id="e04ae-121">**tooconfigure i criteri di accesso condizionale, eseguire:**</span><span class="sxs-lookup"><span data-stu-id="e04ae-121">**tooconfigure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="e04ae-122">Nel portale di Azure nella barra di spostamento sinistro hello, hello fare clic su **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-122">In hello Azure portal, on hello left navbar, click **Azure Active Directory**.</span></span> 

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="e04ae-124">In hello **Azure Active Directory** pannello in hello **Gestisci** fare clic su **accesso condizionale**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-124">On hello **Azure Active Directory** blade, in hello **Manage** section, click **Conditional access**.</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="e04ae-126">In hello **accesso condizionale** blade, hello tooopen **New** pannello, nella barra degli strumenti hello nella parte superiore di hello, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-126">On hello **Conditional Access** blade, tooopen hello **New** blade, in hello toolbar on hello top, click **Add**.</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="e04ae-128">In hello **New** pannello in hello **nome** casella di testo, digitare un nome per il criterio.</span><span class="sxs-lookup"><span data-stu-id="e04ae-128">On hello **New** blade, in hello **Name** textbox, type a name for your policy.</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="e04ae-130">In hello **assegnazione** fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-130">In hello **Assignment** section, click **Users and groups**.</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="e04ae-132">In hello **utenti e gruppi** pannello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e04ae-132">On hello **Users and groups** blade, perform hello following steps:</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="e04ae-134">a.</span><span class="sxs-lookup"><span data-stu-id="e04ae-134">a.</span></span> <span data-ttu-id="e04ae-135">Fare clic su **Seleziona utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-135">Click **Select users and groups**.</span></span>

    <span data-ttu-id="e04ae-136">b.</span><span class="sxs-lookup"><span data-stu-id="e04ae-136">b.</span></span> <span data-ttu-id="e04ae-137">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-137">Click **Select**.</span></span>

    <span data-ttu-id="e04ae-138">c.</span><span class="sxs-lookup"><span data-stu-id="e04ae-138">c.</span></span> <span data-ttu-id="e04ae-139">In hello **selezionare** pannello, selezionare l'utente test e quindi fare clic su **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-139">On hello **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="e04ae-140">d.</span><span class="sxs-lookup"><span data-stu-id="e04ae-140">d.</span></span> <span data-ttu-id="e04ae-141">In hello **utenti e gruppi** pannello, fare clic su **eseguita**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-141">On hello **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="e04ae-142">In hello **New** blade, hello tooopen **App Cloud** pannello in hello **assegnazione** fare clic su **App Cloud**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-142">On hello **New** blade, tooopen hello **Cloud apps** blade, in hello **Assignment** section, click **Cloud apps**.</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="e04ae-144">In hello **App Cloud** pannello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e04ae-144">On hello **Cloud apps** blade, perform hello following steps:</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="e04ae-146">a.</span><span class="sxs-lookup"><span data-stu-id="e04ae-146">a.</span></span> <span data-ttu-id="e04ae-147">Fare clic su **Selezionare le app**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-147">Click **Select apps**.</span></span>

    <span data-ttu-id="e04ae-148">b.</span><span class="sxs-lookup"><span data-stu-id="e04ae-148">b.</span></span> <span data-ttu-id="e04ae-149">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-149">Click **Select**.</span></span>

    <span data-ttu-id="e04ae-150">c.</span><span class="sxs-lookup"><span data-stu-id="e04ae-150">c.</span></span> <span data-ttu-id="e04ae-151">In hello **selezionare** pannello, selezionare l'applicazione cloud e quindi fare clic su **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-151">On hello **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="e04ae-152">d.</span><span class="sxs-lookup"><span data-stu-id="e04ae-152">d.</span></span> <span data-ttu-id="e04ae-153">In hello **App Cloud** pannello, fare clic su **eseguita**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-153">On hello **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="e04ae-154">In hello **New** blade, hello tooopen **condizioni** pannello in hello **assegnazione** fare clic su **condizioni**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-154">On hello **New** blade, tooopen hello **Conditions** blade, in hello **Assignment** section, click **Conditions**.</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="e04ae-156">In hello **condizioni** blade, hello tooopen **percorsi** pannello, fare clic su **percorsi**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-156">On hello **Conditions** blade, tooopen hello **Locations** blade, click **Locations**.</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="e04ae-158">In hello **percorsi** pannello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e04ae-158">On hello **Locations** blade, perform hello following steps:</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="e04ae-160">a.</span><span class="sxs-lookup"><span data-stu-id="e04ae-160">a.</span></span> <span data-ttu-id="e04ae-161">In **Configura** fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-161">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="e04ae-162">b.</span><span class="sxs-lookup"><span data-stu-id="e04ae-162">b.</span></span> <span data-ttu-id="e04ae-163">In **Includi** fare clic su **Tutte le località**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-163">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="e04ae-164">c.</span><span class="sxs-lookup"><span data-stu-id="e04ae-164">c.</span></span> <span data-ttu-id="e04ae-165">Fare clic su **Escludi** e quindi su **Tutti gli indirizzi IP attendibili**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-165">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="e04ae-167">d.</span><span class="sxs-lookup"><span data-stu-id="e04ae-167">d.</span></span> <span data-ttu-id="e04ae-168">Fare clic su **Done**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-168">Click **Done**.</span></span>

12. <span data-ttu-id="e04ae-169">In hello **condizioni** pannello, fare clic su **eseguita**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-169">On hello **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="e04ae-170">In hello **New** blade, hello tooopen **Grant** pannello in hello **controlli** fare clic su **Grant**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-170">On hello **New** blade, tooopen hello **Grant** blade, in hello **Controls** section, click **Grant**.</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="e04ae-172">In hello **Grant** pannello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e04ae-172">On hello **Grant** blade, perform hello following steps:</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="e04ae-174">a.</span><span class="sxs-lookup"><span data-stu-id="e04ae-174">a.</span></span> <span data-ttu-id="e04ae-175">Selezionare **Richiedi autenticazione a più fattori**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-175">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="e04ae-176">b.</span><span class="sxs-lookup"><span data-stu-id="e04ae-176">b.</span></span> <span data-ttu-id="e04ae-177">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-177">Click **Select**.</span></span>

15. <span data-ttu-id="e04ae-178">In hello **New** pannello, in **abilitare i criteri di**, fare clic su **su**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-178">On hello **New** blade, under **Enable policy**, click **On**.</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="e04ae-180">In hello **New** pannello, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="e04ae-180">On hello **New** blade, click **Create**.</span></span>


## <a name="testing-hello-policy"></a><span data-ttu-id="e04ae-181">Criteri di test hello</span><span class="sxs-lookup"><span data-stu-id="e04ae-181">Testing hello policy</span></span>

<span data-ttu-id="e04ae-182">tootest dei criteri, è necessario accedere all'app da un dispositivo che:</span><span class="sxs-lookup"><span data-stu-id="e04ae-182">tootest your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="e04ae-183">Accedere all'app da un dispositivo con un indirizzo IP compreso nell'intervallo di indirizzi IP attendibili configurato.</span><span class="sxs-lookup"><span data-stu-id="e04ae-183">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="e04ae-184">Accedere all'app da un dispositivo con un indirizzo IP non compreso nell'intervallo di indirizzi IP attendibili configurato.</span><span class="sxs-lookup"><span data-stu-id="e04ae-184">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="e04ae-185">L'autenticazione a più fattori deve essere necessaria solo durante il tentativo di connessione da un dispositivo con un indirizzo IP non compreso nell'intervallo di indirizzi attendibili.</span><span class="sxs-lookup"><span data-stu-id="e04ae-185">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="e04ae-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e04ae-186">Next steps</span></span>

<span data-ttu-id="e04ae-187">Se si desidera toolearn ulteriori informazioni sull'accesso condizionale, vedere [accesso condizionale di Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e04ae-187">If you would like toolearn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

