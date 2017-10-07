---
title: creazione di un'applicazione di Proxy applicazione aaaProblem | Documenti Microsoft
description: Come tootroubleshoot genera la creazione di applicazioni Proxy dell'applicazione nel portale di amministrazione di Active Directory di Azure hello
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
ms.openlocfilehash: 24fab83c38a49a9e5754854acf2f9711e374e559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-creating-an-application-proxy-application"></a><span data-ttu-id="49e32-103">Problema durante la creazione di un'applicazione Proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="49e32-103">Problem creating an Application Proxy application</span></span> 

<span data-ttu-id="49e32-104">Di seguito sono alcuni dei problemi comuni di hello faccia persone quando si crea una nuova applicazione proxy di applicazione.</span><span class="sxs-lookup"><span data-stu-id="49e32-104">Below are some of hello common issues people face when creating a new application proxy application.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="49e32-105">Documenti consigliati</span><span class="sxs-lookup"><span data-stu-id="49e32-105">Recommended documents</span></span> 

<span data-ttu-id="49e32-106">vedere toolearn informazioni sulla creazione di un'applicazione Proxy dell'applicazione tramite il portale di amministrazione, hello [pubblicare applicazioni mediante il Proxy di applicazione AD Azure](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="49e32-106">toolearn more about creating an Application Proxy application through hello Admin Portal, see [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="49e32-107">Se si riceve un errore durante la creazione di un'applicazione hello sono operazioni hello in tale documento, vedere i dettagli dell'errore hello per le informazioni e suggerimenti per la modalità toofix hello applicazione.</span><span class="sxs-lookup"><span data-stu-id="49e32-107">If you are following hello steps in that document and are getting an error creating hello application, see hello error details for information and suggestions for how toofix hello application.</span></span> <span data-ttu-id="49e32-108">La maggior parte dei messaggi di errore include una correzione suggerita.</span><span class="sxs-lookup"><span data-stu-id="49e32-108">Most error messages include a suggested fix.</span></span> 

## <a name="specific-things-toocheck"></a><span data-ttu-id="49e32-109">Operazioni specifiche toocheck</span><span class="sxs-lookup"><span data-stu-id="49e32-109">Specific things toocheck</span></span>

<span data-ttu-id="49e32-110">gli errori comuni tooavoid, verificare che:</span><span class="sxs-lookup"><span data-stu-id="49e32-110">tooavoid common errors, verify:</span></span>

-   <span data-ttu-id="49e32-111">Si è un amministratore con autorizzazioni toocreate un'applicazione Proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="49e32-111">You are an administrator with permission toocreate an Application Proxy application</span></span>

-   <span data-ttu-id="49e32-112">URL interno Hello è univoco</span><span class="sxs-lookup"><span data-stu-id="49e32-112">hello internal URL is unique</span></span>

-   <span data-ttu-id="49e32-113">URL esterno Hello è univoco</span><span class="sxs-lookup"><span data-stu-id="49e32-113">hello external URL is unique</span></span>

-   <span data-ttu-id="49e32-114">Hello gli URL avvio con http o https e terminare con una "/"</span><span class="sxs-lookup"><span data-stu-id="49e32-114">hello URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="49e32-115">Hello URL deve essere un nome di dominio e non un indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="49e32-115">hello URL should be a domain name and not an IP address</span></span>

<span data-ttu-id="49e32-116">messaggio di errore Hello riporterà nell'angolo superiore destro di hello quando si crea un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="49e32-116">hello error message should display in hello top right corner when you create hello application.</span></span> <span data-ttu-id="49e32-117">È anche possibile selezionare i messaggi di errore di hello notifica icona toosee hello.</span><span class="sxs-lookup"><span data-stu-id="49e32-117">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Prompt di notifica](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a><span data-ttu-id="49e32-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="49e32-119">Next steps</span></span>
[<span data-ttu-id="49e32-120">Abilitare il Proxy di applicazione nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="49e32-120">Enable Application Proxy in hello Azure portal</span></span>](active-directory-application-proxy-enable.md)
