# Git Branch & Git Merge

- 在 git 版本控管中，允許建立一個或多個 branch (分支)，獨立進行版本控管。
- 基本上 git repo 的預設分支為 `master`，在 GitLab 上可以額外設定 git repo 的 default branch。
- 在同一個 git repo 中允許任意兩條 branch 進行合併 (merge) 的操作，因為以結果而言，實際上的行爲是把兩條 branch 各個最後一個 commit 的檔案差異進行合併。

## Git Branch

- `git branch`

  - 列出目前本地端 local 所有的 branch。
  - 會顯示出目前 HEAD 所在的 branch。

    ```
      develop
    * feature/dotnet6-upgrade
      feature/test-ci-pipeline
      master
      release/dotnet-standard2.0
    ```

- `git branch -r`

  - 列出目前遠端 remote 所有 branch。

    $`\textcolor{red}{\text{(因為 HEAD 目前沒有指向任何一個遠端分支，因此沒有 * 符號提示當前所在的 branch!)}}`$

    ```
    origin/develop
    origin/feature/ServiceActionLocator
    origin/feature/dotnet6-upgrade
    origin/feature/test-ci-pipeline
    origin/master
    origin/release/dotnet-standard2.0
    ```

- `git branch -a`

  - 列出 git repo 中目前所有的 branch，如果 git repo 有 upstream，會列出包括 remote 遠端的 branch。
  - 以下輸出中，以 `remotes` 開頭前綴的即為遠端分支，遠端分支顯示格式為: `remotes/{remote_name}/{branch_name}`

    ```
      develop
    * feature/dotnet6-upgrade
      feature/test-ci-pipeline
      master
      release/dotnet-standard2.0
      remotes/origin/develop
      remotes/origin/feature/ServiceActionLocator
      remotes/origin/feature/dotnet6-upgrade
      remotes/origin/feature/test-ci-pipeline
      remotes/origin/master
      remotes/origin/release/dotnet-standard2.0
    ```

- `git branch -u {remote_name}/{branch_name}`

  - 指定目前 loacl branch 對應 remote 的上游 branch，如果想要指定其他的 local branch 可以執行 `git branch -u {local_branch_name} {remote_name}/{remote_branch_name}`。
  - 先解釋一下對於 git 來說 upstream 的意思。
    - upstream，意指「上游」，代表一條 local branch 應該要對應到「哪一個」遠端的 repo 中的哪一條 branch?

  - 如果 local 的 git repo 設定有多個 git remote repo 的情況，可以用此指令，指定目前 local branch 的 upstream 為哪一個 remote 的哪一條 branch。
  - 指定了之後，`git fetch`、`git pull` 或 `git push` 指令，都會對這個 remote repo 的 branch 進行操作。

    - `remote_name`: 遠端 repo 名稱，可以使用 `git remote -v` 查看目前有哪一些 remote。
    - `branch_name`: 遠端分支的名稱。

- `git branch {new_branch_name}`

  - 在 local 的 git repo 建立一個新的 branch，建立完成之後 $`\textcolor{red}{\text{不會}}`$ 自動切換到新建立的 branch。

- `git branch -m {old_branch_name} {new_branch_name}`

  - 對 local 的 git repo 的某一個 branch 重新命名。
  - 如果改為 `git branch -M {old_branch_name} {new_branch_name}` 則會強制重新命名。

- `git branch -d {branch_name}`

  - 刪除 local 的 git repo 的 branch。
  - 如果改為 `git branch -D {branch_name}` 則會強制進行刪除。

- `git push {remote_name} -d {remote_branch_name}`

  - 刪除遠端 remote 的 branch。

- `git checkout -b {new_branch_name}`

  - 從當前的 branch 中最後一個 commit 建立一個新的 local branch，建立完成之後，$`\textcolor{red}{\text{會直接自動切換過去新建立的 local branch}}`$。

- `git checkout -b {new_local_branch_name} -t {remote_name}/{remote_branch_name}`

  - 從指定的 remote repo 的某一條 branch 的最後一個 commit 在 local 以 `{new_local_branch_name}` 名稱建立一個新的 branch。

