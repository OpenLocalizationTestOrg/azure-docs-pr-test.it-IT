
codice Hello per tutte le funzioni hello in un'app di funzione specificata si trova in una cartella radice che contiene un file di configurazione di host e le sottocartelle di uno o più, ognuna delle quali contengono codice hello per una funzione separata, come hello di esempio seguente:

```
wwwroot
 | - host.json
 | - mynodefunction
 | | - function.json
 | | - index.js
 | | - node_modules
 | | | - ... packages ...
 | | - package.json
 | - mycsharpfunction
 | | - function.json
 | | - run.csx
```

Hello *host.json* file contiene una configurazione di runtime specifiche e si trova nella cartella radice hello di hello funzione app. Per informazioni sulle impostazioni disponibili, vedere [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) nel wiki di hello WebJobs.Script repository.

Ogni funzione presenta una cartella che contiene uno o più file di codice, configurazione function.json hello e altre dipendenze.

