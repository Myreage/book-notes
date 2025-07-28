Domain-Driven Design: Tackling Complexity in the Heart of Software
Eric Evans

# Part 1 - Putting the Domain Model to work

## Preface + Chapter 1 - Crunching knowledge

- La plupart du temps, le gros focus des SE devrait être le domaine et la domain logic
- Complex domain designs should be based on a model

Le DDD est:

- une façon de penser
- un set de prios pour accélerer le dev de logiciels complexes en terme de domaine

Période d'évolution des process:

- on ne veut plus du vieux process "Design then Code" car on s'est rendu compte qu'il manque cruellement de feedback loop et qu'il est trop rigide
- on lui préfère l'agilité: continuous refactoring, etc mais on tombe alors dans l'inverse: on va trop vite, on abstrait plus, on accumule de la dette, le logiciel devient bordélique

Le DDD se base sur la mise au point d'un modèle du domaine, en collaboration entre devs et experts métiers. Ce modèle sert de base de communication entre les équipes, et de base d'implémentation du logiciel (enfait, il doit être totalement lié au code)

Ingrédients pour construire un modèle efficacement:

- Lier le modèle et l'implementation: le code doit être à jour si le modèle évolue
- Cultiver un langage basé sur le modèle
- Avoir de la connaissance dans son modèle: pas juste un schema d'objets, il faut que le modèle contienne les règles, les comportements, etc
- Distiller le modèle: quand des concepts ne sont plus utiles, il doivent sortir du modèle
- Brainstorms et expérimentation: il faut se faire des séances de discussions, de schemas gribouillis, pour arriver à un modèle. L'attitude "brainsto" aide beaucoup

Au niveau du code, il est important qu'on retrouve clairement cette knowledge. Dans l'idéal, avec un tout petit peu d'aide d'un dev, un domain expert doit pouvoir lire le code et rapidement y retrouver les business rules qu'il connait de son métier.

