====== n-tier RAD for web application ======

En 2015, il existe surement plusieurs milliers de frameworks web, répartis sur différentes technologies. Chacun offrant plus ou moins de possibilités.

La mode va vers les frameworks Javascript, aussi bien coté client que coté serveur (nodejs / express).

Coté client, le OnePageApp a pris le dessus, et les frameworks clients permettant le rendu et le management d'application existent aussi en quantité astronomique. Les plus populaires étant ReactJS, EmberJS, AngularJS.

Après 7 ans de développement interne chez opendena, la tendance nous amène à nous orienter sur une stack de ce type. Nos réflexions, et études n'ont bien évidemment pas permis de faire ressortir un framework plus intéressant que les autres. Cependant, voici ici l'axe que je souhaite prendre pour structurer les développements à l'avenir pour avoir à disposition un design pattern permettant de sortir rapidement des applications web ou mobiles, sans réécrire ou réinventer la roue à chaque nouvelle implémentation.

====== JS everywhere ======
.


====== Séparer les affichages de la fourniture des données ======

Il est je pense nécessaire maintenant de séparer la partie Application rendering (HTML) de la partie Application working (API)

Cela va au-delà de la simple utilisation de templates et de vue coté client. Le modèle MVC appliqué au stockage du projet. 

La complexité d'un projet se retrouve au final à la complexité de son arborescence, et ses routes ou configurations pour fournir les différentes parties.

Il n'est plus nécessaire de maintenir dans le même projet la partie apps de la partie API et créer cette séparation de manière explicité via la gestion du projet doit permettre d'exploiter au maximum la gestion en micro-service.

L'émergence de site fournissant la database(firebase.io) ou les services annexes(pubsub.io) en mode SaaS pour des applis web prouvent la tendance à vouloir/pouvoir séparer les affichages (vue) du comportement ou des fournisseurs de données. 


====== WebFront  HTML ======

Contient les pages/codes/astuces/algo/tests(end2end) pour le rendering des pages/rubriques de l'application.
En théorie, l'application doit être capable de fonctionner sur une API bouchon ne contenant que des jsons statistiques ou un firebase.

Le frontend est généré via un make install.

L'appli est fourni en statique. 

Le webserveur ne doit pas interagir dans le fonctionnement de l'application.


====== BackOffice for microservice API responsive ======

Le(s) site(s) met à disposition la ou les API pour fournir /répondre à un service / demande.
Il peut y avoir plusieurs sous api, ou un seul router. L'idéal est aussi de séparer les services du projet tant qu'un service loader cohérent n'existe pas.

Le système dispose d'une authentification et l'accès à des tokens. 

Le système cloisonne et isole les ressources par domaine

Actuellement, le framework retenu pour gérer le(s) backend(s) API est loopback


====== Contents components (CDN like) ======

L'émergence des webcomponents doit permettre aussi d'ajouter un niveau de cloisonement supplémentaire. Ce niveau doit permettre de simplifier la vue "haute" de l'application et ses concepts, celle-ci faisant appel à plus ou moins de composants applicatifs appelant eux-même les API dont ils ont besoin.

Modules, snippets, et webcomponents sont mis à disposition sur un troisième backend.  

La question de la gestion des modules en nodejs/bower/etc ne se posent quasiment plus sur les modules principaux accessibles ici ou via leur origine. 

Des packages/bundles doivent permettre d'accéder à ces mêmes modules packagés (minifiés/sourcés/etc...)

====== Communications intercomposants & réactions évenementiels (one way workflow) ======




