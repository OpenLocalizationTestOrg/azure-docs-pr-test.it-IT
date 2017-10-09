---
title: aaaHow tooconfigure un servizio cloud (portale classico) | Documenti Microsoft
description: Informazioni su come dei servizi cloud tooconfigure in Azure. Informazioni di configurazione del servizio cloud tooupdate hello e configurare accesso remoto toorole istanze.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4902f79d-ea91-41ca-89a4-7c818180ee5f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 1ea2320f97f667153f7984e4d61d373a6344cf6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a>Come tooConfigure dei servizi Cloud
> [!div class="op_single_selector"]
> * [Portale di Azure](cloud-services-how-to-configure-portal.md)
> * [portale di Azure classico](cloud-services-how-to-configure.md)
> 
> 

È possibile configurare le impostazioni di hello più comunemente usato per un servizio cloud nel portale di Azure classico hello. In alternativa, se si desidera tooupdate i file di configurazione direttamente, scaricare un tooupdate di file di configurazione del servizio e quindi caricare hello aggiornare file e aggiornamento hello servizio cloud con le modifiche alla configurazione di hello. In entrambi i casi, gli aggiornamenti della configurazione hello vengono inviati tooall le istanze del ruolo.

Hello portale di Azure classico consente inoltre troppo[abilitare connessione Desktop remoto per un ruolo in servizi Cloud di Azure](cloud-services-role-enable-remote-desktop.md)

Azure per garantire la disponibilità del servizio al 99,95% durante hello gli aggiornamenti della configurazione se si dispone di almeno due istanze del ruolo per ogni ruolo. Che consente una macchina virtuale tooprocess client richieste durante l'aggiornamento hello altri. Per altre informazioni, vedere [Contratti di servizio](https://azure.microsoft.com/support/legal/sla/).

## <a name="change-a-cloud-service"></a>Modificare un servizio cloud
1. In hello [portale di Azure classico](http://manage.windowsazure.com/), fare clic su **servizi Cloud**, fare clic sul nome del servizio cloud hello hello e quindi fare clic su **configura**.
   
    ![Pagina Configurazione](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage1.png)
   
    In hello **configura** pagina, è possibile configurare impostazioni di monitoraggio, aggiornamento ruolo e scegliere sistema operativo guest di hello e familiari per istanze del ruolo. 
2. In **monitoraggio**, hello set monitoraggio livello tooVerbose o minima e configurare stringhe di connessione di diagnostica hello necessari per il monitoraggio dettagliato.
3. Per i ruoli del servizio (raggruppati per ruolo), è possibile aggiornare hello seguenti impostazioni:
   
    * **Impostazioni** modificare i valori hello varie impostazioni di configurazione vengono specificate in hello *ConfigurationSettings* elementi hello servizio (. cscfg) del file di configurazione.

    * **Certificates**  
        Modifica hello identificazione personale del certificato utilizzato nella crittografia SSL per un ruolo. toochange un certificato, è necessario innanzitutto caricare nuovo certificato hello (su hello **certificati** pagina). Aggiornare quindi l'identificazione personale di hello nella stringa del certificato hello visualizzata nelle impostazioni di ruolo hello.
4. In **del sistema operativo**, è possibile modificare la famiglia di sistemi operativi hello o la versione per le istanze del ruolo o scegliere **automatica** tooenable aggiornamenti automatici della versione corrente del sistema operativo hello. impostazioni del sistema operativo Hello applicano tooweb ruoli o di lavoro, ma non influiscono le macchine virtuali.
   
    Durante la distribuzione, versione del sistema operativo più recente hello è installato in tutte le istanze di ruolo e i sistemi operativi hello vengono aggiornati automaticamente per impostazione predefinita. 
   
    Se è necessario per il toorun servizio cloud in una versione diversa del sistema operativo a causa dei requisiti di compatibilità del codice, è possibile scegliere una famiglia di sistemi operativi e la versione. Quando si sceglie una versione specifica del sistema operativo, aggiornamenti automatici del sistema operativo per il servizio cloud hello vengono sospesi. Sarà necessario tooensure sistemi operativi hello ricevere gli aggiornamenti.
   
    Se si risolve tutti i problemi di compatibilità con le app con una versione più recente del sistema operativo hello, è possibile abilitare gli aggiornamenti automatici del sistema operativo dalla versione del sistema operativo hello impostazione troppo**automatica**. 
   
    ![Impostazioni del sistema operativo](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage_OSSettings.png)
5. toosave le impostazioni di configurazione e inviarli toohello le istanze del ruolo, fare clic su **salvare**. (Fare clic su **annullare** modifiche hello toocancel.) **Salvare** e **annullare** vengono aggiunti toohello barra dei comandi dopo la modifica di un'impostazione.

## <a name="update-a-cloud-service-configuration-file"></a>Aggiornare il file di configurazione di un servizio cloud
1. Scaricare un file di configurazione di servizio (. cscfg) cloud con la configurazione corrente di hello. In hello **configura** pagina per il servizio cloud hello, fare clic su **scaricare**. Quindi fare clic su **salvare**, oppure fare clic su **Salva con nome** file hello toosave.
2. Dopo aver aggiornato il file di configurazione servizio hello, caricare e applicare gli aggiornamenti della configurazione hello:
   
   1. In hello **configura** pagina, fare clic su **caricare**.
      
       ![Caricamento della configurazione](./media/cloud-services-how-to-configure/CloudServices_UploadConfigFile.png)
   2. In **file di configurazione**, utilizzare **Sfoglia** tooselect hello aggiornati i file con estensione cscfg.
   3. Se il servizio cloud contiene i ruoli che hanno solo un'istanza, selezionare hello **applicare configurazione anche se uno o più ruoli contengono una singola istanza** casella di controllo tooenable hello gli aggiornamenti della configurazione per tooproceed ruoli hello.
      
       Se non si definiscono almeno due istanze di ogni ruolo, non è possibile garantire almeno il 99,95% di disponibilità del servizio cloud in Azure durante gli aggiornamenti della configurazione. Per altre informazioni, vedere [Contratti di servizio](https://azure.microsoft.com/support/legal/sla/).
   4. Fare clic su **OK** (segno di spunta). 

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[distribuire un servizio cloud](cloud-services-how-to-create-deploy.md).
* Configurare un [nome di dominio personalizzato](cloud-services-custom-domain-name.md).
* [Gestire il servizio cloud](cloud-services-how-to-manage.md).
* [Impostare una connessione Desktop remoto per un ruolo nei servizi cloud di Azure](cloud-services-role-enable-remote-desktop.md)
* Configurare i [certificati ssl](cloud-services-configure-ssl-certificate.md).

