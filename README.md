# Video to Code

A Claude Code plugin that converts video animations, GIFs, and interactive demos into production-ready React components using AI-powered frame-by-frame analysis.

## Features

- **Video Analysis**: Uses Google Gemini 2.5 Flash to analyze animations frame-by-frame
- **Smart Download**: Handles authenticated URLs (Cloudflare R2, signed URLs) via Puppeteer
- **Animation Lab**: Interactive preview environment for real-time iteration
- **Feedback Loop**: Structured feedback collection to refine animations until perfect
- **Framework Support**: Works with Next.js (App Router & Pages Router) and Vite

## Installation

### 1. Add the plugin to Claude Code

```bash
claude mcp add-json video-to-code '{"type": "project", "scope": "global", "path": "/path/to/claude-video-to-code"}'
```

Or manually add to your Claude Code settings.

### 2. Set up Gemini API Key

1. Go to [Google AI Studio](https://aistudio.google.com/apikey)
2. Click "Create API key"
3. Add to your shell config (`~/.zshrc` or `~/.bashrc`):

```bash
export GEMINI_API_KEY="your-api-key-here"
```

4. Restart your terminal and Claude Code

## Usage

Just ask Claude to convert a video to code:

```
/video-to-code
```

Or describe what you want:

- "Convert this video animation to React code"
- "Replicate this interaction from the video"
- "Build this GIF animation in React"
- "Implement this motion effect"

### Supported Input Types

- Direct video URLs (mp4, webm)
- GIF URLs
- Webpage URLs containing video/animation
- Local video file paths

## How It Works

1. **Download**: Fetches the video (uses Puppeteer for authenticated URLs)
2. **Analyze**: Sends to Gemini 2.5 Flash for detailed motion analysis
3. **Generate**: Creates a React component in Animation Lab
4. **Preview**: You review at `/__animation_lab` route
5. **Iterate**: Provide feedback, Claude adjusts until perfect
6. **Export**: Final component saved to your preferred location

## Animation Lab

The plugin creates a temporary preview environment:

```
.claude-animation/
├── lab/
│   └── Animation.tsx       # Current implementation
├── gemini-spec.md          # Raw Gemini analysis
└── iteration-log.md        # Changes across iterations
```

Preview at `http://localhost:[PORT]/__animation_lab`

## Common Adjustments

| Issue | Solution |
|-------|----------|
| Too stiff | Lower `stiffness`, increase `damping` |
| Too bouncy | Increase `damping`, lower `mass` |
| Too slow | Increase `stiffness` |
| Too fast | Lower `stiffness`, increase `mass` |
| Not enough movement | Increase rotation/movement multiplier |
| Too much movement | Decrease rotation/movement multiplier |

## Requirements

- Claude Code CLI
- Node.js 18+
- Google Gemini API key
- React project (Next.js or Vite recommended)
- `framer-motion` for most animations

## License

MIT
