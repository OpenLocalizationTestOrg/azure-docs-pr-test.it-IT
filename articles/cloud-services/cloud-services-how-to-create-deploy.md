---
title: aaaHow toocreate e distribuire un servizio cloud | Documenti Microsoft
description: Informazioni su come toocreate e distribuire un servizio cloud usando il metodo di creazione rapida hello in Azure.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 0ea78ccc-5e7d-40f8-bdb6-478c0eb0e265
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 09f889f81ccee6e8a7657116183aa4100410214c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a>Come tooCreate e distribuire un servizio Cloud
> [!div class="op_single_selector"]
> * [Portale di Azure](cloud-services-how-to-create-deploy-portal.md)
> * [portale di Azure classico](cloud-services-how-to-create-deploy.md)
> 
> 

sono disponibili due metodi per l'utente toocreate Hello portale di Azure classico e distribuire un servizio cloud: **creazione rapida** e **creazione personalizzata**.

Questo argomento viene illustrato come toouse hello creazione rapida metodo toocreate un nuovo servizio cloud e quindi utilizzare **caricare** tooupload e distribuire un pacchetto del servizio cloud in Azure. Quando si utilizza questo metodo, hello portale di Azure classico rende disponibili utili collegamenti per il completamento di tutti i requisiti man mano. Se si è pronti toodeploy durante la creazione del servizio cloud, è possibile eseguire sia hello utilizzando **creazione personalizzata**.

> [!NOTE]
> Se si intende toopublish il servizio cloud da Visual Studio Team Services (VSTS), utilizzare **creazione rapida**e quindi impostare la pubblicazione di Visual Studio Team Services da **avvio rapido** o dashboard hello.
> 
> 

## <a name="concepts"></a>Concetti
In ordine toodeploy del servizio dell'applicazione in un cloud in Azure, sono necessari tre componenti:

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

