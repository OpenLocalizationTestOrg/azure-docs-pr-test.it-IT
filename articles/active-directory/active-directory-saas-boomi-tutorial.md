---
title: 'Esercitazione: Integrazione di Azure Active Directory con Boomi | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Boomi.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 1121d22beddf73fd2109a4b410422f76dd37478e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a><span data-ttu-id="dbff3-103">Esercitazione: Integrazione di Azure Active Directory con Boomi</span><span class="sxs-lookup"><span data-stu-id="dbff3-103">Tutorial: Azure Active Directory integration with Boomi</span></span>

<span data-ttu-id="dbff3-104">Questa esercitazione descrive come integrare Boomi con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dbff3-104">In this tutorial, you learn how to integrate Boomi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dbff3-105">L'integrazione di Boomi con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="dbff3-105">Integrating Boomi with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dbff3-106">È possibile controllare in Azure AD chi può accedere a Boomi</span><span class="sxs-lookup"><span data-stu-id="dbff3-106">You can control in Azure AD who has access to Boomi</span></span>
- <span data-ttu-id="dbff3-107">È possibile abilitare gli utenti per l'accesso automatico a Boomi (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbff3-107">You can enable your users to automatically get signed-on to Boomi (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dbff3-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dbff3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dbff3-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dbff3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbff3-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dbff3-110">Prerequisites</span></span>

<span data-ttu-id="dbff3-111">Per configurare l'integrazione di Azure AD con Boomi, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="dbff3-111">To configure Azure AD integration with Boomi, you need the following items:</span></span>

- <span data-ttu-id="dbff3-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dbff3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dbff3-113">Sottoscrizione di Boomi abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="dbff3-113">A Boomi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dbff3-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="dbff3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dbff3-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="dbff3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dbff3-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="dbff3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dbff3-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dbff3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dbff3-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="dbff3-118">Scenario description</span></span>
<span data-ttu-id="dbff3-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="dbff3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dbff3-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="dbff3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dbff3-121">Aggiunta di Boomi dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="dbff3-121">Adding Boomi from the gallery</span></span>
2. <span data-ttu-id="dbff3-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbff3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-boomi-from-the-gallery"></a><span data-ttu-id="dbff3-123">Aggiunta di Boomi dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="dbff3-123">Adding Boomi from the gallery</span></span>
<span data-ttu-id="dbff3-124">Per configurare l'integrazione di Boomi in Azure AD, è necessario aggiungere Boomi dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="dbff3-124">To configure the integration of Boomi into Azure AD, you need to add Boomi from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dbff3-125">**Per aggiungere Boomi dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="dbff3-125">**To add Boomi from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dbff3-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="dbff3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dbff3-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dbff3-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="dbff3-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="dbff3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="dbff3-133">Nella casella di ricerca digitare **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-133">In the search box, type **Boomi**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. <span data-ttu-id="dbff3-135">Nel pannello dei risultati selezionare **Boomi** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="dbff3-135">In the results panel, select **Boomi**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dbff3-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbff3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dbff3-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Boomi in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dbff3-138">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dbff3-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Boomi che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dbff3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Boomi is to a user in Azure AD.</span></span> <span data-ttu-id="dbff3-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Boomi.</span><span class="sxs-lookup"><span data-stu-id="dbff3-140">In other words, a link relationship between an Azure AD user and the related user in Boomi needs to be established.</span></span>

