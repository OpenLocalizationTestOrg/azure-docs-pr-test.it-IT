---
title: Ricerca di applicazioni cloud non gestite con Cloud App Discovery | Documentazione Microsoft
description: Fornisce informazioni sull'individuazione e la gestione delle applicazioni con Cloud App Discovery, quali sono i vantaggi e il relativo funzionamento.
services: active-directory
keywords: cloud app discovery, gestione delle applicazioni
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6284ff5bac8edbc19561d0916adef153526dfbe3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="99c64-104">Ricerca di applicazioni cloud non gestite con Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="99c64-104">Finding unmanaged cloud applications with Cloud App Discovery</span></span>
## <a name="overview"></a><span data-ttu-id="99c64-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="99c64-105">Overview</span></span>
<span data-ttu-id="99c64-106">Nelle aziende moderne spesso i reparti IT non sono a conoscenza di tutte le applicazioni cloud usate dai membri dell'organizzazione per svolgere il proprio lavoro.</span><span class="sxs-lookup"><span data-stu-id="99c64-106">In modern enterprises, IT departments are often not aware of all the cloud applications that members of their organization use to do their work.</span></span> <span data-ttu-id="99c64-107">L'accesso non autorizzato ai dati aziendali, le possibili perdite di dati e altri rischi di sicurezza rappresentano una preoccupazione per gli amministratori.</span><span class="sxs-lookup"><span data-stu-id="99c64-107">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span></span> <span data-ttu-id="99c64-108">A causa di questa mancanza di consapevolezza, la creazione di un piano per la gestione dei rischi per la sicurezza potrebbe sembrare complicata.</span><span class="sxs-lookup"><span data-stu-id="99c64-108">This lack of awareness can make creating a plan for dealing with these security risks seem daunting.</span></span>

<span data-ttu-id="99c64-109">Cloud App Discovery è una funzionalità dell'edizione Premium di Azure Active Directory (AD) che consente di individuare le applicazioni cloud usate dai dipendenti dell'azienda.</span><span class="sxs-lookup"><span data-stu-id="99c64-109">Cloud App Discovery is a feature of Azure Active Directory (AD) Premium that enables you to discover cloud applications being used by the people in your organization.</span></span>

<span data-ttu-id="99c64-110">**Cloud App Discovery consente di:**</span><span class="sxs-lookup"><span data-stu-id="99c64-110">**With Cloud App Discovery, you can:**</span></span>

* <span data-ttu-id="99c64-111">Individuare le applicazioni cloud in uso e misurarne l'utilizzo in base al numero di utenti, al volume di traffico o al numero di richieste Web all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="99c64-111">Find the cloud applications being used and measure that usage by number of users, volume of traffic or number of web requests to the application.</span></span>
* <span data-ttu-id="99c64-112">Identificare gli utenti che usano un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="99c64-112">Identify the users that are using an application.</span></span>
* <span data-ttu-id="99c64-113">Esportare i dati per analisi offline.</span><span class="sxs-lookup"><span data-stu-id="99c64-113">Export data for offline analysis.</span></span>
* <span data-ttu-id="99c64-114">Portare le applicazioni sotto il controllo IT e abilitare la funzionalità Single Sign-On per la gestione degli utenti.</span><span class="sxs-lookup"><span data-stu-id="99c64-114">Bring these applications under IT control and enable single sign on for user management.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="99c64-115">Funzionamento</span><span class="sxs-lookup"><span data-stu-id="99c64-115">How it works</span></span>
1. <span data-ttu-id="99c64-116">Gli agenti di utilizzo dell'applicazione vengono installati nei computer dell'utente.</span><span class="sxs-lookup"><span data-stu-id="99c64-116">Application usage agents are installed on user's computers.</span></span>
2. <span data-ttu-id="99c64-117">Le informazioni sull'utilizzo delle applicazioni acquisite dagli agenti vengono inviate tramite un canale crittografato sicuro al servizio Cloud App Discovery.</span><span class="sxs-lookup"><span data-stu-id="99c64-117">The application usage information captured by the agents is sent over a secure, encrypted channel to the cloud app discovery service.</span></span>
3. <span data-ttu-id="99c64-118">Il servizio Cloud App Discovery valuta i dati e genera report.</span><span class="sxs-lookup"><span data-stu-id="99c64-118">The Cloud App Discovery service evaluates the data and generates reports.</span></span>

![Diagramma di Cloud App Discovery](./media/active-directory-cloudappdiscovery/cad01.png)

<span data-ttu-id="99c64-120">Per iniziare a usare Cloud App Discovery, vedere l' [introduzione a Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span><span class="sxs-lookup"><span data-stu-id="99c64-120">To get started with Cloud App Discovery, see [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span></span>

## <a name="related-articles"></a><span data-ttu-id="99c64-121">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="99c64-121">Related articles</span></span>
* [<span data-ttu-id="99c64-122">Considerazioni sulla sicurezza e sulla privacy in Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="99c64-122">Cloud App Discovery Security and Privacy Considerations</span></span>](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [<span data-ttu-id="99c64-123">Guida alla distribuzione di criteri di gruppo di Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="99c64-123">Cloud App Discovery Group Policy Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [<span data-ttu-id="99c64-124">Guida alla distribuzione di Cloud App Discovery System Center</span><span class="sxs-lookup"><span data-stu-id="99c64-124">Cloud App Discovery System Center Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [<span data-ttu-id="99c64-125">Impostazioni del Registro di sistema di Cloud App Discovery per servizi proxy con porte personalizzate</span><span class="sxs-lookup"><span data-stu-id="99c64-125">Cloud App Discovery Registry Settings for Proxy Servers with Custom Ports</span></span>](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [<span data-ttu-id="99c64-126">Log modifiche dell'agente di Cloud App Discovery </span><span class="sxs-lookup"><span data-stu-id="99c64-126">Cloud App Discovery Agent Changelog </span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [<span data-ttu-id="99c64-127">Domande frequenti di Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="99c64-127">Cloud App Discovery Frequently Asked Questions</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [<span data-ttu-id="99c64-128">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99c64-128">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

