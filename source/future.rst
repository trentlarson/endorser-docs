
Future
======

- For self ownership of credentials
  - Current: IDs are not revealed outside server, are custodied on server (trusting admins of server)

  - Future Option: move data to personal devices
    - searches can be sent as hashes (to avoid revealing claim to whole network)
    - searches can be allowed selectively & transmitted
    - downsides: intermittent availability

  - Future Option: move to BBS+ signatures (simple encryption checks)
    - previous claims & confirmations could be signed again
    - able to keep proof of time for hash
    - downsides: many previous confirmations would not be signed, migrated claim timestamps wouldn't have global proof of time

  - Future Option: move to homomorphic encryption (richer predicates than BBS+ signatures)
    - to migrate, previous claims & confirmations could be signed again
    - able to keep proof of time for hash
    - downsides: many previous confirmations would not be signed, migrated claim timestamps wouldn't have global proof of time

- For proof of time:
  - Current: merkle tree backed by other claims

  - Future Option: merkle tree is anchored in a blockchain
    - downsides: items previous to start don't have exact global proof of time

- For private searches
  - Current: trusting admins of server
  - Future Option: homomorphic encryption
  - Future Option: DID Comm

- For translation into cryptocurrency wallet
  - able to sign transactions with same key




- `BBS+ signature schemes <https://mattrglobal.github.io/bbs-signatures-spec/>`_ and `zero-knowledge proofs <https://en.wikipedia.org/wiki/Zero-knowledge_proof>`_ enable you to send hidden data and later reveal parts of it or even just prove that it fits your purpose without revealing the data. (An example is proving that you're over 21 without revealing your exact age. Magic, right?) We can use these to iterate our way to better server-side privacy. This may be what Evernym calls "safe signatures", but we've got to understand this more.

- Build on another platform for transport:

  - `Element <https://element.io>`_

  - `Keybase <https://keybase.io>`_

  - `Signal <https://signal.org>`_. It's amazing. For example, they store `minimal information about your contacts on their servers <https://signal.org/blog/private-contact-discovery/>`_, such that they cannot even tell who are your contacts while still letting you find ones that are in your address book. Add to that their work with `anonymous credentials <https://eprint.iacr.org/2019/1416.pdf>`_, groups, and payments (the latter is still in progress) and that seems the best platform on which to build these features. We'll go there as soon as we can figure out how.

  - `Holochain <https://www.holochain.org/>`_

  - `Backchannel <https://www.inkandswitch.com/backchannel/>`_

- Let's move more functionality to our own devices. An always-connected service makes things convenient, but we should all have the option of owning our data and managing it on our own phones and computers. We could connect through bluetooth or a local network when in close proximity. A search request might be sent out and results could trickle back in as devices respond. It would be fun!

- Create or leverage a browser extension. A friend told how easy it is to use MetaMask for various platforms, and how inconvenient it is to have to pull out a phone to do work.

- Although this is a labor of love and (we hope) a good foundation to support community work, we'd like to get resources to support this development effort. Great user-interfaces take time and effort to create, so that's worth something. We can also build more infrastructure that cater to organizations who could pay.


Outside Work
------------

- `Self-Sovereign Identity <https://en.wikipedia.org/wiki/Self-sovereign_identity>`_ is a set of emerging standards based on cryptography and specifications like `Decentralized IDs <https://w3c.github.io/did-core/>`_ (DIDs) and `Verifiable Credentials <https://www.w3.org/TR/vc-data-model/>`_ (VCs). `There are many SSI wallets <https://github.com/Gimly-Blockchain/ssi-wallets>`_. (Our mobile app creates both DIDs and VCs.)

- https://mobilecoin.com/cryptorenaissance - slide at 4:45, 2-minute description starting at 3:00. See also https://patternsinthevoid.net/hyphae/hyphae.pdf


- Besides `schema.org <https://schema.org/>`_, there are many other vocabularies to use: `Linked Open Vocabularies (LOV) <https://lov.linkeddata.es/dataset/lov/>`_ is a great place to start looking (though some of the pointers no longer work).

- Other projects that are close but don't cover all our use-cases:

  - `Other wallets <https://github.com/Gimly-Blockchain/ssi-wallets>`_ allow creation of VCs but are typically for organizational use.

  - The paper `Bottom-up Trust Registry in Self Sovereign Identity <https://arxiv.org/pdf/2208.04624.pdf>`_ explains one way to create a registry for issuers, but we care more about managing your personal trust network.

  - Yingme.co has some time-banking, but it's still working on the onboarding and how to share the technology.

  - Keybase aims to be a general-purpose identity wallet. It doesn't have VCs built-in, but it could be a viable approach. Their sigchains could be useful.

  - MetaMask & Trezor also don't have VCs built in; while they could sign transactions, they're oriented toward cryptocurrencies so we don't envision their use for VCs.

  - We must give a shout-out to blockchains because they brought user-managed cryptography to the mainstream (and still pushing the boundaries for self-sovereign asset management). They're public, so they're not good candidates for any private data.

Selected History
----------------

- Always appreciate how far we've come. :-) For example, this used to be `based on uPort <https://github.com/trentlarson/uport-demo/blob/5c3d7fcb751ad34ed10ebb7adab650b2cfebb7d1/src/components/Welcome.js#L96>`_. The `first shared transaction was on Jan 2019 <https://endorser.ch/reportClaim?claimId=01D25AVGQG1N8E9JNGK7C7DZRD>`_ (before the Verified Credentials Working Draft was submitted).
