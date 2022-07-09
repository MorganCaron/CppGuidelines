# Cpp Guidelines

## Introduction

Ce document comprend une coding style et une compilation de guidelines pour des projets en C++.

### A qui s'adresse ce document ?
Ce document s'adresse à toute personne souhaitant contribuer sur un projet pour lequel il est indiqué de respecter cette coding style.
Cela requiert de bonnes compétences en C++ moderne.
Des liens vers des ressources (documentations, tutoriels, vidéos) seront fournis pour combler d'éventuelles lacunes si besoin.

### Pourquoi une coding style ?
Le choix d'une coding style n'est pas arbitraire, chaque choix fait dans ce document a été réfléchis, pas seulement pour ses avantages en terme de lisibilité mais aussi pour réduire les risques d'erreurs, les ambiguïtés, les comportements indéfinis du compilateur ([CppReference: Undefined Behavior]), problèmes d'optimisation, etc.
Chacune de ces raisons est soigneusement expliqué pour pouvoir être remis en question à chaque évolution du langage. Ce document n'est pas figé, il est ouvert aux débats et est voué à changer pour s'adapter aux nouvelles fonctionnalités du C++.

### Pourquoi modifier la coding style avec le temps ?
Le métier de développeur est un métier dont la formation ne s'arrête jamais.
Il faut se tenir au courant des nouveaux progrès dans nos domaines pour pouvoir fournir du travail de meilleur qualité sans rester attaché à des notions devenues obsolètes.

Les anciens codes conçus avec des fonctions obsolètes seront menés à être rénovées progressivement par les développeurs qui tomberont dessus (pas de refonte totale nécessaire).
Ainsi les programmeurs s'assureront de bien tester les fonctions qu'ils recodent pour s'assurer de l'absence de régression de code (avec des tests unitaires et des tests fonctionnels).

## Philosophie

### Clean Code
Le Clean Code n'est pas un ensemble de règles strictes mais désigne plutôt une série de principes pour produire un code compréhensible et facile à modifier.
Compréhensible signifie dans ce cas un code immédiatement intelligible par n'importe quel développeur qualifié.
Un code est facile à modifier lorsqu'il peut être facilement ajusté et complété.
Un code facilement modifiable comporte les attributs suivants:
- Les classes et les méthodes sont **petites** et, dans la mesure du possible, ont une seule et unique tâche.
- Les classes et les méthodes sont **prévisibles**, fonctionnent de la façon attendue.

### Principe KISS
KISS ([Wikipedia: KISS]) ("**K**eep **i**t **s**imple, **s**tupid", en français: "garde ça simple, idiot") est l’un des plus anciens principes du Clean Code.
KISS rappelle aux programmeurs de construire leur code de façon aussi simple que possible.
Toute complexité inutile doit être évitée.
En programmation, il n’y a jamais une seule façon pour résoudre un problème. Une algorithme peut toujours être exprimé de différentes manières. Par conséquent, les programmeurs observant le principe KISS doivent constamment se demander s’ils ne peuvent pas résoudre un problème plus facilement.

> Ce principe est lié au concept du Rasoir d'Ockham ([Wikipedia: Rasoir d'Ockham]) en raisonnement, qui consiste à préférer les explications les plus simples, car elles sont généralement plus crédibles que les explications complexes.

