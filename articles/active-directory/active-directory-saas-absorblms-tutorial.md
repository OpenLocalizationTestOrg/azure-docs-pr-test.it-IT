---
title: 'Esercitazione: Integrazione di Azure Active Directory con Absorb LMS | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e assorbire LMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: a140a78a3a9474a6372a3ad4fb8251bd2452c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a><span data-ttu-id="bbdca-103">Esercitazione: Integrazione di Azure Active Directory con Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="bbdca-103">Tutorial: Azure Active Directory integration with Absorb LMS</span></span>

<span data-ttu-id="bbdca-104">In questa esercitazione, è illustrato come toointegrate Absorb LMS con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bbdca-104">In this tutorial, you learn how toointegrate Absorb LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bbdca-105">Integrazione di assorbire LMS con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="bbdca-105">Integrating Absorb LMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bbdca-106">È possibile controllare in Azure AD che ha accesso tooAbsorb LMS</span><span class="sxs-lookup"><span data-stu-id="bbdca-106">You can control in Azure AD who has access tooAbsorb LMS</span></span>
- <span data-ttu-id="bbdca-107">È possibile abilitare l'utenti tooautomatically get connesso tooAbsorb LMS (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbdca-107">You can enable your users tooautomatically get signed-on tooAbsorb LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bbdca-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="bbdca-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bbdca-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere.</span><span class="sxs-lookup"><span data-stu-id="bbdca-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="bbdca-110">[Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bbdca-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbdca-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bbdca-111">Prerequisites</span></span>

<span data-ttu-id="bbdca-112">integrazione di Azure AD con assorbire LMS tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="bbdca-112">tooconfigure Azure AD integration with Absorb LMS, you need hello following items:</span></span>

- <span data-ttu-id="bbdca-113">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbdca-113">An Azure AD subscription</span></span>
- <span data-ttu-id="bbdca-114">Sottoscrizione di Absorb LMS abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="bbdca-114">An Absorb LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bbdca-115">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="bbdca-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bbdca-116">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="bbdca-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bbdca-117">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="bbdca-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bbdca-118">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bbdca-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bbdca-119">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="bbdca-119">Scenario description</span></span>
<span data-ttu-id="bbdca-120">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="bbdca-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bbdca-121">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="bbdca-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bbdca-122">Aggiunta di assorbire LMS dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="bbdca-122">Adding Absorb LMS from hello gallery</span></span>
2. <span data-ttu-id="bbdca-123">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbdca-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-absorb-lms-from-hello-gallery"></a><span data-ttu-id="bbdca-124">Aggiunta di assorbire LMS dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="bbdca-124">Adding Absorb LMS from hello gallery</span></span>
<span data-ttu-id="bbdca-125">integrazione hello tooconfigure di assorbire LMS in tooAzure Active Directory, è necessario tooadd Absorb LMS dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="bbdca-125">tooconfigure hello integration of Absorb LMS in tooAzure AD, you need tooadd Absorb LMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bbdca-126">**tooadd Absorb LMS dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bbdca-126">**tooadd Absorb LMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbdca-127">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="bbdca-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="bbdca-129">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="bbdca-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bbdca-130">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="bbdca-130">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="bbdca-132">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="bbdca-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="bbdca-134">Nella casella di ricerca hello, digitare **assorbire LMS**selezionare **assorbire LMS** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="bbdca-134">In hello search box, type **Absorb LMS**, select **Absorb LMS** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Assorbire LMS nell'elenco risultati hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bbdca-136">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbdca-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="bbdca-137">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Absorb LMS usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bbdca-137">In this section, you configure and test Azure AD single sign-on with Absorb LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bbdca-138">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in assorbire LMS è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbdca-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Absorb LMS is tooa user in Azure AD.</span></span> <span data-ttu-id="bbdca-139">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato hello assorbire LMS deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="bbdca-139">In other words, a link relationship between an Azure AD user and hello related user in Absorb LMS needs toobe established.</span></span>

<span data-ttu-id="bbdca-140">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in assorbire LMS.</span><span class="sxs-lookup"><span data-stu-id="bbdca-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Absorb LMS.</span></span>

