---
title: una distribuzione del servizio cloud (Node.js) aaaStage | Documenti Microsoft
description: Informazioni su come toodeploy tooa l'applicazione Azure gestione temporanea di ambiente, quindi distribuire tooa ambiente di produzione tramite scambio IP virtuale (VIP).
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d65d26a6-b424-49cd-a88c-7ef46bb112a8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 0656c84ac444a10f152f441265f85141347bf1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="staging-an-application-in-azure"></a>Gestione temporanea di un'applicazione in Azure
Un pacchetto dell'applicazione può essere distribuito toohello in Azure toobe testata prima di spostarla produzione toohello ambiente di gestione temporanea ambiente nel quale hello è accessibile su Internet hello applicazione. Ambiente di gestione temporanea è esattamente come ambiente di produzione hello, ad eccezione del fatto che è possibile solo hello di accesso di gestione temporanea dell'applicazione con un URL offuscato che viene generato da Azure. Dopo aver verificato che l'applicazione funzioni correttamente, può essere distribuito toohello ambiente di produzione mediante l'esecuzione di uno scambio di IP virtuale (VIP).

> [!NOTE]
> Hello passaggi in questo articolo si applicano solo applicazioni toonode ospitate come servizio Cloud Azure.
> 
> 

## <a name="step-1-stage-an-application"></a>Passaggio 1: Gestire un'applicazione in modo temporaneo
Questa attività illustra come un'applicazione utilizzando toostage hello **Microsoft Azure PowerShell**.

1. Quando si pubblica un servizio, è sufficiente passare hello **-Slot** parametro hello **pubblica AzureServiceProject** cmdlet.
   
   ```powershell
   Publish-AzureServiceProject -Slot staging
   ```
2. Accesso toohello [portale di Azure classico] e selezionare **servizi Cloud**. Dopo il servizio cloud hello viene creato e hello **gestione temporanea** stato della colonna è stato aggiornato troppo**esecuzione**, fare clic sul nome del servizio hello.
   
   ![Portale con servizio in esecuzione][cloud-service]
3. Seleziona hello **Dashboard**, quindi selezionare **gestione temporanea**.
   
   ![Dashboard del servizio cloud][cloud-service-dashboard]
4. Si noti il valore di hello in hello **URL del sito** destra toohello voce. nome DNS Hello è un ID interno offuscato generato Azure.
   
    ![Site URL][cloud-service-staging-url]

È ora possibile verificare che un'applicazione hello funzioni correttamente nell'ambiente di gestione temporanea usando l'URL del sito di gestione temporanea hello hello.

## <a name="step-2-upgrade-an-application-in-production-by-swapping-vips"></a>Passaggio 2: Aggiornare un'applicazione in produzione tramite lo scambio di indirizzi VIP
Dopo aver verificato hello versione aggiornata di un'applicazione nell'ambiente di gestione temporanea, è possibile impostarlo disponibili nell'ambiente di produzione scambiando gli indirizzi IP virtuale (VIP) degli ambienti di gestione temporanea e produzione hello hello.

> [!NOTE]
> Questo passaggio si presuppone di aver già distribuito tooproduction un'applicazione e hello versione aggiornata dell'applicazione di gestione temporanea.
> 
> 

1. Accedere al hello [portale di Azure classico], fare clic su **servizi Cloud** , quindi selezionare il nome di servizio hello.
2. Da hello **Dashboard**selezionare **gestione temporanea**, quindi fare clic su **scambiare** nella parte inferiore di hello della pagina hello. Si aprirà hello finestra di dialogo di scambio VIP.
   
   ![Finestra di dialogo VIP Swap][vip-swap-dialog]
3. Esaminare le informazioni di hello e quindi fare clic su **OK**. due distribuzioni Hello iniziano l'aggiornamento come hello distribuzione commutatori tooproduction e hello produzione distribuzione commutatori toostaging di gestione temporanea.

Scalare una distribuzione e aggiornamento di una distribuzione di produzione scambiando gli indirizzi VIP con la distribuzione di hello in gestione temporanea completata.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Come tooDeploy un tooProduction l'aggiornamento del servizio tramite lo scambio VIP in Azure]

[portale di Azure classico]: http://manage.windowsazure.com
[cloud-service]: ./media/cloud-services-nodejs-stage-application/staging-cloud-service-running.png
[cloud-service-dashboard]: ./media/cloud-services-nodejs-stage-application/cloud-service-dashboard-staging.png
[cloud-service-staging-url]: ./media/cloud-services-nodejs-stage-application/cloud-service-staging-url.png
[vip-swap-dialog]: ./media/cloud-services-nodejs-stage-application/vip-swap-dialog.png
[Come tooDeploy un tooProduction l'aggiornamento del servizio tramite lo scambio VIP in Azure]: cloud-services-how-to-manage.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
