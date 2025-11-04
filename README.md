 # What's next ? Symfony Instructions 
 ## doctrine/doctrine-bundle  instructions:

  * Modify your DATABASE_URL config in .env

  * Configure the driver (postgresql) and
    server_version (16) in config/packages/doctrine.yaml

 ## phpunit/phpunit  instructions:

  * Write test cases in the ``tests/`` folder
  * Use MakerBundle's ``php bin/console make:test`` command as a shortcut!  
            👉 À quoi ça sert ?
            Gagner du temps : Au lieu d’écrire manuellement la structure de base d’un test, la commande génère pour toi une classe de test avec les use nécessaires, la méthode de test et même des assertions basiques.
            Respecter les bonnes pratiques : Les tests générés suivent les conventions de Symfony et PHPUnit.
            Faciliter l’intégration : La commande détecte automatiquement si tu utilises PHPUnit ou Pest, et adapte le code généré.

  * Run the tests with ``php bin/phpunit``

 ## symfony/messenger  instructions:

  * You're ready to use the Messenger component. You can define your own message buses
    or start using the default one right now by injecting the message_bus service
    or type-hinting Symfony\Component\Messenger\MessageBusInterface in your code.

  * To send messages to a transport and handle them asynchronously:

    1. Update the MESSENGER_TRANSPORT_DSN env var in .env if needed
       and framework.messenger.transports.async in config/packages/messenger.yaml;
    2. (if using Doctrine) Generate a Doctrine migration bin/console doctrine:migration:diff
       and execute it bin/console doctrine:migration:migrate
    3. Route your message classes to the async transport in config/packages/messenger.yaml.

  * Read the documentation at https://symfony.com/doc/current/messenger.html

 ## symfony/mailer  instructions:

  * You're ready to send emails.

  * If you want to send emails via a supported email provider, install
    the corresponding bridge.
    For instance, composer require mailgun-mailer for Mailgun.

  * If you want to send emails asynchronously:

    1. Install the messenger component by running composer require messenger;
    2. Add 'Symfony\Component\Mailer\Messenger\SendEmailMessage': amqp to the
       config/packages/messenger.yaml file under framework.messenger.routing
       and replace amqp with your transport name of choice.

  * Read the documentation at https://symfony.com/doc/master/mailer.html


  # Configurations du projet
1. Configurer le dossier avec symfony 
```console
  *composer create-project symfony/skeleton:"^7.3" blogstudisymfony*
  *composer require webapp*

```
2. Configurer le serveur local WAMP 
  Dans le fichier HTTPD-VHOSTS.CONF, mettre :
```console
   <VirtualHost *:80>
    DocumentRoot "C:/wamp64/www/blogstudisymfony/public"
    ServerName blogstudisymfony.local
    <Directory "C:/wamp64/www/blogstudisymfony/public">
        Options +Indexes +Includes +FollowSymLinks +MultiViews
        AllowOverride All
        Require all granted
    </Directory>
    SetEnv APP_ENV dev
    SetEnv APP_DEBUG 1
</VirtualHost>
```

3. Configurer le fichier HOSTS de Windows (⚠️EN MODE ADMINISTRATEUR)
Ajouter l'adresse et le nom du projet  :

```console
127.0.0.1 blogstudisymfony.local
```
👉 Redémmarrer WAMP, puis tester la connexion dans le navigateur : *blogstudisymfony.local/*

4. Configurer GIT

*git init* dans le projet

*git add .* pour ajouter toute la config du projet

*git commit -m "first commit"* 

*git branch -M main* créer la branche principal (main)

👉 sur [GitHub.com](https://github.com) créer un Repository au nom du projet

*git remote add origin https://github.com/Guigui5122/blogstudisymfony.git* permet de lier le projet au repository sur Github

*git push -u origin main* pousser les modifications sur Github (1er commit + toute la config symfony, etc...)

*git status* voir l'état de git

5. Configuration Translation.yaml

👉 Dans le dossier $Config/Packages/translation.yaml$ -> mettre *'fr'* à la place de *'en'*

6. Configuration des fichiers d'Environnement (.env / .env.local)

Dans le fichier .env mettre uniquement des informations d'exemples car il est commit sur Git et accessible par d'autres utilisateurs
Créer un fichier .env.local pour la configuration avec les données personnels (DATABASE, SMTP, etc...)



7. Création des tables de notre Bdd avec Doctrine
  1) Taper la commande : 

```console
  php bin/console make:entity

```  
  2) Création et paramétrage de l'entité
  La console pose une série de questions qui permet de configurer la table (ajout de propriété, type de champ (bool, int, string), etc...)

👉 Action à répéter 'x' fois le nombre de table dont vous avez besoin! 

8. Création d'une entité User (Commande spéciale qui un système de gestion des utilisateurs)

  Taper la commande : 

    ```console
    php bin/console make:user
    ```
9. Terminer la configuration de la BDD :
  Taper les commandes suivvantes dans l'ordre :

  Création de la base de données, et migration :

```console
  php bin/console doctrine:database:create
  php bin/console make:migration
  php bin/console doctrine:migration:migrate

```

>> création des vues, routes et controleurs 