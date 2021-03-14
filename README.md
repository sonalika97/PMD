@@ -23,20 +23,20 @@ function maven_dependencies_resolve() {
    # build first the modules, that have dependencies between themselves
    # first build pmd-lang-test, pmd-test and pmd-core - used by all modules
    ./mvnw clean install -pl pmd-core,pmd-test,pmd-lang-test -DskipTests -Dpmd.skip=true \
           --no-transfer-progress -Dcheckstyle.skip=true -Dmaven.javadoc.skip=true -Dmaven.source.skip=true
           -B -Dcheckstyle.skip=true -Dmaven.javadoc.skip=true -Dmaven.source.skip=true
    # then build dependencies for pmd-visualforce needs: pmd-apex->pmd-apex-jorje+pmd-test+pmd-core
    ./mvnw clean install -pl pmd-core,pmd-test,pmd-lang-test,pmd-apex-jorje,pmd-apex -DskipTests -Dpmd.skip=true \
           --no-transfer-progress -Dcheckstyle.skip=true -Dmaven.javadoc.skip=true -Dmaven.source.skip=true
           -B -Dcheckstyle.skip=true -Dmaven.javadoc.skip=true -Dmaven.source.skip=true

    # the resolve most other projects. The excluded projects depend on other projects in the reactor, which is not
    # completely built yet, so these are excluded.
    ./mvnw dependency:resolve -pl '!pmd-dist,!pmd-java8,!pmd-doc,!pmd-scala'  -Dsilent --no-transfer-progress
    ./mvnw dependency:resolve -pl '!pmd-dist,!pmd-java8,!pmd-doc,!pmd-scala'  -Dsilent -B

    ./mvnw dependency:get --no-transfer-progress -Dsilent \
    ./mvnw dependency:get -B -Dsilent \
           -DgroupId=org.jetbrains.dokka \
           -DartifactId=dokka-maven-plugin \
           -Dversion=${dokka_version} \
           -Dpackaging=jar \
           -DremoteRepositories=jcenter::default::https://jcenter.bintray.com/
    ./mvnw dependency:resolve-plugins --no-transfer-progress -Dsilent -DexcludeGroupIds=org.jetbrains.dokka -Psign
    ./mvnw dependency:resolve-plugins -B -Dsilent -DexcludeGroupIds=org.jetbrains.dokka -Psign
}
