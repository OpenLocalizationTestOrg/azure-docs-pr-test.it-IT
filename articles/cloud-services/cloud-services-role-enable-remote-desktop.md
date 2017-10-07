---
title: aaaEnable Desktop remoto in un servizio Cloud di Azure | Documenti Microsoft
description: "La modalità di cloud di azure di tooconfigure connessioni desktop remoto tooallow all'applicazione di servizio"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: d3110ee8-6526-4585-aba5-d0bc9a713e9b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: b3c0180bf5ad29cb77e5303ccbd6f9ccc44b7b0a
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

È possibile abilitare una connessione Desktop remoto nel ruolo durante lo sviluppo includendo i moduli di Desktop remoto hello nella definizione del servizio oppure è possibile scegliere tooenable Desktop remoto tramite hello estensione Desktop remoto. Hello approccio consigliato è toouse hello Desktop remoto estensione come è possibile abilitare Desktop remoto anche dopo la distribuzione di un'applicazione hello senza tooredeploy l'applicazione.

## <a name="configure-remote-desktop-from-hello-azure-classic-portal"></a>Configurare Desktop remoto dal portale di Azure classico hello
portale di Azure classico Hello utilizza l'approccio di estensione di Desktop remoto di hello in cui è possibile abilitare Desktop remoto anche dopo la distribuzione di un'applicazione hello. Hello **configura** pagina per il servizio cloud consente tooenable Desktop remoto, account di amministratore locale modifica hello usato tooconnect toohello le macchine virtuali, il certificato di hello usati nell'autenticazione e imposta hello Data di scadenza.

