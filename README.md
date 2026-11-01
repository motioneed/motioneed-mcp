# Motioneed MCP

Make a product launch video from your AI agent. Give it a URL, get back an MP4 with your real UI, animation, music cut on the beat, and optional voiceover.

> "Make a 15-second vertical launch video for https://your-product.com and give me a share link."

Remote MCP server (Streamable HTTP): `https://www.motioneed.com/mcp`. Nothing to install or render locally: the video is made on Motioneed's servers in a few minutes.

## Setup

1. Get an API key at [motioneed.com/developers](https://www.motioneed.com/developers?ref=github-mcp). A free account gets one (videos up to 10 seconds, with the Motioneed logo). Paid plans: longer videos, no logo.
2. Add the server.

**Claude Code**

```bash
claude mcp add --transport http motioneed https://www.motioneed.com/mcp \
  --header "Authorization: Bearer mk_..."
```

**Cursor** (`.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "motioneed": {
      "url": "https://www.motioneed.com/mcp",
      "headers": { "Authorization": "Bearer mk_..." }
    }
  }
}
```

**Any other MCP client**: server URL `https://www.motioneed.com/mcp`, header `Authorization: Bearer mk_...`.

## Tools

| Tool | What it does |
|---|---|
| `create_video` | Start a video from a public URL and/or a one-line prompt. Options: `seconds` (10, 15, 30, 60, 90), `aspect` (16:9, 9:16, 4:3, 3:4), `purpose` (ad, demo, launch), `voice`, up to 10 screenshots to put on screen. |
| `get_video` | Status and links. Poll until `ready`. |
| `revise_video` | Change a ready video with a note, e.g. "make the headline shorter". The earlier cut is kept. |
| `share_video` | Turn a public share link on or off. |
| `list_videos` | Your 50 newest videos. |
| `get_account` | Plan and credits left. |

Videos spend credits from your account; `get_account` shows the balance. A failed video returns its credits.

## Examples

- "Make a 30-second launch video for https://… with narration."
- "Cut a 9:16 version for X and TikTok."
- "Make the opening slower and end on the pricing page."

## Also

- REST API: `https://www.motioneed.com/v1` ([docs](https://www.motioneed.com/developers?ref=github-mcp#api))
- GitHub Action that turns every release into a launch video: [motioneed/release-video-action](https://github.com/motioneed/release-video-action)
