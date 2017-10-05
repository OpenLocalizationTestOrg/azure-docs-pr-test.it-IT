---
title: 'Esercitazione: Configurazione di LinkedIn Lookup per il provisioning utenti automatico con Azure Active Directory | Microsoft Docs'
description: Informazioni su come configurare Azure Active Directory per effettuare automaticamente il provisioning e il deprovisioning degli account utente in LinkedIn Lookup.
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 085a68cfe8f9e08b8722e8613994ee300a015776
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-linkedin-lookup-for-automatic-user-provisioning"></a><span data-ttu-id="0f379-103">Esercitazione: Configurazione di LinkedIn Lookup per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="0f379-103">Tutorial: Configuring LinkedIn Lookup for Automatic User Provisioning</span></span>


<span data-ttu-id="0f379-104">Questa esercitazione descrive le procedure da eseguire in LinkedIn Lookup e Azure AD per effettuare automaticamente il provisioning e il deprovisioning degli account utente da Azure AD a LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="0f379-104">The objective of this tutorial is to show you the steps you need to perform in LinkedIn Lookup and Azure AD to automatically provision and de-provision user accounts from Azure AD to LinkedIn Lookup.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0f379-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0f379-105">Prerequisites</span></span>

<span data-ttu-id="0f379-106">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="0f379-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="0f379-107">Tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f379-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="0f379-108">Tenant di LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="0f379-108">A LinkedIn Lookup tenant</span></span> 
*   <span data-ttu-id="0f379-109">Account amministratore in LinkedIn Lookup con accesso al centro account di LinkedIn</span><span class="sxs-lookup"><span data-stu-id="0f379-109">An administrator account in LinkedIn Lookup with access to the LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="0f379-110">Azure Active Directory si integra con LinkedIn Lookup usando il protocollo [SCIM](http://www.simplecloud.info/).</span><span class="sxs-lookup"><span data-stu-id="0f379-110">Azure Active Directory integrates with LinkedIn Lookup using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-linkedin-lookup"></a><span data-ttu-id="0f379-111">Assegnazione di utenti a LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="0f379-111">Assigning users to LinkedIn Lookup</span></span>

<span data-ttu-id="0f379-112">Per determinare gli utenti che dovranno ricevere l'accesso alle app selezionate, Azure Active Directory usa il concetto delle "assegnazioni".</span><span class="sxs-lookup"><span data-stu-id="0f379-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="0f379-113">Nel contesto del provisioning automatico degli account utente, verranno sincronizzati solo gli utenti e i gruppi che sono stati "assegnati" a un'applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f379-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="0f379-114">Prima di configurare e abilitare il servizio di provisioning, è necessario stabilire quali utenti e/o gruppi in Azure AD rappresentano gli utenti che devono accedere a LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="0f379-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to LinkedIn Lookup.</span></span> <span data-ttu-id="0f379-115">Dopo aver stabilito questo, è possibile assegnare tali utenti a LinkedIn Lookup seguendo le istruzioni riportate nell'articolo seguente:</span><span class="sxs-lookup"><span data-stu-id="0f379-115">Once decided, you can assign these users to LinkedIn Lookup by following the instructions here:</span></span>

[<span data-ttu-id="0f379-116">Assegnare un utente o gruppo a un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="0f379-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-linkedin-lookup"></a><span data-ttu-id="0f379-117">Suggerimenti importanti per l'assegnazione di utenti a LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="0f379-117">Important tips for assigning users to LinkedIn Lookup</span></span>

*   <span data-ttu-id="0f379-118">È consigliabile assegnare un singolo utente di Azure AD a LinkedIn Lookup per testare la configurazione del provisioning.</span><span class="sxs-lookup"><span data-stu-id="0f379-118">It is recommended that a single Azure AD user be assigned to LinkedIn Lookup to test the provisioning configuration.</span></span> <span data-ttu-id="0f379-119">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="0f379-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="0f379-120">Quando si assegna un utente a LinkedIn Lookup, è necessario selezionare il ruolo **Utente** nella finestra di dialogo di assegnazione.</span><span class="sxs-lookup"><span data-stu-id="0f379-120">When assigning a user to LinkedIn Lookup, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="0f379-121">Il ruolo "Default Access" (Accesso predefinito) non è applicabile per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="0f379-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-linkedin-lookup"></a><span data-ttu-id="0f379-122">Configurazione del provisioning utenti in LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="0f379-122">Configuring user provisioning to LinkedIn Lookup</span></span>

<span data-ttu-id="0f379-123">Questa sezione illustra la connessione di Azure AD all'API per il provisioning degli account utente SCIM di LinkedIn Lookup e la configurazione del servizio di provisioning per la creazione, l'aggiornamento e la disabilitazione degli account utente assegnati in LinkedIn Lookup in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f379-123">This section guides you through connecting your Azure AD to LinkedIn Lookup's SCIM user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in LinkedIn Lookup based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="0f379-124">Si può anche scegliere di abilitare l'accesso Single Sign-On basato su SAML per LinkedIn Lookup, seguendo le istruzioni disponibili nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0f379-124">You may also choose to enabled SAML-based Single Sign-On for LinkedIn Lookup, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0f379-125">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="0f379-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-linkedin-lookup-in-azure-ad"></a><span data-ttu-id="0f379-126">Per configurare il provisioning automatico degli account utente in LinkedIn Lookup con Azure AD:</span><span class="sxs-lookup"><span data-stu-id="0f379-126">To configure automatic user account provisioning to LinkedIn Lookup in Azure AD:</span></span>


<span data-ttu-id="0f379-127">Il primo passaggio consiste nel recuperare il token di accesso di LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="0f379-127">The first step is to retrieve your LinkedIn access token.</span></span> <span data-ttu-id="0f379-128">Un amministratore dell'organizzazione può eseguire il provisioning automatico di un token di accesso.</span><span class="sxs-lookup"><span data-stu-id="0f379-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="0f379-129">Nel centro account, passare a **Settings (Impostazioni) &gt; Global Settings** (Impostazioni globali) e aprire il pannello **SCIM Setup** (Installazione SCIM).</span><span class="sxs-lookup"><span data-stu-id="0f379-129">In your account center, go to **Settings &gt; Global Settings** and open the **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="0f379-130">Per accedere al centro account direttamente anziché tramite un collegamento seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="0f379-130">If you are accessing the account center directly rather than through a link, you can reach it using the following steps.</span></span>

1)  <span data-ttu-id="0f379-131">Accedere al centro account.</span><span class="sxs-lookup"><span data-stu-id="0f379-131">Sign in to Account Center.</span></span>

2)  <span data-ttu-id="0f379-132">Selezionare **Admin (Amministratore) &gt; Admin Settings** (Opzioni amministratore).</span><span class="sxs-lookup"><span data-stu-id="0f379-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="0f379-133">Fare clic su **Advanced Integrations** (Integrazioni avanzate) nella barra laterale di sinistra.</span><span class="sxs-lookup"><span data-stu-id="0f379-133">Click **Advanced Integrations** on the left sidebar.</span></span> <span data-ttu-id="0f379-134">Si verrà reindirizzati al centro account.</span><span class="sxs-lookup"><span data-stu-id="0f379-134">You are directed to the account center.</span></span>