<span data-ttu-id="bbdca-141">tooconfigure e prova AD Azure single sign-on con assorbire LMS, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="bbdca-141">tooconfigure and test Azure AD single sign-on with Absorb LMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bbdca-142">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="bbdca-142">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bbdca-143">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbdca-143">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bbdca-144">**[Creare un utente test assorbire LMS](#create-an-absorb-lms-test-user)**  -toohave un equivalente di Britta Simon in LMS assorbire che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="bbdca-144">**[Create an Absorb LMS test user](#create-an-absorb-lms-test-user)** - toohave a counterpart of Britta Simon in Absorb LMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bbdca-145">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bbdca-145">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bbdca-146">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="bbdca-146">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="bbdca-147">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbdca-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="bbdca-148">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione assorbire LMS.</span><span class="sxs-lookup"><span data-stu-id="bbdca-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Absorb LMS application.</span></span>

<span data-ttu-id="bbdca-149">**Azure AD tooconfigure single sign-on con assorbire LMS, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bbdca-149">**tooconfigure Azure AD single sign-on with Absorb LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbdca-150">Nel portale di Azure su hello hello **assorbire LMS** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="bbdca-150">In hello Azure portal, on hello **Absorb LMS** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="bbdca-152">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bbdca-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. <span data-ttu-id="bbdca-154">In hello **assorbire LMS dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bbdca-154">On hello **Absorb LMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    <span data-ttu-id="bbdca-156">a.</span><span class="sxs-lookup"><span data-stu-id="bbdca-156">a.</span></span> <span data-ttu-id="bbdca-157">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="bbdca-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>

    <span data-ttu-id="bbdca-158">b.</span><span class="sxs-lookup"><span data-stu-id="bbdca-158">b.</span></span> <span data-ttu-id="bbdca-159">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="bbdca-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="bbdca-160">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="bbdca-160">These values are not hello real.</span></span> <span data-ttu-id="bbdca-161">Aggiornare questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="bbdca-161">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="bbdca-162">Contatto [team di supporto Client di LMS assorbire](https://www.absorblms.com/support) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="bbdca-162">Contact [Absorb LMS Client support team](https://www.absorblms.com/support) tooget these values.</span></span> 

4. <span data-ttu-id="bbdca-163">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="bbdca-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. <span data-ttu-id="bbdca-165">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="bbdca-165">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="bbdca-167">In hello **assorbire configurazione LMS** fare clic su **configurare LMS assorbire** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="bbdca-167">On hello **Absorb LMS Configuration** section, click **Configure Absorb LMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bbdca-168">Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="bbdca-168">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. <span data-ttu-id="bbdca-170">In una finestra del web browser, accedere come amministratore nel sito della società di assorbire LMS tooyour.</span><span class="sxs-lookup"><span data-stu-id="bbdca-170">In a different web browser window, log in tooyour Absorb LMS company site as an administrator.</span></span>

9. <span data-ttu-id="bbdca-171">Fare clic su hello **icona Account** sull'interfaccia di amministrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="bbdca-171">Click hello **Account Icon** on hello admin interface.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-absorblms-tutorial/1.png)

10. <span data-ttu-id="bbdca-173">Fare clic su **Impostazioni portale**.</span><span class="sxs-lookup"><span data-stu-id="bbdca-173">Click **Portal Settings**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. <span data-ttu-id="bbdca-175">Fare clic su hello **utenti** scheda.</span><span class="sxs-lookup"><span data-stu-id="bbdca-175">Click hello **Users** tab.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-absorblms-tutorial/3.png)

12. <span data-ttu-id="bbdca-177">Eseguire hello seguendo i passaggi tooaccess hello Single Sign-On i campi della configurazione:</span><span class="sxs-lookup"><span data-stu-id="bbdca-177">Perform hello following steps tooaccess hello Single Sign-On configuration fields:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-absorblms-tutorial/4.png)

    <span data-ttu-id="bbdca-179">a.</span><span class="sxs-lookup"><span data-stu-id="bbdca-179">a.</span></span> <span data-ttu-id="bbdca-180">Seleziona hello appropriato **modalità**.</span><span class="sxs-lookup"><span data-stu-id="bbdca-180">Select hello appropriate **Mode**.</span></span>

    <span data-ttu-id="bbdca-181">b.</span><span class="sxs-lookup"><span data-stu-id="bbdca-181">b.</span></span> <span data-ttu-id="bbdca-182">Aprire hello certificato scaricato dal portale di Azure nel blocco note, hello rimuovere hello **---BEGIN CERTIFICATE---** e **---END CERTIFICATE---** tag e quindi incollare hello rimanente contenuto in Hello **chiave** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="bbdca-182">Open hello Certificate that you have downloaded from hello Azure portal in notepad, remove hello **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste hello remaining content in hello **Key** textbox.</span></span>
    
    <span data-ttu-id="bbdca-183">c.</span><span class="sxs-lookup"><span data-stu-id="bbdca-183">c.</span></span> <span data-ttu-id="bbdca-184">In hello **Id proprietà**, selezionare hello attributo appropriato che è stato configurato come hello identificatore utente in hello Azure Active Directory (ad esempio, se viene selezionato userprinciplename hello in Azure AD, nome utente potrebbe essere selezionato qui).</span><span class="sxs-lookup"><span data-stu-id="bbdca-184">In hello **Id Property**, select hello appropriate attribute which you have configured as hello user identifier in hello Azure AD (For example, If hello userprinciplename is selected in Azure AD, then Username would be selected here.)</span></span>

    <span data-ttu-id="bbdca-185">d.</span><span class="sxs-lookup"><span data-stu-id="bbdca-185">d.</span></span> <span data-ttu-id="bbdca-186">In hello **URL di accesso**, incollare hello **"SAML Single Sign-On Service URL"** valore copiato da hello **Configura sign-on** finestra di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bbdca-186">In hello **Login URL**, paste hello **“SAML Single Sign-On Service URL”** value you have copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

    <span data-ttu-id="bbdca-187">e.</span><span class="sxs-lookup"><span data-stu-id="bbdca-187">e.</span></span> <span data-ttu-id="bbdca-188">In hello **Logout URL**, incollare hello **"Sign-Out URL"** valore copiato da hello **Configura sign-on** finestra di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bbdca-188">In hello **Logout URL**, paste hello **“Sign-Out URL”** value you have copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

