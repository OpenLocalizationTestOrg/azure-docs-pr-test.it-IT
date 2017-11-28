---
title: aaaHow toouse le password di App di Azure MFA? | Microsoft Docs
description: "Questa pagina consente agli utenti comprendere quali sono le password di app e quali sono utilizzati per con considerare tooAzure autenticazione a più fattori."
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
ms.openlocfilehash: 3afa2003d8e87576f035bf9440a1dba67bd85f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a><span data-ttu-id="a1a3e-104">Che cosa sono le password per le app in Azure Multi-Factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="a1a3e-104">What are App Passwords in Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="a1a3e-105">Alcune App non basate su browser, ad esempio, client di posta elettronica native Apple hello che usa Exchange Active Sync, attualmente non supportano l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-105">Certain non-browser apps, such as hello Apple native email client that uses Exchange Active Sync, currently do not support multi-factor authentication.</span></span> <span data-ttu-id="a1a3e-106">L’autenticazione a più fattori viene abilitata per singolo utente.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-106">Multi-factor authentication is enabled per user.</span></span>  <span data-ttu-id="a1a3e-107">Ciò significa che l'utente non può usare l'autenticazione a più fattori se:</span><span class="sxs-lookup"><span data-stu-id="a1a3e-107">This means that a user can't use multi-factor authentication if:</span></span>

- <span data-ttu-id="a1a3e-108">Hello utente è abilitato per multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="a1a3e-108">hello user has been enabled for multi-factor authentication</span></span>
- <span data-ttu-id="a1a3e-109">utente Hello tenta toouse un'app non basate su browser.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-109">hello user is trying toouse a non-browser app.</span></span>

<span data-ttu-id="a1a3e-110">Una password di app consente hello utente toouse hello app.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-110">An app password allows hello user toouse hello app.</span></span>

<span data-ttu-id="a1a3e-111">Dopo avere creato una password dell'app, è possibile usarla al posto della password originale con le applicazioni non basate su browser.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-111">Once you have an app password, you use it in place of your original password with these non-browser apps.</span></span> <span data-ttu-id="a1a3e-112">Quando si registra per la verifica in due passaggi, si sta indica Microsoft non toolet tutti gli utenti di accedere con la password se non possono inoltre eseguire la verifica di hello secondo.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-112">When you register for two-step verification, you're telling Microsoft not toolet anyone sign in with your password if they can't also perform hello second verification.</span></span> <span data-ttu-id="a1a3e-113">client di posta elettronica native Apple Hello sul telefono non è possibile accedere come si perché non è possibile richiedere la verifica in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-113">hello Apple native email client on your phone can't sign in as you because it can't ask for two-step verification.</span></span> <span data-ttu-id="a1a3e-114">soluzione toothis problema Hello è una password più sicura di app che non si utilizza toocreate quotidiane.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-114">hello solution toothis problem is toocreate a more secure app password that you don't use day-to-day.</span></span> <span data-ttu-id="a1a3e-115">Le password di app sono destinate solo a tutte le app che non supportano la verifica in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-115">App passwords are only for those apps that can't support two-step verification.</span></span> <span data-ttu-id="a1a3e-116">Utilizzare password dell'app hello in modo che le applicazioni possono ignorare multi-factor authentication e continuare toowork.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-116">Use hello app password so that apps can bypass multi-factor authentication and continue toowork.</span></span>


> [!NOTE]
> <span data-ttu-id="a1a3e-117">I client di Office 2013, tra cui Outlook, supportano i nuovi protocolli di autenticazione e possono essere usati con la verifica in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-117">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span></span> <span data-ttu-id="a1a3e-118">Le password di app non vengono richieste per l'uso con i client Office 2013.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-118">App passwords are not required for use with Office 2013 clients.</span></span>  <span data-ttu-id="a1a3e-119">Per altre informazioni, vedere l'[annuncio dell'anteprima pubblica dell'autenticazione moderna di Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span><span class="sxs-lookup"><span data-stu-id="a1a3e-119">For more information, see [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span></span>


## <a name="how-toouse-app-passwords"></a><span data-ttu-id="a1a3e-120">Come le password di app toouse</span><span class="sxs-lookup"><span data-stu-id="a1a3e-120">How toouse app passwords</span></span>
<span data-ttu-id="a1a3e-121">Ecco alcuni aspetti tooknow sulle password di app:</span><span class="sxs-lookup"><span data-stu-id="a1a3e-121">Here are some things tooknow about app passwords:</span></span>

