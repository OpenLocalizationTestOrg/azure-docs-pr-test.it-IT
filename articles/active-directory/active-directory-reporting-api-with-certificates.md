---
title: Ottenere dati con l'API di creazione report di Azure AD con certificati | Microsoft Docs
description: Spiega come usare l'API di creazione report di Azure AD con le credenziali del certificato per ottenere i dati provenienti da directory senza intervento dell'utente.
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: c1345dcda6e52267a8037ffd7207e6bc3b0d3b31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-data-using-the-azure-ad-reporting-api-with-certificates"></a><span data-ttu-id="5c4fb-103">Ottenere dati con l'API di creazione report di Azure AD con certificati</span><span class="sxs-lookup"><span data-stu-id="5c4fb-103">Get data using the Azure AD Reporting API with certificates</span></span>
<span data-ttu-id="5c4fb-104">Questo articolo spiega come usare l'API di creazione report di Azure AD con le credenziali del certificato per ottenere i dati provenienti da directory senza intervento dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5c4fb-104">This article discusses how to use the Azure AD Reporting API with certificate credentials to get data from directories without user intervention.</span></span> 

## <a name="use-the-azure-ad-reporting-api"></a><span data-ttu-id="5c4fb-105">Usare l'API di creazione report di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c4fb-105">Use the Azure AD Reporting API</span></span> 
<span data-ttu-id="5c4fb-106">L'API di creazione report di Azure AD richiede il completamento dei passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="5c4fb-106">Azure AD Reporting API requires that you complete the following steps:</span></span>
 *  <span data-ttu-id="5c4fb-107">Installare i componenti prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5c4fb-107">Install prerequisites</span></span>
 *  <span data-ttu-id="5c4fb-108">Impostare il certificato nell'app</span><span class="sxs-lookup"><span data-stu-id="5c4fb-108">Set the certificate in your app</span></span>
 *  <span data-ttu-id="5c4fb-109">Ottenere un token di accesso</span><span class="sxs-lookup"><span data-stu-id="5c4fb-109">Get an access token</span></span>
 *  <span data-ttu-id="5c4fb-110">Usare il token di accesso per chiamare l'API Graph</span><span class="sxs-lookup"><span data-stu-id="5c4fb-110">Use the access token to call the Graph API</span></span>

