---
title: utilizzando dati aaaGet hello API Azure AD Reporting con certificati | Documenti Microsoft
description: Viene illustrato come toouse hello API Azure AD Reporting con dati tooget le credenziali del certificato dalla directory senza intervento dell'utente.
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
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a><span data-ttu-id="703d8-103">Acquisizione di dati utilizzando l'API di Reporting di hello Azure AD con certificati</span><span class="sxs-lookup"><span data-stu-id="703d8-103">Get data using hello Azure AD Reporting API with certificates</span></span>
<span data-ttu-id="703d8-104">Questo articolo illustra come toouse hello API Azure AD Reporting con dati tooget le credenziali del certificato dalla directory senza intervento dell'utente.</span><span class="sxs-lookup"><span data-stu-id="703d8-104">This article discusses how toouse hello Azure AD Reporting API with certificate credentials tooget data from directories without user intervention.</span></span> 

## <a name="use-hello-azure-ad-reporting-api"></a><span data-ttu-id="703d8-105">Utilizzare hello API Azure AD Reporting</span><span class="sxs-lookup"><span data-stu-id="703d8-105">Use hello Azure AD Reporting API</span></span> 
<span data-ttu-id="703d8-106">API Azure AD Reporting richiede di completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="703d8-106">Azure AD Reporting API requires that you complete hello following steps:</span></span>
 *  <span data-ttu-id="703d8-107">Installare i componenti prerequisiti</span><span class="sxs-lookup"><span data-stu-id="703d8-107">Install prerequisites</span></span>
 *  <span data-ttu-id="703d8-108">Impostare il certificato hello nell'app</span><span class="sxs-lookup"><span data-stu-id="703d8-108">Set hello certificate in your app</span></span>
 *  <span data-ttu-id="703d8-109">Ottenere un token di accesso</span><span class="sxs-lookup"><span data-stu-id="703d8-109">Get an access token</span></span>
 *  <span data-ttu-id="703d8-110">Utilizzare hello toocall token di accesso hello API Graph</span><span class="sxs-lookup"><span data-stu-id="703d8-110">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="703d8-111">Per informazioni sul codice sorgente, vedere [Sfruttare il modulo dell'API di creazione report](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span><span class="sxs-lookup"><span data-stu-id="703d8-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span></span> 

### <a name="install-prerequisites"></a><span data-ttu-id="703d8-112">Installare i componenti prerequisiti</span><span class="sxs-lookup"><span data-stu-id="703d8-112">Install prerequisites</span></span>
<span data-ttu-id="703d8-113">Sarà necessario toohave Azure AD PowerShell V2 e AzureADUtils modulo installato.</span><span class="sxs-lookup"><span data-stu-id="703d8-113">You will need toohave Azure AD PowerShell V2 and AzureADUtils module installed.</span></span>

1. <span data-ttu-id="703d8-114">Scaricare e installare Azure AD Powershell V2, attenendosi alle istruzioni hello in [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="703d8-114">Download and install Azure AD Powershell V2, following hello instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span></span>
2. <span data-ttu-id="703d8-115">Scaricare il modulo di Azure AD Utils hello da [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span><span class="sxs-lookup"><span data-stu-id="703d8-115">Download hello Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span></span> 
  <span data-ttu-id="703d8-116">Questo modulo offre diversi cmdlet di utilità, tra cui:</span><span class="sxs-lookup"><span data-stu-id="703d8-116">This module provides several utility cmdlets including:</span></span>
   * <span data-ttu-id="703d8-117">versione più recente di Hello della libreria ADAL tramite Nuget</span><span class="sxs-lookup"><span data-stu-id="703d8-117">hello latest version of ADAL using Nuget</span></span>
   * <span data-ttu-id="703d8-118">Token di accesso dell'utente, chiavi dell'applicazione e certificati con ADAL</span><span class="sxs-lookup"><span data-stu-id="703d8-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
   * <span data-ttu-id="703d8-119">API Graph che gestisce i risultati di paging</span><span class="sxs-lookup"><span data-stu-id="703d8-119">Graph API handling paged results</span></span>

<span data-ttu-id="703d8-120">**modulo di Azure AD Utils tooinstall hello:**</span><span class="sxs-lookup"><span data-stu-id="703d8-120">**tooinstall hello Azure AD Utils module:**</span></span>

1. <span data-ttu-id="703d8-121">Creare un modulo di utilità hello toosave directory (ad esempio, c:\azureAD) e scaricare il modulo di hello da GitHub.</span><span class="sxs-lookup"><span data-stu-id="703d8-121">Create a directory toosave hello utilities module (for example, c:\azureAD) and download hello module from GitHub.</span></span>
2. <span data-ttu-id="703d8-122">Aprire una sessione di PowerShell e passare toohello directory che appena creata.</span><span class="sxs-lookup"><span data-stu-id="703d8-122">Open a PowerShell session, and go toohello directory you just created.</span></span> 
3. <span data-ttu-id="703d8-123">Importare il modulo hello e installarlo nel percorso di modulo di PowerShell hello utilizzando il cmdlet Install-AzureADUtilsModule hello.</span><span class="sxs-lookup"><span data-stu-id="703d8-123">Import hello module, and install it in hello PowerShell module path using hello Install-AzureADUtilsModule cmdlet.</span></span> 

<span data-ttu-id="703d8-124">sessione Hello dovrebbe essere simile toothis schermo:</span><span class="sxs-lookup"><span data-stu-id="703d8-124">hello session should look similar toothis screen:</span></span>

  ![Windows Powershell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a><span data-ttu-id="703d8-126">Impostare il certificato hello nell'app</span><span class="sxs-lookup"><span data-stu-id="703d8-126">Set hello certificate in your app</span></span>
1. <span data-ttu-id="703d8-127">Se si dispone già di un'app, è possibile ottenere l'ID di oggetto da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="703d8-127">If you already have an app, get its Object ID from hello Azure Portal.</span></span> 

  ![Portale di Azure](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. <span data-ttu-id="703d8-129">Aprire una sessione di PowerShell e connettersi AD tooAzure utilizzando il cmdlet Connect-AzureAD hello.</span><span class="sxs-lookup"><span data-stu-id="703d8-129">Open a PowerShell session and connect tooAzure AD using hello Connect-AzureAD cmdlet.</span></span>

  ![Portale di Azure](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. <span data-ttu-id="703d8-131">Utilizzare il cmdlet New-AzureADApplicationCertificateCredential hello da AzureADUtils tooadd tooit di credenziali un certificato.</span><span class="sxs-lookup"><span data-stu-id="703d8-131">Use hello New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils tooadd a certificate credential tooit.</span></span> 

>[!Note]
><span data-ttu-id="703d8-132">È necessaria un'applicazione hello tooprovide ID di oggetto acquisita in precedenza, nonché hello oggetto certificato (ottenere questa operazione utilizzando hello Cert: unità).</span><span class="sxs-lookup"><span data-stu-id="703d8-132">You need tooprovide hello application Object ID that you captured earlier, as well as hello certificate object (get this using hello Cert: drive).</span></span>
>


  ![Portale di Azure](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a><span data-ttu-id="703d8-134">Ottenere un token di accesso</span><span class="sxs-lookup"><span data-stu-id="703d8-134">Get an access token</span></span>

<span data-ttu-id="703d8-135">tooget un token di accesso, utilizzare il cmdlet Get-AzureADGraphAPIAccessTokenFromCert hello da AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="703d8-135">tooget an access token, use hello Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span></span> 

>[!NOTE]
><span data-ttu-id="703d8-136">È necessario toouse hello ID applicazione anziché hello ID di oggetto utilizzati nell'ultima sezione hello.</span><span class="sxs-lookup"><span data-stu-id="703d8-136">You need toouse hello Application ID instead of hello Object ID that you used in hello last section.</span></span>
>

 ![Portale di Azure](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a><span data-ttu-id="703d8-138">Utilizzare hello toocall token di accesso hello API Graph</span><span class="sxs-lookup"><span data-stu-id="703d8-138">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="703d8-139">È ora possibile creare script hello.</span><span class="sxs-lookup"><span data-stu-id="703d8-139">Now you can create hello script.</span></span> <span data-ttu-id="703d8-140">Di seguito è riportato un esempio, tramite il cmdlet Invoke-AzureADGraphAPIQuery hello da hello AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="703d8-140">Below is an example using hello Invoke-AzureADGraphAPIQuery cmdlet from hello AzureADUtils.</span></span> <span data-ttu-id="703d8-141">Questo cmdlet gestisce i risultati con più pagine e quindi invia tali pipeline di PowerShell toohello risultati.</span><span class="sxs-lookup"><span data-stu-id="703d8-141">This cmdlet handles multi-paged results, and then sends those results toohello PowerShell pipeline.</span></span> 

 ![Portale di Azure](./media/active-directory-report-api-with-certificates/script-completed.png)

<span data-ttu-id="703d8-143">Si sono ora pronti tooexport tooa CSV e Salva sistema SIEM tooa.</span><span class="sxs-lookup"><span data-stu-id="703d8-143">You are now ready tooexport tooa CSV and save tooa SIEM system.</span></span> <span data-ttu-id="703d8-144">È possibile anche includere lo script in un tooget attività pianificata, i dati di Azure AD dal tenant periodicamente senza chiavi applicazione toostore nel codice sorgente hello.</span><span class="sxs-lookup"><span data-stu-id="703d8-144">You can also wrap your script in a scheduled task tooget Azure AD data from your tenant periodically without having toostore application keys in hello source code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="703d8-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="703d8-145">Next steps</span></span>
[<span data-ttu-id="703d8-146">Nozioni fondamentali su Hello della gestione delle identità di Azure</span><span class="sxs-lookup"><span data-stu-id="703d8-146">hello fundamentals of Azure identity management</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



