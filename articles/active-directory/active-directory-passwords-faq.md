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
ms.openlocfilehash: d04a9efeb3b35421aa605cadb2aa25f656a4d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="e82da-104">Domande frequenti sulla gestione delle password</span><span class="sxs-lookup"><span data-stu-id="e82da-104">Password management frequently asked questions</span></span>

<span data-ttu-id="e82da-105">Hello seguente è riportate alcune domande frequenti per tutti gli elementi correlati toopassword reimpostare.</span><span class="sxs-lookup"><span data-stu-id="e82da-105">hello following are some frequently asked questions for all things related toopassword reset.</span></span>

<span data-ttu-id="e82da-106">Se si dispone di una domanda generale sulle AD Azure password self-service e ripristino, che non viene risposta qui, è possibile richiedere community hello assistenza sul hello [forum di Azure Ad](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span><span class="sxs-lookup"><span data-stu-id="e82da-106">If you have a general question about Azure AD and self-service password reset, that is not answered here, you can ask hello community for assistance on hello [Azure Ad forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span></span> <span data-ttu-id="e82da-107">I membri della community di hello includere tecnici, responsabili di prodotto, MVP e fellow ai professionisti IT.</span><span class="sxs-lookup"><span data-stu-id="e82da-107">Members of hello community include Engineers, Product Managers, MVPs, and fellow IT Professionals.</span></span>

<span data-ttu-id="e82da-108">Questa sezione è suddivisa in hello le sezioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e82da-108">This FAQ is split into hello following sections:</span></span>

* [<span data-ttu-id="e82da-109">**Domande sulla registrazione per la reimpostazione della password**</span><span class="sxs-lookup"><span data-stu-id="e82da-109">**Questions about Password Reset Registration**</span></span>](#password-reset-registration)
* [<span data-ttu-id="e82da-110">**Domande sulla reimpostazione della password**</span><span class="sxs-lookup"><span data-stu-id="e82da-110">**Questions about Password Reset**</span></span>](#password-reset)
* [<span data-ttu-id="e82da-111">**Domande sulla modifica della password**</span><span class="sxs-lookup"><span data-stu-id="e82da-111">**Questions about Password Change**</span></span>](#password-change)
* [<span data-ttu-id="e82da-112">**Domande relative ai report di gestione delle password**</span><span class="sxs-lookup"><span data-stu-id="e82da-112">**Questions about password management Reports**</span></span>](#password-management-reports)
* [<span data-ttu-id="e82da-113">**Domande sul writeback delle password**</span><span class="sxs-lookup"><span data-stu-id="e82da-113">**Questions about password writeback**</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="e82da-114">Registrazione per la reimpostazione della password</span><span class="sxs-lookup"><span data-stu-id="e82da-114">Password reset registration</span></span>
* <span data-ttu-id="e82da-115">**D: Gli utenti possono registrare i propri dati per la reimpostazione della password?**</span><span class="sxs-lookup"><span data-stu-id="e82da-115">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="e82da-116">**R:** Sì, purché la reimpostazione della password è abilitata e sono concessi in licenza, possono passare toohello portale di registrazione della reimpostazione della Password in http://aka.ms/ssprsetup tooregister le informazioni di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e82da-116">**A:** Yes, as long as password reset is enabled and they are licensed, they can go toohello Password Reset Registration portal at http://aka.ms/ssprsetup tooregister their authentication information.</span></span> <span data-ttu-id="e82da-117">Gli utenti possono anche registrarsi tramite Pannello di accesso toohello passare a http://myapps.microsoft.com, facendo clic sulla scheda profilo hello e facendo clic su hello registro per l'opzione di reimpostazione della Password.</span><span class="sxs-lookup"><span data-stu-id="e82da-117">Users can also register by going toohello access panel at http://myapps.microsoft.com, clicking hello profile tab, and clicking hello Register for Password Reset option.</span></span>
  >
  >
* <span data-ttu-id="e82da-118">**D: è possibile definire i dati di reimpostazione della password per conto degli utenti?**</span><span class="sxs-lookup"><span data-stu-id="e82da-118">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="e82da-119">**R:** Sì, è possibile farlo con Azure AD Connect, PowerShell, hello [portale di Azure](https://portal.azure.com), o il portale di amministrazione di Office hello.</span><span class="sxs-lookup"><span data-stu-id="e82da-119">**A:** Yes, you can do so with Azure AD Connect, PowerShell, hello [Azure portal](https://portal.azure.com), or hello Office Admin portal.</span></span> <span data-ttu-id="e82da-120">Per ulteriori informazioni, vedere l'articolo hello [dati utilizzati da Azure AD Self-Service di reimpostazione della Password](active-directory-passwords-data.md).</span><span class="sxs-lookup"><span data-stu-id="e82da-120">For more information, see hello article [Data used by Azure AD Self-Service Password Reset](active-directory-passwords-data.md).</span></span>
  >
  >
* <span data-ttu-id="e82da-121">**D: È possibile sincronizzare i dati per le domande di sicurezza dall'ambiente locale?**</span><span class="sxs-lookup"><span data-stu-id="e82da-121">**Q:  Can I synchronize data for security questions from on premises?**</span></span>

  > <span data-ttu-id="e82da-122">**R:** Attualmente non è possibile.</span><span class="sxs-lookup"><span data-stu-id="e82da-122">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="e82da-123">**D: Gli utenti possono registrare i dati in modo che non siano visibili ad altri utenti?**</span><span class="sxs-lookup"><span data-stu-id="e82da-123">**Q:  Can my users register data in such a way that other users cannot see this data?**</span></span>

  > <span data-ttu-id="e82da-124">**R:** Sì, quando gli utenti registrano dati tramite hello registrazione del portale di reimpostazione Password viene salvata in campi privati di autenticazione visibili solo gli amministratori globali e hello utente.</span><span class="sxs-lookup"><span data-stu-id="e82da-124">**A:** Yes, when users register data using hello Password Reset Registration Portal it is saved into private authentication fields that are only visible by Global Administrators and hello user.</span></span>
    >
    > [!NOTE]
    > <span data-ttu-id="e82da-125">Se un **account amministratore Azure** registra il numero di telefono di autenticazione viene inoltre popolato nel campo del telefono cellulare hello e visibile.</span><span class="sxs-lookup"><span data-stu-id="e82da-125">If an **Azure Administrator account** registers their authentication phone number it is also populated into hello mobile phone field and is visible.</span></span>
    >
  >
  >
* <span data-ttu-id="e82da-126">**D: gli utenti hanno toobe registrati prima di poter usare la reimpostazione della password?**</span><span class="sxs-lookup"><span data-stu-id="e82da-126">**Q:  Do my users have toobe registered before they can use password reset?**</span></span>

  > <span data-ttu-id="e82da-127">**R:** No, se si definiscono informazioni di autenticazione sufficienti per loro conto, gli utenti non sono tooregister.</span><span class="sxs-lookup"><span data-stu-id="e82da-127">**A:** No, if you define enough authentication information on their behalf, users do not have tooregister.</span></span> <span data-ttu-id="e82da-128">Funzionamento della reimpostazione password, purché siano formattati correttamente i dati archiviati nei campi appropriati di hello nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="e82da-128">Password reset works as long as you have properly formatted data stored in hello appropriate fields in hello directory.</span></span>
  >
  >
* <span data-ttu-id="e82da-129">**D: è possibile sincronizzare o impostare i campi di hello telefono per l'autenticazione, posta elettronica di autenticazione o telefono alternativo per l'autenticazione per conto degli utenti?**</span><span class="sxs-lookup"><span data-stu-id="e82da-129">**Q:  Can I synchronize or set hello Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="e82da-130">**R:** Attualmente non è possibile.</span><span class="sxs-lookup"><span data-stu-id="e82da-130">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="e82da-131">**D: come portale di registrazione hello sapere quali tooshow opzioni gli utenti?**</span><span class="sxs-lookup"><span data-stu-id="e82da-131">**Q:  How does hello registration portal know which options tooshow my users?**</span></span>

  > <span data-ttu-id="e82da-132">**R:** portale di registrazione di reimpostazione della password di hello solo Mostra hello opzioni che è stata abilitata per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="e82da-132">**A:** hello password reset registration portal only shows hello options that you have enabled for your users.</span></span> <span data-ttu-id="e82da-133">Queste opzioni sono disponibili nella sezione criteri di reimpostazione Password utente della scheda Configura della directory hello. Ad esempio, ciò significa che se non si abilita domande di sicurezza, quindi gli utenti non sono in grado di tooregister per tale opzione.</span><span class="sxs-lookup"><span data-stu-id="e82da-133">These options are found under hello User Password Reset Policy section of your directory’s Configure tab. For example, this means that if you do not enable security questions, then users are not able tooregister for that option.</span></span>
  >
  >
* <span data-ttu-id="e82da-134">**D: Quando un utente viene considerato registrato?**</span><span class="sxs-lookup"><span data-stu-id="e82da-134">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="e82da-135">**R:** un utente è considerato registrato per SSPR quando essi sono registrati almeno hello **numero di metodi obbligatorio tooreset** che sono stati impostati nel hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e82da-135">**A:** A user is considered registered for SSPR when they have registered at least hello **Number of methods required tooreset** that you have set in hello [Azure portal](https://portal.azure.com).</span></span>
  >
  >
## <a name="password-reset"></a><span data-ttu-id="e82da-136">Reimpostazione delle password</span><span class="sxs-lookup"><span data-stu-id="e82da-136">Password reset</span></span>
* <span data-ttu-id="e82da-137">**D: come tempo è consigliabile attendere tooreceive un messaggio di posta elettronica, SMS o chiamata telefonica di reimpostazione della password?**</span><span class="sxs-lookup"><span data-stu-id="e82da-137">**Q:  How long should I wait tooreceive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="e82da-138">**R:** posta elettronica, i messaggi SMS e telefonate dovrebbero arrivare in un minuto, in hello normale entro 5-20 secondi.</span><span class="sxs-lookup"><span data-stu-id="e82da-138">**A:** Email, SMS messages, and phone calls should arrive in under one minute, with hello normal case being 5-20 seconds.</span></span>
    ><span data-ttu-id="e82da-139">Se non si riceve notifica hello in questo periodo di tempo:</span><span class="sxs-lookup"><span data-stu-id="e82da-139">If you do not receive hello notification in this time frame:</span></span>
        > * <span data-ttu-id="e82da-140">Controllare la cartella della posta indesiderata.</span><span class="sxs-lookup"><span data-stu-id="e82da-140">Check your junk folder.</span></span>
        > * <span data-ttu-id="e82da-141">Verificare il numero hello o posta elettronica contattato è hello previsto.</span><span class="sxs-lookup"><span data-stu-id="e82da-141">Check hello number or email being contacted is hello one you expect.</span></span>
        > * <span data-ttu-id="e82da-142">Controllare i dati di autenticazione hello nella directory hello sono formattati correttamente.</span><span class="sxs-lookup"><span data-stu-id="e82da-142">Check hello authentication data in hello directory is correctly formatted.</span></span>
                >     * <span data-ttu-id="e82da-143">Esempio: "+1 4255551234" o "user@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="e82da-143">Example: "+1 4255551234" or "user@contoso.com"</span></span>
  >
  >
* <span data-ttu-id="e82da-144">**D: Quali lingue sono supportate per la reimpostazione della password?**</span><span class="sxs-lookup"><span data-stu-id="e82da-144">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="e82da-145">**R:** hello la reimpostazione della password dell'interfaccia utente, i messaggi SMS e vocale chiamate sono localizzate in hello stesse lingue supportate in Office 365.</span><span class="sxs-lookup"><span data-stu-id="e82da-145">**A:** hello password reset UI, SMS messages, and voice calls are localized in hello same languages that are supported in Office 365.</span></span>
  >
  >
* <span data-ttu-id="e82da-146">**Q: quali parti dell'esperienza di reimpostazione della password hello personalizzate quando si imposta aziendale di branding nella directory di configurazione della scheda?**</span><span class="sxs-lookup"><span data-stu-id="e82da-146">**Q:  What parts of hello password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="e82da-147">**R:** hello portale di reimpostazione della password viene mostrato il logo aziendale e consente tooconfigure hello, contattare l'amministratore collegamento toopoint tooa personalizzato tramite posta elettronica o URL.</span><span class="sxs-lookup"><span data-stu-id="e82da-147">**A:** hello password reset portal shows your organizational logo and allows you tooconfigure hello Contact your administrator link toopoint tooa custom email or URL.</span></span> <span data-ttu-id="e82da-148">Qualsiasi messaggio di posta elettronica viene inviato per la reimpostazione della password include il logo dell'organizzazione, colori, il nome nel corpo di hello del messaggio di posta elettronica hello e personalizzate dal nome.</span><span class="sxs-lookup"><span data-stu-id="e82da-148">Any email that gets sent by password reset includes your organization’s logo, colors, name in hello body of hello email, and customized from name.</span></span>
  >
  >
* <span data-ttu-id="e82da-149">**D: come è possibile indicare agli utenti dove toogo tooreset le proprie password?**</span><span class="sxs-lookup"><span data-stu-id="e82da-149">**Q:  How can I educate my users about where toogo tooreset their passwords?**</span></span>

  > <span data-ttu-id="e82da-150">**R:** è possibile inviare direttamente i toohttps://passwordreset.microsoftonline.com utenti oppure è possibile indicare loro hello tooclick **non può accedere il collegamento di account** trovato in qualsiasi pagina accesso aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="e82da-150">**A:** You can send your users toohttps://passwordreset.microsoftonline.com directly, or you can instruct them tooclick hello **Can’t access your account link** found on any Work or School sign-in page.</span></span> <span data-ttu-id="e82da-151">È anche possibile pubblicare questi collegamenti in un utenti tooyour facilmente accessibili sul posto.</span><span class="sxs-lookup"><span data-stu-id="e82da-151">You can also publish these links in a place easily accessible tooyour users.</span></span>
  >
  >
* <span data-ttu-id="e82da-152">**D: Questa pagina può essere usata da un dispositivo mobile?**</span><span class="sxs-lookup"><span data-stu-id="e82da-152">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="e82da-153">**R:** Sì, la pagina funziona anche sui dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="e82da-153">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="e82da-154">**D: È supportato lo sblocco di account Active Directory locali quando gli utenti reimpostano le password?**</span><span class="sxs-lookup"><span data-stu-id="e82da-154">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="e82da-155">**R:** Sì, quando un utente reimposta la password e il writeback delle password viene distribuito mediante Azure AD Connect, tale account utente viene sbloccato automaticamente quando si reimposta la password.</span><span class="sxs-lookup"><span data-stu-id="e82da-155">**A:** Yes, when a user resets their password and password writeback has been deployed using Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span></span>
  >
  >
* <span data-ttu-id="e82da-156">**D: Come è possibile integrare la reimpostazione della password direttamente nell'esperienza di accesso desktop degli utenti?**</span><span class="sxs-lookup"><span data-stu-id="e82da-156">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="e82da-157">**R:** nel caso di un cliente di Azure AD Premium, è possibile installare Microsoft Identity Manager senza alcun costo aggiuntivo e distribuire hello locale password reset soluzione toomeet questo requisito.</span><span class="sxs-lookup"><span data-stu-id="e82da-157">**A:** If you are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy hello on-premises password reset solution toomeet this requirement.</span></span>
  >
  >
* <span data-ttu-id="e82da-158">**D: È possibile impostare domande di sicurezza diverse per impostazioni locali diverse?**</span><span class="sxs-lookup"><span data-stu-id="e82da-158">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="e82da-159">**R:** Attualmente non è possibile.</span><span class="sxs-lookup"><span data-stu-id="e82da-159">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="e82da-160">**D: quante domande è possibile configurare per l'opzione di autenticazione domande di sicurezza hello?**</span><span class="sxs-lookup"><span data-stu-id="e82da-160">**Q:  How many questions can we configure for hello Security Questions authentication option?**</span></span>

  > <span data-ttu-id="e82da-161">**R:** è possibile configurare le domande di sicurezza personalizzato too20 in hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e82da-161">**A:** You can configure up too20 custom security questions in hello [Azure portal](https://portal.azure.com).</span></span>
  >
  >
* <span data-ttu-id="e82da-162">**D: Qual è la lunghezza delle domande di sicurezza?**</span><span class="sxs-lookup"><span data-stu-id="e82da-162">**Q:  How long may security questions be?**</span></span>

  > <span data-ttu-id="e82da-163">**R:** Le domande di sicurezza possono avere una lunghezza compresa tra 3 e 200 caratteri.</span><span class="sxs-lookup"><span data-stu-id="e82da-163">**A:** Security questions may be between 3 and 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="e82da-164">**D: come long risposte toosecurity domande sia?**</span><span class="sxs-lookup"><span data-stu-id="e82da-164">**Q:  How long may answers toosecurity questions be?**</span></span>

  > <span data-ttu-id="e82da-165">**R:** le risposte possono contenere 3 too40 caratteri.</span><span class="sxs-lookup"><span data-stu-id="e82da-165">**A:** Answers may be 3 too40 characters long.</span></span>
  >
  >
* <span data-ttu-id="e82da-166">**D: sono rifiutate le risposte duplicate toosecurity domande?**</span><span class="sxs-lookup"><span data-stu-id="e82da-166">**Q:  Are duplicate answers toosecurity questions rejected?**</span></span>

  > <span data-ttu-id="e82da-167">**R:** Sì, vengono rifiutate le risposte duplicate toosecurity domande.</span><span class="sxs-lookup"><span data-stu-id="e82da-167">**A:** Yes, we reject duplicate answers toosecurity questions.</span></span>
  >
  >
* <span data-ttu-id="e82da-168">**Q: maggio un registro utente hello stessa domanda di sicurezza più volte?**</span><span class="sxs-lookup"><span data-stu-id="e82da-168">**Q:  May a user register hello same security question more than once?**</span></span>

  > <span data-ttu-id="e82da-169">**R:** No. Dopo che l'utente ha registrato una determinata domanda, non potrà registrarsi per quella domanda una seconda volta.</span><span class="sxs-lookup"><span data-stu-id="e82da-169">**A:** No, once a user registers a particular question, they may not register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="e82da-170">**D: è possibile tooset un limite minimo di domande di sicurezza per la registrazione e la reimpostazione?**</span><span class="sxs-lookup"><span data-stu-id="e82da-170">**Q:  Is it possible tooset a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="e82da-171">**R:** Sì, è possibile impostare un limite per la registrazione e un altro per la reimpostazione.</span><span class="sxs-lookup"><span data-stu-id="e82da-171">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="e82da-172">Possono essere richieste da 3 a 5 domande di sicurezza per la registrazione e da 3 a 5 domande di sicurezza per la reimpostazione.</span><span class="sxs-lookup"><span data-stu-id="e82da-172">3-5 security questions may be required for registration and 3-5 may be required for reset.</span></span>
  >
  >
* <span data-ttu-id="e82da-173">**D: se un utente ha registrato più di numero massimo di hello di domande necessarie tooreset, come le domande di sicurezza selezionate durante la reimpostazione?**</span><span class="sxs-lookup"><span data-stu-id="e82da-173">**Q:  If a user has registered more than hello maximum number of questions required tooreset, how are security questions selected during reset?**</span></span>

  > <span data-ttu-id="e82da-174">**R:** sicurezza N domande vengono selezionate casualmente rispetto totale hello di domande che un utente è registrato, dove N è hello **numero di domande necessarie tooreset**.</span><span class="sxs-lookup"><span data-stu-id="e82da-174">**A:** N security questions are selected at random out of hello total number of questions a user has registered for, where N is hello **Number of questions required tooreset**.</span></span> <span data-ttu-id="e82da-175">Ad esempio, se un utente ha registrato 5 domande di sicurezza, ma solo 3 sono necessari tooreset, sono selezionati in modo casuale 3 di 5 hello e sono presentati alla reimpostazione.</span><span class="sxs-lookup"><span data-stu-id="e82da-175">For example, if a user has 5 security questions registered, but only 3 are required tooreset, 3 of hello 5 are selected randomly and presented at reset.</span></span> <span data-ttu-id="e82da-176">Se l'utente hello Ottiene le risposte hello domande toohello errato, si ripete il processo di selezione hello tooprevent domanda hammering.</span><span class="sxs-lookup"><span data-stu-id="e82da-176">If hello user gets hello answers toohello questions wrong, hello selection process reoccurs tooprevent question hammering.</span></span>
  >
  >
* <span data-ttu-id="e82da-177">**D: Viene impedito agli utenti di provare a reimpostare la password più volte in un breve periodo di tempo?**</span><span class="sxs-lookup"><span data-stu-id="e82da-177">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span></span>

  > <span data-ttu-id="e82da-178">**R:** Sì, sono disponibili funzionalità di sicurezza incorporate in tooprotect di reimpostazione della password da utilizzi impropri.</span><span class="sxs-lookup"><span data-stu-id="e82da-178">**A:** Yes, there are security features built into password reset tooprotect from misuse.</span></span> <span data-ttu-id="e82da-179">Gli utenti possono effettuare solo 5 tentativi di reimpostazione della password nell'arco di un'ora, prima di essere bloccati per 24 ore.</span><span class="sxs-lookup"><span data-stu-id="e82da-179">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="e82da-180">Gli utenti possono provare solo toovalidate un numero di telefono 5 volte entro un'ora prima di essere bloccati per 24 ore.</span><span class="sxs-lookup"><span data-stu-id="e82da-180">Users may only try toovalidate a phone number 5 times within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="e82da-181">Gli utenti possono provare solo 5 volte un singolo metodo di autenticazione nell'arco di un'ora, prima di essere bloccati per 24 ore.</span><span class="sxs-lookup"><span data-stu-id="e82da-181">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span></span>
  >
  >
* <span data-ttu-id="e82da-182">**D: per quanto tempo è posta elettronica hello e passcode monouso SMS valido?**</span><span class="sxs-lookup"><span data-stu-id="e82da-182">**Q:  For how long are hello email and SMS one-time passcode valid?**</span></span>

  > <span data-ttu-id="e82da-183">**R:** hello durata della sessione per la reimpostazione della password è di 105 minuti.</span><span class="sxs-lookup"><span data-stu-id="e82da-183">**A:** hello session lifetime for password reset is 105 minutes.</span></span> <span data-ttu-id="e82da-184">Da inizio hello di hello operazione di reimpostazione della password, utente hello ha 105 minuti tooreset la propria password.</span><span class="sxs-lookup"><span data-stu-id="e82da-184">From hello beginning of hello password reset operation, hello user has 105 minutes tooreset their password.</span></span> <span data-ttu-id="e82da-185">Hello posta elettronica e il passcode monouso SMS non sono validi dopo questo periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="e82da-185">hello email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="e82da-186">Modifica della password</span><span class="sxs-lookup"><span data-stu-id="e82da-186">Password change</span></span>
* <span data-ttu-id="e82da-187">**D: dove gli utenti diverranno toochange le proprie password?**</span><span class="sxs-lookup"><span data-stu-id="e82da-187">**Q:  Where should my users go toochange their passwords?**</span></span>

  > <span data-ttu-id="e82da-188">**R:** gli utenti possono modificare le password in qualsiasi punto visualizzano le immagine del profilo o l'icona (come in hello angolo superiore destro della loro [Office 365](https://portal.office.com) o [Pannello di accesso](https://myapps.microsoft.com) esperienze.</span><span class="sxs-lookup"><span data-stu-id="e82da-188">**A:** Users may change their passwords anywhere they see their profile picture or icon (like in hello upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="e82da-189">Gli utenti possono modificare le password da hello [pagina del profilo di Pannello di accesso](https://account.activedirectory.windowsazure.com/r#/profile).</span><span class="sxs-lookup"><span data-stu-id="e82da-189">Users may change their passwords from hello [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="e82da-190">Gli utenti possono inoltre essere richiesto toochange le proprie password automaticamente nella schermata di accesso hello Azure AD, se la password è scaduta.</span><span class="sxs-lookup"><span data-stu-id="e82da-190">Users may also be asked toochange their passwords automatically at hello Azure AD sign-in screen if their passwords have expired.</span></span> <span data-ttu-id="e82da-191">Infine, gli utenti possono spostarsi toohello [portale di modifica Password di Azure AD](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) direttamente se desiderano toochange le proprie password.</span><span class="sxs-lookup"><span data-stu-id="e82da-191">Finally, users may navigate toohello [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish toochange their passwords.</span></span>
  >
  >
* <span data-ttu-id="e82da-192">**D: è possibile agli utenti una notifica nel portale di Office hello quando scade la password in locale?**</span><span class="sxs-lookup"><span data-stu-id="e82da-192">**Q:  Can my users be notified in hello Office Portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="e82da-193">**R:** attualmente è possibile se si utilizza ADFS seguendo le istruzioni di hello qui: [l'invio di attestazioni di criteri Password con ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="e82da-193">**A:** This is possible today if you are using ADFS by following hello instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="e82da-194">Se si usa la sincronizzazione dell'hash della password, al momento non è possibile.</span><span class="sxs-lookup"><span data-stu-id="e82da-194">If you are using password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="e82da-195">Infatti, non è la sincronizzazione criteri password locale, pertanto non è possibile che ci toopost scadenza notifiche toocloud esperienze.</span><span class="sxs-lookup"><span data-stu-id="e82da-195">This is because we do not sync password policies from on-premises, so it is not possible for us toopost expiry notifications toocloud experiences.</span></span> <span data-ttu-id="e82da-196">In entrambi i casi, è anche possibile troppo[notificare agli utenti le cui password stanno tooexpire tramite PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span><span class="sxs-lookup"><span data-stu-id="e82da-196">In either case, it is also possible too[notify users whose passwords are about tooexpire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="e82da-197">Report di gestione delle password</span><span class="sxs-lookup"><span data-stu-id="e82da-197">Password management reports</span></span>
* <span data-ttu-id="e82da-198">**D: come tempo occorre per dati tooshow backup nei report di gestione di password hello?**</span><span class="sxs-lookup"><span data-stu-id="e82da-198">**Q:  How long does it take for data tooshow up on hello password management reports?**</span></span>

  > <span data-ttu-id="e82da-199">**R:** dati devono essere visualizzati nei report di gestione di hello password entro 5-10 minuti.</span><span class="sxs-lookup"><span data-stu-id="e82da-199">**A:** Data should appear on hello password management reports within 5-10 minutes.</span></span> <span data-ttu-id="e82da-200">Alcune istanze potrebbe richiedere fino a tooan ora tooappear.</span><span class="sxs-lookup"><span data-stu-id="e82da-200">It some instances it may take up tooan hour tooappear.</span></span>
  >
  >
* <span data-ttu-id="e82da-201">**D: come è possibile filtrare i report di gestione di password hello?**</span><span class="sxs-lookup"><span data-stu-id="e82da-201">**Q:  How can I filter hello password management reports?**</span></span>

  > <span data-ttu-id="e82da-202">**R:** è possibile filtrare i report di gestione di password hello facendo hello piccola lente di ingrandimento toohello estremità destra delle etichette di colonna hello, parte superiore di hello del report hello.</span><span class="sxs-lookup"><span data-stu-id="e82da-202">**A:** You can filter hello password management reports by clicking hello small magnifying glass toohello extreme right of hello column labels, near hello top of hello report.</span></span> <span data-ttu-id="e82da-203">Se si desidera toodo di filtro più completa, è possibile scaricare tooexcel report hello e creare una tabella pivot.</span><span class="sxs-lookup"><span data-stu-id="e82da-203">If you want toodo richer filtering, you can download hello report tooexcel and create a pivot table.</span></span>
  >
  >
* <span data-ttu-id="e82da-204">**D: qual è il numero massimo di hello degli eventi vengono archiviati nel report di gestione di password hello?**</span><span class="sxs-lookup"><span data-stu-id="e82da-204">**Q: What is hello maximum number of events are stored in hello password management reports?**</span></span>

  > <span data-ttu-id="e82da-205">**R:** backup too75, 000 password Reimposta o password registrazione eventi di reimpostazione vengono archiviati nel report di gestione password hello, spanning too30 giorni di backup.</span><span class="sxs-lookup"><span data-stu-id="e82da-205">**A:** Up too75,000 password reset or password reset registration events are stored in hello password management reports, spanning back up too30 days.</span></span>  <span data-ttu-id="e82da-206">Stiamo lavorando tooexpand questo numero tooinclude più eventi.</span><span class="sxs-lookup"><span data-stu-id="e82da-206">We are working tooexpand this number tooinclude more events.</span></span>
  >
  >
* <span data-ttu-id="e82da-207">**Q: fino passare hello report di gestione delle password?**</span><span class="sxs-lookup"><span data-stu-id="e82da-207">**Q:  How far back do hello password management reports go?**</span></span>

  > <span data-ttu-id="e82da-208">**R:** la gestione delle password hello report mostra le operazioni che si verificano all'interno di hello ultimi 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="e82da-208">**A:** hello password management reports show operations occurring within hello last 30 days.</span></span> <span data-ttu-id="e82da-209">Per il momento, se è necessario tooarchive questi dati, si scaricare periodicamente report di hello e salvarli in una posizione separata.</span><span class="sxs-lookup"><span data-stu-id="e82da-209">For now, if you need tooarchive this data, you can download hello reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="e82da-210">**D: è presente un numero massimo di righe che possono essere visualizzati nei report di gestione di password hello?**</span><span class="sxs-lookup"><span data-stu-id="e82da-210">**Q:  Is there a maximum number of rows that can appear on hello password management reports?**</span></span>

  > <span data-ttu-id="e82da-211">**R:** Sì, in uno dei report di gestione delle password di hello, può essere visualizzato un massimo di 75.000 righe se vengono visualizzati nella hello dell'interfaccia utente o in corso il download.</span><span class="sxs-lookup"><span data-stu-id="e82da-211">**A:** Yes, a maximum of 75,000 rows may appear on either of hello password management reports, whether they are being shown in hello UI or being downloaded.</span></span>
  >
  >
* <span data-ttu-id="e82da-212">**D: è un'API tooaccess hello password Reimposta o registrazione dati dei report?**</span><span class="sxs-lookup"><span data-stu-id="e82da-212">**Q:  Is there an API tooaccess hello password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="e82da-213">**R:** Sì, vedere hello seguenti toolearn documentazione come accedere a password hello reimpostare reporting flusso di dati.</span><span class="sxs-lookup"><span data-stu-id="e82da-213">**A:** Yes, see hello following documentation toolearn how you can access hello password reset reporting data stream.</span></span>  <span data-ttu-id="e82da-214">[Informazioni su come tooaccess di reimpostazione della password eventi di reporting a livello di codice](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span><span class="sxs-lookup"><span data-stu-id="e82da-214">[Learn how tooaccess password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="e82da-215">Writeback delle password</span><span class="sxs-lookup"><span data-stu-id="e82da-215">Password writeback</span></span>
* <span data-ttu-id="e82da-216">**D: come funziona il writeback delle password in background hello?**</span><span class="sxs-lookup"><span data-stu-id="e82da-216">**Q:  How does password writeback work behind hello scenes?**</span></span>

  > <span data-ttu-id="e82da-217">**R:** vedere [funzionamento di writeback delle password](active-directory-passwords-writeback.md) per una spiegazione di ciò che accade quando si abilita il writeback delle password e il flusso dei dati tramite il sistema hello nuovamente nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="e82da-217">**A:** See [How password writeback works](active-directory-passwords-writeback.md) for an explanation of what happens when you enable password writeback, and how data flows through hello system back into your on-premises environment.</span></span>
  >
  >
* <span data-ttu-id="e82da-218">**D: come writeback delle password tempo toowork?  Esiste un ritardo di sincronizzazione come per la sincronizzazione di hash della password?**</span><span class="sxs-lookup"><span data-stu-id="e82da-218">**Q:  How long does password writeback take toowork?  Is there a synchronization delay like with password hash sync?**</span></span>

  > <span data-ttu-id="e82da-219">**R:** Il writeback delle password è immediato.</span><span class="sxs-lookup"><span data-stu-id="e82da-219">**A:** Password writeback is instant.</span></span> <span data-ttu-id="e82da-220">Si tratta di una pipeline sincrona che funziona fondamentalmente in modo diverso rispetto alla sincronizzazione di hash della password.</span><span class="sxs-lookup"><span data-stu-id="e82da-220">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="e82da-221">Writeback delle password consente agli utenti tooget feedback in tempo reale sulla riuscita hello del loro password reimpostare o modificare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="e82da-221">Password writeback allows users tooget real-time feedback about hello success of their password reset or change operation.</span></span> <span data-ttu-id="e82da-222">tempo medio di Hello per un writeback della password riuscito è inferiore a 500 ms.</span><span class="sxs-lookup"><span data-stu-id="e82da-222">hello average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="e82da-223">**D: Se l'account locale è disabilitato, cosa succede all'accesso o all'account cloud?**</span><span class="sxs-lookup"><span data-stu-id="e82da-223">**Q:  If my on-premises account is disabled, how is my cloud account/access affected?**</span></span>

  > <span data-ttu-id="e82da-224">**R:** se l'ID locale è disabilitato, il cloud verranno disabilitata anche ID o l'accesso all'intervallo di sincronizzazione successivo di hello mediante AAD Connect byt predefinito tratta ogni 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="e82da-224">**A:** If your on-premises ID is disabled, your cloud ID/access will also be disabled at hello next sync interval via AAD Connect byt default this is every 30 minutes.</span></span>
  >
  >
* <span data-ttu-id="e82da-225">**D: se l'account locale è vincolato da un criterio di password di Active Directory locale, SSPR rispetta questo criterio quando si modifica la password di hello?**</span><span class="sxs-lookup"><span data-stu-id="e82da-225">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change hello password?**</span></span>

  > <span data-ttu-id="e82da-226">**R:** Sì, SSPR si basa su e ha aderito all'accordo hello locale criteri password di Active Directory, inclusi i criteri password di dominio Active Directory tipico, nonché eventuali criteri password granulari definiti tooa dato utente di destinazione.</span><span class="sxs-lookup"><span data-stu-id="e82da-226">**A:** Yes, SSPR relies on and abides by hello on-premises AD password policy, including typical AD domain password policy, as well as any defined fine grained password policies targeted tooa given user.</span></span>
  >
  >
* <span data-ttu-id="e82da-227">**D: Per quali tipi di account funziona il writeback delle password?**</span><span class="sxs-lookup"><span data-stu-id="e82da-227">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="e82da-228">**R:** Funziona per gli utenti federati e con sincronizzazione di hash della password.</span><span class="sxs-lookup"><span data-stu-id="e82da-228">**A:** Password writeback works for Federated and Password Hash Synchronized users.</span></span>
  >
  >
* <span data-ttu-id="e82da-229">**D: Il writeback delle password applica i criteri di password del dominio?**</span><span class="sxs-lookup"><span data-stu-id="e82da-229">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="e82da-230">**R:** Sì, applica validità, cronologia, complessità, filtri e qualsiasi altra restrizione eventualmente applicata alle password nel dominio locale.</span><span class="sxs-lookup"><span data-stu-id="e82da-230">**A:** Yes, password writeback enforces password age, history, complexity, filters, and any other restriction you may put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="e82da-231">**D: Il writeback delle password è sicuro?  Come si può essere certi di non essere oggetto di un attacco?**</span><span class="sxs-lookup"><span data-stu-id="e82da-231">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="e82da-232">**R:** Sì, il writeback delle password è sicuro.</span><span class="sxs-lookup"><span data-stu-id="e82da-232">**A:** Yes, password writeback is secure.</span></span> <span data-ttu-id="e82da-233">tooread ulteriori informazioni sui livelli di hello quattro di sicurezza implementata dal servizio di writeback della password hello, estrarre hello [modello di sicurezza di writeback della Password](active-directory-passwords-writeback.md#password-writeback-security-model) sezione nel funzionamento di writeback delle password.</span><span class="sxs-lookup"><span data-stu-id="e82da-233">tooread more about hello four layers of security implemented by hello password writeback service, check out hello [Password writeback security model](active-directory-passwords-writeback.md#password-writeback-security-model) section in How password writeback works.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="e82da-234">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e82da-234">Next steps</span></span>

<span data-ttu-id="e82da-235">Hello seguenti collegamenti fornisce ulteriori informazioni sull'uso di Azure AD di reimpostazione della password</span><span class="sxs-lookup"><span data-stu-id="e82da-235">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="e82da-236">[**Guida introduttiva**](active-directory-passwords-getting-started.md) - Iniziare a usare la gestione self-service delle password di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e82da-236">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="e82da-237">[**Licenze**](active-directory-passwords-licensing.md) - configurare le licenze di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e82da-237">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="e82da-238">[**Dati** ](active-directory-passwords-data.md) : comprendere hello i dati necessari e come utilizzarlo per la gestione delle password</span><span class="sxs-lookup"><span data-stu-id="e82da-238">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="e82da-239">[**Implementazione** ](active-directory-passwords-best-practices.md) -pianificare e distribuire agli utenti di tooyour SSPR utilizzando istruzioni hello disponibili qui</span><span class="sxs-lookup"><span data-stu-id="e82da-239">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="e82da-240">[**Personalizzare** ](active-directory-passwords-customize.md) -personalizzare hello aspetto di hello SSPR esperienza per l'azienda.</span><span class="sxs-lookup"><span data-stu-id="e82da-240">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="e82da-241">[**Creazione di report**](active-directory-passwords-reporting.md) - verificare se, quando e dove gli utenti accedono alla reimpostazione password self-service</span><span class="sxs-lookup"><span data-stu-id="e82da-241">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="e82da-242">[**Criteri**](active-directory-passwords-policy.md): comprendere e impostare i criteri password di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e82da-242">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="e82da-243">[**Writeback delle password**](active-directory-passwords-writeback.md): funzionamento del writeback delle password con la directory locale</span><span class="sxs-lookup"><span data-stu-id="e82da-243">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="e82da-244">[**Approfondimento tecnico** ](active-directory-passwords-how-it-works.md) -Vai dietro hello pannelli toounderstand come funziona</span><span class="sxs-lookup"><span data-stu-id="e82da-244">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="e82da-245">[**Risoluzione dei problemi** ](active-directory-passwords-troubleshoot.md) -informazioni su come tooresolve comuni problemi che vedremo con SSPR</span><span class="sxs-lookup"><span data-stu-id="e82da-245">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
