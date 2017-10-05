---
title: Studio su Azure Active Directory Identity Protection | Documentazione Microsoft
description: "Informazioni su come Azure AD Identity Protection consente di limitare la possibilità di un utente malintenzionato di sfruttare un'identità o un dispositivo compromesso e di proteggere un'identità o un dispositivo che in precedenza è stato sospettato o ritenuto essere compromesso."
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
ms.openlocfilehash: 2ecd07faed785fa6aa179ac1cca35a70d965e1dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a><span data-ttu-id="96f68-104">Studio sulla protezione delle identità di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96f68-104">Azure Active Directory Identity Protection playbook</span></span>
<span data-ttu-id="96f68-105">Questo studio consente di:</span><span class="sxs-lookup"><span data-stu-id="96f68-105">This playbook helps you to:</span></span>

* <span data-ttu-id="96f68-106">Inserire i dati nell'ambiente Identity Protection simulando eventi di rischio e vulnerabilità</span><span class="sxs-lookup"><span data-stu-id="96f68-106">Populate data in the Identity Protection environment by simulating risk events and vulnerabilities</span></span>
* <span data-ttu-id="96f68-107">Impostare criteri di accesso condizionali basati sui rischi e testare l'impatto di questi criteri</span><span class="sxs-lookup"><span data-stu-id="96f68-107">Set up risk-based conditional access policies and test the impact of these policies</span></span>

## <a name="simulating-risk-events"></a><span data-ttu-id="96f68-108">Simulazione di eventi di rischio</span><span class="sxs-lookup"><span data-stu-id="96f68-108">Simulating Risk Events</span></span>
<span data-ttu-id="96f68-109">Questa sezione riporta i passaggi per la simulazione dei seguenti tipi di eventi di rischio:</span><span class="sxs-lookup"><span data-stu-id="96f68-109">This section provides you with steps for simulating the following risk event types:</span></span>

* <span data-ttu-id="96f68-110">Accessi da indirizzi IP anonimi (facile)</span><span class="sxs-lookup"><span data-stu-id="96f68-110">Sign-ins from anonymous IP addresses (easy)</span></span>
* <span data-ttu-id="96f68-111">Accessi da posizioni non note (intermedio)</span><span class="sxs-lookup"><span data-stu-id="96f68-111">Sign-ins from unfamiliar locations (moderate)</span></span>
* <span data-ttu-id="96f68-112">Trasferimento impossibile a posizioni atipiche (difficile)</span><span class="sxs-lookup"><span data-stu-id="96f68-112">Impossible travel to atypical locations (difficult)</span></span>

<span data-ttu-id="96f68-113">Non è possibile simulare altri eventi di rischio in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="96f68-113">Other risk events cannot be simulated in a secure manner.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="96f68-114">Accessi da indirizzi IP anonimi</span><span class="sxs-lookup"><span data-stu-id="96f68-114">Sign-ins from anonymous IP addresses</span></span>
<span data-ttu-id="96f68-115">Questo tipo di evento di rischio identifica gli utenti che hanno eseguito l'accesso da un indirizzo IP riconosciuto come un indirizzo IP proxy anonimo.</span><span class="sxs-lookup"><span data-stu-id="96f68-115">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="96f68-116">Questi proxy vengono usati da persone che vogliono nascondere l'indirizzo IP del dispositivo e possono essere usati per attacchi dannosi.</span><span class="sxs-lookup"><span data-stu-id="96f68-116">These proxies are used by people who want to hide their device’s IP address and may be used for malicious intent.</span></span>

<span data-ttu-id="96f68-117">**Per simulare un accesso da un IP anonimo, seguire questa procedura**:</span><span class="sxs-lookup"><span data-stu-id="96f68-117">**To simulate a sign-in from an anonymous IP, perform the following steps**:</span></span>

