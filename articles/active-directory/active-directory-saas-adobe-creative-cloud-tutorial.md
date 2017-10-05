---
title: 'Esercitazione: Integrazione di Azure Active Directory con Adobe Creative Cloud | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Adobe Creative Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 3d13608612c77236346b0e98551d7fc427d602e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="4c524-103">Esercitazione: Integrazione di Azure Active Directory con Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="4c524-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="4c524-104">Questa esercitazione descrive come integrare Adobe Creative Cloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4c524-104">In this tutorial, you learn how to integrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4c524-105">L'integrazione di Adobe Creative Cloud con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c524-105">Integrating Adobe Creative Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4c524-106">È possibile controllare in Azure AD chi può accedere ad Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="4c524-106">You can control in Azure AD who has access to Adobe Creative Cloud</span></span>
- <span data-ttu-id="4c524-107">È possibile abilitare gli utenti per l'accesso automatico ad Adobe Creative Cloud (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c524-107">You can enable your users to automatically get signed-on to Adobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4c524-108">È possibile gestire gli account da una posizione centrale: il portale di gestione di Azure</span><span class="sxs-lookup"><span data-stu-id="4c524-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="4c524-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4c524-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c524-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4c524-110">Prerequisites</span></span>

<span data-ttu-id="4c524-111">Per configurare l'integrazione di Azure AD con Adobe Creative Cloud, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c524-111">To configure Azure AD integration with Adobe Creative Cloud, you need the following items:</span></span>

- <span data-ttu-id="4c524-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c524-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4c524-113">Sottoscrizione di Adobe Creative Cloud abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4c524-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4c524-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4c524-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4c524-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c524-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4c524-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4c524-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="4c524-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c524-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4c524-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4c524-118">Scenario description</span></span>
<span data-ttu-id="4c524-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4c524-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4c524-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c524-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4c524-121">Aggiunta di Adobe Creative Cloud dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="4c524-121">Adding Adobe Creative Cloud from the gallery</span></span>
2. <span data-ttu-id="4c524-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c524-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-the-gallery"></a><span data-ttu-id="4c524-123">Aggiungere Adobe Creative Cloud dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="4c524-123">Adding Adobe Creative Cloud from the gallery</span></span>
<span data-ttu-id="4c524-124">Per configurare l'integrazione di Adobe Creative Cloud in Azure AD, è necessario aggiungere Adobe Creative Cloud dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4c524-124">To configure the integration of Adobe Creative Cloud into Azure AD, you need to add Adobe Creative Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4c524-125">**Per aggiungere Adobe Creative Cloud dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4c524-125">**To add Adobe Creative Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4c524-126">Nel **[portale di gestione di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="4c524-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4c524-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4c524-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4c524-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4c524-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="4c524-131">Fare clic sul pulsante **Aggiungi** nella parte superiore della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4c524-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="4c524-133">Nella casella di ricerca digitare **Adobe Creative Cloud**.</span><span class="sxs-lookup"><span data-stu-id="4c524-133">In the search box, type **Adobe Creative Cloud**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="4c524-135">Nel pannello dei risultati selezionare **Adobe Creative Cloud** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4c524-135">In the results panel, select **Adobe Creative Cloud**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4c524-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c524-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4c524-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Adobe Creative Cloud con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4c524-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4c524-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve sapere qual è l'utente di Adobe Creative Cloud che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c524-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Creative Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="4c524-140">In altre parole deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c524-140">In other words, a link relationship between an Azure AD user and the related user in Adobe Creative Cloud needs to be established.</span></span>