Avec un bon modèle, le code qui suit, et des méthodes itératives, on peut à terme avoir une codebase motrice en features (le modèle est si bien implémenté que les features émergent d'elles-mêmes)

## Chapter 2 - Communication and the use of language

Le business a son langage, les devs ont leur langage. Pour communiquer entre eux, ils sont obligés de faire des traductions. Or qui dit traduction, dit téléphone arabe, imprécisions, etc. Pour palier à ça, on met au point un `Ubiquitous Language` qui permet à tout le monde d'utiliser le même langage dans le cadre de discussions dans le scope du domain model.
Model et UL doivent être complètement liés. Si l'un change, l'autre aussi. Les domain experts doivent s'assurer que les termes sont adéquats, et les experts techs doivent s'assurer qu'il n'y a pas d'ambiguité ou d'inconsistence.
Cet UL doit se retrouve partout: dans les discussions, les schemas, le code, etc
Pour mettre au point et raffiner ce langage, il faut le pratiquer. Et se forcer à n'utiliser que lui dans les discussion. Quand on se rend compte qu'il manque qq chose ou qu'il faut l'altérer, on reporte immédiatement les changements dans le code et les diagrammes.

### Diagrammes

C'est très bien de faire plein de diagrammes, surtout dans le cadre de discussions pour que tout le monde s'y retrouve. Il ne faut pas accorder trop d'importance au format (UML, sequence, patates...). Le diagramme est juste là pour faciliter la communication. **Le modèle n'est pas le diagramme**. Il n'est donc pas productif de faire des giga diagrammes qui contiennent absolument toute la logique. Le code est bien meilleur pour ça.

### Documents

Il en va de même pour les documents. Le code est un bien meilleur candidat pour documenter le modèle avec précision. Les documents doivent juste apporter des petits compléments. Ils doivent rester clairs, succins, et surtout à jour.

## Chapter 3 - Binding model and implementation

Bien souvent, on a un modèle et au moment de l'implémenter on se rend compte qu'il n'est pas du tout pratique à coder. Dans ces cas là on peut être tenté de développer un autre modèle plus technique: une sorte de modèle analytique. Mais dans ce cas là, on part dans tous les sens et le modèle initial perd de son utilité. Donc no ! Un seul modèle ! Il faut donc organiser l'implem de façon à refléter le modèle avec des abstractions par exemple, et éventuellement tweak le modèle lui-même pour le rendre plus "implémentable"

Pour cela, la POO est tout indiquée. Les objets existent réellement, ont des relations entre eux, etc etc.

En dissimulant la réalité technique au user, on s'expose à des bugs ou à des incompréhensions. Exemple, les favoris d'un web browser:

- le user s'attend à ce que ce soit juste une url pinnée
- en réalité, c'est stocké sous forme de fichier
- si le user appelle son favoris "Cuisine: les bases", le système va gueuler "invalid filename"
- le user va être complètement paumé, pourquoi on lui parle de file ?

Plus le modèle est au point, plus l'implémentation lui est fidèle, et plus ses entrailles sont exposables au user.

On le répète mais il est **crucial** que les gens qui maintiennent le modèle soient les même que ceux qui codent.

# Part 2 - The Building Blocks of a Model-Driven Design

Le style de design dans ce bouquin suit le principe de "responsibility-driven design" (Wirfs-Brock 1990 & Wirfs-Brock 2003) et le "design by contract" (Meyer 1988).
Les termes utilisés ici font partie d'un Ubiquitous Language du DDD, que chacun devrait maitriser. Cf nagiation map p.66

## Chapter 4 - Isolating the Domain

Le domain est souvent qu'une petite partie de la codebase, mais son importance est énorme.
Il est important qu'il soit clairement lisible et identifiable pour qu'on puisse le travailler, sans avoir à déchiffre/extraire ce code dans un mic-mac technique -> il faut l'isoler.

### Layered architecture

L'idée de la layered architecture est de diviser les concerns de l'application (UX, application, domain, infra par exemple), et chaque couche ne dépend que d'elle-même ou des layers d'en dessous. Le communication avec les autres couches se fait de façon indirecte.
Les grand classiques (mais ce n'est pas nécessairement "la seule et unique façon"):

- User Interface: s'occupe de montrer et de récupérer les inputs user
- Application Layer: coordinateur, expose ce que l'application est capable de faire sans introduire de logique
- Domain Layer: le coeur du domain
- Interface Layer: persistence, dépendances, envoi de messages, librairies UX, etc etc

### The Domain Layer is Where the Model Lives

domain model = concepts
domain layer = manifestation de ces concepts (mirroir)

### The Smart UI "Anti-Pattern"

Quand on est une petite team, sur un petit projet, faut pas non plus aller faire du DDD pour le plaisir.
Quand c'est applicable, juste go foutre toute la logique dans le front, en decouplant bien les "applications", avec une db chiasseuse.
Avantages:

- mega productivité
- n'importe quel dev peut s'y coller
- itérations rapides
- refacto rapide
  Désavantages:
- Pas d'abstraction, pas de réusabilité
- Refacto devient rapidement complexe
- On se fait vite rattraper par la complexité

## Chapter 5 - A Model Expressed in Software

3 patterns expriment le modèle:

- Entities: objet avec une identité et une continuité
- Value objects: un attribut qui décrit l'état de quelque chose d'autre
- Services: pour tout ce qui s'exprime en actions/operations plutôt qu'objets. Un service est quelque chose qui est fait pour un client on request.

### Associations

Les associations entre objets c'est facile sur le modèle, mais pas facile à implémenter.
"For every traversable association in the model, there is a mechanism in the software with the same properties"

C'est pas facile à implémenter, mais c'est omni-présent dans le modèle. Alors comment faire ?
3 idées:

- imposer une direction de lecture
- ajouter un qualifier, pour réduire la multiplicité
- eliminer les associations inutiles

#### Exemple:

Country <-president-> Person

On va généralement partir de Country pour savoir qui est son président, pas partir d'une personne et se demander "de quel pays est-elle président" ?
Donc Country -president-> Person

Ensuite, on va généralement chercher qui était le président à telle date. Donc on ajoute un qualifier
Country[period] -president-> Person

### Entities

Exemple simple = une personne
Une personne a une identité. Elle reste la même personne toute sa vie, mais ses paramètres changent: taille, poids, cheveux....

"Some objects are not defined primarily by their attributes. They represent a thread of identity that runs through time and often accross distinct representations. Sometimes such an object must be matched with another object even though attributes differ. An object must be distinguished from other objects even though they might have the same attributes. Mistake identity can lean to data corruption".

Entity = objet défini principalement par son identité.
Une entité a un lifecycle, elle nait, meurt, évolue au court du temps.

Ce n'est pas parcequ'un objet a un id qu'il est une entity.

"When an object is distinguished by its identity, rather than its attributes, make this primary to its definition in the model. Keep the class definition simple and focused on life cycle continuity and identity. Define a means of distinguishing each object regardless of its form or history. Be alert to requirements that call for matching objects by attributes. Define an operatino that is guaranteed to produce a unique result for each object, possibly by attaching a symbol that is guaranteed unique. This means of identification may come from the outside, or it may be an arbitraty identifier created by and for the system, but it must correspond to the identity distinctions in the model. The model must define what it means to be the same thing"

#### Modeling Entities

La responsabilité la plus basique d'une entity est d'établir la continuité pour que le comportement soit clair et prédictible.
Il faut commencer petit, ne prendre que les attributs vraiment importants, en particulier ceux qui définissent l'identité.
En particulier, les attributs propres à l'identité devraient être dans l'entity, pas une autre (par ex le phone number d'un customer ne devrait pas être dans une autre entity CustomerContact)
Il ne faut ajouter que les comportements essentiels au concept, et les attributs nécessaires à ces comportements.
Le reste sera peut être géré par d'autres entities ou value objects

#### Designing the identity operation

"Each entity must have an operational way of establishing its identity with another object"

### Value Objects

N'ont pas d'identité
Servent à décrire les caractéristiques de qq chose.
On pourrait coller un id à tout objet d'un système, mais il y a des objets qui n'ont pas besoin d'identité. Dans ce cas on alourdit et complexifie le système pour rien

Une value object n'est pas forcément un scalaire, ça peut être un assemblage d'objets. Ca peut même référencer une Entity: par exemple dans un système de GPS, une Route qui référence 2 Locations (qui sont elles des Entities)

Les Value Object doivent être immutables: en effet, vu qu'ils n'ont pas d'identité, on pourrait imaginer 2 Person avec le même Name. Si on mute ce name sur un des Person, il mute pour l'autre. No good !
On peut déroger à cette règle dans certains cas par simplification, mais il faut faire gaffe ! Par exemple:

- la valeur change fréquemment
- le coup de création/deletion est élevé
- il n'y a pas de sharing

De façon générale, partager des VO peut être un peu risqué donc c'est à utiliser avec parcimonie
Les avantages de partager étant principalement de l'ordre de l'optimisation (stockage par ex)

Bref les faire immutables, c'est plus safe.

De préférence, les infos doivent être un "whole". Donc par exemple au lieu d'avoir city, street, postalCode sur une entity Person, on va avoir un Value Object Address qui contient tout ça

### Services

Parfois on arrive pas à relier des opérations à un objet.
Dans ces cas là parfois on va essayer de les foutre dans un objet quand même, menant à une perte de clarté, et à une distorsion du modèle.
C'est là que les Services interviennent.

Un Service est tout simplement une opération qu'on expose. Elle n'a pas de state comme les entities ou les vo.
Il est purement défini par "ce qu'il peut faire pour le client".
Il est plutôt défini par un verbe que par un nom.
Sa responsabilité doit clairement être définie, et faire partie du domain model.

3 caractéristiques d'un bon service:

- L'opération fait référence à un concept domain qui ne fait pas naturellement partie d'une entity ou vo
- L'interface est définie avec d'autres éléments du domain model
- L'opération est stateless

En terme de layers ça donne ça par exemple:

- Application: Funds Transfer App Service - digère l'input, envoie un mess au domain service pour effectuer la demande, listen pour la confirmation, décide d'envoyer une notif en utilisant l'infrastructure service
- Domain: Funds Transfer Domain Service - intéragis avec Account et Ledger pour faire les débits et les crédits, fournit des résultats sur la transaction (not allowed, etc)
- Infra: Send Notification Service - envoie les mails, notifs, etc comme demandé par l'application

### Modules

Egalement appelés packages, sont plus une contrainte technique qu'autre chose.
Si on les utilise, il faut respecter le principe de "low coupling, high cohesion" -> les modules doivent être découplés, mais à l'intérieur tout doit être cohérent.
Si on les utilise, il faut les référencer dans le domain model
C'est cependant intéressant pour séparer la domain logic du reste du code

### Modeling paradigms

La POO est parfaitement alignée avec le DDD parcequ'on parle d'objets, que la techno est robuste et très utilisée.
On peut faire autrement, mais il faut respecter la règle "l'implem doit refléter le model". Si on y arrive pas, c'est qu'il faut arrêter cette techno (ou le DDD)

## Chapter 6 - The life cycle of a domain object

### Aggregates

On a vu plus tôt que c'est mieux de simplifier au maximum les associations. En réalité, y en a tellement partout que ça devient vite le bordel.

An Aggregate is a cluster of associated objects that we treat as a unit for the purpose of data change.

Un aggregate a:

- une root: le seul élément de l'aggregate que l'exterieur peut référencer
- une boudary: définit ce qu'il y a dans l'aggregate

Exemple de la voiture p.127

- L'entity root a une identité globale, et est responsable de maintenir les invariants
- Les entities dans la boundary (autre que la root) ont des identités locales, valables uniquement au sein de l'aggregate
- A l'extérieur de l'aggregate, rien ne peut tenir de référence aux entities internes à part la root. La root peut cependant transmettre des références aux entités internes, pour un usage temporaire
- Seul la root peut être obtenue par une query db. Les autres sont trouvés par des associations
- Les objets dans l'aggregat peuvent référencer d'autres aggregate roots
- Un DELETE doit supprimer tout ce qui se trouve dans l'aggregat
- Quand un changement a lieu dans la boundary, tous les invariants doivent être satisfaits

-> Il est très utile d'avoir un framework qui permette de déclarer des aggregates

Exemple Purchase Order p.130

### Factories

Parfois la création d'un objet est très complexe (dans le cas d'Aggregates par exemple), et elle n'a pas un gros interêt d'un pdv du domaine. Par contre, ça reste la responsabilité du domain. Dans ce cas là, on peut créer des Factories, dont la seule responsabilité est de créer des objets.
Globalement, on crée des factories quand on veut cacher les détails techniques de la création

Pour une bonne Factory il faut:

- Atomique et assure tous les invariants.
- Abtrait en le type désiré, plutôt que dans la classe crée concrètement

Parfois le constructeur c'est quand même mieux quand:

- L'implem est importante
- La construction est simple

### Repositories

Récupérer des trucs de la db (ou plutôt reconstituer), ça doit se limiter aux entities et aux root entities:

- les VO doivent être récupérés transversalement (Person.adress)
- les objets internes des aggregates sont obligatoirement récupérés transversalement aussi (PO.productLines)

Autrement dit, SEULES LES ROOT ENTITIES ONT DROIT AUX REPOSITORIES (ou celles qui sont root de leur aggregate dans lequel elles sont toutes seules)

Les Repositories sont là pour encapsuler la logique de database et nous laisser nous focus sur le domain et l'intention.

Avantages:

- Modèle simple pour obtenir des objets persistants et gérer leur lifecycle
- Découplage
- Communique des décisions de design au sujet de l'accès aux objets
- Permette de mocker facilement (testing)

Attention: encapsuler la logique de storage c'est potentiellement dangereux. En effet, les utilisateurs du repository ne savent pas ce qui se passent under the hood, et peuvent sans le savoir utiliser des query ultra gourmandes par exemple.

Quelques idées pour l'implem:

- puisque c'est découplé, on peut en profiter pour faire "du sale": de la grosse optim, etc
- laisser les transactions au client: c'est souvent dans le contexte d'utilisation qu'on sait ce qu'on veut transactionnaliser. C'est donc potentiellement plus simple de ne pas gérer les transactions dans le repository

-> Utile d'avoir un framework pour faire des repository
Pour plus de lecture là dessus, Fowler 2022

C'est super clean de déléguer la reconstitution/création de l'objet à la factory.
Genre le repository query l'objet, et c'est la factory qui crée l'objet derrière

## Chapter 7 - Using the Language: An Extended Example

Exemple de conception qui utilise tous les termes évoqués précédemment, sur un exemple de Cargo Shipping

# Part 3 - Refactoring Toward Deeper Insight

Le modèle initial est souvent initial et naïf, basé sur une connaissance partielle

Un deep model donne une expression lucide des besoins primaires des domaines experts et de leur knowledge, tout en évincant les aspects superficiels du domaine.

Dans une démarche de refactoring constant, le design lui-même doit être pensé pour le changement.

Pour trouver de bons moyens de modéliser les concepts, on va en général dépendre de notre créativité et de trial/error

## Chapter 8 - Breakthrough

Parfois on réalise qu'il faudrait faire un très gros changement dans le modèle: un breakthrough. En particulier quand on cherche à passer d'un shallow model à un deep model.

## Chapter 9 - Making Implicit Concepts Explicit

Beaucoup de transformations du code et du modèle arrivent quand un concept passe d'implicite à explicite. (ex Ovrsea: les PO)
Ceci parceque le modèle se raffine et s'approfondit avec le temps.

Comment trouver ces concepts ?
En écoutant les users et en se posant des questions:

- est-ce que ce terme revient souvent ?
- est-ce que ce terme cache quelque chose de plus compliqué ?

## Chapter 10 - Supple Design

Supple design = un design avec lequel on prend du plaisir à travailler et qui est agréable à changer.
Quelques patterns qui vont dans ce sens:

- Intention-Revealing Interfaces: nommer ses fonctions de façon ) décrire leur but et effet, sans mentionner le "comment" elles fonctionnent (tout en restant ubiquitous). Le but est que les devs n'aient pas à fouiller l'implem pour comprendre ce qu'ils utilisent
- Side-effect-free functions: C'est relou parceque souvent on veut utiliser une opération, et on se doute qu'elle a plein de side effects mais on sait pas trop lesquels. Pour contenir un peu ça, on peut (ex p.253):
  - CQS: Query = pas de side effects
  - Mettre un maximum de logique dans des opérations qui n'ont pas de side effects.
- Assertions: Quand on a beaucoup de side effects, on a pas d'autre choix que de traver les relations cause/effet pour comprendre. Pour limiter ça, on peut utiliser des invariants, des pré-conditions, post-conditions, assertions, etc. Soit via le langage s'il le permet, soit par exemple via des test unitaires
- Conceptual Contours: ???
- Standalone Classes: moins une classe est liée à d'autres classes/dépendences, moins on a de choses à comprendre pour l'utiliser. Aggregats et modules aident dans ce sens, et pour aller plus loin il faut penser low coupling

Quelques angles d'attaque:

- Subdomains: Y aller petit, commencer avec un petit morceau de domaine
- Se baser sur des formalises existants (dans la littérature, le web, etc, plein de problèmes ont déjà été résolus)

Exemple p.284

## Chapter 11 - Applying Analysis Patterns

= concepts qui représentent un problème classique en modelling. cf le bouquin Analysis Patterns de Fownler.
On peut s'en servir en DDD dans pas mal de cas.

## Chapter 12 - Relating Design Patterns to the Model

Tout ce qu'on a vu ici comme patterns c'est des Domain Patterns, pas des Design Patterns.
Les Design Patterns sont des implementations de pb classiques, et on peut piocher dedans.
Par exemple: Strategy (Policy), Composite

## Chapter 13 - Refactoring Toward Deeper Insight

Quand on refacto, il faut garder en focus:

- Vivre dans le domaine
- Regarder les choses d'un autre angle
- Dialoguer avec les experts

Process classique:

- On trouve un truc qui va pas et qu'on veut (re)modéliser
- On monte une squad express d'une poignée de personnes, avec éventuellement un domain expert, et on brainstorm 30mn-1h30
- On code, ou on laisse reposer un peu le modèle et on re-brainstorm
  Pour garder ce process productif:
- Pas besoin de bordel administratif ou de gestion de projet: on monte juste une petite squad commando
- 2-3 petites réus doivent être suffisantes. Sinon c'est qu'on over-engineer ou qu'on a mal scopé
- Ubiquitous: à pratiquer à fond

Souvent il y a de bons exemples dans le state of the art, faut pas réinventer la roue

Il ne faut pas attendre et faire du continuous refactoring, en particulier quand:

- Le design n'exprime pas la compréhension qu'on a du domaine
- Il y a des implicites à expliciter
- On veut rendre le design suppler

Parfois une crise représente une super opportunité: on nous demande une feature hyper dure à implémenter avec le modèle actuel, on se rend compte qu'il faut reprendre le modèle.
