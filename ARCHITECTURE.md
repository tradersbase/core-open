# TradersBase Architecture

## System Overview

TradersBase is a full-stack web application built with a modern, scalable architecture designed for real-time Solana token analysis.

```
┌─────────────┐      ┌─────────────┐      ┌─────────────┐
│   Frontend  │─────▶│   Backend   │─────▶│  Blockchain │
│   (Vercel)  │◀─────│  (Render)   │◀─────│    APIs     │
└─────────────┘      └─────────────┘      └─────────────┘
      │                     │                     │
      │                     │                     │
      ▼                     ▼                     ▼
  React SPA          Express API           Helius/Jupiter
  TailwindCSS          Redis              DexScreener
  TypeScript         TypeScript           Solana RPC
```

---

## Frontend Architecture

### Technology Stack
- **React 18.3** - UI library with hooks
- **TypeScript 5.6** - Type safety
- **Vite 5.4** - Build tool and dev server
- **TailwindCSS 3.4** - Utility-first styling
- **React Router 6** - Client-side routing

### Component Structure
```
src/
├── components/        # Reusable UI components
│   ├── Layout.tsx    # App layout wrapper
│   ├── Navbar.tsx    # Navigation header
│   ├── Footer.tsx    # Site footer
│   └── Toast.tsx     # Notification system
│
├── pages/            # Route pages
│   ├── SearchPage.tsx      # Homepage with search
│   ├── TokenPage.tsx       # Token analysis view
│   ├── RoadmapPage.tsx     # Product roadmap
│   ├── PrivacyPage.tsx     # Privacy policy
│   ├── TermsPage.tsx       # Terms of service
│   └── ComingSoonPage.tsx  # Placeholder page
│
├── App.tsx           # Root component
└── main.tsx          # Entry point
```

### State Management
- React hooks (useState, useEffect)
- Context API for global state (Toast notifications)
- URL parameters for navigation state
- No external state management (Redux, etc.)

### Styling Approach
- TailwindCSS utility classes
- Custom color palette in theme
- Responsive design (mobile-first)
- Dark theme optimized
- CSS animations for UX polish

---

## Backend Architecture

### Technology Stack
- **Node.js 22** - Runtime environment
- **Express 4.19** - Web framework
- **TypeScript 5.4** - Type safety
- **Redis** - Caching layer
- **Axios** - HTTP client

### API Structure
```
src/
├── routes/           # API endpoints
│   └── token.ts      # Token analysis routes
│
├── services/         # Business logic
│   ├── metadata.ts   # Token metadata fetching
│   ├── holders.ts    # Holder analysis
│   ├── liquidity.ts  # Price & liquidity
│   └── risk.ts       # Risk scoring
│
├── types/            # TypeScript definitions
│   └── index.ts      # Shared types
│
├── utils/            # Utilities
│   └── redis.ts      # Cache management
│
└── index.ts          # Server entry point
```

### API Endpoints

#### `GET /api/token/:mint`
Main endpoint for token analysis
- **Input**: Solana token mint address
- **Output**: Complete token analysis object
- **Cache**: 10 minutes (600 seconds)
- **Response Time**: ~2-5 seconds (cold) / <100ms (cached)

### Caching Strategy
```typescript
Cache Key Pattern: `token:${mintAddress}`
TTL: 600 seconds (10 minutes)
Strategy: Cache-aside pattern
Invalidation: Time-based expiration
```

### Error Handling
- Structured error responses
- Graceful API fallbacks
- Client-friendly error messages
- Logging for debugging

---

## Data Flow

### Token Analysis Request Flow
```
1. User enters mint address
   ↓
2. Frontend validates format
   ↓
3. API request to backend
   ↓
4. Backend checks Redis cache
   ├─ Cache HIT → Return cached data
   └─ Cache MISS → Fetch from APIs
      ↓
5. Parallel API calls:
   - Helius: Metadata + Holders
   - Jupiter: Price + Liquidity
   - DexScreener: Fallback data
      ↓
6. Risk scoring calculation
      ↓
7. Store in Redis cache
      ↓
8. Return to frontend
      ↓
9. Display results to user
```

