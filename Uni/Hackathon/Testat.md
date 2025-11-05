stp programm angucken?
permissions?
1. chmod
2. 1. hidden feature?
3. 1. cheat sheet erlaubt
4. ipython3
5. 1. funktionen mit tab angezeigt; funktion? für infos




# Aufgabe 1
## 1.1 Linux (`task1`)

In diesem Schritt wird ein vordefiniertes Python-Script erstellt und ausgeführt.

### 1.1.a Verzeichnis und Script

1. Erstellen Sie in Ihrem Home-Verzeichnis ein neues leeres Verzeichnis mit dem Namen `~/uebung/task1`  _mkdir_
2. Wechseln Sie in das neue Verzeichnis. _cd_
3. Erstellen Sie im neuen Verzeichnis die Datei `hello.py` und fügen Sie die folgenden Zeilen ein: _nano hello.py_

```python
#!/bin/python3
import hashlib
import sys

input_str = sys.argv[1]

input_str = input_str + "DasIstEinTest123"


with open("hello.txt", "w") as f:

    f.write(input_str + "\n")

```

#### 1.1.b Script ausführen

1. Machen Sie das Skript ausführbar und
2. führen Sie es mit Ihrem Login-Namen als Argument aus.
3. Prüfen Sie, ob hello.txt erstellt wurde.

## 1.2. Python (`task2`)

Ziel dieser Aufgabe ist es,
einen modular aufgebauten Python-Code zu erstellen,
der Systeminformationen verarbeitet und über MQTT versendet.

Sie müssen
- neuen Python-Code entwickeln und
- vorhandenen Python-Code nutzen und erweitern.

Das Ziel ist ein Python-Code der mittels `/proc/cpuinfo` die im System verfügbaren Prozessoren bzw. Prozessorkerne zählt und das Ergebniss zusammen mit Metadaten per MQTT verschickt.
Der Code für das Verschicken per MQTT ist vorgegeben und soll per Funktionsaufruf genutzt werden.

### 1.2.a Vorbereitung

1. Erstellen Sie in Ihrem Home-Verzeichnis ein neues leeres Verzeichnis: `uebung/task2`
2. Kopieren Sie alle Dateien aus dem Verzeichnis `/opt/task2` in das neue Verzeichnis.
3. Wechseln Sie in das erstellte Verzeichnis.
4. Lassen Sie sich die Dateien in `uebung/task2` anzeigen.

### 1.2.b Erweiterung von `info_helper.py`

Erweitern Sie die Datei `info_helper.py` um eine Python-Funktion mit dem Namen `get_current_path`.

- Die Funktion gibt den Pfad in dem das Skript ausgeführt wird als String zurück.
- Die Funktion hat keine Übergabeparameter.
- Die Funktion hat den folgenden Header bzw. die folgende Signatur: `def get_current_path() -> str:`

Lösungshinweis:

- Die Funktion `getcwd()` aus der Bibliothek `os` gibt den Pfad zurück, in dem das Script ausgeführt wird.


### 1.2.c Entwicklung von `count_and_publish.py`

#### Schritt 1

Erstellen Sie im neuen Verzeichnis eine neue Datei `count_and_publish.py` und
kopieren den folgenden Inhalt in die Datei:

```python
import re
from info_helper import get_current_path, get_meta_data
from mqtt_helper import mqtt_publish

####################################
# Do not modify code above this line

# Hier Ihr Code für Schritt 2 (s.h. unten)

# Do not modify code below this line
####################################

def publish(path_to_file: str) -> None:
    """Kette der Funktionsaufrufe:
    count_proc -> get_meta_data -> mqtt_publish
    - message: Rückgabewert von get_meta_data
    - user: Rückgabewert von get_current_path
    """
    counted = count_proc(path_to_file)
    meta = get_meta_data(counted)
    mqtt_publish(message=meta, user=get_current_path())


if __name__ == "__main__":
    try:
        publish("/proc/cpuinfo")
    except Exception as e:
        # Bei fehlender MQTT-Konfiguration o.ä. nur ausgeben
        print(f"Publish fehlgeschlagen: {e}")

```

#### Schritt 2

Erweitern Sie die Datei um die Funktion `def count_proc(path_to_file: str) -> str:`,
die die Anzahl der Prozessoren in einer Datei wie `/proc/cpuinfo` zählt,
die ermittelte Anzahl in der internern Variablen `DasIstEinTest456` zwischenspeichert
und als String zusammen mit dem aktuellen Pfad zurückgibt


Lösungshinweise:

