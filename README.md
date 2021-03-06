# keycloak-export

You can deploy as a module by running:

    $KEYCLOAK_HOME/bin/jboss-cli.sh --command="module add --name=io.cloudtrust.keycloak-export --resources=target/keycloak-export-0.1-SNAPSHOT.jar --dependencies=org.keycloak.keycloak-core,org.keycloak.keycloak-server-spi,org.keycloak.keycloak-server-spi-private,org.keycloak.keycloak-services,javax.ws.rs.api"

Then registering the provider by editing `standalone/configuration/standalone.xml` and adding the module to the providers element:

    <providers>
        ...
        <provider>module:io.cloudtrust.keycloak-export</provider>
    </providers>

Then start (or restart) the server. Once started open http://localhost:8080/auth/realms/master/export/realm and you should see a json with the exported content.
You can also invoke the endpoint for other realms by replacing `master` with the realm name in the above url.

To use this module, the client (i.e. admin-cli) must have full scope allowed in the master realm.

## Testing

For running the tests for this export module, you need to have a separate Keycloak server running on `localhost` with the following characteristics:
* HTTP Port: `8180`
* HTTP Management Port: `10090`
* Admin user: `admin` / `admin`