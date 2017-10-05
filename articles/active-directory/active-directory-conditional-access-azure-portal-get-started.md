---
title: Introduzione all'accesso condizionale in Azure Active Directory | Microsoft Docs
description: "Verificare l'accesso condizionale usando una condizione della località."
services: active-directory
keywords: accesso condizionale alle app, accesso condizionale con Azure AD, accesso sicuro alle risorse aziendali, criteri di accesso condizionale
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
ms.openlocfilehash: cd53e8be32d1e98aaf9f72177895871dba69df86
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a><span data-ttu-id="16d94-104">Introduzione all'accesso condizionale in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="16d94-104">Get started with conditional access in Azure Active Directory</span></span>

<span data-ttu-id="16d94-105">L'accesso condizionale è una funzionalità di Azure Active Directory che consente di definire le condizioni in base alle quali gli utenti autorizzati possono accedere alle app.</span><span class="sxs-lookup"><span data-stu-id="16d94-105">Conditional access is a capability of Azure Active Directory that enables you to define conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="16d94-106">Questo argomento fornisce istruzioni per testare un accesso condizionale in base a una condizione della località nell'ambiente usato.</span><span class="sxs-lookup"><span data-stu-id="16d94-106">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="16d94-107">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="16d94-107">Scenario description</span></span>

<span data-ttu-id="16d94-108">In molte organizzazioni è necessaria solo l'autenticazione a più fattori per l'accesso alle app che non viene eseguito dalla Intranet aziendale.</span><span class="sxs-lookup"><span data-stu-id="16d94-108">One common requirement in many organizations is to only require multi-factor authentication for access to apps that is not performed from the corporate intranet.</span></span> <span data-ttu-id="16d94-109">Azure Active Directory permette di ottenere facilmente questo risultato mediante la configurazione di criteri di accesso condizionale basati sulla località.</span><span class="sxs-lookup"><span data-stu-id="16d94-109">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="16d94-110">Questo argomento fornisce istruzioni dettagliate per la configurazione di criteri correlati,</span><span class="sxs-lookup"><span data-stu-id="16d94-110">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="16d94-111">che fanno uso di [indirizzi IP attendibili](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) per distinguere tra i tentativi di accesso eseguiti dalla Intranet aziendale e da tutte le altre località.</span><span class="sxs-lookup"><span data-stu-id="16d94-111">The policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) to distinguish between access attempts made from the corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="16d94-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="16d94-112">Prerequisites</span></span>

