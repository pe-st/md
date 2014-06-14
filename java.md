* Java

** Java Online Ressourcen

- Thinking in Java
- Critical Comparison to C++ (1997):
  http://www.objectmentor.com/resources/articles/javacpp.pdf
- Java-C++ Comparison:
  http://www.cc.gatech.edu/classes/AY2002/cs6390_fall/resources/java/YannisJava-cpp.pdf

** eclipse

http://developer.apple.com/tools/usingeclipse.html

** Java vs C++

- Wrapper-Typen f�r primitive Typen
- keine unsigned Typen
- char ist Unicode, belegt 2 Bytes
- Alles ist eine Referenz (Referenzen k�nnen aber neu zugewiesen werden)
  . auch this ist eine Referenz und kein Zeiger (logisch...)
  . keine Objekte auf dem Stack
  . Schl�sselwort "null" f�r eine "Null-Referenz"
- Garbage Collector
- Scope-Regeln. In Java keine gleichnamige neue Objekte in inneren Scopes
- kein Semikolon nach class {}
- Namensr�ume mit umgekehrten Domain-Namen (ch.schlau.pesche);
  vorgegebene Verzeichnis-Struktur (packages)
  . package = library of classes
  . import und package statt include
  . nur eine public-Klasse pro .java-File
- main ist eine "public static" Methode mit fixer Signatur;
  Klassenname muss Filenamen entsprechen
- public/protected/private bei jedem Element, default ist "package-private"
- Auch Klassen sind public oder "package-private"
- kein Pr�prozessor
- kein �berladen von Operatoren
- == testet auf Identit�t; f�r �quivalenz equals() verwenden
  (uU f�r eigene Klasse �berschreiben n�tig)
- bool heisst boolean und unterscheidet sich st�rker von integers:
  - keine automatische Konversion von int zu boolean in logischen
    Ausdr�cken
- zwei verschiedene Rechts-Schiebe-Operatoren:
  >> signed right shift
  >>> unsigned right shift (zero extension)
- komma ist kein Operator (nur f�r for-Schlaufen)
- Casts: C-Style Casts, nicht alles erlaubt ("casts are safe")
- es gibt kein sizeof
- kein goto, aber break und continue mit Labels
- Initialisierung auch von non-const Klassenelementen bei der Definition
  . passiert vor den Konstruktoren
  . static clause (static block)
  . instance initialization clause
- const heisst final, volatile bleibt volatile
  . finale Referenzen entsprechen T* const, f�r const T* gibt es keine Entsprechung
  . blank finals: unterschiedliche Werte f�r verschiedene Exemplare
  . finale Argument entsprechen const T& Argumenten
  . finale Methoden k�nnen nicht �berschrieben werden
  . finale Klassen k�nnen nicht beerbt werden
- Konstruktor forwarding mit this(argumente,f�r,anderen,ctor)
- keine Destruktoren, finalize nur selten n�tig (im Zshg mit native Code),
  aber n�tzlich zum Testen der Termination Condition
- Arrays:
  . zwei M�glichkeiten zur Array-Definition:
    int[] a;
    int a[];
  . keine Gr�ssendefinition m�glich
- Variable Anzahl Argumente (varargs): f(Type... t), t als Array �bergeben
- Vererbung
  . Derived extends Base
  . Schl�sselwort super
  . ctor-Aufruf von Basisklasse mit super(...)
  . ctor von abgeleiteten Klassen kann Exceptions von Basis-ctor nicht fangen (!)
    (Vgl. Stroustrup 14.4.6.1 Exceptions and Member Initialization)
  . Methoden mit anderer Signatur verdecken Basisklassen-Methoden NICHT
  . private Methoden k�nnen nicht �berschrieben werden
  . alle nicht-static und nicht-final Methoden sind "virtual"
  . Schl�sselwort "abstract" statt "= 0" (pure virtual),
    kann auch f�r Klassen benutzt werden
  . in Konstruktoren k�nnen virtuelle Methoden verwendet werden (!)
  . jeder Cast ist "safe" (entspricht einem dynamic_cast)
- Keine Mehrfachvererbung, aber interface-Klassen
  . entspricht ungef�hr Mixin-Klassen ohne Implementation)
  . "implements" statt "extends"
  . interface-Klassen k�nnen von mehreren interfaces erben (mit "extends") (!)
  . "tagging" Interfaces ohne Methoden (vgl. Serializable)
- Verschachtelte Klassen
  . Scope-Operator ist . statt :: (bzw $ f�r den Filenamen: Outer$Inner.class)
  . auch in Methoden (local inner class) und Bl�cken
  . anonyme Klassen inkl. Vererbung (grob verwandt mit anonymen structs: struct {...} variable;)
  . innere Klassen haben Zugriff auf alle Elemente der �usseren Klasse;
    explizite Referenz mit Outer.this
  . erzeugen von inneren Klassen: "outer.new Inner()"
  . "nested class": statische innere Klasse
  . nested class auch in interfaces m�glich
  . innere Klassen k�nnen erben, auch wenn die �ussere Klasse auch schon
    abgeleitet ist: eine Art Mehrfachvererbung...
  . innere Klassen praktisch f�r Closures und Callbacks
- Exceptions
  . Die meisten Ausnahmen sind abgeleitet von Exception und dies wiederum
    ist abgeleitet von Throwable
  . Error ist auch von Throwable abgeleitet (und sollte nocht behandelt werden)
  . es gibt fertige Methode zur Stack-Trace-Behandlung
  . rethrow mit parameter: "throw e"
  . "checked exceptions" : Exception specifications sind zwingend,
    ausser von Error und RuntimeException abgeleitete Klassen
  . exception chaining: fr�here Exceptions ("history") in neuen Exceptions speichern
  . finally (nach allen catch-clauses geschrieben) wird immer bedient
  . wenn eine Exception geworfen wird, w�hrend eine andere noch h�ngig ist, geht
    die �ltere verloren (!)
