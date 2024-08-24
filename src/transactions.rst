
Gifts & Projects
================

How do we represent donations, or resource commitments and subsequently their delivery?

Here are a few scenarios:

  #. I donate time (or money or other resources) to someone.

  #. Someone makes a request, possibly in trade.

  #. I offer to give resources at some future date, possibly after conditions are met.

  #. I delivered those resources.

  #. Someone confirms that I delivered. In other words, they agree that I followed through on my commitment.

Here are the verbs used for assertions -- many recorded in the mobile app by default.

A diagram showing successive relationships between these objects is `here <./_static/entity-relationships.pdf>`_.

- "Join" shows attendance or membership in a group. Technically: `schema.org "JoinAction" <https://schema.org/JoinAction>`_

- "Give" shows transfer of ownership. Items like money and time would be included as the 'object'. Note that a Give can be part of a Trade, but if there is no link to a Trade or a reciprocal action then it is assumed to be one-sided (at least, in our system). Technically: `schema.org "GiveAction" <https://schema.org/GiveAction>`_

.. table:: Properties of a Give at Endorser.ch

  ==================== ====

  Name                 Description

  ==================== ====
  @context             always the schema: "https://schema.org"
  @type                always the type: "GiveAction"
  object               optional item or service or array of them; see Give "object" table below
  description          optional free-form description of what is given
  agent                optional `{ identifier: "DID" }` for the Person who gave (as opposed to a non-Person provider) (For multiple individual agents, a separate claim for each is recommended, or aggregate into a PlanAction or Project or Organization 'provider'.) A missing value means the giver is unnamed.
  provider             optional `[{ "@type": "...", identifier: "..." }]` array of PlanAction or Project or Organization records who helped make this possible (since non-Person entities are worth separating), like the "agent" but for a non-Person
  recipient            optional `{ identifier: "DID" }` for receiving Person if this is directly to an entity (as opposed to being part of a non-Person, which belong in things linked by "fulfills") (For multiple individual recipients, a separate claim for each is recommended, or declare it "fulfills" an aggregate PlanAction or Project or Organization.) A missing value means the recipient is unnamed, which may be the case if the benficiary is a non-person (listed in "fulfills").
  fulfills             optional `[{ "@type": "...", identifier: "..." }]` Offer or DonateAction or GiveAction or TradeAction or PlanAction which is the target, like the "recipient" but for a non-Person, and may be an array (eg. when tagged as a DonateAction as well as a contributor to a PlanAction); see "fulfills" table below (This is not currently part of schema.org specs.) Note that the type can be helpful even if no identifier is provided, eg. a "TradeAction" or "DonateAction" to mark things given with or without reciprocation; put this last if this is in an array, eg. with a fulfilled plan. A single fulfills relationship is preferred (and multiple may not be fully tracked), though this may also involve an individual recipient.
  identifier           optional identifier for this action, which should be a full URI (If `lastClaimId` is provided then this is unnecessary because this shares the same ID.)
  lastClaimId          optional reference to the previous plan which is being edited by this one (This is typically assigned by the system but may be a hash or SAID. It is a pointer to the most recent edit, not the first record.)
  ==================== ====




.. table:: Properties of a Give "object" or Offer "includesObject" at Endorser.ch

  ==================== ====

  Name                 Description

  ==================== ====
  @context             the schema "https://schema.org" (which is optional if the enclosing object already has it)
  @type                the type of this item, eg "TypeAndQuantityNode"
  amountOfThisGood     required numeric amount
  unitCode             required unit of amount, eg "HUR" for hour, "USD" for US Dollar, "BTC" for Bitcoin. `As specified <https://schema.org/unitCode>`_, this follows `UN/CEFACT codes <https://unece.org/trade/uncefact>`_, particularly `for time (Recommendation No. 20 - Revision 17 (Annexes I to III)) <https://unece.org/sites/default/files/2021-06/rec20_Rev17e-2021.xlsx>`_ and `for currency (ISO-4217) <https://www.six-group.com/dam/download/financial-information/data-center/iso-currrency/lists/list-one.xls>`_.
  ==================== ====



Example:

.. code:: json

  {
    "@context": "https://schema.org",
    "@type": "GiveAction",
    "description": "Made desserts for talent show -- thanks!",
    "object": {
      "@type": "TypeAndQuantityNode",
      "amountOfThisGood": 1,
      "unitCode": "HUR"
    },
    "fulfills": [
      {
        "@type": "Offer",
        "identifier": "https://endorser.ch/entity/ABCDEFGHIJKLMNOPQRSTUVWXYZ"
      },
      {
        "@type": "DonateAction"
      }
    ]
  }

