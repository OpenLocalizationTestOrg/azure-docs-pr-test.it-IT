---
title: 'Esercitazione: Integrazione di Azure Active Directory con Clever | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Clever.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 84082ff567e37d7fff80be9e089c67cfab911861
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a><span data-ttu-id="ef4d0-103">Esercitazione: Integrazione di Azure Active Directory con Clever</span><span class="sxs-lookup"><span data-stu-id="ef4d0-103">Tutorial: Azure Active Directory integration with Clever</span></span>

<span data-ttu-id="ef4d0-104">Questa esercitazione descrive come integrare Clever con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ef4d0-104">In this tutorial, you learn how to integrate Clever with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ef4d0-105">L'integrazione di Clever con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ef4d0-105">Integrating Clever with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ef4d0-106">È possibile controllare in Azure AD chi può accedere a Clever.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-106">You can control in Azure AD who has access to Clever.</span></span>
- <span data-ttu-id="ef4d0-107">È possibile abilitare gli utenti per l'accesso automatico a Clever (Single Sign-On) con gli account Azure AD personali.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-107">You can enable your users to automatically get signed-on to Clever (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ef4d0-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="ef4d0-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ef4d0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef4d0-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ef4d0-110">Prerequisites</span></span>

<span data-ttu-id="ef4d0-111">Per configurare l'integrazione di Azure AD con Clever, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ef4d0-111">To configure Azure AD integration with Clever, you need the following items:</span></span>