- Der Übergabeparameters wird als Pfad zu einer Datei interpretiert die den gleichen Aufbau hat wie `/proc/cpuinfo`.
- `/proc/cpuinfo` enthält eine Liste mit Beschreibungen der Prozessoren bzw. Prozessorkerne im System.
    - Jeder Beschreibung eines Prozessors bzw. Prozessorkerns in der Liste startet mit der Zeile `processor : {id}`:
        - `{id}` ist ein Platzhalter für eine Zahl mit einer bis drei Stellen.
        - Der tatsächliche Wert von `{id}` enspricht dem Index des Prozessors bzw. Prozessorkerns im System.
        - Achtung: die Anzahl der Leerzeichen vor und nach `processor`, `:` und `{id}` kann variieren.
    - Beispiele für `/proc/cpuinfo`:
        - Beispieldateien mit diesem Aufbau sind im Unterverzeichnis `cpuinfo` des Übungsverzeichnisses abgelegt.
        - Sie können sich den Inhalt von `/proc/cpuinfo` auf diesem System mittels `cat /proc/cpuinfo` ausgeben lassen.
- Tipps/Lösungsansätze für das Zählen der Prozessoren bzw. Prozessorkerne:
    1. Zeilen die mit `processor` starten zählen.
    2. Die letzte Zeile mit `processor` finden und `{id}` + 1 rechnen.
- Tipps für das Erstellen des Rückgabewertes (String):
    - Beispiel für Implementierung: `str(DasIstEinTest456) + " " + str(get_current_path())`
    - Beispiele für erzeugten String: `12 /home/macur001/uebung/task2`, `4 /home/adlov001/uebung/task2`
- Beispiel für das Öffnen einer Datei:
  ```python
  with open("/path/to/file", "r") as f:
  lines = f.readlines()
  ```

#### Schritt 3

Führen die Anwendung (gegebener und entwickelter Python-Code) aus,
in dem Sie die Datei `count_and_publish.py` ausführen.








# 2. Aufgabe: Versionskontrolle und Testing (`task3`)


## 2.1 Eigener Branch und erster Commit

In diesem Schritt wird in einem Repository ein persönlicher Branch erzeugt und ein erster Commit erstellt.

1. Beantragen Sie Zugriff auf das Repository BCSM505/testatuebung25.
    - Öffnen Sie das Repository im Webbrowser via https://git.ide3.de/bcsm505/testatuebung25
    - Klicken Sie auf "Request Access" und beantragen Sie Zugriff auf das Repository.
    - Warten Sie bis Ihr Zugriff freigeschaltet wurde (melden Sie sich ggf. bei den Lehrpersonen)
2. Erstellen Sie im Repository BCSM505/testatuebung25 einen Branch mit Ihrem Login (Username) auf dem Sie gerade per SSH arbeiten.
    - Für den Branchnamen sollen nur Kleinbuchstaben verwendet werden.
3. Clonen Sie das Repository in das Verzeichnis `uebung/task3` in Ihrem Home-Verzeichnis.
4. Kopieren Sie die Inhalte aus `uebung/task2` in `uebung/task3` und erstellen Sie einen Commit mit diesen Inhalten.
    - Die Commit-Nachricht soll lauten: `Starting task3.`
5. Pushen Sie Ihre lokalen Änderungen und prüfen Sie:
    - Das im Repository in unserem GitLab der neue Branch _mit Ihrem Login_ existiert.
    - Der Inhalt des Ordners `uebung/task2` enthalten ist.




## 2.2 Testing und Zweiter Commit

In diesem Schritt wird der persönliche Branch um Tests für `count_and_publish.py` erweitert,
in dem die Abhängigkeiten zu anderen Python-Modulen aufgelöst werden und ein Testablauf mit `pytest` definiert wird.
Das Ergebnis wird als neuer Commit im persönlichen Branch gespeichert.


### 2.2.a Vorbereiteung für das Testen

1. Kopieren Sie das Script `test_start.sh` aus dem Verzeichnis `/opt/task3` in das Verzeichnis `uebung/task3`.
2. Erstellen Sie ein neues Verzeichnis `tests` im Verzeichnis `uebung/task3`.
    - Das neue Verzeichnis sollte unter diesem Pfad erreichbar sein: `~/uebung/task3/tests`
3. Wechseln Sie in das Verzeichnis `~/uebung/task3/tests`.


### 2.2.b Testen der `count_proc`-Funktion

Erstellen Sie im neuen Verzeichnis eine neue Datei: `test_count.py`

#### Geforderter Inhalt (Anforderungen):

- 2-3 sinnvolle Testfälle für die Funktion `count_proc` aus dem Modul `count_and_publish`.
- Die Tests basieren auf `pytest`.
- Nutzen Sie anstelle von `/proc/cpuinfo` eine Testdatei mit bekanntem und systemunabhängigem Inhalt.

#### Tipp (Lösungsvorschlag):

