Per stabilire se l'applicazione usa Python, Azure verifica se **entrambe le condizioni seguenti sono soddisfatte**:

* Requirements.txt file nella cartella radice hello
* qualsiasi file py nella cartella radice hello o un runtime.txt che specifica di python

Quando è il caso di hello, utilizza uno script di distribuzione specifico Python, che esegue la sincronizzazione di standard hello dei file, nonché altre operazioni di Python, ad esempio:

* Gestione automatica dell'ambiente virtuale
* Installazione dei pacchetti elencati in requirements.txt tramite pip
* Creazione di Web. config appropriato hello in base a hello selezionato versione di Python.
* Raccolta di file statici per le applicazioni Django

È possibile controllare alcuni aspetti di passaggi di distribuzione predefinito hello senza script hello toocustomize.

Se si desidera tooskip tutti i passaggi di distribuzione di Python, è possibile creare questo file vuoto:

    \.skipPythonDeployment

Se si desidera tooskip raccolta dei file statici per l'applicazione Django:

    \.skipDjango 

Per un maggiore controllo sulla distribuzione, è possibile eseguire l'override di script di distribuzione predefinito hello creando hello i seguenti file:

    \.deployment
    \deploy.cmd

È possibile utilizzare hello [interfaccia della riga di comando di Azure] [ Azure command-line interface] file hello toocreate.  Usare questo comando dalla cartella del progetto:

    azure site deploymentscript --python

Se questi file non esistono, Azure creerà uno script di distribuzione temporaneo e lo eseguirà.  È identico toohello quello che si crea con hello comando precedente.

[Azure command-line interface]: http://azure.microsoft.com/downloads/
