### <a name="prepare-for-a-push-installation-on-a-linux-server"></a>Preparare un'installazione push in un server Linux

1. Verificare che vi sia connettività di rete tra i computer Linux hello e il server di elaborazione hello.
2. Creare un account di che tale server di elaborazione hello può usare computer hello tooaccess. Hello account deve essere un **radice** utente nel server di hello origine Linux. (Utilizzare questo account solo per l'installazione push hello e per aggiornamenti).
3. Controllare il file /etc/hosts hello sull'origine hello Linux server dispone di voci che eseguono il mapping di indirizzi di tooIP hello nome host locale associati a tutte le schede di rete.
4. Installare i pacchetti di openssh e openssh server openssl più recenti hello nel computer di hello che si desidera tooreplicate.
5. Assicurarsi che SSH (Secure Shell) sia abilitato e in esecuzione sulla porta 22.
6. Abilitare l'autenticazione SFTP di sottosistema e la password nel file sshd_config hello:
  1.  Accedere come utente **root**.
  2.  In hello file via/ssh/file sshd_config, trova hello riga che inizia con **PasswordAuthentication**.
  3.  Rimuovere il commento riga hello e modificare il valore di hello troppo**Sì**.
  4.  Riga hello di ricerca che inizia con **sottosistema** e rimuovere il commento riga hello.

     ![Linux](./media/site-recovery-prepare-push-install-mob-svc-lin/mobility2.png)
  5. Riavviare hello **sshd** servizio.

7. Aggiungere account hello creati in CSPSConfigtool.
    1.  Accedi a server di configurazione tooyour.
    2.  Aprire **cspsconfigtool.exe**. (È disponibile come collegamento sul desktop hello e nella cartella %ProgramData%\home\svsystems\bin hello.)
    3.  In hello **Gestisci account** scheda, fare clic su **Aggiungi Account**.
    4.  Aggiungere account hello creato. 
    5.  Immettere le credenziali di hello che è utilizzare quando si abilita la replica per un computer.