13. <span data-ttu-id="bbdca-189">Abilitare **Only Allow SSO Login** (Consenti solo accesso SSO).</span><span class="sxs-lookup"><span data-stu-id="bbdca-189">Enable **‘Only Allow SSO Login’**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-absorblms-tutorial/5.png)

14. <span data-ttu-id="bbdca-191">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="bbdca-191">Click **"Save."**</span></span>

> [!TIP]
> <span data-ttu-id="bbdca-192">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="bbdca-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bbdca-193">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="bbdca-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bbdca-194">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bbdca-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bbdca-195">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbdca-195">Create an Azure AD test user</span></span>

<span data-ttu-id="bbdca-196">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="bbdca-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="bbdca-198">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bbdca-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbdca-199">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="bbdca-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bbdca-201">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="bbdca-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bbdca-203">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="bbdca-203">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bbdca-205">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bbdca-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![finestra di dialogo utente Hello](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bbdca-207">a.</span><span class="sxs-lookup"><span data-stu-id="bbdca-207">a.</span></span> <span data-ttu-id="bbdca-208">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bbdca-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bbdca-209">b.</span><span class="sxs-lookup"><span data-stu-id="bbdca-209">b.</span></span> <span data-ttu-id="bbdca-210">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bbdca-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bbdca-211">c.</span><span class="sxs-lookup"><span data-stu-id="bbdca-211">c.</span></span> <span data-ttu-id="bbdca-212">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="bbdca-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bbdca-213">d.</span><span class="sxs-lookup"><span data-stu-id="bbdca-213">d.</span></span> <span data-ttu-id="bbdca-214">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="bbdca-214">Click **Create**.</span></span>

### <a name="create-an-absorb-lms-test-user"></a><span data-ttu-id="bbdca-215">Creare un utente di test di Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="bbdca-215">Create an Absorb LMS test user</span></span>

<span data-ttu-id="bbdca-216">toolog agli utenti di Azure AD tooenable in tooAbsorb LMS, è necessario eseguirne il provisioning in tooAbsorb LMS.</span><span class="sxs-lookup"><span data-stu-id="bbdca-216">tooenable Azure AD users toolog in tooAbsorb LMS, they must be provisioned in tooAbsorb LMS.</span></span>  
<span data-ttu-id="bbdca-217">In Absorb LMS il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="bbdca-217">For Absorb LMS, provisioning is a manual task.</span></span>

<span data-ttu-id="bbdca-218">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bbdca-218">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbdca-219">Accedi tooyour sito della società assorbire LMS come amministratore.</span><span class="sxs-lookup"><span data-stu-id="bbdca-219">Log in tooyour Absorb LMS company site as an administrator.</span></span>