<span data-ttu-id="5c4fb-111">Per informazioni sul codice sorgente, vedere [Sfruttare il modulo dell'API di creazione report](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span><span class="sxs-lookup"><span data-stu-id="5c4fb-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span></span> 

### <a name="install-prerequisites"></a><span data-ttu-id="5c4fb-112">Installare i componenti prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5c4fb-112">Install prerequisites</span></span>
<span data-ttu-id="5c4fb-113">È necessario avere installato Azure AD PowerShell V2 e il modulo AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="5c4fb-113">You will need to have Azure AD PowerShell V2 and AzureADUtils module installed.</span></span>

1. <span data-ttu-id="5c4fb-114">Scaricare e installare Azure AD Powershell V2 seguendo le istruzioni illustrate in [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="5c4fb-114">Download and install Azure AD Powershell V2, following the instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span></span>
2. <span data-ttu-id="5c4fb-115">Scaricare il modulo AzureADUtils da [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span><span class="sxs-lookup"><span data-stu-id="5c4fb-115">Download the Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span></span> 
  <span data-ttu-id="5c4fb-116">Questo modulo offre diversi cmdlet di utilità, tra cui:</span><span class="sxs-lookup"><span data-stu-id="5c4fb-116">This module provides several utility cmdlets including:</span></span>
   * <span data-ttu-id="5c4fb-117">La versione più recente di ADAL con NuGet</span><span class="sxs-lookup"><span data-stu-id="5c4fb-117">The latest version of ADAL using Nuget</span></span>
   * <span data-ttu-id="5c4fb-118">Token di accesso dell'utente, chiavi dell'applicazione e certificati con ADAL</span><span class="sxs-lookup"><span data-stu-id="5c4fb-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
   * <span data-ttu-id="5c4fb-119">API Graph che gestisce i risultati di paging</span><span class="sxs-lookup"><span data-stu-id="5c4fb-119">Graph API handling paged results</span></span>

<span data-ttu-id="5c4fb-120">**Per installare il modulo AzureADUtils:**</span><span class="sxs-lookup"><span data-stu-id="5c4fb-120">**To install the Azure AD Utils module:**</span></span>

1. <span data-ttu-id="5c4fb-121">Creare una directory in cui salvare il modulo delle utilità, ad esempio c:\azureAD, e scaricare il modulo da GitHub.</span><span class="sxs-lookup"><span data-stu-id="5c4fb-121">Create a directory to save the utilities module (for example, c:\azureAD) and download the module from GitHub.</span></span>
2. <span data-ttu-id="5c4fb-122">Aprire una sessione di PowerShell e passare alla directory appena creata.</span><span class="sxs-lookup"><span data-stu-id="5c4fb-122">Open a PowerShell session, and go to the directory you just created.</span></span> 
3. <span data-ttu-id="5c4fb-123">Importare il modulo e installarlo nel percorso del modulo di PowerShell usando il cmdlet Install-AzureADUtilsModule.</span><span class="sxs-lookup"><span data-stu-id="5c4fb-123">Import the module, and install it in the PowerShell module path using the Install-AzureADUtilsModule cmdlet.</span></span> 

<span data-ttu-id="5c4fb-124">La sessione avrà un aspetto simile a questa schermata:</span><span class="sxs-lookup"><span data-stu-id="5c4fb-124">The session should look similar to this screen:</span></span>

  ![Windows Powershell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-the-certificate-in-your-app"></a><span data-ttu-id="5c4fb-126">Impostare il certificato nell'app</span><span class="sxs-lookup"><span data-stu-id="5c4fb-126">Set the certificate in your app</span></span>
1. <span data-ttu-id="5c4fb-127">Se è già disponibile un'app, ottenere il relativo ID oggetto dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5c4fb-127">If you already have an app, get its Object ID from the Azure Portal.</span></span> 

  ![Portale di Azure](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. <span data-ttu-id="5c4fb-129">Aprire una sessione di PowerShell e connettersi ad Azure AD usando il cmdlet Connect-AzureAD.</span><span class="sxs-lookup"><span data-stu-id="5c4fb-129">Open a PowerShell session and connect to Azure AD using the Connect-AzureAD cmdlet.</span></span>

  ![Portale di Azure](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. <span data-ttu-id="5c4fb-131">Usare il cmdlet New-AzureADApplicationCertificateCredential da AzureADUtils per aggiungere una credenziale di certificato.</span><span class="sxs-lookup"><span data-stu-id="5c4fb-131">Use the New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils to add a certificate credential to it.</span></span> 

>[!Note]
><span data-ttu-id="5c4fb-132">È necessario specificare l'ID oggetto dell'applicazione acquisito in precedenza, nonché l'oggetto certificato che può essere ottenuto usando l'unità Cert:</span><span class="sxs-lookup"><span data-stu-id="5c4fb-132">You need to provide the application Object ID that you captured earlier, as well as the certificate object (get this using the Cert: drive).</span></span>
>


  ![Portale di Azure](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a><span data-ttu-id="5c4fb-134">Ottenere un token di accesso</span><span class="sxs-lookup"><span data-stu-id="5c4fb-134">Get an access token</span></span>

<span data-ttu-id="5c4fb-135">Per ottenere un token di accesso, usare il cmdlet Get-AzureADGraphAPIAccessTokenFromCert da AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="5c4fb-135">To get an access token, use the Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span></span> 

>[!NOTE]
><span data-ttu-id="5c4fb-136">È necessario usare l'ID applicazione invece dell'ID oggetto usato nell'ultima sezione.</span><span class="sxs-lookup"><span data-stu-id="5c4fb-136">You need to use the Application ID instead of the Object ID that you used in the last section.</span></span>
>

 ![Portale di Azure](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-the-access-token-to-call-the-graph-api"></a><span data-ttu-id="5c4fb-138">Usare il token di accesso per chiamare l'API Graph</span><span class="sxs-lookup"><span data-stu-id="5c4fb-138">Use the access token to call the Graph API</span></span>

<span data-ttu-id="5c4fb-139">È ora possibile creare lo script.</span><span class="sxs-lookup"><span data-stu-id="5c4fb-139">Now you can create the script.</span></span> <span data-ttu-id="5c4fb-140">Di seguito è riportato un esempio con il cmdlet Invoke-AzureADGraphAPIQuery di AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="5c4fb-140">Below is an example using the Invoke-AzureADGraphAPIQuery cmdlet from the AzureADUtils.</span></span> <span data-ttu-id="5c4fb-141">Questo cmdlet gestisce i risultati di multi-paging e li invia alla pipeline di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5c4fb-141">This cmdlet handles multi-paged results, and then sends those results to the PowerShell pipeline.</span></span> 

 ![Portale di Azure](./media/active-directory-report-api-with-certificates/script-completed.png)

<span data-ttu-id="5c4fb-143">A questo punto è possibile esportare in un file CSV e salvare in un sistema SIEM.</span><span class="sxs-lookup"><span data-stu-id="5c4fb-143">You are now ready to export to a CSV and save to a SIEM system.</span></span> <span data-ttu-id="5c4fb-144">È anche possibile eseguire il wrapping dello script in un'attività pianificata per ottenere periodicamente i dati di Azure AD dal tenant senza dover archiviare le chiavi dell'applicazione nel codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="5c4fb-144">You can also wrap your script in a scheduled task to get Azure AD data from your tenant periodically without having to store application keys in the source code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5c4fb-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5c4fb-145">Next steps</span></span>
[<span data-ttu-id="5c4fb-146">Concetti fondamentali sulla gestione delle identità di Azure</span><span class="sxs-lookup"><span data-stu-id="5c4fb-146">The fundamentals of Azure identity management</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



