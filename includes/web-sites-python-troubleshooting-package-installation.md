Alcuni pacchetti potrebbero non essere installati tramite pip se eseguiti su Azure.  È possibile semplicemente che il pacchetto di hello non è disponibile in hello indice del pacchetto Python.  È possibile che un compilatore è obbligatorio (un compilatore non è disponibile nel computer in esecuzione hello web app hello in Azure App Service).

In questa sezione verrà esaminato toodeal modi con questo problema.

### <a name="request-wheels"></a>Richiedere i file wheel
Se l'installazione del pacchetto hello richiede al compilatore, è consigliabile provare a contattare hello pacchetto proprietario toorequest ruote essere rese disponibili per il pacchetto di hello.

Con la disponibilità di recente hello di [compilatore Microsoft Visual C++ per Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], è ora più semplice toobuild i pacchetti con codice nativo per Python 2.7.

### <a name="build-wheels-requires-windows"></a>Creare i file wheel (richiede Windows)
Nota: Quando si utilizza questa opzione, assicurarsi di pacchetto di hello toocompile che usa un ambiente di Python che corrisponde a hello/architettura/versione della piattaforma che viene utilizzato nell'applicazione web hello in Azure App Service (Windows/32-bit/2.7 o 3.4).

Se il pacchetto di hello non viene installata perché richiede un compilatore, è possibile installare del compilatore hello sul computer locale e compilare una ruota per pacchetto hello, che verranno quindi incluse nel repository.

Gli utenti Mac/Linux: Se non si dispone di computer Windows tooa di accesso, vedere [creare una macchina virtuale che esegue Windows] [ Create a Virtual Machine Running Windows] come toocreate una macchina virtuale in Azure.  È possibile usarlo ruote hello toobuild, aggiungerli toohello repository e annullare hello macchina virtuale se lo si desidera. 

Per Python 2.7, è possibile installare [compilatore Microsoft Visual C++ per Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].

Per Python 3.4, è possibile installare [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].

toobuild ruote, è necessario pacchetto rotellina hello:

    env\scripts\pip install wheel

Si utilizzerà `pip wheel` toocompile una dipendenza:

    env\scripts\pip wheel azure==0.8.4

Verrà creato un file .whl nella cartella \wheelhouse hello.  Aggiungi cartella \wheelhouse hello e del selettore file tooyour repository.

Modificare il hello tooadd requirements.txt `--find-links` opzione nella parte superiore di hello. In questo modo toolook pip per una corrispondenza esatta nella cartella locale di hello prima di indice del pacchetto python toohello continua.

    --find-links wheelhouse
    azure==0.8.4

Se si desidera tooinclude tutte le dipendenze di hello \wheelhouse cartella e non utilizzare hello pacchetto python indice affatto, è possibile forzare l'indice del pacchetto pip tooignore hello aggiungendo `--no-index` toohello cima il requirements.txt.

    --no-index

### <a name="customize-installation"></a>Personalizzare l'installazione
È possibile personalizzare hello distribuzione script tooinstall un pacchetto nell'ambiente virtuale di hello utilizzando un programma di installazione alternativo, ad esempio semplice\_installare.  Per un esempio impostato come commento, vedere deploy.cmd.  Verificare che tali pacchetti non sono elencate nella requirements.txt, tooprevent pip da eseguirne l'installazione.

Aggiungere questo script di distribuzione toohello:

    env\scripts\easy_install somepackage

Potrebbe essere in grado di toouse facile\_installare tooinstall da un programma di installazione exe (alcuni sono zip in modo semplice, compatibile\_installazione supportarle).  Aggiungi repository tooyour programma di installazione di hello e richiamare semplice\_installare passando hello percorso toohello eseguibile.

Aggiungere questo script di distribuzione toohello:

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a>Includere l'ambiente virtuale hello nel repository di hello (richiede Windows)
Nota: Quando si utilizza questa opzione, assicurarsi che toouse un ambiente virtuale corrispondente hello/architettura/versione della piattaforma che viene utilizzato nell'applicazione web hello in Azure App Service (Windows/32-bit/2.7 o 3.4).

Se si include l'ambiente virtuale hello nel repository di hello, è possibile impedire lo script di distribuzione hello dalla gestione dell'ambiente virtuale in Azure tramite la creazione di un file vuoto:

    .skipPythonDeployment

È consigliabile eliminare ambiente virtuale esistente hello in app hello, tooprevent file rimasti dall'ambiente virtuale hello è stato gestito automaticamente.

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
