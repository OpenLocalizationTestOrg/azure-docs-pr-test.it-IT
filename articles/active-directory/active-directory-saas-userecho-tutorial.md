---
title: 'Esercitazione: Integrazione di Azure Active Directory con UserEcho | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e UserEcho.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bedd916b-8f69-4b50-9b8d-56f4ee3bd3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2d824d8d5eb8a25db128397b908a126bd87213ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-userecho"></a><span data-ttu-id="467bc-103">Esercitazione: Integrazione di Azure Active Directory con UserEcho</span><span class="sxs-lookup"><span data-stu-id="467bc-103">Tutorial: Azure Active Directory integration with UserEcho</span></span>

<span data-ttu-id="467bc-104">Questa esercitazione descrive come integrare UserEcho con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="467bc-104">In this tutorial, you learn how to integrate UserEcho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="467bc-105">L'integrazione di UserEcho con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="467bc-105">Integrating UserEcho with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="467bc-106">È possibile controllare in Azure AD chi può accedere a UserEcho.</span><span class="sxs-lookup"><span data-stu-id="467bc-106">You can control in Azure AD who has access to UserEcho</span></span>
- <span data-ttu-id="467bc-107">È possibile abilitare gli utenti per l'accesso automatico a UserEcho (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="467bc-107">You can enable your users to automatically get signed-on to UserEcho (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="467bc-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="467bc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="467bc-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="467bc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="467bc-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="467bc-110">Prerequisites</span></span>

<span data-ttu-id="467bc-111">Per configurare l'integrazione di Azure AD con UserEcho, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="467bc-111">To configure Azure AD integration with UserEcho, you need the following items:</span></span>

- <span data-ttu-id="467bc-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="467bc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="467bc-113">Sottoscrizione di UserEcho abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="467bc-113">A UserEcho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="467bc-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="467bc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="467bc-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="467bc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="467bc-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="467bc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="467bc-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="467bc-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="467bc-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="467bc-118">Scenario description</span></span>
<span data-ttu-id="467bc-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="467bc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="467bc-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="467bc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="467bc-121">Aggiunta di UserEcho dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="467bc-121">Adding UserEcho from the gallery</span></span>
2. <span data-ttu-id="467bc-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="467bc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-userecho-from-the-gallery"></a><span data-ttu-id="467bc-123">Aggiunta di UserEcho dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="467bc-123">Adding UserEcho from the gallery</span></span>
<span data-ttu-id="467bc-124">Per configurare l'integrazione di UserEcho in Azure AD, è necessario aggiungere UserEcho dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="467bc-124">To configure the integration of UserEcho into Azure AD, you need to add UserEcho from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="467bc-125">**Per aggiungere UserEcho dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="467bc-125">**To add UserEcho from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="467bc-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="467bc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="467bc-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="467bc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="467bc-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="467bc-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="467bc-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="467bc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="467bc-133">Nella casella di ricerca digitare **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="467bc-133">In the search box, type **UserEcho**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_search.png)

5. <span data-ttu-id="467bc-135">Nel pannello dei risultati selezionare **UserEcho** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="467bc-135">In the results panel, select **UserEcho**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="467bc-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="467bc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="467bc-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con UserEcho con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="467bc-138">In this section, you configure and test Azure AD single sign-on with UserEcho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="467bc-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di UserEcho che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="467bc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UserEcho is to a user in Azure AD.</span></span> <span data-ttu-id="467bc-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in UserEcho.</span><span class="sxs-lookup"><span data-stu-id="467bc-140">In other words, a link relationship between an Azure AD user and the related user in UserEcho needs to be established.</span></span>

<span data-ttu-id="467bc-141">Per stabilire la relazione di collegamento, in UserEcho assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="467bc-141">In UserEcho, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="467bc-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con UserEcho, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="467bc-142">To configure and test Azure AD single sign-on with UserEcho, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="467bc-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="467bc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="467bc-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="467bc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="467bc-145">**[Creazione di un utente test per UserEcho](#creating-a-userecho-test-user)**: per avere una controparte di Britta Simon in UserEcho collegata alla relativa rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="467bc-145">**[Creating a UserEcho test user](#creating-a-userecho-test-user)** - to have a counterpart of Britta Simon in UserEcho that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="467bc-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="467bc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="467bc-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="467bc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="467bc-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="467bc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="467bc-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione UserEcho.</span><span class="sxs-lookup"><span data-stu-id="467bc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UserEcho application.</span></span>

<span data-ttu-id="467bc-150">**Per configurare l'accesso Single Sign-On di Azure AD con UserEcho, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="467bc-150">**To configure Azure AD single sign-on with UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="467bc-151">Nella pagina di integrazione dell'applicazione **UserEcho** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="467bc-151">In the Azure portal, on the **UserEcho** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="467bc-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="467bc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_samlbase.png)

