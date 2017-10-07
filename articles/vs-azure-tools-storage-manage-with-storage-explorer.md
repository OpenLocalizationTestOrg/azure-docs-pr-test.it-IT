---
title: aaaGet avviato con Esplora risorse di archiviazione (anteprima) | Documenti Microsoft
description: Gestire le risorsa di archiviazione di Azure con Storage Explorer (anteprima)
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/17/2017
ms.author: kraigb
ms.openlocfilehash: 57737b51baace92858eb07c7dbc3139bd7e041f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-storage-explorer-preview"></a>Guida introduttiva a Storage Explorer (anteprima)
## <a name="overview"></a>Panoramica
Esplora archivi Azure (anteprima) è un'applicazione autonoma che consente di utilizzare tooeasily dati di archiviazione di Azure in Windows, macOS e Linux. In questo articolo viene illustrato hello diverse modalità di connessione tooand gestione degli account di archiviazione di Azure.

![Microsoft Azure Storage Explorer (anteprima)][15]

## <a name="prerequisites"></a>Prerequisiti
* [Scaricare e installare Storage Explorer (anteprima)](http://www.storageexplorer.com)

## <a name="connect-tooa-storage-account-or-service"></a>Connettersi al servizio o account di archiviazione tooa
Esplorazione dell'archiviazione (anteprima) fornisce diversi metodi tooconnect toostorage account. Ad esempio, è possibile:
* Collegare gli account toostorage associati alle sottoscrizioni di Azure.
* Connettersi toostorage account e servizi che vengono condivisi da altre sottoscrizioni di Azure.
* Connettersi tooand gestire l'archiviazione locale tramite hello emulatore di archiviazione Azure. 

Inoltre, è possibile usare gli account di archiviazione in Azure globale e nazionale:

* [Connettersi tooan sottoscrizione di Azure](#connect-to-an-azure-subscription): gestire le risorse di archiviazione che appartengono tooyour sottoscrizione di Azure.
* [Utilizzare l'archiviazione locale per lo sviluppo](#work-with-local-development-storage): gestire l'archiviazione locale tramite hello emulatore di archiviazione Azure.
* [Collega archiviazione tooexternal](#attach-or-detach-an-external-storage-account): gestire le risorse di archiviazione che appartengono tooanother sottoscrizione di Azure o che si trovano in national cloud di Azure con nome, chiave e gli endpoint dell'account di archiviazione hello.
* [Collegare un account di archiviazione tramite una firma di accesso condiviso](#attach-storage-account-using-sas): gestire le risorse di archiviazione che appartengono tooanother sottoscrizione di Azure tramite una firma di accesso condiviso (SAS).
* [Collegare un servizio utilizzando una firma di accesso condiviso](#attach-service-using-sas): gestione di un servizio di archiviazione specifico (contenitore blob, coda o tabella) che appartiene tooanother sottoscrizione di Azure tramite una firma di accesso condiviso.

## <a name="connect-tooan-azure-subscription"></a>Connettersi tooan sottoscrizione di Azure
> [!NOTE]
> Se non si ha un account Azure, è possibile [iscriversi per ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) oppure [attivare i vantaggi della sottoscrizione di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
>
>

1. In Storage Explorer (anteprima), selezionare **Azure Account settings**(Impostazioni account Azure).

    ![Azure Account settings][0]

2. riquadro di sinistra Hello Visualizza tutti gli account di Microsoft hello a che è stato effettuato l'accesso. tooconnect tooanother account, selezionare **aggiungere un account**, quindi seguire hello istruzioni toosign con un account Microsoft associato ad almeno una sottoscrizione di Azure attiva.

    >[!NOTE]
    >Connessione toonational Azure (ad esempio Azure in Germania, Azure per enti pubblici e Cina di Azure tramite Accedi) non è attualmente supportata. Vedere hello "collegamento o scollegamento di un account di archiviazione esterno" sezione per informazioni su come tooconnect toonational account di archiviazione Azure.

3. Dopo aver accedere correttamente con un account Microsoft, a sinistra hello riquadro viene popolato con hello le sottoscrizioni di Azure associate all'account. Selezionare le sottoscrizioni di Azure che si desidera toowork con e quindi selezionare di hello **applica**. (Selezione **tutte le sottoscrizioni** attiva o disattiva la selezione di tutti o nessuno dei hello elencate le sottoscrizioni di Azure.)

    ![Selezionare le sottoscrizioni di Azure][3]  
    riquadro di sinistra Hello consente di visualizzare gli account di archiviazione hello associati alle sottoscrizioni Azure hello selezionato.

    ![Sottoscrizioni di Azure selezionate][4]

## <a name="connect-tooan-azure-stack-subscription"></a>La connessione di sottoscrizione di Azure Stack tooan

Per informazioni sulla sottoscrizione di Azure Stack tooan connessione, vedere [tooan connettere Esplora archivi sottoscrizione Azure Stack](azure-stack/azure-stack-storage-connect-se.md).

## <a name="work-with-local-development-storage"></a>Utilizzare la risorsa di archiviazione locale
Con Esplora risorse di archiviazione (anteprima), è possibile utilizzare nel servizio di archiviazione locale tramite hello emulatore di archiviazione Azure. Questo approccio consente di scrivere codice in base e i test di archiviazione senza dover necessariamente un account di archiviazione distribuito in Azure, perché l'account di archiviazione hello è emulata da hello emulatore di archiviazione Azure.

> [!NOTE]
> Hello emulatore di archiviazione di Azure è attualmente supportata solo per Windows.
>
>

1. Nel riquadro sinistro di hello di esplorazione dell'archiviazione (anteprima), espandere hello **(locale e connesse)** > **gli account di archiviazione** > **(sviluppo)** nodo.

    ![Nodo di sviluppo locale][21]

2. Se non è stato ancora installato hello emulatore di archiviazione Azure, si toodo richiesta in questo caso, tramite una barra informazioni. Se viene visualizzata la barra informazioni hello, selezionare **versione più recente di Download hello**e quindi installare l'emulatore hello.

    ![Richiesta di download dell'Emulatore di archiviazione di Azure][22]

3. Dopo l'installazione dell'emulatore hello, è possibile creare e lavorare con le tabelle, code e BLOB locali. toolearn come tipo toowork con ogni account di archiviazione, vedere uno dei seguenti hello:

    * [Gestire le risorse dell'archivio BLOB di Azure](vs-azure-tools-storage-explorer-blobs.md)
    * Manage Azure file share storage resources (Gestire risorse di condivisione file di Azure): *presto disponibile*
    * Manage Azure queue storage resources (Gestire risorse di archiviazione code di Azure): *presto disponibile*
    * Manage Azure table storage resources (Gestire risorse di archiviazione tabelle di Azure): *presto disponibile*

## <a name="attach-or-detach-an-external-storage-account"></a>Collegare o scollegare un account di archiviazione esterno
Con Esplora risorse di archiviazione (anteprima), è possibile collegare gli account di archiviazione tooexternal in modo che gli account di archiviazione possono essere condivisa con facilità. Questa sezione viene illustrato come tooattach too(and detach from) gli account di archiviazione esterno.

### <a name="get-hello-storage-account-credentials"></a>Ottenere le credenziali dell'account di archiviazione hello
tooshare un account di archiviazione esterno, proprietario hello di tale account deve innanzitutto ottenere credenziali hello (nome dell'account e la chiave) per conto di hello e quindi condividere le informazioni che richiede account toothat (esterna) tooattach persona hello. È possibile ottenere le credenziali dell'account di archiviazione hello tramite hello portale di Azure eseguendo hello seguenti:

1. Accedi toohello [portale di Azure](https://portal.azure.com).

2. Selezionare **Esplora**.

3. Selezionare **Account di archiviazione**.

4. In hello **gli account di archiviazione** blade, account di archiviazione selezionare hello desiderato.

5. In hello **impostazioni** pannello hello selezionato di account di archiviazione, selezionare **le chiavi di accesso**.

    ![Opzione Chiavi di accesso][5]

6. In hello **le chiavi di accesso** blade, hello copia **nome account di archiviazione** e **key1** valori da utilizzare quando ci si connette toohello account di archiviazione.

    ![Chiavi di accesso][6]

### <a name="attach-tooan-external-storage-account"></a>Collegare l'account di archiviazione esterno tooan
account di archiviazione esterno tooan tooattach, è necessario nome e la chiave dell'account hello. sezione "Get hello archiviazione le credenziali dell'account" Hello viene illustrato come questi valori da tooobtain hello portale di Azure. Tuttavia, nel portale di hello, viene chiamata chiave dell'account hello **key1**. Pertanto, in Esplora archivi (anteprima) richiede una chiave dell'account, è immettere hello **key1** valore.

1. In Esplora archivi (anteprima), selezionare **connettere archiviazione tooAzure**.

    ![Opzione di archiviazione tooAzure di connessione][23]

2. In hello **connettersi tooAzure archiviazione** finestra di dialogo, specificare una chiave dell'account di hello (hello **key1** valore dal portale di Azure hello), quindi selezionare **successivo**.

    > [!NOTE]
    > È possibile immettere una stringa di connessione di archiviazione hello da un account di archiviazione in Azure nazionali. Gli account di archiviazione Germania tooAzure tooconnect, ad esempio, immettere la seguente connessione stringhe simili toohello: 
    >
    >* DefaultEndpointsProtocol=https
    >* AccountName=cawatest03
    >* AccountKey=<storage_account_key>
    >* EndpointSuffix=core.cloudapi.de
    
    >È possibile ottenere la stringa di connessione hello da hello Azure portale in hello stesso modo come descritto in hello sezione "Ottenere le credenziali dell'account di archiviazione hello".

    ![Finestra di dialogo archiviazione tooAzure di connessione][24]

3. In hello **collega archiviazione esterna** della finestra di dialogo hello **nome Account** , immettere il nome di account di archiviazione hello, specificare le altre impostazioni desiderate e quindi selezionare **Avanti**.

    ![Finestra di dialogo Associa archiviazione esterna][8]

4. In hello **connessione riepilogo** finestra di dialogo casella, verificare le informazioni di hello. Se si desidera toochange qualsiasi valore diverso, selezionare **nuovamente** e immettere nuovamente le impostazioni di hello desiderato. 

5. Selezionare **Connessione**.

6. Una volta stabilita la connessione, l'account di archiviazione esterno hello viene visualizzato con **(esterna)** aggiunto toohello nome account di archiviazione.

    ![Risultato della connessione di account di archiviazione esterno tooan][9]

### <a name="detach-from-an-external-storage-account"></a>Scollegarsi da un account di archiviazione esterno
1. Fare doppio clic su account di archiviazione esterno hello desidera toodetach e quindi selezionare **scollegamento**.

    ![Opzione per scollegarsi da un account di archiviazione][10]

2. Nel messaggio di conferma hello, selezionare **Sì** la disconnessione di hello tooconfirm dall'account di archiviazione esterna hello.

## <a name="attach-a-storage-account-by-using-an-sas"></a>Collegare un account di archiviazione usando la firma di accesso condiviso
Un [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) consente di concedere l'account di archiviazione di un accesso temporaneo tooa senza credenziali di sottoscrizione di Azure tooprovide salve di una sottoscrizione di Azure.

tooillustrate questo scenario, si ad esempio che utente a è un amministratore di una sottoscrizione di Azure ed è UserA tooallow UserB tooaccess uno spazio di archiviazione dell'account per un periodo limitato con determinate autorizzazioni:

1. UserA genera una firma di accesso condiviso (costituito dalla stringa di connessione hello per account di archiviazione hello) per un'ora specifica periodo e con le autorizzazioni di hello desiderato.

2. Condivisioni UserA hello SAS con hello persona (in questo esempio UserB) richiede l'account di archiviazione toohello di accesso.  

3. UserB utilizza Esplora archivi (Preview) tooattach toohello account appartiene tooUserA utilizzando hello fornito SAS.

### <a name="get-an-sas-for-hello-account-you-want-tooshare"></a>Ottenere una firma di accesso condiviso per conto di hello desiderato tooshare
1. In Esplora archivi (anteprima), fare doppio clic su account di archiviazione hello da condividere e quindi selezionare **ottenere firma di accesso condiviso**.

    ![Menu di scelta rapida Get SAS (Ottieni firma di accesso condiviso)][13]

2. In hello **firma di accesso condiviso** finestra di dialogo, specificare l'intervallo di tempo hello e le autorizzazioni desiderate per l'account di hello e quindi selezionare **crea**.

    ![Finestra di dialogo Get SAS][14] (Ottieni firma di accesso condiviso)  
    Hello **firma di accesso condiviso** la finestra di dialogo viene visualizzata e viene visualizzato hello SAS.

3. Toohello Avanti **stringa di connessione**, selezionare **copia** toocopy è toohello Appunti, quindi selezionare **Chiudi**.

### <a name="attach-toohello-shared-account-by-using-hello-sas"></a>Associare account toohello condiviso utilizzando hello SAS
1. In Esplora archivi (anteprima), selezionare **connettere archiviazione tooAzure**.

    ![Opzione di archiviazione tooAzure di connessione][23]

2. In hello **connettersi tooAzure archiviazione** la finestra di dialogo, specificare la stringa di connessione hello e quindi selezionare **Avanti**.

    ![Finestra di dialogo archiviazione tooAzure di connessione][24]

3. In hello **connessione riepilogo** finestra di dialogo casella, verificare le informazioni di hello. modifiche toomake, selezionare **nuovamente**, quindi immettere impostazioni hello desiderate. 

4. Selezionare **Connessione**.

5. Dopo la connessione, viene visualizzato l'account di archiviazione di hello con **(SAS)** aggiunto toohello nome dell'account specificate.

    ![Risultato dell'account collegato tooan tramite firma di accesso condiviso][17]

## <a name="attach-a-service-by-using-an-sas"></a>Collegare un servizio usando la firma di accesso condiviso
sezione "Collegare un account di archiviazione tramite una firma di accesso condiviso" Hello viene illustrato come un amministratore della sottoscrizione di Azure può concedere l'account di archiviazione di un accesso temporaneo tooa mediante la generazione e la condivisione di una firma di accesso condiviso per l'account di archiviazione hello. È allo stesso modo possibile generare una firma di accesso condiviso per un servizio specifico, ovvero contenitore BLOB, coda o tabella, in un account di archiviazione.  

### <a name="generate-an-sas-for-hello-service-that-you-want-tooshare"></a>Generare una firma di accesso condiviso per il servizio di hello che si desidera tooshare
In questo contesto, un servizio può essere un contenitore BLOB, una coda o una tabella. toogenerate hello firma di accesso condiviso per un servizio elencato, vedere:

* [Ottenere hello firma di accesso condiviso per un contenitore blob](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* Ottenere hello firma di accesso condiviso per una condivisione file: *sarà presto disponibile*
* Ottenere hello firma di accesso condiviso per una coda: *sarà presto disponibile*
* Ottenere hello firma di accesso condiviso per una tabella: *sarà presto disponibile*

### <a name="attach-toohello-shared-account-service-by-using-hello-sas"></a>Collegare toohello condiviso account di servizio utilizzando hello SAS
1. In Esplora archivi (anteprima), selezionare **connettere archiviazione tooAzure**.

    ![Opzione di archiviazione tooAzure di connessione][23]

2. In hello **connettersi tooAzure archiviazione** nella finestra di dialogo specificare hello URI SAS e quindi selezionare **Avanti**.

    ![Finestra di dialogo archiviazione tooAzure di connessione][24]

3. In hello **connessione riepilogo** finestra di dialogo casella, verificare le informazioni di hello. modifiche toomake, selezionare **nuovamente**, quindi immettere impostazioni hello desiderate. 

4. Selezionare **Connessione**.

5. Dopo la connessione, hello servizio appena collegato viene visualizzato in hello **(servizio SAS)** nodo.

    ![Risultato dell'associazione servizio tooa condivisa tramite una firma di accesso condiviso][20]

## <a name="search-for-storage-accounts"></a>Cercare gli account di archiviazione
Se si dispone di un lungo elenco di account di archiviazione, toolocate un modo rapido un determinato account di archiviazione è casella di ricerca toouse hello nella parte superiore di hello del riquadro di sinistra hello.

Mentre si digita nella casella di ricerca hello, hello riquadro a sinistra consente di visualizzare hello account di archiviazione corrispondono hello valore di ricerca che immesso toothat un punto. Ad esempio, una ricerca per gli account di archiviazione il cui nome contiene **tarcher** è illustrato nella seguente schermata hello:

![Ricerca dell'account di archiviazione][11]

## <a name="next-steps"></a>Passaggi successivi
* [Gestire le risorse dell'archivio BLOB di Azure con Storage Explorer (anteprima)](vs-azure-tools-storage-explorer-blobs.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png