<span data-ttu-id="4c524-141">La relazione di collegamento viene stabilita assegnando il valore del **nome utente** di Azure AD come valore di **Username** in Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c524-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="4c524-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Adobe Creative Cloud, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c524-142">To configure and test Azure AD single sign-on with Adobe Creative Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4c524-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4c524-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4c524-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c524-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4c524-145">**[Creazione di un utente di test di Adobe Creative Cloud](#creating-an-adobe-creative-cloud-test-user)**: per avere una controparte di Britta Simon in Adobe Creative Cloud collegata alla relativa rappresentazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c524-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - to have a counterpart of Britta Simon in Adobe Creative Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="4c524-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c524-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4c524-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="4c524-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4c524-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c524-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4c524-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di gestione di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c524-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="4c524-150">**Per configurare l'accesso Single Sign-On di Azure AD con Adobe Creative Cloud, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4c524-150">**To configure Azure AD single sign-on with Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="4c524-151">Nella pagina di integrazione dell'applicazione **Adobe Creative Cloud** del portale di gestione di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="4c524-151">In the Azure Management portal, on the **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="4c524-153">Nella finestra di dialogo **Single Sign-On** in **Modalità** selezionare **Accesso basato su SAML** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="4c524-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="4c524-155">Nella sezione **URL e dominio Adobe Creative Cloud**, se si vuole configurare l'applicazione in modalità avviata da **IDP**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4c524-155">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="4c524-157">a.</span><span class="sxs-lookup"><span data-stu-id="4c524-157">a.</span></span> <span data-ttu-id="4c524-158">Nella casella di testo **Identificatore** digitare il valore `https://www.okta.com/saml2/service-provider/<token>`</span><span class="sxs-lookup"><span data-stu-id="4c524-158">In the **Identifier** textbox, type the value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="4c524-159">b.</span><span class="sxs-lookup"><span data-stu-id="4c524-159">b.</span></span> <span data-ttu-id="4c524-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span><span class="sxs-lookup"><span data-stu-id="4c524-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4c524-161">Si noti che questi non sono i valori reali.</span><span class="sxs-lookup"><span data-stu-id="4c524-161">Please note that these are not the real values.</span></span> <span data-ttu-id="4c524-162">È necessario aggiornare questi valori con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="4c524-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="4c524-163">In questo caso è consigliabile usare in Identificatore il valore univoco della stringa.</span><span class="sxs-lookup"><span data-stu-id="4c524-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="4c524-164">Per creare un utente manualmente, è necessario contattare il team di supporto di Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c524-164">If you need to create an user manually, you need to contact the Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="4c524-165">Nella sezione **URL e dominio Adobe Creative Cloud**, se si vuole configurare l'applicazione in modalità avviata da **SP**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4c524-165">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="4c524-167">a.</span><span class="sxs-lookup"><span data-stu-id="4c524-167">a.</span></span> <span data-ttu-id="4c524-168">Fare clic sull'opzione **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="4c524-168">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="4c524-169">b.</span><span class="sxs-lookup"><span data-stu-id="4c524-169">b.</span></span> <span data-ttu-id="4c524-170">Nella casella di testo **URL di accesso** digitare il valore come: `https://adobe.com`</span><span class="sxs-lookup"><span data-stu-id="4c524-170">In the **Sign-on URL** textbox, type the value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="4c524-171">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="4c524-171">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="4c524-173">Nella sezione **Configurazione di Adobe Creative Cloud** fare clic su **Configura Adobe Creative Cloud** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="4c524-173">On the **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4c524-174">Copiare l'**ID di entità SAML** e l'**URL del servizio SSO SAML** dalla sezione Riferimento rapido.</span><span class="sxs-lookup"><span data-stu-id="4c524-174">Please copy the **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="4c524-176">In un'altra finestra del Web browser accedere al tenant Adobe Creative Cloud come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4c524-176">In a different web browser window, sign-on to your Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="4c524-177">Passare a **Identity** (Identità) nel riquadro di spostamento a sinistra e scegliere il dominio.</span><span class="sxs-lookup"><span data-stu-id="4c524-177">Go to **Identity** on the left navigation pane and click your domain.</span></span> <span data-ttu-id="4c524-178">Eseguire i passaggi descritti di seguito nella sezione di **configurazione dell'accesso Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="4c524-178">Then perform the following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="4c524-179">![Impostazioni](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="4c524-179">![Settings](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="4c524-180">Fare clic su **Browse** (Sfoglia) per caricare il certificato scaricato da Azure AD in **IDP Certificate** (Certificato IDP).</span><span class="sxs-lookup"><span data-stu-id="4c524-180">Click **Browse** to upload the downloaded certificate from Azure AD to **IDP Certificate**.</span></span>

