# Java

## Java Online Ressourcen

- Thinking in Java
- Critical Comparison to C++ (1997):
  http://www.objectmentor.com/resources/articles/javacpp.pdf
- Java-C++ Comparison:
  http://www.cc.gatech.edu/classes/AY2002/cs6390_fall/resources/java/YannisJava-cpp.pdf

### 2014

- Introduction to Programming Using Java, Sixth Edition
  http://math.hws.edu/javanotes/
- Java ist auch eine Insel (Christian Ullenboom)
  http://openbook.galileocomputing.de/javainsel/

## eclipse

http://developer.apple.com/tools/usingeclipse.html

## Java vs C++

- Wrapper-Typen für primitive Typen
- keine unsigned Typen
- char ist Unicode, belegt 2 Bytes
- Alles ist eine Referenz (Referenzen können aber neu zugewiesen werden)
  - auch this ist eine Referenz und kein Zeiger (logisch...)
  - keine Objekte auf dem Stack
  - Schlüsselwort "null" für eine "Null-Referenz"
- Garbage Collector
- Scope-Regeln. In Java keine gleichnamige neue Objekte in inneren Scopes
- kein Semikolon nach class {}
- Namensräume mit umgekehrten Domain-Namen (ch.schlau.pesche);
  vorgegebene Verzeichnis-Struktur (packages)
  - package = library of classes
  - import und package statt include
  - nur eine public-Klasse pro .java-File
- main ist eine "public static" Methode mit fixer Signatur;
  Klassenname muss Filenamen entsprechen
- public/protected/private bei jedem Element, default ist "package-private"
- Auch Klassen sind public oder "package-private"
- kein Präprozessor
- strings können nicht ohne + konkateniert werden ("foo" "bar" ist nicht möglich)
- kein Überladen von Operatoren
- == testet auf Identität; für Äquivalenz equals() verwenden
  (uU für eigene Klasse überschreiben nötig)
- bool heisst boolean und unterscheidet sich stärker von integers:
  - keine automatische Konversion von int zu boolean in logischen
    Ausdrücken
- zwei verschiedene Rechts-Schiebe-Operatoren:
  - `>>` signed right shift
  - `>>>` unsigned right shift (zero extension)
- komma ist kein Operator (nur für for-Schlaufen)
- Casts: C-Style Casts, nicht alles erlaubt ("casts are safe")
- es gibt kein sizeof
- kein goto, aber break und continue mit Labels
- Initialisierung auch von non-const Klassenelementen bei der Definition
  - passiert vor den Konstruktoren
  - static clause (static block)
  - instance initialization clause
- const heisst final, volatile bleibt volatile
  - finale Referenzen entsprechen T* const, für const T* gibt es keine Entsprechung
  - blank finals: unterschiedliche Werte für verschiedene Exemplare
  - finale Argumente entsprechen const T& Argumenten (wirklich nötig nur bei Weitergabe an anonyme innere Klassen)
  - final spielt für Signatur-Check von Parametern keine Rolle
  - finale Methoden können nicht überschrieben werden
  - finale Klassen können nicht beerbt werden
- Konstruktor forwarding mit this(argumente,für,anderen,ctor)
- keine Destruktoren, finalize nur selten nötig (im Zshg mit native Code),
  aber nützlich zum Testen der Termination Condition
- Arrays:
  - zwei Möglichkeiten zur Array-Definition:
    int[] a;
    int a[];
  - keine Grössendefinition möglich
- Variable Anzahl Argumente (varargs): f(Type... t), t als Array übergeben
- Vererbung
  - Derived extends Base
  - Schlüsselwort super
  - ctor-Aufruf von Basisklasse mit super(...)
  - ctor von abgeleiteten Klassen kann Exceptions von Basis-ctor nicht fangen (!)
    (Vgl. Stroustrup 14.4.6.1 Exceptions and Member Initialization)
  - Methoden mit anderer Signatur verdecken Basisklassen-Methoden NICHT
  - private Methoden können nicht überschrieben werden
  - alle nicht-static und nicht-final Methoden sind "virtual"
  - Schlüsselwort "abstract" statt "= 0" (pure virtual),
    kann auch für Klassen benutzt werden
  - in Konstruktoren können virtuelle Methoden verwendet werden (!)
  - jeder Cast ist "safe" (entspricht einem dynamic_cast)
- Keine Mehrfachvererbung, aber interface-Klassen
  - entspricht ungefähr Mixin-Klassen ohne Implementation)
  - "implements" statt "extends"
  - interface-Klassen können von mehreren interfaces erben (mit "extends") (!)
  - "tagging" Interfaces ohne Methoden (vgl. Serializable)
- Verschachtelte Klassen
  - Scope-Operator ist `.` statt `::` (bzw `$` für den Filenamen: `Outer$Inner.class`)
  - auch in Methoden (local inner class) und Blöcken
  - anonyme Klassen inkl. Vererbung (grob verwandt mit anonymen structs: struct {...} variable;)
  - innere Klassen haben Zugriff auf alle Elemente der äusseren Klasse;
    explizite Referenz mit Outer.this
  - erzeugen von inneren Klassen: "outer.new Inner()"
  - "nested class": statische innere Klasse
  - nested class auch in interfaces möglich
  - innere Klassen können erben, auch wenn die äussere Klasse auch schon
    abgeleitet ist: eine Art Mehrfachvererbung...
  - innere Klassen praktisch für Closures und Callbacks
