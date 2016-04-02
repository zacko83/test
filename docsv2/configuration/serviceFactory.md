---
layout: docs-default
---

# Service Factory

IdentityServer3 contains many features for implementing OpenID Connect and OAuth2. Many of these features have been designed so they can be replaced. This would be useful for the scenarios where the default logic doesn’t match the hosting application’s requirements, or simply the application wishes to provide an entirely different implementation. And in fact, there are some extensibility points within IdentityServer3 that are required to be provided by the hosting application (such as the storage for configuration data or the identity management implementation for validating users’ credentials).

The `IdentityServer3.Core.Configuration.IdentityServerServiceFactory` holds all these building blocks and must be supplied at startup time using the `IdentityServerOptions` class (see [here](http://identityserver.github.io/Documentation/docs/configuration/identityServerOptions.html) for more information on configuration options).

The extensibility points fall into three categories.

## Mandatory

* `UserService`
    * Implements user authentication against the local user store, association of external users, claims retrieval and sign-out logic.
    There are two standard implementations for [MembershipReboot](https://github.com/thinktecture/Thinktecture.IdentityServer.v3.MembershipReboot)
    and [ASP.NET Identity](https://github.com/thinktecture/Thinktecture.IdentityServer.v3.AspNetIdentity)
* `ScopeStore`
    * Implements retrieval of scopes configuration data
* `ClientStore`
    * Implements retrieval of client configuration data

The `IdentityServerServiceFactory` allows setting up a service factory by providing in-memory stores for users, clients and scopes (see [here](inMemory.html)).

## Mandatory for production scenarios (but with default in-memory implementations)

* `AuthorizationCodeStore`
    * Implements storage and retrieval of authorization codes ([interface](https://github.com/thinktecture/Thinktecture.IdentityServer.v3/blob/master/source%2FCore%2FServices%2FITransientDataRepository.cs))
* `TokenHandleStore` 
    * Implements storage and retrieval of handles for reference tokens ([interface](https://github.com/thinktecture/Thinktecture.IdentityServer.v3/blob/master/source%2FCore%2FServices%2FITransientDataRepository.cs))
* `RefreshTokenStore` 
    * Implements storage and retrieval of refresh tokens ([interface](https://github.com/thinktecture/Thinktecture.IdentityServer.v3/blob/master/source%2FCore%2FServices%2FITransientDataRepository.cs))
* `ConsentStore` 
    * Implements storage and retrieval of consent decisions ([interface](https://github.com/thinktecture/Thinktecture.IdentityServer.v3/blob/master/source/Core/Services/IConsentStore.cs))
* `ViewService`
    * Implements retrieval of UI assets. Defaults to using the embedded assets. ([interface](https://github.com/thinktecture/Thinktecture.IdentityServer.v3/blob/master/source%2FCore%2FServices%2FIViewService.cs))

## Optional (can be replaced, but have default implementations)

* `TokenService`
    * Implements creation of identity and access tokens ([interface](https://github.com/thinktecture/Thinktecture.IdentityServer.v3/blob/master/source%2FCore%2FServices%2FITokenService.cs))
* `ClaimsProvider`
    * Implements retrieval of claims for identity and access tokens ([interface](https://github.com/thinktecture/Thinktecture.IdentityServer.v3/blob/master/source%2FCore%2FServices%2FIClaimsProvider.cs))
* `TokenSigningService`
    * Implements creation and signing of security tokens ([interface](https://github.com/thinktecture/Thinktecture.IdentityServer.v3/blob/master/source%2FCore%2FServices%2FITokenSigningService.cs))
* `CustomGrantValidator`
    * Implements validation of custom grant types ([interface](https://github.com/thinktecture/Thinktecture.IdentityServer.v3/blob/master/source%2FCore%2FServices%2FICustomGrantValidator.cs))
* `CustomRequestValidator`
    * Implements custom additional validation of authorize and token requests ([interface](https://github.com/thinktecture/Thinktecture.IdentityServer.v3/blob/master/source%2FCore%2FServices%2FICustomRequestValidator.cs))
* `RefreshTokenService`
    * Implements creation and updates of refresh tokens ([interface](https://github.com/thinktecture/Thinktecture.IdentityServer.v3/blob/master/source%2FCore%2FServices%2FIRefreshTokenService.cs))
* `ExternalClaimsFilter`
    * Implements filtering and transformation of claims for external identity providers ([interface](https://github.com/thinktecture/Thinktecture.IdentityServer.v3/blob/master/source%2FCore%2FServices%2FIExternalClaimsFilter.cs))
* `CustomTokenValidator`
    * Implements custom additional validation of tokens for the token validation endpoints ([interface](https://github.com/thinktecture/Thinktecture.IdentityServer.v3/blob/master/source%2FCore%2FServices%2FICustomTokenValidator.cs))
* `CustomTokenResponseGenerator`
    * Allows adding additional data to a token response [interface](https://github.com/IdentityServer/IdentityServer3/blob/dev/source/Core/Services/ICustomTokenResponseGenerator.cs)
* `ConsentService` 
    * Implements logic of consent decisions ([interface](https://github.com/thinktecture/Thinktecture.IdentityServer.v3/blob/master/source/Core/Services/IConsentService.cs))
* `ClientPermissionsService`
    * Implements retrieval and revocation of consents, reference and refresh tokens ([interface](https://github.com/thinktecture/Thinktecture.IdentityServer.v3/blob/master/source%2FCore%2FServices%2FIClientPermissionsService.cs))
* `EventService`
    * Implements forwarding events to some logging system (e.g. elastic search) ([interface](https://github.com/thinktecture/Thinktecture.IdentityServer.v3/blob/master/source%2FCore%2FServices%2FIEventService.cs))
* `RedirectUriValidator`
    * Implements validation of redirect and post logout URIs ([interface](https://github.com/thinktecture/Thinktecture.IdentityServer.v3/blob/master/source%2FCore%2FServices%2FIRedirectUriValidator.cs))
* `LocalizationService`
    * Implements localization of display strings ([interface](https://github.com/thinktecture/Thinktecture.IdentityServer.v3/blob/master/source%2FCore%2FServices%2FILocalizationService.cs))
* `CorsPolicyService`
    * Implements CORS policy ([interface](https://github.com/thinktecture/Thinktecture.IdentityServer.v3/blob/master/source%2FCore%2FServices%2FICorsPolicyService.cs))


See [here](../advanced/customServices.html) for more information on registering your custom service and store implementations.
