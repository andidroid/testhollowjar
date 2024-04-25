https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/8-beta/html/using_single_sign-on_with_jboss_eap/con_openid-connect-configuration-in-jboss-eap_default

oidc.json:
{
"client-id" : "customer-portal", 1
"provider-url" : "http://localhost:8180/auth/realms/demo", 2
"ssl-required" : "external", 3
"credentials" : {
"secret" : "234234-234234-234234" 4
}
}

<subsystem xmlns="urn:wildfly:elytron-oidc-client:1.0">
    <secure-deployment name="DEPLOYMENT_RUNTIME_NAME.war"> 
        <client-id>customer-portal</client-id> 
        <provider-url>http://localhost:8180/auth/realms/demo</provider-url> 
        <ssl-required>external</ssl-required> 
        <credential name="secret" secret="0aa31d98-e0aa-404c-b6e0-e771dba1e798" /> 
    </secure-deployment>
</subsystem>

<subsystem xmlns="urn:wildfly:elytron-oidc-client:1.0">
    <provider name="${OpenID_provider_name}">
        <provider-url>http://localhost:8080/auth/realms/demo</provider-url>
        <ssl-required>external</ssl-required>
    </provider>
    <secure-deployment name="customer-portal.war"> 1
        <provider>${OpenID_provider_name}</provider>
        <client-id>customer-portal</client-id>
        <credential name="secret" secret="0aa31d98-e0aa-404c-b6e0-e771dba1e798" />
    </secure-deployment>
    <secure-deployment name="product-portal.war"> 2
        <provider>${OpenID_provider_name}</provider>
        <client-id>product-portal</client-id>
        <credential name="secret" secret="0aa31d98-e0aa-404c-b6e0-e771dba1e798" />
    </secure-deployment>
</subsystem>