- Exceptions
  - Die meisten Ausnahmen sind abgeleitet von Exception und dies wiederum
    ist abgeleitet von Throwable
  - Error ist auch von Throwable abgeleitet (und sollte nocht behandelt werden)
  - es gibt fertige Methode zur Stack-Trace-Behandlung
  - rethrow mit parameter: `throw e`
  - "checked exceptions" : Exception specifications sind zwingend,
    ausser von Error und RuntimeException abgeleitete Klassen
  - exception chaining: frühere Exceptions ("history") in neuen Exceptions speichern
  - finally (nach allen catch-clauses geschrieben) wird immer bedient
  - wenn eine Exception geworfen wird, während eine andere noch hängig ist, geht
    die ältere verloren (!)
- RTTI und Reflection
  - für jede geladene Klasse ex. ein Class-Exemplar
  - für alle Typen gibt es das "class literal" (MyClass.class)
  - für Wrapper der primitiven Typen gibt es ein TYPE Element:
    Character.TYPE entspricht char.class
  - instanceof Operator (gibt boolean) bzw. Class.isInstance()
  - bei Reflection müssen Klassen erst zur Runtime vorhanden sein
- Container
  - keine Möglichkeit des Zugriffs ohne Bereichsprüfung
  - nur Array kann primitive Typen aufnehmen
  - Aggregat-Init auch mit non-const Elementen
  - Iteratoren: iterator() statt begin(), next() statt operator++(),
    iter.hasNext() statt cont.end()
  - References (entfernt verwandt mit weak_ptr): Soft-/Weak-/Phantom-
    in einer ReferenceQueue darf der GC die Objekte schon löschen
  - Collections.unmodifiable{List,Set,...} erzeugt readonly Container
  - ähnlich: Collections.synchronized{List,Set,...}
  - wenn Iteratoren ungültig werden: beim nächsten next() eine
    ConcurrentModificationException ("fail-fast")
  - einige Methoden des Collection-Interfaces sind "optional Methods"
    und nicht von allen Containern implementiert (zB Array.asList())
    Wenn man es trotzdem probiert: UnsupportedOperationException
  - veraltet: Vector/Hashtable/Stack, Enumeration (alte Iteratoren)
  - Gegenüberstellung:
    ```
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
    ```
- I/O
  - seit Java 1.1 char-oriented IO (Unicode) statt byte-oriented:
    Input-/Outputstream sind byte-oriented, Reader/Writer Zeichenorientiert
  - nio (new IO): bessere Performance (seit JDK 1.4)
    nio arbeitet mit Buffers und Channels und unterstützt "type casts"
    von primitiven Typen auf die binäre Repräsentation
  - Memory-mapped Files mit nio
  - File-Locking eingebaut. Welche Art von Lock, nur Schreiben oder auch Lesen?
  - Zip und Gzip direkt unterstützt, ebenso Checksummen
  - Jar's (Java Archives) sind entweder gezippt oder unkomprimiert;
    unkomprimiert im CLASSPATH erlaubt
  - Einfache Persistenz mit Interface Serializable; mehr Möglichkeiten
    mit Java Data Objects (JDO) oder "Hibernate"
  - Serialisierung unter anderem nötig für RMI (Remote Method Invocation = Java
    RPC) und JavaBeans
  - Mehr Kontrolle über Serialisierung mit Externalizable
  - Felder mit dem "transient" Qualifier werden nicht serialisiert
    (zB für Passwörter)
  - Serializable: "tagging" Interfaces ohne Methoden, aber bestimmte private (!)
    Methode dienen als Anpassungs-Schnittstelle -> schwarze Magie...
  - statische Felder müssen explizit/manuell serialisiert werden
  - Preferences verwenden unter Windows die Registry. Und unter OS X?
  - Regexp: spezielle Behandlung von '\', zB '\' = "\\\\" (!)
  - Regexp: zusätzlich zu "greedy" und "reluctant" auch noch "possessive"
