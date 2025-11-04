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