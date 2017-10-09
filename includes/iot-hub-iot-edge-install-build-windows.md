## <a name="install-hello-prerequisites"></a>Installare i prerequisiti di hello

1. Installare [Visual Studio 2015 o 2017](https://www.visualstudio.com). È possibile utilizzare hello libero Community Edition se vengono soddisfatti i requisiti di licenza hello. Essere tooinclude che Visual C++ e gestione pacchetti NuGet.

1. Installare [git](http://www.git-scm.com) e assicurarsi che sia possibile eseguire git.exe dalla riga di comando hello.

1. Installare [CMake](https://cmake.org/download/) e assicurarsi che sia possibile eseguire cmake.exe dalla riga di comando hello. È consigliabile usare CMake versione 3.7.2 o successive. Hello **con estensione msi** programma di installazione è l'opzione più semplice di hello in Windows. Aggiungere CMake toohello percorso per hello almeno l'utente corrente quando viene richiesto dal programma di installazione hello.

1. Installare [Python 2.7](https://www.python.org/downloads/release/python-27). Assicurarsi di aggiungere Python tooyour `PATH` variabile di ambiente nel **Pannello di controllo -> sistema -> avanzate le impostazioni di sistema -> variabili di ambiente**.

1. Al prompt dei comandi, eseguire hello comando tooclone hello Azure IoT Edge GitHub repository tooyour locali seguenti:

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a>Come toobuild hello esempio

È ora possibile generare hello IoT Edge runtime ed esempi sul computer locale:

1. Aprire un **prompt dei comandi per gli sviluppatori per VS 2015** o un **prompt dei comandi per gli sviluppatori per VS 2017**.

1. Esplorazione delle cartelle radice toohello nella copia locale di hello **iot edge** repository.

1. Eseguire lo script di compilazione come segue:

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

Questo script crea un file di soluzione di Visual Studio e compila la soluzione hello. È possibile trovare una soluzione di Visual Studio hello in hello **compilare** cartella nella copia locale di hello **iot edge** repository. Se si desidera toobuild e hello unit test, aggiungere hello `--run-unittests` parametro. Se si desidera toobuild ed eseguire i test di tooend hello fine, aggiungere hello `--run-e2e-tests`.

> [!NOTE]
> Ogni volta che si esegue hello **build.cmd** script, Elimina e ricrea quindi hello **compilare** cartella nella cartella radice hello della copia locale di hello **iot edge** repository.
