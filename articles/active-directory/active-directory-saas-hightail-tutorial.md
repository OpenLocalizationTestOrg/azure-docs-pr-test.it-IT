---
title: 'Esercitazione: Integrazione di Azure Active Directory con Hightail | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Hightail.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: ba55f9b62d274aa3eb91723c62b53f54de0891b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="774ec-103">Esercitazione: Integrazione di Azure Active Directory con Hightail</span><span class="sxs-lookup"><span data-stu-id="774ec-103">Tutorial: Azure Active Directory integration with Hightail</span></span>

<span data-ttu-id="774ec-104">Questa esercitazione descrive come integrare Hightail con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="774ec-104">In this tutorial, you learn how to integrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="774ec-105">L'integrazione di Hightail con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="774ec-105">Integrating Hightail with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="774ec-106">È possibile controllare in Azure AD chi può accedere a Hightail</span><span class="sxs-lookup"><span data-stu-id="774ec-106">You can control in Azure AD who has access to Hightail</span></span>
- <span data-ttu-id="774ec-107">È possibile abilitare gli utenti per l'accesso automatico a Hightail (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="774ec-107">You can enable your users to automatically get signed-on to Hightail (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="774ec-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="774ec-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="774ec-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="774ec-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="774ec-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="774ec-110">Prerequisites</span></span>

<span data-ttu-id="774ec-111">Per configurare l'integrazione di Azure AD con Hightail, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="774ec-111">To configure Azure AD integration with Hightail, you need the following items:</span></span>

- <span data-ttu-id="774ec-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="774ec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="774ec-113">Sottoscrizione di Hightail abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="774ec-113">A Hightail single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="774ec-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="774ec-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="774ec-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="774ec-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="774ec-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="774ec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="774ec-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="774ec-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="774ec-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="774ec-118">Scenario description</span></span>
<span data-ttu-id="774ec-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="774ec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="774ec-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="774ec-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="774ec-121">Aggiunta di Hightail dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="774ec-121">Adding Hightail from the gallery</span></span>
2. <span data-ttu-id="774ec-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="774ec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hightail-from-the-gallery"></a><span data-ttu-id="774ec-123">Aggiunta di Hightail dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="774ec-123">Adding Hightail from the gallery</span></span>
<span data-ttu-id="774ec-124">Per configurare l'integrazione di Hightail in Azure AD, è necessario aggiungere Hightail dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="774ec-124">To configure the integration of Hightail into Azure AD, you need to add Hightail from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="774ec-125">**Per aggiungere Hightail dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="774ec-125">**To add Hightail from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="774ec-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="774ec-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="774ec-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="774ec-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="774ec-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="774ec-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="774ec-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="774ec-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="774ec-133">Nella casella di ricerca, digitare **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="774ec-133">In the search box, type **Hightail**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. <span data-ttu-id="774ec-135">Nel pannello dei risultati selezionare **Hightail** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="774ec-135">In the results panel, select **Hightail**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="774ec-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="774ec-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="774ec-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Hightail mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="774ec-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="774ec-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere quale utente di Hightail corrisponde a un determinato utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="774ec-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Hightail is to a user in Azure AD.</span></span> <span data-ttu-id="774ec-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Hightail.</span><span class="sxs-lookup"><span data-stu-id="774ec-140">In other words, a link relationship between an Azure AD user and the related user in Hightail needs to be established.</span></span>

