# Git Fetch, Git Pull & Git Push

- 當 local git repo 已經使用 [Git 遠端協作指令與設定 [Git Remote]](./git-remote.md) 中提及的指令設定組態好遠端的 remote repo 之後，則可以使用 `git fetch`、`git pull` 和 `git push` 等等常見的指令與 remote repo 協同合作版本控管。

----------------------

## Git Fetch

- 抓取 remote repo 遠端的 commit 與檔案異動到本地端 local 中，$`\textcolor{red}{\text{但是不直接更新當前 local repo 的 local branch}}`$。
- 只會先把 remote repo 抓取下來的 commit 暫存在 local repo 的 `FETCH_HEAD` 這個暫存的 branch 中。

- `git fetch {remote_name}`

  - `remote_name`: 指定 fetch 的 remote_name 名稱，預設為 **origin**。

- `git fetch {remote_name} --all`

  - 對 `remote_name` 這一個遠端，抓取所有 remote repo 遠端的 branch 的 commit。

----------------------

## Git Pull

- 抓取 remote repo 遠端的 commit 並且直接將遠端的 commit merge 到 local repo 當前的 branch 中。

- `git pull {remote_name}`

  - `remote_name`: 指定 fetch 的 remote_name 名稱，預設為 **origin**。
  - 這個指令會隱式的依照順序執行以下兩個指令。

    - `git fetch {remote_name}`

      - 先把遠端所有的 commit 先抓下來，放在 FETCH_HEAD 暫存分之中。

    - `git merge --ff {FETCH_HEAD}`

      - 然後把剛才抓下來的放在 FETCH_HEAD 中的 commit merge 到目前 local branch 中。
      - 如果 **不能直接 merge 完成，git 會提示 auto merge 失敗，需要手動 resolve conflict，完成中後才可以完成 merge，這一次的 `git pull` 才算完成**。

- `git pull {remote_name} --no-ff`

  - 代表執行 `git merge FETCH_HEAD` 合併時，請加上 `--no-ff` 參數，不使用快轉模式進行 merge。


- `git pull {remote_name} --rebase`

  - 代表當嘗試把 FETCH_HEAD 的 commit 合併到 local branch 時，不要使用 `git merge` 指令，而是使用 `git rebase` 指令進行 merge 操作。
  - 譬如，當遠端的 remote branch 可能曾經被 `git push --force` 強制更新了該 remote branch 的 commit history log 紀錄，這時候可以考慮使用 `git pull --rebase` 也更新本地端的 local branch 的 commit history 紀錄。

----------------------

## Git Push

- 把本地端的 local branch 的異動推送到 remote repo 中，實際上在 remote branch 中，也會發生 `git merge` 的操作。
- 這就是為什麼當 remote repo 發現無法 auto merge 成功時，會回應 error 訊息到 local repo，要求先在 local repo 把 conflict 解除掉，再進行 `git push` 操作。

- `git push {remote_name}`

  - `remote_name`: 指定 push 的 remote_name 名稱，預設為 **origin**。
  - 通常只會把 local repo 當前的 local branch 的 commit 推送到 remote repo 中。

- `git push {remote_name} -u {local_branch_name}`

  - 當 local repo 的 local branch 還沒有指定一個 remote repo 當作 upstream 的情況下，則需要使用 `-u` 參數去指定此次 push 的 upstream 上游分之名稱。
  - 簡言之，這種情況就是: **local repo 有這一條新的 branch，但是 remote repo 還沒有這一條 branch。(通常這種情況發生在，自己在 local repo 上，`git checkout -b` 建立了一條新的 local branch 時，但 remote repo 還沒有這條 branch。)**

- `git push {remote_name} --all`

  - 把 local repo 所有的 local branch 的 commit 都推送到 remote repo 中。
  - 但這只侷限於，local branch 已經有設定對應的 upstream 才會推送成功。

- `git push {remote_name} --all -u`

  - 把 local repo 所有的 local branch 的 commit 都推送到 remote repo 中，如果還沒有設定 upstream 會自動依照 local branch name 進行設定。

- `git push {remote_name} --tag`

  - 把屬於在這一條 local branch 的 tag 全部都推送到 remote repo 對應的 remote branch 中。

- `git push {remote_name} --tag {tag_name}`

  - 只把 local repo 特定的 tag 推送到 remote repo 中。
  - `tag_name`: 為 tag 名稱，可以使用 `git tag --list -n` 指令查看。

