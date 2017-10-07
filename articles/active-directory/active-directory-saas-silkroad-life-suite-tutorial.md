---
title: 'Esercitazione: Integrazione di Azure Active Directory con SilkRoad Life Suite | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e SilkRoad vita Suite.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 07367282ab42b7332f166d64743b4b447aec4935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="3a7cf-103">Esercitazione: Integrazione di Azure Active Directory con SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="3a7cf-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="3a7cf-104">obiettivo di Hello di questa esercitazione è tooshow è come toointegrate SilkRoad vita Suite con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3a7cf-104">hello objective of this tutorial is tooshow you how toointegrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="3a7cf-105">Integrazione SilkRoad vita Suite con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="3a7cf-105">Integrating SilkRoad Life Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="3a7cf-106">È possibile controllare in Azure AD che ha accesso tooSilkRoad vita Suite</span><span class="sxs-lookup"><span data-stu-id="3a7cf-106">You can control in Azure AD who has access tooSilkRoad Life Suite</span></span> 
* <span data-ttu-id="3a7cf-107">È possibile abilitare l'utenti tooautomatically get connesso tooSilkRoad vita Suite single sign-on (SSO) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a7cf-107">You can enable your users tooautomatically get signed-on tooSilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="3a7cf-108">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3a7cf-108">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a7cf-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3a7cf-109">Prerequisites</span></span>
<span data-ttu-id="3a7cf-110">integrazione di Azure AD con SilkRoad vita Suite tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="3a7cf-110">tooconfigure Azure AD integration with SilkRoad Life Suite, you need hello following items:</span></span>

* <span data-ttu-id="3a7cf-111">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-111">An Azure AD subscription</span></span>
* <span data-ttu-id="3a7cf-112">Sottoscrizione di SilkRoad Life Suite abilitata per l'accesso SSO</span><span class="sxs-lookup"><span data-stu-id="3a7cf-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="3a7cf-113">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-113">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="3a7cf-114">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="3a7cf-114">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="3a7cf-115">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="3a7cf-116">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3a7cf-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="3a7cf-117">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="3a7cf-117">Scenario Description</span></span>
<span data-ttu-id="3a7cf-118">obiettivo di Hello di questa esercitazione è tooenable si tootest SSO AD Azure in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-118">hello objective of this tutorial is tooenable you tootest Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="3a7cf-119">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="3a7cf-119">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3a7cf-120">Aggiunta gruppo vita SilkRoad dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="3a7cf-120">Adding SilkRoad Life Suite from hello gallery</span></span> 
2. <span data-ttu-id="3a7cf-121">Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a7cf-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-hello-gallery"></a><span data-ttu-id="3a7cf-122">Aggiungere il gruppo di vita SilkRoad dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="3a7cf-122">Add SilkRoad Life Suite from hello gallery</span></span>
<span data-ttu-id="3a7cf-123">integrazione hello tooconfigure di SilkRoad vita Suite in Azure AD, è necessario tooadd SilkRoad vita gruppo dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-123">tooconfigure hello integration of SilkRoad Life Suite into Azure AD, you need tooadd SilkRoad Life Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3a7cf-124">**tooadd SilkRoad vita Suite dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3a7cf-124">**tooadd SilkRoad Life Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a7cf-125">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-125">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="3a7cf-127">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-127">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="3a7cf-128">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-128">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Applicazioni][2]

4. <span data-ttu-id="3a7cf-130">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-130">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Applicazioni][3]

5. <span data-ttu-id="3a7cf-132">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-132">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Applicazioni][4]

6. <span data-ttu-id="3a7cf-134">Nella casella di ricerca hello, digitare **SilkRoad vita Suite**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-134">In hello search box, type **SilkRoad Life Suite**.</span></span>
   
    ![Applicazioni][5]

