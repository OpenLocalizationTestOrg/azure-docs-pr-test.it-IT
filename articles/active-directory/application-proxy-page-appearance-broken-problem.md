---
title: pagina aaaApplication non viene visualizzato correttamente per un'applicazione Proxy dell'applicazione | Documenti Microsoft
description: "Quando la pagina hello non vengono visualizzati correttamente in un'applicazione di Proxy di applicazione è stata integrata con Azure AD"
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
ms.openlocfilehash: f4abaa4e94c512868f2085affe59cac443784a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="2f729-103">La pagina dell'applicazione non viene visualizzata correttamente per un'applicazione proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="2f729-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="2f729-104">Questo articolo è utile tootroubleshoot problemi con applicazioni di Proxy dell'applicazione Azure Active Directory quando si passa toohello pagina, ma un elemento nella pagina di hello non sembra corretto.</span><span class="sxs-lookup"><span data-stu-id="2f729-104">This article help you tootroubleshoot issues with Azure Active Directory Application Proxy applications when you navigate toohello page, but something on hello page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="2f729-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2f729-105">Overview</span></span>
<span data-ttu-id="2f729-106">Quando si pubblica un'app di Proxy dell'applicazione, solo le pagine nella cartella principale sono accessibili quando si accede a un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2f729-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing hello application.</span></span> <span data-ttu-id="2f729-107">Se non è la corretta visualizzazione pagina hello, hello radice URL interno utilizzato per un'applicazione hello potrebbero mancare alcune risorse di pagina.</span><span class="sxs-lookup"><span data-stu-id="2f729-107">If hello page isn’t displaying correctly, hello root internal URL used for hello application may be missing some page resources.</span></span> <span data-ttu-id="2f729-108">tooresolve, assicurarsi di aver pubblicato *tutti* hello risorse per la pagina hello come parte dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f729-108">tooresolve, make sure you have published *all* hello resources for hello page as part of your application.</span></span>

<span data-ttu-id="2f729-109">È possibile verificare questo problema hello aprendo l'individuazione di rete (ad esempio Fiddler o F12 strumenti in Internet Explorer o Edge), il caricamento della pagina hello e cercare 404 errori.</span><span class="sxs-lookup"><span data-stu-id="2f729-109">You can verify this is hello issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading hello page, and looking for 404 errors.</span></span> <span data-ttu-id="2f729-110">Che indica le pagine di hello che attualmente non è state trovate e potrebbe essere ancora necessario toobe pubblicato.</span><span class="sxs-lookup"><span data-stu-id="2f729-110">That indicates hello pages that currently cannot be found and may still need toobe published.</span></span>

<span data-ttu-id="2f729-111">Si supponga ad esempio di questo caso, è stata pubblicata un'applicazione di spese utilizzando un URL interno di <http://myapps/expenses>, ma hello app utilizza hello stylesheet <http://myapps/style.css>.</span><span class="sxs-lookup"><span data-stu-id="2f729-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but hello app uses hello stylesheet <http://myapps/style.css>.</span></span> <span data-ttu-id="2f729-112">In questo caso, hello foglio di stile non è pubblicato nell'applicazione, pertanto il caricamento delle app spese hello generano un errore durante il tentativo tooload style.css 404.</span><span class="sxs-lookup"><span data-stu-id="2f729-112">In this case, hello stylesheet is not published in your application, so loading hello expenses app throw a 404 error while trying tooload style.css.</span></span> <span data-ttu-id="2f729-113">In questo esempio, hello problema potrebbe essere risolto tramite la pubblicazione di un URL interno di un'applicazione hello <http://myapp/> invece.</span><span class="sxs-lookup"><span data-stu-id="2f729-113">In this example, hello problem would be resolved by publishing hello application with an internal URL of <http://myapp/> instead.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="2f729-114">Problemi relativi alla pubblicazione come singola applicazione</span><span class="sxs-lookup"><span data-stu-id="2f729-114">Problems with publishing as one application</span></span>

<span data-ttu-id="2f729-115">Se non è possibile toopublish tutte le risorse all'interno di hello stessa applicazione, è necessario toopublish più applicazioni e abilitare i collegamenti tra di essi.</span><span class="sxs-lookup"><span data-stu-id="2f729-115">If it is not possible toopublish all resources within hello same application, you need toopublish multiple applications and enable links between them.</span></span>

<span data-ttu-id="2f729-116">toodo in tal caso, si consiglia di utilizzare hello [domini personalizzati](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) soluzione.</span><span class="sxs-lookup"><span data-stu-id="2f729-116">toodo so, we recommend using hello [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span></span> <span data-ttu-id="2f729-117">Tuttavia, questa soluzione richiede che il certificato di hello si è proprietari del dominio e le applicazioni utilizzano nomi di dominio completo (FQDN).</span><span class="sxs-lookup"><span data-stu-id="2f729-117">However, this solution requires that you own hello certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="2f729-118">Per altre opzioni, vedere hello [risolvere collegamenti non funzionanti documentazione](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span><span class="sxs-lookup"><span data-stu-id="2f729-118">For other options, see hello [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f729-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2f729-119">Next steps</span></span>
[<span data-ttu-id="2f729-120">Pubblicare applicazioni mediante il proxy di applicazione AD Azure</span><span class="sxs-lookup"><span data-stu-id="2f729-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
