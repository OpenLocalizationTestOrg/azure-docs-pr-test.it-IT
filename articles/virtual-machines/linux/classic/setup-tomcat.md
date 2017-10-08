---
title: aaaSet backup Apache Tomcat in una macchina virtuale Linux | Documenti Microsoft
description: Informazioni su come tooset backup Tomcat7 Apache tramite le macchine virtuali di Azure che eseguono Linux.
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 45ecc89c-1cb0-4e80-8944-bd0d0bbedfdc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: ningk
ms.openlocfilehash: b837a73e91fcb25d5459d993a0e93ceef1a1fc8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a>Configurare Tomcat7 in una macchina virtuale Linux con Azure
Apache Tomcat (o semplicemente Tomcat, anche in precedenza denominato Tomcat Giacarta) è un server web di origine aperti e il contenitore servlet sviluppato da hello Apache Software Foundation ASF (). Tomcat implementa hello Servlet Java e le specifiche Java Server Pages (JSP) hello di Sun Microsystems. Tomcat fornisce un ambiente di server web HTTP Java puro in cui toorun codice Java. In configurazione più semplice hello Tomcat viene eseguito in un processo unico sistema operativo. Questo processo esegue una macchina virtuale Java (JVM). Ogni richiesta HTTP da un browser di tooTomcat viene elaborato come un thread separato nel processo di Tomcat hello.  

> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager e classico](../../../resource-manager-deployment-model.md). Questo articolo descrive come toouse hello modello di distribuzione classica. È consigliabile che più nuove distribuzioni di usare il modello di gestione risorse hello. vedere toouse toodeploy di modello un VM Ubuntu con Open JDK e Tomcat, un gestore delle risorse [questo articolo](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).

In questo articolo si installerà Tomcat7 su un'immagine Linux e la si distribuirà in Azure.  

Si acquisiranno le nozioni seguenti:  

* Come toocreate una macchina virtuale in Azure.
* Tooprepare hello come macchina virtuale per Tomcat7.
* Come tooinstall Tomcat7.

