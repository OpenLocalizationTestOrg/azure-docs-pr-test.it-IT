### <a name="is-custom-ipsecike-policy-supported-on-all-azure-vpn-gateway-skus"></a>I criteri IPsec/IKE personalizzati sono supportati in tutti gli SKU del gateway VPN di Azure?
I criteri IPsec/IKE personalizzati sono supportati nei gateway VPN **VpnGw1, VpnGw2, VpnGw3, Standard** e **HighPerformance** di Azure. **Basic** NON è supportato.

### <a name="how-many-policies-can-i-specify-on-a-connection"></a>Quanti criteri è possibile specificare per una connessione?
Per una determinata connessione è possibile specificare ***una*** sola combinazione di criteri.

### <a name="can-i-specify-a-partial-policy-on-a-connection-eg-only-ike-algorithms-but-not-ipsec"></a>Per una connessione è possibile specificare criteri parziali, ad esempio solo algoritmi IKE ma non IPsec?
No. È necessario specificare tutti gli algoritmi e i parametri sia per IKE (modalità principale) che per IPsec (modalità rapida). Non è consentito specificare criteri parziali.

### <a name="what-are-hello-algorithms-and-key-strengths-supported-in-hello-custom-policy"></a>Quali sono gli algoritmi di hello e vantaggi chiave supportate nei criteri personalizzati di hello?
tabella di Hello seguente sono elencati i vantaggi chiave configurabile da parte dei clienti hello e algoritmi di crittografia di hello è supportato. È necessario selezionare un'opzione per ogni campo.

| **IPsec/IKEv2**  | **Opzioni**                                                                   |
| ---              | ---                                                                           |
| Crittografia IKEv2 | AES256, AES192, AES128, DES3, DES                                             |
| Integrità IKEv2  | SHA384, SHA256, SHA1, MD5                                                     |
| Gruppo DH         | DHGroup24, ECP384, ECP256, DHGroup14 (DHGroup2048), DHGroup2, DHGroup1, None |
| Crittografia IPsec | GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None      |
| Integrità IPsec  | GCMAES256, GCMAES192, GCMAES128, SHA256, SHA1, MD5                            |
| Gruppo PFS        | PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, None                              |
| Durata associazione di sicurezza in modalità rapida   | Secondi (intero; **min. 300**/valore predefinito di 27000 secondi)<br>Kilobyte (intero; **min 1024**/valore predefinito di 102400000 KB)           |
| Selettore di traffico | UsePolicyBasedTrafficSelectors ($True/$False; valore predefinito: $False)                 |
|                  |                                                                               |