* <span data-ttu-id="a1a3e-122">La password per l'app non viene creata dall'utente,</span><span class="sxs-lookup"><span data-stu-id="a1a3e-122">You don't create your own app passwords.</span></span> <span data-ttu-id="a1a3e-123">Vengono generate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-123">They are automatically generated.</span></span>
* <span data-ttu-id="a1a3e-124">Al momento esiste un limite di 40 password per utente.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-124">Currently there is a limit of 40 passwords per user.</span></span> 
* <span data-ttu-id="a1a3e-125">Se si tenta di toocreate una password dell'app dopo aver raggiunto il limite di hello, sarà necessario toodelete una delle password esistenti prima di creare una nuova.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-125">If you try toocreate an app password after you have reached hello limit, you'll have toodelete one of your existing app passwords before you create a new one.</span></span>
* <span data-ttu-id="a1a3e-126">Usare una sola password per dispositivo, non per applicazione.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-126">Use one app password per device, not per application.</span></span> <span data-ttu-id="a1a3e-127">Ad esempio, è possibile creare una sola password per il computer portatile e usarla per tutte le applicazioni su tale computer.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-127">For example, you can create one app password for your laptop and use that app password for all of your applications on that laptop.</span></span> <span data-ttu-id="a1a3e-128">Creare quindi un secondo toouse password di app per tutte le app sul desktop.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-128">Then, create a second app password toouse for all your apps on your desktop.</span></span> 
* <span data-ttu-id="a1a3e-129">È possibile hello password di app una prima volta che si registra per la verifica in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-129">You are given one app password hello first time you register for two-step verification.</span></span>  <span data-ttu-id="a1a3e-130">Se sono necessarie password aggiuntive, è possibile crearle.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-130">If you need additional ones, you can create them.</span></span>



## <a name="creating-and-deleting-app-passwords"></a><span data-ttu-id="a1a3e-131">Creazione ed eliminazione delle password di app</span><span class="sxs-lookup"><span data-stu-id="a1a3e-131">Creating and deleting app passwords</span></span>
<span data-ttu-id="a1a3e-132">Durante l'accesso iniziale, viene fornita una password dell'app che è possibile usare.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-132">During your initial sign-in, you are given an app password that you can use.</span></span>  <span data-ttu-id="a1a3e-133">È possibile anche creare ed eliminare le password per le app in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-133">You can also create and delete app passwords later on.</span></span> <span data-ttu-id="a1a3e-134">La procedura di eliminazione delle password di app dipende dalla modalità di utilizzo dell'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-134">How you delete app passwords depends on how you use multi-factor authentication.</span></span> <span data-ttu-id="a1a3e-135">Hello risposte seguenti domande toodetermine in cui è necessario usare password di app toomanage:</span><span class="sxs-lookup"><span data-stu-id="a1a3e-135">Answer hello following questions toodetermine where you should go toomanage app passwords:</span></span> 

1. <span data-ttu-id="a1a3e-136">La verifica in due passaggi viene usata per l'account Microsoft personale?</span><span class="sxs-lookup"><span data-stu-id="a1a3e-136">Do you use two-step verification for your personal Microsoft account?</span></span> <span data-ttu-id="a1a3e-137">In caso affermativo, è consigliabile consultare toohello [verifica in due passaggi e le password di App](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) articolo per la Guida.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-137">If yes, you should refer toohello [App passwords and two-step verification](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article for help.</span></span> <span data-ttu-id="a1a3e-138">Se no, continua tooquestion due.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-138">If no, continue tooquestion two.</span></span>

2. <span data-ttu-id="a1a3e-139">Pertanto, la verifica in due passaggi viene usata per un account aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-139">Ok, so you use two-step verification for your work or school account.</span></span> <span data-ttu-id="a1a3e-140">Utilizzi toosign nelle App tooOffice 365?</span><span class="sxs-lookup"><span data-stu-id="a1a3e-140">Do you use it toosign in tooOffice 365 apps?</span></span> <span data-ttu-id="a1a3e-141">In caso affermativo, è consigliabile consultare troppo[creare una password di app per Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) per assistenza.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-141">If yes, you should refer too[Create an app password for Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) for help.</span></span> <span data-ttu-id="a1a3e-142">Se no, continua tooquestion tre.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-142">If no, continue tooquestion three.</span></span> 

