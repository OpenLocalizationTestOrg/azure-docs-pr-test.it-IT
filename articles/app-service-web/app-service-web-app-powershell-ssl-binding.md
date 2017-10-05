---
title: Binding di certificati SSL con PowerShell
description: Informazioni su come associare certificati SSL a un'app Web con PowerShell.
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
ms.openlocfilehash: a1fcc618fb0c68778e39cc227368a60b008f9401
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a><span data-ttu-id="30c27-103">Binding di certificati SSL del servizio App di Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="30c27-103">Azure App Service SSL Certificate Binding using PowerShell</span></span>
<span data-ttu-id="30c27-104">Con il rilascio di Microsoft Azure PowerShell versione 1.1.0 è stato aggiunto un nuovo cmdlet che consente all'utente di associare i certificati SSL nuovi o esistenti a un'app Web esistente.</span><span class="sxs-lookup"><span data-stu-id="30c27-104">With the release of Microsoft Azure PowerShell version 1.1.0 a new cmdlet has been added that would give the user the ability to bind existing or new SSL certificates to an existing Web App.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="30c27-105">Per informazioni su come usare cmdlet di Azure PowerShell basati su Azure Resource Manager per gestire le app Web, vedere [Uso di comandi di PowerShell basati su Azure Resource Manager per la gestione di app Web di Azure](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="30c27-105">To learn about using Azure Resource Manager based Azure PowerShell cmdlets to manage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="uploading-and-binding-a-new-ssl-certificate"></a><span data-ttu-id="30c27-106">Caricamento e binding di un nuovo certificato SSL</span><span class="sxs-lookup"><span data-stu-id="30c27-106">Uploading and Binding a new SSL certificate</span></span>
<span data-ttu-id="30c27-107">Scenario: l'utente vuole associare un certificato SSL a una delle proprie app Web.</span><span class="sxs-lookup"><span data-stu-id="30c27-107">Scenario: The user would like to bind an SSL certificate to one of his web apps.</span></span>

<span data-ttu-id="30c27-108">Conoscendo il nome del gruppo di risorse che contiene l'app Web, il nome dell'app Web, il percorso del file PFX del certificato nel computer dell'utente, la password per il certificato e il nome host personalizzato, è possibile usare il comando di PowerShell seguente per creare il binding SSL:</span><span class="sxs-lookup"><span data-stu-id="30c27-108">Knowing the resource group name that contains the web app, the web app name, the certificate .pfx file path on the user machine, the password for the certificate, and the custom hostname, we can use the following PowerShell command to create that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

<span data-ttu-id="30c27-109">Si noti che prima di aggiungere un binding SSL a un'app Web, è necessario avere un nome host (dominio personalizzato) già configurato.</span><span class="sxs-lookup"><span data-stu-id="30c27-109">Note that before adding a SSL binding to a web app, you must have a host name (custom domain) already configured.</span></span> <span data-ttu-id="30c27-110">Se il nome host non è configurato, durante l'esecuzione di New-AzureRmWebAppSSLBinding verrà visualizzato un errore per indicare che "nomehost" non esiste.</span><span class="sxs-lookup"><span data-stu-id="30c27-110">If the host name is not configured , then you will get an error 'hostname' does not exist while running  New-AzureRmWebAppSSLBinding.</span></span> <span data-ttu-id="30c27-111">È possibile aggiungere un nome host direttamente dal portale o con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="30c27-111">You can add a hostname directly from the portal or using Azure PowerShell.</span></span> <span data-ttu-id="30c27-112">Per configurare il nome host prima di eseguire New-AzureRmWebAppSSLBinding, è possibile usare il frammento di PowerShell seguente.</span><span class="sxs-lookup"><span data-stu-id="30c27-112">The following PowerShell snippet can be to configure the hostname before running New-AzureRmWebAppSSLBinding.</span></span>   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

<span data-ttu-id="30c27-113">È importante tenere presente che il cmdlet Set-AzureRmWebApp sovrascrive i nomi host per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="30c27-113">It is important to understand that the Set-AzureRmWebApp cmdlet overwrites the hostnames for the web app.</span></span> <span data-ttu-id="30c27-114">Perciò il frammento di PowerShell precedente aggiunge una voce all'elenco di nomi host per l'app Web esistente.</span><span class="sxs-lookup"><span data-stu-id="30c27-114">Hence the above PowerShell snippet is appending to the existing list of the host names for the web app.</span></span>  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a><span data-ttu-id="30c27-115">Caricamento e binding di un certificato SSL esistente</span><span class="sxs-lookup"><span data-stu-id="30c27-115">Uploading and Binding an existing SSL certificate</span></span>
<span data-ttu-id="30c27-116">Scenario: l'utente vuole associare un certificato SSL caricato in precedenza a una delle proprie app Web.</span><span class="sxs-lookup"><span data-stu-id="30c27-116">Scenario: The user would like to bind a previously uploaded SSL certificate to one of his web apps.</span></span>

<span data-ttu-id="30c27-117">È possibile ottenere l'elenco dei certificati già caricati in un gruppo di risorse specifico usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="30c27-117">We can get the list of certificates already uploaded to a specific resource group by using the following command</span></span>

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

<span data-ttu-id="30c27-118">Si noti che i certificati sono locali rispetto a un percorso e un gruppo di risorse specifici, quindi l'utente deve ricaricare il certificato se l'app Web configurata si trova in un percorso e in gruppo di risorse diversi da quelli del certificato richiesto.</span><span class="sxs-lookup"><span data-stu-id="30c27-118">Note that the certificates are local to a specific location and resource group, the user need to re-upload the certificate if the configured web app is in a different location and resource group other that that of the needed certificate</span></span> 

<span data-ttu-id="30c27-119">Conoscendo il nome del gruppo di risorse che contiene l'app Web, il nome dell'app Web, l'identificazione personale del certificato e il nome host personalizzato, è possibile usare il comando di PowerShell seguente per creare il binding SSL:</span><span class="sxs-lookup"><span data-stu-id="30c27-119">Knowing the resource group name that contains the web app, the web app name, the certificate thumbprint, and the custom hostname, we can use the following PowerShell command to create that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a><span data-ttu-id="30c27-120">Eliminazione di un binding SSL esistente</span><span class="sxs-lookup"><span data-stu-id="30c27-120">Deleting an existing SSL binding</span></span>
<span data-ttu-id="30c27-121">Scenario: l'utente vuole eliminare un binding SSL esistente.</span><span class="sxs-lookup"><span data-stu-id="30c27-121">Scenario: The user would like to delete an existing SSL binding.</span></span>

<span data-ttu-id="30c27-122">Conoscendo il nome del gruppo di risorse che contiene l'app Web, il nome dell'app Web e il nome host personalizzato, è possibile usare il comando di PowerShell seguente per rimuovere il binding SSL:</span><span class="sxs-lookup"><span data-stu-id="30c27-122">Knowing the resource group name that contains the web app, the web app name, and the custom hostname, we can use the following PowerShell command to remove that SSL binding:</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

<span data-ttu-id="30c27-123">Si noti che se il binding SSL rimosso era l'ultimo binding che usava quel certificato in quel percorso, per impostazione predefinita il certificato viene eliminato. Se l'utente vuole mantenere il certificato, può usare invece l'opzione DeleteCertificate.</span><span class="sxs-lookup"><span data-stu-id="30c27-123">Note that if the removed SSL binding was the last binding using that certificate in that location, by default the certificate will be deleted, if the user want to keep the certificate he can use the DeleteCertificate option to keep the certificate</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a><span data-ttu-id="30c27-124">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="30c27-124">References</span></span>
* [<span data-ttu-id="30c27-125">Uso di comandi di PowerShell basati su Azure Resource Manager per la gestione di app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="30c27-125">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="30c27-126">Introduzione all'ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="30c27-126">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="30c27-127">Uso di Azure PowerShell con Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="30c27-127">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