- RTTI und Reflection
  . f�r jede geladene Klasse ex. ein Class-Exemplar
  . f�r alle Typen gibt es das "class literal" (MyClass.class)
  . f�r Wrapper der primitiven Typen gibt es ein TYPE Element:
    Character.TYPE entspricht char.class
  . instanceof Operator (gibt boolean) bzw. Class.isInstance()
  . bei Reflection m�ssen Klassen erst zur Runtime vorhanden sein
- Container
  . keine M�glichkeit des Zugriffs ohne Bereichspr�fung
  . nur Array kann primitive Typen aufnehmen
  . Aggregat-Init auch mit non-const Elementen
  . Iteratoren: iterator() statt begin(), next() statt operator++(),
    iter.hasNext() statt cont.end()
  . References (entfernt verwandt mit weak_ptr): Soft-/Weak-/Phantom-
    in einer ReferenceQueue darf der GC die Objekte schon l�schen
  . Collections.unmodifiable{List,Set,...} erzeugt readonly Container
  . �hnlich: Collections.synchronized{List,Set,...}
  . wenn Iteratoren ung�ltig werden: beim n�chsten next() eine
    ConcurrentModificationException ("fail-fast")
  . einige Methoden des Collection-Interfaces sind "optional Methods"
    und nicht von allen Containern implementiert (zB Array.asList())
    Wenn man es trotzdem probiert: UnsupportedOperationException
  . veraltet: Vector/Hashtable/Stack, Enumeration (alte Iteratoren)
  . Gegen�berstellung:
    |--------------+-----------------|
    | C++          | Java            |
    |--------------+-----------------|
    | []           | Array           |
    | vector       | ArrayList       |
    | list         | LinkedList      |
    | deque        | (LinkedList)    |
    | set          | TreeSet         |
    | (hashed set) | HashSet         |
    |              | LinkedHashSet   |
    | multiset     |                 |
    | map          | TreeMap         |
    | multimap     |                 |
    | (hashed map) | HashMap         |
    |              | LinkedHashMap   |
    |              | WeakHashMap     |
    |              | IdentityHashMap |
    | vector<bool> | BitSet          |
    |--------------+-----------------|

- I/O
  . seit Java 1.1 char-oriented IO (Unicode) statt byte-oriented:
    Input-/Outputstream sind byte-oriented, Reader/Writer Zeichenorientiert
  . nio (new IO): bessere Performance (seit JDK 1.4)
    nio arbeitet mit Buffers und Channels und unterst�tzt "type casts"
    von primitiven Typen auf die bin�re Repr�sentation
  . Memory-mapped Files mit nio
  . File-Locking eingebaut. Welche Art von Lock, nur Schreiben oder auch Lesen?
  . Zip und Gzip direkt unterst�tzt, ebenso Checksummen
  . Jar's (Java Archives) sind entweder gezippt oder unkomprimiert;
    unkomprimiert im CLASSPATH erlaubt
  . Einfache Persistenz mit Interface Serializable; mehr M�glichkeiten
    mit Java Data Objects (JDO) oder "Hibernate"
  . Serialisierung unter anderem n�tig f�r RMI (Remote Method Invocation = Java
    RPC) und JavaBeans
  . Mehr Kontrolle �ber Serialisierung mit Externalizable
  . Felder mit dem "transient" Qualifier werden nicht serialisiert
    (zB f�r Passw�rter)
  . Serializable: "tagging" Interfaces ohne Methoden, aber bestimmte private (!)
    Methode dienen als Anpassungs-Schnittstelle -> schwarze Magie...
  . statische Felder m�ssen explizit/manuell serialisiert werden
  . Preferences verwenden unter Windows die Registry. Und unter OS X?
  . Regexp: spezielle Behandlung von '\', zB '\' = "\\\\" (!)
  . Regexp: zus�tzlich zu "greedy" und "reluctant" auch noch "possessive"
- Threads, Concurrency
  . Unterscheidung zwischen normalen und Daemon-Threads (setDaemon, isDaemon):
    eine Applikation kann trotz laufender Daemon-Threads terminieren
  . Vokabular: yield, sleep, wait*, join, interrupt, notify*, notifyAll*
    deprecated: stop, destroy, suspend, resume
    (* Methoden von Object, nicht Thread, da Bezug auf den Lock jedes Objekts;
       Verwendung nur in synchronized-Kontext)
  . Thread-Stati: new, runnable, dead, blocked
  . entweder von Thread ableiten oder Runnable implementieren
  . Zuweisung und R�ckgabe von primitiven Typen (ausser long und double) sind
    atomar. Bei long und double ist volatile n�tig.
  . synchronized als Qualifier einer Methode: alle synchronized-Methoden eines
    Objekts benutzen denselben impliziten Mutex pro Objekt
  . synchronized ist nicht Teil der Signatur
  . synchronized als Block : synchronized(object) { /* critical section */ }
  . Beim Mischen von synchronized-Methoden und synchronized-Bl�cken
    synchronized(this) verwenden, damit derselbe Semaphor verwendet wird.
  . Producer/Consumer Pattern mit
    Producer: produce something; synchronize(consumer) { consumer.notify(); }
    Consumer: while (nothing to consume) wait();
  . Producer/Consumer ohne wait: mit PipedWriter/PipedReader
  . �berarbeitetes Memory-Model mit Java 1.5
    (http://www.artima.com/forums/flat.jsp?forum=226&thread=180936&message=235937)

* eof

Local Variables:
mode: outline
coding: latin-1
End:
