---
share: true
aliases:
  - IoC
tags:
  - cleancode
title: Inversion of Control Container
---
 
# Inversion of Control Container

>**Warum?**
>Nur, was nicht fest verdrahtet ist, kann leichter umkonfiguriert werden.

Bereits im [gelben Grad](Gelber%20Grad.md) hat der [CCD](Clean%20Code%20Developer.md) das [Dependency Inversion Principle](Dependency%20Inversion%20Principle.md) kennengelernt. Dabei wurden die Abhängigkeiten noch „von Hand“ aufgelöst. Der nächste logische Schritt besteht nun darin, das Auflösen der Abhängigkeiten zu automatisieren. Dazu stehen zwei Verfahren zur Verfügung:

-   Locator
-   Container

Beide verwenden einen sogenannten _Inversion of Control Container_ (IoC Container). Vor der Verwendung des Containers müssen die verwendeten Klassen im Container hinterlegt werden. Anschließend kann der Container Instanzen der hinterlegten Klassen liefern. Beim _[Locator](Locator.md)_ geschieht dies explizit. Dies hat den Vorteil, dass die Abhängigkeiten nicht alle im Konstruktor der Klasse aufgeführt werden müssen. Bei Querschnittsaufgaben wie beispielsweise _[Logging](Logging.md)_ ist dies ein übliches Vorgehen. In der Regel werden die Abhängigkeiten jedoch als Parameter des Konstruktors aufgeführt. Dies hat den Vorteil dass alle Abhängigkeiten sichtbar sind. Der Container ist damit in der Lage die Abhängigkeiten implizit aufzulösen in dem er rekursiv alle benötigten Objekte über den Container instanziert.

IoC Container werden wichtig, sobald die Anzahl der Klassen wächst. Wenn man _[Separation of Concerns](Separation%20of%20Concerns.md)_ beherzigt, entstehen viele kleine Klassen mit überschaubaren Aufgaben. Das Zusammensetzen von Instanzen dieser Klassen wird entsprechend aufwendiger. Genau hier setzt der IoC Container an, er hilft beim Instanziieren und Verbinden der vielen kleinen Objekte.

Ein weiterer Vorteil von IoC Containern ist die Tatsache, dass der _Lebenszyklus_ eines Objektes per Konfiguration bestimmt werden kann. Soll es zur Laufzeit nur eine einzige Instanz eines Objektes geben (_[Singleton](Singleton.md)_) kann der Container angewiesen werden, immer ein und dieselbe Instanz zu liefern. Auch andere Lebenszyklen wie z.B. _eine Instanz pro Session_ werden unterstützt.

Um bei Verwendung eines Locators nicht in Abhängigkeit zu einem bestimmten IoC Container zu geraten, kann der _[Microsoft Common Service Locator](Microsoft%20Common%20Service%20Locator.md)_ (siehe Tools) verwendet werden. Dieser bietet eine vereinheitlichte Schnittstelle zu den gängigen IoC Containern.

Zum Verständnis der Mechanik die hinter einem IoC Container steckt, ist es nützlich die Funktionalität einmal selber zu implementieren. Dabei soll kein vollständiger Container implementiert werden sondern lediglich die Grundfunktionen.

Siehe auch unter [Tools](https://clean-code-developer.de/weitere-infos/werkzeuge/).