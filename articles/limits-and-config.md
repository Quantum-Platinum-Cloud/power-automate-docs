---
title: Limits and configuration
description: Learn about limits and configuration.
services: ''
suite: flow
documentationcenter: na
author: ChrisGarty
Contributors:
  - ChrisGarty
  - PriyaKodukula
  - v-aangie
ms.subservice: cloud-flow
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2023
ms.author: CGarty
ms.reviewer: angieandrews
search.audienceType: 
  - flowmaker
  - enduser
---

# Limits for automated, scheduled, and instant flows

This topic contains information about the current limits and configuration details for automated, scheduled, and instant flows.

Check out the [pricing](https://make.powerautomate.com/pricing) for details on the different plans.

## Performance profiles

Flows have different limits depending on their *performance profile*. There are four possible values, depending on the flow owner's plan.

| Performance profile | Plans |
|---------------------|-------|
| Low                 | - Free <br />- Microsoft 365 plans <br /> - Power Apps Plan 1, Per App plans <br /> - Power Automate Plan 1 <br /> - All license trials <br>- Dynamics 365 Team Member<br>- Microsoft Power Apps for Developer | 
| Medium              | - Power Apps triggered flows, manual flows, child flows, Power Apps Plan 2, Power Apps per user plan <br />- Power Automate Plan 2, Power Automate per user, Power Automate per user with Attended RPA plans <br /> Dynamics 365 Enterprise plans, Dynamics 365 Professional plans<br /> - [Dynamics 365 non-licensed users, application users, users with special free licenses](/power-platform/admin/api-request-limits-allocations#non-licensed-usersapplication-usersusers-with-special-free-licenses)|
| High                | - Power Automate per flow plan |
| Unlimited Extended  | - Pay-as-you-go flows, Dynamics in context flows running under service principal  

If a user has multiple plans, such as a Microsoft 365 plan and a Dynamics 365 plan, the flow will have the performance profile of the higher of the two plans. For the exact set of plans that include Power Automate, go to the Microsoft [Power Platform Licensing Guide](https://go.microsoft.com/fwlink/p/?linkid=2085130).

If needed, users can review their current plan by opening the session debugging information by pressing **Ctrl** + **Alt** + **A** in the maker portal. The plan being used will have **isCurrent=true**.

The flow uses the plan of the owner of a cloud flow. If a cloud flow has been shared with multiple people, then generally the owner is the original creator. If you're unsure, you can change the owner of a cloud flow using the [Web API](web-api.md). At this time, if the original owner leaves an organization, the flow will be reverted to the **Low** performance profile.

## Flow definition limits

The following table contains the limits for a single flow definition.

| Name | Limit | Notes |
| ---- | ----- | ----- |
| Actions per workflow | 500 | You can add child flows to extend this limit, as needed. Flows with a large number of actions may encounter performance issues while you edit them, even if they have fewer than 500 actions. If you encounter performance issues while you edit your flow, consider using child flows to reduce the number of actions in a single flow. |
| Allowed nesting depth for actions | 8 | To extend this limit, you can add child flows as needed. |
| Switch scope cases limit | 25 | |
| Variables per workflow | 250 | |
| Name for `action` or `trigger` | 80 characters | |
| Characters per expression | 8,192 | |
| Length of `description` | 256 characters | |
| Maximum size for `trackedProperties` | 16,000 characters | |

## My flows limit

The following table contains the limit for the My flows and Team flows tab.

| Name | Limit | Notes |
| ---- | ----- | ----- |
| Number of flows owned by a single user | 600 | To extend this limit, use flows under solutions. |

## Duration and retention limits

The following tables contain the duration and retention limits.

### Duration limits

The following table contains the duration limits for a single flow run.

| Name | Limit | Notes |
|------|-------|-------|
| Run duration | 30 days |  Run duration is calculated by using a run's start time. Includes flows with pending steps like approvals. After 30 days, any pending steps time-out.|
| Run retention in storage | 30 days |  Run retention is calculated by using a run's start time. |
| Minimum recurrence interval | 60 seconds |
| Maximum recurrence interval | 500 days |
| Minimum postpone interval | 5 seconds for Low, 1 second for all others |

### Retention limits

The following table contains the limits on how long flows will remain turned on before they expire and get turned off.

| Name                 | Limit   | Notes |
|----------------------|---------|-------|
| Flows with errors    | 14 days |  A cloud flow that has a trigger or actions that fail continuously will be turned off. Fix your trigger or actions and turn on the  flow. These flows will have FlowSuspensionReason=AlwaysFailingDetected. |
| Not triggered (dormant) flows | 90 days for Free, Trial, Community and Microsoft 365 Plans.No expiration limit for all others | A cloud flow that has no successful triggers will expire and be turned off. After 90 days of inactivity, the flow creator and co-owners will receive an email. If no action is taken in next 30 days, the flow will be systematically turned off, and the creator and co-owners will be notified in an email. For enterprise scenarios, we recommend you buy a standalone Power Automate license listed on [Power Automate pricing](https://make.powerautomate.com/pricing) to ensure your flow isn’t turned off due to inactivity. You can turn your cloud flows back on anytime. These flows will have FlowSuspensionReason=NeverTriggeringDetected. |
| Consistently throttled flows | 14 days |A cloud flow that's consistently throttled for 14 days will be turned off. The flow creator and co-creators will get an email when the flow starts throttling and when the flow is turned off. For enterprise scenarios, we recommend you buy a standalone Power Automate license listed on [Power Automate pricing](https://make.powerautomate.com/pricing) to get higher action limits. You can turn your cloud flows back on anytime.|
|Premium flows without premium licenses| 14 days | Flows that were created with premium features (premium connectors, custom connectors, HTTP connectors, on premises gateway, and business process flows) but don't have a premium Power Automate license will be turned off after 14 days. This situation happens if the original owner leaves the organization, or if they have an expired trial or premium license. The flow owner and co-owners will get an email when the trial or premium license expires, or when the owner isn't found in Azure Active Directory (AAD). The flow will continue to work for 14 days. If a premium license isn't assigned to the flow within 14 days, the flow is automatically turned off, and the owner and co-owners are notified through email. Newly created or edited premium flows without a premium license are saved but turned off. Once a premium Power Automate license is assigned to the owner or flow, you can turn on the flow. Admins can [find these flows](/power-platform/admin/power-automate-licensing/faqs#how-can-i-identify-flows-that-need-premium-licenses-to-avoid-interruptions). Assign a per flow license or a per user license to the owner to keep the flow running.|
|Power Apps out of context flows| 90 days|Power Apps licenses include a limited set of Power Automate capabilities that allow for in context flows. To learn more, go to [Power Apps license questions](/power-platform/admin/power-automate-licensing/faqs#what-power-automate-capabilities-are-included-in-power-apps-licenses). Premium automated or scheduled flows not linked to an app require a Power Automate license, and the owner has 90 days to get a license before the flows turn off. Admins can [find these flows](/power-platform/admin/power-automate-licensing/faqs#how-can-i-identify-flows-that-need-premium-licenses-to-avoid-interruptions) and assign a per flow license or a Power Automate per user license to the owner to keep the flow running. Alternatively, if the flow is supporting a Power App, [associate the flow to the app](/power-platform/admin/power-automate-licensing/faqs#how-can-i-associate-in-context-flows-to-apps). Flows triggered by Power Apps are excluded from this enforcement. Starting June 1, 2023, new flows using premium features without a license will be turned off by default. Owners and co-owners of flows created before June 1, 2023 will be notified, have a 90-day grace period, and will be turned off starting September 1, 2023 if no action is taken. Turning on these flows requires a premium Power Automate license or association with the corresponding app.|
|Dynamics out of context flows| 90 days|Dynamics licenses include a limited set of Power Automate capabilities that allow users to run flows that allow for in context flows. To learn more, go to [Power Automate use rights included with Dynamics licenses](/power-platform/admin/power-automate-licensing/faqs#what-power-automate-capabilities-are-included-in-dynamics-365-licenses). Premium automated or scheduled flows not linked to an app require a Power Automate license, and the owner has 90 days to get a license before the flows turn off. Admins can [find these flows](/power-platform/admin/power-automate-licensing/faqs#how-can-i-identify-flows-that-need-premium-licenses-to-avoid-interruptions) and assign a per flow license to the flow or a Power Automate per user license to the owner to keep the flow running. Alternatively, if the flow is supporting a D365 app, [associate the flow to the app](/power-platform/admin/power-automate-licensing/faqs#how-can-i-associate-in-context-flows-to-apps). Starting June 1, 2023, new flows using premium features without a license will be turned off by default. Owners and co-owners of flows created before June 1, 2023 will be notified, have a 90-day grace period, and will be turned off starting September 1, 2023 if no action is taken. Turning on these flows requires a premium Power Automate license or association with the corresponding app. Flows using first party Dynamics apps or talking to Dynamics entities in Dataverse are excluded from this enforcement.|
|Over allocated per flow flows| 90 days|A Per flow license can only be assigned to one flow. Environments with more flows with per flow licenses than allowed will trigger email notifications to Owners and co-owners of newer per flow flows. Admins can [find these flows](/power-platform/admin/power-automate-licensing/faqs#how-can-i-identify-flows-that-need-premium-licenses-to-avoid-interruptions). Starting June 1, 2023, new flows can't use per flow plans if all plans are in use. Flows created before June 1, 2023 get a grace period of 90 days. If the owner of the flow has a Power Automate license, after 90 days, the flow will start using the owner's license. If no action is taken, the flows are turned off starting September 1, 2023. Assign a per flow license to the flow or a Power Automate per user license to the owner to keep the flow running.|
|Service Principal flows missing Per flow license | 90 days | Premium flows whose owner is a service principal will either need to have a per flow license or in the context of Dynamics 365 application. Starting June 1, 2023, new service principal flows using premium features without a Per flow license will be turned off by default. Owners and co-owners of flows created before June 1, 2023 will be notified, have a 90-day grace period, and will be turned off starting September 1, 2023 if no action is taken. Turning on these flows requires a premium Power Automate per flow license or [association with the corresponding Dynamics app](/power-platform/admin/power-automate-licensing/faqs#how-can-i-associate-in-context-flows-to-apps). Flows using first party Dynamics apps or talking to Dynamics entities in Dataverse are exempt from this enforcement.|

## Concurrency, looping, and debatching limits

The following table contains the limits for a single flow run.

| Name | Limit | Notes |
| ---- | ----- | ----- |
| Trigger concurrency | - Unlimited when the concurrency control is turned off <br />- 25 is the default limit when the concurrency control is turned on, which you can't undo after you enable concurrency. You can change the default to a value between 1 and 100 inclusively in the settings for the trigger under **Concurrency Control**. | This limit describes the highest number of flow runs that can run at the same time, or in parallel. <br />**Note**: When concurrency is turned on, the SplitOn limit is reduced to 100 items for debatching arrays. |
| Maximum waiting runs | - With concurrency, the minimum number of waiting runs is the number of concurrent runs (trigger concurrency). As this is dependent on runtime behavior, use the trigger concurrency setting instead. | This limit describes the highest number of flow runs that can wait to run when your flow is already running the maximum concurrent instances. |
| Apply to each array items | 5,000 for Low, 100,000 for all others | This limit describes the highest number of array items that an "apply to each" loop can process. <br />To filter larger arrays, you can use the query action. |
| Apply to each concurrency | 1 is the default limit. You can change the default to a value between 1 and 50 inclusively. | This limit is highest number of "apply to each" loop iterations that can run at the same time, or in parallel. |
| Split on items | - 5,000 for Low without trigger concurrency  <br />- 100,000 for all others without trigger concurrency <br />- 100 with trigger concurrency | For triggers that return an array, you can specify an expression that uses a 'SplitOn' property that splits or debatches array items into multiple workflow instances for processing, rather than use a "Foreach" loop. This expression references the array to use for creating and running a workflow instance for each array item. <br />**Note**: When concurrency is turned on, the Split on limit is reduced to 100 items. |
| Until iterations | - Default: 60 <br />- Maximum: 5,000 | |
| Paginated items | 5,000 for Low, 100,000 for all others | To process more items, trigger multiple flow runs over your data. |

## Throughput limits

Here are the time-bound limits for a single version of a cloud flow definition. These limits apply across all runs of the flow version, and are calculated on sliding windows.

If a cloud flow exceeds one of the limits, activity for the flow will be slowed and will automatically resume when the sliding window has activity below the limit. However, if a cloud flow consistently remains above the limits for 14 days, it will be turned off (see above duration limits). Be sure to monitor email for notifications about such flows. If a cloud flow consistently exceeds the limits, you'll need to update the flow to remain below the limits to prevent it from being turned off.

>[!TIP]
>Because these limits are for a single version, if you update your flow it will reset these limits.

### Power platform request limits

Power platform request limits are limits to the number of requests a cloud flow can run. To learn more about Power platform requests, go to [Power Platform requests](/power-platform/admin/power-automate-licensing/types#power-platform-requests). These requests are counted for all types of actions, including connector actions, HTTP actions, and built-in actions from initializing variables to a simple compose action. Both succeeded and failed actions count towards these limits. Additionally, retries and additional requests from pagination count as action runs. You can see the number of actions your flow has run by selecting **Analytics** from the flow details page and reviewing the **Actions** tab.

| Name | Transition period limit | Notes |
| ---- | ----- |----- |
| Power platform requests per 5 minutes | 100,000 | Distribute the workload across more than one flow as necessary. |
| Power platform requests per 24 hours|10,000 for Low, 100,000 for Medium, 500,000 for High, up to 10,000,000 for Unlimited Extended | Because of the current [transition period](/power-platform/admin/power-automate-licensing/types#transition-period), these limits are less strict than the values called out in [Requests limits and allocations](/power-platform/admin/api-request-limits-allocations). These limits represent approximations of how many requests will be allowed daily. They aren't guarantees. Actual amounts may be smaller, but will be greater than the documented requests limits and allocations during the transition period. The documented limits were substantially increased in late 2021. For public preview reporting for Power Platform requests, go to [View detailed Power Platform request usage information in the Power Platform admin center (preview)](/power-platform/admin/api-request-limits-allocations#view-detailed-power-platform-request-usage-information-in-the-power-platform-admin-center-preview). Any potential high usage enforcement based on these [limits](/power-platform/admin/api-request-limits-allocations) wouldn't start until six months after reports have been made generally available. Distribute the workload across more than one flow as necessary. | 
| Concurrent outbound calls | 500 for Low, 2,500 for all others | You can reduce the number of concurrent requests or reduce the duration as necessary. |

As of October 2019, there are limits on the number of Microsoft Power Platform requests an account can make across all of their flows, Power Apps, or any applications calling into the Microsoft Dataverse. No performance is guaranteed above these limits, although enforcement of these limits isn't as strict during the transition period. To learn more, go to [Requests limits and allocations](/power-platform/admin/api-request-limits-allocations).

>[!TIP]
>Individual connectors have their own limits, which often will be reached before the limits mentioned earlier. Be sure to check the documentation for your connector on [Power Platform and Azure Logic Apps connectors documentation](/connectors/).

### Runtime endpoint request limits

The runtime endpoint is the direct access URL for a given flow. It starts with something like: `https://prod-00.westus.logic.azure.com:443/`.

| Name | Limit | Notes |
| ---- | ----- | ----- |
| Concurrent inbound calls | ~1,000 | You can reduce the number of concurrent requests or reduce the duration as necessary. |
| Read calls per 5 minutes  | 6,000 for Low, 60,000 for all others | This limit applies to calls that get the raw inputs and outputs from a cloud flow's run history. You can distribute the workload across more than one flow as necessary. |
| Invoke calls per 5 minutes | 4,500 for Low, 45,000 for all others | You can distribute workload across more than one flow as necessary. |

### Content throughput limits

The content throughput limits refer to the amount of data that's read from or written to the run history of the cloud flow.

| Name | Limit | Notes |
| ---- | ----- | ----- |
| Content throughput per 5 minutes | 600 MB for Low, 6 GB for all others | You can distribute workload across more than one flow as necessary. |
| Content throughput per 24 hours | 1 GB for Low, 10 GB for Medium, 50 GB for High | You can distribute workload across more than one flow as necessary. |

## Gateway limits

Power Automate supports write operations, including inserts and updates, through the gateway. However, these operations have [limits on their payload size](/data-integration/gateway/service-gateway-onprem#considerations).

## HTTP limits

Here are the limits for a single outgoing or incoming HTTP call:

### Timeout

Some connector operations make asynchronous calls or listen for webhook requests, so the timeout for these operations might be longer than these limits. For more information, see the technical details for the specific connector.

| Name | Limit | Notes |
|------|-------|-------|
| Outbound synchronous request | 120 seconds <br>(2 minutes) | Examples of outbound requests include calls made by HTTP triggers. <br />**Tip**: For longer running operations, use an asynchronous polling pattern or an until loop. To work around timeout limits when you call another flow that has a callable endpoint, you can use the built-in action instead, which you can find in the connector picker under **Built-in**. |
| Outbound asynchronous request | Configurable up to 30 days |  |
| Inbound request | 120 seconds <br>(2 minutes) | Examples of inbound requests include calls received by request triggers and webhook triggers. <br />**Note**: For the original caller to get the response, all steps in the response must finish within the limit unless you call another flow as a child flow. |

>[!NOTE]
>If you test a cloud flow that runs for longer than 10 minutes, you may get a timeout message in Power Automate, even though the flow continues to run in the background. If this happens, re-open the view to receive the current status.

### Message size

| Name | Limit | Notes |
|------|-------|-------|
| Message size | 100 MB | To work around this limit, consider allowing chunking under the action content transfer settings. However, some connectors and APIs might not support chunking or even the default limit.|
| Message size with chunking | 1 GB | This limit applies to actions that either natively support chunking or let you enable chunking in their runtime configuration. |

### Character limits

| Name | Limit | Notes |
|------|-------|-------|
| Expression evaluation limit | 131,072 characters | The `@concat()`, `@base64()`, `@string()` expressions can't be longer than this limit. |
| Request URL character limit | 16,384 characters |

### Retry policy

#### Default retry policy

| Performance profile | Description |
| ------------------- | ----------- |
| Low | This policy sends up to two retries at *exponentially increasing* intervals, which scale by 5 minutes up to an interval of approximately 10 minutes for the last retry. |
| Medium, High | This policy sends up to eight retries at *exponentially increasing* intervals, which scale by seven (7) seconds up to an interval of approximately 15 minutes for the last retry. |

#### Retry setting limits

To change the default settings, use the retry policy parameter. Here are the limits for the retry settings.

| Name | Limit |
| ---- | ----- |
| Retry attempts | 90 |
| Retry maximum delay | 1 day |
| Retry minimum delay | 5 seconds |

For more information on other retry policies, go to **Handle errors and exceptions in Azure Logic Apps**, [Retry policies](/azure/logic-apps/logic-apps-exception-handling#retry-policies).

## Turning off or deleting flows

When you turn off a cloud flow, no new runs are instantiated. All in-progress and pending runs continue until they finish, which might take time to complete.

When you delete a cloud flow, no new runs are instantiated. All in-progress and pending runs are canceled. If you have thousands of runs, cancellation might take significant time to complete.

## Custom connector limits

Here are the limits for custom connectors that you can create from web APIs.

| Name | Limit |  Notes |
|------|-------|-------|
| Number of custom connectors | 50 per user ||
| Number of requests per minute for a custom connector | 500 requests per minute per connection |  |

>[!NOTE]
>You must have a premium or trial license to run any flow that has a custom connector.

## SharePoint limits

There are [limitations](/connectors/sharepointonline/#limits) on how you can use Microsoft SharePoint with Power Automate and Power Apps.

[!INCLUDE [sharepoint-detailed-docs](includes/sharepoint-detailed-docs.md)]

## IP addresses

Requests from Power Automate use IP addresses that are associated with the region of the [environment](./environments-overview-maker.md) in which your flow exists.

Calls made from connectors in cloud flows come from [these IP addresses](/connectors/common/outbound-ip-addresses#power-platform). Add them to your network's allow list to facilitate communications from Power Automate.

## Allow list of namespaces endpoints required for runtime

By default, administrators need to authorize endpoints, including **\*.servicebus.windows.net**, to allow desktop flow runs.

If you don’t want to authorize this public endpoint, you can alternatively allow all the following namespace endpoints.

> [!NOTE]
> This list of namespace endpoints can evolve. Therefore, ensure that you regularly check this page to keep the list of authorized endpoints up to date.

| **URI**                                                                   | **Power Platform Region** | **Is preview** |
|---------------------------------------------------------------------------|----------------------|-----|
| prodnorwayeastmmrns-1-whuok7nwdzy2s.servicebus.windows.net                | Norway               |  No |
| prodnorwaywestmmrns-1-oa47o5hk7gvoo.servicebus.windows.net                | Norway               |  No |
| prodkoreacentralmmrns-1-4gkez6gmtnxxy.servicebus.windows.net              | Korea                |  No |
| prodkoreasouthmmrns-1-o7ut2fobjmj7k.servicebus.windows.net                | Korea                |  No |
| prdnzammrns-1-8vyvi02tfal5rjlmfsqvqs7dtx9ph4xegxxh.servicebus.windows.net | South Africa         |  No |
| prdnzammrns-1-oqy5jh1vwobriyl4u6ameplcssg308bohfwd.servicebus.windows.net | South Africa         |  No |
| prdeusmmrns-3-gh4xbnrswp4annlprgyqmdwyziat22jn2hmt.servicebus.windows.net | United States        | Yes |
| prdeusmmrns-3-ju5nmbisb8h7216w1o1md66mv77e0uh0gbqt.servicebus.windows.net | United States        | Yes |
| previeweastusmmrns-1-fmkqes4e4ximc.servicebus.windows.net                 | United States        | Yes |
| previeweastusmmrns-2-HWd3f6eulXLM.servicebus.windows.net                  | United States        | Yes |
| previewwestusmmrns-1-uwbsm24d2qrgi.servicebus.windows.net                 | United States        | Yes |
| previewwestusmmrns-2-J5NRqQ0tPJ3n.servicebus.windows.net                  | United States        | Yes |
| prdeusmmrns-11-u9pep9gw4ehrsgnxtu72spfhhrsmmgbom99.servicebus.windows.net | United States        |  No |
| prdeusmmrns-11-vi712adqt8zhhekoz48g0rj96ahcs2lngln.servicebus.windows.net | United States        |  No |
| prdeusmmrns-12-kkx3ko9h7a3q8fyzodjpc9s2n6l6emux4le.servicebus.windows.net | United States        |  No |
| prdeusmmrns-12-p04f5v86v08h7bckioz41ml1nchtgged6jn.servicebus.windows.net | United States        |  No |
| prdeusmmrns-13-mt5nm5ozm9y379uildo40xevuc7i6og9jib.servicebus.windows.net | United States        |  No |
| prdeusmmrns-13-nsa7ru2qzbhpdbjkqn1xe0tr35y03igcvpg.servicebus.windows.net | United States        |  No |
| prdeusmmrns-16-1httpeaxvd89sv9y92f3tsabapkcrsa2t8f.servicebus.windows.net | United States        |  No |
| prdeusmmrns-17-3zk2vbt7quh9qmfd81la44igwcw2claddv8.servicebus.windows.net | United States        |  No |
| prdeusmmrns-17-w641qe2st5y4iif6hts0p9xzo17m6yxzhc2.servicebus.windows.net | United States        |  No |
| prdeusmmrns-18-cxlk5673wpp7ced81cdeykv71er75pkq2r0.servicebus.windows.net | United States        |  No |
| prdeusmmrns-19-738isaepl448wtnw0210lqytrtiz4hvrzjf.servicebus.windows.net | United States        |  No |
| prdeusmmrns-20-34ftg033c3iylghwgj16m3dqpccd4nbigp0.servicebus.windows.net | United States        |  No |
| prdeusmmrns-20-fdacpnw20pftxqx9bmn7137pqrn5o1g4tnl.servicebus.windows.net | United States        |  No |
| prdwusmmrns-10-1agsripqec30708vj3ithv3dp8lg5kr5s3n.servicebus.windows.net | United States        |  No |
| prdwusmmrns-10-ebhaiy2tuf6jrr41h531fhdct7iu4v7idm4.servicebus.windows.net | United States        |  No |
| prdwusmmrns-14-8pj3mtexc3t96c6to5denqxm2rq7w01s6nw.servicebus.windows.net | United States        |  No |
| prdwusmmrns-14-u8lv1g6tp94vvp06h847g4zczi9s8fob3wu.servicebus.windows.net | United States        |  No |
| prdwusmmrns-15-wrozqfemq1qibz5ykjjzjkpm5s80bogumtd.servicebus.windows.net | United States        |  No |
| prdwusmmrns-15-xebdresepogmc40q3nznan4w1wvtooaa20k.servicebus.windows.net | United States        |  No |
| prdwusmmrns-16-mphmqg4oagnzzci27l1sd5ggamvhr9vayx8.servicebus.windows.net | United States        |  No |
| prdwusmmrns-18-cb9mb3sevtl0au7kvr5h7xft35nnzvaiby7.servicebus.windows.net | United States        |  No |
| prdwusmmrns-19-zv1krgy2m185ioa8vk8dvqmc8omimizwew3.servicebus.windows.net | United States        |  No |
| prdwusmmrns-21-naj2wt2tqebvv102pz8embfe50se1gdpb4i.servicebus.windows.net | United States        |  No |
| prdwusmmrns-21-t5svpy06ve482zb6oljzrqdohkrfx42xvxz.servicebus.windows.net | United States        |  No |
| prdwusmmrns-23-hisirbhw8e6hi1hdg37354tvv4rtyvosxui.servicebus.windows.net | United States        |  No |
| prdwusmmrns-23-pflxh92egchq0oxbef9hy49s5p5eucq5oij.servicebus.windows.net | United States        |  No |
| prdwusmmrns-25-8rz4j9842zpjqr8e7vrjjykzr3fnxypmad0.servicebus.windows.net | United States        |  No |
| prdwusmmrns-25-ct38n2ulxz7081mttf5sha5n2kq2skl1sux.servicebus.windows.net | United States        |  No |
| prdwusmmrns-26-cgqwgm01glorgvdrblvr9uzf80e45skb2xo.servicebus.windows.net | United States        |  No |
| prdwusmmrns-26-o3ljq2nytljdghu6h1wqbpyqaxbiqbi4pte.servicebus.windows.net | United States        |  No |
| prdwusmmrns-27-der2ntjxpz5i2uqshm9vznltkhngn06xlyg.servicebus.windows.net | United States        |  No |
| prdwusmmrns-28-t4d8h0j42o6jjs2i2e3fm6fj30wy7j3k7ip.servicebus.windows.net | United States        |  No |
| prdwusmmrns-29-9zr3xphm5vb2snbr9d8fay99ejze0ggwvue.servicebus.windows.net | United States        |  No |
| prdwusmmrns-29-aerqzlinnqitgyqsa0lmh5lbrs1ady3nfck.servicebus.windows.net | United States        |  No |
| prdwusmmrns-34-mmpbgjlfm4ydo3amtopfs2moy9b2zo1xoo8.servicebus.windows.net | United States        |  No |
| prdwusmmrns-34-rp998x7g6h4lu5ksitso69xwvky5oh3cxfq.servicebus.windows.net | United States        |  No |
| prdwusmmrns-6-04hdqdf3chg2n2t4siaal0v5hwqas9zbt6vx.servicebus.windows.net | United States        |  No |
| prdwusmmrns-6-cwodfc8u8qqrqielru8w7ckyrj5le87q1ozi.servicebus.windows.net | United States        |  No |
| prdeusmmrns-22-wsbpw23z70wq24aypvkvtlgbhzp0xe70ne2.servicebus.windows.net | United States        |  No |
| prdeusmmrns-22-x6bcxy40pv2hpfpzrjx21ssdu8rvawtr8w8.servicebus.windows.net | United States        |  No |
| prdeusmmrns-24-suv0kt1lf0ok7hua0ccogywp15p6kcx04x2.servicebus.windows.net | United States        |  No |
| prdeusmmrns-24-y9wy0tcmsgspsjhf8ur7z08mjztmffq9goe.servicebus.windows.net | United States        |  No |
| prdeusmmrns-27-8t7l05rslj7qwfsgxu18q3h7aypmztd5fdj.servicebus.windows.net | United States        |  No |
| prdeusmmrns-28-0cprxw2r4q5sw0c94hcsf0dme1y4svhlm8o.servicebus.windows.net | United States        |  No |
| prdeusmmrns-3-1fmod9del85tghiub70xfpgavep5tpqbixbq.servicebus.windows.net | United States        |  No |
| prdeusmmrns-3-xgpjelrz4vp0e5dt2nnl8l29tiu6r3ksg174.servicebus.windows.net | United States        |  No |
| prdeusmmrns-30-ft1ogu8rkhcami798vghm3lye1y9ca4nq6g.servicebus.windows.net | United States        |  No |
| prdeusmmrns-30-v63cua3zd53b7dznsybo56mdb5112f30wlr.servicebus.windows.net | United States        |  No |
| prdeusmmrns-32-1e8py596s9z03jv9brc4p1u89h9pr7ka52j.servicebus.windows.net | United States        |  No |
| prdeusmmrns-32-91xx20kvkw12y878prtg9uq2z3a4nxcb4sh.servicebus.windows.net | United States        |  No |
| prdeusmmrns-33-83pgwjs703eluiqyo20zgkqpi79y41w0zyj.servicebus.windows.net | United States        |  No |
| prdeusmmrns-33-t46vqpf8wplhrjsp9yqfn1tzaoq1sft1tsm.servicebus.windows.net | United States        |  No |
| prdeusmmrns-4-c31zz9l8qalw7h1pvr18glfxqptzq6ph34dl.servicebus.windows.net | United States        |  No |
| prdeusmmrns-4-r2gcr4bg70k14spwohd1yeijpvstud3deq82.servicebus.windows.net | United States        |  No |
| prdeusmmrns-5-3jof0fvvl3astjtfo2gikxpimouynog68o6r.servicebus.windows.net | United States        |  No |
| prdeusmmrns-5-5x8c4o299zquku2yauz4yo813as2g22zhsf9.servicebus.windows.net | United States        |  No |
| prdeusmmrns-9-6nsicrn14urv2cjs87z4955gptr3s0x8plbv.servicebus.windows.net | United States        |  No |
| prdeusmmrns-9-rgbo8j4gzrecu7x89g76kxggt23lz58npwsm.servicebus.windows.net | United States        |  No |
| prdwusmmrns-7-7tmen1irly7syq5c0fthjskb0lf1613g6ymt.servicebus.windows.net | United States        |  No |
| prdwusmmrns-7-i48wrshewyk88q4s5kp39zrd498usidvd9z0.servicebus.windows.net | United States        |  No |
| prdwusmmrns-8-jrn8ds8r8py7w4gi2wk1vpymyqkxionnli2s.servicebus.windows.net | United States        |  No |
| prdwusmmrns-8-wwr2q3m9lkv3f49ondkfj3x8yc2iradok3pz.servicebus.windows.net | United States        |  No |
| prodeastusmmrns-1-plck7l3prc43s.servicebus.windows.net                    | United States        |  No |
| prodeastusmmrns-2-uvq9wfwvvrbqg.servicebus.windows.net                    | United States        |  No |
| prodwestusmmrns-1-3r77ocb7nmtak.servicebus.windows.net                    | United States        |  No |
| prodwestusmmrns-2-wt88pe23kbp8g.servicebus.windows.net                    | United States        |  No |
| prdeusmmrns-31-awy3sb1iblyim8xdejbyg4xtt4revfqjai3.servicebus.windows.net | United States        |  No |
| prdeusmmrns-31-bai0vj8wzgejcj6xzbukvvfcaqpiouccjmb.servicebus.windows.net | United States        |  No |
| prdwukmmrns-2-655eda4qyw2sv8yoh48rvypa4cgywlbwcqhv.servicebus.windows.net | United Kingdom       |  No |
| prdwukmmrns-2-vn35h7uhxr3nriaunptdudd0avl6nzhnglhr.servicebus.windows.net | United Kingdom       |  No |
| produksouthmmrns-1-cx4kejh3frvae.servicebus.windows.net                   | United Kingdom       |  No |
| produkwestmmrns-1-ndmh2gqzqj6e4.servicebus.windows.net                    | United Kingdom       |  No |
| prodjapaneastmmrns-1-nafowbv7uqqzi.servicebus.windows.net                 | Japan                |  No |
| prodjapanwestmmrns-1-7fhv7yfs3b7oo.servicebus.windows.net                 | Japan                |  No |
| prdwjpmmrns-5-alkrfltpxcxxjdgdvullh28wv064it08xh7p.servicebus.windows.net | Japan                |  No |
| prdwjpmmrns-6-4zas09oyw0z88m15l32s4hqcfrlavchfpso8.servicebus.windows.net | Japan                |  No |
| prdwjpmmrns-6-r9onumpa34h1abopfbtz7387zvqmwdk9yz52.servicebus.windows.net | Japan                |  No |
| prdwjpmmrns-7-59gnwfs0axi99oh46nieh0amw9lz8rvkm0ev.servicebus.windows.net | Japan                |  No |
| prdwjpmmrns-7-94nw9gtat4zpo97jcgudkgvc2ge48b2zdylb.servicebus.windows.net | Japan                |  No |
| prdwjpmmrns-9-mf0gib6ot7yzs53fon9908m9abwa7tqlqmbf.servicebus.windows.net | Japan                |  No |
| prdwjpmmrns-9-rysrv03djr8ojnp0e0lo60k6fp0ppa8aka9z.servicebus.windows.net | Japan                |  No |
| prdwjpmmrns-3-jrzvs2jn2wfqhqdm78w4opp4j07woaerh9a4.servicebus.windows.net | Japan                |  No |
| prdwjpmmrns-13-dz20gg7ban7335qy3uuu2bhdokzhqguluxi.servicebus.windows.net | Japan                |  No |
| prdwjpmmrns-5-183yd443d6abopy05eqhnx6ppzgdlz9cg0lw.servicebus.windows.net | Japan                |  No |
| prdwjpmmrns-2-z1iyi9x93h8a5p2rf0bxpa3xkr3s1st0shem.servicebus.windows.net | Japan                |  No |
| prdwjpmmrns-2-zwl9wqzfhhuj8de04s6iyo320gmvbshaqwpr.servicebus.windows.net | Japan                |  No |
| prdwjpmmrns-15-mzoitgrmkb9x8qt7shqm1a3ad3t45qb3l75.servicebus.windows.net | Japan                |  No |
| prdwjpmmrns-3-h62j5nlty1v9x4auvdejpwe7ngo3lsgau6fb.servicebus.windows.net | Japan                |  No |
| prdejpmmrns-14-osbksh1kc2h9bc5zynk6485ttm162r7qmb8.servicebus.windows.net | Japan                |  No |
| prdejpmmrns-15-tovckjt2c987eih8021ez4pa1hrwcrd3043.servicebus.windows.net | Japan                |  No |
| prdejpmmrns-4-0bq94lkcwh89ljh00y238hjallak9rtw5mwo.servicebus.windows.net | Japan                |  No |
| prdejpmmrns-4-8ox2iqi1zw8g4g6npao62epqsif70pxqwhlt.servicebus.windows.net | Japan                |  No |
| prdejpmmrns-8-rja3avsyaksfqqkfmsxejpt1f5gw0l5rjhek.servicebus.windows.net | Japan                |  No |
| prdejpmmrns-8-yqkn1hnj6urmthhsi2nd3r6tmacw06k6s0xl.servicebus.windows.net | Japan                |  No |
| prdwjpmmrns-10-i4t18vcq6bymi0q41ct6l9omrsmpu1xb66q.servicebus.windows.net | Japan                |  No |
| prdwjpmmrns-11-db2a6de90pl6bqjuorg331y7hwlt3ksb9je.servicebus.windows.net | Japan                |  No |
| prdwjpmmrns-13-yctdcx8q7te9y7q36umn9nrp6cxdss5gd6t.servicebus.windows.net | Japan                |  No |
| prdejpmmrns-10-bstijlyba2qkct0t5sre5vfbtr0k3r2756i.servicebus.windows.net | Japan                |  No |
| prdejpmmrns-11-j5a9t7g5ye30tcbyr3qeylocw36g4fw5jiz.servicebus.windows.net | Japan                |  No |
| prdejpmmrns-12-pje8gv6enxklxo1fuhiztzlpxdf6hrn0y5c.servicebus.windows.net | Japan                |  No |
| prdejpmmrns-12-xzbymnq8jbxzzf8rw0gd9amryk5y0sqkuhi.servicebus.windows.net | Japan                |  No |
| prdejpmmrns-14-j9jags4umi7jkuje9a7syf8wo9wrk9p1sma.servicebus.windows.net | Japan                |  No |
| prdsinmmrns-2-yg3uf3bg2tx76131363l5twjngscb68cdztl.servicebus.windows.net | India                |  No |
| prdcinmmrns-3-wnn89ixhem8i605q4edtwo9r8r0t2796kx3d.servicebus.windows.net | India                |  No |
| prdsinmmrns-2-rdf8f0ew8d30vxdo2y9l17npmi44q7s6w7z9.servicebus.windows.net | India                |  No |
| prdcinmmrns-3-t2y6tdtbryy4k4c1l4tffmdx0b7k4ikerkaa.servicebus.windows.net | India                |  No |
| prodsouthindiammrns-1-7kqjp7tvfvvku.servicebus.windows.net                | India                |  No |
| prodcentralindiammrns-1-h34hrnss44v7s.servicebus.windows.net              | India                |  No |
| prodfrancecentralmmrns-1-xzhxhbzl7vhc6.servicebus.windows.net             | France               |  No |
| prodfrancesouthmmrns-1-xorsknhtb2lm2.servicebus.windows.net               | France               |  No |
| prdweummrns-26-ldz8cnwwyocr0ejev8xvyhiezuxmdq1yxqk.servicebus.windows.net | Europe               |  No |
| prdweummrns-6-715t9odrb0d5xqu9mcvl95tl3vss0h4ywvql.servicebus.windows.net | Europe               |  No |
| prdweummrns-6-k903fojp2zajhe9m2uy026gmd8o92j7egocc.servicebus.windows.net | Europe               |  No |
| prdweummrns-7-ieo6v7w85hvc7kfspwkn5iwga4sfx906lb4n.servicebus.windows.net | Europe               |  No |
| prdweummrns-7-mxvjm5wdlp57s36i1tnari51ork5qz16q1f2.servicebus.windows.net | Europe               |  No |
| prdweummrns-9-igv6i1ythpy1wz7sayq1fvnxh5bkakwz06i3.servicebus.windows.net | Europe               |  No |
| prdweummrns-9-ngzlxpwmf83v36kz9qf7xlnexgbf5v8fpggk.servicebus.windows.net | Europe               |  No |
| prodnortheuropemmrns-1-jc3usmvyk4wcy.servicebus.windows.net               | Europe               |  No |
| prodnortheuropemmrns-2-y9bgs3kphntyf.servicebus.windows.net               | Europe               |  No |
| prodwesteuropemmrns-1-il3kcpbupz3gm.servicebus.windows.net                | Europe               |  No |
| prodwesteuropemmrns-2-p1m53clst99fe.servicebus.windows.net                | Europe               |  No |
| prdneummrns-10-dfsba8r6fetlj0naynltmekwrx8s8mgbb26.servicebus.windows.net | Europe               |  No |
| prdneummrns-10-xlb6mnbn4oo6i2836ys0z23370t9qmg1z8v.servicebus.windows.net | Europe               |  No |
| prdneummrns-11-4h432bhqewib20lftea3c7xrlmuzr8a66pc.servicebus.windows.net | Europe               |  No |
| prdneummrns-11-fc9x0e1i5yf1rb37iug3bend5k0v32rq59k.servicebus.windows.net | Europe               |  No |
| prdneummrns-12-q8mb2fc6q3h1kuct9tvxhya46eyuso4e8iz.servicebus.windows.net | Europe               |  No |
| prdneummrns-12-qfegk9w902b6b3difrniuhv2hyo9lug1yxk.servicebus.windows.net | Europe               |  No |
| prdneummrns-15-2wuay5ujwfhkb3tkk4tt05g6qj7k5p3jkve.servicebus.windows.net | Europe               |  No |
| prdneummrns-15-xxqly3x8p04ydglxhb8p7pyup7jngl8apy5.servicebus.windows.net | Europe               |  No |
| prdneummrns-17-6ku1rh49w81ofdmrr3c5bo8ssui68zbozjl.servicebus.windows.net | Europe               |  No |
| prdneummrns-17-argn0agthuw69l4njzblsmbi697b77nz62l.servicebus.windows.net | Europe               |  No |
| prdweummrns-13-3d8l3g60vj020rzpnv0vb7hrk348wymi9fb.servicebus.windows.net | Europe               |  No |
| prdweummrns-13-xvjnyxshe38m9o8bwp8axrxoqlg4tjbyrle.servicebus.windows.net | Europe               |  No |
| prdweummrns-14-m17rqz9zbhu9d98tttthmxy4no6ou21268v.servicebus.windows.net | Europe               |  No |
| prdweummrns-14-oz7piy3p711feggc608fa8isdynyis8sffv.servicebus.windows.net | Europe               |  No |
| prdweummrns-16-2rhp0evcj8avmcvwzdls9r4n8byctxnyb7p.servicebus.windows.net | Europe               |  No |
| prdweummrns-16-soafhbsvtlwquwzxi03onf8oa25f93kcboi.servicebus.windows.net | Europe               |  No |
| prdweummrns-19-yeh6wlbkp1av8roke94xgi3iqpx2a3xtvj9.servicebus.windows.net | Europe               |  No |
| prdweummrns-20-jfd262oyt2s5i2m9afvhmmn7oh8m9ylt87t.servicebus.windows.net | Europe               |  No |
| prdweummrns-20-kb4j7ljpdtkqjzzd1cf2y7ud79apid1azpx.servicebus.windows.net | Europe               |  No |
| prdweummrns-22-roua85rgg4d3omi9cnq0gm3q5ykjej2fp48.servicebus.windows.net | Europe               |  No |
| prdweummrns-23-pxf43dpfsyd3m6dqldszf6735fqy419mxw8.servicebus.windows.net | Europe               |  No |
| prdweummrns-24-ho7hs6f61184mawfirly3xohh3hqtwm7cpv.servicebus.windows.net | Europe               |  No |
| prdweummrns-25-czz7mnkehsuki22mmitllf8mo7klfqwpkkg.servicebus.windows.net | Europe               |  No |
| prdneummrns-18-6e9asgh3q54wug2g85c7dvtwysx5vg38qn4.servicebus.windows.net | Europe               |  No |
| previewnortheuropemmrns-1-ny3jbez7yclw4.servicebus.windows.net            | Europe               | Yes |
| previewwesteuropemmrns-1-pli5p5xheu4lc.servicebus.windows.net             | Europe               | Yes |
| prdneummrns-18-6ycvn49mc7zhbshadks0tfjwjg6g1q9f6g2.servicebus.windows.net | Europe               |  No |
| prdneummrns-19-0pfazhfb4vytcl52r6dryrgi71aufv5pw14.servicebus.windows.net | Europe               |  No |
| prdneummrns-21-rx2d4tdu9zyhb9br9n6v06xhlnyd9em854v.servicebus.windows.net | Europe               |  No |
| prdneummrns-21-y72fn30ujex4govc1yzvpvyp2j782gd2zwc.servicebus.windows.net | Europe               |  No |
| prdneummrns-22-xzhu3hmk0w19hprhbce39d18b5lioem8ywk.servicebus.windows.net | Europe               |  No |
| prdneummrns-23-1jsqh281qvmjp09kut3auw06bad16ht2z6f.servicebus.windows.net | Europe               |  No |
| prdneummrns-24-est7ogob7mhkjqygi9fncj64cp1f92olgkx.servicebus.windows.net | Europe               |  No |
| prdneummrns-25-l16teela0xo5gj401u2bqjx8lvevpkv4yy5.servicebus.windows.net | Europe               |  No |
| prdneummrns-26-6v8e6mten7nvn78qpgfrke2ogedjedwxdqe.servicebus.windows.net | Europe               |  No |
| prdneummrns-3-ijnvx1ne9xr4cdg4boj0ko17o6r0mo01fxry.servicebus.windows.net | Europe               |  No |
| prdneummrns-3-w7wi2kmzbqlyhbgz8or8ccsv6dt4kcq7wng4.servicebus.windows.net | Europe               |  No |
| prdneummrns-4-6eadpq66lmsng2z3qfbt5h0dz8y1ev1g7f9f.servicebus.windows.net | Europe               |  No |
| prdneummrns-4-saphm2ye8z0dvr0cjifyo7nq1e20umpb3ulp.servicebus.windows.net | Europe               |  No |
| prdneummrns-5-2ksg36axkdor8krdojxudtq9kaylps6amcf0.servicebus.windows.net | Europe               |  No |
| prdneummrns-5-qphyin8kfcgypsb7b6wjf6lxijd8v3xx2of9.servicebus.windows.net | Europe               |  No |
| prdneummrns-8-ieav13ew8673n0h1okr1ehlg65hr90vzwq57.servicebus.windows.net | Europe               |  No |
| prdneummrns-8-o2j51ngtrr5uevmw8af9jfpnz8ycydpghlv5.servicebus.windows.net | Europe               |  No |
| prdndemmrns-2-go7xeqf077mt2vuq4dyth0gwfm9s2aemmjm9.servicebus.windows.net | Germany              |  No |
| prdndemmrns-2-yqlb2eueujjpuxauq3us19ia6pboepamtmdh.servicebus.windows.net | Germany              |  No |
| prodgermanynorthmmrns-1-q7unzu7nsvdxg.servicebus.windows.net              | Germany              |  No |
| prodgermanywestcentralmmrns-1-zqcmawxslzfbi.servicebus.windows.net        | Germany              |  No |
| prdnchmmrns-2-6aufi5bwfag8r54td32bjj8bpl845eagkz2y.servicebus.windows.net | Switzerland          |  No |
| prdnchmmrns-2-d8hfqw2v8niumsl2jaqjrqq4lhp10rvjnjc9.servicebus.windows.net | Switzerland          |  No |
| prodswitzerlandnorthmmrns-1-2d2uums4njavc.servicebus.windows.net          | Switzerland          |  No |
| prodswitzerlandwestmmrns-1-n3jwwj2am7fgy.servicebus.windows.net           | Switzerland          |  No |
| prdccammrns-2-8s6kb0vay4f0koa6jsws726gyns43uh4591e.servicebus.windows.net | Canada               |  No |
| prdecammrns-2-ginyhguvgct78u1knii7f1m6vfrsubf8gr8f.servicebus.windows.net | Canada               |  No |
| prodcanadacentralmmrns-1-r7keih3ctpbo4.servicebus.windows.net             | Canada               |  No |
| prodcanadaeastmmrns-1-vmq2eniku7w3e.servicebus.windows.net                | Canada               |  No |
| previewcanadacentralmmrns-1-s4wweqcy62z32.servicebus.windows.net          | Canada               | Yes |
| previewcanadaeastmmrns-1-35pw2xpwvfyrq.servicebus.windows.net             | Canada               | Yes |
| prdsbrmmrns-2-69n5a3ojd4crv4qpj93l0vi9xwul5qygykqu.servicebus.windows.net | South America        |  No |
| prdsbrmmrns-2-gh3flzhrf9ax9glm87xs23dxrykcuoakpics.servicebus.windows.net | South America        |  No |
| prdsbrmmrns-3-4ex758s96an2i2hfd1ypws4s59qre3fruvb5.servicebus.windows.net | South America        |  No |
| prdsbrmmrns-3-ufhjfys24383anexi9oioic5z8ub5smb3ogo.servicebus.windows.net | South America        |  No |
| prodbrazilsouthmmrns-1-duxgufn3xsxm6.servicebus.windows.net               | South America        |  No |
| prodsouthcentralusmmrns-1-v2gwsxxmesfkw.servicebus.windows.net            | South America        |  No |
| prdeaummrns-2-if84st2om5meh741f8vanxwcz07mnq6vgpgz.servicebus.windows.net | Australia            |  No |
| prdeaummrns-2-z1cqmm14ao5gt1nqpqx9llazq1vd0dg8418w.servicebus.windows.net | Australia            |  No |
| prdseaummrns-3-5gveu7rksy51oh4rfx54fbc4qt5qc8502bh.servicebus.windows.net | Australia            |  No |
| prdseaummrns-3-aiqa1jis4kacxb46aqyb0n01gvih0zuwctd.servicebus.windows.net | Australia            |  No |
| prodaustraliaeastmmrns-1-broykyq53frty.servicebus.windows.net             | Australia            |  No |
| prodaustraliasoutheastmmrns-1-g7yhvdys4yu2s.servicebus.windows.net        | Australia            |  No |
| previewaustraliaeastmmrns-1-e5g6njcwtfobg.servicebus.windows.net          | Australia            | Yes |
| previewaustraliasoutheastmmrns-1-onma5d3r2tevi.servicebus.windows.net     | Australia            | Yes |
| prdeasmmrns-2-1lngpyk311cxsmgr513wlgj053ezi6lj2eks.servicebus.windows.net | Asia                 |  No |
| prdeasmmrns-2-bmrbhomvn76odohg3wy43lmaj8i3y2lyfdif.servicebus.windows.net | Asia                 |  No |
| prdeasmmrns-6-dy3qfh1dr2jlqy20o7q5jpgx8i5f7f4lutsv.servicebus.windows.net | Asia                 |  No |
| prdeasmmrns-7-imtver1279xmke7qe3s57b3l80a6tf1bf1l7.servicebus.windows.net | Asia                 |  No |
| prdeasmmrns-7-r96lkkijqfgi4e7ujfnp4wb5s9msitwar29g.servicebus.windows.net | Asia                 |  No |
| prdseasmmrns-3-dj4e6cmp72khzsmxzrna6i7twn3i9z8la04.servicebus.windows.net | Asia                 |  No |
| prdseasmmrns-3-o8i3mkmfo6n3xt40j91ps6bh51kysnejk5r.servicebus.windows.net | Asia                 |  No |
| prdseasmmrns-4-02brgu6vvf454a96wtwaq4sza2uvgaze5m8.servicebus.windows.net | Asia                 |  No |
| prdseasmmrns-4-tvhxmw4xs4voyhiafd0wyj7rzj3nzslx8in.servicebus.windows.net | Asia                 |  No |
| prdseasmmrns-5-97zsx33ra6s2esktyr6pnj4hp9ppnl4zkmu.servicebus.windows.net | Asia                 |  No |
| prdseasmmrns-5-yuj2dcu7yyw305zlob38zdrdynodyc2s27w.servicebus.windows.net | Asia                 |  No |
| prdseasmmrns-6-2ubnk0mpzbeng7m3465wmvxbdkqozp7e9ig.servicebus.windows.net | Asia                 |  No |
| prodeastasiammrns-1-a7p5u2p76nykc.servicebus.windows.net                  | Asia                 |  No |
| prodsoutheastasiammrns-1-2zisdacd3p4yq.servicebus.windows.net             | Asia                 |  No |
| produaecentralmmrns-1-6v46fkb43e56k.servicebus.windows.net                | United Arab Emirates |  No |
| produaenorthmmrns-1-6rlrfzdyg6y2s.servicebus.windows.net                  | United Arab Emirates |  No |

## Other configuration

For additional details on how to permit access to automated, scheduled, and instant flows, including required endpoints, go to [IP address configuration](ip-address-configuration.md).

## Flow suspension because of runtime limits

Suspended flows will be shown as suspended in the Power Automate maker portal and the Power Platform Admin Center. When a flow is returned through API, PowerShell, or the [Power Automate Management connector list flows as admin action](/connectors/flowmanagement/#list-flows-as-admin), the flow will be **State=Suspended**, and have appropriate **FlowSuspensionReason** and **FlowSuspensionTime** values.

FlowSuspensionReason values for runtime limits:

- AllActionsFailingDetected
- AlwaysFailingDetected
- ApiCallOverageDetected
- BillingConsumption
- BillingConsumptionMissingRPALicense
- NeverTriggeringDetected

[!INCLUDE[footer-include](includes/footer-banner.md)]