La procedura presuppone che l'utente disponga già di una sottoscrizione di Azure.  Se non è possibile iscriversi per una valutazione gratuita in [hello sito Web di Azure](https://azure.microsoft.com/). Se si ha un abbonamento MSDN, vedere [Offerte speciali di Microsoft Azure: vantaggi per i membri di MSDN, MPN e Bizspark](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39). toolearn ulteriori informazioni su Azure, vedere [cos'è Azure?](https://azure.microsoft.com/overview/what-is-azure/).

Questo articolo presuppone che l'utente abbia una conoscenza pratica di base di Tomcat e Linux.  

## <a name="phase-1-create-an-image"></a>Fase 1: creare un'immagine.
In questa fase si creerà una macchina virtuale usando un'immagine Linux in Azure.  

### <a name="step-1-generate-an-ssh-authentication-key"></a>Passaggio 1: generare una chiave di autenticazione SSH
SSH è uno strumento importante per gli amministratori di sistema. Non è consigliabile tuttavia configurare la protezione di accesso in base a una password stabilita da una persona fisica. Con un nome utente e una password debole, il sistema può essere esposto all'attacco da parte di utenti malintenzionati.

buone notizie Hello sono che non esiste un modo tooleave di accesso remoto aprire senza doversi preoccupare delle password. Il metodo consiste nell'autenticazione con crittografia asimmetrica. Hello chiave privata dell'utente è hello uno che consente l'autenticazione di hello. È anche possibile bloccare hello account utente toonot consentire l'autenticazione di password.

Un altro vantaggio di questo metodo è che non è necessario toosign password diverse toodifferent server. È possibile eseguire l'autenticazione usando la chiave privata personale hello in tutti i server, che consente di evitare tooremember password diversi.



Seguire questi passaggi toogenerate hello autenticazione la chiave SSH.

1. Scaricare e installare PuTTYgen dalla seguente posizione hello: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
2. Eseguire Puttygen.exe.
3. Fare clic su **genera** chiavi hello toogenerate. Nel processo di hello, è possibile aumentare la casualità per lo spostamento del mouse hello sull'area vuota di hello nella finestra di hello.  
   ![PuTTY schermata generatore di chiavi che mostra hello generare di nuovo pulsante chiave][1]
4. Dopo aver hello genera processo, Puttygen.exe mostrerà la nuova chiave pubblica.  
   ![Schermata di generatore di chiavi puTTY che mostra nuova chiave pubblica hello e hello salvare pulsante chiave privata][2]
5. Selezionare e copiare la chiave pubblica di hello e salvarlo in un file denominato publicKey.pem. Non fare clic su **Salva la chiave pubblica**, poiché hello salvato il formato di file della chiave pubblica è diversa dalla chiave pubblica di hello desiderato.
6. Fare clic su **Save private key** e salvarla in un file denominato privateKey.ppk.

### <a name="step-2-create-hello-image-in-hello-azure-portal"></a>Passaggio 2: Creare l'immagine di hello in hello portale di Azure
1. In hello [portale](https://portal.azure.com/), fare clic su **New** nel hello attività barra toocreate un'immagine. Scegliere l'immagine Linux hello che è in base alle proprie esigenze. Hello esempio seguente Usa immagine Ubuntu 14.04 hello.
![Schermata del portale hello che mostra il pulsante nuovo hello][3]

2. Per **nome Host**, specificare nome hello URL hello che i client Internet dovranno essere utilizzate dalle tooaccess questa macchina virtuale. Definire l'ultima parte di hello del nome DNS hello, ad esempio, tomcatdemo. Azure genera quindi l'URL di hello come tomcatdemo.cloudapp.net.  

3. Per **chiave di autenticazione SSH**, copiarne il valore della chiave hello file publicKey.pem hello che contiene la chiave pubblica hello generata da PuTTYgen.  
![Chiave di autenticazione SSH casella nel portale di hello][4]

4. Configurare altre impostazioni in base alle esigenze, quindi fare clic su **Crea**.  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a>Fase 2: preparare la macchina virtuale per Tomcat7
In questa fase, si configura un endpoint per il traffico di Tomcat e connettiti tooyour nuova macchina virtuale.

### <a name="step-1-open-hello-http-port-tooallow-web-access"></a>Passaggio 1: Aprire hello HTTP porta tooallow web access
Gli endpoint di Azure sono costituiti da un protocollo TCP o UDP, insieme a una porta pubblica e privata. porta privata Hello è porta hello che hello servizio è in ascolto macchina virtuale di tooon hello. porta pubblica Hello è porta hello hello servizio cloud di Azure è in ascolto tooexternally per il traffico in ingresso, basato su Internet.  

La porta TCP 8080 è numero di porta predefinito hello Tomcat utilizzato toolisten. Se si apre questa porta con un endpoint di Azure, l'utente e altri client Internet potranno accedere alle pagine Tomcat.  

1. Nel portale di hello, fare clic su **Sfoglia** > **macchine virtuali**, quindi fare clic su hello macchina virtuale in cui è stato creato.  
   ![Schermata della directory di hello macchine virtuali][5]
2. tooadd una macchina virtuale tooyour endpoint, fare clic su hello **endpoint** casella.
   ![Schermata che Mostra casella endpoint hello][6]
3. Fare clic su **Aggiungi**.  

   1. Per l'endpoint di hello, immettere un nome per l'endpoint hello **Endpoint**, quindi immettere 80 in **porta pubblica**.  

      Se si imposta la proprietà too80, non è necessario tooinclude numero di porta hello in URL hello utilizzati tooaccess Tomcat. Ad esempio, http://tomcatdemo.cloudapp.net.    

      Se si imposta il valore di tooanother, ad esempio 81, è necessario tooadd hello porta numero toohello URL tooaccess Tomcat. Ad esempio http://tomcatdemo.cloudapp.net:81/.
   2. Digitare 8080 in **Porta privata**. Per impostazione predefinita Tomcat è in ascolto sulla porta TCP 8080. Se è stata modificata hello predefinito ascolto porta di Tomcat, è necessario aggiornare **porta privata** toobe hello stesso hello porta di ascolto Tomcat.  
      ![Schermata dell'interfaccia utente che mostra il comando Aggiungi, Porta pubblica e Porta privata][7]
4. Fare clic su **OK** la macchina virtuale tooadd hello endpoint tooyour.

### <a name="step-2-connect-toohello-image-you-created"></a>Passaggio 2: Connettere immagine toohello creato
È possibile scegliere qualsiasi macchina virtuale SSH strumento tooconnect tooyour. In questo esempio viene usato PuTTY.  

1. Ottenere il nome DNS hello della macchina virtuale dal portale di hello.
    1. Fare clic su **Sfoglia** > **Macchine virtuali**.
    2. Selezionare il nome di hello della macchina virtuale e quindi fare clic su **proprietà**.
    3. In hello **proprietà** riquadro, cercare in hello **nome di dominio** nome DNS della casella tooget hello.  

2. Ottenere il numero di porta hello per le connessioni SSH da hello **SSH** casella.  
![Schermata che mostra i numero di porta di connessione SSH hello][8]

3. Scaricare [PuTTY](http://www.putty.org/).  

4. Dopo il download, fare clic sul file eseguibile hello Putty.exe. Configurazione PuTTY, configurare le opzioni di base hello con il nome host hello e il numero ottenuto dalla proprietà hello della macchina virtuale porta.   
![Schermata che mostra l'host di configurazione di PuTTY hello opzioni di nome e la porte][9]

5. Nel riquadro di sinistra hello, fare clic su **connessione** > **SSH** > **Auth**, quindi fare clic su **Sfoglia** toospecify percorso di Hello del file di privateKey.ppk hello. file privateKey.ppk Hello contiene la chiave privata hello generato da PuTTYgen in hello "fase 1: creare un'immagine" sezione di questo articolo.  
![Schermata che illustra una gerarchia di directory hello connessione e il pulsante Sfoglia][10]

6. Fare clic su **Apri**. Si potrebbe ricevere un avviso da una finestra di messaggio. Se è stato configurato il nome DNS hello e il numero di porta corretto, fare clic su **Sì**.
![Schermata che illustra la notifica hello][11]

7. Si sono tooenter richiesto il nome utente.  
![Schermata che mostra dove nome utente tooenter][12]

8. Immettere un nome utente hello utilizzato macchina virtuale di toocreate hello in hello "fase 1: creare un'immagine" sezione più indietro in questo articolo. Si noterà simile alla seguente hello:  
![Schermata che Mostra conferma authentication hello][13]

## <a name="phase-3-install-software"></a>Fase 3: installare il software
In questa fase, installare Java runtime environment di hello Tomcat7 e altri componenti Tomcat7.  

### <a name="java-runtime-environment"></a>Ambiente di runtime Java
Tomcat è scritto in Java. Esistono due tipi di Java Development Kit (JDK): OpenJDK e Oracle JDK. È possibile scegliere hello quello desiderato.  

> [!NOTE]
> Sia JDK sono quasi hello stesso codice per le classi hello hello API Java, ma il codice hello per la macchina virtuale hello è diverso. OpenJDK tende librerie aperte toouse, mentre tende Oracle JDK toouse chiuso quelle. Oracle JDK dispone di più classi e include alcuni bug corretti, inoltre è più stabile di OpenJDK.

#### <a name="install-openjdk"></a>Installare OpenJDK  

Comando che segue di hello utilizzare toodownload OpenJDK.   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* toocreate toocontain una directory hello file JDK:  

        sudo mkdir /usr/lib/jvm  
* file JDK tooextract hello in hello usr/lib/jvm/directory:  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a>Installare Oracle JDK


Utilizzare hello seguente toodownload comando Oracle JDK dal sito Web Oracle hello.  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* toocreate toocontain una directory hello file JDK:  

        sudo mkdir /usr/lib/jvm  
* file JDK tooextract hello in hello usr/lib/jvm/directory:  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* tooset Oracle JDK come hello predefinito Java virtual machine:  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a>Verificare che l'installazione di Java sia riuscita
È possibile utilizzare un comando simile hello seguente tootest se hello Java runtime environment sia installato correttamente:  

    java -version  

Se è installato OpenJDK, si verrà visualizzato un messaggio hello seguente: ![messaggio di installazione ha esito positivo OpenJDK][14]

Se è installato Oracle JDK, si verrà visualizzato un messaggio hello seguente: ![messaggio di installazione ha esito positivo Oracle JDK][15]

### <a name="install-tomcat7"></a>Installare Tomcat7
Utilizzare hello successivo comando tooinstall Tomcat7.  

    sudo apt-get install tomcat7  

Se non si utilizza Tomcat7, utilizzare la variante appropriata di hello di questo comando.  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a>Verificare che l'installazione di Tomcat7 sia riuscita
Se è stata installata Tomcat7, toocheck Sfoglia nome DNS del server Tomcat tooyour. In questo articolo, l'URL di esempio hello è http://tomcatexample.cloudapp.net/. Se viene visualizzato un messaggio hello seguente, Tomcat7 sia installato correttamente.
![Messaggio con l'avviso che l'installazione di Tomcat7 è riuscita][16]

### <a name="install-other-tomcat7-components"></a>Installare altri componenti di Tomcat7
Esistono altri componenti facoltativi di Tomcat che è possibile installare.  

Hello utilizzare **sudo apt della cache di ricerca tomcat7** toosee comando tutti i componenti disponibili hello. Utilizzare hello comandi che seguono tooinstall alcuni componenti utili.  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools toocreate user instances  

## <a name="phase-4-configure-tomcat7"></a>Fase 4: configurare Tomcat7
In questa fase si amministra Tomcat.

### <a name="start-and-stop-tomcat7"></a>Avviare e arrestare Tomcat7
Hello Tomcat7 avviata automaticamente durante l'installazione. È inoltre possibile avviare con hello comando seguente:   

    sudo /etc/init.d/tomcat7 start

toostop Tomcat7:

    sudo /etc/init.d/tomcat7 stop

stato di hello tooview di Tomcat7:

    sudo /etc/init.d/tomcat7 status

servizi di Tomcat toorestart: 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a>Amministrazione di Tomcat7
È possibile modificare hello Tomcat utente configurazione file tooset backup le credenziali di amministratore. Utilizzare hello comando seguente:  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

Di seguito è fornito un esempio:  
![Schermata che mostra l'output del comando vi hello sudo][17]  

> [!NOTE]
> Creare una password complessa per nome utente amministratore hello.  

Dopo avere modificato questo file, è necessario riavviare servizi Tomcat7 con hello comando tooensure che le modifiche di hello abbiano l'effetto seguente:  

    sudo /etc/init.d/tomcat7 restart  

Aprire il browser e immettere **http://<your tomcat server DNS name>manager/html** come hello URL. Ad esempio hello in questo articolo, l'URL hello è http://tomcatexample.cloudapp.net/manager/html.  

Dopo la connessione, verrà visualizzato un codice simile toohello seguenti:  
![Schermata di gestione di applicazioni Web Tomcat hello][18]

## <a name="common-issues"></a>Problemi comuni
### <a name="cant-access-hello-virtual-machine-with-tomcat-and-moodle-from-hello-internet"></a>Non è possibile accedere a hello la macchina virtuale con Tomcat e Moodle hello Internet
#### <a name="symptom"></a>Sintomo  
  Tomcat è in esecuzione ma non è possibile visualizzare pagina predefinita di Tomcat hello con il browser.
#### <a name="possible-root-cause"></a>Possibile causa principale   

  * porta di ascolto Hello Tomcat non è hello come porta privata di hello dell'endpoint della macchina virtuale per il traffico di Tomcat.  

     Controllare la porta pubblica e privata endpoint impostazioni porta e verificare la porta privata hello è hello uguali a quelli di Tomcat hello porta di ascolto. Per istruzioni sulla configurazione degli endpoint per la macchina virtuale vedere la sezione di questo articolo "Fase 1: creare un'immagine".  

     hello toodetermine Tomcat porta di ascolto, aprire /etc/httpd/conf/httpd.conf (Red Hat versione) o /etc/tomcat7/server.xml (Debian versione). Per impostazione predefinita, la porta di ascolto Tomcat hello è 8080. Di seguito è fornito un esempio:  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     Se si utilizza una macchina virtuale come Debian o Ubuntu e si desidera toochange hello predefinito porta di Tomcat ascolto (ad esempio 8081), è necessario aprire anche la porta hello per sistema operativo hello. Prima di tutto, aprire il profilo di hello:  

        sudo vi /etc/default/tomcat7  

     Quindi rimuovere l'ultima riga hello e modificare "no" troppo "yes".  

        AUTHBIND=yes
  2. firewall Hello è disabilitato hello porta di ascolto di Tomcat.

     È possibile visualizzare solo pagina predefinita di Tomcat hello dall'host locale hello. problema di Hello è molto probabile che la porta hello, vale a dire ascoltato tooby Tomcat, è bloccata da firewall hello. È possibile utilizzare la pagina hello hello w3m strumento toobrowse. Hello seguenti comandi installare w3m e passare pagina predefinita di Tomcat toohello:  


        sudo yum install w3m w3m-img


        w3m http://localhost:8080  
#### <a name="solution"></a>Soluzione

  * Se la porta di ascolto Tomcat hello è non hello stesso come porta privata di hello dell'endpoint hello per la macchina virtuale di traffico toohello, è necessario modificare la porta privata hello toobe hello stesso hello porta di ascolto Tomcat.   
  2. Se il problema di hello è determinato dal firewall/iptables, aggiungere hello seguenti righe troppo/ecc/sysconfig/iptables. seconda riga Hello è necessaria solo per il traffico https:  

      -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT

      -A INPUT -p tcp -m tcp --dport 443 -j ACCEPT  

     > [!IMPORTANT]
     > Verificare che le righe precedenti hello vengono posizionate sopra tutte le righe che verrebbero globale limitare l'accesso, come illustrato di seguito hello: - A -j REJECT - rifiuto-con icmp-host-consentito di INPUT



tooreload hello iptables, eseguire hello comando seguente:

    service iptables restart

Questa installazione è stata effettuata su CentOS 6.3.

### <a name="permission-denied-when-you-upload-project-files-toovarlibtomcat7webapps"></a>Autorizzazione negata quando si carica progetto file troppo/var/lib/tomcat7/webapps /
#### <a name="symptom"></a>Sintomo
  Quando si usa una macchina virtuale SFTP client (ad esempio FileZilla) tooconnect tooyour e passare troppo/var/lib/tomcat7/webapps/toopublish del sito, verrà un errore messaggio simili toohello segue:  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a>Possibile causa principale
  È non presente alcuna cartella di /var/lib/tomcat7/webapps hello tooaccess autorizzazioni.  
#### <a name="solution"></a>Soluzione  
  Sono necessarie autorizzazioni tooget dall'account radice hello. È possibile modificare la proprietà hello della cartella dal nome utente toohello radice utilizzato quando è stato effettuato il provisioning macchina hello. Di seguito è riportato un esempio con il nome di account azureuser hello:  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  Utilizzare autorizzazioni hello di hello -R opzione tooapply anche per tutti i file all'interno di una directory.  

  Questo comando funziona anche per le directory. le modifiche all'opzione -R Hello salve le autorizzazioni per tutti i file e directory all'interno della directory hello. Di seguito è fornito un esempio:  

     sudo chown -R username:group directory  

  Questo comando modifica la proprietà (utente e gruppo) per tutti i file e directory che sono all'interno della directory hello.  

  Hello comando seguente cambia solo autorizzazione hello di directory della cartella hello. Hello file e cartelle all'interno della directory hello non vengono modificate.  

     sudo chown username:group directory

[1]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-01.png
[2]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-02.png
[3]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-03.png
[4]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-04.png
[5]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-05.png
[6]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-06.png
[7]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-07.png
[8]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-08.png
[9]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-09.png
[10]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-10.png
[11]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-11.png
[12]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-12.png
[13]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-13.png
[14]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-14.png
[15]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-15.png
[16]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-16.png
[17]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-17.png
[18]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-18.png
