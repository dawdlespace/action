# dawdle.space GitHub Action

Upload a directory to [dawdle.space](https://dawdle.space).

## Usage

Add the site API key to your repository as a secret, for example
`DAWDLE_API_KEY`, and use the action after building the site:

```yaml
name: Deploy

on:
  push:
    branches: [main]

permissions:
  contents: read

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Build site
        run: npm run build

      - name: Upload to Dawdle
        uses: dawdlespace/action@v1
        with:
          site-id: my-site-id
          api-key: ${{ secrets.DAWDLE_API_KEY }}
          path: dist
          replace: true
```

## Inputs

| Input     | Required | Default | Description                                            |
| --------- | -------- | ------- | ------------------------------------------------------ |
| `site-id` | Yes      |         | Dawdle site ID                                         |
| `api-key` | Yes      |         | Dawdle site API key                                    |
| `path`    | Yes      |         | Directory to upload                                    |
| `replace` | No       | `true`  | Replace all site files. Set to `false` to merge files. |

The action supports GitHub-hosted Linux and macOS runners.

## API key security

Store the API key as a GitHub Actions secret and pass it using the `secrets`
context. Do not put the key directly in the workflow file. Use a key for the
target site and rotate it if it is exposed.
