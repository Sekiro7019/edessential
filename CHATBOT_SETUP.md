# Newton AI Chatbot Setup Guide

Newton is an intelligent AI assistant that can answer questions about education, business, reasoning, mathematics, and general knowledge. It uses multiple AI APIs for fast, accurate responses.

## 🚀 Quick Start (Free APIs)

### Option 1: Groq API (Recommended - Fastest)
1. Visit https://console.groq.com/keys
2. Sign up for free account
3. Create an API key
4. Add to `.env.local`: `REACT_APP_GROQ_API_KEY=your_key_here`
5. **Model Used**: Llama 3.1 70B (Most powerful, fastest inference)

### Option 2: Cohere API (Great for Reasoning)
1. Visit https://dashboard.cohere.com/api-keys
2. Sign up for free account
3. Generate API key
4. Add to `.env.local`: `REACT_APP_COHERE_API_KEY=your_key_here`
5. **Model Used**: Command-R (Excellent reasoning & analysis)

### Option 3: Together AI (Powerful Models)
1. Visit https://api.together.xyz/settings/api-keys
2. Create free account
3. Generate API key
4. Add to `.env.local`: `REACT_APP_TOGETHER_API_KEY=your_key_here`
5. **Model Used**: Llama 3 70B (Advanced capabilities)

### Option 4: Hugging Face (Versatile)
1. Visit https://huggingface.co/settings/tokens
2. Create free account
3. Generate access token
4. Add to `.env.local`: `REACT_APP_HUGGINGFACE_API_KEY=your_key_here`
5. **Models Used**: Mixtral 8x7B, Mistral 7B, Llama 2 70B

### Option 5: AI/ML API (GPT-3.5 Access)
1. Visit https://aimlapi.com/app/keys
2. Sign up for free tier
3. Copy API key
4. Add to `.env.local`: `REACT_APP_AIML_API_KEY=your_key_here`
5. **Model Used**: GPT-3.5 Turbo (ChatGPT-like responses)

### Option 6: WolframAlpha (For Mathematics)
1. Visit https://products.wolframalpha.com/api/
2. Sign up for free tier (2,000 queries/month)
3. Get App ID
4. Add to `.env.local`: `REACT_APP_WOLFRAM_APPID=your_appid_here`
5. **Best For**: Math calculations, formulas, data queries

### Option 7: Ollama (Offline, No API Key)
1. Download Ollama: https://ollama.ai/download
2. Install and run: `ollama pull llama3`
3. Start server: `ollama serve`
4. No API key needed!
5. **Best For**: Privacy, offline use, unlimited queries

## 🎯 How Newton Works

### Intelligent Request Routing
Newton automatically detects the type of question and routes to the best AI:

- **Math Questions** → WolframAlpha (instant calculations)
- **Business Questions** → Cohere (strategic reasoning)
- **Reasoning Questions** → Groq/Together AI (logical analysis)
- **General Questions** → Any available AI (fastest response)

### Speed Optimization
- **Parallel Racing**: Multiple APIs compete, first response wins
- **Response Time**: Typically 1-3 seconds
- **Fallback Chain**: 7 different AI sources + web search
- **Timeout Protection**: Never waits more than 10 seconds

### Capability Matrix

| API | Speed | Math | Business | Reasoning | General | Free Tier |
|-----|-------|------|----------|-----------|---------|-----------|
| Groq | ⚡️⚡️⚡️ | ✅ | ✅ | ✅ | ✅ | 14,400 req/day |
| Cohere | ⚡️⚡️ | ✅ | ⭐️⭐️⭐️ | ⭐️⭐️⭐️ | ✅ | 100 req/min |
| Together AI | ⚡️⚡️ | ✅ | ✅ | ⭐️⭐️⭐️ | ✅ | $25 free credit |
| Hugging Face | ⚡️ | ✅ | ✅ | ✅ | ✅ | Unlimited (slower) |
| AI/ML API | ⚡️⚡️ | ✅ | ✅ | ✅ | ⭐️⭐️⭐️ | 100 req/day |
| WolframAlpha | ⚡️⚡️⚡️ | ⭐️⭐️⭐️ | ❌ | ❌ | ⚡️ | 2,000 req/month |
| Ollama | ⚡️ | ✅ | ✅ | ✅ | ✅ | Unlimited (local) |

