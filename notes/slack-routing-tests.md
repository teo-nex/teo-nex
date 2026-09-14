# A passing filter test can still miss a routing regression

*14 September 2026 · Hermes Agent · Testing*

Slack lifecycle notices such as `channel_join` can contain both a user ID and text. In Hermes free-response channels, those notices could start an agent turn. [Upstream issue #110778](https://github.com/NousResearch/hermes-agent/issues/110778) led to a proposed allowlist of conversational message subtypes.

That allowlist introduced a second problem: it also rejected messages that should still reach the agent. The follow-up described here restores those cases and tests the adapter's delivery boundary.

## Two decisions to keep separate

The adapter needs to answer two questions:

1. **Is this sender allowed?** `allow_bots` controls whether bot posts are ignored, accepted only when they mention Hermes, or accepted generally.
2. **Is this a conversational event?** A channel being renamed is different from a message, file share, or explicit app mention.

The proposed filter omitted `bot_message`, even after the sender had passed the bot policy. It also omitted `document_mention`, which Slack uses for an [app mention inside a canvas](https://docs.slack.dev/reference/events/message/document_mention/).

The correction adds these two subtypes to the existing allowlist. It keeps the preceding sender-policy check in place.

## What the original test actually proved

A simplified version of the drop test looked like this:

```python
assert await adapter._prefilter_inbound(event, None) is None
adapter.handle_message.assert_not_awaited()
```

The first assertion is useful: it checks the filter's return value.

The second cannot distinguish a correct filter from a broken one. `_prefilter_inbound()` never calls `handle_message()`; delivery happens later in the adapter. The mock would remain untouched even if the filter incorrectly accepted the event.

[@wtfsayo identified this assertion in review](https://github.com/NousResearch/hermes-agent/pull/110780#pullrequestreview-5196887942). The positive filter tests also covered only a subset of valid message kinds, so they did not expose the lost bot posts or canvas mentions.

## Test the observable handoff

The follow-up calls the real adapter handler and records what it hands to `handle_message()`:

```python
await adapter._handle_slack_message(event)

assert adapter.handle_message.await_count == int(accepted)
if accepted:
    delivered = adapter.handle_message.await_args.args[0]
    assert delivered.text == "A message"
    assert delivered.source.is_bot is True
```

A fake Slack transport supplies user and channel metadata. The normalization, sender checks, subtype filter, and message construction remain real.

The bot-policy cases are:

| Bot policy | Mentions Hermes | Expected handoff |
| --- | --- | --- |
| `none` | No | No |
| `none` | Yes | No |
| `mentions` | No | No |
| `mentions` | Yes | Yes |
| `all` | No | Yes |

Each case runs as an original event and inside a `message_changed` envelope: ten cases. Two more check original and edited canvas mentions. This matters because edit normalization preserves the inner message's subtype.

Adding these cases would also improve a focused filter test. Driving the full handler adds a separate check: accepted events reach the handoff with their text and sender identity intact.

## Before and after

The baseline here is **the proposed allowlist PR**, not unmodified upstream `main`.

| Source revision | Check | Result |
| --- | --- | --- |
| `74b3cdf` — proposed allowlist | New routing cases | 6 failed, 6 passed |
| `d2e2678` — follow-up | New routing cases | 12 passed |
| `d2e2678` — follow-up | All 36 Slack test files | 527 passed, 0 failed |

The [GitHub Actions run](https://github.com/teo-nex/hermes-agent/actions/runs/34836182026) used Linux, Python 3.11, and Hermes's canonical `scripts/run_tests.sh` runner with retries disabled.

The validation covers the real adapter with a fake transport. No live Slack workspace or model calls were used.

## Contribution and review

[My follow-up PR #13](https://github.com/liuhao1024/hermes-agent/pull/13) was merged into [@liuhao1024's upstream PR #110780](https://github.com/NousResearch/hermes-agent/pull/110780), with commit authorship preserved. As of 14 September 2026, the upstream PR is still under review.

The [committed regression tests](https://github.com/teo-nex/hermes-agent/blob/d2e2678e7bdb7848cd1f50c96e5a927a83ed7bb9/tests/gateway/test_slack_conversational_senders.py) contain the complete fixture and cases.

The useful testing rule is simple: assert a side effect at a boundary that can actually produce it. Filter tests can check acceptance decisions; adapter tests can check whether a message reaches the next stage.

[Back to profile](https://github.com/teo-nex)
