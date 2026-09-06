# GovGuide AI

**Knowledge-Graph-Grounded Agentic RAG with Hallucination Verification**

GovGuide AI is a demo-first academic/research prototype that helps people discover government welfare schemes, understand eligibility, and review evidence-backed guidance in a clear, conversational interface.

The project is designed to run locally in **Demo Mode** without paid AI APIs, a vector database, Neo4j, a speech provider, or live government credentials.

> **Important:** GovGuide AI is not affiliated with the Government of India. The sample scheme catalogue is illustrative demo data. Always verify eligibility, benefits, deadlines, and application procedures with the responsible department.

## What the project demonstrates

GovGuide AI presents a complete research pipeline:

```text
Voice / Text
    ↓
Lightweight NLP
    ↓
Agentic query planning
    ↓
Local RAG-style retrieval + Knowledge Graph
    ↓
Evidence fusion
    ↓
Answer generation
    ↓
Claim extraction and verification
    ↓
Confidence and evidence-backed answer
```

### Main capabilities

- Public landing page explaining the research prototype
- Demo authentication flow with local browser persistence
- Personalized dashboard and scheme recommendations
- Searchable government scheme explorer
- Scheme detail pages with eligibility, benefits, documents, and application steps
- Eligibility checker with incomplete-information handling
- Scheme comparison for up to three schemes
- AI Assistant with quick prompts and local retrieval
- Visible high-level agentic processing trail without exposing hidden chain-of-thought
- Claim verification states including verified, partially verified, unsupported, and contradicted
- Evidence and confidence cards for assistant answers
- Browser speech recognition where supported
- Browser text-to-speech for reading answers aloud
- Interactive client-side knowledge graph
- Saved schemes and question history
- Profile editing for recommendation context
- Architecture, About, How It Works, and Admin/demo-data screens
- Responsive layouts for desktop, tablet, and mobile
- Loading, empty, error, and unsupported-browser states

## Tech stack

- React
- TypeScript
- Vite
- Tailwind CSS
- Wouter
- TanStack Query
- Lucide React
- Framer Motion
- pnpm workspaces
- Browser Web Speech API
- LocalStorage for demo persistence

## Project structure

```text
.
├── artifacts/
│   ├── govguide-ai/          # Main React + Vite application
│   ├── api-server/           # Shared API server scaffold
│   └── mockup-sandbox/       # Component preview sandbox
├── lib/
│   ├── api-client-react/     # Generated API client package
│   ├── api-spec/             # OpenAPI source
│   ├── api-zod/              # Generated validation package
│   └── db/                   # Drizzle database package scaffold
├── scripts/                  # Workspace utility scripts
├── package.json              # Root workspace scripts
├── pnpm-workspace.yaml       # Workspace configuration
└── README.md
```

The main product code lives in:

```text
artifacts/govguide-ai/src/
├── App.tsx
├── index.css
├── lib/demo-data.ts
├── components/
└── pages/
```

## Requirements

- Node.js 20 or newer
- pnpm 9 or newer
- VS Code (recommended)
- A modern browser

Chrome or Microsoft Edge is recommended for speech recognition. The rest of the application works in Demo Mode without browser speech support.

## Run in VS Code

### 1. Open the project

Open the repository folder in VS Code:

```bash
code .
```

If the `code` command is not available, open VS Code and choose **File → Open Folder**.

### 2. Install dependencies

From the VS Code integrated terminal:

```bash
corepack enable
pnpm install
```

### 3. Start the GovGuide AI web app

#### macOS / Linux / Git Bash

```bash
PORT=5173 BASE_PATH=/ pnpm --filter @workspace/govguide-ai run dev
```

#### Windows PowerShell

```powershell
$env:PORT="5173"
$env:BASE_PATH="/"
pnpm --filter @workspace/govguide-ai run dev
```

Open the URL printed by Vite, normally:

```text
http://localhost:5173
```

### 4. Use the demo

You can explore the public pages without signing in. To use the personalized workspace:

1. Select **Try the demo** or **Open the demo**.
2. Use the demo sign-in flow.
3. Open **AI Assistant**.
4. Try a prompt such as:

   ```text
   Naku Andhra Pradesh lo farmers ki government schemes kavali
   ```

