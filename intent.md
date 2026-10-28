# Intent — Results-ready notification

## Problem

I-1. Patients at the fictional clinic make avoidable calls to ask whether their
results are ready. The intent is to reduce these status-only calls while keeping
clinical questions distinct. This is an intent for discovery and specification,
not approval to build or launch the feature.

The approved PRD is the decision authority, supported by the current discovery
notes. The early request is superseded and supplies no current approval.
Sources: [approved PRD](inputs/01-approved-prd.md),
[current notes](inputs/02-current-meeting.md), and
[superseded request](inputs/03-superseded-request.md).

## Proposed outcome

I-2. A patient learns that an update is available for review through the existing
authenticated portal. A notification is eligible only after a doctor has both
reviewed and released the result. Laboratory upload completion alone does not
make a result ready, and abnormality is not an approved notification condition.
Source: [approved PRD](inputs/01-approved-prd.md) and
[current notes](inputs/02-current-meeting.md).

I-3. Success will be observed by measuring results-status-only calls separately
from clinical questions and comparing them with a measured baseline, alongside
measuring delivery failures. Fewer status-only calls are the intended outcome;
a reduction in all inbound calls is not the measure. The baseline and numerical
target remain to be agreed during discovery. No numeric target or delivery
deadline is approved.
Source: [approved PRD](inputs/01-approved-prd.md) and
[current notes](inputs/02-current-meeting.md).

## Affected users and systems

I-4. Patients receive the availability notice and use the existing authenticated
portal to view their results. Doctors control review and release. Support keeps
status-only calls distinct from clinical questions. Product and privacy own the
channel decision; clinical and privacy own referring-doctor recipient authorization.
Engineering confirms that the existing portal path is adequate.
Affected systems are the existing authenticated portal and its result route, the
doctor review-and-release step that gates eligibility, the notification delivery
path, and the notification and operational logs, which must stay free of
clinical content. The approved scope uses the existing portal result route, prevents duplicate
notifications for the same released result version, and handles delivery failures
without duplicate patient messages.
Source: [approved PRD](inputs/01-approved-prd.md) and
[current notes](inputs/02-current-meeting.md).

## Out of scope

I-5. Portal redesign, a new patient dashboard, appointment scheduling, clinical
interpretation and third-party notifications are excluded from the approved scope.
Referring-doctor notifications are a separate unresolved authorization decision,
not an approved recipient group. The old requests for immediate notification on
lab upload, clinical results in SMS, copying the referring doctor, rebuilding the
dashboard and an aggressive call-reduction target are superseded.
Source: [approved PRD](inputs/01-approved-prd.md),
[current notes](inputs/02-current-meeting.md), and
[superseded request](inputs/03-superseded-request.md).

## Constraints

I-6. Doctor review and release must both precede notification eligibility. The
message may say only that an update is available and direct the patient to the
existing authenticated portal. It must contain no test name, result value,
clinical measurement, diagnosis or treatment detail. Messages and operational logs
must expose no sensitive clinical content.

I-7. Result access stays authenticated through the existing portal: no attached
results or public result links. Prevent duplicate notifications for the same
released result version and handle delivery failures without creating duplicate
patient messages. Do not select a channel, infer consent or authorize another
recipient while the relevant decisions remain open.
Source for I-6 and I-7: [approved PRD](inputs/01-approved-prd.md) and
[current notes](inputs/02-current-meeting.md).

## Open questions with their owners

OPEN-1. Which channel should be used: SMS, email or portal push? The product owner
and privacy owner must decide after reviewing consent and delivery considerations.
No channel is approved by this intent.

OPEN-2. May the referring doctor receive a notification, and under what recipient
authorization? The clinical owner and privacy owner must decide. Neither the old
request nor this intent grants that authorization.

Sources: [approved PRD](inputs/01-approved-prd.md) and
[current notes](inputs/02-current-meeting.md).

```json
{
  "notifyWhen": ["doctor-reviewed", "released"],
  "messageMayInclude": ["update-available"],
  "inScope": [
    "existing-portal-route",
    "duplicate-prevention",
    "delivery-failure-handling"
  ],
  "openDecisions": [
    {"topic": "channel", "owners": ["product", "privacy"]},
    {"topic": "referring-doctor-notification", "owners": ["clinical", "privacy"]}
  ],
  "successMeasures": ["status-only-calls", "delivery-failures"],
  "numericTarget": null
}
```
