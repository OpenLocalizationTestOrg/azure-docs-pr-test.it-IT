Una macchina virtuale di Azure supporta il collegamento di un numero di dischi dati. Per ottenere prestazioni ottimali, è consigliabile toolimit hello di dischi utilizzati elevata collegata toohello macchina virtuale tooavoid possibili la limitazione delle richieste. Se non tutti i dischi sono in uso elevata a hello contemporaneamente, account di archiviazione hello può supportare un numero maggiore di dischi.

* **Per i dischi gestito di Azure:** numero massimo di dischi gestiti è regionale e dipende inoltre dal tipo di archiviazione hello. Hello predefinito e anche il limite massimo di hello è 10.000 per ogni sottoscrizione, per ogni area e per ogni tipo di archiviazione. Ad esempio, è possibile creare backup too10, 000 standard gestiti dischi e anche 10.000 premium gestiti dischi in una sottoscrizione e in un'area. 

    Snapshot gestito e le immagini vengono conteggiate rispetto hello che limitare dischi gestiti.

* **Per gli account di archiviazione standard:** un account di archiviazione standard con una frequenza totale massima di richieste di 20.000 IOPS. Hello IOPS totali per tutti i dischi di macchina virtuale in un account di archiviazione standard non deve superare questo limite.
  
    È possibile calcolare approssimativamente il numero di hello di dischi utilizzati elevata supportati da un account di archiviazione singolo standard basato sul limite di velocità richiesta hello. Ad esempio, per un macchina virtuale, di livello Basic hello numero massimo di altamente utilizzati dischi è circa 66 (20.000/300 di IOPS per disco) e per una macchina virtuale livello Standard, è di circa 40 (20.000/500 IOPS per ogni disco), come illustrato nella tabella hello riportata di seguito. 
* **Per gli account di archiviazione Premium:** un account di archiviazione Premium ha una velocità effettiva totale massima di 50 Gbps. velocità effettiva totale Hello in tutti i dischi di macchina virtuale non deve superare questo limite.

