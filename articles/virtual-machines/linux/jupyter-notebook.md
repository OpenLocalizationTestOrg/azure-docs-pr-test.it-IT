---
title: aaaCreate un Notebook Jupyter/IPython | Documenti Microsoft
description: Informazioni su come creata i toodeploy hello Notebook Jupyter/IPython in una macchina virtuale Linux con modello di distribuzione Gestione risorse hello in Azure.
services: virtual-machines-linux
documentationcenter: python
author: crwilcox
manager: wpickett
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 519f36dd-865e-4c1d-abe7-b87037796aa7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 11/10/2015
ms.author: crwilcox
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d7f2e45a8ba95163ebfb0f10babc91a2b3fd9390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a>Creazione di una macchina virtuale di Azure, installazione di Jupyter ed esecuzione di Jupyter Notebook in Azure
Hello [Jupyter progetto](http://jupyter.org), precedentemente hello [IPython progetto](http://ipython.org), fornisce una raccolta di strumenti per l'elaborazione scientifica utilizzando una potente shell interattiva che combinano l'esecuzione del codice con la creazione di hello di un documento di calcolo in tempo reale. I file dei blocchi appunti possono contenere testo arbitrario, formule matematiche, codice di input, risultati, grafica, video e altri tipi di contenuti multimediali visualizzabili sui moderni Web browser. Se si sta tooPython assolutamente nuovo e si desidera toolearn in una divertente, ambiente interattivo o eseguire alcune grave parallelo o tecnico computing, hello server Jupyter Notebook rappresenta un'ottima scelta.

![Schermata di](./media/jupyter-notebook/ipy-notebook-spectral.png) SciPy usando Matplotlib pacchetti tooanalyze hello struttura e di una registrazione audio.

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a>Due modi di Jupyter: Azure Notebook o distribuzione personalizzata
Azure fornisce un servizio che è possibile utilizzare anche[iniziare rapidamente a utilizzare Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).  Utilizzando hello Azure Notebook servizio, è possibile ottenere facilmente interfaccia web accessibile del tooJupyter accesso alle risorse di calcolo scalabile con tutta la potenza di hello di Python e le relative librerie molti.  Poiché l'installazione di hello viene gestita dal servizio hello, gli utenti possono accedere a queste risorse senza necessità di hello di amministrazione e configurazione utente hello.

Se il servizio di notebook hello non funziona per lo scenario continuare tooread in questo articolo in cui verrà sono visualizzate come toodeploy hello server Jupyter Notebook in Microsoft Azure, utilizzando macchine virtuali Linux (VM).

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a>Creazione e configurazione di una macchina virtuale in Azure
primo passaggio Hello è toocreate una macchina virtuale (VM) in esecuzione in Azure.
Questa macchina virtuale è un sistema operativo completo nel cloud hello e verrà utilizzata per eseguire hello server Jupyter Notebook. È in grado di eseguire le macchine virtuali Linux e Windows Azure e illustra l'installazione di hello del server Jupyter su entrambi i tipi di macchine virtuali.

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a>Creare una VM Linux e aprire una porta per Jupyter
Seguire le istruzioni di hello data [qui] [ portal-vm-linux] toocreate una macchina virtuale di hello *Ubuntu* distribuzione. Questa esercitazione utilizza Ubuntu Server 14.04 LTS. Si presupporrà che il nome di utente hello *azureuser*.

Dopo la distribuzione di macchina virtuale hello è necessario tooopen una regola di protezione nel gruppo di sicurezza di rete hello.  Dal portale di Azure hello, andare troppo**gruppi di sicurezza di rete** scheda hello open per hello tooyour corrispondente di gruppo di protezione VM e. È necessario tooadd una regola di sicurezza in ingresso con hello seguenti impostazioni: **TCP** per il protocollo hello  **\***  per la porta di origine (pubblico) hello e **9999** per porta di destinazione (privato) Hello.

![Schermata](./media/jupyter-notebook/azure-add-endpoint.png)

Mentre nel gruppo di sicurezza di rete, fare clic su **interfacce di rete** e hello nota **indirizzo IP pubblico** poiché sarà necessario tooconnect tooyour VM nel passaggio successivo hello.

## <a name="install-required-software-on-hello-vm"></a>Installare il software necessario in hello VM
toorun hello server Jupyter Notebook la macchina virtuale, sarà necessario installare innanzitutto Jupyter e le relative dipendenze. Connettere la macchina virtuale linux tooyour tramite ssh e coppia di nome utente/password hello scelto al momento della creazione hello macchina virtuale. In questa esercitazione verrà utilizzato PuTTY e ci si connetterà da Windows.

### <a name="installing-jupyter-on-ubuntu"></a>Installazione di Jupyter su Ubuntu
Installare Anaconda, una distribuzione di python di analisi scientifica dei dati comuni, utilizzando uno dei collegamenti hello forniti da [Continuum Analitica](https://www.continuum.io/downloads).  A partire dalla scrittura hello di questo documento, hello collegamenti riportati di seguito sono hello più backup toodate versioni.

#### <a name="anaconda-installs-for-linux"></a>Installazione di Anaconda per Linux
<table>
  <th>Python 3.4</th>
  <th>Python 2.7</th>
  <tr>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </td>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </td>
  </tr>
  <tr>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </td>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a>Installazione di Anaconda3 2.3.0 a 64 bit su Ubuntu
Ad esempio, in questo modo è possibile installare Anaconda su Ubuntu

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter toohello latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![Schermata](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a>Configurazione di Jupyter e utilizzo di SSL
Dopo l'installazione è necessario tootake un file di configurazione attualmente hello toosetup per Jupyter. Se si verificano dei problemi relativi alla configurazione Jupyter potrebbe essere utile toolook in hello [Jupyter documentazione per l'esecuzione di un Server Notebook](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).

Avanti è `cd` toohello profilo toocreate directory il certificato SSL e modificare i file di configurazione di profili di hello.

In Linux usare hello comando seguente.

    cd ~/.jupyter

Utilizzare hello successivo comando toocreate hello certificato SSL (Linux e Windows).

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

Si noti che poiché viene creato un certificato SSL autofirmato, quando ci si connette toohello notebook nel browser verrà visualizzato un avviso di sicurezza.  Per la produzione a lungo termine, sarà necessario toouse un certificato firmato correttamente associato all'organizzazione.  Poiché la gestione dei certificati esula dall'ambito hello di questa dimostrazione, si verrà soffermeremo certificato autofirmato tooa per ora.

Inoltre toousing un certificato, è necessario fornire anche un tooprotect password notebook da usi non autorizzati.  Per motivi di sicurezza Jupyter password crittografate nel file di configurazione, pertanto sarà necessario tooencrypt la password viene utilizzata prima.  IPython fornisce un toodo utilità. a un prompt dei comandi eseguire hello comando seguente.

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

Questo richiederà una password e conferma e verrà quindi password hello. Annotare questo per hello riportata dopo il passaggio.

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided hello rest for security)

Successivamente, è necessario modificare i file di configurazione del profilo di hello, ovvero il `jupyter_notebook_config.py` file nella directory hello in.  Si noti che questo file non esiste, crearla solo se è questo caso hello.  Questo file contiene alcuni campi, tutti impostati come commento per impostazione predefinita.  È possibile aprire questo file con qualsiasi editor di testo di base alle proprie esigenze, e accertarsi che ha almeno hello in seguito il contenuto. **Essere c.NotebookApp.password di hello tooreplace che nella configurazione di hello con sha1 hello dal passaggio precedente hello**.

    c = get_config()

    # You must give hello path toohello certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-hello-jupyter-notebook"></a>Eseguire hello server Jupyter Notebook
A questo punto siamo toostart pronto hello server Jupyter Notebook. toodo, passare toohello directory desiderato notebook toostore e avviare hello server Jupyter Notebook con hello comando seguente.

    /anaconda3/bin/jupyter-notebook

Dovrebbe ora essere in grado di tooaccess Jupyter Notebook all'indirizzo hello `https://[PUBLIC-IP-ADDRESS]:9999`.

Quando si accede a notebook, pagina di accesso hello richiede la password. E quando si accede, verrà visualizzato hello "Jupyter Notebook Dashboard", ovvero il centro ontrollo per tutte le operazioni di blocco note.  In questa pagina è possibile creare nuovi blocchi appunti e aprire quelli esistenti.

![Schermata](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-hello-jupyter-notebook"></a>Utilizzo di hello server Jupyter Notebook
Se si fa clic hello **New** pulsante, verrà visualizzato hello seguente pagina di apertura.

![Schermata](./media/jupyter-notebook/jupyter-untitled-notebook.png)

area Hello contrassegnati con un `In []:` prompt dei comandi è l'area di input hello, qui è possibile digitare qualsiasi codice Python valido e verrà eseguito quando si raggiunge `Shift-Enter` o fare clic sull'icona "Play" hello (hello verso destra triangolo nella barra degli strumenti hello).

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a>Un potente paradigma: documenti di calcolo in tempo reale con contenuti multimediali
blocco appunti Hello stesso dovrebbero risultare tooanyone molto naturale che ha utilizzato Python e un elaboratore di testo, perché è in qualche modo una combinazione di entrambi: è possibile eseguire i blocchi di codice Python, ma è anche possibile mantenere le note e altro testo modificando troppo stile hello di una cella da "Code" "Ma rkdown"utilizzando il menu di scelta rapida hello nella barra degli strumenti.

Jupyter è molto di più di un elaboratore di testo, in quanto consente di combinare calcolo e contenuti multimediali, ossia testo, grafica, video e qualsiasi altro contenuto visualizzabile in un moderno Web browser. È possibile combinare, testo, codice, video e altro ancora!

![Schermata](./media/jupyter-notebook/jupyter-editing-experience.png)

E con la potenza di molte librerie eccellente di Python per il calcolo di scientifici e tecnici, nella seguente schermata hello hello un calcolo semplice può essere eseguito con hello stesso semplificano come un'analisi di rete complessi, in un ambiente.

Questo paradigma di combinazione di risparmio energia hello Web moderna hello con calcolo in tempo reale offre molte possibilità ed è idealmente appropriato per il cloud hello. è possibile utilizzare Hello Notebook:

* Toorecord un calcolo area dettatura esplorativo collaborare su un problema.
* tooshare risultati con i colleghi, nel modulo di calcolo 'in tempo reale' o in copia cartacea formati (HTML, PDF).
* toodistribute e presente in tempo reale per insegnanti materiali che implicano il calcolo, in modo studenti sperimentare immediatamente codice effettivo hello, modificarlo ed eseguirla di nuovo in modo interattivo.
* tooprovide "paper eseguibile" per visualizzare i risultati hello della ricerca in modo che può essere riprodotta immediatamente, convalidato ed esteso da altri utenti.
* Come piattaforma per il calcolo collaborazione: più utenti possono accedere toothe stesso server notebook tooshare una sessione di calcolo in tempo reale.

Se si passa il codice sorgente IPython toohello [repository][repository], si noterà un'intera directory con gli esempi di notebook che è possibile scaricare e quindi provare a utilizzare la propria macchina virtuale Jupyter di Azure.  Basta scaricare hello `.ipynb` file hello del sito e caricarle in dashboard hello del blocco note macchina virtuale di Azure (o scaricarli direttamente in hello VM).

## <a name="conclusion"></a>Conclusioni
Hello Server Jupyter Notebook fornisce un'interfaccia potente per accedere in modo interattivo power hello dell'ecosistema di hello Python in Azure.  Rende possibile un'ampia gamma di casi di utilizzo, tra cui la semplice esplorazione di Python per apprenderne le funzionalità, l'analisi e la visualizzazione di dati, la simulazione e l'elaborazione parallela. documenti Notebook risultanti Hello contengono un record completo dei calcoli hello che vengono eseguiti e possono essere condivisi con altri utenti Jupyter.  Hello Server Jupyter Notebook può essere utilizzato come un'applicazione locale, ma è ideale per le distribuzioni di cloud in Azure

funzionalità di base di Hello di Jupyter sono inoltre disponibili all'interno di Visual Studio tramite il [Python Tools per Visual Studio] [ Python Tools for Visual Studio] (PTVS). un plug-in open source reso disponibile da Microsoft che trasforma Visual Studio in un ambiente di sviluppo Python avanzato, con l'integrazione di un editor avanzato con IntelliSense, debug, profili ed elaborazione parallela.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere hello [Centro per sviluppatori Python](/develop/python/).

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
