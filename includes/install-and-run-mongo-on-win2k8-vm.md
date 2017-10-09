Seguire questi passaggi tooinstall ed eseguire MongoDB in una macchina virtuale che esegue Windows Server.

> [!IMPORTANT]
> Le funzionalità di sicurezza MongoDB, ad esempio l'autenticazione e l'associazione di indirizzi IP, non sono abilitate per impostazione predefinita. Funzionalità di sicurezza devono essere abilitate prima di distribuire l'ambiente di produzione tooa MongoDB.  Per altre informazioni, vedere [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication)Sicurezza e autenticazione.
>
>

1. Dopo aver collegato toohello virtual machine tramite Desktop remoto, aprire Internet Explorer da hello **avviare** menu nella macchina virtuale hello.
2. Seleziona hello **strumenti** pulsante nell'angolo superiore destro di hello.  In **Opzioni Internet**selezionare hello **sicurezza** scheda e quindi selezionare hello **siti attendibili** icona e infine fare clic su hello **siti** pulsante. Aggiungere *https://\*. mongodb.org* toohello elenco dei siti attendibili.
3. Andare troppo[Scarica - MongoDB](https://www.mongodb.com/download-center#community).
4. Trovare hello **versione stabile corrente** di **Server Community**selezionare hello più recente **64-bit** versione nella colonna di Windows hello. Scaricare, quindi eseguire il programma di installazione di hello MSI.
5. MongoDB viene in genere installato in C:\Programmi\MongoDB. Cercare le variabili di ambiente nel desktop hello e aggiungere il componente toohello percorso variabile del percorso dei file binari hello MongoDB. Ad esempio, si potrebbero individuare i file binari di hello in c:\Programmi\Microsoft Files\MongoDB\Server\3.4\bin nel computer.
6. Creare le directory di dati e di log di MongoDB nel disco dati hello (ad esempio unità **f:**) è stato creato in hello passaggi precedenti. Da **avviare**selezionare **prompt dei comandi** tooopen una finestra del prompt dei comandi.  Digitare:

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. database hello toorun, eseguire:

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    Tutti i messaggi di log sono diretto toohello *F:\MongoLogs\mongolog.log* file mongod.exe server viene avviato e prealloca una quantità file journal. Può richiedere alcuni minuti per MongoDB toopreallocate file journal hello e avvia l'ascolto delle connessioni. prompt dei comandi di Hello rimane attivo per l'attività mentre è in esecuzione l'istanza di MongoDB.
8. hello toostart shell amministrativa MongoDB, aprire un'altra finestra di comando da **avviare** e hello tipo seguenti comandi:

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    Hello database viene creato da insert hello.
9. In alternativa, è possibile installare mongod.exe come servizio:

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    Viene installato un servizio denominato MongoDB con la descrizione "MongoDB". Hello `--logpath` opzione deve essere toospecify utilizzato un file di log, poiché hello servizio non dispone di un output toodisplay finestra di comando.  Hello `--logappend` opzione specifica che un riavvio del servizio hello provoca output tooappend toohello file di log esistente.  Hello `--dbpath` opzione specifica hello percorso della directory di dati hello. Per altre opzioni della riga di comando relative ai servizi, vedere le [opzioni della riga di comando relative ai servizi][MongoWindowsSvcOptions].

    servizio hello toostart, eseguire questo comando:

        C:\> net start MongoDB
10. Ora che MongoDB sia installato e in esecuzione, è necessario tooopen una porta in Windows Firewall in modo è possibile connettersi in remoto tooMongoDB.  Da hello **avviare** dal menu **strumenti di amministrazione** e quindi **Windows Firewall con sicurezza avanzata**.
11. a) nel riquadro sinistro hello selezionare **regole connessioni in entrata**.  In hello **azioni** riquadro a destra, hello seleziona **nuova regola...** .

    ![Windows Firewall][Image1]

    b) in hello **in ingresso Creazione guidata nuova regola**selezionare **porta** e quindi fare clic su **Avanti**.

    ![Windows Firewall][Image2]

    c) Selezionare **TCP** e quindi **Porte locali specifiche**.  Specificare una porta di "27017" (porta predefinita hello MongoDB in ascolto) e fare clic su **Avanti**.

    ![Windows Firewall][Image3]

    d) selezionare **Consenti connessione hello** e fare clic su **Avanti**.

    ![Windows Firewall][Image4]

    e) Fare di nuovo clic su **Avanti**.

    ![Windows Firewall][Image5]

    f) consente di specificare un nome per la regola di hello, ad esempio "MongoPort", quindi fare clic su **fine**.

    ![Windows Firewall][Image6]

12. Se un endpoint non è stata configurata per MongoDB al momento della creazione macchina virtuale hello, è possibile farlo ora. È necessario regola del firewall hello sia hello endpoint toobe tooconnect in grado di tooMongoDB in modalità remota.

  Nel portale di Azure hello, fare clic su **macchine virtuali (classico)**, fare clic sul nome della nuova macchina virtuale hello e quindi fare clic su **endpoint**.

    ![Endpoint][Image7]

13. Fare clic su **Aggiungi**.

14. Aggiungere un endpoint con nome "Mongo", protocollo **TCP**ed entrambi **pubblica** e **privata** porte set troppo "27017". Apertura di questa porta consente toobe MongoDB accesso remoto.

    ![Endpoint][Image9]

> [!NOTE]
> porta Hello 27017 è utilizzata da MongoDB la porta predefinita hello. È possibile modificare la porta predefinita specificando hello `--port` parametro durante l'avvio hello mongod.exe server. Rendere toogive che hello stesso numero di porta nel firewall hello e hello l'endpoint "Mongo" hello istruzioni precedente.
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png