1. Importieren Sie das Modul `count_and_publish` als _Module-Under-Test_ via `import count_and_publish as mud`.
2. Referenzieren Sie `count_proc` über `mud` mittels `mud.count_proc`.
3. Testdateien für `/proc/cpuinfo` finden Sie im Repository BCSM505/testatuebung25.


### 2.2.c Testen der `publish`-Funktion (__optional__)

Erstellen Sie im neuen Verzeichnis eine neue Datei: `test_publish.py`

#### Geforderter Inhalt (Anforderungen):

- 2-3 sinnvolle Testfälle für die Funktion `publish` aus dem Modul `count_and_publish`.
- Auf pytest-Monkeypatch basierende Mocks für die Module `meta_helper`, `mqtt_helper` und `get_current_path`.
- Die Tests basieren auf `pytest`.

#### Tipp (Lösungsvorschlag):

1. Importieren Sie das Modul `count_and_publish` als _Module-Under-Test_ via `import count_and_publish as mud`.
2. Referenzieren Sie `publish` über `mud` mittels `mud.publish`.
3. Referenzieren Sie die zu mockenden Funktionen auf die gleiche Weise wie `publish`.


### 2.2.d Commit

Erzeugen Sie einen neuen Commit der den Code für das Testing beinhaltet.




## 2.3 Continuous Testing

Erstellen Sie für Ihren Branch eine Pipeline mit einer Stage, die mit jedem neuen Commit die Tests ausführt (per `script`).

Im Repository liegt eine Beispiel `.gitlab-ci.yml`, diese können Sie löschen, leeren und als Vorlage benutzen.

Hinweis: Mit dem Repository ist kein Runner verbunden, d.h. die Pipeline wird nicht ausgeführt.








# 3. Abschluss

Stellen Sie sicher, dass Ihr Branch auf unserem GitLab (Remote) und in Ihrem Home-Verzeichnis (Local) synchronisiert sind und über den gleichen Stand verfügen.
















-----------------------------

4. ![](../../Attachments/Pasted%20image%2020251030144815.png)


BEFEHLE
chmod 777  oder chmod +x
cp -r /opt/task2/ ./task2 ::::copy folder 

ipyhton3 hello.py cedoh001 - hier als input für sys.argv



SCHRITT 2
```python
import re
from info_helper import get_current_path, get_meta_data
from mqtt_helper import mqtt_publish

####################################
# Do not modify code above this line

def count_proc(path_to_file:str) -> str:
    lastid = 0
    with open(path_to_file, "r") as f:
        lines = f.readlines()
        for l in lines:
            if l.startswith("processor"):
                lastid = int(l.split(":")[1].strip())

    lastid+= 1
    return str(lastid) + " " + str(get_current_path())




# Do not modify code below this line
####################################

def publish(path_to_file: str) -> None:
    """Kette der Funktionsaufrufe:
    count_proc -> get_meta_data -> mqtt_publish
    - message: Rückgabewert von get_meta_data
    - user: Rückgabewert von get_current_path
    """
    counted = count_proc(path_to_file)
    meta = get_meta_data(counted)
    mqtt_publish(message=meta, user=get_current_path())


if __name__ == "__main__":
    try:
        publish("/proc/cpuinfo")
    except Exception as e:
        # Bei fehlender MQTT-Konfiguration o.ä. nur ausgeben
        print(f"Publish fehlgeschlagen: {e}")

```


![](../../Attachments/Pasted%20image%2020251030195306.png)

dateien von einem verzeichnis in ein anderes kopieren

cp -a pfadzumverzeichnis/.         .





```python
import sys

# Einfach den vollständigen Pfad zum Ordner 'task3' hart codieren
task3_path = "/home/cedoh001/uebung/task3" # Passe diesen Pfad an!

if task3_path not in sys.path:
    sys.path.insert(0, task3_path)

import info_helper as ih
import count_and_publish as mud

def test_count_and_publish2():
    assert mud.count_proc("../cpuinfo/cpuinfo_2") == "2" + " " + str(ih.get_current_path())

def test_count_and_publish4():
    assert mud.count_proc("../cpuinfo/cpuinfo_4") == "4" + " " + str(ih.get_current_path())

def test_count_and_publish12():
    assert mud.count_proc("../cpuinfo/cpuinfo_12") == "12" + " " + str(ih.get_current_path())
```



