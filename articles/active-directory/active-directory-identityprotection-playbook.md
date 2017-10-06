---
title: "playbook la protezione dell'identità di Active Directory aaaAzure | Documenti Microsoft"
description: "Informazioni su come Azure AD Identity Protection consenta il possibilità hello toolimit di un tooexploit malintenzionato un'identità compromessa o il dispositivo e toosecure un'identità o un dispositivo che in precedenza era noto o sospetta toobe compromesso."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestione applicazioni, sicurezza, rischio, livello di rischio, vulnerabilità, criteri di sicurezza"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6252bc133fc0c0f84800ee245a04bbf62d4cd25b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a><span data-ttu-id="97243-104">Studio sulla protezione delle identità di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97243-104">Azure Active Directory Identity Protection playbook</span></span>
<span data-ttu-id="97243-105">Questo studio consente di:</span><span class="sxs-lookup"><span data-stu-id="97243-105">This playbook helps you to:</span></span>

* <span data-ttu-id="97243-106">Popolare i dati nell'ambiente di protezione dell'identità hello da simulare eventi di rischio e vulnerabilità</span><span class="sxs-lookup"><span data-stu-id="97243-106">Populate data in hello Identity Protection environment by simulating risk events and vulnerabilities</span></span>
* <span data-ttu-id="97243-107">Impostare i criteri di accesso condizionale basati sui rischi e hello impatto di questi criteri di test</span><span class="sxs-lookup"><span data-stu-id="97243-107">Set up risk-based conditional access policies and test hello impact of these policies</span></span>

## <a name="simulating-risk-events"></a><span data-ttu-id="97243-108">Simulazione di eventi di rischio</span><span class="sxs-lookup"><span data-stu-id="97243-108">Simulating Risk Events</span></span>
<span data-ttu-id="97243-109">Questa sezione fornisce passaggi per la simulazione hello seguenti tipi di eventi di rischio:</span><span class="sxs-lookup"><span data-stu-id="97243-109">This section provides you with steps for simulating hello following risk event types:</span></span>

* <span data-ttu-id="97243-110">Accessi da indirizzi IP anonimi (facile)</span><span class="sxs-lookup"><span data-stu-id="97243-110">Sign-ins from anonymous IP addresses (easy)</span></span>
* <span data-ttu-id="97243-111">Accessi da posizioni non note (intermedio)</span><span class="sxs-lookup"><span data-stu-id="97243-111">Sign-ins from unfamiliar locations (moderate)</span></span>
* <span data-ttu-id="97243-112">Impossibile tooatypical corsa (complesso)</span><span class="sxs-lookup"><span data-stu-id="97243-112">Impossible travel tooatypical locations (difficult)</span></span>

<span data-ttu-id="97243-113">Non è possibile simulare altri eventi di rischio in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="97243-113">Other risk events cannot be simulated in a secure manner.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="97243-114">Accessi da indirizzi IP anonimi</span><span class="sxs-lookup"><span data-stu-id="97243-114">Sign-ins from anonymous IP addresses</span></span>
<span data-ttu-id="97243-115">Questo tipo di evento di rischio identifica gli utenti che hanno eseguito l'accesso da un indirizzo IP riconosciuto come un indirizzo IP proxy anonimo.</span><span class="sxs-lookup"><span data-stu-id="97243-115">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="97243-116">Questi proxy vengono utilizzati dagli utenti che desiderano toohide indirizzo IP del dispositivo in uso e possono essere utilizzate per fini dannosi.</span><span class="sxs-lookup"><span data-stu-id="97243-116">These proxies are used by people who want toohide their device’s IP address and may be used for malicious intent.</span></span>

<span data-ttu-id="97243-117">**toosimulate sign-in da un IP anonimo, eseguire operazioni hello**:</span><span class="sxs-lookup"><span data-stu-id="97243-117">**toosimulate a sign-in from an anonymous IP, perform hello following steps**:</span></span>

