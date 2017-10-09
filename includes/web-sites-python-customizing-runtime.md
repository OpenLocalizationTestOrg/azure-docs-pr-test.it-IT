Azure determina hello versione di Python toouse per l'ambiente virtuale con hello priorità seguenti:

1. versione specificata in runtime.txt nella cartella radice hello
2. versione specificata dall'impostazione di Python nella configurazione di app web hello (hello **impostazioni** > **le impostazioni dell'applicazione** pannello per l'app web nel portale di Azure hello)
3. Python 2.7 è predefinito hello se è stata specificata alcuna di hello precedente

Valori validi per il contenuto di hello 

    \runtime.txt

sono:

* python-2.7
* python-3.4

Se versione micro hello (terza cifra) viene specificato, viene ignorato.

