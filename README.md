# Ciona Atlas

実際のCionectome再構成形態を、ブラウザーで回転・拡大し、細胞群ごとに色分けして見るビューアーです。MorphoNetは不要です。

## GitHubで共有

1. このZIPを展開し、GitHubにAtlas専用の空のリポジトリ（例: ciona-atlas）を作成します。一般公開する場合はPublicを選びます。
2. 展開先でPowerShellを開き、`./publish.ps1 -RepositoryUrl https://github.com/OWNER/ciona-atlas.git` を実行します。Gitが必要です。認証が出た場合は自分のGitHubアカウントでログインしてください。
3. リポジトリの Settings → Pages → Build and deployment で、Sourceを Deploy from a branch、Branchを main、フォルダーを /(root) にしてSaveします。
4. Pagesに表示される公開URLを共有します。閲覧者はNode.jsやPythonをインストールする必要がありません。

## 操作

- 全体・色分け：全206形態を表示。
- 細胞パネル：細胞群を選択。名前や番号でも検索できます。
- 選択した細胞を強調：周囲を薄く表示。
- 選択だけ表示／選択にズーム：局所を詳しく確認。
- この表示のリンク：細胞選択とカメラ位置を保存したURLをコピー。
- ドラッグで回転、ホイールで拡大。タッチ操作にも対応。

初回は全形態の読込に約436 MBを使用します。全体表示はGPUメモリーも必要です。端末によっては個別表示を使ってください。

## データ・帰属・解釈

形態データ: Ryan, Borba & Miao (2024), https://zenodo.org/records/12705627 。ライセンス: CC BY 4.0 (https://creativecommons.org/licenses/by/4.0/) 。
元の high res DXFをブラウザー向けの頂点・法線・三角形インデックスに変換し、可逆gzip圧縮しています。同一点のインデックス共有と退化面除去を行い、空間的な形状間引きは行っていません。

細胞群とEM IDの対応は classification.json に出典付きで記録。PNIN・PBV PNINはRyan et al. (2018), https://doi.org/10.1002/cne.24353 のTable 1、BPINなどはRyan & Meinertzhagen (2019), https://pmc.ncbi.nlm.nih.gov/articles/PMC6551260/ のTable 1に基づきます。形態分類と接続分類が重なる場合は代表色を使用し、未照合の形態は「その他」です。

RTENは再構成範囲内の軸索・終末です。細胞体の位置や細胞全体を示すものではありません。ATENグループはaATEN（ATEN1–4）です。座標軸と生体の左右・背腹との対応は未校正です。体全体の組織面やシナプス接続表は含みません。

本ビューアーは独立した可視化実装で、元データの著者やMorphoNetの公式サービスではありません。

## ファイル

index.html / viewer.js: 表示と操作。atlas.json: 形態一覧。classification.json: 細胞分類。data/*.gz: 個別の圧縮形態（各ファイル100 MB未満）。.nojekyll: GitHub Pagesで静的ファイルをそのまま配信するための設定。
