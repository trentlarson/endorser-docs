
Server Overview
===============

The server holds a log of signed claims. That is it's main purpose; other functions are for convenience or for features that are temporary while full P2P features are implemented.

This service is not good for totally private claims. (Try Mastodon or Nostr or ACDCs.)

* Use `/api/claim <https://test.endorser.ch:8000/api-docs/#/claim>`_ endpoints to record and retrieve claims, via standard REST.

  * To `POST <https://test.endorser.ch:8000/api-docs/#/claim/post_api_claim>`_ a claim, it must be signed and sent in a JWT; the body looks like this: ``{ "jwtEncoded" : "{JWT}" }``

  * All other endpoints have various levels of permissions based on the signed DID (`"Decentralized IDentifier" <https://www.w3.org/TR/did-core/>`_). Send an ``Authorization`` HTTP header with a ``Bearer {JWT}`` token to retrieve full sets of data later.

  * All claim payloads are expected to be in `JSON-LD <https://json-ld.org/>`_ format, which basically means that there are two properties: ``@context`` and ``@type``.

    * As shown in pages like `transactions <transactions>`_, we typically recommend `schema.org <https://schema.org>`_ as templates for claim data.

  * To `retrieve claims, use GET <https://test.endorser.ch:8000/api-docs/#/claim/get_api_claim>`_ to get the original claim in a ``claim`` field along with some other fields such as the server ID, date issued, etc. An example is available directly in a browser (though much data will be hidden): `https://test.endorser.ch:8000/api/claim <https://test.endorser.ch:8000/api/claim>`_

    * One can only see personally identifiable IDs if the creator has made a claim about them or explicitly allowed them visibility.

  * `/api/v2/report <https://test.endorser.ch:8000/api-docs/#/reportAll>`_ endpoints (and the older `/api/report <https://test.endorser.ch:8000/api-docs/#/report>`_ endpoints) do more targeted retrievals of claims.

    * Besides generic reports, there are ways to retrieve well-known types of claims: `actions <https://test.endorser.ch:8000/api-docs/#/action>`_, `events <https://test.endorser.ch:8000/api-docs/#/event>`_, `plans and projects <https://test.endorser.ch:8000/api-docs/#/project>`_, `tenure <https://test.endorser.ch:8000/api-docs/#/tenure>`_

      * These well-known claims retrieve a different format than the generic "claims" reports: they don't have an embedded "claim" with the details because all the details are at the top level.

      * For example, a `PlanAction <https://schema.org/PlanAction>`_ can be retrieved via `/api/plan/{HANDLE_ID} <http://localhost:3000/api-docs/#/project/get_api_plan__id_>`_ where the ``HANDLE_ID`` is the value of the permanent ``handleId`` of the original plan claim. A handle ID can be supplied by the original recorder; if not supplied then the system will generate one.

      * Note that the handle ID can be used as an editing mechanism: whenever a claim has an ``identifier`` property, the handle ID can be used to retrieve the latest version with that identifier.

  * All data (including source claims) are filtered such that fields with DIDs are hidden if the originator has not allowed visibility.

* The server maintains control of visibility for users via the `network <https://test.endorser.ch:8000/api-docs/#/network>`_ endpoints.

  * When someone makes a claim about someone else, their DID is automatically made visible to the subject of the claim.

  * One can explicitly make themselves visible or invisible to other DID holders, eg. with `canSeeMe <https://test.endorser.ch:8000/api-docs/#/network/post_api_report_canSeeMe>`_

* The server maintains some other data for other purposes.

  * The ability to make claims (and onboard others) is controlled by registrations.

    * These are sent as `RegisterAction <https://schema.org/RegisterAction>`_ claims with requester as ``agent``, target as ``participant``, and the ``object`` as the value ``"endorser.ch"``.

  * Merkle hashes of data are maintained for later proof.

