---
title: 'Esercitazione: Integrazione di Azure Active Directory con Kudos | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Kudos.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 353798fcfd4ad7ce017fc2fddf4110715db3ace2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a><span data-ttu-id="78cd0-103">Esercitazione: integrazione di Azure Active Directory con Kudos</span><span class="sxs-lookup"><span data-stu-id="78cd0-103">Tutorial: Azure Active Directory integration with Kudos</span></span>

<span data-ttu-id="78cd0-104">Questa esercitazione descrive come integrare Kudos con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="78cd0-104">In this tutorial, you learn how to integrate Kudos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="78cd0-105">L'integrazione di Kudos con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="78cd0-105">Integrating Kudos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="78cd0-106">È possibile controllare in Azure AD chi può accedere a Kudos</span><span class="sxs-lookup"><span data-stu-id="78cd0-106">You can control in Azure AD who has access to Kudos</span></span>
- <span data-ttu-id="78cd0-107">È possibile abilitare gli utenti per l'accesso automatico a Kudos (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="78cd0-107">You can enable your users to automatically get signed-on to Kudos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="78cd0-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="78cd0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="78cd0-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="78cd0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78cd0-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="78cd0-110">Prerequisites</span></span>

<span data-ttu-id="78cd0-111">Per configurare l'integrazione di Azure AD con Kudos, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="78cd0-111">To configure Azure AD integration with Kudos, you need the following items:</span></span>

- <span data-ttu-id="78cd0-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78cd0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="78cd0-113">Sottoscrizione di Kudos abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="78cd0-113">A Kudos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="78cd0-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="78cd0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="78cd0-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="78cd0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="78cd0-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="78cd0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="78cd0-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="78cd0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="78cd0-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="78cd0-118">Scenario description</span></span>
<span data-ttu-id="78cd0-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="78cd0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="78cd0-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="78cd0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="78cd0-121">Aggiunta di Kudos dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="78cd0-121">Adding Kudos from the gallery</span></span>
2. <span data-ttu-id="78cd0-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="78cd0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kudos-from-the-gallery"></a><span data-ttu-id="78cd0-123">Aggiunta di Kudos dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="78cd0-123">Adding Kudos from the gallery</span></span>
<span data-ttu-id="78cd0-124">Per configurare l'integrazione di Kudos in Azure AD, è necessario aggiungere Kudos dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="78cd0-124">To configure the integration of Kudos into Azure AD, you need to add Kudos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="78cd0-125">**Per aggiungere Kudos dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="78cd0-125">**To add Kudos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="78cd0-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="78cd0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="78cd0-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="78cd0-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="78cd0-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="78cd0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="78cd0-133">Nella casella di ricerca digitare **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-133">In the search box, type **Kudos**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_search.png)

5. <span data-ttu-id="78cd0-135">Nel pannello dei risultati selezionare **Kudos** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="78cd0-135">In the results panel, select **Kudos**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="78cd0-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="78cd0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="78cd0-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Kudos usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="78cd0-138">In this section, you configure and test Azure AD single sign-on with Kudos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="78cd0-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente controparte di Kudos che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78cd0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kudos is to a user in Azure AD.</span></span> <span data-ttu-id="78cd0-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Kudos.</span><span class="sxs-lookup"><span data-stu-id="78cd0-140">In other words, a link relationship between an Azure AD user and the related user in Kudos needs to be established.</span></span>

