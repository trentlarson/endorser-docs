
Intro to Community Credentials
==============================

Quick Start
-----------

  - See the `Tutorial Videos <https://endorser.ch/doc-tutorial>`_.

  - The mobile app is on `Google Play`_ and `Apple's App Store`_.

.. _`Google Play`: https://play.google.com/store/apps/details?id=ch.endorser.mobile
.. _`Apple's App Store`: https://apps.apple.com/us/app/endorser-mobile/id1556368693


Overview
--------

We support the growth of community networks at whatever level of privacy you prefer. Meta (AKA Facebook) has created an engaging user interface around networks but they control it all; Google allows more control but still has access to your data and shares it. Let's build networks where individuals have as much control as possible while still allowing discovery.

This is a set of projects to do just that, with the following features:

- Store & share standard data schemas, so that other tools can interoperate easily.

- Allow for local storage with optional sharing, all depending on your choices for openness and discovery.

Said more technically:

- Issue credentials about yourself and your community, easily & verifiably. This is done based on standards for Verifiable Credentials that use personal public & private keys, with apps to make the process as simple as possible.  Most other approaches assume mature, centralized credential authorities; there is a place for those, but there are even more uses for an evolving credential system based on existing networks.

- Share them, then search to network with people you know -- with permissions. When credentials are saved to our server, people may then see claims about others -- but only if allowed to see them. But there's one further possibility: if someone is two friends away, then your common friend can introduce you. This allows for discovery: although you may not have access to other people's claims, if you are linked by a contact then you can use other means to find that information, depending on the comfort level of your shared contact. This is all done [local-first](https://www.inkandswitch.com/local-first.html).


Scenarios
---------

  - Commit time or other resources (conditionally or unconditionally), then verify their follow-through. See :doc:`transactions`.

  - Find other people in your community with similar interests and even goals. See :doc:`discovery`.







Implementation
--------------

See the `Endorser home page <https://endorser.ch>`_ to install our app.

The goals of this implementation are as follows:

  - Create and show verifiable credentials about you, which are only revealed at your discretion.

    This is achieved with server-side permissions, only allowing access to verifiable credentials via requests signed in real-time.

  - Discover people with claims or credentials of interest, and potentially contact them.

    This is achieved with visibility flags, where each user manages what other users can see their DID.

  - Store minimal data on an external server.

    This is achieved by storing only user-managed IDs in the credentials; there are also explicit permissions that allow the user to only reveal them to users with selected IDs (ie. holders of the permissioned keys).

Credentials and claims are good primitives for a wide range of functions such as: voting, workflows, membership, and even transactions.

  - :doc:`Advertise & discover skills & services. <discovery>`

  - :doc:`Record time commitments (or any transactions). <transactions>`

  - :doc:`Record pledges & membership. <pledge>`

  - :doc:`Show appreciation semi-privately. <witness>`

Here are some other details about the current system, for the technically-minded:

* These tools aim for a system that will support close-knit communities; they are not meant for worldwide traffic.

* The mobile app is very general-purpose so it is flexible, but not yet entirely user-friendly. It demonstrates the capabilities, and now we can start creating domain-specific apps that are powerful but also easy to use.

* The next primary enhancement is to store & share claims & IDs directly from personal devices. (The only current option is to share your IDs with a shared server -- which is useful but which is not the end goal.) New encryption and selective disclosure approaches will allow you to share only what you want other people to discover, and provide various levels of access for them to contact you... all controlled by your devices, provably. We intend to migrate to that technology when it is more readily available; for now we offer this service and require the minimal amount of knowledge while still providing value. See :doc:`future` for more details.

Other Content
-------------

  - `These demos <https://endorser.ch/doc-tutorial>`_ show the user experience quickly.

  - Source Code

    - the `server that stores and reports on claims <https://github.com/trentlarson/endorser-ch>`_

    - the `mobile app to create verifiable credentials <https://github.com/trentlarson/endorser-mobile>`_

    - this `website <https://github.com/trentlarson/uport-demo>`_

  - Mobile app is in the `Apple Store <https://apps.apple.com/us/app/endorser-mobile/id1556368693>`_ and the `Play Store <https://play.google.com/store/apps/details?id=ch.endorser.mobile>`_

  - The `Endorser.ch Privacy Policy <https://endorser.ch/privacy-policy>`_ emphasizes these concepts.

  - There is `a diagram for a simple workflow <https://whimsical.com/liberty-certification-KS6ocCfbFWSPhY4uKFWsTx>`_.

  - There are `sample claims <https://endorser.ch/doc-sample-claims>`_ to scan into the mobile app.


Finally, see :doc:`Future, Past, and Related work <future>`.

