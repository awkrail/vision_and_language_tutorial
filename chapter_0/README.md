# Chater 0. Vision-and-Languageとは?
## はじめに
Vision and Languageとは、視覚情報と言語情報を「つなぐ」技術の総称を指します。
たとえば、[画像を入力としてその説明文を生成](https://www.cv-foundation.org/openaccess/content_cvpr_2015/papers/Vinyals_Show_and_Tell_2015_CVPR_paper.pdf)したり、逆に[説明文を入力に与えて画像を生成](http://proceedings.mlr.press/v48/reed16.pdf)したりといった技術です。
2021年にはOpen AIが[DALL-E](https://openai.com/blog/dall-e/)という画像-テキストの組み合わせの大規模なデータセットを用いてニューラルネットワークを学習させ、説明文からいかにもそれらしい画像を出力できることを示し話題となりました。

Vision and Languageは深層学習以前から行われてきた課題ではありましたが、視覚情報と言語情報を同時に処理することは難しく、萌芽的な取り組みに止まっていました。
深層学習の普及によって、状況は大きく変わります。言語、画像のそれぞれの情報を処理するモデルをニューラルネットワークによって統一的に記述し最適化することで、視覚・言語情報を同時に処理することがが可能となってきました。 
たとえば、画像を処理するネットワークは畳み込みニューラルネットワーク(CNN)を用いて特徴を抽出することができ、言語を処理するネットワークは再帰的ニューラルネットワーク(RNN)を用いて特徴を抽出することができます。こうしたネットワークの出力に対して適切な損失関数を設定しそれを最小化する(例えば画像から説明文を生成する場合、説明文の負の対数尤度関数を最小化します)ことで、両方のニューラルネットワークを同時に最適化することが可能になります。こうして得られた結果は深層学習が発展する以前の結果を圧倒するものであり、現在も活発に研究が行われています。

著しい発展を見せているVision and Languageですが、コードを書きながら体系的に学ぶ資料は今のところありません(私の知る限り)。そこで、本チュートリアルではこうした技術をソースコードを書くことによって学んでいきます。2022年現在、この分野でホットであるだろう分野、あるいは知っておいた方がいい分野を6つ挙げました。どこから読んでも大丈夫なように作成していきたいと考えていますが、難易度的に簡単な方から順になるようにソートしています(完全に私の主観です)。

### 取り組む課題の簡単な説明

**Chapter 1. 共有埋め込み空間の獲得 (Joint embedding space):** 共有埋め込み空間とは、視覚情報とそれに対応する言語情報が同じ点に射影されるような空間を指します。こうした空間では言語情報から視覚情報を双方向に検索することが可能になります。本章では[Triplet Margin Lossを用いた共有埋め込み空間](https://arxiv.org/pdf/1703.07737.pdf)を取り上げます。

**Chapter 2. 画像/動画からのキャプション生成 (Image/Video captioning):** 画像や動画からその説明文を生成する技術について学びます。画像キャプション生成については[Show and Tell](https://www.cv-foundation.org/openaccess/content_cvpr_2015/papers/Vinyals_Show_and_Tell_2015_CVPR_paper.pdf)を実装します。動画キャプション生成については[TBD]()を実装していきます。

**Chapter 3. 画像を用いた質問応答 (Visual question answering):** 画像とそれを参照する質問文が与えられたとき、質問に対する答えを出力する課題です。[TBD]()を実装します。

**Chapter 4. キャプションからの画像生成 (Text-to-image generation):** Chapter 2では画像や動画から説明文を生成する課題に取り組みました。この課題ではその逆、説明文から画像を生成する課題に取り組みます。この課題において標準的に用いられるモデルである[Stack GAN++](https://arxiv.org/abs/1710.10916)を実装します。

**Chapter 5. 事前学習モデル (Vision-and-language pretraining):** 自然言語処理において大規模な事前学習モデル[BERT](https://aclanthology.org/N19-1423.pdf)が台頭したことをきっかけに、それをVision and Languageに拡張する取り組みも活発に行われています。この章では[TBD]()を実装することを通してVision and Languageの事前学習モデルを習得します。

**Chapter 6. 言語によるエージェントの移動 (Vision-and-language navigation):** あまり知らないので[TBD]()


## 注意事項
本チュートリアルの対象者はVision and Languageを学びたい方です。より具体的には、Python、深層学習の実装方法はある程度理解しており(画像やテキストの分類問題を解くニューラルネットワークの実装を行うことができる程度)、Vision and Languageの技術に焦点を当てて学びたい人向けとなっております。深層学習の理論や実装につきましては、別の資料で学んでいただけますと幸いです。私のオススメは[ゼロから作るDeep Learning ――Pythonで学ぶディープラーニングの理論と実装](https://www.oreilly.co.jp/books/9784873117584/)です。

## 参考資料
Vision and Languageは近年急速に注目を集めている分野で、まとまった資料は多くはありません。
以下にVision and Languageに関する資料をいくつか列挙します。この部分は今後も加筆していく予定です(あるいはPull Requestを送っていただけると嬉しいです)。

### 日本語
牛久先生の資料
- [Deep Learning による視覚×言語融合の最前線](https://speakerdeck.com/yushiku/deep-learning-niyorushi-jue-xyan-yu-rong-he-falsezui-qian-xian?slide=3)
- [Vision and Languageとその先へ](https://speakerdeck.com/yushiku/vision-and-language-tosofalsexian-he)

品川先生の資料
- [Vision and Languageと分野を取り巻く深層学習手法の紹介](https://speakerdeck.com/sei88888/vision-and-languagetofen-ye-woqu-rijuan-kushen-ceng-xue-xi-shou-fa-falseshao-jie)
- [Vision and LanguageとTransformers](https://speakerdeck.com/sei88888/2022-dot-2-11-di-6hui-tong-ji-ji-jie-xue-xi-ruo-shou-sinpoziumu-tiyutoriarujiang-yan-vision-and-languagetotransformers)

書籍
- [キッチン・インフォマティクス-料理を支える自然言語処理と画像処理- (4章にクロスモーダル処理について記述されています)](https://www.amazon.co.jp/%E3%82%AD%E3%83%83%E3%83%81%E3%83%B3%E3%83%BB%E3%82%A4%E3%83%B3%E3%83%95%E3%82%A9%E3%83%9E%E3%83%86%E3%82%A3%E3%82%AF%E3%82%B9-%E6%96%99%E7%90%86%E3%82%92%E6%94%AF%E3%81%88%E3%82%8B%E8%87%AA%E7%84%B6%E8%A8%80%E8%AA%9E%E5%87%A6%E7%90%86%E3%81%A8%E7%94%BB%E5%83%8F%E5%87%A6%E7%90%86-%E5%8E%9F%E5%B3%B6-%E7%B4%94/dp/4274226565)

### 英語
WIP
