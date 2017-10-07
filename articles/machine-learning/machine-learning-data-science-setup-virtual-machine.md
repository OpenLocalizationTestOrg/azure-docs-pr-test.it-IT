---
title: aaaSet rapidamente una macchina virtuale come server IPython Notebook | Documenti Microsoft
description: Configurare una macchina virtuale di Azure per usarla in un ambiente di analisi scientifica dei dati con IPython Server per le analisi avanzate.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 818617c1-048e-49c2-b941-f9a983f93998
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: 58386140ec7742ade1f7e183ec842a2b09b9dfca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>Configurare una macchina virtuale di Azure come server IPython Notebook per l'analisi avanzata
Questo argomento viene illustrato come tooprovision e configurare una macchina virtuale di Azure per analitica avanzata che può essere utilizzato come parte di un ambiente di analisi scientifica dei dati. macchina virtuale di Windows Hello è configurato con supporto di strumenti, ad esempio IPython Notebook, Azure Storage Explorer, AzCopy, nonché altre utilità che sono utili per i progetti analitica avanzate. Azure Storage Explorer e AzCopy, ad esempio, fornire agevolmente archiviazione blob di tooAzure tooupload dati dal computer locale o toodownload è tooyour locali dall'archiviazione blob.

## <a name="create-vm"></a>Passaggio 1: Creare una macchina virtuale di Azure per uso generico
Se si dispone già di una macchina virtuale di Azure e si desidera semplicemente tooset di un server di IPython Notebook su di esso, è possibile ignorare questo passaggio e procedere troppo[passaggio 2: aggiungere un endpoint per la macchina virtuale esistente di IPython notebook tooan](#add-endpoint).

Prima di iniziare il processo di hello di creazione di una macchina virtuale in Azure, è necessario dimensioni hello toodetermine di macchina hello dati hello tooprocess necessari per il progetto. Le macchine di dimensioni inferiori sono dotate di meno memoria e core CPU rispetto alle macchine di dimensioni più elevate, ma sono anche meno costose. Per un elenco di tipi di computer e sui prezzi, vedere hello <a href="http://azure.microsoft.com/pricing/details/virtual-machines/" target="_blank">macchine virtuali: prezzi </a> pagina

1. Accedi troppo<a href="https://manage.windowsazure.com" target="_blank">portale di Azure classico</a>, fare clic su **New** nell'angolo inferiore sinistro di hello. Viene visualizzata una finestra. Selezionare **CALCOLO** -> **MACCHINA VIRTUALE** -> **DA RACCOLTA**.
   
    ![Creare un'area di lavoro][24]
2. Scegliere una delle seguenti immagini hello:
   
   * Windows Server 2012 R2 Datacenter
   * Esperienza Windows Server Essentials (Windows Server 2012 R2)
     
     Quindi, fare clic sulla freccia di hello verso destra hello inferiore destra toogo hello pagina Configurazione successiva.
     
     ![Creare un'area di lavoro][25]
3. Immettere un nome per la macchina virtuale hello desiderato toocreate, dimensioni hello selezionare della macchina di hello (predefinita: A3) in base alle dimensioni di hello della macchina di hello dati hello è corso tooprocess e delle dimensioni desiderate hello macchina toobe (memoria hello dimensioni e il numero di core di calcolo) , immettere un nome utente e una password per la macchina hello. Quindi, fare clic sulla freccia di hello verso destra toogo toohello pagina di configurazione successiva.
   
    ![Creare un'area di lavoro][26]
4. Seleziona hello **AFFINITÀ di area/gruppo/rete virtuale** contenente hello **ACCOUNT di archiviazione** prevede toouse per questa macchina virtuale e quindi selezionare l'account di archiviazione. Aggiungere un endpoint nella parte inferiore di hello in hello **endpoint** campo immettendo hello nome dell'endpoint hello (qui per "IPython"). È possibile scegliere qualsiasi stringa come hello **nome** del punto di fine hello e qualsiasi numero intero compreso tra 0 e 65536 è **disponibile** come hello **porta pubblica**. Hello **porta privata** è toobe **9999**. È necessario **evitare** di usare le porte pubbliche già assegnate a servizi Internet. In <a href="http://www.chebucto.ns.ca/~rakerman/port-table.html" target="_blank">Porte per servizi Internet</a> viene fornito un elenco di porte già assegnate che non devono essere usate.
   
    ![Creare un'area di lavoro][27]
5. Fare clic sulla macchina virtuale hello segno di spunta toostart hello processo di provisioning.
   
    ![Creare un'area di lavoro][28]

Macchina virtuale hello toocomplete 25-15 minuti il processo di provisioning può richiedere. Dopo che è stata creata la macchina virtuale di hello, deve essere stato hello di questa macchina **esecuzione**.

![Creare un'area di lavoro][29]

## <a name="add-endpoint"></a>Passaggio 2: Aggiungere un endpoint per la macchina virtuale esistente di IPython notebook tooan
Se è stato creato seguendo le istruzioni di hello nel passaggio 1 macchina virtuale hello, endpoint hello per IPython Notebook è già stato aggiunto ed è possibile ignorare questo passaggio.

Se esiste già una macchina virtuale hello, ed è necessario un endpoint tooadd per IPython Notebook che verrà installato nel passaggio 3 riportato di seguito, primo account di accesso tooAzure portale classico, selezionare la macchina virtuale di hello e aggiungere endpoint hello per server IPython Notebook. Hello figura riportata di seguito contiene una cattura di schermata del portale hello dopo aver aggiunto endpoint hello per IPython Notebook tooa macchina virtuale di Windows.

![Creare un'area di lavoro][17]

## <a name="run-commands"></a>Passaggio 3: Installare IPython Notebook e altri strumenti di supporto
Dopo la creazione di macchine virtuali hello, usare Remote Desktop Protocol (RDP) toolog in toohello macchina virtuale di Windows. Per istruzioni, vedere [come tooLog nella macchina virtuale che esegue Windows Server tooa](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Aprire hello **prompt dei comandi** (**non finestra di comando Powershell hello**) come un **amministratore** e hello esecuzione comando seguente.

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

Al termine di installazione di hello, hello server IPython Notebook viene avviato automaticamente in hello *c:\\utenti\\\<nome utente\>\\documenti\\IPython Notebook* directory.

Quando richiesto, immettere una password per hello IPython Notebook e la password di hello dell'amministratore del computer hello. In questo modo hello IPython Notebook toorun come servizio nel computer di hello.

## <a name="access"></a>Passaggio 4: Accedere a IPython Notebook da un Web browser
hello tooaccess server IPython Notebook, aprire un web browser e input *nome DNS del computer https://&#60;virtual >: &#60; numero di porta pubblica >* nella casella di testo URL hello. In questo caso, hello *&#60; numero di porta pubblica >* hello numero di porta specificato quando hello endpoint IPython Notebook è stato aggiunto.

Hello *&#60; nome DNS della macchina virtuale >* è reperibile in hello portale di Azure classico. Dopo la registrazione nel portale classico toohello, fare clic su **macchine VIRTUALI**selezionare macchina hello è creato e quindi selezionare **DASHBOARD**, verrà visualizzato il nome DNS hello come indicato di seguito:

![Creare un'area di lavoro][19]

Verrà visualizzato un avviso che informa che *si è verificato un problema con il certificato di sicurezza del sito Web* (Internet Explorer) o *la connessione non è privata* (Chrome), come illustrato nell'esempio hello nelle figure. Fare clic su **sito Web toothis continua (non consigliato)** (Internet Explorer) o **avanzate** e quindi  **procedere troppo &#60;* Nome DNS*> (non sicuro) * * toocontinue (Chrome). Quindi immettere una password di hello è specificato tooaccess precedenti hello IPython notebook.

**Internet Explorer:**
![Creare un'area di lavoro][20]

**Chrome:**
![Creare un'area di lavoro][21]

Dopo l'accesso toohello IPython Notebook, una directory *DataScienceSamples* verranno visualizzati nel browser hello. Questa directory contiene esempio IPython notebook condivisi da attività di analisi scientifica dei dati di Microsoft toohelp utenti comportamento. Questi esempio IPython notebook vengono estratti dal [ **repository GitHub** ](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) toohello le macchine virtuali durante il processo di installazione server IPython Notebook hello. Microsoft gestisce e aggiorna frequentemente questi repository. Gli utenti possono visitare hello GitHub repository tooget aggiornato di recente: esempio hello IPython notebook.
![Creare un'area di lavoro][18]

## <a name="upload"></a>Passaggio 5: Caricare un blocco appunti IPython esistente da un server IPython Notebook di toohello computer locale
IPython notebook forniscono un modo semplice per tooupload agli utenti un blocco appunti IPython esistente nel loro toohello computer locali, server IPython Notebook nelle macchine virtuali hello. Dopo l'accesso toohello IPython Notebook in un web browser, fare clic su in hello **directory** tale hello IPython Notebook verrà caricato. Selezionare quindi un tooupload di IPython Notebook .ipynb file dal computer locale di hello in hello **Esplora File**e trascinamento della selezione è toohello directory IPython Notebook nel browser web hello. Fare clic su hello **caricare** pulsante tooupload hello .ipynb file toohello server IPython Notebook. Gli altri utenti potranno quindi iniziare a usarlo dai Web browser di cui dispongono.

![Creare un'area di lavoro][22]

![Creare un'area di lavoro][23]

## <a name="shutdown"></a>Arrestare e deallocare la macchina virtuale quando non è in uso
Macchine virtuali di Azure è disponibile con **pagamento a consumo**. tooensure che non vengono fatturate quando non si utilizza la macchina virtuale, è toobe in hello **arrestato (deallocato)** stato quando non è in uso.

> [!NOTE]
> Se si arresta macchina virtuale hello in all'interno di macchina virtuale (tramite Opzioni risparmio energia di Windows), hello hello VM è stato arrestato ma rimane allocata. tooensure toobe fatturati, non si continua sempre arrestare le macchine virtuali da hello [portale di Azure classico](http://manage.windowsazure.com/). È anche possibile arrestare hello VM tramite Powershell chiamando **ShutdownRoleOperation** con "PostShutdownAction" uguale troppo "StoppedDeallocated".
> 
> 

tooshut verso il basso e deallocare una macchina virtuale hello:

1. Accedi toohello [portale di Azure classico](http://manage.windowsazure.com/) con l'account.  
2. Selezionare **macchine VIRTUALI** dalla barra di spostamento a sinistra di hello.
3. Nell'elenco di hello delle macchine virtuali, fare clic sul nome hello la macchina virtuale, quindi passa toohello **DASHBOARD** pagina.
4. Nella parte inferiore di hello della pagina hello, fare clic su **arresto**.

![Arresto della macchina virtuale][15]

macchina virtuale Hello verranno deallocata ma non eliminato. È possibile riavviare la macchina virtuale in qualsiasi momento da hello portale di Azure classico.

## <a name="your-azure-vm-is-ready-toouse-whats-next"></a>La macchina virtuale di Azure è pronta toouse: che cos'è successivo?
La macchina virtuale è ora pronto toouse negli esercizi di analisi scientifica dei dati. macchina virtuale Hello è pronto per l'utilizzo come un server di IPython Notebook per l'elaborazione dei dati e l'esplorazione di hello e altre attività in combinazione con Azure Machine Learning e hello processo di analisi scientifica dei dati del Team.

Hello passaggi successivi nel processo di analisi scientifica dei dati di Team vengono mappati in hello hello [percorso di apprendimento](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) e possono includere passaggi spostare i dati in HDInsight, processo e, di esempio in preparazione per l'apprendimento dai dati hello con Azure macchina Apprendimento.

[15]: ./media/machine-learning-data-science-setup-virtual-machine/vmshutdown.png
[17]: ./media/machine-learning-data-science-setup-virtual-machine/add-endpoints-after-creation.png
[18]: ./media/machine-learning-data-science-setup-virtual-machine/sample-ipnbs.png
[19]: ./media/machine-learning-data-science-setup-virtual-machine/dns-name-and-host-name.png
[20]: ./media/machine-learning-data-science-setup-virtual-machine/browser-warning-ie.png
[21]: ./media/machine-learning-data-science-setup-virtual-machine/browser-warning.png
[22]: ./media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-1.png
[23]: ./media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-2.png
[24]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-1.png
[25]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-2.png
[26]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-3.png
[27]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-4.png
[28]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-5.png
[29]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-6.png
