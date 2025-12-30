# Algorythmen und Datenstrukturen
This repository contains various algorithms and data structures implemented in Java. 
The goal is to provide a comprehensive collection of common algorithms and data structures for educational purposes.

---

### Was ist Gradle?

**Gradle** ist ein Build-Automatisierungstool für Java-Projekte (und andere Sprachen).

**Hauptfunktionen:**
- **Dependency Management**: Verwaltet externe Bibliotheken automatisch
- **Build Automation**: Kompiliert Code, führt Tests aus, erstellt JARs
- **Task-basiert**: Definiert wiederverwendbare Build-Schritte
- **Konvention über Konfiguration**: Standard-Projektstruktur vorgegeben

**Vergleich zu Alternativen:**
- **Maven**: XML-basiert, strenger, verbose
- **Gradle**: Groovy/Kotlin-basiert, flexibler, moderner

**Gradle vs. Maven vs. Manuell:**
```
Manuell:
├─ Bibliotheken selbst herunterladen
├─ Classpath manuell setzen
└─ Kompilierung per javac-Befehle

Maven/Gradle:
├─ Bibliotheken automatisch heruntergeladen
├─ Standardisierte Projektstruktur
└─ Ein Befehl für Build/Test/Package
```

### Gradle Kernkonzepte

1. **build.gradle(.kts)**: Haupt-Konfigurationsdatei
    - Definiert Projekt-Metadaten
    - Dependencies
    - Tasks
    - Plugins

2. **settings.gradle(.kts)**: Projekt-Einstellungen
    - Projektname
    - Multi-Modul-Projekte

3. **gradle/wrapper**: Gradle Wrapper
    - Garantiert gleiche Gradle-Version für alle Entwickler
    - Kein globales Gradle-Installation nötig

4. **Standard-Verzeichnisstruktur:**
```
projekt/
├── src/
│   ├── main/
│   │   ├── java/          # Produktionscode
│   │   └── resources/     # Ressourcen (configs, etc.)
│   └── test/
│       ├── java/          # Test-Code
│       └── resources/     # Test-Ressourcen
├── build.gradle           # Build-Konfiguration
├── settings.gradle        # Projekt-Settings
└── gradle/                # Gradle Wrapper Files
```

---

## Teil 2: Step-by-Step IntelliJ Projekt Setup

### Schritt 1: IntelliJ IDEA öffnen

1. Starte **IntelliJ IDEA**
2. Wähle **"New Project"**

### Schritt 2: Projekt konfigurieren

**Im "New Project" Dialog:**

```
┌─────────────────────────────────────────┐
│ Name: datenstrukturen-uebungen         │
│ Location: /pfad/zu/deinem/verzeichnis  │
│                                         │
│ Language: Java                          │
│ Build System: Gradle                    │
│                                         │
│ JDK: 17 (oder höher)                   │
│ [Falls nicht vorhanden: Download JDK]   │
│                                         │
│ Gradle DSL: Groovy (oder Kotlin)       │
│                                         │
│ [X] Add sample code                     │
│                                         │
│ Advanced Settings:                      │
│   GroupId: de.fernuni.datenstrukturen  │
│   ArtifactId: uebungen                 │
│                                         │
│             [Create]                    │
└─────────────────────────────────────────┘
```

**Einstellungen erklärt:**
- **Name**: Projektname (frei wählbar)
- **Build System**: Gradle auswählen
- **JDK**: Java Development Kit (mindestens Version 11, empfohlen 17+)
- **Gradle DSL**:
    - Groovy: Traditionell, mehr Beispiele online
    - Kotlin: Moderner, type-safe
- **GroupId**: Namespace (z.B. deine Uni-Domain rückwärts)
- **ArtifactId**: Projekt-Identifier

### Schritt 3: Warten auf Gradle Sync

Nach dem Erstellen:
1. IntelliJ lädt Gradle herunter (falls nötig)
2. Projekt-Struktur wird initialisiert
3. Dependencies werden heruntergeladen
4. Status unten rechts: "Gradle sync in progress..."

**Warte bis "Gradle sync completed" erscheint!**

### Schritt 4: Projekt-Struktur prüfen

Deine Struktur sollte so aussehen:

```
datenstrukturen-uebungen/
├── .gradle/                    # Gradle Cache (ignorieren)
├── .idea/                      # IntelliJ Konfiguration (ignorieren)
├── gradle/
│   └── wrapper/
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── src/
│   ├── main/
│   │   ├── java/              # HIER: Produktionscode
│   │   └── resources/
│   └── test/
│       ├── java/              # HIER: Test-Code
│       └── resources/
├── .gitignore                 # Git Ignore File
├── build.gradle               # Gradle Build Config
├── gradlew                    # Gradle Wrapper (Unix)
├── gradlew.bat                # Gradle Wrapper (Windows)
└── settings.gradle            # Projekt Settings
```

