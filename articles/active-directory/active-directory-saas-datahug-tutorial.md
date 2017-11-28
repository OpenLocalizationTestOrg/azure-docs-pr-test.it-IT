---
title: 'Esercitazione: integrazione di Azure Active Directory con Datahug | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Datahug.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: 79ccb939c7a19720bcf696af141f747db00c8a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a><span data-ttu-id="171a6-103">Esercitazione: Integrazione di Azure Active Directory con Datahug</span><span class="sxs-lookup"><span data-stu-id="171a6-103">Tutorial: Azure Active Directory integration with Datahug</span></span>

<span data-ttu-id="171a6-104">In questa esercitazione, è illustrato come toointegrate Datahug con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="171a6-104">In this tutorial, you learn how toointegrate Datahug with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="171a6-105">Integrazione Datahug con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="171a6-105">Integrating Datahug with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="171a6-106">È possibile controllare in Azure AD che ha accesso tooDatahug</span><span class="sxs-lookup"><span data-stu-id="171a6-106">You can control in Azure AD who has access tooDatahug</span></span>
- <span data-ttu-id="171a6-107">È possibile abilitare l'utenti tooautomatically get connesso tooDatahug (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="171a6-107">You can enable your users tooautomatically get signed-on tooDatahug (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="171a6-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="171a6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="171a6-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere.</span><span class="sxs-lookup"><span data-stu-id="171a6-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="171a6-110">[Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="171a6-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="171a6-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="171a6-111">Prerequisites</span></span>

<span data-ttu-id="171a6-112">integrazione di Azure AD con Datahug tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="171a6-112">tooconfigure Azure AD integration with Datahug, you need hello following items:</span></span>

- <span data-ttu-id="171a6-113">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="171a6-113">An Azure AD subscription</span></span>
- <span data-ttu-id="171a6-114">Sottoscrizione di Datahug abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="171a6-114">A Datahug single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="171a6-115">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="171a6-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="171a6-116">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="171a6-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="171a6-117">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="171a6-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="171a6-118">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="171a6-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="171a6-119">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="171a6-119">Scenario description</span></span>
<span data-ttu-id="171a6-120">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="171a6-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="171a6-121">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="171a6-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="171a6-122">Aggiunta di Datahug dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="171a6-122">Adding Datahug from hello gallery</span></span>
2. <span data-ttu-id="171a6-123">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="171a6-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-datahug-from-hello-gallery"></a><span data-ttu-id="171a6-124">Aggiunta di Datahug dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="171a6-124">Adding Datahug from hello gallery</span></span>
<span data-ttu-id="171a6-125">integrazione hello tooconfigure di Datahug in Azure AD, è necessario tooadd Datahug dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="171a6-125">tooconfigure hello integration of Datahug into Azure AD, you need tooadd Datahug from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="171a6-126">**tooadd Datahug dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="171a6-126">**tooadd Datahug from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="171a6-127">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="171a6-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="171a6-129">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="171a6-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="171a6-130">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="171a6-130">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="171a6-132">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="171a6-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="171a6-134">Nella casella di ricerca hello, digitare **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="171a6-134">In hello search box, type **Datahug**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. <span data-ttu-id="171a6-136">Nel riquadro dei risultati hello, selezionare **Datahug**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="171a6-136">In hello results panel, select **Datahug**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="171a6-138">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="171a6-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="171a6-139">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Datahug in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="171a6-139">In this section, you configure and test Azure AD single sign-on with Datahug based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="171a6-140">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Datahug è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="171a6-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Datahug is tooa user in Azure AD.</span></span> <span data-ttu-id="171a6-141">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Datahug deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="171a6-141">In other words, a link relationship between an Azure AD user and hello related user in Datahug needs toobe established.</span></span>

<span data-ttu-id="171a6-142">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Datahug.</span><span class="sxs-lookup"><span data-stu-id="171a6-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Datahug.</span></span>

