## <a name="install-hello-prerequisites"></a>Installare i prerequisiti di hello

passaggi di Hello in questa esercitazione si presuppone il che uso Ubuntu Linux.

Aprire una shell ed eseguire i seguenti pacchetti dei prerequisiti di comandi tooinstall hello hello:

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

Nella shell di hello, eseguire hello successivo comando tooclone hello Azure IoT Edge GitHub repository tooyour locale:

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a>Come toobuild hello esempio

È ora possibile generare hello IoT Edge runtime ed esempi sul computer locale:

1. Aprire una shell.

1. Esplorazione delle cartelle radice toohello nella copia locale di hello **iot edge** repository.

1. Eseguire lo script di compilazione come segue:

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

Questo script utilizza il **cmake** toocreate utilità una cartella denominata **compilare** nella cartella radice hello della copia locale del **iot edge** repository e generare un makefile. script Hello quindi compila la soluzione hello, ignorando gli unit test e tooend fine. Se si desidera toobuild e hello unit test, aggiungere hello `--run-unittests` parametro. Se si desidera toobuild ed eseguire i test di tooend hello fine, aggiungere hello `--run-e2e-tests`.

> [!NOTE]
> Ogni volta che si esegue hello **build.sh** script, Elimina e ricrea quindi hello **compilare** cartella nella cartella radice hello della copia locale di hello **iot edge** repository.
