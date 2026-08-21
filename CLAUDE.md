# このリポジトリで作業するときの必須ルール

`nippo`は`ns-portal`と**同じSupabaseプロジェクト（ハブ）を共有**している。プロジェクト全体の唯一の正は`ns-portal`リポジトリの`WORKLOG.md`（要件定義書の最新版・システム全体像・DBテーブルの持ち主・接続情報・進行中の作業が冒頭に集約されている）。このリポジトリ単体にはWORKLOGを置かず、`ns-portal/WORKLOG.md`に一本化している。

GitHub: https://github.com/mirai-oss/ns-portal/blob/main/WORKLOG.md
このMacでは通常 `/Users/mirai/Claude/ns-portal/WORKLOG.md`（`nippo`の隣のディレクトリ）にある。無ければ`git clone`するかGitHubで直接読むこと。

## 作業を始める前に必ずやること

1. `ns-portal/WORKLOG.md`冒頭の「📍現在の状況」を読む。
2. `git fetch origin && git log --oneline -1 origin/main` で**nippo自身**の実際の最新コミットを確認する。ローカルより進んでいたら`git pull --rebase origin main`。**nippoは`index.html`1ファイルに全部入っているため並行編集で衝突しやすい**（過去に他セッションの42コミット分と衝突し手作業で解消した実績あり）。
3. ハブDB（`sf_*`/`users`/`stores`等の共有テーブル）に関わる変更をする場合は、`ns-portal/WORKLOG.md`の「🔐共有ハブDBのテーブル持ち主整理」も確認する。

## 作業を終える前に必ずやること（絶対に省略しない）

1. 変更をコミットし、`git push`する。
2. `ns-portal/WORKLOG.md`に今回の作業内容を時系列セクションとして追記する（nippo側の変更でも、ここが唯一の記録場所）。
3. `ns-portal/WORKLOG.md`冒頭の**「📍現在の状況」を今の状態に書き換える**（上書き）: 最終更新日時・進行中の作業・`ns-portal`と`nippo`それぞれの直近コミットハッシュ・次にやること候補。
4. 更新した`ns-portal/WORKLOG.md`をコミットし、`git push`する（`ns-portal`リポジトリ側でコミット・pushすることになる点に注意）。

この4ステップを終えて初めて「作業完了」。nippo側だけコミットしてWORKLOGを更新し忘れる、が一番の事故パターンなので注意。

## その他の鉄則（詳細は`ns-portal/WORKLOG.md`参照）

- 本番Supabaseへの SQL実行・Edge Functionのデプロイはユーザー確認を得てから行う。
- 本番データを直接テストに使わない。テストは使い捨てユーザー・使い捨てデータで行い、作業後に完全削除して0件を確認する。