```python
import sys
import os
import pytest  # Importiere pytest, um pytest.raises zu verwenden

# --- Import-Setup ---
# Stelle sicher, dass Python das 'count_and_publish'-Modul finden kann.
task3_path = "/home/cedoh001/uebung/task3"
if task3_path not in sys.path:
    sys.path.insert(0, task3_path)

import count_and_publish as mud

# --- Testvorbereitung ---
def create_test_cpuinfo_file(tmp_path, processor_id):
    """Erstellt eine temporäre cpuinfo-Datei mit einer Prozessor-ID."""
    cpuinfo_file = tmp_path / "test_cpuinfo"
    with open(cpuinfo_file, "w") as f:
        f.write(f"processor: {processor_id}\n")
    return str(cpuinfo_file)


# --- Testfälle für die 'publish'-Funktion ---

def test_publish_calls_dependencies_correctly(monkeypatch, tmp_path):
    """
    Testfall 1: Überprüft, ob 'publish' seine internen Funktionen
    in der richtigen Reihenfolge und mit den korrekten Werten aufruft.
    """
    # 1. Vorbereitung (Arrange)
    call_order = []
    test_file_path = create_test_cpuinfo_file(tmp_path, 7)

    # Definiere Mock-Funktionen mit korrekten Signaturen
    def mock_get_meta_data(counted_value): # KORRIGIERT: Akzeptiert ein Argument
        call_order.append("get_meta_data")
        # Optional, aber gut: Prüfe, ob der korrekte Wert von count_proc ankommt
        assert counted_value == "8 /fake/path"
        return {"id": "test-meta-123"}

    def mock_mqtt_publish(message, user):
        call_order.append("mqtt_publish")
        assert message == {"id": "test-meta-123"}
        assert user == "/fake/path"

    def mock_get_current_path():
        call_order.append("get_current_path")
        return "/fake/path"

    # 2. Anwenden der Mocks
    monkeypatch.setattr(mud, 'get_meta_data', mock_get_meta_data)
    monkeypatch.setattr(mud, 'mqtt_publish', mock_mqtt_publish)
    monkeypatch.setattr(mud, 'get_current_path', mock_get_current_path)

    # 3. Aktion (Act)
    mud.publish(test_file_path)

    # 4. Überprüfung (Assert)
    assert call_order == ["get_current_path", "get_meta_data", "get_current_path", "mqtt_publish"]


def test_publish_raises_file_not_found_when_file_missing(monkeypatch):
    """
    Testfall 2 (NEU): Überprüft, ob 'publish' einen FileNotFoundError auslöst,
    wenn die angegebene Datei nicht existiert, da count_proc diesen Fehler nicht fängt.
    """
    # 1. Vorbereitung (Arrange)
    # Wir müssen nichts mocken, da der Fehler VOR den Mocks in count_proc auftritt.
    # Wir könnten die Mocks trotzdem definieren, um sicherzustellen, dass sie NICHT aufgerufen werden,
    # aber für diesen Test ist das nicht zwingend notwendig.

    # 2. Aktion & Überprüfung (Act & Assert)
    # Wir verwenden pytest.raises als Kontextmanager. Der Test ist erfolgreich,
    # wenn der Code *innerhalb* dieses Blocks einen FileNotFoundError auslöst.
    with pytest.raises(FileNotFoundError):
        mud.publish("/path/that/definitely/does/not/exist.txt")

    # Nach diesem Block können wir sicher sein, dass der erwartete Fehler aufgetreten ist.
    # Es gibt keine weiteren Asserts, da der erfolgreiche Abschluss des 'with'-Blocks der Test ist.


# Optional: Ein dritter Testfall, um sicherzustellen, dass die Mocks
# NICHT aufgerufen werden, wenn der Fehler auftritt.
def test_publish_does_not_call_helpers_on_file_not_found(monkeypatch):
    """
    Testfall 3 (Optional, aber gut): Bestätigt, dass get_meta_data und mqtt_publish
    NICHT aufgerufen werden, wenn ein FileNotFoundError auftritt.
    """
    # 1. Vorbereitung (Arrange)
    # Zähler, um zu sehen, wie oft die Mocks aufgerufen werden
    meta_data_calls = 0
    mqtt_publish_calls = 0

    def mock_get_meta_data(counted_value):
        nonlocal meta_data_calls
        meta_data_calls += 1

    def mock_mqtt_publish(message, user):
        nonlocal mqtt_publish_calls
        mqtt_publish_calls += 1

    # 2. Anwenden der Mocks
    monkeypatch.setattr(mud, 'get_meta_data', mock_get_meta_data)
    monkeypatch.setattr(mud, 'mqtt_publish', mock_mqtt_publish)

    # 3. Aktion & Überprüfung
    with pytest.raises(FileNotFoundError):
        mud.publish("/another/non/existent/path.txt")

    # 4. Zusätzliche Überprüfung
    # Stelle sicher, dass die Zähler immer noch bei 0 sind.
    assert meta_data_calls == 0
    assert mqtt_publish_calls == 0
```
