The Pragmatic Programmer
David Thomas
Andrew Hunt

# Chapter 1 - A pragmatic philosophy

## It's your life

On est dans un métier où on a beaucoup d'agency. Il faut s'en servir plutôt que moisir:

- si un truc me déplait => essayer de le changer
- si ça veut vraiment pas => chercher ailleurs

> [!NOTE]
> Mon avis: dépend de la boite, du contexte... pas toujours si facile de changer la boite ou de changer de boite. Ce qu'il faut retenir c'est qu'il faut essayer d'agir et pas rester spectateur d'un truc qui nous déplait

## The cat ate my source code

Prendre ses responsabilités:

- si on prend ses responsabilités, les gens nous font confiance, et la team tourne bien
- ça veut pas dire que tout se passe bien quand on prend nos responsabilités, dans ces cas là ce qui compte c'est d'être honnête, assumer, et avoir des options plutôt que des excuses pourries.

> [!Tip]
> Plutôt que dire "c'est pas possible", arriver avec des options à proposer. En gros, se mettre à la place de son interlocuteur pour anticiper les idées qu'il va avoir. C'est beaucoup mieux que de débarquer avec des vieilles excuses pourries.

## Entropy

La dette technique s'accumule souvent à partir d'une broken window (le fameux théorème qui dit qu'il suffit d'une fenêtre pétée pour que le batiment soit tag de partout et squatté dans les prochains jours)

> [!NOTE]
> Software Rot plutôt que Technical Debt parcequ'on paye rarement la dette

C'est donc très important de fix les trucs crado TRÈS VITE. Ou à défaut, de les blinder de commentaires en mode "TODO: FIX THIS ASAP"

## Stone Soup and boiled frogs

Parfois on veut faire un truc, mais on sait qu'il va y avoir soit de l'opposition, soit des delais, des deadlines, etc...
Il faut trouver la carotte: dév un petit truc qui fasse rêver les stakeholders, pour qu'ils soient hypés et te laissent faire ton truc, voir se mettent à proposer des additions.
Il faut essayer d'être le catalyseur du changement.
C'est plus facile pour les gens de join le mouvement d'un truc qui qui roule.

Il faut garder en tête la big picture pour ne pas laisser les choses dégénérer lentement sans que personne s'en rende compte

## Good enough software

Il faut trouver le juste milieu dans lequel le produit satisfait tout le monde (moi y compris).
Le parallèle avec la peinture est pas mal: en ajoutant des couches et des couches, on peut ruiner une oeuvre qui était alors parfaite. Vouloir absolument aller plus loin pour sur-embellir le truc est contre productif.
Attention cependant à ne pas tomber dans l'écueil inverse ! Il ne s'agit pas de faire du code pourri. Simplement du code "satisfaisant"

## Your knowledge portfolio

Investir dans soi même c'est le meilleur bet, et autant le voir comme un vrai investissement financier:

- **Investir REGULIÈREMENT**: prendre l'habitude, même si c'est peu
- Diversifier: pour être plus changement-ready, et globalement être plus attractif
- Gérer le risque: ne pas tout miser sur des trucs high risk (genre la blockchain lol), mais y mettre le nez peut quand même être un excellent pari
- Buy low, sell high: Etre le premier sur une techno prometteuse a un payoff extraordinaire
- Review: ne pas rester stuck sur une techno qui sert plus à rien, se rendre compte quand au contraire on s'ouvre pas assez, etc

Idées de goals:

- apprendre un langage par an
- lire un livre technique par mois
- lire tout court
- prendre des cours
- participer aux meetups locaux, aux groupes...
- expérimenter dans des environnements différents (win, linux, vscode, vim...)
- faire de la veille

Mais dans tout ça, rester critique !

- 5 whys (se poser 5 fois de suite la question et y répondre pour dig)
- à qui ça profite ?
- quel est le contexte ?
- quand et où est-ce que ça peut marcher ?
- pourquoi c'est un problème ?

## Communicate

Bon les basiques hein faire attention à son audience, la forme, le fond, le timing, etc...

Petite parenthèse sur la documentation: c'est très bien de commenter son code, en particulier les fonctions importantes qui vont être utilisées par d'autres développeurs. En revanche, tout commenter par automatisme c'est une perte de temps et ça introduit potentiellement plus de trucs à mettre à jour (qui seront pas forcément mis à jour) et donc des inconsistences.

> [!TIP]
> It's both what you say and the way you say it

# Chapter 2

## The essence of good design

Une bonne mesure d'un good design est son ETC = Easier To Change.
Découpler = ETC, SRP = ETC, bon namings = ETC, etc etc.

Pour ça, il convient de se poser la question tout le temps "est-ce que ce que je viens de faire rend le code plus ETC ou moins ETC ?"

## DRY - The Evils of Duplication