### Schritt 5: build.gradle anpassen

Öffne `build.gradle` und stelle sicher, dass es so aussieht:

```groovy
plugins {
    id 'java'
}

group = 'de.fernuni.datenstrukturen'
version = '1.0-SNAPSHOT'

repositories {
    mavenCentral()
}

dependencies {
    // JUnit 5 für Tests
    testImplementation platform('org.junit:junit-bom:5.10.0')
    testImplementation 'org.junit.jupiter:junit-jupiter'
}

// Java Version
java {
    toolchain {
        languageVersion = JavaLanguageVersion.of(17)
    }
}

// Test Configuration
test {
    useJUnitPlatform()
}
```

**Wichtige Sections erklärt:**

1. **plugins**: Aktiviert Java-Plugin
2. **repositories**: Wo Dependencies heruntergeladen werden
3. **dependencies**: Externe Bibliotheken (hier JUnit für Tests)
4. **java.toolchain**: Welche Java-Version verwendet wird
5. **test**: Test-Konfiguration

### Schritt 6: Erste Package-Struktur erstellen

**Im Project Explorer (links):**

1. Rechtsklick auf `src/main/java`
2. **New → Package**
3. Name: `de.fernuni.datenstrukturen.lektion2`
4. Enter

**Wiederhole für Tests:**
1. Rechtsklick auf `src/test/java`
2. **New → Package**
3. Name: `de.fernuni.datenstrukturen.lektion2`

**Ergebnis:**
```
src/
├── main/
│   └── java/
│       └── de/
│           └── fernuni/
│               └── datenstrukturen/
│                   └── lektion2/
│                       # Hier: Deine Implementierungen
└── test/
    └── java/
        └── de/
            └── fernuni/
                └── datenstrukturen/
                    └── lektion2/
                        # Hier: Deine Tests
```

### Schritt 7: Erste Test-Klasse erstellen

**Test-Driven Development Ansatz:**

1. Rechtsklick auf `src/test/java/.../lektion2`
2. **New → Java Class**
3. Name: `ListTest`
4. Enter

### Schritt 8: Tests ausführen

**Option 1: Über UI**
- Rechtsklick auf Test-Klasse → "Run 'ListTest'"
- Oder: Grüner Play-Button neben Klasse/Methode

**Option 2: Gradle Task**
- Rechts: "Gradle" Tab öffnen
- `Tasks → verification → test` doppelklicken

**Option 3: Terminal**
```bash
./gradlew test
```

### Schritt 9: GitHub Integration

**Repository initialisieren:**

1. **VCS → Enable Version Control Integration**
2. Git auswählen → OK
3. **VCS → Commit** (oder Ctrl+K)
4. Initial commit durchführen

**GitHub Repository erstellen:**

1. Auf GitHub.com: "New Repository"
2. Name: `datenstrukturen-uebungen`
3. **NICHT** mit README initialisieren
4. Create Repository

**Remote hinzufügen:**

```bash
# Im IntelliJ Terminal (unten):
git remote add origin https://github.com/DEIN_USERNAME/datenstrukturen-uebungen.git
git branch -M main
git push -u origin main
```

**Oder über IntelliJ UI:**
- **VCS → Git → Remotes → +**
- URL eingeben → OK
- **VCS → Git → Push**

### Schritt 10: .gitignore prüfen

IntelliJ erstellt automatisch `.gitignore`. Prüfe ob enthalten:

```gitignore
# Gradle
.gradle
build/
!gradle/wrapper/gradle-wrapper.jar

# IntelliJ
.idea/
*.iml
*.iws
*.ipr
out/

# OS
.DS_Store
Thumbs.db

# Compiled
*.class
```

---

## Teil 3: Typischer Workflow

### Übungsaufgabe bearbeiten

**1. Test-Klasse erstellen (TDD-Ansatz):**
```
src/test/java/.../lektion2/StackTest.java
```

**2. Test schreiben:**

**3. Test laufen lassen → Fehlschlag (Klasse existiert nicht)**

**4. Implementierung erstellen:**
```
src/main/java/.../lektion2/Stack.java
```

**5. Implementieren bis Test grün**

**6. Commit:**
```bash
git add .
git commit -m "Implement Stack with push/pop"
git push
```

### Nützliche Gradle Tasks

**Im Terminal oder Gradle Tab:**

```bash
# Projekt kompilieren
./gradlew build

# Tests ausführen
./gradlew test

# Nur kompilieren (keine Tests)
./gradlew compileJava

# Projekt aufräumen
./gradlew clean

# Alle Tasks anzeigen
./gradlew tasks

# Build ohne Tests
./gradlew build -x test
```

### IntelliJ Shortcuts

**Code Navigation:**
- `Ctrl + N`: Klasse suchen
- `Ctrl + Shift + N`: Datei suchen
- `Ctrl + B`: Zur Definition springen
- `Alt + F7`: Verwendungen finden

