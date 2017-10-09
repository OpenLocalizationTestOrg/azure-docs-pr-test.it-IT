
* Hello serie M offre hello più alto numero di CPU virtuali (backup too128 Vcpu) e memoria più grande (backup too2.0 TiB) di qualsiasi macchina virtuale nel cloud hello.  È ideale per database molto grandi o altre applicazioni che traggono vantaggio da un elevato numero di vCPU e una grande quantità di memoria.

* Serie Dv2 serie D, G, serie e controparti DS o GS hello sono ideali per le applicazioni che richiedono Vcpu più veloce, migliorare le prestazioni di archiviazione temporanea, o versioni successive richieste di memoria.  Offrono una potente combinazione per molte applicazioni di livello aziendale.

* Macchine virtuali serie D sono progettate toorun applicazioni che richiedono maggiore potenza di calcolo e le prestazioni del disco temporaneo. Le macchine virtuali serie D forniscono processori più veloci, un rapporto tra memoria e vCPU superiore e un'unità SSD per l'archiviazione temporanea. Per informazioni dettagliate, vedere annuncio hello sul blog di Azure, hello [nuove dimensioni delle macchine virtuali di serie D](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/).

* Dv2-series, un toohello successivi serie D originale, dotato di una CPU più potente. Hello Dv2 serie CPU è circa 35% più rapida rispetto hello serie D CPU. Si basa su hello ultima generazione 2,4 GHz Intel Xeon® E5-2673 v3 processore (Haswalle) e con hello Intel turbina Boost tecnologia 2.0, possono aumentare fino too3.1 GHz. Hello Dv2 serie è hello stesse configurazioni di memoria e disco come hello serie D.


## <a name="esv3-series"></a>Serie ESv3

Unità di calcolo di Azure: 160-190

Le istanze di ESv3 serie sono basate su hello 2,3 GHz Intel XEON® E5-2673 v4 processore (Broadwell) e ottenere 3.5GHz con Intel turbina Boost tecnologia 2.0 e usare l'archiviazione premium. Le istanze della serie Ev3 sono ideali per applicazioni aziendali a uso intensivo di memoria.


| Dimensione             | vCPU | Memoria: GiB | GiB di archiviazione temp (unità SSD) | Valore massimo per dischi di dati | Velocità effettiva massima di archiviazione temporanea e nella cache: IOPS/MBps (dimensioni della cache in GiB) | Max velocità effettiva del disco non memorizzato nella cache: IOPS/MBps | Schede di interfaccia di rete max/prestazioni rete previste (Mbps) |
|------------------|--------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------------------------|
| Standard_E2s_v3  | 2      | 16          | 32             | 4              | 4,000 / 32 (50)                                                       | 3.200/48                                | 2/moderata                                   |
| Standard_E4s_v3  | 4      | 32          | 64             | 8              | 8,000 / 64 (100)                                                      | 6.400/96                                | 2/moderata                                   |
| Standard_E8s_v3  | 8      | 64          | 128            | 16             | 16,000 / 128 (200)                                                    | 12.800/192                              | 4/alta                                       |
| Standard_E16s_v3 | 16     | 128         | 256            | 32             | 32,000 / 256 (400)                                                    | 25.600/384                              | 8/alta                                       |
| Standard_E32s_v3 | 32     | 256         | 512            | 32             | 64,000 / 512 (800)                                                    | 51.200/768                              | 8/estremamente alta                             |
| Standard_E64s_v3 | 64     | 432         | 864            | 32             | 128,000/1024 (1600)                                                   | 80,000 / 1200                             | 8/estremamente alta                             |



## <a name="ev3-series"></a>Serie Ev3

Unità di calcolo di Azure: 160-190 

Le istanze di Ev3 serie sono basate su hello 2,3 GHz Intel XEON® E5-2673 v4 processore (Broadwell) e che possa raggiungere 3.5GHz con Intel turbina Boost tecnologia 2.0. Le istanze della serie Ev3 sono ideali per applicazioni aziendali a uso intensivo di memoria.

L'archiviazione su disco dati viene fatturata separatamente dalle macchine virtuali. dischi di archiviazione premium toouse utilizzare dimensioni ESv3 hello. Hello prezzi e fatturazione metri per dimensioni ESv3 sono hello stesso come Ev3 serie. 


| Dimensione            | vCPU | Memoria: GiB | GiB di archiviazione temp (unità SSD) | Valore massimo per dischi di dati | Velocità effettiva massima di archiviazione temporanea: IOPS/Mbps di lettura/Mbps di scrittura | Larghezza di banda della rete/scheda NIC max |
|-----------------|-----------|-------------|----------------|----------------|----------------------------------------------------------|------------------------------|
| Standard_E2_v3  | 2         | 16          | 50             | 4              | 3000/46/23                                               | 2/moderata                 |
| Standard_E4_v3  | 4         | 32          | 100            | 8              | 6000/93/46                                               | 2/moderata                 |
| Standard_E8_v3  | 8         | 64          | 200            | 16             | 12000/187/93                                             | 4/alta                     |
| Standard_E16_v3 | 16        | 128         | 400            | 32             | 24000/375/187                                            | 8/alta                     |
| Standard_E32_v3 | 32        | 256         | 800            | 32             | 48000/750/375                                            | 8/estremamente alta           |
| Standard_E64_v3 | 64        | 432         | 1600           | 32             | 96000/1000/500                                           | 8/estremamente alta           |


