---
title: problemi di Gateway di gestione dati aaaTroubleshoot | Documenti Microsoft
description: Fornisce suggerimenti tootroubleshoot problemi correlati tooData Gateway di gestione.
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a>Risolvere i problemi nell'uso del gateway di gestione dati
Questo articolo offre informazioni sulla risoluzione dei problemi nell'uso del gateway di gestione dati.

> [!NOTE]
> Vedere hello [Gateway di gestione dati](data-factory-data-management-gateway.md) articolo per informazioni dettagliate sul gateway hello. Vedere hello [spostare i dati tra sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo per una procedura dettagliata di spostare i dati da un tooMicrosoft di database di SQL Server locale nell'archiviazione Blob di Azure tramite gateway hello.
>
>

## <a name="failed-tooinstall-or-register-gateway"></a>Gateway tooinstall o registrare non riuscito
### <a name="1-problem"></a>1. Problema
Viene visualizzato questo messaggio di errore durante l'installazione e la registrazione di un gateway, in particolare, durante il download dei file di installazione di gateway hello.

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a>Causa
macchina Hello in cui si sta tentando di gateway hello tooinstall non riuscita toodownload hello ultimo gateway file di installazione dall'area download hello a causa di problemi di rete tooa.

#### <a name="resolution"></a>Risoluzione
Verificare toosee di impostazioni del firewall proxy server se la connessione di rete hello da hello computer toohello il bambino hello [area download](https://download.microsoft.com/)e aggiornare le impostazioni di hello di conseguenza.

In alternativa, è possibile scaricare i file di installazione hello gateway più recente di hello da hello [area download](https://www.microsoft.com/download/details.aspx?id=39717) in altri computer che possono accedere area download hello. È possibile quindi gateway di toohello file di programma di installazione di copia hello computer host e lo si esegue manualmente gateway hello tooinstall e update.

### <a name="2-problem"></a>2. Problema
Questo errore viene visualizzato quando si tenta un gateway tooinstall facendo **installare direttamente in questo computer** in hello portale di Azure.

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a>Causa
Un gateway è già installato nel computer di hello.

#### <a name="resolution"></a>Risoluzione
Disinstallare hello gateway esistente nel computer di hello e fare clic su hello **installare direttamente in questo computer** collegare di nuovo.

### <a name="3-problem"></a>3. Problema
Questo errore può verificarsi quando si registra un nuovo gateway.

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a>Causa
Verrà visualizzato questo messaggio per uno dei seguenti motivi hello:

* formato Hello della chiave del gateway hello è valido.
* chiave del gateway Hello è stata invalidata.
* chiave del gateway Hello è stata rigenerata dal portale hello.  

#### <a name="resolution"></a>Risoluzione
Verificare se si utilizza una chiave di gateway corretto hello dal portale hello. Se è necessario rigenerare una chiave e utilizzare hello tooregister chiave hello gateway.

### <a name="4-problem"></a>4. Problema
È possibile visualizzare hello seguente messaggio di errore quando si sta registrando un gateway.

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![Il contenuto o il formato della chiave non è valido](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a>Causa
Hello contenuto o il formato della chiave del gateway input hello non è corretto. Uno dei motivi hello è possibile che solo una parte della chiave hello copiato dal portale hello o si usa una chiave non valida.

#### <a name="resolution"></a>Risoluzione
Generare una chiave del gateway nel portale di hello e utilizzare hello copia pulsante toocopy hello intera chiave. Quindi incollarlo in questo gateway di hello tooregister finestra.

### <a name="5-problem"></a>5. Problema
È possibile visualizzare hello seguente messaggio di errore quando si sta registrando un gateway.

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![La chiave del gateway non è valida oppure è vuota](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a>Causa
è stata rigenerata la chiave del gateway Hello o gateway hello è stato eliminato nel portale di Azure hello. Può inoltre verificarsi se il programma di installazione di hello Gateway di gestione dati non è più recente.

#### <a name="resolution"></a>Risoluzione
Controllare se l'installazione di Gateway di gestione dati hello è la versione più recente di hello, è possibile trovare la versione più recente di hello in hello Microsoft [area download](https://go.microsoft.com/fwlink/p/?LinkId=271260).

Se dell'installazione corrente / più recente e gateway esiste ancora nel portale, rigenerare la chiave di gateway hello in hello portale di Azure, utilizzare hello copia pulsante toocopy hello intera chiave e quindi incollarlo in questo gateway di hello tooregister finestra. In caso contrario, ricreare il gateway di hello e ricominciare.

### <a name="6-problem"></a>6. Problema
È possibile visualizzare hello seguente messaggio di errore quando si sta registrando un gateway.

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![La chiave del gateway non è valida oppure è vuota](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a>Causa
Questo errore potrebbe verificarsi perché hello gateway è stato eliminato o è stata rigenerata la chiave del gateway associato hello.

#### <a name="resolution"></a>Risoluzione
Se il gateway hello è stato eliminato, ricreare il gateway hello dal portale di hello, fare clic su **registrare**, copiare hello chiave dal portale di hello, incollare il codice e provare il gateway di hello tooregister.

Se il gateway hello esiste ancora, ma è stata rigenerata la chiave, usare hello nuova chiave tooregister hello gateway. Se non si dispone di chiave hello, rigenerare la chiave hello nuovamente dal portale di hello.

### <a name="7-problem"></a>7. Problema
Quando si sta registrando un gateway, potrebbe essere necessario tooenter percorso e la password di un certificato.

![Specificare un certificato](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a>Causa
Hello gateway è stato registrato in altri computer prima di. Durante la registrazione iniziale di hello del gateway, un certificato di crittografia è stato associato al gateway hello. certificato Hello può essere automatico generato dal gateway hello o specificato dall'utente hello.  Questo certificato è usato tooencrypt le credenziali dell'archivio dati hello (servizio collegato).  

![Esportare il certificato](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

Quando il ripristino di gateway hello in un computer host diverso, hello registrazione guidata per questo toodecrypt certificato credenziali precedentemente crittografati con questo certificato.  Senza questo certificato, credenziali hello non possono essere decrittografate dal nuovo gateway hello e associate a questo nuovo gateway esecuzioni di attività di copia successive avranno esito negativo.  

#### <a name="resolution"></a>Risoluzione
Se è stata esportata certificato delle credenziali hello dal computer gateway originale hello utilizzando hello **esportare** pulsante hello **impostazioni** scheda in Data Management Gateway Configuration Manager, utilizzare hello certificato.

Non è possibile ignorare questo passaggio quando si recupera un gateway. Se il certificato di hello è presente, è necessario toodelete hello gateway dal portale hello e ricreare un nuovo gateway.  Inoltre, aggiornare tutti i servizi collegati che sono correlati toohello gateway da reinserimento le proprie credenziali.

### <a name="8-problem"></a>8. Problema
È possibile visualizzare hello seguente messaggio di errore.

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a>Causa
Questo errore si verifica quando il gateway è in un ambiente che richiede un tooaccess proxy HTTP risorse Internet, o viene modificata la password di autenticazione del proxy, ma non viene aggiornata di conseguenza nel gateway.

#### <a name="resolution"></a>Risoluzione
Seguire le istruzioni hello hello [considerazioni sui server Proxy](#proxy-server-considerations) sezione di questo articolo e configurare le impostazioni del proxy con dati Gestione Gateway di Gestione configurazione.

## <a name="gateway-is-online-with-limited-functionality"></a>Il gateway è online con funzionalità limitate
### <a name="1-problem"></a>1. Problema
Verranno visualizzati lo stato di hello del gateway hello online con funzionalità limitate.

#### <a name="cause"></a>Causa
È visualizzato lo stato di hello del gateway hello online con funzionalità limitate per uno dei seguenti motivi hello:

* Gateway non è possibile connettersi toocloud servizio tramite il Bus di servizio di Azure.
* Servizio cloud non può connettersi toogateway tramite Bus di servizio.

Quando il gateway di hello è online con funzionalità limitate, potrebbe non essere in grado di toouse pipeline di dati toocreate di Data Factory Copia guidata hello per la copia dei dati tooor dagli archivi dati locali. In alternativa, è possibile utilizzare l'Editor delle Data Factory nel portale di hello, Visual Studio o Azure PowerShell.

#### <a name="resolution"></a>Risoluzione
Risoluzione di questo problema (online con funzionalità limitate) si basa sul se gateway hello non può connettersi toohello del servizio cloud o hello altro modo. Hello le sezioni seguenti fornisce queste risoluzioni.

### <a name="2-problem"></a>2. Problema
Viene visualizzato il seguente errore hello.

`Error: Gateway cannot connect toocloud service through service bus`

![Gateway non è possibile connettersi toocloud servizio](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a>Causa
Gateway non è possibile connettersi servizio cloud toohello tramite Bus di servizio.

#### <a name="resolution"></a>Risoluzione
Seguire un gateway a questi hello tooget di passaggi in linea:

1. Consenti indirizzi IP regole in uscita sul computer del gateway hello e firewall aziendale hello. È possibile trovare gli indirizzi IP dal registro eventi di Windows hello (ID = = 401): è stato eseguito un tentativo effettuato tooaccess un socket in modo non è consentito dalle relative autorizzazioni di accesso XX. XX. XX. XX:9350.
* Configurare le impostazioni proxy nel gateway hello. Vedere hello [considerazioni sui server Proxy](#proxy-server-considerations) sezione per informazioni dettagliate.
* Abilitare le porte in uscita 5671 e 9350-9354 su entrambi hello Windows Firewall nel computer del gateway hello e firewall aziendale hello. Vedere hello [porte e firewall](#ports-and-firewall) sezione per informazioni dettagliate. Questo passaggio è facoltativo, ma consigliato per considerazioni relative alle prestazioni.

### <a name="3-problem"></a>3. Problema
Viene visualizzato il seguente errore hello.

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a>Causa
Errore temporaneo nella connettività di rete.

#### <a name="resolution"></a>Risoluzione
Seguire un gateway a questi hello tooget di passaggi in linea:

1. Attendere un paio di minuti, la connettività di hello verrà ripristinata automaticamente quando non viene più visualizzato errore hello.
* Se hello errore persiste, riavviare il servizio gateway hello.

## <a name="failed-tooauthor-linked-service"></a>Servizio non riuscite tooauthor collegato
### <a name="problem"></a>Problema
Si potrebbe essere visualizzato questo errore quando si tenta di toouse Gestione credenziali le credenziali di portale tooinput hello per un servizio collegato di nuovo o aggiornare le credenziali per un servizio collegato esistente.

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

Quando viene visualizzato questo errore, pagina Impostazioni hello di Data Management Gateway Configuration Manager potrebbe essere simile hello seguente schermata.

![Impossibile raggiungere il database](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a>Causa
certificato SSL Hello possibile abbia perso nel computer gateway hello. Impossibile caricare il computer gateway Hello hello certificato attualmente utilizzato per la crittografia SSL. È inoltre potrebbe essere visualizzato un messaggio di errore nel registro eventi di hello che è simile toohello seguente messaggio.

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a>Risoluzione
Seguire questi problema hello toosolve di passaggi:

1. Avviare Gestione configurazione di Gateway di gestione dati.
2. Passare toohello **impostazioni** scheda.  
3. Fare clic su hello **modifica** certificato SSL di hello toochange pulsante.

   ![Pulsate Cambia per cambiare il certificato](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. Selezionare un nuovo certificato come certificato SSL hello. È possibile usare qualsiasi certificato SSL generato dall'utente o da qualsiasi organizzazione.

   ![Specificare un certificato](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a>L'attività di copia ha esito negativo
### <a name="problem"></a>Problema
È possibile riscontrare hello seguito a un errore di "UserErrorFailedToConnectToSqlserver" dopo aver impostato una pipeline nel portale di hello.

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a>Causa
Questo problema può verificarsi per diversi motivi e la mitigazione varia di conseguenza.

#### <a name="resolution"></a>Risoluzione
Consentire le connessioni TCP in uscita sulla porta TCP/1433 sul lato client di Gateway di gestione dati hello prima della connessione di database SQL tooan.

Se il database di destinazione hello è un database SQL di Azure, verificare SQL Server impostazioni del firewall per Azure nonché.

Vedere hello seguendo l'archivio di dati di sezione tootest hello connessione toohello locale.

## <a name="data-store-connection-or-driver-related-errors"></a>Errori correlati alla connessione all'archivio dati o al driver
Se i dati visualizzati archiviare connessione o errori correlati al driver, completare hello alla procedura seguente:

1. Avviare Gestione configurazione di Gateway di gestione di dati nel computer gateway hello.
2. Passare toohello **diagnostica** scheda.
3. In **Test connessione**, aggiungere i valori del gruppo gateway hello.
4. Fare clic su **Test** toosee se è possibile connettersi toohello locale origine dati dal computer del gateway hello utilizzando le informazioni di connessione hello e le credenziali. Se la connessione di prova hello non riesce dopo aver installato un driver, riavvio hello gateway per tale toopick modifica più recente di hello.

![Test connessione nella scheda Diagnostica](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a>Log del gateway
### <a name="send-gateway-logs-toomicrosoft"></a>Inviare tooMicrosoft registri gateway
Quando si contatta Guida tooget supporto alla risoluzione dei problemi del gateway, potrebbe essere necessario tooshare i registri del gateway. Con la versione di hello del gateway hello, è possibile condividere i log necessari gateway con due pulsanti in Data Management Gateway Configuration Manager.    

1. Passare toohello **diagnostica** scheda in Data Management Gateway Configuration Manager.

    ![Gateway di gestione dati - Scheda Diagnostica](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. Fare clic su **inviare i log** hello toosee seguendo la finestra di dialogo.

    ![Gateway di gestione dati - Invia log](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. (Facoltativo) Fare clic su **visualizzare log** tooreview registra nel Visualizzatore eventi hello.
4. (Facoltativo) Fare clic su **privacy** informativa sulla privacy dei servizi web di Microsoft tooreview.
5. Quando si è soddisfatti cosa si sta tooupload, fare clic su **inviare i log** tooactually inviare i log di hello dal hello ultimi sette giorni tooMicrosoft per la risoluzione dei problemi. Stato di hello dell'operazione di invio log hello verrà visualizzato come illustrato nella seguente schermata hello.

    ![Gateway di gestione dati - Stato dell'operazione Invia log](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. Al termine operazione hello, come illustrato nella seguente schermata hello è visualizzata una finestra di dialogo.

    ![Gateway di gestione dati - Stato dell'operazione Invia log](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. Salvare hello **ID Report** e condividerlo con il supporto Microsoft. ID report Hello è toolocate utilizzati registri del gateway hello caricato per la risoluzione dei problemi.  ID report Hello viene salvato anche nel Visualizzatore eventi hello.  È possibile trovarlo esaminando l'ID evento hello "25" e verificare hello data e ora.

    ![Gateway di gestione dati - ID report dell'operazione Invia log](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a>Archiviare i log del gateway nel computer host del gateway
Esistono dei casi in cui si verificano problemi con il gateway e non è possibile condividere direttamente i log del gateway:

* Installare il gateway hello manualmente e registrare il gateway hello.
* Si tenta di gateway hello tooregister con una chiave rigenerata in Data Management Gateway Configuration Manager.
* Si tenta di registri toosend e non è possibile connettere il servizio host di hello gateway.

In questi casi, è possibile salvare i log del gateway come file zip e condividerlo quando si contatta il supporto Microsoft. Ad esempio, se viene visualizzato un errore mentre si registra il gateway hello come illustrato nella seguente schermata hello.   

![Gateway di gestione dati - Errore di registrazione](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

Fare clic su hello **archiviare log gateway** collegamento tooarchive e salvare i registri e quindi di condividere file con estensione zip hello con il supporto tecnico Microsoft.

![Gateway di gestione dati - Archivia log](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a>Trovare i log del gateway
Per informazioni dettagliate gateway log nei registri eventi di Windows hello.

1. Avviare il **Visualizzatore eventi** di Windows.
2. Individuare i log in hello **registri applicazioni e servizi** > **Gateway di gestione dati** cartella.

 Quando si sta risolvendo problemi relativi al gateway, cercare gli eventi a livello di errore nel Visualizzatore eventi hello.

![Gateway di gestione dati - Log nel Visualizzatore eventi](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
