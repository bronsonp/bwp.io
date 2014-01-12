---
layout: post
title: "Emacs: interactive regexp search and replace across multiple files"
description: "How to use Emacs to search and replace with regular expressions across an entire project"
tags: [emacs]
---

Here's how to use Emacs to for an interactive search and replace across multiple files.

1. Open a `dired` buffer containing the files to be searched. An easy way to list files in all subdirectories is with `M-x find-dired`.
2. Mark the files that you want to search with `% m`.
3. Run the multi-file search and replace with `Q`. Press `y` to accept a replacement and `n` to skip it.
4. Afterwards, you need to save all the modified buffers. Open `ibuffer` mode with `M-x ibuffer` then press `* u` to mark unsaved buffers, and `S` to save them.
