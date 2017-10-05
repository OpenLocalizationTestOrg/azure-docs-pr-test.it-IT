---
title: 'Esercitazione: Integrazione di Azure Active Directory con BeeLine | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e BeeLine.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0726859d-1dac-44a0-810b-da56d89039ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 93acbd90bbe5f0a40bf3f56edb766a0fdd30f68f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-beeline"></a><span data-ttu-id="94cbe-103">Esercitazione: Integrazione di Azure Active Directory con BeeLine</span><span class="sxs-lookup"><span data-stu-id="94cbe-103">Tutorial: Azure Active Directory integration with BeeLine</span></span>

<span data-ttu-id="94cbe-104">Questa esercitazione descrive come integrare BeeLine con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="94cbe-104">In this tutorial, you learn how to integrate BeeLine with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="94cbe-105">L'integrazione di BeeLine con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="94cbe-105">Integrating BeeLine with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="94cbe-106">È possibile controllare in Azure AD chi può accedere a BeeLine</span><span class="sxs-lookup"><span data-stu-id="94cbe-106">You can control in Azure AD who has access to BeeLine</span></span>
- <span data-ttu-id="94cbe-107">È possibile abilitare gli utenti per l'accesso automatico a BeeLine (Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="94cbe-107">You can enable your users to automatically get signed-on to BeeLine (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="94cbe-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="94cbe-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="94cbe-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="94cbe-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94cbe-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="94cbe-110">Prerequisites</span></span>

<span data-ttu-id="94cbe-111">Per configurare l'integrazione di Azure AD con BeeLine, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="94cbe-111">To configure Azure AD integration with BeeLine, you need the following items:</span></span>

- <span data-ttu-id="94cbe-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94cbe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="94cbe-113">Sottoscrizione di BeeLine abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="94cbe-113">A BeeLine single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="94cbe-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="94cbe-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="94cbe-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="94cbe-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="94cbe-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="94cbe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="94cbe-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="94cbe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="94cbe-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="94cbe-118">Scenario description</span></span>
<span data-ttu-id="94cbe-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="94cbe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="94cbe-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="94cbe-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="94cbe-121">Aggiunta di BeeLine dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="94cbe-121">Adding BeeLine from the gallery</span></span>
2. <span data-ttu-id="94cbe-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="94cbe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-beeline-from-the-gallery"></a><span data-ttu-id="94cbe-123">Aggiunta di BeeLine dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="94cbe-123">Adding BeeLine from the gallery</span></span>
<span data-ttu-id="94cbe-124">Per configurare l'integrazione di BeeLine in Azure AD, è necessario aggiungere BeeLine dalla raccolta all'elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="94cbe-124">To configure the integration of BeeLine into Azure AD, you need to add BeeLine from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="94cbe-125">**Per aggiungere BeeLine dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="94cbe-125">**To add BeeLine from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="94cbe-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="94cbe-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="94cbe-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="94cbe-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="94cbe-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="94cbe-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="94cbe-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="94cbe-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="94cbe-133">Nella casella di ricerca digitare **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="94cbe-133">In the search box, type **BeeLine**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_search.png)

5. <span data-ttu-id="94cbe-135">Nel pannello dei risultati selezionare **BeeLine** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94cbe-135">In the results panel, select **BeeLine**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="94cbe-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="94cbe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="94cbe-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con BeeLine usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="94cbe-138">In this section, you configure and test Azure AD single sign-on with BeeLine based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="94cbe-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di BeeLine corrispondente a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94cbe-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BeeLine is to a user in Azure AD.</span></span> <span data-ttu-id="94cbe-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in BeeLine.</span><span class="sxs-lookup"><span data-stu-id="94cbe-140">In other words, a link relationship between an Azure AD user and the related user in BeeLine needs to be established.</span></span>

<span data-ttu-id="94cbe-141">Per stabilire la relazione di collegamento, in BeeLine assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="94cbe-141">In BeeLine, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="94cbe-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con BeeLine, è necessario completare le procedure di base seguenti:</span><span class="sxs-lookup"><span data-stu-id="94cbe-142">To configure and test Azure AD single sign-on with BeeLine, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="94cbe-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'utilizzo di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="94cbe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="94cbe-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="94cbe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="94cbe-145">**[Creazione di un utente di test di BeeLine](#creating-a-beeline-test-user)**: per avere una controparte di Britta Simon in BeeLine collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94cbe-145">**[Creating a BeeLine test user](#creating-a-beeline-test-user)** - to have a counterpart of Britta Simon in BeeLine that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="94cbe-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94cbe-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="94cbe-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="94cbe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="94cbe-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="94cbe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="94cbe-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione BeeLine.</span><span class="sxs-lookup"><span data-stu-id="94cbe-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BeeLine application.</span></span>

