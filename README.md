# Bürokratt onboarding

## In case you're just wondering

Bürokratt is an initiative by the [Ministry of Economics Affairs and Communications of Estonia](https://www.mkm.ee/) to, in the end, provide all of the Estonian government e-services (about 3,000 of them), plus potentially any of the private sector ones, via both text-based and voice input.

Technical implementation of Bürokratt is provided by the Department of Machine Learning and Language Technology of [Information System Authority of Estonia](https://www.ria.ee/).

Recording from last Bürokratt Information day (07.08.2024) can be seen [here](https://www.youtube.com/watch?v=u_HXF-Rnuac)



## How we develop Bürokratt

### Open development

Bürokratt is being developed on the basis of open development. You can [read more about it from here](https://medium.com/digiriik/why-b%C3%BCrokratt-chose-the-model-of-open-development-fd20d32a04b). In short - no private repos, no private planning, no private nothing. The code committed by developers ends up straight at public GitHub repos and the moment we see it, everyone else sees it as well.

Everything starts from https://github.com/buerokratt. All of our project can be found from https://github.com/orgs/buerokratt/projects and repos from https://github.com/orgs/buerokratt/repositories.

### Procurements and partners

We switched from relying on a small number of partners **to having a wide range of development partners.** Everyone who wanted to sign up for a procurement had a chance to do it regardless of their size, history, etc. As a result, we currently have 25 partners eligible to participate in our mini-tenders and ca 40+ waiting for the paperwork to be finished so they could join as well.

## If you want to participate as a developer

### Architecture

A high-level overview of Bürokratt architecture can be found at https://koodivaramu.eesti.ee/buerokratt/architecture/buerokratt-high-level.

A couple of flows to look at are [chat flow](https://koodivaramu.eesti.ee/buerokratt/architecture/buerokratt-high-level/-/blob/master/buerokratt_chat_flow.png) and [input processing](https://koodivaramu.eesti.ee/buerokratt/architecture/buerokratt-high-level/-/blob/master/buerokratt_input_processing.png).

### GitHub

#### References

All of Bürokratt's projects can be found from https://github.com/orgs/buerokratt/projects.

All projects have a corresponding repo. To see the full list of them, go to https://github.com/orgs/buerokratt/repositories.

#### Pull requests

All pull requests of Bürokratt can be found from https://github.com/pulls?user=buerokratt

#### Permissions

As a partner, first send us your GitHub account name so we could give you appropriate permissions.

**Project managers** do not have permissions to create, edit or delete project issues or their status. This is done by Bürokratt's core team to prevent unwanted results due to miscommunication, etc.

**Developers** (but also project managers) have a "Triage" permission level. You can [read more about it from here](https://docs.github.com/en/organizations/managing-user-access-to-your-organizations-repositories/repository-roles-for-an-organization) but in short, this means that you first need to first fork the repo you are / will be working on, and commit your code through pull requests.

#### Commits

We require daily commits. If you're not done yet, use _draft pull requests_ to keep everyone up-to-date with your work. Also, every commit has to be linked with its parent issue - pull requests covering different issues are not allowed.

### Mock-services

We encourage you to first set up the full flow of planned services as mocks by using [Ruuter mocks](https://github.com/buerokratt/Ruuter/blob/main/samples/steps/mock.md) for it.

### Warranty and responsibilities

In most cases, there is at least a 6-, often 12-months warranty period for the custom code provided by partners.

The exception goes for (most of the) services built based on Bükstack components. This means that if, for example, services are built as Ruuter DSLs (YAMLs) but Ruuter itself contains vulnerabilities, the partner only creating DSLs and not developing the core functionality of Ruuter itself is free of such liabilities.

Also, if Bükstack components lack of necessary functionality, both mock and to-be DSLs will be created. Missing core functionality will be provided within another parallel projects and will not be a blocker for the partner creating DSL-based services when handing over their work.

### DSL-based developments

The first thing to understand is that we strongly believe in DSL-based developments. This means that unless you are working with either front-end, language technology or developing our core components themselves, you almost never get to write code in Java or other so-called actual programming languages. Instead, you work with YAML, standard SQL queries as text files, [Handlebars DSL](https://handlebarsjs.com/), etc. To better understand the logic behind it, please [read this article](https://medium.com/digiriik/reasons-behind-b%C3%BCrokratt-giving-less-freedom-to-developers-fc04b0751).

### Key repos and third-party components to focus on when onboarding

#### Ruuter | Bükstack

https://github.com/buerokratt/Ruuter

All of our services are based on Ruuter. Whenever you want to make POST, GET or other requests, it's done via Ruuter. The same goes for if/else statements, creating and using templated services, etc. Ruuter also acts as a reverse proxy to mediate all traffic between any of the components. Go through the [guide](https://github.com/buerokratt/Ruuter/blob/main/samples/GUIDE.md) and definitely create your own [Ruuter-based mock services](https://github.com/buerokratt/Ruuter/blob/main/samples/steps/mock.md) to get the first grip of it.

#### Resql | Bükstack

https://github.com/buerokratt/Resql

Resql is used for all of our [Postgres](https://www.postgresql.org/) requests. Every single database query lies in a separate `.sql` file and is consumable as a REST endpoint. You can take a look at [some of our chatbot-related database queries from here](https://github.com/buerokratt/Buerokratt-Chatbot/tree/main/DSL.Resql).

> PS! Using `UPDATE` and `DELETE` in SQL queries is forbidden throughout all of our projects! Every action must leave a record in a database table.

#### DataMapper | Bükstack

https://github.com/buerokratt/DataMapper

DataMapper (you can also find it under the name of DMapper from here and there) is actually [https://handlebarsjs.com](https://handlebarsjs.com/) wrapped in Java. We will replace it with pure Handlebars on [Node.js](https://nodejs.org/en) soon. We use DataMapper to re-structure JSON outputs according to our needs. See some of our [currently in use DataMapper / Handlebars DSLs from here](https://github.com/buerokratt/Buerokratt-Chatbot/tree/main/DSL.DMapper).

#### TIM | Bükstack

https://github.com/buerokratt/TIM

TIM is an acronym for "[TARA](https://www.ria.ee/en/state-information-system/electronic-identity-eid-and-trust-services/central-authentication-services) Integration Module", making it possible to start using TARA-based authentication by just updating your configuration file. TIM also provides functionality to create and use N number of custom [JWTs](https://en.wikipedia.org/wiki/JSON_Web_Token).

#### CVI

https://github.com/buerokratt/cvi

CVI is new to us but will be used a lot from now on. It's a fork of https://github.com/e-gov/cvi - also a very new initiative. Long story short - all of our GUI/front-end re-usable React componentes will end up there and will get committed back to the original project.

#### PostgreSQL

We use PostgreSQL as a relational database. [See here](https://github.com/buerokratt/Third-party-components/tree/main/Postgres) for a quick setup.

#### Liquibase

We use https://www.liquibase.org to manage our database schema changes. Sample on setting up initial databases and running Liquibase can be found from https://github.com/buerokratt/Installation-Guides/blob/main/DB_installation.md, some of the sample Liquibase DSLs from https://github.com/buerokratt/Buerokratt-Chatbot/tree/main/DSL.Liquibase.

#### OpenSearch

[OpenSearch](https://opensearch.org/) will become more and more important part of our technical stack. Definitely get to know with their [Query DSL](https://opensearch.org/docs/latest/opensearch/query-dsl/index/) to onboard faster.

#### NB!
For development purposes, it is often useful to run both the Bükstack and individual modules locally. This can be done using Docker Compose. Refer to the README in each module's repository for instructions.

### Contact 

If you want to contact regarding to Bürokratt's **technical solutions,** contact varmo.helemae at ria.ee.

## If you want to participate as a language technologist

> We are still making our first steps regarding to language technology, so give us some time to update this section here.

### Technical stack

#### Rasa

We currently rely heavily on Rasa for building conversational rules, stories, and intent-based actions. However, starting from Q4 2025, we plan to make some changes:

- We will likely replace Rasa's intent recognition with a more flexible approach, especially to support multi-intent recognition.

- Rasa remains available for rules, stories, and custom actions on client request, but without official support.

#### LLM-based approach and Common Knowledge Base

Recently, we have started experimenting with a large language model (LLM) approach. As part of this, we have developed a Common Knowledge Base (CKB) project:

- Users can provide a webpage via a simple UI, which is then scraped and cleaned.

#### Global Classifier

- The Global Classifier (GC) ingests this data and, with the help of an LLM, generates synthetic training data (questions related to the domain).

- This synthetic data is then used to train domain-specific models, enabling more flexible and knowledge-driven intent recognition and question answering.

#### BYK-RAG (Retrieval-Augmented Generation Module)

The **BYK-RAG Module** is part of the Burokratt ecosystem and provides **retrieval-augmented generation (RAG)** capabilities:

- It uses data scraped and cleaned via the Common Knowledge Base (CKB).

- It integrates with multiple LLM providers to generate AI-powered responses that are reliable, multilingual, and compliant.

- The module includes flexible configuration and monitoring features for administrators.

**NB!**
By the end of this year, we expect to offer a choice between continuing with Rasa but without support or moving to an LLM/RAG-based approach, depending on the requirements of each task.

### Contact

If you want to contact regarding to Bürokratt's language technology, contact merlepaula.videvik at ria.ee

## Bürokratt as network

#### DMR

The DMR project acts as a mediator for conversations between multiple clients. It ensures secure, reliable, and efficient message exchange across the network, allowing different client instances to interact seamlessly.

#### CentOps

CentOps is a central hub and orchestration tool for managing deployments across multiple Kubernetes clusters. While it is part of the Bürokratt ecosystem, it is designed as a standalone platform that can be used independently for managing any delivery pipeline. Depending on the architecture, additional clusters can be added — for example, development, testing, staging, and production — giving operations engineers full control over the deployment lifecycle and environment management.

## If you want to start using Bürokratt as an institution

### Bürokratt on Estonian Government Cloud

We are well-prepared to deploy Bürokratt on [Estonian Government Cloud](https://riigipilv.ee/en). After all the (legal) preparations, technical deployment usually takes just couple of hours.

### Bürokratt as SaaS

We are actively working on making Bürokratt available as SaaS on [Estonian Government Cloud](https://riigipilv.ee/en). Any of Estonian public sector institutions should be able to start and stop using Bürokratt as a pre-configured SaaS Q1 2024.

### Bürokratt on-site

Bürokratt can also be deployed on-site. Please note that on-site deployment requires a Kubernetes platform. Detailed deployment instructions are currently under preparation.

### Contact

If you want to contact regarding to start using Bürokratt as an institution, contact rasmus.eimla at ria.ee

## If you're asked to deploy Bürokratt for your client

### Kubernetes

Bürokratt is fully deployable on Kubernetes, supporting all core functionalities.

### Contact

If you want to contact regarding to start using Bürokratt as an institution, contact varmo.helemae at ria.ee
