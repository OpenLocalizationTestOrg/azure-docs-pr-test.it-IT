---
title: benchmark aaaCompute punteggi per le macchine virtuali Linux | Documenti Microsoft
description: Confrontare i punteggi di benchmark di CoreMark calcolo per le VM di Azure che eseguono Linux
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 93e812c1-79dd-40c5-b97b-aa79f5cd7d76
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: cynthn
ms.openlocfilehash: b2c1ca5fbd80cea030ac2cc22156c4e9444c6726
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="compute-benchmark-scores-for-linux-vms"></a>Calcolare i punteggi di benchmark per le VM Linux
Hello seguente mostra i punteggi di CoreMark benchmark delle prestazioni per l'elemento lineup di macchina virtuale ad alte prestazioni di Azure in esecuzione Ubuntu di calcolo. I punteggi di benchmark sul calcolo sono disponibili anche per le [VM Windows](../windows/compute-benchmark-scores.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="a-series---compute-intensive"></a>Serie A - Elevato utilizzo di calcolo
| Dimensione | vCPU | Nodi NUMA | CPU | Esecuzioni | Iterazioni/sec | Deviazione standard |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_A8 |8 |1 |CPU Intel Xeon E5-2670 0 a 2,6 GHz |179 |110.294 |554 |
| Standard_A9 |16 |2 |CPU Intel Xeon E5-2670 0 a 2,6 GHz |189 |210.816 |2.126 |
| Standard_A10 |8 |1 |CPU Intel Xeon E5-2670 0 a 2,6 GHz |188 |110.025 |1.045 |
| Standard_A11 |16 |2 |CPU Intel Xeon E5-2670 0 a 2,6 GHz |188 |210.727 |2.073 |

## <a name="dv2-series"></a>Serie Dv2
| Dimensione | vCPU | Nodi NUMA | CPU | Esecuzioni | Iterazioni/sec | Deviazione standard |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_D1_v2 |1 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |140 |14.852 |780 |
| Standard_D2_v2 |2 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |133 |29.467 |1.863 |
| Standard_D3_v2 |4 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |139 |56.205 |1.167 |
| Standard_D4_v2 |8 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |126 |108.543 |3.446 |
| Standard_D5_v2 |16 |2 |Intel Xeon E5-2673 v3 a 2,4 GHz |126 |205.332 |9.998 |
| Standard_D11_v2 |2 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |125 |28.598 |1.510 |
| Standard_D12_v2 |4 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |131 |55.673 |1.418 |
| Standard_D13_v2 |8 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |140 |107.986 |3.089 |
| Standard_D14_v2 |16 |2 |Intel Xeon E5-2673 v3 a 2,4 GHz |140 |208.186 |8.839 |
| Standard_D15_v2 |20 |2 |Intel Xeon E5-2673 v3 a 2,4 GHz |28 |268.560 |4.667 |

## <a name="f-series"></a>Serie F
| Dimensione | vCPU | Nodi NUMA | CPU | Esecuzioni | Iterazioni/sec | Deviazione standard |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_F1 |1 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |154 |15.602 |787 |
| Standard_F2 |2 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |126 |29.519 |1.233 |
| Standard_F4 |4 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |147 |58.709 |1.227 |
| Standard_F8 |8 |1 |Intel Xeon E5-2673 v3 a 2,4 GHz |224 |112.772 |3.006 |
| Standard_F16 |16 |2 |Intel Xeon E5-2673 v3 a 2,4 GHz |42 |218.571 |5.113 |

## <a name="g-series"></a>Serie G
| Dimensione | vCPU | Nodi NUMA | CPU | Esecuzioni | Iterazioni/sec | Deviazione standard |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_G1 |2 |1 |Intel Xeon E5-2698B v3 a 2 GHz |83 |31.310 |2.891 |
| Standard_G2 |4 |1 |Intel Xeon E5-2698B v3 a 2 GHz |84 |60.112 |3.537 |
| Standard_G3 |8 |1 |Intel Xeon E5-2698B v3 a 2 GHz |84 |107.522 |4.537 |
| Standard_G4 |16 |1 |Intel Xeon E5-2698B v3 a 2 GHz |83 |195.116 |5.024 |
| Standard_G5 |32 |2 |Intel Xeon E5-2698B v3 a 2 GHz |84 |360.329 |14.212 |

## <a name="gs-series"></a>Serie GS
| Dimensione | vCPU | Nodi NUMA | CPU | Esecuzioni | Iterazioni/sec | Deviazione standard |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_GS1 |2 |1 |Intel Xeon E5-2698B v3 a 2 GHz |84 |28.613 |1.884 |
| Standard_GS2 |4 |1 |Intel Xeon E5-2698B v3 a 2 GHz |83 |54.348 |3.474 |
| Standard_GS3 |8 |1 |Intel Xeon E5-2698B v3 a 2 GHz |83 |104.564 |1.834 |
| Standard_GS4 |16 |1 |Intel Xeon E5-2698B v3 a 2 GHz |84 |194.111 |4.735 |
| Standard_GS5 |32 |2 |Intel Xeon E5-2698B v3 a 2 GHz |84 |357.396 |16.228 |

## <a name="h-series"></a>Serie H
| Dimensione | vCPU | Nodi NUMA | CPU | Esecuzioni | Iterazioni/sec | Deviazione standard |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_H8 |8 |1 |Intel Xeon E5-2667 v3 a 3,2 GHz |28 |140.782 |2512 |
| Standard_H16 |16 |2 |Intel Xeon E5-2667 v3 a 3,2 GHz |35 |275.289 |7110 |
| Standard_H18m |8 |1 |Intel Xeon E5-2667 v3 a 3,2 GHz |28 |139.071 |3988 |
| Standard_H16m |16 |2 |Intel Xeon E5-2667 v3 a 3,2 GHz |28 |275.988 |6963 |
| Standard_H16r |16 |2 |Intel Xeon E5-2667 v3 a 3,2 GHz |28 |273.982 |6069 |
| Standard_H16mr |16 |2 |Intel Xeon E5-2667 v3 a 3,2 GHz |28 |274.523 |5698 |

## <a name="about-coremark"></a>Informazioni su CoreMark
I numeri di Linux sono stati calcolati eseguendo [CoreMark](http://www.eembc.org/coremark/faq.php) su Ubuntu. Concorrenza impostati tooPThreads coreMark è stato configurato con hello numero thread set toohello di CPU virtuali. numero di destinazione Hello di iterazioni è stato modificato in base alle prestazioni tooprovide un runtime di almeno 20 secondi (in genere molto più tempo). punteggio finale Hello rappresenta il numero di hello di iterazioni completato diviso hello numero di secondi che necessari test hello toorun. Ogni test è stato eseguito almeno sette volte per ogni VM. Test (tranne che per H series_ sono stati eseguiti in ottobre 2015 in più macchine virtuali in ogni hello area pubblica Azure VM è supportata data hello eseguire.

## <a name="next-steps"></a>Passaggi successivi
* Per conoscere le capacità di archiviazione, i dettagli sul disco e per considerazioni aggiuntive sulla scelta delle dimensioni delle macchine virtuali, vedere [Dimensioni delle macchine virtuali in Azure](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* script di CoreMark toorun hello in macchine virtuali Linux, scaricare hello [CoreMark pack script](http://download.microsoft.com/download/3/0/5/305A3707-4D3A-4599-9670-AAEB423B4663/AzureCoreMarkScriptPack.zip).

