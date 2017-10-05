---
title: Problema durante la creazione di un'applicazione Proxy di applicazione | Microsoft Docs
description: Come risolvere i problemi di creazione di applicazioni Proxy di applicazione nel portale di amministrazione di Azure AD
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
ms.openlocfilehash: fe56f56162ba7186f1b660a5b44fcef38f1dee9d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="problem-creating-an-application-proxy-application"></a><span data-ttu-id="b09ef-103">Problema durante la creazione di un'applicazione Proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="b09ef-103">Problem creating an Application Proxy application</span></span> 

<span data-ttu-id="b09ef-104">Di seguito vengono riportati alcuni dei problemi comuni relativi alla creazione di una nuova applicazione Proxy di applicazione.</span><span class="sxs-lookup"><span data-stu-id="b09ef-104">Below are some of the common issues people face when creating a new application proxy application.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="b09ef-105">Documenti consigliati</span><span class="sxs-lookup"><span data-stu-id="b09ef-105">Recommended documents</span></span> 

<span data-ttu-id="b09ef-106">Per altre informazioni sulla creazione di un'applicazione Proxy di applicazione tramite il portale di amministrazione, vedere [Pubblicare applicazioni mediante il proxy di applicazione AD Azure](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="b09ef-106">To learn more about creating an Application Proxy application through the Admin Portal, see [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="b09ef-107">Se si seguono i passaggi in tale documento e si riceve un errore durante la creazione dell'applicazione, vedere i dettagli dell'errore per informazioni e suggerimenti per la correzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b09ef-107">If you are following the steps in that document and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span></span> <span data-ttu-id="b09ef-108">La maggior parte dei messaggi di errore include una correzione suggerita.</span><span class="sxs-lookup"><span data-stu-id="b09ef-108">Most error messages include a suggested fix.</span></span> 

## <a name="specific-things-to-check"></a><span data-ttu-id="b09ef-109">Elementi specifici da controllare</span><span class="sxs-lookup"><span data-stu-id="b09ef-109">Specific things to check</span></span>

<span data-ttu-id="b09ef-110">Per evitare errori comuni, verificare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b09ef-110">To avoid common errors, verify:</span></span>

-   <span data-ttu-id="b09ef-111">Si dispone del ruolo di amministratore con l'autorizzazione a creare un'applicazione proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="b09ef-111">You are an administrator with permission to create an Application Proxy application</span></span>

-   <span data-ttu-id="b09ef-112">L'URL interno è univoco</span><span class="sxs-lookup"><span data-stu-id="b09ef-112">The internal URL is unique</span></span>

-   <span data-ttu-id="b09ef-113">L'URL esterno è univoco</span><span class="sxs-lookup"><span data-stu-id="b09ef-113">The external URL is unique</span></span>

-   <span data-ttu-id="b09ef-114">Gli URL iniziano con http o https e terminano con un carattere "/"</span><span class="sxs-lookup"><span data-stu-id="b09ef-114">The URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="b09ef-115">L'URL deve essere un nome di dominio e non un indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="b09ef-115">The URL should be a domain name and not an IP address</span></span>

<span data-ttu-id="b09ef-116">Quando si crea l'applicazione, il messaggio di errore dovrebbe essere visualizzato in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="b09ef-116">The error message should display in the top right corner when you create the application.</span></span> <span data-ttu-id="b09ef-117">È anche possibile selezionare l'icona di notifica per visualizzare i messaggi di errore.</span><span class="sxs-lookup"><span data-stu-id="b09ef-117">You can also select the notification icon to see the error messages.</span></span>

   ![Prompt di notifica](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a><span data-ttu-id="b09ef-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b09ef-119">Next steps</span></span>
[<span data-ttu-id="b09ef-120">Abilitare il proxy di applicazione nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b09ef-120">Enable Application Proxy in the Azure portal</span></span>](active-directory-application-proxy-enable.md)