## 🔧 Configuration

### Minimum Setup (1 API Key)
Just add **one** of these to `.env.local`:
```env
REACT_APP_GROQ_API_KEY=your_groq_key_here
```

### Recommended Setup (3 API Keys)
For best coverage and redundancy:
```env
REACT_APP_GROQ_API_KEY=your_groq_key_here
REACT_APP_COHERE_API_KEY=your_cohere_key_here
REACT_APP_WOLFRAM_APPID=your_wolfram_id_here
```

### Maximum Setup (All APIs)
For ultimate reliability and performance:
```env
REACT_APP_GROQ_API_KEY=your_groq_key_here
REACT_APP_COHERE_API_KEY=your_cohere_key_here
REACT_APP_TOGETHER_API_KEY=your_together_key_here
REACT_APP_HUGGINGFACE_API_KEY=your_hf_key_here
REACT_APP_AIML_API_KEY=your_aiml_key_here
REACT_APP_WOLFRAM_APPID=your_wolfram_id_here
REACT_APP_OLLAMA_URL=http://localhost:11434
```

## 📊 Example Questions Newton Can Answer

### Mathematics
```
"Calculate the derivative of x^3 + 2x^2 - 5x + 1"
"What is 15% of 340?"
"Solve the equation: 2x + 5 = 15"
```

### Business
```
"What are effective marketing strategies for startups?"
"How to calculate ROI on an investment?"
"Best practices for customer retention"
```

### Reasoning & Logic
```
"Why does the sky appear blue?"
"How does photosynthesis work?"
"Explain the principle of supply and demand"
```

### General Knowledge
```
"Who invented the telephone?"
"What is quantum computing?"
"Tell me about machine learning algorithms"
```

### Personal & Educational
```
"How to improve time management skills?"
"Best way to learn programming?"
"Tips for effective studying"
```

## 🛠️ Troubleshooting

### Newton not responding?
1. Check if at least one API key is configured in `.env.local`
2. Restart the development server: `npm start`
3. Check browser console for error messages
4. Verify API keys are valid and have remaining quota

### Slow responses?
1. Add REACT_APP_GROQ_API_KEY for fastest responses
2. Consider running Ollama locally for instant responses
3. Check your internet connection
4. Some APIs may be rate-limited (wait a minute and try again)

### "Unable to access AI services" error?
- This means no API keys are configured
- Add at least one API key from the options above
- Web search fallback will still work for factual questions

## 💡 Pro Tips

1. **Use Multiple APIs**: Configure 2-3 APIs for redundancy
2. **Groq for Speed**: Best for real-time conversations
3. **Cohere for Business**: Best for strategic questions
4. **WolframAlpha for Math**: Always accurate calculations
5. **Ollama for Privacy**: No data leaves your computer
6. **Free Tiers**: All listed APIs have generous free tiers
7. **Rate Limits**: Newton automatically handles rate limits by trying alternative APIs

## 🔒 Privacy & Security

- API keys stored in `.env.local` (never committed to git)
- Ollama option provides 100% local processing
- No conversation history stored on external servers
- Each API call is independent (no tracking)
- HTTPS encryption for all API communications

## 📈 API Rate Limits (Free Tiers)

- **Groq**: 14,400 requests/day, 30 requests/minute
- **Cohere**: 100 requests/minute
- **Together AI**: $25 free credit (~2,500 requests)
- **Hugging Face**: Unlimited (may queue during high load)
- **AI/ML API**: 100 requests/day
- **WolframAlpha**: 2,000 requests/month
- **Ollama**: Unlimited (runs on your hardware)

## 🚀 Performance Metrics

- **Average Response Time**: 1-3 seconds
- **Success Rate**: 95%+ (with 2+ APIs configured)
- **Concurrent Requests**: Handled via racing algorithm
- **Fallback Depth**: 7 AI sources + web search
- **Timeout**: Maximum 10 seconds per question

---

**Need Help?** Open an issue or check the main README.md for general setup instructions.
