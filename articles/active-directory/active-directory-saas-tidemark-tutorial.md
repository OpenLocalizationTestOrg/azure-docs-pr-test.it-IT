---
title: 'Esercitazione: Integrazione di Azure Active Directory con Tidemark | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Tidemark.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5cf80d4e-6e8b-48ec-81c8-27872af5e5d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 170dc58363b12ec671c2fab8c80c7720d3dbf352
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tidemark"></a><span data-ttu-id="d6b70-103">Esercitazione: Integrazione di Azure Active Directory con Tidemark</span><span class="sxs-lookup"><span data-stu-id="d6b70-103">Tutorial: Azure Active Directory integration with Tidemark</span></span>

<span data-ttu-id="d6b70-104">Questa esercitazione descrive come integrare Tidemark con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d6b70-104">In this tutorial, you learn how to integrate Tidemark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d6b70-105">L'integrazione di Tidemark con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6b70-105">Integrating Tidemark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d6b70-106">È possibile controllare in Azure AD chi può accedere a Tidemark.</span><span class="sxs-lookup"><span data-stu-id="d6b70-106">You can control in Azure AD who has access to Tidemark</span></span>
- <span data-ttu-id="d6b70-107">È possibile abilitare gli utenti per l'accesso automatico a Tidemark (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6b70-107">You can enable your users to automatically get signed-on to Tidemark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d6b70-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d6b70-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d6b70-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d6b70-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6b70-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d6b70-110">Prerequisites</span></span>

<span data-ttu-id="d6b70-111">Per configurare l'integrazione di Azure AD con Tidemark, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6b70-111">To configure Azure AD integration with Tidemark, you need the following items:</span></span>

- <span data-ttu-id="d6b70-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6b70-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d6b70-113">Sottoscrizione di Tidemark abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d6b70-113">A Tidemark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d6b70-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d6b70-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d6b70-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6b70-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d6b70-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d6b70-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d6b70-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d6b70-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d6b70-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d6b70-118">Scenario description</span></span>
<span data-ttu-id="d6b70-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d6b70-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d6b70-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6b70-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d6b70-121">Aggiunta di Tidemark dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d6b70-121">Adding Tidemark from the gallery</span></span>
2. <span data-ttu-id="d6b70-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6b70-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tidemark-from-the-gallery"></a><span data-ttu-id="d6b70-123">Aggiunta di Tidemark dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="d6b70-123">Adding Tidemark from the gallery</span></span>
<span data-ttu-id="d6b70-124">Per configurare l'integrazione di Tidemark in Azure AD, è necessario aggiungere Tidemark dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d6b70-124">To configure the integration of Tidemark into Azure AD, you need to add Tidemark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d6b70-125">**Per aggiungere Tidemark dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d6b70-125">**To add Tidemark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d6b70-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d6b70-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d6b70-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d6b70-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d6b70-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d6b70-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d6b70-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="d6b70-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d6b70-133">Nella casella di ricerca digitare **Tidemark**.</span><span class="sxs-lookup"><span data-stu-id="d6b70-133">In the search box, type **Tidemark**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_search.png)

5. <span data-ttu-id="d6b70-135">Nel pannello dei risultati selezionare **Tidemark** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d6b70-135">In the results panel, select **Tidemark**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d6b70-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6b70-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d6b70-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Tidemark in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d6b70-138">In this section, you configure and test Azure AD single sign-on with Tidemark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d6b70-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Tidemark che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6b70-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tidemark is to a user in Azure AD.</span></span> <span data-ttu-id="d6b70-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Tidemark.</span><span class="sxs-lookup"><span data-stu-id="d6b70-140">In other words, a link relationship between an Azure AD user and the related user in Tidemark needs to be established.</span></span>

<span data-ttu-id="d6b70-141">Per stabilire la relazione di collegamento, in Tidemark assegnare il valore di **nome utente** in Azure AD come valore di **Username**.</span><span class="sxs-lookup"><span data-stu-id="d6b70-141">In Tidemark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d6b70-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con Tidemark, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6b70-142">To configure and test Azure AD single sign-on with Tidemark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d6b70-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d6b70-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d6b70-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d6b70-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d6b70-145">**[Creazione di un utente di test Tidemark](#creating-a-tidemark-test-user)**: per avere una controparte di Britta Simon in Tidemark collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6b70-145">**[Creating a Tidemark test user](#creating-a-tidemark-test-user)** - to have a counterpart of Britta Simon in Tidemark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d6b70-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6b70-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d6b70-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="d6b70-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d6b70-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6b70-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d6b70-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione Tidemark.</span><span class="sxs-lookup"><span data-stu-id="d6b70-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tidemark application.</span></span>

<span data-ttu-id="d6b70-150">**Per configurare l'accesso Single Sign-On di Azure AD con Tidemark, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d6b70-150">**To configure Azure AD single sign-on with Tidemark, perform the following steps:**</span></span>

1. <span data-ttu-id="d6b70-151">Nella pagina di integrazione dell'applicazione **Tidemark** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d6b70-151">In the Azure portal, on the **Tidemark** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d6b70-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="d6b70-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_samlbase.png)

3. <span data-ttu-id="d6b70-155">Nella sezione **URL e dominio Tidemark** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d6b70-155">On the **Tidemark Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_url.png)

    <span data-ttu-id="d6b70-157">a.</span><span class="sxs-lookup"><span data-stu-id="d6b70-157">a.</span></span> <span data-ttu-id="d6b70-158">Nella casella di testo **URL di accesso** digitare un URL usando i criteri seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6b70-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    | |
    |--|
    | `https://<subdomain>.tidemark.com/login` |
    | `https://<subdomain>.tidemark.net/login` |

    <span data-ttu-id="d6b70-159">b.</span><span class="sxs-lookup"><span data-stu-id="d6b70-159">b.</span></span> <span data-ttu-id="d6b70-160">Nella casella di testo **Identificatore** digitare un URL usando i criteri seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6b70-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
    | |
    |--|
    | `https://<subdomain>.tidemark.com/saml` |
    | `https://<subdomain>.tidemark.net/saml` |

    > [!NOTE] 
    > <span data-ttu-id="d6b70-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="d6b70-161">These values are not real.</span></span> <span data-ttu-id="d6b70-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="d6b70-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d6b70-163">Per ottenere questi valori, contattare il [team di supporto client di Tidemark](http://www.tidemark.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="d6b70-163">Contact [Tidemark Client support team](http://www.tidemark.com/contact-us) to get these values.</span></span> 
 
4. <span data-ttu-id="d6b70-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="d6b70-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_certificate.png) 

5. <span data-ttu-id="d6b70-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d6b70-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tidemark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d6b70-168">Nella sezione **Configurazione di Tidemark** fare clic su **Configura Tidemark** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="d6b70-168">On the **Tidemark Configuration** section, click **Configure Tidemark** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d6b70-169">Copiare l'**URL di disconnessione, l'ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="d6b70-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_configure.png) 

