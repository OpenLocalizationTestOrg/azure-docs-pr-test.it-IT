---
title: 'Azure AD Connect: guida introduttiva all''accesso Single Sign-On facile | Documentazione Microsoft'
description: "Questo articolo descrive la modalità di avvio tooget con Azure Active Directory trasparente Single Sign-On."
services: active-directory
keywords: "che cos'è Azure AD Connect, installare Active Directory, componenti richiesti per Azure AD, SSO, Single Sign-On"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 97d40ed41b3bfad9ff7e11ddbdb8de594ee85de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a><span data-ttu-id="da8b6-104">Accesso Single Sign-On facile di Azure Active Directory: guida introduttiva</span><span class="sxs-lookup"><span data-stu-id="da8b6-104">Azure Active Directory Seamless Single Sign-On: Quick start</span></span>

## <a name="how-toodeploy-seamless-sso"></a><span data-ttu-id="da8b6-105">Come toodeploy SSO trasparente</span><span class="sxs-lookup"><span data-stu-id="da8b6-105">How toodeploy Seamless SSO</span></span>

<span data-ttu-id="da8b6-106">Azure Active Directory trasparente Single Sign-On (SSO senza problemi per Azure AD) accede automaticamente gli utenti quando si trovano sulla rete aziendale connesso tooyour desktop aziendali.</span><span class="sxs-lookup"><span data-stu-id="da8b6-106">Azure Active Directory Seamless Single Sign-On (Azure AD Seamless SSO) automatically signs users in when they are on their corporate desktops connected tooyour corporate network.</span></span> <span data-ttu-id="da8b6-107">Fornisce agli utenti l'accesso semplice applicazioni basate su cloud tooyour senza la necessità di tutti i componenti locali aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="da8b6-107">It provides your users easy access tooyour cloud-based applications without needing any additional on-premises components.</span></span>

>[!IMPORTANT]
><span data-ttu-id="da8b6-108">caratteristica di SSO trasparente Hello è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="da8b6-108">hello Seamless SSO feature is currently in preview.</span></span>

<span data-ttu-id="da8b6-109">toodeploy SSO senza problemi, è necessario toofollow questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="da8b6-109">toodeploy Seamless SSO, you need toofollow these steps:</span></span>

## <a name="step-1-check-prerequisites"></a><span data-ttu-id="da8b6-110">Passaggio 1: Verificare i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="da8b6-110">Step 1: Check prerequisites</span></span>

<span data-ttu-id="da8b6-111">Verificare che hello seguenti prerequisiti siano soddisfatti:</span><span class="sxs-lookup"><span data-stu-id="da8b6-111">Ensure that hello following prerequisites are in place:</span></span>

