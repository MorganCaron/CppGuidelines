# C++ Guidelines

## Introduction

Ce document comprend une coding style et une liste de guidelines pour des projets en C++.

<details><summary>A qui s'adresse ce document ?</summary><p>

Ce document s'adresse à toute personne souhaitant contribuer sur un projet sur lequel il est indiqué d'appliquer cette coding style.
Cela requiert de bonnes compétences en C++ moderne.
Des liens vers des ressources (documentations, tutoriels, vidéos) seront fournis pour combler d'éventuelles lacunes si besoin.

---
</p></details>

<details><summary>Pourquoi une coding style ?</summary><p>

Le choix d'une coding style n'est pas arbitraire, chaque choix fait dans ce document a été réfléchis, pas seulement pour ses avantages en terme de lisibilité mais aussi pour réduire les risques d'erreurs, les ambiguïtés, la redondance, les comportements indéfinis du compilateur ([CppReference: Undefined Behavior]), problèmes d'optimisation, etc.
Chacune de ces raisons est soigneusement expliqué pour pouvoir être remis en question à chaque évolution du langage. Ce document n'est pas figé, il est ouvert aux débats et est voué à changer pour s'adapter aux nouvelles fonctionnalités du C++.

---
</p></details>

<details><summary>Pourquoi modifier la coding style avec le temps ?</summary><p>

Le métier de développeur est un métier dont la formation ne s'arrête jamais.
Il faut se tenir au courant des nouveaux progrès dans ce domaine pour pouvoir fournir du travail de meilleur qualité sans rester attaché à des notions devenues obsolètes.

La coding style d'un projet doit s'adapter aux évolutions du langage.
Mais on peut aussi penser à de nouveaux choix de norme dont on avait pas pensé initialement, ou simplement vouloir améliorer l'existant.

Les anciens codes conçus avec des fonctions obsolètes seront menés à être rénovées progressivement par les développeurs qui tomberont dessus (pas de refonte totale nécessaire).
Ainsi les programmeurs s'assureront de bien tester les fonctions qu'ils recodent pour s'assurer de l'absence de régression de code (avec des tests unitaires et des tests fonctionnels).

---
</p></details>

## Philosophie

<details><summary>Clean Code</summary><p>

Le Clean Code n'est pas un ensemble de règles strictes mais désigne plutôt une série de principes pour produire un code compréhensible et facile à modifier.
Compréhensible signifie dans ce cas un code immédiatement intelligible par n'importe quel développeur qualifié.
Un code est facile à modifier lorsqu'il peut être facilement ajusté et complété.
Un code facilement modifiable comporte les attributs suivants:
- Les classes et les méthodes sont **petites** et, dans la mesure du possible, ont une seule et unique tâche.
- Les classes et les méthodes sont **prévisibles**, fonctionnent de la façon attendue.

---
</p></details>

<details><summary>Principe KISS</summary><p>

KISS ([Wikipedia: KISS]) ("**K**eep **i**t **s**imple, **s**tupid", en français: "garde ça simple, idiot") est l’un des plus anciens principes du Clean Code.
KISS rappelle aux programmeurs de construire leur code de façon aussi simple que possible.
Toute complexité inutile doit être évitée.
En programmation, il n’y a jamais une seule façon pour résoudre un problème. Une algorithme peut toujours être exprimé de différentes manières. Par conséquent, les programmeurs observant le principe KISS doivent constamment se demander s’ils ne peuvent pas résoudre un problème plus facilement.

> Ce principe est lié au concept du Rasoir d'Ockham ([Wikipedia: Rasoir d'Ockham]) en raisonnement, qui consiste à préférer les explications les plus simples, car elles sont généralement plus crédibles que les explications complexes.

---
</p></details>

<details><summary>Principe DRY</summary><p>

