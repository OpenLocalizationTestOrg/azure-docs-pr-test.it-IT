---
title: 'Procedura: usare le password per le app in Azure MFA | Microsoft Docs'
description: Questa pagina consente agli utenti di comprendere il ruolo e la funzione delle password per le app in Azure MFA.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 1ecc2bdef5ff7ef8ed8dded7dc12428ce9657821
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a><span data-ttu-id="a2385-104">Che cosa sono le password per le app in Azure Multi-Factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="a2385-104">What are App Passwords in Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="a2385-105">Alcune applicazioni non basate su browser, come il client di posta elettronica di Apple, utilizzano Exchange Active Sync e attualmente non supportano l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="a2385-105">Certain non-browser apps, such as the Apple native email client that uses Exchange Active Sync, currently do not support multi-factor authentication.</span></span> <span data-ttu-id="a2385-106">L’autenticazione a più fattori viene abilitata per singolo utente.</span><span class="sxs-lookup"><span data-stu-id="a2385-106">Multi-factor authentication is enabled per user.</span></span>  <span data-ttu-id="a2385-107">Ciò significa che l'utente non può usare l'autenticazione a più fattori se:</span><span class="sxs-lookup"><span data-stu-id="a2385-107">This means that a user can't use multi-factor authentication if:</span></span>

- <span data-ttu-id="a2385-108">L'utente è stato abilitato per la modalità Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="a2385-108">The user has been enabled for multi-factor authentication</span></span>
- <span data-ttu-id="a2385-109">L'utente sta tentando di usare un'app non basata su browser.</span><span class="sxs-lookup"><span data-stu-id="a2385-109">The user is trying to use a non-browser app.</span></span>

<span data-ttu-id="a2385-110">Una password di app consente all'utente di usare l'app.</span><span class="sxs-lookup"><span data-stu-id="a2385-110">An app password allows the user to use the app.</span></span>

<span data-ttu-id="a2385-111">Dopo avere creato una password dell'app, è possibile usarla al posto della password originale con le applicazioni non basate su browser.</span><span class="sxs-lookup"><span data-stu-id="a2385-111">Once you have an app password, you use it in place of your original password with these non-browser apps.</span></span> <span data-ttu-id="a2385-112">Quando ci si registra per la verifica in due passaggi, si indica a Microsoft di non consentire l'accesso con la password a un utente che non possa eseguire anche la seconda verifica.</span><span class="sxs-lookup"><span data-stu-id="a2385-112">When you register for two-step verification, you're telling Microsoft not to let anyone sign in with your password if they can't also perform the second verification.</span></span> <span data-ttu-id="a2385-113">Il client di posta elettronica di Apple sul telefono non può accedere perché per questo client non è possibile richiedere la verifica in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="a2385-113">The Apple native email client on your phone can't sign in as you because it can't ask for two-step verification.</span></span> <span data-ttu-id="a2385-114">Per risolvere questo problema, creare una password di app più sicura che non si usa quotidianamente.</span><span class="sxs-lookup"><span data-stu-id="a2385-114">The solution to this problem is to create a more secure app password that you don't use day-to-day.</span></span> <span data-ttu-id="a2385-115">Le password di app sono destinate solo a tutte le app che non supportano la verifica in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="a2385-115">App passwords are only for those apps that can't support two-step verification.</span></span> <span data-ttu-id="a2385-116">Usare la password per l'app per ignorare l’autenticazione a più fattori e proseguire.</span><span class="sxs-lookup"><span data-stu-id="a2385-116">Use the app password so that apps can bypass multi-factor authentication and continue to work.</span></span>


