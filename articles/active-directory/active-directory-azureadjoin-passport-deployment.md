---
title: Abilitare Microsoft Windows Hello for Business nell'organizzazione | Documentazione Microsoft
description: Istruzioni per la distribuzione per abilitare Microsoft Passport all'interno dell'organizzazione.
services: active-directory
documentationcenter: 
keywords: configurare Microsoft Passport, distribuzione di Microsoft Windows Hello for Business
author: MarkusVi
manager: femila
tags: azure-classic-portal
ms.assetid: 7dbbe3c6-1cd7-429c-a9b2-115fcbc02416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: 58943e1e29755c983e55c675dd4fe7b75ac47b34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a><span data-ttu-id="563fa-104">Abilitare Microsoft Windows Hello for Business nell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="563fa-104">Enable Microsoft Windows Hello for Business in your organization</span></span>
<span data-ttu-id="563fa-105">Dopo [aver connesso i dispositivi appartenenti a un dominio di Windows 10 ad Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), seguire questa procedura per abilitare Microsoft Windows Hello for Business nell'organizzazione:</span><span class="sxs-lookup"><span data-stu-id="563fa-105">After [connecting Windows 10 domain-joined devices with Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), do the following to enable Microsoft Windows Hello for Business in your organization:</span></span>

1. <span data-ttu-id="563fa-106">Distribuire System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="563fa-106">Deploy System Center Configuration Manager</span></span>  
2. <span data-ttu-id="563fa-107">Configurare le impostazioni dei criteri</span><span class="sxs-lookup"><span data-stu-id="563fa-107">Configure policy settings</span></span>
3. <span data-ttu-id="563fa-108">Configurare il profilo certificato</span><span class="sxs-lookup"><span data-stu-id="563fa-108">Configure the certificate profile</span></span>  

## <a name="deploy-system-center-configuration-manager"></a><span data-ttu-id="563fa-109">Distribuire System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="563fa-109">Deploy System Center Configuration Manager</span></span>
<span data-ttu-id="563fa-110">Per distribuire certificati utente in base alle chiavi di Windows Hello for Business, è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="563fa-110">To deploy user certificates based on Windows Hello for Business keys, you need the following:</span></span>

