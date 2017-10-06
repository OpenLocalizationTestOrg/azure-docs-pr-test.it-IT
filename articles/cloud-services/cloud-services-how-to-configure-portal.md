---
title: aaaHow tooconfigure un servizio cloud (portale) | Documenti Microsoft
description: Informazioni su come dei servizi cloud tooconfigure in Azure. Informazioni di configurazione del servizio cloud tooupdate hello e configurare accesso remoto toorole istanze. Questi esempi utilizzano hello portale di Azure.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: 969a08558473e8c79153192942bfda587eb5ada5
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

È possibile configurare le impostazioni di hello più comunemente usato per un servizio cloud nel portale di Azure hello. In alternativa, se si desidera tooupdate i file di configurazione direttamente, scaricare un tooupdate di file di configurazione del servizio e quindi caricare hello aggiornare file e aggiornamento hello servizio cloud con le modifiche alla configurazione di hello. In entrambi i casi, gli aggiornamenti della configurazione hello vengono inviati tooall le istanze del ruolo.

È inoltre possibile gestire le istanze di hello dei ruoli del servizio cloud o desktop remoto in essi.

Azure per garantire la disponibilità del servizio al 99,95% durante hello gli aggiornamenti della configurazione se si dispone di almeno due istanze del ruolo per ogni ruolo. Che consente una macchina virtuale tooprocess client richieste durante l'aggiornamento hello altri. Per altre informazioni, vedere [Contratti di servizio](https://azure.microsoft.com/support/legal/sla/).

## <a name="change-a-cloud-service"></a>Modificare un servizio cloud
Dopo l'apertura hello [portale di Azure](https://portal.azure.com/), passare servizio cloud tooyour. Da qui è possibile gestire molti aspetti.

![Pagina Impostazioni](./media/cloud-services-how-to-configure-portal/cloud-service.png)

Hello **impostazioni** o **tutte le impostazioni** collegamenti determina l'apertura dei hello **impostazioni** pannello in cui è possibile modificare hello **proprietà**, modificare hello **Configurazione**, gestire hello **certificati**, il programma di installazione **regole di avviso**e gestire hello **utenti** che dispongono dell'accesso toothis servizio cloud.

![Pannello delle impostazioni del servizio cloud di Azure](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a>Gestire la versione del sistema operativo guest

Per impostazione predefinita, Azure Aggiorna periodicamente il guest immagine del sistema operativo toohello più recenti supportate all'interno di hello famiglia di sistemi operativi specificati nella configurazione del servizio (con estensione cscfg), ad esempio Windows Server 2016.

Se è necessario tootarget una specifica versione del sistema operativo, è possibile impostare in hello **configurazione** blade.

![Configurare la versione del sistema operativo](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> La scelta di una versione specifica del sistema operativo comporta la disabilitazione degli aggiornamenti automatici del sistema operativo e rende l'applicazione di patch a carico dell'utente. È necessario assicurarsi che le istanze del ruolo ricezione degli aggiornamenti o potrebbe esporre le vulnerabilità toosecurity l'applicazione.

## <a name="monitoring"></a>Monitoraggio
È possibile aggiungere il servizio cloud tooyour di avvisi. Fare clic su **Impostazioni** > **Regole di avviso** > **Aggiungi avviso**.

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

Da qui è possibile configurare un avviso. Con hello **metrica** elenchi a discesa, è possibile configurare un avviso per hello seguenti tipi di dati.

* Lettura disco
* Scrittura disco
* Rete in ingresso
* Rete in uscita
* Percentuale CPU

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a>Configurazione del monitoraggio da un riquadro della metrica
Anziché utilizzare **impostazioni** > **le regole di avviso**, è possibile fare clic su uno dei riquadri di metrica hello in hello **monitoraggio** sezione di hello **Cloud servizio** blade.

![Monitoraggio del servizio cloud](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

Da qui è possibile personalizzare il grafico di hello utilizzato con il riquadro hello o aggiungere una regola di avviso.

## <a name="reboot-reimage-or-remote-desktop"></a>Riavviare il computer, ricreare l'immagine o creare una connessione Desktop remoto
In questo momento non è possibile configurare desktop remoto utilizzando hello **portale di Azure**. Tuttavia, è possibile configurarlo tramite hello [portale di Azure classico](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), o tramite [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).

Fare clic sull'istanza di servizio cloud hello.

![Istanza del servizio cloud](./media/cloud-services-how-to-configure-portal/cs-instance.png)

Da hello pannello visualizzato è possibile avviare una connessione desktop remoto, riavviare in remoto hello istanza o in modalità remota istanza hello ricreazione dell'immagine (inizia con un'immagine aggiornata).

![Pulsanti di istanza del servizio cloud](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a>Riconfigurare il file con estensione cscfg
Potrebbe essere necessario tooreconfigure il servizio cloud tramite hello [configurazione del servizio (cscfg)](cloud-services-model-and-package.md#cscfg) file. È necessario innanzitutto toodownload il file con estensione cscfg del file, modificarlo e caricarlo.

1. Fare clic su hello **impostazioni** icona o hello **tutte le impostazioni** collegamento tooopen backup hello **impostazioni** blade.

    ![Pagina Impostazioni](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. Fare clic su hello **configurazione** elemento.

    ![Blade Configurazione](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. Fare clic su hello **scaricare** pulsante.

    ![Scaricare](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. Dopo aver aggiornato il file di configurazione servizio hello, caricare e applicare gli aggiornamenti della configurazione hello:

    ![Carica](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. Selezionare i file con estensione cscfg hello e fare clic su **OK**.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[distribuire un servizio cloud](cloud-services-how-to-create-deploy-portal.md).
* Configurare un [nome di dominio personalizzato](cloud-services-custom-domain-name-portal.md).
* [Gestire il servizio cloud](cloud-services-how-to-manage-portal.md).
* Configurare i [certificati ssl](cloud-services-configure-ssl-certificate-portal.md).
