# cosmos-transfer2.5-brev-starter

NVIDIA Brev上でCosmos Transfer2.5を動かすためのスターターガイドです。

NVIDIA学生アンバサダープログラムのワークショップのおまけとして作成しました。

ワークショップでの発表資料・動画は後日公開いたします。

## Lanchables

CARLAシミュレーターが動かせるLanchableです。
- [aboshi-carla-test](https://brev.nvidia.com/launchable/deploy?launchableID=env-39nylroJ9eQpxQYGRS0cQ7ZzJhb)

Cosmos Transfer2.5が動かせるLanchableです。
- [aboshi-cosmos-transfer2.5](https://brev.nvidia.com/launchable/deploy?launchableID=env-3AAopd7LOfpGDmbs7sbCgCcQeF1)

## 使い方

### 1. 入力用の動画を準備する

IsaacSimやCARLAシミュレーターなどで作成した動画をご用意ください。

`/Samples`ディレクトリの動画はご自由につかっていただけます。

独自の映像を作成したい方は、以下のLanchableからNVIDIA Brev上でCARLAシミュレーターを動かせます。

[aboshi-carla-test](https://brev.nvidia.com/launchable/deploy?launchableID=env-39nylroJ9eQpxQYGRS0cQ7ZzJhb)

### 2. Hugging Faceのアクセストークンを取得する

https://huggingface.co/settings/tokens

以下の条件のアクセストークンを発行してください。<br>
アクセストークンは一旦.txtなどに保存してください。
- Token type: `Read`
- Token name: `cosmos-transfer2.5`

以下の3つのモデルのに同意してください。

- [nvidia/Cosmos-Guardrail1](https://huggingface.co/nvidia/Cosmos-Guardrail1)
- [nvidia/Cosmos-Predict2.5-2B](https://huggingface.co/nvidia/Cosmos-Predict2.5-2B)
- [nvidia/Cosmos-Transfer2.5-2B](https://huggingface.co/nvidia/Cosmos-Transfer2.5-2B)

### 3. NVIDIA Brevでインスタンスを作成する
### 4. 環境構築

NVIDIA Brev上でCosmos Transfer2.5が動かせるLanchableを用意しました。

こちらから、1Clickで環境が整います。

[aboshi-cosmos-transfer2.5](https://brev.nvidia.com/launchable/deploy?launchableID=env-3AAopd7LOfpGDmbs7sbCgCcQeF1)

Build完了後、`Open Notebook`をクリックしてください。
Jupyter Notebookのターミナルより、`run.sh`を実行してください。

huggingfaceのアクセストークンの入力を求められますので、入力後Enterを押していただきますと、

Cosmos Transfer2.5のDockerが起動し、環境構築が完了いたします。

### 5. Cosmos Transfer2.5の実行

実行コマンド例
```bash
# <>の適切な値に書き換えてください。
python examples/inference.py -i <prompt_json_path> -o <output_dir>
# こんな感じです。
python examples/inference.py -i prompt.json -o output/
```

JSONファイルのサンプル
```json
{
    "name": "出力ファイル名",
    "prompt": "プロンプト(英語・300ワード以内)",
    "video_path": "base.mp4",
    "max_frames": 93,
    // 深度マップ
    "depth": { "control_path": "depth.mp4", "control_weight": 0.5 },
    // エッジ
    "edge": { "control_path": "edge.mp4", "control_weight": 0.2 },
    // セグメンテーション
    "segmentation": { "control_path": "segmentation.mp4", "control_weight": 0.3 },
    // ぼかし
    "vis": { "control_path": "vis.mp4", "control_weight": 1.0 }
}
```

## ライセンス

本リポジトリのスクリプトはMIT Licenseです。

Cosmos Transfer 2.5本体は[NVIDIA Open Model License](https://www.nvidia.com/en-us/agreements/enterprise-software/nvidia-open-model-license/)に従うようにお願いいたします。

## 参考

- [NVIDIA Cosmos](https://www.nvidia.com/en-us/ai/cosmos/)
- [Cosmos Transfer 2.5 GitHub](https://github.com/nvidia-cosmos/cosmos-transfer2.5)
- [NVIDIA Brev](https://brev.nvidia.com/)