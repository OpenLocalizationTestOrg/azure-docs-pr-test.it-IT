---
title: aaaEnable connessione Desktop remoto per un ruolo in servizi Cloud di Azure | Documenti Microsoft
description: "La modalità di cloud di azure di tooconfigure connessioni desktop remoto tooallow all'applicazione di servizio"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: mmccrory
ms.openlocfilehash: 55d7043df571c2e88b04aa9ef01dc8ae1d6784f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a>Impostare una connessione Desktop remoto per un ruolo nei servizi cloud di Azure
> [!div class="op_single_selector"]
> * [Portale di Azure](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Portale di Azure classico](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

Desktop remoto consente desktop hello tooaccess di un ruolo in esecuzione in Azure. È possibile utilizzare un tootroubleshoot connessione Desktop remoto e diagnosticare i problemi dell'applicazione mentre è in esecuzione.

È possibile abilitare una connessione Desktop remoto nel ruolo durante lo sviluppo includendo i moduli di Desktop remoto hello nella definizione del servizio oppure è possibile scegliere tooenable Desktop remoto tramite hello estensione Desktop remoto. Hello approccio consigliato è toouse hello Desktop remoto estensione come è possibile abilitare Desktop remoto anche dopo la distribuzione di un'applicazione hello senza tooredeploy l'applicazione.

## <a name="configure-remote-desktop-from-hello-azure-portal"></a>Configurare Desktop remoto dal portale di Azure hello
portale di Azure Hello utilizza l'approccio di estensione Desktop remoto di hello in cui è possibile abilitare Desktop remoto anche dopo la distribuzione di un'applicazione hello. Hello **Desktop remoto** pannello per il servizio cloud consente tooenable Desktop remoto, account di amministratore locale modifica hello usata tooconnect toohello le macchine virtuali, certificato hello usati nell'autenticazione e imposta hello Data di scadenza.

1. Fare clic su **servizi Cloud**, fare clic sul nome del servizio cloud hello hello e quindi fare clic su **Desktop remoto**.

    ![Servizi cloud per Desktop remoto](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. Scegliere se si desidera tooenable Desktop remoto per un singolo ruolo o per tutti i ruoli, quindi modifica il valore di hello di hello selezione troppo**abilitato**.

3. Compilare i campi necessario hello per nome utente, password, scadenza e certificati.

    ![Servizi cloud per Desktop remoto](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > Tutte le istanze del ruolo verranno riavviate la prima volta che si abilita Desktop remoto e si fa clic su OK (segno di spunta). tooprevent un riavvio, la password di hello hello certificato tooencrypt utilizzato deve essere installato nel ruolo hello. un riavvio, tooprevent [caricare un certificato per il servizio cloud hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) e restituirne toothis finestra di dialogo.
   >
   >
3. In **ruoli**selezionare ruolo hello desiderato tooupdate **tutti** per tutti i ruoli.

4. Al termine degli aggiornamenti della configurazione, fare clic su **Salva**. Saranno necessari alcuni minuti prima che le istanze del ruolo siano pronti tooreceive connessioni.

## <a name="remote-into-role-instances"></a>Accedere in remoto alle istanze del ruolo
Dopo aver abilitato Desktop remoto per i ruoli di hello, è possibile avviare una connessione direttamente dal portale di Azure hello:

1. Fare clic su **istanze** tooopen hello **istanze** blade.
2. Selezionare un'istanza del ruolo per cui è configurato Desktop remoto.
3. Fare clic su **Connetti** toodownload un RDP file per l'istanza del ruolo hello.

    ![Servizi cloud per Desktop remoto](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. Fare clic su **aprire** e quindi **Connetti** toostart hello connessione Desktop remoto.

>[!NOTE]
> Se il servizio cloud si trova dietro a un gruppo, potrebbe essere necessario toocreate regole che consentano il traffico sulle porte **3389** e **20000**.  Desktop remoto usa la porta **3389**.  Le istanze del servizio cloud sono con carico bilanciato, pertanto non è possibile controllare direttamente quale tooconnect istanza di.  Hello *RemoteForwarder* e *RemoteAccess* gli agenti di gestire il traffico RDP e consentire hello client toosend un cookie RDP e specificare tooconnect una singola istanza di.  Hello *RemoteForwarder* e *RemoteAccess* agenti richiedono tale porta **20000*** aperto, che può essere bloccato se si dispone di un gruppo.

## <a name="additional-resources"></a>Risorse aggiuntive

[Come servizi Cloud tooConfigure](cloud-services-how-to-configure.md)
[domande frequenti - servizi Cloud Desktop remoto](cloud-services-faq.md)
