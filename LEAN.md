# Lean fork

A cost-reduced copy of [No-Stream/nostreambot-metaculus-bot](https://github.com/No-Stream/nostreambot-metaculus-bot)
(MIT, upstream commit b87365b), run by AnemometerRefiner's bot for the Metaculus MiniBench and FutureEval tournaments.

Changes from upstream:

- **Forecasters:** two models instead of three (OpenAI GPT-6.1 Sol and Claude Opus 5.5), both at reasoning
  effort `high` instead of `xhigh`. The Gemini slot is removed because it was pinned to a personal Google key.
  Both remaining slots route through the Metaculus-donated OpenRouter key first.
- **MiniBench research:** Gemini grounded search and both gap-fill passes are off. AskNews, OpenAI native
  search, prediction-market prices, financial data, the time-series anchor and the free resolution-source
  fetches stay on. No Google key is set, so the paid url_context rung never runs.
- **Workflows:** only the MiniBench workflow runs on a schedule. The others are disabled in GitHub Actions
  rather than deleted, so the upstream test suite still applies.
- One test (`tests/test_ft_llm_seams.py`) accepts effort `high` as well as `xhigh`.

To return to the full upstream setup, undo the roster change in `metaculus_bot/llm_configs.py` and set the
four MiniBench research flags back to `'true'`.
