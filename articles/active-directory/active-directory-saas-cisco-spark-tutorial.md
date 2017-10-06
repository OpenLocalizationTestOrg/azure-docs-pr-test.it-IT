---
title: 'Esercitazione: Integrazione di Azure Active Directory con Cisco Spark | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Spark Cisco.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 386c4fd816095e1c61de01dd1dee1bbd00311a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="748cb-103">Esercitazione: Integrazione di Azure Active Directory con Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="748cb-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>

<span data-ttu-id="748cb-104">In questa esercitazione, è illustrato come toointegrate Cisco nascita con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="748cb-104">In this tutorial, you learn how toointegrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="748cb-105">L'integrazione di Cisco Spark in Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="748cb-105">Integrating Cisco Spark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="748cb-106">È possibile controllare in Azure AD che ha accesso tooCisco Spark</span><span class="sxs-lookup"><span data-stu-id="748cb-106">You can control in Azure AD who has access tooCisco Spark</span></span>
- <span data-ttu-id="748cb-107">È possibile abilitare l'utenti tooautomatically get connesso tooCisco Spark (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="748cb-107">You can enable your users tooautomatically get signed-on tooCisco Spark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="748cb-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="748cb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="748cb-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="748cb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="748cb-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="748cb-110">Prerequisites</span></span>

<span data-ttu-id="748cb-111">integrazione di Azure AD con Cisco Spark tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="748cb-111">tooconfigure Azure AD integration with Cisco Spark, you need hello following items:</span></span>

- <span data-ttu-id="748cb-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="748cb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="748cb-113">Sottoscrizione di Cisco Spark abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="748cb-113">A Cisco Spark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="748cb-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="748cb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="748cb-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="748cb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="748cb-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="748cb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="748cb-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="748cb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="748cb-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="748cb-118">Scenario description</span></span>
<span data-ttu-id="748cb-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="748cb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="748cb-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="748cb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="748cb-121">Aggiunta di Cisco Spark dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="748cb-121">Adding Cisco Spark from hello gallery</span></span>
2. <span data-ttu-id="748cb-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="748cb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-spark-from-hello-gallery"></a><span data-ttu-id="748cb-123">Aggiunta di Cisco Spark dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="748cb-123">Adding Cisco Spark from hello gallery</span></span>
<span data-ttu-id="748cb-124">integrazione hello tooconfigure di Cisco Spark in Azure AD, è necessario tooadd Cisco Spark dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="748cb-124">tooconfigure hello integration of Cisco Spark into Azure AD, you need tooadd Cisco Spark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="748cb-125">**tooadd Spark Cisco dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="748cb-125">**tooadd Cisco Spark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="748cb-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="748cb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="748cb-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="748cb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="748cb-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="748cb-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="748cb-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="748cb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="748cb-133">Nella casella di ricerca hello, digitare **Spark Cisco**.</span><span class="sxs-lookup"><span data-stu-id="748cb-133">In hello search box, type **Cisco Spark**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. <span data-ttu-id="748cb-135">Nel riquadro dei risultati hello, selezionare **Spark Cisco**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="748cb-135">In hello results panel, select **Cisco Spark**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="748cb-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="748cb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="748cb-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Cisco Spark mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="748cb-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="748cb-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Spark Cisco è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="748cb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cisco Spark is tooa user in Azure AD.</span></span> <span data-ttu-id="748cb-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Spark Cisco deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="748cb-140">In other words, a link relationship between an Azure AD user and hello related user in Cisco Spark needs toobe established.</span></span>