1. <span data-ttu-id="da8b6-112">Configurare il server di Azure AD Connect: se si usa l'[autenticazione pass-through](active-directory-aadconnect-pass-through-authentication.md) come metodo di accesso, non è necessaria alcuna altra azione.</span><span class="sxs-lookup"><span data-stu-id="da8b6-112">Set up your Azure AD Connect server: If you use [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) as your sign-in method, no further action is required.</span></span> <span data-ttu-id="da8b6-113">Se come metodo di accesso si usa la [sincronizzazione dell'hash delle password](active-directory-aadconnectsync-implement-password-synchronization.md) e se vi è un firewall tra Azure AD Connect e Azure AD, assicurarsi che:</span><span class="sxs-lookup"><span data-stu-id="da8b6-113">If you use [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) as your sign-in method, and if there is a firewall between Azure AD Connect and Azure AD, ensure that:</span></span>
- <span data-ttu-id="da8b6-114">Si usi la versione 1.1.484.0 o versioni successive di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="da8b6-114">You are using versions 1.1.484.0 or later of Azure AD Connect.</span></span>
- <span data-ttu-id="da8b6-115">Azure AD Connect possa comunicare con gli URL `*.msappproxy.net` e tramite la porta 443.</span><span class="sxs-lookup"><span data-stu-id="da8b6-115">Azure AD Connect can communicate with `*.msappproxy.net` URLs and over port 443.</span></span> <span data-ttu-id="da8b6-116">Questo prerequisito è applicabile solo quando si abilita le funzionalità di hello, non per l'accesso degli utenti effettivi.</span><span class="sxs-lookup"><span data-stu-id="da8b6-116">This prerequisite is applicable only when you enable hello feature, not for actual user sign-ins.</span></span>
- <span data-ttu-id="da8b6-117">Azure AD Connect è possibile apportare diretto IP connessioni toohello [data center di Azure intervalli IP](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="da8b6-117">Azure AD Connect can make direct IP connections toohello [Azure data center IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="da8b6-118">Anche questo prerequisito è applicabile solo quando si abilita la funzionalità hello.</span><span class="sxs-lookup"><span data-stu-id="da8b6-118">Again, this prerequisite is applicable only when you enable hello feature.</span></span>
2. <span data-ttu-id="da8b6-119">Sono necessarie le credenziali di amministratore di dominio per ogni foresta di Active Directory di sincronizzare tooAzure Active Directory (tramite Azure AD Connect) e per gli utenti di cui si desidera tooenable SSO senza problemi.</span><span class="sxs-lookup"><span data-stu-id="da8b6-119">You need Domain Administrator credentials for each AD forest that you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want tooenable Seamless SSO.</span></span>

## <a name="step-2-enable-hello-feature"></a><span data-ttu-id="da8b6-120">Passaggio 2: Abilitare la funzionalità hello</span><span class="sxs-lookup"><span data-stu-id="da8b6-120">Step 2: Enable hello feature</span></span>

<span data-ttu-id="da8b6-121">La funzionalità Accesso SSO facile può essere abilitata tramite [Azure AD Connect](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="da8b6-121">Seamless SSO can be enabled using [Azure AD Connect](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="da8b6-122">Se si sta eseguendo una nuova installazione di Azure AD Connect, scegliere hello [percorso di installazione personalizzato](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="da8b6-122">If you are doing a fresh installation of Azure AD Connect, choose hello [custom installation path](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="da8b6-123">In hello "utente" pagina di accesso, verificare l'opzione "Abilita single sign-on" hello.</span><span class="sxs-lookup"><span data-stu-id="da8b6-123">At hello "User sign-in" page, check hello "Enable single sign on" option.</span></span>

![Azure AD Connect - Accesso utente](./media/active-directory-aadconnect-sso/sso8.png)

<span data-ttu-id="da8b6-125">Se Azure AD Connect è già installato, scegliere la pagina "Cambia l'accesso utente" in Azure AD Connect e fare clic su "Avanti".</span><span class="sxs-lookup"><span data-stu-id="da8b6-125">If you already have an installation of Azure AD Connect, choose "Change user sign-in page" on Azure AD Connect and click "Next".</span></span> <span data-ttu-id="da8b6-126">Verificare quindi l'opzione "Abilita single sign-on" hello.</span><span class="sxs-lookup"><span data-stu-id="da8b6-126">Then check hello "Enable single sign on" option.</span></span>

![Azure AD Connect - Cambiare l'accesso utente](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

<span data-ttu-id="da8b6-128">Continuare con la procedura guidata hello fino a ottenere pagina "Enable single sign-on" toohello.</span><span class="sxs-lookup"><span data-stu-id="da8b6-128">Continue through hello wizard until you get toohello "Enable single sign on" page.</span></span> <span data-ttu-id="da8b6-129">Fornire le credenziali di amministratore di dominio per ogni foresta di Active Directory di sincronizzare tooAzure Active Directory (tramite Azure AD Connect) e per gli utenti di cui si desidera tooenable SSO senza problemi.</span><span class="sxs-lookup"><span data-stu-id="da8b6-129">Provide Domain Administrator credentials for each AD forest that you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want tooenable Seamless SSO.</span></span> 

<span data-ttu-id="da8b6-130">Dopo il completamento della procedura guidata hello, trasparente SSO è abilitato per il tenant.</span><span class="sxs-lookup"><span data-stu-id="da8b6-130">After completion of hello wizard, Seamless SSO is enabled on your tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="da8b6-131">le credenziali di amministratore di dominio Hello non vengono archiviate in Azure AD Connect o in Azure AD, ma sono solo funzionalità di hello tooenable utilizzato.</span><span class="sxs-lookup"><span data-stu-id="da8b6-131">hello Domain Administrator credentials are not stored in Azure AD Connect or in Azure AD, but are only used tooenable hello feature.</span></span>

<span data-ttu-id="da8b6-132">Seguire questi tooverify istruzioni che è stata attivata correttamente trasparente SSO:</span><span class="sxs-lookup"><span data-stu-id="da8b6-132">Follow these instructions tooverify that you have enabled Seamless SSO correctly:</span></span>

1. <span data-ttu-id="da8b6-133">Accedi toohello [centro di amministrazione di Azure Active Directory](https://aad.portal.azure.com) con credenziali di amministratore globale di hello per il tenant.</span><span class="sxs-lookup"><span data-stu-id="da8b6-133">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with hello Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="da8b6-134">Selezionare **Azure Active Directory** nella navigazione a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="da8b6-134">Select **Azure Active Directory** on hello left-hand navigation.</span></span>
3. <span data-ttu-id="da8b6-135">Selezionare **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="da8b6-135">Select **Azure AD Connect**.</span></span>
4. <span data-ttu-id="da8b6-136">Verificare che hello **Single Sign-On trasparente** funzionalità Mostra come **abilitato**.</span><span class="sxs-lookup"><span data-stu-id="da8b6-136">Verify that hello **Seamless Single Sign-On** feature shows as **Enabled**.</span></span>

![Portale di Azure - Pannello Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-hello-feature"></a><span data-ttu-id="da8b6-138">Passaggio 3: Distribuire funzionalità hello</span><span class="sxs-lookup"><span data-stu-id="da8b6-138">Step 3: Roll out hello feature</span></span>

<span data-ttu-id="da8b6-139">tooroll gli utenti di tooyour hello funzionalità, è necessario l'area Intranet degli toousers di tooadd due gli URL (https://autologon.microsoftazuread-sso.com e https://aadg.windows.net.nsatc.net) di Azure Active Directory tramite criteri di gruppo in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="da8b6-139">tooroll out hello feature tooyour users, you need tooadd two Azure AD URLs (https://autologon.microsoftazuread-sso.com and https://aadg.windows.net.nsatc.net) toousers' Intranet zone settings via Group Policy in Active Directory.</span></span>

>[!NOTE]
> <span data-ttu-id="da8b6-140">Hello seguendo le istruzioni sono disponibili solo per Internet Explorer e Google Chrome in Windows (se i set di URL sito attendibile condivide con Internet Explorer).</span><span class="sxs-lookup"><span data-stu-id="da8b6-140">hello following instructions only work for Internet Explorer and Google Chrome on Windows  (if it shares set of trusted site URLs with Internet Explorer).</span></span> <span data-ttu-id="da8b6-141">Leggere la sezione successiva di hello per le istruzioni tooset Mozilla Firefox e Google Chrome su Mac.</span><span class="sxs-lookup"><span data-stu-id="da8b6-141">Read hello next section for instructions tooset up Mozilla Firefox and Google Chrome on Mac.</span></span>

### <a name="why-do-you-need-toomodify-users-intranet-zone-settings"></a><span data-ttu-id="da8b6-142">Motivo per cui è necessario area Intranet di toomodify degli utenti?</span><span class="sxs-lookup"><span data-stu-id="da8b6-142">Why do you need toomodify users' Intranet zone settings?</span></span>

<span data-ttu-id="da8b6-143">Per impostazione predefinita, il browser hello calcola automaticamente zona di destra hello (Internet o Intranet) da un URL.</span><span class="sxs-lookup"><span data-stu-id="da8b6-143">By default, hello browser automatically calculates hello right zone (Internet or Intranet) from a URL.</span></span> <span data-ttu-id="da8b6-144">Ad esempio, http://contoso/ è mappato toohello area Intranet, mentre http://intranet.contoso.com/ infatti toohello mappato l'area Internet (URL hello contiene un punto).</span><span class="sxs-lookup"><span data-stu-id="da8b6-144">For example, http://contoso/ is mapped toohello Intranet zone, whereas http://intranet.contoso.com/ is mapped toohello Internet zone (because hello URL contains a period).</span></span> <span data-ttu-id="da8b6-145">Browser non inviare l'endpoint di cloud tooa i ticket Kerberos, ad esempio hello due Azure AD URL -, a meno che il relativo URL viene aggiunto in modo esplicito l'area Intranet toohello del browser.</span><span class="sxs-lookup"><span data-stu-id="da8b6-145">Browsers don't send Kerberos tickets tooa cloud endpoint - like hello two Azure AD URLs - unless its URL is explicitly added toohello browser's Intranet zone.</span></span>

### <a name="detailed-steps"></a><span data-ttu-id="da8b6-146">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="da8b6-146">Detailed steps</span></span>

1. <span data-ttu-id="da8b6-147">Aprire lo strumento di gestione criteri di gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="da8b6-147">Open hello Group Policy Management tool.</span></span>
2. <span data-ttu-id="da8b6-148">Modificare i criteri di gruppo applicati toosome o tutti gli utenti di hello.</span><span class="sxs-lookup"><span data-stu-id="da8b6-148">Edit hello Group Policy that is applied toosome or all your users.</span></span> <span data-ttu-id="da8b6-149">In questo esempio, si usa hello **criterio dominio predefinito**.</span><span class="sxs-lookup"><span data-stu-id="da8b6-149">In this example, we use hello **Default Domain Policy**.</span></span>
3. <span data-ttu-id="da8b6-150">Passare troppo**utente Configurazione computer\Modelli amministrativi\Componenti di Windows\Internet Explorer\Pannello controllo Internet\pagina** e selezionare **tooZone elenco di assegnazione sito**.</span><span class="sxs-lookup"><span data-stu-id="da8b6-150">Navigate too**User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security Page** and select **Site tooZone Assignment List**.</span></span>
<span data-ttu-id="da8b6-151">![Single Sign-On](./media/active-directory-aadconnect-sso/sso6.png)</span><span class="sxs-lookup"><span data-stu-id="da8b6-151">![Single sign-on](./media/active-directory-aadconnect-sso/sso6.png)</span></span>  
4. <span data-ttu-id="da8b6-152">Abilitare i criteri di hello e immettere hello seguenti valori (Azure AD URL in cui vengono inoltrati i ticket Kerberos) e dati (*1* indica l'area Intranet) nella finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="da8b6-152">Enable hello policy, and enter hello following values (Azure AD URLs where Kerberos tickets are forwarded) and data (*1* indicates Intranet zone) in hello dialog box.</span></span>

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> <span data-ttu-id="da8b6-153">Se si desidera toodisallow alcuni utenti dall'utilizzo di SSO senza problemi, ad esempio, se questi utenti accedono in condivisi chioschi - impostare hello che precede i valori troppo*4*.</span><span class="sxs-lookup"><span data-stu-id="da8b6-153">If you want toodisallow some users from using Seamless SSO - for instance, if these users are signing in on shared kiosks - set hello preceding values too*4*.</span></span> <span data-ttu-id="da8b6-154">Questa azione aggiunge hello Azure AD URL toohello area siti con restrizioni e ha esito negativo tutto il tempo hello SSO senza problemi.</span><span class="sxs-lookup"><span data-stu-id="da8b6-154">This action adds hello Azure AD URLs toohello Restricted Zone, and fails Seamless SSO all hello time.</span></span>

5. <span data-ttu-id="da8b6-155">Fare clic su **OK**, quindi nuovamente su **OK**.</span><span class="sxs-lookup"><span data-stu-id="da8b6-155">Click **OK** and **OK** again.</span></span>

![Single sign-on](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a><span data-ttu-id="da8b6-157">Considerazioni sui browser</span><span class="sxs-lookup"><span data-stu-id="da8b6-157">Browser considerations</span></span>

#### <a name="mozilla-firefox"></a><span data-ttu-id="da8b6-158">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="da8b6-158">Mozilla Firefox</span></span>

<span data-ttu-id="da8b6-159">Mozilla Firefox non esegue automaticamente l'autenticazione Kerberos.</span><span class="sxs-lookup"><span data-stu-id="da8b6-159">Mozilla Firefox doesn't automatically do Kerberos Authentication.</span></span> <span data-ttu-id="da8b6-160">Ogni utente dispone di toomanually aggiungere le impostazioni Firefox tootheir URL hello Azure AD utilizzando hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="da8b6-160">Each user has toomanually add hello Azure AD URLs tootheir Firefox settings using hello following steps:</span></span>
1. <span data-ttu-id="da8b6-161">Eseguire Firefox e immettere `about:config` nella barra degli indirizzi hello.</span><span class="sxs-lookup"><span data-stu-id="da8b6-161">Run Firefox and enter `about:config` in hello address bar.</span></span> <span data-ttu-id="da8b6-162">Eliminare tutte le notifiche visualizzate.</span><span class="sxs-lookup"><span data-stu-id="da8b6-162">Dismiss any notifications that you see.</span></span>
2. <span data-ttu-id="da8b6-163">Ricerca di hello **network.negotiate-auth.trusted-URI** preferenza.</span><span class="sxs-lookup"><span data-stu-id="da8b6-163">Search for hello **network.negotiate-auth.trusted-uris** preference.</span></span> <span data-ttu-id="da8b6-164">Questa preferenza elenca i siti attendibili di Firefox per l'autenticazione Kerberos.</span><span class="sxs-lookup"><span data-stu-id="da8b6-164">This preference lists Firefox's trusted sites for Kerberos authentication.</span></span>
3. <span data-ttu-id="da8b6-165">Fare clic con il pulsante destro del mouse e selezionare "Modifica".</span><span class="sxs-lookup"><span data-stu-id="da8b6-165">Right-click and select "Modify".</span></span>
4. <span data-ttu-id="da8b6-166">Immettere "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" nel campo hello.</span><span class="sxs-lookup"><span data-stu-id="da8b6-166">Enter "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" in hello field.</span></span>
5. <span data-ttu-id="da8b6-167">Fare clic su "OK" e riaprire il browser hello.</span><span class="sxs-lookup"><span data-stu-id="da8b6-167">Click "OK" and reopen hello browser.</span></span>

#### <a name="safari-on-mac-os"></a><span data-ttu-id="da8b6-168">Safari su Mac OS</span><span class="sxs-lookup"><span data-stu-id="da8b6-168">Safari on Mac OS</span></span>

<span data-ttu-id="da8b6-169">Assicurarsi che tale macchina di hello in esecuzione Mac OS tooAD unita in join.</span><span class="sxs-lookup"><span data-stu-id="da8b6-169">Ensure that hello machine running Mac OS is joined tooAD.</span></span> <span data-ttu-id="da8b6-170">Vedere le istruzioni su come toodo che [qui](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span><span class="sxs-lookup"><span data-stu-id="da8b6-170">See instructions on how toodo that [here](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span></span>

#### <a name="google-chrome-on-mac-os"></a><span data-ttu-id="da8b6-171">Google Chrome su Mac OS</span><span class="sxs-lookup"><span data-stu-id="da8b6-171">Google Chrome on Mac OS</span></span>

<span data-ttu-id="da8b6-172">Per Google Chrome in Mac OS e altre piattaforme non Windows, vedere troppo[questo articolo](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) per informazioni su come toowhitelist hello gli URL di Azure AD per l'autenticazione integrata.</span><span class="sxs-lookup"><span data-stu-id="da8b6-172">For Google Chrome on Mac OS and other non-Windows platforms, refer too[this article](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) for information on how toowhitelist hello Azure AD URLs for integrated authentication.</span></span>

<span data-ttu-id="da8b6-173">Utilizzo di criteri di gruppo di terze parti Active Directory tooroll estensioni tooFirefox URL AD Azure hello e Google Chrome sugli utenti Mac esula dall'ambito di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="da8b6-173">Using third-party Active Directory Group Policy extensions tooroll out hello Azure AD URLs tooFirefox and Google Chrome on Mac users is outside of this article's scope.</span></span>

#### <a name="known-limitations"></a><span data-ttu-id="da8b6-174">Limitazioni note</span><span class="sxs-lookup"><span data-stu-id="da8b6-174">Known limitations</span></span>

<span data-ttu-id="da8b6-175">L'accesso SSO facile non funziona in modalità di esplorazione privata in Firefox e nel browser Edge.</span><span class="sxs-lookup"><span data-stu-id="da8b6-175">Seamless SSO doesn't work in private browsing mode on Firefox and Edge browsers.</span></span> <span data-ttu-id="da8b6-176">Inoltre non funziona in Internet Explorer se hello browser viene eseguito in modalità di protezione avanzata.</span><span class="sxs-lookup"><span data-stu-id="da8b6-176">It also doesn't work on Internet Explorer if hello browser is running in Enhanced Protection mode.</span></span>

>[!IMPORTANT]
><span data-ttu-id="da8b6-177">È recente eseguito il rollback il supporto per Edge tooinvestigate problemi segnalati.</span><span class="sxs-lookup"><span data-stu-id="da8b6-177">We recently rolled back support for Edge tooinvestigate customer-reported issues.</span></span>

## <a name="step-4-test-hello-feature"></a><span data-ttu-id="da8b6-178">Passaggio 4: Testare la funzionalità di hello</span><span class="sxs-lookup"><span data-stu-id="da8b6-178">Step 4: Test hello feature</span></span>

<span data-ttu-id="da8b6-179">funzionalità di hello tootest per un utente specifico, assicurarsi che _tutti_ hello le condizioni seguenti siano soddisfatti:</span><span class="sxs-lookup"><span data-stu-id="da8b6-179">tootest hello feature for a specific user, ensure that _all_ hello following conditions are in place:</span></span>
  - <span data-ttu-id="da8b6-180">utente Hello accede in un dispositivo aziendale.</span><span class="sxs-lookup"><span data-stu-id="da8b6-180">hello user is signing in on a corporate device.</span></span>
  - <span data-ttu-id="da8b6-181">dispositivo Hello è stata tooyour aggiunti in precedenza a un dominio di Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="da8b6-181">hello device has been previously joined tooyour Active Directory (AD) domain.</span></span>
  - <span data-ttu-id="da8b6-182">dispositivo Hello è tooyour una connessione diretta Domain Controller (DC), in rete cablata o wireless aziendale hello o tramite una connessione di accesso remoto, ad esempio una connessione VPN.</span><span class="sxs-lookup"><span data-stu-id="da8b6-182">hello device has a direct connection tooyour Domain Controller (DC), either on hello corporate wired or wireless network or via a remote access connection, such as a VPN connection.</span></span>
  - <span data-ttu-id="da8b6-183">Hai [implementato funzionalità hello](##step-3-roll-out-the-feature) toothis utente tramite criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="da8b6-183">You have [rolled out hello feature](##step-3-roll-out-the-feature) toothis user using Group Policy.</span></span>

<span data-ttu-id="da8b6-184">scenario di hello tootest dove hello immessi solo hello username, ma non la password di hello:</span><span class="sxs-lookup"><span data-stu-id="da8b6-184">tootest hello scenario where hello user enters only hello username, but not hello password:</span></span>
- <span data-ttu-id="da8b6-185">Accedere a *https://myapps.microsoft.com/* in una nuova sessione del browser privata.</span><span class="sxs-lookup"><span data-stu-id="da8b6-185">Sign into *https://myapps.microsoft.com/* in a new private browser session.</span></span>

<span data-ttu-id="da8b6-186">nello scenario hello tootest utente hello non dispone di password di nome utente o hello hello tooenter:</span><span class="sxs-lookup"><span data-stu-id="da8b6-186">tootest hello scenario where hello user doesn't have tooenter hello username or hello password:</span></span> 
- <span data-ttu-id="da8b6-187">Accedere a *https://myapps.microsoft.com/contoso.onmicrosoft.com* in una nuova sessione del browser privata.</span><span class="sxs-lookup"><span data-stu-id="da8b6-187">Sign into *https://myapps.microsoft.com/contoso.onmicrosoft.com* in a new private browser session.</span></span> <span data-ttu-id="da8b6-188">Sostituire "*contoso*" con il nome del tenant.</span><span class="sxs-lookup"><span data-stu-id="da8b6-188">Replace "*contoso*" with your tenant's name.</span></span>
- <span data-ttu-id="da8b6-189">In alternativa, accedere a *https://myapps.microsoft.com/contoso.com* in una nuova sessione del browser privata.</span><span class="sxs-lookup"><span data-stu-id="da8b6-189">Or sign into *https://myapps.microsoft.com/contoso.com* in a new private browser session.</span></span> <span data-ttu-id="da8b6-190">Sostituire "*contoso.com*" con un dominio verificato, non un dominio federato, nel tenant.</span><span class="sxs-lookup"><span data-stu-id="da8b6-190">Replace "*contoso.com*" with a verified domain (not a federated domain) in your tenant.</span></span>

## <a name="step-5-roll-over-keys"></a><span data-ttu-id="da8b6-191">Passaggio 5: Rinnovare le chiavi</span><span class="sxs-lookup"><span data-stu-id="da8b6-191">Step 5: Roll over keys</span></span>

<span data-ttu-id="da8b6-192">Nel passaggio 2, Azure AD Connect crea gli account computer (che rappresentano Azure AD) in tutte le foreste hello Active Directory in cui è stata attivata SSO senza problemi.</span><span class="sxs-lookup"><span data-stu-id="da8b6-192">In Step 2, Azure AD Connect creates computer accounts (representing Azure AD) in all hello AD forests on which you have enabled Seamless SSO.</span></span> <span data-ttu-id="da8b6-193">[Qui](active-directory-aadconnect-sso-how-it-works.md) sono disponibili informazioni dettagliate a riguardo.</span><span class="sxs-lookup"><span data-stu-id="da8b6-193">Learn more in detail [here](active-directory-aadconnect-sso-how-it-works.md).</span></span> <span data-ttu-id="da8b6-194">Per migliorare la sicurezza, è consigliabile che spesso il rollover delle chiavi di decrittografia Kerberos hello di questi account computer.</span><span class="sxs-lookup"><span data-stu-id="da8b6-194">For improved security, it is recommended that  you frequently roll over hello Kerberos decryption keys of these computer accounts.</span></span>

>[!IMPORTANT]
><span data-ttu-id="da8b6-195">Non è necessario di questo passaggio toodo _immediatamente_ dopo avere abilitato la funzionalità hello.</span><span class="sxs-lookup"><span data-stu-id="da8b6-195">You don't need toodo this step _immediately_ after you have enabled hello feature.</span></span> <span data-ttu-id="da8b6-196">Il rollover delle chiavi di decrittografia Kerberos hello almeno ogni 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="da8b6-196">Roll over hello Kerberos decryption keys at least every 30 days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da8b6-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="da8b6-197">Next steps</span></span>

- <span data-ttu-id="da8b6-198">[**Approfondimento tecnico**](active-directory-aadconnect-sso-how-it-works.md): informazioni sul funzionamento di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="da8b6-198">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="da8b6-199">[**Domande frequenti su** ](active-directory-aadconnect-sso-faq.md) -risposte toofrequently domande frequenti.</span><span class="sxs-lookup"><span data-stu-id="da8b6-199">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="da8b6-200">[**Risoluzione dei problemi** ](active-directory-aadconnect-troubleshoot-sso.md) -informazioni su come le problematiche comuni tooresolve con funzionalità hello.</span><span class="sxs-lookup"><span data-stu-id="da8b6-200">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="da8b6-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): per l'invio di richieste di nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="da8b6-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
