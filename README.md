# Arthurite Integrated — Blog Posts

The posts behind the blog on the Arthurite Integrated landing site.

This repo holds content only. [`Arthurite-Integrated/official-landing`](https://github.com/Arthurite-Integrated/official-landing)
mounts it as a git submodule at `content/blog` and renders every `.mdx` file in `posts/` with Fumadocs MDX, inside the
site's own navigation bar and footer.

## Layout

```
posts/<slug>.mdx                 one file per post — the filename is the URL
posts/YYYY/MM/DD/<slug>.mdx      same, filed by publish date
images/                          cover images and images used inside posts
```

`posts/planning-an-aws-migration.mdx` and `posts/2026/09/14/planning-an-aws-migration.mdx` are both served at `/blog/planning-an-aws-migration`.

## How a post goes live

1. **Open a pull request here.** The **Validate posts** workflow builds the landing site against your branch, so a
   frontmatter mistake or a broken image path fails on the pull request instead of on the live site.
2. **Merge it into `main`.** The **Publish to landing** workflow sends the merge commit to `official-landing`.
3. **`official-landing` publishes it.** Its **Update blog content** workflow points `content/blog` at that commit, merges
   the change into its `main`, and Vercel deploys the site.

Nothing in `official-landing` is edited by hand to publish a post.

## One-time setup

**Publish to landing** needs a repository secret named `LANDING_DISPATCH_TOKEN`: a fine-grained personal access token
with

- **Resource owner:** `Arthurite-Integrated`
- **Repository access:** only `official-landing`
- **Permissions:** Contents — Read and write

Without it the workflow fails loudly and nothing is published.

## Writing a post

See [CONTRIBUTING.md](CONTRIBUTING.md) for the frontmatter contract, categories, images, and how to preview a post in the
real site before merging.
