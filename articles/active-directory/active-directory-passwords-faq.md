---
title: 'Domande frequenti: reimpostazione della password self-service di Azure AD | Microsoft Docs'
description: Domande frequenti su sulla reimpostazione della password self-service di Azure AD
services: active-directory
keywords: gestione delle password in Active Directory, gestione delle password, reimpostazione della password self-service di Azure AD
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: b3fab99ff9fab5bc67fa70113dc5b06fac775b09
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="7749f-104">Domande frequenti sulla gestione delle password</span><span class="sxs-lookup"><span data-stu-id="7749f-104">Password management frequently asked questions</span></span>

<span data-ttu-id="7749f-105">Di seguito sono riportate alcune domande frequenti su tutti gli aspetti riguardanti la reimpostazione delle password.</span><span class="sxs-lookup"><span data-stu-id="7749f-105">The following are some frequently asked questions for all things related to password reset.</span></span>

<span data-ttu-id="7749f-106">In caso di domande generiche su Azure AD e la reimpostazione della password self-service per cui non è possibile trovare una risposta qui, è possibile richiedere assistenza alla community sui [forum di Azure AD](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span><span class="sxs-lookup"><span data-stu-id="7749f-106">If you have a general question about Azure AD and self-service password reset, that is not answered here, you can ask the community for assistance on the [Azure Ad forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span></span> <span data-ttu-id="7749f-107">La community è composta da ingegneri, responsabili dei prodotti, MVP e informatici.</span><span class="sxs-lookup"><span data-stu-id="7749f-107">Members of the community include Engineers, Product Managers, MVPs, and fellow IT Professionals.</span></span>

<span data-ttu-id="7749f-108">Questo articolo di domande frequenti è suddiviso nelle sezioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7749f-108">This FAQ is split into the following sections:</span></span>

* [<span data-ttu-id="7749f-109">**Domande sulla registrazione per la reimpostazione della password**</span><span class="sxs-lookup"><span data-stu-id="7749f-109">**Questions about Password Reset Registration**</span></span>](#password-reset-registration)
* [<span data-ttu-id="7749f-110">**Domande sulla reimpostazione della password**</span><span class="sxs-lookup"><span data-stu-id="7749f-110">**Questions about Password Reset**</span></span>](#password-reset)
* [<span data-ttu-id="7749f-111">**Domande sulla modifica della password**</span><span class="sxs-lookup"><span data-stu-id="7749f-111">**Questions about Password Change**</span></span>](#password-change)
* [<span data-ttu-id="7749f-112">**Domande relative ai report di gestione delle password**</span><span class="sxs-lookup"><span data-stu-id="7749f-112">**Questions about password management Reports**</span></span>](#password-management-reports)
* [<span data-ttu-id="7749f-113">**Domande sul writeback delle password**</span><span class="sxs-lookup"><span data-stu-id="7749f-113">**Questions about password writeback**</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="7749f-114">Registrazione per la reimpostazione della password</span><span class="sxs-lookup"><span data-stu-id="7749f-114">Password reset registration</span></span>
* <span data-ttu-id="7749f-115">**D: Gli utenti possono registrare i propri dati per la reimpostazione della password?**</span><span class="sxs-lookup"><span data-stu-id="7749f-115">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="7749f-116">**R:** Sì, a condizione che la reimpostazione della password sia abilitata, gli utenti con licenza possono accedere al portale di registrazione per la reimpostazione della password all'indirizzo http://aka.ms/ssprsetup per registrare le informazioni di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="7749f-116">**A:** Yes, as long as password reset is enabled and they are licensed, they can go to the Password Reset Registration portal at http://aka.ms/ssprsetup to register their authentication information.</span></span> <span data-ttu-id="7749f-117">Gli utenti possono anche registrarsi tramite il pannello di accesso all'indirizzo http://myapps.microsoft.com, facendo clic sulla scheda del profilo e scegliendo l'opzione Esegui la registrazione per la reimpostazione della password.</span><span class="sxs-lookup"><span data-stu-id="7749f-117">Users can also register by going to the access panel at http://myapps.microsoft.com, clicking the profile tab, and clicking the Register for Password Reset option.</span></span>
  >
  >
* <span data-ttu-id="7749f-118">**D: è possibile definire i dati di reimpostazione della password per conto degli utenti?**</span><span class="sxs-lookup"><span data-stu-id="7749f-118">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="7749f-119">**R:** Sì, è possibile farlo con Azure AD Connect, PowerShell, con il [portale di Azure](https://portal.azure.com) o tramite l'interfaccia di amministrazione di Office.</span><span class="sxs-lookup"><span data-stu-id="7749f-119">**A:** Yes, you can do so with Azure AD Connect, PowerShell, the [Azure portal](https://portal.azure.com), or the Office Admin portal.</span></span> <span data-ttu-id="7749f-120">Per altre informazioni, vedere l'articolo [Dati usati dal servizio di reimpostazione della password self-service di Azure AD](active-directory-passwords-data.md).</span><span class="sxs-lookup"><span data-stu-id="7749f-120">For more information, see the article [Data used by Azure AD Self-Service Password Reset](active-directory-passwords-data.md).</span></span>
  >
  >
* <span data-ttu-id="7749f-121">**D: È possibile sincronizzare i dati per le domande di sicurezza dall'ambiente locale?**</span><span class="sxs-lookup"><span data-stu-id="7749f-121">**Q:  Can I synchronize data for security questions from on premises?**</span></span>

  > <span data-ttu-id="7749f-122">**R:** Attualmente non è possibile.</span><span class="sxs-lookup"><span data-stu-id="7749f-122">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="7749f-123">**D: Gli utenti possono registrare i dati in modo che non siano visibili ad altri utenti?**</span><span class="sxs-lookup"><span data-stu-id="7749f-123">**Q:  Can my users register data in such a way that other users cannot see this data?**</span></span>

  > <span data-ttu-id="7749f-124">**R:** Sì. I dati che gli utenti registrano tramite il portale di registrazione per la reimpostazione della password vengono salvati in campi di autenticazione privati visibili solo agli amministratori globali e agli utenti.</span><span class="sxs-lookup"><span data-stu-id="7749f-124">**A:** Yes, when users register data using the Password Reset Registration Portal it is saved into private authentication fields that are only visible by Global Administrators and the user.</span></span>
    >
    > [!NOTE]
    > <span data-ttu-id="7749f-125">Se un **account amministratore di Azure** registra il numero di telefono di autenticazione, questo viene inserito anche nel campo Cellulare ed è visibile.</span><span class="sxs-lookup"><span data-stu-id="7749f-125">If an **Azure Administrator account** registers their authentication phone number it is also populated into the mobile phone field and is visible.</span></span>
    >
  >
  >
* <span data-ttu-id="7749f-126">**D: Gli utenti devono essere registrati prima di poter usare la funzionalità di reimpostazione della password?**</span><span class="sxs-lookup"><span data-stu-id="7749f-126">**Q:  Do my users have to be registered before they can use password reset?**</span></span>

  > <span data-ttu-id="7749f-127">**R:** No. Se le informazioni di autenticazione definite per conto degli utenti sono sufficienti, gli utenti non dovranno registrarsi.</span><span class="sxs-lookup"><span data-stu-id="7749f-127">**A:** No, if you define enough authentication information on their behalf, users do not have to register.</span></span> <span data-ttu-id="7749f-128">La reimpostazione della password funziona purché i dati archiviati nei campi appropriati nella directory siano formattati correttamente.</span><span class="sxs-lookup"><span data-stu-id="7749f-128">Password reset works as long as you have properly formatted data stored in the appropriate fields in the directory.</span></span>
  >
  >
* <span data-ttu-id="7749f-129">**D: È possibile sincronizzare o impostare i campi Telefono per l'autenticazione, Indirizzo di posta elettronica per l'autenticazione o Telefono di autenticazione alternativo per conto degli utenti?**</span><span class="sxs-lookup"><span data-stu-id="7749f-129">**Q:  Can I synchronize or set the Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="7749f-130">**R:** Attualmente non è possibile.</span><span class="sxs-lookup"><span data-stu-id="7749f-130">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="7749f-131">**D: In che modo il portale di registrazione riconosce le opzioni da visualizzare agli utenti?**</span><span class="sxs-lookup"><span data-stu-id="7749f-131">**Q:  How does the registration portal know which options to show my users?**</span></span>

  > <span data-ttu-id="7749f-132">**R:** Il portale di registrazione per la reimpostazione delle password mostra solo le opzioni che sono state abilitate per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="7749f-132">**A:** The password reset registration portal only shows the options that you have enabled for your users.</span></span> <span data-ttu-id="7749f-133">Queste opzioni si trovano nella sezione Criteri di reimpostazione password utente della scheda Configura relativa alla directory.</span><span class="sxs-lookup"><span data-stu-id="7749f-133">These options are found under the User Password Reset Policy section of your directory’s Configure tab.</span></span> <span data-ttu-id="7749f-134">Di conseguenza, se ad esempio non si abilitano le domande di sicurezza, gli utenti non possono registrarsi per questa opzione.</span><span class="sxs-lookup"><span data-stu-id="7749f-134">For example, this means that if you do not enable security questions, then users are not able to register for that option.</span></span>
  >
  >
* <span data-ttu-id="7749f-135">**D: Quando un utente viene considerato registrato?**</span><span class="sxs-lookup"><span data-stu-id="7749f-135">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="7749f-136">**R:** Un utente viene considerato registrato per la reimpostazione della password self-service quando è stato registrato almeno il **numero di metodi necessari per la reimpostazione** impostato nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7749f-136">**A:** A user is considered registered for SSPR when they have registered at least the **Number of methods required to reset** that you have set in the [Azure portal](https://portal.azure.com).</span></span>
  >
  >
## <a name="password-reset"></a><span data-ttu-id="7749f-137">Reimpostazione delle password</span><span class="sxs-lookup"><span data-stu-id="7749f-137">Password reset</span></span>
* <span data-ttu-id="7749f-138">**D: Quanto tempo occorre attendere prima di ricevere un messaggio di posta elettronica, un SMS o una telefonata relativa alla reimpostazione della password?**</span><span class="sxs-lookup"><span data-stu-id="7749f-138">**Q:  How long should I wait to receive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="7749f-139">**R:** I messaggi di posta elettronica, gli SMS e le telefonate dovrebbero arrivare entro un minuto, normalmente tra 5 e 20 secondi.</span><span class="sxs-lookup"><span data-stu-id="7749f-139">**A:** Email, SMS messages, and phone calls should arrive in under one minute, with the normal case being 5-20 seconds.</span></span>
    ><span data-ttu-id="7749f-140">Se non si riceve la notifica entro questo periodo di tempo:</span><span class="sxs-lookup"><span data-stu-id="7749f-140">If you do not receive the notification in this time frame:</span></span>
        > * <span data-ttu-id="7749f-141">Controllare la cartella della posta indesiderata.</span><span class="sxs-lookup"><span data-stu-id="7749f-141">Check your junk folder.</span></span>
        > * <span data-ttu-id="7749f-142">Controllare che il numero o il messaggio di posta elettronica contattato sia quello che previsto.</span><span class="sxs-lookup"><span data-stu-id="7749f-142">Check the number or email being contacted is the one you expect.</span></span>
        > * <span data-ttu-id="7749f-143">Controllare che i dati di autenticazione nella directory siano formattati correttamente.</span><span class="sxs-lookup"><span data-stu-id="7749f-143">Check the authentication data in the directory is correctly formatted.</span></span>
                >     * <span data-ttu-id="7749f-144">Esempio: "+1 4255551234" o "user@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="7749f-144">Example: "+1 4255551234" or "user@contoso.com"</span></span>
  >
  >
* <span data-ttu-id="7749f-145">**D: Quali lingue sono supportate per la reimpostazione della password?**</span><span class="sxs-lookup"><span data-stu-id="7749f-145">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="7749f-146">**R:** L'interfaccia utente, gli SMS e le chiamate vocali per la reimpostazione della password sono localizzati nelle stesse lingue supportate in Office 365.</span><span class="sxs-lookup"><span data-stu-id="7749f-146">**A:** The password reset UI, SMS messages, and voice calls are localized in the same languages that are supported in Office 365.</span></span>
  >
  >
* <span data-ttu-id="7749f-147">**D: A quali parti dell'esperienza di reimpostazione della password vengono applicate le impostazioni di personalizzazione dell'organizzazione specificate nella scheda Configura della directory?**</span><span class="sxs-lookup"><span data-stu-id="7749f-147">**Q:  What parts of the password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="7749f-148">**R:** Il portale per la reimpostazione della password mostra il logo dell'organizzazione e consente di configurare il collegamento Contattare l'amministratore che punti a un indirizzo di posta elettronica o a un URL personalizzato.</span><span class="sxs-lookup"><span data-stu-id="7749f-148">**A:** The password reset portal shows your organizational logo and allows you to configure the Contact your administrator link to point to a custom email or URL.</span></span> <span data-ttu-id="7749f-149">Nel corpo di tutti i messaggi di posta elettronica inviati dalla funzionalità di reimpostazione della password sono inclusi il logo, i colori e il nome dell'organizzazione, oltre al nome Da personalizzato.</span><span class="sxs-lookup"><span data-stu-id="7749f-149">Any email that gets sent by password reset includes your organization’s logo, colors, name in the body of the email, and customized from name.</span></span>
  >
  >
* <span data-ttu-id="7749f-150">**D: In che modo è possibile spiegare agli utenti come fare per reimpostare le proprie password?**</span><span class="sxs-lookup"><span data-stu-id="7749f-150">**Q:  How can I educate my users about where to go to reset their passwords?**</span></span>

  > <span data-ttu-id="7749f-151">**R:** È possibile indirizzare gli utenti direttamente al sito https://passwordreset.microsoftonline.com oppure invitarli a fare clic sul **collegamento Problemi di accesso all'account?** disponibile in qualsiasi schermata di accesso aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="7749f-151">**A:** You can send your users to https://passwordreset.microsoftonline.com directly, or you can instruct them to click the **Can’t access your account link** found on any Work or School sign-in page.</span></span> <span data-ttu-id="7749f-152">È anche possibile pubblicare questi collegamenti in una posizione facilmente accessibile agli utenti.</span><span class="sxs-lookup"><span data-stu-id="7749f-152">You can also publish these links in a place easily accessible to your users.</span></span>
  >
  >
* <span data-ttu-id="7749f-153">**D: Questa pagina può essere usata da un dispositivo mobile?**</span><span class="sxs-lookup"><span data-stu-id="7749f-153">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="7749f-154">**R:** Sì, la pagina funziona anche sui dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="7749f-154">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="7749f-155">**D: È supportato lo sblocco di account Active Directory locali quando gli utenti reimpostano le password?**</span><span class="sxs-lookup"><span data-stu-id="7749f-155">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="7749f-156">**R:** Sì, quando un utente reimposta la password e il writeback delle password viene distribuito mediante Azure AD Connect, tale account utente viene sbloccato automaticamente quando si reimposta la password.</span><span class="sxs-lookup"><span data-stu-id="7749f-156">**A:** Yes, when a user resets their password and password writeback has been deployed using Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span></span>
  >
  >
* <span data-ttu-id="7749f-157">**D: Come è possibile integrare la reimpostazione della password direttamente nell'esperienza di accesso desktop degli utenti?**</span><span class="sxs-lookup"><span data-stu-id="7749f-157">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="7749f-158">**R:** I clienti di Azure AD Premium possono installare gratuitamente Microsoft Identity Manager e distribuire la soluzione di reimpostazione della password locale per soddisfare questo requisito.</span><span class="sxs-lookup"><span data-stu-id="7749f-158">**A:** If you are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy the on-premises password reset solution to meet this requirement.</span></span>
  >
  >
* <span data-ttu-id="7749f-159">**D: È possibile impostare domande di sicurezza diverse per impostazioni locali diverse?**</span><span class="sxs-lookup"><span data-stu-id="7749f-159">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="7749f-160">**R:** Attualmente non è possibile.</span><span class="sxs-lookup"><span data-stu-id="7749f-160">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="7749f-161">**D: Quante domande si possono configurare per l'opzione di autenticazione Domande di sicurezza?**</span><span class="sxs-lookup"><span data-stu-id="7749f-161">**Q:  How many questions can we configure for the Security Questions authentication option?**</span></span>

  > <span data-ttu-id="7749f-162">**R:** Nel [portale di Azure](https://portal.azure.com) è possibile configurare un massimo di 20 domande di sicurezza personalizzate.</span><span class="sxs-lookup"><span data-stu-id="7749f-162">**A:** You can configure up to 20 custom security questions in the [Azure portal](https://portal.azure.com).</span></span>
  >
  >
* <span data-ttu-id="7749f-163">**D: Qual è la lunghezza delle domande di sicurezza?**</span><span class="sxs-lookup"><span data-stu-id="7749f-163">**Q:  How long may security questions be?**</span></span>

  > <span data-ttu-id="7749f-164">**R:** Le domande di sicurezza possono avere una lunghezza compresa tra 3 e 200 caratteri.</span><span class="sxs-lookup"><span data-stu-id="7749f-164">**A:** Security questions may be between 3 and 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="7749f-165">**D: Qual è la lunghezza delle risposte alle domande di sicurezza?**</span><span class="sxs-lookup"><span data-stu-id="7749f-165">**Q:  How long may answers to security questions be?**</span></span>

  > <span data-ttu-id="7749f-166">**R:** Le risposte possono avere una lunghezza compresa tra 3 e 40 caratteri.</span><span class="sxs-lookup"><span data-stu-id="7749f-166">**A:** Answers may be 3 to 40 characters long.</span></span>
  >
  >
* <span data-ttu-id="7749f-167">**D: Le risposte duplicate alle domande di sicurezza vengono rifiutate?**</span><span class="sxs-lookup"><span data-stu-id="7749f-167">**Q:  Are duplicate answers to security questions rejected?**</span></span>

  > <span data-ttu-id="7749f-168">**R:** Sì, vengono rifiutate.</span><span class="sxs-lookup"><span data-stu-id="7749f-168">**A:** Yes, we reject duplicate answers to security questions.</span></span>
  >
  >
* <span data-ttu-id="7749f-169">**D: Un utente può registrarsi più di una volta per la stessa domanda di sicurezza?**</span><span class="sxs-lookup"><span data-stu-id="7749f-169">**Q:  May a user register the same security question more than once?**</span></span>

  > <span data-ttu-id="7749f-170">**R:** No. Dopo che l'utente ha registrato una determinata domanda, non potrà registrarsi per quella domanda una seconda volta.</span><span class="sxs-lookup"><span data-stu-id="7749f-170">**A:** No, once a user registers a particular question, they may not register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="7749f-171">**D: È possibile impostare un limite minimo di domande di sicurezza per la registrazione e la reimpostazione?**</span><span class="sxs-lookup"><span data-stu-id="7749f-171">**Q:  Is it possible to set a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="7749f-172">**R:** Sì, è possibile impostare un limite per la registrazione e un altro per la reimpostazione.</span><span class="sxs-lookup"><span data-stu-id="7749f-172">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="7749f-173">Possono essere richieste da 3 a 5 domande di sicurezza per la registrazione e da 3 a 5 domande di sicurezza per la reimpostazione.</span><span class="sxs-lookup"><span data-stu-id="7749f-173">3-5 security questions may be required for registration and 3-5 may be required for reset.</span></span>
  >
  >
* <span data-ttu-id="7749f-174">**D: Se un utente ha registrato più del numero massimo di domande per reimpostare la password, come vengono selezionate le domande di sicurezza durante la reimpostazione?**</span><span class="sxs-lookup"><span data-stu-id="7749f-174">**Q:  If a user has registered more than the maximum number of questions required to reset, how are security questions selected during reset?**</span></span>

  > <span data-ttu-id="7749f-175">**R:** Dal numero totale di domande per cui l'utente si è registrato vengono selezionate casualmente N domande di sicurezza, dove N è il **numero di domande richieste per la reimpostazione**.</span><span class="sxs-lookup"><span data-stu-id="7749f-175">**A:** N security questions are selected at random out of the total number of questions a user has registered for, where N is the **Number of questions required to reset**.</span></span> <span data-ttu-id="7749f-176">Ad esempio, se un utente ha registrato 5 domande di sicurezza, ma per la reimpostazione ne sono richieste solo 3, ne verranno selezionate casualmente e presentate 3 di quelle 5 al momento della reimpostazione.</span><span class="sxs-lookup"><span data-stu-id="7749f-176">For example, if a user has 5 security questions registered, but only 3 are required to reset, 3 of the 5 are selected randomly and presented at reset.</span></span> <span data-ttu-id="7749f-177">Se un utente sbaglia le risposte alle domande, il processo di selezione verrà eseguito di nuovo per evitare la ripetizione delle domande.</span><span class="sxs-lookup"><span data-stu-id="7749f-177">If the user gets the answers to the questions wrong, the selection process reoccurs to prevent question hammering.</span></span>
  >
  >
* <span data-ttu-id="7749f-178">**D: Viene impedito agli utenti di provare a reimpostare la password più volte in un breve periodo di tempo?**</span><span class="sxs-lookup"><span data-stu-id="7749f-178">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span></span>

  > <span data-ttu-id="7749f-179">**R:** Sì. Per evitarne l'uso improprio, il processo di reimpostazione della password comprende funzionalità di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="7749f-179">**A:** Yes, there are security features built into password reset to protect from misuse.</span></span> <span data-ttu-id="7749f-180">Gli utenti possono effettuare solo 5 tentativi di reimpostazione della password nell'arco di un'ora, prima di essere bloccati per 24 ore.</span><span class="sxs-lookup"><span data-stu-id="7749f-180">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="7749f-181">Gli utenti possono convalidare un numero di telefono solo 5 volte nell'arco di un'ora, prima di essere bloccati per 24 ore.</span><span class="sxs-lookup"><span data-stu-id="7749f-181">Users may only try to validate a phone number 5 times within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="7749f-182">Gli utenti possono provare solo 5 volte un singolo metodo di autenticazione nell'arco di un'ora, prima di essere bloccati per 24 ore.</span><span class="sxs-lookup"><span data-stu-id="7749f-182">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span></span>
  >
  >
* <span data-ttu-id="7749f-183">**D: Per quanto tempo è valido il passcode monouso inviato per posta elettronica o SMS?**</span><span class="sxs-lookup"><span data-stu-id="7749f-183">**Q:  For how long are the email and SMS one-time passcode valid?**</span></span>

  > <span data-ttu-id="7749f-184">**R:** La durata della sessione per la reimpostazione della password è di 105 minuti.</span><span class="sxs-lookup"><span data-stu-id="7749f-184">**A:** The session lifetime for password reset is 105 minutes.</span></span> <span data-ttu-id="7749f-185">Dall'inizio dell'operazione di reimpostazione della password l'utente ha 105 minuti per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="7749f-185">From the beginning of the password reset operation, the user has 105 minutes to reset their password.</span></span> <span data-ttu-id="7749f-186">Allo scadere di questo periodo di tempo, il passcode monouso inviato per SMS o posta elettronica non sarà più valido.</span><span class="sxs-lookup"><span data-stu-id="7749f-186">The email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="7749f-187">Modifica della password</span><span class="sxs-lookup"><span data-stu-id="7749f-187">Password change</span></span>
* <span data-ttu-id="7749f-188">**D: Dove devono andare gli utenti per modificare la password?**</span><span class="sxs-lookup"><span data-stu-id="7749f-188">**Q:  Where should my users go to change their passwords?**</span></span>

  > <span data-ttu-id="7749f-189">**R:** Gli utenti possono modificare le password in qualsiasi punto visualizzino l'immagine o l'icona del profilo, ad esempio nell'angolo in alto a destra della sezione [Office 365](https://portal.office.com) o [Access Panel](https://myapps.microsoft.com) (Pannello di accesso).</span><span class="sxs-lookup"><span data-stu-id="7749f-189">**A:** Users may change their passwords anywhere they see their profile picture or icon (like in the upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="7749f-190">Gli utenti possono modificare le password dalla [pagina profilo del Pannello di accesso](https://account.activedirectory.windowsazure.com/r#/profile).</span><span class="sxs-lookup"><span data-stu-id="7749f-190">Users may change their passwords from the [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="7749f-191">Se la password è scaduta, agli utenti potrebbe venir richiesto di modificare la password automaticamente nella schermata di accesso di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7749f-191">Users may also be asked to change their passwords automatically at the Azure AD sign-in screen if their passwords have expired.</span></span> <span data-ttu-id="7749f-192">Infine, se desiderano modificare la password, gli utenti possono accedere direttamente al [portale di modifica della password di Azure AD](https://account.activedirectory.windowsazure.com/ChangePassword.aspx).</span><span class="sxs-lookup"><span data-stu-id="7749f-192">Finally, users may navigate to the [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish to change their passwords.</span></span>
  >
  >
* <span data-ttu-id="7749f-193">**D: Gli utenti possono ricevere una notifica nel portale di Office alla scadenza della propria password locale?**</span><span class="sxs-lookup"><span data-stu-id="7749f-193">**Q:  Can my users be notified in the Office Portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="7749f-194">**R:** Attualmente è possibile se si usa ADFS seguendo le istruzioni riportate di seguito: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396) (Invio delle attestazioni dei criteri delle password con ADFS).</span><span class="sxs-lookup"><span data-stu-id="7749f-194">**A:** This is possible today if you are using ADFS by following the instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="7749f-195">Se si usa la sincronizzazione dell'hash della password, al momento non è possibile.</span><span class="sxs-lookup"><span data-stu-id="7749f-195">If you are using password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="7749f-196">Ciò avviene perché i criteri della password locale non vengono sincronizzati, pertanto non è possibile inviare notifiche sulla scadenza nel cloud.</span><span class="sxs-lookup"><span data-stu-id="7749f-196">This is because we do not sync password policies from on-premises, so it is not possible for us to post expiry notifications to cloud experiences.</span></span> <span data-ttu-id="7749f-197">In entrambi i casi, è anche possibile [inviare notifiche tramite PowerShell agli utenti le cui password stanno per scadere](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span><span class="sxs-lookup"><span data-stu-id="7749f-197">In either case, it is also possible to [notify users whose passwords are about to expire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="7749f-198">Report di gestione delle password</span><span class="sxs-lookup"><span data-stu-id="7749f-198">Password management reports</span></span>
* <span data-ttu-id="7749f-199">**D: Quanto tempo trascorre prima che i dati vengono visualizzati nei report di gestione delle password?**</span><span class="sxs-lookup"><span data-stu-id="7749f-199">**Q:  How long does it take for data to show up on the password management reports?**</span></span>

  > <span data-ttu-id="7749f-200">**R:** I dati dovrebbero essere visualizzati in tali report entro 5-10 minuti.</span><span class="sxs-lookup"><span data-stu-id="7749f-200">**A:** Data should appear on the password management reports within 5-10 minutes.</span></span> <span data-ttu-id="7749f-201">In alcuni casi, potrebbero richiedere fino a un'ora.</span><span class="sxs-lookup"><span data-stu-id="7749f-201">It some instances it may take up to an hour to appear.</span></span>
  >
  >
* <span data-ttu-id="7749f-202">**D: Come si possono filtrare i report di gestione delle password?**</span><span class="sxs-lookup"><span data-stu-id="7749f-202">**Q:  How can I filter the password management reports?**</span></span>

  > <span data-ttu-id="7749f-203">**R:** Per filtrare i report di gestione delle password, è possibile fare clic sulla piccola lente di ingrandimento all'estrema destra delle etichette di colonna, vicino alla parte superiore del report.</span><span class="sxs-lookup"><span data-stu-id="7749f-203">**A:** You can filter the password management reports by clicking the small magnifying glass to the extreme right of the column labels, near the top of the report.</span></span> <span data-ttu-id="7749f-204">Per applicare una funzione di filtro più completa, scaricare il report in Excel e creare una tabella pivot.</span><span class="sxs-lookup"><span data-stu-id="7749f-204">If you want to do richer filtering, you can download the report to excel and create a pivot table.</span></span>
  >
  >
* <span data-ttu-id="7749f-205">**D: qual è il numero massimo di eventi che vengono archiviati nei report di gestione della password?**</span><span class="sxs-lookup"><span data-stu-id="7749f-205">**Q: What is the maximum number of events are stored in the password management reports?**</span></span>

  > <span data-ttu-id="7749f-206">**R:** Nei report di gestione della password vengono archiviati fino a 75.000 eventi di reimpostazione della password o di registrazione della reimpostazione della password, con un backup fino a 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="7749f-206">**A:** Up to 75,000 password reset or password reset registration events are stored in the password management reports, spanning back up to 30 days.</span></span>  <span data-ttu-id="7749f-207">Stiamo lavorando per espandere questo numero al fine di includere un maggior numero di eventi.</span><span class="sxs-lookup"><span data-stu-id="7749f-207">We are working to expand this number to include more events.</span></span>
  >
  >
* <span data-ttu-id="7749f-208">**D: Fino a quando risalgono i report di gestione delle password?**</span><span class="sxs-lookup"><span data-stu-id="7749f-208">**Q:  How far back do the password management reports go?**</span></span>

  > <span data-ttu-id="7749f-209">**R:** Questi report mostrano le operazioni che si sono verificate negli ultimi 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="7749f-209">**A:** The password management reports show operations occurring within the last 30 days.</span></span> <span data-ttu-id="7749f-210">Per il momento, se occorre archiviare i dati, è possibile scaricare i report periodicamente e salvarli in un percorso separato.</span><span class="sxs-lookup"><span data-stu-id="7749f-210">For now, if you need to archive this data, you can download the reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="7749f-211">**D: Esiste un limite al numero massimo di righe visualizzabili nei report di gestione delle password?**</span><span class="sxs-lookup"><span data-stu-id="7749f-211">**Q:  Is there a maximum number of rows that can appear on the password management reports?**</span></span>

  > <span data-ttu-id="7749f-212">**R:** Sì, è possibile visualizzare un massimo di 75.000 righe nei report di gestione delle password, sia quando vengono riprodotti nell'interfaccia utente sia quando vengono scaricati.</span><span class="sxs-lookup"><span data-stu-id="7749f-212">**A:** Yes, a maximum of 75,000 rows may appear on either of the password management reports, whether they are being shown in the UI or being downloaded.</span></span>
  >
  >
* <span data-ttu-id="7749f-213">**D: Esiste un'API per accedere alla reimpostazione della password o alla raccolta dei dati di registrazione?**</span><span class="sxs-lookup"><span data-stu-id="7749f-213">**Q:  Is there an API to access the password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="7749f-214">**R:** Sì, per informazioni su come accedere al flusso dei dati del report sulla reimpostazione della password, vedere la documentazione seguente.</span><span class="sxs-lookup"><span data-stu-id="7749f-214">**A:** Yes, see the following documentation to learn how you can access the password reset reporting data stream.</span></span>  <span data-ttu-id="7749f-215">[Informazioni su come accedere agli eventi di report della reimpostazione della password a livello di programmazione](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span><span class="sxs-lookup"><span data-stu-id="7749f-215">[Learn how to access password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="7749f-216">Writeback delle password</span><span class="sxs-lookup"><span data-stu-id="7749f-216">Password writeback</span></span>
* <span data-ttu-id="7749f-217">**D: Come funziona il writeback delle password in background?**</span><span class="sxs-lookup"><span data-stu-id="7749f-217">**Q:  How does password writeback work behind the scenes?**</span></span>

  > <span data-ttu-id="7749f-218">**R:** Per una spiegazione di ciò che accade quando si abilita il writeback delle password, nonché del modo in cui i dati transitano dal sistema all'ambiente locale, vedere [Funzionamento del writeback delle password](active-directory-passwords-writeback.md).</span><span class="sxs-lookup"><span data-stu-id="7749f-218">**A:** See [How password writeback works](active-directory-passwords-writeback.md) for an explanation of what happens when you enable password writeback, and how data flows through the system back into your on-premises environment.</span></span>
  >
  >
* <span data-ttu-id="7749f-219">**D: Entro quanto tempo si attiva il funzionamento del writeback delle password?  Esiste un ritardo di sincronizzazione come per la sincronizzazione di hash della password?**</span><span class="sxs-lookup"><span data-stu-id="7749f-219">**Q:  How long does password writeback take to work?  Is there a synchronization delay like with password hash sync?**</span></span>

  > <span data-ttu-id="7749f-220">**R:** Il writeback delle password è immediato.</span><span class="sxs-lookup"><span data-stu-id="7749f-220">**A:** Password writeback is instant.</span></span> <span data-ttu-id="7749f-221">Si tratta di una pipeline sincrona che funziona fondamentalmente in modo diverso rispetto alla sincronizzazione di hash della password.</span><span class="sxs-lookup"><span data-stu-id="7749f-221">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="7749f-222">Il writeback delle password consente agli utenti di avere un feedback in tempo reale sulla riuscita dell'operazione di reimpostazione o modifica della propria password.</span><span class="sxs-lookup"><span data-stu-id="7749f-222">Password writeback allows users to get real-time feedback about the success of their password reset or change operation.</span></span> <span data-ttu-id="7749f-223">L'intervallo medio per un writeback della password riuscito è inferiore a 500 ms.</span><span class="sxs-lookup"><span data-stu-id="7749f-223">The average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="7749f-224">**D: Se l'account locale è disabilitato, cosa succede all'accesso o all'account cloud?**</span><span class="sxs-lookup"><span data-stu-id="7749f-224">**Q:  If my on-premises account is disabled, how is my cloud account/access affected?**</span></span>

  > <span data-ttu-id="7749f-225">**R:** Se l'ID locale è disabilitato, anche l'ID o l'accesso cloud verranno disabilitati al successivo intervallo di sincronizzazione tramite AAD Connect; per impostazione predefinita questo avviene ogni 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="7749f-225">**A:** If your on-premises ID is disabled, your cloud ID/access will also be disabled at the next sync interval via AAD Connect byt default this is every 30 minutes.</span></span>
  >
  >
* <span data-ttu-id="7749f-226">**D: Se l'account locale è vincolato da un criterio di password di Active Directory locale, la reimpostazione della password self-service rispetta questo criterio quando si modifica la password?**</span><span class="sxs-lookup"><span data-stu-id="7749f-226">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change the password?**</span></span>

  > <span data-ttu-id="7749f-227">**R:** Sì, la reimpostazione della password self-service si basa e si attiene ai criteri della password di Active Directory locale, che includono il tipico criterio della password di dominio AD, nonché tutti i criteri della password con granularità fine definiti destinati a un determinato utente.</span><span class="sxs-lookup"><span data-stu-id="7749f-227">**A:** Yes, SSPR relies on and abides by the on-premises AD password policy, including typical AD domain password policy, as well as any defined fine grained password policies targeted to a given user.</span></span>
  >
  >
* <span data-ttu-id="7749f-228">**D: Per quali tipi di account funziona il writeback delle password?**</span><span class="sxs-lookup"><span data-stu-id="7749f-228">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="7749f-229">**R:** Funziona per gli utenti federati e con sincronizzazione di hash della password.</span><span class="sxs-lookup"><span data-stu-id="7749f-229">**A:** Password writeback works for Federated and Password Hash Synchronized users.</span></span>
  >
  >
* <span data-ttu-id="7749f-230">**D: Il writeback delle password applica i criteri di password del dominio?**</span><span class="sxs-lookup"><span data-stu-id="7749f-230">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="7749f-231">**R:** Sì, applica validità, cronologia, complessità, filtri e qualsiasi altra restrizione eventualmente applicata alle password nel dominio locale.</span><span class="sxs-lookup"><span data-stu-id="7749f-231">**A:** Yes, password writeback enforces password age, history, complexity, filters, and any other restriction you may put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="7749f-232">**D: Il writeback delle password è sicuro?  Come si può essere certi di non essere oggetto di un attacco?**</span><span class="sxs-lookup"><span data-stu-id="7749f-232">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="7749f-233">**R:** Sì, il writeback delle password è sicuro.</span><span class="sxs-lookup"><span data-stu-id="7749f-233">**A:** Yes, password writeback is secure.</span></span> <span data-ttu-id="7749f-234">Per altre informazioni sui 4 livelli di sicurezza implementati dal servizio di writeback delle password, vedere la sezione [Password writeback security model](active-directory-passwords-writeback.md#password-writeback-security-model) (Modello di sicurezza del writeback della password) in Funzionamento del writeback delle password.</span><span class="sxs-lookup"><span data-stu-id="7749f-234">To read more about the four layers of security implemented by the password writeback service, check out the [Password writeback security model](active-directory-passwords-writeback.md#password-writeback-security-model) section in How password writeback works.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="7749f-235">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7749f-235">Next steps</span></span>

<span data-ttu-id="7749f-236">I collegamenti seguenti forniscono altre informazioni sull'uso della reimpostazione della password con Azure AD</span><span class="sxs-lookup"><span data-stu-id="7749f-236">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="7749f-237">[**Guida introduttiva**](active-directory-passwords-getting-started.md) - Iniziare a usare la gestione self-service delle password di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7749f-237">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="7749f-238">[**Licenze**](active-directory-passwords-licensing.md): configurare le licenze di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7749f-238">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="7749f-239">[**Dati** ](active-directory-passwords-data.md): informazioni sui dati necessari e su come vengono usati per la gestione delle password</span><span class="sxs-lookup"><span data-stu-id="7749f-239">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="7749f-240">[**Implementazione**](active-directory-passwords-best-practices.md): pianificare e distribuire agli utenti la reimpostazione password self-service usando le istruzioni disponibili in questo articolo</span><span class="sxs-lookup"><span data-stu-id="7749f-240">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="7749f-241">[**Personalizzazione**](active-directory-passwords-customize.md): personalizzare l'aspetto dell'esperienza della reimpostazione password self-service per l'azienda.</span><span class="sxs-lookup"><span data-stu-id="7749f-241">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="7749f-242">[**Reporting** ](active-directory-passwords-reporting.md): verificare se, quando e dove gli utenti accedono alla reimpostazione password self-service</span><span class="sxs-lookup"><span data-stu-id="7749f-242">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="7749f-243">[**Criteri**](active-directory-passwords-policy.md): comprendere e impostare i criteri password di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7749f-243">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="7749f-244">[**Writeback delle password**](active-directory-passwords-writeback.md): funzionamento del writeback delle password con la directory locale</span><span class="sxs-lookup"><span data-stu-id="7749f-244">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="7749f-245">[**Approfondimento tecnico**](active-directory-passwords-how-it-works.md): approfondimento sul funzionamento</span><span class="sxs-lookup"><span data-stu-id="7749f-245">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="7749f-246">[**Risoluzione dei problemi**](active-directory-passwords-troubleshoot.md): informazioni su come risolvere i problemi comuni con la reimpostazione password self-service</span><span class="sxs-lookup"><span data-stu-id="7749f-246">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>
