---
title: "i dati personali aaaProtect con controlli di identità e accessi Azure | Documenti Microsoft"
description: "Tramite Azure toohelp di controlli di identità e accessi proteggere i dati personali"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a><span data-ttu-id="d41d4-103">Azure Active Directory e Multi-Factor Authentication: proteggere i dati personali usando l'identità e i controlli di accesso</span><span class="sxs-lookup"><span data-stu-id="d41d4-103">Azure Active Directory and Multi-Factor Authentication: Protect personal data with identity and access controls</span></span>

<span data-ttu-id="d41d4-104">Questo articolo fornisce informazioni e procedure che è possibile utilizzare i dati personali a tooprotect usando i servizi e funzionalità di sicurezza di autenticazione di Azure Active Directory e a più fattori.</span><span class="sxs-lookup"><span data-stu-id="d41d4-104">This article provides information and procedures you can use tooprotect personal data using Azure Active Directory and Multi-factor authentication security features and services.</span></span>

## <a name="scenario"></a><span data-ttu-id="d41d4-105">Scenario</span><span class="sxs-lookup"><span data-stu-id="d41d4-105">Scenario</span></span>

<span data-ttu-id="d41d4-106">Una società crociera di grandi dimensioni, la sede centrale negli Stati Uniti hello espansione relativo itinerari toooffer operazioni Mediterraneo hello, Adriatico e mare Baltico, nonché hello isole britannico.</span><span class="sxs-lookup"><span data-stu-id="d41d4-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="d41d4-107">toosupport tali attività, che è stato acquisito più righe crociera inferiori basate in Italia, Germania, Danimarca e hello Regno Unito</span><span class="sxs-lookup"><span data-stu-id="d41d4-107">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="d41d4-108">la società Hello utilizza i dati aziendali di Microsoft Azure toostore nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="d41d4-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="d41d4-109">Questi includono informazioni personali come nomi, indirizzi, numeri di telefono e dati delle carte di credito della base clienti globale,</span><span class="sxs-lookup"><span data-stu-id="d41d4-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="d41d4-110">Include inoltre informazioni sulle risorse umane di tradizionali, ad esempio indirizzi, i numeri di telefono, codici fiscali e informazioni mediche relativi ai dipendenti della società in tutte le posizioni.</span><span class="sxs-lookup"><span data-stu-id="d41d4-110">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="d41d4-111">riga crociera Hello gestisce anche un database di grandi dimensioni di benefici e la fedeltà dei membri del programma che include informazioni personali tootrack relazioni con i clienti correnti e precedenti.</span><span class="sxs-lookup"><span data-stu-id="d41d4-111">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="d41d4-112">Rete con i dipendenti aziendali accesso hello da sedi remote e agenzie di viaggio hello aziendali presenti in ogni HelloWorld hanno accesso alle risorse aziendali toosome.</span><span class="sxs-lookup"><span data-stu-id="d41d4-112">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="d41d4-113">Presentazione del problema</span><span class="sxs-lookup"><span data-stu-id="d41d4-113">Problem statement</span></span>

<span data-ttu-id="d41d4-114">società Hello devono proteggere privacy hello dei dati personali dei dipendenti e clienti da utenti malintenzionati tentando di accedere toogain di identità toouse compromesso.</span><span class="sxs-lookup"><span data-stu-id="d41d4-114">hello company must protect hello privacy of customers’ and employees’ personal data from attackers seeking toouse compromised identities toogain access.</span></span> <span data-ttu-id="d41d4-115">È inoltre necessario verificare che toopersonal di accesso ai dati in base agli utenti legittimi sono limitati solo a quelli che ne hanno bisogno toodo i processi.</span><span class="sxs-lookup"><span data-stu-id="d41d4-115">They also must ensure that access toopersonal data by legitimate users is restricted to only those who need it toodo their jobs.</span></span>

## <a name="company-goal"></a><span data-ttu-id="d41d4-116">Obiettivo dell'azienda</span><span class="sxs-lookup"><span data-stu-id="d41d4-116">Company goal</span></span>

