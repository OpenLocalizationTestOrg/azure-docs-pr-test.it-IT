---
title: 'Esercitazione: Integrazione di Azure Active Directory con Klue | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Klue.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 08341008-980b-4111-adb2-97bbabbf1e47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: c64417c136340b3ffa5d67c618c6fe037d2992b5
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-klue"></a><span data-ttu-id="9e7c9-103">Esercitazione: Integrazione di Azure Active Directory con Klue</span><span class="sxs-lookup"><span data-stu-id="9e7c9-103">Tutorial: Azure Active Directory integration with Klue</span></span>

<span data-ttu-id="9e7c9-104">Questa esercitazione descrive come integrare Klue con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9e7c9-104">In this tutorial, you learn how to integrate Klue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9e7c9-105">L'integrazione di Klue con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9e7c9-105">Integrating Klue with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9e7c9-106">È possibile controllare in Azure AD chi può accedere a Klue</span><span class="sxs-lookup"><span data-stu-id="9e7c9-106">You can control in Azure AD who has access to Klue</span></span>
- <span data-ttu-id="9e7c9-107">È possibile abilitare gli utenti per l'accesso automatico a Klue (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e7c9-107">You can enable your users to automatically get signed-on to Klue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9e7c9-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9e7c9-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9e7c9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e7c9-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9e7c9-110">Prerequisites</span></span>

<span data-ttu-id="9e7c9-111">Per configurare l'integrazione di Azure AD con Klue, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9e7c9-111">To configure Azure AD integration with Klue, you need the following items:</span></span>

- <span data-ttu-id="9e7c9-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9e7c9-113">Sottoscrizione di Klue abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9e7c9-113">A Klue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9e7c9-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9e7c9-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9e7c9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9e7c9-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9e7c9-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9e7c9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9e7c9-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="9e7c9-118">Scenario description</span></span>
<span data-ttu-id="9e7c9-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9e7c9-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9e7c9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9e7c9-121">Aggiunta di Klue dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="9e7c9-121">Adding Klue from the gallery</span></span>
2. <span data-ttu-id="9e7c9-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e7c9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-klue-from-the-gallery"></a><span data-ttu-id="9e7c9-123">Aggiunta di Klue dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="9e7c9-123">Adding Klue from the gallery</span></span>
<span data-ttu-id="9e7c9-124">Per configurare l'integrazione di Klue in Azure AD, è necessario aggiungere Klue dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-124">To configure the integration of Klue into Azure AD, you need to add Klue from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9e7c9-125">**Per aggiungere Klue dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="9e7c9-125">**To add Klue from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9e7c9-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9e7c9-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9e7c9-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="9e7c9-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="9e7c9-133">Nella casella di ricerca digitare **Klue**.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-133">In the search box, type **Klue**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-klue-tutorial/tutorial_klue_search.png)

5. <span data-ttu-id="9e7c9-135">Nel pannello dei risultati selezionare **Klue** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-135">In the results panel, select **Klue**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-klue-tutorial/tutorial_klue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9e7c9-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e7c9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9e7c9-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Klue in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9e7c9-138">In this section, you configure and test Azure AD single sign-on with Klue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9e7c9-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Klue che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Klue is to a user in Azure AD.</span></span> <span data-ttu-id="9e7c9-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Klue.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-140">In other words, a link relationship between an Azure AD user and the related user in Klue needs to be established.</span></span>

