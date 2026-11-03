---
name: update-paper
description: Update a working paper on hirth.dk after a new version is posted on SSRN, by refreshing its date and abstract, moving it to the top of the Working Papers list, and adding a news item. Use when the user says a paper was updated or revised, gives an SSRN link or abstract_id, or runs /update-paper.
argument-hint: "<SSRN URL or abstract_id>"
---

# Update a paper from SSRN

A paper update always touches two data files:

- `_data/working_papers.yml`: the paper's entry (`title`, `authors`, `date`, `links`, `abstract`)
- `_data/news.yml`: a news item announcing the new version

## 1. Find the paper

Grep the repo for the SSRN abstract_id (the number in the URL). Entries link to SSRN in two forms, `https://papers.ssrn.com/sol3/papers.cfm?abstract_id=N` and `https://ssrn.com/abstract=N`, so search for the bare number. If it is not in `working_papers.yml`, it is a new paper or a published one: ask the user before going further.

## 2. Read the SSRN page

SSRN blocks automated fetches:
- WebFetch gets HTTP 403.
- The built-in browser gets stuck on a Cloudflare bot check. Never try to get past it.

Use **Claude in Chrome**, which gets through because it runs in the user's own browser. Load the `anthropic-skills:chrome-browser` skill first. If `tabs_context_mcp` says it is not connected, run `list_connected_browsers`. The extension sometimes takes a moment to pair, so if the list is empty, ask the user to check that the extension is signed in, then try again. If Chrome still can't be reached, ask the user to paste the "Date Written" and the abstract.

Open the page in a new tab, read it with `get_page_text`, and close the tab afterwards. From the page, take:
- **Date Written**, which becomes the `date` (format "November 3, 2026")
- **Abstract**
- Title and authors, only to check them against the existing entry
- **JEL Classification**: check it fits the paper. Finance papers use G codes, so codes from another field are probably a submission typo. Point it out to the user; don't change anything on SSRN.

## 3. Edit `working_papers.yml`

- Set `date` to the Date Written.
- Replace `abstract` with the SSRN text if it changed. Keep the folded `>-` block, wrap lines at about 100 characters, and follow the site's style, for example "2008-09" rather than SSRN's LaTeX-style "2008--09". Tell the user which sentences changed.
- Move the entry to the **top** of the `papers:` list, and leave the other papers in their current order.
- Keep `authors` and `links` as they are unless SSRN shows a change. If it does, confirm with the user first.

## 4. Add a news item to `news.yml`

Items above `- divider: true` are upcoming events. Put the new item **directly below the divider**, since it becomes the newest item in the past log:

```yaml
- date: "3 Nov 2026"
  text: |-
    A new version of "<Title>" is [available at SSRN](<SSRN URL as used in working_papers.yml>).
```

For a paper that is new to the site, use `A new working paper "<Title>" is [available at SSRN](...)`.

## 5. Preview

Start the `jekyll` server from `.claude/launch.json` with `preview_start`. Wait until `http://localhost:4000/` responds, then check:
- `/working-papers/`: the paper comes first and shows the new date and abstract.
- `/`: the news item appears. The page renders straight quotes as curly ones (“ ”), so if text searches in the browser miss, grep `_site/index.html` instead.

## 6. Commit and push, only when the user asks

- Commit message: `Update <short title> paper to <Mon YYYY> version`.
- Before pushing, run `git fetch`. PRs are often merged on GitHub in the meantime, so if `origin/main` is ahead, rebase the unpushed commit onto it, then push.
