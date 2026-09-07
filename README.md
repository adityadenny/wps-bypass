# wps-bypass

Someone sent you a WPS link. You clicked it. Instead of opening the file, it asked you to install WPS Office.

You just wanted to see a PDF.

This fixes that.

## What it does

Paste the WPS share link. Get a direct link that opens the file in your browser. No app install. No account. No tracking.

It works because WPS share links have two versions of every URL:
- `/cms/docs/d/{SID}` — the "please install our app" funnel page
- `/l/{SID}` — the actual file viewer

This tool extracts the SID from the annoying link and gives you the viewer link.

## Try it

Open `index.html` in any browser. Or visit the live version:

**[Open WPS Link Bypass →](https://adityadenny.github.io/wps-bypass/)**

Paste one or more WPS links (one per line), hit convert, and you get:
- A direct preview link you can open immediately
- A copy button for sharing
- An inline preview so you can check before opening

## How to save as PDF

After the file opens in your browser:
1. Press `Ctrl + P` (or `Cmd + P` on Mac)
2. Select "Save as PDF" as the printer
3. Done

You now have the file locally. No WPS installed.

## Supported link formats

- `ap.wps.com/cms/docs/d/...` (WPS international share links)
- `www.kdocs.cn/view/doc/...` (KDocs Chinese share links)
- `ap.wps.com/l/...` (already short links — passes through)
- `www.kdocs.cn/l/...` (KDocs short links)

## Why this exists

WPS Office makes decent software. Their share links, though, are designed to funnel you into installing their app regardless of whether you need it. The file is right there on their servers, viewable in any browser. They just choose not to show you that option.

Someone shared boarding passes through WPS at work. Four PDFs. Each link opened a page telling me to download a 200MB office suite. I reverse-engineered the share link structure and found the direct viewer path.

Saved the code. Made it a tool. Now you don't have to figure this out yourself.

## How it works (technical)

The tool does client-side URL pattern matching. No server. No API calls. Your links never leave your browser.

```
Input:  https://ap.wps.com/cms/docs/d/cbPaejZVD597hxKT?lg=id-ID&fn=boarding_pass.pdf
                                      ↓ extract SID
Output: https://ap.wps.com/l/cbPaejZVD597hxKT
```

The SID is the unique identifier for the shared document. Both URLs point to the same file. The first one is gated behind an install prompt. The second one opens directly.

## Deploy your own

This is a single HTML file. No build step. No dependencies. Host it anywhere:

- GitHub Pages (free)
- Netlify (free, drag and drop)
- Vercel (free, import from GitHub)
- Any web server
- Your own computer (just double-click the file)

## Privacy

Everything runs in your browser. There are no analytics scripts, no tracking pixels, no cookies, no server-side processing. The code is a single HTML file you can read in five minutes.

## License

MIT. Use it, fork it, host it, modify it. If it saves you from installing WPS, that's enough.
