---
title: un'immagine di macchina virtuale per hello Azure Marketplace aaaCreating | Documenti Microsoft
description: Istruzioni dettagliate su come una macchina virtuale toocreate immagine per hello Azure Marketplace per altri toopurchase.
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5c937b8e-e28d-4007-9fef-624046bca2ae
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio; v-divte
ms.openlocfilehash: 65e1c0530bb050fb379a52544e36c55faacd84df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-virtual-machine-image-for-hello-azure-marketplace"></a>Guida toocreate un'immagine di macchina virtuale per hello Azure Marketplace
In questo articolo, **passaggio 2**, illustra preparazione hello dischi rigidi virtuali (VHD) che si distribuirà toohello Azure Marketplace. I dischi rigidi virtuali sono foundation hello dello SKU. processo Hello varia a seconda se si specifica una SKU basati su Windows o Linux. In questo articolo vengono descritti entrambi gli scenari. Questo processo può essere eseguito parallelamente alla [creazione e registrazione dell'account][link-acct-creation].

## <a name="1-define-offers-and-skus"></a>1. Definire le offerte e gli SKU
In questa sezione vengono offerte hello toodefine e i relativi SKU associato.

Un'offerta è un tooall "padre" di relativi SKU. È possibile disporre di più offerte. Come si decide di toostructure le offerte è tooyou. Quando un'offerta viene inserita toostaging, esso viene inserito insieme a tutti i relativi SKU. Valutare attentamente gli identificatori SKU, poiché saranno visibili nell'URL hello:

* Azure.com: http://azure.microsoft.com/marketplace/partners/{PartnerNamespace}/{OfferIdentifier}-{SKUidentifier}
* Portale di anteprima di Azure: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{SKUIDdentifier}  

Uno SKU è hello nome commerciale un'immagine di macchina virtuale. Un'immagine di macchina virtuale contiene un disco del sistema operativo e zero o più dischi dati. È essenzialmente hello completo profilo di archiviazione per una macchina virtuale. È necessario un disco rigido virtuale per ogni disco. I dischi di dati vuoto anche richiedono toobe un disco rigido virtuale creato.

Indipendentemente dal quale sistema operativo in uso, aggiungere solo hello numero minimo di dischi di dati necessari per hello SKU. I clienti non è possibile rimuovere i dischi che fanno parte di un'immagine in fase di distribuzione di hello ma è sempre possono aggiungere dischi durante o dopo la distribuzione se hanno bisogno.

> [!IMPORTANT]
> **Non modificare il numero di dischi in una nuova versione dell'immagine.** Se è necessario riconfigurare i dischi dati nell'immagine di hello, definire uno SKU di nuovo. Pubblicare una nuova versione di immagine con conteggi di diversi disco avranno potenziale hello di danneggiare la nuova distribuzione basata su hello nuova versione di immagine in caso di distribuzioni automatiche, ridimensionamento automatico di soluzioni tramite modelli ARM e altri scenari.
>
>

### <a name="11-add-an-offer"></a>1.1 Aggiungere un'offerta
1. Accedi toohello [portale pubblicazione] [ link-pubportal] utilizzando l'account.
2. Seleziona hello **macchine virtuali** scheda di hello portale di pubblicazione. Nel campo di immissione richiesta hello, immettere il nome dell'offerta. nome dell'offerta Hello è in genere il nome di hello del prodotto hello o un servizio che si prevede di toosell in hello Azure Marketplace.
3. Selezionare **Crea**.

### <a name="12-define-a-sku"></a>1.2 Definire uno SKU
Dopo aver aggiunto un'offerta, è necessario toodefine e identificare le SKU. È possibile avere più offerte e ogni offerta può includere più SKU. Quando un'offerta viene inserita toostaging, esso viene inserito insieme a tutti i relativi SKU.

1. **Aggiungere uno SKU.** Hello SKU richiede un identificatore, viene utilizzato nell'URL hello. Identificatore Hello deve essere univoci all'interno del profilo di pubblicazione, ma non c'è alcun rischio di conflitti di identificatore con altri server di pubblicazione.

   > [!NOTE]
   > offerta Hello e gli identificatori SKU vengono visualizzati nell'URL offerta hello hello Marketplace.
   >
   >
2. **Aggiungere una descrizione di riepilogo per lo SKU.** Descrizioni di riepilogo sono toocustomers visibile, è consigliabile eseguire li facilmente leggibili. Queste informazioni non è necessario toobe bloccato finché non sarà fase "Push tooStaging" hello. Fino ad allora, si libera tooedit è.
3. Se si utilizza SKU basati su Windows, seguire i collegamenti consigliati hello tooacquire hello approvato le versioni di Windows Server.

## <a name="2-create-an-azure-compatible-vhd-linux-based"></a>2. Creare un VHD compatibile con Azure (basato su Linux)
In questa sezione è incentrata sulle procedure consigliate per la creazione di un'immagine di macchina virtuale basata su Linux per hello Azure Marketplace. Per una procedura dettagliata, vedere toohello seguente documentazione: [creazione e caricamento di un disco rigido virtuale contenente hello del sistema operativo Linux](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="3-create-an-azure-compatible-vhd-windows-based"></a>3. Creare un VHD compatibile con Azure (basato su Windows)
In questa sezione è incentrata sulla hello passaggi toocreate uno SKU basato su Windows Server per hello Azure Marketplace.

### <a name="31-ensure-that-you-are-using-hello-correct-base-vhds"></a>3.1 Assicurarsi che si sta utilizzando hello correggere VHD di base
sistema operativo di Hello disco rigido virtuale per l'immagine di macchina virtuale deve essere basato su un'immagine di base approvato Azure che contiene il Server di Windows o SQL Server.

toobegin, creare una macchina virtuale da una delle seguenti immagini, disponibile all'indirizzo hello hello [portale Microsoft Azure][link-azure-portal]:

* Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1][link-datactr-2008-r2])
* SQL Server 2014 ([Enterprise][link-sql-2014-ent], [Standard][link-sql-2014-std], [Web][link-sql-2014-web])
* SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent], [Standard][link-sql-2012-std], [Web][link-sql-2012-web])

