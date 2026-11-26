# Church relationship manager

A secretary can use this specification to admit a member, prepare a dated roll or issue a transfer letter. A ministry leader can plan a service, find an eligible substitute and arrange transport. A household can register for an event, correct a contact route or ask for a confidential visit. Each workflow identifies who may act, which records change, what other people may learn and how the church handles an exception.

The same model serves a congregation keeping its first electronic register, a church operating several campuses, and independent churches cooperating on a camp or a district return. The church sets its terminology, membership rules, governing authority and enabled services. A visitor, family member, donor, officeholder and sign-in account represent different relationships. One person can hold several at the same time.

## Scope and integrations

Start with the [capability and ownership map](docs/foundation/product-scope.md). It pairs church tasks with their records, operating rules, acceptance evidence and external dependencies. The church can operate the register, pastoral work, events and governance independently. It can connect an existing accounting package, an LMS, a website, a member app or another approved service as its needs grow.

The [API, MCP and church app requirements](docs/platform/church-apps-and-integrations.md) cover receiving information from other systems, extending the church's own app, and exchanging authorized updates in both directions. The [giving and accounting handoff](docs/finance/README.md) and [church classes and learning provider](docs/ministry/learning.md) specify which side owns each decision. API and MCP provision through Joomla Component Builder is a delivery requirement. The business specification applies before deciding how to divide the product into Joomla components.

## Find a church task

| I need to… | Start here |
| --- | --- |
| Set up congregations, campuses, roles, forms or local policy | [Organization and shared rules](docs/foundation/README.md) |
| Welcome a visitor, maintain households, admit or transfer a member, record a rite or coordinate confidential care | [People and care](docs/people/README.md) |
| Coordinate groups, class meetings, worship, volunteers, events, check-in, rooms, equipment or transport | [Ministry operations](docs/ministry/README.md) |
| Give formal notice, establish quorum, approve minutes or follow up a resolution | [Governance](docs/governance/README.md) |
| Find the safe recipient, prepare a bulletin or follow up an undelivered notice | [Communications](docs/communications/README.md) |
| Record an offering, track a pledge, acknowledge a gift or resolve an accounting handoff | [Giving and stewardship](docs/finance/README.md) |
| Handle an event fee, a church bookstall enquiry, or permission to publish a sermon | [Church desk and media](docs/commerce/README.md) |
| Arrange a wedding or burial, lend a resource, appoint a worker, deliver relief or prepare a church return | [Church administration](docs/administration/README.md) |
| Run an appeal, steward donor preferences or report a partnership's results | [Fundraising and partnerships](docs/development/README.md) |
| Report an incident, handle a complaint independently or account for people during a disruption | [Assurance and independent review](docs/assurance/README.md) |
| Manage access, privacy, migration, accessibility, recovery or reporting | [Platform services](docs/platform/README.md) |

## Design and verify a workflow

Use the [desk manuals](docs/handbook/README.md) for the operator's decisions, the [relationship map](docs/foundation/boundaries.md) for handoffs and the [record catalogue](docs/reference/records.md) and [field specifications](docs/implementation/README.md) for the data. The [worked decisions](docs/decisions/README.md) give exact expected outcomes for named church policies. The [verification guide](docs/verification/README.md) covers adoption, cross-department rehearsal and recovery. The [reference guide](docs/foundation/product-scope.md#reference-guides) connects selected ERP and LMS chapters to the church tasks that use them.
