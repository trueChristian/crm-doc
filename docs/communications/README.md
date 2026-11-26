# Communications and reminders

A secretary announces a changed service time, a team leader requests a volunteer's confirmation, a treasurer issues a private giving statement, and an archivist prints notices for members without digital access. All use the same dispatch register while retaining distinct eligibility, purposes, permissions and evidence.

| Need | Read | Operational result |
| --- | --- | --- |
| Register addresses, verify a messaging identity, choose topics and set quiet hours | [Recipients and channel policy](recipients-and-channels.md) | A current decision for a specific person, endpoint and purpose |
| Prepare a notice, translate it, select an audience and release it | [Campaigns and content](campaigns-and-content.md) | An approved edition with a reproducible intended audience |
| Trigger reminders, stop obsolete sends and handle calendar changes | [Reminders and orchestration](reminders-and-orchestration.md) | One accountable schedule for each eligible occurrence |
| Deliver, record replies, reconcile failures and prove what happened | [Delivery and responses](delivery-and-responses.md) | Per-recipient outcomes or one channel-post result |
| Operate pastoral contact lists, prayer requests, printable digests and emergency call trees | [Community communication](community-communication.md) | Permissioned sharing and accountable follow-through |

Logical tables use immutable `id` primary keys, and an `X ref` field identifies one X. A suffix `?` denotes optionality. Child records inherit their parent's organization scope. An instant includes a time reference independent of the current local clock. Restrict raw destinations, personal preferences, audience membership and provider response details to the roles that need them. Logs identify actor and purpose and hold only the minimum necessary message information.

The member can manage preferences without access to staff lists. A leader can send to eligible members of their own MinistryGroup. An editor drafts content, a reviewer approves protected topics, an operator resolves failures and a communication administrator manages approved sender identities. Report aggregates follow the same visibility rules as recipient-level records. Access restrictions on giving, safeguarding and pastoral information apply to messages, replies and attachments. An external provider sending a document on behalf of the church receives only the approved delivery package.

The canonical handoff starts with a DispatchRequest from an authorized business workflow. It must name its owner, purpose, audience, origin revision, approved content or template version, and duplicate-prevention key. Communications returns the dispatch reference, the next scheduled time if any, recipient exclusions a caller is authorized to see and the documented delivery outcomes. A successful channel post is one publication. Claiming that each subscriber received or read it requires separate individual evidence.