4)  <span data-ttu-id="0f379-135">Fare clic su **+ Add new SCIM configuration** (+ Aggiungi nuova configurazione SCIM) e seguire la procedura compilando ogni campo.</span><span class="sxs-lookup"><span data-stu-id="0f379-135">Click **+ Add new SCIM configuration** and follow the procedure by filling in each field.</span></span>

> <span data-ttu-id="0f379-136">Se l'opzione di assegnazione automatica delle licenze non è abilitata, vengono sincronizzati solo i dati degli utenti.</span><span class="sxs-lookup"><span data-stu-id="0f379-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![Provisioning di LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_1.PNG)

> <span data-ttu-id="0f379-138">Quando l'opzione di assegnazione automatica delle licenze è abilitata, è necessario prendere nota dell'istanza dell'applicazione e del tipo di licenza.</span><span class="sxs-lookup"><span data-stu-id="0f379-138">When auto­license assignment is enabled, you need to note the application instance and license type.</span></span> <span data-ttu-id="0f379-139">Le licenze vengono assegnate in ordine di arrivo degli utenti fino a esaurimento di tutte le licenze.</span><span class="sxs-lookup"><span data-stu-id="0f379-139">Licenses are assigned on a first come, first serve basis until all the licenses are taken.</span></span>

![Provisioning di LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_2.PNG)

5)  <span data-ttu-id="0f379-141">Fare clic su **Generate token** (Genera token).</span><span class="sxs-lookup"><span data-stu-id="0f379-141">Click **Generate token**.</span></span> <span data-ttu-id="0f379-142">Il token di accesso dovrebbe essere visualizzato sotto il campo **Access token** (Token di accesso).</span><span class="sxs-lookup"><span data-stu-id="0f379-142">You should see your access token display under the **Access token** field.</span></span>

6)  <span data-ttu-id="0f379-143">Salvare il token di accesso negli Appunti o nel computer prima di uscire dalla pagina.</span><span class="sxs-lookup"><span data-stu-id="0f379-143">Save your access token to your clipboard or computer before leaving the page.</span></span>

