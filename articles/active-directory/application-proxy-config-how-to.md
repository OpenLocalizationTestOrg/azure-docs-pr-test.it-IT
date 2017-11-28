---
title: aaaHow tooconfigure un'applicazione Proxy dell'applicazione | Documenti Microsoft
description: Informazioni su come toocreate un Configura applicazione Proxy dell'applicazione in pochi semplici passaggi
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a><span data-ttu-id="b42e5-103">Come tooconfigure un'applicazione Proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="b42e5-103">How tooconfigure an Application Proxy application</span></span>

<span data-ttu-id="b42e5-104">Questo articolo è utile toounderstand tooconfigure un'applicazione Proxy dell'applicazione all'interno di Azure AD tooexpose il toohello applicazioni on-premise di cloud.</span><span class="sxs-lookup"><span data-stu-id="b42e5-104">This article help you toounderstand how tooconfigure an Application Proxy application within Azure AD tooexpose your on-premises applications toohello cloud.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="b42e5-105">Documenti consigliati</span><span class="sxs-lookup"><span data-stu-id="b42e5-105">Recommended documents</span></span> 

<span data-ttu-id="b42e5-106">toolearn sulla creazione di un'applicazione Proxy dell'applicazione tramite il portale di amministrazione, hello e le configurazioni iniziali hello seguire hello [pubblicare applicazioni mediante il Proxy di applicazione AD Azure](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="b42e5-106">toolearn about hello initial configurations and creation of an Application Proxy application through hello Admin Portal, follow hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="b42e5-107">Per informazioni dettagliate sulla configurazione dei connettori, vedere [abilitare i Proxy di applicazione nel portale di Azure hello](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="b42e5-107">For details on configuring Connectors, see [Enable Application Proxy in hello Azure portal](active-directory-application-proxy-enable.md).</span></span>

<span data-ttu-id="b42e5-108">Per informazioni sul caricamento di certificati e sull'uso di domini personalizzati, vedere [Utilizzo di domini personalizzati nel proxy dell'applicazione di Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="b42e5-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span>

## <a name="create-hello-applicationsetting-hello-urls"></a><span data-ttu-id="b42e5-109">Creare hello/impostazione dell'applicazione hello URL</span><span class="sxs-lookup"><span data-stu-id="b42e5-109">Create hello Application/Setting hello URLs</span></span>

<span data-ttu-id="b42e5-110">Se si segue hello passaggi hello [pubblicare applicazioni mediante il Proxy di applicazione AD Azure](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentazione e sono il recupero di un errore durante la creazione di un'applicazione hello, vedere i dettagli dell'errore hello per le informazioni e i suggerimenti su come applicazione hello toofix.</span><span class="sxs-lookup"><span data-stu-id="b42e5-110">If you are following hello steps in hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation and are getting an error creating hello application, see hello error details for information and suggestions for how toofix hello application.</span></span> <span data-ttu-id="b42e5-111">La maggior parte dei messaggi di errore include una correzione suggerita.</span><span class="sxs-lookup"><span data-stu-id="b42e5-111">Most error messages include a suggested fix.</span></span> <span data-ttu-id="b42e5-112">gli errori comuni tooavoid, verificare che:</span><span class="sxs-lookup"><span data-stu-id="b42e5-112">tooavoid common errors, verify:</span></span>

-   <span data-ttu-id="b42e5-113">Si è un amministratore con autorizzazioni toocreate un'applicazione Proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="b42e5-113">You are an administrator with permission toocreate an Application Proxy application</span></span>

-   <span data-ttu-id="b42e5-114">URL interno Hello è univoco</span><span class="sxs-lookup"><span data-stu-id="b42e5-114">hello internal URL is unique</span></span>

-   <span data-ttu-id="b42e5-115">URL esterno Hello è univoco</span><span class="sxs-lookup"><span data-stu-id="b42e5-115">hello external URL is unique</span></span>

-   <span data-ttu-id="b42e5-116">Hello gli URL avvio con http o https e terminare con una "/"</span><span class="sxs-lookup"><span data-stu-id="b42e5-116">hello URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="b42e5-117">Hello URL deve essere un nome di dominio, non un indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="b42e5-117">hello URL should be a domain name, not an IP address</span></span>

<span data-ttu-id="b42e5-118">messaggio di errore Hello riporterà nell'angolo superiore destro di hello quando si crea un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b42e5-118">hello error message should display in hello top right corner when you create hello application.</span></span> <span data-ttu-id="b42e5-119">È anche possibile selezionare i messaggi di errore di hello notifica icona toosee hello.</span><span class="sxs-lookup"><span data-stu-id="b42e5-119">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Prompt di notifica](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a><span data-ttu-id="b42e5-121">Configurare connettori/gruppi di connettori</span><span class="sxs-lookup"><span data-stu-id="b42e5-121">Configure connectors/connector groups</span></span>

<span data-ttu-id="b42e5-122">Se si riscontrano difficoltà di configurazione dell'applicazione a causa di avviso sui connettori di hello e gruppi di connettori, vedere le istruzioni sull'abilitazione di Proxy dell'applicazione per informazioni dettagliate su come i connettori toodownload.</span><span class="sxs-lookup"><span data-stu-id="b42e5-122">If you are having difficulty configuring your application because of warning about hello connectors and connector groups, see instructions on enabling Application Proxy for details on how toodownload connectors.</span></span> <span data-ttu-id="b42e5-123">Se si desidera toolearn informazioni sui connettori, vedere hello [documentazione connettori](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span><span class="sxs-lookup"><span data-stu-id="b42e5-123">If you want toolearn more about connectors, see hello [connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span></span>

<span data-ttu-id="b42e5-124">Se i connettori sono inattivi, ciò significa che sono servizio hello tooreach non è possibile.</span><span class="sxs-lookup"><span data-stu-id="b42e5-124">If your connectors are inactive, this means that they are unable tooreach hello service.</span></span> <span data-ttu-id="b42e5-125">Si tratta spesso perché tutte le porte hello necessario non sono aperte.</span><span class="sxs-lookup"><span data-stu-id="b42e5-125">This is often because all hello required ports are not open.</span></span> <span data-ttu-id="b42e5-126">toosee un elenco delle porte necessarie, vedere sezione Prerequisiti hello hello attivare la documentazione di Proxy dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b42e5-126">toosee a list of required ports, see hello pre-requisites section of hello enabling Application Proxy documentation.</span></span>

## <a name="upload-certificates-for-custom-domains"></a><span data-ttu-id="b42e5-127">Caricare certificati per domini personalizzati</span><span class="sxs-lookup"><span data-stu-id="b42e5-127">Upload certificates for custom domains</span></span>

<span data-ttu-id="b42e5-128">Domini personalizzati consentono di dominio di hello toospecify dell'URL esterno.</span><span class="sxs-lookup"><span data-stu-id="b42e5-128">Custom Domains allow you toospecify hello domain of your external URLs.</span></span> <span data-ttu-id="b42e5-129">toouse domini personalizzati, è necessario il certificato di hello tooupload per quel dominio.</span><span class="sxs-lookup"><span data-stu-id="b42e5-129">toouse custom domains, you need tooupload hello certificate for that domain.</span></span> <span data-ttu-id="b42e5-130">Per informazioni sull'uso di certificati e domini personalizzati, vedere [Utilizzo di domini personalizzati nel proxy dell'applicazione di Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="b42e5-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span> 

<span data-ttu-id="b42e5-131">Se si rilevano problemi di caricamento del certificato, cercare i messaggi di errore hello nel portale di hello per le informazioni aggiuntive sul problema hello con certificato hello.</span><span class="sxs-lookup"><span data-stu-id="b42e5-131">If you are encountering issues uploading your certificate, look for hello error messages in hello portal for additional information on hello problem with hello certificate.</span></span> <span data-ttu-id="b42e5-132">Problemi comuni relativi ai certificati:</span><span class="sxs-lookup"><span data-stu-id="b42e5-132">Common certificate problems include:</span></span>

-   <span data-ttu-id="b42e5-133">Certificato scaduto</span><span class="sxs-lookup"><span data-stu-id="b42e5-133">Expired certificate</span></span>

-   <span data-ttu-id="b42e5-134">Certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="b42e5-134">Certificate is self-signed</span></span>

-   <span data-ttu-id="b42e5-135">La chiave privata di hello mancante nel certificato</span><span class="sxs-lookup"><span data-stu-id="b42e5-135">Certificate is missing hello private key</span></span>

<span data-ttu-id="b42e5-136">visualizzazione messaggi di errore Hello in hello angolo superiore destro quando si tenta di certificato hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="b42e5-136">hello error message display in hello top right corner as you try tooupload hello certificate.</span></span> <span data-ttu-id="b42e5-137">È anche possibile selezionare i messaggi di errore di hello notifica icona toosee hello.</span><span class="sxs-lookup"><span data-stu-id="b42e5-137">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Prompt di notifica](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a><span data-ttu-id="b42e5-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b42e5-139">Next steps</span></span>
[<span data-ttu-id="b42e5-140">Pubblicare applicazioni mediante il proxy di applicazione AD Azure</span><span class="sxs-lookup"><span data-stu-id="b42e5-140">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
