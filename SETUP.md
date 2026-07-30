# Setup

## 1. Create the repo

Your GitHub profile README lives in a repo named exactly after your GitHub username.
If your username is `Astronomox`, the repo is `Astronomox/Astronomox`.

Create it (or replace the existing one), then push this folder's contents to it.

## 2. Generate the portrait

You need a good headshot photo. Side lighting works best (window at ~45 degrees).

```bash
pip install pillow numpy opencv-python-headless rembg onnxruntime
python3 scripts/make_portrait.py your-photo.png --preview
```

If the crop is off, pass `--crop left,top,right,bottom` (pixel coords).
Once it looks right:

```bash
python3 scripts/embed_portrait_font.py
```

This inlines JetBrains Mono into ascii.svg so spacing is correct everywhere.

## 3. First stats run

Generate the initial stat SVGs locally:

```bash
export GITHUB_TOKEN=ghp_your_personal_access_token
export GH_LOGIN=YourGitHubUsername
python3 scripts/generate_stats.py
```

You need a GitHub personal access token with `read:user` scope.
Create one at https://github.com/settings/tokens.

## 4. Push and enable the action

```bash
git add -A
git commit -m "init profile readme"
git push
```

The GitHub Action runs daily at 05:17 UTC and auto-commits updated SVGs.
You can also trigger it manually from the Actions tab > "refresh stats" > Run workflow.

## 5. Customize

- **Username**: `GH_LOGIN` in `generate_stats.py` defaults to `Astronomox`. The Action overrides this with `${{ github.repository_owner }}`, so it works automatically.
- **Links**: edit the link row in README.md.
- **About text**: edit the blockquote and paragraph under `hd-about.svg`.
- **Projects**: add/remove entries under `hd-projects.svg`.
- **Stack**: edit the `<samp>` line under `hd-stack.svg`.
- **Headings**: to rename a section, change the word in `generate_stats.py`'s heading list and update the README reference.
