---
title: aaaWeb la clonazione di App tramite il portale di Azure
description: Informazioni su come tooclone il toonew App Web App Web tramite il portale di Azure.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: 605c4879f34d568e9981c34109f9496731c9ed18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a>Clonazione di app del servizio app di Azure con il portale di Azure
la funzionalità di clonazione Hello [App Web di servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) consente di eseguire facilmente la clonazione app web esistente App tooa appena creato in un'area diversa o in hello stessa area. In questo modo i clienti toodeploy un numero di App in aree geografiche diverse in modo semplice e rapido.

La clonazione di app è attualmente supportata solo per i piani di servizio app Premium. Usa funzionalità nuova Hello hello stesso limitazioni delle funzionalità di Backup di applicazioni Web, vedere [eseguire il backup di un'app web in Azure App Service](web-sites-backup.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a>Clonazione di un'app esistente
app web Hello deve essere eseguita in hello **Premium** modalità affinché si toocreate un duplicato per l'app web hello.

1. In hello [portale Azure](https://portal.azure.com/), aprire il pannello dell'app web.
2. Fare clic su **Strumenti**. Quindi, nel hello **strumenti** pannello, fare clic su **Clone App**.
   
    ![][1]
   
   > [!NOTE]
   > Se hello web app non è già in hello **Premium** modalità, si riceverà un messaggio che indica la modalità di hello è supportato per la clonazione di app. A questo punto, si dispone di hello opzione tooselect **aggiornamento**.
   > 
   > 
3. In hello **Clone App** pannello consente di specificare un nome di hello nuova app web, gruppo di risorse e piano di servizio App. Anche hello utente sarà in grado di toochoose se tooclone una serie di impostazioni app web di origine o non.
   
    ![][2]
4. Dopo aver fatto clic **creare** piattaforma hello inizierà a funzionare per la creazione di un clone di hello app web di origine.

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a>La clonazione di un tooan App esistenti di ambiente del servizio App
In hello **Clone App** cliente hello pannello avrà hello opzione toochoose un pool di applicazioni in un ambiente di servizio App esistente.

## <a name="current-restrictions"></a>Restrizioni attuali
Questa funzionalità è attualmente in anteprima, Microsoft è impegnata tooadd nuove funzionalità nel tempo, hello seguente elenco sono hello restrizioni note sul supporto corrente hello di clonazione app nel portale di Azure:

* Le impostazioni di Gestione traffico di Azure non vengono clonate.
* Le impostazioni di ridimensionamento automatico non vengono clonate.
* Le impostazioni di pianificazione del backup non vengono clonate.
* Le impostazioni della rete virtuale non vengono clonate.
* App Insights non automaticamente impostate nell'applicazione web di destinazione hello
* Le impostazioni di Easy Auth non vengono clonate.
* L'estensione Kudu non viene clonata.
* Le regole TiP non vengono clonate.
* Il contenuto di database non viene clonato.

### <a name="references"></a>Riferimenti
* [Clonazione di app Web con PowerShell](app-service-web-app-cloning.md)
* [Eseguire il backup di un'app Web nel servizio app di Azure](web-sites-backup.md)
* [Come tooCreate un ambiente del servizio App](app-service-web-how-to-create-an-app-service-environment.md)
* [Creare un'app Web in un ambiente del servizio app](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Introduzione tooApp ambiente del servizio](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