1. <span data-ttu-id="97243-118">Scaricare hello [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span><span class="sxs-lookup"><span data-stu-id="97243-118">Download hello [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span></span>
2. <span data-ttu-id="97243-119">Utilizzando hello Tor Browser, passare troppo[https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="97243-119">Using hello Tor Browser, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>   
3. <span data-ttu-id="97243-120">Immettere le credenziali di hello di account di hello si vuole tooappear in hello **accessi da indirizzi IP anonimi** report.</span><span class="sxs-lookup"><span data-stu-id="97243-120">Enter hello credentials of hello account you want tooappear in hello **Sign-ins from anonymous IP addresses** report.</span></span>

<span data-ttu-id="97243-121">Accedi Hello verranno visualizzati nel dashboard di protezione dell'identità hello entro 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="97243-121">hello sign-in will show up on hello Identity Protection dashboard within 5 minutes.</span></span> 

### <a name="sign-ins-from-unfamiliar-locations"></a><span data-ttu-id="97243-122">Accessi da posizioni non note</span><span class="sxs-lookup"><span data-stu-id="97243-122">Sign-ins from unfamiliar locations</span></span>
<span data-ttu-id="97243-123">rischio posizioni non familiari Hello è un meccanismo di valutazione dell'accesso in tempo reale che prende in considerazione oltre i percorsi di accesso (IP, latitudine / longitudine e ASN) toodetermine nuovo / familiarità percorsi.</span><span class="sxs-lookup"><span data-stu-id="97243-123">hello unfamiliar locations risk is a real-time sign-in evaluation mechanism that considers past sign-in locations (IP, Latitude / Longitude and ASN) toodetermine new / unfamiliar locations.</span></span> <span data-ttu-id="97243-124">sistema Hello archivia gli indirizzi IP precedente, latitudine / longitudine e ASN di un utente e considera questi percorsi familiarità toobe.</span><span class="sxs-lookup"><span data-stu-id="97243-124">hello system stores previous IPs, Latitude / Longitude, and ASNs of a user and considers these toobe familiar locations.</span></span> <span data-ttu-id="97243-125">Un percorso di accesso viene considerato non familiare se hello posizione di accesso non corrisponde a nessuno dei percorsi familiarità esistente hello.</span><span class="sxs-lookup"><span data-stu-id="97243-125">A sign-in location is considered unfamiliar if hello sign-in location does not match any of hello existing familiar locations.</span></span>

<span data-ttu-id="97243-126">Azure Active Directory Identity Protection:</span><span class="sxs-lookup"><span data-stu-id="97243-126">Azure Active Directory Identity Protection:</span></span>  

* <span data-ttu-id="97243-127">ha un periodo di apprendimento iniziale di 14 giorni, durante i quali le nuove posizioni non vengono contrassegnate come posizioni non note.</span><span class="sxs-lookup"><span data-stu-id="97243-127">has an initial learning period of 14 days during which it does not flag any new locations as unfamiliar locations.</span></span>
* <span data-ttu-id="97243-128">Ignora accessi da dispositivi familiarità e percorsi di posizione familiare esistente tooan geograficamente Chiudi.</span><span class="sxs-lookup"><span data-stu-id="97243-128">ignores sign-ins from familiar devices and locations that are geographically close tooan existing familiar location.</span></span>

<span data-ttu-id="97243-129">posizioni non familiari toosimulate, aver toosign in un percorso e un dispositivo che account hello ha non eseguito l'accesso dalla prima.</span><span class="sxs-lookup"><span data-stu-id="97243-129">toosimulate unfamiliar locations, you have toosign in from a location and device that hello account has not signed in from before.</span></span> 

<span data-ttu-id="97243-130">**toosimulate sign-in da una posizione familiarità, eseguire hello alla procedura seguente**:</span><span class="sxs-lookup"><span data-stu-id="97243-130">**toosimulate a sign-in from an unfamiliar location, perform hello following steps**:</span></span>

1. <span data-ttu-id="97243-131">Scegliere un account che abbia una cronologia di accesso di almeno 14 giorni.</span><span class="sxs-lookup"><span data-stu-id="97243-131">Choose an account that has at least a 14-day sign-in history.</span></span> 
2. <span data-ttu-id="97243-132">È possibile procedere in due modi:</span><span class="sxs-lookup"><span data-stu-id="97243-132">Do either:</span></span>
   
   <span data-ttu-id="97243-133">a.</span><span class="sxs-lookup"><span data-stu-id="97243-133">a.</span></span> <span data-ttu-id="97243-134">Quando si utilizza una connessione VPN, passare troppo[https://myapps.microsoft.com](https://myapps.microsoft.com) e immettere le credenziali di hello di account di hello si vuole toosimulate hello rischio relativo.</span><span class="sxs-lookup"><span data-stu-id="97243-134">While using a VPN, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com) and enter hello credentials of hello account you want toosimulate hello risk event for.</span></span>
   
   <span data-ttu-id="97243-135">b.</span><span class="sxs-lookup"><span data-stu-id="97243-135">b.</span></span> <span data-ttu-id="97243-136">Chiedere a un collega in toosign un percorso diverso utilizzando le credenziali dell'account hello (scelta non consigliate).</span><span class="sxs-lookup"><span data-stu-id="97243-136">Ask an associate in a different location toosign in using hello account’s credentials (not recommended).</span></span>

<span data-ttu-id="97243-137">Accedi Hello verranno visualizzati nel dashboard di protezione dell'identità hello entro 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="97243-137">hello sign-in will show up on hello Identity Protection dashboard within 5 minutes.</span></span>

### <a name="impossible-travel-tooatypical-location"></a><span data-ttu-id="97243-138">Impossibile tooatypical viaggio.</span><span class="sxs-lookup"><span data-stu-id="97243-138">Impossible travel tooatypical location</span></span>
<span data-ttu-id="97243-139">Simulazione di condizione di comunicazione Impossibile: hello è difficile perché l'algoritmo hello Usa machine learning tooweed out falsi positivi, ad esempio viaggio Impossibile da dispositivi familiari o accessi da connessioni VPN che vengono utilizzati da altri utenti nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="97243-139">Simulating hello impossible travel condition is difficult because hello algorithm uses machine learning tooweed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in hello directory.</span></span> <span data-ttu-id="97243-140">Algoritmo hello richiede inoltre una cronologia di accesso di 3 giorni too14 per utente hello prima di avviare la generazione di eventi di rischio.</span><span class="sxs-lookup"><span data-stu-id="97243-140">Additionally, hello algorithm requires a sign-in history of 3 too14 days for hello user before it begins generating risk events.</span></span>

<span data-ttu-id="97243-141">**toosimulate un impossibili tooatypical viaggio, eseguire hello alla procedura seguente**:</span><span class="sxs-lookup"><span data-stu-id="97243-141">**toosimulate an impossible travel tooatypical location, perform hello following steps**:</span></span>

1. <span data-ttu-id="97243-142">Utilizzando il browser standard, passare troppo[https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="97243-142">Using your standard browser, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>  
2. <span data-ttu-id="97243-143">Immettere le credenziali di hello di account di hello per che si vuole toogenerate un evento di rischio per la comunicazione Impossibile.</span><span class="sxs-lookup"><span data-stu-id="97243-143">Enter hello credentials of hello account you want toogenerate an impossible travel risk event for.</span></span>
3. <span data-ttu-id="97243-144">Modificare l'agente utente.</span><span class="sxs-lookup"><span data-stu-id="97243-144">Change your user agent.</span></span> <span data-ttu-id="97243-145">Per modificare l'agente utente in Internet Explorer, usare Strumenti di sviluppo. Per modificare l'agente utente in Firefox o Chrome, usare un componente aggiuntivo di selezione dell'agente utente.</span><span class="sxs-lookup"><span data-stu-id="97243-145">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span></span>
4. <span data-ttu-id="97243-146">Modificare l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="97243-146">Change your IP address.</span></span> <span data-ttu-id="97243-147">È possibile modificare l'indirizzo IP usando una VPN, un componente aggiuntivo Tor o avviare un nuovo computer in Azure in un altro data center.</span><span class="sxs-lookup"><span data-stu-id="97243-147">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span></span>
5. <span data-ttu-id="97243-148">Accedi troppo[https://myapps.microsoft.com](https://myapps.microsoft.com) utilizzando hello stesse credenziali come prima ed entro pochi minuti dopo hello precedente accesso.</span><span class="sxs-lookup"><span data-stu-id="97243-148">Sign-in too[https://myapps.microsoft.com](https://myapps.microsoft.com) using hello same credentials as before and within a few minutes after hello previous sign-in.</span></span>

<span data-ttu-id="97243-149">Accedi Hello verranno visualizzati nel dashboard di protezione dell'identità hello entro 2-4 ore.</span><span class="sxs-lookup"><span data-stu-id="97243-149">hello sign-in will show up in hello Identity Protection dashboard within 2-4 hours.</span></span><br>
<span data-ttu-id="97243-150">A causa di hello complesso modelli di machine learning coinvolti, è probabile che sarà non prelevata.</span><span class="sxs-lookup"><span data-stu-id="97243-150">Because of hello complex machine learning models involved, there is a chance it will not get picked up.</span></span><br> <span data-ttu-id="97243-151">È possibile tooreplicate questi passaggi per più account di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97243-151">You might want tooreplicate these steps for multiple Azure AD accounts.</span></span>

## <a name="simulating-vulnerabilities"></a><span data-ttu-id="97243-152">Simulazione di vulnerabilità</span><span class="sxs-lookup"><span data-stu-id="97243-152">Simulating vulnerabilities</span></span>
<span data-ttu-id="97243-153">Le vulnerabilità sono punti deboli in un ambiente Azure AD che possono essere sfruttati da un utente malintenzionato.</span><span class="sxs-lookup"><span data-stu-id="97243-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span></span> <span data-ttu-id="97243-154">In Azure AD Identity Protection sono attualmente visibili 3 tipi di vulnerabilità che consentono di sfruttare altre funzionalità di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97243-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span></span> <span data-ttu-id="97243-155">Queste vulnerabilità verranno visualizzate nel dashboard di protezione dell'identità hello automaticamente una volta impostate queste funzionalità.</span><span class="sxs-lookup"><span data-stu-id="97243-155">These Vulnerabilities will be displayed on hello Identity Protection dashboard automatically once these features are set up.</span></span>

* <span data-ttu-id="97243-156">Azure AD [Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="97243-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>
* <span data-ttu-id="97243-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="97243-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
* <span data-ttu-id="97243-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="97243-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="user-compromise-risk"></a><span data-ttu-id="97243-159">Rischio di compromissione dell'utente</span><span class="sxs-lookup"><span data-stu-id="97243-159">User compromise risk</span></span>
<span data-ttu-id="97243-160">**tootest il rischio di manomissione di utente, eseguire operazioni hello**:</span><span class="sxs-lookup"><span data-stu-id="97243-160">**tootest User compromise risk, perform hello following steps**:</span></span>

1. <span data-ttu-id="97243-161">Accedi troppo[https://portal.azure.com](https://portal.azure.com) con credenziali di amministratore globale per il tenant.</span><span class="sxs-lookup"><span data-stu-id="97243-161">Sign-in too[https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="97243-162">Passare troppo**Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="97243-162">Navigate too**Identity Protection**.</span></span> 
3. <span data-ttu-id="97243-163">Nella finestra principale di hello **Azure AD Identity Protection** pannello, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="97243-163">On hello main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="97243-164">In hello **le impostazioni del portale** pannello, in **regole di sicurezza**, fare clic su **il rischio di compromissione utente**.</span><span class="sxs-lookup"><span data-stu-id="97243-164">On hello **Portal Settings** blade, under **Security rules**, click **User compromise risk**.</span></span> 
5. <span data-ttu-id="97243-165">In hello **Accedi rischio** pannello, attivare **Abilita regola** off e quindi fare clic su **salvare** impostazioni.</span><span class="sxs-lookup"><span data-stu-id="97243-165">On hello **Sign in Risk** blade, turn **Enable rule** off, and then click **Save** settings.</span></span>
6. <span data-ttu-id="97243-166">Per un determinato account utente, simulare un evento di rischio IP anonimo o posizione non nota.</span><span class="sxs-lookup"><span data-stu-id="97243-166">For a given user account, simulate an unfamiliar locations or anonymous IP risk event.</span></span> <span data-ttu-id="97243-167">Questo verrà elevare un livello di rischio hello utente per tale utente troppo**Media**.</span><span class="sxs-lookup"><span data-stu-id="97243-167">This will elevate hello user risk level for that user too**Medium**.</span></span>
7. <span data-ttu-id="97243-168">Attendere alcuni minuti e poi verificare che il livello utente sia **Medio**.</span><span class="sxs-lookup"><span data-stu-id="97243-168">Wait a few minutes, and then verify that user level for your user is **Medium**.</span></span>
8. <span data-ttu-id="97243-169">Passare toohello **le impostazioni del portale** blade.</span><span class="sxs-lookup"><span data-stu-id="97243-169">Go toohello **Portal Settings** blade.</span></span>
9. <span data-ttu-id="97243-170">In hello **il rischio di compromissione utente** pannello, in **Abilita regola**selezionare **su** .</span><span class="sxs-lookup"><span data-stu-id="97243-170">On hello **User Compromise Risk** blade, under **Enable rule**, select **On** .</span></span> 
10. <span data-ttu-id="97243-171">Selezionare una delle seguenti opzioni hello:</span><span class="sxs-lookup"><span data-stu-id="97243-171">Select one of hello following options:</span></span>
    
    <span data-ttu-id="97243-172">a.</span><span class="sxs-lookup"><span data-stu-id="97243-172">a.</span></span> <span data-ttu-id="97243-173">tooblock, selezionare **Media** in **blocco Accedi**.</span><span class="sxs-lookup"><span data-stu-id="97243-173">tooblock, select **Medium** under **Block sign in**.</span></span>
    
    <span data-ttu-id="97243-174">b.</span><span class="sxs-lookup"><span data-stu-id="97243-174">b.</span></span> <span data-ttu-id="97243-175">modifica della password sicura tooenforce, selezionare **Media** in **richiede l'autenticazione a più fattori**.</span><span class="sxs-lookup"><span data-stu-id="97243-175">tooenforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
11. <span data-ttu-id="97243-176">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="97243-176">Click **Save**.</span></span>
12. <span data-ttu-id="97243-177">A questo punto è possibile testare l'accesso condizionale basato sul rischio eseguendo l'accesso come un utente con un livello di rischio elevato.</span><span class="sxs-lookup"><span data-stu-id="97243-177">You can now test risk-based conditional access by signing in using a user with an elevated risk level.</span></span> <span data-ttu-id="97243-178">Se il rischio di utente hello è Media, a seconda della configurazione di hello dei criteri, l'accesso è sia bloccato o se è necessario toochange la password.</span><span class="sxs-lookup"><span data-stu-id="97243-178">If hello user risk is Medium, depending on hello configuration of your policy, your sign-in is be either blocked or you are forced toochange your password.</span></span> 
    <br><br><span data-ttu-id="97243-179">
    ![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
    </span><span class="sxs-lookup"><span data-stu-id="97243-179">
![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
</span></span><br>

## <a name="sign-in-risk"></a><span data-ttu-id="97243-180">Rischio di accesso</span><span class="sxs-lookup"><span data-stu-id="97243-180">Sign-in risk</span></span>
<span data-ttu-id="97243-181">**tootest Accedi rischio, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="97243-181">**tootest a sign in risk, perform hello following steps:**</span></span>

1. <span data-ttu-id="97243-182">Accedi troppo[https://portal.azure.com ](https://portal.azure.com) con credenziali di amministratore globale per il tenant.</span><span class="sxs-lookup"><span data-stu-id="97243-182">Sign-in too[https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="97243-183">Passare troppo**Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="97243-183">Navigate too**Identity Protection**.</span></span>
3. <span data-ttu-id="97243-184">Nella finestra principale di hello **Azure AD Identity Protection** pannello, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="97243-184">On hello main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="97243-185">In hello **le impostazioni del portale** pannello, in **regole di sicurezza**, fare clic su **Accedi rischio**.</span><span class="sxs-lookup"><span data-stu-id="97243-185">On hello **Portal Settings** blade, under **Security rules**, click **Sign in risk**.</span></span>
5. <span data-ttu-id="97243-186">In hello * * Accedi rischio * * pannello seleziona **su** in **Abilita regola**.</span><span class="sxs-lookup"><span data-stu-id="97243-186">On hello **Sign in Risk **blade, select **On** under **Enable rule**.</span></span> 
6. <span data-ttu-id="97243-187">Selezionare una delle seguenti opzioni hello:</span><span class="sxs-lookup"><span data-stu-id="97243-187">Select one of hello following options:</span></span>
   
   <span data-ttu-id="97243-188">a.</span><span class="sxs-lookup"><span data-stu-id="97243-188">a.</span></span> <span data-ttu-id="97243-189">tooblock, selezionare **Media** in **blocco Accedi**</span><span class="sxs-lookup"><span data-stu-id="97243-189">tooblock, select **Medium** under **Block sign in**</span></span>
   
   <span data-ttu-id="97243-190">b.</span><span class="sxs-lookup"><span data-stu-id="97243-190">b.</span></span> <span data-ttu-id="97243-191">modifica della password sicura tooenforce, selezionare **Media** in **richiede l'autenticazione a più fattori**.</span><span class="sxs-lookup"><span data-stu-id="97243-191">tooenforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="97243-192">tooblock, seleziona Media sotto blocco Accedi.</span><span class="sxs-lookup"><span data-stu-id="97243-192">tooblock, select Medium under Block sign in.</span></span>
8. <span data-ttu-id="97243-193">autenticazione a più fattori tooenforce, seleziona **Media** in **richiede l'autenticazione a più fattori**.</span><span class="sxs-lookup"><span data-stu-id="97243-193">tooenforce multi-factor authentication, select **Medium** under **Require multi-factor authentication**.</span></span>
9. <span data-ttu-id="97243-194">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="97243-194">Click on **Save**.</span></span>
10. <span data-ttu-id="97243-195">È ora possibile testare l'accesso condizionale basati sui rischi simulando posizioni non familiari hello o IP anonimo rischio eventi perché sono entrambi **Media** gli eventi di rischio.</span><span class="sxs-lookup"><span data-stu-id="97243-195">You can now test risk-based conditional access by simulating hello unfamiliar locations or anonymous IP risk events because they are both **Medium** risk events.</span></span>


<span data-ttu-id="97243-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span><span class="sxs-lookup"><span data-stu-id="97243-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span></span>


## <a name="see-also"></a><span data-ttu-id="97243-197">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="97243-197">See also</span></span>
* [<span data-ttu-id="97243-198">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="97243-198">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

