---
title: Certificati aaaSSL binding utilizzando PowerShell
description: Informazioni su come toobind SSL certificati tooyour web app tramite PowerShell.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 8ce32508-e982-48d3-b878-0e526afda537
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: 82f0e7c796da99ab50f69f3638ef64d55a94fc8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a><span data-ttu-id="fe7c4-103">Binding di certificati SSL del servizio App di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe7c4-103">Azure App Service SSL Certificate Binding using PowerShell</span></span>
<span data-ttu-id="fe7c4-104">Con la versione di hello di Microsoft Azure PowerShell versione 1.1.0 è stato aggiunto il nuovo cmdlet assegnano hello utente hello possibilità toobind nuova o esistente SSL certificati tooan App Web esistente.</span><span class="sxs-lookup"><span data-stu-id="fe7c4-104">With hello release of Microsoft Azure PowerShell version 1.1.0 a new cmdlet has been added that would give hello user hello ability toobind existing or new SSL certificates tooan existing Web App.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="fe7c4-105">toolearn sull'utilizzo di gestione risorse di Azure basato su toomanage cmdlet PowerShell di Azure l'archiviazione di applicazioni Web [Gestione risorse di Azure basato su comandi di PowerShell per App Web di Azure](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="fe7c4-105">toolearn about using Azure Resource Manager based Azure PowerShell cmdlets toomanage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="uploading-and-binding-a-new-ssl-certificate"></a><span data-ttu-id="fe7c4-106">Caricamento e binding di un nuovo certificato SSL</span><span class="sxs-lookup"><span data-stu-id="fe7c4-106">Uploading and Binding a new SSL certificate</span></span>
<span data-ttu-id="fe7c4-107">Scenario: utente hello sarebbe toobind un tooone certificato SSL di suo App web.</span><span class="sxs-lookup"><span data-stu-id="fe7c4-107">Scenario: hello user would like toobind an SSL certificate tooone of his web apps.</span></span>

<span data-ttu-id="fe7c4-108">Nome gruppo di risorse hello che contiene l'app web hello, nome dell'applicazione web hello, percorso del file con estensione pfx certificato hello computer utente hello conoscere hello password certificato hello e hello nome host personalizzato, sarà possibile utilizzare hello toocreate comando PowerShell seguente che Associazione di SSL:</span><span class="sxs-lookup"><span data-stu-id="fe7c4-108">Knowing hello resource group name that contains hello web app, hello web app name, hello certificate .pfx file path on hello user machine, hello password for hello certificate, and hello custom hostname, we can use hello following PowerShell command toocreate that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

<span data-ttu-id="fe7c4-109">Si noti che prima di aggiungere un'app web di tooa associazione SSL, è necessario disporre già configurato un nome host (dominio personalizzato).</span><span class="sxs-lookup"><span data-stu-id="fe7c4-109">Note that before adding a SSL binding tooa web app, you must have a host name (custom domain) already configured.</span></span> <span data-ttu-id="fe7c4-110">Se il nome host hello non è configurato, quindi si verificherà un errore durante l'esecuzione di New-AzureRmWebAppSSLBinding 'hostname' non esiste.</span><span class="sxs-lookup"><span data-stu-id="fe7c4-110">If hello host name is not configured , then you will get an error 'hostname' does not exist while running  New-AzureRmWebAppSSLBinding.</span></span> <span data-ttu-id="fe7c4-111">Direttamente dal portale di hello o con Azure PowerShell, è possibile aggiungere un nome host.</span><span class="sxs-lookup"><span data-stu-id="fe7c4-111">You can add a hostname directly from hello portal or using Azure PowerShell.</span></span> <span data-ttu-id="fe7c4-112">Hello seguente frammento di PowerShell può essere tooconfigure hello hostname prima di eseguire di nuovo AzureRmWebAppSSLBinding.</span><span class="sxs-lookup"><span data-stu-id="fe7c4-112">hello following PowerShell snippet can be tooconfigure hello hostname before running New-AzureRmWebAppSSLBinding.</span></span>   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

<span data-ttu-id="fe7c4-113">È importante toounderstand che il cmdlet Set-AzureRmWebApp hello sovrascrive hello nomi host per l'app web hello.</span><span class="sxs-lookup"><span data-stu-id="fe7c4-113">It is important toounderstand that hello Set-AzureRmWebApp cmdlet overwrites hello hostnames for hello web app.</span></span> <span data-ttu-id="fe7c4-114">Di conseguenza hello sopra il frammento di PowerShell viene aggiunta toohello elenco esistente di nomi host hello per l'app web hello.</span><span class="sxs-lookup"><span data-stu-id="fe7c4-114">Hence hello above PowerShell snippet is appending toohello existing list of hello host names for hello web app.</span></span>  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a><span data-ttu-id="fe7c4-115">Caricamento e binding di un certificato SSL esistente</span><span class="sxs-lookup"><span data-stu-id="fe7c4-115">Uploading and Binding an existing SSL certificate</span></span>
<span data-ttu-id="fe7c4-116">Scenario: utente hello sarebbe toobind un tooone del certificato SSL caricato in precedenza di suo App web.</span><span class="sxs-lookup"><span data-stu-id="fe7c4-116">Scenario: hello user would like toobind a previously uploaded SSL certificate tooone of his web apps.</span></span>

<span data-ttu-id="fe7c4-117">È possibile ottenere elenco hello certificati già caricato tooa determinato gruppo di risorse utilizzando hello comando seguente</span><span class="sxs-lookup"><span data-stu-id="fe7c4-117">We can get hello list of certificates already uploaded tooa specific resource group by using hello following command</span></span>

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

<span data-ttu-id="fe7c4-118">Si noti che i certificati di hello sono tooa locale gruppo di percorso e di risorse specifico, hello utente necessario toore caricamento hello certificato se hello configurato web app è in un percorso diverso e gruppo di risorse non necessari di hello certificato</span><span class="sxs-lookup"><span data-stu-id="fe7c4-118">Note that hello certificates are local tooa specific location and resource group, hello user need toore-upload hello certificate if hello configured web app is in a different location and resource group other that that of hello needed certificate</span></span> 

<span data-ttu-id="fe7c4-119">Nome gruppo di risorse hello che contiene l'app web hello, conoscere hello nome dell'applicazione web, hello identificazione personale del certificato ed hello nome host personalizzato, è possibile utilizzare tale associazione SSL hello toocreate comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="fe7c4-119">Knowing hello resource group name that contains hello web app, hello web app name, hello certificate thumbprint, and hello custom hostname, we can use hello following PowerShell command toocreate that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a><span data-ttu-id="fe7c4-120">Eliminazione di un binding SSL esistente</span><span class="sxs-lookup"><span data-stu-id="fe7c4-120">Deleting an existing SSL binding</span></span>
<span data-ttu-id="fe7c4-121">Scenario: utente hello sarebbe toodelete un'associazione SSL esistente.</span><span class="sxs-lookup"><span data-stu-id="fe7c4-121">Scenario: hello user would like toodelete an existing SSL binding.</span></span>

<span data-ttu-id="fe7c4-122">Nome gruppo di risorse hello che contiene l'app web hello, conoscere hello nome dell'applicazione web e hello nome host personalizzato, è possibile utilizzare tale associazione SSL hello tooremove comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="fe7c4-122">Knowing hello resource group name that contains hello web app, hello web app name, and hello custom hostname, we can use hello following PowerShell command tooremove that SSL binding:</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

<span data-ttu-id="fe7c4-123">Si noti che se hello rimosso l'associazione SSL è stato hello ultimo binding utilizzando tale certificato in tale posizione, da un certificato predefinito hello verranno eliminati, utente hello certificato hello tookeep è possibile utilizzare il certificato hello tookeep di hello DeleteCertificate opzione</span><span class="sxs-lookup"><span data-stu-id="fe7c4-123">Note that if hello removed SSL binding was hello last binding using that certificate in that location, by default hello certificate will be deleted, if hello user want tookeep hello certificate he can use hello DeleteCertificate option tookeep hello certificate</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a><span data-ttu-id="fe7c4-124">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="fe7c4-124">References</span></span>
* [<span data-ttu-id="fe7c4-125">Uso di comandi di PowerShell basati su Azure Resource Manager per la gestione di app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="fe7c4-125">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="fe7c4-126">Introduzione tooApp ambiente del servizio</span><span class="sxs-lookup"><span data-stu-id="fe7c4-126">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="fe7c4-127">Uso di Azure PowerShell con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fe7c4-127">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

