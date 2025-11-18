# 🚀 Quick API Setup Guide

Get Newton AI chatbot running with powerful AI in under 5 minutes!

## Option 1: Groq API (⚡ Fastest - RECOMMENDED)

**Why Groq?** Blazing fast responses (1-2 seconds), powerful 70B model, 14,400 free requests per day.

### Setup Steps:
1. Visit: https://console.groq.com/keys
2. Click "Sign up" (free account)
3. Verify email
4. Click "Create API Key"
5. Copy the key
6. Create `.env.local` file in project root:
   ```env
   REACT_APP_GROQ_API_KEY=gsk_your_key_here
   ```
7. Restart: `npm start`
8. Test Newton!

**That's it!** Newton is now powered by Llama 3.1 70B.

---

## Option 2: Cohere (🧠 Best for Business/Reasoning)

**Why Cohere?** Excellent reasoning, great for business questions, 100 req/min free.

### Setup Steps:
1. Visit: https://dashboard.cohere.com/api-keys
2. Sign up with email or Google
3. Click "Create Trial Key"
4. Copy the key
5. Add to `.env.local`:
   ```env
   REACT_APP_COHERE_API_KEY=your_key_here
   ```
6. Restart: `npm start`

---

## Option 3: Together AI (💪 Most Powerful)

**Why Together?** Access to largest models, $25 free credit.

### Setup Steps:
1. Visit: https://api.together.xyz/signup
2. Sign up (email verification required)
3. Go to: https://api.together.xyz/settings/api-keys
4. Click "Create new API key"
5. Copy the key
6. Add to `.env.local`:
   ```env
   REACT_APP_TOGETHER_API_KEY=your_key_here
   ```
7. Restart: `npm start`

---

## Option 4: For Math Questions - WolframAlpha

**Why Wolfram?** Perfect for calculations, instant answers for math.

### Setup Steps:
1. Visit: https://products.wolframalpha.com/api/
2. Click "Get an AppID"
3. Sign up (free tier: 2,000 queries/month)
4. Copy your AppID
5. Add to `.env.local`:
   ```env
   REACT_APP_WOLFRAM_APPID=your_appid_here
   ```
6. Restart: `npm start`

Now Newton can solve complex math instantly!

---

## Multiple APIs (Recommended)

For best performance and reliability, add 2-3 APIs:

```env
# Fast general AI
REACT_APP_GROQ_API_KEY=gsk_your_groq_key

# Business reasoning
REACT_APP_COHERE_API_KEY=your_cohere_key

# Math calculations
REACT_APP_WOLFRAM_APPID=your_wolfram_id
```

Newton will automatically:
- Use fastest available API
- Fallback if one is rate-limited
- Route questions to best AI

---

## Troubleshooting

### Newton not using AI?
- Check `.env.local` file exists in project root
- Verify keys are correct (no extra spaces)
- Restart dev server: Stop (Ctrl+C) → `npm start`

### "Rate limit" errors?
- Add second API key as backup
- Wait 1 minute and try again
- Free tiers reset daily

### Still using web search?
- Web search is default fallback (always works)
- Add any API key for AI-powered responses
- Check console for error messages (F12)

---

## Testing Your Setup

After adding API key(s):

1. Restart: `npm start`
2. Open Newton chatbot (Dashboard → "Ask Newton")
3. Try these test questions:
   - Math: "Calculate 15% of 340"
   - Business: "Best marketing strategy for startups?"
   - Reasoning: "Why is the sky blue?"
   - General: "Explain React hooks"

**Fast response (1-3 sec) = AI working! ✅**
**Slow response (5+ sec) = Using web fallback**

---

## Which API Should I Choose?

| If you want... | Choose... | Free Limit |
|----------------|-----------|------------|
| Fastest responses | Groq | 14,400/day |
| Business advice | Cohere | 100/min |
| Most powerful | Together AI | $25 credit |
| Math/calculations | WolframAlpha | 2,000/month |
| Privacy/offline | Ollama | Unlimited |

**Pro tip**: Add Groq + WolframAlpha for speed + math = best combo! 🚀

---

## Next Steps

- ✅ Got API working? Check out [CHATBOT_SETUP.md](./CHATBOT_SETUP.md) for advanced features
- 💡 Want more? Add AI/ML API for GPT-3.5 access
- 🔒 Want privacy? Install Ollama for 100% local AI

**Questions?** Check the main [README.md](./README.md) or open an issue.

---

**Time to get API key: 3-5 minutes**  
**Result: 10x better chatbot responses! 🎉**
