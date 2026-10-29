# Manewax — Static HTML Site

A plain HTML/CSS version of the Manewax storefront, with no JavaScript and no build step. It's meant to be hosted from an S3 bucket.

## Pages

| Path | File |
| --- | --- |
| `/` | `index.html` |
| `/info.html` | `info.html` |
| any missing path | `error.html` |

Products are listed on the home page. The site does not link to third-party websites.

## Layout

```
assets/css/site.css   Compiled Tailwind stylesheet
assets/media/         Font files referenced by site.css
images/               Product and Information-page photos
manewax-logo.png, favicon*
```

To edit a product, change its card in `index.html`. The styling uses Tailwind utility classes that already exist in `site.css`. A class that isn't already used somewhere on the site won't have any styles.

## Preview locally

Preview through a local web server instead of opening the files directly:

```bash
python3 -m http.server 8000
# open http://localhost:8000/
```

## Deploy to S3

1. Turn on **Static website hosting** for the bucket, with index document `index.html` and error document `error.html`.
2. Upload:

```bash
aws s3 sync . s3://YOUR_BUCKET --delete \
  --exclude ".git/*" --exclude ".github/*" --exclude "README.md" --exclude ".DS_Store"
```

3. If CloudFront is in front of the bucket, invalidate `/*` after uploading.