Questi collegamenti sono disponibili nel portale di pubblicazione di hello in pagina SKU hello.

> [!TIP]
> Se si utilizza il portale di Azure corrente di hello o PowerShell, sono approvate le immagini di Windows Server pubblicate 8 settembre 2014 e versioni successive.
>
>

### <a name="32-create-your-windows-based-vm"></a>3.2 Creare la macchina virtuale basata su Windows
Dal portale di Microsoft Azure hello, è possibile creare la macchina virtuale in base a un'immagine di base approvata in pochi semplici passaggi. esempio Hello viene fornita una panoramica del processo di hello:

1. Immagine di base hello pagina selezionare **crea macchina virtuale** toobe indirizzate toohello nuova [portale Microsoft Azure][link-azure-portal].

    ![disegno][img-acom-1]
2. Accedi portale toohello con account Microsoft hello e una password per la sottoscrizione di Azure da toouse hello.
3. Seguire hello richieste toocreate una macchina virtuale utilizzando l'immagine di base hello selezionata. È necessario tooprovide un nome host (nome del computer hello), un nome utente (registrato come amministratore) e una password per hello macchina virtuale.

    ![disegno][img-portal-vm-create]
4. Selezionare dimensione hello di hello VM toodeploy:

    a.    Se si prevede di toodevelop hello disco rigido virtuale locale, hello dimensione non è importante. È consigliabile utilizzare uno dei hello macchine virtuali più piccole.

    b.    Se si prevede di immagine hello toodevelop in Azure, prendere in considerazione l'uso di uno di hello consigliato dimensioni delle macchine Virtuali per l'immagine selezionata hello.

    c.    Per informazioni sui prezzi, vedere toohello **consigliato i livelli di prezzo** selettore visualizzati nel portale di hello. Fornirà hello tre le dimensioni consigliate fornite dall'autore hello. (In questo caso, server di pubblicazione hello è Microsoft.)

    ![disegno][img-portal-vm-size]
5. Impostare le proprietà:

    a.    Per la distribuzione rapida, è possibile lasciare hello valori predefiniti per proprietà hello in **configurazione facoltativa** e **gruppo di risorse**.

    b.    In **Account di archiviazione**, è possibile selezionare facoltativamente l'account di archiviazione hello in quale sistema operativo di hello VHD verranno archiviati.

    c.    In **gruppo di risorse**, è possibile selezionare facoltativamente gruppo logico di hello in cui tooplace hello macchina virtuale.
6. Seleziona hello **percorso** per la distribuzione:

    a.    Se si prevede di toodevelop hello disco rigido virtuale locale, il percorso di hello non è importante perché hello immagine tooAzure verrà caricato in un secondo momento.

    b.    Se si prevede di immagine hello toodevelop in Azure, è consigliabile utilizzare una delle regioni di Microsoft Azure basata negli Stati Uniti hello dall'inizio hello. Questo velocizza hello VHD processo di copia che Microsoft esegue per conto dell'utente quando si invia l'immagine per la certificazione.

    ![disegno][img-portal-vm-location]
7. Fare clic su **Crea**. Hello VM avvia toodeploy. In pochi minuti, si avrà una corretta distribuzione e iniziarne immagine hello toocreate per lo SKU.

### <a name="33-develop-your-vhd-in-hello-cloud"></a>3.3 sviluppare il disco rigido virtuale nel cloud hello
Si consiglia di sviluppare il disco rigido virtuale nel cloud hello tramite Remote Desktop Protocol (RDP). Connessione tooRDP con nome utente hello e la password specificati durante il provisioning.

> [!IMPORTANT]
> Se si sviluppa il VHD in locale (scelta non consigliata), vedere l'articolo relativo alla [creazione di un'immagine di macchina virtuale in locale](marketplace-publishing-vm-image-creation-on-premise.md). Scaricare il disco rigido virtuale non è necessaria se si sviluppa in cloud hello.
>
>

**Connetti tramite RDP usando hello [portale Microsoft Azure][link-azure-portal]**

1. Selezionare **Sfoglia** > **Macchine virtuali**.
2. Apre il pannello di macchine virtuali Hello. Verificare che tale macchina virtuale che si desidera tooconnect con hello è in esecuzione e quindi selezionarlo dall'elenco di hello di macchine virtuali distribuite.
3. Verrà visualizzata una blade che descrive hello seleziona macchina virtuale. Nella parte superiore di hello, fare clic su **Connetti**.
4. Si è nome utente di hello tooenter richiesta e la password specificata durante il provisioning.

**Connettersi tramite RDP usando PowerShell**

toodownload un computer locale tooa di file del desktop remoto, utilizzare hello [cmdlet Get-AzureRemoteDesktopFile][link-technet-2]. In ordine toouse questo cmdlet, è necessario nome hello tooknow del servizio hello e il nome di hello macchina virtuale. Se è stato creato hello VM da hello [portale Microsoft Azure][link-azure-portal], è possibile trovare queste informazioni nella casella delle proprietà della macchina virtuale:

