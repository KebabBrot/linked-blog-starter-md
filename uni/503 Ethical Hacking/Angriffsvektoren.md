Die Hauptursache für HTTP Request Smuggling (HRS) Schwachstellen liegt tatsächlich oft darin, dass die HTTP/1-Spezifikation **zwei verschiedene Methoden** zur Angabe des Endes einer Anfrage bietet: den **`Content-Length`**-Header und den **`Transfer-Encoding`**-Header. Wenn Front-End- und Back-End-Systeme in Bezug auf diese Header uneins sind, können Request-Grenzen falsch interpretiert werden.

Basierend auf den Quellen, insbesondere dem wissenschaftlichen Papier, das HRS systematisch untersucht, gibt es jedoch eine Vielzahl weiterer Ursachen, die zu Verarbeitungsdiskrepanzen führen können, sowie fortgeschrittene Angriffsvarianten und Präventionsmöglichkeiten.

### 1. Weitere Ursachen und Angriffsvektoren aus der wissenschaftlichen Studie

Das Forschungspapier zeigt, dass HRS ein komplexes Systeminteraktionsproblem ist, bei dem Diskrepanzen entstehen können, selbst wenn die einzelnen Komponenten nicht fehlerhaft sind. Die Autoren haben mithilfe von Differential Fuzzing systematisch nach Schwachstellen gesucht, die durch Manipulation von Anfrageteilen jenseits der bekannten Header entstehen.

Die Ergebnisse der Studie zeigen, dass Angriffe durch die Manipulation **jedes Teils einer Anfrage** ausgelöst werden können.

#### A. Manipulation der Request Line (Anfragezeile)
Diskrepanzen können durch Modifikationen an der Request Line (die Methode, URI und Protokollversion enthält) hervorgerufen werden. Erfolgreiche Kategorien, die zu HRS führten, umfassten:

*   **Mangled Method (Veränderte Methode):** Hierbei wird der Methodenname modifiziert, etwa durch Ändern der Groß-/Kleinschreibung oder Ersetzen des gesamten Methodennamens.
*   **Distorted Protocol (Verzerrtes Protokoll):** Zum Beispiel das Ersetzen eines Zeichens im Protokollnamen oder das Ändern der Groß-/Kleinschreibung eines bestehenden Buchstabens.
*   **Invalid Version (Ungültige Version):** Hinzufügen oder Ersetzen von Ziffern in der Versionsnummer, sodass diese ungültig, aber numerisch bleibt (z. B. `HTTP/1.19`).
*   **Manipulated Termination (Manipulierte Terminierung):** Hinzufügen eines Leerzeichens, eines Tabs oder eines weiteren CRLF vor dem terminierenden CRLF der Request Line.
*   **Embedded Request Lines (Eingebettete Anfragezeilen):** Einfügen einer vollständigen Request Line an verschiedenen Stellen innerhalb der bestehenden Request Line.
*   **Various Method Version Combinations (Verschiedene Methoden-Versions-Kombinationen):** Inkonsistentes Verhalten, das durch die Kombination bestimmter Methoden und Versionen ausgelöst wird, ohne dass Mutationen nötig sind.

#### B. Manipulation von HTTP-Headern (Jenseits von CL und TE)
Neben CL und TE können Diskrepanzen auch durch andere Header-Manipulationen entstehen, die die Boundary-Bestimmung beeinflussen:

*   **Distorted Header Value (Verzerrter Header-Wert):** Hinzufügen spezifischer Zeichen (z. B. vertikaler Tabulator, Leerzeichen oder Komma) zum Anfang oder Ende von Header-Werten.
*   **Manipulated Termination (Manipulierte Terminierung):** Einfügen eines Leerzeichens oder Tabs nach dem CRLF, das den Header terminiert, was zu Diskrepanzen führen kann.
*   **Expect Header:** Der Header `Expect: 100-continue` kann von verschiedenen Servern unterschiedlich interpretiert werden, wobei Apache beispielsweise den Body ignoriert.
*   **Identity Encoding:** Ein `Transfer-Encoding`-Header mit dem Wert `identity` wird von einigen Servern (Squid, ATS) ignoriert, während andere den Message Body parsen und weiterleiten.
*   **V1.0 Chunked Encoding:** Einige Server (z. B. Tomcat) unterstützen Chunked Encoding in HTTP Version 1.0 nicht, was zu Inkonsistenzen führt, wenn sowohl `Transfer-Encoding` als auch `Content-Length` vorhanden sind.
*   **Double Transfer-Encoding:** Das Vorhandensein von zwei `Transfer-Encoding`-Headern kann dazu führen, dass Server unterschiedliche Header zur Bestimmung der Nachrichtengrenze verwenden.

