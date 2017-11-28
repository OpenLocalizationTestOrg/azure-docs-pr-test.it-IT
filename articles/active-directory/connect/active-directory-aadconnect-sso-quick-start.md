---
title: 'Azure AD Connect: guida introduttiva all''accesso Single Sign-On facile | Documentazione Microsoft'
description: "In questo articolo vengono descritte le attività iniziali dell'accesso Single Sign-On facile di Azure Active Directory."
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
ms.openlocfilehash: 977108687734a5eb7f7a30419de2a6bdef184d0e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a><span data-ttu-id="3b2d6-104">Accesso Single Sign-On facile di Azure Active Directory: guida introduttiva</span><span class="sxs-lookup"><span data-stu-id="3b2d6-104">Azure Active Directory Seamless Single Sign-On: Quick start</span></span>

## <a name="how-to-deploy-seamless-sso"></a><span data-ttu-id="3b2d6-105">Come distribuire l'accesso Single Sign-On facile</span><span class="sxs-lookup"><span data-stu-id="3b2d6-105">How to deploy Seamless SSO</span></span>

<span data-ttu-id="3b2d6-106">La funzionalità Accesso Single Sign-On facile (Accesso SSO facile) di Azure Active Directory consente agli utenti di eseguire l'accesso automaticamente dai desktop di proprietà dell'azienda connessi alla rete aziendale.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-106">Azure Active Directory Seamless Single Sign-On (Azure AD Seamless SSO) automatically signs users in when they are on their corporate desktops connected to your corporate network.</span></span> <span data-ttu-id="3b2d6-107">Consente agli utenti di accedere facilmente alle applicazioni basate su cloud senza la necessità di componenti aggiuntivi in locale.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-107">It provides your users easy access to your cloud-based applications without needing any additional on-premises components.</span></span>

>[!IMPORTANT]
><span data-ttu-id="3b2d6-108">La funzionalità Accesso Single Sign-On facile è attualmente in fase di anteprima.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-108">The Seamless SSO feature is currently in preview.</span></span>

<span data-ttu-id="3b2d6-109">Per distribuire l'accesso SSO facile, è necessario seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3b2d6-109">To deploy Seamless SSO, you need to follow these steps:</span></span>

## <a name="step-1-check-prerequisites"></a><span data-ttu-id="3b2d6-110">Passaggio 1: Verificare i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3b2d6-110">Step 1: Check prerequisites</span></span>

<span data-ttu-id="3b2d6-111">Accertarsi di aver soddisfatto i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="3b2d6-111">Ensure that the following prerequisites are in place:</span></span>

