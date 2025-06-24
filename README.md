# 🚭 Stop Smoking Motivator - LLM Vibe-Coding Comparison

A comprehensive comparison of three leading AI models implementing a single-page web application from a detailed Product Requirements Document (PRD).

## 📋 Project Overview

This project evaluates the coding capabilities of three state-of-the-art AI models by having them implement the same web application: a **Stop Smoking Motivator**. Each model receives the same PRD and is tasked with creating a self-contained, single-page HTML application.

### 🔄 Iterative Approach

This comparison uses an **iterative development approach** where each model will go through multiple iterations to refine their implementations:

- **Iteration 1**: Core functionality implementation from PRD specifications. No human feedback will be given from this iteration.
- **Iteration 2**: Image analysis enhancement - models analyze a screenshot of their iteration 1 result and create improvements
- **Future Iterations**: Additional refinements based on specific feedback or feature requests

Each iteration is saved as `index-N.html` in its folder where N is the iteration number.

### 🎯 Application Features

The Stop Smoking Motivator is a web app that helps recent quitters stay motivated by showing:

- **Real-time Progress Tracking** - Live counters for time smoke-free, cigarettes avoided, and money saved
- **Health Benefits Timeline** - 21 physiological milestones with progress visualization
- **Motivational Content** - Rotating inspirational quotes and achievement celebrations
- **Multi-currency Support** - Thailand (฿) and USA ($) pricing

### 🤖 Models Under Comparison

| Model | Version | Provider | Iteration 1 | Iteration 2 |
|-------|---------|----------|-------------|-------------|
| **o3** | Latest | OpenAI | ✅ Complete | ✅ Complete |
| **Claude Sonnet** | 4.0 | Anthropic | ✅ Complete | ✅ Complete |
| **Gemini** | 2.5 Pro | Google | ✅ Complete | ✅ Complete |

## 📊 Implementation Tracking

### Iteration Results

| Model | Iteration | Status | Key Achievements | Issues/Gaps | Overall Score |
|-------|-----------|--------|------------------|-------------|---------------|
| **o3** | 2 | ✅ Complete | Fixed missing Edit button autonomously, slight improvements in several fields | | 4/10 |
| **Claude Sonnet 4.0** | 2 | ✅ Complete | Improvements in several fields | | 8/10 |
| **Gemini 2.5 Pro** | 2 | ✅ Complete | Big improvements, autonomously discovered timeline should be vertical | | 9/10 |

### Evaluation Criteria

Each implementation will be scored (1-10) based on overall subjective assessment of quality, functionality, and user experience.

## 📁 File Structure

```
stop-smoking-calc/
├── README.md              # This comparison document
├── PRD.md                 # Product Requirements Document
├── prompt-1.txt           # Initial implementation prompt
├── prompt-2.txt           # Image analysis iteration prompt
├── o3/
│   ├── index-1.html       # OpenAI o3 implementation (Iteration 1)
│   └── index-2.html       # OpenAI o3 implementation (Iteration 2)
├── sonnet4/
│   ├── index-1.html       # Claude Sonnet 4.0 implementation (Iteration 1)
│   └── index-2.html       # Claude Sonnet 4.0 implementation (Iteration 2)
└── gemini/
    ├── index-1.html       # Gemini 2.5 Pro implementation (Iteration 1)
    └── index-2.html       # Gemini 2.5 Pro implementation (Iteration 2)
```

## 🎨 Technical Requirements

Based on the PRD, each implementation must:

- **Single File** - Complete app in one `index.html` file
- **No Dependencies** - Pure HTML, CSS, and JavaScript only
- **Offline Capable** - Works without internet after initial load
- **Mobile Responsive** - Mobile-first design with desktop optimization
- **Performance** - First Contentful Paint < 0.5s on 3G Fast
- **Privacy First** - No external network requests (optional analytics)

## 🚀 Getting Started

### Testing an Implementation

1. Navigate to the desired model's folder (e.g., `o3/`, `sonnet4/`, `gemini/`)
2. Open `index-1.html` (or the desired iteration) in your web browser
3. Enter your quit data and explore the features
4. Test sharing functionality and responsive design

## 🔍 Image Analysis Methodology (Iteration 2)

Iteration 2 introduces a unique testing approach to evaluate each model's **visual analysis capabilities**:

### Process Overview
1. **Screenshot Capture** - Each model's iteration 1 implementation is manually tested in Chrome and screenshotted
2. **Visual Analysis Prompt** - The same `prompt-2.txt` is used for all models along with their respective screenshot
3. **Enhancement Implementation** - Models must analyze their visual output and create improved `index-2.html` versions

### What This Tests
- **Visual Design Understanding** - Can models assess UI/UX quality from screenshots?
- **Self-Assessment** - How well can models critique their own work?
- **Design Improvement** - Can models translate visual observations into code improvements?
- **Image-to-Code Translation** - Testing multimodal capabilities in practical coding scenarios

## 📝 Notes

- **Iteration 1** uses the same PRD as input for all models
- **Iteration 2** uses the same prompt for all models + model-specific screenshot as input

---

**Last Updated:** [Current Date]  
**Status:** Iteration 1 Complete (3/3 Models) | Iteration 2 Complete (3/3 Models)