1. Fare clic su **servizi Cloud**, fare clic sul nome del servizio cloud hello hello e quindi fare clic su **configura**.
2. Fare clic su hello **remoto** pulsante nella parte inferiore di hello.

    ![Servizi cloud remoti](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > Tutte le istanze del ruolo verranno riavviate la prima volta che si abilita Desktop remoto e si fa clic su OK (segno di spunta). tooprevent un riavvio, la password di hello hello certificato tooencrypt utilizzato deve essere installato nel ruolo hello. un riavvio, tooprevent [caricare un certificato per il servizio cloud hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) e restituirne toothis finestra di dialogo.

3. In **ruoli**selezionare ruolo hello desiderato tooupdate **tutti** per tutti i ruoli.
4. Apportare le hello seguenti modifiche:

   * Desktop remoto, seleziona hello tooenable **Abilita Desktop remoto** casella di controllo. Desktop remoto, la casella di controllo crittografato hello toodisable.
   * Creare un account toouse nelle connessioni Desktop remoto istanze del ruolo toohello.
   * Aggiornare la password di hello per l'account esistente di hello.
   * Selezionare un toouse certificato caricato per l'autenticazione (caricamento hello certificato utilizzando **caricare** su hello **certificati** pagina) o creare un nuovo certificato.
   * Modificare la data di scadenza hello per la configurazione di Desktop remoto hello.

5. Dopo aver completato gli aggiornamenti della configurazione, fare clic su **OK** (segno di spunta).

## <a name="remote-into-role-instances"></a>Accedere in remoto alle istanze del ruolo
Dopo aver abilitato Desktop remoto per i ruoli di hello è possibile remota in un'istanza del ruolo tramite diversi strumenti.

istanza del ruolo tooa tooconnect dal portale di Azure classico hello:

1. Fare clic su **istanze** tooopen hello **istanze** pagina.
2. Selezionare un'istanza del ruolo per cui è configurato Desktop remoto.
3. Fare clic su **Connetti**e seguire desktop hello tooopen istruzioni di hello.
4. Fare clic su **aprire** e quindi **Connetti** toostart hello connessione Desktop remoto.

### <a name="use-visual-studio-tooremote-into-a-role-instance"></a>Utilizzare Visual Studio tooremote in un'istanza del ruolo
In Esplora server di Visual Studio:

1. Espandere hello **Azure** > **servizi Cloud** > **[nome servizio cloud]** nodo.
2. Espandere **Gestione temporanea** o **Produzione**.
3. Espandere i singoli ruoli di hello.
4. Fare doppio clic su una delle istanze del ruolo hello, fare clic su **connessione tramite Desktop remoto...** , quindi immettere nome utente hello e una password.

![Desktop remoto di Esplora server](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-tooget-hello-rdp-file"></a>Utilizzare PowerShell tooget hello RDP file
È possibile utilizzare hello [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) file RDP hello tooretrieve di cmdlet. È quindi possibile utilizzare il file RDP hello con servizio cloud di hello tooaccess connessione Desktop remoto.

### <a name="programmatically-download-hello-rdp-file-through-hello-service-management-rest-api"></a>A livello di codice, scaricare file RDP hello tramite hello API REST di gestione
È possibile utilizzare hello [scaricare il File RDP](https://msdn.microsoft.com/library/jj157183.aspx) file con estensione RDP hello toodownload operazione REST.

## <a name="tooconfigure-remote-desktop-in-hello-service-definition-file"></a>Desktop remoto nel file di definizione del servizio hello tooconfigure
Questo metodo consente tooenable Desktop remoto per un'applicazione hello durante lo sviluppo. Questo approccio richiede password crittografate da archiviare nella configurazione del servizio file e qualsiasi configurazione di desktop remoto di aggiornamenti toohello richiederebbe una ridistribuzione di un'applicazione hello. Se si desidera tooavoid questi svantaggi, è necessario utilizzare l'estensione di desktop remoto hello basato approccio descritto in precedenza.  

È possibile utilizzare Visual Studio troppo[abilitare una connessione desktop remoto](../vs-azure-tools-remote-desktop-roles.md) utilizzando l'approccio file di definizione del servizio hello.  
Hello riportato di seguito viene descritta la hello le modifiche necessarie toohello servizio modello file tooenable desktop remoto. Visual Studio eseguirà automaticamente queste modifiche durante la pubblicazione.

### <a name="set-up-hello-connection-in-hello-service-model"></a>Impostare la connessione di hello nel modello di servizio hello
Hello utilizzare **importazioni** hello tooimport elemento **RemoteAccess** modulo e hello **RemoteForwarder** modulo toohello [Servicedefinition](cloud-services-model-and-package.md#csdef) file.

Hello file di definizione del servizio deve essere simile toohello seguente esempio con hello `<Imports>` elemento aggiunto.

```xml
<ServiceDefinition name="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2013-03.2.0">
    <WebRole name="WebRole1" vmsize="Small">
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="Endpoint1" endpointName="Endpoint1" />
                </Bindings>
            </Site>
        </Sites>
        <Endpoints>
            <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
            <Import moduleName="Diagnostics" />
            <Import moduleName="RemoteAccess" />
            <Import moduleName="RemoteForwarder" />
        </Imports>
    </WebRole>
</ServiceDefinition>
```
Hello [ServiceConfiguration. cscfg](cloud-services-model-and-package.md#cscfg) file deve essere simile toohello seguente esempio, si noti hello `<ConfigurationSettings>` e `<Certificates>` elementi. Hello certificato specificato deve essere [caricato servizio cloud toohello](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2013-03.2.0">
    <Role name="WebRole1">
        <Instances count="2" />
        <ConfigurationSettings>
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.Enabled" value="true" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountUsername" value="[name-of-user-account]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountEncryptedPassword" value="[base-64-encrypted-user-password]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountExpiration" value="[certificate-expiration]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteForwarder.Enabled" value="true" />
        </ConfigurationSettings>
        <Certificates>
            <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="[certificate-thumbprint]" thumbprintAlgorithm="sha1" />
        </Certificates>
    </Role>
</ServiceConfiguration>
```


## <a name="additional-resources"></a>Risorse aggiuntive
[Come servizi Cloud tooConfigure](cloud-services-how-to-configure.md)
[domande frequenti - servizi Cloud Desktop remoto](cloud-services-faq.md)