<span data-ttu-id="9e7c9-141">Per stabilire la relazione di collegamento, in Klue assegnare il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="9e7c9-141">In Klue, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9e7c9-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Klue, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="9e7c9-142">To configure and test Azure AD single sign-on with Klue, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9e7c9-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9e7c9-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9e7c9-145">**[Creazione di un utente di test di Klue](#creating-a-klue-test-user)**: per avere una controparte di Britta Simon in Klue collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-145">**[Creating a Klue test user](#creating-a-klue-test-user)** - to have a counterpart of Britta Simon in Klue that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9e7c9-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9e7c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9e7c9-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e7c9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9e7c9-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Klue.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Klue application.</span></span>

<span data-ttu-id="9e7c9-150">**Per configurare l'accesso Single Sign-On di Azure AD con Klue, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="9e7c9-150">**To configure Azure AD single sign-on with Klue, perform the following steps:**</span></span>

1. <span data-ttu-id="9e7c9-151">Nella pagina di integrazione dell'applicazione **Klue** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-151">In the Azure portal, on the **Klue** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="9e7c9-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-klue-tutorial/tutorial_klue_samlbase.png)

3. <span data-ttu-id="9e7c9-155">Nella sezione **URL e dominio Klue** se si vuole configurare l'applicazione in modalità avviata da **IDP**:</span><span class="sxs-lookup"><span data-stu-id="9e7c9-155">On the **Klue Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-klue-tutorial/tutorial_klue_url1.png)

    <span data-ttu-id="9e7c9-157">a.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-157">a.</span></span> <span data-ttu-id="9e7c9-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `urn:klue:<Customer ID>`</span><span class="sxs-lookup"><span data-stu-id="9e7c9-158">In the **Identifier** textbox, type a URL using the following pattern: `urn:klue:<Customer ID>`</span></span>

    <span data-ttu-id="9e7c9-159">b.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-159">b.</span></span> <span data-ttu-id="9e7c9-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span><span class="sxs-lookup"><span data-stu-id="9e7c9-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span></span>

4. <span data-ttu-id="9e7c9-161">Selezionare **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="9e7c9-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="9e7c9-162">se si desidera configurare l'applicazione in modalità avviata da **SP**:</span><span class="sxs-lookup"><span data-stu-id="9e7c9-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-klue-tutorial/tutorial_klue_url2.png)

    <span data-ttu-id="9e7c9-164">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://app.klue.com/account/auth/saml/<Customer UUID>/`</span><span class="sxs-lookup"><span data-stu-id="9e7c9-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="9e7c9-165">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="9e7c9-165">These values are not real.</span></span> <span data-ttu-id="9e7c9-166">aggiornarli con l'URL di risposta, l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-166">Update these values with the actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="9e7c9-167">Per ottenere questi valori, contattare il [team di supporto clienti di Klue](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="9e7c9-167">Contact [Klue Client support team](mailto:support@klue.com) to get these values.</span></span>

5. <span data-ttu-id="9e7c9-168">L'applicazione Klue prevede un formato specifico per le asserzioni SAML. È quindi necessario aggiungere mapping di attributi personalizzati alla configurazione degli attributi del token SAML.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-168">The Klue application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="9e7c9-169">È possibile gestire i valori di questi attributi dalla sezione "**Attributi utente**" nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-169">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-klue-tutorial/attribute.png)

6. <span data-ttu-id="9e7c9-171">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On** configurare l'attributo del token SAML come indicato nell'immagine precedente ed eseguire i passaggi descritti di seguito:</span><span class="sxs-lookup"><span data-stu-id="9e7c9-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
    
    | <span data-ttu-id="9e7c9-172">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="9e7c9-172">Attribute Name</span></span>      | <span data-ttu-id="9e7c9-173">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="9e7c9-173">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="9e7c9-174">first_name</span><span class="sxs-lookup"><span data-stu-id="9e7c9-174">first_name</span></span>          | <span data-ttu-id="9e7c9-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="9e7c9-175">user.givenname</span></span> |
    | <span data-ttu-id="9e7c9-176">last_name</span><span class="sxs-lookup"><span data-stu-id="9e7c9-176">last_name</span></span>           | <span data-ttu-id="9e7c9-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="9e7c9-177">user.surname</span></span> |
    | <span data-ttu-id="9e7c9-178">email</span><span class="sxs-lookup"><span data-stu-id="9e7c9-178">email</span></span>               | <span data-ttu-id="9e7c9-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="9e7c9-179">user.userprincipalname</span></span>|
    
    <span data-ttu-id="9e7c9-180">a.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-180">a.</span></span> <span data-ttu-id="9e7c9-181">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-klue-tutorial/tutorial_attribute_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-klue-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="9e7c9-184">b.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-184">b.</span></span> <span data-ttu-id="9e7c9-185">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="9e7c9-186">c.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-186">c.</span></span> <span data-ttu-id="9e7c9-187">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="9e7c9-188">d.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-188">d.</span></span> <span data-ttu-id="9e7c9-189">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-189">Click **Ok**.</span></span>

7. <span data-ttu-id="9e7c9-190">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-190">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-klue-tutorial/tutorial_klue_certificate.png) 