> [!NOTE]
> <span data-ttu-id="a2385-117">I client di Office 2013, tra cui Outlook, supportano i nuovi protocolli di autenticazione e possono essere usati con la verifica in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="a2385-117">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span></span> <span data-ttu-id="a2385-118">Le password di app non vengono richieste per l'uso con i client Office 2013.</span><span class="sxs-lookup"><span data-stu-id="a2385-118">App passwords are not required for use with Office 2013 clients.</span></span>  <span data-ttu-id="a2385-119">Per altre informazioni, vedere l'[annuncio dell'anteprima pubblica dell'autenticazione moderna di Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span><span class="sxs-lookup"><span data-stu-id="a2385-119">For more information, see [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span></span>


## <a name="how-to-use-app-passwords"></a><span data-ttu-id="a2385-120">Come utilizzare le password delle app</span><span class="sxs-lookup"><span data-stu-id="a2385-120">How to use app passwords</span></span>
<span data-ttu-id="a2385-121">Informazioni importanti sulle password di app:</span><span class="sxs-lookup"><span data-stu-id="a2385-121">Here are some things to know about app passwords:</span></span>

* <span data-ttu-id="a2385-122">La password per l'app non viene creata dall'utente,</span><span class="sxs-lookup"><span data-stu-id="a2385-122">You don't create your own app passwords.</span></span> <span data-ttu-id="a2385-123">Vengono generate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a2385-123">They are automatically generated.</span></span>
* <span data-ttu-id="a2385-124">Al momento esiste un limite di 40 password per utente.</span><span class="sxs-lookup"><span data-stu-id="a2385-124">Currently there is a limit of 40 passwords per user.</span></span> 
* <span data-ttu-id="a2385-125">Se si tenta di creare una password di app dopo avere raggiunto il limite, sarà necessario eliminare una delle password di app esistenti prima di crearne una nuova.</span><span class="sxs-lookup"><span data-stu-id="a2385-125">If you try to create an app password after you have reached the limit, you'll have to delete one of your existing app passwords before you create a new one.</span></span>
* <span data-ttu-id="a2385-126">Usare una sola password per dispositivo, non per applicazione.</span><span class="sxs-lookup"><span data-stu-id="a2385-126">Use one app password per device, not per application.</span></span> <span data-ttu-id="a2385-127">Ad esempio, è possibile creare una sola password per il computer portatile e usarla per tutte le applicazioni su tale computer.</span><span class="sxs-lookup"><span data-stu-id="a2385-127">For example, you can create one app password for your laptop and use that app password for all of your applications on that laptop.</span></span> <span data-ttu-id="a2385-128">Quindi, creare una seconda password per le app da usare per tutte le app sul desktop.</span><span class="sxs-lookup"><span data-stu-id="a2385-128">Then, create a second app password to use for all your apps on your desktop.</span></span> 
* <span data-ttu-id="a2385-129">La prima volta che si esegue la registrazione per la verifica in due passaggi viene comunicata una sola password per le app.</span><span class="sxs-lookup"><span data-stu-id="a2385-129">You are given one app password the first time you register for two-step verification.</span></span>  <span data-ttu-id="a2385-130">Se sono necessarie password aggiuntive, è possibile crearle.</span><span class="sxs-lookup"><span data-stu-id="a2385-130">If you need additional ones, you can create them.</span></span>



## <a name="creating-and-deleting-app-passwords"></a><span data-ttu-id="a2385-131">Creazione ed eliminazione delle password di app</span><span class="sxs-lookup"><span data-stu-id="a2385-131">Creating and deleting app passwords</span></span>
<span data-ttu-id="a2385-132">Durante l'accesso iniziale, viene fornita una password dell'app che è possibile usare.</span><span class="sxs-lookup"><span data-stu-id="a2385-132">During your initial sign-in, you are given an app password that you can use.</span></span>  <span data-ttu-id="a2385-133">È possibile anche creare ed eliminare le password per le app in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="a2385-133">You can also create and delete app passwords later on.</span></span> <span data-ttu-id="a2385-134">La procedura di eliminazione delle password di app dipende dalla modalità di utilizzo dell'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="a2385-134">How you delete app passwords depends on how you use multi-factor authentication.</span></span> <span data-ttu-id="a2385-135">Rispondere alle domande seguenti per determinare il luogo in cui è possibile gestire le password per le app:</span><span class="sxs-lookup"><span data-stu-id="a2385-135">Answer the following questions to determine where you should go to manage app passwords:</span></span> 

1. <span data-ttu-id="a2385-136">La verifica in due passaggi viene usata per l'account Microsoft personale?</span><span class="sxs-lookup"><span data-stu-id="a2385-136">Do you use two-step verification for your personal Microsoft account?</span></span> <span data-ttu-id="a2385-137">Se sì, è consigliabile consultare l'articolo [Password per app e verifica in due passaggi](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) per avere altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="a2385-137">If yes, you should refer to the [App passwords and two-step verification](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article for help.</span></span> <span data-ttu-id="a2385-138">Altrimenti passare alla seconda domanda.</span><span class="sxs-lookup"><span data-stu-id="a2385-138">If no, continue to question two.</span></span>

2. <span data-ttu-id="a2385-139">Pertanto, la verifica in due passaggi viene usata per un account aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="a2385-139">Ok, so you use two-step verification for your work or school account.</span></span> <span data-ttu-id="a2385-140">È usata per accedere alle applicazioni di Office 365?</span><span class="sxs-lookup"><span data-stu-id="a2385-140">Do you use it to sign in to Office 365 apps?</span></span> <span data-ttu-id="a2385-141">Se sì, è consigliabile consultare [Creare una password dell'app per Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) per avere maggiori informazioni.</span><span class="sxs-lookup"><span data-stu-id="a2385-141">If yes, you should refer to [Create an app password for Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) for help.</span></span> <span data-ttu-id="a2385-142">Altrimenti passare alla terza domanda.</span><span class="sxs-lookup"><span data-stu-id="a2385-142">If no, continue to question three.</span></span> 

3. <span data-ttu-id="a2385-143">La verifica in due passaggi viene usata con Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="a2385-143">Do you use two-step verification with Microsoft Azure?</span></span> <span data-ttu-id="a2385-144">Se sì, passare alla sezione [Gestione delle password per le app nel Portale di Azure](#manage-app-passwords-in-the-Azure-portal) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a2385-144">If yes, continue to the [Manage app passwords in the Azure portal](#manage-app-passwords-in-the-Azure-portal) section of this article.</span></span> <span data-ttu-id="a2385-145">Altrimenti passare alla quarta domanda.</span><span class="sxs-lookup"><span data-stu-id="a2385-145">If no, continue to question four.</span></span>

4. <span data-ttu-id="a2385-146">Non si è sicuri su dove venga usata la verifica in due passaggi?</span><span class="sxs-lookup"><span data-stu-id="a2385-146">Not sure where you use two-step verification?</span></span> <span data-ttu-id="a2385-147">Passare alla sezione [Gestione delle password per le app nel Portale MyApps](#manage-app-passwords-with-the-myapps-portal) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a2385-147">Continue to the [Manage app passwords with the MyApps portal](#manage-app-passwords-with-the-myapps-portal) section of this article.</span></span> 


## <a name="manage-app-passwords-in-the-azure-portal"></a><span data-ttu-id="a2385-148">Gestione delle password per le app nel Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a2385-148">Manage app passwords in the Azure portal</span></span>
<span data-ttu-id="a2385-149">Se si usa la verifica in due passaggi con Azure, è consigliabile creare password per le app tramite il Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a2385-149">If you use two-step verification with Azure, you want to create app passwords through the Azure portal.</span></span>

### <a name="to-create-app-passwords-in-the-azure-portal"></a><span data-ttu-id="a2385-150">Per creare password dell'app nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a2385-150">To create app passwords in the Azure portal</span></span>
1. <span data-ttu-id="a2385-151">Accedere al portale di Microsoft Azure classico.</span><span class="sxs-lookup"><span data-stu-id="a2385-151">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="a2385-152">Nella parte superiore fare clic con il pulsante destro del mouse sul nome utente, quindi scegliere Verifica aggiuntiva di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="a2385-152">At the top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="a2385-153">Nella parte superiore della pagina di verifica selezionare le password dell'app.</span><span class="sxs-lookup"><span data-stu-id="a2385-153">On the proofup page, at the top, select app passwords</span></span>
4. <span data-ttu-id="a2385-154">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a2385-154">Click **Create**.</span></span>
5. <span data-ttu-id="a2385-155">Immettere un nome per la password dell'app e quindi fare clic su **Avanti**</span><span class="sxs-lookup"><span data-stu-id="a2385-155">Enter a name for the app password and click **Next**</span></span>
6. <span data-ttu-id="a2385-156">Copiare la password per l'app negli Appunti, quindi incollarla nell'app.</span><span class="sxs-lookup"><span data-stu-id="a2385-156">Copy the app password to the clipboard and paste it into your app.</span></span>
   
   ![Cloud](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="to-delete-app-passwords-in-the-azure-portal"></a><span data-ttu-id="a2385-158">Per eliminare password per le app nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a2385-158">To delete app passwords in the Azure portal</span></span>
1. <span data-ttu-id="a2385-159">Accedere al portale di Microsoft Azure classico.</span><span class="sxs-lookup"><span data-stu-id="a2385-159">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="a2385-160">Nella parte superiore fare clic con il pulsante destro del mouse sul nome utente, quindi scegliere Verifica aggiuntiva di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="a2385-160">At the top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="a2385-161">Nella parte superiore, accanto alla verifica aggiuntiva di sicurezza, fare clic su **Password dell'app.**</span><span class="sxs-lookup"><span data-stu-id="a2385-161">At the top, next to additional security verification, select **app passwords.**</span></span>
4. <span data-ttu-id="a2385-162">Accanto alla password dell’app che si desidera rimuovere, selezionare **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="a2385-162">Next to the app password you want to delete, select **Delete**.</span></span>
5. <span data-ttu-id="a2385-163">Confermare l'eliminazione facendo clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="a2385-163">Confirm the deletion by clicking **yes**.</span></span>
6. <span data-ttu-id="a2385-164">Dopo che la password dell’app è stata eliminata, è possibile fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="a2385-164">Once the app password is deleted, you can click **close**.</span></span>


## <a name="manage-app-passwords-with-the-myapps-portal"></a><span data-ttu-id="a2385-165">Gestione delle password per le app nel portale MyApps.</span><span class="sxs-lookup"><span data-stu-id="a2385-165">Manage app passwords with the MyApps portal.</span></span>
<span data-ttu-id="a2385-166">Se non si è certi di come utilizzare Multi-Factor Authentication, è sempre possibile creare ed eliminare le password per le app tramite il portale Myapps.</span><span class="sxs-lookup"><span data-stu-id="a2385-166">If you are not sure how you use multi-factor authentication, then you can always create and delete app passwords through the myapps portal.</span></span>

### <a name="to-create-an-app-password-using-the-myapps-portal"></a><span data-ttu-id="a2385-167">Per creare una password di app tramite il portale Myapps</span><span class="sxs-lookup"><span data-stu-id="a2385-167">To create an app password using the Myapps portal</span></span>
1. <span data-ttu-id="a2385-168">Effettuare l'accesso ad [https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="a2385-168">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="a2385-169">Fare clic sul nome in alto a destra e scegliere **Profilo**.</span><span class="sxs-lookup"><span data-stu-id="a2385-169">Click your name at the top right, and choose **Profile**.</span></span>
3. <span data-ttu-id="a2385-170">Selezionare **Verifica aggiuntiva di sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="a2385-170">Select **Additional Security Verification**.</span></span>
   <span data-ttu-id="a2385-171">![Selezionare Verifica aggiuntiva di sicurezza: schermata](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span><span class="sxs-lookup"><span data-stu-id="a2385-171">![Select additional security verification - screenshot](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span></span>

4. <span data-ttu-id="a2385-172">Selezionare **Password delle app**.</span><span class="sxs-lookup"><span data-stu-id="a2385-172">Select **app passwords**.</span></span>
   <span data-ttu-id="a2385-173">![Selezionare le password per le app: schermata](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span><span class="sxs-lookup"><span data-stu-id="a2385-173">![Select app passwords - screenshot](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span></span>

5. <span data-ttu-id="a2385-174">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a2385-174">Click **Create**.</span></span>
6. <span data-ttu-id="a2385-175">Immettere un nome per la password dell'app e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a2385-175">Enter a name for the app password and click **Next**.</span></span>
7. <span data-ttu-id="a2385-176">Copiare la password dell'app negli Appunti, quindi incollarla nell'app.</span><span class="sxs-lookup"><span data-stu-id="a2385-176">Copy the app password to the clipboard and paste it into your app.</span></span>
   <span data-ttu-id="a2385-177">![Creare la password di un'app](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span><span class="sxs-lookup"><span data-stu-id="a2385-177">![Create an app password](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span></span>

### <a name="to-delete-an-app-password-using-the-myapps-portal"></a><span data-ttu-id="a2385-178">Per eliminare una password di app tramite il portale Myapps</span><span class="sxs-lookup"><span data-stu-id="a2385-178">To delete an app password using the Myapps portal</span></span>
1. <span data-ttu-id="a2385-179">Effettuare l'accesso ad [https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="a2385-179">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="a2385-180">Nella parte superiore selezionare il profilo.</span><span class="sxs-lookup"><span data-stu-id="a2385-180">At the top, select profile.</span></span>
3. <span data-ttu-id="a2385-181">Selezionare **Verifica aggiuntiva di sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="a2385-181">Select **Additional Security Verification**.</span></span>

   ![Selezionare Verifica aggiuntiva di sicurezza: schermata](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. <span data-ttu-id="a2385-183">Selezionare **Password delle app**.</span><span class="sxs-lookup"><span data-stu-id="a2385-183">Select **app passwords**.</span></span>

   ![Selezionare le password per le app: schermata](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. <span data-ttu-id="a2385-185">Accanto alla password dell’app che si desidera rimuovere, selezionare **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="a2385-185">Next to the app password you want to delete, click **Delete**.</span></span>

   ![Eliminare una password di app](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. <span data-ttu-id="a2385-187">Confermare che si desidera eliminare la password facendo clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="a2385-187">Confirm that you want to delete that password by clicking **yes**.</span></span>
7. <span data-ttu-id="a2385-188">Dopo che la password dell’app è stata eliminata, è possibile fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="a2385-188">Once the app password is deleted, you can click **close**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2385-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a2385-189">Next steps</span></span>

- [<span data-ttu-id="a2385-190">Gestire le impostazioni della verifica in due passaggi</span><span class="sxs-lookup"><span data-stu-id="a2385-190">Manage your two-step verification settings</span></span>](multi-factor-authentication-end-user-manage-settings.md)

- <span data-ttu-id="a2385-191">Provare l'[app Microsoft Authenticator](microsoft-authenticator-app-how-to.md) per verificare gli accessi con le notifiche delle app, invece di ricevere messaggi o chiamate.</span><span class="sxs-lookup"><span data-stu-id="a2385-191">Try out the [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) to verify your sign-ins with app notifications, instead of receiving texts or calls.</span></span> 