- `git push {remote_name} --force` 或 `git push {remote_name} --force-with-lease`

  - 強制把 local branch 的 commit 推送到 remote repo 的 remote branch 上，這個操作會對 remote branch 上的 commit history 進行 rewrite 改寫 (因為實際上這是一個 `git rebase` 操作。)
  - 首先，`git push --force` 強制推送，雖然確實是屬於比較危險的行為，但這在 git 的世界中完全合理，請不要以為這種行為或操作一定都是有問題的。所以在 GitHub 或 GitLab 上強制把 `git push --force` 「強制推送」功能關閉這是不建議的行為。因為以下馬上就要介紹，什麼樣子的情境，使用到 `git push --force` 完全合情合理。

    _(同常認為 force push 不合理的人，是根本不會 `git rebase` 這種強大的操作，所以才會認為 force push 是錯誤操作! 簡單的說，這種人叫做自己白癡! 因為根本就是典型的 git 半調子，有哪些 git CLI 根本搞不懂，只會自以為是的以為強制推送就一定很危險，很不安全... 就傻屌一個啊...)_

    - 當某一條 local branch，曾經執行 `git rebase` 合併並且 rewrite 目前這條 local branch 的 commit history 時，**這時候其實無法直接執行 `git push` 推送至遠端，因為兩邊的 commit log 紀錄已經不同!**
    - 這時候需要使用 `git push --force` 或 $`\textcolor{red}{\text{(更為安全的)}}`$ `git push --force-with-lease` $`\textcolor{red}{\text{指令，強制更新遠端的 commit log 紀錄與 local repo 的一致}}`$。
    - 此時，如果別人要從 remote repo，去 pull 這一條 branch 的 commit 時，他就可以使用 `git pull --rebase` 這一個指令去更新他自己的 local branch。

- `git push {remote_name} --all -u --force`

  - 強制對 `remote_name` 這一個 remote repo 遠端推送所有 local branch 的 commit，並且自動加上 upstream。
  - 這個指令代表強制把 local branch 所有東西都覆蓋掉到 remote repo 上，請小心使用。


  - 補充，執行 `git push --force` 指令時，如果 remote repo 對於 **該 remote branch 如果有設定「不允許」push 的設定** $`\textcolor{red}{\text{(即為 protected branch)}}`$，此情況下，即便執行 `--force` 仍無法成功推送到遠端。

- `git push {remote_name} :{remote_branch_name}`

  - 把 remote repo 的 remote branch 進行刪除。

  - 譬如: 執行 `git push origin :feature/IB-1145` 指令，代表要求把 remote repo 遠端的 feature/IB-1145 branch 刪除掉。
  - 注意，這個指令只會刪除遠端的分支，如果原本 local repo 就有 tract 這個 branch，在 local repo 中不會被刪除。
  - 如果想要把這條 feature/IB-1145 分支徹底從本地端與遠端刪除，並且在刪除之後執行 `git branch -a` 也看不到這條 branch，可以依照以下的指定進行操作。

    ```sh
    # 先同步本地端和遠端的 commit，並且切換到另一條我沒有要刪除的分支上。
    git checkout master
    git remote update origin

    # 刪除本地端的分支
    git branch -D feature/IB-1145

    # 刪除遠端的分支
    git push origin :feature/IB-1145

    # 更新 branch 資訊，把已經刪除掉的分支移除掉  
    git remote update origin
    git remote prune origin
    git fetch origin --prune
    ```

    - 此時再執行 `git branch -a`，可以發現 feature/IB-1145 這條分支已經完全在遠端和本地端都刪除掉了。

- 假設你現在想要修改目前 remote reop 最後一個 commit message，可以怎麼操作?

  - 先在 local repo 執行 `git fetch {remote_name}` 和 `git pull {remote_name}`，確保當下的 local repo 是跟 remote repo 一致的。
  - 然後這時候在 local reop 執行 `git commit --amend` 指令去修改最後一個 commit message。
  - 修改完成之後，可以先執行 `git log --graph` 確認一下是否修改成功。
  - 因為這個操作，除了會修改 local repo 最後一個 commit message 之外，其實還會修改最後一個 commit 的 commit id，因此這時候執行 `git status` 會顯示類似以下訊息，提示說 **目前你 local 的 commit 和 remote 有一個差異** 這是正常的情況。

    ```
    $ git status

    On branch feature/NewHappyBearHouse
    Your branch and 'origin/feature/NewHappyBearHouse' have diverged,
    and have 1 and 1 different commits each, respectively.
      (use "git pull" to merge the remote branch into yours)

    nothing to commit, working tree clean
    ```

  - 但其實所有檔案的檔案內容，都應該是一樣的，因為 `git commit --amend` 只是改 commit message 和 commit id，不會修改檔案內容。<br/>
    如果想要確認 loacl repo 和 remote reop 所有檔案內容是一樣的，可以執行 `git diff {remote_name}/{branch_name}` 去檢查檔案是否有差異。<br/>
    執行完成之後，應該會跳出一個「空的視窗」提示，因為沒有檔案差異，所以這是完全正確的，按下 `q` 就可以跳出。

  - 最後，在 local repo 執行 `git push {remote_name} --force-with-lease` 指令，把這個 commit message 的改動強制推送到 remote reop，然後遠端最後一的 commit message 就修改成功嘍。

----------------------

- References

  - [Pull 下載更新](https://gitbook.tw/chapters/github/pull-from-github.html)
  - [如何 Push 上傳到 GitHub](https://gitbook.tw/chapters/github/push-to-github.html)
  - [git fetch與git pull的區別](https://www.itread01.com/content/1545176737.html)
  - [上傳分支](https://zlargon.gitbooks.io/git-tutorial/content/remote/push.html)

----------------------

### [回到目錄](../index.md#目錄)
