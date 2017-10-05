---
title: 'Esercitazione: Integrazione di Azure Active Directory con Citrix GoToMeeting | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Citrix GoToMeeting.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: c1ac144c4fa43312ec26fce03cd0ee1bfcf73d4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="7f158-103">Esercitazione: Integrazione di Azure Active Directory con Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="7f158-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="7f158-104">Questa esercitazione descrive come integrare Citrix GoToMeeting con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7f158-104">In this tutorial, you learn how to integrate Citrix GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7f158-105">L'integrazione di Citrix GoToMeeting con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7f158-105">Integrating Citrix GoToMeeting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7f158-106">È possibile controllare in Azure AD chi può accedere a Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="7f158-106">You can control in Azure AD who has access to Citrix GoToMeeting</span></span>
- <span data-ttu-id="7f158-107">È possibile abilitare gli utenti per l'accesso automatico a Citrix GoToMeeting (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f158-107">You can enable your users to automatically get signed-on to Citrix GoToMeeting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7f158-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f158-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7f158-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7f158-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f158-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7f158-110">Prerequisites</span></span>

<span data-ttu-id="7f158-111">Per configurare l'integrazione di Azure AD con Citrix GoToMeeting, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7f158-111">To configure Azure AD integration with Citrix GoToMeeting, you need the following items:</span></span>

- <span data-ttu-id="7f158-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f158-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7f158-113">Una sottoscrizione di Citrix GoToMeeting abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7f158-113">A Citrix GoToMeeting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7f158-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="7f158-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7f158-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7f158-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7f158-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="7f158-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7f158-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7f158-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7f158-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="7f158-118">Scenario description</span></span>
<span data-ttu-id="7f158-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="7f158-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7f158-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7f158-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7f158-121">Aggiunta di Citrix GoToMeeting dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="7f158-121">Adding Citrix GoToMeeting from the gallery</span></span>
2. <span data-ttu-id="7f158-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f158-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-citrix-gotomeeting-from-the-gallery"></a><span data-ttu-id="7f158-123">Aggiunta di Citrix GoToMeeting dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="7f158-123">Adding Citrix GoToMeeting from the gallery</span></span>
<span data-ttu-id="7f158-124">Per configurare l'integrazione di Citrix GoToMeeting in Azure AD, è necessario aggiungere Citrix GoToMeeting dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="7f158-124">To configure the integration of Citrix GoToMeeting into Azure AD, you need to add Citrix GoToMeeting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7f158-125">**Per aggiungere Citrix GoToMeeting dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7f158-125">**To add Citrix GoToMeeting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7f158-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="7f158-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7f158-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="7f158-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7f158-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7f158-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="7f158-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="7f158-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="7f158-133">Nella casella di ricerca digitare **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="7f158-133">In the search box, type **Citrix GoToMeeting**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. <span data-ttu-id="7f158-135">Nel pannello dei risultati selezionare **Citrix GoToMeeting** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7f158-135">In the results panel, select **Citrix GoToMeeting**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7f158-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f158-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7f158-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Citrix GoToMeeting in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7f158-138">In this section, you configure and test Azure AD single sign-on with Citrix GoToMeeting based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7f158-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente di Citrix GoToMeeting che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f158-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix GoToMeeting is to a user in Azure AD.</span></span> <span data-ttu-id="7f158-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="7f158-140">In other words, a link relationship between an Azure AD user and the related user in Citrix GoToMeeting needs to be established.</span></span>

<span data-ttu-id="7f158-141">La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **NomeUtente** in Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="7f158-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Citrix GoToMeeting.</span></span>

