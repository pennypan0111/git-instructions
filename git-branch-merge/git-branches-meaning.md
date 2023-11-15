# Git Branches (Git 分支名稱主要的意義)。

- git 版本控管原本就被設計為分散式，並且支援多人協同開發情況下，多人使用的版本控管工具，因此 git branch 每一條分支的意義相當重要。
- 在 git 版本控管中，任何一個 git repo 基本上沒有 branch 分支數量的上限，正常情況下，任意兩條 branch 也可以進行 merge 合併的操作。

## 常見的 git branch 用途與意義說明。

- 但在 git repository 中通常會有以下的 branch，代表以下的意義。

  - `master`

    - 如果是先在 local 使用 `git init` 建立 local git repo，通常預設就會有這一條 `master` 分支。
    - 通常 `master` 代表是這個 git repo 的 **主要分支也是預設分支**，理論上，所有其他的 branch 都會直接或間接地從這條 `master` checkout 出去新的分支。
    - 如果是使用 `git clone` 複製遠端的分支建立 local git repo，有可能遠端的 git repo 設定 default branch 不是 `master`，而是其他的 branch。
      - 如果是以上情況，當 `git clone` 成功之後，預設在 local checkout 就會是遠端 repo 設定的那一條 defautl branch (譬如可能是 **master 或 develop** branch)。
      - 遠端的 remote repo，其實也可以額外設定「哪一些」branch 是屬於 protected branch，代表這種 branch，是不允許一般的 member 直接使用 `git push` 將 local 送出到 remote repo 中，一般情況下，default branch 都會設定為 protected branch。

    - `master` branch 代表最重要的意義為: $`\textcolor{red}{\text{通常代表已經經過某種測試或確認，較為穩定版本的 commit，則會允許 merge 到 master 中!}}`$
    - 能 merge 到 `master` 的 commit 通常會有以下幾種意義:

      - 確認可以進行 **發布或發行 (Release or Publish) ** 的穩定版本，或者已經被發布或發行 (Released or Published) 的穩定版本 (通常看團隊跑哪一種 git flow)。
      - 確認可以進行 佈署 (deployment) 的穩定版本，或者已經被佈署到 **正式區 (production)** 完成的穩定版本。
      - 如果是一個 open source 的 repo，通常用戶如果回報一個 bug issue，可以從 `master` 中找到 issue 的檔案、段落與問題，簡單的說，就是可以在 `master` 分支上發現這個 issue。
      - 如果 `master` 的版本可以對應一個 **環境**，通常這個環境別會是 $`\textcolor{red}{\text{正式區 (production)}}`$，或代表一個 **主要使用或相對穩定的環境**。
        - _(有時候依照團隊不同的定義，`master` 也可能代表對應到不同的環境別。)_

  - `develop`

    - 通常代表一個 **需求開發完成而且經過某種程度測試，相對穩定的版本** 的 branch 。
    - 通常 `develop` 的 commit 會比 `master` 相對更新，因為持續會有新的功能完成之後，被 merge 到 `develop` branch 來。
    - 通常 `develop` 也可能代表
      - **準備要被部署到「某一個」開發測試時期的環境**，進行測試的 branch。
      - **已經被部署到「某一個」開發測試時期的環境**，正在執行測試，或已經被測試完成的 branch。
      - _(實際為以上哪一種情況，可能會依照不同團隊跑的 git flow 流程不同而有不同。)_

  - `feature/XXX`

    - 通常代表一個新的需求，已經被確認要開發之後，用來開發這一個新需求的 branch。
    - 其中 `{XXX}` branch name 建議盡量稍微能描述出主要需求意思，或者直接給相關 Ticket System (譬如: Jira 或 Azure DevOps) 的 Ticket No，譬如以下。
      
      - `feature/HK-market-for-eStock-trader`
      - `feature/ER-10034`

    - 通常 `feature/XXX` 會從 `develop` checkout 建立出來，但也有可能是從特定的 git tag 上 checkout 建立出來。
    - 當 `feature/XXX` 上的新需求或新功能，已經開發得差不多完成之後，可能會 merge 回 `develop` branch。

  - `bugfix/XXX`

    - 通常代表一個 bug 修正的分支，代表系統被發現一個已經確認要修正的 bug，專門建立一條獨立的 branch 用來修正此 bug，通常跟 `feature/XXX` 分支差不多，只是這種是專門用來改正 bug 的分支。
    - 通常 `bugfix/XXX` 會從 `develop` checkout 建立出來，但也有可能是從特定的 git tag 上 checkout 建立出來。
    - 當 `bugfix/XXX` 上的 bug，已經修正完成之後，可能會 merge 回 `develop` branch。

  - `hotfix/XXX` 

    - 通常代表 **正式區環境 (production)** 上被發現 bug 或 issue，需要緊急對正式區環境進行修正處理的 branch 分支。
    - 通常 $`\textcolor{red}{\text{可能會從}}`$ `master` $`\textcolor{red}{\text{checkout 建立出來}}`$，或由 $`\textcolor{red}{\text{可以代表目前正式區環境的 branch 或 tag }}`$ checkout 建立出 `hotfix/XXX` 分支。
    - 通常完成對正式區的 hotfix 之後，多數的團隊的 git flow 流程可能會包含 `git cherry-pick` 回到 `master` 或 `develop` 分支的操作，或其他後續操作。

  - `release/XXX` 
  - `build/XXX` 
  - `deploy/XXX`

    - 這種通常代表該團隊，對於某一次特定版本的發行、建置或部署的 branch。
    - `{XXX}` 有可能代表一個版本號，或是 `git tag` 版本號。

----------------------

- Reference

  - [Git Workflow — 善用Git分支強化專案的開發流程](https://medium.com/act-as-a-software-engineer/git-workflow-善用git分支強化專案的開發流程-c7af53da7b6e)
  - [簡述分支](https://git-scm.com/book/zh-tw/v2/使用-Git-分支-簡述分支)

----------------------

### [回到目錄](../index.md#目錄)

