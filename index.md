# Git 原始碼檔案版本控管工具簡介

- Author: Pony L.
- Create At: 2021-11-23
- Contact: ponylin1985@gmail.com

----------------------

## Git 簡介

- [git wiki](https://zh.wikipedia.org/wiki/Git)
- [什麼是 Git？為什麼要學習它？](https://gitbook.tw/chapters/introduction/what-is-git.html)
- [Git簡介](https://medium.com/hjorus-sharing/git簡介-cbd9b6e9edb4)

----------------------

## 安裝 Git CLI

- 基本上都是需要安裝 git CLI (Command-line interface)，其餘 Git GUI 客戶端工具背後實際都是使用 Git CLI，所以 Git CLI 是必要安裝工具。
- 只是也許某修 Git GUI 工具在安裝過程中，會順便背地裡把 Git CLI 安裝完成。
- 保證永久不用錢!

### Windows

- [安裝在 Windows 作業系統](https://gitbook.tw/chapters/environment/install-git-in-windows.html)
- [Git 介紹與在Windows系統下安裝](https://progressbar.tw/posts/1)


### macOS

- 建議依照此篇安裝，使用 homebrew 安裝，不要安裝 XCode 這種垃圾。
  - [安裝在 Mac OSX 作業系統](https://gitbook.tw/chapters/environment/install-git-in-mac.html)
  - [macOS 用 Homebrew 安裝 git 指令](https://shengyu7697.github.io/mac-git/)
- 其他安裝方式，譬如用 XCode 這種垃圾或其他 GUI Tool
  - [開始 - Git 安裝教學](https://git-scm.com/book/zh-tw/v2/開始-Git-安裝教學)

## Linux

#### 大便派 (Debian、Ubuntu 或醜醜的 Mint)

- [Ubuntu環境下，如何安裝git](http://samwhelp.github.io/blog/read/git/install/)
- [How To Install Git on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-git-on-ubuntu-20-04)

#### 小紅帽 or 妃妃 (Red Hat、CentOS、Fedora)

- [How To Install Git on CentOS 7](https://www.digitalocean.com/community/tutorials/how-to-install-git-on-centos-7)
- [How to Install & Configure Git on Fedora 35](https://www.linuxcapable.com/how-to-install-configure-git-on-fedora-35/)
- [How to Install Git and Setup Git Account in RHEL, CentOS and Fedora](https://www.tecmint.com/install-git-centos-fedora-redhat/)

### Git GUI Tools 參考

- [SourceTree](https://www.sourcetreeapp.com) - 有免費版，不用錢。
- [SmartGit](https://www.syntevo.com/smartgit/) - 有免費版，也有付費版。
- [GitKraken](https://www.gitkraken.com/) - 簡稱「海怪」，非常強大的 Git GUI 工具，可能是使用 Git GUI 做得最完善的一個工具，要 Licence 購買授權。
- [TortoiseGit](https://tortoisegit.org) - 適合 windows 檔案總管上的 Git GUI Shell 工具，有免費版，不用錢。
- [Git on Visual Studio](https://www.youtube.com/watch?v=jUiuIAZt6Dw&ab_channel=TechGenix) - 在 Visual Studio 上內建的 Git GUI 管理工具，算是堪用。
- [GitLens for VS Code Git Extensions](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens) - 在 VS Code 上其他 Git 的 extension 都不用裝，**只需要裝這個就可以了，因為這是公認最強大的 git extension，沒有之一!**

----------------------

## 目錄

- [Git 組態設定 & Git 儲存倉儲 [Git Config & Git Init]](./git-configuration-init/git-config-init.md)
- [Git 狀態 & commit 與 undo 操作 [Git Status & Git Commit & Git Undo]](./git-status/git-status-commit-undo.md)
- [Git 分支與合併 [Git Branch & Git Merge]](./git-branch-merge/git-branch-merge.md)
- [Git 遠端協作指令與設定 [Git Remote]](./git-remote/git-remote.md)
- [GitLab 新增遠端倉儲 [GitLab Repo, GitLab SSH Key, Git Clone]](./git-remote/gitlab/gitlab-new-repo.md) -
  對 Dynasafe AI 同事補充: 使用 ssh 是最安全最建議的遠端存取方式，但由於 ssh key 金鑰需要管理，**並且現階段公司內部的 Azure DevOps Git Repo 使用的是 http basic 身分驗證 (就是當你要存取時，請你直接輸入你的 AD 帳密!)**，因此 ssh 的手法建議自行看過大致理解就好，有興趣多了解並且設置 ssh config 設定檔案同事歡迎隨時找 [Pony (私人 Email)](ponylin1985@gmail.com) 或 [Pony Lin (Dynasafe Email)](pony.lin@dynasafe.com.tw)。
- [Git 遠端協作指定: Git Fetch, Git Pull & Git Push](./git-remote/git-fetch-pull-push.md)
- [Git 常見分支用途與意義 [Git Branches Meaning]](./git-branch-merge/git-branches-meaning.md)
- [GitLab 新增 Merge Request 與合併操作](./git-remote/gitlab/gitlab-merge-request.md)
- [GitFlow 簡介與說明](./git-branch-merge/gitflow.md)
- [GitFlow 分支圖](./git-remote/gitlab/git-flow.drawio) 此為 .drawio xml 檔案，請直接於 drawio 網站上開起，或在 VS Code 上安裝 drawio extension 之後，也可以在 local 上預覽。
  - [基礎流程 GitFlow 流程圖說明](./git-remote/gitlab/git-flow-gitflow.jpg)
  - [進階流程 GitGlow 流程圖說明](./git-remote/gitlab/git-flow-better-gitflow-with-ci_cd.jpg)
