---
title: aaaAzure IoT Suite e Azure Active Directory | Documenti Microsoft
description: Descrive l'utilizzo di autorizzazioni di Azure Active Directory toomanage Azure IoT Suite.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: dobett
ms.openlocfilehash: 4768630f2de4bb431731fbd4e8929232bc80b9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-on-hello-azureiotsuitecom-site"></a><span data-ttu-id="d1619-103">Autorizzazioni nel sito azureiotsuite.com hello</span><span class="sxs-lookup"><span data-stu-id="d1619-103">Permissions on hello azureiotsuite.com site</span></span>

## <a name="what-happens-when-you-sign-in"></a><span data-ttu-id="d1619-104">Cosa accade quando si accede</span><span class="sxs-lookup"><span data-stu-id="d1619-104">What happens when you sign in</span></span>

<span data-ttu-id="d1619-105">Hello prima volta che accedi a [azureiotsuite.com][lnk-azureiotsuite], sito hello determina i livelli di autorizzazione hello basato sul hello attualmente selezionato tenant Azure Active Directory (AAD) e Azure sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d1619-105">hello first time you sign in at [azureiotsuite.com][lnk-azureiotsuite], hello site determines hello permission levels you have based on hello currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span></span>

1. <span data-ttu-id="d1619-106">In primo luogo, elenco toopopulate hello del nome utente tooyour Avanti tenant visualizzato sito hello rileva da Azure cui si appartiene i tenant AAD.</span><span class="sxs-lookup"><span data-stu-id="d1619-106">First, toopopulate hello list of tenants seen next tooyour username, hello site finds out from Azure which AAD tenants you belong to.</span></span> <span data-ttu-id="d1619-107">Attualmente, sito hello può ricevere solo i token utente per un tenant alla volta.</span><span class="sxs-lookup"><span data-stu-id="d1619-107">Currently, hello site can only obtain user tokens for one tenant at a time.</span></span> <span data-ttu-id="d1619-108">Pertanto, quando si passa tenant usando l'elenco a discesa hello nell'angolo superiore destro di hello, sito hello consente l'accesso i token di hello toothat tenant tooobtain per tenant.</span><span class="sxs-lookup"><span data-stu-id="d1619-108">Therefore, when you switch tenants using hello dropdown in hello top right corner, hello site logs you in toothat tenant tooobtain hello tokens for that tenant.</span></span>

2. <span data-ttu-id="d1619-109">Successivamente, il sito hello rileva dalle sottoscrizioni che sono stati associati a hello selezionato tenant di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1619-109">Next, hello site finds out from Azure which subscriptions you have associated with hello selected tenant.</span></span> <span data-ttu-id="d1619-110">Vedrai sottoscrizioni disponibili hello quando si crea una nuova soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="d1619-110">You see hello available subscriptions when you create a new preconfigured solution.</span></span>

3. <span data-ttu-id="d1619-111">Infine, sito hello recupera tutte le risorse di hello in sottoscrizioni hello e gruppi di risorse contrassegnate come soluzioni preconfigurate e popola riquadri hello hello home page.</span><span class="sxs-lookup"><span data-stu-id="d1619-111">Finally, hello site retrieves all hello resources in hello subscriptions and resource groups tagged as preconfigured solutions and populates hello tiles on hello home page.</span></span>

<span data-ttu-id="d1619-112">Hello le sezioni seguenti vengono descritti i ruoli di hello che controllano l'accesso toohello preconfigurato soluzioni.</span><span class="sxs-lookup"><span data-stu-id="d1619-112">hello following sections describe hello roles that control access toohello preconfigured solutions.</span></span>

## <a name="aad-roles"></a><span data-ttu-id="d1619-113">Ruoli AAD</span><span class="sxs-lookup"><span data-stu-id="d1619-113">AAD roles</span></span>

