
1. privilegi tooescalate, tipo:
   
        sudo -s
   
    Immettere la password.
2. tooinstall Server di MySQL Community edition, digitare:
   
        zypper install mysql-community-server
   
    Attendere fino al termine del download e dell'installazione di MySQL.
3. tooset MySQL toostart sistema hello all'avvio, digitare:
   
        insserv mysql
4. Avviare manualmente il daemon di MySQL hello (mysqld) con questo comando:
   
        rcmysql start
   
    stato hello toocheck di hello daemon MySQL, digitare:
   
        rcmysql status
   
    hello toostop daemon MySQL, digitare:
   
        rcmysql stop
   
   > [!IMPORTANT]
   > Dopo l'installazione, la password radice di MySQL hello è vuota per impostazione predefinita. È consigliabile eseguire **mysql\_secure\_installation**, uno script per la protezione di MySQL. script Hello richiede la password radice di MySQL hello toochange, rimuovere gli account utente anonimo, disabilitare gli account di accesso remoto radice, rimuovere i database di test e ricaricare tabella privilegi hello. È consigliabile rispondere Sì tooall di queste opzioni e modificare la password radice hello.
   > 
   > 
5. Digitare lo script hello toorun script di installazione di MySQL:
   
        mysql_secure_installation
6. Accedi tooMySQL:
   
        mysql -u root -p
   
    Immettere la password radice hello MySQL (che è stato modificato nel passaggio precedente hello) e verrà visualizzata con un prompt dei comandi in cui è possibile emettere toointeract istruzioni SQL con database hello.
7. toocreate un nuovo utente di MySQL, eseguire il seguente hello hello **mysql >** prompt dei comandi:
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    Si noti che i punti e virgola di hello (;) alla fine hello hello sono fondamentali per la chiusura di comandi hello righe.
8. toocreate hello un database e concedere `mysqluser` autorizzazioni su di esso, hello problema seguenti comandi:
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    Si noti che i nomi di database utente e password vengono utilizzate solo per gli script di connessione database toohello.  I nomi di account utente di database non rappresentano necessariamente gli account utente effettivo nel sistema hello.
9. toolog in da un altro computer, digitare:
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    dove `ip-address` è hello l'indirizzo IP del computer di hello da cui verrà effettuata la connessione tooMySQL.
10. hello tooexit utilità di amministrazione di database MySQL, digitare:
    
        quit

## <a name="add-an-endpoint"></a>Aggiungere un endpoint
1. Dopo l'installazione di MySQL, è necessario in modalità remota tooconfigure un tooaccess endpoint MySQL. Accedi toohello [portale di Azure classico][AzurePortal]. Fare clic su **macchine virtuali**, fare clic sul nome della nuova macchina virtuale hello e quindi fare clic su **endpoint**.
2. Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.
3. Aggiungere un endpoint denominato "MySQL" con protocollo **TCP**, e **pubblica** e **privata** porte set troppo "3306".
4. tooremotely connessione macchina virtuale toohello dal computer, tipo:
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    Ad esempio, utilizza una macchina virtuale hello che è create in questa esercitazione, digitare questo comando:
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
