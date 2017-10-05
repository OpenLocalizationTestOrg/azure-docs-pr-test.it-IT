---
title: 'Esercitazione: Integrazione di Azure Active Directory con PurelyHR | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e PurelyHR.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 86a9c454-596d-4902-829a-fe126708f739
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: a9075b1759ebd39f164bfe288fb0a365acdcc44c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-purelyhr"></a><span data-ttu-id="ad013-103">Esercitazione: Integrazione di Azure Active Directory con PurelyHR</span><span class="sxs-lookup"><span data-stu-id="ad013-103">Tutorial: Azure Active Directory integration with PurelyHR</span></span>

<span data-ttu-id="ad013-104">Questa esercitazione descrive come integrare PurelyHR con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ad013-104">In this tutorial, you learn how to integrate PurelyHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ad013-105">L'integrazione di PurelyHR con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ad013-105">Integrating PurelyHR with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ad013-106">È possibile controllare in Azure AD chi può accedere a PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="ad013-106">You can control in Azure AD who has access to PurelyHR</span></span>
- <span data-ttu-id="ad013-107">È possibile abilitare gli utenti per l'accesso automatico a PurelyHR (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad013-107">You can enable your users to automatically get signed-on to PurelyHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ad013-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ad013-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ad013-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ad013-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad013-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ad013-110">Prerequisites</span></span>

<span data-ttu-id="ad013-111">Per configurare l'integrazione di Azure AD con PurelyHR, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ad013-111">To configure Azure AD integration with PurelyHR, you need the following items:</span></span>

- <span data-ttu-id="ad013-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad013-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ad013-113">Sottoscrizione di PurelyHR abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="ad013-113">A PurelyHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ad013-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ad013-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ad013-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="ad013-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ad013-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="ad013-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ad013-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ad013-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ad013-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="ad013-118">Scenario description</span></span>
<span data-ttu-id="ad013-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="ad013-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ad013-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ad013-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ad013-121">Aggiunta di PurelyHR dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="ad013-121">Adding PurelyHR from the gallery</span></span>
2. <span data-ttu-id="ad013-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad013-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-purelyhr-from-the-gallery"></a><span data-ttu-id="ad013-123">Aggiunta di PurelyHR dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="ad013-123">Adding PurelyHR from the gallery</span></span>
<span data-ttu-id="ad013-124">Per configurare l'integrazione di PurelyHR in Azure AD, è necessario aggiungere PurelyHR dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="ad013-124">To configure the integration of PurelyHR into Azure AD, you need to add PurelyHR from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ad013-125">**Per aggiungere PurelyHR dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ad013-125">**To add PurelyHR from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ad013-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="ad013-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ad013-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="ad013-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ad013-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ad013-129">Then go to **All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="ad013-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="ad013-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="ad013-133">Nella casella di ricerca digitare **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="ad013-133">In the search box, type **PurelyHR**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_search.png)

5. <span data-ttu-id="ad013-135">Nel pannello dei risultati selezionare **PurelyHR** e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ad013-135">In the results panel, select **PurelyHR**, and then click **Add** button to add the application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ad013-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad013-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ad013-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con PurelyHR con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ad013-138">In this section, you configure and test Azure AD single sign-on with PurelyHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ad013-139">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di PurelyHR che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad013-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PurelyHR is to a user in Azure AD.</span></span> <span data-ttu-id="ad013-140">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="ad013-140">In other words, a link relationship between an Azure AD user and the related user in PurelyHR needs to be established.</span></span>

