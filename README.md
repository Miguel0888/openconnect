# OpenConnect - GitLab-Fork fuer Java/JNI-Wrapper

Dieses Repository ist ein Fork/Mirror des offiziellen OpenConnect-Repositories auf GitLab:

- Upstream: https://gitlab.com/openconnect/openconnect

Die eigentliche Entwicklung des OpenConnect-VPN-Clients findet weiterhin auf GitLab statt. Dieses GitHub-Repo dient vor allem dazu, den Java/JNI-Wrapper (openconnect-wrapper) zu bauen und als Artefakt z. B. ueber GitHub Packages in Java-Projekten wiederverwenden zu koennen.

Lizenzhinweis: OpenConnect steht unter der LGPL 2.1. Die Lizenzbedingungen des Upstreams gelten auch fuer diesen Fork. Dies ist kein offizielles OpenConnect-Release.

## Zweck dieses Forks

- Bau der nativen JNI-Library openconnect-wrapper (z. B. openconnect-wrapper.dll / libopenconnect-wrapper.so).
- Bau eines Java-JARs mit den Klassen aus java/src/org/infradead/libopenconnect.
- Veroeffentlichung dieser Artefakte z. B. in GitHub Packages, damit sie in Java-Projekten als Maven- oder Gradle-Dependency genutzt werden koennen.

Die eigentliche C-Bibliothek libopenconnect und der CLI-Client gehoeren weiterhin zum Upstream-Projekt; dieser Fork konzentriert sich auf Build- und Packaging-Aspekte fuer Java.

## Upstream-Updates aus GitLab einziehen

Remotes sind typischerweise so konfiguriert:

```bash
git remote -v
# origin   https://github.com/Miguel0888/openconnect.git (fetch)
# origin   https://github.com/Miguel0888/openconnect.git (push)
# upstream https://gitlab.com/openconnect/openconnect.git (fetch)
# upstream https://gitlab.com/openconnect/openconnect.git (push)
```

### 1. Neueste Aenderungen vom Upstream holen

```bash
git fetch upstream
git fetch upstream --tags
```

### 2. Lokalen Branch aktualisieren

```bash
git checkout master
git merge upstream/master
# alternativ:
# git rebase upstream/master
```

### 3. Mirror nach GitHub pushen

```bash
git push origin master
git push origin --tags
```

Damit bleibt dieses GitHub-Repository eng am offiziellen Upstream ausgerichtet.

## Nutzung des Java/JNI-Wrappers (Ueberblick)

Im Verzeichnis java/ befindet sich ein JNI-Interface-Layer fuer libopenconnect sowie Beispielcode (LibTest).

Typischer Build-Ablauf (vereinfacht):

```bash
./autogen.sh
./configure --with-java
make
cd java
ant
```

Danach befinden sich in ..libs die nativen Libraries (z. B. openconnect-wrapper.dll / libopenconnect-wrapper.so) und in java/dist das Java-JAR.

Vor der Verwendung von LibOpenConnect muss die native Library geladen sein, z. B. ueber java.library.path oder einen eigenen Loader, der die DLL oder SO aus einem JAR entpackt und per System.load aufruft.

## Original-Dokumentation

Die vollstaendige Dokumentation (Features, Protokolle, Installationsanleitungen usw.) befindet sich weiterhin im Upstream-Repository und auf der Projekt-Webseite:

- Upstream-Repo (GitLab): https://gitlab.com/openconnect/openconnect
- Projektseite: https://www.infradead.org/openconnect/

Dieses GitHub-Repository fokussiert sich primaer auf den Java/JNI-Wrapper und die Integration in Java-Build- und Releaseprozesse.