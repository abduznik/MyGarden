![]( https://youtu.be/6s6DT1yN4dw?si=pFphzzIx5smJr6QG)
# Quick Grabs

```bash
npx quartz sync
```

```bash
npx quartz build --serve
```

# Main


```timestamp 
 04:24
 ```
Clone the repo and cd into it, initialize with npm and then create an empty project with quartz
```bash
git clone https://github.com/jackyzha0/quartz.git my-notes
cd my-notes
npm i
npm quartz create

x Empty Quartz
- Copy an existing folder
- Symlink an existing folder

Choose how Quartz should resolve links in your content. You can change this later in `quartz.config.ts`.
- Treat links as absolute path
x Treat links as shortest path
- Treat links as relative paths
```

<div style="page-break-after: always;"></div>


```timestamp 
 07:15
 ```
You can create a repo from zero or simply fork the existing quartz4 by pressing the button below

[Github Quartz Site](https://github.com/jackyzha0/quartz)

After you got to the site press on ***Fork*** or by pressing the button below

[Fork Site](https://github.com/jackyzha0/quartz/fork)

After you forked it simply clone it using **GIT**
```bash
git clone https://github.com/your-username/my-fork
```

```timestamp 
 08:51
 ```
You can easily afterwards take the fork you made and cloned, open it via obsidian and let it index, afterwards you can edit freely inside the **contents** folder!

```timestamp 
 13:16
 ```
To sync your content simply write the following command in the terminal:
```bash
npx quartz sync
```

```timestamp 
 13:56
 ```
To run the quartz server locally use:
```bash
npx quartz build --serve
```

<div style="page-break-after: always;"></div>


```timestamp 
 15:00
 ```
To publish you must first add the deploy.yml file, you can by making this new file at **.github/workflows** inside there paste this deploy code.

```yaml
name: Deploy Quartz site to GitHub Pages

on:
  push:
    branches:
      - v4

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0 # Fetch all history for git info
      - uses: actions/setup-node@v4
        with:
          node-version: 22
      - name: Install Dependencies
        run: npm ci
      - name: Build Quartz
        run: npx quartz build
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: public

  deploy:
    needs: build
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

```timestamp 
 15:31
 ```
Afterwards go to your repo on github, settings and then to pages, inside there choose GITHUB ACTIONS

Now if you want to always refresh your site simply use:
```bash
npx quartz sync
```