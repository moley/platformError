#Bug scenario

We have the problem that in a special combination of platforms which extend each other we run in a bug, which is
an error in resolving dependencies.

stamm-platform is released once and be used in guirecherche.
stamm-platform is released again and be used in guistamm.
Afterwards guistamm is released and used in guirecherche.

So guirecherche has an old version of stamm directly and a newer version of stamm transitive through guistamm.
After replacing the old version in guirecherche-platform directly with the newer one the dependency resolution would work


# Reproducing
I have added a docker-compose to setup a local artifactory OSS instance. To reproduce do the following:

* Call docker-compose up to setup this server
* Step to http://localhost/artifactory/webapp/#/home in your browser
* Step through the wizard and add a maven repository
* Configure anonymous to be able to upload any local repo via (Admin... / Users -> Anything -> Users -> Enable "Deploy/Cache")
* Call ./gradlew resolveDependenciesGuiRechercheFails in the root project to build all the releases and recieve the exception
* Call ./gradlew resolveDependenciesGuiRechercheOk in the root project to build all the releases and recieve the exception