3. <span data-ttu-id="a1a3e-143">La verifica in due passaggi viene usata con Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="a1a3e-143">Do you use two-step verification with Microsoft Azure?</span></span> <span data-ttu-id="a1a3e-144">In caso affermativo, continuare toohello [gestione delle password di app nel portale di Azure hello](#manage-app-passwords-in-the-Azure-portal) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-144">If yes, continue toohello [Manage app passwords in hello Azure portal](#manage-app-passwords-in-the-Azure-portal) section of this article.</span></span> <span data-ttu-id="a1a3e-145">Se no, continua tooquestion quattro.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-145">If no, continue tooquestion four.</span></span>

4. <span data-ttu-id="a1a3e-146">Non si è sicuri su dove venga usata la verifica in due passaggi?</span><span class="sxs-lookup"><span data-stu-id="a1a3e-146">Not sure where you use two-step verification?</span></span> <span data-ttu-id="a1a3e-147">Continuare toohello [gestione delle password di app con il portale MyApps hello](#manage-app-passwords-with-the-myapps-portal) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-147">Continue toohello [Manage app passwords with hello MyApps portal](#manage-app-passwords-with-the-myapps-portal) section of this article.</span></span> 


## <a name="manage-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="a1a3e-148">Gestione delle password di app nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="a1a3e-148">Manage app passwords in hello Azure portal</span></span>
<span data-ttu-id="a1a3e-149">Se si usa verifica in due passaggi con Azure, è necessario toocreate le password di app tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-149">If you use two-step verification with Azure, you want toocreate app passwords through hello Azure portal.</span></span>

### <a name="toocreate-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="a1a3e-150">password di app toocreate in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a1a3e-150">toocreate app passwords in hello Azure portal</span></span>
1. <span data-ttu-id="a1a3e-151">Accedi toohello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-151">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="a1a3e-152">Nella parte superiore di hello, fare doppio clic su nome utente e selezionare verifica aggiuntiva di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-152">At hello top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="a1a3e-153">Nella pagina di verifica hello, nella parte superiore di hello, selezionare le password di app</span><span class="sxs-lookup"><span data-stu-id="a1a3e-153">On hello proofup page, at hello top, select app passwords</span></span>
4. <span data-ttu-id="a1a3e-154">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-154">Click **Create**.</span></span>
5. <span data-ttu-id="a1a3e-155">Immettere un nome per la password di app hello e fare clic su **successivo**</span><span class="sxs-lookup"><span data-stu-id="a1a3e-155">Enter a name for hello app password and click **Next**</span></span>
6. <span data-ttu-id="a1a3e-156">Copiare negli Appunti toohello password di app hello e incollarlo nell'app.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-156">Copy hello app password toohello clipboard and paste it into your app.</span></span>
   
   ![Cloud](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="toodelete-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="a1a3e-158">password di app toodelete in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a1a3e-158">toodelete app passwords in hello Azure portal</span></span>
1. <span data-ttu-id="a1a3e-159">Accedi toohello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-159">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="a1a3e-160">Nella parte superiore di hello, fare doppio clic su nome utente e selezionare verifica aggiuntiva di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-160">At hello top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="a1a3e-161">Nella parte superiore di hello, verifica di sicurezza tooadditional successiva, selezionare **le password di app.**</span><span class="sxs-lookup"><span data-stu-id="a1a3e-161">At hello top, next tooadditional security verification, select **app passwords.**</span></span>
4. <span data-ttu-id="a1a3e-162">Password di app toohello successiva da toodelete, selezionare **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-162">Next toohello app password you want toodelete, select **Delete**.</span></span>
5. <span data-ttu-id="a1a3e-163">Confermare l'eliminazione di hello facendo **Sì**.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-163">Confirm hello deletion by clicking **yes**.</span></span>
6. <span data-ttu-id="a1a3e-164">Una volta la password di app hello viene eliminata, è possibile fare clic su **chiudere**.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-164">Once hello app password is deleted, you can click **close**.</span></span>


## <a name="manage-app-passwords-with-hello-myapps-portal"></a><span data-ttu-id="a1a3e-165">Gestione delle password di app con il portale MyApps hello.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-165">Manage app passwords with hello MyApps portal.</span></span>
<span data-ttu-id="a1a3e-166">Se non sei sicuro come si utilizza l'autenticazione a più fattori, quindi è possibile creare ed eliminare le password di app tramite il portale di myapps hello.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-166">If you are not sure how you use multi-factor authentication, then you can always create and delete app passwords through hello myapps portal.</span></span>

### <a name="toocreate-an-app-password-using-hello-myapps-portal"></a><span data-ttu-id="a1a3e-167">una password di app utilizzando toocreate hello portale Myapps</span><span class="sxs-lookup"><span data-stu-id="a1a3e-167">toocreate an app password using hello Myapps portal</span></span>
1. <span data-ttu-id="a1a3e-168">Accedi troppo[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="a1a3e-168">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="a1a3e-169">Fare clic sul nome in alto a destra hello e scegliere **profilo**.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-169">Click your name at hello top right, and choose **Profile**.</span></span>
3. <span data-ttu-id="a1a3e-170">Selezionare **Verifica aggiuntiva di sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-170">Select **Additional Security Verification**.</span></span>
   <span data-ttu-id="a1a3e-171">![Selezionare Verifica aggiuntiva di sicurezza: schermata](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span><span class="sxs-lookup"><span data-stu-id="a1a3e-171">![Select additional security verification - screenshot](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span></span>

4. <span data-ttu-id="a1a3e-172">Selezionare **Password delle app**.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-172">Select **app passwords**.</span></span>
   <span data-ttu-id="a1a3e-173">![Selezionare le password per le app: schermata](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span><span class="sxs-lookup"><span data-stu-id="a1a3e-173">![Select app passwords - screenshot](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span></span>

5. <span data-ttu-id="a1a3e-174">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-174">Click **Create**.</span></span>
6. <span data-ttu-id="a1a3e-175">Immettere un nome per la password di app hello e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-175">Enter a name for hello app password and click **Next**.</span></span>
7. <span data-ttu-id="a1a3e-176">Copiare negli Appunti toohello password di app hello e incollarlo nell'app.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-176">Copy hello app password toohello clipboard and paste it into your app.</span></span>
   <span data-ttu-id="a1a3e-177">![Creare una password di app](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span><span class="sxs-lookup"><span data-stu-id="a1a3e-177">![Create an app password](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span></span>

### <a name="toodelete-an-app-password-using-hello-myapps-portal"></a><span data-ttu-id="a1a3e-178">una password di app utilizzando toodelete hello portale Myapps</span><span class="sxs-lookup"><span data-stu-id="a1a3e-178">toodelete an app password using hello Myapps portal</span></span>
1. <span data-ttu-id="a1a3e-179">Accedi troppo[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="a1a3e-179">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="a1a3e-180">Nella parte superiore di hello, selezionare il profilo.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-180">At hello top, select profile.</span></span>
3. <span data-ttu-id="a1a3e-181">Selezionare **Verifica aggiuntiva di sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-181">Select **Additional Security Verification**.</span></span>

   ![Selezionare Verifica aggiuntiva di sicurezza: schermata](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. <span data-ttu-id="a1a3e-183">Selezionare **Password delle app**.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-183">Select **app passwords**.</span></span>

   ![Selezionare le password per le app: schermata](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. <span data-ttu-id="a1a3e-185">Fare clic su Avanti password di app toohello da toodelete, **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-185">Next toohello app password you want toodelete, click **Delete**.</span></span>

   ![Eliminare una password di app](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. <span data-ttu-id="a1a3e-187">Confermare che si desidera toodelete che la password facendo clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-187">Confirm that you want toodelete that password by clicking **yes**.</span></span>
7. <span data-ttu-id="a1a3e-188">Una volta la password di app hello viene eliminata, è possibile fare clic su **chiudere**.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-188">Once hello app password is deleted, you can click **close**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1a3e-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a1a3e-189">Next steps</span></span>

- [<span data-ttu-id="a1a3e-190">Gestire le impostazioni della verifica in due passaggi</span><span class="sxs-lookup"><span data-stu-id="a1a3e-190">Manage your two-step verification settings</span></span>](multi-factor-authentication-end-user-manage-settings.md)

- <span data-ttu-id="a1a3e-191">Provare a hello [app Authenticator Microsoft](microsoft-authenticator-app-how-to.md) tooverify gli accessi con le notifiche dell'app, anziché la ricezione di testi o chiamate.</span><span class="sxs-lookup"><span data-stu-id="a1a3e-191">Try out hello [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) tooverify your sign-ins with app notifications, instead of receiving texts or calls.</span></span> 