## <a name="m-series"></a>Serie M*

ACU: 160-180

| Dimensione            | vCPU | Memoria: GiB | GiB di archiviazione temp (unità SSD) | Valore massimo per dischi di dati | Velocità effettiva massima di archiviazione temporanea e nella cache: IOPS/MBps (dimensioni della cache in GiB) | Max velocità effettiva del disco non memorizzato nella cache: IOPS/MBps | Schede di interfaccia di rete max/prestazioni rete previste (Mbps) |
|-----------------|------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------|
| Standard_M64ms  | 64   | 1792        | 2048           | 32             | 80.000 / 800 (6348)       | 40.000/1.000                            | 8 / 16000          |
| Standard_M128s** | 128  | 2048        | 4096           | 64             | 160.000 / 1.600 (12.696) | 80.000/2.000                            | 8 / 25000          |



* Le macchine virtuali Serie M integrano la tecnologia Intel® Hyper-Threading

** Data la presenza di più di 64 vCPU, è necessario uno dei seguenti sistemi operativi supportati: Windows Server 2016, Ubuntu 16.04 LTS, SLES 12 SP2 e Red Hat Enterprise Linux o CentOS 7.3 con LIS 4.2.1 

<br>

## <a name="gs-series"></a>Serie GS*

ACU: 180 - 240

| Dimensione | vCPU | Memoria: GiB | GiB di archiviazione temp (unità SSD) | Valore massimo per dischi di dati | Velocità effettiva massima di archiviazione temporanea e nella cache: IOPS/MBps (dimensioni della cache in GiB) | Max velocità effettiva del disco non memorizzato nella cache: IOPS/MBps | Schede di interfaccia di rete max/prestazioni rete previste (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_GS1 |2 |28 |56 |4 |10.000/100 (264) |5.000/125 |2 / 2000 |
| Standard_GS2 |4 |56 |112 |8 |20.000/200 (528) |10.000/250 |2 / 4000 |
| Standard_GS3 |8 |112 |224 |16 |40.000/400 (1.056) |20.000/500 |4 / 8000 |
| Standard_GS4 |16 |224 |448 |32 |80.000/800 (2,112) |40.000/1.000 |8 / 6000 - 16000 &#8224; |
| Standard_GS5** |32 |448 |896 |64 |160.000/1.600 (4.224) |80.000/2.000 |8 / 20000 |

* hello massima velocità effettiva del disco (IOPS o MBps) con una serie di GS VM può essere limitata dal numero di hello, dimensioni e lo striping di hello associata dischi. Per altre informazioni, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../articles/storage/common/storage-premium-storage.md). 

* * Istanza è di tipo isolato toohardware tooa dedicato singolo cliente.


<br>

## <a name="g-series"></a>Serie G

ACU: 180 - 240

| Dimensione         | vCPU | Memoria: GiB | GiB di archiviazione temp (unità SSD) | Velocità effettiva massima di archiviazione temporanea: IOPS/Mbps di lettura/Mbps di scrittura | Velocità effettiva/disco di dati massimo: IOPS | Schede di interfaccia di rete max/prestazioni rete previste (Mbps) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_G1  | 2         | 28          | 384            | 6000 / 93 / 46                                           | 4/4 x 500                       | 2 / 2000                     |
| Standard_G2  | 4         | 56          | 768            | 12000 / 187 / 93                                         | 8/8 x 500                       | 2 / 4000                     |
| Standard_G3  | 8         | 112         | 1.536          | 24000 / 375 / 187                                        | 16/16 x 500                     | 4 / 8000                |
| Standard_G4  | 16        | 224         | 3.072          | 48000 / 750 / 375                                        | 32/32 x 500                     | 8 / 6000 - 16000 &#8224;          |
| Standard_G5* | 32        | 448         | 6.144          | 96000 / 1500 / 750                                       | 64/64 x 500                     | 8 / 20000           |

* L'istanza è di tipo isolato toohardware tooa dedicato singolo cliente.
<br>


## <a name="dsv2-series"></a>Serie DSv2*

ACU: 210 - 250

