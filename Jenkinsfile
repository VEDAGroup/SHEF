pipeline {

/*
    Jenkinsfile für das Projekt "SHEF"

    Maven Goals: clean verify -U -Dorg.slf4j.simpleLogger.defaultLogLevel=warn
    Tools: Maven 3.9.14, Azul Java 17 ( LTS) JDK + Java FX 17
    Gesperrte Ressourcen: AllVariants_ITest_Trunk

    Hinweise zu den mvn Parametern:
    -U --update-snapshots Forces a check for updated releases and snapshots on remote repositories
    -Dorg.slf4j.simpleLogger.defaultLogLevel=warn Setzt das Log-Level auf warn (reduzierte Ausgabe)

    Ziel dieser Pipeline: Entwicklern zeitnah Feedback über fehlschlagende Tests zu geben. Es erfolgt kein deploy.
*/

    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '4', artifactNumToKeepStr: '4'))

        disableConcurrentBuilds abortPrevious: true
    }

    tools {
        maven 'Maven 3.9.14'
        jdk 'Azul Java 17 ( LTS) JDK + Java FX 17'
    }

    stages {
        stage('Build') {

            steps {

                withMaven {
                    bat "mvn clean verify -U -Dorg.slf4j.simpleLogger.defaultLogLevel=warn"
                }
            }

            post {
                always {
                    // Sende E-Mails an Entwickler und Auslöser des Builds
                    emailext subject: '$DEFAULT_SUBJECT',
                            body: '$DEFAULT_CONTENT',
                            from: 'noreply@bil-ci.veda.de',
                            // Die explizite Angabe einer to: Adresse kann weggelassen werden, unter der Annahme, 
                            // dass es (mindestens) einen developer oder einen requestor gibt.
                            // Mail an Developer (Author der Änderung) / Auslöser des Builds senden:
                            recipientProviders: [culprits(), developers(), requestor()]
                }
            }
        }
    }
}
