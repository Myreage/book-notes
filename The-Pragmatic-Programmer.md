The Pragmatic Programmer
David Thomas
Andrew Hunt

# Chapter 1 - A pragmatic philosophy

## It's your life

On est dans un métier où on a beaucoup d'agency. Il faut s'en servir plutôt que moisir:

- si un truc me déplait => essayer de le changer
- si ça veut vraiment pas => chercher ailleurs

## The cat ate my source code

Prendre ses responsabilités:

- si on prend ses responsabilités, les gens nous font confiance, et la team tourne bien
- ça veut pas dire que tout se passe bien quand on prend nos responsabilités

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

## Good enough software

Il faut trouver le juste milieu dans lequel le produit satisfait tout le monde (moi y compris).
Le parallèle avec la peinture est pas mal: en ajoutant des couches et des couches, on peut ruiner une oeuvre qui était alors parfaite. Vouloir absolument aller plus loin pour sur-embellir le truc est contre productif.
Attention cependant à ne pas tomber dans l'écueil inverse ! Il ne s'agit pas de faire du code pourri. Simplement du code "satisfaisant"

## Your knowledge portfolio

Investir dans soi même c'est le meilleur bet, et autant le voir comme un vrai investissement financier:

- **Investir REGULIÈREMENT**: prendre l'habitude, même si c'est peu Diversifier: pour être plus changement-ready, et globalement être plus attractif
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
