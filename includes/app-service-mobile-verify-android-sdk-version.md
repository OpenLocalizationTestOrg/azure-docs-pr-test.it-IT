A causa di sviluppo, versione di Android SDK hello in Android Studio potrebbe non corrispondere versione hello nel codice hello. Hello, Android SDK a cui fa riferimento in questa esercitazione è hello 23, versione più recente in fase di hello di scrittura. può aumentare il numero di versione di Hello come le nuove versioni di hello SDK vengono visualizzati e si consiglia di utilizzare hello ultima versione disponibile.

Due sintomi di una mancata corrispondenza delle versioni sono i seguenti:

- Quando si compila o si ricompila il progetto di hello, si possa ricevere messaggi di errore Gradle come "**non riuscita di destinazione toofind Google Inc.:Google APIs:n**".
- Gli oggetti Android standard nel codice che dovrebbero risolversi in base a istruzioni `import` potrebbero generare messaggi di errore.

Se uno di questi viene visualizzata, versione di hello di hello Android SDK installato in Android Studio potrebbe non corrispondere destinazione SDK hello del progetto hello scaricato. versione di hello tooverify, rendere hello seguenti modifiche:

1. In Android Studio fare clic su **Tools** (Strumenti)  > **Android** > **SDK Manager**. Se non è installato hello versione hello Platform SDK, quindi fare clic su tooinstall è. Prendere nota del numero di versione di hello.
2. In hello **Esplora progetti** nella scheda **Gradle script**, aprire il file hello **gradle (modeule: app)**. Verificare che hello **compileSdkVersion** e **buildToolsVersion** impostati toohello SDK più recente installata. tag Hello potrebbe essere simile al seguente:

             compileSdkVersion 'Google Inc.:Google APIs:23'
            buildToolsVersion "23.0.2"
3. Hello, Android Studio Project Explorer di nodo del progetto hello pulsante destro del mouse, scegliere **proprietà**, nella colonna sinistra hello scegliere **Android**. Verificare che hello **destinazione di compilazione progetto** è impostato toohello stessa versione di SDK di hello **targetSdkVersion**.

In Android Studio file manifesto hello non è più utilizzato toospecify hello destinazione SDK e versione SDK minima, a differenza dei case hello con Eclipse.