..

There are some similar concepts at schema.org:

  - "Donate" is an act of giving a gift, typically toward an entity rather than a project (as opposed to a "Grant" for a goal). It is similar to "Give" but used to explicitly record that these is no reciprocation; the Endorser service recognizes that a GiveAction is a donation if a DonateAction is sent in the "fulfills" field (and if there is not TradeAction). Technically: `schema.org "DonateAction" <https://schema.org/DonateAction>`_

  - "Grant" represents donations toward a goal or project (as opposed to "Donate" to an entity for whatever purpose they choose). This is not used by the Endorser service, preferring to keep a simple "Donate" for all this kind of activity with a "fulfills" link if attached to a wider Plan or Project. (Note that this isn't yet fully accepted at schema.org.) Technically: `schema.org "Grant" <https://schema.org/Grant>`_

- "Loan Or Credit" represents temporary transfer of money. Technically: `schema.org "LoanOrCredit" <https://schema.org/LoanOrCredit>`_

- "Plan" proposes some activity to be executed; it typically aims at a particular time frame. "Offer" is different because the object in question is specific amounts of money or time; this is useful for advertising and proposing an initiative for others to join. "Project" is different because it targets an outcome; this focuses on a particular activity rather than a goal. Technically: `schema.org "PlanAction" <https://schema.org/PlanAction>`_




.. table:: Properties of a Plan at Endorser.ch

  ============ ====

  Name         Description

  ============ ====
  @context     always the schema: "https://schema.org"
  @type        always the type: "PlanAction"
  agent        optional `{ identifier: "DID" }` for the proposing Person or Organization
  description  optional free-form explanation
  endTime      optional date when the planned activity will end
  identifier   optional identifier for this plan, which should be a full URI  (If `lastClaimId` is provided then this is unnecessary because this shares the same ID.)
  image        optional image URL
  lastClaimId  optional reference to the previous plan which is being edited by this one (This is typically assigned by the system but may be a hash or SAID. It is a pointer to the most recent edit, not the first record.)
  name         optional short name
  startTime    optional date when the planned activity will start
  url          optional external URL for the project
  ============ ====

Example:

.. code:: json

  {
    "@context": "https://schema.org",
    "@type": "PlanAction",
    "agent": { "identifier": "did:..." },
    "identifier": "...",
    "name": "KickStarter for Time",
    "description": "Deliver an app that...",
    "image": "https://live.staticflickr.com/2853/9194403742_c8297b965b_b.jpg",
    "startTime": "2022-07",
    "endTime": "2023-03"
  }
..


- "Project" is for a large-scale initiative, typically associated with an organization for some long-term benefit. "Plan" is different because it aims at a more specific action at a point in time. Technically: `schema.org "Project" proposal <https://schema.org/Project>`_

  - The Endorser service currently uses PlanAction because Project is a new addition to schema.org and still getting feedback. It is actually a subtype of Organization; it may make for more mature projects, and there is probably space for both, with a distinction between a long-lived project with stable members vs a shorter-lived event or activity plan. (Maybe there will be a path where PlanActions will contribute to Projects.)

- "Offer" proposes a transfer or service, often with conditions or a price. When the proposal is fulfilled, there is a resulting "Give" or "Donate" or more complicated transfer such as "Trade". Technically: `schema.org "Offer" <https://schema.org/Offer>`_ (The opposite is a `"Demand" <https://schema.org/Demand>`_.)

.. table:: Properties of an Offer at Endorser.ch

  ============================== ====

  Name                           Description

  ============================== ====
  @context                       always the schema: "https://schema.org"
  @type                          always the type: "Offer"
  actionAccessibilityRequirement optional declaration of conditions for this offer; see "ActionAccessSpecification" table below (This is not currently part of schema.org specs on Offer.)
  description                    optional free-form explanation of conditions
  identifier                     optional identifier for this offer, which should be a full URI (If `lastClaimId` is provided then this is unnecessary because this shares the same ID.)
  includesObject                 optional specific "TypeAndQuantityNode"; see "includesObject" table above
  itemOffered                    optional description of the item or service; see "itemOffered" table below
  lastClaimId                    optional reference to the previous plan which is being edited by this one (This is typically assigned by the system but may be a hash or SAID. It is a pointer to the most recent edit, not the first record.)
  offeredBy                      optional (but recommended for clarity) `{ identifier: "..." }` individual or org doing the offer, which is assumed to be the issuer if not supplied (and which the Endorser service will reject if a DID different from the issuer)
  recipient                      optional `{ identifier: "..." }` individual or organization if this is directly to an entity (as opposed to being part of an activity or project)
  validThrough                   optional time after which this offer is no longer available
  ============================== ====


.. table:: Properties of an Offer "itemOffered" at Endorser.ch

  ==================== ====

  Name                 Description

  ==================== ====
  @context             optional schema "https://schema.org" (which is assumed if the enclosing object already has it)
  @type                optional type of this item, eg "CreativeWork" or "Service" (but recommended to plan future expansion)
  description          optional free-form explanation of deliverable or work contribution
  isPartOf             optional reference to a bigger activity (AKA "`PlanAction <https://schema.org/PlanAction>`_") or "`Project <https://schema.org/Project>`_" (This is not currently part of schema.org specs on all "itemOffered" objects. It is similar to the "fulfills" in a GiveAction.)
  ==================== ====


.. table:: Properties of an Offer "actionAccessibilityRequirement" property at Endorser.ch

  ==================== ====

  Name                 Description

  ==================== ====
  @context             optional schema "https://schema.org" (which is assumed if the enclosing object already has it)
  @type                optional type of this item (which is assumed to be "ActionAccessSpecification")
  requiresOffers       optional number telling how many other offers should be committed before this offer is valid (This is not currently part of schema.org specs.)
  requiresOffersTotal  optional total "TypeAndQuantityNode" in other offers that should be committed before this offer is valid (This is not currently part of schema.org specs.)
  ==================== ====




Example:

.. code:: json

  {
    "@context": "https://schema.org",
    "@type": "Offer",
    "offeredBy": "did:ethr:0x111c4aCD2B13e26137221AC86c2c23730c9A315A",
    "includesObject": { "amountOfThisGood": 2, "unitCode": "HUR" },
    "itemOffered": {
      "@type": "CreativeWork",
      "description": "Time for coding on...",
      "isPartOf": { "@type": "PlanAction", "identifier": "..." }
    },
    "actionAccessibilityRequirement": {
      "requiresOffers": 3,
      "requiresOffersTotal": { "amountOfThisGood": 5, "unitCode": "HUR" }
    },
    "validThrough": "2023-03"
  }


Note that the "includesObject" and "requiresOffersTotal" don't include an "@type" of "TypeAndQuantityNode" because that is what our software will consider the default.


- "Accept" signals that someone accepts some contract or pledge. (This could be used to state alignment to terms for a later transfer. This is different from "Agree" because it signals a commitment, eg. to a policy or proposal.) Technically: `schema.org "AcceptAction" <https://schema.org/AcceptAction>`_

  - There is also a "Take" to show that something has been received or redeemed, which is the opposite of "Give"; however, in these applications, a recipient shows fulfilment of a previous "Give" action with an "AgreeAction" where the 'object' has the originating "Give" action (or 'identifier'). Technically: `schema.org "TakeAction" <https://schema.org/TakeAction>`_.

  - There is also `"Send" <https://schema.org/SendAction>`_ and `"Receive" <https://schema.org/ReceiveAction>`_ to signify that an 'object' has been transported, but they don't indicate any transfer of ownership (and are not used in these applications).

- "Trade" is an exchange action. Technically: `schema.org "TradeAction" <https://schema.org/TradeAction>`_

- "Agree" shows that the user concurs with some other assertion. This is the preferred way for any counterparties to confirm that someone's claim is true. Technically: `schema.org "AgreeAction" <https://schema.org/AgreeAction>`_

Hopefully it's clear how to apply those assertions to the numbered scenarios above:

  #. `"Give" <https://schema.org/GiveAction>`_ an 'object' to a 'recipient'. For promises, `"Offer" <https://schema.org/Offer>`_ an 'itemOffered'... time or money or even a `"Service" <https://schema.org/Service>`_.

      - One could also `"Grant" <https://schema.org/Grant>`_, though that is new to the schema.

  #. `"Ask" <https://schema.org/AskAction>`_ for 'object', or `"Demand" <https://schema.org/Demand>`_ some help or resource 'itemOffered'.

  #. `"Offer" <https://schema.org/Offer>`_ some help or resource, eg. some 'eligibleQuantity' of 'itemOffered' at a 'price' until 'validThrough'.

      - One could also `"LoanOrCredit" <https://schema.org/LoanOrCredit>`_ some 'amount' of 'currency' for 'loanTerm'.

  #. `"Give" <https://schema.org/GiveAction>`_ to say that a transfer is done. Senders use this to claim that they transfer ownership to someone else.

  #. `"Agree" <https://schema.org/AgreeAction>`_ to confirm delivery of a "GiveAction" which is included as the 'object'. This is how recipients signal they've received whatever was given or donated.

In our Endorser app, you can try many of these such as Time or Money Donations.




**Other References**

- Besides `schema.org <https://schema.org>`_, there are other formal ontologies that are a close fit and may even be useful as shared projects evolve. (We may also find it useful to create our own.)

  - For Project schemas, there are some other choices beyond Schema.org's "PlanAction" (and the upcoming "Project") and we anticipate getting more specific over time and using one of these. For now, we're focused on getting the mechanics of Offer & Give correct, but there are these when we expand:

    - The `Valueflows ontology <https://www.valueflo.ws/specification/uml/>`_ has many of the same concepts and is written specifically for "next economy" value networks.

    - `The EP-PLAN ontology <https://trustlens.github.io/EP-PLAN/>`_ includes a "Plan" as well.

    - Ontology Design Patterns has concepts in their DUL section for `Plan <http://www.ontologydesignpatterns.org/ont/dul/DUL.owl#Plan>`_ and `Goal <http://www.ontologydesignpatterns.org/ont/dul/DUL.owl#Goal>`_, and in their CP section for `"basicplanexecution.owl" <http://www.ontologydesignpatterns.org/cp/owl/basicplanexecution.owl>`_ among `other definitions <http://www.ontologydesignpatterns.org/cp/owl/>`_.

    - There's a `FOAF Project <http://xmlns.com/foaf/0.1/#term_Project>`_.

  - When it comes to conditions for an Offer, we chose to add `"actionAccessibilityRequirement" <https://schema.org/actionAccessibilityRequirement>`_ with new properties "requiresOffers" & "requiresOffersTotal". There were other options:

    - Schema.org has properties like `expectsAcceptanceOf <https://schema.org/expectsAcceptanceOf>`_ and `"freeShippingThreshold" <https://schema.org/freeShippingThreshold>`_ (but "requires" is more apropos than those), and `"eligibleQuantity" <https://schema.org/eligibleQuantity>`_ (though that is geared toward quantities of this offering and not quantities outside this offering).

    - Data Quality Constraint Library (with this `helpful graphic <http://semwebquality.org/dqm-vocabulary/v1/UML_DQM-Vocabulary.png>`_) has `hasCondition <http://semwebquality.org/dqm-vocabulary/v1/dqm#hasCondition>`_ that could be for Offer prerequisites.

    - Inria has `GoalCondition <http://ns.inria.fr/ludo/v1/docs/gamemodel.html#GoalCondition>`_.

    - Web Service Modeling Ontology has `a "lite" set <http://www.wsmo.org/ns/wsmo-lite/index.rdfxml>`_ with a "Condition" type.

    - Dublin Core has `type "Requires" <https://www.dublincore.org/resources/userguide/creating_metadata/#Requires>`_ and `property "requires" <https://www.dublincore.org/resources/userguide/publishing_metadata/#dcterms:requires>`_.

  - For delivery of an offer, besides Schema.org's "GiveAction", there are the following:

    - For reference to the object being given, Thing objects have a "potentialAction" property (but that wouldn't be used to reference the GiveAction because the Offer is not the object; rather, the time or money is the object).

    - For the reference back to the Offer, there are "referencesOrder" and "partOfInvoice" (but those are specific to a listing on an invoice to a customer).

  - `Linked Online Vocabularies <https://lov.linkeddata.es>`_ allow searching through many ontologies.

- Units for currencies are described in multiple places at schema.org:

  - https://schema.org/currency

  - https://schema.org/priceCurrency

  - https://schema.org/price

  We've chosen HUR from UN/CEFACT for the length of time.
  Time units can be a single string in ISO 8601 format for schema.org but we don't use that (yet).


- Some have tackled these problems with tokens; that's a valid approach as well, with upsides of broader markets but downsides of complicated issuance and less private data.

  - `Ying <https://yingme.co/>`_ is building an app with a currency built in.

  - `Let's B More <https://letsbmore.timebanks.org/>`_ has a search through their offerings.

- There are signing technologies for cash without a central blockchain: `"Untraceable Off-line Cash in Wallets with Observers" by Stefan Brands <https://courses.csail.mit.edu/6.857/2009/handouts/untraceable.pdf>`_ shows one way... this `"note on blind signature schemes" <https://blog.cryptographyengineering.com/a-note-on-blind-signature-schemes/>`_ has other links but most are broken. I believe there is more recent work as well but it's hard to find.
