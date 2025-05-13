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