<span data-ttu-id="774ec-141">Per stabilire la relazione di collegamento, in Hightail assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="774ec-141">In Hightail, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="774ec-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Hightail, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="774ec-142">To configure and test Azure AD single sign-on with Hightail, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="774ec-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="774ec-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="774ec-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="774ec-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="774ec-145">**[Creazione di un utente test di Hightail](#creating-a-hightail-test-user)**: per avere una controparte di Britta Simon in Hightail collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="774ec-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - to have a counterpart of Britta Simon in Hightail that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="774ec-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="774ec-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="774ec-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="774ec-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="774ec-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="774ec-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="774ec-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Hightail.</span><span class="sxs-lookup"><span data-stu-id="774ec-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="774ec-150">**Per configurare l'accesso Single Sign-On di Azure AD con Hightail, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="774ec-150">**To configure Azure AD single sign-on with Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="774ec-151">Nella pagina di integrazione dell'applicazione **Hightail** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="774ec-151">In the Azure portal, on the **Hightail** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="774ec-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="774ec-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. <span data-ttu-id="774ec-155">Nella sezione **URL e dominio Hightail** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="774ec-155">On the **Hightail Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     <span data-ttu-id="774ec-157">Nella casella di testo **URL di risposta** digitare un URL come indicato di seguito: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span><span class="sxs-lookup"><span data-stu-id="774ec-157">In the **Reply URL** textbox, type the URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="774ec-158">Il valore precedente non è un valore reale.</span><span class="sxs-lookup"><span data-stu-id="774ec-158">The preceding value is not real value.</span></span> <span data-ttu-id="774ec-159">È necessario aggiornarlo con l'URL di risposta reale, descritto più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="774ec-159">You will update the value with the actual Reply URL, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="774ec-160">Nella sezione **URL e dominio Hightail** seguire questa procedura per configurare l'applicazione in **modalità avviata da SP**:</span><span class="sxs-lookup"><span data-stu-id="774ec-160">On the **Hightail Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    <span data-ttu-id="774ec-162">a.</span><span class="sxs-lookup"><span data-stu-id="774ec-162">a.</span></span> <span data-ttu-id="774ec-163">Fare clic su **Mostra impostazioni URL avanzate**.</span><span class="sxs-lookup"><span data-stu-id="774ec-163">Click the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="774ec-164">b.</span><span class="sxs-lookup"><span data-stu-id="774ec-164">b.</span></span> <span data-ttu-id="774ec-165">Nella casella di testo **URL di accesso** digitare un URL come indicato di seguito: `https://www.hightail.com/loginSSO`</span><span class="sxs-lookup"><span data-stu-id="774ec-165">In the **Sign On URL** textbox, type the URL as: `https://www.hightail.com/loginSSO`</span></span>

4. <span data-ttu-id="774ec-166">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="774ec-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. <span data-ttu-id="774ec-168">L'applicazione Hightail si aspetta che le asserzioni SAML abbiano un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="774ec-168">Hightail application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="774ec-169">Configurare le attestazioni seguenti per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="774ec-169">Please configure the following claims for this application.</span></span> <span data-ttu-id="774ec-170">È possibile gestire i valori di questi attributi dalla scheda **Attribute (Attributo)** dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="774ec-170">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="774ec-171">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="774ec-171">The following screenshot shows an example for this.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. <span data-ttu-id="774ec-173">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On** configurare l'attributo del token SAML come illustrato nell'immagine e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="774ec-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="774ec-174">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="774ec-174">Attribute Name</span></span> | <span data-ttu-id="774ec-175">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="774ec-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="774ec-176">FirstName</span><span class="sxs-lookup"><span data-stu-id="774ec-176">FirstName</span></span> | <span data-ttu-id="774ec-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="774ec-177">user.givenname</span></span> |
    | <span data-ttu-id="774ec-178">LastName</span><span class="sxs-lookup"><span data-stu-id="774ec-178">LastName</span></span> | <span data-ttu-id="774ec-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="774ec-179">user.surname</span></span> |
    | <span data-ttu-id="774ec-180">Email</span><span class="sxs-lookup"><span data-stu-id="774ec-180">Email</span></span> | <span data-ttu-id="774ec-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="774ec-181">user.mail</span></span> |    
    | <span data-ttu-id="774ec-182">UserIdentity</span><span class="sxs-lookup"><span data-stu-id="774ec-182">UserIdentity</span></span> | <span data-ttu-id="774ec-183">user.mail</span><span class="sxs-lookup"><span data-stu-id="774ec-183">user.mail</span></span> |
    
    <span data-ttu-id="774ec-184">a.</span><span class="sxs-lookup"><span data-stu-id="774ec-184">a.</span></span> <span data-ttu-id="774ec-185">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="774ec-185">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="774ec-188">b.</span><span class="sxs-lookup"><span data-stu-id="774ec-188">b.</span></span> <span data-ttu-id="774ec-189">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="774ec-189">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="774ec-190">c.</span><span class="sxs-lookup"><span data-stu-id="774ec-190">c.</span></span> <span data-ttu-id="774ec-191">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="774ec-191">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="774ec-192">d.</span><span class="sxs-lookup"><span data-stu-id="774ec-192">d.</span></span> <span data-ttu-id="774ec-193">Lasciare vuota la casella **Spazio dei nomi**.</span><span class="sxs-lookup"><span data-stu-id="774ec-193">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="774ec-194">e.</span><span class="sxs-lookup"><span data-stu-id="774ec-194">e.</span></span> <span data-ttu-id="774ec-195">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="774ec-195">Click **Ok**.</span></span>