5. Review the detected intent, retrieval trail, graph context, verified claims, evidence, and confidence.
6. Save a scheme and confirm it appears under **Saved**.
7. Open **History** to review the question.

Demo data and saved state are stored in the browser's LocalStorage. Use the Admin/demo-data screen to reset local demo state.

## Useful VS Code commands

Run these commands from the repository root.

### Type check the main app

#### macOS / Linux / Git Bash

```bash
PORT=5173 BASE_PATH=/ pnpm --filter @workspace/govguide-ai run typecheck
```

#### Windows PowerShell

```powershell
$env:PORT="5173"
$env:BASE_PATH="/"
pnpm --filter @workspace/govguide-ai run typecheck
```

### Type check the whole workspace

```bash
pnpm run typecheck
```

### Build the production bundle

#### macOS / Linux / Git Bash

```bash
PORT=5173 BASE_PATH=/ pnpm --filter @workspace/govguide-ai run build
```

#### Windows PowerShell

```powershell
$env:PORT="5173"
$env:BASE_PATH="/"
pnpm --filter @workspace/govguide-ai run build
```

The output is written to:

```text
artifacts/govguide-ai/dist/public/
```

### Preview the production build

#### macOS / Linux / Git Bash

```bash
PORT=4173 BASE_PATH=/ pnpm --filter @workspace/govguide-ai run serve
```

#### Windows PowerShell

```powershell
$env:PORT="4173"
$env:BASE_PATH="/"
pnpm --filter @workspace/govguide-ai run serve
```

### Run the shared API server

The main GovGuide AI Demo Mode does not require the API server. It is included as a workspace service for future backend integrations.

```bash
pnpm --filter @workspace/api-server run dev
```

### Run the component preview sandbox

```bash
pnpm --filter @workspace/mockup-sandbox run dev
```

## Application routes

| Route | Purpose |
| --- | --- |
| `/` | Public landing page |
| `/login` | Demo sign-in |
| `/signup` | Demo account creation |
| `/dashboard` | Personalized workspace overview |
| `/assistant` | AI Assistant and evidence-backed answers |
| `/schemes` | Search and filter scheme catalogue |
| `/schemes/:id` | Scheme detail and eligibility tools |
| `/graph` | Interactive knowledge graph |
| `/history` | Recent questions and verification status |
| `/saved` | Saved scheme list |
| `/profile` | User recommendation profile |
| `/how-it-works` | Retrieval, graph, and verification explanation |
| `/about` | Research prototype overview |
| `/architecture` | End-to-end system architecture |
| `/admin` | Demo data and local state management |

## Demo architecture

The app keeps its external dependencies optional:

- **NLP service:** lightweight rule-based intent and entity extraction
- **RAG service:** keyword and structured-record matching over local scheme data
- **Knowledge Graph:** client-side graph nodes and relationships
- **Verification service:** compares generated claims with retrieved demo evidence
- **Voice service:** browser `SpeechRecognition` / `webkitSpeechRecognition` and `speechSynthesis`
- **Authentication:** local demo authentication state for presentations
- **Persistence:** browser LocalStorage

This makes the project suitable for a final-year B.Tech demonstration while leaving clear replacement points for a verified production data source, vector search, real authentication, or an optional LLM integration later.

## Demo data and safety

All sample scheme records are marked as demo content. The app intentionally avoids inventing official URLs, live deadlines, or guaranteed eligibility decisions. Unsupported claims are not shown as verified.

When browser speech recognition is unavailable, the app explains that Chrome or Microsoft Edge can be used instead. The text assistant remains available.

## Future extension points

- Replace local scheme records with verified official government data
- Add server-side authentication
- Add a persistent PostgreSQL/Supabase data layer
- Replace keyword retrieval with pgvector or another vector store
- Add a production knowledge graph database
- Add optional LLM providers through a server-side abstraction
- Add multilingual response generation for Telugu, Hindi, Tamil, Kannada, and Malayalam
- Add official source ingestion and scheduled freshness checks

## License and academic use

This project is intended as an academic/research prototype and presentation-ready demonstration. Add the license and institutional attribution required by your course or project guide before distributing it publicly.