<span data-ttu-id="78cd0-141">Per stabilire la relazione di collegamento, in Kudos assegnare il valore di **nome utente** di Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="78cd0-141">In Kudos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="78cd0-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Kudos, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="78cd0-142">To configure and test Azure AD single sign-on with Kudos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="78cd0-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="78cd0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="78cd0-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="78cd0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="78cd0-145">**[Creazione di un utente test di Kudos](#creating-a-kudos-test-user)**: per avere una controparte di Britta Simon in Kudos collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78cd0-145">**[Creating a Kudos test user](#creating-a-kudos-test-user)** - to have a counterpart of Britta Simon in Kudos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="78cd0-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78cd0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="78cd0-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="78cd0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="78cd0-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="78cd0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="78cd0-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Kudos.</span><span class="sxs-lookup"><span data-stu-id="78cd0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kudos application.</span></span>

<span data-ttu-id="78cd0-150">**Per configurare l'accesso Single Sign-On di Azure AD con Kudos, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="78cd0-150">**To configure Azure AD single sign-on with Kudos, perform the following steps:**</span></span>

1. <span data-ttu-id="78cd0-151">Nella pagina di integrazione dell'applicazione **Kudos** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-151">In the Azure portal, on the **Kudos** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="78cd0-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="78cd0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_samlbase.png)

3. <span data-ttu-id="78cd0-155">Nella sezione **URL e dominio Kudos** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="78cd0-155">On the **Kudos Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_url.png)

    <span data-ttu-id="78cd0-157">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<company>.kudosnow.com`</span><span class="sxs-lookup"><span data-stu-id="78cd0-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.kudosnow.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="78cd0-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="78cd0-158">This value is not real.</span></span> <span data-ttu-id="78cd0-159">aggiornare questo valore con l'URL di accesso effettivo.</span><span class="sxs-lookup"><span data-stu-id="78cd0-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="78cd0-160">Per ottenere questo valore, contattare il [team di supporto clienti di Kudos](http://success.kudosnow.com/home).</span><span class="sxs-lookup"><span data-stu-id="78cd0-160">Contact [Kudos Client support team](http://success.kudosnow.com/home) to get this value.</span></span> 
 
4. <span data-ttu-id="78cd0-161">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="78cd0-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_certificate.png) 

5. <span data-ttu-id="78cd0-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="78cd0-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kudos-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="78cd0-165">Nella sezione **Configurazione di Kudos** fare clic su **Configura Kudos** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-165">On the **Kudos Configuration** section, click **Configure Kudos** to open **Configure sign-on** window.</span></span> <span data-ttu-id="78cd0-166">Copiare l'**URL servizio Single Sign-On SAML e l'URL di disconnessione** dalla sezione **Riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-166">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_configure.png) 

7. <span data-ttu-id="78cd0-168">In un'altra finestra del Web browser accedere al sito aziendale di Kudos come amministratore.</span><span class="sxs-lookup"><span data-stu-id="78cd0-168">In a different web browser window, log into your Kudos company site as an administrator.</span></span>

8. <span data-ttu-id="78cd0-169">Nel menu in alto fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-169">In the menu on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="78cd0-170">![Impostazioni](./media/active-directory-saas-kudos-tutorial/ic787806.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="78cd0-170">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

9. <span data-ttu-id="78cd0-171">Fare clic su **Integrations (Integrazioni) \> SSO**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-171">Click **Integrations \> SSO**.</span></span>

10. <span data-ttu-id="78cd0-172">Nella sezione **SSO** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="78cd0-172">In the **SSO** section, perform the following steps:</span></span>
   
    <span data-ttu-id="78cd0-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span><span class="sxs-lookup"><span data-stu-id="78cd0-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span></span>
   
    <span data-ttu-id="78cd0-174">a.</span><span class="sxs-lookup"><span data-stu-id="78cd0-174">a.</span></span> <span data-ttu-id="78cd0-175">Nella casella di testo **Sign on URL** (URL di accesso) incollare il valore di **SAML Single Sign-On Service URL** (URL servizio Single Sign-On) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="78cd0-175">In **Sign on URL** textbox, paste the value of  **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="78cd0-176">b.</span><span class="sxs-lookup"><span data-stu-id="78cd0-176">b.</span></span> <span data-ttu-id="78cd0-177">Aprire il certificato con codifica base 64 nel blocco note, copiarne il contenuto negli appunti e incollarlo nella casella di testo **Certificato X.509**</span><span class="sxs-lookup"><span data-stu-id="78cd0-177">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 certificate** textbox</span></span>
   
    <span data-ttu-id="78cd0-178">c.</span><span class="sxs-lookup"><span data-stu-id="78cd0-178">c.</span></span> <span data-ttu-id="78cd0-179">In **Logout To URL** (URL di disconnessione) incollare il valore di **Sign-Out URL** (URL di disconnessione) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="78cd0-179">In **Logout To URL**, paste the value of  **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="78cd0-180">d.</span><span class="sxs-lookup"><span data-stu-id="78cd0-180">d.</span></span> <span data-ttu-id="78cd0-181">Nella casella di testo **URL di Kudos** digitare il nome della società.</span><span class="sxs-lookup"><span data-stu-id="78cd0-181">In the **Your Kudos URL** textbox, type your company name.</span></span>
   
    <span data-ttu-id="78cd0-182">e.</span><span class="sxs-lookup"><span data-stu-id="78cd0-182">e.</span></span> <span data-ttu-id="78cd0-183">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="78cd0-184">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="78cd0-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="78cd0-185">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="78cd0-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="78cd0-186">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="78cd0-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="78cd0-187">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="78cd0-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="78cd0-188">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="78cd0-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="78cd0-190">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="78cd0-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="78cd0-191">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="78cd0-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="78cd0-193">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="78cd0-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="78cd0-195">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="78cd0-197">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="78cd0-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="78cd0-199">a.</span><span class="sxs-lookup"><span data-stu-id="78cd0-199">a.</span></span> <span data-ttu-id="78cd0-200">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="78cd0-201">b.</span><span class="sxs-lookup"><span data-stu-id="78cd0-201">b.</span></span> <span data-ttu-id="78cd0-202">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="78cd0-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="78cd0-203">c.</span><span class="sxs-lookup"><span data-stu-id="78cd0-203">c.</span></span> <span data-ttu-id="78cd0-204">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="78cd0-205">d.</span><span class="sxs-lookup"><span data-stu-id="78cd0-205">d.</span></span> <span data-ttu-id="78cd0-206">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-206">Click **Create**.</span></span>
 
### <a name="creating-a-kudos-test-user"></a><span data-ttu-id="78cd0-207">Creazione di un utente test di Kudos</span><span class="sxs-lookup"><span data-stu-id="78cd0-207">Creating a Kudos test user</span></span>

<span data-ttu-id="78cd0-208">Per consentire agli utenti di Azure AD di accedere a Kudos, è necessario eseguirne il provisioning in Kudos.</span><span class="sxs-lookup"><span data-stu-id="78cd0-208">In order to enable Azure AD users to log into Kudos, they must be provisioned into Kudos.</span></span> 

<span data-ttu-id="78cd0-209">Nel caso di Kudos, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="78cd0-209">In the case of Kudos, provisioning is a manual task.</span></span>

<span data-ttu-id="78cd0-210">**Per eseguire il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="78cd0-210">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="78cd0-211">Accedere al sito aziendale di **Kudos** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="78cd0-211">Log in to your **Kudos** company site as administrator.</span></span>

2. <span data-ttu-id="78cd0-212">Nel menu in alto fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-212">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="78cd0-213">![Impostazioni](./media/active-directory-saas-kudos-tutorial/ic787806.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="78cd0-213">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

3. <span data-ttu-id="78cd0-214">Fare clic su **User Admin**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-214">Click **User Admin**.</span></span>

4. <span data-ttu-id="78cd0-215">Fare clic sulla scheda **Users** (Utenti) e quindi su **Add a User** (Aggiungi un utente).</span><span class="sxs-lookup"><span data-stu-id="78cd0-215">Click the **Users** tab, and then click **Add a User**.</span></span>
   
   <span data-ttu-id="78cd0-216">![Amministratore utenti](./media/active-directory-saas-kudos-tutorial/ic787809.png "Amministratore utenti")</span><span class="sxs-lookup"><span data-stu-id="78cd0-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin")</span></span>

5. <span data-ttu-id="78cd0-217">Nella sezione **Aggiungi un utente** eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="78cd0-217">In the **Add a User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="78cd0-218">![Aggiungere un utente](./media/active-directory-saas-kudos-tutorial/ic787810.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="78cd0-218">![Add a User](./media/active-directory-saas-kudos-tutorial/ic787810.png "Add a User")</span></span>
   
    <span data-ttu-id="78cd0-219">a.</span><span class="sxs-lookup"><span data-stu-id="78cd0-219">a.</span></span> <span data-ttu-id="78cd0-220">Nelle caselle **First Name**, **Last Name**, **Email** e così via immettere il nome, cognome, indirizzo di posta elettronica e altri dettagli di un account Azure Active Directory valido di cui si vuole eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="78cd0-220">Type the **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="78cd0-221">b.</span><span class="sxs-lookup"><span data-stu-id="78cd0-221">b.</span></span> <span data-ttu-id="78cd0-222">Fare clic su **Create User**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-222">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="78cd0-223">È possibile utilizzare qualsiasi altro strumento di creazione di account utente di Kudos o le API fornite da Kudos per eseguire il provisioning degli account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="78cd0-223">You can use any other Kudos user account creation tools or APIs provided by Kudos to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="78cd0-224">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="78cd0-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="78cd0-225">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Kudos.</span><span class="sxs-lookup"><span data-stu-id="78cd0-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kudos.</span></span>

![Assegna utente][200] 

<span data-ttu-id="78cd0-227">**Per assegnare Britta Simon a Kudos, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="78cd0-227">**To assign Britta Simon to Kudos, perform the following steps:**</span></span>

1. <span data-ttu-id="78cd0-228">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="78cd0-230">Nell'elenco delle applicazioni selezionare **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-230">In the applications list, select **Kudos**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_app.png) 

3. <span data-ttu-id="78cd0-232">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="78cd0-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="78cd0-234">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-234">Click **Add** button.</span></span> <span data-ttu-id="78cd0-235">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="78cd0-237">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="78cd0-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="78cd0-238">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="78cd0-239">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="78cd0-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="78cd0-240">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="78cd0-240">Testing single sign-on</span></span>

<span data-ttu-id="78cd0-241">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="78cd0-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="78cd0-242">Quando si fa clic sul riquadro Kudos nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Kudos.</span><span class="sxs-lookup"><span data-stu-id="78cd0-242">When you click the Kudos tile in the Access Panel, you should get automatically signed-on to your Kudos application.</span></span> <span data-ttu-id="78cd0-243">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="78cd0-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="78cd0-244">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="78cd0-244">Additional resources</span></span>

* [<span data-ttu-id="78cd0-245">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78cd0-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="78cd0-246">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78cd0-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_203.png

