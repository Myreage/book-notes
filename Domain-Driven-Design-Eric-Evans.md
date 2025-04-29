# Preface + Chapitre 1 - Crunching knowledge

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
