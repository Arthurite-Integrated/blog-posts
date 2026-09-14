# Contributing a blog post

## 1. Create the file

Add one file per post to `posts/` or `posts/YYYY/MM/DD/`. The filename becomes the URL, so it must be:

- lowercase words separated by hyphens — `planning-an-aws-migration.mdx`, not `Planning AWS Migration.mdx`
- permanent — renaming a published post changes its URL and breaks every link to it

## 2. Frontmatter

Every post starts with this block. The landing site rejects a post that is missing a required field or has a field that
is not listed here.

```mdx
---
title: Planning a migration to AWS
excerpt: One or two sentences shown on the blog card and in link previews.
date: 2026-09-14
author: Jane Doe
category: Cloud
cover: planning-an-aws-migration.jpg
featured: false
---

The post body starts here, written in Markdown.
```

| Field      | Required | Rules                                                                        |
| ---------- | -------- | ---------------------------------------------------------------------------- |
| `title`    | yes      | The post headline.                                                           |
| `excerpt`  | yes      | Keep it short; it is clipped on the blog card.                               |
| `date`     | yes      | `YYYY-MM-DD`. Posts are listed newest first.                                 |
| `author`   | yes      | The name shown on the post.                                                  |
| `category` | yes      | Exactly one of the categories below.                                         |
| `cover`    | no       | A filename inside `images/`. Without it the post shows a branded panel.      |
| `featured` | no       | `true` puts the post in the large slot at the top of `/blog`. Default false. |

### Categories

`Cloud`, `AI & Data`, `Engineering`, `Company`

Categories are defined in `official-landing` (`src/lib/blog/categories.ts`). Adding one means changing that file and this
list together.

## 3. Images

Put image files in `images/`.

- **Cover:** set `cover` to the filename, e.g. `cover: planning-an-aws-migration.jpg`.
- **Inside the post:** reference the image relative to the post file:

  ```md
  ![Architecture of the target AWS environment](../images/target-architecture.png)
  ```

Always write real alt text describing what the image shows.

## 4. Preview in the real site

Posts are previewed inside a local checkout of the landing site, where `content/blog` is a full clone of this repo.

```bash
git clone git@github.com:Arthurite-Integrated/official-landing.git
cd official-landing
git submodule update --init
bun install

cd content/blog
git remote set-url --push origin git@github.com:Arthurite-Integrated/blog-posts.git
git switch -c post/planning-an-aws-migration
# write posts/planning-an-aws-migration.mdx

cd ../..
bun dev
```

Open `http://localhost:3000/blog`. Edits to a post reload the page; a brand-new post file needs `bun dev` restarted.

When the post is ready, commit and push **from inside `content/blog`** — that is this repo — and open a pull request here.
Never commit the `content/blog` change in `official-landing`; publishing moves that pointer for you.

## 5. Merge

The **Validate posts** check must pass before merging. Merging into `main` publishes the post.