<span data-ttu-id="7f158-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Citrix GoToMeeting, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7f158-142">To configure and test Azure AD single sign-on with Citrix GoToMeeting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7f158-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7f158-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7f158-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7f158-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7f158-145">**[Creazione di un utente test di Citrix GoToMeeting](#creating-a-citrix-gotomeeting-test-user)**: per avere una controparte di Britta Simon in Citrix GoToMeeting collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f158-145">**[Creating a Citrix GoToMeeting test user](#creating-a-citrix-gotomeeting-test-user)** - to have a counterpart of Britta Simon in Citrix GoToMeeting that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7f158-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f158-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7f158-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="7f158-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7f158-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f158-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7f158-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="7f158-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix GoToMeeting application.</span></span>

<span data-ttu-id="7f158-150">**Per configurare Single Sign-On di Azure AD con Citrix GoToMeeting, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7f158-150">**To configure Azure AD single sign-on with Citrix GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="7f158-151">Nella pagina di integrazione dell'applicazione **Citrix GoToMeeting** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="7f158-151">In the Azure portal, on the **Citrix GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="7f158-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="7f158-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. <span data-ttu-id="7f158-155">Non è necessario eseguire alcuna operazione nella sezione **URL e dominio Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="7f158-155">On the **Citrix GoToMeeting Domain and URLs** section, no need to perform any steps.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. <span data-ttu-id="7f158-157">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="7f158-157">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. <span data-ttu-id="7f158-159">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="7f158-159">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. <span data-ttu-id="7f158-161">Nella sezione Configurazione Citrix GoToMeeting SAML scegliere Configura Citrix GoToMeeting SAML per aprire la finestra Configura accesso.</span><span class="sxs-lookup"><span data-stu-id="7f158-161">On the Citrix GoToMeeting SAML Configuration section, click Configure Citrix GoToMeeting SAML to open Configure sign-on window.</span></span> <span data-ttu-id="7f158-162">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="7f158-162">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

6. <span data-ttu-id="7f158-163">In un'altra finestra del browser accedere al sito [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span><span class="sxs-lookup"><span data-stu-id="7f158-163">In a different browser window, log in to your [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

7. <span data-ttu-id="7f158-164">Fare clic sulla scheda **Identity Provider** e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7f158-164">Click the **Identity Provider** tab, and then perform the following steps:</span></span>  
   
    <span data-ttu-id="7f158-165">![Configurazione SAML](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "Configurazione SAML")</span><span class="sxs-lookup"><span data-stu-id="7f158-165">![SAML setup](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="7f158-166">a.</span><span class="sxs-lookup"><span data-stu-id="7f158-166">a.</span></span> <span data-ttu-id="7f158-167">Selezionare **Manual**</span><span class="sxs-lookup"><span data-stu-id="7f158-167">Select **Manual**</span></span>

    <span data-ttu-id="7f158-168">b.</span><span class="sxs-lookup"><span data-stu-id="7f158-168">b.</span></span> <span data-ttu-id="7f158-169">Nella finestra di dialogo **Configura accesso Single Sign-On in Citrix GoToMeeting** del portale di Azure copiare il valore di **URL servizio Single Sign-On SAML** e incollarlo nella casella di testo dell'**URL della pagina di accesso**.</span><span class="sxs-lookup"><span data-stu-id="7f158-169">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="7f158-170">c.</span><span class="sxs-lookup"><span data-stu-id="7f158-170">c.</span></span> <span data-ttu-id="7f158-171">Nella finestra di dialogo **Configura accesso Single Sign-On in Citrix GoToMeeting** del portale di Azure copiare il valore di **URL di disconnessione** e incollarlo nella casella di testo dell'**URL della pagina di disconnessione**.</span><span class="sxs-lookup"><span data-stu-id="7f158-171">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **Sign-Out URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="7f158-172">d.</span><span class="sxs-lookup"><span data-stu-id="7f158-172">d.</span></span> <span data-ttu-id="7f158-173">Nella finestra di dialogo **Configura accesso Single Sign-On in Citrix GoToMeeting** del portale di Azure copiare il valore di **ID entità SAML** e incollarlo nella casella di testo dell'**ID entità del provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="7f158-173">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **SAML Entity ID** value, and then paste it into the **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="7f158-174">e.</span><span class="sxs-lookup"><span data-stu-id="7f158-174">e.</span></span> <span data-ttu-id="7f158-175">Per caricare il certificato scaricato, fare clic su **Upload Certificate**.</span><span class="sxs-lookup"><span data-stu-id="7f158-175">To upload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="7f158-176">f.</span><span class="sxs-lookup"><span data-stu-id="7f158-176">f.</span></span> <span data-ttu-id="7f158-177">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="7f158-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7f158-178">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="7f158-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7f158-179">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="7f158-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7f158-180">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7f158-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7f158-181">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f158-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="7f158-182">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f158-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="7f158-184">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7f158-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7f158-185">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="7f158-185">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7f158-187">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="7f158-187">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7f158-189">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="7f158-189">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7f158-191">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7f158-191">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7f158-193">a.</span><span class="sxs-lookup"><span data-stu-id="7f158-193">a.</span></span> <span data-ttu-id="7f158-194">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7f158-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7f158-195">b.</span><span class="sxs-lookup"><span data-stu-id="7f158-195">b.</span></span> <span data-ttu-id="7f158-196">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7f158-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7f158-197">c.</span><span class="sxs-lookup"><span data-stu-id="7f158-197">c.</span></span> <span data-ttu-id="7f158-198">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="7f158-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7f158-199">d.</span><span class="sxs-lookup"><span data-stu-id="7f158-199">d.</span></span> <span data-ttu-id="7f158-200">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7f158-200">Click **Create**.</span></span>
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a><span data-ttu-id="7f158-201">Creazione di un utente test Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="7f158-201">Creating a Citrix GoToMeeting test user</span></span>

<span data-ttu-id="7f158-202">In questa sezione viene creato un utente di nome Britta Simon in Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="7f158-202">In this section, a user called Britta Simon is created in Citrix GoToMeeting.</span></span> <span data-ttu-id="7f158-203">Citrix GoToMeeting supporta il provisioning JIT (Just-In-Time) che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="7f158-203">Citrix GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="7f158-204">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="7f158-204">There is no action item for you in this section.</span></span> <span data-ttu-id="7f158-205">Se un utente non esiste in Citrix GoToMeeting, ne viene creato uno nuovo quando si tenta di accedere a Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="7f158-205">If a user doesn't already exist in Citrix GoToMeeting, a new one is created when you attempt to access Citrix GoToMeeting.</span></span>

>[!Note]
><span data-ttu-id="7f158-206">Se è necessario creare un utente manualmente, contattare il [team di supporto di Citrix GoToMeeting](https://care.citrixonline.com/gotomeeting)</span><span class="sxs-lookup"><span data-stu-id="7f158-206">If you need to create a user manually, Contact [Citrix GoToMeeting support team](https://care.citrixonline.com/gotomeeting)</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7f158-207">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f158-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7f158-208">In questa sezione si abilita Britta Simon all'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="7f158-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix GoToMeeting.</span></span>

![Assegna utente][200] 

<span data-ttu-id="7f158-210">**Per assegnare Britta Simon a Citrix GoToMeeting, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="7f158-210">**To assign Britta Simon to Citrix GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="7f158-211">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7f158-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="7f158-213">Nell'elenco delle applicazioni, selezionare **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="7f158-213">In the applications list, select **Citrix GoToMeeting**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. <span data-ttu-id="7f158-215">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="7f158-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="7f158-217">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7f158-217">Click **Add** button.</span></span> <span data-ttu-id="7f158-218">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7f158-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="7f158-220">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="7f158-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7f158-221">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7f158-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7f158-222">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7f158-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7f158-223">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7f158-223">Testing single sign-on</span></span>

<span data-ttu-id="7f158-224">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="7f158-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7f158-225">Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="7f158-225">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="7f158-226">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7f158-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7f158-227">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="7f158-227">Additional resources</span></span>

* [<span data-ttu-id="7f158-228">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f158-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7f158-229">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f158-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="7f158-230">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="7f158-230">Configure User Provisioning</span></span>](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png

