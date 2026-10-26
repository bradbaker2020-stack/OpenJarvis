# OmniRoute free-provider action plan

Source: your running OmniRoute **v3.8.52** (`http://127.0.0.1:20128`). This plan combines:
- `GET /v1/models` with your key: **502 models from 16 connected providers**
- OmniRoute's built-in provider registry (372 providers) and its hand-checked free-tier catalog (last checked **2026-10-19**), read from `%APPDATA%\npm\node_modules\omniroute`

Legend: ✅ already connected · ⚠️ OmniRoute's terms check says "avoid" or "ambiguous" · 🔁 the free allowance renews · 1️⃣ a one-time signup credit that runs out

## How to add a provider (same for every row)
1. Open `http://localhost:20128/dashboard` and log in with your dashboard password.
2. Go to **Providers**, find the provider by name, then choose **Add API Key**, **Connect** (OAuth) or **Add Account** (web cookie).
3. For key-based gateways, turn on **"import only free models"** so paid models never get added.
4. Test the connection, then check that the new `alias/...` model IDs show up in `/v1/models`.
5. In OpenJarvis, set `default_model` in `~/.openjarvis/config.toml` to the exact ID from `/v1/models`.

---

## 1. No account, no API key (just enable)
| Provider | Alias | What you get | Status |
|---|---|---|---|
| Cloudflare AI Playground | `cfp` | GLM 5.2, Kimi K2.7 Code, DeepSeek V4 Pro, gpt-oss-120B and more | ✅ |
| DuckDuckGo AI Chat | `ddgw` | Anonymous chat with several models | ✅ ⚠️ terms say avoid |
| UncloseAI | `unc` | OpenAI-compatible, no signup | ✅ |
| AI Horde | `horde`/`aihorde` | Volunteer GPUs; a shared queue with no cap, but it can be slow | ✅ |
| VEO AI Free (video) | `veo-free` | VEO 3.1 / Seedance, 6 requests/hour | ✅ |
| **LLM7** | `llm7` | ✅ Added 2026-10-26 (connection "keyless", placeholder key). Working models: `llm7/gpt-oss:20b`, `llm7/codestral-latest`, `llm7/minimax-m2.7`, `llm7/mistral-Nemo-Instruct-2407`, `llm7/nemotron-3-nano:30b`. The 4 built-in LLM7 IDs are out of date and return "unavailable" | ✅ |
| Context7 (docs search) | `context7` | Works through `/v1/search` with no connection | ✅ |
| ~~Pollinations~~ | `pol` | **No longer keyless**: calls return 401 "A valid API key is required". Moved to section 3 (free key at enter.pollinations.ai). A "keyless" connection was added on 2026-10-26 and kept on purpose: paste a real key into it later | ❌ |
| ~~Liquid~~ | `liquid` | Placeholder key rejected, so it needs a real key (section 3) | ❌ |
| ~~OVHcloud~~ | `ovh` | Placeholder key rejected. OmniRoute's form requires a key, so this needs a free OVH key (section 3) | ❌ |
| ~~AnySearch~~ | `anysearch` | OmniRoute requires a key ("No credentials configured"), so this needs the free 1000/day key (section 3) | ❌ |
| TinyCMS (web) | `tcw` | Needs the site's `app-config-uuid` session token pasted in, which you must do yourself (section 5) | ⏳ |

## 2. Runs on your own computer (install software, no key)
| Provider | Default URL | Notes |
|---|---|---|
| Ollama | `localhost:11434/v1` | ✅ connected (`ollama-local`) |
| LM Studio | `localhost:1234/v1` | Install LM Studio and start its server |
| llama.cpp server | `localhost:8080/v1` | Supports embeddings too |
| Lemonade | `localhost:13305/api/v1` | Good fit for AMD/Ryzen AI; embeddings too |
| Docker Model Runner | `localhost:12434/v1` | Needs Docker Desktop |
| Llamafile, Xinference, oobabooga, vLLM, Triton | various | Optional. vLLM/Triton need a strong NVIDIA GPU, and **port 8000 is already in use here** |
| SD WebUI / ComfyUI | `7860` / `8188` | Free local image generation |
| SearXNG | your instance | Self-hosted web search |
| MLX Gemma/Qwen | — | **Mac only**, so skip on Windows |

## 3. Free account + API key, no credit card (main to-do list)
Sign up on the provider's site (usually with email, Google or GitHub), create an API key, and paste it into OmniRoute.

