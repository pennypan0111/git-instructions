# Git Rebase

## 合併 Git Commit

- 當某個開發中的 branch 有過多的 commit，造成不容易還原到某一個版本，或不容易觀察主要的開發檔案異動紀錄時，可以考慮將一些 commit 合併起來。

###  假設情境

   -  git remote branch
      -  `origin/master`
      -  `origin/develop`

   -  git local branch
      -  `master`
      -  `develop`

###  在 local branch 使用 rebase 合併 commit

   -  `git checkout develop`
   -  `git log --graph`
   
      ```
      commit_id_c  commit_message_c
      commit_id_b  commit_message_b
      commit_id_a  commit_message_a
      ```

   -  假若想要把，`commit_id_c` 和 `commit_id_b` 進行合併。
      -  代表不動的 commit id 為 `commit_id_a`
      -  執行 `git rebase -i {維持不動的 commit id}`  -->  即為 `git rebase -i commit_id_a`

   -  git rebase interactive terminal 互動介面中。

      -  原始為 `pick`

         ```
         pick commit_id_b  commit_message_b
         pick commit_id_c  commit_message_c
         ```

      -  改為 `squash`

         ```
         pick commit_id_b  commit_message_b
         squash commit_id_c  commit_message_c
         ```

      -  執行 `:wq` 存檔後離開。

      -  在 git commit 互動介面中輸入新的 commit message，`:wq` 存檔後離開，即完成 git rebase 合併 `commit_id_c` 和 `commit_id_b`。
   
   -  可以先使用 `git log --graph` 檢查，理論上，應該出現以下的 git commit 圖形。

      ```
      commit_id_new  commit_message_b
                     commit_message_c
      commit_id_a    commit_message_a
      ```

   -  如果這時候 `git status` 發現與 `origin/develop` 有 commit 差異。

      -  使用 `git pull --rebase` 會重新把 origin 遠端的 commit 抓下來，自動進行 git rebase。 $`\textcolor{red}{\text{但是，之前在 local 合併後的 git commit 會消失不見!!!}}`$
      -  如果想要把 local `develop` branch 合併後的 commit 強制往 `origin/develop` 進行更新，可以執行 `git push origin --force`，則可以強制更新 `origin/develop` 的 branch，把合併後的 commit 更新至遠端。
      -  或者可以使用 `git push origin --force-with-lease` 同樣可以達到強制更新遠端 branch，但更為安全的指令。