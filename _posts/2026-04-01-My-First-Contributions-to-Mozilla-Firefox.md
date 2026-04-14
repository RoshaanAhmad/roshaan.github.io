---
title: 'My First Contributions to Mozilla Firefox: Setup, Fixes, and the Lessons I Learned'
date: 2026-04-01
permalink: /posts/2026/04/My-First-Contributions-to-Mozilla-Firefox/
tags:
  - Mozilla Firefox
  - Open-Source
  - Outreachy
---

# My First Contributions to Mozilla Firefox: Setup, Fixes, and the Lessons I Learned

Contributing to **Mozilla Firefox** has been one of the most valuable experiences in my journey as a developer. It gave me firsthand exposure to how a large-scale, production-grade open-source project is structured, maintained, and collaboratively improved by contributors around the world.

This blog documents my experience setting up the Firefox codebase locally, understanding its architecture, and contributing multiple frontend fixes as part of my open-source journey.

---

## Setting Up Firefox Locally

Setting up Firefox locally was one of the most challenging yet educational parts of my journey. Unlike smaller projects, Firefox is a massive codebase with many dependencies, build tools, and platform-specific configurations.

I followed the official [Firefox build documentation for Linux](https://firefox-source-docs.mozilla.org/setup/linux_build.html) and carefully prepared my environment step by step.

### 1. System Preparation

To build Firefox, it is necessary to have Python version 3.9 or later installed. Python 2 is no longer required for building Firefox, although it is still needed for running some types of tests. Additionally, you may need Python development files to install certain pip packages.

You should be able to install Python and Git using your system package manager:

* For Debian-based Linux (such as Ubuntu):
  ```sudo apt update && sudo apt install curl python3 python3-venv git```

* For Fedora Linux:
  ```sudo dnf install python3 git```

---

### 2. Bootstrap a Copy of the Firefox Source Code

The second step is to bootstrap a copy of the Firefox source code.

Now that your system is ready, you can download the source code and allow Firefox to automatically fetch the dependencies it needs. The following command will download a large amount of data (including years of Firefox history) and guide you through an interactive setup process.

Firefox provides a bootstrap script that simplifies environment setup. Running this script helped configure most dependencies automatically and guided me through the required installations.

This step significantly reduced manual setup complexity and ensured my environment matched the expected build configuration.

```
curl -LO https://raw.githubusercontent.com/mozilla-firefox/firefox/refs/heads/main/python/mozboot/bin/bootstrap.py

python3 bootstrap.py
```

#### Choosing a Build Type

If you aren’t modifying the Firefox backend, you can select one of the [Artifact Mode](https://firefox-source-docs.mozilla.org/contributing/build/artifact_builds.html#understanding-artifact-builds) options. If you are building Firefox for Android, you should refer to the [GeckoView Contributor Guide](https://firefox-source-docs.mozilla.org/mobile/android/geckoview/contributor/geckoview-quick-start.html#geckoview-contributor-guide).

---

### 3. Building Firefox

After setup, and once your system is bootstrapped, you should be able to build Firefox.

I built Firefox locally using the following commands:

```bash
cd firefox
git pull
./mach build
```

* The first build took a significant amount of time due to compiling the entire codebase.
* Subsequent builds were faster using incremental compilation.
* Once the build completed successfully, I was able to run a local version of Firefox.

🎉 Congratulations! You’ve built your own Firefox. You should see a success message in your terminal after the build completes.

You can now run your locally built browser using: ```./mach run```

😎 Seeing the browser launch from my own build was a very rewarding moment and gave me the confidence to start contributing.

**Note:** If you encounter build errors, refer to the [official troubleshooting documentation](https://firefox-source-docs.mozilla.org/setup/linux_build.html#troubleshooting).

---

## The Contribution Phase

Now the fun begins — time to start contributing!

At this stage, you should join [Matrix](https://chat.mozilla.org/) and introduce yourself in the [Introduction Channel](https://chat.mozilla.org/#/room/#introduction:mozilla.org).

### 1. Start Looking for Beginner-Friendly Bugs

You can search for beginner-friendly bugs on the [contribute](https://codetribute.mozilla.org/) page based on your tech stack. After finding a bug, create an account on [Bugzilla](https://bugzilla.mozilla.org/) and request a mentor to assign it to you. Once assigned, you can begin working on it.

---

### 2. Understanding the Large Codebase

One of the key lessons I learned is that large open-source projects are not just about writing code—they are about understanding patterns, conventions, and existing architecture before making changes.

Your next step is to familiarize yourself with the codebase. Two tools that helped me significantly are:

* [**Searchfox**](https://searchfox.org/) – a source code indexing tool for Firefox
* [**Browser Toolbox**](https://firefox-source-docs.mozilla.org/devtools-user/browser_toolbox/index.html) – allows you to debug the browser’s internal JavaScript and UI

The Browser Toolbox works on the entire browser context, not just a single webpage, which makes it very powerful for debugging frontend issues.

**Note:** If you are unsure about what changes to make, use the *needinfo* feature on Bugzilla to ask your mentor for clarification.

---

### 3. Writing and Submitting a Patch

After identifying the files that need changes, follow this workflow:

#### Start from the main branch

```bash
git checkout main
git pull
```

#### Create a new branch for your bug

```bash
git checkout -b Bug-XXXXXXX
```

#### Make your changes and prepare to commit

#### Commit your changes

```bash
git add <file>
git commit -m "Bug XXXXXXX - Description of fix"
```

#### Submit to Phabricator

```bash
moz-phab submit --no-wip
```

---

## My Contributions to Firefox

After getting comfortable with the setup, I started working on small but meaningful issues. My goal was to begin with manageable tasks while learning the contribution workflow.

### 1. Add tab note background color for default light theme [D290018](https://github.com/mozilla-firefox/firefox/commit/6fcae532ae2d)

Contributed a UI improvement by adding a proper background color for tab notes in the default light theme.
This improved visual consistency and readability by ensuring tab notes remain distinguishable from the tab background.

---

### 2. Fix typo in OpenInTabsUtils.sys.mjs – confirmOpenInTabs() [D291855](https://github.com/mozilla-firefox/firefox/commit/0a0a5196de8e)

Fixed a typo in the `confirmOpenInTabs()` function, improving code clarity and maintainability.
Although a small change, it contributes to overall code quality in a commonly used utility module.

---

### 3. Fix splitter border lines and tab-screen corner issue in split view [D292101](https://github.com/mozilla-firefox/firefox/commit/b0c06ce109fb)

Resolved a UI rendering issue where splitter borders and tab corners were misaligned.
Tested across different window sizes and operating systems (Windows and Linux) to ensure consistent behavior.

---

## Challenges I Faced

Working on Firefox was not easy, especially as a first-time contributor to such a large codebase.

Some of the main challenges included:

* Setting up the build environment correctly
* Understanding a large and complex code structure
* Locating the correct files for specific UI components
* Ensuring changes did not introduce unintended side effects

Each challenge helped me improve my debugging skills and think more carefully before making changes.

---

## What I Learned

This experience taught me much more than just coding. I learned:

* How large-scale open-source projects are structured and maintained
* How to read and navigate unfamiliar codebases efficiently
* The importance of incremental changes and careful testing
* How to follow real-world contribution workflows
* How to communicate and collaborate as a contributor

Most importantly, I learned how to stay consistent and patient while working through uncertainty. Open source is not about immediate results—it is about persistence and continuous improvement.

---

## Final Thoughts

Contributing to Firefox has been one of the most valuable learning experiences in my journey so far. It gave me real exposure to professional open-source development and helped me understand what it means to work on software used by millions of people.

I am still at the beginning of my journey, but this experience has given me the confidence to continue contributing to impactful open-source projects.

---


