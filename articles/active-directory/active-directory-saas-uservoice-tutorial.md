---
title: 'Esercitazione: Integrazione di Azure Active Directory con UserVoice | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e UserVoice.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: fcfda1c2ecb162fb93b70574a18bd745b72ee4db
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a><span data-ttu-id="b9bab-103">Esercitazione: Integrazione di Azure Active Directory con UserVoice</span><span class="sxs-lookup"><span data-stu-id="b9bab-103">Tutorial: Azure Active Directory integration with UserVoice</span></span>

<span data-ttu-id="b9bab-104">Questa esercitazione descrive come integrare UserVoice con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b9bab-104">In this tutorial, you learn how to integrate UserVoice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9bab-105">L'integrazione di UserVoice con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b9bab-105">Integrating UserVoice with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b9bab-106">È possibile controllare in Azure AD chi può accedere a UserVoice.</span><span class="sxs-lookup"><span data-stu-id="b9bab-106">You can control in Azure AD who has access to UserVoice.</span></span>
- <span data-ttu-id="b9bab-107">È possibile abilitare gli utenti per l'accesso automatico a UserVoice (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9bab-107">You can enable your users to automatically get signed-on to UserVoice (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b9bab-108">È possibile gestire gli account da una posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bab-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b9bab-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b9bab-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9bab-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b9bab-110">Prerequisites</span></span>

<span data-ttu-id="b9bab-111">Per configurare l'integrazione di Azure AD con UserVoice, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b9bab-111">To configure Azure AD integration with UserVoice, you need the following items:</span></span>

