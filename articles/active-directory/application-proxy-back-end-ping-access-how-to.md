---
title: Come configurare un'applicazione proxy dell'applicazione per l'uso di PingAccess | Microsoft Docs
description: Informazioni su come usare PingAccess per estendere i vantaggi del proxy dell'applicazione alle applicazioni che usano l'autenticazione basata su intestazione
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
ms.openlocfilehash: a9da67373465cebbdbecae5c8fb8bd0a0ee3c171
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-an-application-proxy-application-to-use-pingaccess"></a><span data-ttu-id="17787-103">Come configurare un'applicazione proxy dell'applicazione per l'uso di PingAccess</span><span class="sxs-lookup"><span data-stu-id="17787-103">How to configure an Application Proxy application to use PingAccess</span></span>

<span data-ttu-id="17787-104">La nostra collaborazione con PingAccess ci permette ora di estendere i vantaggi del proxy dell'applicazione alle applicazioni che usano l'autenticazione basata su intestazione.</span><span class="sxs-lookup"><span data-stu-id="17787-104">Our collaboration with PingAccess now allows you to extend the benefits of Application Proxy to applications using header-based authentication.</span></span> <span data-ttu-id="17787-105">Se le applicazioni non usano intestazioni, vedere la nostra [documentazione relativa a Single Sign-On](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) per ottenere dettagli su altre opzioni.</span><span class="sxs-lookup"><span data-stu-id="17787-105">If your applications do not use headers, see our [Single Sign-On documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) for details on other options.</span></span>

## <a name="overview-of-steps-and-recommended-documents"></a><span data-ttu-id="17787-106">Panoramica dei passaggi e documenti consigliati</span><span class="sxs-lookup"><span data-stu-id="17787-106">Overview of steps and recommended documents</span></span>

<span data-ttu-id="17787-107">Per configurare un'applicazione con PingAccess, sono disponibili quattro passaggi:</span><span class="sxs-lookup"><span data-stu-id="17787-107">To configure an application with PingAccess, there are four steps:</span></span>

1.  <span data-ttu-id="17787-108">Configurare i connettori del proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="17787-108">Configure Application Proxy Connectors</span></span>

2.  <span data-ttu-id="17787-109">Creare un'applicazione del proxy dell'applicazione Azure AD</span><span class="sxs-lookup"><span data-stu-id="17787-109">Create an Azure AD Application Proxy Application</span></span>

3.  <span data-ttu-id="17787-110">Scaricare e configurare PingAccess</span><span class="sxs-lookup"><span data-stu-id="17787-110">Download & Configure PingAccess</span></span>

4.  <span data-ttu-id="17787-111">Configurare le applicazioni in PingAccess</span><span class="sxs-lookup"><span data-stu-id="17787-111">Configure Applications in PingAccess</span></span>

<span data-ttu-id="17787-112">Per i dettagli su ogni passaggio, vedere la nostra [documentazione relativa a Single Sign-On con intestazioni](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span><span class="sxs-lookup"><span data-stu-id="17787-112">For details on each of these steps, see our [Single Sign-On with Headers documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span></span>