* <span data-ttu-id="563fa-111">**System Center Configuration Manager Current Branch**: è necessario installare la versione 1606 o successiva.</span><span class="sxs-lookup"><span data-stu-id="563fa-111">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span></span> <span data-ttu-id="563fa-112">Per altre informazioni, vedere la [documentazione di System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) e il [blog del team di System Center Configuration Manager](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span><span class="sxs-lookup"><span data-stu-id="563fa-112">For more information, see the [Documentation for System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) and [System Center Configuration Manager Team Blog](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span></span>
* <span data-ttu-id="563fa-113">**Infrastruttura a chiave pubblica (PKI)**: per abilitare Microsoft Windows Hello for Business usando i certificati utente, è necessario avere un'infrastruttura PKI.</span><span class="sxs-lookup"><span data-stu-id="563fa-113">**Public key infrastructure (PKI)** - To enable Microsoft Windows Hello for Business by using user certificates, you must have a PKI in place.</span></span> <span data-ttu-id="563fa-114">Se non si dispone di un'infrastruttura di questo tipo o non si desidera usarla per i certificati utente, è possibile distribuire un nuovo controller di dominio che abbia installato Windows Server 2016 build 10551 (o versione successiva).</span><span class="sxs-lookup"><span data-stu-id="563fa-114">If you don’t have one, or you don’t want to use it for user certificates, you can deploy a new domain controller that has Windows Server 2016 build 10551 (or better) installed.</span></span> <span data-ttu-id="563fa-115">Seguire i passaggi per [installare un controller di dominio di replica in un dominio esistente](https://technet.microsoft.com/library/jj574134.aspx) o per [installare una nuova foresta di Active Directory, se si crea un nuovo ambiente](https://technet.microsoft.com/library/jj574166).</span><span class="sxs-lookup"><span data-stu-id="563fa-115">Follow the steps to [install a replica domain controller in an existing domain](https://technet.microsoft.com/library/jj574134.aspx) or to [install a new Active Directory forest, if you're creating a new environment](https://technet.microsoft.com/library/jj574166).</span></span> <span data-ttu-id="563fa-116">I file con estensione iso sono disponibili per il download in [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).</span><span class="sxs-lookup"><span data-stu-id="563fa-116">(The ISOs are available for download on [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span></span>

## <a name="configure-policy-settings"></a><span data-ttu-id="563fa-117">Configurare le impostazioni dei criteri</span><span class="sxs-lookup"><span data-stu-id="563fa-117">Configure policy settings</span></span>
<span data-ttu-id="563fa-118">Per configurare le impostazioni dei criteri di Microsoft Windows Hello for Business, sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="563fa-118">To configure the Microsoft Windows Hello for Business policy settings, you have two options:</span></span>

* <span data-ttu-id="563fa-119">Criteri di gruppo in Active Directory</span><span class="sxs-lookup"><span data-stu-id="563fa-119">Group Policy in Active Directory</span></span> 
* <span data-ttu-id="563fa-120">System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="563fa-120">The System Center Configuration Manager</span></span> 

<span data-ttu-id="563fa-121">Usare Criteri di gruppo in Active Directory è il metodo consigliato per configurare le impostazioni dei criteri di Microsoft Windows Hello for Business.</span><span class="sxs-lookup"><span data-stu-id="563fa-121">Using Group Policy in Active Directory is the recommended method to configure Microsoft Windows Hello for Business policy settings.</span></span> 

<span data-ttu-id="563fa-122">Usare System Center Configuration Manager è il metodo preferito quando lo si usa anche per distribuire i certificati.</span><span class="sxs-lookup"><span data-stu-id="563fa-122">Using System Center Configuration Manager is the preferred method when you also use it to deploy certificates.</span></span> <span data-ttu-id="563fa-123">Questo scenario:</span><span class="sxs-lookup"><span data-stu-id="563fa-123">This scenario:</span></span>

* <span data-ttu-id="563fa-124">Assicura la compatibilità con gli scenari di distribuzione più recenti</span><span class="sxs-lookup"><span data-stu-id="563fa-124">Ensures compatibility with the newer deployment scenarios</span></span>
* <span data-ttu-id="563fa-125">Richiede Windows 10 versione 1607 o successiva sul lato client.</span><span class="sxs-lookup"><span data-stu-id="563fa-125">Requires on the client side Windows 10 Version 1607 or better.</span></span>

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a><span data-ttu-id="563fa-126">Configurare Microsoft Windows Hello for Business tramite Criteri di gruppo in Active Directory</span><span class="sxs-lookup"><span data-stu-id="563fa-126">Configure Microsoft Windows Hello for Business via group policy in Active Directory</span></span>
<span data-ttu-id="563fa-127">**Passaggi**:</span><span class="sxs-lookup"><span data-stu-id="563fa-127">**Steps**:</span></span>

1. <span data-ttu-id="563fa-128">Aprire Server Manager e passare a **Strumenti** > **Gestione Criteri di gruppo**.</span><span class="sxs-lookup"><span data-stu-id="563fa-128">Open Server Manager, and navigate to **Tools** > **Group Policy Management**.</span></span>
2. <span data-ttu-id="563fa-129">Da Gestione Criteri di gruppo passare al nodo corrispondente al dominio in cui abilitare la funzionalità di aggiunta ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="563fa-129">From Group Policy Management, navigate to the domain node that corresponds to the domain in which you want to enable Azure AD Join.</span></span>
3. <span data-ttu-id="563fa-130">Fare clic con il pulsante destro del mouse su **Oggetti Criteri di gruppo** e scegliere **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="563fa-130">Right-click **Group Policy Objects**, and select **New**.</span></span> <span data-ttu-id="563fa-131">Assegnare un nome all'oggetto Criteri di gruppo, ad esempio Abilita Windows Hello for Business.</span><span class="sxs-lookup"><span data-stu-id="563fa-131">Give your Group Policy Object a name, for example, Enable Windows Hello for Business.</span></span> <span data-ttu-id="563fa-132">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="563fa-132">Click **OK**.</span></span>
4. <span data-ttu-id="563fa-133">Fare clic con il pulsante destro del mouse sul nuovo oggetto Criteri di gruppo e scegliere **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="563fa-133">Right-click your new Group Policy Object, and then select **Edit**.</span></span>
5. <span data-ttu-id="563fa-134">Passare a **Configurazione computer** > **Criteri** > **Modelli amministrativi** > **Componenti di Windows** > **Windows Hello for Business**.</span><span class="sxs-lookup"><span data-stu-id="563fa-134">Navigate to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Windows Hello for Business**.</span></span>
6. <span data-ttu-id="563fa-135">Fare doppio clic su **Abilita Windows Hello for Business** e selezionare **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="563fa-135">Right-click **Enable Windows Hello for Business**, and then select **Edit**.</span></span>
7. <span data-ttu-id="563fa-136">Selezionare il pulsante di opzione **Abilitato** e fare clic su **Applica**.</span><span class="sxs-lookup"><span data-stu-id="563fa-136">Select the **Enabled** option button, and then click **Apply**.</span></span> <span data-ttu-id="563fa-137">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="563fa-137">Click **OK**.</span></span>
8. <span data-ttu-id="563fa-138">È ora possibile collegare l'oggetto Criteri di gruppo a una posizione di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="563fa-138">You can now link the Group Policy Object to a location of your choice.</span></span> <span data-ttu-id="563fa-139">Per abilitare questo oggetto per tutti i dispositivi appartenenti a un dominio di Windows 10 nell'organizzazione, collegarlo al dominio.</span><span class="sxs-lookup"><span data-stu-id="563fa-139">To enable this policy for all of the domain-joined Windows 10 devices in your organization, link the Group Policy to the domain.</span></span> <span data-ttu-id="563fa-140">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="563fa-140">For example:</span></span>
   * <span data-ttu-id="563fa-141">Una specifica unità organizzativa in Active Directory in cui saranno posizionati i computer Windows 10 aggiunti a un dominio.</span><span class="sxs-lookup"><span data-stu-id="563fa-141">A specific organizational unit (OU) in Active Directory where Windows 10 domain-joined computers will be located</span></span>
   * <span data-ttu-id="563fa-142">Uno specifico gruppo di sicurezza contenente i computer appartenenti a un dominio di Windows 10 che verranno registrati automaticamente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="563fa-142">A specific security group that contains Windows 10 domain-joined computers that will be automatically registered with Azure AD</span></span>

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a><span data-ttu-id="563fa-143">Configurare Windows Hello for Business mediante System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="563fa-143">Configure Windows Hello for Business using System Center Configuration Manager</span></span>
<span data-ttu-id="563fa-144">**Passaggi**:</span><span class="sxs-lookup"><span data-stu-id="563fa-144">**Steps**:</span></span>

1. <span data-ttu-id="563fa-145">Aprire **System Center Configuration Manager**, passare ad **Asset e conformità > Impostazioni di conformità > Accesso risorse aziendali > Profili Windows Hello for Business**.</span><span class="sxs-lookup"><span data-stu-id="563fa-145">Open the **System Center Configuration Manager**, and then navigate to **Assets & Compliance > Compliance Settings > Company Resource Access > Windows Hello for Business Profiles**.</span></span>
   
    ![Configurare Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. <span data-ttu-id="563fa-147">Nella barra degli strumenti nella parte superiore fare clic su **Crea profilo Windows Hello for Business**.</span><span class="sxs-lookup"><span data-stu-id="563fa-147">In the toolbar on the top, click **Create Windows Hello for business Profile**.</span></span>
   
    ![Configurare Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. <span data-ttu-id="563fa-149">Nella finestra di dialogo **Generale** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="563fa-149">On the **General** dialog, perform the following steps:</span></span>
   
    ![Configurare Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    <span data-ttu-id="563fa-151">a.</span><span class="sxs-lookup"><span data-stu-id="563fa-151">a.</span></span> <span data-ttu-id="563fa-152">Nella casella di testo **Nome** digitare un nome per il profilo, ad esempio **Il mio profilo WHfB**.</span><span class="sxs-lookup"><span data-stu-id="563fa-152">In the **Name** textbox, type a name for your profile, for example, **My WHfB Profile**.</span></span>
   
    <span data-ttu-id="563fa-153">b.</span><span class="sxs-lookup"><span data-stu-id="563fa-153">b.</span></span> <span data-ttu-id="563fa-154">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="563fa-154">Click **Next**.</span></span>
4. <span data-ttu-id="563fa-155">Nella finestra di dialogo **Piattaforme supportate** selezionare le piattaforme che saranno fornite con questo profilo Windows Hello for Business e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="563fa-155">On the **Supported Platforms** dialog, select the platforms that will be provisioned with this Windows Hello for business profile, and then click **Next**.</span></span>
   
    ![Configurare Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. <span data-ttu-id="563fa-157">Nella finestra di dialogo **Impostazioni** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="563fa-157">On the **Settings** dialog, perform the following steps:</span></span>
   
    ![Configurare Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    <span data-ttu-id="563fa-159">a.</span><span class="sxs-lookup"><span data-stu-id="563fa-159">a.</span></span> <span data-ttu-id="563fa-160">Per **Configura Windows Hello for Business** selezionare **Attivato**.</span><span class="sxs-lookup"><span data-stu-id="563fa-160">As **Configure Windows Hello for Business**, select **Enabled**.</span></span>
   
    <span data-ttu-id="563fa-161">b.</span><span class="sxs-lookup"><span data-stu-id="563fa-161">b.</span></span> <span data-ttu-id="563fa-162">Per **Usa Trusted Platform Module (TPM)** selezionare **Richiesto**.</span><span class="sxs-lookup"><span data-stu-id="563fa-162">As **Use a Trusted Platform Module (TPM)**, select **Required**.</span></span> 
   
    <span data-ttu-id="563fa-163">c.</span><span class="sxs-lookup"><span data-stu-id="563fa-163">c.</span></span> <span data-ttu-id="563fa-164">Per **Metodo di autenticazione** selezionare **Basata su certificati**.</span><span class="sxs-lookup"><span data-stu-id="563fa-164">As **Authentication method**, select **Certificate-based**.</span></span>
   
    <span data-ttu-id="563fa-165">d.</span><span class="sxs-lookup"><span data-stu-id="563fa-165">d.</span></span> <span data-ttu-id="563fa-166">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="563fa-166">Click **Next**.</span></span>
6. <span data-ttu-id="563fa-167">Nella finestra di dialogo **Riepilogo** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="563fa-167">On the **Summary** dialog, click **Next**.</span></span>
7. <span data-ttu-id="563fa-168">Nella finestra di dialogo **Completamento** fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="563fa-168">On the **Completion** dialog, click **Close**.</span></span>
8. <span data-ttu-id="563fa-169">Nel barra degli strumenti in alto fare clic su **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="563fa-169">In the toolbar on the top, click **Deploy**.</span></span>
   
    ![Configurare Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-the-certificate-profile"></a><span data-ttu-id="563fa-171">Configurare il profilo certificato</span><span class="sxs-lookup"><span data-stu-id="563fa-171">Configure the certificate profile</span></span>
<span data-ttu-id="563fa-172">Se si usa l'autenticazione basata su certificato per l'autenticazione locale, è necessario configurare e distribuire un profilo del certificato.</span><span class="sxs-lookup"><span data-stu-id="563fa-172">If you are using certificate-based authentication for on-premises authentication, you need to configure and deploy a certificate profile.</span></span> <span data-ttu-id="563fa-173">Questa attività richiede di configurare un server NDES e il ruolo del sito del punto di registrazione certificati in System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="563fa-173">This task requires you to set up an NDES server and Certificate Registration Point site role in the System Center Configuration Manager.</span></span> <span data-ttu-id="563fa-174">Per altre informazioni, vedere [Prerequisiti per i profili certificato in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span><span class="sxs-lookup"><span data-stu-id="563fa-174">For more details, see the [Prerequisites for Certificate Profiles in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span></span>

1. <span data-ttu-id="563fa-175">Aprire **System Center Configuration Manager**, quindi passare ad **Asset e conformità > Impostazioni di conformità > Accesso risorse aziendali > Profili certificato**.</span><span class="sxs-lookup"><span data-stu-id="563fa-175">Open the **System Center Configuration Manager**, and then navigate to **Assets & Compliance > Compliance Settings > Company Resource Access > Certificate Profiles**.</span></span>
2. <span data-ttu-id="563fa-176">Selezionare un modello dotato di utilizzo chiavi avanzato (EKU) per l'accesso con smart card.</span><span class="sxs-lookup"><span data-stu-id="563fa-176">Select a template that has Smart Card sign-in extended key usage (EKU).</span></span>

<span data-ttu-id="563fa-177">Nella pagina **Registrazione SCEP** del profilo certificato è necessario scegliere **Installa in Passport for Work oppure genera errore** come **Provider di archiviazione chiavi**.</span><span class="sxs-lookup"><span data-stu-id="563fa-177">On the **SCEP Enrollment** page of the certificate profile, you need to choose **Install to Passport for Work otherwise fail** as the **Key Storage Provider**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="563fa-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="563fa-178">Next steps</span></span>
* [<span data-ttu-id="563fa-179">Windows 10 per le aziende: modalità d'uso dei dispositivi di lavoro</span><span class="sxs-lookup"><span data-stu-id="563fa-179">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="563fa-180">Estensione delle funzionalità del cloud ai dispositivi Windows 10 tramite Aggiunta ad Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="563fa-180">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="563fa-181">Autenticazione delle identità senza password con Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="563fa-181">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="563fa-182">Scenari di utilizzo per Aggiunta ad Azure AD</span><span class="sxs-lookup"><span data-stu-id="563fa-182">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="563fa-183">Connettere dispositivi appartenenti a un dominio ad Azure AD per usufruire di Windows 10</span><span class="sxs-lookup"><span data-stu-id="563fa-183">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="563fa-184">Configurare Aggiunta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="563fa-184">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

