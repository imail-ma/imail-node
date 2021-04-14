# imail.ma for Node

Librairie pour l'envoie d'e-mails via imail.ma en Node.

## Installation

Installez la librairie en utilisant  [NPM](https://www.npmjs.com/):

```
$ npm install @imail.ma/imail --save
```

## Usage

L'envoi d'un e-mail est très simple. Suivez simplement l'exemple ci-dessous. Avant de pouvoir commencer, vous vous devez vous connecter à notre interface Web et générer un nouvel identifiant API.

```javascript
// Inclure la librairie imail.ma 
var Imail = require('@imail.ma/imail');

// Créez un nouveau client imail à l'aide de la clé de serveur que vous générez dans l'interface Web 
var client = new Imail.Client('https://mx.imail.ma', 'your-api-key');

// Créer un nouveau message 
var message = new Imail.SendMessage(client);

// Ajouter quelques destinataires 
message.to('simo@domaine.ma');
message.to('youssef@domaine.ma');
message.cc('mehdi@domaine.ma');
message.bcc('secret@domaine.ma');

// Spécifiez de qui le message doit provenir. Cela doit provenir d'un domaine vérifié 
// sur votre serveur de messagerie.
message.from('test@domaine.ma');

// Définir le sujet
message.subject('Salam!');

// Définir le contenu de l'e-mail 
message.plainBody('Hello world!');
message.htmlBody('<p>Hello world!</p>');

// Ajouter des en-têtes personnalisés
message.header('X-PHP-Test', 'value');

// Joindre des fichiers 
message.attach('textmessage.txt', 'text/plain', 'Hello world!');

// Envoyez le message et obtenez le résultat 
message.send()
  .then(function (result) {
    var recipients = result.recipients();
    // Parcourez chacun des destinataires pour obtenir l'ID du message
    for (var email in recipients) {
      var message = recipients[email];
      console.log(message.id());    // Renvoie l'ID du message 
      console.log(message.token()); // Renvoie le jeton du message 
    }
  }).catch(function (error) {
    // Faire quelque chose avec l'erreur 
    console.log(error.code);
    console.log(error.message);
  });
```