### 3a. Highest value: large free allowances that renew 🔁
| # | Provider | Alias | Free allowance |
|---|---|---|---|
| 1 | **Mistral** (Experiment tier) | `mistral` | ~1B tokens/month, all models, rate limited |
| 2 | **Nara** | `nara` | 7M tokens/day, 15 requests/min, 8 models |
| 3 | **xKiro** | `xkiro` | 5M tokens/day across 39 free models |
| 4 | **BazaarLink** | `bzl` | 4M tokens/day with `auto:free` routing |
| 5 | **Groq** | `groq` | ~200K tokens/day per chat model; very fast |
| 6 | **Google Gemini** (AI Studio) | `gemini` | Free tier with per-model quotas; Google account |
| 7 | **API Airforce** | `af` | 55 free models (Grok-3, Kimi-K2, Gemini Flash…) |
| 8 | **OpenRouter** | `openrouter` | `:free` models, 20 requests/min, 200/day |
| 9 | **Kilo Gateway** | `kg` | Free models with no fixed cap (rate limited) |
| 10 | **OpenCode Zen** | `opencode-zen` | Free models with no fixed cap |
| 11 | **Ollama Cloud** | `ollamacloud` | Cloud models with no fixed cap ⚠️ terms ambiguous |
| 12 | **Bluesminds** | `bm` | Daily free credits, 200+ models ⚠️ terms ambiguous |
| 13 | **Requesty** | `requesty` | ~200 requests/day |
| 14 | **Cohere** | `cohere` | 1,000 calls/month |
| 15 | **Hugging Face** | `hf` | Inference API, small monthly credit |
| 16 | **Reka** | `reka` | $10/month in credits |
| 17 | **Morph** | `morph` | 250K credits/month |
| 18 | **Navy** | `navy` | 150K tokens/day pool |
| 19 | **Arcee AI** | `arcee` | Free Trinity Large Thinking (262K context) |
| 20 | **SambaNova** | `samba` | Daily free limits |
| 21 | **Nous Research** | `nous` | 50 requests/min, 500K tokens/min |
| 22 | **AnyAPI** | `anyapi` | 100K tokens/day |
| 23 | **Zylo API** | `zylo` | 200K tokens/day, 7,200 requests/day |
| 24 | **HelyxAI** | `helyxai` | 100K tokens/day |
| 25 | **Ant Ling** | `ling` | 500K tokens/day |
| 26 | **InternLM** | `internlm` | ~1M input / 3M output tokens per month |
| 27 | **Inference.net** | `inet` | Monthly credits |
| 28 | **Z.ai GLM** (international) | `glm` | Free GLM Flash models, no cap |
| 29 | **Agnes** | `agnes` | Free permanently |
| 30 | **SEA-LION** | `sealion` | Free permanently, 10 requests/min |
| 31 | **Aion** | `aion` | ~20K tokens/day |
| 32 | **AINative** | `ainative` | ~10M tokens/month (the provider's own claim) |
| 33 | **Routeway** | `routeway` | `:free` models, ~200 requests/day |
| 34 | **Typhoon** | `typhoon` | 200 requests/min |
| 35 | **Bytez** | `bytez` | $1 every 4 weeks ⚠️ terms ambiguous |

### 3b. Smaller or unclear free tiers (add if you want more fallbacks)
Onomeo (30 calls per 5 hours), UnoRouter, FastRouter (10/day per model), ElectronHub, LLMGateway, Lyceum, LLM Kiwi, LiteRouter, Y-API (4 models free), MNN-AI ($1/month), Meganova (550 requests/day), Mixlayer, Speka ($1/month), TokenReply, Yolo-Auto, DXNT (100/day), CloudCode-One, OfoxAI, ChatAnywhere (personal use only), Auriko, Poixe, Naga AI (`naga-ai`), Naga (`naga`), Chat-Oripe, DGrid (100/day), Zenmux (`zm`), OpenAdapter, TokenRouter, Dahl (**"Add Account" can generate a token for you**), Charm Hyper, Void-AI, Poolside (free during preview), Openference API (`ofa`), Liquid.
- **FreeTheAI** (`fta`): needs a **daily check-in** on their site to keep free models unlocked.
- **Free-AI** (`free-ai`): requires **email verification**, and usage beyond 30K tokens/day can be billed.
- **Logfare**: free with no limits, but **every prompt is logged for research**. Don't send anything private.

### 3c. One-time signup credits only 1️⃣ (good for testing, not for daily use)
AgentRouter ($200), FreeModel.dev ($300, GPT-5.x), DeepSeek (5M tokens), Inception (10M tokens), Scaleway (1M tokens, EU), Novita ($0.50), Hyperbolic, Nebius, Nscale ($5), DeepInfra, Predibase ($25), Baseten ($30), MonsterAPI, PublicAI, OpenVecta, SeekAi, NVIDIA NIM (dev access, ~40 requests/min, 70+ models: **very useful, add early**), Vertex AI (needs a Google Cloud service account).

### 3d. Embeddings, reranking and tools (free keys)
Voyage AI (200M tokens), Jina AI (10M tokens, non-commercial), Jina Reader (web page to markdown), Nomic Embed, Mixedbread, Segmind (image credits), Speechmatics (8 hours/month of speech-to-text), Dify, plus search: Serper, Exa, Tavily, Firecrawl (each has a free key tier).

## 4. Sign in with an existing account (OAuth or CLI login)
| Provider | Alias | What's needed | Notes |
|---|---|---|---|
| Openference | `of` | Sign in | Qwen3.8 27B, Llama 3.2 3B free |
| Qoder | `if` | Install `qodercli` locally plus a PAT token | 1️⃣ plain chat only, 45-second limit |
| Antigravity (`agy`) | `agy` | Import a login from the Antigravity CLI | ⚠️ **terms say avoid** |
| Kiro | `kr` | AWS Builder ID | ⚠️ **terms say avoid**, 50 credits/month |
| Amazon Q | `aq` | AWS Builder ID | ⚠️ **terms say avoid** |

## 5. Web login + browser cookie (log into the website, OmniRoute uses your session)
| Provider | Alias | Notes |
|---|---|---|
| HuggingChat | `huggingchat` | Hugging Face account, 24 models 🔁 |
| Arena (LMArena) | `lma` | Many chat models, no subscription |
| Zenmux Free | `zmf` | 5 "flows" per 5 hours |
| TinyCMS | `tcw` | **No login needed**: GPT 5.4, Gemini 3.5, Grok 4.20 |
| Yuanbao | `ybw` | DeepSeek V3/R1 + Hunyuan (Tencent account) |
| Tencent AI Studio | `tasw` | Hunyuan models |
| Z.ai chat | `zw` | GLM chat models |
| NoTrack | `ntw` | notrack assistant |
| Meta AI (Muse Spark) | `ms-web` | ⚠️ terms say avoid |
| T3 Chat | `t3chat` | ⚠️ terms say avoid |

## 6. Needs more than an email (ID check, phone, card or approval)
| Provider | Requirement |
|---|---|
| ModelScope (`ms`) | Alibaba account + **mainland-China identity verification** |
| SiliconFlow | **Identity verification** to unlock the $0 models |
| LongCat (`lc`) | Signup + **KYC check**, then a one-time 10M tokens |
| iFlytek / SparkDesk | **Chinese real-name verification** ⚠️ terms restrict this use |
| Baidu ERNIE, Tencent Hunyuan, Doubao, Baichuan, StepFun, SenseNova, 360 AI, GLM-CN, Agnes-CN, HCNSec | Chinese cloud accounts, which **usually need a mainland phone number**. Agnes-CN and GLM-CN are free permanently. HCNSec needs daily check-ins |
| Sarvam | Indian platform, ₹1,000 credit |
| Cerebras | 1️⃣ $5 credit, **needs a payment method** |
| FreeInference | Research access; **non-Harvard sign-ups are approved by hand** |
| Modal | $30/month, but ⚠️ terms say avoid |

## 7. Skip: OmniRoute's terms check marks these "avoid" (proxy use forbidden)
Fireworks, AI21, FriendliAI, Blackbox, NLP Cloud, Coze, Modal, Kiro, Amazon Q, Antigravity, Meta AI web, T3 web, iFlytek. DuckDuckGo is already connected and also marked "avoid", so consider turning it off.

---

## Suggested order
1. **Today, no signup:** LLM7, Pollinations, Liquid, OVHcloud, AnySearch, Context7, TinyCMS.
2. **Biggest wins (about 30 minutes):** Mistral, Groq, Gemini, OpenRouter, NVIDIA NIM, Nara, xKiro, BazaarLink, API Airforce, Kilo Gateway, OpenCode Zen, Cohere, Hugging Face. Together these give OpenJarvis billions of free tokens a month across strong models.
3. **Fallback depth:** the rest of 3a, then 3b if you want more redundancy.
4. **Local:** add LM Studio or Lemonade next to Ollama for offline use.
5. **Embeddings and search for OpenJarvis memory and research:** Voyage, Jina, Nomic, Tavily, Exa.
6. After adding providers, rebuild OmniRoute's `auto/*` combos (Dashboard → Combos) so routing prefers free providers, and turn on the strict zero-cost filter if you never want to be billed.

Already connected but not on the free list: `dva` (Devin CLI bridge), `aug`, `zc`, `cxa`. These use your own CLI logins.

---

## Signup links: free providers that need an API key
Links come from OmniRoute's catalog. Where a provider has a well-known key page, that is linked instead of the homepage.

### Free allowance renews (best value)
| Provider | Link | Free allowance |
|---|---|---|
| Mistral | https://console.mistral.ai/api-keys | ~1B tokens/month (Experiment tier) |
| Nara | https://bynara.id | 7M tokens/day |
| xKiro | https://xkiro.com | 5M tokens/day |
| BazaarLink | https://bazaarlink.ai | 4M tokens/day |
| Groq | https://console.groq.com/keys | ~200K tokens/day per model |
| Google Gemini | https://aistudio.google.com/apikey | Per-model free quotas |
| NVIDIA NIM | https://build.nvidia.com | ~40 requests/min, 70+ models |
| API Airforce | https://api.airforce | 55 free models |
| OpenRouter | https://openrouter.ai/keys | `:free` models, 200 requests/day |
| Kilo Gateway | https://kilo.ai | Free models, no fixed cap |
| OpenCode Zen | https://opencode.ai/zen | Free models, no fixed cap |
| Ollama Cloud | https://ollama.com/settings/keys | Cloud models, no fixed cap |
| Bluesminds | https://www.bluesminds.com | Daily credits |
| Requesty | https://requesty.ai | ~200 requests/day |
| Cohere | https://dashboard.cohere.com/api-keys | 1,000 calls/month |
| Hugging Face | https://huggingface.co/settings/tokens | Small monthly credit |
| Pollinations | https://enter.pollinations.ai | Paste into the existing `pol` connection |
| Reka | https://docs.reka.ai/chat/overview | $10/month |
| Morph | https://morphllm.com | 250K credits/month |
| Navy | https://api.navy | 150K tokens/day |
| Arcee AI | https://arcee.ai | Trinity Large Thinking |
| SambaNova | https://cloud.sambanova.ai | Daily free limits |
| Nous Research | https://portal.nousresearch.com | 50 requests/min |
| AnyAPI | https://anyapi.ai | 100K tokens/day |
| Zylo API | https://zyloai.net | 200K tokens/day |
| HelyxAI | https://helyxai.space | 100K tokens/day |
| Ant Ling | https://developer.ant-ling.com/en/docs/ | 500K tokens/day |
| InternLM | https://internlm.intern-ai.org.cn/ | ~1M input / 3M output tokens per month |
| Inference.net | https://inference.net | Monthly credits |
| Z.ai GLM | https://z.ai | Free Flash models |
| Agnes | https://agnes-ai.com | Free permanently |
| SEA-LION | https://sea-lion.ai | Free permanently, 10 requests/min |
| Aion | https://www.aionlabs.ai | ~20K tokens/day |
| AINative | https://ainative.studio | ~10M tokens/month (their claim) |
| Routeway | https://routeway.ai | `:free` models, ~200 requests/day |
| Typhoon | https://docs.opentyphoon.ai | 200 requests/min |
| Bytez | https://bytez.com | $1 every 4 weeks |
| Liquid | https://liquid.ai | LFM2.5 models |
| OVHcloud AI Endpoints | https://www.ovhcloud.com | Free endpoints |

### Smaller or unclear free tiers
Onomeo https://onomeo.com · UnoRouter https://unorouter.ai · FastRouter https://fastrouter.ai · ElectronHub https://www.electronhub.ai · LLMGateway https://llmgateway.io · Lyceum https://lyceum.technology · LLM Kiwi https://llm.kiwi · LiteRouter https://literouter.com · Y-API https://y-api.bestvirtualgoods.com · MNN-AI https://mnnai.ru · Meganova https://meganova.ai · Mixlayer https://www.mixlayer.com · Speka https://speka.me · TokenReply https://www.tokenreply.com · Yolo-Auto https://yolo-auto.com · DXNT https://www.dxnt.com · CloudCode-One https://cloudcode.one · OfoxAI https://ofox.ai · ChatAnywhere https://chatanywhere.tech · Auriko https://www.auriko.ai · Poixe https://poixe.com · Naga https://naga.ac · Chat-Oripe https://api.oriper.com · DGrid https://dgrid.ai · Zenmux https://zenmux.ai · OpenAdapter https://openadapter.dev · TokenRouter https://tokenrouter.com · Dahl https://inference.dahl.global/tokens · Charm Hyper https://hyper.charm.land · Void-AI https://voidai.app · Poolside https://poolside.ai · Openference https://openference.com · FreeTheAI https://freetheai.org (daily check-in) · Free-AI https://free.ai (email verification) · Logfare https://logfare.ai (logs every prompt)

### One-time signup credits
AgentRouter https://agentrouter.org · FreeModel.dev https://freemodel.dev · DeepSeek https://platform.deepseek.com/api_keys · Inception https://docs.inceptionlabs.ai · Scaleway https://www.scaleway.com/en/docs/ai-data/generative-apis/ · Novita https://novita.ai · Hyperbolic https://hyperbolic.xyz · Nebius https://nebius.com · Nscale https://nscale.com · DeepInfra https://deepinfra.com · Predibase https://predibase.com · Baseten https://baseten.co · MonsterAPI https://monsterapi.ai · PublicAI https://publicai.co · OpenVecta https://openvecta.com · SeekAi https://seekai.cc · Vertex AI https://cloud.google.com/vertex-ai

### Embeddings, search and tools
Voyage AI https://www.voyageai.com · Jina AI https://jina.ai · Jina Reader https://jina.ai/reader · Nomic https://nomic.ai · Mixedbread https://www.mixedbread.com · Segmind https://segmind.com · Speechmatics https://www.speechmatics.com · Dify https://dify.ai · AnySearch https://anysearch.com · Serper https://serper.dev · Exa https://dashboard.exa.ai · Tavily https://app.tavily.com · Firecrawl https://firecrawl.dev/app/api-keys

### Key requires ID, phone, card or approval
ModelScope https://modelscope.cn · SiliconFlow https://cloud.siliconflow.com · LongCat https://longcat.chat/platform/docs · Cerebras (card) https://cloud.cerebras.ai · FreeInference (approval) https://freeinference.org · Sarvam https://docs.sarvam.ai · Baidu ERNIE https://ernie.baidu.com/ · Tencent Hunyuan https://hunyuan.tencent.com · Doubao https://doubao.com · Baichuan https://www.baichuan-ai.com/ · StepFun https://stepfun.com · SenseNova https://platform.sensenova.cn · 360 AI https://ai.360.cn · GLM-CN https://open.bigmodel.cn · Agnes-CN https://api.agnes-ai.cn · HCNSec https://api.hcnsec.cn

---

## No credit card needed (documented in OmniRoute's catalog)
These providers' own terms, as recorded in OmniRoute's catalog, say signup needs **no card**. ⭐ = OmniRoute also confirms a **hard stop**: past the free limit you get an error instead of a bill.

### Free allowance renews
| Provider | Sign up / get key | Free allowance |
|---|---|---|
| ⭐ xKiro | https://xkiro.com | 5M tokens/day, 39 models |
| ⭐ Groq | https://console.groq.com/keys | ~200K tokens/day per model |
| BazaarLink | https://bazaarlink.ai | 4M tokens/day |
| Mistral | https://console.mistral.ai/api-keys | Experiment tier, all models (may ask for phone verification) |
| Cohere | https://dashboard.cohere.com/api-keys | 1,000 calls/month |
| Nous Research | https://portal.nousresearch.com | 50 requests/min |
| Arcee AI | https://arcee.ai | Trinity Large Thinking |
| AnyAPI | https://anyapi.ai | 100K tokens/day |
| AINative | https://ainative.studio | ~10M tokens/month |
| Aion | https://www.aionlabs.ai | ~20K tokens/day |
| Agnes | https://agnes-ai.com | Free permanently |
| SEA-LION | https://sea-lion.ai | Free permanently (Google sign-in) |
| OpenAdapter | https://dashboard.openadapter.in | Daily quota, 15+ models |
| Speka | https://speka.me | $1/month |
| Meganova | https://meganova.ai | 550 requests/day |
| Onomeo | https://onomeo.com | 30 calls per 5 hours (email, Google or GitHub) |
| Logfare | https://logfare.ai | No limits, **but logs every prompt** |

### One-time credit, no card
DeepSeek (5M tokens) https://platform.deepseek.com/api_keys · Inception (10M tokens) https://docs.inceptionlabs.ai · SambaNova ($5) https://cloud.sambanova.ai · FreeModel.dev ($300) https://freemodel.dev · MonsterAPI https://monsterapi.ai

### Embeddings and audio, no card
Jina AI https://jina.ai · Nomic https://atlas.nomic.ai · Mixedbread https://www.mixedbread.com · Segmind https://segmind.com · Speechmatics https://www.speechmatics.com

### Not in the catalog's no-card notes, but widely known not to need a card
Google Gemini https://aistudio.google.com/apikey · OpenRouter `:free` models https://openrouter.ai/keys · Hugging Face https://huggingface.co/settings/tokens · NVIDIA NIM https://build.nvidia.com (may ask for phone verification)

### Known to require a card: skip
Cerebras (stated in the catalog).
