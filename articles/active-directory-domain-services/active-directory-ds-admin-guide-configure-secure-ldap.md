---
title: Configurare l'accesso LDAP sicuro (LDAPS) in Azure Active Directory Domain Services | Microsoft Docs
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
ms.openlocfilehash: 93afa49166c5b31d23237c308b9d34f6d6f3507d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="ae64f-103">Configurare l'accesso LDAP sicuro (LDAPS) per un dominio gestito di Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="ae64f-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="ae64f-104">Questo articolo illustra come abilitare l'accesso LDAPS (Secure Lightweight Directory Access Protocol) per il dominio gestito di Servizi di dominio Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae64f-104">This article shows how you can enable Secure Lightweight Directory Access Protocol (LDAPS) for your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="ae64f-105">L'accesso LDAP sicuro è noto anche come LDAP (Lightweight Directory Access Protocol) su SSL (Secure Sockets Layer) / TLS (Transport Layer Security).</span><span class="sxs-lookup"><span data-stu-id="ae64f-105">Secure LDAP is also known as 'Lightweight Directory Access Protocol (LDAP) over Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ae64f-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="ae64f-106">Before you begin</span></span>
<span data-ttu-id="ae64f-107">Per eseguire le attività elencate in questo articolo sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ae64f-107">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="ae64f-108">Una **sottoscrizione di Azure**valida.</span><span class="sxs-lookup"><span data-stu-id="ae64f-108">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="ae64f-109">Una **directory di Azure AD** sincronizzata con una directory locale o con una directory solo cloud.</span><span class="sxs-lookup"><span data-stu-id="ae64f-109">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="ae64f-110">**Servizi di dominio Azure AD** devono essere abilitati per la directory di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae64f-110">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="ae64f-111">Se non è stato fatto, eseguire tutte le attività descritte nella [guida introduttiva](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="ae64f-111">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="ae64f-112">Un **certificato da usare per abilitare l'accesso LDAP sicuro**.</span><span class="sxs-lookup"><span data-stu-id="ae64f-112">A **certificate to be used to enable secure LDAP**.</span></span>

   * <span data-ttu-id="ae64f-113">È **consigliabile** ottenere un certificato da un'autorità di certificazione pubblica attendibile.</span><span class="sxs-lookup"><span data-stu-id="ae64f-113">**Recommended** - Obtain a certificate from a trusted public certification authority.</span></span> <span data-ttu-id="ae64f-114">Questa opzione di configurazione è più sicura.</span><span class="sxs-lookup"><span data-stu-id="ae64f-114">This configuration option is more secure.</span></span>
   * <span data-ttu-id="ae64f-115">In alternativa, è anche possibile scegliere di [creare un certificato autofirmato](#task-1---obtain-a-certificate-for-secure-ldap) , come illustrato più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="ae64f-115">Alternately, you may also choose to [create a self-signed certificate](#task-1---obtain-a-certificate-for-secure-ldap) as shown later in this article.</span></span>

<br>

### <a name="requirements-for-the-secure-ldap-certificate"></a><span data-ttu-id="ae64f-116">Requisiti per il certificato LDAP sicuro</span><span class="sxs-lookup"><span data-stu-id="ae64f-116">Requirements for the secure LDAP certificate</span></span>
<span data-ttu-id="ae64f-117">Acquisire un certificato valido in base alle linee guida riportate di seguito prima di abilitare l'accesso LDAP sicuro.</span><span class="sxs-lookup"><span data-stu-id="ae64f-117">Acquire a valid certificate per the following guidelines, before you enable secure LDAP.</span></span> <span data-ttu-id="ae64f-118">Se si prova ad abilitare l'accesso LDAP sicuro per il dominio gestito con un certificato non valido o non corretto, si verificano errori.</span><span class="sxs-lookup"><span data-stu-id="ae64f-118">You encounter failures if you try to enable secure LDAP for your managed domain with an invalid/incorrect certificate.</span></span>

1. <span data-ttu-id="ae64f-119">**Autorità di certificazione attendibile** : il certificato deve essere emesso da un'autorità ritenuta attendibile dai computer connessi al dominio gestito tramite accesso LDAP sicuro.</span><span class="sxs-lookup"><span data-stu-id="ae64f-119">**Trusted issuer** - The certificate must be issued by an authority trusted by computers connecting to the managed domain using secure LDAP.</span></span> <span data-ttu-id="ae64f-120">L'autorità può essere un'autorità di certificazione pubblica considerata attendibile da questi computer.</span><span class="sxs-lookup"><span data-stu-id="ae64f-120">This authority may be a public certification authority trusted by these computers.</span></span>
2. <span data-ttu-id="ae64f-121">**Durata** : il certificato deve essere valido almeno per i 3-6 mesi successivi.</span><span class="sxs-lookup"><span data-stu-id="ae64f-121">**Lifetime** - The certificate must be valid for at least the next 3-6 months.</span></span> <span data-ttu-id="ae64f-122">L'accesso LDAP sicuro al dominio gestito viene interrotto allo scadere del certificato.</span><span class="sxs-lookup"><span data-stu-id="ae64f-122">Secure LDAP access to your managed domain is disrupted when the certificate expires.</span></span>
3. <span data-ttu-id="ae64f-123">**Nome soggetto** : il nome del soggetto nel certificato deve includere un carattere jolly per il dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="ae64f-123">**Subject name** - The subject name on the certificate must be a wildcard for your managed domain.</span></span> <span data-ttu-id="ae64f-124">Ad esempio, se il dominio è denominato "contoso100.com", il nome del soggetto nel certificato deve essere "*.contoso100.com".</span><span class="sxs-lookup"><span data-stu-id="ae64f-124">For instance, if your domain is named 'contoso100.com', the certificate's subject name must be '*.contoso100.com'.</span></span> <span data-ttu-id="ae64f-125">Impostare il nome DNS (nome soggetto alternativo) su questo nome con caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="ae64f-125">Set the DNS name (subject alternate name) to this wildcard name.</span></span>
4. <span data-ttu-id="ae64f-126">**Utilizzo chiavi** : il certificato deve essere configurato per l'uso nelle firme digitali e nella crittografia a chiave.</span><span class="sxs-lookup"><span data-stu-id="ae64f-126">**Key usage** - The certificate must be configured for the following uses - Digital signatures and key encipherment.</span></span>
5. <span data-ttu-id="ae64f-127">**Scopo del certificato** : il certificato deve essere valido per l'autenticazione server SSL.</span><span class="sxs-lookup"><span data-stu-id="ae64f-127">**Certificate purpose** - The certificate must be valid for SSL server authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="ae64f-128">**Autorità di certificazione globali (enterprise):** Azure AD Domain Services non supporta l'uso di certificati LDAP sicuri rilasciati dall'autorità di certificazione globale (enterprise) dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="ae64f-128">**Enterprise Certification Authorities:** Azure AD Domain Services does not support using secure LDAP certificates issued by your organization's enterprise certification authority.</span></span> <span data-ttu-id="ae64f-129">Questa restrizione è dovuta al fatto che il servizio non considera attendibile la CA come autorità di certificazione radice.</span><span class="sxs-lookup"><span data-stu-id="ae64f-129">This restriction is because the service does not trust your enterprise CA as a root certification authority.</span></span> 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a><span data-ttu-id="ae64f-130">Attività 1: Ottenere un certificato per l'accesso LDAP sicuro</span><span class="sxs-lookup"><span data-stu-id="ae64f-130">Task 1 - obtain a certificate for secure LDAP</span></span>
<span data-ttu-id="ae64f-131">La prima attività consiste nell'ottenere un certificato da usare per l'accesso LDAP sicuro al dominio gestito.</span><span class="sxs-lookup"><span data-stu-id="ae64f-131">The first task involves obtaining a certificate used for secure LDAP access to the managed domain.</span></span> <span data-ttu-id="ae64f-132">Sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="ae64f-132">You have two options:</span></span>

* <span data-ttu-id="ae64f-133">Ottenere un certificato da un'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="ae64f-133">Obtain a certificate from a certification authority.</span></span> <span data-ttu-id="ae64f-134">L'autorità può essere un'autorità di certificazione pubblica.</span><span class="sxs-lookup"><span data-stu-id="ae64f-134">The authority may be a public certification authority.</span></span>
* <span data-ttu-id="ae64f-135">Creare un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="ae64f-135">Create a self-signed certificate.</span></span>

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a><span data-ttu-id="ae64f-136">Opzione A (scelta consigliata): ottenere un certificato LDAP sicuro da un'autorità di certificazione</span><span class="sxs-lookup"><span data-stu-id="ae64f-136">Option A (Recommended) - Obtain a secure LDAP certificate from a certification authority</span></span>
<span data-ttu-id="ae64f-137">Se l'organizzazione ottiene i certificati da un'autorità di certificazione pubblica, è necessario ottenere il certificato LDAP sicuro dall'autorità di certificazione pubblica.</span><span class="sxs-lookup"><span data-stu-id="ae64f-137">If your organization obtains its certificates from a public certification authority, you need to obtain the secure LDAP certificate from that public certification authority.</span></span>

<span data-ttu-id="ae64f-138">Quando si richiede un certificato, assicurarsi di soddisfare tutti i requisiti descritti nella sezione [Requisiti per il certificato LDAP sicuro](#requirements-for-the-secure-ldap-certificate).</span><span class="sxs-lookup"><span data-stu-id="ae64f-138">When requesting a certificate, ensure that you satisfy all the requirements outlined in [Requirements for the secure LDAP certificate](#requirements-for-the-secure-ldap-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="ae64f-139">I computer client che devono connettersi al dominio gestito tramite l'accesso LDAP sicuro devono considerare attendibile l'autorità emittente del certificato LDAP sicuro.</span><span class="sxs-lookup"><span data-stu-id="ae64f-139">Client computers that need to connect to the managed domain using secure LDAP must trust the issuer of the secure LDAP certificate.</span></span>
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a><span data-ttu-id="ae64f-140">Opzione B: creare un certificato autofirmato per l'accesso LDAP sicuro</span><span class="sxs-lookup"><span data-stu-id="ae64f-140">Option B - Create a self-signed certificate for secure LDAP</span></span>
<span data-ttu-id="ae64f-141">Se non si prevede di usare un certificato di un'autorità di certificazione pubblica, è possibile scegliere di creare un certificato autofirmato per LDAP sicuro.</span><span class="sxs-lookup"><span data-stu-id="ae64f-141">If you do not expect to use a certificate from a public certification authority, you may choose to create a self-signed certificate for secure LDAP.</span></span>

<span data-ttu-id="ae64f-142">**Creare un certificato autofirmato con PowerShell**</span><span class="sxs-lookup"><span data-stu-id="ae64f-142">**Create a self-signed certificate using PowerShell**</span></span>

<span data-ttu-id="ae64f-143">Per creare un nuovo certificato autofirmato in un computer Windows, aprire una nuova finestra di PowerShell come **amministratore** e digitare i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="ae64f-143">On your Windows computer, open a new PowerShell window as **Administrator** and type the following commands, to create a new self-signed certificate.</span></span>

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

<span data-ttu-id="ae64f-144">Nell'esempio precedente sostituire "*.contoso100.com" con il nome di dominio DNS del dominio gestito. Ad esempio, se è stato creato un dominio gestito chiamato 'contoso100.onmicrosoft.com', sostituire '*. contoso100.com' nello script precedente con '*.contoso100.onmicrosoft.com').</span><span class="sxs-lookup"><span data-stu-id="ae64f-144">In the preceding sample, replace '*.contoso100.com' with the DNS domain name of your managed domain. For example, if you created a managed domain called 'contoso100.onmicrosoft.com', replace '*.contoso100.com' in the above script with '*.contoso100.onmicrosoft.com').</span></span>

![Selezionare una directory di Azure AD](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

<span data-ttu-id="ae64f-146">Il certificato autofirmato appena creato viene inserito nell'archivio certificati del computer locale.</span><span class="sxs-lookup"><span data-stu-id="ae64f-146">The newly created self-signed certificate is placed in the local machine's certificate store.</span></span>


## <a name="next-step"></a><span data-ttu-id="ae64f-147">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="ae64f-147">Next step</span></span>
[<span data-ttu-id="ae64f-148">Attività 2: Esportare il certificato LDAP sicuro in un file PFX</span><span class="sxs-lookup"><span data-stu-id="ae64f-148">Task 2 - export the secure LDAP certificate to a .PFX file</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
