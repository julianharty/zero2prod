# From Zero to Production in Rust JH edition
## Context
This is is my edition of the material in the From Zero to Production in Rust book. I'm building on and adapting that material e.g. to test GitHub Actions locally on a mac using ACT.

## Adaptions
I'm mainly using macOS and therefore following guides and examples for this operating system. `rustup` was installed directly as was `homebrew`. 

Homebrew was used to install:
these packages
```aiignore bash
act llvm tree
```
- <https://nektosact.com/installation/homebrew.html>

and these casks
```aiignore bash
docker-desktop
```

I found <https://www.cprime.com/resources/blog/docker-for-mac-with-homebrew-a-step-by-step-tutorial/> helpful but still had to extricate myself from Docker Desktop wanting to install Rosetta etc.

### Nekos ACT
Context: I want to run webdriver.io tests for a codebase with Tauri v2 and Rust that needs to run with GitHub provided compute using GitHub Actions.
[Nekos ACT](https://nektosact.com/introduction.html) enables GitHub actions to be run locally. Note: their standard containers do not seem to include Rust development tools. See below for the fix that worked for me.


```aiignore bash
act push -P macos-latest=-self-hosted -P ubuntu-latest=ghcr.io/catthehacker/ubuntu:rust-latest    --container-architecture linux/amd64 --verbose
```
Thank you very much to <https://github.com/nektos/act/discussions/2386#discussioncomment-9980043> for the nub of this command i.e. `rust-latest`.

Further reading:
- <https://www.freecodecamp.org/news/how-to-run-github-actions-locally/> A good overview of using `act` generally.
- <https://jimbobbennett.dev/blogs/build-github-actions-faster-with-act/> Practical experiences of using `act`.
- <https://github.com/nektos/act/issues/107#issuecomment-1957722088> which helped me get unstuck after I'd picked the default micro-sized docker image and couldn't find a way to replace it.
- <https://nektosact.com/usage/runners.html#:~:text=act%20%2DP%20macos%2Dlatest=%2Dself%2Dhosted> reminded me of what I'd forgotten about running `act` on macOS i.e. `act -P macos-latest=-self-hosted`.
- <https://github.com/nektos/act/issues/1960> Rust isn't available in the full ubuntu image (but should be).
