---
title: aaaHow toocreate e distribuire un servizio cloud | Documenti Microsoft
description: Informazioni su come toocreate e distribuire un servizio cloud con hello portale di Azure.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: dc8b81a594f3514e662c49c9a46a33da8a551f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a>Come toocreate e distribuire un servizio cloud
> [!div class="op_single_selector"]
> * [Portale di Azure](cloud-services-how-to-create-deploy-portal.md)
> * [portale di Azure classico](cloud-services-how-to-create-deploy.md)
>
>

sono disponibili due metodi per l'utente toocreate Hello portale di Azure e distribuire un servizio cloud: *creazione rapida* e *creazione personalizzata*.

Questo articolo viene illustrato come toouse hello creazione rapida metodo toocreate un nuovo servizio cloud e quindi utilizzare **caricare** tooupload e distribuire un pacchetto del servizio cloud in Azure. Quando si utilizza questo metodo, hello portale di Azure rende disponibili utili collegamenti per il completamento di tutti i requisiti man mano. Se si è pronti toodeploy durante la creazione del servizio cloud, è possibile eseguire sia hello contemporaneamente utilizzando creazione personalizzata.

> [!NOTE]
> Se si intende toopublish il servizio cloud da Visual Studio Team Services (VSTS), usare creazione rapida e quindi impostare la pubblicazione di Visual Studio Team Services dal dashboard di avvio rapido di Azure o hello hello. Per ulteriori informazioni, vedere [tooAzure la distribuzione continua da utilizzando Visual Studio Team Services][TFSTutorialForCloudService], vedere la Guida per hello o **avvio rapido** pagina.
>
>

## <a name="concepts"></a>Concetti
Tre componenti sono necessari toodeploy un'applicazione come servizio cloud in Azure:

* **Definizione del servizio**  
  file di definizione del servizio cloud Hello (con estensione csdef) definisce il modello di servizio hello, incluso il numero di hello dei ruoli.
* **Configurazione del servizio**  
  file di configurazione del servizio cloud Hello (. cscfg) fornisce le impostazioni di configurazione per servizio cloud hello e singoli ruoli, tra cui hello numero di istanze del ruolo.
* **Pacchetto del servizio**  
  pacchetto del servizio Hello (con estensione cspkg) contiene il codice dell'applicazione hello e le configurazioni e file di definizione del servizio hello.

Sono disponibili ulteriori informazioni su questi e in che modo un pacchetto toocreate [qui](cloud-services-model-and-package.md).

## <a name="prepare-your-app"></a>Preparare l'app
Prima di poter distribuire un servizio cloud, è necessario creare pacchetto del servizio cloud hello (con estensione cspkg) dal codice dell'applicazione e un file di configurazione del servizio cloud (. cscfg). Hello Azure SDK sono disponibili strumenti per la preparazione di questi file di distribuzione necessarie. È possibile installare SDK hello hello [download di Azure](https://azure.microsoft.com/downloads/) pagina, nella lingua hello in cui si preferisce toodevelop il codice dell'applicazione.

Per poter esportare un pacchetto di servizio, è necessario configurare tre funzionalità del servizio cloud:

* Se si desidera che un servizio cloud che utilizza Secure Sockets Layer (SSL) per la crittografia dei dati, toodeploy [configurare l'applicazione](cloud-services-configure-ssl-certificate-portal.md#modify) per SSL.
* Se si desidera tooconfigure istanze di toorole connessioni Desktop remoto, [configurare ruoli hello](cloud-services-role-enable-remote-desktop-new-portal.md) per Desktop remoto.
* Se si desidera tooconfigure dettagliato di monitoraggio per il servizio cloud, abilitare la diagnostica di Azure per il servizio cloud hello. *Monitoraggio minimo* (impostazione predefinita hello monitoraggio livello) usa i contatori delle prestazioni raccolti dai sistemi operativi host di hello per le istanze del ruolo (macchine virtuali). *Monitoraggio dettagliato* raccoglie le metriche aggiuntive basate sui dati delle prestazioni all'interno di hello ruolo istanze tooenable analisi ravvicinata dei problemi che si verificano durante l'elaborazione dell'applicazione. toofind come tooenable diagnostica di Azure, vedere [abilitazione di diagnostica Azure](cloud-services-dotnet-diagnostics.md).

toocreate un servizio cloud con distribuzioni di ruoli web o ruoli di lavoro, è necessario [Crea pacchetto del servizio hello](cloud-services-model-and-package.md#servicepackagecspkg).

## <a name="before-you-begin"></a>Prima di iniziare
* Se non è stato installato hello Azure SDK, fare clic su **installare Azure SDK** tooopen hello [pagina di download di Azure](https://azure.microsoft.com/downloads/)e quindi scaricare hello SDK per la lingua di hello in cui si preferisce toodevelop il codice. (Sarà necessario questo toodo un'opportunità in un secondo momento.)
* Se tutte le istanze di ruolo richiedono un certificato, è possibile creare certificati hello. I servizi cloud richiedono un file con estensione pfx con una chiave privata. È possibile caricare hello certificati tooAzure come creare e distribuire il servizio di cloud hello.

## <a name="create-and-deploy"></a>Creazione e distribuzione
1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Fare clic su **nuovo > calcolo**e quindi scorrere verso il basso fare clic su tooand **servizio Cloud**.

    ![Pubblicare il servizio cloud](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. Nella nuova hello **servizio Cloud** pannello, immettere un valore per hello **nome DNS**.
4. Creare un nuovo **Gruppo di risorse** o selezionarne uno esistente.
5. Selezionare un **percorso**.
6. Fare clic su **Pacchetto**. Verrà aperta hello **caricare un pacchetto** blade. Compilare i campi necessario hello. Se sono presenti ruoli contenenti una singola istanza, assicurarsi che l'opzione **Distribuisci anche se uno o più ruoli contengono una singola istanza** sia selezionata.
7. Assicurarsi che l'opzione **Avvia distribuzione** sia selezionata.
8. Fare clic su **OK** verranno chiusi hello **caricare un pacchetto** blade.
9. Se non si dispone di qualsiasi tooadd certificati, fare clic su **crea**.

    ![Pubblicare il servizio cloud](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a>Caricamento di un certificato
Se il pacchetto di distribuzione è stata [configurato i certificati toouse](cloud-services-configure-ssl-certificate-portal.md#modify), è possibile caricare il certificato di hello ora.

1. Selezionare **certificati**e in hello **aggiungere certificati** pannello selezionare file pfx del certificato SSL hello e quindi fornire hello **Password** certificato hello,
2. Fare clic su **certificato Connetti**, quindi fare clic su **OK** su hello **aggiungere certificati** blade.
3. Fare clic su **crea** su hello **servizio Cloud** blade. Quando la distribuzione di hello ha raggiunto hello **pronto** stato, è possibile procedere toohello passaggi.

    ![Pubblicare il servizio cloud](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a>Verificare che la distribuzione sia stata completata correttamente
1. Scegliere l'istanza del servizio cloud hello.

    Hello stato risulterà che servizio hello è **esecuzione**.
2. In **Essentials**, fare clic su hello **URL del sito** tooopen del servizio cloud in un web browser.

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a>Passaggi successivi
* [Configurazione generale del servizio cloud](cloud-services-how-to-configure-portal.md).
* Configurare un [nome di dominio personalizzato](cloud-services-custom-domain-name-portal.md).
* [Gestire il servizio cloud](cloud-services-how-to-manage-portal.md).
* Configurare i [certificati ssl](cloud-services-configure-ssl-certificate-portal.md).
