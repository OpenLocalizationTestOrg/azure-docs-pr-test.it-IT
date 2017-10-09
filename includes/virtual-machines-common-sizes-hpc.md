<!-- A-series - compute-intensive instances, H-series -->

Hello dimensioni A8 A11 e H serie sono noti anche come *istanze con utilizzo intensivo di calcolo*. progettato e ottimizzato per un utilizzo intensivo di calcolo hardware Hello che esegue queste dimensioni e applicazioni a elevato utilizzo di rete, calcolo ad alte prestazioni (HPC) tra cluster di applicazioni, modellazione e simulazioni. Hello A8 A11 serie utilizza Intel Xeon E5-2670 2,6 GHz e hello H serie utilizza 2667 con Intel Xeon E5 v3 @ 3,2 GHz. 

Macchine virtuali di Azure H serie sono hello successiva generazione elaborazione a elevate prestazioni esigenze di elaborazione di fascia alta, come la modellazione molecolare e fluidodinamica computazionale intese a macchine virtuali. Questi CPU 8 e 16 virtuale le macchine virtuali sono basati sulla tecnologia di processore Intel-2667 Haswalle E5 V3 hello che presenta DDR4 memoria e archiviazione temporanea basate su SSD. 

Offre inoltre la potenza della CPU sostanziale di toohello, hello H serie diverse opzioni per la rete RDMA di bassa latenza utilizzando FDR InfiniBand e diverse configurazioni toosupport memoria con utilizzo intensivo calcolo i requisiti di memoria.



## <a name="h-series"></a>Serie H

ACU: 290-300

| Dimensione | vCPU | Memoria: GiB | GiB di archiviazione temp (unità SSD) | Valore massimo per dischi di dati | Velocità effettiva del disco max: IOPS | Schede di interfaccia di rete max |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_H8 |8 |56 |1000 |16 |16x500 |2  |
| Standard_H16 |16 |112 |2000 |32 |32x500 |4 |
| Standard_H8m |8 |112 |1000 |16 |16x500 |2  |
| Standard_H16m |16 |224 |2000 |32 |32x500 |4  |
| Standard_H16r* |16 |112 |2000 |32 |32x500 |4  |
| Standard_H16mr* |16 |224 |2000 |32 |32x500 |4 |

*Per le applicazioni MPI, la rete back-end RDMA dedicata viene abilitata dalla rete InfiniBand FDR, che offre latenza estremamente bassa e larghezza di banda elevata.

<br>



## <a name="a-series---compute-intensive-instances"></a>Serie A - Istanze a elevato utilizzo di calcolo

ACU: 225

| Dimensione | vCPU | Memoria: GiB | Spazio di archiviazione temp (HDD): GiB | Valore massimo per dischi di dati | Velocità effettiva del disco di dati max: IOPS | Schede di interfaccia di rete max|
| --- | --- | --- | --- | --- | --- | --- |
| Standard_A8* |8 |56 |382 |16 |16x500 |2 |
| Standard_A9* |16 |112 |382 |16 |16x500 |4 |
| Standard_A10 |8 |56 |382 |16 |16x500 |2  |
| Standard_A11 |16 |112 |382 |16 |16x500 |4 |

*Per le applicazioni MPI, la rete back-end RDMA dedicata viene abilitata dalla rete InfiniBand FDR, che offre latenza estremamente bassa e larghezza di banda elevata.

<br>