<span data-ttu-id="d41d4-117">obiettivo della società Hello è tooensure che accedono ai dati toopersonal è rigorosamente controllate.</span><span class="sxs-lookup"><span data-stu-id="d41d4-117">hello company’s goal is tooensure that access toopersonal data is strictly controlled.</span></span> <span data-ttu-id="d41d4-118">È essenziale che le identità degli utenti con accesso ai dati toopersonal sia protetta da autenticazione avanzata.</span><span class="sxs-lookup"><span data-stu-id="d41d4-118">It is essential that identities of users with access toopersonal data be protected by strong authentication.</span></span> <span data-ttu-id="d41d4-119">Un criterio di [privilegio minimo] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) deve essere applicata in modo che solo livello hello di accesso necessarie, non di più utenti autorizzati.</span><span class="sxs-lookup"><span data-stu-id="d41d4-119">A policy of [least privilege] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) must be enforced so that legitimate users have only hello level of  access they need, and no more.</span></span>

## <a name="solutions"></a><span data-ttu-id="d41d4-120">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="d41d4-120">Solutions</span></span>

<span data-ttu-id="d41d4-121">Microsoft Azure offre gli strumenti di gestione delle identità e accessi toohelp società chi ha accesso tooresources che contengono dati personali.</span><span class="sxs-lookup"><span data-stu-id="d41d4-121">Microsoft Azure provides identity and access management tools toohelp companies control who has access tooresources that contain personal data.</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="d41d4-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d41d4-122">Azure Active Directory</span></span>

<span data-ttu-id="d41d4-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) gestisce le identità e controlla l'accesso tooAzure così come altri locali e altre risorse cloud, dati e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="d41d4-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) manages identities and controls access tooAzure as well as other on-premises and other cloud resources, data, and applications.</span></span> <span data-ttu-id="d41d4-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) aiuta gli amministratori di Azure toominimize hello numerose persone che hanno accesso toocertain informazioni quali dati personali.</span><span class="sxs-lookup"><span data-stu-id="d41d4-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) helps Azure administrators toominimize hello number of people who have access toocertain information such as personal data.</span></span> <span data-ttu-id="d41d4-125">Consente loro toodiscover, limitare e monitorare le identità con privilegi e i relativi tooresources e tooassign temporaneo,-Time (JIT) diritti amministrativi tooeligible gli utenti di accesso.</span><span class="sxs-lookup"><span data-stu-id="d41d4-125">It enables them toodiscover, restrict, and monitor privileged identities and their access tooresources, and tooassign temporary, Just-In-Time (JIT) administrative rights tooeligible users.</span></span> <span data-ttu-id="d41d4-126">Consente anche di ottenere informazioni su coloro che hanno privilegi amministrativi di AAD.</span><span class="sxs-lookup"><span data-stu-id="d41d4-126">It also provides insight into those who have AAD administrative privileges.</span></span>

<span data-ttu-id="d41d4-127">le attività di Hello relativi all'utilizzo di AAD PIM includono:</span><span class="sxs-lookup"><span data-stu-id="d41d4-127">hello activities involved in using AAD PIM include:</span></span>

- <span data-ttu-id="d41d4-128">Abilitazione di Privileged Identity Management per la directory</span><span class="sxs-lookup"><span data-stu-id="d41d4-128">Enabling Privileged Identity Management for your directory</span></span>

- <span data-ttu-id="d41d4-129">Utilizzando Gestione identità con privilegi amministratore dashboard toosee importanti informazioni a colpo d'occhio</span><span class="sxs-lookup"><span data-stu-id="d41d4-129">Using Privileged Identity Management admin dashboard toosee important information at a glance</span></span>

- <span data-ttu-id="d41d4-130">La gestione delle identità con privilegiata hello (amministratori) aggiungendo o rimuovendo ruolo tooeach amministratori permanenti o idonei</span><span class="sxs-lookup"><span data-stu-id="d41d4-130">Managing hello privileged identities (administrators) by adding or removing permanent or eligible administrators tooeach role</span></span>

- <span data-ttu-id="d41d4-131">Configurazione delle impostazioni di attivazione di hello ruolo</span><span class="sxs-lookup"><span data-stu-id="d41d4-131">Configuring hello role activation settings</span></span>

- <span data-ttu-id="d41d4-132">Attivazione dei ruoli</span><span class="sxs-lookup"><span data-stu-id="d41d4-132">Activating roles</span></span>

- <span data-ttu-id="d41d4-133">Verifica dell'attività dei ruoli</span><span class="sxs-lookup"><span data-stu-id="d41d4-133">Reviewing role activity</span></span>

#### <a name="how-do-i-enable-aad-pim"></a><span data-ttu-id="d41d4-134">Come abilitare Azure Active Directory Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="d41d4-134">How do I enable AAD PIM?</span></span>

<span data-ttu-id="d41d4-135">usare PIM per la directory, toostart hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="d41d4-135">toostart using PIM for your directory, do hello following:</span></span>

1. <span data-ttu-id="d41d4-136">Accedi toohello portale di Azure come amministratore globale della directory.</span><span class="sxs-lookup"><span data-stu-id="d41d4-136">Sign in toohello Azure portal as a global administrator of your directory.</span></span>

2. <span data-ttu-id="d41d4-137">Se l'organizzazione dispone di più di una directory, selezionare il nome utente in hello nell'angolo superiore destro di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d41d4-137">If your organization has more than one directory, select your username in hello upper right-hand corner of hello Azure portal.</span></span> <span data-ttu-id="d41d4-138">Selezionare la directory di hello in cui si userà Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="d41d4-138">Select hello directory where you will use Azure AD Privileged Identity Management.</span></span>

3. <span data-ttu-id="d41d4-139">Selezionare **più servizi** e utilizzare hello **filtro** toosearch casella di testo per Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="d41d4-139">Select **More services** and use hello **Filter** textbox toosearch for Azure AD Privileged Identity Management.</span></span>

4. <span data-ttu-id="d41d4-140">Controllare **Pin toodashboard** e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="d41d4-140">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="d41d4-141">verrà visualizzata la finestra di Hello applicazione Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="d41d4-141">hello Privileged Identity Management application opens.</span></span>

<span data-ttu-id="d41d4-142">Una volta configurato, Azure AD Privileged Identity Management vedrai il pannello di navigazione hello ogni volta che si apre un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="d41d4-142">Once Azure AD Privileged Identity Management is set up, you see hello navigation blade whenever you open hello application.</span></span>

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

