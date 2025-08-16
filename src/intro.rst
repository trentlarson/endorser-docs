
Intro to Community Credentials
==============================

Quick Start
-----------

  - See `Time Safari <https://timesafari.org>`_ for many of the claims on our server -- 'give' claims in the feed, plus 'project' claims, and 'offer' claims on those projects.

Overview
--------

We support the growth of community networks at whatever level of privacy you prefer.

  Meta (AKA Facebook) has created an engaging user interface around networks but they control it all; Google allows more control but still has access to your data and shares it; NextDoor is another service that holds the data you submit. Let's build networks where individuals have as much control as possible while still allowing discovery.

This is a set of projects to do just that, with the following features:

- Store & share standard data schemas, so that other tools can interoperate easily.

- Allow for local storage with optional sharing, all depending on your choices for openness and discovery.

Said more technically:

- Issue credentials about yourself and your community, easily & verifiably. This is done based on standards for Verifiable Credentials that use personal public & private keys, with apps to make the process as simple as possible.  Most other approaches assume mature, centralized credential authorities; there is a place for those, but there are even more uses for an evolving credential system based on existing networks.

- Share them, then search to network with people you know -- with the right permissions. When credentials are saved to our server, people may then see claims about others, if allowed by the originator. There's one further possibility: if someone is two friends away, then your common friend can introduce you. This allows for discovery: although you may not have access to other people's claims, if you are linked by a contact then you can use other means to find that information; you must communicate with your shared contact some other way to get an introduction. This is all done `local-first <https://www.inkandswitch.com/local-first.html>`_.


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

* These tools aim for a system that will support close-knit communities; no services currently would support worldwide traffic, and we expect no single service ever will.

* The mobile app is very general-purpose so it is flexible, but not yet entirely user-friendly. It demonstrates the capabilities, and now we can start creating domain-specific apps that are powerful but also easy to use.

* The data people share are captured in semantic data formats, eg. `Schema.org <https://schema.org>`_, `Dublin Core <https://www.dublincore.org/schemas/>`_, etc. We try to find the best match for this project's concepts, including searches through the `Linked Open Vocabularies <https://lov.linkeddata.es/dataset/lov/>`_; however, these standards are still evolving and we are open to alternative or even custom schemas (fully realizing we may have to map between old and new terms in the future).

* The next primary enhancement is to store & share claims & IDs directly from personal devices. (The only current option is to share your IDs with a shared server -- which is useful but which is not the end goal.) New encryption and selective disclosure approaches will allow you to share only what you want other people to discover, and provide various levels of access for them to contact you... all controlled by your devices, provably. We intend to migrate to that technology when it is more readily available; for now we offer this service and require the minimal amount of knowledge while still providing value. See :doc:`future` for more details.

Finally, see :doc:`Future, Past, and Related work <future>`.


Other Content
-------------

  - Source Code

    - for the `server that stores and reports on claims <https://github.com/trentlarson/endorser-ch>`_

    - for the `Time Safari app based on those claims <https://gitea.anomalistdesign.com/trent_larson/crowd-funder-for-time-pwa>`_.

    - for this `website <https://github.com/trentlarson/uport-demo>`_ and `documentation <https://github.com/trentlarson/endorser-docs>`_.

  - The `Endorser.ch Privacy Policy <https://endorser.ch/privacy-policy>`_ emphasizes these concepts.

  - There is `a diagram for the workflow for making decisions about people with whom to work or play <https://whimsical.com/liberty-certification-KS6ocCfbFWSPhY4uKFWsTx>`_.