<span data-ttu-id="16d94-113">Lo scenario descritto in questo argomento presuppone che si abbia familiarità con i concetti illustrati in [Accesso condizionale in Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="16d94-113">The scenario outlined in this topic assumes that you are familiar with the concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="16d94-114">Per testare questo scenario, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="16d94-114">To test this scenario, you need to:</span></span>

- <span data-ttu-id="16d94-115">Creare un utente test.</span><span class="sxs-lookup"><span data-stu-id="16d94-115">Create a test user</span></span> 

- <span data-ttu-id="16d94-116">Assegnare una licenza Azure AD Premium all'utente test.</span><span class="sxs-lookup"><span data-stu-id="16d94-116">Assign an Azure AD Premium license to the test user</span></span>

- <span data-ttu-id="16d94-117">Configurare un'app gestita e assegnarle l'utente test.</span><span class="sxs-lookup"><span data-stu-id="16d94-117">Configure a managed app and assign your test user to it</span></span>

- <span data-ttu-id="16d94-118">Configurare indirizzi IP attendibili.</span><span class="sxs-lookup"><span data-stu-id="16d94-118">Configure trusted IPs</span></span>

<span data-ttu-id="16d94-119">Per altre informazioni sull'argomento, vedere [Indirizzi IP attendibili](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="16d94-119">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="16d94-120">Procedura di configurazione dei criteri</span><span class="sxs-lookup"><span data-stu-id="16d94-120">Policy configuration steps</span></span>

<span data-ttu-id="16d94-121">**Per configurare i criteri di accesso condizionale, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="16d94-121">**To configure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="16d94-122">Sulla barra di spostamento a sinistra nel portale di Azure fare clic su **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="16d94-122">In the Azure portal, on the left navbar, click **Azure Active Directory**.</span></span> 

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="16d94-124">Nella sezione **Gestisci** del pannello **Azure Active Directory** fare clic su **Accesso condizionale**.</span><span class="sxs-lookup"><span data-stu-id="16d94-124">On the **Azure Active Directory** blade, in the **Manage** section, click **Conditional access**.</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="16d94-126">Nel pannello **Accesso condizionale** aprire il pannello **Nuovo** facendo clic su **Aggiungi** nella barra degli strumenti in alto.</span><span class="sxs-lookup"><span data-stu-id="16d94-126">On the **Conditional Access** blade, to open the **New** blade, in the toolbar on the top, click **Add**.</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="16d94-128">Nel pannello **Nuovo** digitare un nome per i criteri nella casella di testo **Nome**.</span><span class="sxs-lookup"><span data-stu-id="16d94-128">On the **New** blade, in the **Name** textbox, type a name for your policy.</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="16d94-130">Nella sezione **Assegnazioni** fare clic su **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="16d94-130">In the **Assignment** section, click **Users and groups**.</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="16d94-132">Nel pannello **Utenti e gruppi** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="16d94-132">On the **Users and groups** blade, perform the following steps:</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="16d94-134">a.</span><span class="sxs-lookup"><span data-stu-id="16d94-134">a.</span></span> <span data-ttu-id="16d94-135">Fare clic su **Seleziona utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="16d94-135">Click **Select users and groups**.</span></span>

    <span data-ttu-id="16d94-136">b.</span><span class="sxs-lookup"><span data-stu-id="16d94-136">b.</span></span> <span data-ttu-id="16d94-137">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="16d94-137">Click **Select**.</span></span>

    <span data-ttu-id="16d94-138">c.</span><span class="sxs-lookup"><span data-stu-id="16d94-138">c.</span></span> <span data-ttu-id="16d94-139">Nel pannello **Seleziona** scegliere l'utente test e quindi fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="16d94-139">On the **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="16d94-140">d.</span><span class="sxs-lookup"><span data-stu-id="16d94-140">d.</span></span> <span data-ttu-id="16d94-141">Nel pannello **Utenti e gruppi** fare clic su **Fatto**.</span><span class="sxs-lookup"><span data-stu-id="16d94-141">On the **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="16d94-142">Nel pannello **Nuovo** aprire il pannello **App cloud** nella sezione **Assegnazioni** facendo clic su **App cloud**.</span><span class="sxs-lookup"><span data-stu-id="16d94-142">On the **New** blade, to open the **Cloud apps** blade, in the **Assignment** section, click **Cloud apps**.</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="16d94-144">Nel pannello **App cloud** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="16d94-144">On the **Cloud apps** blade, perform the following steps:</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="16d94-146">a.</span><span class="sxs-lookup"><span data-stu-id="16d94-146">a.</span></span> <span data-ttu-id="16d94-147">Fare clic su **Selezionare le app**.</span><span class="sxs-lookup"><span data-stu-id="16d94-147">Click **Select apps**.</span></span>

    <span data-ttu-id="16d94-148">b.</span><span class="sxs-lookup"><span data-stu-id="16d94-148">b.</span></span> <span data-ttu-id="16d94-149">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="16d94-149">Click **Select**.</span></span>

    <span data-ttu-id="16d94-150">c.</span><span class="sxs-lookup"><span data-stu-id="16d94-150">c.</span></span> <span data-ttu-id="16d94-151">Nel pannello **Seleziona** scegliere l'app cloud e quindi fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="16d94-151">On the **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="16d94-152">d.</span><span class="sxs-lookup"><span data-stu-id="16d94-152">d.</span></span> <span data-ttu-id="16d94-153">Nel pannello **App cloud** fare clic su **Fatto**.</span><span class="sxs-lookup"><span data-stu-id="16d94-153">On the **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="16d94-154">Nel pannello **Nuovo** aprire il pannello **Condizioni** nella sezione **Assegnazioni** facendo clic su **Condizioni**.</span><span class="sxs-lookup"><span data-stu-id="16d94-154">On the **New** blade, to open the **Conditions** blade, in the **Assignment** section, click **Conditions**.</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="16d94-156">Nel pannello **Condizioni** aprire il pannello **Località** facendo clic su **Località**.</span><span class="sxs-lookup"><span data-stu-id="16d94-156">On the **Conditions** blade, to open the **Locations** blade, click **Locations**.</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="16d94-158">Nel pannello **Località** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="16d94-158">On the **Locations** blade, perform the following steps:</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="16d94-160">a.</span><span class="sxs-lookup"><span data-stu-id="16d94-160">a.</span></span> <span data-ttu-id="16d94-161">In **Configura** fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="16d94-161">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="16d94-162">b.</span><span class="sxs-lookup"><span data-stu-id="16d94-162">b.</span></span> <span data-ttu-id="16d94-163">In **Includi** fare clic su **Tutte le località**.</span><span class="sxs-lookup"><span data-stu-id="16d94-163">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="16d94-164">c.</span><span class="sxs-lookup"><span data-stu-id="16d94-164">c.</span></span> <span data-ttu-id="16d94-165">Fare clic su **Escludi** e quindi su **Tutti gli indirizzi IP attendibili**.</span><span class="sxs-lookup"><span data-stu-id="16d94-165">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="16d94-167">d.</span><span class="sxs-lookup"><span data-stu-id="16d94-167">d.</span></span> <span data-ttu-id="16d94-168">Fare clic su **Done**.</span><span class="sxs-lookup"><span data-stu-id="16d94-168">Click **Done**.</span></span>

12. <span data-ttu-id="16d94-169">Nel pannello **Condizioni** fare clic su **Fatto**.</span><span class="sxs-lookup"><span data-stu-id="16d94-169">On the **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="16d94-170">Nel pannello **Nuovo** aprire il pannello **Concedi** nella sezione **Controlli** facendo clic su **Concedi**.</span><span class="sxs-lookup"><span data-stu-id="16d94-170">On the **New** blade, to open the **Grant** blade, in the **Controls** section, click **Grant**.</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="16d94-172">Nel pannello **Concedi** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="16d94-172">On the **Grant** blade, perform the following steps:</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="16d94-174">a.</span><span class="sxs-lookup"><span data-stu-id="16d94-174">a.</span></span> <span data-ttu-id="16d94-175">Selezionare **Richiedi autenticazione a più fattori**.</span><span class="sxs-lookup"><span data-stu-id="16d94-175">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="16d94-176">b.</span><span class="sxs-lookup"><span data-stu-id="16d94-176">b.</span></span> <span data-ttu-id="16d94-177">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="16d94-177">Click **Select**.</span></span>

15. <span data-ttu-id="16d94-178">Nel pannello **Nuovo** in **Abilita criteri** fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="16d94-178">On the **New** blade, under **Enable policy**, click **On**.</span></span>

    ![Accesso condizionale](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="16d94-180">Nel pannello **Nuovo** fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="16d94-180">On the **New** blade, click **Create**.</span></span>


## <a name="testing-the-policy"></a><span data-ttu-id="16d94-181">Test dei criteri</span><span class="sxs-lookup"><span data-stu-id="16d94-181">Testing the policy</span></span>

<span data-ttu-id="16d94-182">Per testare i criteri, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="16d94-182">To test your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="16d94-183">Accedere all'app da un dispositivo con un indirizzo IP compreso nell'intervallo di indirizzi IP attendibili configurato.</span><span class="sxs-lookup"><span data-stu-id="16d94-183">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="16d94-184">Accedere all'app da un dispositivo con un indirizzo IP non compreso nell'intervallo di indirizzi IP attendibili configurato.</span><span class="sxs-lookup"><span data-stu-id="16d94-184">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="16d94-185">L'autenticazione a più fattori deve essere necessaria solo durante il tentativo di connessione da un dispositivo con un indirizzo IP non compreso nell'intervallo di indirizzi attendibili.</span><span class="sxs-lookup"><span data-stu-id="16d94-185">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="16d94-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="16d94-186">Next steps</span></span>

<span data-ttu-id="16d94-187">Per altre informazioni sull'argomento, vedere [Accesso condizionale in Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="16d94-187">If you would like to learn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

