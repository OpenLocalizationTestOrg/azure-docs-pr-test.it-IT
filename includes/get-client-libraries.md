### <a name="install-via-composer"></a>Installazione tramite Composer
1. [Installare Git][install-git]. Si noti che in Windows, è necessario aggiungere anche variabile di ambiente PATH tooyour eseguibile hello Git. 
2. Creare un file denominato **composer.json** in hello radice del progetto e aggiungere hello tooit di codice seguente:
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. Scaricare **[composer.phar][composer-phar]** nella radice del progetto.
4. Aprire un prompt dei comandi ed eseguire hello seguente comando nella radice del progetto
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