7. <span data-ttu-id="774ec-196">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="774ec-196">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="774ec-198">Nella sezione **Configurazione di Hightail** fare clic su **Configura Hightail** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="774ec-198">On the **Hightail Configuration** section, click **Configure Hightail** to open **Configure sign-on** window.</span></span> <span data-ttu-id="774ec-199">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="774ec-199">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    ><span data-ttu-id="774ec-201">Prima di configurare l'accesso Single Sign-On sull'app Hightail inserire il dominio di posta elettronica nell'elenco dei domini consentiti con il team Hightail, in modo che tutti gli utenti del dominio possano beneficiare della funzionalità Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="774ec-201">Before configuring the Single Sign On at Hightail app, please white list your email domain with Hightail team so that all the users who are using this domain can use Single Sign On functionality.</span></span>


9. <span data-ttu-id="774ec-202">Per configurare l'accesso SSO sull'applicazione, è necessario accedere al tenant di Hightail come amministratore.</span><span class="sxs-lookup"><span data-stu-id="774ec-202">To get SSO configured for your application, you need to sign-on to your Hightail tenant as an administrator.</span></span>
   
    <span data-ttu-id="774ec-203">a.</span><span class="sxs-lookup"><span data-stu-id="774ec-203">a.</span></span> <span data-ttu-id="774ec-204">Nel menu in alto fare clic sulla scheda **Account** e selezionare **Configure SAML** (Configura SAML).</span><span class="sxs-lookup"><span data-stu-id="774ec-204">In the menu on the top, click the **Account** tab and select **Configure SAML**.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    <span data-ttu-id="774ec-206">b.</span><span class="sxs-lookup"><span data-stu-id="774ec-206">b.</span></span> <span data-ttu-id="774ec-207">Selezionare la casella di controllo **Enable SAML Authentication (Abilita autenticazione SAML)**.</span><span class="sxs-lookup"><span data-stu-id="774ec-207">Select the checkbox of **Enable SAML Authentication**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    <span data-ttu-id="774ec-209">c.</span><span class="sxs-lookup"><span data-stu-id="774ec-209">c.</span></span> <span data-ttu-id="774ec-210">Aprire nel Blocco note il certificato con codifica Base 64 scaricato dal portale di Azure, copiarne il contenuto negli Appunti e incollarlo nella casella di testo **SAML Token Signing Certificate** (Certificato per la firma di token SAML).</span><span class="sxs-lookup"><span data-stu-id="774ec-210">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Token Signing Certificate** textbox.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    <span data-ttu-id="774ec-212">d.</span><span class="sxs-lookup"><span data-stu-id="774ec-212">d.</span></span> <span data-ttu-id="774ec-213">Nella casella di testo **SAML Authority (Identity Provider)** (Autorità SAML - Provider di identità) incollare il valore di **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="774ec-213">In the **SAML Authority (Identity Provider)** textbox, paste the value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    <span data-ttu-id="774ec-215">e.</span><span class="sxs-lookup"><span data-stu-id="774ec-215">e.</span></span> <span data-ttu-id="774ec-216">Se si desidera configurare l'applicazione in **modalità avviata da IDP**, selezionare **"Identity Provider (IdP) initiated log in"** ("Accesso avviato con provider di identità (IdP)").</span><span class="sxs-lookup"><span data-stu-id="774ec-216">If you wish to configure the application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span></span> <span data-ttu-id="774ec-217">Se si usa la **modalità avviata da SP**, selezionare **"Service Provider (SP) initiated log in"** ("Accesso avviato con provider di servizi (SP)").</span><span class="sxs-lookup"><span data-stu-id="774ec-217">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    <span data-ttu-id="774ec-219">f.</span><span class="sxs-lookup"><span data-stu-id="774ec-219">f.</span></span> <span data-ttu-id="774ec-220">Copiare l'URL consumer di SAML dell'istanza in uso e incollarlo nella casella di testo **Reply URL** (URL di risposta) della sezione **URL e dominio Hightail** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="774ec-220">Copy the SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="774ec-221">g.</span><span class="sxs-lookup"><span data-stu-id="774ec-221">g.</span></span> <span data-ttu-id="774ec-222">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="774ec-222">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="774ec-223">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="774ec-223">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="774ec-224">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="774ec-224">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="774ec-225">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="774ec-225">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="774ec-226">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="774ec-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="774ec-227">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="774ec-227">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="774ec-229">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="774ec-229">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="774ec-230">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="774ec-230">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="774ec-232">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="774ec-232">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="774ec-234">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="774ec-234">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="774ec-236">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="774ec-236">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="774ec-238">a.</span><span class="sxs-lookup"><span data-stu-id="774ec-238">a.</span></span> <span data-ttu-id="774ec-239">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="774ec-239">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="774ec-240">b.</span><span class="sxs-lookup"><span data-stu-id="774ec-240">b.</span></span> <span data-ttu-id="774ec-241">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="774ec-241">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="774ec-242">c.</span><span class="sxs-lookup"><span data-stu-id="774ec-242">c.</span></span> <span data-ttu-id="774ec-243">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="774ec-243">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="774ec-244">d.</span><span class="sxs-lookup"><span data-stu-id="774ec-244">d.</span></span> <span data-ttu-id="774ec-245">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="774ec-245">Click **Create**.</span></span>
 
