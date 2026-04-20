# Ideal Match AI

> Build your ideal partner profile with AI, then chat with the match you create.

---

## Live Demo
- **Production:** https://www.idealmatchai.com

![Preview Image](https://www.idealmatchai.com/images/heart.png)

---

## What Is This Website?

Ideal Match AI is a web app that helps people clarify relationship preferences, generate a personalized AI match profile, and continue the experience through chat.

- **Who it's for:** People exploring compatibility, self-reflection, and relationship preferences
- **Problem it solves:** Most users struggle to describe what they want in a partner with depth and structure
- **Why it's unique:** It combines trait-based generation, shareable public match pages, and ongoing AI conversation in one flow

---

## Key Features

### For Users
- Profile-first onboarding with structured trait inputs
- AI-generated match profile with biography, score, and image support
- Dashboard with status tracking, sharing, and match chat threads

### For Developers (optional)
- Typed Next.js API proxy layer for backend contracts
- Mock API mode for deterministic frontend testing without backend availability

---

## How It Works

### For Users
1. Fill in your profile and preferred match traits.
2. Generate your AI match profile and review biography, traits, and score.
3. Save, share, organize, and chat with your generated match from the dashboard.

### For Developers
- **Frontend:** Next.js App Router app with reusable UI components, typed forms, and route-level SEO metadata
- **Backend:** External API consumed via `/api/*` proxy routes with normalized error handling and auth header forwarding
- **Data Flow:** UI forms -> frontend validation -> Next.js proxy route -> backend API -> normalized response -> dashboard/match/chat views

---

## Tech Stack

- **Frontend:** Next.js 15, React 19, TypeScript, Tailwind CSS 4, shadcn/ui, Radix/Base UI primitives
- **Backend:** External REST API behind Next.js route handlers (`src/app/api/*`)
- **Database:** Managed by backend service (not in this repository)
- **Infrastructure:** Vercel deployment with scheduled cron for chat reply processing
- **APIs / AI:** Auth0 for authentication, AI-powered generation and messaging via backend endpoints

---

## Architecture Overview

The app uses a frontend-first architecture where all browser calls go through internal Next.js route handlers. Those proxy handlers enforce validation, apply auth context, normalize errors, and forward requests to the backend API.

```text
[Browser UI]
    |
    v
[Next.js App Router Pages + Components]
    |
    v
[Typed API Client (src/lib/api-client.ts)]
    |
    v
[Next.js Proxy Routes (/api/*)] --auth headers, validation, guest rules-->
    |
    v
[IdealMatch Backend API]
    |
    v
[Generation, Match Storage, Chat Processing]
```

---

## Setup & Installation

```bash
# Clone the repository
git clone https://github.com/aisuretech/ideal-match-ai.git

# Navigate into the project
cd ideal-match-ai

# Install dependencies
npm install

# Start development server
npm run dev
```

### Environment Variables

Create a `.env.local` file:

```env
AUTH0_DOMAIN=your-tenant.us.auth0.com
AUTH0_CLIENT_ID=your-auth0-client-id
AUTH0_CLIENT_SECRET=your-auth0-client-secret
NEXT_PUBLIC_AUTH0_DOMAIN=your-domain.auth0.com
NEXT_PUBLIC_AUTH0_CLIENT_ID=your-client-id
NEXT_PUBLIC_AUTH0_AUDIENCE=your-backend-api-audience
NEXT_PUBLIC_API_BASE_URL=your-base-url
NEXT_PUBLIC_USE_MOCK_API=false
NEXT_PUBLIC_MOCK_API_SCENARIO=success
NEXT_PUBLIC_GENERATE_PHRASE_INTERVAL_MS=5000
AUTH0_SECRET=replace-with-long-random-secret
APP_BASE_URL=https://www.idealmatchai.com
```

### Prerequisites
- Node.js 20+
- npm 10+

---

## API / Backend Details

### Example Endpoint

```http
GET /api/matches?page=1&limit=10
```

### Example Response

```json
{
  "matches": [
    {
      "id": "match-123",
      "publicId": "public-123",
      "createdAt": "2026-04-10T12:00:00.000Z"
    }
  ],
  "total": 42,
  "page": 1,
  "limit": 10
}
```

### Authentication
Authentication is handled with Auth0 Universal Login. Protected UI routes (like dashboard and chat) require an authenticated session. Proxy routes forward `Authorization`, `x-user-id`, and `x-user-authenticated` headers to backend services.

---

## Screenshots / UI Preview

| Feature | Preview |
|--------|--------|
| Match generation experience | ![](https://www.idealmatchai.com/images/about-match.jpg) |
| Chat and conversation flow | ![](https://www.idealmatchai.com/images/chat.jpg) |

---

## Use Cases

- Define and refine partner preferences in a structured way
- Create shareable AI match profiles for discussion and reflection
- Continue asynchronous conversations with generated matches

---

## Roadmap

- [ ] Complete performance optimization and Core Web Vitals tuning (Phase 9)
- [ ] Add full unit, integration, and E2E test coverage for key journeys (Phase 10)
- [ ] Finalize launch readiness tasks for production rollout (Phase 11)

---

## Contributing

Contributions are welcome!

1. Fork the repo
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes
4. Push to your branch
5. Open a Pull Request

---

## License

Proprietary (All rights reserved)

---

## Links

- GitHub Organization: https://github.com/aisuretech/
- Website: https://www.idealmatchai.com
- Contact: info@AISureTech.com

---

## Final Note

If this project interests you, check out the live site and explore what it can do.

> Build your profile, generate your match, and start the conversation.