<span data-ttu-id="748cb-141">In Spark Cisco, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="748cb-141">In Cisco Spark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="748cb-142">tooconfigure e test Azure single sign-on AD con Cisco Spark, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="748cb-142">tooconfigure and test Azure AD single sign-on with Cisco Spark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="748cb-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="748cb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="748cb-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="748cb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="748cb-145">**[Creazione di un utente test Spark Cisco](#creating-a-cisco-spark-test-user)**  -toohave un equivalente di Britta Simon in Spark Cisco che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="748cb-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - toohave a counterpart of Britta Simon in Cisco Spark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="748cb-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="748cb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="748cb-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="748cb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="748cb-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="748cb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="748cb-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Spark Cisco.</span><span class="sxs-lookup"><span data-stu-id="748cb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="748cb-150">**Azure AD tooconfigure single sign-on con Cisco Spark, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="748cb-150">**tooconfigure Azure AD single sign-on with Cisco Spark, perform hello following steps:**</span></span>

1. <span data-ttu-id="748cb-151">Nel portale di Azure su hello hello **Spark Cisco** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="748cb-151">In hello Azure portal, on hello **Cisco Spark** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="748cb-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="748cb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. <span data-ttu-id="748cb-155">In hello **Cisco Spark dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="748cb-155">On hello **Cisco Spark Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    <span data-ttu-id="748cb-157">a.</span><span class="sxs-lookup"><span data-stu-id="748cb-157">a.</span></span> <span data-ttu-id="748cb-158">In hello **Sign-on URL** casella di testo, digitare un URL come:`https://web.ciscospark.com/#/signin`</span><span class="sxs-lookup"><span data-stu-id="748cb-158">In hello **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span></span>

    <span data-ttu-id="748cb-159">b.</span><span class="sxs-lookup"><span data-stu-id="748cb-159">b.</span></span> <span data-ttu-id="748cb-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://idbroker.webex.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="748cb-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://idbroker.webex.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="748cb-161">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="748cb-161">This value is not real.</span></span> <span data-ttu-id="748cb-162">Aggiorna il valore con hello identificatore effettivo.</span><span class="sxs-lookup"><span data-stu-id="748cb-162">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="748cb-163">Contatto [team di supporto Client di Spark Cisco](https://support.ciscospark.com/) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="748cb-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) tooget this value.</span></span> 
 
4. <span data-ttu-id="748cb-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="748cb-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. <span data-ttu-id="748cb-166">Applicazione di Spark Cisco prevede attributi specifici toocontain di hello asserzioni SAML.</span><span class="sxs-lookup"><span data-stu-id="748cb-166">Cisco Spark application expects hello SAML assertions toocontain specific attributes.</span></span> <span data-ttu-id="748cb-167">Configurare gli attributi per questa applicazione seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="748cb-167">Configure hello following attributes  for this application.</span></span> <span data-ttu-id="748cb-168">È possibile gestire i valori hello di questi attributi da hello **gli attributi utente** sezione nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="748cb-168">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="748cb-169">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="748cb-169">hello following screenshot shows an example for this.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. <span data-ttu-id="748cb-171">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nell'immagine di hello precedente ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="748cb-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="748cb-172">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="748cb-172">Attribute Name</span></span>  | <span data-ttu-id="748cb-173">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="748cb-173">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="748cb-174">uid</span><span class="sxs-lookup"><span data-stu-id="748cb-174">uid</span></span>    | <span data-ttu-id="748cb-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="748cb-175">user.userprincipalname</span></span> |   

    <span data-ttu-id="748cb-176">a.</span><span class="sxs-lookup"><span data-stu-id="748cb-176">a.</span></span> <span data-ttu-id="748cb-177">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="748cb-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="748cb-180">b.</span><span class="sxs-lookup"><span data-stu-id="748cb-180">b.</span></span> <span data-ttu-id="748cb-181">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="748cb-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="748cb-182">c.</span><span class="sxs-lookup"><span data-stu-id="748cb-182">c.</span></span> <span data-ttu-id="748cb-183">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="748cb-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="748cb-184">d.</span><span class="sxs-lookup"><span data-stu-id="748cb-184">d.</span></span> <span data-ttu-id="748cb-185">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="748cb-185">Click **Ok**.</span></span>

7. <span data-ttu-id="748cb-186">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="748cb-186">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="748cb-188">Accedi troppo[Cisco Cloud collaborazione gestione](https://admin.ciscospark.com/) con le credenziali di amministratore completo.</span><span class="sxs-lookup"><span data-stu-id="748cb-188">Sign in too[Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

9. <span data-ttu-id="748cb-189">Selezionare **impostazioni** in hello **autenticazione** fare clic su **modifica**.</span><span class="sxs-lookup"><span data-stu-id="748cb-189">Select **Settings** and under hello **Authentication** section, click **Modify**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. <span data-ttu-id="748cb-191">Selezionare **Integrate a 3rd-party identity provider. (Avanzate)**  e toohello andare nella schermata successiva.</span><span class="sxs-lookup"><span data-stu-id="748cb-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go toohello next screen.</span></span>

11. <span data-ttu-id="748cb-192">In hello **Import Idp Metadata** pagina entrambi trascinare e rilasciare file di metadati hello Azure AD nella pagina hello o utilizzare hello file browser opzione toolocate e caricare il file di metadati hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="748cb-192">On hello **Import Idp Metadata** page, either drag and drop hello Azure AD metadata file onto hello page or use hello file browser option toolocate and upload hello Azure AD metadata file.</span></span> <span data-ttu-id="748cb-193">Selezionare quindi **Require certificate signed by a certificate authority in Metadata (more secure)** (Richiedi certificato firmato da un'autorità di certificazione in metadati - più sicura) e fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="748cb-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. <span data-ttu-id="748cb-195">Selezionare **Test SSO Connection** (Test connessione SSO) e, quando viene aperta una nuova scheda del browser, eseguire l'autenticazione con Azure AD effettuando l'accesso.</span><span class="sxs-lookup"><span data-stu-id="748cb-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

13. <span data-ttu-id="748cb-196">Restituire toohello **Cisco Cloud collaborazione gestione** scheda del browser. Se hello è stata stabilita, selezionare **questa è stata stabilita. Enable Single Sign-On**  (Test riuscito. Abilita Single Sign-On), quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="748cb-196">Return toohello **Cisco Cloud Collaboration Management** browser tab. If hello test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="748cb-197">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="748cb-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="748cb-198">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="748cb-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="748cb-199">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="748cb-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="748cb-200">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="748cb-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="748cb-201">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="748cb-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="748cb-203">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="748cb-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="748cb-204">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="748cb-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="748cb-206">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="748cb-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="748cb-208">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="748cb-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="748cb-210">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="748cb-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="748cb-212">a.</span><span class="sxs-lookup"><span data-stu-id="748cb-212">a.</span></span> <span data-ttu-id="748cb-213">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="748cb-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="748cb-214">b.</span><span class="sxs-lookup"><span data-stu-id="748cb-214">b.</span></span> <span data-ttu-id="748cb-215">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="748cb-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="748cb-216">c.</span><span class="sxs-lookup"><span data-stu-id="748cb-216">c.</span></span> <span data-ttu-id="748cb-217">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="748cb-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="748cb-218">d.</span><span class="sxs-lookup"><span data-stu-id="748cb-218">d.</span></span> <span data-ttu-id="748cb-219">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="748cb-219">Click **Create**.</span></span>
 
### <a name="creating-a-cisco-spark-test-user"></a><span data-ttu-id="748cb-220">Creazione di un utente test di Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="748cb-220">Creating a Cisco Spark test user</span></span>

<span data-ttu-id="748cb-221">In questa sezione viene creato un utente di nome Britta Simon in Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="748cb-221">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="748cb-222">In questa sezione viene creato un utente di nome Britta Simon in Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="748cb-222">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="748cb-223">Passare toohello [Cisco Cloud collaborazione gestione](https://admin.ciscospark.com/) con le credenziali di amministratore completo.</span><span class="sxs-lookup"><span data-stu-id="748cb-223">Go toohello [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

2. <span data-ttu-id="748cb-224">Fare clic su **Users** (Utenti) e quindi su **Manage Users** (Gestisci utenti).</span><span class="sxs-lookup"><span data-stu-id="748cb-224">Click **Users** and then **Manage Users**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. <span data-ttu-id="748cb-226">In hello **Manage User** selezionare **agli utenti di modificare o aggiungere manualmente** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="748cb-226">In hello **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>

4. <span data-ttu-id="748cb-227">Selezionare **Names and Email address** (Nomi e indirizzi di posta elettronica).</span><span class="sxs-lookup"><span data-stu-id="748cb-227">Select **Names and Email address**.</span></span> <span data-ttu-id="748cb-228">Quindi, compilare hello casella di testo come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="748cb-228">Then, fill out hello textbox as follows:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    <span data-ttu-id="748cb-230">a.</span><span class="sxs-lookup"><span data-stu-id="748cb-230">a.</span></span> <span data-ttu-id="748cb-231">In hello **nome** casella tipo **Laura**.</span><span class="sxs-lookup"><span data-stu-id="748cb-231">In hello **First Name** textbox, type **Britta**.</span></span> 
    
    <span data-ttu-id="748cb-232">b.</span><span class="sxs-lookup"><span data-stu-id="748cb-232">b.</span></span> <span data-ttu-id="748cb-233">In hello **cognome** casella tipo **Simon**.</span><span class="sxs-lookup"><span data-stu-id="748cb-233">In hello **Last Name** textbox, type **Simon**.</span></span>
    
    <span data-ttu-id="748cb-234">c.</span><span class="sxs-lookup"><span data-stu-id="748cb-234">c.</span></span> <span data-ttu-id="748cb-235">In hello **indirizzo di posta elettronica** casella tipo  **britta.simon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="748cb-235">In hello **Email address** textbox, type **britta.simon@contoso.com**.</span></span>

5. <span data-ttu-id="748cb-236">Fare clic su hello segno tooadd Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="748cb-236">Click hello plus sign tooadd Britta Simon.</span></span> <span data-ttu-id="748cb-237">Quindi fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="748cb-237">Then, click **Next**.</span></span>

6. <span data-ttu-id="748cb-238">In hello **Aggiungi servizi per gli utenti** finestra, fare clic su **salvare** e quindi **fine**.</span><span class="sxs-lookup"><span data-stu-id="748cb-238">In hello **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="748cb-239">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="748cb-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="748cb-240">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooCisco Spark.</span><span class="sxs-lookup"><span data-stu-id="748cb-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCisco Spark.</span></span>

![Assegna utente][200] 

<span data-ttu-id="748cb-242">**tooassign Britta Simon tooCisco Spark, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="748cb-242">**tooassign Britta Simon tooCisco Spark, perform hello following steps:**</span></span>

1. <span data-ttu-id="748cb-243">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="748cb-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="748cb-245">Nell'elenco di applicazioni hello, selezionare **Spark Cisco**.</span><span class="sxs-lookup"><span data-stu-id="748cb-245">In hello applications list, select **Cisco Spark**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. <span data-ttu-id="748cb-247">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="748cb-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="748cb-249">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="748cb-249">Click **Add** button.</span></span> <span data-ttu-id="748cb-250">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="748cb-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="748cb-252">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="748cb-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="748cb-253">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="748cb-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="748cb-254">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="748cb-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="748cb-255">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="748cb-255">Testing single sign-on</span></span>

<span data-ttu-id="748cb-256">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="748cb-256">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="748cb-257">Quando si fa clic su riquadro Cisco Spark hello in hello Pannello di accesso, è necessario ottenere applicazione Spark Cisco tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="748cb-257">When you click hello Cisco Spark tile in hello Access Panel, you should get automatically signed-on tooyour Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="748cb-258">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="748cb-258">Additional resources</span></span>

* [<span data-ttu-id="748cb-259">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="748cb-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="748cb-260">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="748cb-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

