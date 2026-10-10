---
name: sop-from-recording
description: Use when the user gives a transcript of a narrated screen recording or explains a task step by step and wants written instructions, an SOP or a checklist. Turns it into a numbered SOP with checks, exceptions and approval points. Not for inventing steps the user did not describe.
---

# SOP from a narrated recording

1. Read the transcript. A step is something the person did ("open", "click", "type", "save", "send").
   Reasons ("because...") attach to the step before them; "make sure"/"check that" lines become checks
   under the step; "if/when/sometimes" lines are exceptions; "never/always" lines are rules.
2. Write the SOP:
   - **Context**: when the task runs and why, in one or two lines.
   - **Apps used**.
   - **Steps**, numbered, each starting with the action. Keep the recording's times when given.
     A check is never its own numbered step: nest it as an indented `- Check:` line under the
     step it verifies (the step just before it in the transcript), for example
     `5. Click New, then Bill.` followed by `   - Check: the total matches the invoice.`
   - **Rules**, **Exceptions**, and **Approval points**: any step that sends, pays, submits or deletes
     something waits for the owner's OK.
   - **Fresh-input test**: run the SOP on three new examples and compare with the owner's own result
     before relying on it.
3. Never add a step, value or app the person did not say, not even an obvious-looking one such as
   "repeat for each" or "fill in the fields". Every numbered step must match a sentence in the
   transcript. Anything you think is missing goes under "Questions for the owner", never into Steps.
4. Mask customer details (emails, phone numbers, account numbers) as [email], [phone], [number].
