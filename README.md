# The pages that open Addressed files

Addressed locks a file with a key made of two halves. Our server keeps one half and gives it only to someone who
signs in as one of the people the file was sent to. The other half never reaches us: it travels inside the file (an
attachment) or in the link after the `#` (a link), which browsers never send to any server.

The page that joins the two halves in your browser is served by us, from `envelope.addressed.me`. A changed page could read
what it is given, so we publish every version of it here, exactly as browsers receive it, with its SHA-256. Anyone can
check that the page they were served is the one everybody gets.

- `pages/`: the pages as served now. Their history is this repository's history (`ram-sh/addressed-link-page`).
  - `open.html`: `https://envelope.addressed.me/open`, where an attachment is opened.
  - `l-<kind>.html`: `https://envelope.addressed.me/l?t=<kind>`, where a link is opened (the kind only changes the preview
    picture chat apps show).
- `versions.jsonl`: one line per deploy: when, which revision, and the SHA-256 of every page.

## Check it yourself

```
python -c "import hashlib,urllib.request as u;print(hashlib.sha256(u.urlopen(u.Request('https://envelope.addressed.me/l?t=image',headers={'User-Agent':'check'})).read()).hexdigest())"
```

Compare the result with `"/l?t=image"` on the last line of `versions.jsonl`. In a browser: open the link page, save it
(Ctrl+S, "Webpage, HTML only") and hash the saved file.

## What this can and can't show

- It shows that a page was published, and makes a changed page visible to anyone who checks.
- It does not stop a changed page from being served to someone who doesn't check. No web page can prove that to
  itself; only a browser that checks pages before running them could, and browsers don't do that for ordinary sites yet.