8. <span data-ttu-id="9e7c9-192">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="9e7c9-192">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-klue-tutorial/tutorial_general_400.png)
    
9. <span data-ttu-id="9e7c9-194">Nella sezione **Configurazione di Klue** fare clic su **Configura Klue** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-194">On the **Klue Configuration** section, click **Configure Klue** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9e7c9-195">Copiare l'**ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="9e7c9-195">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-klue-tutorial/tutorial_klue_configure.png) 

10. <span data-ttu-id="9e7c9-197">Per configurare l'accesso Single Sign-On sul lato **Klue**, è necessario inviare il **certificato (Base64) scaricato, l'URL del servizio Single Sign-On SAML e l'ID di entità SAML** al [team di supporto di Klue](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="9e7c9-197">To configure single sign-on on **Klue** side, you need to send the downloaded **Certificate(Base64), SAML Single Sign-On Service URL, and SAML Entity ID** to [Klue support team](mailto:support@klue.com).</span></span>

> [!TIP]
> <span data-ttu-id="9e7c9-198">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9e7c9-199">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9e7c9-200">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9e7c9-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9e7c9-201">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e7c9-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="9e7c9-202">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="9e7c9-204">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9e7c9-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9e7c9-205">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9e7c9-207">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9e7c9-209">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9e7c9-211">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9e7c9-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9e7c9-213">a.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-213">a.</span></span> <span data-ttu-id="9e7c9-214">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9e7c9-215">b.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-215">b.</span></span> <span data-ttu-id="9e7c9-216">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9e7c9-217">c.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-217">c.</span></span> <span data-ttu-id="9e7c9-218">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9e7c9-219">d.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-219">d.</span></span> <span data-ttu-id="9e7c9-220">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-220">Click **Create**.</span></span>
 
### <a name="creating-a-klue-test-user"></a><span data-ttu-id="9e7c9-221">Creazione di un utente di test di Klue</span><span class="sxs-lookup"><span data-stu-id="9e7c9-221">Creating a Klue test user</span></span>

<span data-ttu-id="9e7c9-222">L'obiettivo di questa sezione consiste nel creare un utente chiamato Britta Simon in Klue.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-222">The objective of this section is to create a user called Britta Simon in Klue.</span></span> <span data-ttu-id="9e7c9-223">Klue supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-223">Klue supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="9e7c9-224">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-224">There is no action item for you in this section.</span></span> <span data-ttu-id="9e7c9-225">Durante un tentativo di accesso a Klue viene creato un nuovo utente, se questo non esiste già.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-225">A new user is created during an attempt to access Klue if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="9e7c9-226">Se è necessario creare un utente manualmente, contattare il [team di supporto di Klue](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="9e7c9-226">If you need to create a user manually, Contact [Klue support team](mailto:support@klue.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9e7c9-227">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e7c9-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9e7c9-228">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Klue.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Klue.</span></span>

![Assegna utente][200] 

<span data-ttu-id="9e7c9-230">**Per assegnare Britta Simon a Klue, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="9e7c9-230">**To assign Britta Simon to Klue, perform the following steps:**</span></span>

1. <span data-ttu-id="9e7c9-231">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="9e7c9-233">Nell'elenco delle applicazioni selezionare **Klue**.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-233">In the applications list, select **Klue**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-klue-tutorial/tutorial_klue_app.png) 

3. <span data-ttu-id="9e7c9-235">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="9e7c9-237">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-237">Click **Add** button.</span></span> <span data-ttu-id="9e7c9-238">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="9e7c9-240">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9e7c9-241">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9e7c9-242">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9e7c9-243">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9e7c9-243">Testing single sign-on</span></span>

<span data-ttu-id="9e7c9-244">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9e7c9-245">Quando si fa clic sul riquadro Klue nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Klue.</span><span class="sxs-lookup"><span data-stu-id="9e7c9-245">When you click the Klue tile in the Access Panel, you should get automatically signed-on to your Klue application.</span></span>
<span data-ttu-id="9e7c9-246">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9e7c9-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9e7c9-247">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="9e7c9-247">Additional resources</span></span>

* [<span data-ttu-id="9e7c9-248">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e7c9-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9e7c9-249">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e7c9-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-klue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-klue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-klue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-klue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-klue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-klue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-klue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-klue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-klue-tutorial/tutorial_general_203.png