<span data-ttu-id="94cbe-150">**Per configurare l'accesso Single Sign-On di Azure AD con BeeLine, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="94cbe-150">**To configure Azure AD single sign-on with BeeLine, perform the following steps:**</span></span>

1. <span data-ttu-id="94cbe-151">Nella pagina di integrazione dell'applicazione **BeeLine** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="94cbe-151">In the Azure portal, on the **BeeLine** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="94cbe-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="94cbe-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_samlbase.png)

3. <span data-ttu-id="94cbe-155">Nella sezione **URL e dominio BeeLine** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="94cbe-155">On the **BeeLine Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_url.png)

    <span data-ttu-id="94cbe-157">a.</span><span class="sxs-lookup"><span data-stu-id="94cbe-157">a.</span></span> <span data-ttu-id="94cbe-158">Nella casella di testo **Identificatore** digitare l'URL adottando il modello seguente: `https://projects.beeline.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="94cbe-158">In the **Identifier** textbox, type a URL using the following pattern: `https://projects.beeline.net/<instancename>`</span></span>

    <span data-ttu-id="94cbe-159">b.</span><span class="sxs-lookup"><span data-stu-id="94cbe-159">b.</span></span> <span data-ttu-id="94cbe-160">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente:</span><span class="sxs-lookup"><span data-stu-id="94cbe-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://projects.beeline.net/<instancename>/SSO_External.ashx`|
    | `https://projects.beeline.net/<companyname>/SSO_External.ashx` |

    > [!NOTE] 
    > <span data-ttu-id="94cbe-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="94cbe-161">These values are not real.</span></span> <span data-ttu-id="94cbe-162">è necessario aggiornarli con l'identificatore e l'URL di risposta effettivi.</span><span class="sxs-lookup"><span data-stu-id="94cbe-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="94cbe-163">Per ottenere questi valori contattare il [team di supporto di BeeLine](https://www.beeline.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="94cbe-163">Contact [BeeLine support team](https://www.beeline.com/contact-us/) to get these values.</span></span>
 
4. <span data-ttu-id="94cbe-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="94cbe-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_certificate.png) 

5. <span data-ttu-id="94cbe-166">L'applicazione Beeline si aspetta che le asserzioni SAML abbiano un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="94cbe-166">Your Beeline application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="94cbe-167">Rivolgersi prima al [team di supporto di BeeLine](https://www.beeline.com/contact-us/) per individuare l'identificatore utente corretto di cui verrà eseguito il mapping nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94cbe-167">Please work with [BeeLine support team](https://www.beeline.com/contact-us/) first to identify the correct user identifier which will be mapped into the application.</span></span> <span data-ttu-id="94cbe-168">Seguire anche le indicazioni del [team di supporto di BeeLine](https://www.beeline.com/contact-us/) relative all'attributo da usare per il mapping.</span><span class="sxs-lookup"><span data-stu-id="94cbe-168">Also please take the guidance from [BeeLine support team](https://www.beeline.com/contact-us/) about the attribute which they want to use for this mapping.</span></span> <span data-ttu-id="94cbe-169">È possibile gestire il valore di questo attributo dalla scheda **User Attributes** (Attributi utente) dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94cbe-169">You can manage the value of this attribute from the **User Attributes** tab of the application.</span></span> <span data-ttu-id="94cbe-170">La schermata seguente illustra un esempio relativo a questa operazione.</span><span class="sxs-lookup"><span data-stu-id="94cbe-170">The following screenshot shows an example for this.</span></span> <span data-ttu-id="94cbe-171">In questo caso abbiamo mappato l'attestazione **Identificatore utente** con l'attributo **userprincipalname**, ottenendo un ID utente univoco che verrà inviato all'applicazione BeeLine in ogni risposta SAML corretta.</span><span class="sxs-lookup"><span data-stu-id="94cbe-171">Here we have mapped the **User Identifier** claim with the **userprincipalname** attribute, which provides unique user ID, which will be sent to the Beeline application in the every successful SAML Response.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-beeline-tutorial/tutorial_attribute.png)  

6. <span data-ttu-id="94cbe-173">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="94cbe-173">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-beeline-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="94cbe-175">Nella sezione **Configurazione di BeeLine** fare clic su **Configura BeeLine** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="94cbe-175">On the **BeeLine Configuration** section, click **Configure BeeLine** to open **Configure sign-on** window.</span></span> <span data-ttu-id="94cbe-176">Copiare l'**URL di disconnessione** e l'**ID di entità SAML** dalla **sezione di riferimento rapido**.</span><span class="sxs-lookup"><span data-stu-id="94cbe-176">Copy the **Sign-Out URL** and **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_configure.png) 