1. <span data-ttu-id="96f68-118">Scaricare [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span><span class="sxs-lookup"><span data-stu-id="96f68-118">Download the [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span></span>
2. <span data-ttu-id="96f68-119">Usando Tor Browser, passare ad [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="96f68-119">Using the Tor Browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>   
3. <span data-ttu-id="96f68-120">Immettere le credenziali dell'account da visualizzare nel report **Accessi da indirizzi IP anonimi** .</span><span class="sxs-lookup"><span data-stu-id="96f68-120">Enter the credentials of the account you want to appear in the **Sign-ins from anonymous IP addresses** report.</span></span>

<span data-ttu-id="96f68-121">L’accesso verrà visualizzato nel dashboard Identity Protection entro 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="96f68-121">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span></span> 

### <a name="sign-ins-from-unfamiliar-locations"></a><span data-ttu-id="96f68-122">Accessi da posizioni non note</span><span class="sxs-lookup"><span data-stu-id="96f68-122">Sign-ins from unfamiliar locations</span></span>
<span data-ttu-id="96f68-123">L'evento di rischio per gli accessi da posizioni non note è un meccanismo di valutazione dell'accesso in tempo reale che prende in considerazione le posizioni di accesso precedenti, come l'indirizzo IP, la latitudine, la longitudine e l'ASN, per determinare posizioni nuove o non note.</span><span class="sxs-lookup"><span data-stu-id="96f68-123">The unfamiliar locations risk is a real-time sign-in evaluation mechanism that considers past sign-in locations (IP, Latitude / Longitude and ASN) to determine new / unfamiliar locations.</span></span> <span data-ttu-id="96f68-124">Il sistema archivia gli indirizzi IP, la latitudine, la longitudine e gli ASN usati in precedenza da un utente e li considera posizioni "note".</span><span class="sxs-lookup"><span data-stu-id="96f68-124">The system stores previous IPs, Latitude / Longitude, and ASNs of a user and considers these to be familiar locations.</span></span> <span data-ttu-id="96f68-125">Una posizione di accesso viene considerata non nota se non corrisponde a nessuna delle posizioni note esistenti.</span><span class="sxs-lookup"><span data-stu-id="96f68-125">A sign-in location is considered unfamiliar if the sign-in location does not match any of the existing familiar locations.</span></span>

<span data-ttu-id="96f68-126">Azure Active Directory Identity Protection:</span><span class="sxs-lookup"><span data-stu-id="96f68-126">Azure Active Directory Identity Protection:</span></span>  

* <span data-ttu-id="96f68-127">ha un periodo di apprendimento iniziale di 14 giorni, durante i quali le nuove posizioni non vengono contrassegnate come posizioni non note.</span><span class="sxs-lookup"><span data-stu-id="96f68-127">has an initial learning period of 14 days during which it does not flag any new locations as unfamiliar locations.</span></span>
* <span data-ttu-id="96f68-128">ignora gli accessi da dispositivi noti e le posizioni geograficamente vicine a una posizione nota esistente.</span><span class="sxs-lookup"><span data-stu-id="96f68-128">ignores sign-ins from familiar devices and locations that are geographically close to an existing familiar location.</span></span>

<span data-ttu-id="96f68-129">Per simulare posizioni non note, è necessario accedere da una posizione e da un dispositivo mai usati prima con l'account.</span><span class="sxs-lookup"><span data-stu-id="96f68-129">To simulate unfamiliar locations, you have to sign in from a location and device that the account has not signed in from before.</span></span> 

<span data-ttu-id="96f68-130">**Per simulare un accesso da una posizione non nota, seguire questa procedura**:</span><span class="sxs-lookup"><span data-stu-id="96f68-130">**To simulate a sign-in from an unfamiliar location, perform the following steps**:</span></span>

1. <span data-ttu-id="96f68-131">Scegliere un account che abbia una cronologia di accesso di almeno 14 giorni.</span><span class="sxs-lookup"><span data-stu-id="96f68-131">Choose an account that has at least a 14-day sign-in history.</span></span> 
2. <span data-ttu-id="96f68-132">È possibile procedere in due modi:</span><span class="sxs-lookup"><span data-stu-id="96f68-132">Do either:</span></span>
   
   <span data-ttu-id="96f68-133">a.</span><span class="sxs-lookup"><span data-stu-id="96f68-133">a.</span></span> <span data-ttu-id="96f68-134">Mentre si usa una VPN, passare ad [https://myapps.microsoft.com](https://myapps.microsoft.com) e immettere le credenziali dell'account per cui si vuole simulare l'evento di rischio.</span><span class="sxs-lookup"><span data-stu-id="96f68-134">While using a VPN, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com) and enter the credentials of the account you want to simulate the risk event for.</span></span>
   
   <span data-ttu-id="96f68-135">b.</span><span class="sxs-lookup"><span data-stu-id="96f68-135">b.</span></span> <span data-ttu-id="96f68-136">Chiedere a un collega in un’altra posizione di accedere usando le credenziali dell'account (scelta non consigliata).</span><span class="sxs-lookup"><span data-stu-id="96f68-136">Ask an associate in a different location to sign in using the account’s credentials (not recommended).</span></span>

<span data-ttu-id="96f68-137">L’accesso verrà visualizzato nel dashboard Identity Protection entro 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="96f68-137">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span></span>

### <a name="impossible-travel-to-atypical-location"></a><span data-ttu-id="96f68-138">Trasferimento impossibile a posizioni atipiche</span><span class="sxs-lookup"><span data-stu-id="96f68-138">Impossible travel to atypical location</span></span>
<span data-ttu-id="96f68-139">La condizione di trasferimento impossibile è difficile da simulare perché l'algoritmo usa Machine Learning per eliminare i falsi positivi, ad esempio il trasferimento impossibile da dispositivi noti o l'accesso da VPN usate da altri utenti nella directory.</span><span class="sxs-lookup"><span data-stu-id="96f68-139">Simulating the impossible travel condition is difficult because the algorithm uses machine learning to weed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in the directory.</span></span> <span data-ttu-id="96f68-140">Per iniziare a generare eventi di rischio, l'algoritmo richiede anche una cronologia di accesso da 3 a 14 giorni per l'utente.</span><span class="sxs-lookup"><span data-stu-id="96f68-140">Additionally, the algorithm requires a sign-in history of 3 to 14 days for the user before it begins generating risk events.</span></span>

<span data-ttu-id="96f68-141">**Per simulare un trasferimento impossibile a posizioni atipiche, seguire questa procedura**:</span><span class="sxs-lookup"><span data-stu-id="96f68-141">**To simulate an impossible travel to atypical location, perform the following steps**:</span></span>

1. <span data-ttu-id="96f68-142">Usando il browser standard, passare ad [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="96f68-142">Using your standard browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>  
2. <span data-ttu-id="96f68-143">Immettere le credenziali dell'account per cui si vuole generare un evento di rischio trasferimento impossibile.</span><span class="sxs-lookup"><span data-stu-id="96f68-143">Enter the credentials of the account you want to generate an impossible travel risk event for.</span></span>
3. <span data-ttu-id="96f68-144">Modificare l'agente utente.</span><span class="sxs-lookup"><span data-stu-id="96f68-144">Change your user agent.</span></span> <span data-ttu-id="96f68-145">Per modificare l'agente utente in Internet Explorer, usare Strumenti di sviluppo. Per modificare l'agente utente in Firefox o Chrome, usare un componente aggiuntivo di selezione dell'agente utente.</span><span class="sxs-lookup"><span data-stu-id="96f68-145">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span></span>
4. <span data-ttu-id="96f68-146">Modificare l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="96f68-146">Change your IP address.</span></span> <span data-ttu-id="96f68-147">È possibile modificare l'indirizzo IP usando una VPN, un componente aggiuntivo Tor o avviare un nuovo computer in Azure in un altro data center.</span><span class="sxs-lookup"><span data-stu-id="96f68-147">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span></span>
5. <span data-ttu-id="96f68-148">Accedere ad [https://myapps.microsoft.com](https://myapps.microsoft.com) con le stesse credenziali usate in precedenza ed entro pochi minuti dall'accesso precedente.</span><span class="sxs-lookup"><span data-stu-id="96f68-148">Sign-in to [https://myapps.microsoft.com](https://myapps.microsoft.com) using the same credentials as before and within a few minutes after the previous sign-in.</span></span>

<span data-ttu-id="96f68-149">L’accesso verrà visualizzato nel dashboard Identity Protection entro 2-4 ore.</span><span class="sxs-lookup"><span data-stu-id="96f68-149">The sign-in will show up in the Identity Protection dashboard within 2-4 hours.</span></span><br>
<span data-ttu-id="96f68-150">A causa dei complessi modelli di Machine Learning coinvolti, potrebbe non essere rilevato.</span><span class="sxs-lookup"><span data-stu-id="96f68-150">Because of the complex machine learning models involved, there is a chance it will not get picked up.</span></span><br> <span data-ttu-id="96f68-151">Potrebbe essere utile ripetere questi passaggi per più account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96f68-151">You might want to replicate these steps for multiple Azure AD accounts.</span></span>

## <a name="simulating-vulnerabilities"></a><span data-ttu-id="96f68-152">Simulazione di vulnerabilità</span><span class="sxs-lookup"><span data-stu-id="96f68-152">Simulating vulnerabilities</span></span>
<span data-ttu-id="96f68-153">Le vulnerabilità sono punti deboli in un ambiente Azure AD che possono essere sfruttati da un utente malintenzionato.</span><span class="sxs-lookup"><span data-stu-id="96f68-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span></span> <span data-ttu-id="96f68-154">In Azure AD Identity Protection sono attualmente visibili 3 tipi di vulnerabilità che consentono di sfruttare altre funzionalità di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96f68-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span></span> <span data-ttu-id="96f68-155">Tali vulnerabilità verranno visualizzate automaticamente nel dashboard Identity Protection dopo aver impostato le funzionalità seguenti.</span><span class="sxs-lookup"><span data-stu-id="96f68-155">These Vulnerabilities will be displayed on the Identity Protection dashboard automatically once these features are set up.</span></span>

* <span data-ttu-id="96f68-156">Azure AD [Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="96f68-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>
* <span data-ttu-id="96f68-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="96f68-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
* <span data-ttu-id="96f68-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="96f68-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="user-compromise-risk"></a><span data-ttu-id="96f68-159">Rischio di compromissione dell'utente</span><span class="sxs-lookup"><span data-stu-id="96f68-159">User compromise risk</span></span>
<span data-ttu-id="96f68-160">**Per testare il rischio di compromissione dell'utente, seguire questa procedura**:</span><span class="sxs-lookup"><span data-stu-id="96f68-160">**To test User compromise risk, perform the following steps**:</span></span>

1. <span data-ttu-id="96f68-161">Accedere ad [https://portal.azure.com](https://portal.azure.com) con le credenziali di amministratore globale del tenant.</span><span class="sxs-lookup"><span data-stu-id="96f68-161">Sign-in to [https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="96f68-162">Passare a **Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="96f68-162">Navigate to **Identity Protection**.</span></span> 
3. <span data-ttu-id="96f68-163">Nel pannello principale di **Azure AD Identity Protection** fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="96f68-163">On the main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="96f68-164">Nel pannello **Impostazioni del portale** in **Regole di sicurezza** fare clic su **Rischio di compromissione dell'utente**.</span><span class="sxs-lookup"><span data-stu-id="96f68-164">On the **Portal Settings** blade, under **Security rules**, click **User compromise risk**.</span></span> 
5. <span data-ttu-id="96f68-165">Nel pannello **Rischio di accesso** disattivare **Abilita regola** e quindi fare clic su **Salva** per salvare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="96f68-165">On the **Sign in Risk** blade, turn **Enable rule** off, and then click **Save** settings.</span></span>
6. <span data-ttu-id="96f68-166">Per un determinato account utente, simulare un evento di rischio IP anonimo o posizione non nota.</span><span class="sxs-lookup"><span data-stu-id="96f68-166">For a given user account, simulate an unfamiliar locations or anonymous IP risk event.</span></span> <span data-ttu-id="96f68-167">In questo modo il livello di rischio utente verrà innalzato a **Medio**per tale utente.</span><span class="sxs-lookup"><span data-stu-id="96f68-167">This will elevate the user risk level for that user to **Medium**.</span></span>
7. <span data-ttu-id="96f68-168">Attendere alcuni minuti e poi verificare che il livello utente sia **Medio**.</span><span class="sxs-lookup"><span data-stu-id="96f68-168">Wait a few minutes, and then verify that user level for your user is **Medium**.</span></span>
8. <span data-ttu-id="96f68-169">Passare al pannello **Impostazioni del portale** .</span><span class="sxs-lookup"><span data-stu-id="96f68-169">Go to the **Portal Settings** blade.</span></span>
9. <span data-ttu-id="96f68-170">Nel pannello **Rischio di compromissione dell'utente** in **Abilita regola** selezionare **Sì**.</span><span class="sxs-lookup"><span data-stu-id="96f68-170">On the **User Compromise Risk** blade, under **Enable rule**, select **On** .</span></span> 
10. <span data-ttu-id="96f68-171">Selezionare una delle opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="96f68-171">Select one of the following options:</span></span>
    
    <span data-ttu-id="96f68-172">a.</span><span class="sxs-lookup"><span data-stu-id="96f68-172">a.</span></span> <span data-ttu-id="96f68-173">Per bloccare, selezionare **Medio** in **Blocca l'accesso**.</span><span class="sxs-lookup"><span data-stu-id="96f68-173">To block, select **Medium** under **Block sign in**.</span></span>
    
    <span data-ttu-id="96f68-174">b.</span><span class="sxs-lookup"><span data-stu-id="96f68-174">b.</span></span> <span data-ttu-id="96f68-175">Per applicare la modifica della password di protezione, selezionare **Medio** in **Richiedi autenticazione a più fattori**.</span><span class="sxs-lookup"><span data-stu-id="96f68-175">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
11. <span data-ttu-id="96f68-176">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="96f68-176">Click **Save**.</span></span>
12. <span data-ttu-id="96f68-177">A questo punto è possibile testare l'accesso condizionale basato sul rischio eseguendo l'accesso come un utente con un livello di rischio elevato.</span><span class="sxs-lookup"><span data-stu-id="96f68-177">You can now test risk-based conditional access by signing in using a user with an elevated risk level.</span></span> <span data-ttu-id="96f68-178">Se il rischio dell'utente è medio, l'accesso verrà bloccato o verrà richiesto di modificare la password, a seconda della configurazione dei criteri.</span><span class="sxs-lookup"><span data-stu-id="96f68-178">If the user risk is Medium, depending on the configuration of your policy, your sign-in is be either blocked or you are forced to change your password.</span></span> 
    <br><br><span data-ttu-id="96f68-179">
    ![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
    </span><span class="sxs-lookup"><span data-stu-id="96f68-179">
![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
</span></span><br>

## <a name="sign-in-risk"></a><span data-ttu-id="96f68-180">Rischio di accesso</span><span class="sxs-lookup"><span data-stu-id="96f68-180">Sign-in risk</span></span>
<span data-ttu-id="96f68-181">**Per testare un rischio di accesso, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="96f68-181">**To test a sign in risk, perform the following steps:**</span></span>

1. <span data-ttu-id="96f68-182">Accedere ad [https://portal.azure.com ](https://portal.azure.com) con le credenziali di amministratore globale del tenant.</span><span class="sxs-lookup"><span data-stu-id="96f68-182">Sign-in to [https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="96f68-183">Passare a **Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="96f68-183">Navigate to **Identity Protection**.</span></span>
3. <span data-ttu-id="96f68-184">Nel pannello principale di **Azure AD Identity Protection** fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="96f68-184">On the main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="96f68-185">Nel pannello **Impostazioni del portale** in **Regole di sicurezza** fare clic su **Rischio di accesso**.</span><span class="sxs-lookup"><span data-stu-id="96f68-185">On the **Portal Settings** blade, under **Security rules**, click **Sign in risk**.</span></span>
5. <span data-ttu-id="96f68-186">Nel * * Accedi rischio * * pannello seleziona **su** in **Abilita regola**.</span><span class="sxs-lookup"><span data-stu-id="96f68-186">On the **Sign in Risk **blade, select **On** under **Enable rule**.</span></span> 
6. <span data-ttu-id="96f68-187">Selezionare una delle opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="96f68-187">Select one of the following options:</span></span>
   
   <span data-ttu-id="96f68-188">a.</span><span class="sxs-lookup"><span data-stu-id="96f68-188">a.</span></span> <span data-ttu-id="96f68-189">Per bloccare, selezionare **Medio** in **Blocca l'accesso**</span><span class="sxs-lookup"><span data-stu-id="96f68-189">To block, select **Medium** under **Block sign in**</span></span>
   
   <span data-ttu-id="96f68-190">b.</span><span class="sxs-lookup"><span data-stu-id="96f68-190">b.</span></span> <span data-ttu-id="96f68-191">Per applicare la modifica della password di protezione, selezionare **Medio** in **Richiedi autenticazione a più fattori**.</span><span class="sxs-lookup"><span data-stu-id="96f68-191">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="96f68-192">Per bloccare, selezionare Medio in Blocca l'accesso.</span><span class="sxs-lookup"><span data-stu-id="96f68-192">To block, select Medium under Block sign in.</span></span>
8. <span data-ttu-id="96f68-193">Per applicare l'autenticazione a più fattori, selezionare **Medio** in **Richiedi autenticazione a più fattori**.</span><span class="sxs-lookup"><span data-stu-id="96f68-193">To enforce multi-factor authentication, select **Medium** under **Require multi-factor authentication**.</span></span>
9. <span data-ttu-id="96f68-194">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="96f68-194">Click on **Save**.</span></span>
10. <span data-ttu-id="96f68-195">A questo punto è possibile testare l'accesso condizionale basato sul rischio simulando gli eventi di rischio relativi a posizioni insolite o indirizzi IP anonimi, perché sono entrambi eventi di rischio di livello **Medio** .</span><span class="sxs-lookup"><span data-stu-id="96f68-195">You can now test risk-based conditional access by simulating the unfamiliar locations or anonymous IP risk events because they are both **Medium** risk events.</span></span>


<span data-ttu-id="96f68-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span><span class="sxs-lookup"><span data-stu-id="96f68-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span></span>


## <a name="see-also"></a><span data-ttu-id="96f68-197">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="96f68-197">See also</span></span>
* [<span data-ttu-id="96f68-198">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="96f68-198">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