#### C. Manipulation des Request Body
Die Manipulation des Chunked Transfer Encodings im Request Body selbst kann zu Diskrepanzen führen. Erfolgreiche Angriffskategorien waren:

*   **Chunk-Size Chunk-Data Mismatch:** Die Größe der Chunk-Daten stimmt nicht mit der deklarierten Größe im Chunk Size überein.
*   **Manipulated Chunk-Size Termination:** Modifikation des CRLF, das die Chunk Size terminiert (z. B. durch Hinzufügen von Zeichen wie einem Semikolon oder Tabulator).
*   **Mangled Last-Chunk:** Entfernen oder Modifizieren des letzten Chunks (Größe null), der die Nachricht beendet.

### 2. Weitere Möglichkeiten (Fortgeschrittene Vektoren und Prävention)

Die Quellen nennen auch fortgeschrittene Techniken (Möglichkeiten für Angriffe) sowie Möglichkeiten zur Prävention dieser Schwachstellen.

#### A. Fortgeschrittene Angriffsvektoren (Advanced Request Smuggling)

*   **HTTP/2 Downgrading:** Obwohl HTTP/2 selbst inhärent immun gegen klassisches HRS ist, da es einen robusten Mechanismus zur Längenbestimmung verwendet, sind viele Webseiten anfällig, wenn ein HTTP/2-sprechender Front-End-Server Anfragen auf HTTP/1 für den Back-End-Server herabstufen muss (HTTP downgrading). Dies führt zu **H2.CL- und H2.TE-Schwachstellen**.
*   **Request Smuggling via CRLF Injection:** Dies beinhaltet die Injektion über Headernamen, die Bereitstellung eines **mehrdeutigen Hosts** oder **mehrdeutigen Pfades**, die Injektion einer vollständigen Request Line oder die Injektion von Newlines.
*   **Browser-Powered Request Smuggling (Client-Side Desync Attacks):** Diese Angriffe beruhen darauf, absichtlich falsch formatierte Requests zu senden, die den Browser eines Opfers dazu bringen, seine eigene Verbindung zur anfälligen Webseite zu vergiften. Dies funktioniert selbst bei Single-Server-Sites und nutzt möglicherweise normale `Content-Length`-Header, um die Desynchronisation zu erreichen.
*   **CL.0/H2.0-Schwachstellen:** Diese entstehen, weil einige Server fälschlicherweise annehmen, dass eine Anfrage keinen Body hat, wenn kein Längen-Header vorhanden ist.

#### B. Möglichkeiten zur Prävention von HTTP Request Smuggling

Um HRS-Schwachstellen zu verhindern, werden folgende Maßnahmen empfohlen, da diese entstehen, wenn Front-End- und Back-End-Server unterschiedliche Mechanismen zur Bestimmung der Request-Grenzen verwenden:

*   **HTTP/2 End-to-End verwenden:** Wenn möglich, sollte durchgängig HTTP/2 genutzt werden, da es aufgrund seines robusten Mechanismus zur Längenbestimmung einen **inhärenten Schutz gegen Request Smuggling** bietet.
*   **HTTP Downgrading vermeiden oder absichern:** Sollte das Downgrading von HTTP/2 auf HTTP/1 unvermeidbar sein, muss die umgeschriebene Anfrage gegen die HTTP/1.1-Spezifikation validiert werden. Beispielsweise sollten Anfragen abgelehnt werden, die Newlines in Headern, Doppelpunkte in Headernamen oder Leerzeichen in der Request-Methode enthalten.
*   **Umgang mit mehrdeutigen Anfragen:** Der Front-End-Server sollte mehrdeutige Anfragen **normalisieren**. Sollten Anfragen dennoch mehrdeutig bleiben, sollte der Back-End-Server diese **ablehnen** und die TCP-Verbindung dabei schließen.
*   **Annahmen über Request-Body vermeiden:** Die grundlegende Ursache für CL.0- und client-seitige Desync-Schwachstellen ist die Annahme, dass Anfragen keinen Body haben. Diese Annahme sollte vermieden werden.
*   **Verbindungsverwerfung bei Ausnahmen:** Standardmäßig sollte die Verbindung verworfen werden, wenn auf Server-Ebene Ausnahmen bei der Verarbeitung von Anfragen ausgelöst werden.