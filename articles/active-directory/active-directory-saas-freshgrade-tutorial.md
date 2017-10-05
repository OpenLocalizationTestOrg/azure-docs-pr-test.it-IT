---
title: 'Esercitazione: Integrazione di Azure Active Directory con FreshGrade | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e FreshGrade.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1055bba6-f4df-462e-bc9b-1ad5ada0f638
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 3ff3e5aab679f8ee610c98f8a4089308adcce48f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshgrade"></a><span data-ttu-id="fb83e-103">Esercitazione: Integrazione di Azure Active Directory con FreshGrade</span><span class="sxs-lookup"><span data-stu-id="fb83e-103">Tutorial: Azure Active Directory integration with FreshGrade</span></span>

<span data-ttu-id="fb83e-104">Questa esercitazione descrive come integrare FreshGrade con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fb83e-104">In this tutorial, you learn how to integrate FreshGrade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fb83e-105">L'integrazione di FreshGrade con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="fb83e-105">Integrating FreshGrade with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fb83e-106">È possibile controllare in Azure AD chi può accedere a FreshGrade</span><span class="sxs-lookup"><span data-stu-id="fb83e-106">You can control in Azure AD who has access to FreshGrade</span></span>
- <span data-ttu-id="fb83e-107">È possibile abilitare gli utenti per l'accesso automatico Single Sign-On a FreshGrade con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb83e-107">You can enable your users to automatically get signed-on to FreshGrade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fb83e-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fb83e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fb83e-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fb83e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb83e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fb83e-110">Prerequisites</span></span>

<span data-ttu-id="fb83e-111">Per configurare l'integrazione di Azure AD con FreshGrade, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="fb83e-111">To configure Azure AD integration with FreshGrade, you need the following items:</span></span>

- <span data-ttu-id="fb83e-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb83e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fb83e-113">Sottoscrizione di FreshGrade abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fb83e-113">A FreshGrade single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fb83e-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="fb83e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fb83e-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="fb83e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fb83e-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="fb83e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fb83e-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fb83e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fb83e-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="fb83e-118">Scenario description</span></span>
<span data-ttu-id="fb83e-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="fb83e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fb83e-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="fb83e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fb83e-121">Aggiunta di FreshGrade dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="fb83e-121">Adding FreshGrade from the gallery</span></span>
2. <span data-ttu-id="fb83e-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb83e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshgrade-from-the-gallery"></a><span data-ttu-id="fb83e-123">Aggiunta di FreshGrade dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="fb83e-123">Adding FreshGrade from the gallery</span></span>
<span data-ttu-id="fb83e-124">Per configurare l'integrazione di FreshGrade in Azure AD, è necessario aggiungerla dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="fb83e-124">To configure the integration of FreshGrade into Azure AD, you need to add FreshGrade from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fb83e-125">**Per aggiungere FreshGrade dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="fb83e-125">**To add FreshGrade from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fb83e-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="fb83e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fb83e-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="fb83e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fb83e-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fb83e-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="fb83e-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="fb83e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="fb83e-133">Nella casella di ricerca digitare **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="fb83e-133">In the search box, type **FreshGrade**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_search.png)

5. <span data-ttu-id="fb83e-135">Nel pannello dei risultati selezionare **FreshGrade** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fb83e-135">In the results panel, select **FreshGrade**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fb83e-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb83e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fb83e-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con FreshGrade in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fb83e-138">In this section, you configure and test Azure AD single sign-on with FreshGrade based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fb83e-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di FreshGrade che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb83e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshGrade is to a user in Azure AD.</span></span> <span data-ttu-id="fb83e-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="fb83e-140">In other words, a link relationship between an Azure AD user and the related user in FreshGrade needs to be established.</span></span>

<span data-ttu-id="fb83e-141">Per stabilire la relazione di collegamento, in FreshGrade assegnare il valore di **nome utente** di Azure AD come valore dell'attributo **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="fb83e-141">In FreshGrade, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fb83e-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con FreshGrade, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="fb83e-142">To configure and test Azure AD single sign-on with FreshGrade, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fb83e-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="fb83e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fb83e-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fb83e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fb83e-145">**[Creazione di un utente test di FreshGrade](#creating-a-freshgrade-test-user)**: per avere una controparte di Britta Simon in FreshGrade collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb83e-145">**[Creating a FreshGrade test user](#creating-a-freshgrade-test-user)** - to have a counterpart of Britta Simon in FreshGrade that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fb83e-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb83e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fb83e-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="fb83e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fb83e-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb83e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fb83e-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="fb83e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FreshGrade application.</span></span>