1. Nel portale di Microsoft Azure hello selezionare **Sfoglia** > **macchine virtuali**.
2. Apre il pannello di macchine virtuali Hello. Selezionare hello macchina virtuale che è stato distribuito.
3. Verrà visualizzata una blade che descrive hello seleziona macchina virtuale.
4. Fare clic su **Proprietà**.
5. Hello prima parte del nome di dominio hello è il nome di servizio hello. nome host Hello è il nome di macchina virtuale hello.

    ![disegno][img-portal-vm-rdp]
6. file RDP per desktop locale dell'amministratore di hello creato VM toohello Hello cmdlet toodownload hello è come indicato di seguito.

        Get‐AzureRemoteDesktopFile ‐ServiceName “baseimagevm‐6820cq00” ‐Name “BaseImageVM” –LocalPath “C:\Users\Administrator\Desktop\BaseImageVM.rdp”

Ulteriori informazioni su RDP sono reperibile in MSDN nell'articolo hello [connettersi tooan macchina virtuale di Azure con RDP o SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx).

**Configurare una macchina virtuale e creare lo SKU**

Dopo aver hello il sistema operativo che viene scaricata disco rigido virtuale, utilizzare Hyper-v e configurare un toobegin VM creazione lo SKU. Procedura dettagliata è reperibile in hello seguendo il collegamento di TechNet: [installare Hyper-v e configurare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="34-choose-hello-correct-vhd-size"></a>3.4 scegliere dimensioni disco rigido virtuale corrette hello
sistema operativo Windows di Hello VHD dell'immagine di macchina virtuale deve essere creata come un disco rigido virtuale in formato fisso 128 GB.  

Se la dimensione fisica di hello è inferiore a 128 GB, hello disco rigido virtuale deve essere di tipo sparsa. immagini di Windows e SQL Server base Hello fornite già soddisfa questi requisiti, pertanto, non modificare hello formato o hello la dimensione del disco rigido virtuale ottenuto hello.  

I dischi dati possono avere dimensioni fino a 1 TB. Quando si scelgono dimensioni disco hello, tenere presente che i clienti non è possibile ridimensionare i dischi rigidi virtuali all'interno di un'immagine in fase di hello della distribuzione. I VHD dei dischi dati devono essere creati come VHD con formato fisso, ma devono anche essere di tipo sparse. I dischi dati possono essere vuoti o contenere dati.

### <a name="35-install-hello-latest-windows-patches"></a>3.5 installare patch più recente di Windows hello
le immagini di base Hello contengono le patch più recente di hello backup tootheir data di pubblicazione. Prima di pubblicare il sistema operativo hello disco rigido virtuale è stato creato, verificare che Windows Update è stato eseguito e che tutti hello critici più recenti e sono stati installati gli aggiornamenti della sicurezza importante.

### <a name="36-perform-additional-configuration-and-schedule-tasks-as-necessary"></a>3.6 Eseguire eventuali configurazioni aggiuntive e pianificare le attività nel modo necessario
Se è necessaria una configurazione aggiuntiva, considerare l'uso di un'attività pianificata che viene eseguito all'avvio toomake qualsiasi toohello modifiche finali VM dopo che è stato distribuito:

* È un'attività di hello di best practice toohave eliminare se stesso al termine dell'esecuzione ha esito positivo.
* Nessuna configurazione affidamento esclusivamente su unità diversa da unità C e D, perché queste offrono prestazioni hello solo due unità che è sempre garantita tooexist. L'unità C è disco del sistema operativo hello e D unità disco locale temporaneo hello.

### <a name="37-generalize-hello-image"></a>3.7 generalizzare l'immagine di hello
Tutte le immagini in Azure Marketplace hello devono essere riutilizzabile in modo generico. In altre parole, il sistema operativo hello disco rigido virtuale deve essere generalizzato:

* Per Windows, l'immagine hello deve essere "Sysprep" e nessuna configurazione devono essere eseguita che non supportano hello **sysprep** comando.
* È possibile eseguire hello comando seguente dalla finestra di windir%\System32\Sysprep directory hello.

        sysprep.exe /generalize /oobe /shutdown

  Informazioni aggiuntive su come sistema operativo di hello toosysprep viene fornito nel passaggio di hello MSDN articolo seguente: [creazione e caricamento di un disco rigido virtuale di Windows Server di tooAzure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="4-deploy-a-vm-from-your-vhds"></a>4. Distribuire una macchina virtuale dai VHD
Dopo aver caricato i dischi rigidi virtuali (VHD del sistema operativo generalizzato hello e zero o più dati su disco di dischi rigidi virtuali) tooan account di archiviazione di Azure, è possibile registrarli come immagine di macchina virtuale un utente. ed eseguirne il test. Si noti che, poiché il sistema operativo in disco rigido virtuale generalizzato, si hello VM non è possibile distribuire direttamente, fornendo hello URL VHD.

toolearn ulteriori informazioni sulle immagini di macchina virtuale, hello revisione post di blog seguente:

* [Immagine VM](https://azure.microsoft.com/blog/vm-image-blog-post/)
* [Procedure di PowerShell per immagini VM](https://azure.microsoft.com/blog/vm-image-powershell-how-to-blog-post/)
* [Informazioni sulle immagini di macchine virtuali in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)

### <a name="set-up-hello-necessary-tools-powershell-and-azure-cli"></a>Configurare gli strumenti necessari di hello, PowerShell e CLI di Azure
* [Come toosetup PowerShell](/powershell/azure/overview)
* [Come toosetup CLI di Azure](../cli-install-nodejs.md)

### <a name="41-create-a-user-vm-image"></a>4.1 Creare un'immagine di macchina virtuale degli utenti
#### <a name="capture-vm"></a>Acquisire la macchina virtuale
Leggere i collegamenti di hello forniti di seguito per informazioni sull'acquisizione hello macchina virtuale usando PowerShell/API/Azure CLI.

* [API](https://msdn.microsoft.com/library/mt163560.aspx)
* [PowerShell](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Interfaccia della riga di comando di Azure](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="generalize-image"></a>Generalizzare l'immagine
Leggere i collegamenti di hello forniti di seguito per informazioni sull'acquisizione hello macchina virtuale usando PowerShell/API/Azure CLI.

* [API](https://msdn.microsoft.com/library/mt269439.aspx)
* [PowerShell](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Interfaccia della riga di comando di Azure](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="42-deploy-a-vm-from-a-user-vm-image"></a>4.2 Distribuire una macchina virtuale da un'immagine di macchina virtuale degli utenti
toodeploy una macchina virtuale da un'immagine di macchina virtuale di utente, è possibile utilizzare hello corrente [portale di Azure](https://manage.windowsazure.com) o PowerShell.

**Distribuire una macchina virtuale dal portale di Azure corrente hello**

1. Andare troppo**New** > **calcolo** > **macchina virtuale** > **dalla raccolta**.

    ![disegno][img-manage-vm-new]
2. Andare troppo**immagini personali**, e quindi selezionare hello immagine di macchina virtuale da cui toodeploy una macchina virtuale:

   1. Pagamento attenzione toowhich l'immagine selezionata, in quanto hello **immagini personali** visualizzazione Elenca le immagini del sistema operativo e immagini di macchina virtuale.
   2. Esaminando il numero di hello dei dischi consente di determinare il tipo di immagine di distribuzione, perché la maggior parte hello di immagini di macchina virtuale dispone di più di un disco. Tuttavia, è comunque possibile toohave un'immagine di macchina virtuale con solo un singolo disco del sistema operativo che sarà necessario **numero di dischi** impostare too1.

      ![disegno][img-manage-vm-select]
3. Attenersi alla procedura guidata di creazione di VM hello e specificare il nome di macchina virtuale hello, dimensioni di macchina virtuale, percorso, nome utente e password.

**Distribuire una macchina virtuale da PowerShell**

toodeploy generalizzata di una macchina virtuale di grandi dimensioni da hello immagine di macchina virtuale appena creato, è possibile utilizzare hello cmdlet seguente.

    $img = Get-AzureVMImage -ImageName "myVMImage"
    $user = "user123"
    $pass = "adminPassword123"
    $myVM = New-AzureVMConfig -Name "VMImageVM" -InstanceSize "Large" -ImageName $img.ImageName | Add-AzureProvisioningConfig -Windows -AdminUsername $user -Password $pass
    New-AzureVM -ServiceName "VMImageCloudService" -VMs $myVM -Location "West US" -WaitForBoot

> [!IMPORTANT]
> Per maggiori informazioni, consultare l'articolo Risoluzione di problemi comuni incontrati durante la creazione del disco rigido virtuale.
>
>

## <a name="5-obtain-certification-for-your-vm-image"></a>5. Ottenere la certificazione per l'immagine di macchina virtuale
passaggio successivo di Hello nella preparazione dell'immagine di macchina virtuale per hello Azure Marketplace è toohave che sono certificate.

Questo processo include l'esecuzione di uno strumento di certificazione speciali, il caricamento di hello verifica risultati toohello immagine contenitore in cui si trovano i dischi rigidi virtuali di Azure, aggiunta di un'offerta, che definisce lo SKU e invio di una macchina virtuale per la certificazione.

### <a name="51-download-and-run-hello-certification-test-tool-for-azure-certified"></a>5.1 scaricare ed eseguire lo strumento di Test di certificazione hello per Azure Certified
strumento di certificazione Hello viene eseguito in una macchina virtuale in esecuzione, il provisioning dall'immagine VM utente, tooensure che hello immagine di macchina virtuale è compatibile con Microsoft Azure. Verificherà che siano stati soddisfatti indicazioni hello e requisiti sulla preparazione del disco rigido virtuale. output di Hello dello strumento hello è un report di compatibilità deve essere caricato in hello portale di pubblicazione durante la richiesta di certificazione.

strumento di certificazione Hello può essere utilizzato con le macchine virtuali Linux e Windows. Si connette a macchine virtuali basate su tooWindows tramite PowerShell e tooLinux VM SSH.Net:

1. Scaricare innanzitutto strumento certificazione hello hello [sito di download Microsoft][link-msft-download].
2. Aprire lo strumento di certificazione hello e quindi fare clic su hello **Avvia nuovo Test** pulsante.
3. Da hello **Test informazioni** schermata, immettere un nome per l'esecuzione dei test hello.
4. Specificare se la macchina virtuale è su Linux o Windows. A seconda che si sceglie, selezionare le opzioni successive hello.

### <a name="connect-hello-certification-tool-tooa-linux-vm-image"></a>**Connettersi hello certificazione strumento tooa immagine VM Linux**
1. Modalità di autenticazione SSH selezionare hello: file di chiave o password.
2. Se si utilizza l'autenticazione basata su password, immettere il nome di sistema DNS (Domain Name) hello, nome utente e password.
3. Se si utilizza l'autenticazione di file di chiave, immettere il nome DNS hello, nome utente e percorso della chiave privata.

   ![Autenticazione della password dell'immagine VM Linux][img-cert-vm-pswd-lnx]

   ![Autenticazione del file della chiave dell'immagine VM Linux][img-cert-vm-key-lnx]

### <a name="connect-hello-certification-tool-tooa-windows-based-vm-image"></a>**Immagine di macchina virtuale basata su Windows tooa di hello certificazione dello strumento di connessione**
1. Immettere il nome di macchina virtuale DNS hello completo (ad esempio, MyVMName.Cloudapp.net).
2. Immettere nome utente hello e password.

   ![Autenticazione della password dell'immagine VM Windows][img-cert-vm-pswd-win]

Dopo aver selezionato le opzioni corrette hello per l'immagine di Linux o macchina virtuale basata su Windows, selezionare **Test connessione** tooensure che SSH.Net o PowerShell dispone di una connessione valida a scopo di test. Dopo aver stabilita una connessione, selezionare **Avanti** test hello toostart.

Una volta completato il test di hello, si riceverà risultati hello (passaggio/errore/avviso) per ogni elemento di test.

![Test case per l'immagine VM Linux][img-cert-vm-test-lnx]

![Test case per l'immagine VM Windows][img-cert-vm-test-win]

Se uno di hello test non riesce, l'immagine non essere certificato. In questo caso, esaminare i requisiti di hello e apportare le modifiche necessarie.

Dopo hello automated test, viene richiesto un input aggiuntivo tooprovide nell'immagine di macchina virtuale tramite una schermata questionario.  Completare domande hello e quindi selezionare **Avanti**.

![Questionario dello strumento di certificazione][img-cert-vm-questionnaire]

![Questionario dello strumento di certificazione][img-cert-vm-questionnaire-2]

Dopo aver completato questionario hello, è possibile fornire informazioni aggiuntive, ad esempio informazioni di accesso SSH per l'immagine VM Linux hello e una spiegazione per le valutazioni non riuscite. È possibile scaricare i risultati dei test hello e file di log per hello eseguita test case questionario toohello risposte tooyour di addizione. Salvare i risultati di hello in hello i dischi rigidi virtuali nello stesso contenitore.

![Salvare i risultati del test di certificazione][img-cert-vm-results]

### <a name="52-get-hello-shared-access-signature-uri-for-your-vm-images"></a>5.2 ottenere l'URI di firma di accesso condiviso hello per le immagini di macchina virtuale
Durante il processo di pubblicazione di hello, specificare hello uniform resource identifier (URI) che portano tooeach di hello dischi rigidi virtuali per lo SKU è stata creata. Durante il processo di certificazione hello Microsoft necessita di accesso toothese dischi rigidi virtuali. Pertanto, è necessario toocreate un URI di firma di accesso condiviso per ogni disco rigido virtuale. Si tratta di hello URI che devono essere specificato nel **immagini** scheda hello portale di pubblicazione.

firma di accesso condiviso Hello URI creato deve rispettare toohello seguenti requisiti:

* Per la generazione degli URI di firma di accesso condiviso per i VHD, sono sufficienti le autorizzazioni List e Read­. Evitare di fornire accesso con autorizzazioni di scrittura o eliminazione.
* durata Hello per l'accesso deve essere un minimo di tre (3) settimane da quando viene creata la firma di accesso condiviso hello URI.
* toosafeguard per l'ora UTC giorno hello selezionare prima hello data corrente. Ad esempio, se hello data corrente è il 6 ottobre 2014, selezionare 5/10/2014.

URL di firma di accesso condiviso può essere generato in più modi tooshare il disco rigido virtuale di Azure Marketplace.
Seguenti sono hello 3 strumenti consigliati:

1.  Azure Storage Explorer
2.  Microsoft Storage Explorer
3.  Interfaccia della riga di comando di Azure

**Azure Storage Explorer (scelta consigliata per gli utenti di Windows)**

Di seguito sono hello operazioni per la generazione di URL SAS tramite Esplora archivi Azure

1. Scaricare [Azure Storage Explorer 6 Anteprima 3](https://azurestorageexplorer.codeplex.com/) da CodePlex. Andare troppo[Azure Storage Explorer 6 Preview](https://azurestorageexplorer.codeplex.com/) e fare clic su **"Scarica"**.

    ![disegno](media/marketplace-publishing-vm-image-creation/img5.2_01.png)

2. Scaricare [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) e installarlo dopo averlo decompresso.

    ![disegno](media/marketplace-publishing-vm-image-creation/img5.2_02.png)

3. Dopo l'installazione, aprire un'applicazione hello.
4. Fare clic su **Add Account**.

    ![disegno](media/marketplace-publishing-vm-image-creation/img5.2_03.png)

5. Specificare nome account di archiviazione hello, chiave dell'account di archiviazione e dominio di endpoint di archiviazione. Si tratta di account di archiviazione hello nella sottoscrizione di Azure in cui è stato lasciato il disco rigido virtuale nel portale di Azure.

    ![disegno](media/marketplace-publishing-vm-image-creation/img5.2_04.png)

6. Una volta connesso Azure Storage Explorer tooyour account di archiviazione specifico, verrà avviato con tutti i hello contiene nell'account di archiviazione hello. Selezionare il contenitore di hello in cui è stato copiato file VHD del disco del sistema operativo hello (anche dischi dati se sono applicabili per il proprio scenario).

    ![disegno](media/marketplace-publishing-vm-image-creation/img5.2_05.png)

7. Dopo aver selezionato il contenitore di blob hello, Azure Storage Explorer avvia la visualizzazione di file hello all'interno del contenitore di hello. Selezionare i file di immagine di hello (con estensione vhd) che deve toobe inviato.

    ![disegno](media/marketplace-publishing-vm-image-creation/img5.2_06.png)

8.  Dopo aver selezionato i file con estensione vhd hello nel contenitore di hello, fare clic su hello **sicurezza** scheda.

    ![disegno](media/marketplace-publishing-vm-image-creation/img5.2_07.png)

9.  In hello **sicurezza contenitore Blob** nella finestra di dialogo Impostazioni predefinite hello lasciare hello **livello di accesso** scheda e quindi fare clic su **firme di accesso condiviso** scheda.

    ![disegno](media/marketplace-publishing-vm-image-creation/img5.2_08.png)

10. Seguire i passaggi di hello di sotto di una firma di accesso condiviso URI per l'immagine con estensione vhd hello toogenerate:

    ![disegno](media/marketplace-publishing-vm-image-creation/img5.2_09.png)

    a. **Accesso consentito da:** toosafeguard per l'ora UTC giorno hello selezionare prima hello data corrente. Ad esempio, se hello data corrente è il 6 ottobre 2014, selezionare 5/10/2014.

    b. **Accesso consentito:** selezionare una data di almeno 3 settimane dopo hello **accesso consentito da** Data.

    c. **Azioni consentite:** hello seleziona **elenco** e **lettura** autorizzazioni.

    d. Se è stato selezionato il file con estensione vhd in modo corretto, quindi il file viene visualizzato in **tooaccess nome Blob** con estensione vhd.

    e. Fare clic su **Generate Signature**.

    f. In **generato condiviso firma URI di accesso di questo contenitore**, cercare hello seguente come evidenziato sopra:

       - Assicurarsi che l'immagine del nome di file e **"VHD"** in hello URI.
       - Alla fine di hello della firma hello, assicurarsi che **"= rl"** viene visualizzato. Questo indica che le autorizzazioni Read e List sono state fornite correttamente.
       - Al centro della firma hello, assicurarsi che **"sr = c"** viene visualizzato. Questo dimostra che l'utente dispone dell'accesso al livello contenitore

11. tooensure hello generato condivisi works URI firma di accesso, fare clic su **Test nel Browser**. È necessario avviare il processo di download di hello.

12. Copiare l'URI di firma di accesso condiviso hello. Si tratta di hello URI toopaste in hello portale di pubblicazione.

13. Ripetere i passaggi da 6 a 10 per ogni disco rigido virtuale in hello SKU.

**Microsoft Azure Storage Explorer (Windows/MAC/Linux)**

Di seguito sono hello operazioni per la generazione di URL SAS tramite Esplora archivi di Microsoft Azure

1.  Scaricare Microsoft Azure Storage Explorer dal sito Web [http://storageexplorer.com/](http://storageexplorer.com/). Andare troppo[Microsoft Azure Storage Explorer](http://storageexplorer.com/releasenotes.html) e fare clic su **"Download per Windows"**.

    ![disegno](media/marketplace-publishing-vm-image-creation/img5.2_10.png)

2.  Dopo l'installazione, aprire un'applicazione hello.

3.  Fare clic su **Add Account**.

4.  Configurare una sottoscrizione di Microsoft Azure Storage Explorer tooyour da tooyour account di accesso

    ![disegno](media/marketplace-publishing-vm-image-creation/img5.2_11.png)

5.  Account toostorage scegliere hello contenitore

6.  Selezionare **"Get Share Access Signature.."** ("Richiedi firma di accesso condiviso...") tramite il clic destro di hello **contenitore**

    ![disegno](media/marketplace-publishing-vm-image-creation/img5.2_12.png)

7.  Aggiornare la data di inizio, la scadenza e le autorizzazioni come indicato di seguito

    ![disegno](media/marketplace-publishing-vm-image-creation/img5.2_13.png)

    a.  **Ora di inizio:** toosafeguard per l'ora UTC giorno hello selezionare prima hello data corrente. Ad esempio, se hello data corrente è il 6 ottobre 2014, selezionare 5/10/2014.

    b.  **Ora di scadenza:** selezionare una data di almeno 3 settimane dopo hello **ora di inizio** Data.

    c.  **Autorizzazioni:** hello seleziona **elenco** e **lettura** autorizzazioni

8.  Copiare l'URI della firma di accesso condiviso per il contenitore

    ![disegno](media/marketplace-publishing-vm-image-creation/img5.2_14.png)

    URL di firma di accesso condiviso generato per contenitore di livello e abbiamo bisogno di nome VHD tooadd in essa contenuti.

    Formato dell'URL SAS livello contenitore: `https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    Inserisci nome VHD dopo il nome di contenitore hello nell'URL SAS come indicato di seguito`https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    Esempio:

    ![disegno](media/marketplace-publishing-vm-image-creation/img5.2_15.png)

    TestRGVM201631920152.vhd è hello VHD nome verrà utilizzato come URL di firma di accesso condiviso di disco rigido virtuale`https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    - Assicurarsi che l'immagine del nome di file e **"VHD"** in hello URI.
    - Al centro della firma hello, assicurarsi che **"sp = rl"** viene visualizzato. Questo indica che le autorizzazioni Read e List sono state fornite correttamente.
    - Al centro della firma hello, assicurarsi che **"sr = c"** viene visualizzato. Questo dimostra che l'utente dispone dell'accesso al livello contenitore

9.  tooensure che hello works URI firma di accesso condiviso generata, testarlo nel browser. È necessario avviare il processo di download di hello

10. Copiare l'URI di firma di accesso condiviso hello. Si tratta di hello URI toopaste in hello portale di pubblicazione.

11. Ripetere questi passaggi per ogni disco rigido virtuale in hello SKU.

**Interfaccia della riga di comando di Azure (scelta consigliata per integrazione continua e utenti non Windows)**

Di seguito sono hello operazioni per la generazione di URL SAS tramite l'interfaccia CLI di Azure

1.  Scaricare l'interfaccia della riga di comando di Azure da [qui](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/). Esistono diversi link per **[Windows](http://aka.ms/webpi-azure-cli)** e **[MAC OS](http://aka.ms/mac-azure-cli)**.

2.  Dopo averlo scaricato, installarlo

3.  Creare un file di PowerShell con il codice seguente e salvarlo in locale

          $conn="DefaultEndpointsProtocol=https;AccountName=<StorageAccountName>;AccountKey=<Storage Account Key>"
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl <Permission End Date> -c $conn --start <Permission Start Date>  

    Aggiornare il seguente hello parametri in precedenza

    a. **`<StorageAccountName>`**: per dare un nome all'account di archiviazione

    b. **`<Storage Account Key>`**: per dare una chiave all'account di archiviazione

    c. **`<Permission Start Date>`**: toosafeguard per l'ora UTC giorno hello selezionare prima hello data corrente. Ad esempio, se hello data corrente è 26 ottobre 2016, quindi il valore deve essere 25/10/2016

    d. **`<Permission End Date>`**: Selezionare una data di almeno 3 settimane dopo hello **data di inizio**. Il valore quindi sarà **02/11/2016**.

    Ecco il codice di esempio hello dopo aver aggiornato i parametri appropriati

          $conn="DefaultEndpointsProtocol=https;AccountName=st20151;AccountKey=TIQE5QWMKHpT5q2VnF1bb+NUV7NVMY2xmzVx1rdgIVsw7h0pcI5nMM6+DVFO65i4bQevx21dmrflA91r0Vh2Yw=="
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl 11/02/2016 -c $conn --start 10/25/2016  

4.  Aprire l'editor di Powershell con la modalità "Esegui come amministratore" e aprire i file nel passaggio #3.

5.  Script di esecuzione hello e fornirà che Hello URL SAS per l'accesso a livello di contenitore

    Output di hello parte hello firma SAS e copia hello evidenziato in blocco note sarà seguente

    ![disegno](media/marketplace-publishing-vm-image-creation/img5.2_16.png)

6.  Ora verrà visualizzato il livello di contenitore URL SAS e per conoscere il nome di file VHD tooadd in essa contenuti.

    URL SAS a livello di contenitore

    `https://st20151.blob.core.windows.net/vhds?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

7.  Inserisci nome VHD dopo il nome di contenitore hello nell'URL SAS, come illustrato di seguito`https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    Esempio:

    TestRGVM201631920152.vhd è hello VHD nome verrà utilizzato come URL di firma di accesso condiviso di disco rigido virtuale

    `https://st20151.blob.core.windows.net/vhds/ TestRGVM201631920152.vhd?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    - Assicurarsi che il nome del file immagine e "VHD" sono hello URI.
    -   Al centro della firma hello, assicurarsi che "sp = rl" viene visualizzato. Questo indica che le autorizzazioni Read e List sono state fornite correttamente.
    -   Al centro della firma hello, assicurarsi che "sr = c" viene visualizzato. Questo dimostra che l'utente dispone dell'accesso al livello contenitore

8.  tooensure che hello works URI firma di accesso condiviso generata, testarlo nel browser. È necessario avviare il processo di download di hello

9.  Copiare l'URI di firma di accesso condiviso hello. Si tratta di hello URI toopaste in hello portale di pubblicazione.

10. Ripetere questi passaggi per ogni disco rigido virtuale in hello SKU.


### <a name="53-provide-information-about-hello-vm-image-and-request-certification-in-hello-publishing-portal"></a>5.3 forniscono informazioni sull'immagine di macchina virtuale hello e richiesta di certificazione in hello portale di pubblicazione
Dopo aver creato l'offerta e SKU, è necessario immettere i dettagli dell'immagine hello associati a tale SKU:

1. Passare toohello [portale pubblicazione][link-pubportal]e quindi accedere con l'account.
2. Seleziona hello **immagini di macchina virtuale** scheda.
3. Identificatore Hello elencati all'inizio di hello di hello pagina è effettivamente identificatore dell'offerta hello e non identificatore SKU di hello.
4. Compilare le proprietà di hello in hello **SKU** sezione.
5. In **famiglia di sistemi operativi**, fare clic su tipo di sistema operativo hello associata con il sistema operativo hello disco rigido virtuale.
6. In hello **del sistema operativo** casella, descrivere hello del sistema operativo. Usare preferibilmente il formato famiglia di sistemi operativi, tipo, versione e aggiornamenti. Esempio: "Windows Server Datacenter 2014 R2".
7. Selezionare le dimensioni di macchina virtuale consigliate toosix. Si tratta di indicazioni che ottengono cliente toohello visualizzato nel Pannello di livello di prezzo hello nel portale di Azure hello quando decidere toopurchase e distribuire l'immagine. **Questi sono solo indicazioni. cliente Hello è in grado di tooselect qualsiasi dimensione di macchina virtuale che supporta dischi hello specificato nell'immagine.**
8. Immettere una versione di hello. il campo della versione Hello incapsula un prodotto di hello tooidentify versione semantica e i relativi aggiornamenti:
   * Versioni devono avere il formato di hello X.Y.Z, dove X, Y e Z sono numeri interi.
   * Le immagini in SKU diversi possono avere versioni principali e secondarie diverse.
   * Versioni all'interno di una SKU devono essere solo le modifiche incrementali, che aumentano la versione di patch hello (Z da X.Y.Z).
9. In hello **URL VHD del sistema operativo** , immettere una firma di accesso condiviso hello URI creato per il sistema operativo hello disco rigido virtuale.
10. Se sono presenti dischi dati associati a questo prodotto, selezionare hello unità logica toowhich (LUN) numero desiderato di questo toobe disco dati montati durante la distribuzione.
11. In hello **URL VHD di LUN X** , immettere una firma di accesso condiviso hello URI creato per i dati prima di hello disco rigido virtuale.

    ![disegno](media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-3.png)


## <a name="common-sas-url-issues--fixes"></a>Problemi e correzioni comuni dell'URL SAS

|Problema|Messaggio di errore|Correzione|Link alla documentazione|
|---|---|---|---|
|Errore durante la copia di immagini: "?" non è presente nell'URL SAS|Errore: copia di immagini. Non è possibile toodownload blob utilizzando fornito Uri SAS.|L'uso di Url SAS hello aggiornamento consigliato strumenti|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Errore durante la copia di immagini: parametri "st" e "se" non presenti nell'URL SAS|Errore: copia di immagini. Non è possibile toodownload blob utilizzando fornito Uri SAS.|Aggiornare hello Url SAS con date di inizio e fine.|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Errore durante la copia di immagini: "sp=rl" non è presente nell'URL SAS|Errore: copia di immagini. Non è possibile toodownload blob fornito Uri SAS|Aggiornare hello Url SAS con le autorizzazioni impostate come "Lettura" e "elenco|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Errore nella copia di immagini: l'URL SAS presenta spazi vuoti nel nome del file con estensione vhd|Errore: copia di immagini. Non è possibile toodownload blob utilizzando fornito Uri SAS.|Aggiornare hello Url SAS, senza spazi vuoti|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Errore nella copia di immagini: errore di autorizzazione URL SAS|Errore: copia di immagini. Blob non è possibile toodownload a causa di errore tooauthorization|Rigenerare hello Url SAS|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|


## <a name="next-step"></a>Passaggio successivo
Dopo avere completato con i dettagli SKU hello, è possibile spostare in avanti toohello [Guida contenuto marketing Azure Marketplace][link-pushstaging]. In questo passaggio di processo di pubblicazione hello, si fornisce hello marketing prima di necessarie altre informazioni, prezzi e contenuto troppo**passaggio 3: la macchina virtuale di test offrono in gestione temporanea**, in cui è testare vari scenari di casi di utilizzo prima della distribuzione Hello offerta toohello Azure Marketplace per visibilità pubblica e l'acquisto.  

## <a name="see-also"></a>Vedere anche
* [Guida introduttiva: come toopublish un toohello offerta Azure Marketplace](marketplace-publishing-getting-started.md)

[img-acom-1]:media/marketplace-publishing-vm-image-creation/vm-image-acom-datacenter.png
[img-portal-vm-size]:media/marketplace-publishing-vm-image-creation/vm-image-portal-size.png
[img-portal-vm-create]:media/marketplace-publishing-vm-image-creation/vm-image-portal-create-vm.png
[img-portal-vm-location]:media/marketplace-publishing-vm-image-creation/vm-image-portal-location.png
[img-portal-vm-rdp]:media/marketplace-publishing-vm-image-creation/vm-image-portal-rdp.png
[img-azstg-add]:media/marketplace-publishing-vm-image-creation/vm-image-storage-add.png
[img-manage-vm-new]:media/marketplace-publishing-vm-image-creation/vm-image-manage-new.png
[img-manage-vm-select]:media/marketplace-publishing-vm-image-creation/vm-image-manage-select.png
[img-cert-vm-key-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-keyfile-linux.png
[img-cert-vm-pswd-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-linux.png
[img-cert-vm-pswd-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-win.png
[img-cert-vm-test-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-linux.png
[img-cert-vm-test-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-win.png
[img-cert-vm-results]:media/marketplace-publishing-vm-image-creation/vm-image-certification-results.png
[img-cert-vm-questionnaire]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire.png
[img-cert-vm-questionnaire-2]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire-2.png
[img-pubportal-vm-skus]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus.png
[img-pubportal-vm-skus-2]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-2.png

[link-pushstaging]:marketplace-publishing-push-to-staging.md
[link-github-waagent]:https://github.com/Azure/WALinuxAgent
[link-azure-codeplex]:https://azurestorageexplorer.codeplex.com/
[link-azure-2]:../storage/blobs/storage-dotnet-shared-access-signature-part-2.md
[link-azure-1]:../storage/common/storage-dotnet-shared-access-signature-part-1.md
[link-msft-download]:http://www.microsoft.com/download/details.aspx?id=44299
[link-technet-3]:https://technet.microsoft.com/library/hh846766.aspx
[link-technet-2]:https://msdn.microsoft.com/library/dn495261.aspx
[link-azure-portal]:https://portal.azure.com
[link-pubportal]:https://publish.windowsazure.com
[link-sql-2014-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014enterprisewindowsserver2012r2/
[link-sql-2014-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014standardwindowsserver2012r2/
[link-sql-2014-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014webwindowsserver2012r2/
[link-sql-2012-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2enterprisewindowsserver2012/
[link-sql-2012-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2standardwindowsserver2012/
[link-sql-2012-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2webwindowsserver2012/
[link-datactr-2012-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012r2datacenter/
[link-datactr-2012]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012datacenter/
[link-datactr-2008-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2008r2sp1/
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-technet-1]:https://technet.microsoft.com/library/hh848454.aspx
[link-azure-vm-2]:./virtual-machines-linux-agent-user-guide/
[link-openssl]:https://www.openssl.org/
[link-intsvc]:http://www.microsoft.com/download/details.aspx?id=41554
[link-python]:https://www.python.org/