| Dimensione | vCPU | Memoria: GiB | GiB di archiviazione temp (unità SSD) | Valore massimo per dischi di dati | Velocità effettiva massima di archiviazione temporanea e nella cache: IOPS/MBps (dimensioni della cache in GiB) | Max velocità effettiva del disco non memorizzato nella cache: IOPS/MBps | Schede di interfaccia di rete max/prestazioni rete previste (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS11_v2 |2 |14 |28 |4 |8.000/64 (72) |6.400/96 |2 / 1500 |
| Standard_DS12_v2 |4 |28 |56 |8 |16.000/128 (144) |12.800/192 |4 / 3000 |
| Standard_DS13_v2 |8 |56 |112 |16 |32.000/256 (288) |25.600/384 |8 / 6000 |
| Standard_DS14_v2 |16 |112 |224 |32 |64.000/512 (576) |51.200/768 |8 / 6000 - 12000 &#8224; |
| Standard_DS15_v2** |20 |140 |280 |40 |80.000/640 (720) |64.000/960 |8 / 20000***

* hello massima velocità effettiva del disco (IOPS o MBps) con una serie di DSv2 VM può essere limitata dal numero di hello, dimensioni e lo striping di hello associata dischi.  Per altre informazioni, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../articles/storage/common/storage-premium-storage.md).

* * Istanza è un nodo di tipo isolato che garantisce che la macchina virtuale è hello solo macchina virtuale in questo nodo Haswalle Intel.

***25000 Mbps con rete accelerata.

<br>

## <a name="dv2-series"></a>Serie Dv2

ACU: 210 - 250

| Dimensione              | vCPU | Memoria: GiB | GiB di archiviazione temp (unità SSD) | Velocità effettiva massima di archiviazione temporanea: IOPS/Mbps di lettura/Mbps di scrittura | Velocità effettiva/disco di dati massimo: IOPS | Schede di interfaccia di rete max/prestazioni rete previste (Mbps) |
|-------------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_D11_v2   | 2         | 14          | 100            | 6000 / 93 / 46                                           | 4/4 x 500                         | 2 / 1500                     |
| Standard_D12_v2   | 4         | 28          | 200            | 12000 / 187 / 93                                         | 8/8 x 500                         | 4 / 3000                     |
| Standard_D13_v2   | 8         | 56          | 400            | 24000 / 375 / 187                                        | 16/16 x 500                       | 8 / 6000                     |
| Standard_D14_v2   | 16        | 112         | 800            | 48000 / 750 / 375                                        | 32/32 x 500                       | 8 / 6000 - 12000 &#8224;          |
| Standard_D15_v2* | 20        | 140         | 1.000          | 60000 / 937 / 468                                        | 40/40 x 500                       | 8 / 20000** |

* L'istanza è un nodo di tipo isolato che garantisce che la macchina virtuale è hello solo macchina virtuale in questo nodo Haswalle Intel.

**25000 Mbps with Accelerated Networking.

<br>

## <a name="ds-series"></a>Serie DS*

ACU: 160

| Dimensione | vCPU | Memoria: GiB | GiB di archiviazione temp (unità SSD) | Valore massimo per dischi di dati | Velocità effettiva massima di archiviazione temporanea e nella cache: IOPS/MBps (dimensioni della cache in GiB) | Max velocità effettiva del disco non memorizzato nella cache: IOPS/MBps | Schede di interfaccia di rete max/prestazioni rete previste (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS11 |2 |14 |28 |4 |8.000/64 (72) |6.400/64 |2 / 1000 |
| Standard_DS12 |4 |28 |56 |8 |16.000/128 (144) |12.800/128 |4 / 2000 |
| Standard_DS13 |8 |56 |112 |16 |32.000/256 (288) |25.600/256 |8 / 4000 |
| Standard_DS14 |16 |112 |224 |32 |64.000/512 (576) |51.200/512 |8 / 6000 - 8000 &#8224; |

* hello massima velocità effettiva del disco (IOPS o MBps) con una VM di serie DS può essere limitata dal numero di hello, dimensioni e lo striping di hello associata dischi.  Per altre informazioni, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../articles/storage/common/storage-premium-storage.md).


## <a name="d-series"></a>Serie D

ACU: 160

| Dimensione         | vCPU | Memoria: GiB | GiB di archiviazione temp (unità SSD) | Velocità effettiva massima di archiviazione temporanea: IOPS/Mbps di lettura/Mbps di scrittura | Velocità effettiva/disco di dati massimo: IOPS | Schede di interfaccia di rete max/prestazioni rete previste (Mbps) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_D11 | 2         | 14          | 100            | 6000 / 93 / 46                                           | 4/4 x 500                         | 2 / 1000                     |
| Standard_D12 | 4         | 28          | 200            | 12000 / 187 / 93                                         | 8/8 x 500                         | 4 / 2000                     |
| Standard_D13 | 8         | 56          | 400            | 24000 / 375 / 187                                        | 16/16 x 500                       | 8 / 4000                     |
| Standard_D14 | 16        | 112         | 800            | 48000 / 750 / 375                                        | 32/32 x 500                       | 8 / 6000 - 8000 &#8224;                |

<br>