DRY c'est important pour la KNOWLEDGE. L'étendre à tout c'est un erreur. Parfois on veut découpler des choses, ou bien des fonctions ont l'air rigoureusement similaires mais elles n'ont rien à voir entre elles d'un pdv logique.

Documenter comme un fou ses fonctions c'est une DRY violation: il suffit de lire le code (s'il est bien écrit), pas la peine de dupliquer la logique dans un commentaire au dessus du nom de la fonction (qui va pas être à jour dans 2 semaines)

Il faut rester DRY dans la data aussi: si on a start et end, pas besoin d'avoir length

Il est difficile de respecter le DRY quand il y a bcp d'équipes: des gens vont réimplémenter des choses sans savoir que ça existe déjà. Pour ça, il faut encourager la communication inter équipes, et développer des choses faciles à re-use.

## Orthogonality

= découplage

Bénefs:

- moins de temps pour dev
- réutilisabilité
- réduction des risques
- robustesse
- meilleurs tests
- pas couplé à un tiers

## Reversibility

Le monde du software est ultra changeant, et il faut design en conséquence. A savoir rendre le changement plus simple:

- planquer les 3rd parties sous des abstractions maison
- DRY, découplage,...

## Tracer Bullets

Quand on dev des nouveautés on est un peu à l'aveugle: est-ce que ça va marcher, est-ce que le user va capter etc.
Plutôt que de faire un giga calcul à l'avance pour prévoir/estimer/concevoir tout ça, on peut utiliser des tracer bullets.

Concrètement, plutôt que tout faire d'un coup, commencer par dev l'essentiel, s'assurer que ça "hit", puis dev la suite.
Pas en mode crado cependant, l'idée est pas de faire un dirty POC. On fait du vrai code clean, mais baby steps.
Avantages:

- Les users ont un truc rapidement
- Les fondations sont posées pour le dev
- L'intégration est prête (rajouter un truc -> directement intégré au système et testable)
- On a qq chose dont on peut faire une démo
- Meilleure sensation de progression

A partir du feedback user sur les tracer bullets, on sait si on est dans la bonne direction ou s'il faut réctifier le tir.

Différence avec un prototype/POC/MVP: on jette pas le code à la poubelle
Le tracer vise à vraiment tester le système "en conditions réelles", avec la DX derrière.

## Prototypes and Post-it Notes

Faire du prototyping est utile quand on veut tester ou apprendre sur une variété de choses:

- archi
- features
- 3rd parties
- perf
- UX

Un proto peut très bien être un dessin, des post-its, whatever

Choses qu'on peut ignorer quand on fait un proto:

- Corrrectness (fake data)
- Completeness (faut juste que le chemin "démo" fonctionne)
- Robustesse
- Style

Il faut être **très clair** sur le fait que c'est du code temporaire
Si l'idée de devoir tout refaire ne plait pas, alors les tracer bullets marcheront mieux.

## Domain Languages

pas grand chose à dire

## Estimating

Le but d'estimer est d'éviter les surprises.
Pour estimer, il faut:

- comprendre la demande
- faire un modèle mental du système
- découper ce modèle
- valuer chaque morceau
- suivre la progression et réctifier

Quand on te demande "ça va prendre combien de temps ?" la meilleure réponse est souvent "Je reviens vers toi" plutôt que de donner un truc faux à la va vite dont on va se mordre les doigts.

# Chapter 3

## The Power of Plain Text

Le plain text, c'est le meilleur moyen de garder de la knowledge. C'est encore mieux si c'est du plain text lisible (genre pas un truc encrypté bizarre)

- pas d'obsolescence
- compatible avec la plupart des outils
- facile à tester

## Shell Games

Les GUI c'est super mais c'est limitant, on peut être bcp plus productif avec son terminal.
Un vrai bg personnalise son shell:

- themes
- prompt
- aliases
- command completion

## Power editing

Important d'être fluent avec son outil principal: l'éditeur.
C'est mieux d'en utiliser un seul pour tout.
Liste de choses à savoir faire sans la souris:

- savoir bouger et sélectionner par caractère, mot, ligne, paragraphe
- bouger par delimiters, functions, modules
- réindenter
- comment/uncomment
- undo/redo
- split window + navigation entre splits
- go to line
- sort lines
- search par mot, pattern, regex
- multi cursor
- display erreurs
- lancer tests

Pour progresser là dedans il faut s'inspecter, et à chaque fois qu'on fait un truc répétitif ou painful, chercher un meilleur moyen.

Idée de challenge: Une semaine entière sans la souris

## Version Control

Evidemment c'est un must have
Permet de :

- undo/redo
- historiser
- track les changements
- identifier les releases
- paralléliser le taff

Les branches permettent de travailler en isolation

C'est également une excellente idée de VCS-iser absolument tout: config perso, scripts, etc
