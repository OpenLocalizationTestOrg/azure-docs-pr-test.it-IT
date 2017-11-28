---
title: 'Esercitazione: Integrazione di Azure Active Directory con YouEarnedIt | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e YouEarnedIt.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3011d44d-dfcf-4061-888f-cff90fbc8150
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: c29d218dbca581f102caf8070fa40894e7006e71
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-youearnedit"></a><span data-ttu-id="cc29c-103">Esercitazione: Integrazione di Azure Active Directory con YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="cc29c-103">Tutorial: Azure Active Directory integration with YouEarnedIt</span></span>

<span data-ttu-id="cc29c-104">Questa esercitazione descrive come integrare YouEarnedIt con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc29c-104">In this tutorial, you learn how to integrate YouEarnedIt with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc29c-105">L'integrazione di YouEarnedIt con Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="cc29c-105">Integrating YouEarnedIt with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cc29c-106">È possibile controllare in Azure AD chi può accedere a YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="cc29c-106">You can control in Azure AD who has access to YouEarnedIt.</span></span>
- <span data-ttu-id="cc29c-107">È possibile abilitare gli utenti per l'accesso automatico a YouEarnedIt (Single Sign-On) con gli account Azure AD personali.</span><span class="sxs-lookup"><span data-stu-id="cc29c-107">You can enable your users to automatically get signed-on to YouEarnedIt (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="cc29c-108">È possibile gestire gli account in un'unica posizione centrale: il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cc29c-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="cc29c-109">Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cc29c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc29c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cc29c-110">Prerequisites</span></span>

<span data-ttu-id="cc29c-111">Per configurare l'integrazione di Azure AD con YouEarnedIt, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="cc29c-111">To configure Azure AD integration with YouEarnedIt, you need the following items:</span></span>

- <span data-ttu-id="cc29c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc29c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc29c-113">Sottoscrizione di YouEarnedIt abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cc29c-113">A YouEarnedIt single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc29c-114">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="cc29c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc29c-115">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="cc29c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc29c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="cc29c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc29c-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc29c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc29c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="cc29c-118">Scenario description</span></span>
<span data-ttu-id="cc29c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="cc29c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc29c-120">Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="cc29c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc29c-121">Aggiunta di YouEarnedIt dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="cc29c-121">Adding YouEarnedIt from the gallery</span></span>
2. <span data-ttu-id="cc29c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc29c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-youearnedit-from-the-gallery"></a><span data-ttu-id="cc29c-123">Aggiunta di YouEarnedIt dalla raccolta</span><span class="sxs-lookup"><span data-stu-id="cc29c-123">Adding YouEarnedIt from the gallery</span></span>
<span data-ttu-id="cc29c-124">Per configurare l'integrazione di YouEarnedIt in Azure AD, è necessario aggiungere YouEarnedIt dalla raccolta al proprio elenco di app SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="cc29c-124">To configure the integration of YouEarnedIt into Azure AD, you need to add YouEarnedIt from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cc29c-125">**Per aggiungere YouEarnedIt dalla raccolta, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="cc29c-125">**To add YouEarnedIt from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cc29c-126">Nel **[portale di Azure](https://portal.azure.com)** fare clic sull'icona di **Azure Active Directory** nel riquadro di spostamento sinistro.</span><span class="sxs-lookup"><span data-stu-id="cc29c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Pulsante Azure Active Directory][1]

2. <span data-ttu-id="cc29c-128">Passare ad **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="cc29c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cc29c-129">Andare quindi a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cc29c-129">Then go to **All applications**.</span></span>

    ![Pannello Applicazioni aziendali][2]
    
3. <span data-ttu-id="cc29c-131">Fare clic sul pulsante **Nuova applicazione** nella parte superiore della finestra di dialogo per aggiungere una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="cc29c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Pulsante Nuova applicazione][3]

