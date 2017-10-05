---
title: Come configurare un'applicazione proxy dell'applicazione | Microsoft Docs
description: Informazioni su come creare e configurare un'applicazione proxy dell'applicazione in pochi semplici passaggi
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
ms.openlocfilehash: c8f98536048a85ebb3f061d840457130579196d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-an-application-proxy-application"></a><span data-ttu-id="91cae-103">Come configurare un'applicazione proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="91cae-103">How to configure an Application Proxy application</span></span>

<span data-ttu-id="91cae-104">Questo articolo spiega come configurare un'applicazione proxy dell'applicazione in Azure AD per esporre le applicazioni locali nel cloud.</span><span class="sxs-lookup"><span data-stu-id="91cae-104">This article help you to understand how to configure an Application Proxy application within Azure AD to expose your on-premises applications to the cloud.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="91cae-105">Documenti consigliati</span><span class="sxs-lookup"><span data-stu-id="91cae-105">Recommended documents</span></span> 

<span data-ttu-id="91cae-106">Per altre informazioni sulle configurazioni iniziali e sulla creazione di un'applicazione proxy dell'applicazione tramite il portale di amministrazione, vedere [Pubblicare applicazioni mediante il proxy dell'applicazione Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="91cae-106">To learn about the initial configurations and creation of an Application Proxy application through the Admin Portal, follow the [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="91cae-107">Per i dettagli sulla configurazione dei connettori, vedere [Abilitare il proxy di applicazione nel portale di Azure](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="91cae-107">For details on configuring Connectors, see [Enable Application Proxy in the Azure portal](active-directory-application-proxy-enable.md).</span></span>

<span data-ttu-id="91cae-108">Per informazioni sul caricamento di certificati e sull'uso di domini personalizzati, vedere [Utilizzo di domini personalizzati nel proxy dell'applicazione di Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="91cae-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span>

## <a name="create-the-applicationsetting-the-urls"></a><span data-ttu-id="91cae-109">Creare l'applicazione/impostazione degli URL</span><span class="sxs-lookup"><span data-stu-id="91cae-109">Create the Application/Setting the URLs</span></span>

<span data-ttu-id="91cae-110">Se si seguono i passaggi nel documento [Pubblicare applicazioni mediante il proxy dell'applicazione di Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) e si riceve un errore durante la creazione dell'applicazione, vedere i dettagli dell'errore per informazioni e suggerimenti per la correzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="91cae-110">If you are following the steps in the [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span></span> <span data-ttu-id="91cae-111">La maggior parte dei messaggi di errore include una correzione suggerita.</span><span class="sxs-lookup"><span data-stu-id="91cae-111">Most error messages include a suggested fix.</span></span> <span data-ttu-id="91cae-112">Per evitare errori comuni, verificare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="91cae-112">To avoid common errors, verify:</span></span>

-   <span data-ttu-id="91cae-113">Si dispone del ruolo di amministratore con l'autorizzazione a creare un'applicazione proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="91cae-113">You are an administrator with permission to create an Application Proxy application</span></span>

-   <span data-ttu-id="91cae-114">L'URL interno è univoco</span><span class="sxs-lookup"><span data-stu-id="91cae-114">The internal URL is unique</span></span>

-   <span data-ttu-id="91cae-115">L'URL esterno è univoco</span><span class="sxs-lookup"><span data-stu-id="91cae-115">The external URL is unique</span></span>

-   <span data-ttu-id="91cae-116">Gli URL iniziano con http o https e terminano con un carattere "/"</span><span class="sxs-lookup"><span data-stu-id="91cae-116">The URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="91cae-117">L'URL deve essere un nome di dominio e non un indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="91cae-117">The URL should be a domain name, not an IP address</span></span>

<span data-ttu-id="91cae-118">Quando si crea l'applicazione, il messaggio di errore dovrebbe essere visualizzato in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="91cae-118">The error message should display in the top right corner when you create the application.</span></span> <span data-ttu-id="91cae-119">È anche possibile selezionare l'icona di notifica per visualizzare i messaggi di errore.</span><span class="sxs-lookup"><span data-stu-id="91cae-119">You can also select the notification icon to see the error messages.</span></span>

   ![Prompt di notifica](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a><span data-ttu-id="91cae-121">Configurare connettori/gruppi di connettori</span><span class="sxs-lookup"><span data-stu-id="91cae-121">Configure connectors/connector groups</span></span>

<span data-ttu-id="91cae-122">Se si riscontrano difficoltà nella configurazione dell'applicazione a causa di un'avvertenza sui connettori e sui gruppi di connettori, vedere le istruzioni per abilitare il proxy dell'applicazione per informazioni dettagliate su come scaricare i connettori.</span><span class="sxs-lookup"><span data-stu-id="91cae-122">If you are having difficulty configuring your application because of warning about the connectors and connector groups, see instructions on enabling Application Proxy for details on how to download connectors.</span></span> <span data-ttu-id="91cae-123">Per altre informazioni sui connettori, vedere la [documentazione relativa ai connettori](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span><span class="sxs-lookup"><span data-stu-id="91cae-123">If you want to learn more about connectors, see the [connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span></span>

<span data-ttu-id="91cae-124">Se i connettori sono inattivi, non sono in grado di raggiungere il servizio.</span><span class="sxs-lookup"><span data-stu-id="91cae-124">If your connectors are inactive, this means that they are unable to reach the service.</span></span> <span data-ttu-id="91cae-125">Spesso questa situazione si verifica poiché non sono aperte tutte le porte necessarie.</span><span class="sxs-lookup"><span data-stu-id="91cae-125">This is often because all the required ports are not open.</span></span> <span data-ttu-id="91cae-126">Per visualizzare un elenco delle porte necessarie, vedere la sezione dei prerequisiti della documentazione relativa all'abilitazione del proxy dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="91cae-126">To see a list of required ports, see the pre-requisites section of the enabling Application Proxy documentation.</span></span>

## <a name="upload-certificates-for-custom-domains"></a><span data-ttu-id="91cae-127">Caricare certificati per domini personalizzati</span><span class="sxs-lookup"><span data-stu-id="91cae-127">Upload certificates for custom domains</span></span>

<span data-ttu-id="91cae-128">I domini personalizzati consentono di specificare il dominio degli URL esterni.</span><span class="sxs-lookup"><span data-stu-id="91cae-128">Custom Domains allow you to specify the domain of your external URLs.</span></span> <span data-ttu-id="91cae-129">Per usare un dominio personalizzato, è necessario caricare il certificato per tale dominio.</span><span class="sxs-lookup"><span data-stu-id="91cae-129">To use custom domains, you need to upload the certificate for that domain.</span></span> <span data-ttu-id="91cae-130">Per informazioni sull'uso di certificati e domini personalizzati, vedere [Utilizzo di domini personalizzati nel proxy dell'applicazione di Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="91cae-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span> 

<span data-ttu-id="91cae-131">Se si verificano problemi durante il caricamento del certificato, cercare i messaggi di errore nel portale per altre informazioni sul problema con il certificato.</span><span class="sxs-lookup"><span data-stu-id="91cae-131">If you are encountering issues uploading your certificate, look for the error messages in the portal for additional information on the problem with the certificate.</span></span> <span data-ttu-id="91cae-132">Problemi comuni relativi ai certificati:</span><span class="sxs-lookup"><span data-stu-id="91cae-132">Common certificate problems include:</span></span>

-   <span data-ttu-id="91cae-133">Certificato scaduto</span><span class="sxs-lookup"><span data-stu-id="91cae-133">Expired certificate</span></span>

-   <span data-ttu-id="91cae-134">Certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="91cae-134">Certificate is self-signed</span></span>

-   <span data-ttu-id="91cae-135">Certificato privo di chiave privata</span><span class="sxs-lookup"><span data-stu-id="91cae-135">Certificate is missing the private key</span></span>

<span data-ttu-id="91cae-136">Quando si tenta di caricare il certificato, il messaggio di errore viene visualizzato nell'angolo superiore destro.</span><span class="sxs-lookup"><span data-stu-id="91cae-136">The error message display in the top right corner as you try to upload the certificate.</span></span> <span data-ttu-id="91cae-137">È anche possibile selezionare l'icona di notifica per visualizzare i messaggi di errore.</span><span class="sxs-lookup"><span data-stu-id="91cae-137">You can also select the notification icon to see the error messages.</span></span>

   ![Prompt di notifica](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a><span data-ttu-id="91cae-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="91cae-139">Next steps</span></span>
[<span data-ttu-id="91cae-140">Pubblicare applicazioni mediante il proxy di applicazione AD Azure</span><span class="sxs-lookup"><span data-stu-id="91cae-140">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