<span data-ttu-id="171a6-143">tooconfigure e prova AD Azure single sign-on con Datahug, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="171a6-143">tooconfigure and test Azure AD single sign-on with Datahug, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="171a6-144">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="171a6-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="171a6-145">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="171a6-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="171a6-146">**[Creazione di un utente test Datahug](#creating-a-datahug-test-user)**  -toohave un equivalente di Britta Simon in Datahug che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="171a6-146">**[Creating a Datahug test user](#creating-a-datahug-test-user)** - toohave a counterpart of Britta Simon in Datahug that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="171a6-147">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="171a6-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="171a6-148">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="171a6-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="171a6-149">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="171a6-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="171a6-150">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Datahug.</span><span class="sxs-lookup"><span data-stu-id="171a6-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Datahug application.</span></span>

<span data-ttu-id="171a6-151">**Azure AD tooconfigure single sign-on con Datahug, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="171a6-151">**tooconfigure Azure AD single sign-on with Datahug, perform hello following steps:**</span></span>

1. <span data-ttu-id="171a6-152">Nel portale di Azure su hello hello **Datahug** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="171a6-152">In hello Azure portal, on hello **Datahug** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="171a6-154">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="171a6-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. <span data-ttu-id="171a6-156">In hello **Datahug dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="171a6-156">On hello **Datahug Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    <span data-ttu-id="171a6-158">a.</span><span class="sxs-lookup"><span data-stu-id="171a6-158">a.</span></span> <span data-ttu-id="171a6-159">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://apps.datahug.com/identity/<uniqueID>`</span><span class="sxs-lookup"><span data-stu-id="171a6-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://apps.datahug.com/identity/<uniqueID>`</span></span>

    <span data-ttu-id="171a6-160">b.</span><span class="sxs-lookup"><span data-stu-id="171a6-160">b.</span></span> <span data-ttu-id="171a6-161">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://apps.datahug.com/identity/<uniqueID>/acs`</span><span class="sxs-lookup"><span data-stu-id="171a6-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://apps.datahug.com/identity/<uniqueID>/acs`</span></span>

4. <span data-ttu-id="171a6-162">Selezionare **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="171a6-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="171a6-163">Se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="171a6-163">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    <span data-ttu-id="171a6-165">In hello **Sign-on URL** casella di testo, digitare un URL come:`https://apps.datahug.com/`</span><span class="sxs-lookup"><span data-stu-id="171a6-165">In hello **Sign-on URL** textbox, type a URL as: `https://apps.datahug.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="171a6-166">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="171a6-166">These values are not hello real.</span></span> <span data-ttu-id="171a6-167">Aggiornare questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="171a6-167">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="171a6-168">In questo caso, è consigliabile si toouse hello valore univoco della stringa nell'identificatore hello e l'URL di risposta.</span><span class="sxs-lookup"><span data-stu-id="171a6-168">Here we suggest you toouse hello unique value of string in hello Identifier and Reply URL.</span></span> <span data-ttu-id="171a6-169">Contatto [team di supporto Datahug Client](http://datahug.com/about/contact-us/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="171a6-169">Contact [Datahug Client support team](http://datahug.com/about/contact-us/) tooget these values.</span></span> 

5. <span data-ttu-id="171a6-170">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="171a6-170">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  <span data-ttu-id="171a6-172">Controllare **"Mostra avanzate impostazioni firma del certificato"** ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="171a6-172">Check **“Show advanced certificate signing settings”** and perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    <span data-ttu-id="171a6-174">a.</span><span class="sxs-lookup"><span data-stu-id="171a6-174">a.</span></span> <span data-ttu-id="171a6-175">In **Opzione di firma**, selezionare **Firma asserzione SAML**.</span><span class="sxs-lookup"><span data-stu-id="171a6-175">In **Signing Option**, select **Sign SAML assertion**.</span></span>
    
    <span data-ttu-id="171a6-176">b.</span><span class="sxs-lookup"><span data-stu-id="171a6-176">b.</span></span> <span data-ttu-id="171a6-177">In **Algoritmo di firma**, selezionare **SHA1**.</span><span class="sxs-lookup"><span data-stu-id="171a6-177">In **Signing algorithm**, select **SHA1**.</span></span>
 
7. <span data-ttu-id="171a6-178">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="171a6-178">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="171a6-180">In hello **Datahug configurazione** fare clic su **configurare Datahug** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="171a6-180">On hello **Datahug Configuration** section, click **Configure Datahug** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="171a6-181">Hello copia **ID entità SAML** e **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="171a6-181">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. <span data-ttu-id="171a6-183">tooconfigure single sign-on sul **Datahug** lato, è necessario hello toosend scaricato **Metadata XML**, **ID entità SAML** e **servizio SAML Single Sign-On URL** troppo[Datahug supporto](http://datahug.com/about/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="171a6-183">tooconfigure single sign-on on **Datahug** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** too[Datahug support](http://datahug.com/about/contact-us/).</span></span> <span data-ttu-id="171a6-184">Impostano l'applicazione di hello toohave connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="171a6-184">They set this application up toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="171a6-185">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="171a6-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="171a6-186">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="171a6-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="171a6-187">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="171a6-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="171a6-188">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="171a6-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="171a6-189">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="171a6-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="171a6-191">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="171a6-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="171a6-192">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="171a6-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="171a6-194">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="171a6-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="171a6-196">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="171a6-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="171a6-198">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="171a6-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="171a6-200">a.</span><span class="sxs-lookup"><span data-stu-id="171a6-200">a.</span></span> <span data-ttu-id="171a6-201">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="171a6-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="171a6-202">b.</span><span class="sxs-lookup"><span data-stu-id="171a6-202">b.</span></span> <span data-ttu-id="171a6-203">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="171a6-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="171a6-204">c.</span><span class="sxs-lookup"><span data-stu-id="171a6-204">c.</span></span> <span data-ttu-id="171a6-205">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="171a6-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="171a6-206">d.</span><span class="sxs-lookup"><span data-stu-id="171a6-206">d.</span></span> <span data-ttu-id="171a6-207">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="171a6-207">Click **Create**.</span></span>
 
### <a name="creating-a-datahug-test-user"></a><span data-ttu-id="171a6-208">Creazione di un utente test di Datahug</span><span class="sxs-lookup"><span data-stu-id="171a6-208">Creating a Datahug test user</span></span>

<span data-ttu-id="171a6-209">toolog agli utenti di Azure AD tooenable in tooDatahug, è necessario eseguirne il provisioning in Datahug.</span><span class="sxs-lookup"><span data-stu-id="171a6-209">tooenable Azure AD users toolog in tooDatahug, they must be provisioned into Datahug.</span></span>  
<span data-ttu-id="171a6-210">In Datahug il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="171a6-210">When Datahug, provisioning is a manual task.</span></span>

<span data-ttu-id="171a6-211">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="171a6-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="171a6-212">Accedi tooyour sito della società Datahug come amministratore.</span><span class="sxs-lookup"><span data-stu-id="171a6-212">Log in tooyour Datahug company site as an administrator.</span></span>

2. <span data-ttu-id="171a6-213">Passare il mouse su hello **ruota dentata** nell'angolo superiore destro di hello e fare clic su **impostazioni**</span><span class="sxs-lookup"><span data-stu-id="171a6-213">Hover over hello **cog** in hello top right-hand corner and click **Settings**</span></span>
   
   ![Aggiungere un dipendente](./media/active-directory-saas-datahug-tutorial/1.png)

3. <span data-ttu-id="171a6-215">Scegliere **persone** e fare clic su hello **Aggiungi utenti** scheda</span><span class="sxs-lookup"><span data-stu-id="171a6-215">Choose **People** and click hello **Add Users** tab</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-datahug-tutorial/2.png)

4. <span data-ttu-id="171a6-217">Tipo messaggio di posta elettronica hello di persona hello desideri toocreate un account per e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="171a6-217">Type hello email of hello person you would like toocreate an account for and click **Add**.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > <span data-ttu-id="171a6-219">È possibile inviare toouser di posta elettronica di registrazione selezionando **Invia messaggio di benvenuto** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="171a6-219">You can send registration mail toouser by selecting **Send welcome email** checkbox.</span></span>  
    > <span data-ttu-id="171a6-220">Se si sta creando un account di Salesforce non in grado di inviare il messaggio di benvenuto hello.</span><span class="sxs-lookup"><span data-stu-id="171a6-220">If you are creating an account for Salesforce do not send hello welcome email.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="171a6-221">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="171a6-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="171a6-222">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooDatahug.</span><span class="sxs-lookup"><span data-stu-id="171a6-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDatahug.</span></span>

![Assegna utente][200] 

<span data-ttu-id="171a6-224">**tooassign Britta Simon tooDatahug, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="171a6-224">**tooassign Britta Simon tooDatahug, perform hello following steps:**</span></span>

1. <span data-ttu-id="171a6-225">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="171a6-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="171a6-227">Nell'elenco di applicazioni hello, selezionare **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="171a6-227">In hello applications list, select **Datahug**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. <span data-ttu-id="171a6-229">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="171a6-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="171a6-231">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="171a6-231">Click **Add** button.</span></span> <span data-ttu-id="171a6-232">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="171a6-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="171a6-234">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="171a6-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="171a6-235">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="171a6-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="171a6-236">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="171a6-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="171a6-237">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="171a6-237">Testing single sign-on</span></span>

<span data-ttu-id="171a6-238">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="171a6-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="171a6-239">Quando si fa clic su riquadro Datahug hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Datahug applicazione.</span><span class="sxs-lookup"><span data-stu-id="171a6-239">When you click hello Datahug tile in hello Access Panel, you should get automatically signed-on tooyour Datahug application.</span></span> <span data-ttu-id="171a6-240">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="171a6-240">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="171a6-241">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="171a6-241">Additional resources</span></span>

* [<span data-ttu-id="171a6-242">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="171a6-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="171a6-243">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="171a6-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png

