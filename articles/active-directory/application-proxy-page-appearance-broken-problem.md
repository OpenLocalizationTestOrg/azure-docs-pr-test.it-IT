---
title: La pagina dell'applicazione non viene visualizzata correttamente per un'applicazione proxy di applicazione | Microsoft Docs
description: Linee guida per i casi in cui la pagina non viene visualizzata correttamente in un'applicazione proxy di applicazione integrata con Azure AD
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
ms.openlocfilehash: cac4c333e59ef9a0f28a2f93a7afee22eeafd54e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="db86a-103">La pagina dell'applicazione non viene visualizzata correttamente per un'applicazione proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="db86a-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="db86a-104">Questo articolo semplifica la risoluzione dei problemi relativi ad applicazioni proxy di applicazione di Azure Active Directory quando è possibile passare alla pagina, ma questa non viene visualizzata correttamente.</span><span class="sxs-lookup"><span data-stu-id="db86a-104">This article help you to troubleshoot issues with Azure Active Directory Application Proxy applications when you navigate to the page, but something on the page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="db86a-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="db86a-105">Overview</span></span>
<span data-ttu-id="db86a-106">Quando si pubblica un'app proxy di applicazione, solo le pagine all'interno della radice sono accessibili quando si accede all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="db86a-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing the application.</span></span> <span data-ttu-id="db86a-107">Se la pagina non viene visualizzata correttamente, l'URL interno radice usato per l'applicazione potrebbe non includere alcune risorse della pagina.</span><span class="sxs-lookup"><span data-stu-id="db86a-107">If the page isn’t displaying correctly, the root internal URL used for the application may be missing some page resources.</span></span> <span data-ttu-id="db86a-108">Per risolvere questo problema, assicurarsi di aver pubblicato *tutte* le risorse per la pagina come parte dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="db86a-108">To resolve, make sure you have published *all* the resources for the page as part of your application.</span></span>

<span data-ttu-id="db86a-109">Per verificare che il problema sia questo, aprire lo strumento di individuazione di rete, ad esempio Fiddler o altri strumenti F12 in Internet Explorer/Edge, caricare la pagina e cercare eventuali errori 404.</span><span class="sxs-lookup"><span data-stu-id="db86a-109">You can verify this is the issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading the page, and looking for 404 errors.</span></span> <span data-ttu-id="db86a-110">Questi errori indicano che le pagine non possono essere trovate e potrebbero dover essere pubblicate.</span><span class="sxs-lookup"><span data-stu-id="db86a-110">That indicates the pages that currently cannot be found and may still need to be published.</span></span>

<span data-ttu-id="db86a-111">Come esempio di questo caso, si supponga di aver pubblicato un'applicazione per il calcolo delle spese usando l'URL interno <http://myapps/expenses>, mentre l'app usa il foglio di stile <http://myapps/style.css>.</span><span class="sxs-lookup"><span data-stu-id="db86a-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but the app uses the stylesheet <http://myapps/style.css>.</span></span> <span data-ttu-id="db86a-112">In questo caso, il foglio di stile non viene pubblicato nell'applicazione e di conseguenza il caricamento dell'app genera un errore 404 mentre tenta di caricare style.css.</span><span class="sxs-lookup"><span data-stu-id="db86a-112">In this case, the stylesheet is not published in your application, so loading the expenses app throw a 404 error while trying to load style.css.</span></span> <span data-ttu-id="db86a-113">In questo esempio il problema può essere risolto pubblicando l'applicazione con l'URL interno <http://myapp/>.</span><span class="sxs-lookup"><span data-stu-id="db86a-113">In this example, the problem would be resolved by publishing the application with an internal URL of <http://myapp/> instead.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="db86a-114">Problemi relativi alla pubblicazione come singola applicazione</span><span class="sxs-lookup"><span data-stu-id="db86a-114">Problems with publishing as one application</span></span>

<span data-ttu-id="db86a-115">Se non è possibile pubblicare tutte le risorse all'interno della stessa applicazione, è necessario pubblicare più applicazioni e abilitare i collegamenti tra loro.</span><span class="sxs-lookup"><span data-stu-id="db86a-115">If it is not possible to publish all resources within the same application, you need to publish multiple applications and enable links between them.</span></span>

<span data-ttu-id="db86a-116">A questo scopo, è consigliabile usare la soluzione con [domini personalizzati](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="db86a-116">To do so, we recommend using the [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span></span> <span data-ttu-id="db86a-117">Con questa soluzione, tuttavia, è necessario essere il proprietario del certificato per il dominio e che le applicazioni usino nomi di domino completi (FQDN).</span><span class="sxs-lookup"><span data-stu-id="db86a-117">However, this solution requires that you own the certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="db86a-118">Per altre opzioni, vedere la [documentazione per la risoluzione dei problemi relativi a collegamenti interrotti](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span><span class="sxs-lookup"><span data-stu-id="db86a-118">For other options, see the [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="db86a-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="db86a-119">Next steps</span></span>
[<span data-ttu-id="db86a-120">Pubblicare applicazioni mediante il proxy di applicazione AD Azure</span><span class="sxs-lookup"><span data-stu-id="db86a-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