2. <span data-ttu-id="bbdca-220">Fare clic sulla scheda **Utenti** scheda.</span><span class="sxs-lookup"><span data-stu-id="bbdca-220">Click **Users** tab.</span></span>

    ![Invita persone](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. <span data-ttu-id="bbdca-222">Fare clic su **utenti** in hello **utenti** scheda.</span><span class="sxs-lookup"><span data-stu-id="bbdca-222">Click **Users** under hello **Users** tab.</span></span>

    ![Invita persone](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  <span data-ttu-id="bbdca-224">Dal menu a discesa **Aggiungi nuovo** selezionare **Utente**.</span><span class="sxs-lookup"><span data-stu-id="bbdca-224">Select **User** from **Add New** drop-down.</span></span>

    ![Invita persone](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. <span data-ttu-id="bbdca-226">In hello **Aggiungi utente** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bbdca-226">On hello **Add User** page, perform hello following steps:</span></span>

    ![Invita persone](./media/active-directory-saas-absorblms-tutorial/user.png)

    <span data-ttu-id="bbdca-228">a.</span><span class="sxs-lookup"><span data-stu-id="bbdca-228">a.</span></span> <span data-ttu-id="bbdca-229">In hello **nome** casella di testo, nome del primo tipo hello come Laura.</span><span class="sxs-lookup"><span data-stu-id="bbdca-229">In hello **First Name** textbox, type hello first name like Britta.</span></span>

    <span data-ttu-id="bbdca-230">b.</span><span class="sxs-lookup"><span data-stu-id="bbdca-230">b.</span></span> <span data-ttu-id="bbdca-231">In hello **cognome** casella di testo, digitare hello cognome come Simon.</span><span class="sxs-lookup"><span data-stu-id="bbdca-231">In hello **Last Name** textbox, type hello last name like Simon.</span></span>
    
    <span data-ttu-id="bbdca-232">c.</span><span class="sxs-lookup"><span data-stu-id="bbdca-232">c.</span></span> <span data-ttu-id="bbdca-233">In hello **Username** casella di testo, digitare il nome utente hello come Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbdca-233">In hello **Username** textbox, type hello user name like Britta Simon.</span></span>

    <span data-ttu-id="bbdca-234">d.</span><span class="sxs-lookup"><span data-stu-id="bbdca-234">d.</span></span> <span data-ttu-id="bbdca-235">In hello **Password** casella di testo, digitare la password di Britta Simon hello.</span><span class="sxs-lookup"><span data-stu-id="bbdca-235">In hello **Password** textbox, type hello password of Britta Simon.</span></span>

    <span data-ttu-id="bbdca-236">e.</span><span class="sxs-lookup"><span data-stu-id="bbdca-236">e.</span></span> <span data-ttu-id="bbdca-237">In hello **Conferma Password** casella di testo, hello tipo stessa password.</span><span class="sxs-lookup"><span data-stu-id="bbdca-237">In hello **Confirm Password** textbox, type hello same password.</span></span>
    
    <span data-ttu-id="bbdca-238">f.</span><span class="sxs-lookup"><span data-stu-id="bbdca-238">f.</span></span> <span data-ttu-id="bbdca-239">Rendere la password **attiva**.</span><span class="sxs-lookup"><span data-stu-id="bbdca-239">Make it as **ACTIVE**.</span></span>   

6. <span data-ttu-id="bbdca-240">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="bbdca-240">Click **"Save."**</span></span>
 
### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="bbdca-241">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbdca-241">Assign hello Azure AD test user</span></span>

<span data-ttu-id="bbdca-242">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooAbsorb LMS.</span><span class="sxs-lookup"><span data-stu-id="bbdca-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAbsorb LMS.</span></span>

![Assegnazione del ruolo utente hello][200]

<span data-ttu-id="bbdca-244">**tooassign Britta Simon tooAbsorb LMS, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bbdca-244">**tooassign Britta Simon tooAbsorb LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbdca-245">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="bbdca-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="bbdca-247">Nell'elenco di applicazioni hello, selezionare **assorbire LMS**.</span><span class="sxs-lookup"><span data-stu-id="bbdca-247">In hello applications list, select **Absorb LMS**.</span></span>

    ![Hello assorbire LMS collegamento nell'elenco delle applicazioni hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. <span data-ttu-id="bbdca-249">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="bbdca-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202] 

4. <span data-ttu-id="bbdca-251">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="bbdca-251">Click **Add** button.</span></span> <span data-ttu-id="bbdca-252">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="bbdca-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="bbdca-254">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="bbdca-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bbdca-255">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="bbdca-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bbdca-256">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="bbdca-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bbdca-257">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bbdca-257">Test single sign-on</span></span>

<span data-ttu-id="bbdca-258">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="bbdca-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bbdca-259">Fare clic su hello assorbire LMS riquadro in hello Pannello di accesso, si otterranno applicazione assorbire LMS tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="bbdca-259">Click hello Absorb LMS tile in hello Access Panel, you will get automatically signed-on tooyour Absorb LMS application.</span></span> <span data-ttu-id="bbdca-260">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="bbdca-260">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bbdca-261">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="bbdca-261">Additional resources</span></span>

* [<span data-ttu-id="bbdca-262">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbdca-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bbdca-263">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbdca-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