* Se si desidera che un servizio cloud che utilizza Secure Sockets Layer (SSL) per la crittografia dei dati, toodeploy [configurare l'applicazione](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) per SSL.
* Se si desidera tooconfigure istanze di toorole connessioni Desktop remoto, [configurare ruoli hello](cloud-services-role-enable-remote-desktop.md) per Desktop remoto.
* Se si desidera tooconfigure dettagliato di monitoraggio per il servizio cloud, abilitare la diagnostica di Azure per il servizio cloud hello. *Monitoraggio minimo* (impostazione predefinita hello monitoraggio livello) usa i contatori delle prestazioni raccolti dai sistemi operativi host di hello per le istanze del ruolo (macchine virtuali). "Il monitoraggio dettagliato * raccoglie le metriche aggiuntive basate sui dati delle prestazioni all'interno di hello ruolo istanze tooenable analisi ravvicinata dei problemi che si verificano durante l'elaborazione dell'applicazione. toofind come tooenable diagnostica di Azure, vedere [abilitazione di diagnostica Azure](cloud-services-dotnet-diagnostics.md).

toocreate un servizio cloud con distribuzioni di ruoli web o ruoli di lavoro, è necessario [Crea pacchetto del servizio hello](cloud-services-model-and-package.md#servicepackagecspkg).

## <a name="before-you-begin"></a>Prima di iniziare
* Se non è stato installato hello Azure SDK, fare clic su **installare Azure SDK** tooopen hello [pagina di download di Azure](https://azure.microsoft.com/downloads/)e quindi scaricare hello SDK per la lingua di hello in cui si preferisce toodevelop il codice. (Sarà necessario questo toodo un'opportunità in un secondo momento.)
* Se tutte le istanze di ruolo richiedono un certificato, è possibile creare certificati hello. I servizi cloud richiedono un file con estensione pfx con una chiave privata. È possibile [caricare hello certificati tooAzure](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) come creare e distribuire il servizio di cloud hello.
* Se si prevede il gruppo di affinità tooan toodeploy hello cloud del servizio, creare il gruppo di affinità hello. È possibile utilizzare un gruppo di affinità di toodeploy il servizio cloud e toohello altri servizi di Azure stesso percorso in un'area. È possibile creare il gruppo di affinità hello in hello **reti** area del portale di Azure classico, in hello hello **gruppi di affinità** pagina.

## <a name="how-to-create-a-cloud-service-using-quick-create"></a>Procedura: Creare un servizio cloud con Creazione rapida
1. In hello [portale di Azure classico](http://manage.windowsazure.com/), fare clic su **New**>**calcolo**>**servizio Cloud** > **Creazione rapida**.
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_QuickCreate.png)
2. In **URL**, immettere un toouse nome di sottodominio in URL pubblico hello per l'accesso al servizio cloud nelle distribuzioni di produzione. formato URL Hello per le distribuzioni di produzione: http://*myURL*. cloudapp.net.
3. In **regione o gruppo di affinità**, selezionare hello geografica regione o gruppo di affinità toodeploy hello servizio cloud. Selezionare un gruppo di affinità, se si desidera toodeploy il toohello servizio cloud stessa posizione di altri servizi all'interno di un'area di Azure.
4. Fare clic su **Create Cloud Service**.
   
    ![CloudServices_Region](./media/cloud-services-how-to-create-deploy/CloudServices_Regionlist.png)
   
    È possibile monitorare lo stato di hello del processo di hello nell'area dei messaggi hello nella parte inferiore di hello della finestra hello.
   
    Hello **servizi Cloud** verrà visualizzata l'area, hello nuovo servizio cloud visualizzati. Quando lo stato di hello cambia tooCreated, creazione del servizio cloud è stata completata.
   
    ![CloudServices_CloudServicesPage](./media/cloud-services-how-to-create-deploy/CloudServices_CloudServicesPage.png)

## <a name="how-to-upload-a-certificate-for-a-cloud-service"></a>Procedura: Caricare un certificato per un servizio cloud
1. In hello [portale di Azure classico](http://manage.windowsazure.com/), fare clic su **servizi Cloud**, fare clic sul nome del servizio cloud hello hello e quindi fare clic su **certificati**.
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_EmptyDashboard.png)
2. Fare clic su **Carica un certificato** o su **Carica**.
3. In **File**, utilizzare **Sfoglia** certificato hello tooselect (file con estensione pfx).
4. In **Password**, immettere la chiave privata per il certificato di hello hello.
5. Fare clic su **OK** (segno di spunta).
   
    ![CloudServices_AddaCertificate](./media/cloud-services-how-to-create-deploy/CloudServices_AddaCertificate.png)
   
    È possibile controllare lo stato di avanzamento hello del caricamento hello nell'area dei messaggi hello, illustrato di seguito. Al termine del caricamento di hello, il certificato di hello viene aggiunto toohello tabella. Nell'area dei messaggi hello, fare clic sul messaggio hello tooclose OK.
   
    ![CloudServices_CertificateProgress](./media/cloud-services-how-to-create-deploy/CloudServices_CertificateProgress.png)

## <a name="how-to-deploy-a-cloud-service"></a>Procedura: Distribuire un servizio cloud
1. In hello [portale di Azure classico](http://manage.windowsazure.com/), fare clic su **servizi Cloud**, fare clic sul nome del servizio cloud hello hello e quindi fare clic su **Dashboard**.
2. Fare clic su **Carica una nuova distribuzione di produzione** o **Carica**.
3. In **etichetta distribuzione**, immettere un nome per la distribuzione di nuovi hello - ad esempio, MyCloudServicev4.
4. In **pacchetto**, utilizzare **Sfoglia** tooselect hello servizio pacchetto file (con estensione cspkg) toouse.
5. In **configurazione**, utilizzare **Sfoglia** servizio hello tooselect configurare toouse file (. cscfg).
6. Se il servizio di cloud hello includerà eventuali ruoli con una sola istanza, selezionare hello **Distribuisci anche se uno o più ruoli contengono una singola istanza** tooproceed distribuzione hello tooenable di casella di controllo.
   
    Azure può garantire pari al 99,95% accesso toohello cloud servizio durante gli aggiornamenti di manutenzione e il servizio solo se ogni ruolo dispone di almeno due istanze. Se necessario, è possibile aggiungere altre istanze di ruolo su hello **scala** pagina dopo la distribuzione del servizio cloud hello. Per altre informazioni, vedere [Contratti di servizio](https://azure.microsoft.com/support/legal/sla/).
7. Fare clic su **OK** distribuzione del servizio cloud hello toobegin (segno di spunta).
   
    ![CloudServices_UploadaPackage](./media/cloud-services-how-to-create-deploy/CloudServices_UploadaPackage.png)
   
    È possibile monitorare lo stato di hello della distribuzione hello nell'area dei messaggi hello. Fare clic su OK toohide messaggio.
   
    ![CloudServices_UploadProgress](./media/cloud-services-how-to-create-deploy/CloudServices_UploadProgress.png)

## <a name="verify-your-deployment-completed-successfully"></a>Verificare che la distribuzione sia stata completata correttamente
1. Fare clic su **Dashboard**.
   
    Hello stato risulterà che servizio hello è **esecuzione**.
2. In **riepilogo rapido**, fare clic su tooopen URL del sito di hello del servizio cloud in un web browser.
   
    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy/CloudServices_QuickGlance.png)


## <a name="next-steps"></a>Passaggi successivi
* [Configurazione generale del servizio cloud](cloud-services-how-to-configure.md).
* Configurare un [nome di dominio personalizzato](cloud-services-custom-domain-name.md).
* [Gestire il servizio cloud](cloud-services-how-to-manage.md).
* Configurare i [certificati ssl](cloud-services-configure-ssl-certificate.md).