7. <span data-ttu-id="d6b70-171">Per configurare l'accesso Single Sign-On sul lato **Tidemark**, è necessario inviare il file di **Certificato (Base64) scaricato, l'ID entità SAML, l'URL di disconnessione e l'URL del servizio Single Sign-On SAML** al [team di supporto di Tidemark](http://www.tidemark.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="d6b70-171">To configure single sign-on on **Tidemark** side, you need to send the downloaded **Certificate(Base64), SAML Entity ID, Sign-Out URL and SAML Single Sign-On Service URL** to [Tidemark support team](http://www.tidemark.com/contact-us).</span></span> <span data-ttu-id="d6b70-172">Questa impostazione viene configurata in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="d6b70-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d6b70-173">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="d6b70-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d6b70-174">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="d6b70-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d6b70-175">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d6b70-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d6b70-176">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6b70-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="d6b70-177">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d6b70-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d6b70-179">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d6b70-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d6b70-180">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="d6b70-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tidemark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d6b70-182">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="d6b70-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tidemark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d6b70-184">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="d6b70-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tidemark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d6b70-186">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d6b70-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tidemark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d6b70-188">a.</span><span class="sxs-lookup"><span data-stu-id="d6b70-188">a.</span></span> <span data-ttu-id="d6b70-189">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d6b70-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d6b70-190">b.</span><span class="sxs-lookup"><span data-stu-id="d6b70-190">b.</span></span> <span data-ttu-id="d6b70-191">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d6b70-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d6b70-192">c.</span><span class="sxs-lookup"><span data-stu-id="d6b70-192">c.</span></span> <span data-ttu-id="d6b70-193">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="d6b70-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d6b70-194">d.</span><span class="sxs-lookup"><span data-stu-id="d6b70-194">d.</span></span> <span data-ttu-id="d6b70-195">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d6b70-195">Click **Create**.</span></span>
 
### <a name="creating-a-tidemark-test-user"></a><span data-ttu-id="d6b70-196">Creazione di un utente test Tidemark</span><span class="sxs-lookup"><span data-stu-id="d6b70-196">Creating a Tidemark test user</span></span>

<span data-ttu-id="d6b70-197">Questa sezione descrive come creare un utente chiamato Britta Simon in Tidemark.</span><span class="sxs-lookup"><span data-stu-id="d6b70-197">The objective of this section is to create a user called Britta Simon in Tidemark.</span></span> <span data-ttu-id="d6b70-198">Collaborare con il [team di supporto di Tidemark](http://www.tidemark.com/contact-us) per aggiungere utenti all'account Tidemark.</span><span class="sxs-lookup"><span data-stu-id="d6b70-198">Please work with [Tidemark support team](http://www.tidemark.com/contact-us) to add the users in the Tidemark account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d6b70-199">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6b70-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d6b70-200">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendo l'accesso a Tidemark.</span><span class="sxs-lookup"><span data-stu-id="d6b70-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tidemark.</span></span>

![Assegna utente][200] 

<span data-ttu-id="d6b70-202">**Per assegnare Britta Simon a Tidemark, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="d6b70-202">**To assign Britta Simon to Tidemark, perform the following steps:**</span></span>

1. <span data-ttu-id="d6b70-203">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d6b70-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d6b70-205">Nell'elenco di applicazioni selezionare **Tidemark**.</span><span class="sxs-lookup"><span data-stu-id="d6b70-205">In the applications list, select **Tidemark**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tidemark-tutorial/tutorial_tidemark_app.png) 

3. <span data-ttu-id="d6b70-207">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="d6b70-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d6b70-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d6b70-209">Click **Add** button.</span></span> <span data-ttu-id="d6b70-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d6b70-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d6b70-212">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="d6b70-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d6b70-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d6b70-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d6b70-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d6b70-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d6b70-215">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d6b70-215">Testing single sign-on</span></span>

<span data-ttu-id="d6b70-216">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d6b70-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d6b70-217">Quando si fa clic sul riquadro Tidemark nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Tidemark.</span><span class="sxs-lookup"><span data-stu-id="d6b70-217">When you click the Tidemark tile in the Access Panel, you should get automatically signed-on to your Tidemark application.</span></span>
<span data-ttu-id="d6b70-218">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d6b70-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d6b70-219">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d6b70-219">Additional resources</span></span>

* [<span data-ttu-id="d6b70-220">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6b70-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d6b70-221">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6b70-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tidemark-tutorial/tutorial_general_203.png

