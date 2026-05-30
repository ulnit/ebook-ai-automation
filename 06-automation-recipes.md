# Chapter 6: Automation Recipes

## Recipe 1: Daily Dev.to Publisher

```python
import urllib.request, json

def publish_devto(title, body, tags):
    url = "https://dev.to/api/articles"
    data = json.dumps({
        "article": {
            "title": title,
            "body_markdown": body,
            "published": True,
            "tags": tags[:4]
        }
    }).encode()
    req = urllib.request.Request(url, data=data,
        headers={"Content-Type": "application/json",
                 "api-key": "YOUR_KEY"})
    return json.loads(urllib.request.urlopen(req).read())
```

## Recipe 2: GitHub Trending Scraper

```python
import urllib.request, json

def trending_repos(days=7):
    url = f"https://api.github.com/search/repositories?q=stars:>100+created:>{days}days&sort=stars&order=desc&per_page=10"
    data = json.loads(urllib.request.urlopen(url).read())
    return [{"name": r["full_name"], "stars": r["stargazers_count"],
             "desc": r.get("description",""), "url": r["html_url"]}
            for r in data["items"]]
```

## Recipe 3: Hacker News Trend Monitor

```python
def hn_trending(query="AI agent", hits=10):
    url = f"https://hn.algolia.com/api/v1/search?query={query}&tags=story&hitsPerPage={hits}"
    data = json.loads(urllib.request.urlopen(url).read())
    return [{"title": h["title"], "points": h["points"],
             "comments": h["num_comments"], "url": h.get("url","")}
            for h in data["hits"] if h.get("points",0) > 10]
```

## Recipe 4: Cron Job Template

```bash
# Add to crontab:
# 0 9 * * * /home/user/scripts/daily-publish.sh

#!/bin/bash
cd /home/user/products
python3 scraper.py > data.json
python3 publisher.py data.json
git add -A && git commit -m "Daily update" && git push
```