1. <span data-ttu-id="3b2d6-112">Configurare il server di Azure AD Connect: se si usa l'[autenticazione pass-through](active-directory-aadconnect-pass-through-authentication.md) come metodo di accesso, non è necessaria alcuna altra azione.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-112">Set up your Azure AD Connect server: If you use [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) as your sign-in method, no further action is required.</span></span> <span data-ttu-id="3b2d6-113">Se come metodo di accesso si usa la [sincronizzazione dell'hash delle password](active-directory-aadconnectsync-implement-password-synchronization.md) e se vi è un firewall tra Azure AD Connect e Azure AD, assicurarsi che:</span><span class="sxs-lookup"><span data-stu-id="3b2d6-113">If you use [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) as your sign-in method, and if there is a firewall between Azure AD Connect and Azure AD, ensure that:</span></span>
- <span data-ttu-id="3b2d6-114">Si usi la versione 1.1.484.0 o versioni successive di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-114">You are using versions 1.1.484.0 or later of Azure AD Connect.</span></span>
- <span data-ttu-id="3b2d6-115">Azure AD Connect possa comunicare con gli URL `*.msappproxy.net` e tramite la porta 443.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-115">Azure AD Connect can communicate with `*.msappproxy.net` URLs and over port 443.</span></span> <span data-ttu-id="3b2d6-116">Questo prerequisito è applicabile solo quando si abilita la funzionalità, non per gli accessi utente effettivi.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-116">This prerequisite is applicable only when you enable the feature, not for actual user sign-ins.</span></span>
- <span data-ttu-id="3b2d6-117">Azure AD Connect possa eseguire connessioni IP dirette agli [intervalli IP dei data center di Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="3b2d6-117">Azure AD Connect can make direct IP connections to the [Azure data center IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="3b2d6-118">Anche questo prerequisito è applicabile solo quando si abilita la funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-118">Again, this prerequisite is applicable only when you enable the feature.</span></span>
2. <span data-ttu-id="3b2d6-119">Sono necessarie le credenziali di amministratore di dominio per ogni foresta di AD che si sincronizza con Azure AD, tramite Azure AD Connect, e per i cui utenti si vuole abilitare la funzionalità Accesso SSO facile.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-119">You need Domain Administrator credentials for each AD forest that you synchronize to Azure AD (using Azure AD Connect) and for whose users you want to enable Seamless SSO.</span></span>

## <a name="step-2-enable-the-feature"></a><span data-ttu-id="3b2d6-120">Passaggio 2: Abilitare la funzionalità</span><span class="sxs-lookup"><span data-stu-id="3b2d6-120">Step 2: Enable the feature</span></span>

<span data-ttu-id="3b2d6-121">La funzionalità Accesso SSO facile può essere abilitata tramite [Azure AD Connect](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="3b2d6-121">Seamless SSO can be enabled using [Azure AD Connect](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="3b2d6-122">Se si esegue una nuova installazione di Azure AD Connect, scegliere il [percorso di installazione personalizzato](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="3b2d6-122">If you are doing a fresh installation of Azure AD Connect, choose the [custom installation path](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="3b2d6-123">Nella pagina "Accesso utente" selezionare l'opzione "Abilita Single Sign-On".</span><span class="sxs-lookup"><span data-stu-id="3b2d6-123">At the "User sign-in" page, check the "Enable single sign on" option.</span></span>

![Azure AD Connect - Accesso utente](./media/active-directory-aadconnect-sso/sso8.png)

<span data-ttu-id="3b2d6-125">Se Azure AD Connect è già installato, scegliere la pagina "Cambia l'accesso utente" in Azure AD Connect e fare clic su "Avanti".</span><span class="sxs-lookup"><span data-stu-id="3b2d6-125">If you already have an installation of Azure AD Connect, choose "Change user sign-in page" on Azure AD Connect and click "Next".</span></span> <span data-ttu-id="3b2d6-126">Selezionare quindi l'opzione "Abilita Single Sign-On".</span><span class="sxs-lookup"><span data-stu-id="3b2d6-126">Then check the "Enable single sign on" option.</span></span>

![Azure AD Connect - Cambiare l'accesso utente](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

<span data-ttu-id="3b2d6-128">Continuare la procedura guidata fino a quando si arriva alla pagina "Abilita Single Sign-On".</span><span class="sxs-lookup"><span data-stu-id="3b2d6-128">Continue through the wizard until you get to the "Enable single sign on" page.</span></span> <span data-ttu-id="3b2d6-129">Immettere le credenziali di amministratore di dominio per ogni foresta di AD che si sincronizza con Azure AD, tramite Azure AD Connect, e per i cui utenti si vuole abilitare la funzionalità Accesso SSO facile.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-129">Provide Domain Administrator credentials for each AD forest that you synchronize to Azure AD (using Azure AD Connect) and for whose users you want to enable Seamless SSO.</span></span> 

<span data-ttu-id="3b2d6-130">Al termine della procedura guidata, l'accesso SSO facile è abilitato nel tenant.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-130">After completion of the wizard, Seamless SSO is enabled on your tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="3b2d6-131">Le credenziali di amministratore di dominio non vengono archiviate in Azure AD Connect o in Azure AD, ma vengono usate solo per abilitare la funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-131">The Domain Administrator credentials are not stored in Azure AD Connect or in Azure AD, but are only used to enable the feature.</span></span>

<span data-ttu-id="3b2d6-132">Seguire queste istruzioni per verificare di aver abilitato correttamente l'accesso Single Sign-On facile:</span><span class="sxs-lookup"><span data-stu-id="3b2d6-132">Follow these instructions to verify that you have enabled Seamless SSO correctly:</span></span>

1. <span data-ttu-id="3b2d6-133">Accedere all'[interfaccia di amministrazione di Azure Active Directory](https://aad.portal.azure.com) con le credenziali di amministratore globale del tenant.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-133">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with the Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="3b2d6-134">Selezionare **Azure Active Directory** nell'opzione di spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-134">Select **Azure Active Directory** on the left-hand navigation.</span></span>
3. <span data-ttu-id="3b2d6-135">Selezionare **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-135">Select **Azure AD Connect**.</span></span>
4. <span data-ttu-id="3b2d6-136">Verificare che la funzionalità **Accesso Single Sign-On facile** sia impostata su **Abilitato**.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-136">Verify that the **Seamless Single Sign-On** feature shows as **Enabled**.</span></span>

![Portale di Azure - Pannello Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-the-feature"></a><span data-ttu-id="3b2d6-138">Passaggio 3: Distribuire la funzionalità</span><span class="sxs-lookup"><span data-stu-id="3b2d6-138">Step 3: Roll out the feature</span></span>

<span data-ttu-id="3b2d6-139">Per distribuire la funzionalità agli utenti, è necessario aggiungere due URL di Azure AD, https://autologon.microsoftazuread-sso.com e https://aadg.windows.net.nsatc.net, alle impostazioni dell'area Intranet degli utenti tramite Criteri di gruppo in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-139">To roll out the feature to your users, you need to add two Azure AD URLs (https://autologon.microsoftazuread-sso.com and https://aadg.windows.net.nsatc.net) to users' Intranet zone settings via Group Policy in Active Directory.</span></span>

>[!NOTE]
> <span data-ttu-id="3b2d6-140">Le istruzioni seguenti valgono solo per Internet Explorer e Google Chrome in Windows, se condivide l'insieme di URL di siti attendibili con Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-140">The following instructions only work for Internet Explorer and Google Chrome on Windows  (if it shares set of trusted site URLs with Internet Explorer).</span></span> <span data-ttu-id="3b2d6-141">Vedere la sezione successiva per istruzioni sulla configurazione di Mozilla Firefox e Google Chrome su Mac.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-141">Read the next section for instructions to set up Mozilla Firefox and Google Chrome on Mac.</span></span>

### <a name="why-do-you-need-to-modify-users-intranet-zone-settings"></a><span data-ttu-id="3b2d6-142">Motivo per cui è necessario modificare le impostazioni della zona Intranet degli utenti</span><span class="sxs-lookup"><span data-stu-id="3b2d6-142">Why do you need to modify users' Intranet zone settings?</span></span>

<span data-ttu-id="3b2d6-143">Per impostazione predefinita, il browser calcola automaticamente l'area giusta, Internet o Intranet, dall'URL.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-143">By default, the browser automatically calculates the right zone (Internet or Intranet) from a URL.</span></span> <span data-ttu-id="3b2d6-144">Ad esempio l'URL http://contoso/ viene mappato all'area Intranet, mentre l'URL http://intranet.contoso.com/ viene mappato all'area Internet perché l'URL contiene un punto.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-144">For example, http://contoso/ is mapped to the Intranet zone, whereas http://intranet.contoso.com/ is mapped to the Internet zone (because the URL contains a period).</span></span> <span data-ttu-id="3b2d6-145">I browser non inviano i ticket Kerberos a un endpoint del cloud, come i due URL di Azure AD, a meno che l'URL relativo non venga aggiunto all'area Intranet del browser.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-145">Browsers don't send Kerberos tickets to a cloud endpoint - like the two Azure AD URLs - unless its URL is explicitly added to the browser's Intranet zone.</span></span>

### <a name="detailed-steps"></a><span data-ttu-id="3b2d6-146">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="3b2d6-146">Detailed steps</span></span>

1. <span data-ttu-id="3b2d6-147">Aprire lo strumento Gestione criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-147">Open the Group Policy Management tool.</span></span>
2. <span data-ttu-id="3b2d6-148">Modificare i Criteri di gruppo applicati ad alcuni utenti o a tutti.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-148">Edit the Group Policy that is applied to some or all your users.</span></span> <span data-ttu-id="3b2d6-149">In questo esempio viene usato **Criterio dominio predefinito**.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-149">In this example, we use the **Default Domain Policy**.</span></span>
3. <span data-ttu-id="3b2d6-150">Passare a **Configurazione utente\Modelli amministrativi\Componenti di Windows\Internet Explorer\Pannello di controllo Internet\Scheda Sicurezza** e selezionare **Elenco di assegnazione siti ad aree**.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-150">Navigate to **User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security Page** and select **Site to Zone Assignment List**.</span></span>
<span data-ttu-id="3b2d6-151">![Single Sign-On](./media/active-directory-aadconnect-sso/sso6.png)</span><span class="sxs-lookup"><span data-stu-id="3b2d6-151">![Single sign-on](./media/active-directory-aadconnect-sso/sso6.png)</span></span>  
4. <span data-ttu-id="3b2d6-152">Abilitare i criteri e immettere i valori seguenti (URL di Azure AD in cui vengono inoltrati i ticket Kerberos) e i dati (*1* indica l'area Intranet) nella finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-152">Enable the policy, and enter the following values (Azure AD URLs where Kerberos tickets are forwarded) and data (*1* indicates Intranet zone) in the dialog box.</span></span>

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> <span data-ttu-id="3b2d6-153">Se si vuole impedire ad alcuni utenti di usare l'accesso SSO facile, ad esempio se tali utenti accedono da chioschi multimediali condivisi, impostare i valori precedenti su *4*.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-153">If you want to disallow some users from using Seamless SSO - for instance, if these users are signing in on shared kiosks - set the preceding values to *4*.</span></span> <span data-ttu-id="3b2d6-154">Questa azione aggiunge gli URL di Azure AD all'Area con restrizioni e fa sì che l'accesso SSO facile abbia sempre esito negativo.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-154">This action adds the Azure AD URLs to the Restricted Zone, and fails Seamless SSO all the time.</span></span>

5. <span data-ttu-id="3b2d6-155">Fare clic su **OK**, quindi nuovamente su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-155">Click **OK** and **OK** again.</span></span>

![Single sign-on](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a><span data-ttu-id="3b2d6-157">Considerazioni sui browser</span><span class="sxs-lookup"><span data-stu-id="3b2d6-157">Browser considerations</span></span>

#### <a name="mozilla-firefox"></a><span data-ttu-id="3b2d6-158">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="3b2d6-158">Mozilla Firefox</span></span>

<span data-ttu-id="3b2d6-159">Mozilla Firefox non esegue automaticamente l'autenticazione Kerberos.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-159">Mozilla Firefox doesn't automatically do Kerberos Authentication.</span></span> <span data-ttu-id="3b2d6-160">Ogni utente deve aggiungere manualmente gli URL di Azure AD alle impostazioni di Firefox usando la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3b2d6-160">Each user has to manually add the Azure AD URLs to their Firefox settings using the following steps:</span></span>
1. <span data-ttu-id="3b2d6-161">Eseguire Firefox e immettere `about:config` nella barra degli indirizzi.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-161">Run Firefox and enter `about:config` in the address bar.</span></span> <span data-ttu-id="3b2d6-162">Eliminare tutte le notifiche visualizzate.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-162">Dismiss any notifications that you see.</span></span>
2. <span data-ttu-id="3b2d6-163">Cercare la preferenza **network.negotiate-auth.trusted-uris**.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-163">Search for the **network.negotiate-auth.trusted-uris** preference.</span></span> <span data-ttu-id="3b2d6-164">Questa preferenza elenca i siti attendibili di Firefox per l'autenticazione Kerberos.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-164">This preference lists Firefox's trusted sites for Kerberos authentication.</span></span>
3. <span data-ttu-id="3b2d6-165">Fare clic con il pulsante destro del mouse e selezionare "Modifica".</span><span class="sxs-lookup"><span data-stu-id="3b2d6-165">Right-click and select "Modify".</span></span>
4. <span data-ttu-id="3b2d6-166">Immettere "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" nel campo.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-166">Enter "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" in the field.</span></span>
5. <span data-ttu-id="3b2d6-167">Fare clic su "OK" e riaprire il browser.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-167">Click "OK" and reopen the browser.</span></span>

#### <a name="safari-on-mac-os"></a><span data-ttu-id="3b2d6-168">Safari su Mac OS</span><span class="sxs-lookup"><span data-stu-id="3b2d6-168">Safari on Mac OS</span></span>

<span data-ttu-id="3b2d6-169">Verificare che il computer che esegue Mac OS sia stato aggiunto a un dominio di AD.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-169">Ensure that the machine running Mac OS is joined to AD.</span></span> <span data-ttu-id="3b2d6-170">[Qui](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf) sono disponibili istruzioni su come eseguire l'operazione.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-170">See instructions on how to do that [here](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span></span>

#### <a name="google-chrome-on-mac-os"></a><span data-ttu-id="3b2d6-171">Google Chrome su Mac OS</span><span class="sxs-lookup"><span data-stu-id="3b2d6-171">Google Chrome on Mac OS</span></span>

<span data-ttu-id="3b2d6-172">Per Google Chrome su Mac OS e altre piattaforme non Windows, fare riferimento a [questo articolo](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) per informazioni su come aggiungere gli URL di Azure AD all'elenco degli elementi consentiti per l'autenticazione integrata.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-172">For Google Chrome on Mac OS and other non-Windows platforms, refer to [this article](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) for information on how to whitelist the Azure AD URLs for integrated authentication.</span></span>

<span data-ttu-id="3b2d6-173">L'uso delle estensioni dei Criteri di gruppo di Active Directory di terze parti per distribuire gli URL di Azure AD in Firefox e Google Chrome su Mac esula dall'ambito di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-173">Using third-party Active Directory Group Policy extensions to roll out the Azure AD URLs to Firefox and Google Chrome on Mac users is outside of this article's scope.</span></span>

#### <a name="known-limitations"></a><span data-ttu-id="3b2d6-174">Limitazioni note</span><span class="sxs-lookup"><span data-stu-id="3b2d6-174">Known limitations</span></span>

<span data-ttu-id="3b2d6-175">L'accesso SSO facile non funziona in modalità di esplorazione privata in Firefox e nel browser Edge.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-175">Seamless SSO doesn't work in private browsing mode on Firefox and Edge browsers.</span></span> <span data-ttu-id="3b2d6-176">Non funziona inoltre in Internet Explorer se il browser è in esecuzione in modalità di protezione avanzata.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-176">It also doesn't work on Internet Explorer if the browser is running in Enhanced Protection mode.</span></span>

>[!IMPORTANT]
><span data-ttu-id="3b2d6-177">Di recente è stato eseguito il rollback del supporto per Microsoft Edge per analizzare i problemi segnalati dai clienti.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-177">We recently rolled back support for Edge to investigate customer-reported issues.</span></span>

## <a name="step-4-test-the-feature"></a><span data-ttu-id="3b2d6-178">Passaggio 4: Testare la funzionalità</span><span class="sxs-lookup"><span data-stu-id="3b2d6-178">Step 4: Test the feature</span></span>

<span data-ttu-id="3b2d6-179">Per testare la funzionalità per un utente specifico, assicurarsi che _tutte_ le condizioni seguenti siano soddisfatte:</span><span class="sxs-lookup"><span data-stu-id="3b2d6-179">To test the feature for a specific user, ensure that _all_ the following conditions are in place:</span></span>
  - <span data-ttu-id="3b2d6-180">L'utente esegue l'accesso da un dispositivo aziendale.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-180">The user is signing in on a corporate device.</span></span>
  - <span data-ttu-id="3b2d6-181">Il dispositivo è stato aggiunto in precedenza al dominio di Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="3b2d6-181">The device has been previously joined to your Active Directory (AD) domain.</span></span>
  - <span data-ttu-id="3b2d6-182">Il dispositivo ha una connessione diretta al controller di dominio (DC, Domain Controller), nella rete aziendale cablata o wireless o tramite una connessione di accesso remoto, ad esempio una connessione VPN.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-182">The device has a direct connection to your Domain Controller (DC), either on the corporate wired or wireless network or via a remote access connection, such as a VPN connection.</span></span>
  - <span data-ttu-id="3b2d6-183">La [funzionalità è stata distribuita](##step-3-roll-out-the-feature) all'utente tramite Criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-183">You have [rolled out the feature](##step-3-roll-out-the-feature) to this user using Group Policy.</span></span>

<span data-ttu-id="3b2d6-184">Per testare lo scenario in cui l'utente immette solo il nome utente ma non la password:</span><span class="sxs-lookup"><span data-stu-id="3b2d6-184">To test the scenario where the user enters only the username, but not the password:</span></span>
- <span data-ttu-id="3b2d6-185">Accedere a *https://myapps.microsoft.com/* in una nuova sessione del browser privata.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-185">Sign into *https://myapps.microsoft.com/* in a new private browser session.</span></span>

<span data-ttu-id="3b2d6-186">Per testare lo scenario in cui l'utente non è obbligato a immettere nome utente o password:</span><span class="sxs-lookup"><span data-stu-id="3b2d6-186">To test the scenario where the user doesn't have to enter the username or the password:</span></span> 
- <span data-ttu-id="3b2d6-187">Accedere a *https://myapps.microsoft.com/contoso.onmicrosoft.com* in una nuova sessione del browser privata.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-187">Sign into *https://myapps.microsoft.com/contoso.onmicrosoft.com* in a new private browser session.</span></span> <span data-ttu-id="3b2d6-188">Sostituire "*contoso*" con il nome del tenant.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-188">Replace "*contoso*" with your tenant's name.</span></span>
- <span data-ttu-id="3b2d6-189">In alternativa, accedere a *https://myapps.microsoft.com/contoso.com* in una nuova sessione del browser privata.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-189">Or sign into *https://myapps.microsoft.com/contoso.com* in a new private browser session.</span></span> <span data-ttu-id="3b2d6-190">Sostituire "*contoso.com*" con un dominio verificato, non un dominio federato, nel tenant.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-190">Replace "*contoso.com*" with a verified domain (not a federated domain) in your tenant.</span></span>

## <a name="step-5-roll-over-keys"></a><span data-ttu-id="3b2d6-191">Passaggio 5: Rinnovare le chiavi</span><span class="sxs-lookup"><span data-stu-id="3b2d6-191">Step 5: Roll over keys</span></span>

<span data-ttu-id="3b2d6-192">Nel passaggio 2, Azure AD Connect crea gli account computer, che rappresentano Azure AD, in tutte le foreste di AD in cui è stato abilitato l'accesso SSO facile.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-192">In Step 2, Azure AD Connect creates computer accounts (representing Azure AD) in all the AD forests on which you have enabled Seamless SSO.</span></span> <span data-ttu-id="3b2d6-193">[Qui](active-directory-aadconnect-sso-how-it-works.md) sono disponibili informazioni dettagliate a riguardo.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-193">Learn more in detail [here](active-directory-aadconnect-sso-how-it-works.md).</span></span> <span data-ttu-id="3b2d6-194">Per una maggiore sicurezza, è consigliabile rinnovare spesso le chiavi di decrittografia di Kerberos di questi account computer.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-194">For improved security, it is recommended that  you frequently roll over the Kerberos decryption keys of these computer accounts.</span></span>

>[!IMPORTANT]
><span data-ttu-id="3b2d6-195">Non è necessario farlo _subito_ dopo aver abilitato la funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-195">You don't need to do this step _immediately_ after you have enabled the feature.</span></span> <span data-ttu-id="3b2d6-196">Rinnovare le chiave di decrittografia di Kerberos almeno ogni 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-196">Roll over the Kerberos decryption keys at least every 30 days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b2d6-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3b2d6-197">Next steps</span></span>

- <span data-ttu-id="3b2d6-198">[**Approfondimento tecnico**](active-directory-aadconnect-sso-how-it-works.md): informazioni sul funzionamento di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-198">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="3b2d6-199">[**Domande frequenti**](active-directory-aadconnect-sso-faq.md): risposte alle domande più frequenti.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-199">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="3b2d6-200">[**Risoluzione dei problemi**](active-directory-aadconnect-troubleshoot-sso.md): informazioni su come risolvere i problemi comuni relativi a questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-200">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="3b2d6-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): per l'invio di richieste di nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3b2d6-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
