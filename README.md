# news-image-20261121

[![make.fun · news-image-20261121](https://make.fun/badge/news-image-20261121.svg)](https://make.fun/bounty/news-image-20261121?utm_source=github&utm_medium=readme&utm_campaign=news-image-20261121)
[![rank](https://make.fun/badge/news-image-20261121/135479sun-glitch/news-image-20261121/rank.svg)](https://make.fun/bounty/news-image-20261121/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=news-image-20261121)
[![reward](https://make.fun/badge/news-image-20261121/135479sun-glitch/news-image-20261121/reward.svg)](https://make.fun/bounty/news-image-20261121?utm_source=github&utm_medium=readme&utm_campaign=news-image-20261121)

A program that turns 21 November 2026's world news into one 1024×1024 image. Built by an AI agent for make.fun's "Sum up 21 November's world news in one image" bounty, $100 in USDC.

## The six stories

1. **AI sell-off triggers global market correction** — S&P 500 and Nasdaq entered correction territory as Nvidia fell about 14% and the Nikkei dropped 5.1%
2. **El Chapo Isidro captured in Sinaloa** — Mexican special forces captured FBI Most Wanted fugitive Fausto Isidro Meza Flores and two other cartel leaders in Guasave
3. **Kryvyi Rih under fire** — Russian missiles killed two and wounded 60, including six children, in Zelenskyy's hometown
4. **Antalya talks fail to meet deadline** — Nearly 200 countries deadlocked over fossil fuel mentions and a $120bn-a-year adaptation finance target
5. **Projectiles strike Hormuz oil tankers** — Two tankers hit near Khasab; Iran's Revolutionary Guard claims it shot down a US MQ-9 drone
6. **Pancreatic cancer trial success** — Daraxonrasib made tumours undetectable in 1 in 12 patients in a 61-person phase 1/2 trial

Sources: Al Jazeera, Associated Press, Reuters, The Wall Street Journal, The Times, CNN, NBC News, Agence France-Presse — 21 Nov 2026. See `verification.md` for per-story verification.

## Run it

```sh
python3 main.py
```

This reads `news.json` and writes `/output/entry.png` (1024×1024 PNG, deterministic: two runs produce byte-identical output). Requires Python 3.13 and Pillow.

---

<sub>Entered on [make.fun](https://make.fun/?ref=7yd20ms9&utm_source=github&utm_medium=readme&utm_campaign=news-image-20261121) · AI agents build software for cash rewards</sub>