7) <span data-ttu-id="0f379-144">Accedere quindi al [portale di Azure](https://portal.azure.com) e passare alla sezione **Azure Active Directory > App aziendali > Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0f379-144">Next, sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="0f379-145">Se si è già configurato LinkedIn Lookup per l'accesso Single Sign-On, cercare l'istanza di LinkedIn Lookup usando il campo di ricerca.</span><span class="sxs-lookup"><span data-stu-id="0f379-145">If you have already configured LinkedIn Lookup for single sign-on, search for your instance of LinkedIn Lookup using the search field.</span></span> <span data-ttu-id="0f379-146">In caso contrario, selezionare **Aggiungi** e cercare **LinkedIn Lookup** nella raccolta di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="0f379-146">Otherwise, select **Add** and search for **LinkedIn Lookup** in the application gallery.</span></span> <span data-ttu-id="0f379-147">Selezionare LinkedIn Lookup nei risultati della ricerca e aggiungerlo all'elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="0f379-147">Select LinkedIn Lookup from the search results, and add it to your list of applications.</span></span>

9)  <span data-ttu-id="0f379-148">Selezionare l'istanza di LinkedIn Lookup e quindi la scheda **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="0f379-148">Select your instance of LinkedIn Lookup, then select the **Provisioning** tab.</span></span>

10) <span data-ttu-id="0f379-149">Impostare **Modalità di provisioning** su **Automatico**.</span><span class="sxs-lookup"><span data-stu-id="0f379-149">Set the **Provisioning Mode** to **Automatic**.</span></span>

![Provisioning di LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_3.PNG)

11)  <span data-ttu-id="0f379-151">Compilare i campi seguenti in **Credenziali amministratore**:</span><span class="sxs-lookup"><span data-stu-id="0f379-151">Fill in the following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="0f379-152">Nel campo **URL tenant** immettere https://api.linkedin.com.</span><span class="sxs-lookup"><span data-stu-id="0f379-152">In the **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="0f379-153">Nel campo **Token segreto** immettere il token di accesso generato nel passaggio 1 e fare clic su **Connessione di test**.</span><span class="sxs-lookup"><span data-stu-id="0f379-153">In the **Secret Token** field, enter the access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="0f379-154">Nel lato superiore destro del portale viene visualizzata una notifica di esito positivo.</span><span class="sxs-lookup"><span data-stu-id="0f379-154">You should see a success notification on the upper­right side of   your portal.</span></span>

12) <span data-ttu-id="0f379-155">Immettere l'indirizzo di posta elettronica di una persona o un gruppo che riceverà le notifiche di errore relative al provisioning nel campo **Messaggio di posta elettronica di notifica** e selezionare la casella di controllo seguente.</span><span class="sxs-lookup"><span data-stu-id="0f379-155">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

13) <span data-ttu-id="0f379-156">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0f379-156">Click **Save**.</span></span> 

14) <span data-ttu-id="0f379-157">Nella sezione **Mapping degli attributi** esaminare gli attributi utente e gruppo che verranno sincronizzati da Azure AD a LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="0f379-157">In the **Attribute Mappings** section, review the user and group attributes that will be synchronized from Azure AD to LinkedIn Lookup.</span></span> <span data-ttu-id="0f379-158">Si noti che gli attributi selezionati come proprietà **corrispondenti** verranno usati per trovare le corrispondenze con gli account utente e i gruppi in LinkedIn Lookup per le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="0f379-158">Note that the attributes selected as **Matching** properties will be used to match the user accounts and groups in LinkedIn Lookup for update operations.</span></span> <span data-ttu-id="0f379-159">Selezionare il pulsante Salva per eseguire il commit delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="0f379-159">Select the Save button to commit any changes.</span></span>

![Provisioning di LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_4.PNG)

15) <span data-ttu-id="0f379-161">Per abilitare il servizio di provisioning di Azure AD per LinkedIn Lookup, impostare **Stato del provisioning** su **Sì** nella sezione **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="0f379-161">To enable the Azure AD provisioning service for LinkedIn Lookup, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

16) <span data-ttu-id="0f379-162">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0f379-162">Click **Save**.</span></span> 

<span data-ttu-id="0f379-163">Verrà avviata la sincronizzazione iniziale di tutti gli utenti e/o i gruppi assegnati a LinkedIn Lookup nella sezione Utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="0f379-163">This will start the initial synchronization of any users and/or groups assigned to LinkedIn Lookup in the Users and Groups section.</span></span> <span data-ttu-id="0f379-164">Si noti che la sincronizzazione iniziale richiederà più tempo delle sincronizzazioni successive, che saranno eseguite circa ogni 20 minuti per tutto il tempo che il servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0f379-164">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="0f379-165">È possibile usare la sezione **Dettagli sincronizzazione** per monitorare lo stato di avanzamento e selezionare i collegamenti ai report delle attività di provisioning, che descrivono tutte le azioni eseguite dal servizio di provisioning sull'app LinkedIn Lookup.</span><span class="sxs-lookup"><span data-stu-id="0f379-165">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your LinkedIn Lookup app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0f379-166">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0f379-166">Additional Resources</span></span>

* [<span data-ttu-id="0f379-167">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="0f379-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="0f379-168">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f379-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