### <a name="creating-a-hightail-test-user"></a><span data-ttu-id="774ec-246">Creazione di un utente test di Hightail</span><span class="sxs-lookup"><span data-stu-id="774ec-246">Creating a Hightail test user</span></span>

<span data-ttu-id="774ec-247">Questa sezione descrive come creare un utente chiamato Britta Simon in Hightail.</span><span class="sxs-lookup"><span data-stu-id="774ec-247">The objective of this section is to create a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="774ec-248">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="774ec-248">There is no action item for you in this section.</span></span> <span data-ttu-id="774ec-249">Hightail supporta il provisioning utente just-in-time basato su attestazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="774ec-249">Hightail supports just-in-time user provisioning based on the custom claims.</span></span> <span data-ttu-id="774ec-250">Se sono state configurate le attestazioni personalizzate come illustrato nella sezione **[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** in alto, viene automaticamente creato un utente nell'applicazione se ancora non esiste.</span><span class="sxs-lookup"><span data-stu-id="774ec-250">If you have configured the custom claims as shown in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in the application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="774ec-251">Per creare un utente manualmente è necessario contattare il [team di supporto di Hightail](mailto:support@hightail.com).</span><span class="sxs-lookup"><span data-stu-id="774ec-251">If you need to create a user manually, you need to contact the [Hightail support team](mailto:support@hightail.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="774ec-252">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="774ec-252">Assigning the Azure AD test user</span></span>

<span data-ttu-id="774ec-253">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Hightail.</span><span class="sxs-lookup"><span data-stu-id="774ec-253">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Hightail.</span></span>

![Assegna utente][200] 

<span data-ttu-id="774ec-255">**Per assegnare Britta Simon a Hightail, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="774ec-255">**To assign Britta Simon to Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="774ec-256">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="774ec-256">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="774ec-258">Nell'elenco delle applicazioni, selezionare **Hightail**.</span><span class="sxs-lookup"><span data-stu-id="774ec-258">In the applications list, select **Hightail**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. <span data-ttu-id="774ec-260">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="774ec-260">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="774ec-262">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="774ec-262">Click **Add** button.</span></span> <span data-ttu-id="774ec-263">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="774ec-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="774ec-265">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="774ec-265">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="774ec-266">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="774ec-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="774ec-267">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="774ec-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="774ec-268">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="774ec-268">Testing single sign-on</span></span>

<span data-ttu-id="774ec-269">Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="774ec-269">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="774ec-270">Quando si fa clic sul riquadro Hightail nel pannello di accesso, viene effettuato automaticamente l'accesso all'applicazione Hightail.</span><span class="sxs-lookup"><span data-stu-id="774ec-270">When you click the Hightail tile in the Access Panel, you should get automatically signed-on to your Hightail application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="774ec-271">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="774ec-271">Additional resources</span></span>

* [<span data-ttu-id="774ec-272">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="774ec-272">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="774ec-273">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="774ec-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

