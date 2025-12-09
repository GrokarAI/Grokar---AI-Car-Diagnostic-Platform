# Grokar - AI Car Diagnostic Platform

<div align="center">

**Your AI-Powered Mechanic Friend**

*A wise, witty 40-year veteran mechanic in your pocket*

[Features](#features) | [Privacy](#privacy) | [Demo](#demo) | [Tech Stack](#tech-stack) | [Getting Started](#getting-started)

</div>

---

## Overview

Grokar is an AI-powered automotive diagnostic companion that helps you decode VINs, diagnose vehicle issues, check recalls, estimate market values, and analyze OBD codes. It's like having a trusted mechanic friend who's seen it all and tells it like it is.

The AI personality is a legendary 40-year veteran mechanic - warm, witty, and straight-shooting. No corporate fluff, just real advice with colorful expressions and wisdom nuggets.

## Privacy

<div align="center">

**We don't store your data. Period.**

</div>

Grokar is built with privacy-first principles:
- No personal information collected or stored
- No VIN history logging - searches are processed and forgotten
- No conversation persistence on our servers
- No tracking cookies or analytics
- No data selling or sharing

All your saved vehicles and service history are stored **locally in your browser** - they never leave your device.

[Read our full Privacy Policy](PRIVACY.md)

## Features

### Core Features

| Feature | Description |
|---------|-------------|
| **VIN Decoding** | Decode any 17-character VIN to get complete vehicle specs using NHTSA API |
| **AI Chat** | Conversational interface for diagnosing car problems with personality |
| **OBD Code Analysis** | Upload photos of OBD scanners to interpret diagnostic trouble codes |
| **Market Valuation** | Get estimated trade-in, private party, and retail values |
| **Vehicle Garage** | Save and manage multiple vehicles with full history |

### Advanced Features

| Feature | Description |
|---------|-------------|
| **Voice Input** | Speech-to-text using Web Speech API with real-time transcription |
| **Live Camera VIN Scan** | Use device camera to capture and extract VIN numbers using Grok Vision AI |
| **Service History Log** | Track all repairs and maintenance with date, cost, mileage, and notes |
| **Car Health Score** | Algorithm-based 0-100 rating using mileage, age, maintenance compliance |
| **Nearby Mechanic Finder** | Geolocation-based auto shop discovery |
| **Vehicle Comparison Tool** | Side-by-side analysis of multiple vehicles |
| **Real NHTSA Recall API** | Live recall data integration with dedicated UI |
| **Future Cost Predictor** | 1-3 year maintenance cost projections based on vehicle data |

### Money-Saving Tools

| Feature | Description |
|---------|-------------|
| **Photo Damage Estimator** | Upload photos of car damage (dents, scratches) and get AI-powered repair cost estimates |
| **Sound Diagnosis** | Describe engine sounds (clicking, squealing, knocking) for AI diagnosis of potential issues |
| **Part Price Comparison** | Search for parts and compare prices across AutoZone, RockAuto, Amazon, O'Reilly, and more |
| **Gas Price Tracker** | Find the cheapest gas stations near you with real-time price comparisons |

## Demo

### Chat Interface
The centered, dark-first UI inspired by Grok/X provides a clean chat experience:
- Send messages about car symptoms
- Upload VIN plate photos or OBD scanner screenshots
- Get concise, personality-filled responses
- View decoded vehicle info in context cards

### Sample Interaction
```
You: My 2019 Honda Accord makes a clicking noise when turning

Grokar: Here's the deal - that clicking when turning is your CV joints 
saying hello. Seen it a thousand times on these Accords.

**Most likely:** Worn CV axle joint (outer)
- Fix cost: $30-50 DIY | $200-400 shop
- Urgency: Fix within 30 days
- Also check: CV boot for tears, grease splatter on wheel

Pro tip: If you catch it early, sometimes just replacing 
the boot and repacking grease buys you another year.
```

## Tech Stack

### Frontend
- **React 18+** with TypeScript
- **Vite** for blazing fast builds
- **Tailwind CSS** with custom dark theme
- **Shadcn/ui** component library
- **TanStack Query** for data fetching
- **Wouter** for routing

### Backend
- **Express.js** on Node.js
- **Drizzle ORM** with PostgreSQL
- **Multer** for file uploads
- **Zod** for validation

### AI Services
- **Grok (xAI)** via OpenRouter - Conversational AI & Image analysis/OCR
- **NHTSA vPIC API** - Free VIN decoding & recalls

## Getting Started

### Prerequisites
- Node.js 18+
- PostgreSQL database
- OpenRouter API key (for Grok AI access)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/grokar.git
cd grokar
```

2. Install dependencies:
```bash
npm install
```

3. Set up environment variables:
```env
DATABASE_URL=your_postgres_connection_string
SESSION_SECRET=your_session_secret
OPENROUTER_API_KEY=your_openrouter_api_key
```

4. Push database schema:
```bash
npm run db:push
```

5. Start development server:
```bash
npm run dev
```

The app will be available at `http://localhost:5000`

## Project Structure

```
grokar/
├── client/                 # React frontend
│   ├── src/
│   │   ├── components/     # UI components
│   │   ├── hooks/          # Custom React hooks
│   │   ├── lib/            # Utilities
│   │   └── pages/          # Route pages
├── server/                 # Express backend
│   ├── services/           # AI & external APIs
│   │   ├── openrouter.ts   # Grok AI chat integration
│   │   ├── vision.ts       # Grok Vision image analysis
│   │   └── nhtsa.ts        # VIN/recall APIs
│   ├── routes.ts           # API endpoints
│   └── storage.ts          # Data layer
├── shared/                 # Shared types
│   └── schema.ts           # Drizzle schema
└── package.json
```

## API Reference

### Chat Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/sessions` | List all chat sessions |
| POST | `/api/sessions` | Create new session |
| GET | `/api/sessions/:id` | Get session with messages |
| DELETE | `/api/sessions/:id` | Delete session |
| POST | `/api/sessions/:id/messages` | Send message |

### Vehicle Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/vehicles` | List saved vehicles |
| POST | `/api/vehicles` | Save vehicle to garage |
| GET | `/api/vehicles/:id` | Get vehicle details |
| DELETE | `/api/vehicles/:id` | Remove from garage |
| GET | `/api/vehicles/:id/recalls` | Get recalls for vehicle |

### Service History

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/vehicles/:id/service-history` | Get service records |
| POST | `/api/vehicles/:id/service-history` | Add service record |
| DELETE | `/api/service-history/:id` | Delete record |

### Analysis Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/scan-vin` | OCR scan VIN from image |
| POST | `/api/predict-costs` | Get maintenance cost predictions |
| GET | `/api/recalls/:vin` | Check recalls by VIN |

## AI Personality

Grokar's personality is carefully crafted to be:
- **Warm & Approachable** - Like your trusted mechanic friend
- **Witty & Colorful** - Uses expressions like "Here's the deal..."
- **Straight-Shooting** - No corporate fluff, just real talk
- **Helpful** - Calls out rip-offs, shares insider tips
- **Concise** - Responses under 200 words with clear formatting

## Design Philosophy

- **Dark-first UI** inspired by Grok/X aesthetic
- **Information density** - Show what matters, hide the rest
- **Mobile-friendly** - Works great on any device
- **Resilient** - Graceful handling of API failures
- **Fast** - Optimized with caching and lazy loading

## Contributing

Contributions are welcome! Please read our contributing guidelines before submitting PRs.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [NHTSA](https://vpic.nhtsa.dot.gov/) for free VIN decoding API
- [OpenRouter](https://openrouter.ai/) for Grok API access
- [Shadcn/ui](https://ui.shadcn.com/) for beautiful components
- [xAI](https://x.ai/) for Grok AI

---

<div align="center">

**Built with passion for car enthusiasts everywhere**

*"Between you and me, this app is gonna save you some serious cash at the shop."* - Grokar

</div>