- <span data-ttu-id="b9bab-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9bab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9bab-113">Sottoscrizione di UserVoice abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b9bab-113">A UserVoice single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9bab-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b9bab-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9bab-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b9bab-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9bab-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b9bab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b9bab-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9bab-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9bab-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b9bab-118">Scenario description</span></span>
<span data-ttu-id="b9bab-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b9bab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9bab-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b9bab-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9bab-121">Aggiunta di UserVoice dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b9bab-121">Adding UserVoice from the gallery</span></span>
2. <span data-ttu-id="b9bab-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9bab-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-uservoice-from-the-gallery"></a><span data-ttu-id="b9bab-123">Aggiunta di UserVoice dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="b9bab-123">Adding UserVoice from the gallery</span></span>
<span data-ttu-id="b9bab-124">Per configurare l'integrazione di UserVoice in Azure AD, è necessario aggiungere UserVoice dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b9bab-124">To configure the integration of UserVoice into Azure AD, you need to add UserVoice from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b9bab-125">**Per aggiungere UserVoice dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b9bab-125">**To add UserVoice from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b9bab-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="b9bab-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="b9bab-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b9bab-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="b9bab-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="b9bab-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="b9bab-133">Nella casella di ricerca digitare **UserVoice**, selezionare **UserVoice** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b9bab-133">In the search box, type **UserVoice**, select **UserVoice** from result panel then click **Add** button to add the application.</span></span>

    ![UserVoice nell'elenco dei risultati](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b9bab-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9bab-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b9bab-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con UserVoice in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b9bab-136">In this section, you configure and test Azure AD single sign-on with UserVoice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b9bab-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di UserVoice che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9bab-137">For single sign-on to work, Azure AD needs to know what the counterpart user in UserVoice is to a user in Azure AD.</span></span> <span data-ttu-id="b9bab-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in UserVoice.</span><span class="sxs-lookup"><span data-stu-id="b9bab-138">In other words, a link relationship between an Azure AD user and the related user in UserVoice needs to be established.</span></span>

<span data-ttu-id="b9bab-139">Per stabilire la relazione di collegamento, in UserVoice assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="b9bab-139">In UserVoice, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b9bab-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con UserVoice, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b9bab-140">To configure and test Azure AD single sign-on with UserVoice, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b9bab-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b9bab-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b9bab-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9bab-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9bab-143">**[Creare un utente di test di UserVoice](#create-a-uservoice-test-user)**: per avere una controparte di Britta Simon in UserVoice collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9bab-143">**[Create a UserVoice test user](#create-a-uservoice-test-user)** - to have a counterpart of Britta Simon in UserVoice that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b9bab-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9bab-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9bab-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="b9bab-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b9bab-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9bab-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b9bab-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione UserVoice.</span><span class="sxs-lookup"><span data-stu-id="b9bab-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UserVoice application.</span></span>

<span data-ttu-id="b9bab-148">**Per configurare Single Sign-On di Azure AD con UserVoice, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b9bab-148">**To configure Azure AD single sign-on with UserVoice, perform the following steps:**</span></span>

1. <span data-ttu-id="b9bab-149">Nella pagina di integrazione dell'applicazione **UserVoice** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-149">In the Azure portal, on the **UserVoice** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="b9bab-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b9bab-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. <span data-ttu-id="b9bab-153">Nella sezione **URL e dominio UserVoice** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b9bab-153">On the **UserVoice Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni sull'accesso Single Sign-On per URL e dominio di UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    <span data-ttu-id="b9bab-155">a.</span><span class="sxs-lookup"><span data-stu-id="b9bab-155">a.</span></span> <span data-ttu-id="b9bab-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<tenantname>.UserVoice.com`.</span><span class="sxs-lookup"><span data-stu-id="b9bab-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    <span data-ttu-id="b9bab-157">b.</span><span class="sxs-lookup"><span data-stu-id="b9bab-157">b.</span></span> <span data-ttu-id="b9bab-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="b9bab-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b9bab-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="b9bab-159">These values are not real.</span></span> <span data-ttu-id="b9bab-160">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="b9bab-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b9bab-161">Per ottenere questi valori, contattare il [team di supporto clienti di UserVoice](https://www.uservoice.com/).</span><span class="sxs-lookup"><span data-stu-id="b9bab-161">Contact [UserVoice Client support team](https://www.uservoice.com/) to get these values.</span></span>

4. <span data-ttu-id="b9bab-162">Nella sezione **Certificato di firma SAML** copiare il valore **IDENTIFICAZIONE PERSONALE** del certificato.</span><span class="sxs-lookup"><span data-stu-id="b9bab-162">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. <span data-ttu-id="b9bab-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="b9bab-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b9bab-166">Nella sezione **Configurazione di UserVoice** fare clic su **Configura UserVoice** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-166">On the **UserVoice Configuration** section, click **Configure UserVoice** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b9bab-167">Copiare i valori **Sign-Out URL (URL di disconnessione) e SAML Single Sign-On Service URL (URL servizio Single Sign-On SAML)** dalla sezione **Quick Reference** (Riferimento rapido).</span><span class="sxs-lookup"><span data-stu-id="b9bab-167">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. <span data-ttu-id="b9bab-169">In un'altra finestra del browser Web accedere al sito aziendale di UserVoice come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b9bab-169">In a different web browser window, log in to your UserVoice company site as an administrator.</span></span>

8. <span data-ttu-id="b9bab-170">Sulla barra degli strumenti in alto fare clic su **Impostazioni**, quindi selezionare **Portale Web** nel menu.</span><span class="sxs-lookup"><span data-stu-id="b9bab-170">In the toolbar on the top, click **Settings**, and then select **Web portal** from the menu.</span></span>
   
    <span data-ttu-id="b9bab-171">![Sezione Impostazioni sul lato dell'app](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="b9bab-171">![Settings Section On App Side](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Settings")</span></span>

9. <span data-ttu-id="b9bab-172">Nelle sezione **User authentication** (Autenticazione utente) della scheda **Web portal** (Portale Web) fare clic su **Edit** (Modifica) per aprire la finestra di dialogo **Edit User Authentication** (Modifica autenticazione utente).</span><span class="sxs-lookup"><span data-stu-id="b9bab-172">On the **Web portal** tab, in the **User authentication** section, click **Edit** to open the **Edit User Authentication** dialog page.</span></span>
   
    <span data-ttu-id="b9bab-173">![Scheda Portale Web](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Portale Web")</span><span class="sxs-lookup"><span data-stu-id="b9bab-173">![Web portal Tab](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portal")</span></span>

10. <span data-ttu-id="b9bab-174">Nella finestra di dialogo **Edit User Authentication** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b9bab-174">On the **Edit User Authentication** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="b9bab-175">![Modificare l'autenticazione utente](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Modificare l'autenticazione utente")</span><span class="sxs-lookup"><span data-stu-id="b9bab-175">![Edit user authentication](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Edit user authentication")</span></span>
   
    <span data-ttu-id="b9bab-176">a.</span><span class="sxs-lookup"><span data-stu-id="b9bab-176">a.</span></span> <span data-ttu-id="b9bab-177">Fare clic su **Single Sign-On (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-177">Click **Single Sign-On (SSO)**.</span></span>
 
    <span data-ttu-id="b9bab-178">b.</span><span class="sxs-lookup"><span data-stu-id="b9bab-178">b.</span></span> <span data-ttu-id="b9bab-179">Incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure nella casella di testo **SSO Remote Sign-In** (Accesso remoto SSO).</span><span class="sxs-lookup"><span data-stu-id="b9bab-179">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **SSO Remote Sign-In** textbox.</span></span>

    <span data-ttu-id="b9bab-180">c.</span><span class="sxs-lookup"><span data-stu-id="b9bab-180">c.</span></span> <span data-ttu-id="b9bab-181">Incollare il valore dell'**URL di disconnessione** copiato dal portale di Azure nella casella di testo **SSO Remote Sign-Out** (Disconnessione remota SSO).</span><span class="sxs-lookup"><span data-stu-id="b9bab-181">Paste the **Sign-Out URL** value, which you have copied from the Azure portal into the **SSO Remote Sign-Out textbox**.</span></span>
 
    <span data-ttu-id="b9bab-182">d.</span><span class="sxs-lookup"><span data-stu-id="b9bab-182">d.</span></span> <span data-ttu-id="b9bab-183">Nella casella di testo **Current certificate SHA1 fingerprint** (Impronta digitale SHA1 certificato corrente) incollare il valore **Identificazione personale** del certificato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bab-183">Paste the **Thumbprint** value , which you have copied from Azure portal  into the **Current certificate SHA1 fingerprint** textbox.</span></span>
    
    <span data-ttu-id="b9bab-184">e.</span><span class="sxs-lookup"><span data-stu-id="b9bab-184">e.</span></span> <span data-ttu-id="b9bab-185">Fare clic su **Salva le impostazioni di autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-185">Click **Save authentication settings**.</span></span>

> [!TIP]
> <span data-ttu-id="b9bab-186">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="b9bab-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b9bab-187">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="b9bab-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b9bab-188">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b9bab-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b9bab-189">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9bab-189">Create an Azure AD test user</span></span>

<span data-ttu-id="b9bab-190">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bab-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="b9bab-192">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b9bab-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b9bab-193">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="b9bab-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b9bab-195">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b9bab-197">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b9bab-199">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b9bab-199">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b9bab-201">a.</span><span class="sxs-lookup"><span data-stu-id="b9bab-201">a.</span></span> <span data-ttu-id="b9bab-202">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-202">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9bab-203">b.</span><span class="sxs-lookup"><span data-stu-id="b9bab-203">b.</span></span> <span data-ttu-id="b9bab-204">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9bab-204">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b9bab-205">c.</span><span class="sxs-lookup"><span data-stu-id="b9bab-205">c.</span></span> <span data-ttu-id="b9bab-206">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b9bab-207">d.</span><span class="sxs-lookup"><span data-stu-id="b9bab-207">d.</span></span> <span data-ttu-id="b9bab-208">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-208">Click **Create**.</span></span>
 
### <a name="create-a-uservoice-test-user"></a><span data-ttu-id="b9bab-209">Creare un utente di test per UserVoice</span><span class="sxs-lookup"><span data-stu-id="b9bab-209">Create a UserVoice test user</span></span>

<span data-ttu-id="b9bab-210">Per consentire agli utenti di Azure AD di accedere a UserVoice, è necessario eseguirne il provisioning in UserVoice.</span><span class="sxs-lookup"><span data-stu-id="b9bab-210">To enable Azure AD users to log in to UserVoice, they must be provisioned into UserVoice.</span></span> <span data-ttu-id="b9bab-211">Nel caso di UserVoice, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="b9bab-211">In the case of UserVoice, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="b9bab-212">Per eseguire il provisioning di un account utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b9bab-212">To provision a user account, perform the following steps:</span></span>
1. <span data-ttu-id="b9bab-213">Accedere al tenant di **UserVoice** .</span><span class="sxs-lookup"><span data-stu-id="b9bab-213">Log in to your **UserVoice** tenant.</span></span>

2. <span data-ttu-id="b9bab-214">Passare a **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-214">Go to **Settings**.</span></span>
   
    <span data-ttu-id="b9bab-215">![Impostazioni](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="b9bab-215">![Settings](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Settings")</span></span>

3. <span data-ttu-id="b9bab-216">Fare clic su **Generale**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-216">Click **General**.</span></span>

4. <span data-ttu-id="b9bab-217">Fare clic su **Agents and permissions**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-217">Click **Agents and permissions**.</span></span>
   
    <span data-ttu-id="b9bab-218">![Agenti e autorizzazioni](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agenti e autorizzazioni")</span><span class="sxs-lookup"><span data-stu-id="b9bab-218">![Agents and permissions](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agents and permissions")</span></span>

5. <span data-ttu-id="b9bab-219">Fare clic su **Aggiungi amministratori**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-219">Click **Add admins**.</span></span>
   
    <span data-ttu-id="b9bab-220">![Aggiungere amministratori](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Aggiungere amministratori")</span><span class="sxs-lookup"><span data-stu-id="b9bab-220">![Add admins](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Add admins")</span></span>

6. <span data-ttu-id="b9bab-221">Nella finestra di dialogo **Invita amministratori** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b9bab-221">On the **Invite admins** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="b9bab-222">![Invitare gli amministratori](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Invitare gli amministratori")</span><span class="sxs-lookup"><span data-stu-id="b9bab-222">![Invite admins](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Invite admins")</span></span>
   
    <span data-ttu-id="b9bab-223">a.</span><span class="sxs-lookup"><span data-stu-id="b9bab-223">a.</span></span> <span data-ttu-id="b9bab-224">Nella casella di testo Emails digitare l'indirizzo di posta elettronica dell'account di cui si vuole eseguire il provisioning e quindi fare clic su **Add**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-224">In the Emails textbox, type the email address of the account you want to provision, and then click **Add**.</span></span>
   
    <span data-ttu-id="b9bab-225">b.</span><span class="sxs-lookup"><span data-stu-id="b9bab-225">b.</span></span> <span data-ttu-id="b9bab-226">Fare clic su **Invita**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-226">Click **Invite**.</span></span>

> [!NOTE]
> <span data-ttu-id="b9bab-227">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da UserVoice per eseguire il provisioning degli account utente Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9bab-227">You can use any other UserVoice user account creation tools or APIs provided by UserVoice to provision AAD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b9bab-228">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9bab-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="b9bab-229">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a UserVoice.</span><span class="sxs-lookup"><span data-stu-id="b9bab-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UserVoice.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="b9bab-231">**Per assegnare Britta Simon a UserVoice, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="b9bab-231">**To assign Britta Simon to UserVoice, perform the following steps:**</span></span>

1. <span data-ttu-id="b9bab-232">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b9bab-234">Nell'elenco delle applicazioni selezionare **UserVoice**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-234">In the applications list, select **UserVoice**.</span></span>

    ![Collegamento UserVoice nell'elenco delle applicazioni](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. <span data-ttu-id="b9bab-236">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="b9bab-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="b9bab-238">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-238">Click **Add** button.</span></span> <span data-ttu-id="b9bab-239">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="b9bab-241">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="b9bab-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b9bab-242">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b9bab-243">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b9bab-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b9bab-244">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b9bab-244">Test single sign-on</span></span>

<span data-ttu-id="b9bab-245">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b9bab-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b9bab-246">Quando si fa clic sul riquadro UserVoice nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione UserVoice.</span><span class="sxs-lookup"><span data-stu-id="b9bab-246">When you click the UserVoice tile in the Access Panel, you should get automatically signed-on to your UserVoice application.</span></span>
<span data-ttu-id="b9bab-247">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b9bab-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b9bab-248">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b9bab-248">Additional resources</span></span>

* [<span data-ttu-id="b9bab-249">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9bab-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b9bab-250">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9bab-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

