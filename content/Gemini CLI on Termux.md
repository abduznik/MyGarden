This procedure is rather easy to do but very effective for work and usage, you can install termux via the site F-DROID
[Download Termux Here](https://f-droid.org/en/packages/com.termux/)
and afterwards you can follow a few easy steps:
1. After installing make sure termux repos are set up properly with
```bash
termux-change-repo
```
2. after that, make sure your storage is also up to date with
```bash
termux-setup-storage
```
3. once you're done with that, make sure you install the NODEJS package as it is required to work with Gemini CLI
```bash
pkg install nodejs
```
4. finally, install Gemini CLI
```bash 
npm install -g @google/gemini-cli
```
Once you've finished you can easily open the CLI by writing in termux 
```bash
Gemini --debug
```
This way, you can enter the first time to Gemini in debug mode which will let you copy a login link to login into your Google account. you might also need to write 
```bash
/auth
```
to get the link, after that though, you wont be needing to do this again!

![[gemini_example.jpg]]
# Commands used in this post:

```bash
termux-change-repo
```

```bash
termux-setup-storage
```

```bash
pkg install nodejs
```

```bash
npm install -g @google/gemini-cli
```

```bash
gemini --debug
```

```bash
gemini
```