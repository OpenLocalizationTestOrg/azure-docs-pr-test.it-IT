---
title: aaaConfigure Secure LDAP (LDAPS) in servizi di dominio Active Directory di Azure | Documenti Microsoft
description: Configurare l'accesso LDAP sicuro (LDAPS) per un dominio gestito di Servizi di dominio Azure AD
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 99e44d917b115d7f7a67ff0a5e22c5c9165287e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="969ac-103">Configurare l'accesso LDAP sicuro (LDAPS) per un dominio gestito di Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="969ac-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="969ac-104">Questo articolo illustra come abilitare l'accesso LDAPS (Secure Lightweight Directory Access Protocol) per il dominio gestito di Servizi di dominio Azure AD.</span><span class="sxs-lookup"><span data-stu-id="969ac-104">This article shows how you can enable Secure Lightweight Directory Access Protocol (LDAPS) for your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="969ac-105">L'accesso LDAP sicuro è noto anche come LDAP (Lightweight Directory Access Protocol) su SSL (Secure Sockets Layer) / TLS (Transport Layer Security).</span><span class="sxs-lookup"><span data-stu-id="969ac-105">Secure LDAP is also known as 'Lightweight Directory Access Protocol (LDAP) over Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="969ac-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="969ac-106">Before you begin</span></span>
<span data-ttu-id="969ac-107">attività di hello tooperform elencate in questo articolo, è necessario:</span><span class="sxs-lookup"><span data-stu-id="969ac-107">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="969ac-108">Una **sottoscrizione di Azure**valida.</span><span class="sxs-lookup"><span data-stu-id="969ac-108">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="969ac-109">Una **directory di Azure AD** sincronizzata con una directory locale o con una directory solo cloud.</span><span class="sxs-lookup"><span data-stu-id="969ac-109">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="969ac-110">**Servizi di dominio AD Azure** deve essere abilitato per la directory hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="969ac-110">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="969ac-111">Se non è ancora fatto, seguire tutte le attività descritte nella hello hello [Guida introduttiva](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="969ac-111">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="969ac-112">Oggetto **tooenable toobe utilizzato certificato secure LDAP**.</span><span class="sxs-lookup"><span data-stu-id="969ac-112">A **certificate toobe used tooenable secure LDAP**.</span></span>

   * <span data-ttu-id="969ac-113">È **consigliabile** ottenere un certificato da un'autorità di certificazione pubblica attendibile.</span><span class="sxs-lookup"><span data-stu-id="969ac-113">**Recommended** - Obtain a certificate from a trusted public certification authority.</span></span> <span data-ttu-id="969ac-114">Questa opzione di configurazione è più sicura.</span><span class="sxs-lookup"><span data-stu-id="969ac-114">This configuration option is more secure.</span></span>
   * <span data-ttu-id="969ac-115">In alternativa, è possibile anche scegliere troppo[creare un certificato autofirmato](#task-1---obtain-a-certificate-for-secure-ldap) come illustrato più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="969ac-115">Alternately, you may also choose too[create a self-signed certificate](#task-1---obtain-a-certificate-for-secure-ldap) as shown later in this article.</span></span>

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a><span data-ttu-id="969ac-116">Requisiti di certificato LDAP sicuro hello</span><span class="sxs-lookup"><span data-stu-id="969ac-116">Requirements for hello secure LDAP certificate</span></span>
<span data-ttu-id="969ac-117">Acquisire un certificato valido per hello seguendo le istruzioni, prima di abilitare accesso LDAP sicuro.</span><span class="sxs-lookup"><span data-stu-id="969ac-117">Acquire a valid certificate per hello following guidelines, before you enable secure LDAP.</span></span> <span data-ttu-id="969ac-118">Si verificano errori, se si tenta di tooenable LDAP sicuro per il dominio gestito con un certificato non valido o corretto.</span><span class="sxs-lookup"><span data-stu-id="969ac-118">You encounter failures if you try tooenable secure LDAP for your managed domain with an invalid/incorrect certificate.</span></span>

1. <span data-ttu-id="969ac-119">**Autorità emittente attendibile** -hello certificato deve essere emesso da un'autorità attendibile dai computer che si connettono toohello dominio gestito utilizzando il protocollo LDAP sicuro.</span><span class="sxs-lookup"><span data-stu-id="969ac-119">**Trusted issuer** - hello certificate must be issued by an authority trusted by computers connecting toohello managed domain using secure LDAP.</span></span> <span data-ttu-id="969ac-120">L'autorità può essere un'autorità di certificazione pubblica considerata attendibile da questi computer.</span><span class="sxs-lookup"><span data-stu-id="969ac-120">This authority may be a public certification authority trusted by these computers.</span></span>
2. <span data-ttu-id="969ac-121">**Durata** -hello certificato deve essere valido per almeno hello Avanti 3-6 mesi.</span><span class="sxs-lookup"><span data-stu-id="969ac-121">**Lifetime** - hello certificate must be valid for at least hello next 3-6 months.</span></span> <span data-ttu-id="969ac-122">Scadenza del certificato hello, accesso LDAP sicuro tooyour una dominio gestito non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="969ac-122">Secure LDAP access tooyour managed domain is disrupted when hello certificate expires.</span></span>
3. <span data-ttu-id="969ac-123">**Nome del soggetto** -nome del soggetto hello certificato hello deve essere un carattere jolly per il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="969ac-123">**Subject name** - hello subject name on hello certificate must be a wildcard for your managed domain.</span></span> <span data-ttu-id="969ac-124">Ad esempio, se il dominio è denominato 'contoso100.com', nome del soggetto del certificato hello deve essere ' *. contoso100.com'.</span><span class="sxs-lookup"><span data-stu-id="969ac-124">For instance, if your domain is named 'contoso100.com', hello certificate's subject name must be '*.contoso100.com'.</span></span> <span data-ttu-id="969ac-125">Impostare il nome di carattere jolly toothis hello DNS nome (nome alternativo soggetto).</span><span class="sxs-lookup"><span data-stu-id="969ac-125">Set hello DNS name (subject alternate name) toothis wildcard name.</span></span>
4. <span data-ttu-id="969ac-126">**Utilizzo chiave** - hello certificato deve essere configurato per hello seguente utilizza - firme digitali e crittografia chiave.</span><span class="sxs-lookup"><span data-stu-id="969ac-126">**Key usage** - hello certificate must be configured for hello following uses - Digital signatures and key encipherment.</span></span>
5. <span data-ttu-id="969ac-127">**Scopo del certificato** -hello certificato deve essere valido per l'autenticazione server SSL.</span><span class="sxs-lookup"><span data-stu-id="969ac-127">**Certificate purpose** - hello certificate must be valid for SSL server authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="969ac-128">**Autorità di certificazione globali (enterprise):** Azure AD Domain Services non supporta l'uso di certificati LDAP sicuri rilasciati dall'autorità di certificazione globale (enterprise) dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="969ac-128">**Enterprise Certification Authorities:** Azure AD Domain Services does not support using secure LDAP certificates issued by your organization's enterprise certification authority.</span></span> <span data-ttu-id="969ac-129">Questa restrizione è perché il servizio di hello non considera attendibile la CA come autorità di certificazione radice dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="969ac-129">This restriction is because hello service does not trust your enterprise CA as a root certification authority.</span></span> 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a><span data-ttu-id="969ac-130">Attività 1: Ottenere un certificato per l'accesso LDAP sicuro</span><span class="sxs-lookup"><span data-stu-id="969ac-130">Task 1 - obtain a certificate for secure LDAP</span></span>
<span data-ttu-id="969ac-131">Hello prima attività comporta l'acquisizione di un certificato utilizzato per l'accesso LDAP sicuro toohello una dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="969ac-131">hello first task involves obtaining a certificate used for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="969ac-132">Sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="969ac-132">You have two options:</span></span>

* <span data-ttu-id="969ac-133">Ottenere un certificato da un'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="969ac-133">Obtain a certificate from a certification authority.</span></span> <span data-ttu-id="969ac-134">autorità Hello potrebbe essere un'autorità di certificazione pubblica.</span><span class="sxs-lookup"><span data-stu-id="969ac-134">hello authority may be a public certification authority.</span></span>
* <span data-ttu-id="969ac-135">Creare un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="969ac-135">Create a self-signed certificate.</span></span>

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a><span data-ttu-id="969ac-136">Opzione A (scelta consigliata): ottenere un certificato LDAP sicuro da un'autorità di certificazione</span><span class="sxs-lookup"><span data-stu-id="969ac-136">Option A (Recommended) - Obtain a secure LDAP certificate from a certification authority</span></span>
<span data-ttu-id="969ac-137">Se l'organizzazione Ottiene i certificati da un'autorità di certificazione pubblica, è necessario certificati secure LDAP tooobtain hello da tale autorità di certificazione pubblica.</span><span class="sxs-lookup"><span data-stu-id="969ac-137">If your organization obtains its certificates from a public certification authority, you need tooobtain hello secure LDAP certificate from that public certification authority.</span></span>

<span data-ttu-id="969ac-138">Quando viene richiesto un certificato, assicurarsi che siano soddisfatti tutti i requisiti di hello descritti [requisiti di certificato LDAP sicuro hello](#requirements-for-the-secure-ldap-certificate).</span><span class="sxs-lookup"><span data-stu-id="969ac-138">When requesting a certificate, ensure that you satisfy all hello requirements outlined in [Requirements for hello secure LDAP certificate](#requirements-for-the-secure-ldap-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="969ac-139">Computer client che devono tooconnect toohello dominio gestito utilizzando il protocollo LDAP sicuro deve emittente hello del certificato LDAP sicuro hello.</span><span class="sxs-lookup"><span data-stu-id="969ac-139">Client computers that need tooconnect toohello managed domain using secure LDAP must trust hello issuer of hello secure LDAP certificate.</span></span>
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a><span data-ttu-id="969ac-140">Opzione B: creare un certificato autofirmato per l'accesso LDAP sicuro</span><span class="sxs-lookup"><span data-stu-id="969ac-140">Option B - Create a self-signed certificate for secure LDAP</span></span>
<span data-ttu-id="969ac-141">Se non si prevede di toouse un certificato da un'autorità di certificazione pubblica, è possibile scegliere toocreate un certificato autofirmato per l'accesso LDAP sicuro.</span><span class="sxs-lookup"><span data-stu-id="969ac-141">If you do not expect toouse a certificate from a public certification authority, you may choose toocreate a self-signed certificate for secure LDAP.</span></span>

<span data-ttu-id="969ac-142">**Creare un certificato autofirmato con PowerShell**</span><span class="sxs-lookup"><span data-stu-id="969ac-142">**Create a self-signed certificate using PowerShell**</span></span>

<span data-ttu-id="969ac-143">Nel computer Windows, aprire una nuova finestra di PowerShell come **amministratore** e hello tipo seguendo i comandi, toocreate un nuovo certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="969ac-143">On your Windows computer, open a new PowerShell window as **Administrator** and type hello following commands, toocreate a new self-signed certificate.</span></span>

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

<span data-ttu-id="969ac-144">Nel precedente esempio di hello, sostituire "*. contoso100.com' con nome di dominio DNS hello del dominio gestito. Ad esempio, se è stato creato un dominio gestito chiamato 'contoso100.onmicrosoft.com', sostituire "*. contoso100.com' in hello di sopra di script con ' *. contoso100.onmicrosoft.com').</span><span class="sxs-lookup"><span data-stu-id="969ac-144">In hello preceding sample, replace '*.contoso100.com' with hello DNS domain name of your managed domain. For example, if you created a managed domain called 'contoso100.onmicrosoft.com', replace '*.contoso100.com' in hello above script with '*.contoso100.onmicrosoft.com').</span></span>

![Selezionare una directory di Azure AD](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

<span data-ttu-id="969ac-146">certificato autofirmato Hello appena creato viene inserito nell'archivio certificati del computer locale hello.</span><span class="sxs-lookup"><span data-stu-id="969ac-146">hello newly created self-signed certificate is placed in hello local machine's certificate store.</span></span>


## <a name="next-step"></a><span data-ttu-id="969ac-147">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="969ac-147">Next step</span></span>
[<span data-ttu-id="969ac-148">Attività 2: esportare hello sicura LDAP certificato tooa. File PFX</span><span class="sxs-lookup"><span data-stu-id="969ac-148">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
