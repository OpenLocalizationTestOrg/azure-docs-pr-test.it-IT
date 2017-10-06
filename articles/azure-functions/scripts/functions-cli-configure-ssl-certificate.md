---
title: Script di esempio CLI - aaaAzure associare un'app di funzione tooa di certificato SSL personalizzata | Documenti Microsoft
description: Esempio di Script Azure CLI - binding SSL certificato tooa funzione app personalizzata in Azure
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 04/10/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 692dbc03583f2978131823083f1bfd257882664c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-function-app"></a>Associare un'app di funzione tooa di certificati SSL personalizzata

Questo script di esempio crea un'app di funzione nel servizio App con le relative risorse correlate, quindi associa il certificato SSL hello di un tooit nome di dominio personalizzato. Per questo esempio è necessario:

* Pagina di configurazione DNS del registrar di dominio tooyour di accesso.
* Un oggetto valido. Il file PFX e la relativa password per hello SSL certificato desidera tooupload e il binding.

toobind un certificato SSL, è necessario creare l'app di funzione in un piano di servizio App e non in un piano di utilizzo.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script di esempio

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello i comandi seguenti. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Crea un toobind necessario piano di servizio App di certificati SSL. |
| [az functionapp create]() | Creare un'app per le funzioni. |
| [az appservice web config hostname add](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | Esegue il mapping di un'app di funzione toohello dominio personalizzato. |
| [az appservice web config ssl upload](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | Carica un'app di funzione tooa certificato SSL. |
| [az appservice web config ssl bind](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | Associa un'app di funzione tooa di certificati SSL caricata. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).

Esempi di script aggiuntivi CLI di servizio App sono reperibile in hello [documentazione di Azure App Service]().