4. <span data-ttu-id="cc29c-133">Nella casella di ricerca digitare **YouEarnedt**, selezionare **YouEarnedt** nel pannello dei risultati e quindi fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cc29c-133">In the search box, type **YouEarnedt**, select  **YouEarnedt**  from result panel then click **Add** button to add the application.</span></span>

    ![YouEarnedIt nell'elenco risultati](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="cc29c-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc29c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="cc29c-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con YouEarnedIt in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cc29c-136">In this section, you configure and test Azure AD single sign-on with YouEarnedIt based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cc29c-137">Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di YouEarnedIt che corrisponde a un utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc29c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in YouEarnedIt is to a user in Azure AD.</span></span> <span data-ttu-id="cc29c-138">In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="cc29c-138">In other words, a link relationship between an Azure AD user and the related user in YouEarnedIt needs to be established.</span></span>

<span data-ttu-id="cc29c-139">Per stabilire la relazione di collegamento, in YouEarnedIt assegnare il valore del **nome utente** in Azure AD come valore di **Username** (Nome utente).</span><span class="sxs-lookup"><span data-stu-id="cc29c-139">In YouEarnedIt, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cc29c-140">Per configurare e testare l'accesso Single Sign-On di Azure AD con YouEarnedIt, è necessario completare i blocchi predefiniti seguenti:</span><span class="sxs-lookup"><span data-stu-id="cc29c-140">To configure and test Azure AD single sign-on with YouEarnedIt, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cc29c-141">**[Configurare l'accesso Single Sign-On di Azure AD](#configure-azure-ad-single-sign-on)**: per consentire agli utenti di usare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="cc29c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cc29c-142">**[Creare un utente di test di Azure AD](#create-an-azure-ad-test-user)**: per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc29c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cc29c-143">**[Creare un utente di test di YouEarnedIt](#create-a-youearnedit-test-user)**: per avere una controparte di Britta Simon in YouEarnedIt collegata alla rappresentazione dell'utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc29c-143">**[Create a YouEarnedIt test user](#create-a-youearnedit-test-user)** - to have a counterpart of Britta Simon in YouEarnedIt that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cc29c-144">**[Assegnare l'utente test di Azure AD](#assign-the-azure-ad-test-user)**: per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc29c-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cc29c-145">**[Testare l'accesso Single Sign-On](#test-single-sign-on)** per verificare se la configurazione funziona.</span><span class="sxs-lookup"><span data-stu-id="cc29c-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="cc29c-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc29c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="cc29c-147">In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure e viene configurato l'accesso Single Sign-On nell'applicazione YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="cc29c-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your YouEarnedIt application.</span></span>

<span data-ttu-id="cc29c-148">**Per configurare l'accesso Single Sign-On di Azure AD con YouEarnedIt, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="cc29c-148">**To configure Azure AD single sign-on with YouEarnedIt, perform the following steps:**</span></span>

1. <span data-ttu-id="cc29c-149">Nella pagina di integrazione dell'applicazione **YouEarnedIt** del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="cc29c-149">In the Azure portal, on the **YouEarnedIt** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento Configura accesso Single Sign-On][4]

2. <span data-ttu-id="cc29c-151">Nella finestra di dialogo **Single Sign-On** selezionare **Accesso basato su SAML** per **Modalità** per abilitare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="cc29c-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_samlbase.png)

3. <span data-ttu-id="cc29c-153">Nella sezione **URL e dominio YouEarnedIt** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="cc29c-153">On the **YouEarnedIt Domain and URLs** section, perform the following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_url.png)

    <span data-ttu-id="cc29c-155">a.</span><span class="sxs-lookup"><span data-stu-id="cc29c-155">a.</span></span> <span data-ttu-id="cc29c-156">Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente:</span><span class="sxs-lookup"><span data-stu-id="cc29c-156">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    | <span data-ttu-id="cc29c-157">Environment</span><span class="sxs-lookup"><span data-stu-id="cc29c-157">Environment</span></span>  | <span data-ttu-id="cc29c-158">Modello</span><span class="sxs-lookup"><span data-stu-id="cc29c-158">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="cc29c-159">Produzione</span><span class="sxs-lookup"><span data-stu-id="cc29c-159">Production</span></span> | `https://<company name>.youearnedit.com/users/sign_in` |
    | <span data-ttu-id="cc29c-160">Sandbox</span><span class="sxs-lookup"><span data-stu-id="cc29c-160">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com/users/sign_in` |

    <span data-ttu-id="cc29c-161">b.</span><span class="sxs-lookup"><span data-stu-id="cc29c-161">b.</span></span> <span data-ttu-id="cc29c-162">Nella casella di testo **Identificatore** digitare un URL usando i criteri seguenti:</span><span class="sxs-lookup"><span data-stu-id="cc29c-162">In the **Identifier** textbox, type a URL using the following patterns:</span></span>
    | <span data-ttu-id="cc29c-163">Environment</span><span class="sxs-lookup"><span data-stu-id="cc29c-163">Environment</span></span>  | <span data-ttu-id="cc29c-164">Modello</span><span class="sxs-lookup"><span data-stu-id="cc29c-164">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="cc29c-165">Produzione</span><span class="sxs-lookup"><span data-stu-id="cc29c-165">Production</span></span> | `https://<company name>.youearnedit.com` |
    | <span data-ttu-id="cc29c-166">Sandbox</span><span class="sxs-lookup"><span data-stu-id="cc29c-166">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com` |

    > [!NOTE] 
    > <span data-ttu-id="cc29c-167">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="cc29c-167">These values are not real.</span></span> <span data-ttu-id="cc29c-168">Aggiornare questi valori con l'identificatore e l'URL di accesso effettivi.</span><span class="sxs-lookup"><span data-stu-id="cc29c-168">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cc29c-169">Per ottenere questi valori, contattare il [team di supporto clienti di YouEarnedIt](https://youearnedit.freshdesk.com/support/tickets/new).</span><span class="sxs-lookup"><span data-stu-id="cc29c-169">Contact [YouEarnedIt Client support team](https://youearnedit.freshdesk.com/support/tickets/new) to get these values.</span></span> 
 
4. <span data-ttu-id="cc29c-170">Nella sezione **Certificato di firma SAML** fare clic su **Certificato (Base64)** e quindi salvare il file del certificato nel computer.</span><span class="sxs-lookup"><span data-stu-id="cc29c-170">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Collegamento di download del certificato](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_certificate.png) 

5. <span data-ttu-id="cc29c-172">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="cc29c-172">Click **Save** button.</span></span>

    ![Pulsante Salva per la configurazione dell'accesso Single Sign-On](./media/active-directory-saas-youearnedit-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cc29c-174">Nella sezione **Configurazione di YouEarnedIt** fare clic su **Configura YouEarnedIt** per aprire la finestra **Configura accesso**.</span><span class="sxs-lookup"><span data-stu-id="cc29c-174">On the **YouEarnedIt Configuration** section, click **Configure YouEarnedIt** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cc29c-175">Copiare l'**URL servizio Single Sign-On SAML** dalla **sezione Riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="cc29c-175">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurazione di YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_configure.png) 

7. <span data-ttu-id="cc29c-177">Per configurare l'accesso Single Sign-On sul lato **YouEarnedIt**, è necessario inviare il **certificato (Base64)** e l'**URL del servizio Single Sign-On SAML** scaricati al [team di supporto di YouEarnedIt](https://youearnedit.freshdesk.com/support/tickets/new).</span><span class="sxs-lookup"><span data-stu-id="cc29c-177">To configure single sign-on on **YouEarnedIt** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [YouEarnedIt support team](https://youearnedit.freshdesk.com/support/tickets/new).</span></span> <span data-ttu-id="cc29c-178">La configurazione viene eseguita in modo che la connessione SSO SAML sia impostata correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="cc29c-178">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="cc29c-179">Un riepilogo delle istruzioni è disponibile all'interno del [portale di Azure](https://portal.azure.com) durante la configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="cc29c-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cc29c-180">Dopo aver aggiunto l'app dalla sezione **Active Directory > Applicazioni aziendali** è sufficiente fare clic sulla scheda **Single Sign-On** e accedere alla documentazione incorporata tramite la sezione **Configurazione** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="cc29c-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cc29c-181">Altre informazioni sulla funzione di documentazione incorporata sono disponibili in [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985) (Documentazione incorporata di Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc29c-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="cc29c-182">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc29c-182">Create an Azure AD test user</span></span>

<span data-ttu-id="cc29c-183">Questa sezione descrive come creare un utente test denominato Britta Simon nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cc29c-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="cc29c-185">**Per creare un utente test in Azure AD, eseguire la procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cc29c-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cc29c-186">Nel portale di Azure fare clic sul pulsante **Azure Active Directory** nel riquadro sinistro.</span><span class="sxs-lookup"><span data-stu-id="cc29c-186">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Pulsante Azure Active Directory](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="cc29c-188">Per visualizzare l'elenco di utenti, passare a **Utenti e gruppi** e quindi fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="cc29c-188">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Collegamenti "Utenti e gruppi" e "Tutti gli utenti"](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="cc29c-190">Per aprire la finestra di dialogo **Utente** fare clic su **Aggiungi** nella parte superiore della finestra di dialogo **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="cc29c-190">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Pulsante Aggiungi](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="cc29c-192">Nella finestra di dialogo **Utente** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="cc29c-192">In the **User** dialog box, perform the following steps:</span></span>

    ![Finestra di dialogo Utente](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="cc29c-194">a.</span><span class="sxs-lookup"><span data-stu-id="cc29c-194">a.</span></span> <span data-ttu-id="cc29c-195">Nella casella **Nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc29c-195">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc29c-196">b.</span><span class="sxs-lookup"><span data-stu-id="cc29c-196">b.</span></span> <span data-ttu-id="cc29c-197">Nella casella **Nome utente** digitare l'indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc29c-197">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="cc29c-198">c.</span><span class="sxs-lookup"><span data-stu-id="cc29c-198">c.</span></span> <span data-ttu-id="cc29c-199">Selezionare la casella di controllo **Mostra password** e quindi prendere nota del valore visualizzato nella casella **Password**.</span><span class="sxs-lookup"><span data-stu-id="cc29c-199">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="cc29c-200">d.</span><span class="sxs-lookup"><span data-stu-id="cc29c-200">d.</span></span> <span data-ttu-id="cc29c-201">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="cc29c-201">Click **Create**.</span></span>
 
### <a name="create-a-youearnedit-test-user"></a><span data-ttu-id="cc29c-202">Creare un utente di test di YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="cc29c-202">Create a YouEarnedIt test user</span></span>

<span data-ttu-id="cc29c-203">In questa sezione viene creato un utente di nome Britta Simon in YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="cc29c-203">In this section, you create a user called Britta Simon in YouEarnedIt.</span></span> <span data-ttu-id="cc29c-204">Collaborare con il team di supporto di YouEarnedIt per aggiungere gli utenti alla piattaforma YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="cc29c-204">Please work with YouEarnedIt support team to add the users in the YouEarnedIt platform.</span></span>

>[!NOTE]
><span data-ttu-id="cc29c-205">YouEarnedIt prevede che il provider di identità fornisca un indirizzo di posta elettronica o un nome utente nell'attributo NameID.</span><span class="sxs-lookup"><span data-stu-id="cc29c-205">YouEarnedIt expect the Identity Provider to supply an EmailAddress  or UserName in the NameID attribute.</span></span> <span data-ttu-id="cc29c-206">Se non viene trovato un indirizzo di posta elettronica o un nome utente perfettamente corrispondente, l'autenticazione avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="cc29c-206">Authentication will fail if a corresponding UserName or EmailAddress is not found within the database or does not match exactly.</span></span> <span data-ttu-id="cc29c-207">È quindi necessario importare gli account nel sistema YouEarnedIt prima dell'integrazione SSO, in genere tramite importazione API o CSV.</span><span class="sxs-lookup"><span data-stu-id="cc29c-207">This will require that accounts be imported into the YouEarnedIt system before the SSO integration (Typically either via API or CSV import).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="cc29c-208">Assegnare l'utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc29c-208">Assign the Azure AD test user</span></span>

<span data-ttu-id="cc29c-209">In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="cc29c-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to YouEarnedIt.</span></span>

![Assegnare il ruolo utente][200] 

<span data-ttu-id="cc29c-211">**Per assegnare Britta Simon a YouEarnedIt, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="cc29c-211">**To assign Britta Simon to YouEarnedIt, perform the following steps:**</span></span>

1. <span data-ttu-id="cc29c-212">Nel portale di Azure aprire la visualizzazione delle applicazioni e quindi la visualizzazione delle directory e passare ad **Applicazioni aziendali**, quindi fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cc29c-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="cc29c-214">Nell'elenco delle applicazioni selezionare **YouEarnedIt**.</span><span class="sxs-lookup"><span data-stu-id="cc29c-214">In the applications list, select **YouEarnedIt**.</span></span>

    ![Collegamento di YouEarnedIt nell'elenco delle applicazioni](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_app.png)  

3. <span data-ttu-id="cc29c-216">Scegliere **Utenti e gruppi** dal menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="cc29c-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][202]

4. <span data-ttu-id="cc29c-218">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cc29c-218">Click **Add** button.</span></span> <span data-ttu-id="cc29c-219">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cc29c-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Riquadro Aggiungi assegnazione][203]

5. <span data-ttu-id="cc29c-221">Nella finestra di dialogo **Utenti e gruppi** selezionare **Britta Simon** nell'elenco Utenti.</span><span class="sxs-lookup"><span data-stu-id="cc29c-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cc29c-222">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="cc29c-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cc29c-223">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cc29c-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="cc29c-224">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cc29c-224">Test single sign-on</span></span>

<span data-ttu-id="cc29c-225">In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="cc29c-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cc29c-226">Quando si fa clic sul riquadro YouEarnedIt nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="cc29c-226">When you click the YouEarnedIt tile in the Access Panel, you should get automatically signed-on to your YouEarnedIt application.</span></span>
<span data-ttu-id="cc29c-227">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cc29c-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cc29c-228">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="cc29c-228">Additional resources</span></span>

* [<span data-ttu-id="cc29c-229">Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc29c-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cc29c-230">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc29c-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_203.png

