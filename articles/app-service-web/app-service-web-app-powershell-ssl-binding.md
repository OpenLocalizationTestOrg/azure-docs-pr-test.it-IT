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
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a>Binding di certificati SSL del servizio App di Azure con PowerShell
Con la versione di hello di Microsoft Azure PowerShell versione 1.1.0 è stato aggiunto il nuovo cmdlet assegnano hello utente hello possibilità toobind nuova o esistente SSL certificati tooan App Web esistente.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

toolearn sull'utilizzo di gestione risorse di Azure basato su toomanage cmdlet PowerShell di Azure l'archiviazione di applicazioni Web [Gestione risorse di Azure basato su comandi di PowerShell per App Web di Azure](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="uploading-and-binding-a-new-ssl-certificate"></a>Caricamento e binding di un nuovo certificato SSL
Scenario: utente hello sarebbe toobind un tooone certificato SSL di suo App web.

Nome gruppo di risorse hello che contiene l'app web hello, nome dell'applicazione web hello, percorso del file con estensione pfx certificato hello computer utente hello conoscere hello password certificato hello e hello nome host personalizzato, sarà possibile utilizzare hello toocreate comando PowerShell seguente che Associazione di SSL:

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

Si noti che prima di aggiungere un'app web di tooa associazione SSL, è necessario disporre già configurato un nome host (dominio personalizzato). Se il nome host hello non è configurato, quindi si verificherà un errore durante l'esecuzione di New-AzureRmWebAppSSLBinding 'hostname' non esiste. Direttamente dal portale di hello o con Azure PowerShell, è possibile aggiungere un nome host. Hello seguente frammento di PowerShell può essere tooconfigure hello hostname prima di eseguire di nuovo AzureRmWebAppSSLBinding.   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

È importante toounderstand che il cmdlet Set-AzureRmWebApp hello sovrascrive hello nomi host per l'app web hello. Di conseguenza hello sopra il frammento di PowerShell viene aggiunta toohello elenco esistente di nomi host hello per l'app web hello.  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a>Caricamento e binding di un certificato SSL esistente
Scenario: utente hello sarebbe toobind un tooone del certificato SSL caricato in precedenza di suo App web.

È possibile ottenere elenco hello certificati già caricato tooa determinato gruppo di risorse utilizzando hello comando seguente

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

Si noti che i certificati di hello sono tooa locale gruppo di percorso e di risorse specifico, hello utente necessario toore caricamento hello certificato se hello configurato web app è in un percorso diverso e gruppo di risorse non necessari di hello certificato 

Nome gruppo di risorse hello che contiene l'app web hello, conoscere hello nome dell'applicazione web, hello identificazione personale del certificato ed hello nome host personalizzato, è possibile utilizzare tale associazione SSL hello toocreate comando PowerShell seguente:

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a>Eliminazione di un binding SSL esistente
Scenario: utente hello sarebbe toodelete un'associazione SSL esistente.

Nome gruppo di risorse hello che contiene l'app web hello, conoscere hello nome dell'applicazione web e hello nome host personalizzato, è possibile utilizzare tale associazione SSL hello tooremove comando PowerShell seguente:

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

Si noti che se hello rimosso l'associazione SSL è stato hello ultimo binding utilizzando tale certificato in tale posizione, da un certificato predefinito hello verranno eliminati, utente hello certificato hello tookeep è possibile utilizzare il certificato hello tookeep di hello DeleteCertificate opzione

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a>Riferimenti
* [Uso di comandi di PowerShell basati su Azure Resource Manager per la gestione di app Web di Azure](app-service-web-app-azure-resource-manager-powershell.md)
* [Introduzione tooApp ambiente del servizio](app-service-app-service-environment-intro.md)
* [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md)

