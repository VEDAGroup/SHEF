SHEF (VEDA Fork)
================

This is a fork of the Swing HTML Editor Framework SHEF from SourceForge (http://svn.code.sf.net/p/shef/code).

We need some improvements to the original component to avoid a NullPointerException that occurs in Java 7 when the editor is integrated into a JPanel.
We also need to add German translation for the dialogs shown by the component.

The project page of SHEF can be found on SourceForge: http://shef.sourceforge.net/
This project, as the original, is licensed under LGPL V2.1: http://www.gnu.org/licenses/lgpl-2.1

Key Facts
---------

- Maven coordinates: `net.veda:SHEF` (see `pom.xml` for the current version)
- Target: Java 8 bytecode. Builds with JDK 1.8 and with JDK 9+ (tested with JDK 17).
  On JDK 9+ the profile `jdk9+` sets `maven.compiler.release=8`, so the code is checked
  against the Java 8 API.
- Dependencies (from the VEDA Nexus, `https://nexus.dev.veda.net/repository/maven-public`):
  `net.sourceforge.shef:sam`, `net.sourceforge.shef:novaworx-syntax`, `org.hibernate:jtidy`.
  The jars in `lib/` are leftovers from the old NetBeans build and are not used by Maven.
- Translations: `messages*.properties` next to the sources (de, en_GB, es, fr, ja).
- Demo: `net.atlanticbb.tantlinger.shef.Demo`
- CI: `Jenkinsfile` runs `mvn clean verify` with Maven 3.9.14 and Azul JDK 17; it does not deploy.
  `distributionManagement` points to `repo.veda.de:8081` for releases and snapshots.

Build
-----

    mvn clean package

Resources in `src/main/resources` are filtered. Binary files whose extension is not in the
resources plugin's default non-filtered list (such as `Thumbs.db`) must be excluded, otherwise
filtering fails. No source encoding is set, so the build uses the platform encoding.