> [!IMPORTANT]
> 1. DHGroup2048 & PFS2048 sono hello stesso come gruppo Diffie-Hellman **14** IKE e IPsec PFS. Vedere [gruppi Diffie-Hellman](#DH) per hello completare i mapping.
> 2. Per gli algoritmi GCMAES, è necessario specificare hello stessa lunghezza di chiave e l'algoritmo GCMAES per la crittografia di IPsec e integrità.
> 3. Durata SA modalità principale di IKEv2 è fissata a 28.800 secondi nei gateway VPN di Azure hello
> 4. Le durate dell'associazione di sicurezza QM sono parametri facoltativi. Se non ne è stato specificato nessuno, vengono usati i valori predefiniti pari a 27.000 secondi (7,5 ore) e 102400000 KB (102 GB).
> 5. UsePolicyBasedTrafficSelector è un parametro di opzione nella connessione hello. Vedere Domande frequenti hello articolo per "UsePolicyBasedTrafficSelectors"

### <a name="does-everything-need-toomatch-between-hello-azure-vpn-gateway-policy-and-my-on-premises-vpn-device-configurations"></a>Tutto il necessario toomatch tra hello criteri gateway VPN di Azure e le configurazioni del dispositivo VPN personale locale?
La configurazione del dispositivo VPN locale deve corrispondere o contenere hello seguenti algoritmi e i parametri specificati in hello criteri IPsec/IKE Azure:

* Algoritmo di crittografia IKE
* Algoritmo di integrità IKE
* Gruppo DH
* Algoritmo di crittografia IPsec
* Algoritmo di integrità IPsec
* Gruppo PFS
* Selettore di traffico (*)

durate Hello SA solo specifiche locale, non è necessario toomatch.

Se si abilita **UsePolicyBasedTrafficSelectors**, è necessario il dispositivo VPN è hello corrispondenza selettori traffico definiti con tutte le combinazioni dei prefissi (gateway di rete locale) di rete locale a/da hello tooensure Prefissi di rete virtuale di Azure, anziché any per qualsiasi. Ad esempio, se i prefissi di rete locale sono 10.1.0.0/16 e 10.2.0.0/16 e i prefissi di rete virtuale sono 192.168.0.0/16 e 172.16.0.0/16, è necessario hello toospecify selettori di traffico seguenti:
* 10.1.0.0/16 <====> 192.168.0.0/16
* 10.1.0.0/16 <====> 172.16.0.0/16
* 10.2.0.0/16 <====> 192.168.0.0/16
* 10.2.0.0/16 <====> 172.16.0.0/16

Fare riferimento troppo[connettere più dispositivi VPN locale basata su criteri](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) per ulteriori informazioni su come toouse questa opzione.

### <a name ="DH"></a>Quali gruppi Diffie-Hellman sono supportati?
tabella di Hello seguente sono elencati i gruppi di Diffie-Hellman hello è supportato per IKE (DHGroup) e IPsec (PFSGroup):

| **Gruppo Diffie-Hellman**  | **DHGroup**              | **PFSGroup** | **Lunghezza chiave** |
| ---                       | ---                      | ---          | ---            |
| 1                         | DHGroup1                 | PFS1         | MODP a 768 bit   |
| 2                         | DHGroup2                 | PFS2         | MODP a 1024 bit  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | MODP a 2048 bit  |
| 19                        | ECP256                   | ECP256       | ECP a 256 bit    |
| 20                        | ECP384                   | ECP284       | ECP a 384 bit    |
| 24                        | DHGroup24                | PFS24        | MODP a 2048 bit  |
|                           |                          |              |                |

Fare riferimento troppo[RFC3526](https://tools.ietf.org/html/rfc3526) e [RFC5114](https://tools.ietf.org/html/rfc5114) per altri dettagli.

### <a name="does-hello-custom-policy-replace-hello-default-ipsecike-policy-sets-for-azure-vpn-gateways"></a>Criteri personalizzati di hello sostituisce hello IPsec/IKE criteri predefiniti per i gateway VPN di Azure?
Sì, dopo aver specificato un criterio personalizzato su una connessione, il gateway VPN di Azure utilizzerà solo criteri hello in connessione hello, sia come iniziatore IKE e il risponditore IKE.

### <a name="if-i-remove-a-custom-ipsecike-policy-does-hello-connection-become-unprotected"></a>Se si rimuove un criterio IPsec/IKE personalizzato, non connessione hello diventa non protetto?
No, connessione hello comunque essere protetti da IPsec/IKE. Dopo aver rimosso i criteri personalizzati di hello da una connessione, i gateway VPN di Azure hello verrà ripristinato toohello Indietro [elenco predefinito delle proposte di IPsec/IKE](../articles/vpn-gateway/vpn-gateway-about-vpn-devices.md) e riavviare hello handshake IKE nuovamente con il dispositivo VPN locale.

### <a name="would-adding-or-updating-an-ipsecike-policy-disrupt-my-vpn-connection"></a>L'aggiunta o l'aggiornamento di criteri IPsec/IKE determinerà un'interruzione della connessione VPN?
Sì, potrebbe causare un'interruzione di piccole dimensioni (alcuni secondi) come gateway VPN di Azure hello verranno nuovamente avviati hello toore handshake IKE e chiudere la connessione esistente hello-stabilire il tunnel IPsec hello con nuovi algoritmi di crittografia hello e parametri. Verificare che il dispositivo VPN locale viene inoltre configurato con gli algoritmi corrispondente hello e interruzioni di hello toominimize vantaggi chiave.

### <a name="can-i-use-different-policies-on-different-connections"></a>È possibile usare criteri diversi per connessioni diverse?
Sì. I criteri personalizzati vengono applicati in base alla connessione. È possibile creare e applicare criteri IPsec/IKE diversi per connessioni diverse. È anche possibile scegliere tooapply criteri personalizzati in un subset di connessioni. Hello restanti utilizzerà hello Azure IPsec/IKE criteri predefiniti.

### <a name="can-i-use-hello-custom-policy-on-vnet-to-vnet-connection-as-well"></a>È possibile utilizzare i criteri personalizzati di hello sulla connessione di rete virtuale a nonché?
Sì. È possibile applicare criteri personalizzati sia a connessioni cross-premise IPsec che a connessioni da rete virtuale a rete virtuale.

### <a name="do-i-need-toospecify-hello-same-policy-on-both-vnet-to-vnet-connection-resources"></a>Necessario toospecify hello stessi criteri in entrambe le risorse di connessione di rete virtuale a?
Sì. Un tunnel da rete virtuale a rete virtuale è costituito da due risorse di connessione di Azure, una per ogni direzione. È necessario tooensure dispongono di entrambe le risorse connessione hello stesso criterio, non consentirà di stabilire hello othereise da rete connessione.

### <a name="does-custom-ipsecike-policy-work-on-expressroute-connection"></a>I criteri IPsec/IKE personalizzati funzionano in una connessione ExpressRoute?
No. Criteri IPsec/IKE funziona solo su VPN S2S e le connessioni di rete virtuale a tramite gateway VPN di Azure hello.
