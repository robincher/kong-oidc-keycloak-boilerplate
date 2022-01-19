# Introduction

Boilerplate for Kong OIDC and KeyCloak.

This repo will show the samples to baked a base Kong image with the **Open-Source** OIDC Plugin maintained by revomatico, and some sample Kubernetes deployment manifest for Kong and KeyCloak 

## Building and Publishing

Steps to build and publish the container with base Kong Image

```
# Build the container with any new changes
docker build -t <<private-registry>>/kong-oidc:<tag> -f Dockerfile . 

# Run the container in detached mode
docker run -d --name kong-oidc <<private-registry>>/kong-oidc:<tag>       

# Pushing the container image to a registry
docker push <<private-registry>>/kong-oidc:<tag>   
```

## Understanding the Kong Plugins

To enjoy features by Kong API Gateway with its Ingress controller, we need to consider the following Kong Plugins.

1. **odic** - This plugin is used to communicate with the Keycloak Identity provider and is required if you'd like to enable (recommended) SSO for your ingress.

2. **request-transformer** - To strip off unnecessary headers upon authentication with the identity platform

3. **cors** - Allow cors at global level

# KeyCloak Configuration Overview

1. Add a new Kong Realm
2. Create a new Kong Client in the realm , eg kong-oidc, and make the necessary changes

3. Go to **Clients**, and then click on **Settings**. Make the following changes:

Access Type: **Confidential**
Valid Redirect URIs: *
Web Origin: **localhost** (Allowed CORS origin)

3. Retrieve Client ID, and then go to **Credentials** to get the **Secret** value.
4. Retrieve OpenID Endpoint Configuration for the discovery path
4. Passed the values to the oidc crds parameters **discovery**, **client_id** and **client_secret**

## Credits

- [Wee Liang - DevOps Engineer @ Thales Airlab](https://www.linkedin.com/in/angweeliang)
- [Arun - DevOps & Integration # Thales Airlab](https://www.linkedin.com/in/arunsudhakar)
- [Kelvin - Software Engineer @ Thales Airlab](https://www.linkedin.com/in/kelvin-neo)

## License

MIT © [Robin Cher](LICENSE)

## References

- [Revomatico OIDC Plugin](https://github.com/revomatico/kong-oidc)