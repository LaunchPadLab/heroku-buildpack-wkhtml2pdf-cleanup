# Heroku Buildpack: wkhtmltopdf Cleanup

This buildpack cleans up unnecessary wkhtmltopdf binaries from the `wkhtmltopdf-binary` gem to reduce slug size on Heroku.

## What it does

The buildpack searches for wkhtmltopdf binary directories in your bundled gems and removes all compressed binary files except the one for Ubuntu 22.04 AMD64 (`*22.04_amd64*`), which is typically what you need on Heroku's runtime.

## Usage

Add this buildpack to your Heroku app after your main buildpacks (like Ruby or Node.js):

```bash
heroku buildpacks:add https://github.com/yourusername/heroku-buildpack-wkhtml2pdf-cleanup.git
```

Or add it to your `app.json`:

```json
{
  "buildpacks": [
    { "url": "heroku/ruby" },
    { "url": "https://github.com/yourusername/heroku-buildpack-wkhtml2pdf-cleanup.git" }
  ]
}
```

## Why use this?

The `wkhtmltopdf-binary` gem includes binary files for multiple operating systems, which can significantly increase your slug size. This buildpack helps keep only the binary you actually need on Heroku's platform.

## Requirements

This buildpack should be run after your main buildpack that installs gems (e.g., after the Ruby buildpack). 