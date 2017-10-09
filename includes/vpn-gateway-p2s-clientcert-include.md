Ogni computer client che si connette tooa virtuale usando Point-to-Site deve avere installato un certificato client. certificato client hello è generato dal certificato radice hello e installato in ogni computer client. Se non è installato un certificato client valido e client hello tenta tooconnect toohello rete virtuale, l'autenticazione ha esito negativo.

È possibile generare un certificato univoco per ogni client oppure è possibile utilizzare hello stesso certificato per più client. i certificati client univoci di Hello vantaggio toogenerating è hello possibilità toorevoke un solo certificato. In caso contrario, se più client utilizzando hello stesso certificato client e necessario toorevoke, aver toogenerate e installare i nuovi certificati per tutti i client che usano tale tooauthenticate certificato di hello.

È possibile generare i certificati client con hello dei seguenti metodi:

- **Certificato aziendale:**

  - Se si utilizza una soluzione di certificato, generare un certificato client con formato del valore nome comune hello 'name@yourdomain.com', invece di formato 'nome dominio\nomeutente.' hello.
  - Verificare che il certificato di client hello è basato sul modello di certificato di 'User' hello con 'Autenticazione Client' come primo elemento nell'elenco utilizzo hello di hello, anziché di Smart Card accesso e così via. È possibile verificare il certificato di hello fare doppio clic sul certificato client hello e visualizzando **dettagli > Utilizzo chiavi avanzato**.

- **Certificato radice autofirmato:** è importante seguire passaggi hello in uno degli articoli certificato hello P2S indicati di seguito. In caso contrario, i certificati client hello creati non sarà compatibili con le connessioni P2S e i client ricevono un errore durante il tentativo di tooconnect. passaggi di Hello in uno dei seguenti articoli hello generano un certificato client compatibile: 

  * [Istruzioni per Windows 10 PowerShell](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientcert): queste istruzioni richiedono certificati toogenerate Windows 10 e PowerShell. certificati Hello generati possono essere installati in qualsiasi client P2S supportati.
  * [Istruzioni MakeCert](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site-makecert.md): utilizzare MakeCert se non si dispongono di accesso tooa Windows 10 computer toouse toogenerate certificati. MakeCert deprecato, ma è comunque possibile usare i certificati toogenerate MakeCert. certificati Hello generati possono essere installati in qualsiasi client P2S supportati.

  Quando si genera un certificato client da un certificato radice autofirmato usando hello precedono le istruzioni, automaticamente installato nel computer di hello utilizzato toogenerate. Se si desidera tooinstall un certificato client in un altro computer client, è necessario tooexport come un file pfx, insieme a hello intera catena di certificati. Questo crea un file con estensione pfx che contiene informazioni sul certificato di hello radice che è necessari per l'autenticazione hello client toosuccessfully. Per passaggi tooexport un certificato, vedere [certificati - esportare un certificato client](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientexport).
