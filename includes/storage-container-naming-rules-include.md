Ogni BLOB nell'archiviazione di Azure deve risiedere in un contenitore. Hello contenitore fa parte del nome blob hello. Ad esempio, `mycontainer` hello nome del contenitore di hello in questi blob URI di esempio:

    https://storagesample.blob.core.windows.net/mycontainer/blob1.txt
    https://storagesample.blob.core.windows.net/mycontainer/photos/myphoto.jpg

Un nome di contenitore deve essere un nome DNS valido, toohello conforme alle regole di denominazione:

1. Il nome del contenitore devono iniziare con una lettera o un numero e possono contenere solo lettere, numeri e hello trattino (-).
2. Ciascun carattere trattino (-) deve essere immediatamente preceduto e seguito da una lettera o un numero: nei nomi dei contenitori non sono consentiti trattini consecutivi.
3. Tutte le lettere in un nome di contenitore deve essere composto solo da minuscole.
4. La lunghezza dei nomi dei contenitori deve essere compresa tra 3 e 63 caratteri.

> [!IMPORTANT]
> Si noti che hello nome di un contenitore deve essere sempre in minuscolo. Se si include una lettera maiuscola in un nome di contenitore o in caso contrario violano le regole di denominazione di hello contenitore, si potrebbe ricevere un errore 400 (richiesta non valida). 
> 
> 