- Threads, Concurrency
  - Unterscheidung zwischen normalen und Daemon-Threads (setDaemon, isDaemon):
    eine Applikation kann trotz laufender Daemon-Threads terminieren
  - Vokabular: yield, sleep, wait*, join, interrupt, notify*, notifyAll*
    deprecated: stop, destroy, suspend, resume
    (* Methoden von Object, nicht Thread, da Bezug auf den Lock jedes Objekts;
       Verwendung nur in synchronized-Kontext)
  - Thread-Stati: new, runnable, dead, blocked
  - entweder von Thread ableiten oder Runnable implementieren
  - Zuweisung und Rückgabe von primitiven Typen (ausser long und double) sind
    atomar. Bei long und double ist volatile nötig.
  - synchronized als Qualifier einer Methode: alle synchronized-Methoden eines
    Objekts benutzen denselben impliziten Mutex pro Objekt
  - synchronized ist nicht Teil der Signatur
  - synchronized als Block : synchronized(object) { /* critical section */ }
  - Beim Mischen von synchronized-Methoden und synchronized-Blöcken
    synchronized(this) verwenden, damit derselbe Semaphor verwendet wird.
  - Producer/Consumer Pattern mit
    Producer: produce something; synchronize(consumer) { consumer.notify(); }
    Consumer: while (nothing to consume) wait();
  - Producer/Consumer ohne wait: mit PipedWriter/PipedReader
  - Überarbeitetes Memory-Model mit Java 1.5
    (http://www.artima.com/forums/flat.jsp?forum=226&thread=180936&message=235937)

## Naming

Konkrete Einfachst-Impl von interfaces: SimpleXxx

## todo

Iterable

## Libraries

### XML

StAX: Streaming API fo XML; https://docs.oracle.com/javase/tutorial/jaxp/stax/
- Cursor API: XMLStreamReader
- Event API: XMLEventReader

XMLStreamReader is more efficient, but XMLEventReader is easier to use, because all the information related to a particular event is encapsulated in a returned XMLEvent object. However, the disadvantage of the event approach is the extra overhead of creating objects for every event, which consumes both time and memory.

Note: XMLEventReader example use in fileloader25/xml/BaseXMLProcessor.java


## Präsentation 2014-06-27 Java 7/8 Philipp Marschall von PASS/netcetera

- https://github.com/marschall
- https://github.com/netcetera

- try-with-resources (kein finally mehr), Klasse muss AutoClosable implementieren
  (besser selbst ein NonThrowingAutoClosable machen)

### java.nio

java.io.File (alt)

- no exceptions
- no copy/move
- no link/symlink
- no support for permissions/notification
- not testable

neue Klassen:
- Path (ohne IO, muss nicht existieren)
- Files
- FileSystem

copy/move nur innerhalb eines FileSystem, zw. versch. file systemen mit der Files Klasse

Portabler Code: Filesystem injecten

### MethodHandles API

Eine Art zweites Reflection API

ermöglicht eine Art Methoden-Zeiger wie in C++


### Java 8 time

(Oracle TIMESTAMPTZ fkt. nur mit EclipseLink, nicht mit Hibernate)

Duration <-> Period

- Duration: 'scientific' (date agnostic)
- Period: 'civil' (1 Tag ist uU 23 oder 25 Stunden bei Sommerzeitwechsel)

Vergleich von Zeitpunkten (zB ZonedDateTime und OffsetDateTime): mit toInstance

JDBC verwendet OffsetDateTime, nicht ZonedDateTime

### Java 8

@FunctionalInterface
- default implementationen
- statische Methoden
- nur eine nicht-impl Methode (wegen Lambdas)

Method References (:: operator) kann anstelle eines Lambdas verwendet werden



## Java EE

### Java Batch JSR-352

Differences to Spring Batch: https://blog.codecentric.de/en/2013/07/spring-batch-and-jsr-352-batch-applications-for-the-java-platform-differences/

### CDI

- FAQ: http://www.cdi-spec.org/faq/
- WELD is the reference implementation: http://weld.cdi-spec.org/
- WELD 2.x reference: http://docs.jboss.org/weld/reference/latest/en-US/pdf/weld-reference.pdf
- JUnit 5 Tests: use weld-junit5 when Mockito is not enough

Relation between EE, CDI and Weld Versions: http://weld.cdi-spec.org/documentation/#9 ; basically:

EE  | CDI     | Weld
--- | ----    | ----
6   | 1.0     | 1.1
7   | 1.1/1.2 | 2.x
6   | 2.0     | 3.0

Scopes:

- `@RequestScoped` (built-in)
- `@SessionScoped` (built-in, serializable)
- `@ApplicationScoped` (built-in)
- `@ConversationScoped` (built-in, serializable)
- `@Singleton` (pseudo-scope, not proxied)
- `@Dependant` (pseudo-scope, not proxied)


### JAX-RS

`http://myHostName/contextPath/servletURI/resourceURI`

**context root**, **context path**:

The context root of a web application determines which URLs the Application Server will delegate to your web application. If your application's context root is myapp then any request for /myapp or /myapp/* will be handled by your application unless a more specific context root exists. If a second web application were assigned the context root myapp/help, a request for /myapp/help/help.jsp would be handled by the second web application, not the first.

Corresponds often to the name of the WAR file

**servlet URI**

Specified by the @ApplicationPath annotation

**resource URI**

Specified by the @Path annotation(s)

#### HTTP methods for REST

- http://www.restapitutorial.com/lessons/httpmethods.html
- https://restfulapi.net/create-rest-apis-with-jax-rs-2-0/
- http://restcookbook.com


## javadoc

### 2014

- package-info.java für dokumentierte packages
- {@inheritDocs} ?


<!--
Local Variables:
coding: utf-8
End:
-->