<span data-ttu-id="d1619-114">ruoli AAD Hello le soluzioni di effettuare il provisioning preconfigurato possibilità hello di controllo e gestire gli utenti in una soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="d1619-114">hello AAD roles control hello ability provision preconfigured solutions and manage users in a preconfigured solution.</span></span>

<span data-ttu-id="d1619-115">Per altre informazioni sui ruoli di amministratore in AAD, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory][lnk-aad-admin].</span><span class="sxs-lookup"><span data-stu-id="d1619-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span></span> <span data-ttu-id="d1619-116">Hello corrente viene descritta la hello **amministratore globale** hello e **utente** ruoli della directory utilizzata da hello preconfigurato soluzioni.</span><span class="sxs-lookup"><span data-stu-id="d1619-116">hello current article focuses on hello **Global Administrator** and hello **User** directory roles as used by hello preconfigured solutions.</span></span>

### <a name="global-administrator"></a><span data-ttu-id="d1619-117">Amministratore globale</span><span class="sxs-lookup"><span data-stu-id="d1619-117">Global administrator</span></span>

<span data-ttu-id="d1619-118">Per ogni tenant di AAD possono essere presenti più amministratori globali:</span><span class="sxs-lookup"><span data-stu-id="d1619-118">There can be many global administrators per AAD tenant:</span></span>

* <span data-ttu-id="d1619-119">Quando si crea un tenant di AAD, si è amministratore predefinito hello globale del tenant.</span><span class="sxs-lookup"><span data-stu-id="d1619-119">When you create an AAD tenant, you are by default hello global administrator of that tenant.</span></span>
* <span data-ttu-id="d1619-120">amministratore globale di Hello è possibile eseguire il provisioning di una soluzione preconfigurata e viene assegnato un **Admin** ruolo per l'applicazione hello interno al proprio tenant AAD.</span><span class="sxs-lookup"><span data-stu-id="d1619-120">hello global administrator can provision a preconfigured solution and is assigned an **Admin** role for hello application inside their AAD tenant.</span></span>
* <span data-ttu-id="d1619-121">Se un altro utente in hello stesso tenant di AAD viene creata un'applicazione, ruolo predefinito hello concesso toohello amministratore globale è **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="d1619-121">If another user in hello same AAD tenant creates an application, hello default role granted toohello global administrator is **ReadOnly**.</span></span>
* <span data-ttu-id="d1619-122">Un amministratore globale può assegnare tooroles gli utenti per applicazioni che utilizzano hello [portale di Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="d1619-122">A global administrator can assign users tooroles for applications using hello [Azure portal][lnk-portal].</span></span>

### <a name="domain-user"></a><span data-ttu-id="d1619-123">Utente di dominio</span><span class="sxs-lookup"><span data-stu-id="d1619-123">Domain user</span></span>

<span data-ttu-id="d1619-124">Per ogni tenant di AAD possono essere presenti molti utenti del dominio:</span><span class="sxs-lookup"><span data-stu-id="d1619-124">There can be many domain users per AAD tenant:</span></span>

* <span data-ttu-id="d1619-125">Un utente di dominio può eseguire il provisioning di una soluzione preconfigurata tramite hello [azureiotsuite.com] [ lnk-azureiotsuite] sito.</span><span class="sxs-lookup"><span data-stu-id="d1619-125">A domain user can provision a preconfigured solution through hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="d1619-126">Per impostazione predefinita, utente di dominio hello viene concessa hello **Admin** ruolo in hello il provisioning dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d1619-126">By default, hello domain user is granted hello **Admin** role in hello provisioned application.</span></span>
* <span data-ttu-id="d1619-127">Un utente di dominio è possibile creare un'applicazione tramite lo script build.cmd hello in hello [azure iot-remoto monitoraggio][lnk-rm-github-repo], [azure-iot--manutenzione predittiva] [ lnk-pm-github-repo], o [azure iot-connessione-factory] [ lnk-cf-github-repo] repository.</span><span class="sxs-lookup"><span data-stu-id="d1619-127">A domain user can create an application using hello build.cmd script in hello [azure-iot-remote-monitoring][lnk-rm-github-repo],  [azure-iot-predictive-maintenance][lnk-pm-github-repo], or [azure-iot-connected-factory][lnk-cf-github-repo] repository.</span></span> <span data-ttu-id="d1619-128">Tuttavia, ruolo predefinito hello concesso è utente di dominio toohello **ReadOnly**, perché un utente di dominio non dispone di ruoli tooassign di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="d1619-128">However, hello default role granted toohello domain user is **ReadOnly**, because a domain user does not have permission tooassign roles.</span></span>
* <span data-ttu-id="d1619-129">Se un altro utente nel tenant AAD hello viene creata un'applicazione, utente di dominio hello viene assegnato hello **ReadOnly** ruolo per impostazione predefinita per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d1619-129">If another user in hello AAD tenant creates an application, hello domain user is assigned hello **ReadOnly** role by default for that application.</span></span>
* <span data-ttu-id="d1619-130">Un utente di dominio non può assegnare ruoli per le applicazioni, quindi non può aggiungere utenti o ruoli per gli utenti di un'applicazione anche se ne è stato effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="d1619-130">A domain user cannot assign roles for applications; therefore a domain user cannot add users or roles for users for an application even if they provisioned it.</span></span>

### <a name="guest-user"></a><span data-ttu-id="d1619-131">Utente guest</span><span class="sxs-lookup"><span data-stu-id="d1619-131">Guest User</span></span>

<span data-ttu-id="d1619-132">Per ogni tenant AAD possono essere presenti molti utenti guest.</span><span class="sxs-lookup"><span data-stu-id="d1619-132">There can be many guest users per AAD tenant.</span></span> <span data-ttu-id="d1619-133">Gli utenti guest dispongono di un set limitato di diritti nel tenant AAD hello.</span><span class="sxs-lookup"><span data-stu-id="d1619-133">Guest users have a limited set of rights in hello AAD tenant.</span></span> <span data-ttu-id="d1619-134">Di conseguenza, gli utenti guest non è possibile eseguire il provisioning di una soluzione preconfigurata nel tenant AAD hello.</span><span class="sxs-lookup"><span data-stu-id="d1619-134">As a result, guest users cannot provision a preconfigured solution in hello AAD tenant.</span></span>

<span data-ttu-id="d1619-135">Per ulteriori informazioni su utenti e ruoli in AAD, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="d1619-135">For more information about users and roles in AAD, see hello following resources:</span></span>

* <span data-ttu-id="d1619-136">[Creare utenti in Azure AD][lnk-create-edit-users]</span><span class="sxs-lookup"><span data-stu-id="d1619-136">[Create users in Azure AD][lnk-create-edit-users]</span></span>
* <span data-ttu-id="d1619-137">[Assegnare gli utenti tooapps][lnk-assign-app-roles]</span><span class="sxs-lookup"><span data-stu-id="d1619-137">[Assign users tooapps][lnk-assign-app-roles]</span></span>

## <a name="azure-subscription-administrator-roles"></a><span data-ttu-id="d1619-138">Ruoli di amministratore della sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="d1619-138">Azure subscription administrator roles</span></span>

<span data-ttu-id="d1619-139">ruoli di amministratore di Azure Hello controllare hello possibilità toomap tenant di tooan AD una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1619-139">hello Azure admin roles control hello ability toomap an Azure subscription tooan AD tenant.</span></span>

<span data-ttu-id="d1619-140">Maggiori informazioni sui ruoli di amministratore Azure hello nell'articolo hello [come tooadd o modificare l'Account amministratore, amministratore del servizio e Azure CO-amministratore][lnk-admin-roles].</span><span class="sxs-lookup"><span data-stu-id="d1619-140">Find out more about hello Azure admin roles in hello article [How tooadd or change Azure Co-Administrator, Service Administrator, and Account Administrator][lnk-admin-roles].</span></span>

