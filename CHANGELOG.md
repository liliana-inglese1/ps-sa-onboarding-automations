# Changelog

## [Unreleased]

### Changed
- `sa-onboarding-plan-builder`: SIP data is now read from Slack `#sa-sip-early-handover` (C0C6VHNLGPL), searched by client name; the SIP placeholder is replaced by this source. Message format still to be confirmed.
- `sa-onboarding-plan-builder-judge`: audit and regression text updated to match.

### Added
- `sa-onboarding-plan-builder` v0.1: Part 1 (inputs, discovery questions, plan, self-serve content). Out of scope: SA-channel trigger, Planhat publishing, post-onboarding audit.
- `sa-onboarding-plan-builder-judge` v0.1: audit mode (9 steps) and regression mode (5 golden cases).
