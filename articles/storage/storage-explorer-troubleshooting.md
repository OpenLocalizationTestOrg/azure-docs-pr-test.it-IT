---
title: Guida alla risoluzione dei problemi di Esplora archivi aaaAzure | Documenti Microsoft
description: "Panoramica della funzionalità di debug hello due di Azure"
services: virtual-machines
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: delhan
ms.openlocfilehash: 21705629500359222bc566c599f0864ad50036ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a>Guida alla risoluzione dei problemi di Azure Storage Explorer

## <a name="introduction"></a>Introduzione

Esplora archivi di Microsoft Azure (anteprima) è un'app autonoma che consente di utilizzare tooeasily dati di archiviazione di Azure in Windows, macOS e Linux. app Hello possono connettersi toStorage account ospitato in Azure, cloud statali e Stack di Azure.

In questa guida sono riepilogate le soluzioni per gli errori comuni riscontrati in Storage Explorer.

## <a name="sign-in-issues"></a>Problemi relativi all'accesso

Sono supportati solo account AAD (Azure Active Directory). Se si utilizza un account di ad FS, sono previsti tooStorage che Explorer non è possibile utilizzare tale accesso. Prima di continuare, provare a riavviare l'applicazione e verificare che i problemi di hello possono essere risolti.

### <a name="error-self-signed-certificate-in-certificate-chain"></a>Errore: certificato autofirmato nella catena di certificati

Esistono diversi motivi, perché questo errore può verificarsi, e due motivi più comuni hello sono i seguenti:

1. app Hello viene connesso tramite un "proxy trasparente", ovvero un server (ad esempio, il server aziendale) è intercetta il traffico HTTPS, la decrittografia e quindi crittografarlo utilizzando un certificato autofirmato.

2. Si esegue un'applicazione, ad esempio software antivirus, che è inserendo messaggi hello HTTPS che si ricevano un certificato SSL autofirmato.

Quando Esplora archivi rileva uno dei problemi di hello, può non sapere se è stata manomessa messaggio HTTPS hello ricevuto. Se si dispone di una copia del certificato autofirmato hello, è possibile utilizzare Esplora archivi di verificare l'attendibilità. Se si è certi di chi esegue l'inserimento dei certificati di hello, seguire questi passaggi toofind è:

1. Installare Open SSL

    - [Windows](https://slproweb.com/products/Win32OpenSSL.html) (qualsiasi versione di hello chiaro dovrebbe essere sufficiente)

    - Mac e Linux: devono essere inclusi nel sistema operativo

2. Eseguire Open SSL

    - Windows: aprire la directory di installazione di hello, fare clic su **/bin/**, quindi fare doppio clic su **openssl.exe**.
    - Mac e Linux: eseguire **openssl** da un terminale.

3. Eseguire s_client -showcerts -connect microsoft.com:443

4. Cercare i certificati autofirmati. Se si è certi che sono autofirmati, cercare in un punto qualsiasi oggetto hello ("s") e sono hello (ricerca per categorie ":") dell'autorità di certificazione stessa.

5. Dopo aver individuato i certificati autofirmati, ciascuno di essi, copiare e incollare tutto da **---BEGIN CERTIFICATE---** troppo**---END CERTIFICATE---** tooa nuovo file con estensione cer.

6. Aprire Esplora risorse di archiviazione, fare clic su **modifica** > **i certificati SSL** > **importazione certificati**e quindi utilizzare hello file selezione toofind, select, e aprire i file con estensione cer hello è stato creato.

Se non si trova alcun certificato autofirmato utilizzando hello sopra passaggi, contattare Microsoft tramite lo strumento di feedback hello per ulteriore assistenza.

### <a name="unable-tooretrieve-subscriptions"></a>Non è possibile tooretrieve sottoscrizioni

Se si è grado tooretrieve le sottoscrizioni dopo l'accesso, seguire questo problema tootroubleshoot questi passaggi:

- Verificare che l'account disponga di accesso toohello sottoscrizioni effettuando l'accesso al portale di Azure hello.

- Assicurarsi di aver effettuato utilizzando l'ambiente corretto di hello (Azure, Cina di Azure, Azure in Germania, Azure del governo o Stack ambiente/Azure personalizzato).

- Se ci si trova dietro un proxy, assicurarsi che il proxy di Esplora archivi hello è stato configurato correttamente.

- Provare a rimuovere e nuova aggiunta account hello.

- Provare a eliminare hello i seguenti file dalla directory radice (vale a dire C:\Users\ContosoUser) e quindi aggiungere nuovamente l'account hello:

    - .adalcache

    - .devaccounts

    - .extaccounts

- Console di strumenti per sviluppatori hello espressioni di controllo (premendo F12) quando si esegue l'accesso per i messaggi di errore:

![strumenti per sviluppatori](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a>Pagina di autenticazione non è possibile toosee hello

Nel caso di pagina di autenticazione non è possibile toosee hello, seguire questo problema tootroubleshoot questi passaggi:

- A seconda della velocità di hello della connessione, potrebbe richiedere alcuni minuti per tooload nella pagina di accesso hello, attendere almeno un minuto prima di chiudere la finestra di dialogo di autenticazione hello.

- Se ci si trova dietro un proxy, assicurarsi che il proxy di Esplora archivi hello è stato configurato correttamente.

- Console per sviluppatori di hello visualizzazione premendo tasto F12 hello. Controllare le risposte hello dalla console per sviluppatori hello e vedere se è possibile trovare qualsiasi indicazione per questo motivo l'autenticazione non funziona.

### <a name="cannot-remove-account"></a>Impossibile rimuovere l'account

Se si è grado tooremove un account o hello Riesegui autenticazione collegamento non ha alcun effetto, seguire questo problema tootroubleshoot questi passaggi:

- Provare a eliminare hello i seguenti file dalla directory radice e quindi nuova aggiunta account hello:

    - .adalcache

    - .devaccounts

    - .extaccounts

- Se si desidera tooremove SAS associata alle risorse di archiviazione, eliminare i seguenti file hello:

    - la cartella %AppData%/StorageExplorer per Windows

    - /Utenti/<your_name>/Library/Applicaiton SUpport/StorageExplorer per Mac

    - ~/.config/StorageExplorer per Linux

> [!NOTE]
>  Sarà necessario tooreenter tutte le credenziali se si eliminano questi file.

## <a name="proxy-issues"></a>Problemi di proxy

Verificare innanzitutto che hello le seguenti informazioni immesse siano tutti corretti:

- Hello URL del proxy e la porta numero

- Nome utente e password se richiesto dal proxy hello

### <a name="common-solutions"></a>soluzioni comuni

Se si verificano ancora problemi, seguire questi passaggi tootroubleshoot loro:

- Se è possibile connettersi toohello Internet senza utilizzare il proxy, verificare che funziona con Esplora archivi senza le impostazioni proxy abilitate. In caso di hello, potrebbe esserci un problema con le impostazioni del proxy. Funziona con i problemi di hello tooidentify amministratore proxy.

- Verificare che altre applicazioni che utilizzano server proxy hello funzionino come previsto.

- Verificare che sia possibile connettersi il portale di Microsoft Azure toohello tramite il web browser

- Verificare di poter ricevere le risposte dagli endpoint del servizio. Immettere uno degli URL dell'endpoint nel browser. Se è possibile connettersi, si dovrebbe ricevere InvalidQueryParameterValue o una risposta XML simile.

- Se anche altre persone usano Storage Explorer con il server proxy, accertarsi che riescano a connettersi. Se è possibile connettersi, è possibile toocontact l'amministratore del server proxy.

### <a name="tools-for-diagnosing-issues"></a>Strumenti per la diagnosi dei problemi

Se si dispone di strumenti di rete, ad esempio Fiddler per Windows, i problemi di hello toodiagnose in grado di può essere come segue:

- Se si dispone di toowork tramite il proxy, è possibile tooconfigure il tooconnect strumento rete tramite proxy hello.

- Controllare il numero di porta hello utilizzato per lo strumento di rete.

- Immettere l'URL host locale hello e numero di porta dello strumento di rete come le impostazioni proxy in Esplora archivi hello. Se questa operazione viene eseguita correttamente, lo strumento rete inizia la registrazione delle richieste di rete dagli endpoint di servizio e toomanagement Esplora archivi. Ad esempio, immettere https://cawablobgrs.blob.core.windows.net/ per l'endpoint blob in un browser e si riceverà una risposta è simile al seguente hello, che suggerisce risorsa hello è presente, anche se non è possibile accedere.

![esempio di codice](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a>Contattare l'amministratore del server proxy

Se le impostazioni proxy siano corrette, è possibile toocontact l'amministratore del server proxy, e

- Assicurarsi che il proxy non blocchi il traffico tooAzure management o risorsa gli endpoint.

- Verificare il protocollo di autenticazione hello del server proxy. Storage Explorer attualmente non supporta i proxy NTLM.

## <a name="unable-tooretrieve-children-error-message"></a>Messaggio di errore "Impossibile tooRetrieve figli"

Se si è connessi tooAzure tramite un proxy, verificare che le impostazioni proxy siano corrette. Se si sono state concesse accesso tooa risorsa dal proprietario hello di hello sottoscrizione o l'account, verificare di avere letto o elencare le autorizzazioni per tale risorsa.

### <a name="issues-with-sas-url"></a>Problemi relativi all'URL SAS
Se ci si connette tooa servizio tramite un URL SAS e verifica l'errore:

- Verificare che l'URL di hello fornisca delle autorizzazioni necessarie hello tooread o un elenco di risorse.

- Verificare che hello che URL non sia scaduto.

- Se hello URL SAS è basata su criteri di accesso, verificare che i criteri di accesso hello non è stato revocato.

## <a name="next-steps"></a>Passaggi successivi

Se nessuna delle soluzioni di hello risolvere il problema, inviare il problema tramite lo strumento di feedback hello con messaggio di posta elettronica e il numero di dettagli sul problema hello incluso come si può, in modo che possiamo contattarti per risolvere il problema di hello.

toodo, fare clic su **Guida** menu e quindi fare clic su **Invia commenti e suggerimenti**.

![Commenti e suggerimenti](./media/storage-explorer-troubleshooting/4022503_en_1.png)