## <a name="application-roles"></a><span data-ttu-id="d1619-141">Ruoli applicazione</span><span class="sxs-lookup"><span data-stu-id="d1619-141">Application roles</span></span>

<span data-ttu-id="d1619-142">i ruoli applicazione Hello controllano accesso toodevices nella soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="d1619-142">hello application roles control access toodevices in your preconfigured solution.</span></span>

<span data-ttu-id="d1619-143">In un'applicazione su cui è stato eseguito il provisioning sono stati definiti due ruoli e uno implicito:</span><span class="sxs-lookup"><span data-stu-id="d1619-143">There are two defined roles and one implicit role defined in a provisioned application:</span></span>

* <span data-ttu-id="d1619-144">**Amministratore:** ha tooadd controllo completo, gestire, rimuovere i dispositivi e modificare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="d1619-144">**Admin:** Has full control tooadd, manage, remove devices, and modify settings.</span></span>
* <span data-ttu-id="d1619-145">**ReadOnly:** è possibile visualizzare i dispositivi, le regole, le azioni, i processi e i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="d1619-145">**ReadOnly:** Can view devices, rules, actions, jobs, and telemetry.</span></span>

<span data-ttu-id="d1619-146">È possibile trovare le autorizzazioni di hello assegnato il ruolo di tooeach in hello [RolePermissions.cs] [ lnk-resource-cs] file di origine.</span><span class="sxs-lookup"><span data-stu-id="d1619-146">You can find hello permissions assigned tooeach role in hello [RolePermissions.cs][lnk-resource-cs] source file.</span></span>

### <a name="changing-application-roles-for-a-user"></a><span data-ttu-id="d1619-147">Modifica dei ruoli applicazione di un utente</span><span class="sxs-lookup"><span data-stu-id="d1619-147">Changing application roles for a user</span></span>

<span data-ttu-id="d1619-148">È possibile utilizzare hello seguendo procedure toomake un utente in Active Directory un amministratore della soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="d1619-148">You can use hello following procedure toomake a user in your Active Directory an administrator of your preconfigured solution.</span></span>

<span data-ttu-id="d1619-149">È necessario essere un ruolo di toochange AAD amministratore globale per un utente:</span><span class="sxs-lookup"><span data-stu-id="d1619-149">You must be an AAD global administrator toochange roles for a user:</span></span>