10. <span data-ttu-id="4c524-181">Nella casella di testo **IDP issuer** (Autorità di certificazione IDP) inserire il valore dell'**ID entità SAML** copiato in precedenza dalla sezione **Configura accesso** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c524-181">In the **IDP issuer** textbox, put the value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="4c524-182">Nella casella di testo **IDP Login URL** (URL di accesso IDP) inserire il valore dell'**URL del servizio SSO SAML** copiato in precedenza dalla sezione **Configura accesso** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c524-182">In the **IDP Login URL** textbox, put the value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="4c524-183">Selezionare **HTTP - Redirect** (HTTP - Reindirizzamento) per **IDP Binding** (Binding IDP).</span><span class="sxs-lookup"><span data-stu-id="4c524-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="4c524-184">Selezionare **Email Address** (Indirizzo di posta elettronica) per **User Login Setting** (Impostazione accesso utente).</span><span class="sxs-lookup"><span data-stu-id="4c524-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="4c524-185">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4c524-185">Click **Save** button.</span></span>

15. <span data-ttu-id="4c524-186">Il dashboard visualizza ora il file XML **"Download Metadata"**,</span><span class="sxs-lookup"><span data-stu-id="4c524-186">The dashboard will now present the XML **"Download Metadata"** file.</span></span> <span data-ttu-id="4c524-187">che contiene l'URL EntityDescriptor e l'URL AssertionConsumerService di Adobe.</span><span class="sxs-lookup"><span data-stu-id="4c524-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="4c524-188">Aprire il file e configurare gli URL nell'applicazione Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c524-188">Please open the file and configure them in the Azure AD application.</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="4c524-191">a.</span><span class="sxs-lookup"><span data-stu-id="4c524-191">a.</span></span> <span data-ttu-id="4c524-192">Usare il valore di EntityDescriptor indicato da Adobe per l'**identificatore** nella finestra di dialogo **Configurare le impostazioni dell'app**.</span><span class="sxs-lookup"><span data-stu-id="4c524-192">Use the EntityDescriptor value Adobe provided you for **Identifier** on the **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="4c524-193">b.</span><span class="sxs-lookup"><span data-stu-id="4c524-193">b.</span></span> <span data-ttu-id="4c524-194">Usare il valore di AssertionConsumerService specificato da Adobe per **URL di risposta** nella finestra di dialogo **Configurare le impostazioni dell'app**.</span><span class="sxs-lookup"><span data-stu-id="4c524-194">Use the AssertionConsumerService value Adobe provided you for **Reply URL** on the **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4c524-195">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c524-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="4c524-196">Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c524-196">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="4c524-198">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4c524-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4c524-199">Nel **portale di gestione di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="4c524-199">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4c524-201">Andare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="4c524-201">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4c524-203">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="4c524-203">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4c524-205">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4c524-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4c524-207">a.</span><span class="sxs-lookup"><span data-stu-id="4c524-207">a.</span></span> <span data-ttu-id="4c524-208">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4c524-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4c524-209">b.</span><span class="sxs-lookup"><span data-stu-id="4c524-209">b.</span></span> <span data-ttu-id="4c524-210">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4c524-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4c524-211">c.</span><span class="sxs-lookup"><span data-stu-id="4c524-211">c.</span></span> <span data-ttu-id="4c524-212">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="4c524-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4c524-213">d.</span><span class="sxs-lookup"><span data-stu-id="4c524-213">d.</span></span> <span data-ttu-id="4c524-214">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4c524-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="4c524-215">Creare un utente test di Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="4c524-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="4c524-216">Per consentire agli utenti di Azure AD di accedere ad Adobe Creative Cloud, è necessario eseguirne il provisioning in Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c524-216">In order to enable Azure AD users to log into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="4c524-217">Nel caso di Adobe Creative Cloud il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="4c524-217">In the case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="4c524-218">**Per effettuare il provisioning di un account utente, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4c524-218">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="4c524-219">Accedere al sito aziendale di Adobe Creative Cloud come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4c524-219">Log in to your Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="4c524-220">Fare clic su **Persone**.</span><span class="sxs-lookup"><span data-stu-id="4c524-220">Click **People**.</span></span>

    <span data-ttu-id="4c524-221">![Persone](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "Persone")</span><span class="sxs-lookup"><span data-stu-id="4c524-221">![People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="4c524-222">Fare clic su **Invite User**.</span><span class="sxs-lookup"><span data-stu-id="4c524-222">Click **Invite User**.</span></span>

    <span data-ttu-id="4c524-223">![Invitare utenti](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invitare utenti")</span><span class="sxs-lookup"><span data-stu-id="4c524-223">![Invite Users](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="4c524-224">Nella finestra di dialogo **Invite People** (Invita persone) seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4c524-224">On the **Invite People** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="4c524-225">![Invitare persone](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invitare persone")</span><span class="sxs-lookup"><span data-stu-id="4c524-225">![Invite People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="4c524-226">a.</span><span class="sxs-lookup"><span data-stu-id="4c524-226">a.</span></span> <span data-ttu-id="4c524-227">Nella casella di testo **Email** (Posta elettronica) digitare l'indirizzo di posta elettronica dell'account di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c524-227">In the **Email** textbox, type the email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="4c524-228">b.</span><span class="sxs-lookup"><span data-stu-id="4c524-228">b.</span></span> <span data-ttu-id="4c524-229">Fare clic su **Invita**.</span><span class="sxs-lookup"><span data-stu-id="4c524-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4c524-230">Il titolare dell'account Azure Active Directory riceverà un messaggio di posta elettronica con un collegamento da selezionare per confermare l'account e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="4c524-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4c524-231">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c524-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4c524-232">In questa sezione viene concesso a Britta Simon l'accesso ad Adobe Creative Cloud per consentirle di usare l'accesso Single Sign-On di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c524-232">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Adobe Creative Cloud.</span></span>

![Assegna utente][200] 

<span data-ttu-id="4c524-234">**Per assegnare Britta Simon ad Adobe Creative Cloud, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="4c524-234">**To assign Britta Simon to Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="4c524-235">Nel portale di gestione di Azure aprire la visualizzazione con le applicazioni e quindi passare alla visualizzazione con le directory e andare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4c524-235">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4c524-237">Nell'elenco di applicazioni selezionare **Adobe Creative Cloud**.</span><span class="sxs-lookup"><span data-stu-id="4c524-237">In the applications list, select **Adobe Creative Cloud**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="4c524-239">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="4c524-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="4c524-241">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4c524-241">Click **Add** button.</span></span> <span data-ttu-id="4c524-242">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4c524-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="4c524-244">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="4c524-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4c524-245">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4c524-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4c524-246">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4c524-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4c524-247">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4c524-247">Testing single sign-on</span></span>

<span data-ttu-id="4c524-248">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4c524-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4c524-249">Quando si fa clic sul riquadro Adobe Creative Cloud nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c524-249">When you click the Adobe Creative Cloud tile in the Access Panel, you should get automatically signed-on to your Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="4c524-250">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4c524-250">Additional resources</span></span>

* [<span data-ttu-id="4c524-251">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4c524-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4c524-252">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4c524-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png