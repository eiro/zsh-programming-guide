Le guide s'adresse à des programmeurs (même occasionels) qui sont
déjà à l'aise avec un langages interprété. nous utiliserons librement
des exemples et des concepts de ces langages pour faciliter l'apprentissage.

Malgré des décenies de critiques incessantes à propos du shell scripting,
force est d'avouer que la succession peine à venir et que nombre de
praticiens experimentés continuent à déverser quotidiennement dans nos
systèmes unix de ces lignes qui semblent heurter les esthètes de la programmation.

Pourtant qu'on se le dise: les langages de programmations émergents
ont bien des choses en commun avec le shell (les channels, les
generateurs, les applications partielles, la programmation higher-order
sont des concepts qui s'imposent et dont le shell dispose sous des noms
plus baroques comme l'expansion et les pipes).

Je pratique le shell depuis que j'ai découvert linux en 1996 et j'ai
constaté que si beaucoup de critiques étaient fondées (et que je décris en
fin de livre en proposant de possibles stratégies), la mauvaise
réputation de ce mauvais garçon du monde unix se nourrissait avant tout
d'ignorance et de religiosité [1].

La religion s'appelle compatibilité POSIX: en vous faisant mirroiter une
place au paradis de la portabilité et en targant qu'elle est la
seule voie possible, elle occulte l'immense liberté que vous propose les
hérétiques et il en est un qui mérite le bucher plus que tout autre:
zsh.

zsh s'inspire librement de tout l'héritage paien des shells unix. On y retrouve
donc de très bonnes idées de shells oubliés parfois injustement par
les linuxiens(ksh[2], rc[3] et tcsh[4]). il se libère la doxa posixenne pour
permettre de proposer des comportements et des fonctionalités qui seraient ceux
attendus par des amateurs langages interprétés traditionnels.

A l'occasion de l'encadrement de travaux pratiques ou la religion
POSIX était de mise, j'ai pris conscience du gouffre fonctionnel
qui existait maintenant entre les shells traditionels et zsh et du confort
que ce dernier apporte. A vrai dire, je rejoins maintenant la position de
nombreuses personnes sur le sujet à un mot prêt: le shell POSIX c'est illisible!

Il faut présenter zsh non plus comme un shell mais comme un langage interprété
dont la philosophie et la syntaxe héritent directement des shell unix. C'est ce
que ce guide se propose de faire: montrer que des différentes parfois
imperceptibles en première lecture donne toute sa puissance à zsh et dire les choses
telles qu'elles sont et nous permettre au final de remplacer ces lignes un peu génantes
que nous avons écrit dans les langages interprétés par méconnaissance d'un outils adapté.

[1] Amis de linuxfr.org et des vendredis productifs: pour mettre fin de suite à toute polémique:
non, je ne crois pas que l'un engendre directement l'autre.
[2] ksh est le shell par défaut sous openbsd
[3] rc est le shell par defaut de plan9 (révolution tombée dans l'oubli pour avoir été trop longtemps propriétaire)
    (TODO: retrouver la quote de ERS dans ARTU). il partage des éléments de syntaxe avec l'outils de construction mk.
    ces deux outils sont disponibles dans la 9base, collection d'outils plan9 portés sous linux et disponibles en paquets
    debian.
[4] tcsh avait beaucoup de défauts et je crois que personne ne le regrettera. il apportait pourtant de bonnes idées
    dont zsh s'inspire librement.

Lorsque les concepts sont réutilisables sans bricolage dans d'autres shells, je le mentionnerais. Ainsi seront
traités de temps à autres:

* [ksh](https://en.wikipedia.org/wiki/Korn_shell) et l'implémentation qui fait
  référence à mes yeux ([mksh](https://www.mirbsd.org/mksh.htm)).
  ksh est présent sur de nombreux unices et est un tres bon choix quand chaque
  Kbyte compte.

* [standard POSIX actuel](http://pubs.opengroup.org/onlinepubs/9699919799/idx/shell.html)

* [rc](?), disponible sous linux via la [9base](.)

Un mot sur bash: son avantage est d'être le shell standard du GNU. Il est fourni
par défaut dans la plupart des distributions linux et je ne peux donc l'ignorer.
Il y est considéré dans le présent document comme une implementation bloated de ksh:
ce qui est valable en ksh l'est aussi en bash ... en plus rapide et moins gourmand.