7. <span data-ttu-id="3a7cf-136">Nel riquadro risultati hello selezionare **SilkRoad vita Suite**, quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-136">In hello results pane, select **SilkRoad Life Suite**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Applicazioni][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3a7cf-138">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a7cf-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="3a7cf-139">obiettivo di Hello di questa sezione è tooshow come tooconfigure e SSO AD Azure con SilkRoad vita Suite di test basato su un utente di test denominato "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3a7cf-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3a7cf-140">Per toowork SSO, Azure AD deve tooknow è quale utente controparte hello utente tooan SilkRoad vita Suite in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-140">For SSO toowork, Azure AD needs tooknow what hello counterpart user in SilkRoad Life Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="3a7cf-141">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello SilkRoad vita Suite deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-141">In other words, a link relationship between an Azure AD user and hello related user in SilkRoad Life Suite needs toobe established.</span></span>

<span data-ttu-id="3a7cf-142">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** SilkRoad vita Suite.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="3a7cf-143">tooconfigure e prova AD Azure single sign-on con SilkRoad vita Suite, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="3a7cf-143">tooconfigure and test Azure AD single sign-on with SilkRoad Life Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3a7cf-144">**[Configurazione di Azure single sign-on AD](#configuring-azure-ad-single-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3a7cf-145">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3a7cf-146">**[Creazione di un utente test SilkRoad vita Suite](#creating-a-silkroad-life-suite-test-user)**  -toohave un equivalente di Britta Simon SilkRoad vita Suite rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - toohave a counterpart of Britta Simon in SilkRoad Life Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="3a7cf-147">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3a7cf-148">**[Test di accesso single sign-on](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-148">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3a7cf-149">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a7cf-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="3a7cf-150">obiettivo di Hello di questa sezione è tooenable SSO AD Azure nel portale di Azure classico hello e tooconfigure SSO nell'applicazione SilkRoad vita Suite.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-150">hello objective of this section is tooenable Azure AD SSO in hello Azure classic portal and tooconfigure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="3a7cf-151">**tooconfigure AD Azure single sign-on con SilkRoad vita Suite eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3a7cf-151">**tooconfigure Azure AD single sign-on with SilkRoad Life Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a7cf-152">Sito dell'azienda SilkRoad tooyour accesso come amministratore.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-152">Sign-on tooyour SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="3a7cf-153">tooobtain accesso toohello applicazione SilkRoad vita Suite autenticazione per configurare la federazione con Microsoft Azure AD, contattare il supporto SilkRoad o il rappresentante SilkRoad servizi.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-153">tooobtain access toohello SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="3a7cf-154">Andare troppo**Provider di servizi**, quindi fare clic su **federazione dettagli**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-154">Go too**Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Single Sign-On di Microsoft Azure AD][10] 

3. <span data-ttu-id="3a7cf-156">Fare clic su **scaricare i metadati della federazione**e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-156">Click **Download Federation Metadata**, and then save hello metadata file on your computer.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][11] 

4. <span data-ttu-id="3a7cf-158">Nel portale di Azure classico, in hello hello **SilkRoad vita Suite** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On**  finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-158">In hello Azure classic portal, on hello **SilkRoad Life Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configura accesso Single Sign-On][6] 

5. <span data-ttu-id="3a7cf-160">In hello **come si sarebbe ad esempio utenti toosign su tooSilkRoad vita Suite** selezionare **Azure Single Sign-On AD**e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-160">On hello **How would you like users toosign on tooSilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][7] 

6. <span data-ttu-id="3a7cf-162">In hello **Configura impostazioni App** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3a7cf-162">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][8]   
 1. <span data-ttu-id="3a7cf-164">In hello **URL di accesso** casella di testo, digitare l'URL hello utilizzato dal sito SilkRoad vita Suite tooyour toosign-on agli utenti (ad esempio: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span><span class="sxs-lookup"><span data-stu-id="3a7cf-164">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="3a7cf-165">Aprire hello scaricato **Silkroad** file di metadati.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-165">Open hello downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="3a7cf-166">Individuare hello **AssertionConsumerService** tag e quindi hello copia **percorso** attributo.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-166">Locate hello **AssertionConsumerService** tag, and then copy hello **Location** attribute.</span></span>         
   
    ![Single Sign-On di Microsoft Azure AD][21] 
 4. <span data-ttu-id="3a7cf-168">Incollare il valore di hello hello **URL di risposta** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-168">Paste hello value into hello **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="3a7cf-169">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-169">Click **Next**.</span></span>

6. <span data-ttu-id="3a7cf-170">In hello **Configura accesso single sign-on SilkRoad vita Suite** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3a7cf-170">On hello **Configure single sign-on at SilkRoad Life Suite** page, perform hello following steps:</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][9]  
 1. <span data-ttu-id="3a7cf-172">Fare clic su Download certificate e quindi salvare il file hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-172">Click Download certificate, and then save hello file on your computer.</span></span>  
 2. <span data-ttu-id="3a7cf-173">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-173">Click **Next**.</span></span>

7. <span data-ttu-id="3a7cf-174">Nell'applicazione **SilkRoad**, fare clic su **Authentication Sources** (Origini autenticazione).</span><span class="sxs-lookup"><span data-stu-id="3a7cf-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![Single Sign-On di Microsoft Azure AD][12] 

8. <span data-ttu-id="3a7cf-176">Fare clic su **Add Authentication Source**(Aggiungi origine autenticazione).</span><span class="sxs-lookup"><span data-stu-id="3a7cf-176">Click **Add Authentication Source**.</span></span> 
   
    ![Single Sign-On di Microsoft Azure AD][13] 

9. <span data-ttu-id="3a7cf-178">In hello **Aggiungi origine autenticazione** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3a7cf-178">In hello **Add Authentication Source** section, perform hello following steps:</span></span> 
   
    ![Single Sign-On di Microsoft Azure AD][14]  
 1. <span data-ttu-id="3a7cf-180">In **opzione 2 - File di metadati**, fare clic su **Sfoglia** hello tooupload scaricato i file di metadati.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-180">Under **Option 2 - Metadata File**, click **Browse** tooupload hello downloaded metadata file.</span></span>  
 2. <span data-ttu-id="3a7cf-181">Fare clic su **Create Identity Provider using File Data**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="3a7cf-182">In hello **origini di autenticazione** fare clic su **modifica**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-182">In hello **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Single Sign-On di Microsoft Azure AD][15] 

11. <span data-ttu-id="3a7cf-184">In hello **Modifica autenticazione origine** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3a7cf-184">On hello **Edit Authentication Source** dialog, perform hello following steps:</span></span> 
    
     ![Single Sign-On di Microsoft Azure AD][16] 
 1. <span data-ttu-id="3a7cf-186">In **Enabled** (Attivo) selezionare **Yes** (Sì).</span><span class="sxs-lookup"><span data-stu-id="3a7cf-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="3a7cf-187">In hello **descrizione IdP** casella di testo, digitare una descrizione per la configurazione (ad esempio: *SSO AD Azure*).</span><span class="sxs-lookup"><span data-stu-id="3a7cf-187">In hello **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="3a7cf-188">In hello **nome IdP** casella di testo, digitare un nome di configurazione tooyour specifico (ad esempio: *Azure SP*).</span><span class="sxs-lookup"><span data-stu-id="3a7cf-188">In hello **IdP Name** textbox, type a name that is specific tooyour configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="3a7cf-189">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-189">Click **Save**.</span></span>

12. <span data-ttu-id="3a7cf-190">Disabilitare tutte le altre origini di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-190">Disable all other authentication sources.</span></span> 
    
     ![Single Sign-On di Microsoft Azure AD][17]

13. <span data-ttu-id="3a7cf-192">Nel portale di Azure classico, in hello hello **Single sign-on conferma** pagina, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-192">In hello Azure classic portal, on hello **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![Single Sign-On di Microsoft Azure AD][18]

14. <span data-ttu-id="3a7cf-194">In hello **Single sign-on conferma** pagina, fare clic su **completa**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![Single Sign-On di Microsoft Azure AD][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3a7cf-196">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a7cf-196">Create an Azure AD test user</span></span>
<span data-ttu-id="3a7cf-197">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure classico chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][20]

<span data-ttu-id="3a7cf-199">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3a7cf-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a7cf-200">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-200">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="3a7cf-202">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-202">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="3a7cf-203">Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-203">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3a7cf-205">hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-205">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="3a7cf-207">In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3a7cf-207">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="3a7cf-209">In Tipo di utente selezionare Nuovo utente nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="3a7cf-210">In nome utente hello **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-210">In hello User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="3a7cf-211">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-211">Click **Next**.</span></span>

6. <span data-ttu-id="3a7cf-212">In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3a7cf-212">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="3a7cf-214">In hello **nome** casella tipo **Laura**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-214">In hello **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="3a7cf-215">In hello **cognome** casella di testo, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-215">In hello **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="3a7cf-216">In hello **nome visualizzato** casella tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-216">In hello **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="3a7cf-217">In hello **ruolo** elenco, selezionare **utente**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-217">In hello **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="3a7cf-218">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-218">Click **Next**.</span></span>

7. <span data-ttu-id="3a7cf-219">In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-219">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="3a7cf-221">In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3a7cf-221">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="3a7cf-223">Annotare il valore di hello di hello **nuova Password**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-223">Write down hello value of hello **New Password**.</span></span> 
 2. <span data-ttu-id="3a7cf-224">Fare clic su **Complete**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="3a7cf-225">Creare un utente test di SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="3a7cf-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="3a7cf-226">obiettivo di Hello di questa sezione è un utente denominato Britta Simon SilkRoad vita Suite toocreate.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-226">hello objective of this section is toocreate a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="3a7cf-227">Laura deve avere un ID di SSO (talvolta tooas un *AuthParam*) corrispondente di Laura **emailaddress** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-227">Britta's must have an SSO ID (sometimes referred tooas an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="3a7cf-228">**un utente denominato Britta Simon SilkRoad vita Suite, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3a7cf-228">**toocreate a user called Britta Simon in SilkRoad Life Suite, perform hello following steps:**</span></span>

- <span data-ttu-id="3a7cf-229">Chiedere a un utente che ha il toocreate team di supporto SilkRoad vita Suite **ID SSO** hello attributo lo stesso valore hello **emailaddress** di Britta Simon in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-229">Ask your SilkRoad Life Suite support team toocreate a user that has as **SSO ID** attribute hello same value as hello **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="3a7cf-230">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a7cf-230">Assign hello Azure AD test user</span></span>
<span data-ttu-id="3a7cf-231">obiettivo Hello di questa sezione è tooenable Britta Simon toouse SSO Azure concedendo proprio tooSilkRoad accesso vita Suite.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-231">hello objective of this section is tooenable Britta Simon toouse Azure SSO by granting her access tooSilkRoad Life Suite.</span></span>

![Assegna utente][200] 

<span data-ttu-id="3a7cf-233">**tooassign Britta Simon tooSilkRoad vita Suite, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3a7cf-233">**tooassign Britta Simon tooSilkRoad Life Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a7cf-234">In hello Azure portale classico, visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-234">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Assegna utente][201] 

2. <span data-ttu-id="3a7cf-236">Nell'elenco di applicazioni hello, selezionare **SilkRoad vita Suite**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-236">In hello applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![Assegna utente][202] 

3. <span data-ttu-id="3a7cf-238">Scegliere dal menu hello in primo piano hello **utenti**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-238">In hello menu on hello top, click **Users**.</span></span>
   
    ![Assegna utente][203] 

4. <span data-ttu-id="3a7cf-240">Nell'elenco di utenti hello, selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-240">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="3a7cf-241">Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-241">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Assegna utente][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="3a7cf-243">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3a7cf-243">Test single sign-on</span></span>
<span data-ttu-id="3a7cf-244">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-244">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="3a7cf-245">Quando si fa clic su riquadro SilkRoad vita Suite hello in hello Pannello di accesso, è necessario ottenere un'applicazione SilkRoad vita Suite tooyour firmato in automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3a7cf-245">When you click hello SilkRoad Life Suite tile in hello Access Panel, you should get automatically signed-on tooyour SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3a7cf-246">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="3a7cf-246">Additional Resources</span></span>
* [<span data-ttu-id="3a7cf-247">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a7cf-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3a7cf-248">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a7cf-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