Le principe DRY (**D**on't **r**epeat **y**ourself) est en quelque sorte la concrétisation du principe KISS. Un Clean Code respectant ce principe implique que chaque fonctionnalité doit avoir une seule et unique représentation au sein du système global.
Il consiste à écrire des fonctions et des classes réutilisables, aussi simples que possible et traitant un minimum de tâches à la fois.
Ce principe encourage à décomposer un programme en de nombreuses classes et fonctions pour garder chaque partie propre sans avoir de répétitions de code.
Un code dans lequel ont copie-colle plusieurs lignes pour gérer des cas supplémentaire est un bon exemple de code qui ne respecte pas le principe DRY.
Le contraire de DRY est WET (**W**e **e**njoy **t**yping). On appelle WET un code comportant des répétitions inutiles.

---
</p></details>

<details><summary>La règle du Scout</summary><p>

[The Boy Scout Rule]

> Un Scout a une règle: "Toujours laisser un endroit dans un état meilleur que celui dans lequel vous l'avez trouvé".

Appliqué au domaine de la programmation, ce principe consiste à nettoyer continuellement chaque petit morceau de dette technique lorsqu'un développeur en a l'occasion.

Cette habitude simple permet à un projet de voir sa qualité augmenter rapidement avec le temps sans avoir à planifier de refactorisation ou de refonte du projet.

Etant donné que ça se fait sur de petites parties à chaque fois, le développeur fait le choix de ne nettoyer que ce qui ne lui fait pas perdre de temps en plus de ces objectifs initiaux.

Il peut se permettre de prendre le temps de nettoyer de grosses parties du code si ça simplifie significativement la réalisation de sa tâche initiale.

Un code obsolète qui fonctionne n'est pas une bonne base sur laquelle se reposer pour bâtir la suite d'un projet.
C'est pourquoi ce petit investissement de temps peut sur le long terme corriger d'importants problèmes de dette technique et ainsi éviter des bugs ou des complications dans la réalisation de futures tâches.

---
</p></details>

## Coding Style

### Indentation

<details><summary>Caractère d'indentation: <code>tabulation</code></summary><p>

En indentant avec le caractère ``espace``, il est souvent préférable de cumuler plusieurs espaces par indentation pour qu'elles soient bien visibles (exemple: 2 espaces ou 4 espaces à la fois). Mais cette écriture rend possible les demi-indentations (avec 1 ou 3 espaces).

Le choix d'espaces plutôt que de tabulation servait à s'assurer que le code ne dépassait pas 80 colonnes pour tenir sur les petits écrans de l'époque. Cette raison n'est plus valable aujourd'hui.

Les tabulations sont plus simples à utiliser: un seul caractère par indentation.
Et chaque développeur peut choisir la taille de l'indentation sur son IDE sans impacter le projet ou l'environnement d'un autre.

---
</p></details>

<details><summary>Indentation des instructions préprocesseur après le caractère '#'</summary><p>

Indentation avant le caractère '#':
```cpp
#if defined(OS_WINDOWS)
	#include <Windows.h>
	#if defined(CPP_20)
		#define ENABLE_CONCEPTS
	#endif
#endif
```

Indentation après le caractère '#':
```cpp
#if defined(OS_WINDOWS)
#	include <Windows.h>
#	if defined(CPP_20)
#		define ENABLE_CONCEPTS
#	endif
#endif
```

|   | Indentation avant le caractère '#' | Indentation après le caractère '#' |
| -:|:-:|:-:|
| La portion d'instructions préprocesseur est plus facile à différencer des autres instructions | ❌ | ✅ |
| Nom de l'instruction préprocesseur plus lisible | ❌ | ✅ |

**=> Indentation après le caractère '#'**

---
</p></details>

<details><summary>Indentation distinctes entre les instructions C++ et les instructions préprocesseur</summary><p>

A - Indentation des instructions préprocesseur dans les scopes C++ (et pas l'inverse):
```cpp
#if defined(OS_WINDOWS)
auto functionImplementationSpecific(int number) -> int
{
	if (number >= 0)
	{
#		if defined(ARCH_64BITS)
		return 64;
#		else
		return 32;
#		endif
	}
	return 0;
}
#endif
```

B - Indentation des instructions C++ dans les scopes préprocesseur (et pas l'inverse):
```cpp
#if defined(OS_WINDOWS)
	auto functionImplementationSpecific(int number) -> int
	{
		if (number >= 0)
		{
#	if defined(ARCH_64BITS)
				return 64;
#	else
				return 32;
#	endif
		}
		return 0;
	}
#endif
```

C - Indentation commune entre les instructions C++ et les instructions préprocesseur:
```cpp
#if defined(OS_WINDOWS)
	auto functionImplementationSpecific(int number) -> int
	{
		if (number >= 0)
		{
#			if defined(ARCH_64BITS)
				return 64;
#			else
				return 32;
#			endif
		}
		return 0;
	}
#endif
```

D - Indentation distinctes entre les instructions C++ et les instructions préprocesseur:
```cpp
#if defined(OS_WINDOWS)
auto functionImplementationSpecific(int number) -> int
{
	if (number >= 0)
	{
#	if defined(ARCH_64BITS)
		return 64;
#	else
		return 32;
#	endif
	}
	return 0;
}
#endif
```

Argument en faveur des choix qui n'indentent pas les instructions C++ dans les scopes préprocesseur (A et D):
1. Une fois les instructions préprocesseur traitées par le compilateur, il ne reste plus que les instructions C++.
Le développeur écrit son code en visualisant ce qu'il deviendra à cette étape de la compilation.
Il n'y a donc pas de raison que les instructions C++ conservent leur indentation causé par les scopes préprocesseur à cette étape de compilation (Ca n'a aucune importance pour la compilation, mais a un impact uniquement dans la façon de se projeter à cette étape de la compilation lorsqu'on lit le code).

|   | A | B | C | D |
| -:|:-:|:-:|:-:|:-:|
| Semble bien indenté au premier coup d'oeil | ❌ | ❌ | ✅ | ✅ |
| Facile à indenter | ❌ | ❌ | ✅ | ✅ |
| Argument 1. | ✅ | ❌ | ❌ | ✅ |

**=> D - Indentation distinctes entre les instructions C++ et les instructions préprocesseur**

---
</p></details>

<details><summary>Pas d'indentation des instructions case et default dans les instructions switch</summary><p>

A - Pas d'indentation des instructions ``case``, ``default`` et ``{}``:
```cpp
switch (number)
{
case 0:
	break;
case 1:
{
	break;
}
default:
	break;
}
```

B - Pas d'indentation des instructions ``case`` et ``default``:
```cpp
switch (number)
{
case 0:
	break;
case 1:
	{
		break;
	}
default:
	break;
}
```

C - Pas d'indentation des accolades:
```cpp
switch (number)
{
	case 0:
		break;
	case 1:
	{
		break;
	}
	default:
		break;
}
```

D - Indentation de toute instruction:
```cpp
switch (number)
{
	case 0:
		break;
	case 1:
		{
			break;
		}
	default:
		break;
}
```

E - Indentation des instructions ``case`` et ``default`` seulement:
```cpp
switch (number)
{
	case 0:
	break;
	case 1:
	{
		break;
	}
	default:
	break;
}
```

> Les accolades sont nécessaires dans un ``case`` lorsqu'elles contiennent une déclaration de variable.

Argument en défaveur du choix A qui n'indente ni les instructions ``case``/``default`` ni les accolades:
- Les accolades des ``case`` sont alignés horizontalement avec les accolades du ``switch``.
Ce n'est pas clair pour savoir si l'accolade du switch est bien fermée.

Les choix C et D semblent aussi bien l'un que l'autre. Le choix B reste néanmoins meilleur car il propose une écriture concise et uniforme avec l'indentation des mots clef ``public:``, ``protected:`` et ``private:`` des struct/class.

Le choix E ne permet pas de voir clairement quelles instructions sont dans chaque ``case``.

**=> B - Pas d'indentation des instructions ``case`` et ``default``**

---
</p></details>

### Nommage

<details><summary>Variables, fonctions et méthodes: lowerCamelCase</summary><p>

---
</p></details>

<details><summary>Attributs privés: lowerCamelCase précédés par "m_"</summary><p>

Les attributs privés d'une classe/structure sont écrits en lowerCamelCase ([Wikipedia: lowerCamelCase]), mais également précédés par "m_" pour les différencier des variables avec un scope local ou global.
Ce préfixe permet d'informer de la portée de la variable, signifiant qu'elle est accessible depuis les méthodes de l'objet uniquement.

```cpp
class Personnage
{
public:
	Personnage(std::string name):
		m_name{std::move(name)}
	{}

	[[nodiscard]] constexpr auto getName() const noexcept -> std::string_view
	{
		return m_name;
	}

private:
	std::string m_name;
};
```

Dans le cas d'une classe/structure avec des attributs publics, il est préférable de garder des noms d'attributs sans préfixe.
Mais si cet objet a un constructeur, on peut se retrouver dans le cas où les paramètres du constructeur ont le même nom que les attributs, causant une ambiguïté pour le compilateur.

```cpp
struct Personnage
{
	Personnage(std::string name):
		name{std::move(name)}
	{}

	std::string name;
};
```

Les compilateurs savent lever ce genre d'ambiguïté, mais par soucis de lisibilité il est préférable de donner des noms différents aux paramètres.
Le préfixe ``p_`` (p comme "parameter") peut servir à différencier ces variables des attributs publics.

```cpp
struct Personnage
{
	Personnage(std::string c_name):
		name{std::move(c_name)}
	{}

	std::string name;
};
```

---
</p></details>

<details><summary>Dossiers, fichiers, namespaces, classes et variables globales: UpperCamelCase</summary><p>

---
</p></details>

<details><summary>Macros préprocesseur: SCREAMING_SNAKE_CASE</summary><p>

---
</p></details>

<details><summary>Pas de nom de type dans les noms de variable</summary><p>

Le nom d'une variable ne doit pas annoncer explicitement son type (sauf pour les types user-defined).
Celui-ci étant déjà renseigné et facilement déductible si le nom est bien choisi.
- On devinera qu'une variable "name" est de type ``std::string`` (ou ``std::string_view`` s'il est clair que la variable ne possède pas la donnée).
- On devinera également qu'un "id" est un ``unsigned int``.
De plus, la plupart des IDE permettent de connaitre le type d'une variable en la survolant avec la souris. Et lorsque ce n'est pas le cas, sa définition reste facilement accessible.

---
</p></details>

<details><summary>Pas de noms arbitraires dénués de sens</summary><p>

Les variables ne doivent pas porter de nom arbitraire dénué de sens (a, b, c, tmp, toto, foo, bar, etc...).
Le nom de la variable doit être assez explicites pour renseigner sur la nature de son contenu.
Et les mots ne doivent pas être interprétés différemment de leur sens réel dans le cadre d'un projet particulier.

---
</p></details>

<details><summary>Pas acronymes ni de contractions de mots (sauf rares exceptions)</summary><p>

Les acronymes et contractions de mots sont proscrits, sauf exceptions assez claires pour ne pas porter à confusion (Id, Json, AST, i18n, etc...).

Décoder les acronymes et les contractions de mots lors de la relecture de code demande une charge mentale supplémentaire pour comprendre ce que le code fait.
De plus, certains acronymes peuvent donner plusieurs mots différents selon le contexte et l'interprétation des développeurs.

❌:
```cpp
using Id = std::uint64_t;

struct DelUserCmd final
{
	Id userId;
};
```

✅:
```cpp
using Id = std::uint64_t;

namespace User
{
	struct DeleteCommand final
	{
		Id userId;
	};
}
```

---
</p></details>

### Préprocesseur

<details><summary>Header-guard: <code>#pragma once</code></summary><p>

Les header-guards ([Wikipedia: Include guard]) protègent les headers contre les multiples importations.
Tous les fichiers headers doivent avoir des headers guards.

Historiquement, les header-guards ont toujours été faits avec des ``#ifndef``:
```cpp
#ifndef PROJECT_PATH_FILE_H_
#	define PROJECT_PATH_FILE_H_

// ...

#endif /* !PROJECT_PATH_FILE_H_ */
```

Pour garantir l'unicité des header-guards, chaque header doit utiliser un nom de macro unique. Afin d'éviter que deux fichiers utilisent le même nom de macro, celui-ci doit contenir le nom du projet ainsi que le chemin complet du fichier.

Les compilateurs C/C++ fournissent ``#pragma once`` qui permet de s'assurer que le fichier n'est importé qu'une fois dans le projet, sans avoir à renseigner un nom unique.
```cpp
#pragma once

// ...
```

L'intérêt de ``#pragma once`` (comme remplacement au header-guard ``#ifndef``) était d'accélérer la compilation, car celui-ci taggait le fichier comme étant déjà inclut (alors que pour les ``#ifndef`` il fallait reparser le fichier pour tester l'existence de la macro).
Aujourd'hui les compilateurs modernes (Clang, GCC et MSVC) reconnaissent les header-guards ``#ifndef`` et les traitent comme des ``#pragma once``:

GCC: [GCC Header-guard](https://gcc.gnu.org/onlinedocs/cppinternals/Guard-Macros.html)
> to prevent the compiler from processing them more than once. The preprocessor notices such header files, so that if the header file appears in a subsequent #include directive and FOO is defined, then it is ignored and it doesn’t preprocess or even re-open the file a second time. This is referred to as the multiple include optimization.

MSVC: [MSVC Header-guard](https://docs.microsoft.com/en-us/cpp/preprocessor/once?view=msvc-170)
> There's no advantage to use of both the include guard idiom and #pragma once in the same file. The compiler recognizes the include guard idiom, and implements the multiple-include optimization the same way as the #pragma once directive if no non-comment code or preprocessor directive comes before or after the standard form of the idiom

``#pragma once`` n'est pas standard mais est supporté par la grande majorité des compilateurs modernes C/C++ ([Wikipedia: Pragma once : Portability]).

---
</p></details>

<details><summary>Utiliser le moins de macros préprocesseur possible</summary><p>

Les macros ``#define`` apportent un moyen simple de faire de la métaprogrammation et des constantes en C++.
Mais au fil des évolutions du langage, leur utilité est de moins en moins pertinente.

Le problème des macros préprocesseur est leur exécution sans aucune vérification sur le typage et le non-respect des namespaces (une macro préprocesseur est globale).
De plus, les macros permettent d'insérer des portions de code sans vérifier si l'insertion est syntaxiquement correcte, laissant une autre étape de la compilation se charger de cette vérification.

Les macros préprocesseur s'exécutent bêtement (un simple copier-coller), sans vérifier si le code généré est correct ou bien formatté.
En cas d'erreur, les messages d'erreur ne sont pas très pertinents car le compilateur évalue un code déjà transformé par le préprocesseur. Il n'indiquera pas précisément d'où vient le problème.

En C++ moderne il existe des alternatives aux macros préprocesseur pour beaucoup d'usages qu'on peut en faire, les rendant ainsi obsolètes dans beaucoup de situations.
Parmis ces alternatives, les templates ainsi que les fonctions et variables ``inline``/``constexpr`` sont de bons candidats pour remplacer la plupart des ``#define``.

> ``constexpr`` implique ``inline``. Le compilateur est libre d'inliner ou non les élements ``inline``

Constante générique compile-time avec ``#define``:
```cpp
#include <iostream>

#define PI 3.14159265358979323846

auto main() -> int
{
    std::cout << PI << std::endl;
}
```
Constante générique compile-time avec ``template`` et ``constexpr``:
```cpp
#include <concepts>
#include <iostream>

template<std::floating_point T>
constexpr T pi = T{3.14159265358979323846};

auto main() -> int
{
    std::cout
		<< pi<float> << '\n'
		<< pi<double> << std::endl;
}
```
Le compilateur est libre d'inliner les variables ``constexpr`` et d'omettre leur initialisation.
Cette variable est aussi typée, ce qui en fait une alternative meilleure que les constantes déclarées avec ``#define``.

Fonction générique compile-time avec ``#define``:
```cpp
#include <iostream>

#define ADD(lhs, rhs) lhs + rhs

auto main() -> int
{
	using namespace std::literals;
    std::cout
		<< ADD(1, 2) << '\n'
		<< ADD("Hello"s, " World!") << std::endl;
}
```

Fonction générique compile-time avec ``template`` et ``constexpr``:
```cpp
#include <iostream>

[[nodiscard]] constexpr auto add(auto lhs, auto rhs) noexcept -> decltype(lhs + rhs)
{
    return lhs + rhs;
}

auto main() -> int
{
	using namespace std::literals;
    std::cout
		<< add(1, 2) << '\n'
		<< add("Hello"s, " World!") << std::endl;
}
```
Cette fonction est typée et ne compile pas pour des types n'ayant pas d'implémentation de l'``operator+`` entre eux.
> (les paramètres ``lhs`` et ``rhs`` de type ``auto`` sont convertis en ``template`` par le compilateur)

Dans certains cas, les macros préprocesseur restent la seule façon de faire.
C'est pourquoi il faut limiter leur usage à ces cas où il n'existe pas encore de meilleure alternative.

---
</p></details>


### Commentaires

<details><summary>Pas de commentaires décoratifs</summary><p>

Les commentaires se font de la manière la plus simple:
```cpp
// Commentaire d'une ligne

/* Commentaire
de plusieurs
lignes */
```

Pas de commentaires formatés de manière à être agréable visuellement:
```cpp
////////////////////////////////////////////////
// Commentaire avec des caractères décoratifs //
////////////////////////////////////////////////

// #############################################

/*
 * Caractères '*'
 * en début
 * de chaque ligne
 */
```

Les caractères supplémentaires de la 2ème écriture ne sont utilisés qu'à titre décoratif.
Ca prend du temps à écrire, surtout si on veut respecter une uniformisation et l'alignement de tous les commentaires d'un fichier.

---
</p></details>

### Espaces

<details><summary>Espaces autour des opérateurs</summary><p>

---
</p></details>

<details><summary>Pas d'espaces autour des parenthèses</summary><p>

---
</p></details>

<details><summary>Espace après les virgules</summary><p>

---
</p></details>

<details><summary>Pas d'espaces pour aligner des éléments</summary><p>

---
</p></details>

### Scopes

<details><summary>Ouverture des accolades sur une nouvelle ligne</summary><p>

Ouverture d'accolades en fin de ligne:
```cpp
auto main() -> int {
    std::cout << "Hello World!" << std::endl;
}
```

Ouverture d'accolades sur une nouvelle ligne:
```cpp
auto main() -> int
{
    std::cout << "Hello World!" << std::endl;
}
```

|   | En fin de ligne | Sur une nouvelle ligne |
| -:|:-:|:-:|
| Facilité à remarquer l'ouverture d'une accolade<br>(exemple: pour une fonction dont la signature est longue) | ❌ | ✅ |
| Facilité à distinguer l'ouverture d'accolade correspondant à une fermeture (ou l'inverse) | ❌ | ✅ |
| Norme majoritaire dans les projets C++ | ❌ | ✅ |

---
</p></details>

<details><summary>Pas d'accolades pour une seule instruction</summary><p>

Mettre des accolades même s'il n'y a qu'une instruction à l'intérieur:
```cpp
if (printLogs)
{
	std::cout << "Info" << std::endl;
}
```

Ne pas mettre d'accolades lorsqu'elles contiennent qu'une instruction:
```cpp
if (printLogs)
	std::cout << "Info" << std::endl;
```

|   | Accolades pour une instruction | Pas d'accolades pour une instruction |
| -:|:-:|:-:|
| Economise des lignes | ❌ | ✅ |
| Lisibilité | ✅ (mais superflu)<sup>1</sup> | ❌ |

1. L'indentation sert à distinguer visuellement un scope d'un autre même en l'absence d'accolades.<br>
Pas besoin d'accolades pour expliciter une seconde fois qu'on est dans un nouveau scope (information superflue).

**=> Ne pas mettre d'accolades lorsqu'elles contiennent qu'une instruction**

---
</p></details>

### Types

<details><summary>Initialisation d'objets avec {}</summary><p>


---
</p></details>

<details><summary>Almost Always Auto</summary><p>


---
</p></details>

<details><summary>Typage en fin de signature</summary><p>


---
</p></details>

<details><summary>Pas de raw-pointer</summary><p>


---
</p></details>

[CppReference: Undefined Behavior]: https://en.cppreference.com/w/cpp/language/ub
[Wikipedia: KISS]: https://fr.wikipedia.org/wiki/Principe_KISS
[Wikipedia: Rasoir d'Ockham]: https://fr.wikipedia.org/wiki/Rasoir_d'Ockham
[The Boy Scout Rule]: https://www.stepsize.com/blog/how-to-be-an-effective-boy-girl-scout-engineer
[Wikipedia: lowerCamelCase]: https://fr.wikipedia.org/wiki/Camel_case
[Wikipedia: UpperCamelCase]: https://fr.wikipedia.org/wiki/Camel_case
[Wikipedia: snake_case]: https://fr.wikipedia.org/wiki/Snake_case
[Wikipedia: Include guard]: https://en.wikipedia.org/wiki/Include_guard
[Wikipedia: Pragma once : Portability]: https://en.wikipedia.org/wiki/Pragma_once#Portability