<span data-ttu-id="dbff3-141">Per stabilire la relazione di collegamento, in Boomi assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="dbff3-141">In Boomi, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dbff3-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Boomi, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="dbff3-142">To configure and test Azure AD single sign-on with Boomi, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dbff3-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="dbff3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dbff3-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dbff3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dbff3-145">**[Creazione di un utente test di Boomi](#creating-a-boomi-test-user)**: per avere una controparte di Britta Simon in Boomi collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dbff3-145">**[Creating a Boomi test user](#creating-a-boomi-test-user)** - to have a counterpart of Britta Simon in Boomi that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dbff3-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dbff3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dbff3-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="dbff3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dbff3-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbff3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dbff3-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Boomi.</span><span class="sxs-lookup"><span data-stu-id="dbff3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Boomi application.</span></span>

<span data-ttu-id="dbff3-150">**Per configurare l'accesso Single Sign-On di Azure AD con Boomi, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="dbff3-150">**To configure Azure AD single sign-on with Boomi, perform the following steps:**</span></span>

1. <span data-ttu-id="dbff3-151">Nella pagina di integrazione dell'applicazione **Boomi** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-151">In the Azure portal, on the **Boomi** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="dbff3-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="dbff3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. <span data-ttu-id="dbff3-155">Nella sezione **URL e dominio Boomi** eseguire i passaggi descritti di seguito:</span><span class="sxs-lookup"><span data-stu-id="dbff3-155">On the **Boomi Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    <span data-ttu-id="dbff3-157">a.</span><span class="sxs-lookup"><span data-stu-id="dbff3-157">a.</span></span> <span data-ttu-id="dbff3-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="dbff3-158">In the **Identifier** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    <span data-ttu-id="dbff3-159">b.</span><span class="sxs-lookup"><span data-stu-id="dbff3-159">b.</span></span> <span data-ttu-id="dbff3-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="dbff3-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dbff3-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="dbff3-161">These values are not real.</span></span> <span data-ttu-id="dbff3-162">è necessario aggiornarli con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="dbff3-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="dbff3-163">Per ottenere tali valori, [contattare il team di supporto di Boomi](https://boomi.com/company/contact/).</span><span class="sxs-lookup"><span data-stu-id="dbff3-163">Contact [Boomi support team](https://boomi.com/company/contact/) to get these values.</span></span>

4. <span data-ttu-id="dbff3-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="dbff3-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. <span data-ttu-id="dbff3-166">L'applicazione Boomi prevede che le asserzioni SAML abbiano un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="dbff3-166">Boomi application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="dbff3-167">Configurare le attestazioni seguenti per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="dbff3-167">Please configure the following claims for this application.</span></span> <span data-ttu-id="dbff3-168">È possibile gestire i valori di questi attributi dalla sezione "**Attributi utente**" nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="dbff3-168">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="dbff3-169">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="dbff3-169">The following screenshot shows an example for this.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="dbff3-171">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On** per ogni riga illustrata nella tabella seguente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="dbff3-171">In the **User Attributes** section on the **Single sign-on** dialog, for each row shown in the table below, perform the following steps:</span></span>

    | <span data-ttu-id="dbff3-172">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="dbff3-172">Attribute Name</span></span> | <span data-ttu-id="dbff3-173">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="dbff3-173">Attribute Value</span></span> |
    | -------------- | --------------- |
    | <span data-ttu-id="dbff3-174">FEDERATION_ID</span><span class="sxs-lookup"><span data-stu-id="dbff3-174">FEDERATION_ID</span></span> | <span data-ttu-id="dbff3-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="dbff3-175">user.mail</span></span> |
    
    <span data-ttu-id="dbff3-176">a.</span><span class="sxs-lookup"><span data-stu-id="dbff3-176">a.</span></span> <span data-ttu-id="dbff3-177">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="dbff3-180">b.</span><span class="sxs-lookup"><span data-stu-id="dbff3-180">b.</span></span> <span data-ttu-id="dbff3-181">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="dbff3-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="dbff3-182">c.</span><span class="sxs-lookup"><span data-stu-id="dbff3-182">c.</span></span> <span data-ttu-id="dbff3-183">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="dbff3-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="dbff3-184">d.</span><span class="sxs-lookup"><span data-stu-id="dbff3-184">d.</span></span> <span data-ttu-id="dbff3-185">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-185">Click **Ok**.</span></span>

6. <span data-ttu-id="dbff3-186">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="dbff3-186">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="dbff3-188">Nella sezione **Configurazione di Boomi** fare clic su **Configura Boomi** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-188">On the **Boomi Configuration** section, click **Configure Boomi** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dbff3-189">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="dbff3-189">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. <span data-ttu-id="dbff3-191">In un'altra finestra del Web browser accedere al sito aziendale di Boomi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="dbff3-191">In a different web browser window, log into your Boomi company site as an administrator.</span></span> 

9. <span data-ttu-id="dbff3-192">Passare a **Nome società** e scegliere **Configurazione**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-192">Navigate to **Company Name** and go to **Set up**.</span></span>

10. <span data-ttu-id="dbff3-193">Fare clic sulla scheda **Opzioni SSO** e seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="dbff3-193">Click the **SSO Options** tab and perform below steps.</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    <span data-ttu-id="dbff3-195">a.</span><span class="sxs-lookup"><span data-stu-id="dbff3-195">a.</span></span> <span data-ttu-id="dbff3-196">Selezionare la casella di controllo **Abilita Single Sign-On SAML**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-196">Check **Enable SAML Single Sign-On** checkbox.</span></span>

    <span data-ttu-id="dbff3-197">b.</span><span class="sxs-lookup"><span data-stu-id="dbff3-197">b.</span></span> <span data-ttu-id="dbff3-198">Fare clic su **Importa** per caricare il certificato scaricato da Azure AD in **Identity Provider Certificate** (Certificato del Provider di identità).</span><span class="sxs-lookup"><span data-stu-id="dbff3-198">Click **Import** to upload the downloaded certificate from Azure AD to **Identity Provider Certificate**.</span></span>
    
    <span data-ttu-id="dbff3-199">c.</span><span class="sxs-lookup"><span data-stu-id="dbff3-199">c.</span></span> <span data-ttu-id="dbff3-200">Nella casella di testo **URL di accesso provider di identità** inserire il valore di **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) dalla finestra di configurazione dell'applicazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dbff3-200">In the **Identity Provider Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="dbff3-201">d.</span><span class="sxs-lookup"><span data-stu-id="dbff3-201">d.</span></span> <span data-ttu-id="dbff3-202">Come **Federation Id Location** selezionare il pulsante di opzione **Federation Id is in FEDERATION_ID Attribute element**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-202">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span></span> 

    <span data-ttu-id="dbff3-203">e.</span><span class="sxs-lookup"><span data-stu-id="dbff3-203">e.</span></span> <span data-ttu-id="dbff3-204">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="dbff3-204">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="dbff3-205">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="dbff3-205">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dbff3-206">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="dbff3-206">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dbff3-207">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dbff3-207">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dbff3-208">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbff3-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="dbff3-209">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dbff3-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="dbff3-211">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="dbff3-211">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dbff3-212">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="dbff3-212">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dbff3-214">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="dbff3-214">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dbff3-216">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-216">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dbff3-218">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="dbff3-218">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dbff3-220">a.</span><span class="sxs-lookup"><span data-stu-id="dbff3-220">a.</span></span> <span data-ttu-id="dbff3-221">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-221">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dbff3-222">b.</span><span class="sxs-lookup"><span data-stu-id="dbff3-222">b.</span></span> <span data-ttu-id="dbff3-223">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dbff3-223">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dbff3-224">c.</span><span class="sxs-lookup"><span data-stu-id="dbff3-224">c.</span></span> <span data-ttu-id="dbff3-225">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-225">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dbff3-226">d.</span><span class="sxs-lookup"><span data-stu-id="dbff3-226">d.</span></span> <span data-ttu-id="dbff3-227">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-227">Click **Create**.</span></span>
 