1. <span data-ttu-id="d1619-150">Passare toohello [portale di Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="d1619-150">Go toohello [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="d1619-151">Selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d1619-151">Select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="d1619-152">Verificare che si utilizzano directory hello che scelto azureiotsuite.com quando è stato effettuato il provisioning della soluzione.</span><span class="sxs-lookup"><span data-stu-id="d1619-152">Make sure you are using hello directory you chose on azureiotsuite.com when you provisioned your solution.</span></span> <span data-ttu-id="d1619-153">Se si dispone di più directory associata alla sottoscrizione, è possibile passare tra loro se si sceglie il nome dell'account in alto a destra di hello del portale hello.</span><span class="sxs-lookup"><span data-stu-id="d1619-153">If you have multiple directories associated with your subscription, you can switch between them if you click your account name at hello top-right of hello portal.</span></span>
4. <span data-ttu-id="d1619-154">Fare clic su **Applicazioni aziendali**, quindi su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d1619-154">Click **Enterprise applications**, then **All applications**.</span></span>
4. <span data-ttu-id="d1619-155">Vengono visualizzate **Tutte le applicazioni** con stato **Qualsiasi**.</span><span class="sxs-lookup"><span data-stu-id="d1619-155">Show **All applications** with **Any** status.</span></span> <span data-ttu-id="d1619-156">Eseguire quindi una ricerca per un'applicazione con il nome della soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="d1619-156">Then search for an application with name of your preconfigured solution.</span></span>
5. <span data-ttu-id="d1619-157">Fare clic su nome hello dell'applicazione hello che corrisponde al nome della soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="d1619-157">Click hello name of hello application that matches your preconfigured solution name.</span></span>
6. <span data-ttu-id="d1619-158">Fare clic su **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d1619-158">Click **Users and groups**.</span></span>
7. <span data-ttu-id="d1619-159">Selezionare utente hello tooswitch ruoli.</span><span class="sxs-lookup"><span data-stu-id="d1619-159">Select hello user you want tooswitch roles.</span></span>
8. <span data-ttu-id="d1619-160">Fare clic su **assegnare** e selezionare hello ruolo (ad esempio **Admin**) tooassign toohello utente, fare clic su hello segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="d1619-160">Click **Assign** and select hello role (such as **Admin**) you'd like tooassign toohello user, click hello check mark.</span></span>

## <a name="faq"></a><span data-ttu-id="d1619-161">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="d1619-161">FAQ</span></span>

### <a name="im-a-service-administrator-and-id-like-toochange-hello-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a><span data-ttu-id="d1619-162">Sono un amministratore del servizio e il mapping della directory hello toochange vorrei tra la sottoscrizione e un tenant di Azure ad specifico.</span><span class="sxs-lookup"><span data-stu-id="d1619-162">I'm a service administrator and I'd like toochange hello directory mapping between my subscription and a specific AAD tenant.</span></span> <span data-ttu-id="d1619-163">Come completare questa attività</span><span class="sxs-lookup"><span data-stu-id="d1619-163">How do I complete this task?</span></span>

1. <span data-ttu-id="d1619-164">Passare toohello [portale di Azure classico][lnk-classic-portal], fare clic su **impostazioni** nell'elenco di hello dei servizi sul lato sinistro di hello.</span><span class="sxs-lookup"><span data-stu-id="d1619-164">Go toohello [Azure classic portal][lnk-classic-portal], click **Settings** in hello list of services on hello left-hand side.</span></span>
2. <span data-ttu-id="d1619-165">Selezionare la sottoscrizione di hello che desideri toochange hello directory mapping.</span><span class="sxs-lookup"><span data-stu-id="d1619-165">Select hello subscription you'd like toochange hello directory mapping to.</span></span>
3. <span data-ttu-id="d1619-166">Fare clic su **Modifica directory**.</span><span class="sxs-lookup"><span data-stu-id="d1619-166">Click **Edit Directory**.</span></span>
4. <span data-ttu-id="d1619-167">Seleziona hello **Directory** desiderato nell'elenco a discesa hello toouse.</span><span class="sxs-lookup"><span data-stu-id="d1619-167">Select hello **Directory** you would like toouse in hello dropdown.</span></span> <span data-ttu-id="d1619-168">Fare clic sulla freccia avanti hello.</span><span class="sxs-lookup"><span data-stu-id="d1619-168">Click hello forward arrow.</span></span>
5. <span data-ttu-id="d1619-169">Confermare il mapping della directory hello e coamministratori interessati.</span><span class="sxs-lookup"><span data-stu-id="d1619-169">Confirm hello directory mapping and affected co-administrators.</span></span> <span data-ttu-id="d1619-170">Se si stanno spostando da un'altra directory, vengono rimossi tutti i hello coamministratori dalla directory originale hello.</span><span class="sxs-lookup"><span data-stu-id="d1619-170">If you are moving from another directory, all hello co-administrators from hello original directory are removed.</span></span>

### <a name="im-a-domain-usermember-on-hello-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a><span data-ttu-id="d1619-171">Un utente/membro di dominio nel tenant AAD hello e ho creato una soluzione preconfigurata.</span><span class="sxs-lookup"><span data-stu-id="d1619-171">I'm a domain user/member on hello AAD tenant and I've created a preconfigured solution.</span></span> <span data-ttu-id="d1619-172">Come gli viene assegnato un ruolo per l'applicazione?</span><span class="sxs-lookup"><span data-stu-id="d1619-172">How do I get assigned a role for my application?</span></span>

<span data-ttu-id="d1619-173">Chiedere a un amministratore globale di toomake è un amministratore globale in hello AAD tenant e quindi assegnare i ruoli toousers.</span><span class="sxs-lookup"><span data-stu-id="d1619-173">Ask a global administrator toomake you a global administrator on hello AAD tenant and then assign roles toousers yourself.</span></span> <span data-ttu-id="d1619-174">In alternativa, chiedere tooassign un amministratore globale è un ruolo direttamente.</span><span class="sxs-lookup"><span data-stu-id="d1619-174">Alternatively, ask a global administrator tooassign you a role directly.</span></span> <span data-ttu-id="d1619-175">Se si desidera tenant AAD toochange hello in che è stata distribuita la soluzione preconfigurata, vedere la domanda successiva hello.</span><span class="sxs-lookup"><span data-stu-id="d1619-175">If you'd like toochange hello AAD tenant your preconfigured solution has been deployed to, see hello next question.</span></span>

### <a name="how-do-i-switch-hello-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a><span data-ttu-id="d1619-176">Come passare la soluzione preconfigurata di monitoraggio remoto e l'applicazione assegnati ai tenant AAD hello?</span><span class="sxs-lookup"><span data-stu-id="d1619-176">How do I switch hello AAD tenant my remote monitoring preconfigured solution and application are assigned to?</span></span>

<span data-ttu-id="d1619-177">È possibile eseguire una distribuzione cloud da <https://github.com/Azure/azure-iot-remote-monitoring> ed eseguire una ridistribuizione con un tenant AAD appena creato.</span><span class="sxs-lookup"><span data-stu-id="d1619-177">You can run a cloud deployment from <https://github.com/Azure/azure-iot-remote-monitoring> and redeploy with a newly created AAD tenant.</span></span> <span data-ttu-id="d1619-178">Poiché sono, per impostazione predefinita, un amministratore globale quando si crea un tenant di AAD, gli utenti tooadd le autorizzazioni e assegnare ruoli agli utenti di toothose.</span><span class="sxs-lookup"><span data-stu-id="d1619-178">Because you are, by default, a global administrator when you create an AAD tenant, you have permissions tooadd users and assign roles toothose users.</span></span>

1. <span data-ttu-id="d1619-179">Creare una directory AAD in hello [portale di Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="d1619-179">Create an AAD directory in hello [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="d1619-180">Andare troppo<https://github.com/Azure/azure-iot-remote-monitoring>.</span><span class="sxs-lookup"><span data-stu-id="d1619-180">Go too<https://github.com/Azure/azure-iot-remote-monitoring>.</span></span>
3. <span data-ttu-id="d1619-181">Eseguire `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}`. Ad esempio `build.cmd cloud debug myRMSolution`.</span><span class="sxs-lookup"><span data-stu-id="d1619-181">Run `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (For example, `build.cmd cloud debug myRMSolution`)</span></span>
4. <span data-ttu-id="d1619-182">Quando richiesto, impostare hello **tenantid** toobe tenant appena creato, anziché del tenant precedente.</span><span class="sxs-lookup"><span data-stu-id="d1619-182">When prompted, set hello **tenantid** toobe your newly created tenant instead of your previous tenant.</span></span>

### <a name="i-want-toochange-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a><span data-ttu-id="d1619-183">Voglio toochange amministratore del servizio o coamministratore quando l'accesso con un account organizzativo</span><span class="sxs-lookup"><span data-stu-id="d1619-183">I want toochange a Service Administrator or Co-Administrator when logged in with an organisational account</span></span>

<span data-ttu-id="d1619-184">Vedere l'articolo del supporto tecnico hello [modifica amministratore del servizio e coamministratore quando l'accesso con un account organizzativo][lnk-service-admins].</span><span class="sxs-lookup"><span data-stu-id="d1619-184">See hello support article [Changing Service Administrator and Co-Administrator when logged in with an organisational account][lnk-service-admins].</span></span>

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-hello-proper-permissions-toocreate-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a><span data-ttu-id="d1619-185">Perché viene visualizzato un errore simile al seguente?</span><span class="sxs-lookup"><span data-stu-id="d1619-185">Why am I seeing this error?</span></span> <span data-ttu-id="d1619-186">"L'account non dispone hello delle autorizzazioni appropriate toocreate una soluzione.</span><span class="sxs-lookup"><span data-stu-id="d1619-186">"Your account does not have hello proper permissions toocreate a solution.</span></span> <span data-ttu-id="d1619-187">Rivolgersi all'amministratore account o provare con un account diverso".</span><span class="sxs-lookup"><span data-stu-id="d1619-187">Please check with your account administrator or try with a different account."</span></span>

<span data-ttu-id="d1619-188">Esaminare hello diagramma per linee guida seguenti:</span><span class="sxs-lookup"><span data-stu-id="d1619-188">Look at hello following diagram for guidance:</span></span>

![][img-flowchart]

> [!NOTE]
> <span data-ttu-id="d1619-189">Se si continua l'errore hello toosee dopo la convalida si è un amministratore globale nel tenant AAD hello e un coamministratore della sottoscrizione di hello, chiedere all'amministratore di account rimuovere utente hello e riassegnare le autorizzazioni necessarie per questo ordine.</span><span class="sxs-lookup"><span data-stu-id="d1619-189">If you continue toosee hello error after validating you are a global administrator on hello AAD tenant and a co-administrator on hello subscription, have your account administrator remove hello user and reassign necessary permissions in this order.</span></span> <span data-ttu-id="d1619-190">Innanzitutto, aggiungere hello utente come amministratore globale e quindi aggiungere l'utente come coamministratore su hello sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1619-190">First, add hello user as a global administrator and then add user as a co-administrator on hello Azure subscription.</span></span> <span data-ttu-id="d1619-191">Se i problemi persistono, contattare il tema [Guida e supporto][lnk-help-support].</span><span class="sxs-lookup"><span data-stu-id="d1619-191">If issues persist, contact [Help & Support][lnk-help-support].</span></span>

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-toocreate-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a><span data-ttu-id="d1619-192">Perché viene visualizzato questo errore quando si dispone di una sottoscrizione di Azure?</span><span class="sxs-lookup"><span data-stu-id="d1619-192">Why am I seeing this error when I have an Azure subscription?</span></span> <span data-ttu-id="d1619-193">"Una sottoscrizione di Azure è necessario toocreate preconfigurato soluzioni.</span><span class="sxs-lookup"><span data-stu-id="d1619-193">"An Azure subscription is required toocreate pre-configured solutions.</span></span> <span data-ttu-id="d1619-194">È possibile creare un account di valutazione gratuito in pochi minuti."</span><span class="sxs-lookup"><span data-stu-id="d1619-194">You can create a free trial account in just a couple of minutes."</span></span>

<span data-ttu-id="d1619-195">Se si è certi di avere una sottoscrizione di Azure, convalidare i mapping per la sottoscrizione del tenant hello e verificare tenant corretto hello sia selezionato nell'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="d1619-195">If you're certain you have an Azure subscription, validate hello tenant mapping for your subscription and ensure hello correct tenant is selected in hello dropdown.</span></span> <span data-ttu-id="d1619-196">Se è stato convalidato hello desiderato tenant è corretto, seguire hello precedente diagramma e convalidare il mapping di hello della sottoscrizione e questo tenant AAD.</span><span class="sxs-lookup"><span data-stu-id="d1619-196">If you’ve validated hello desired tenant is correct, follow hello preceding diagram and validate hello mapping of your subscription and this AAD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1619-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d1619-197">Next steps</span></span>
<span data-ttu-id="d1619-198">toocontinue apprendendo IoT Suite, vedere come è possibile [personalizzare una soluzione preconfigurata][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="d1619-198">toocontinue learning about IoT Suite, see how you can [customize a preconfigured solution][lnk-customize].</span></span>

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-classic-portal]: https://manage.windowsazure.com/
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