<span data-ttu-id="d41d4-143">Per altre informazioni e istruzioni su come iniziare a usare Azure Active Directory Privileged Identity Management, vedere [Iniziare ad usare Azure AD Privileged Identity Management](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started).</span><span class="sxs-lookup"><span data-stu-id="d41d4-143">For more information and instructions on getting started with AAD PIM, see [Start Using Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span></span>

### <a name="azure-role-based-access-control"></a><span data-ttu-id="d41d4-144">Controllo degli accessi in base al ruolo di Azure</span><span class="sxs-lookup"><span data-stu-id="d41d4-144">Azure Role-based Access Control</span></span>

<span data-ttu-id="d41d4-145">[Controllo di accesso basato sui ruoli Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) aiuta gli amministratori di Azure a gestire tooAzure di accedere alle risorse abilitazione hello concessione dell'accesso in base a hello assegnato il ruolo utente.</span><span class="sxs-lookup"><span data-stu-id="d41d4-145">[Azure Role-Based Access Control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) helps Azure administrators manage access tooAzure resources by enabling hello granting of access based on hello user’s assigned role.</span></span> <span data-ttu-id="d41d4-146">È possibile separare i compiti all'interno di un team e concedere solo hello quantità di accesso toousers, gruppi e le applicazioni che devono tooperform i processi.</span><span class="sxs-lookup"><span data-stu-id="d41d4-146">You can segregate duties within a team and grant only hello amount of access toousers, groups and applications that they need tooperform their jobs.</span></span>

<span data-ttu-id="d41d4-147">È possibile concedere accesso basato sui ruoli toousers utilizzando hello portale di Azure, gli strumenti da riga di comando di Azure o le API di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d41d4-147">Role-based access can be granted toousers using hello Azure portal, Azure Command-Line tools or Azure Management APIs.</span></span>

<span data-ttu-id="d41d4-148">Per ulteriori informazioni sui concetti di base sui ruoli di Azure, vedere [introduzione Role-Based Access Control in hello portale di Azure.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span><span class="sxs-lookup"><span data-stu-id="d41d4-148">For more information about Azure RBAC basics, see [Get started with Role-Based Access Control in hello Azure Portal.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span></span>

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a><span data-ttu-id="d41d4-149">Come gestire il controllo degli accessi in base al ruolo con PowerShell</span><span class="sxs-lookup"><span data-stu-id="d41d4-149">How do I manage Azure RBAC with PowerShell?</span></span>

<span data-ttu-id="d41d4-150">È possibile utilizzare i cmdlet di PowerShell toomanage RBAC di Azure, tra cui hello seguenti attività di gestione:</span><span class="sxs-lookup"><span data-stu-id="d41d4-150">You can use PowerShell cmdlets toomanage Azure RBAC, including hello following management tasks:</span></span>

- <span data-ttu-id="d41d4-151">Elenco dei ruoli</span><span class="sxs-lookup"><span data-stu-id="d41d4-151">List roles</span></span>

- <span data-ttu-id="d41d4-152">Assegnazioni di accesso</span><span class="sxs-lookup"><span data-stu-id="d41d4-152">See who has access</span></span>

- <span data-ttu-id="d41d4-153">Concedere l'accesso</span><span class="sxs-lookup"><span data-stu-id="d41d4-153">Grant access</span></span>

- <span data-ttu-id="d41d4-154">Rimuovere un accesso</span><span class="sxs-lookup"><span data-stu-id="d41d4-154">Remove access</span></span>

- <span data-ttu-id="d41d4-155">Creare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="d41d4-155">Create a custom role</span></span>

- <span data-ttu-id="d41d4-156">Ottenere le azioni per un provider di risorse</span><span class="sxs-lookup"><span data-stu-id="d41d4-156">Get Actions for a Resource Provider</span></span>

- <span data-ttu-id="d41d4-157">Modificare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="d41d4-157">Modify a custom role</span></span>

- <span data-ttu-id="d41d4-158">Eliminare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="d41d4-158">Delete a custom role</span></span>

- <span data-ttu-id="d41d4-159">Elencare ruoli personalizzati</span><span class="sxs-lookup"><span data-stu-id="d41d4-159">List custom roles</span></span>

<span data-ttu-id="d41d4-160">Per istruzioni su come toomanage RBAC Azure con PowerShell, vedere [basata sui ruoli di gestione accesso con Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span><span class="sxs-lookup"><span data-stu-id="d41d4-160">For instructions on how toomanage Azure RBAC with PowerShell, see [Manage Role-based Access with Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span></span>

### <a name="azure-multi-factor-authentication"></a><span data-ttu-id="d41d4-161">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="d41d4-161">Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="d41d4-162">[Azure multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) è una soluzione di verifica in due fasi che consente di salvaguardare accesso toodata e applicazioni, rispettando la richiesta dell'utente per un semplice processo.</span><span class="sxs-lookup"><span data-stu-id="d41d4-162">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) is a two-step verification solution that helps safeguard access toodata and applications, while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="d41d4-163">Offre autenticazione avanzata tramite una gamma di metodi di verifica, fra cui una telefonata, un SMS o una verifica dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="d41d4-163">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

<span data-ttu-id="d41d4-164">toodeploy autenticazione a più fattori in hello cloud di Azure, è necessario toofirst attivarla e quindi attivare la verifica in due passaggi per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="d41d4-164">toodeploy MFA in hello Azure cloud, you need toofirst enable it and then turn on two-step verification for users.</span></span>

#### <a name="how-do-i-enable-azure-toouse-mfa"></a><span data-ttu-id="d41d4-165">Come abilitare toouse Azure MFA?</span><span class="sxs-lookup"><span data-stu-id="d41d4-165">How do I enable Azure toouse MFA?</span></span>

<span data-ttu-id="d41d4-166">Se gli utenti hanno le licenze che includono Azure multi-Factor Authentication, non è necessario che è necessario tooturn toodo su Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="d41d4-166">If your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="d41d4-167">In caso contrario, è necessario un provider multi-Factor Authentication toocreate nella directory.</span><span class="sxs-lookup"><span data-stu-id="d41d4-167">If not, you need toocreate a Multi-Factor Auth provider in your directory.</span></span> <span data-ttu-id="d41d4-168">toodo, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="d41d4-168">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="d41d4-169">Selezionare **Active Directory** in hello portale di Azure classico (connesso come amministratore).</span><span class="sxs-lookup"><span data-stu-id="d41d4-169">Select **Active Directory** in hello Azure classic portal (logged on as an administrator).</span></span>

2. <span data-ttu-id="d41d4-170">Selezionare **Provider di Multi-Factor Authentication**.</span><span class="sxs-lookup"><span data-stu-id="d41d4-170">Select **Multi-Factor Authentication Providers.**</span></span>

3. <span data-ttu-id="d41d4-171">Selezionare **Nuovo** e quindi **Provider di Multi-Factor Authentication** in **Servizi app**.</span><span class="sxs-lookup"><span data-stu-id="d41d4-171">Select **New,** and then under **App Services,** select **Multi-Factor Auth Provider.**</span></span>

4. <span data-ttu-id="d41d4-172">Selezionare **Creazione rapida**.</span><span class="sxs-lookup"><span data-stu-id="d41d4-172">Select **Quick Create.**</span></span>

5. <span data-ttu-id="d41d4-173">Compilare il campo di nome hello e selezionare un modello di utilizzo (per l'autenticazione o per utente abilitato).</span><span class="sxs-lookup"><span data-stu-id="d41d4-173">Fill in hello name field and select a usage model (per authentication or per enabled user).</span></span>

6. <span data-ttu-id="d41d4-174">Designare una directory a cui hello è associato il Provider di autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="d41d4-174">Designate a directory with which hello MFA Provider is associated.</span></span>

7. <span data-ttu-id="d41d4-175">Fare clic su hello **crea** pulsante.</span><span class="sxs-lookup"><span data-stu-id="d41d4-175">Click hello **Create** button.</span></span>

![](media/protect-personal-data-identity-access-controls/quick-create.png)

<span data-ttu-id="d41d4-176">Per altre istruzioni su come toomanage Provider multi-Factor Authentication, vedere [Introduzione a un Provider di Azure multi-Factor Authentication.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span><span class="sxs-lookup"><span data-stu-id="d41d4-176">For more instructions on how toomanage your Multi-Factor Auth Provider, see [Getting Started with an Azure Multi-Factor Auth Provider.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span></span>

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a><span data-ttu-id="d41d4-177">Come attivare la verifica in due passaggi per gli utenti</span><span class="sxs-lookup"><span data-stu-id="d41d4-177">How do I turn on two-step verification for users?</span></span>

<span data-ttu-id="d41d4-178">È possibile applicare la verifica in due passaggi per accessi tutti o solo quando si verificano condizioni specifiche, è possibile creare verifica in due passaggi toorequire criteri di accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="d41d4-178">You can enforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when specific conditions apply.</span></span>

<span data-ttu-id="d41d4-179">L'abilitazione di autenticazione a più fattori di Azure, modificare stati utente è l'approccio tradizionale hello per la richiesta di verifica in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="d41d4-179">Enabling Azure MFA by changing user states is hello traditional approach for requiring two-step verification.</span></span> <span data-ttu-id="d41d4-180">Tutti gli utenti di hello che abiliti hello verifica in due passaggi di stesso requisito tooperform ogni volta che effettuano l'accesso.</span><span class="sxs-lookup"><span data-stu-id="d41d4-180">All hello users that you enable will have hello same requirement tooperform two-step verification every time they sign in.</span></span> <span data-ttu-id="d41d4-181">L'abilitazione di un utente sostituisce eventuali criteri di accesso condizionale in vigore per l'utente.</span><span class="sxs-lookup"><span data-stu-id="d41d4-181">Enabling a user overrides any conditional access policies that may affect that user.</span></span>

<span data-ttu-id="d41d4-182">L'abilitazione di Azure MFA con criteri di accesso condizionale è un approccio più flessibile per richiedere la verifica in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="d41d4-182">Enabling Azure MFA with a conditional access policy is a more flexible approach for requiring two-step verification.</span></span> <span data-ttu-id="d41d4-183">È possibile creare criteri di accesso condizionale che si applicano toogroups, nonché a singoli utenti.</span><span class="sxs-lookup"><span data-stu-id="d41d4-183">You can create conditional access policies that apply toogroups as well as individual users.</span></span> <span data-ttu-id="d41d4-184">È possibile, ad esempio, assegnare ai gruppi ad alto rischio più restrizioni rispetto ai gruppi a basso rischio oppure richiedere la verifica in due passaggi solo per le app cloud ad alto rischio e non per quelle a basso rischio.</span><span class="sxs-lookup"><span data-stu-id="d41d4-184">High-risk groups can be given more restrictions than low-risk groups, or two-step verification can be required only for high-risk cloud apps and skipped for low-risk ones.</span></span> <span data-ttu-id="d41d4-185">L'accesso condizionale è tuttavia una funzionalità a pagamento di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d41d4-185">However, conditional access is a paid feature of Azure Active Directory.</span></span>

<span data-ttu-id="d41d4-186">hello tooenable MFA modificando lo stato utente seguenti:</span><span class="sxs-lookup"><span data-stu-id="d41d4-186">tooenable MFA by changing user state, do hello following:</span></span>

1. <span data-ttu-id="d41d4-187">Accedi toohello portale di Azure come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d41d4-187">Sign in toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="d41d4-188">Andare troppo**Azure Active Directory \> utenti e gruppi \> tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="d41d4-188">Go too**Azure Active Directory \> Users and groups \> All users**.</span></span>
3. <span data-ttu-id="d41d4-189">Selezionare **Multi-Factor Authentication**.</span><span class="sxs-lookup"><span data-stu-id="d41d4-189">Select **Multi-Factor Authentication**.</span></span>
4. <span data-ttu-id="d41d4-190">Trova hello utente che si desidera tooenable per Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="d41d4-190">Find hello user that you want tooenable for Azure MFA.</span></span> <span data-ttu-id="d41d4-191">Potrebbe essere necessario toochange hello visualizzazione nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="d41d4-191">You may need toochange hello view at hello top.</span></span>
5. <span data-ttu-id="d41d4-192">Controllare nome hello casella Avanti toohello dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d41d4-192">Check hello box next toohello user’s name.</span></span>
6. <span data-ttu-id="d41d4-193">Sulla destra, nella casella rapide hello, scegliere **abilitare**.</span><span class="sxs-lookup"><span data-stu-id="d41d4-193">On hello right, under quick steps, choose **Enable**.</span></span>

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. <span data-ttu-id="d41d4-194">Confermare la selezione nella finestra popup di hello visualizzata.</span><span class="sxs-lookup"><span data-stu-id="d41d4-194">Confirm your selection in hello pop-up window that opens.</span></span>  <span data-ttu-id="d41d4-195">Gli utenti per cui è stata abilitata l'autenticazione a più fattori verranno chiesto hello tooregister successivo che accesso.</span><span class="sxs-lookup"><span data-stu-id="d41d4-195">Users for whom MFA has been enabled will be asked tooregister hello next time they sign in.</span></span>

<span data-ttu-id="d41d4-196">tooenable Azure MFA con un criterio di accesso condizionale, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="d41d4-196">tooenable Azure MFA with a conditional access policy, do hello following:</span></span>

1. <span data-ttu-id="d41d4-197">Accedi toohello portale di Azure come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d41d4-197">Sign in toohello Azure portal as an administrator.</span></span>

2. <span data-ttu-id="d41d4-198">Andare troppo**Azure Active Directory \> accesso condizionale**.</span><span class="sxs-lookup"><span data-stu-id="d41d4-198">Go too**Azure Active Directory \> Conditional access**.</span></span>

3. <span data-ttu-id="d41d4-199">Selezionare **Nuovi criteri**.</span><span class="sxs-lookup"><span data-stu-id="d41d4-199">Select **New policy**.</span></span>

4. <span data-ttu-id="d41d4-200">In **Assegnazioni** selezionare **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d41d4-200">Under **Assignments**, select **Users and groups**.</span></span> <span data-ttu-id="d41d4-201">Hello utilizzare **Include** e **escludere** schede toospecify quali utenti e gruppi verranno gestiti da criteri hello.</span><span class="sxs-lookup"><span data-stu-id="d41d4-201">Use hello **Include** and     **Exclude** tabs toospecify which users and groups will be managed by hello policy.</span></span>

5. <span data-ttu-id="d41d4-202">In **Assegnazioni** selezionare **App cloud**.</span><span class="sxs-lookup"><span data-stu-id="d41d4-202">Under **Assignments**, select **Cloud apps.**</span></span> <span data-ttu-id="d41d4-203">Scegliere troppo**includono tutte le app cloud**.</span><span class="sxs-lookup"><span data-stu-id="d41d4-203">Choose too**include All cloud apps**.</span></span>
6.  <span data-ttu-id="d41d4-204">In **Controlli di accesso** selezionare **Concedi**.</span><span class="sxs-lookup"><span data-stu-id="d41d4-204">Under **Access controls**, select **Grant**.</span></span> <span data-ttu-id="d41d4-205">Selezionare **Richiedi autenticazione a più fattori**.</span><span class="sxs-lookup"><span data-stu-id="d41d4-205">Choose **Require multi-factor authentication**.</span></span>
7.  <span data-ttu-id="d41d4-206">Attivare **abilitare i criteri di** troppo**su** e quindi selezionare **salvare**.</span><span class="sxs-lookup"><span data-stu-id="d41d4-206">Turn **Enable policy** too**On** and then select **Save**.</span></span>

<span data-ttu-id="d41d4-207">Per informazioni su come tooset le impostazioni di autenticazione a più fattori di Azure tooconfigure di avvisi di illecito, creare un bypass monouso, utilizzare i messaggi vocali personalizzati, configurare la memorizzazione nella cache, specificare indirizzi IP attendibili, creare password dell'app, abilitare la memorizzazione di autenticazione a più fattori per i dispositivi che gli utenti attendibili, selezionare metodi di verifica, vedere [configurare impostazioni di Azure multi-Factor Authentication.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span><span class="sxs-lookup"><span data-stu-id="d41d4-207">For information on how tooconfigure Azure MFA settings tooset up fraud alerts, create a one-time bypass, use custom voice messages, configure caching, specify trusted IPs, create app passwords, enable remembering MFA for devices that users trust, and select verification methods, see [Configure Azure Multi-Factor Authentication Settings.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d41d4-208">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d41d4-208">Next steps</span></span>

- [<span data-ttu-id="d41d4-209">Protezione dell'accesso con privilegi in Azure AD</span><span class="sxs-lookup"><span data-stu-id="d41d4-209">Securing privileged access in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [<span data-ttu-id="d41d4-210">Domande frequenti su Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="d41d4-210">Frequently asked questions about Azure Multi-Factor Authentication</span></span>](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [<span data-ttu-id="d41d4-211">Risoluzione dei problemi del controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="d41d4-211">Role-based Access Control troubleshooting</span></span>](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [<span data-ttu-id="d41d4-212">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="d41d4-212">Azure Active Directory Identity Protection</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