### Principe DRY
Le principe DRY (**D**on't **r**epeat **y**ourself) est en quelque sorte la concrétisation du principe KISS. Un Clean Code respectant ce principe implique que chaque fonctionnalité doit avoir une seule et unique représentation au sein du système global.
Il consiste à écrire des fonctions et des classes réutilisables, aussi simples que possible et traitant un minimum de tâches à la fois.
Ce principe encourage à décomposer un programme en de nombreuses classes et fonctions pour garder chaque partie propre sans avoir de répétitions de code.
Un code dans lequel ont copie-colle plusieurs lignes pour gérer des cas supplémentaire est un bon exemple de code qui ne respecte pas le principe DRY.
Le contraire de DRY est WET (**W**e **e**njoy **t**yping). On appelle WET un code comportant des répétitions inutiles.

### La règle du Scout
[The Boy Scout Rule]

> Un Scout a une règle: "Toujours laisser un endroit dans un état meilleur que celui dans lequel vous l'avez trouvé".

Appliqué au domaine de la programmation, ce principe consiste à nettoyer continuellement chaque petit morceau de dette technique lorsqu'un développeur en a l'occasion.

Cette habitude simple permet à un projet de voir sa qualité augmenter rapidement avec le temps sans avoir à planifier de refactorisation ou de refonte du projet.

Etant donné que ça se fait sur de petites parties à chaque fois, le développeur fait le choix de ne nettoyer que ce qui ne lui fait pas perdre de temps en plus de ces objectifs initiaux.

Il peut se permettre de prendre le temps de nettoyer de grosses parties du code si ça simplifie significativement la réalisation de sa tâche initiale.

Un code obsolète qui fonctionne n'est pas une bonne base sur laquelle se reposer pour bâtir la suite d'un projet.
C'est pourquoi ce petit investissement de temps peut sur le long terme corriger d'importants problèmes de dette technique et ainsi éviter des bugs ou des complications dans la réalisation de futures tâches.

## Coding Style

### Choix du caractère d'indentation

L'indentation doit faire plusieurs caractères de large pour être clairement lisible:
<center>4 espaces ou 1 tabulation faisant la même largeur</center>

Indenter avec 1 tabulations:
```cpp
auto main() -> void
{
	std::cout << "Hello World!" << std::endl;
}
```

Indenter avec 4 espaces:
```cpp
auto main() -> void
{
    std::cout << "Hello World!" << std::endl;
}
```

|   | 1 tabulations | 4 espaces |
| -:|:-----------:|:-------:|
| Pas de demi-indentation possible | ✅ | ❌ |
| Economie de caractères | ✅ | ❌ |

**<center>=> Indenter avec 1 tabulation</center>**

---

### Indentation des instructions préprocesseur

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

**<center>=> Indentation après le caractère '#'</center>**

---

### Assemblage des indentations d'instructions C++ et d'instructions préprocesseur


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

**<center>=> D - Indentation distinctes entre les instructions C++ et les instructions préprocesseur</center>**

---

### Placement des accolades

Ouverture d'accolades en fin de ligne:
```cpp
auto main() -> void {
    std::cout << "Hello World!" << std::endl;
}
```

Ouverture d'accolades sur une nouvelle ligne:
```cpp
auto main() -> void
{
    std::cout << "Hello World!" << std::endl;
}
```

|   | En fin de ligne | Sur une nouvelle ligne |
| -:|:-:|:-:|
| Facilité à remarquer l'ouverture d'une accolade<br>(exemple: pour une fonction dont la signature est longue) | ❌ | ✅ |
| Facilité à distinguer l'ouverture d'accolade correspondant à une fermeture (ou l'inverse) | ❌ | ✅ |
| Norme majoritaire dans les projets C++ | ❌ | ✅ |

**<center>=> Ouverture d'accolades sur une nouvelle ligne</center>**

---

### Présence d'accolades pour une seule instruction

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
| -:|:-----------:|:-------:|
| Economise des lignes | ❌ | ✅ |
| Lisibilité | ✅ (mais superflu)<sup>1</sup> | ❌ |

1. L'indentation sert à distinguer visuellement un scope d'un autre même en l'absence d'accolades.<br>
Pas besoin d'accolades pour expliciter une seconde fois qu'on est dans un nouveau scope (information superflue).

**<center>=> Ne pas mettre d'accolades lorsqu'elles contiennent qu'une instruction</center>**

---
# CppGuidelines
C++ Guidelines

[CppReference: Undefined Behavior]: https://en.cppreference.com/w/cpp/language/ub
[Wikipedia: KISS]: https://fr.wikipedia.org/wiki/Principe_KISS
[Wikipedia: Rasoir d'Ockham]: https://fr.wikipedia.org/wiki/Rasoir_d'Ockham
[The Boy Scout Rule]: https://www.stepsize.com/blog/how-to-be-an-effective-boy-girl-scout-engineer

<style>
table {
	width: 100%;
}
</style>
