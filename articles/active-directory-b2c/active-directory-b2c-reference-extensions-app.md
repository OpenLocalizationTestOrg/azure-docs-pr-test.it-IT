---
title: App Estensioni - Azure AD B2C | Microsoft Docs
description: Ripristino hello b2c-estensioni-app
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f0392e32-0771-473c-a799-81438ca2bcff
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/17/2017
ms.author: parja
ms.openlocfilehash: b36410c18314bd893dc669b49814fdcd77fae054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-extensions-app"></a><span data-ttu-id="0b847-103">Azure AD B2C: app Estensioni</span><span class="sxs-lookup"><span data-stu-id="0b847-103">Azure AD B2C: Extensions app</span></span>

<span data-ttu-id="0b847-104">Quando viene creata una directory di Azure Active Directory B2C, un'app denominata `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` viene automaticamente creato all'interno di hello nuova directory.</span><span class="sxs-lookup"><span data-stu-id="0b847-104">When an Azure AD B2C directory is created, an app called `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` is automatically created inside hello new directory.</span></span> <span data-ttu-id="0b847-105">Questa app, cui viene fatto riferimento tooas hello **b2c-estensioni-app**, è visibile in *registrazioni di App*.</span><span class="sxs-lookup"><span data-stu-id="0b847-105">This app, referred tooas hello **b2c-extensions-app**, is visible in *App registrations*.</span></span> <span data-ttu-id="0b847-106">Viene utilizzato da hello Azure Active Directory B2C servizio toostore informazioni gli utenti e gli attributi personalizzati.</span><span class="sxs-lookup"><span data-stu-id="0b847-106">It is used by hello Azure AD B2C service toostore information about users and custom attributes.</span></span> <span data-ttu-id="0b847-107">Se l'applicazione hello viene eliminato, Azure AD B2C non funzionerà correttamente e ne sarà interessato nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="0b847-107">If hello app is deleted, Azure AD B2C will not function correctly and your production environment will be affected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b847-108">Non eliminare hello b2c-estensioni-app, a meno che non si intende eliminare tooimmediately tenant.</span><span class="sxs-lookup"><span data-stu-id="0b847-108">Do not delete hello b2c-extensions-app unless you are planning tooimmediately delete your tenant.</span></span> <span data-ttu-id="0b847-109">Se l'applicazione hello rimane eliminati per più di 30 giorni, le informazioni utente andranno persi definitivamente.</span><span class="sxs-lookup"><span data-stu-id="0b847-109">If hello app remains deleted for more than 30 days, user information will be permanently lost.</span></span>

## <a name="verifying-that-hello-extensions-app-is-present"></a><span data-ttu-id="0b847-110">Verifica per determinare se è presente tale app estensioni hello</span><span class="sxs-lookup"><span data-stu-id="0b847-110">Verifying that hello extensions app is present</span></span>

<span data-ttu-id="0b847-111">tooverify che hello b2c-estensioni-app è presente:</span><span class="sxs-lookup"><span data-stu-id="0b847-111">tooverify that hello b2c-extensions-app is present:</span></span>

1. <span data-ttu-id="0b847-112">All'interno del tenant di Azure Active Directory B2C, fare clic su **più servizi** nel menu di navigazione a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="0b847-112">Inside your Azure AD B2C tenant, click on **More services** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="0b847-113">Cercare e aprire **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="0b847-113">Search for and open **App registrations**.</span></span>
1. <span data-ttu-id="0b847-114">Cercare un'app che inizia con **b2c-extensions-app**</span><span class="sxs-lookup"><span data-stu-id="0b847-114">Look for an app that begins with **b2c-extensions-app**</span></span>

## <a name="recover-hello-extensions-app"></a><span data-ttu-id="0b847-115">Ripristinare hello estensioni app</span><span class="sxs-lookup"><span data-stu-id="0b847-115">Recover hello extensions app</span></span>

<span data-ttu-id="0b847-116">Se è stato eliminato accidentalmente hello b2c-estensioni-app, è necessario toorecover di 30 giorni è.</span><span class="sxs-lookup"><span data-stu-id="0b847-116">If you accidentally deleted hello b2c-extensions-app, you have 30 days toorecover it.</span></span> <span data-ttu-id="0b847-117">È possibile ripristinare l'applicazione hello utilizzando hello API Graph:</span><span class="sxs-lookup"><span data-stu-id="0b847-117">You can restore hello app using hello Graph API:</span></span>

1. <span data-ttu-id="0b847-118">Sfoglia troppo[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="0b847-118">Browse too[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span></span>
1. <span data-ttu-id="0b847-119">Accedere come amministratore globale per la directory di Azure Active Directory B2C hello da app hello eliminato toorestore per toohello sito.</span><span class="sxs-lookup"><span data-stu-id="0b847-119">Log in toohello site as a global administrator for hello Azure AD B2C directory that you want toorestore hello deleted app for.</span></span>
1. <span data-ttu-id="0b847-120">Inviare una richiesta HTTP GET per URL hello `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` con api-version = 1.6.</span><span class="sxs-lookup"><span data-stu-id="0b847-120">Issue an HTTP GET against hello URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` with api-version=1.6.</span></span> <span data-ttu-id="0b847-121">Verificare che tooreplace `{tenantName}` con il nome del tenant.</span><span class="sxs-lookup"><span data-stu-id="0b847-121">Make sure tooreplace `{tenantName}` with your tenant name.</span></span> <span data-ttu-id="0b847-122">Questa operazione elencherà tutte le applicazioni hello che sono state eliminate all'interno di hello negli ultimi 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="0b847-122">This operation will list all of hello applications that have been deleted within hello past 30 days.</span></span>
1. <span data-ttu-id="0b847-123">Trovare un'applicazione hello hello elenco in cui il nome di hello inizia con 'b2c-estensione-app' e copiare il relativo `objectid` valore della proprietà.</span><span class="sxs-lookup"><span data-stu-id="0b847-123">Find hello application in hello list where hello name begins with 'b2c-extension-app’ and copy its `objectid` property value.</span></span>
1. <span data-ttu-id="0b847-124">Emettere un POST HTTP con URL hello `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span><span class="sxs-lookup"><span data-stu-id="0b847-124">Issue an HTTP POST against hello URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span></span> <span data-ttu-id="0b847-125">Sostituire hello `{OBJECTID}` parte dell'URL hello con hello `objectid` dal passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="0b847-125">Replace hello `{OBJECTID}` portion of hello URL with hello `objectid` from hello previous step.</span></span> 

<span data-ttu-id="0b847-126">È ora possibile troppo[vedere app hello ripristinato](#verifying-that-the-extensions-app-is-present) in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b847-126">You should now be able too[see hello restored app](#verifying-that-the-extensions-app-is-present) in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="0b847-127">Un'applicazione può essere ripristinata solo se è stato eliminato all'interno di hello ultimi 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="0b847-127">An application can only be restored if it has been deleted within hello last 30 days.</span></span> <span data-ttu-id="0b847-128">Se sono trascorsi più di 30 giorni, i dati andranno persi definitivamente.</span><span class="sxs-lookup"><span data-stu-id="0b847-128">If it has been more than 30 days, data will be permanently lost.</span></span> <span data-ttu-id="0b847-129">Per ottenere assistenza, inviare un ticket al supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="0b847-129">For more assistance, file a support ticket.</span></span>