8. <span data-ttu-id="94cbe-178">Per configurare l'accesso Single Sign-On sul lato **BeeLine**, è necessario inviare il file **XML metadati**, l'**ID di entità SAML** e l'**URL del servizio Single Sign-On SAML** al [team di supporto di BeeLine](https://www.beeline.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="94cbe-178">To configure single sign-on on **BeeLine** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID**, **Sign-Out URL** to [BeeLine support team](https://www.beeline.com/contact-us/).</span></span>

> [!TIP]
> <span data-ttu-id="94cbe-179">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="94cbe-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="94cbe-180">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="94cbe-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="94cbe-181">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="94cbe-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="94cbe-182">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="94cbe-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="94cbe-183">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="94cbe-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="94cbe-185">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="94cbe-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="94cbe-186">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="94cbe-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="94cbe-188">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="94cbe-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="94cbe-190">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="94cbe-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="94cbe-192">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="94cbe-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="94cbe-194">a.</span><span class="sxs-lookup"><span data-stu-id="94cbe-194">a.</span></span> <span data-ttu-id="94cbe-195">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="94cbe-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="94cbe-196">b.</span><span class="sxs-lookup"><span data-stu-id="94cbe-196">b.</span></span> <span data-ttu-id="94cbe-197">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="94cbe-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="94cbe-198">c.</span><span class="sxs-lookup"><span data-stu-id="94cbe-198">c.</span></span> <span data-ttu-id="94cbe-199">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="94cbe-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="94cbe-200">d.</span><span class="sxs-lookup"><span data-stu-id="94cbe-200">d.</span></span> <span data-ttu-id="94cbe-201">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="94cbe-201">Click **Create**.</span></span>
 
### <a name="creating-a-beeline-test-user"></a><span data-ttu-id="94cbe-202">Creazione di un utente di test di BeeLine</span><span class="sxs-lookup"><span data-stu-id="94cbe-202">Creating a BeeLine test user</span></span>

<span data-ttu-id="94cbe-203">In questa sezione viene creato un utente di nome Britta Simon in Beeline.</span><span class="sxs-lookup"><span data-stu-id="94cbe-203">In this section, you create a user called Britta Simon in Beeline.</span></span> <span data-ttu-id="94cbe-204">L'applicazione BeeLine richiede che venga effettuato il provisioning di tutti gli utenti all'interno dell'applicazione prima di eseguire l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="94cbe-204">Beeline application needs all the users to be provisioned in the application before doing Single Sign On.</span></span> <span data-ttu-id="94cbe-205">Contattare il [team di supporto di BeeLine](https://www.beeline.com/contact-us/) per effettuare il provisioning di tutti gli utenti nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94cbe-205">So work with the [BeeLine support team](https://www.beeline.com/contact-us/) to provision all these users into the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="94cbe-206">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="94cbe-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="94cbe-207">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a BeeLine.</span><span class="sxs-lookup"><span data-stu-id="94cbe-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BeeLine.</span></span>

![Assegna utente][200] 

<span data-ttu-id="94cbe-209">**Per assegnare Britta Simon a BeeLine, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="94cbe-209">**To assign Britta Simon to BeeLine, perform the following steps:**</span></span>

1. <span data-ttu-id="94cbe-210">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="94cbe-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="94cbe-212">Nell'elenco delle applicazioni selezionare **BeeLine**.</span><span class="sxs-lookup"><span data-stu-id="94cbe-212">In the applications list, select **BeeLine**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_app.png) 

3. <span data-ttu-id="94cbe-214">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="94cbe-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="94cbe-216">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="94cbe-216">Click **Add** button.</span></span> <span data-ttu-id="94cbe-217">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="94cbe-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="94cbe-219">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="94cbe-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="94cbe-220">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="94cbe-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="94cbe-221">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="94cbe-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="94cbe-222">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="94cbe-222">Testing single sign-on</span></span>

<span data-ttu-id="94cbe-223">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="94cbe-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="94cbe-224">Quando si fa clic sul riquadro Beeline nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Beeline.</span><span class="sxs-lookup"><span data-stu-id="94cbe-224">When you click the Beeline tile in the Access Panel, you should get automatically signed-on to your Beeline application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="94cbe-225">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="94cbe-225">Additional resources</span></span>

* [<span data-ttu-id="94cbe-226">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94cbe-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="94cbe-227">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94cbe-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_203.png

