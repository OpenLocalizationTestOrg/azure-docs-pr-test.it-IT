---
title: "disponibilità aaaHigh con gateway di gestione di dati in Data Factory di Azure | Documenti Microsoft"
description: "Questo articolo illustra come è possibile aumentare il numero di istanze di un gateway di gestione dati aggiungendo altri nodi e aumentare le prestazioni accrescendo il numero di processi simultanei che possono essere eseguiti in un nodo."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: abnarain
ms.openlocfilehash: 925f63728e23596bca2655636f6535b509fce0b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway---high-availability-and-scalability-preview"></a>Gateway di gestione dati: disponibilità elevata e scalabilità (anteprima)
Questo articolo consente di configurare una soluzione di disponibilità elevata e scalabilità con Gateway di gestione dati.    

> [!NOTE]
> Questo articolo presuppone che l'utente abbia già familiarità con i concetti di base relativi a Gateway di gestione dati. In caso contrario, vedere [Gateway di gestione dati](data-factory-data-management-gateway.md).

>**Questa funzionalità di anteprima è ufficialmente supportata in Gateway di gestione dati versione 2.12.xxxx.x e successive**. Assicurarsi quindi che sia in uso la versione 2.12.xxxx.x o successiva. Scaricare una versione più recente di hello del Gateway di gestione dati [qui](https://www.microsoft.com/download/details.aspx?id=39717).

## <a name="overview"></a>Panoramica
È possibile associare i gateway di gestione di dati che vengono installati in più computer locale con un singolo gateway logico dal portale hello. Questi computer sono chiamati **nodi**. Possono esistere fino a troppo**quattro nodi** associata a un gateway logico. vantaggi di Hello di disporre di più nodi (computer locale con installato il gateway) per un gateway logico sono:  

- Migliorare le prestazioni dello spostamento dati tra archivi dati locali e cloud.  
- Se uno dei nodi hello Arresta per qualche motivo, gli altri nodi sono ancora disponibili per lo spostamento dei dati di hello. 
- Se uno dei nodi hello necessario toobe in linea per manutenzione, gli altri nodi sono ancora disponibili per lo spostamento dei dati di hello.

È inoltre possibile configurare il numero di hello di **processi lo spostamento dei dati simultanei** che è possibile eseguire su un nodo tooscale la funzionalità di spostamento dei dati tra sedi locali e cloud di hello archivi dati. 

Utilizzando hello portale di Azure, è possibile monitorare lo stato di hello di tali nodi, che consente di decidere se tooadd o rimuovere un nodo da gateway logico hello. 

## <a name="architecture"></a>Architettura 
Hello seguente diagramma fornisce cenni preliminari sull'architettura di hello di scalabilità e funzionalità di disponibilità di hello Gateway di gestione dati: 

![Gateway di gestione dati: disponibilità elevata e scalabilità](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-high-availability-and-scalability.png)

Oggetto **gateway logico** è gateway hello aggiuntivo tooa data factory di hello portale di Azure. Prima era possibile associare a un gateway logico un solo computer Windows locale con Gateway di gestione dati installato. Questo computer gateway locale è detto nodo. A questo punto, è possibile associare i troppo**quattro nodi fisici** con un gateway logico. Un gateway logico con più nodi è detto **gateway multinodo**.  

Tutti questi nodi sono **attivi**. Tutti possono elaborare i dati lo spostamento dei processi toomove dati tra sedi locali e cloud archivi dati. Uno dei nodi hello fungono da dispatcher e di lavoro. Gli altri nodi gruppi hello sono nodi di lavoro. Oggetto **dispatcher** nodo effettua il pull attività o processi lo spostamento dei dati dal servizio cloud hello e li invia nodi tooworker (incluso se stesso). Oggetto **lavoro** nodo esegue lo spostamento dei processi toomove dati tra sedi locali e cloud archivi dati. Tutti i nodi sono ruoli di lavoro. Solo un nodo può essere sia dispatcher che ruolo di lavoro.    

È in genere può iniziare con un nodo e **scalabilità** tooadd più nodi come hello nodi esistenti sono sovraccaricati con hello caricamento lo spostamento dei dati. È anche possibile **scalabilità verticale** hello funzionalità lo spostamento dei dati di un nodo di gateway aumentando il numero di hello di processi simultanei consentiti toorun nel nodo hello. Questa funzionalità è disponibile anche con un gateway a nodo singolo (anche quando non è abilitato funzionalità di scalabilità e disponibilità hello). 

Un gateway con più nodi mantiene la sincronizzazione delle credenziali dell'archivio dati hello in tutti i nodi. Se si verifica un problema di connettività da nodo a nodo, le credenziali di hello possono essere sincronizzate. Quando si impostano le credenziali per un archivio dati locale che utilizza un gateway, Salva le credenziali nel nodo di hello dispatcher/di lavoro. Hello dispatcher nodo esegue la sincronizzazione con altri nodi di lavoro. Questo processo è noto come **credenziali sincronizzazione**. il canale di comunicazione hello tra i nodi può essere **crittografati** da un certificato SSL/TLS pubblico. 

## <a name="set-up-a-multi-node-gateway"></a>Configurare un gateway multinodo
Questa sezione si presuppone che sia già stata consultata hello seguente due articoli o che hanno familiarità con concetti negli articoli seguenti: 

- [Gateway di gestione dati](data-factory-data-management-gateway.md) -fornisce una panoramica dettagliata del gateway hello.
- [Spostare dati tra archivi dati locali e cloud](data-factory-move-data-between-onprem-and-cloud.md): contiene una procedura dettagliata con le istruzioni per usare un gateway a nodo singolo.  

> [!NOTE]
> Prima di installare un gateway di gestione di dati in un computer di Windows locale, vedere i prerequisiti elencati in [articolo principale hello](data-factory-data-management-gateway.md#prerequisites).

1. In hello [procedura dettagliata](data-factory-move-data-between-onprem-and-cloud.md#create-gateway), durante la creazione di un gateway logico, abilitare hello **scalabilità e disponibilità elevata** funzionalità. 

    ![Gateway di gestione dati: abilitare disponibilità elevata e scalabilità](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-enable-high-availability-scalability.png)
2. In hello **configura** pagina, utilizzare una **Express Setup** o **l'installazione manuale** collegamento tooinstall un gateway nel primo nodo di hello (un computer Windows locale).

    ![Gateway di gestione dati: installazione rapida o manuale](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-express-manual-setup.png)

    > [!NOTE]
    > Se si utilizza l'opzione di installazione rapida di hello, comunicazione da nodo a nodo hello viene eseguita senza crittografia. nome del nodo Hello è uguale al nome di computer hello. Se le comunicazioni tra nodi hello deve toobe crittografata o si desidera toospecify un nome di nodo di propria scelta, è necessario utilizzare l'installazione manuale. I nomi di nodo non possono essere modificati in un secondo momento.
3. Se si sceglie **Installazione rapida**
    1. Vedrai hello segue messaggio dopo l'installazione di gateway hello:

        ![Gateway di gestione dati: installazione rapida completata](media/data-factory-data-management-gateway-high-availability-scalability/express-setup-success.png)
    2. Avviare Gestione configurazione di gestione di dati per il gateway hello seguendo [queste istruzioni](data-factory-data-management-gateway.md#configuration-manager). Vedrai il nome del gateway hello, nome del nodo, lo stato e così via.

        ![Gateway di gestione dati: installazione completata](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-installation-success.png)
4. Se si sceglie **Installazione manuale**:
    1. Scaricare il pacchetto di installazione di hello da Microsoft Download Center hello, eseguirlo tooinstall gateway nel computer.
    2. Hello utilizzare **chiave di autenticazione** da hello **configura** gateway hello tooregister di pagina.
    
        ![Gateway di gestione dati: installazione completata](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-authentication-key.png)
    3. In hello **nuovo nodo gateway** pagina, è possibile fornire un oggetto personalizzato **nome** nodo gateway toohello. Per impostazione predefinita, il nome del nodo è uguale al nome di computer hello.    

        ![Gateway di gestione dati: specificare un nome](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-name.png)
    4. Nella pagina successiva di hello, è possibile scegliere se troppo**abilitare la crittografia per la comunicazione da nodo a nodo**. Fare clic su **Skip** crittografia toodisable (impostazione predefinita).

        ![Gateway di gestione dati: abilitare la crittografia](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-node-encryption.png)  
    
        > [!NOTE]
        > Modifica della modalità di crittografia è supportata solo quando si dispone di un nodo singolo gateway in gateway logico hello. modalità di crittografia hello toochange quando un gateway con più nodi, hello i passaggi seguenti: eliminare tutti i nodi di hello ad eccezione di un nodo, modificare la modalità di crittografia hello e quindi aggiungere di nuovo i nodi di hello.
        > 
        > Per un elenco dei requisiti per l'uso di un certificato TLS/SSL, vedere la sezione [Requisiti dei certificati TLS/SSL](#tlsssl-certificate-requirements). 
    5. Gateway hello viene completata l'installazione, fare clic su Avvia Gestione configurazione:
    
        ![Installazione manuale: avviare Gestione configurazione](media/data-factory-data-management-gateway-high-availability-scalability/manual-setup-launch-configuration-manager.png)   
    6. vedere Gestione configurazione di Gateway di gestione di dati nel nodo di hello (computer di Windows locale), che mostra lo stato della connettività, **nome del gateway**, e **nome nodo**.  

        ![Gateway di gestione dati: installazione completata](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-installation-success.png)

        > [!NOTE]
        > Se si esegue il provisioning gateway hello in una macchina virtuale di Azure, è possibile utilizzare [questo modello di gestione risorse di Azure su GitHub](https://github.com/xiaoyingLJ/vms-with-multiple-data-management-gateway). Questo script crea un gateway logico, imposta le macchine virtuali con installato il software Gateway di gestione dati e li registra con gateway logico hello. 
6. Nel portale di Azure, avviare hello **Gateway** pagina: 
    1. Scegliere hello data factory home page nel portale di hello **servizi collegati**.
    
        ![Home page di Data factory](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-home-page.png)
    2. Selezionare hello **gateway** toosee hello **Gateway** pagina:
    
        ![Home page di Data factory](media/data-factory-data-management-gateway-high-availability-scalability/linked-services-gateway.png)
    4. Vedrai hello **Gateway** pagina:   

        ![Visualizzazione del gateway con un nodo singolo](media/data-factory-data-management-gateway-high-availability-scalability/gateway-first-node-portal-view.png) 
7. Fare clic su **aggiunta del nodo** su hello barra degli strumenti tooadd un gateway logico toohello di nodo. Se si prevede l'installazione rapida toouse, eseguire questo passaggio da hello nel computer locale che verrà aggiunto come gateway toohello nodo. 

    ![Gateway di gestione dati: menu Aggiungi nodo](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-add-node-menu.png)
8. I passaggi sono simili toosetting backup primo nodo hello. Hello UI Configuration Manager consente di impostare il nome di nodo hello se si sceglie l'opzione di installazione manuale di hello: 

    ![Gestione configurazione: installare il secondo gateway](media/data-factory-data-management-gateway-high-availability-scalability/install-second-gateway.png)
9. Dopo che gateway hello è installato correttamente nel nodo hello, lo strumento Gestione configurazione hello visualizzato hello seguente schermata:  

    ![Gestione configurazione: installare il secondo gateway](media/data-factory-data-management-gateway-high-availability-scalability/second-gateway-installation-successful.png)
10. Se si apre hello **Gateway** pagina nel portale di hello, vengono mostrati i due nodi gateway ora: 

    ![Gateway con due nodi nel portale di hello](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring.png)
11. Fare clic su un nodo di gateway, toodelete **Elimina nodo** sulla barra degli strumenti hello, selezionare il nodo hello desidera toodelete e quindi fare clic su **eliminare** dalla barra degli strumenti hello. Questa azione Elimina nodo selezionato hello dal gruppo hello. Si noti che questa azione non disinstallare il software gateway di gestione dati hello da nodo hello (computer di Windows locale). Utilizzare **Aggiungi o Rimuovi programmi** nel Pannello di controllo nel gateway di hello locale toouninstall hello. Quando si disinstalla gateway dal nodo hello, viene eliminato automaticamente nel portale di hello.   

## <a name="upgrade-an-existing-gateway"></a>Aggiornare un gateway esistente
È possibile aggiornare un toouse gateway esistente hello la disponibilità elevata e funzionalità di scalabilità. Questa funzionalità funziona solo con i nodi che dispongono di gateway di gestione dati hello della versione > = 2.12.xxxx. È possibile visualizzare una versione di hello dati di gateway di gestione installato in un computer in hello **Guida** scheda di gestione di configurazione di Gateway di gestione dati hello. 

1. Gateway hello aggiornamento hello locale macchina toohello versione più recente seguendo, scaricare ed eseguire un pacchetto di installazione MSI da hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717). Vedere la sezione [Installazione](data-factory-data-management-gateway.md#installation) per i dettagli.  
2. Passare toohello portale di Azure. Avviare hello **pagina Data Factory** per la data factory. Fare clic su collegato servizi riquadro toolaunch hello **pagina servizi collegati**. Hello di hello selezionare gateway toolaunch **pagina gateway**. Fare clic su e abilitare **funzionalità di anteprima** come illustrato nella seguente immagine hello: 

    ![Gateway di gestione dati: abilitare l'anteprima funzionalità](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-existing-gateway-enable-high-availability.png)   
2. Dopo aver abilitato la funzionalità di anteprima hello nel portale di hello, chiudere tutte le pagine. Riaprire hello **pagina gateway** toosee hello nuova anteprima interfaccia utente (UI).
 
    ![Gateway di gestione dati: abilitazione dell'anteprima funzionalità riuscita](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-preview-success.png)

    ![Gateway di gestione dati: interfaccia utente di anteprima](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-preview.png)

    > [!NOTE]
    > Durante l'aggiornamento di hello, nome del primo nodo hello è nome hello della macchina di hello. 
3. Aggiungere ora un nodo. In hello **Gateway** pagina, fare clic su **aggiunta del nodo**.  

    ![Gateway di gestione dati: menu Aggiungi nodo](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-add-node-menu.png)

    Seguire le istruzioni da hello precedente sezione tooset nodo hello. 

### <a name="installation-best-practices"></a>Procedure consigliate per l'installazione

- Configurare risparmio di energia sul computer host hello per gateway hello in modo che hello macchina non lo stato di ibernazione. Se il computer host hello entra in sospensione, gateway hello non risponde toodata richieste.
- Eseguire il backup hello certificato associata hello gateway.
- Per prestazioni ottimali, assicurarsi che tutti i nodi abbiano un configurazione simile (consigliato). 
- Aggiungere almeno due nodi tooensure la disponibilità elevata.  

### <a name="tlsssl-certificate-requirements"></a>Requisiti del certificato TLS/SSL
Di seguito sono i requisiti di hello per certificato TLS/SSL hello che viene utilizzato per proteggere le comunicazioni tra i nodi del gateway:

- certificato di Hello deve essere un X509 pubblicamente attendibile certificato v3.
- Tutti i nodi del gateway devono considerare attendibile questo certificato. 
- È consigliabile usare certificati rilasciati da un'autorità di certificazione (CA) pubblica (terza parte).
- Deve supportare tutte le dimensioni chiave supportate da Windows Server 2012 R2 per i certificati SSL.
- Non deve supportare certificati che usano chiavi CNG.
- I certificati con caratteri jolly sono supportati. 


## <a name="monitor-a-multi-node-gateway"></a>Monitorare un gateway multinodo
### <a name="multi-node-gateway-monitoring"></a>Monitoraggio di un gateway multinodo
Nel portale di Azure hello, è possibile visualizzare snapshot tempo quasi reale di utilizzo delle risorse (CPU, memoria, network(in/out), e così via) in ogni nodo con gli stati dei nodi di gateway. 

![Gateway di gestione dati: monitoraggio di più nodi](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring.png)

È possibile abilitare **impostazioni avanzate** in hello **Gateway** pagina avanzate metriche come toosee **rete**(in/out), **Role & credenziali stato**, che è utile eseguire il debug di problemi del gateway, e **processi simultanei** (in esecuzione / limite) che possono essere modificata / modificata di conseguenza durante l'ottimizzazione delle prestazioni. Hello nella tabella seguente vengono fornite le descrizioni delle colonne in hello **nodi Gateway** elenco:  

Proprietà monitoraggio | Descrizione
:------------------ | :---------- 
Nome | Nome del gateway logico hello e nodi associati hello gateway.  
Stato | Stato del gateway logico hello e nodi gateway hello. Esempio: Online/Offline/Limitato e così via. Per informazioni su questi stati, vedere la sezione [Stato del gateway](#gateway-status). 
Versione | Mostra versione hello del gateway logico hello e ogni nodo del gateway. versione di Hello del gateway logico hello è determinata basato sulla versione di maggioranza dei nodi gruppo hello. Se sono presenti nodi con diverse versioni nella configurazione di gateway logico hello, solo i nodi di hello con hello stesso numero di versione come funzione di gateway logico hello correttamente. Altri utenti sono in modalità limited hello e devono toobe aggiornato manualmente (solo in caso di aggiornamento automatico). 
Memoria disponibile | Memoria disponibile in un nodo del gateway. Questo valore è uno snapshot in tempo quasi reale. 
Uso della CPU | Utilizzo della CPU di un nodo del gateway. Questo valore è uno snapshot in tempo quasi reale. 
Rete (in/out) | Utilizzo della rete da parte di un nodo del gateway. Questo valore è uno snapshot in tempo quasi reale. 
Processi simultanei (in esecuzione/limite) | Numero di processi o di attività in esecuzione in ogni nodo. Questo valore è uno snapshot in tempo quasi reale. Limite indica massimo processi simultanei di hello per ogni nodo. Questo valore viene definito in base alle dimensioni della macchina hello. È possibile aumentare hello limite tooscale di esecuzione di processi simultanei in scenari avanzati in cui CPU / memoria / rete è sottoutilizzato, ma le attività sono in timeout. Questa funzionalità è disponibile anche con un gateway a nodo singolo (anche quando non è abilitato funzionalità di scalabilità e disponibilità hello). Per altre informazioni, vedere la sezione [Considerazioni sulla scalabilità](#scale-considerations). 
Ruolo | Esistono due tipi di ruoli: dispatcher e ruolo di lavoro. Tutti i nodi sono processi di lavoro, ovvero che tutti possono essere utilizzati tooexecute processi. È presente un solo nodo dispatcher, attività o processi di toopull utilizzati dai servizi cloud e il successivo invio di nodi di lavoro toodifferent (incluso se stesso). 

![Gateway di gestione dati: monitoraggio avanzato di più nodi](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring-advanced.png)

### <a name="gateway-status"></a>Stato del gateway

Nella tabella seguente Hello fornisce gli stati possibili di un **nodo gateway**: 

Stato  | Commenti/Scenari
:------- | :------------------
Online | Nodo connesso servizio Factory tooData.
Offline | Il nodo è offline.
Aggiornamento | nodo Hello viene aggiornato automaticamente.
Limitato | A causa di tooConnectivity problema. Potrebbe essere dovuto problema porta 8050 tooHTTP, problema di connettività di bus di servizio o un problema di sincronizzazione delle credenziali. 
Inactive | Nodo si trova in una configurazione diversa dalla configurazione hello degli altri nodi di maggioranza.<br/><br/> Un nodo può essere inattivo quando non è possibile connettersi tooother nodi. 


Nella tabella seguente Hello fornisce gli stati possibili di un **gateway logico**. lo stato del gateway Hello varia a seconda degli stati dei nodi gateway hello. 

Stato | Commenti
:----- | :-------
Needs Registration (Registrazione necessaria) | Nessun nodo è ancora registrato toothis logico gateway
Online | I nodi del gateway sono online
Offline | Nessun nodo nello stato online.
Limitato | Non tutti i nodi in questo gateway sono in uno stato integro. Questo stato è un avviso indicante che qualche nodo potrebbe essere inattivo. <br/><br/>Potrebbe essere dovuto toocredential problema di sincronizzazione nel nodo dispatcher/di lavoro. 

### <a name="pipeline-activities-monitoring"></a>Monitoraggio di pipeline/attività
Hello portale di Azure fornisce una pipeline di esperienza con i dettagli di livello granulare di nodo di monitoraggio. ad esempio mostra le attività eseguite in ogni nodo. Queste informazioni possono essere utili per capire i problemi di prestazioni su un nodo specifico, ad esempio a causa di limitazione delle richieste toonetwork. 

![Gateway di gestione dati: monitoraggio di più nodi per le pipeline](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring-pipelines.png)

![Gateway di gestione dati: dettagli della pipeline](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-pipeline-details.png)

## <a name="scale-considerations"></a>Considerazioni sulla scalabilità

### <a name="scale-out"></a>Scalabilità orizzontale
Quando hello **memoria disponibile è insufficiente** hello e **l'utilizzo della CPU è elevato**, aggiungendo un nuovo nodo consente la scalabilità orizzontale hello carico tra più computer. Se l'attività non riesce a causa di nodo tootime-out o il gateway è offline, è utile se si aggiunge un gateway toohello nodo.
 
### <a name="scale-up"></a>Aumentare le prestazioni
Quando la memoria disponibile hello ed CPU non vengono utilizzati anche ma hello inattivo capacità pari a 0, è consigliabile applicare la scalabilità di aumentare il numero di hello processi simultanei che è possibile eseguire su un nodo verso l'alto. È inoltre possibile tooscale backup quando le attività sono in timeout poiché gateway hello è sovraccarico. Come illustrato nella seguente immagine hello, è possibile aumentare la capacità massima per un nodo hello. È consigliabile raddoppiandole toostart con.  

![Gateway di gestione dati: considerazioni sulla scalabilità](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-scale-considerations.png)


## <a name="known-issuesbreaking-changes"></a>Problemi noti/modifiche significative

- Attualmente, possono esistere fino a nodi fisici gateway toofour per un singolo gateway logico. Se è necessario più di quattro nodi per motivi di prestazioni, inviare un messaggio di posta elettronica troppo[DMGHelp@microsoft.com](mailto:DMGHelp@microsoft.com).
- È possibile registrare nuovamente un nodo di gateway con la chiave di autenticazione hello da un altro gateway logico tooswitch dal gateway logico corrente hello. toore la registrazione, disinstallare gateway hello dal nodo hello, reinstallare il gateway hello e registrarlo con la chiave di autenticazione hello per hello altri gateway logico. 
- Se il proxy HTTP è necessario per tutti i nodi del gateway, impostare il proxy di hello in diahost.exe.config e diawp.exe.config e utilizzare hello server manager toomake che tutti i nodi sono hello stesso diahost.exe.config e diawip.exe.config. Per informazioni dettagliate, vedere la sezione [Configurare le impostazioni del server proxy](data-factory-data-management-gateway.md#configure-proxy-server-settings). 
- modalità di crittografia toochange per la comunicazione da nodo a nodo in Gestione configurazione di Gateway, eliminare tutti i nodi di hello nel portale di hello tranne uno. Quindi, aggiungere i nodi dopo la modifica della modalità di crittografia hello.
- Se si sceglie di canale di comunicazione da nodo a nodo hello tooencrypt, utilizzare un certificato SSL ufficiale. Certificato autofirmato può causare problemi di connettività come hello stesso certificato potrebbe non essere attendibile nell'elenco di autorità di certificazione in altri computer. 
- È possibile registrare un gateway di gateway nodo tooa logico quando versione nodo hello è inferiore alla versione del gateway logico hello. Eliminare tutti i nodi del gateway logico hello dal portale in modo che è possibile registrare un node(downgrade) versione inferiore si. Se si elimina tutti i nodi di un gateway logico, manualmente installare e registrare di nuovo gateway di logica toothat nodi. In questo caso l'installazione rapida non è supportata.
- Non è possibile utilizzare l'installazione rapida tooinstall nodi tooan logico gateway esistente, che continua a utilizzare credenziali del cloud. È possibile controllare in cui le credenziali di hello sono archiviate da hello Gateway Configuration Manager nella scheda Impostazioni hello.
- Non è possibile utilizzare l'installazione rapida tooinstall nodi tooan logico gateway esistente, che è abilitato crittografia nodo a nodo. Come aggiungere manualmente i certificati comporta l'impostazione della modalità di crittografia hello, installazione rapida è non è più un'opzione. 
- Per copiare i file dall'ambiente locale, non è più consigliabile usare \\localhost o C:\files perché localhost o l'unità locale potrebbe non essere accessibile tramite tutti i nodi. Utilizzare invece \\percorso dei file toospecify ServerName\files.


## <a name="rolling-back-from-hello-preview"></a>Rollback dalla versione di anteprima hello 
tooroll da Anteprima hello, eliminare tutti i nodi ma un nodo. I nodi che si elimina, ma verificare di disporre di almeno un nodo nel gateway di hello logico non è importante. È possibile eliminare un nodo per la disinstallazione di gateway nel computer di hello o hello portale di Azure. Nel portale di Azure in hello hello **Data Factory** pagina, fare clic su hello toolaunch di servizi collegati **servizi collegati** pagina. Hello di hello selezionare gateway toolaunch **Gateway** pagina. Nella pagina di hello Gateway, è possibile visualizzare i nodi di hello associati hello gateway. pagina Hello consente di eliminare un nodo da gateway hello.
 
Dopo l'eliminazione, fare clic su **funzionalità di anteprima** in hello stessa pagina del portale Azure e disabilitare la funzionalità di anteprima hello. La reimpostazione del gateway di gateway tooone nodo GA (disponibilità generale).


## <a name="next-steps"></a>Passaggi successivi
Esaminare hello seguenti articoli:
- [Gateway di gestione dati](data-factory-data-management-gateway.md) -fornisce una panoramica dettagliata del gateway hello.
- [Spostare dati tra archivi dati locali e cloud](data-factory-move-data-between-onprem-and-cloud.md): contiene una procedura dettagliata con le istruzioni per usare un gateway a nodo singolo. 
