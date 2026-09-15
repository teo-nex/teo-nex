<picture>
  <source media="(prefers-reduced-motion: reduce)" srcset="assets/animations/pixel-noir-poster.png" />
  <img src="assets/animations/pixel-noir.gif" alt="Пиксельный нуар: дождь за окном тёмного кабинета" width="100%" />
</picture>

# Teo | Nexcore

**Web3 & AI Enthusiast · AR Developer · Independent Research**

[English](#english) · [Русский](#русский)

## English

I research artificial intelligence and Web3, build experimental AI projects, and develop applications for **Even G2** smart glasses. My focus is on new ways to interact with technology, from intelligent tools to augmented reality interfaces.

For me, research is the starting point for creating something new. I'm interested in taking promising ideas through purposeful experimentation and turning concepts into practical solutions.

### Focus

- **AI Research** — research, experiments, and projects in artificial intelligence.
- **AR Development** — applications for **Even G2** smart glasses and augmented reality interfaces.
- **Web3** — decentralized technologies and how they intersect with AI.
- **Emerging Tech** — new directions, unconventional hypotheses, and promising ideas.

---

## Русский

Исследую искусственный интеллект и Web3, развиваю экспериментальные AI-проекты и разрабатываю приложения для умных очков **Even G2**. Мой фокус — новые сценарии взаимодействия с технологиями: от интеллектуальных инструментов до интерфейсов дополненной реальности.

Для меня исследование — это отправная точка для создания нового. Меня интересует путь от перспективной идеи к осмысленному эксперименту и решениям, которые могут выйти за пределы концепции.

### В фокусе

- **AI Research** — исследования, эксперименты и проекты в сфере искусственного интеллекта.
- **AR Development** — разработка приложений для умных очков **Even G2** и работа с интерфейсами дополненной реальности.
- **Web3** — децентрализованные технологии и возможности их пересечения с AI.
- **Emerging Tech** — новые направления, нестандартные гипотезы и поиск перспективных идей.

---

## Open-source contributions

| Project / area | Change | Status |
| --- | --- | --- |
| **Hermes Agent · Slack** | Preserved allowed bot posts and Slack Canvas mentions through message filtering. | [Merged upstream](https://github.com/NousResearch/hermes-agent/pull/111411) · [Authored commit](https://github.com/NousResearch/hermes-agent/commit/90aa5e3511332ea573c648eefba3ae2d630a546f) |
| **Hermes Agent · MoA** | Fixed overflowing cadence values and non-finite temperatures in configuration. | [Merged upstream with authorship preserved](https://github.com/NousResearch/hermes-agent/pull/111355) · [Original PR](https://github.com/NousResearch/hermes-agent/pull/110802) |
| **Hermes Agent · File tools** | Fixed UTF-16 pagination line counts and preserved blank lines. | [Open PR](https://github.com/NousResearch/hermes-agent/pull/110880) |
| **Hermes Agent · CLI** | Restored Bash completion when a profile selector precedes the command. | [Open PR](https://github.com/NousResearch/hermes-agent/pull/110881) |
| **CanvasTTY · Agent orchestration** | Added a native Codex control CLI and orchestration skill with YOLO support. | [Open PR](https://github.com/howdeploy/CanvasTTY/pull/32) |
| **CanvasTTY · Browser tools** | Replaced misleading empty browser results with an actionable viewport error. | [Merged upstream](https://github.com/howdeploy/CanvasTTY/pull/33) |
| **CanvasTTY · Parallel agents** | Added independent browser cards and per-agent ownership; corrected native resize, clipping and frozen-frame transitions. | [Open PR](https://github.com/howdeploy/CanvasTTY/pull/34) · [614 tests and 17/17 desktop CI jobs passed](https://github.com/teo-nex/CanvasTTY/actions/runs/34982053325) |
| **Pi · Prompt templates** | Prepared a tested fix that preserves literal arguments in prompt templates. | [Proposal submitted](https://github.com/earendil-works/pi/issues/9588) · [Prepared fix](https://github.com/teo-nex/pi/commit/8ca829a21fee2e47417c9c0ad0908eb17c924b1c) |

**CanvasTTY × Even G2 — full adaptation for smart glasses**

Adapted CanvasTTY for Even G2 glasses: terminal and AI-agent control through the glasses HUD, voice dictation with local Nemotron speech recognition, session creation, and six-digit local pairing. The integration includes CanvasTTY's desktop controls and the Even G2 companion app.

**Status:** companion v0.5.6 submitted for Even Hub review · **669 tests passed** (622 desktop + 47 companion) · Upstream publication pending moderation.

*Statuses checked on 15 September 2026. Pi's proposal is auto-closed pending maintainer review.*

## Engineering notes

**[A passing filter test can still miss a routing regression](notes/slack-routing-tests.md)**  
A Hermes Agent case study: an assertion that could never fail, two dropped message types, and a 12-case test of the adapter's routing behavior.

<br />

<picture>
  <source media="(prefers-reduced-motion: reduce)" srcset="assets/animations/pixel-noir-footer-poster.png" />
  <img src="assets/animations/pixel-noir-footer.gif" alt="Pixel noir: рабочий стол с терминалом, очками и шахматами; мигающий курсор и мягкий блик на линзах" width="100%" />
</picture>
