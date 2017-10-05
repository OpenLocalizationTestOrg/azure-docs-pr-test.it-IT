---
title: Come selezionare le autorizzazioni per un'API specifica | Microsoft Docs
description: Come trovare gli endpoint di autenticazione per un'applicazione personalizzata che si sta sviluppando o registrando con Azure AD.
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
ms.openlocfilehash: 6966cf145375bf3d830d476564c428502ae40fd4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-select-permissions-for-a-given-api"></a><span data-ttu-id="ea7d5-103">Come selezionare le autorizzazioni per un'API specifica</span><span class="sxs-lookup"><span data-stu-id="ea7d5-103">How to select permissions for a given API</span></span>

<span data-ttu-id="ea7d5-104">È possibile trovare gli endpoint di autenticazione per l'applicazione nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ea7d5-104">You can find the authentication endpoints for your application in the [Azure portal](https://portal.azure.com).</span></span>

-   <span data-ttu-id="ea7d5-105">Passare al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ea7d5-105">Navigate to the [Azure portal](https://portal.azure.com).</span></span>

-   <span data-ttu-id="ea7d5-106">Nel riquadro di spostamento sinistro fare clic su **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea7d5-106">From the left navigation pane, click **Azure Active Directory**.</span></span>

-   <span data-ttu-id="ea7d5-107">Fare clic su **Registrazioni per l'app** e scegliere **Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="ea7d5-107">Click **App Registrations** and choose **Endpoints**.</span></span>

-   <span data-ttu-id="ea7d5-108">Verrà visualizzata la pagina **Endpoint** in cui sono elencati tutti gli endpoint di autenticazione per il tenant.</span><span class="sxs-lookup"><span data-stu-id="ea7d5-108">This open up the **Endpoints** page, which list all the authentication endpoints for your tenant.</span></span>

-   <span data-ttu-id="ea7d5-109">Per creare la richiesta di autenticazione specifica per l'applicazione, usare l'endpoint specifico del protocollo di autenticazione in uso, in combinazione con l'ID applicazione.</span><span class="sxs-lookup"><span data-stu-id="ea7d5-109">Use the endpoint specific to the authentication protocol you are using, in conjunction with the application ID to craft the authentication request specific to your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea7d5-110">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ea7d5-110">Next steps</span></span>
[<span data-ttu-id="ea7d5-111">Guida per gli sviluppatori di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea7d5-111">Azure Active Directory developer's guide</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-developers-guide#authentication-and-authorization-protocols)
