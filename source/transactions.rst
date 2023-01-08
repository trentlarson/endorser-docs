
Transactions & Projects
=========================

How do we represent resource commitments, and then check delivery on those promises?

Here are a few scenarios:

  #. I donate time (or money or other resources) to someone.

  #. Someone makes a request, possibly in trade.

  #. I offer to give resources at some future date, possibly after conditions are met.

  #. I delivered those resources.

  #. Someone confirms that I delivered. In other words, they agree that I followed through on my commitment.

Here are the verbs used for assertions -- many recorded in the mobile app by default.

  - "Join" shows attendance or membership in a group. Technically: `schema.org "JoinAction" <https://schema.org/JoinAction>`_

  - "Give" shows transfer of ownership. Fungible items like money and time would be included as the 'object'. Technically: `schema.org "GiveAction" <https://schema.org/GiveAction>`_

    - "Donate" is an act of giving a gift, typically toward an entity rather than a project (as opposed to a "Grant" for a goal). It is similar to "Give" but used to explicitly record that these is no reciprocation. Technically: `schema.org "DonateAction" <https://schema.org/DonateAction>`_

    - "Grant" represents donations toward a goal or project (as opposed to "Donate" to an entity for whatever purpose they choose). (Note that this isn't yet fully accepted at schema.org.) Technically: `schema.org "Grant" <https://schema.org/Grant>`_

  - "Loan Or Credit" represents temporary transfer of money. Technically: `schema.org "LoanOrCredit" <https://schema.org/LoanOrCredit>`_

  - "Plan" proposes some activity to be executed; it typically aims at a particular time frame. "Offer" is different because the object in question is specific amounts of money or time; this is useful for advertising and proposing an initiative for others to join. "Project" is different because it targets an outcome; this focuses on a particular activity rather than a goal. Technically: `schema.org "PlanAction" <https://schema.org/PlanAction>`_




.. table:: Properties of a Plan at Endorser.ch

  ============ ====

  Name         Description

  ============ ====
  @context     always the schema: "https://schema.org"
  @type        always the type: "PlanAction"
  agent        optional DID of the proposing person or organization
  description  optional free-form explanation
  endTime      optional date when the planned activity will end
  identifier   optional identifier for this plan
  image        optional image URL
  name         optional short name
  startTime    optional date when the planned activity will start
  ============ ====

Example:

.. code:: json

  {
    "@context": "https://schema.org",
    "@type": "PlanAction",
    "agent": "did:ethr:0x000Ee5654b9742f6Fe18ea970e32b97ee2247B51",
    "identifier": "...",
    "name": "KickStarter for Time",
    "description": "Deliver an app that helps people propose plans, and engages others to bring them to life.",
    "image": "https://live.staticflickr.com/2853/9194403742_c8297b965b_b.jpg",
    "startTime": "2022-07",
    "endTime": "2023-03"
  }

..


    - "Project" is for a large-scale initiative, typically associated with an organization for some long-term benefit. "Plan is different because it aims at a more specific action at a point in time. Technically: `schema.org "Project" proposal <https://schema.org/Project>`_

    - "Offer" proposes a transfer or service, often with conditions or a price. When the proposal is fulfilled, there is a resulting "Give" or "Donate" or more complicated transfer such as "Trade". Technically: `schema.org "Offer" <https://schema.org/Offer>`_ (The opposite is a `"Demand" <https://schema.org/Demand>`_.)

.. table:: Properties of an Offer at Endorser.ch

  ==================== ====

  Name                 Description

  ==================== ====
  @context             always the schema: "https://schema.org"
  @type                always the type: "Offer"
  availabilityEnds     optional time when this offer stops being available
  availabilityStarts   optional time when this offer becomes available
  description          optional free-form explanation; to offer specific units of time or money, use "itemOffered"
  identifier           optional identifier for this offer
  minOtherOffers       optional number telling how many other offers should be received before this offer is valid
  minOtherOfferAmounts optional total amount of other offers that should be received before this offer is valid
  recipient            optional individual or organization if this is directly to an entity (as opposed to "result")
  isPartOf             optional reference to a PlanAction if this contributes to some other plan or goal (as opposed to "recipient")
  includesObject       optional specific TypeAndQuantityNode; to make a free-form explanation of the offer, use "description"
  ==================== ====


Example:

.. code:: json

  {
    "@context": "https://schema.org",
    "@type": "Offer",
    "offeredBy": "did:ethr:0x111c4aCD2B13e26137221AC86c2c23730c9A315A",
    "description": "Regular progress, including time for coding and networking",
    "availabilityStarts": "2022-07",
    "availabilityEnds": "2023-03",
    "isPartOf": { "@type": "PlanAction", "identifier": "..." }
    "includesObject": { "@type": "TypeAndQuantityNode", "amountOfThisGood": 2, "unitCode": "HUR" },
  }

Note that "isPartOf" is not an official property of the Offer spec; it's typically a property of CreativeWork. Other similar properties are "result" and "serviceOutput" and "seeks" and "potentialAction"




  - "Watch" says that something was seen. Technically: `schema.org "WatchAction" <https://schema.org/WatchAction>`_

  - "Agree" says that the user concurs with some other assertion. Technically: `schema.org "AgreeAction" <https://schema.org/AgreeAction>`_

  - "Accept" signals that someone accepts some contract or pledge. (This could be used to state alignment to terms for a later transfer. This is different from "Agree" because it signals a commitment, eg. to a policy or proposal. See `schema.org <https://schema.org/>`_ for concrete definitions.) Technically: `schema.org "AcceptAction" <https://schema.org/AcceptAction>`_

    - There is also a "Take" to show that something has been received or redeemed, which is the opposite of "Give"; however, in these applications, a recipient shows fulfilment of a previous "Give" action with an "AgreeAction" where the 'object' has the originating "Give" action (or 'identifier'). Technically: `schema.org "TakeAction" <https://schema.org/TakeAction>`_.

    - There is also `"Send" <https://schema.org/SendAction>`_ and `"Receive" <https://schema.org/ReceiveAction>`_ to signify that an 'object' has been transported, but they don't indicate any transfer of ownership (and are not used in these applications).

Hopefully it's clear how to apply those assertions to the scenarios above:

  #. `"Give" <https://schema.org/GiveAction>`_ an 'object' to a 'recipient', or `"Offer" <https://schema.org/Offer>`_ an 'itemOffered'... time or money or even a `"Service" <https://schema.org/Service>`_.

      - One could also `"Grant" <https://schema.org/Grant>`_, though that is new to the schema.

  #. `"Ask" <https://schema.org/AskAction>`_ for 'object', or `"Demand" <https://schema.org/Demand>`_ some help or resource 'itemOffered'.

  #. `"Offer" <https://schema.org/Offer>`_ some help or resource, eg. some 'eligibleQuantity' of 'itemOffered' at a 'price' when 'availabilityStarts'.

      - One could also `"LoanOrCredit" <https://schema.org/LoanOrCredit>`_ some 'amount' of 'currency' for 'loanTerm'.

  #. `"Give" <https://schema.org/GiveAction>`_ to say that a transfer is done. Senders use this to claim that they transfer ownership to someone else.

  #. `"Agree" <https://schema.org/AgreeAction>`_ to confirm delivery of a "GiveAction" which is included as the 'object'. This is how recipients signal they've received whatever was given or donated.

In our Endorser app, you can try many of these such as Time or Money Donations, or Credit.




**Other References**

- Besides `schema.org <https://schema.org>`_, there are other formal ontologies that are a close fit and may even be useful as shared projects evolve. (We may also find it useful to create our own.)

  - Ontology Design Patterns has `Plan <http://www.ontologydesignpatterns.org/ont/dul/DUL.owl#Plan>`_. It also has `Goal <http://www.ontologydesignpatterns.org/ont/dul/DUL.owl#Goal>`_ if we start refining definitions of results.

  - When it comes to conditions for an offer:

    - Data Quality Constraint Library (with this `helpful graphic <http://semwebquality.org/dqm-vocabulary/v1/UML_DQM-Vocabulary.png>`_) has `hasCondition <http://semwebquality.org/dqm-vocabulary/v1/dqm#hasCondition>`_ that could be for Offer prerequisites.

    - Inria has `GoalCondition <http://ns.inria.fr/ludo/v1/docs/gamemodel.html#GoalCondition>`_.

    - Web Service Modeling Ontology has `a "lite" set <http://www.wsmo.org/ns/wsmo-lite/index.rdfxml>`_ with a "Condition" type.

    - Dublin Core has `type "Requires" <https://www.dublincore.org/resources/userguide/creating_metadata/#Requires>`_ and `property "requires" <https://www.dublincore.org/resources/userguide/publishing_metadata/#dcterms:requires>`_.

  - FOAF has a `Project <http://xmlns.com/foaf/0.1/#term_Project>`_.

  - `Linked Online Vocabularies <https://lov.linkeddata.es>`_ allow searching through many ontologies.

- Some have tackled these problems with tokens; that's a valid approach as well, with upsides of broader markets but downsides of complicated issuance and less private data.

  - `Ying <https://yingme.co/>`_ is building an app with a currency built in.

  - `Let's B More <https://letsbmore.timebanks.org/>`_ has a search through their offerings.

- There are signing technologies for cash without a central blockchain: `"Untraceable Off-line Cash in Wallets with Observers" by Stefan Brands <https://courses.csail.mit.edu/6.857/2009/handouts/untraceable.pdf>`_ shows one way... this `"note on blind signature schemes" <https://blog.cryptographyengineering.com/a-note-on-blind-signature-schemes/>`_ has other links but most are broken. I believe there is more recent work as well but it's hard to find.
