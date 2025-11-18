# Edssentials App

A dark, minimalistic React learning platform with interactive roadmaps, AI chatbot, and comprehensive Computer Science/Engineering resources.

## 🎯 Features

### 🤖 **Newton AI Chatbot** (Ultra-Fast, Multi-Source)
- **7 AI sources** with intelligent routing
- **Speed-optimized**: 1-3 second responses via parallel racing
- **Specialized capabilities**:
  - 🔢 Math: WolframAlpha API (instant calculations)
  - 💼 Business: Cohere API (strategic reasoning)
  - 🧠 Reasoning: Groq API (70B model, fastest)
  - 📚 General: Together AI, Hugging Face, AI/ML API
  - 🔒 Privacy: Ollama (100% offline)
- **Smart fallbacks**: Wikipedia + DuckDuckGo for factual queries
- **No setup required**: Works with web search, enhanced with API keys
- See [CHATBOT_SETUP.md](./CHATBOT_SETUP.md) for detailed guide

### 🗺️ **Interactive Learning Roadmaps** (roadmap.sh style)
- **5 comprehensive paths**: Frontend, Backend, DSA, DevOps, ML Engineer
- **Visual node-based roadmap** with dependency unlocking
- **Direct resource links**: YouTube tutorials, docs, courses
- **Progress tracking** persisted across sessions
- **120+ topics** covering full CS curriculum

### 📚 **Resource Library**
- **GitHub repos** (trending, curated)
- **YouTube courses** (video tutorials)
- **DEV.to articles** (community content)
- **arXiv papers** (research publications)
- **MIT OpenCourseWare** (lecture notes, PDFs)

### 💼 **Jobs & Internships**
- Live listings from **Remotive API**
- Filter by type, location, skills
- Match percentage visualization

### 🧪 **Dynamic Assessments**
- **Open Trivia Database API** integration
- Fresh questions every time
- Multiple difficulty levels

### 👥 **Real-time Community**
- Firebase Firestore sync (optional)
- Like posts, create discussions
- localStorage fallback

## 🚀 Quick Start

```powershell
cd "c:\Users\Ghanshyam\Desktop\Eddsent\edssentials-app"
npm install
npm start
```

Open **http://localhost:3000** and click demo login!

## 🔑 Optional Enhancements

Copy `.env.example` to `.env.local` and add any of these (all are FREE):

### For Ultra-Fast AI Chatbot (Recommended):
1. **Groq API** (Fastest, 14.4K req/day): [console.groq.com/keys](https://console.groq.com/keys)
   ```env
   REACT_APP_GROQ_API_KEY=your_key_here
   ```

2. **Cohere API** (Best for business/reasoning): [dashboard.cohere.com/api-keys](https://dashboard.cohere.com/api-keys)
   ```env
   REACT_APP_COHERE_API_KEY=your_key_here
   ```

3. **Together AI** (Powerful models): [api.together.xyz/settings/api-keys](https://api.together.xyz/settings/api-keys)
   ```env
   REACT_APP_TOGETHER_API_KEY=your_key_here
   ```

4. **AI/ML API** (GPT-3.5 access): [aimlapi.com/app/keys](https://aimlapi.com/app/keys)
   ```env
   REACT_APP_AIML_API_KEY=your_key_here
   ```

5. **WolframAlpha** (Best for math): [products.wolframalpha.com/api](https://products.wolframalpha.com/api)
   ```env
   REACT_APP_WOLFRAM_APPID=your_appid_here
   ```

6. **Ollama** (Offline, unlimited): [ollama.ai/download](https://ollama.ai/download)
   ```bash
   ollama pull llama3
   ollama serve
   ```

📚 **Detailed Setup**: See [CHATBOT_SETUP.md](./CHATBOT_SETUP.md)

### For Enhanced Resources:
- **YouTube Data API**: [Google Cloud Console](https://console.cloud.google.com)

### For Real-time Community:
- **Firebase**: [firebase.google.com](https://firebase.google.com) (Spark plan is free)

**The app works fully without any keys!** Newton uses web search as fallback, but AI APIs provide much better, faster answers.

## 🎓 Learning Paths Coverage

- **Frontend**: Internet → HTML/CSS → JavaScript → React → TypeScript → Testing → Deployment
- **Backend**: Protocols → Node.js → Databases → APIs → Auth → Docker → Microservices
- **DSA**: Complexity → Arrays → Trees → Graphs → DP → Advanced Algorithms
- **DevOps**: Linux → Docker → Kubernetes → CI/CD → AWS → Terraform → Monitoring
- **ML Engineer**: Python → Math → NumPy/Pandas → ML → Deep Learning → NLP/CV → MLOps

Each node includes **curated free resources** (YouTube, docs, courses).

## 📖 Notes

- All APIs are public/free with rate limits
- Ollama runs 100% offline after initial model download
- Progress syncs across browser sessions
# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)
