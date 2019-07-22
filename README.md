# id-coop

A public description of the "Identity Cooperative" concept. Feedback encouraged!



Why the ID CoOp was Created
---------------------------


The "ID CoOp" was created to facilitate online access to people's own sensitive information such as healthcare and financial information. By providing a higher-level of "you are who you say you are", other systems who hold sensitive information (i.e. resource providers) can rely on the ID CoOp to assert a higher level of assurance of a person's identity.

When a person logs in or connects an application "ID CoOp", the application is informed about you and your identity assurance level.  How sure ID CoOp is, that "you are who you say you are" is categorized as a "identity assurance level" of either a `1`, `2`, or `3`).  These levels (`1`,`2`,`3`) are based on [NIST Digital Identity Guidelines SP 800-63-3](https://pages.nist.gov/800-63-3/sp800-63-3.html). Wen a person logs in or connects to the ID CoOp from another application, these "claims" (including name, etc.) are passed to applicationsin in a digitally signed electronic credential known as an ID token (`id_token`).  See  this [faq](https://openid.net/connect/faq/) form more info

High Level Concept of Operations
--------------------------------

The "ID CoOp" will provide a single sign-on service similar to Google OpenID Connect. ID CoOp shall provide an electronic credential bearing an identity assurance claim. Third party applications will function as "relying parties" and rely on the identity electronic credential.  Users who have been given the "ID referee badge" may verify the Identity of other users.  Users can be "agents" of Organizations. This models employer to employee (or contractor, etc.) relationships. These relationships are included in the user's electronic credential (`id_token`).


Raising a User's Identity Assurance Level (and claim)
-----------------------------------------------------


The `ial` claim can be changed from the default of `1` (untrusted) to `2` by adding documentation of an identity proofing event.  This can happen in multiple ways.


* Users in the "Tusted Referee" permission group can raise or lower other user's identity asurtance level. Adherence to our code of coduct is required. 
* Trusted applications can raise or lower other user's identity asurtance level via a RESTFul API.


Current Features in the ID CoOp
-------------------------------


The ID CoOP is based on open source open id connect provider "Verify My Identity" https://TransparentHealth/vmi.  Here is a partial list of some key features already available.


* Open ID Connect Core
* Open ID Connect Discovery
* NIST SP 800-63-3 IAL as `ial` claim in `id_token`
* NIST SP 800-63-3 AAL as `aal` claim in `id_token`
* SMS one-time-password multi-factor authentication. `aal`= `2` in `id_token`.
* FIDO U2F/2 multi-factor authentication. `aal`= `2` in `id_token`.
* Self-service user management interface including profile photo
* Identifiers can be added to user accounts. Can be anything such as an state or federal ID number, master patient index, etc./)
* Organization agent user interface 
* Organization setup administrative user interface. (i.e. add/remove individual agents from and Organization.)
* Organization agent user interface with user search. 
* Trusted referee user interface with user search.
* API trusted 3rd parties to provide identity assurance information. (effectively raise\lower a user’s `ial`)


Blue Sky Feature Wishlist 
-------------------------


The ID CoOP is based on open source open id connect provider "Verify My Identity" https://TransparentHealth/vmi.

(Yes you or your organization can commission the Transparent Health foundation to implement items on this list. )


* Remote ID proofing user interface
* OAuth 2.0 for Native Mobile Applications: https://tools.ietf.org/html/rfc8252 (Already done in BB 2.0 API. just move it over.)
* DOAuth 2.0 Dynamic Client Registration Protocol: https://tools.ietf.org/html/rfc7591)
* Application Proofing\Signing User Interface with tie to Dynamic Client Registration 
* Support for Google Authenticator as a form of 2nd factor authentication.
* Support for push notifications as a form of 2nd factor authentication. (preferred over SMS).

These next 3 are related....

* Document Signing and Publication interface. Consent Receipt Specification: https://kantarainitiative.org/confluence/display/infosharing/Consent+Receipt+Specification 
* Digital wallet public/private keypair for document signing and signature. A Mnemonic (list of words) will allow for a private key’s recovery.
* DNS for publication of public keys and signatures. DNS will provide both provenance and a distributed architecture. DNS is used of a blockchain. 



Rules for 3rd Party Applications (a.k.a. Relying Parties)
---------------------------------------------------------

* You must first sign up as an organization and register your application just like any other OAuth2/OpenID Connect application.  Pilot your application in our sandbox environment.
* If accessing sensitive information, such as protected personal health information (PHI), a client MUST rely on the identity claim in the OpenID Connect identity token (`id_token`).
* Your app must not grant access to one's own health information unless and IAL of `2` is established.
* You application must use https in production when calling any of our APIs.
* Your callback `redirect_uris` may not use `http` in production. `https` in production.
* For production access your application must be vetted.  We will give you a signed JWT (i.e JWS) as a badge that your application is approved.  This is also your application's "ticket" to dynamic client registration. Pass it in the header with your request when using the DynReg endpoint.
