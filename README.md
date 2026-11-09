<p align="center"><img src="logo.png" width="72" alt="Any Video to Text logo"></p>

# Any Video to Text MCP server

Video transcripts for Claude, ChatGPT, Cursor and any MCP client. Paste a **TikTok, YouTube, Instagram, Facebook or X**
video link in the chat and the assistant gets the transcript, a summary, an answer from the video, or a translation.

- **Remote server:** `https://anyvideototext.com/mcp` (Streamable HTTP). Nothing to install or host.
- **Free:** 5 transcripts and 5 summaries a day per account, videos up to 30 minutes.
- **Credits** for more (no subscription): no daily limit, videos up to 2 hours. See [pricing](https://anyvideototext.com/pricing).
- **Sign-in:** OAuth with Google, or a personal API key (`Authorization: Bearer avt_...`) for clients that can't do OAuth.
- Listed in the [official MCP Registry](https://registry.modelcontextprotocol.io/v0/servers?search=com.anyvideototext/any-video-to-text)
  as `com.anyvideototext/any-video-to-text`.

Website and setup guide: **[anyvideototext.com/mcp-server](https://anyvideototext.com/mcp-server)**

## Tools

| Tool | What it does |
|---|---|
| `get_transcript` | Full text of what is said in a public TikTok, YouTube (incl. Shorts), Instagram, Facebook or X video. Optional `[mm:ss]` timestamps. Uses the video's captions when it has them, otherwise Whisper speech-to-text (about 100 languages). |
| `transcribe_status` | Check a transcript that is still being made, by the `jobId` that `get_transcript` or `summarize_video` returned. |
| `summarize_video` | 2-3 sentence TL;DR plus 3-8 key points with timestamps. |
| `ask_video` | Answers one question using only what is said in the video, with up to 3 timestamps. Supports follow-ups. |
| `translate_video` | Translates the transcript line by line into one of 36 languages, in parts for long videos. |
| `list_my_transcripts` | Lists and searches the transcripts kept in your account (titles, creators and what was said). |
| `get_my_transcript` | Full text of a kept transcript by id. Free, however old it is. |
| `my_account` | Credit balance and free transcripts and summaries left today. |

## Connect

### Claude (web, desktop, mobile)
1. **Settings → Connectors → Add custom connector.**
2. Name: `Any Video to Text`. URL: `https://anyvideototext.com/mcp`
3. **Connect**, sign in with Google, then **Allow**.

### ChatGPT
Settings → Connectors → **Create** (turn on developer mode first), paste `https://anyvideototext.com/mcp`, then sign in
with Google.

### Claude Code
```bash
claude mcp add --transport http any-video-to-text https://anyvideototext.com/mcp
```
Then run `/mcp` in Claude Code and sign in.

### Cursor, VS Code, Windsurf and other clients
Add the remote server to the client's MCP config. OAuth sign-in opens in the browser on first use.
See [`examples/`](examples) for ready-made files:

```json
{
  "mcpServers": {
    "any-video-to-text": {
      "url": "https://anyvideototext.com/mcp"
    }
  }
}
```

Clients without OAuth: create an API key on your [account page](https://anyvideototext.com/account#mcp) and send it as a
header:

```json
{
  "mcpServers": {
    "any-video-to-text": {
      "url": "https://anyvideototext.com/mcp",
      "headers": { "Authorization": "Bearer avt_YOUR_KEY" }
    }
  }
}
```

## Try it
> Get the transcript of this video and give me the 5 main points: https://www.youtube.com/watch?v=WZyRbnpGyzQ

> What does the speaker say about pricing in this TikTok? [paste link]

> Translate this Instagram Reel's transcript into Spanish: [paste link]

## Limits and privacy
- Public videos only. Private, age-gated or region-blocked videos can't be read.
- Free: up to 30 minutes per video without captions. With credits: up to 2 hours, 1 credit per started 10 minutes.
  Videos someone already transcribed come back free.
- Transcripts you get while signed in are kept in *My transcripts* until you delete them. Disconnect an app or revoke a
  key from your account page at any time.
- Terms: [anyvideototext.com/terms](https://anyvideototext.com/terms) · Privacy: [anyvideototext.com/privacy](https://anyvideototext.com/privacy)

## What's in this repo
This repo documents the hosted server: setup, tools and client configs. The server itself runs on Cloudflare Workers at
anyvideototext.com and is not self-hosted. `server.json` is the entry published to the official MCP Registry.

## Support
Email [hello@anyvideototext.com](mailto:hello@anyvideototext.com) or open an issue here.
