<!-- F-series, Fs-series* -->

F-serie basata su hello 2,4 GHz Intel Xeon® E5-2673 v3 processore (Haswalle), che può raggiungere la velocità di clock elevata come 3,1 GHz con hello Intel turbina Boost tecnologia 2.0. Questo è hello stesso prestazioni CPU come hello Dv2 serie di macchine virtuali.  Prezzi più bassi per ora elenco, serie F hello è hello valore migliore prezzo in hello Azure portfolio in base a hello Azure Compute Unit (ACU) per ogni CPU virtuali. 

Le VM serie F sono un'ottima scelta per i carichi di lavoro che richiedono CPU più veloci, ma che non necessitano della stessa memoria o risorsa di archiviazione temporanea per ogni vCPU.  I carichi di lavoro, ad esempio analitica, i server di gioco, server web e l'elaborazione batch trarranno vantaggio dal valore hello hello serie F.

Hello serie Fs fornisce tutti i vantaggi di hello di hello F-series, nel servizio di archiviazione tooPremium aggiunta.

## <a name="fs-series"></a>Serie Fs*

ACU: 210 - 250

| Dimensione | vCPU | Memoria: GiB | GiB di archiviazione temp (unità SSD) | Valore massimo per dischi di dati | Velocità effettiva massima di archiviazione temporanea e nella cache: IOPS/MBps (dimensioni della cache in GiB) | Max velocità effettiva del disco non memorizzato nella cache: IOPS/MBps | Schede di interfaccia di rete max/prestazioni rete previste (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_F1s |1 |2 |4 |2 |4.000/32 (12) |3.200/48 |2 / 750 |
| Standard_F2s |2 |4 |8 |4 |8.000/64 (24) |6.400/96 |2 / 1500 |
| Standard_F4s |4 |8 |16 |8 |16.000/128 (48) |12.800/192 |4 / 3000 |
| Standard_F8s |8 |16 |32 |16 |32.000/256 (96) |25.600/384 |8 / 6000 |
| Standard_F16s |16 |32 |64 |32 |64.000/512 (192) |51.200/768 |8 / 6000-12000 &#8224; |

MBps = 10^6 byte al secondo e GiB = 1024^3 byte.

* hello massima velocità effettiva del disco (IOPS o MBps) con una serie di ADFS VM può essere limitata dal numero di hello, dimensioni e lo striping di hello associata dischi.  Per altre informazioni, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../articles/storage/common/storage-premium-storage.md).


<br>

## <a name="f-series"></a>Serie F

ACU: 210 - 250

| Dimensione         | vCPU | Memoria: GiB | GiB di archiviazione temp (unità SSD) | Velocità effettiva massima di archiviazione temporanea: IOPS/Mbps di lettura/Mbps di scrittura | Velocità effettiva/disco di dati massimo: IOPS | Schede di interfaccia di rete max/prestazioni rete previste (Mbps) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_F1  | 1         | 2           | 16             | 3000 / 46 / 23                                           | 2/2 x 500                         | 2 / 750                 |
| Standard_F2  | 2         | 4           | 32             | 6000 / 93 / 46                                           | 4/4 x 500                         | 2 / 1500                     |
| Standard_F4  | 4         | 8           | 64             | 12000 / 187 / 93                                         | 8/8 x 500                         | 4 / 3000                     |
| Standard_F8  | 8         | 16          | 128            | 24000 / 375 / 187                                        | 16/16 x 500                       | 8 / 6000                     |
| Standard_F16 | 16        | 32          | 256            | 48000 / 750 / 375                                        | 32/32 x 500                       | 8 / 6000 - 12000 &#8224;           |


<br>