<span data-ttu-id="ad013-141">Per stabilire la relazione di collegamento, in PurelyHR assegnare il valore di **nome utente** in Azure AD come valore dell'attributo **Username**.</span><span class="sxs-lookup"><span data-stu-id="ad013-141">In PurelyHR, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ad013-142">Per configurare e testare l'accesso Single Sign-On di Azure AD con PurelyHR, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ad013-142">To configure and test Azure AD single sign-on with PurelyHR, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ad013-143">**[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ad013-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ad013-144">**[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad013-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ad013-145">**[Creazione di un utente test di PurelyHR](#creating-a-purelyhr-test-user)**: per avere una controparte di Britta Simon in PurelyHR collegata alla relativa rappresentazione in Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ad013-145">**[Creating a PurelyHR test user](#creating-a-purelyhr-test-user)** - to have a counterpart of Britta Simon in PurelyHR that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ad013-146">**[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad013-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ad013-147">**[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="ad013-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ad013-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad013-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ad013-149">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="ad013-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PurelyHR application.</span></span>

<span data-ttu-id="ad013-150">**Per configurare Single Sign-On di Azure AD con PurelyHR, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ad013-150">**To configure Azure AD single sign-on with PurelyHR, perform the following steps:**</span></span>

1. <span data-ttu-id="ad013-151">Nella pagina di integrazione dell'applicazione **PurelyHR** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="ad013-151">In the Azure portal, on the **PurelyHR** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="ad013-153">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="ad013-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_samlbase.png)

3. <span data-ttu-id="ad013-155">Nella sezione **URL e dominio PurelyHR**, se si vuole configurare l'applicazione in modalità avviata da **IDP**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ad013-155">On the **PurelyHR Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url.png)
   
    <span data-ttu-id="ad013-157">Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://<companyID>.purelyhr.com/sso-consume`</span><span class="sxs-lookup"><span data-stu-id="ad013-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyID>.purelyhr.com/sso-consume`</span></span>

4. <span data-ttu-id="ad013-158">Selezionare **Mostra impostazioni URL avanzate**, se si desidera configurare l'applicazione in modalità avviata da **SP**:</span><span class="sxs-lookup"><span data-stu-id="ad013-158">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url1.png)
    
    <span data-ttu-id="ad013-160">Nella casella di testo **URL di accesso** digitare il valore usando il modello seguente: `https://<companyID>.purelyhr.com/sso-initiate`</span><span class="sxs-lookup"><span data-stu-id="ad013-160">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<companyID>.purelyhr.com/sso-initiate`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="ad013-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="ad013-161">These values are not the real.</span></span> <span data-ttu-id="ad013-162">è necessario aggiornarli con l'URL di risposta e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="ad013-162">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="ad013-163">Per ottenere questi valori, contattare il [team di supporto clienti di PurelyHR](http://support.purelyhr.com/).</span><span class="sxs-lookup"><span data-stu-id="ad013-163">Contact [PurelyHR Client support team](http://support.purelyhr.com/) to get these values.</span></span> 

5. <span data-ttu-id="ad013-164">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="ad013-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_certificate.png) 

6. <span data-ttu-id="ad013-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ad013-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-purelyhr-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="ad013-168">Nella sezione **Configurazione di PurelyHR** fare clic su **Configura PurelyHR** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="ad013-168">On the **PurelyHR Configuration** section, click **Configure PurelyHR** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ad013-169">Copiare l'**ID di entità SAML e l'URL del servizio Single Sign-On SAML** dalla sezione **Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="ad013-169">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_configure.png) 

8. <span data-ttu-id="ad013-171">Per configurare l'accesso Single Sign-On sul lato **PurelyHR**, accedere al sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="ad013-171">To configure single sign-on on **PurelyHR** side, login to their website as an administrator.</span></span>

9. <span data-ttu-id="ad013-172">Aprire il **dashboard** dalle opzioni nella barra degli strumenti e fare clic su **SSO Settings** (Impostazioni SSO).</span><span class="sxs-lookup"><span data-stu-id="ad013-172">Open the **Dashboard** from the options in the toolbar and click **SSO Settings**.</span></span>

10. <span data-ttu-id="ad013-173">Incollare i valori nelle caselle come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="ad013-173">Paste the values in the boxes as described below-</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-purelyhr-tutorial/purelyhr-dashboard-sso-settings.png)    

    <span data-ttu-id="ad013-175">a.</span><span class="sxs-lookup"><span data-stu-id="ad013-175">a.</span></span> <span data-ttu-id="ad013-176">Aprire il certificato **Certificate(Bas64)** scaricato dal portale di Azure nel blocco note e copiare il valore del certificato.</span><span class="sxs-lookup"><span data-stu-id="ad013-176">Open the **Certificate(Bas64)** downloaded from the Azure portal in notepad and copy the certificate value.</span></span> <span data-ttu-id="ad013-177">Incollare il valore copiato nella casella **x509 Certificate** (Certificato x509).</span><span class="sxs-lookup"><span data-stu-id="ad013-177">Paste the copied value into the **X.509 Certificate** box.</span></span>

    <span data-ttu-id="ad013-178">b.</span><span class="sxs-lookup"><span data-stu-id="ad013-178">b.</span></span> <span data-ttu-id="ad013-179">Nella casella **IdP Issuer URL** (URL autorità emittente IdP), incollare l'**ID di entità SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ad013-179">In the **Idp Issuer URL** box, paste the **SAML Entity ID** copied from the Azure portal.</span></span>

    <span data-ttu-id="ad013-180">c.</span><span class="sxs-lookup"><span data-stu-id="ad013-180">c.</span></span> <span data-ttu-id="ad013-181">Nella casella **IdP Endpoint URL**(URL Endpoint IdP) incollare l'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ad013-181">In the **Idp Endpoint URL** box, paste the **SAML Single Sign-On Service URL** copied from the Azure portal.</span></span> 

    <span data-ttu-id="ad013-182">d.</span><span class="sxs-lookup"><span data-stu-id="ad013-182">d.</span></span> <span data-ttu-id="ad013-183">Selezionare la casella di controllo **Auto-Create Users** (Creazione automatica utenti) per abilitare il provisioning utenti automatico in PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="ad013-183">Check the **Auto-Create Users** checkbox to enable automatic user provisioning in PurelyHR.</span></span>

    <span data-ttu-id="ad013-184">e.</span><span class="sxs-lookup"><span data-stu-id="ad013-184">e.</span></span> <span data-ttu-id="ad013-185">Fare clic su **Salva** per salvare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="ad013-185">Click **Save Changes** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="ad013-186">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="ad013-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ad013-187">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="ad013-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ad013-188">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ad013-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ad013-189">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad013-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="ad013-190">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ad013-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="ad013-192">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ad013-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ad013-193">Nel **portale di Azure** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="ad013-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ad013-195">Passare a **Utenti e gruppi** e fare clic su **Tutti gli utenti** per visualizzare l'elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="ad013-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ad013-197">Nella parte superiore della finestra di dialogo fare clic su **Aggiungi** per aprire la finestra di dialogo **Utente**.</span><span class="sxs-lookup"><span data-stu-id="ad013-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ad013-199">Nella pagina della finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ad013-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ad013-201">a.</span><span class="sxs-lookup"><span data-stu-id="ad013-201">a.</span></span> <span data-ttu-id="ad013-202">Nella casella di testo **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ad013-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ad013-203">b.</span><span class="sxs-lookup"><span data-stu-id="ad013-203">b.</span></span> <span data-ttu-id="ad013-204">Nella casella di testo **Nome utente** digitare l'**indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ad013-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ad013-205">c.</span><span class="sxs-lookup"><span data-stu-id="ad013-205">c.</span></span> <span data-ttu-id="ad013-206">Selezionare **Mostra password** e prendere nota del valore della **Password**.</span><span class="sxs-lookup"><span data-stu-id="ad013-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ad013-207">d.</span><span class="sxs-lookup"><span data-stu-id="ad013-207">d.</span></span> <span data-ttu-id="ad013-208">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ad013-208">Click **Create**.</span></span>
 
### <a name="creating-a-purelyhr-test-user"></a><span data-ttu-id="ad013-209">Creazione di un utente test di PurelyHR</span><span class="sxs-lookup"><span data-stu-id="ad013-209">Creating a PurelyHR test user</span></span>

<span data-ttu-id="ad013-210">Per consentire agli utenti di Azure AD di accedere a PurelyHR, è necessario eseguirne il provisioning in PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="ad013-210">To enable Azure AD users to log in to PurelyHR, they must be provisioned into PurelyHR.</span></span> <span data-ttu-id="ad013-211">In PurelyHR, il provisioning è un'attività automatica e non sono necessari passaggi manuali se è abilitato il provisioning utente automatico.</span><span class="sxs-lookup"><span data-stu-id="ad013-211">In PurelyHR, provisioning is an automatic task and no manual steps are required when automatic user provisioning is enabled.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ad013-212">Assegnazione dell'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad013-212">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ad013-213">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="ad013-213">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PurelyHR.</span></span>

![Assegna utente][200] 

<span data-ttu-id="ad013-215">**Per assegnare Britta Simon a PurelyHR, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="ad013-215">**To assign Britta Simon to PurelyHR, perform the following steps:**</span></span>

1. <span data-ttu-id="ad013-216">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ad013-216">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="ad013-218">Nell'elenco di applicazioni selezionare **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="ad013-218">In the applications list, select **PurelyHR**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_app.png) 

3. <span data-ttu-id="ad013-220">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="ad013-220">In the menu on the left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="ad013-222">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ad013-222">Click **Add** button.</span></span> <span data-ttu-id="ad013-223">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ad013-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="ad013-225">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="ad013-225">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ad013-226">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ad013-226">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ad013-227">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ad013-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ad013-228">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ad013-228">Testing single sign-on</span></span>

<span data-ttu-id="ad013-229">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="ad013-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ad013-230">Quando si fa clic sul riquadro Absorb LMS nel pannello di accesso, si accede automaticamente all'applicazione Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="ad013-230">Click the Absorb LMS tile in the Access Panel, you get automatically signed-on to your Absorb LMS application.</span></span>

<span data-ttu-id="ad013-231">Per ulteriori informazioni sul pannello di accesso, vedere</span><span class="sxs-lookup"><span data-stu-id="ad013-231">For more information about the Access Panel, see.</span></span> <span data-ttu-id="ad013-232">[Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586)</span><span class="sxs-lookup"><span data-stu-id="ad013-232">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ad013-233">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ad013-233">Additional resources</span></span>

* [<span data-ttu-id="ad013-234">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ad013-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ad013-235">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ad013-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_203.png