<span data-ttu-id="fb83e-150">**Per configurare Single Sign-On di Azure AD con FreshGrade, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="fb83e-150">**To configure Azure AD single sign-on with FreshGrade, perform the following steps:**</span></span>

1. <span data-ttu-id="fb83e-151">Nella pagina di integrazione dell'applicazione **FreshGrade** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="fb83e-151">In the Azure portal, on the **FreshGrade** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="fb83e-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="fb83e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_samlbase.png)

3. <span data-ttu-id="fb83e-155">Nella sezione **URL e dominio FreshGrade** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="fb83e-155">On the **FreshGrade Domain and URLs** section, perform the following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_url.png)

    <span data-ttu-id="fb83e-157">a.</span><span class="sxs-lookup"><span data-stu-id="fb83e-157">a.</span></span> <span data-ttu-id="fb83e-158">Nella casella di testo **URL di accesso** digitare un URL usando i criteri seguenti:</span><span class="sxs-lookup"><span data-stu-id="fb83e-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
      | |
      |--|
      | `https://<subdomain>.freshgrade.com/login` |    
      | `https://<subdomain>.onboarding.freshgrade.com/login` |

    <span data-ttu-id="fb83e-159">b.</span><span class="sxs-lookup"><span data-stu-id="fb83e-159">b.</span></span> <span data-ttu-id="fb83e-160">Nella casella di testo **Identificatore** digitare un URL usando i criteri seguenti:</span><span class="sxs-lookup"><span data-stu-id="fb83e-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
      | |
      |--|
      | `https://login.onboarding.freshgrade.com:443/saml/metadata/alias/<instancename>` |      
      | `https://login.freshgrade.com:443/saml/metadata/alias/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="fb83e-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="fb83e-161">These values are not real.</span></span> <span data-ttu-id="fb83e-162">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="fb83e-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fb83e-163">Per ottenere questi valori contattare il [team di supporto clienti di FreshGrade](mailTo:support@freshgrade.com).</span><span class="sxs-lookup"><span data-stu-id="fb83e-163">Contact [FreshGrade Client support team](mailTo:support@freshgrade.com) to get these values.</span></span> 
 


4. <span data-ttu-id="fb83e-164">Nella sezione **Certificato di firma SAML** fare clic su **XML di metadati** e quindi salvare il file dei metadati nel computer.</span><span class="sxs-lookup"><span data-stu-id="fb83e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_certificate.png) 

5. <span data-ttu-id="fb83e-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="fb83e-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshgrade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fb83e-168">Nella sezione**Configurazione di FreshGrade** fare clic su **Configura FreshGrade** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="fb83e-168">On the **FreshGrade Configuration** section, click **Configure FreshGrade** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fb83e-169">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="fb83e-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_configure.png) 

7. <span data-ttu-id="fb83e-171">Per generare l'URL dei **metadati**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="fb83e-171">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="fb83e-172">a.</span><span class="sxs-lookup"><span data-stu-id="fb83e-172">a.</span></span> <span data-ttu-id="fb83e-173">Fare clic su **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="fb83e-173">Click **App registrations**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appregistrations.png)
   
    <span data-ttu-id="fb83e-175">b.</span><span class="sxs-lookup"><span data-stu-id="fb83e-175">b.</span></span> <span data-ttu-id="fb83e-176">Fare clic su **Endpoint** per aprire la finestra di dialogo **Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="fb83e-176">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpointicon.png)

    <span data-ttu-id="fb83e-178">c.</span><span class="sxs-lookup"><span data-stu-id="fb83e-178">c.</span></span> <span data-ttu-id="fb83e-179">Fare clic sul pulsante Copia per copiare l'URL del **DOCUMENTO METADATI FEDERAZIONE** e incollarlo nel Blocco note.</span><span class="sxs-lookup"><span data-stu-id="fb83e-179">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpoint.png)
     
    <span data-ttu-id="fb83e-181">d.</span><span class="sxs-lookup"><span data-stu-id="fb83e-181">d.</span></span> <span data-ttu-id="fb83e-182">Passare ora alla pagina delle proprietà di **FreshGrade**, copiare l'**ID applicazione** usando il pulsante **Copia** e incollarlo nel Blocco note.</span><span class="sxs-lookup"><span data-stu-id="fb83e-182">Now go to the property page of **FreshGrade** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appid.png)

    <span data-ttu-id="fb83e-184">e.</span><span class="sxs-lookup"><span data-stu-id="fb83e-184">e.</span></span> <span data-ttu-id="fb83e-185">Generare l'**URL dei metadati** usando il modello seguente: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="fb83e-185">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

8. <span data-ttu-id="fb83e-186">Per configurare l'accesso Single Sign-On sul lato **FreshGrade**, è necessario inviare il file **URL dei metadati** e il valore **SAML Single Sign-On Service URL** (URL servizio Single Sign-On SAML) al [team di supporto di FreshGrade](mailTo:support@freshgrade.com).</span><span class="sxs-lookup"><span data-stu-id="fb83e-186">To configure single sign-on on **FreshGrade** side, you need to send the **Metadata URL** and **SAML Single Sign-On Service URL** to [FreshGrade support team](mailTo:support@freshgrade.com).</span></span> <span data-ttu-id="fb83e-187">Questa impostazione viene configurata in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="fb83e-187">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="fb83e-188">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="fb83e-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fb83e-189">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="fb83e-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fb83e-190">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fb83e-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fb83e-191">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb83e-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="fb83e-192">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fb83e-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="fb83e-194">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fb83e-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fb83e-195">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="fb83e-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fb83e-197">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="fb83e-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fb83e-199">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="fb83e-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fb83e-201">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="fb83e-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fb83e-203">a.</span><span class="sxs-lookup"><span data-stu-id="fb83e-203">a.</span></span> <span data-ttu-id="fb83e-204">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fb83e-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fb83e-205">b.</span><span class="sxs-lookup"><span data-stu-id="fb83e-205">b.</span></span> <span data-ttu-id="fb83e-206">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fb83e-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fb83e-207">c.</span><span class="sxs-lookup"><span data-stu-id="fb83e-207">c.</span></span> <span data-ttu-id="fb83e-208">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="fb83e-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fb83e-209">d.</span><span class="sxs-lookup"><span data-stu-id="fb83e-209">d.</span></span> <span data-ttu-id="fb83e-210">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="fb83e-210">Click **Create**.</span></span>
 
### <a name="creating-a-freshgrade-test-user"></a><span data-ttu-id="fb83e-211">Creazione di un utente test di FreshGrade</span><span class="sxs-lookup"><span data-stu-id="fb83e-211">Creating a FreshGrade test user</span></span>

<span data-ttu-id="fb83e-212">In questa sezione viene creato un utente chiamato Britta Simon in FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="fb83e-212">In this section, you create a user called Britta Simon in FreshGrade.</span></span> <span data-ttu-id="fb83e-213">Collaborare con il [team di supporto di FreshGrade](mailTo:support@freshgrade.com) per aggiungere gli utenti nella piattaforma FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="fb83e-213">Please work with [FreshGrade support team](mailTo:support@freshgrade.com) to add the users in the FreshGrade platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fb83e-214">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb83e-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fb83e-215">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="fb83e-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FreshGrade.</span></span>

![Assegna utente][200] 

<span data-ttu-id="fb83e-217">**Per assegnare Britta Simon a FreshGrade, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="fb83e-217">**To assign Britta Simon to FreshGrade, perform the following steps:**</span></span>

1. <span data-ttu-id="fb83e-218">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fb83e-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="fb83e-220">Nell'elenco delle applicazioni selezionare **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="fb83e-220">In the applications list, select **FreshGrade**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_app.png) 

3. <span data-ttu-id="fb83e-222">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="fb83e-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="fb83e-224">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="fb83e-224">Click **Add** button.</span></span> <span data-ttu-id="fb83e-225">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="fb83e-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="fb83e-227">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="fb83e-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fb83e-228">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="fb83e-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fb83e-229">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="fb83e-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fb83e-230">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fb83e-230">Testing single sign-on</span></span>

<span data-ttu-id="fb83e-231">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="fb83e-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fb83e-232">Quando si fa clic sul riquadro FreshGrade nel pannello di accesso, si accederà automaticamente all'applicazione FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="fb83e-232">When you click the FreshGrade tile in the Access Panel, you should get automatically signed-on to your FreshGrade application.</span></span>
<span data-ttu-id="fb83e-233">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fb83e-233">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fb83e-234">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="fb83e-234">Additional resources</span></span>

* [<span data-ttu-id="fb83e-235">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb83e-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fb83e-236">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb83e-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_203.png

