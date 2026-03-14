---
title: "Subscribe"
description: "How to get notified when new posts are published"
tags:
  - meta
---

# Subscribe to The Data Pipeline Doctrine

Want to know when new posts go live? You have two options, both free and requiring zero sign-up on my end.

**RSS Feed** — The classic. Add the feed to your reader of choice and new posts show up automatically. Works with Feedly, Inoreader, NetNewsWire, or any RSS-compatible app.

**GitHub Watch** — If you're already on GitHub, you can watch the repository and get notified when new content is pushed. Good if you prefer GitHub's notification system over a dedicated feed reader.

Pick whichever fits your workflow. Both methods are explained below.

## RSS Feed

RSS (Really Simple Syndication) is a decades-old protocol that lets you subscribe to websites without giving away your email address. Your feed reader periodically checks for new posts and shows them in a unified inbox. No algorithms, no tracking, no missed updates buried in a spam folder.

**The feed URL:** [/index.xml](/index.xml)

Copy that link into any RSS reader, or use the quick-add links below.

### Feedly

1. Go to [feedly.com](https://feedly.com) and sign in (free account works fine)
2. Click the **+** button or "Follow your favorite websites"
3. Paste the feed URL: `https://davidtwu.github.io/index.xml`
4. Click **Follow**

### Inoreader

1. Go to [inoreader.com](https://www.inoreader.com) and sign in
2. Click the **+** icon in the left sidebar
3. Select "Feeds" and paste: `https://davidtwu.github.io/index.xml`
4. Click **Subscribe**

### NetNewsWire

NetNewsWire is a free, open-source reader for Mac and iOS.

1. Download from [netnewswire.com](https://netnewswire.com)
2. Open the app and press **⌘N** (Mac) or tap **+** (iOS)
3. Paste the feed URL: `https://davidtwu.github.io/index.xml`
4. Click **Add**

Any other RSS reader will work too—just add the feed URL and you're set.


## GitHub Watch

If you already live in GitHub, you can skip the RSS reader entirely and use GitHub's built-in notification system. When you "watch" the repository, GitHub sends you notifications whenever new content is pushed.

**Watch settings:** [github.com/davidtwu/data-pipeline-doctrine](https://github.com/davidtwu/data-pipeline-doctrine)

Go to the repository and click the **Watch** button in the top right.

### Notification Types

GitHub offers three watch modes:

- **Participating and @mentions** — Only notifies you if you're directly involved (not useful for following a blog)
- **All Activity** — Notifies you on every push, issue, PR, and discussion. Comprehensive but potentially noisy.
- **Custom** — Pick exactly what you want. For blog updates, select **Releases** if I tag new posts, or **Pushes** to catch every content update.

For most readers, **Custom → Pushes** strikes the right balance: you'll get notified when new posts are published without noise from other repository activity.

### What You'll Receive

When new content is pushed to the repository, GitHub sends a notification to your configured channels (email, mobile app, or web). The notification includes the commit message, which typically describes the new post.

You can manage notification delivery in your [GitHub notification settings](https://github.com/settings/notifications)—choose email, mobile push, or just the GitHub web inbox.


## Which Should I Choose?

Both options work well—the right choice depends on your existing workflow.

| Feature | RSS Feed | GitHub Watch |
|---------|----------|--------------|
| Requires account | Any RSS reader (many free options) | GitHub account |
| Notification delivery | In your feed reader | Email, mobile push, or GitHub inbox |
| Content preview | Full post content in reader | Commit message only (click through to read) |
| Other subscriptions | Combine with 100s of other blogs/sites | Mixed with your GitHub activity |
| Setup time | ~1 minute | ~30 seconds |
| Works offline | Yes (syncs when online) | No |

**Choose RSS if:**
- You already use a feed reader or want to start
- You follow multiple blogs and want them in one place
- You prefer reading full posts without leaving your reader
- You want your blog subscriptions separate from work notifications

**Choose GitHub Watch if:**
- You're already on GitHub daily and check notifications there
- You don't want to set up another app
- You're comfortable clicking through to read posts
- You want the simplest possible setup
