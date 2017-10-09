Hello nella seguente tabella elenca hello requisiti per gateway basato su criteri e RouteBased VPN. Questa tabella si applica hello tooboth Gestione risorse e i modelli di distribuzione classica. Gateway VPN PolicyBased sono hello stesso gateway statico per il modello classico hello e gateway basato su Route sono hello stesso gateway dinamico.

|  | **Gateway VPN Basic PolicyBased** | **Gateway VPN Basic RouteBased** | **Gateway VPN Standard RouteBased** | **Gateway VPN High Performance RouteBased** |
| --- | --- | --- | --- | --- |
| **Connettività da sito a sito** |Configurazione VPN PolicyBased |Configurazione VPN RouteBased |Configurazione VPN RouteBased |Configurazione VPN RouteBased |
| **Connettività da punto a sito (P2S**) |Non supportate |Supportato (può coesistere con Site-to-Site) |Supportato (può coesistere con Site-to-Site) |Supportato (può coesistere con Site-to-Site) |
| **Metodo di autenticazione** |Chiave condivisa |Chiave precondivisa per la connettività da sito a sito, Certificati per la connettività da punto a sito |Chiave precondivisa per la connettività da sito a sito, Certificati per la connettività da punto a sito |Chiave precondivisa per la connettività da sito a sito, Certificati per la connettività da punto a sito |
| **Numero massimo di connessioni Site-to-Site** |1 |10 |10 |30 |
| **Numero massimo di connessioni Point-to-Site** |Non supportate |128 |128 |128 |
| **Supporto routing attivo (BGP)** |Non supportate |Non supportate |Supportato |Supportato |

