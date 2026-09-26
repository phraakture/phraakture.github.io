# rubai's Personal Website

This project is a personal website and blog for rubai, hosted on GitHub Pages at phraakture.github.io. It serves as a portfolio, blog, and repository of personal reflections.

## Project Structure

- `_posts/`: Contains all blog content, subdivided by type.
    - `blog/`: General articles and technical posts.
    - `weekly-victories/`: Weekly reflection posts, dated on the Friday the week ends on.
- `_layouts/`: Jekyll templates.
    - `default.html`: The main wrapper for all pages, including all CSS.
    - `post.html`: Template specifically for blog posts.
- `_data/currently_reading.json`: Books shown on the Now page, written by the Goodreads sync.
- `imgs/`: Post-specific images, organized into subdirectories named after the post date and slug (e.g., `imgs/2026-09-26-hello-world/`).
- Root Markdown files: Main site pages (`index.md`, `about.md`, `awards.md`, `blog.md`, `build.md`, `now.md`, `publications.md`, `weekly-victories.md`).
- `misc/create_post.py`: Script for creating new posts.
- `scripts/`: Automation run by GitHub Actions.
- `skills/weekly-victories/`: Agent skill and scripts for filling weekly victories from X.

There is no `_config.yml`; the site relies on GitHub Pages' Jekyll defaults.

## Currently reading

`scripts/sync_currently_reading.py` writes `_data/currently_reading.json` from the Goodreads currently-reading RSS feed. GitHub Actions runs it daily (`.github/workflows/sync-currently-reading.yml`).

The script defaults to the public feed for goodreads.com/rubai (user id 72897267). If the profile is ever made private, store the keyed RSS URL from the currently-reading shelf page (My Books → currently-reading → RSS at the bottom) as the repository secret `GOODREADS_RSS_URL`; it overrides the default.

## Weekly victories from time-lapses

`skills/weekly-victories/` is an agent skill whose script `skills/weekly-victories/scripts/build_weekly_victories.py` fills the week's `_posts/weekly-victories/` post from daily time-lapse posts on X. It searches @rubaitf by default (`DEFAULT_HANDLE` in the script; override with `X_HANDLE` or `--handle`). By default it runs the Grok Build CLI headlessly with the local `grok login` session (no API key); `skills/weekly-victories/scripts/install_schedule.sh` schedules it on rubai's machine every Sunday morning. Read `skills/weekly-victories/SKILL.md` before touching weekly victories.

## Development Workflows

### Creating New Content

Use the `misc/create_post.py` script to generate new post files with the correct front matter (run from repo root).

- **Blog Post:**

    ```bash
    python3 misc/create_post.py my-post-slug
    ```

    Creates `_posts/blog/YYYY-MM-DD-my-post-slug.md`.

- **Weekly Victory Post:**
    ```bash
    python3 misc/create_post.py w
    ```
    Creates `_posts/weekly-victories/YYYY-MM-DD-weekly-victories.md` dated the coming Friday.