---

## External APIs

### Helius API
**Purpose**: Solana blockchain data
- Token metadata
- Holder accounts
- Token supply info
- Account balances

**Rate Limits**: Depends on plan
**Fallback**: None (required)

### Jupiter API
**Purpose**: Price and liquidity data
- Token prices (USD)
- Liquidity depth
- Trading volume
- DEX listings

**Rate Limits**: Free tier available
**Fallback**: DexScreener

### DexScreener API
**Purpose**: Market data fallback
- Price information
- Volume tracking
- Liquidity data
- Chart data

**Rate Limits**: Public API
**Fallback**: None (already fallback)

---

## Deployment

### Frontend (Vercel)
- **Platform**: Vercel
- **Build**: `npm run build`
- **Output**: Static SPA in `dist/`
- **Deploy**: Auto on git push to `main`
- **Environment**: Production variables in Vercel dashboard

### Backend (Render)
- **Platform**: Render
- **Type**: Web Service
- **Build**: `npm install && npm run build`
- **Start**: `npm start`
- **Deploy**: Auto on git push to `main`
- **Environment**: Variables in Render dashboard

### Environment Variables

**Frontend (Vercel)**:
```
VITE_API_URL=https://your-backend.onrender.com
VITE_TOKEN_CA=your_token_address (optional)
VITE_TEAM_WALLET=your_team_wallet (optional)
```

**Backend (Render)**:
```
HELIUS_API_KEY=your_helius_key
HELIUS_RPC_URL=https://mainnet.helius-rpc.com/?api-key=key
JUPITER_API_KEY=your_jupiter_key
REDIS_URL=your_redis_connection_string
PORT=3001
NODE_ENV=production
```

---

## Performance Optimizations

### Frontend
- Code splitting with React Router
- Lazy loading of components
- Image optimization
- Minified production builds
- Gzip compression

### Backend
- Redis caching (10min TTL)
- Parallel API requests
- Connection pooling
- Response compression
- Efficient data structures

### API Usage
- Batch requests where possible
- Cache frequently accessed data
- Fallback mechanisms
- Rate limit awareness

---

## Security Considerations

### Frontend
- Input validation (mint address format)
- XSS prevention (React default)
- HTTPS only
- No sensitive data in client

### Backend
- CORS configuration
- API key management (environment variables)
- Rate limiting (future enhancement)
- Input sanitization
- Error message sanitization

### API Keys
- Stored in environment variables
- Never exposed to frontend
- Rotated periodically
- Separate keys per environment

---

## Scalability

### Current Capacity
- Handles ~1000 requests/hour comfortably
- Redis cache reduces API load by ~70%
- Stateless backend (easy to scale horizontally)

### Future Improvements
- Load balancing for backend
- CDN for static assets
- Database for historical data
- Queue system for batch processing
- Distributed caching

---

## Monitoring & Analytics

### Current Setup
- Vercel analytics (frontend)
- Render logs (backend)
- Error tracking via logs
- Basic performance metrics

### Future Enhancements
- Application monitoring (Sentry)
- Custom analytics dashboard
- API usage tracking
- User behavior insights

---

## Tech Stack Summary

| Layer | Technology | Purpose |
|-------|-----------|---------|
| Frontend | React + TypeScript | UI components |
| Build Tool | Vite | Fast dev & build |
| Styling | TailwindCSS | Responsive design |
| Routing | React Router | SPA navigation |
| Backend | Express + TypeScript | API server |
| Cache | Redis | Performance |
| Deployment | Vercel + Render | Hosting |
| APIs | Helius, Jupiter | Blockchain data |

---

## Development Workflow

1. **Local Development**
   - Frontend: `npm run dev` (Vite dev server)
   - Backend: `npm run dev` (nodemon)
   - Redis: Local or cloud instance

2. **Testing**
   - Manual testing in browser
   - API testing with tools like Postman
   - Type checking with TypeScript

3. **Deployment**
   - Push to `main` branch
   - Automatic builds trigger
   - Zero-downtime deployments
   - Environment-specific configs

---

**This architecture is designed for maintainability, performance, and scalability.**
