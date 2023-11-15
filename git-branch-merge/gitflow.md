# Git Flow

- 簡言之，就是需要在一個 git repo 中，先把多人協同合作時，把 git 操作的流程與規範事先定義出來，讓所有參與這個 repo 的人員可以遵循此規範，避免產生問題。
- git 發展至今，目前業界已經很很多種普遍的 **gitflow**，包含原本的 gitflow，以及後來的 GitHub Flow、GitLab Flow ... 等等。
- gitflow 透過 `git flow init` 指令初始化，也可以透過 git GUI tool 工具初始化，也可以只是團隊成員共同定義好的 flow 流程規範，然後大家手動操作時遵循這個規範。
  - 透過 `git flow init` 或工具初始化 gitflow，主要會生效於 local repo 中。
  - 在每一次操作 git 指令動作時，會依照 gitflow 預設的流程，自動化產生一些行為，譬如: 當 `feature` branch 或 `hotfix` branch merge 回到 `develop` 之後，預設會自動把 `feature` 或 `hotfix` branch 刪除掉。
  - 其實不一定非要使用 gitflow 自動化腳本，蠻多團隊也不一定有使用。

- gitflow 實際上，**是可以依照每個團隊，搭配不同的工具，不同的團隊操作習慣，以及特定需求，制定出客製化的 gitflow 操作流程，而且也可以腳本化與自動化**。

----------------------

## GitFlow

- References

  - [Git flow 開發流程](https://ihower.tw/blog/archives/5140)
  - [Git Flow 是什麼？為什麼需要這種東西？](https://gitbook.tw/chapters/gitflow/why-need-git-flow.html)
  - [使用 Git Flow](https://gitbook.tw/chapters/gitflow/using-git-flow.html)
  - [Git Workflow — 善用Git分支強化專案的開發流程](https://medium.com/act-as-a-software-engineer/git-workflow-善用git分支強化專案的開發流程-c7af53da7b6e)

----------------------

## GitHub flow

- References

  - [GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow)
  - [讓我們來了解 GitHub Flow 吧！](https://medium.com/@trylovetom/讓我們來了解-github-flow-吧-4144caf1f1bf)

----------------------

## GitLab flow

- References

  - [Introduction to GitLab Flow](https://docs.gitlab.com/ee/topics/gitlab_flow.html)
  - [GIT 團隊協作 談 流程管理 03 GitLab Flow](https://ithelp.ithome.com.tw/articles/10228195)
  - [What Is GitLab Workflow | GitLab Flow | GitLab Tutorial For Beginners | Part III](https://www.youtube.com/watch?v=7lgGEXpsflI)

----------------------

- References

  - [三種版控流程 [gitflow] vs [github flow] vs [gitlab flow]](https://medium.com/@lf2lf2111/三種版控流程-29c82f5d4469)
  - [GitHub Flow 及 Git Flow 流程使用時機](https://blog.wu-boy.com/2017/12/github-flow-vs-git-flow/)
  - [一文弄懂 Gitflow、Github flow、Gitlab flow 的工作流](https://cloud.tencent.com/developer/article/1646937)

----------------------

### [回到目錄](../index.md#目錄)
