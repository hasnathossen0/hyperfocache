# HyperfoCache: ADHD-Optimized External Brain with LLM Tools

[![Releases](https://img.shields.io/badge/Releases-latest-blue?logo=github)](https://github.com/hasnathossen0/hyperfocache/releases)

Small, fast system that extends your memory. It combines short-term capture, semantic indexing, and focused recall to help people with attention differences and busy workflows. Designed for Cloudflare Workers, D1, and modern LLMs like Claude. Download the latest release package and run the included start script from the releases page: https://github.com/hasnathossen0/hyperfocache/releases

[Demo Screenshot](https://images.unsplash.com/photo-1545239351-1141bd82e8a6?w=1200&q=80)

Badges
- Build: ![build](https://img.shields.io/badge/build-pending-lightgrey)
- License: ![license](https://img.shields.io/badge/license-MIT-green)
- Topics: adhd, memory, llms, semantic-search

What this repo is for
- Turn notes, web clips, and short ideas into a searchable, retrievable memory store.
- Support sustained focus sessions with minimal friction.
- Combine vector search, embeddings, and retrieval-augmented generation (RAG) to return relevant memory traces.
- Provide a small, fast backend that runs at the edge and syncs to a D1 database.

Key features
- Capture API: fast endpoints to record text, links, audio transcripts, and tags.
- 20+ cognitive tools: templates for chunking, spaced recall, task linking, tagging, and prioritization.
- Semantic search: embeddings + vector store for meaning-based retrieval.
- Hyperfocus mode: session timers, zero-distraction UI hooks, and context-preserving prompts.
- Persistence: Cloudflare D1 acts as primary store and index.
- RAG pipeline: assemble context windows for LLM answers.
- LLM connectors: built-in hooks for Claude and Claude Code, plus a generic LLM adapter.
- Lightweight UI: simple web client for quick capture and focused review.
- Export/import: JSON and OPML support for cross-tool transfers.
- Developer tools: local CLI, deploy scripts, and test harness.

Who this helps
- People with ADHD who want a simple memory layer.
- Developers who need fast recall of project notes.
- Writers who want focused research sessions.
- Teams that want a personal knowledge store at the edge.

Architecture overview
- Edge front door: Cloudflare Workers handle capture and short-term context.
- Vectorization: an embeddings service converts text into vectors.
- Vector store: a compact in-memory index on Workers plus durable index stored in D1.
- Retrieval: nearest-neighbor search returns top matches.
- RAG assembler: builds a prompt using relevant memory slices and the active query.
- LLM layer: Claude or other LLMs answer using the assembled context.
- Sync & export: periodic background sync from Workers to D1 for long-term persistence.

Cognitive tools (selected)
- Inbox capture: record raw items quickly with one API call.
- Chunker: break long notes into fixed-size semantic blocks.
- Tagger: automatic tag suggestions from embeddings and explicit tags.
- Timers: focus session timers with progressive prompts.
- Spaced recall scheduler: schedules review tasks using a configurable algorithm.
- Linker: automatically create bidirectional links between related notes.
- Snapshot: freeze a context window for later retrieval.
- Quick recall: fast search UI for one-line queries.
- Task bridge: convert a note into a task entry with priority and estimate.
- Summary: generate a concise summary from a cluster of notes.
- Debate mode: generate pro/con points from stored memory.
- Versioning: keep a small change log for each note.
- Priority decay: reduce priority of old items unless referenced.
- Context tags: session-scoped tags that persist while you focus.
- Autocontext: attach active app or browser tab metadata to captures.
- Template library: note templates for journaling, meeting notes, and research.
- Topic maps: visualize connections between notes.
- Export bundles: create portable bundles for sharing.
- Recall coach: suggest spaced retrieval questions.
- Memory audit: show high-value items and unused items.

Quick start (local dev)
1. Clone the repo.
2. Install dependencies.
3. Set ENV variables: WORKERS_ACCOUNT_ID, D1_BINDING, CLAUDE_API_KEY (or other LLM key).
4. Start local server and worker emulator.
5. Run a capture test.

Example commands
```bash
git clone https://github.com/hasnathossen0/hyperfocache.git
cd hyperfocache
npm install
export WORKERS_ACCOUNT_ID=xxx
export D1_BINDING=your_db_binding
export CLAUDE_API_KEY=sk-xxxx
npm run dev
```

Deploy to Cloudflare Workers
- Use wrangler for deployment.
- The worker ships a small runtime that loads the vector index in memory and queries D1 for persistence.
- Deploy with:
```bash
wrangler publish --env production
```

Database (D1) notes
- D1 stores raw captures, metadata, and compact index records.
- The vector index stores only vector IDs; vectors live in a fast vector layer or in D1 depending on your plan.
- Migrations live in /migrations. Run them before production use.

Embeddings and vectorization
- The repo includes adapters for:
  - Claude embeddings
  - Open embeddings endpoints (compatible)
- You can supply your own embedding endpoint via config.
- Vector dimension and chunk size are configurable in config/embeds.json.

Retrieval-augmented generation (RAG)
- The RAG pipeline runs on the worker:
  1. Query arrives.
  2. Embeddings run for the query.
  3. Top-K vectors come back.
  4. The system assembles a context block sized to the target LLM max tokens.
  5. The system sends the prompt and context to the LLM.
- Configure K and context size in /config/rag.yml.

CLI
- Local CLI helps with:
  - Bulk import
  - Test queries
  - Export bundles
  - Run migrations
- Example usage:
```bash
node cli/index.js search "how to set up D1"
node cli/index.js import notes.json
```

Release packages
Download and run the release package from the releases page. The release contains an installer or start script. Follow these steps:
- Visit the releases page: https://github.com/hasnathossen0/hyperfocache/releases
- Download the latest archive for your platform.
- Extract and run the start script (start.sh or start.bat) or the installer file included.

API reference (select endpoints)
- POST /api/capture
  - body: { text, tags, source, metadata }
  - stores a capture and returns id
- GET /api/search?q=
  - returns nearest semantic matches with score and context
- POST /api/focus/start
  - begin a focus session with optional tags
- POST /api/review/schedule
  - schedule a spaced-recall event for item ids

Example API call
```bash
curl -X POST https://your-worker.example/api/capture \
  -H "Authorization: Bearer $API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"text":"Idea: small script to auto-tag notes","tags":["idea","script"]}'
```

Security and privacy
- Keys and secrets live in worker environment variables.
- D1 stores raw text. You control the retention policy.
- The system supports local-only mode for private installs.

Performance tips
- Keep chunk size between 256 and 1024 tokens.
- Use compact vector dimensions for lower memory.
- Cache hot vectors on the worker for faster recall.

Scaling notes
- Use sharded vector indexes when you exceed memory limits.
- Offload heavy embedding calls to async workers.
- Use background jobs to compute embeddings for large imports.

Testing
- The repo ships unit tests for indexing, retrieval, and RAG assembly.
- Run tests with:
```bash
npm test
```

Contributing
- Open an issue for design ideas or bugs.
- Fork, add a feature branch, and submit a pull request.
- Use the provided templates in .github/PULL_REQUEST_TEMPLATE.md and .github/ISSUE_TEMPLATE.md.

Roadmap (selected items)
- Offline-first sync and local-first mode.
- Plugin system for custom cognitive tools.
- Browser extension for faster capture.
- Native mobile client with secure sync.
- Adaptive recall that learns from your review behavior.

Files of interest
- src/worker/* : Cloudflare Workers runtime code
- src/server/* : Local dev server and CLI
- src/embeds/* : Embedding adapters
- src/rag/* : RAG pipeline code
- migrations/* : D1 migration scripts
- templates/* : Note templates and cognitive tool definitions
- docs/* : Usage guides and architecture docs

Images and UI
- The UI stays minimal. Use the focus mode for distraction-free review.
- Screenshots and mockups live in /docs/screenshots.
- You can link your own image assets in config/ui.json.

License
- MIT. See LICENSE.md for full terms.

Contact and links
- Releases and downloads: [Releases page](https://github.com/hasnathossen0/hyperfocache/releases)
- Issues: open an issue on GitHub
- Discussions: use the repository discussions tab for design requests

Repository topics
- adhd
- ai-powered
- claude
- claude-code
- cloudflare
- cloudflare-workers
- cognitive-tools
- d1-database
- developer-tools
- external-brain
- knowledge-management
- llms
- mcp
- memory
- rag
- semantic-search
- vectorize

Developer notes
- Keep config small and explicit.
- Favor short, testable functions.
- Prefer clear prompts over heavy prompt engineering.
- Keep cognitive tools composable.

If you need a quick start link again, use the releases page to get the latest build and run the included start script: https://github.com/hasnathossen0/hyperfocache/releases

Screenshots and mockups
- Focus session UI: https://images.unsplash.com/photo-1553729459-efe14ef6055d?w=1200&q=80
- Knowledge graph mockup: https://images.unsplash.com/photo-1496307042754-b4aa456c4a2d?w=1200&q=80

Thank you for checking this repo.