---
title: Builder and accounting roles become platform policy
date: 2026-09-10
repos: grabio.space, grabio-platform-docs
---

# 2026-09-10 - Builder and accounting roles become platform policy

**Context:** Builder and accounting client access, account roles, permissions, and environments are partly implemented. Owner assessment: about 60% complete, but it needs more work. The risk is that builder/accounting access remains one-account setup instead of becoming reusable Grabio rules.

**Decision:** Builder/accounting accounts, sub-account permissions, and environment access must become general platform policy. Store admins should get default role templates, with tenant customization when package allows it. Web, Functions, mobile, POS, and invoice app must resolve the same effective permissions.

**Rejected alternatives:**

- Patching one client account to make access work - fast but not scalable.
- Keeping builder/accounting access only as hardcoded route allowlists - difficult to audit and extend.
- Letting mobile/backend permissions drift from web UI permissions - unsafe and confusing.

**Consequences:** Future agents must define role/environment scope before changing access. New role behavior must be a default role template, tenant option, or documented temporary exception. Builder users must not see finance/cost data unless allowed; accounting users must not get website/admin powers unless allowed.

**Repos affected:** grabio.space | grabio-platform-docs

**Links:** [[Architecture/Role-Permission-Environment-Policy]], [[Backlog/Open]]
