[README.md](https://github.com/user-attachments/files/24467647/README.md)
# 🤖 GigWorkSeeker AI Assistant

<p align="center">
  <img src="assets/ai-assistant-banner.png" alt="GigWorkSeeker AI Assistant" width="100%">
</p>

<p align="center">
  <strong>Conversational AI interface for the GigWorkSeeker platform</strong><br>
  Powered by Claude • Built on Solana
</p>

<p align="center">
  <a href="#features">Features</a> •
  <a href="#quick-start">Quick Start</a> •
  <a href="#installation">Installation</a> •
  <a href="#configuration">Configuration</a> •
  <a href="#deployment">Deployment</a>
</p>

---

## Overview

The GigWorkSeeker AI Assistant is a conversational interface that helps users navigate the platform. Built with Claude AI, it understands the complete GigWorkSeeker ecosystem—from gig matching to escrow mechanics to dispute resolution.

### What It Does

| Capability | Description |
|------------|-------------|
| 🔍 **Find Gigs** | Search by location, skills, pay rate, or duration |
| ⭐ **Provider Discovery** | Get recommendations for top-rated service providers |
| 📝 **Natural Language Posting** | Create gig posts through conversation |
| 💡 **Platform Guidance** | Explain escrow, disputes, verification, payments |
| 💎 **Token Info** | Answer questions about GIG tokens and staking |
| 🎯 **Smart Suggestions** | Context-aware follow-up actions |

---

## Features

### Conversational Intelligence
- Full platform context including all gig categories, user types, and features
- Maintains conversation history for contextual responses
- Generates relevant follow-up suggestions based on topic

### Platform Integration
- Understands Customer vs Service Provider workflows
- Knows verification requirements and payment options
- Can explain zero-knowledge proof verification
- Familiar with dispute resolution process

### Design
- Solana-inspired dark theme with signature green/purple gradients
- Smooth animations and typing indicators
- Responsive layout for all screen sizes
- Accessibility-friendly

---

## Quick Start

### Web (React)

```bash
# Clone and install
git clone https://github.com/gigworkseeker/ai-assistant.git
cd ai-assistant/web
npm install

# Start development server
npm run dev
```

### Android

```bash
# Open in Android Studio
cd ai-assistant/android

# Build and run
./gradlew assembleDebug
```

---

## Installation

### Prerequisites

| Platform | Requirements |
|----------|--------------|
| **Web** | Node.js 18+, npm 9+ |
| **Android** | Android Studio Hedgehog+, JDK 17, Kotlin 1.9+ |

### Web Setup

1. **Install dependencies**
   ```bash
   cd web
   npm install
   ```

2. **Configure environment**
   ```bash
   cp .env.example .env
   # Edit .env with your API key (for standalone deployment)
   ```

3. **Start development**
   ```bash
   npm run dev
   ```

### Android Setup

1. **Open project in Android Studio**
   - File → Open → Select `android` directory

2. **Sync Gradle**
   - Android Studio will prompt to sync

3. **Configure API key** (for standalone deployment)
   - Add to `local.properties`:
     ```
     ANTHROPIC_API_KEY=your_key_here
     ```

4. **Run on device/emulator**
   - Click Run or `Shift+F10`

---

## Project Structure

```
gigworkseeker-ai-assistant/
├── README.md
├── web/
│   ├── package.json
│   ├── vite.config.js
│   ├── index.html
│   ├── .env.example
│   └── src/
│       ├── main.jsx
│       ├── App.jsx
│       ├── index.css
│       └── components/
│           └── GigWorkSeekerAI.jsx
├── android/
│   ├── build.gradle.kts
│   ├── settings.gradle.kts
│   ├── gradle.properties
│   └── app/
│       ├── build.gradle.kts
│       └── src/main/
│           ├── AndroidManifest.xml
│           ├── java/com/gigworkseeker/app/
│           │   ├── GigWorkSeekerApp.kt
│           │   └── ui/ai/
│           │       └── AIAssistantFragment.kt
│           └── res/
│               ├── navigation/nav_graph.xml
│               └── values/strings.xml
├── docs/
│   ├── INTEGRATION.md
│   ├── API.md
│   └── CUSTOMIZATION.md
└── assets/
    └── ai-assistant-banner.png
```

---

## Configuration

### Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `VITE_ANTHROPIC_API_KEY` | Claude API key (web) | Standalone only |
| `ANTHROPIC_API_KEY` | Claude API key (Android) | Standalone only |

> **Note**: When running inside Claude.ai artifacts, API keys are handled automatically.

### System Prompt Customization

The AI Assistant's knowledge is defined in the system prompt. Key sections:

```javascript
const systemPrompt = `
PLATFORM OVERVIEW:
// Platform description and value proposition

KEY FEATURES:
// GIG Token, escrow, ZKP, GPS matching, ratings, disputes

USER TYPES:
// Customers and Service Providers

VERIFICATION REQUIREMENTS:
// Photo, ID, face verification

PAYMENT OPTIONS:
// SOL, GIG, Google Pay, bank, cards

YOUR ROLE:
// What the assistant should do

RESPONSE STYLE:
// How to communicate

CATEGORIES AVAILABLE:
// All gig categories
`;
```

---

## Deployment

### Web Deployment

#### Vercel (Recommended)

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
cd web
vercel
```

#### Netlify

```bash
# Build
npm run build

# Deploy dist folder to Netlify
```

#### Docker

```bash
# Build image
docker build -t gigworkseeker-ai .

# Run container
docker run -p 3000:3000 gigworkseeker-ai
```

### Android Deployment

#### Google Play Store

1. Generate signed APK/AAB
   ```bash
   ./gradlew bundleRelease
   ```

2. Upload to Play Console

#### Solana dApp Store

1. Build release APK
2. Follow Solana dApp Store submission guidelines
3. Include wallet integration metadata

---

## Integration with Existing App

### Adding to GigWorkSeeker Web

```jsx
// In your router
import GigWorkSeekerAI from './components/GigWorkSeekerAI';

<Route path="/assistant" element={<GigWorkSeekerAI />} />
```

### Adding to GigWorkSeeker Android

```xml
<!-- In nav_graph.xml -->
<fragment
    android:id="@+id/aiAssistantFragment"
    android:name="com.gigworkseeker.app.ui.ai.AIAssistantFragment"
    android:label="AI Assistant" />
```

See [INTEGRATION.md](docs/INTEGRATION.md) for detailed instructions.

---

## API Reference

### Claude API Call

```javascript
const response = await fetch('https://api.anthropic.com/v1/messages', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'anthropic-version': '2023-06-01'
  },
  body: JSON.stringify({
    model: 'claude-sonnet-4-20250514',
    max_tokens: 1000,
    system: systemPrompt,
    messages: conversationHistory
  })
});
```

### Response Format

```json
{
  "content": [
    {
      "type": "text",
      "text": "Assistant response here..."
    }
  ]
}
```

---

## Customization

### Adding Categories

Update the system prompt's `CATEGORIES AVAILABLE` section:

```javascript
CATEGORIES AVAILABLE:
Home Services, Delivery, Tech Support, Tutoring, Pet Care, 
Cleaning, Landscaping, Handyman, Moving, Photography, 
Event Planning, Personal Training, Cooking/Catering, 
Auto Services, Creative Services, Virtual Assistance,
// Add your new categories here
Legal Services, Healthcare, Education, and more.
```

### Adding Suggestion Patterns

```javascript
// In generateSuggestions function
if (lowerUser.includes('verify') || lowerUser.includes('verification')) {
  return [
    { icon: '📸', text: 'How do I verify my photo?' },
    { icon: '🪪', text: 'What ID do I need?' },
    { icon: '⏱️', text: 'How long does verification take?' }
  ];
}
```

### Theming

Update the color palette in `GWSColors`:

```kotlin
object GWSColors {
    val SolanaGreen = Color(0xFF14F195)  // Primary accent
    val SolanaPurple = Color(0xFF9945FF) // Secondary accent
    val DarkBg = Color(0xFF0D0D0D)       // Background
    // ... customize as needed
}
```

---

## Troubleshooting

### Common Issues

| Issue | Solution |
|-------|----------|
| CORS errors (web) | Use API proxy or configure CORS headers |
| Blank responses | Check console for API errors |
| Android network errors | Verify INTERNET permission in manifest |
| Slow responses | Claude API may have latency; show loading state |

### Debug Mode

Enable verbose logging:

```javascript
// Web
console.log('Request:', requestBody);
console.log('Response:', data);
```

```kotlin
// Android
Log.d("AIAssistant", "Request: $requestBody")
Log.d("AIAssistant", "Response: $responseBody")
```

---

## Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/voice-input`)
3. Commit changes (`git commit -m 'Add voice input support'`)
4. Push to branch (`git push origin feature/voice-input`)
5. Open Pull Request

---

## License

MIT License - see [LICENSE](LICENSE) for details.

---

## Contact

- **Website**: [gigworkseeker.com](https://gigworkseeker.com)
- **Email**: support@gigworkseeker.com
- **Twitter**: [@GigWorkSeeker](https://twitter.com/gigworkseeker)
- **Discord**: [Join Community](https://discord.gg/gigworkseeker)

---

<p align="center">
  <strong>Built with ❤️ on Solana</strong><br>
  <sub>© 2025 GigWorkSeeker. All rights reserved.</sub>
</p>