3. <span data-ttu-id="467bc-155">Nella sezione **URL e dominio UserEcho** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="467bc-155">On the **UserEcho Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_url.png)

    <span data-ttu-id="467bc-157">a.</span><span class="sxs-lookup"><span data-stu-id="467bc-157">a.</span></span> <span data-ttu-id="467bc-158">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<companyname>.userecho.com/`.</span><span class="sxs-lookup"><span data-stu-id="467bc-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.userecho.com/`</span></span>

    <span data-ttu-id="467bc-159">b.</span><span class="sxs-lookup"><span data-stu-id="467bc-159">b.</span></span> <span data-ttu-id="467bc-160">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://<companyname>.userecho.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="467bc-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.userecho.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="467bc-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="467bc-161">These values are not real.</span></span> <span data-ttu-id="467bc-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="467bc-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="467bc-163">Per ottenere questi valori, contattare il [team di supporto clienti di UserEcho](https://feedback.userecho.com/).</span><span class="sxs-lookup"><span data-stu-id="467bc-163">Contact [UserEcho Client support team](https://feedback.userecho.com/) to get these values.</span></span> 

4. <span data-ttu-id="467bc-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="467bc-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_certificate.png) 

5. <span data-ttu-id="467bc-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="467bc-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="467bc-168">Nella sezione **Configurazione di UserEcho** fare clic su **Configura UserEcho** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="467bc-168">On the **UserEcho Configuration** section, click **Configure UserEcho** to open **Configure sign-on** window.</span></span> <span data-ttu-id="467bc-169">Copiare l'**URL servizio Single Sign-On SAML e l'URL di disconnessione** dalla sezione **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="467bc-169">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_configure.png) 

7. <span data-ttu-id="467bc-171">In un'altra finestra del browser accedere al sito aziendale di UserEcho come amministratore.</span><span class="sxs-lookup"><span data-stu-id="467bc-171">In another browser window, sign on to your UserEcho company site as an administrator.</span></span>

8. <span data-ttu-id="467bc-172">Sulla barra degli strumenti in alto, fare clic sul nome utente per espandere il menu e quindi fare clic su **Setup**.</span><span class="sxs-lookup"><span data-stu-id="467bc-172">In the toolbar on the top, click your user name to expand the menu, and then click **Setup**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png) 

9. <span data-ttu-id="467bc-174">Fare clic su **Integrations**.</span><span class="sxs-lookup"><span data-stu-id="467bc-174">Click **Integrations**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_07.png) 

10. <span data-ttu-id="467bc-176">Fare clic su **Sito web** e quindi su **Single sign-on (SAML2)**.</span><span class="sxs-lookup"><span data-stu-id="467bc-176">Click **Website**, and then click **Single sign-on (SAML2)**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_08.png) 

11. <span data-ttu-id="467bc-178">Nella pagina **Single sign-on (SAML)** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="467bc-178">On the **Single sign-on (SAML)** page, perform the following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_09.png)
    
    <span data-ttu-id="467bc-180">a.</span><span class="sxs-lookup"><span data-stu-id="467bc-180">a.</span></span> <span data-ttu-id="467bc-181">Per **SAML-enabled** (Abilitato per SAML) selezionare **Sì**.</span><span class="sxs-lookup"><span data-stu-id="467bc-181">As **SAML-enabled**, select **Yes**.</span></span>
    
    <span data-ttu-id="467bc-182">b.</span><span class="sxs-lookup"><span data-stu-id="467bc-182">b.</span></span> <span data-ttu-id="467bc-183">Incollare l'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure nella casella di testo **SAML SSO URL**.</span><span class="sxs-lookup"><span data-stu-id="467bc-183">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **SAML SSO URL** textbox.</span></span>
    
    <span data-ttu-id="467bc-184">c.</span><span class="sxs-lookup"><span data-stu-id="467bc-184">c.</span></span> <span data-ttu-id="467bc-185">Incollare l'**URL di disconnessione** copiato dal portale di Azure nella casella di testo **Remote Logout URL** (URL di disconnessione remota).</span><span class="sxs-lookup"><span data-stu-id="467bc-185">Paste **Sign-Out URL**, which you have copied from the Azure portal into the **Remote logoout URL** textbox.</span></span>
    
    <span data-ttu-id="467bc-186">d.</span><span class="sxs-lookup"><span data-stu-id="467bc-186">d.</span></span> <span data-ttu-id="467bc-187">Aprire il certificato scaricato nel Blocco note, copiarne il contenuto e incollarlo nella casella di testo **X.509 Certificate** .</span><span class="sxs-lookup"><span data-stu-id="467bc-187">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **X.509 Certificate** textbox.</span></span>
    
    <span data-ttu-id="467bc-188">e.</span><span class="sxs-lookup"><span data-stu-id="467bc-188">e.</span></span> <span data-ttu-id="467bc-189">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="467bc-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="467bc-190">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="467bc-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="467bc-191">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="467bc-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="467bc-192">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="467bc-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="467bc-193">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="467bc-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="467bc-194">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="467bc-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="467bc-196">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="467bc-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="467bc-197">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="467bc-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="467bc-199">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="467bc-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="467bc-201">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="467bc-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="467bc-203">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="467bc-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="467bc-205">a.</span><span class="sxs-lookup"><span data-stu-id="467bc-205">a.</span></span> <span data-ttu-id="467bc-206">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="467bc-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="467bc-207">b.</span><span class="sxs-lookup"><span data-stu-id="467bc-207">b.</span></span> <span data-ttu-id="467bc-208">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="467bc-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="467bc-209">c.</span><span class="sxs-lookup"><span data-stu-id="467bc-209">c.</span></span> <span data-ttu-id="467bc-210">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="467bc-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="467bc-211">d.</span><span class="sxs-lookup"><span data-stu-id="467bc-211">d.</span></span> <span data-ttu-id="467bc-212">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="467bc-212">Click **Create**.</span></span>
 