----------------------

## Git Checkout

- [Git 的 HEAD 意義](https://gitbook.tw/chapters/using-git/what-is-head.html)
- 切記，在 git 的世界中，**$`\textcolor{red}{\text{所有東西幾乎都是 git commit}}`$**!
  - HEAD 其實是指向一個 commit。
  - branch 也是指向一個 commit。
  - tag 還是指向一個 commit。
- 了解以上之後，其實 `git checkout` 這個指令可以理解成: $`\textcolor{red}{\text{在不同的 commit 中切換}}`$。
  - 因此，git 允許你切換不同的 branch、tag 甚至到某一個特定的 commit 上。
  - 因為其實你只是切換的 HEAD 指向的 commit 而已。
  - 也因此 git 能做到不同的 branch 也可以任意 merge，這是集中式版本控管系統 (譬如: svn 或 SourceSafe) 無法做到的事情。

- `git checkout {branch_name}`

  - 切換 local branch。
  - 當 `branch_name` 是 remote branch 時，可以切換到遠端的分支。

- `git checkout -t {remote_branch_name}`

  - 切換並且追蹤 remote branch，切換成功之後，會自動在 local 也新增對應名稱的 local branch，並且設定該 local branch 的 upstream 為該 remote branch 的 remote name。
  - 譬如: `git checkout -t origin/feature/cool-api-functions`
  - 其中 `origin/feature/cool-api-functions` 就是遠端分支的名稱。
  - 此時，會有一條名稱為 `feature/cool-api-functions` 的 local branch，並且它的 updtream 就是 `origin`。

- `git checkout {commit_id}`

  - 切換到 local git repo 上指定的 commit，此時執行 `git branch` 會發現 branch name 為 commit id。
  - 此時會顯示 **detached HEAD** (斷頭) 狀態。

- `git checkout -b {new_branch_name} {commit_id}`

  - 從指定的 commit 建立一個新的 local branch，並且指定新的 branch 名稱。
  - 此時就不會有 **斷頭** 狀態。

- `git checkout tags/{tag_name} -b {new_branch_name}`

  - 從指定的 tag 建立一個新的 local branch，並且指定新的 branch 名稱。
  - 此時也不會有 **斷頭** 狀態。

- 當執行 `git checkout` 時，如果 git 檢查到目前有已經異動的檔案，並且目標 branch 或 commit 該份檔案也有新的 commit 異動，git 在無法判斷應該如何自動合併的情況下，則會中斷 `git checkout` 切換的動作。
  - 可以先把目前的改動先 `git commit`，然後將目標 branch 的 merge 近來，把衝突解決之後，就可以正常 checkout 到目標 branch 中。
  - 如果不前的改動不允許先 commit，則可以先執行 `git stash save` 指令，把目前的改動 **暫存** 起來，此 `git stash` 操作不會產生新的 commit，只會存在暫存區，這時就可以先 checkout 到目標 branch 中，之後可以使用 `git stash pop` 將之前的暫存還原。
    - 但要還原 `git stash pop` 之前，建議先 `git checkout` 到原本進行 stash save 的 branch 中，以避免又有衝突發生。

----------------------

## Git Merge

- 此為 git 對兩個不同的 branch 或 commit 進行合併的動作。

- `git merge {from_branch_name}`

  - 從 `from_branch_name` 分支，把 commit 合併到目前 HEAD 指向的 branch 中。
  - 假若目前是切換到 A branch，然後執行 `git merge B`，這代表把 A branch 的 commit 合併到目前 B branch 中。
    - 如果此時發現衝突，
      - git 會自動停止，出現衝突訊息，此時需要自行選擇要使用 A branch 或 B branch 的檔案內容進行合併。
      - 當把衝突解決完成之後，需要執行 `git add` 指令，然後執行 `git commit`，這樣才算完成 merge 操作。
    - 如果此時沒有衝突，
      - git 會自動進行合併，並且產生一個新的 commit，並且 git 還會自行給定一個 git commit message。

- `git merge --abort`

  - 當在執行 `git merge` 解衝突的過程中，想要放棄這一次的合併操作，可以使用 `git merge --abort` 指令，此時會完全還原到原本 branch 在執行 `git merge` 之前的狀態。

- `git merge {from_branch_name} --no-ff --no-commit`

  - `--no-ff`: 不使用快速滾動模式進行合併。
  - `--no-commit`: 在合併的過程中，不會自動產生 commit，需要由自己手動執行 `git commit` 產生合併的 commit。

- `git merge {from_branch_name} --squash`

  - `--squash`: 不會將原本在 `{from_branch_name}` 的 commit 直接合併到目前的 local branch，而是把 `{from_branch_name}` 所有不在目前 local branch 的 commit 擠壓成一個 commit 之後再合併到 local branch。
  - 這種合併方式雖然以檔案結果來說都會一樣，但會讓 from_branch 和 to_branch 的 commit 越差越多。當使用 `git log {to_branch}..{from_branch}` 比較兩條 branch 的 commit 差異時，會越差越多，介意此情況的人需要考慮使否不要使用 `--no-squash` 參數進行合併。

## Git Rebase

- 將目前的 git commit 記錄重新調整，移花接木。
- 當發生衝突時，與 `git merge` 不同的地方在於
  - `git rebase` 需要一個一個 commit 去解衝突。
  - `git merge` 只要一次解完有最終的衝突，就可以完成。

- `git rebase` 完成後不會產生任何新的 commit，但 `git merge` 完成之後一定會產生一個新的 commit。
  - 因此，`git rebase` 可以讓兩條 branch 的 commit 記錄完全一致。
  - 而 `git merge` 永遠不會讓兩條 branch 的 commit 一致。
  - 只是如果兩種方式 resolve conflict 的結果一樣時，使用 `git diff` 指令比較兩種合併的檔案結果會是相同的。

- 使用 `git rebase` 進行合併操作上較危險一點，但是，因為不會產生額外的 git commit，因此 `git log` 的 commit 圖形會相對容易觀察與檢視。
  - 也因此基本上 remote 是不允許 remote rebase。
  - GitLab 預設是不能在 remote 直接執行 rebase 操作。
  - 但 Azure DevOps Repository 好像可以執行 remote rebase 操作。

- 建議指令
  - `git rebase -i` (建議使用互動模式進行 rebase)
  - `git rebase --continue`
  - `git rebase --abort`

- Reference

  - [另一種合併方式 (使用 rebase)](https://gitbook.tw/chapters/branch/merge-with-rebase.html)
  - [分支合併: merge 與 rebase 差異](https://www.maxlist.xyz/2020/05/02/git-merge-rebase/)
  - [送 PR 前，使用 Git rebase 來整理你的 commit 吧](https://medium.com/starbugs/use-git-interactive-rebase-to-organize-commits-85e692b46dd)
  - [將多個 commit 進行合併操作，整理 commit 紀錄](./git-rebase-merge-commit.md)

## Git Cherry-Pick

- 當想要只用某幾個特定的 commit 合併到目前當前的 branch 情況，則可以使用 `git cherry-pick` 操作。
- 實際上 `git cherry-pick` 指令背後真正是在執行 `git rebase`。
- 建議指令
  - `git cherry-pick {commit_id} --no-ff --no-commit`

----------------------

- Reference

  - [合併分支](https://gitbook.tw/chapters/branch/merge-branch.html)
  - [使用 Git 分支 - 分支和合併的基本用法](https://git-scm.com/book/zh-tw/v2/使用-Git-分支-分支和合併的基本用法)
  - [How to change the remote a branch is tracking?](https://stackoverflow.com/questions/4878249/how-to-change-the-remote-a-branch-is-tracking)
  - [使用 Git 分支 - 遠端分支](https://git-scm.com/book/zh-tw/v2/%E4%BD%BF%E7%94%A8-Git-%E5%88%86%E6%94%AF-%E9%81%A0%E7%AB%AF%E5%88%86%E6%94%AF)

----------------------

### [回到目錄](../index.md#目錄)