- <span data-ttu-id="ef4d0-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ef4d0-113">Sottoscrizione di Clever abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ef4d0-113">A Clever single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ef4d0-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ef4d0-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ef4d0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ef4d0-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ef4d0-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ef4d0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ef4d0-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="ef4d0-118">Scenario description</span></span>
<span data-ttu-id="ef4d0-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ef4d0-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ef4d0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ef4d0-121">Aggiunta di Clever dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="ef4d0-121">Adding Clever from the gallery</span></span>
2. <span data-ttu-id="ef4d0-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef4d0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clever-from-the-gallery"></a><span data-ttu-id="ef4d0-123">Aggiunta di Clever dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="ef4d0-123">Adding Clever from the gallery</span></span>
<span data-ttu-id="ef4d0-124">Per configurare l'integrazione di Clever in Azure AD, è necessario aggiungere Clever dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-124">To configure the integration of Clever into Azure AD, you need to add Clever from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ef4d0-125">**Per aggiungere Clever dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ef4d0-125">**To add Clever from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ef4d0-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="ef4d0-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ef4d0-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="ef4d0-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="ef4d0-133">Nella casella di ricerca digitare **Clever**, selezionare **Clever** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-133">In the search box, type **Clever**, select **Clever** from result panel then click **Add** button to add the application.</span></span>

    ![Clever nell'elenco risultati](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ef4d0-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef4d0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ef4d0-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Clever usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ef4d0-136">In this section, you configure and test Azure AD single sign-on with Clever based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ef4d0-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Clever corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Clever is to a user in Azure AD.</span></span> <span data-ttu-id="ef4d0-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Clever.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-138">In other words, a link relationship between an Azure AD user and the related user in Clever needs to be established.</span></span>

<span data-ttu-id="ef4d0-139">Per stabilire la relazione di collegamento, in Clever assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="ef4d0-139">In Clever, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ef4d0-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con Clever, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="ef4d0-140">To configure and test Azure AD single sign-on with Clever, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ef4d0-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ef4d0-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ef4d0-143">**[Creare un utente di test di Clever](#create-a-clever-test-user)**: per avere una controparte di Britta Simon in Clever collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-143">**[Create a Clever test user](#create-a-clever-test-user)** - to have a counterpart of Britta Simon in Clever that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ef4d0-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ef4d0-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ef4d0-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef4d0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ef4d0-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Clever.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clever application.</span></span>

<span data-ttu-id="ef4d0-148">**Per configurare l'accesso Single Sign-On di Azure AD con Clever, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ef4d0-148">**To configure Azure AD single sign-on with Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="ef4d0-149">Nella pagina di integrazione dell'applicazione **Clever** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-149">In the Azure portal, on the **Clever** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento Configura accesso Single Sign-On][4]

2. <span data-ttu-id="ef4d0-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. <span data-ttu-id="ef4d0-153">Nella sezione **URL e dominio Clever** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ef4d0-153">On the **Clever Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Clever](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    <span data-ttu-id="ef4d0-155">a.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-155">a.</span></span> <span data-ttu-id="ef4d0-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://clever.com/in/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://clever.com/in/<companyname>`</span></span>

    <span data-ttu-id="ef4d0-157">b.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-157">b.</span></span> <span data-ttu-id="ef4d0-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://clever.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="ef4d0-158">In the **Identifier** textbox, type a URL using the following pattern: `https://clever.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ef4d0-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="ef4d0-159">These values are not real.</span></span> <span data-ttu-id="ef4d0-160">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ef4d0-161">Per ottenere questi valori, contattare il [team di supporto clienti di Clever](https://clever.com/about/contact/).</span><span class="sxs-lookup"><span data-stu-id="ef4d0-161">Contact [Clever Client support team](https://clever.com/about/contact/) to get these values.</span></span>

4. <span data-ttu-id="ef4d0-162">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. <span data-ttu-id="ef4d0-164">L'applicazione Clever prevede un formato specifico per le asserzioni SAML. È quindi necessario aggiungere mapping di attributi personalizzati alla configurazione di **Attributi token SAML**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-164">The Clever application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>

    <span data-ttu-id="ef4d0-165">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-165">The following screenshot shows an example for this.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. <span data-ttu-id="ef4d0-167">Nella sezione **Attributi utente** della finestra di dialogo **Single Sign-On** configurare l'attributo del token SAML come indicato nell'immagine precedente e seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ef4d0-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="ef4d0-168">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="ef4d0-168">Attribute Name</span></span>  | <span data-ttu-id="ef4d0-169">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="ef4d0-169">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="ef4d0-170">clever.student.credentials.district\_username</span><span class="sxs-lookup"><span data-stu-id="ef4d0-170">clever.student.credentials.district\_username</span></span>  | <span data-ttu-id="ef4d0-171">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="ef4d0-171">user.userprincipalname</span></span> |
    | <span data-ttu-id="ef4d0-172">Firstname</span><span class="sxs-lookup"><span data-stu-id="ef4d0-172">Firstname</span></span>  | <span data-ttu-id="ef4d0-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="ef4d0-173">user.givenname</span></span> |
    | <span data-ttu-id="ef4d0-174">Lastname</span><span class="sxs-lookup"><span data-stu-id="ef4d0-174">Lastname</span></span>  | <span data-ttu-id="ef4d0-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="ef4d0-175">user.surname</span></span> |    

    <span data-ttu-id="ef4d0-176">a.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-176">a.</span></span> <span data-ttu-id="ef4d0-177">Fare clic su **Aggiungi attributo** per aprire la finestra di dialogo **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="ef4d0-180">b.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-180">b.</span></span> <span data-ttu-id="ef4d0-181">Nella casella di testo **Nome** digitare il nome dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="ef4d0-182">c.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-182">c.</span></span> <span data-ttu-id="ef4d0-183">Nell'elenco **Valore** digitare il valore dell'attributo indicato per la riga.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-183">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="ef4d0-184">d.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-184">d.</span></span> <span data-ttu-id="ef4d0-185">Lasciare vuota la casella di testo **Spazio dei nomi**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-185">Leave the **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="ef4d0-186">d.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-186">d.</span></span> <span data-ttu-id="ef4d0-187">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-187">Click **Ok**.</span></span>     

5. <span data-ttu-id="ef4d0-188">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ef4d0-188">Click **Save** button.</span></span>

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ef4d0-190">Per generare l'URL dei **metadati**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ef4d0-190">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="ef4d0-191">a.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-191">a.</span></span> <span data-ttu-id="ef4d0-192">Fare clic su **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-192">Click **App registrations**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    <span data-ttu-id="ef4d0-194">b.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-194">b.</span></span> <span data-ttu-id="ef4d0-195">Fare clic su **Endpoint** per aprire la finestra di dialogo **Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-195">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    <span data-ttu-id="ef4d0-197">c.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-197">c.</span></span> <span data-ttu-id="ef4d0-198">Fare clic sul pulsante Copia per copiare l'URL del **DOCUMENTO METADATI FEDERAZIONE** e incollarlo nel Blocco note.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-198">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    <span data-ttu-id="ef4d0-200">d.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-200">d.</span></span> <span data-ttu-id="ef4d0-201">Passare ora alla pagina delle proprietà di **Clever**, copiare l'**ID applicazione** usando il pulsante **Copia** e incollarlo nel Blocco note.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-201">Now go to the property page of **Clever** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    <span data-ttu-id="ef4d0-203">e.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-203">e.</span></span> <span data-ttu-id="ef4d0-204">Generare l'**URL dei metadati** usando il modello seguente: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="ef4d0-204">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>   

9. <span data-ttu-id="ef4d0-205">In un'altra finestra del Web browser accedere al sito aziendale di Clever come amministratore.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-205">In a different web browser window, log in to your Clever company site as an administrator.</span></span>

10. <span data-ttu-id="ef4d0-206">Nella barra degli strumenti fare clic su **Instant Login**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-206">In the toolbar, click **Instant Login**.</span></span>

    <span data-ttu-id="ef4d0-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span><span class="sxs-lookup"><span data-stu-id="ef4d0-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span></span>

11. <span data-ttu-id="ef4d0-208">Nella pagina **Instant Login** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ef4d0-208">On the **Instant Login** page, perform the following steps:</span></span>
      
      <span data-ttu-id="ef4d0-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span><span class="sxs-lookup"><span data-stu-id="ef4d0-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span></span>
      
      <span data-ttu-id="ef4d0-210">a.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-210">a.</span></span> <span data-ttu-id="ef4d0-211">Digitare un valore in **URL di accesso**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-211">Type the **Login URL**.</span></span>
      
      >[!NOTE]
      ><span data-ttu-id="ef4d0-212">Per **Login URL** usare un valore personalizzato.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-212">The **Login URL** is a custom value.</span></span> <span data-ttu-id="ef4d0-213">Per ottenere questo valore, contattare il [team di supporto clienti di Clever](https://clever.com/about/contact/).</span><span class="sxs-lookup"><span data-stu-id="ef4d0-213">Contact [Clever Client support team](https://clever.com/about/contact/) to get this value.</span></span>
      
      <span data-ttu-id="ef4d0-214">b.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-214">b.</span></span> <span data-ttu-id="ef4d0-215">Per **Identity System** (Sistema di identità) scegliere **ADFS**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-215">As **Identity System**, select **ADFS**.</span></span>

      <span data-ttu-id="ef4d0-216">c.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-216">c.</span></span> <span data-ttu-id="ef4d0-217">Digitare l'**URL dei metadati** nella relativa **casella** di testo.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-217">Type the **Metadata URL** in the **Metadata URL** textbox.</span></span>
      
      <span data-ttu-id="ef4d0-218">d.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-218">d.</span></span> <span data-ttu-id="ef4d0-219">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-219">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ef4d0-220">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-220">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ef4d0-221">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-221">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ef4d0-222">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ef4d0-222">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ef4d0-223">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef4d0-223">Create an Azure AD test user</span></span>

<span data-ttu-id="ef4d0-224">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-224">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="ef4d0-226">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ef4d0-226">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ef4d0-227">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-227">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ef4d0-229">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-229">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ef4d0-231">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-231">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ef4d0-233">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ef4d0-233">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ef4d0-235">a.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-235">a.</span></span> <span data-ttu-id="ef4d0-236">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-236">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ef4d0-237">b.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-237">b.</span></span> <span data-ttu-id="ef4d0-238">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-238">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="ef4d0-239">c.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-239">c.</span></span> <span data-ttu-id="ef4d0-240">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-240">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="ef4d0-241">d.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-241">d.</span></span> <span data-ttu-id="ef4d0-242">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-242">Click **Create**.</span></span>
 
### <a name="create-a-clever-test-user"></a><span data-ttu-id="ef4d0-243">Creare un utente di test di Clever</span><span class="sxs-lookup"><span data-stu-id="ef4d0-243">Create a Clever test user</span></span>

<span data-ttu-id="ef4d0-244">Per consentire agli utenti di Azure AD di accedere a Clever, è necessario effettuarne il provisioning in Clever.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-244">To enable Azure AD users to log in to Clever, they must be provisioned into Clever.</span></span>

<span data-ttu-id="ef4d0-245">Nel caso di Clever, collaborare con il [team di supporto clienti di Clever](https://clever.com/about/contact/) per aggiungere gli utenti nella piattaforma Clever.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-245">In case of Clever, Work with [Clever Client support team](https://clever.com/about/contact/) to add the users in the Clever platform.</span></span> <span data-ttu-id="ef4d0-246">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-246">Users must be created and activated before you use single sign-on.</span></span> 

>[!NOTE]
><span data-ttu-id="ef4d0-247">È possibile usare qualsiasi altro strumento o API di creazione di account utente di Clever per effettuare il provisioning degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-247">You can use any other Clever user account creation tools or APIs provided by Clever to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ef4d0-248">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef4d0-248">Assign the Azure AD test user</span></span>

<span data-ttu-id="ef4d0-249">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Clever.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Clever.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="ef4d0-251">**Per assegnare Britta Simon a Clever, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ef4d0-251">**To assign Britta Simon to Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="ef4d0-252">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="ef4d0-254">Nell'elenco delle applicazioni selezionare **Clever**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-254">In the applications list, select **Clever**.</span></span>

    ![Collegamento di Clever nell'elenco delle applicazioni](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. <span data-ttu-id="ef4d0-256">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-256">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="ef4d0-258">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-258">Click **Add** button.</span></span> <span data-ttu-id="ef4d0-259">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="ef4d0-261">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ef4d0-262">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ef4d0-263">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ef4d0-264">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ef4d0-264">Test single sign-on</span></span>

<span data-ttu-id="ef4d0-265">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-265">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ef4d0-266">Quando si fa clic sul riquadro Clever nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Clever.</span><span class="sxs-lookup"><span data-stu-id="ef4d0-266">When you click the Clever tile in the Access Panel, you should get automatically signed-on to your Clever application.</span></span>
<span data-ttu-id="ef4d0-267">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ef4d0-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ef4d0-268">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ef4d0-268">Additional resources</span></span>

* [<span data-ttu-id="ef4d0-269">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ef4d0-269">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ef4d0-270">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ef4d0-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png