### <a name="creating-a-userecho-test-user"></a><span data-ttu-id="467bc-213">Creazione di un utente test per UserEcho</span><span class="sxs-lookup"><span data-stu-id="467bc-213">Creating a UserEcho test user</span></span>

<span data-ttu-id="467bc-214">Questa sezione descrive come creare un utente chiamato Britta Simon in UserEcho.</span><span class="sxs-lookup"><span data-stu-id="467bc-214">The objective of this section is to create a user called Britta Simon in UserEcho.</span></span>

<span data-ttu-id="467bc-215">**Per creare un utente denominato Britta Simon in UserEcho, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="467bc-215">**To create a user called Britta Simon in UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="467bc-216">Accedere al sito aziendale di UserEcho come amministratore.</span><span class="sxs-lookup"><span data-stu-id="467bc-216">Sign-on to your UserEcho company site as an administrator.</span></span>

2. <span data-ttu-id="467bc-217">Sulla barra degli strumenti in alto, fare clic sul nome utente per espandere il menu e quindi fare clic su **Setup**.</span><span class="sxs-lookup"><span data-stu-id="467bc-217">In the toolbar on the top, click your user name to expand the menu, and then click **Setup**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png)

3. <span data-ttu-id="467bc-219">Fare clic su **Users** (Utenti) per espandere la sezione **Users** (Utenti).</span><span class="sxs-lookup"><span data-stu-id="467bc-219">Click **Users**, to expand the **Users** section.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_10.png)

4. <span data-ttu-id="467bc-221">Fare clic su **Users**.</span><span class="sxs-lookup"><span data-stu-id="467bc-221">Click **Users**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_11.png)

5. <span data-ttu-id="467bc-223">Fare clic su **Invite a new user**.</span><span class="sxs-lookup"><span data-stu-id="467bc-223">Click **Invite a new user**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_12.png)

6. <span data-ttu-id="467bc-225">Nella finestra di dialogo **Invita un nuovo utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="467bc-225">On the **Invite a new user** dialog, perform the following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_13.png)

    <span data-ttu-id="467bc-227">a.</span><span class="sxs-lookup"><span data-stu-id="467bc-227">a.</span></span> <span data-ttu-id="467bc-228">Nella casella di testo **Name** (Nome) digitare il nome dell'utente, ad esempio Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="467bc-228">In the **Name** textbox, type name of the user like Britta Simon.</span></span>
    
    <span data-ttu-id="467bc-229">b.</span><span class="sxs-lookup"><span data-stu-id="467bc-229">b.</span></span>  <span data-ttu-id="467bc-230">Nella casella di testo **Email** digitare l'indirizzo di posta elettronica dell'utente, ad esempio Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="467bc-230">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="467bc-231">c.</span><span class="sxs-lookup"><span data-stu-id="467bc-231">c.</span></span> <span data-ttu-id="467bc-232">Fare clic su **Invita**.</span><span class="sxs-lookup"><span data-stu-id="467bc-232">Click **Invite**.</span></span>

<span data-ttu-id="467bc-233">A Britta viene inviato un invito che le permette di iniziare a usare UserEcho.</span><span class="sxs-lookup"><span data-stu-id="467bc-233">An invitation is sent to Britta, which enables her to start using UserEcho.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="467bc-234">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="467bc-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="467bc-235">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a UserEcho.</span><span class="sxs-lookup"><span data-stu-id="467bc-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UserEcho.</span></span>

![Assegna utente][200] 

<span data-ttu-id="467bc-237">**Per assegnare Britta Simon a UserEcho, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="467bc-237">**To assign Britta Simon to UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="467bc-238">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="467bc-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="467bc-240">Nell'elenco di applicazioni, selezionare **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="467bc-240">In the applications list, select **UserEcho**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_app.png) 

3. <span data-ttu-id="467bc-242">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="467bc-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="467bc-244">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="467bc-244">Click **Add** button.</span></span> <span data-ttu-id="467bc-245">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="467bc-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="467bc-247">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="467bc-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="467bc-248">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="467bc-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="467bc-249">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="467bc-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="467bc-250">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="467bc-250">Testing single sign-on</span></span>

<span data-ttu-id="467bc-251">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="467bc-251">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="467bc-252">Quando si fa clic sul riquadro UserEcho nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione UserEcho.</span><span class="sxs-lookup"><span data-stu-id="467bc-252">When you click the UserEcho tile in the Access Panel, you should get automatically signed-on to your UserEcho application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="467bc-253">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="467bc-253">Additional resources</span></span>

* [<span data-ttu-id="467bc-254">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="467bc-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="467bc-255">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="467bc-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_203.png

