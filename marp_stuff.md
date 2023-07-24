# MARP FAQ

- [What is Marp?](#WhatIsMarp)
- [How do you install Marp?](#InstalingMarp)
- [My Marp Workflow](#MarpCLIWorkflow)

---

# WhatIsMarp

| Marp (also known as the Markdown Presentation Ecosystem) provides an intuitive experience for creating beautiful slide decks. You only have to focus on writing your story in a Markdown document.

I use Marp instead of Powerpoint to create presenations I use in lectures, talks, and tutorials. If you're a coder or otherwise comfortable with creating documents with plaintext (especially Markdown), then this might be for you. However, for most people, using PowerPoint or some other presenetaiton software package will be faaar easier! An easy way to get started is to use Marp via [VSCode](https://code.visualstudio.com/) or [VSCodium](https://vscodium.com/), but I use Marp CLI with [PyCharm](https://www.jetbrains.com/pycharm/).

[More about Marp Here:](https://marp.app/)

---

# InstalingMarp

## Basic Setup

If you want to use Marp with [VSCode](https://code.visualstudio.com/) or [VSCodium](https://vscodium.com/), you can find it in the normal VSCode marketplace, e.g.:

[Marp for VS Code](https://marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode)

If you want to use Marp with another editor or IDE (I use [PyCharm](https://www.jetbrains.com/pycharm/) becasue I already use it frequently for Python development, otherwise I'd probably use [VSCodium](https://vscodium.com/). This means that I use use Marp-CLI (i.e., the commandline interface). You can learn more more here:

[Marp-CLI](https://github.com/marp-team/marp-cli)

By far the easiest way to install Marp is to use one of the standalone binaries from the marp-cli [Releases Page].

I recommend putting the resulting Marp executable somewhere in your system Path. 

NOTE that if you instead use pip or npx to install Marp, it may already be on your path. Use the [Marp-CLI](https://github.com/marp-team/marp-cli) instructions for info on how to get to the point where you can run Marp from anywhere on your system.

## Setup Chrome Browser for Rendering

The Marp-CLI page discusses how to make sure you have chrome setup for rendering. On [Ubuntu Linux](https://ubuntu.com/download/desktop) (actually, I use [Pop!_OS](https://pop.system76.com/), an OS by system76 based on Ubuntu), I used these instructions:

```bash
sudo add-apt-repository ppa:savoury1/chromium
sudo apt update
sudo apt install chromium-browser
export CHROME_PATH=/usr/bin/chromium-browser
```

---

# MarpCLIWorkflow

## Setup

### For each new slideshow:

- create a new folder to hold the slideshow
- create 2 subfloders, "images" and "media"
- create a markdown file called "slides.md"
- create a batch file called dev.sh (mac or linux, dev.bat on windows??) and make it executable.
- create a batch file called make_pdf.sh (mak or linux, make_pdf.sh on windows??) and make it executable.

### Boilerplate for the top of slides.md

```markdown
---
marp: true
theme: gaia  # default, uncover, gaia
class: invert   # invert for dark mode of any theme
math: mathjax
footer: "(c) 2023 Travis L. Seymour, PhD"
html: true
size: 4:3 # 16:9 4:3 etc.
style: |
  .two_columns {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1rem;
  }

  .two_columns_60_40 {
    display: grid;
    grid-template-columns: 60% 40%;
    gap: 1rem;
  }

  .two_columns_70_30 {
    display: grid;
    grid-template-columns: 70% 30%;
    gap: 1rem;
  }

  .three_columns {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    gap: 1rem;
  }

  /* 
  make sure there are spaces above and below the content, e.g.:
  <div class="centerit">
  
  [w:480px]('./images/my_image.png')
  
  </div>
  */
  .centerit {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }
  
  /* small font bulleted list */
  .small_list ul {
    font-size: 22px;
  }

  /* Watermark (after=off, before=on)*/
  section::after {
    position: absolute;
    display: flex;
  
    /* Copyright text */
    content: ".";  /*  @@@@@@@@@@ You could put copyright info here, or use image below  @@@@@@@@@@@ */
    font-size: 20px;
    color: #C0C0C0;
    padding-left: 1980px;
    align-items: center;
  
    /* Position and size */
    left: 30px;
    bottom: 200px;
    height: 350px;
  
    /* Watermark image no-repeat or repeat */
    /* THIS WILL ONLY SHOW UP IF YOU SET "section::before" above. to disble, use "section::after" */
    background: url("./images/watermark2.png") repeat;   /*  @@@@@@@@@@ I have my copyright info in this watermark image  @@@@@@@@@@@ */
    opacity: 0.4;
  
    /* Allow to control elements under the wa termark */
    pointer-events: none;
  }
---
```

### Contents of dev.sh

NOTE: This may need to be adjusted for Windows.
NOTE: This may need to be adjusted on Macos if you are not using bash.

```bash
#!/bin/bash
marp -w -p --html slides.md
```


### Contents of make_pdf.sh

NOTE: This may need to be adjusted for Windows.
NOTE: This may need to be adjusted on Macos if you are not using bash.

```bash
#!/bin/bash
marp -w -p --html slides.md
```