**Code Generation:**
- `Alt + Insert`: Generate (Constructor, Getter, etc.)
- `Ctrl + O`: Methoden überschreiben
- `Ctrl + Space`: Code Completion

**Refactoring:**
- `Shift + F6`: Rename
- `Ctrl + Alt + M`: Extract Method
- `Ctrl + Alt + V`: Extract Variable

**Tests:**
- `Ctrl + Shift + F10`: Test unter Cursor ausführen
- `Shift + F10`: Letzten Test wiederholen

---

## Teil 4: Empfohlene Packages für Übungen

```
de.fernuni.datenstrukturen/
├── lektion2/
│   ├── list/
│   │   ├── LinkedList.java
│   │   ├── DoublyLinkedList.java
│   │   └── ArrayList.java
│   ├── stack/
│   │   └── Stack.java
│   ├── queue/
│   │   └── Queue.java
│   ├── tree/
│   │   ├── BinaryTree.java
│   │   └── Node.java
│   └── mapping/
│       └── Mapping.java
└── util/
    └── TestHelper.java
```

---

## Teil 5: Troubleshooting

### Problem: "Gradle sync failed"

**Lösung:**
1. **File → Invalidate Caches → Invalidate and Restart**
2. Gradle Version in `gradle-wrapper.properties` prüfen
3. Internet-Verbindung prüfen

### Problem: "Cannot resolve symbol 'Test'"

**Lösung:**
1. Gradle Sync durchführen: **File → Sync Project with Gradle Files**
2. Dependencies in `build.gradle` prüfen
3. JUnit 5 korrekt konfiguriert?

### Problem: Tests werden nicht erkannt

**Lösung:**
1. `test { useJUnitPlatform() }` in `build.gradle` vorhanden?
2. JUnit 5 Annotations verwendet (`@Test`, nicht `@org.junit.Test`)?
3. Test-Klasse im richtigen Verzeichnis (`src/test/java`)?

### Problem: Falsches JDK

**Lösung:**
1. **File → Project Structure → Project**
2. SDK: Korrektes JDK auswählen
3. Language Level: Entsprechend setzen

---

## Teil 6: Best Practices

### Package Naming
```
✓ de.fernuni.datenstrukturen.lektion2.stack
✗ stack
✗ Stack
```

### Class Naming
```
✓ LinkedList.java (Klasse = LinkedList)
✗ linkedList.java
✗ linked_list.java
```

### Test Naming
```
✓ LinkedListTest.java
✓ testInsertAtPosition()
✓ shouldReturnTrueWhenListIsEmpty()

✗ Test1.java
✗ test1()
```

### Commit Messages
```
✓ "Implement doubly linked list insert operation"
✓ "Fix queue dequeue bug when empty"
✓ "Add tests for stack overflow handling"

✗ "update"
✗ "fix"
✗ "asdf"
```

---

## Teil 7: Erweiterte Konfiguration (Optional)

### JUnit 5 Assertions importieren

In `build.gradle` ergänzen:

```groovy
dependencies {
    testImplementation platform('org.junit:junit-bom:5.10.0')
    testImplementation 'org.junit.jupiter:junit-jupiter'
    
    // Optional: Bessere Assertions
    testImplementation 'org.assertj:assertj-core:3.24.2'
}
```

**AssertJ Beispiel:**

```java
// Standard JUnit
// assertEquals(expected, actual);

// AssertJ (flüssiger, bessere Fehlermeldungen)
// assertThat(actual).isEqualTo(expected);
// assertThat(list).hasSize(3).contains("a", "b", "c");
```

### Code Coverage anzeigen

Plugin in `build.gradle`:

```groovy
plugins {
    id 'java'
    id 'jacoco'  // Coverage Plugin
}

jacoco {
    toolVersion = "0.8.10"
}

test {
    useJUnitPlatform()
    finalizedBy jacocoTestReport
}

jacocoTestReport {
    dependsOn test
    reports {
        html.required = true
        xml.required = false
        csv.required = false
    }
}
```

**Coverage anzeigen:**
```bash
./gradlew test jacocoTestReport
# Report: build/reports/jacoco/test/html/index.html
```

---

## Zusammenfassung

**Setup-Reihenfolge:**
1. IntelliJ: New Project → Gradle → Java
2. build.gradle konfigurieren
3. Package-Struktur erstellen
4. Git initialisieren
5. GitHub remote hinzufügen

**Workflow:**
1. Test schreiben
2. Implementieren
3. Test grün machen
4. Commit & Push

**Gradle Basics:**
- `./gradlew build` - Alles bauen
- `./gradlew test` - Tests laufen lassen
- `./gradlew clean` - Aufräumen

**Bei Problemen:**
1. Gradle Sync
2. Cache invalidieren
3. Dependencies prüfen