### <a name="creating-a-boomi-test-user"></a><span data-ttu-id="dbff3-228">Creazione di un utente test di Boomi</span><span class="sxs-lookup"><span data-stu-id="dbff3-228">Creating a Boomi test user</span></span>

<span data-ttu-id="dbff3-229">Per consentire agli utenti di Azure AD di accedere a Boomi, è necessario eseguirne il provisioning in Boomi.</span><span class="sxs-lookup"><span data-stu-id="dbff3-229">In order to enable Azure AD users to log in to Boomi, they must be provisioned into Boomi.</span></span> <span data-ttu-id="dbff3-230">Nel caso di Boomi, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="dbff3-230">In the case of Boomi, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="dbff3-231">Per eseguire il provisioning di un account utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="dbff3-231">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="dbff3-232">Accedere al sito aziendale di Boomi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="dbff3-232">Log in to your Boomi company site as an administrator.</span></span>

2. <span data-ttu-id="dbff3-233">Dopo aver effettuato l'accesso, passare a **Gestione utenti** e scegliere **Utenti**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-233">After logging in, navigate to **User Management** and go to **Users**.</span></span>

    <span data-ttu-id="dbff3-234">![Utenti](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="dbff3-234">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")</span></span>

3. <span data-ttu-id="dbff3-235">Fare clic sull'icona **+**. Si aprirà la finestra di dialogo **Add/Maintain User Roles** (Aggiungi/Gestisci ruoli utente).</span><span class="sxs-lookup"><span data-stu-id="dbff3-235">Click **+**  icon and the **Add/Maintain User Roles** dialog opens.</span></span>

    <span data-ttu-id="dbff3-236">![Utenti](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="dbff3-236">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")</span></span>

    <span data-ttu-id="dbff3-237">![Utenti](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="dbff3-237">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")</span></span>

    <span data-ttu-id="dbff3-238">a.</span><span class="sxs-lookup"><span data-stu-id="dbff3-238">a.</span></span> <span data-ttu-id="dbff3-239">Nella casella di testo **Indirizzo di posta elettronica utente** digitare l'indirizzo di posta elettronica dell'utente, ad esempio BrittaSimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="dbff3-239">In the **User e-mail address** textbox, type the email of user like BrittaSimon@contoso.com.</span></span>
    
    <span data-ttu-id="dbff3-240">b.</span><span class="sxs-lookup"><span data-stu-id="dbff3-240">b.</span></span> <span data-ttu-id="dbff3-241">Digitare il nome dell'utente, ad esempio Britta, nella casella di testo **Nome**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-241">In the **First name** textbox, type the First name of user like Britta.</span></span>

    <span data-ttu-id="dbff3-242">c.</span><span class="sxs-lookup"><span data-stu-id="dbff3-242">c.</span></span> <span data-ttu-id="dbff3-243">Digitare il nome dell'utente, ad esempio Simon, nella casella di testo **Cognome**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-243">In the **Last name** textbox, type the Last name of user like Simon.</span></span>
    
    <span data-ttu-id="dbff3-244">d.</span><span class="sxs-lookup"><span data-stu-id="dbff3-244">d.</span></span> <span data-ttu-id="dbff3-245">Immettere l'**ID federazione** dell'utente.</span><span class="sxs-lookup"><span data-stu-id="dbff3-245">Enter the user's **Federation ID**.</span></span> <span data-ttu-id="dbff3-246">Ogni utente deve avere un ID federazione che lo identifichi in modo univoco all'interno dell'account.</span><span class="sxs-lookup"><span data-stu-id="dbff3-246">Each user must have a Federation ID that uniquely identifies the user within the account.</span></span>
    
    <span data-ttu-id="dbff3-247">e.</span><span class="sxs-lookup"><span data-stu-id="dbff3-247">e.</span></span> <span data-ttu-id="dbff3-248">Assegnare il ruolo **Utente standard** all'utente.</span><span class="sxs-lookup"><span data-stu-id="dbff3-248">Assign the **Standard User** role to the user.</span></span> <span data-ttu-id="dbff3-249">Non assegnare il ruolo Amministratore perché altrimenti l'utente avrebbe l'accesso normale ad AtomSphere, nonché l'accesso Single Sign-on.</span><span class="sxs-lookup"><span data-stu-id="dbff3-249">Do not assign the Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span></span>
    
    <span data-ttu-id="dbff3-250">f.</span><span class="sxs-lookup"><span data-stu-id="dbff3-250">f.</span></span> <span data-ttu-id="dbff3-251">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-251">Click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="dbff3-252">L'utente non riceverà un messaggio di notifica di benvenuto contenente una password che può essere utilizzata per accedere all'account di AtomSphere perché la password viene gestita tramite il provider di identità.</span><span class="sxs-lookup"><span data-stu-id="dbff3-252">The user will not receive a welcome notification email containing a password that can be used to log in to the AtomSphere account because his password is managed through the identity provider.</span></span> <span data-ttu-id="dbff3-253">È possibile usare qualsiasi altro strumento o API di creazione di account utente fornita da Boomi per eseguire il provisioning degli account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="dbff3-253">You may use any other Boomi user account creation tools or APIs provided by Boomi to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dbff3-254">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="dbff3-254">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dbff3-255">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Boomi.</span><span class="sxs-lookup"><span data-stu-id="dbff3-255">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Boomi.</span></span>

![Assegna utente][200] 

<span data-ttu-id="dbff3-257">**Per assegnare Britta Simon a Boomi, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="dbff3-257">**To assign Britta Simon to Boomi, perform the following steps:**</span></span>

1. <span data-ttu-id="dbff3-258">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-258">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="dbff3-260">Nell'elenco delle applicazioni selezionare **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-260">In the applications list, select **Boomi**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. <span data-ttu-id="dbff3-262">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="dbff3-262">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="dbff3-264">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-264">Click **Add** button.</span></span> <span data-ttu-id="dbff3-265">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="dbff3-267">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="dbff3-267">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dbff3-268">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dbff3-269">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="dbff3-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dbff3-270">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="dbff3-270">Testing single sign-on</span></span>

<span data-ttu-id="dbff3-271">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="dbff3-271">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dbff3-272">Quando si fa clic sul riquadro Boomi nel pannello di accesso, si accederà automaticamente all'applicazione Boomi.</span><span class="sxs-lookup"><span data-stu-id="dbff3-272">When you click the Boomi tile in the Access Panel, you should get automatically signed-on to your Boomi application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dbff3-273">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="dbff3-273">Additional resources</span></span>

* [<span data-ttu-id="dbff3-274">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dbff3-274">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dbff3-275">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dbff3-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

