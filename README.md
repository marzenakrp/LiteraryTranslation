# Translating World Literature at a Paragraph-Level

[![arxiv](https://img.shields.io/badge/arXiv-2304.03245-b31b1b.svg)](http://arxiv.org/abs/2304.03245)

This is the official repository for evaluation data from "Large language models effectively leverage document-level context for literary translation, but critical errors persist" (check out our [paper](http://arxiv.org/abs/2304.03245) for details).

## UPDATES


## DATA


This repository contains error annotations on machine translated literary work. The annotations were performed on two translation outputs at a time in [LabelStudio](https://labelstud.io/). You can view the actual interface simply by downloading the data in `./annotations/labelstudio_format_v1` and unploading it to LabelStudio. You will also need to use the code in `labelstudio_interface_code` as the interface. If you just want to download the actual data you should download the `./annotations/default_v1` file. This file contains the pairwise comparisons along with error annotations for each translation and translator's comments. Here is the general structure:

```json
{
  "eval": "fr_ja_1",
  "book": "la_liseuse",
  "author": "paul_fournel",
  "source": "Celui qui est sous ma joue est un manuscrit d’amour : c’est l’histoire d’un mec qui rencontre une fille mais il est marié et elle a un copain… J’en ai lu sept pages et je le connais déjà par cœur. Rien ne pourra me surprendre. Depuis des lunes, je ne lis plus, je relis. La même vieille bouillie dont on fait des « nouveautés », des saisons, des rentrées « littéraires », des succès, des bides, des bides. Du papier qu’on recycle, des camions qui partent le matin et qui rentrent le soir, bourrés de nouveautés déjà hors d’âge.",
  "target": "私の頬の下にあるのは、恋愛小説の原稿。男と女が出会い、男は結婚していて、女には彼氏がいるという物語……七ページ読めば、あとは読まなくてもわかる。はっと驚かされるような場面は出てこないだろう。ずっと前から、新たに読むというよりは再読。繰り返される「新作」、巡りくる季節、秋の文芸賞レース、当たっては外れ、そしてまた外れる。リサイクルに出す紙の山、時代遅れになった新作を満載し、朝に出発して、夜に帰ってくる何台ものトラック。",
  "source_lang": "fr",
  "target_lang": "ja",
  "text1": "私の頬にあるのは、愛のための手稿だ。それは、男が女に出会う物語だが、彼は既婚者で、彼女は彼氏がいる……という物語である。7ページ読んだだけで、もう覚えてしまった。何も私を驚かせることはない。月日が経つにつれて、もう新しい本を読むことはなくなり、繰り返し読むことになった。それは、新しいものを作り出すために使われる古い粥のようなものであり、季節や新学期、文学的な成功や失敗、大失敗などを作り出すものだ。リサイクルした紙、朝出かけて夜帰ってくるトラックが、すでに古臭い新商品でいっぱいだ。",
  "text2": "私の下頬の下にあるのは、愛の物語の手書き原稿だ。それは、男が女に出会う物語だが、彼は既に結婚していて、彼女も彼氏がいる……。私はその七ページを読んだが、もう心から覚えている。何も驚かせるものはない。月日が経つうちに、私はもう新しいものを読むのではなく、古いものを改めて読んでいる。「新しいもの」として、季節や新学期、文学的な「成功」や「失敗」として、何度も何度も取り上げられる古いものだ。朝に出て、夜に帰ってくるトラックは、すでに時代遅れの「新しいもの」でいっぱいだ。",
  "text1_tag": "sent",
  "text2_tag": "para",
  "difficult_choice": "YES, both translations are close in quality and it was hard to choose between them.",
  "comment": "Both translations are relatively good and easy to read. Both translations translate the \"La même vieille...\" sentence in a way that it is very difficult to understand - almost word by word especially in T1. Also the 愛のための手稿 in T1 is awkward and later という物語である is not necessary and ends in である which doesn't fit well with other sentences.\nThe ending すでに時代遅れの「新しいもの」でいっぱいだ in T2 is really good which is why I chose this translation however they are neck and neck and the other one could have be chosen as well.",
  "choice": "text2",
  "added_omitted": "TRANSLATION 2 adds or omits information that significantly change the meaning of the text.",
  "annotations": {
    "text1": [
      {
        "start": 2,
        "end": 6,
        "annotated_text": "頬にある",
        "labels": ["MISTRANSLATION"]
      },
      {
        "start": 135,
        "end": 168,
        "annotated_text": "それは、新しいものを作り出すために使われる古い粥のようなものであり",
        "labels": ["MISTRANSLATION"]
      }
    ],
    "text2": [
      {
        "start": 2,
        "end": 4,
        "annotated_text": "下頬",
        "labels": ["MISTRANSLATION"]
      }
    ]
  }
}
```

Each entry contains the following information:
- `eval`: *(str)* specifies the type of evaluation; numbers correspond to three different pairwise comparisons described in the paper: (1) SENT vs PARA, (2) PARA_SENT vs PARA, (3) GTr vs PARA;
- `book`: *(str)* title of the book;
- `author`: *(str)* author of the book;
- `source`: *(str)* source passage;
- `target`: *(str)* target passage;
- `source_lang`: *(str)* language code for the source language;
- `target_lang`: *(str)* language code for the target language;
- `text1`: *(str)* translation presented to the annotators as translation 1;
- `text2`: *(str)* translation presented to the annotators as translation 2;
- `text1_tag`: *(str)* specifies the type of translation 1 as one of the following: SENT (sentence-level translation with `davinci-003`), PARA (paragraph-level translation with `davinci-003`), PARA_SENT (sentence-level translation including context with `davinci-003`), GTr (output of `GoogleTranslate`);
- `text2_tag`: *(str)* specifies the type of translation 2 as one of the following: SENT (sentence-level translation with `davinci-003`), PARA (paragraph-level translation with `davinci-003`), PARA_SENT (sentence-level translation including context with `davinci-003`), GTr (output of `GoogleTranslate`);
- `difficult_choice`: *(str)* indicator of whether the translator found both translations of similar quality (multiple-choice);
- `comment`: *(str)* translator's comment about the two translation, all references to translations were unified so that translation 1 is referred to as `T1` while translation 2 is referred to as `T2`. Comments made in Polish or Japanese were translated into English;
- `choice`: *(str)* translator's preferences as to which of the two translations is better (multiple-choice);
- `added_omitted`: *(str)* information on whether any of the texts adds or omits important information (multiple-choice);
- `annotations`: *(dict)* a dictionary containing error annotations for `text1` and `text2`. `start` and `end` indicate indices in the given text, `labels` is a list with all labels assigned to the given span.

Translation errors in `v1` can be one of the following:
- `MISTRANSLATION` - text was mistranslated or translated overly literally;
- `GRAMMAR` - translation contains a grammar error irrespective of the source text;
- `UNTRANSLATED` - text was left in the source language or only transliterated into the target language;
- `INCONSISTENT` - translation uses inconsistent terms to refer to the same entity where the same terms should be used;
- `FORMAT` - translation uses wrong format for the target language (mostly wrong punctuation in Japanese);
- `REGISTER` - translation uses wrong register with respect to the source text (annotated mostly for Japanese were these errors were aparent);
- `REPETITION` - text was repeated in the translation (annotated later for PARA_SENT).

### Disclaimer

The selection of novel fragments curated for this evaluation covers a wide variety of topics. Please be aware that among these, certain subject may delve into sensitive issues including mental health struggles such as depression.

During the final check and translation of comments made in languages other than English a few inconsistencies were spotted. These were corrected in the annotations, however, the numbers in the paper were not updated yet. These corrections do NOT change the overall conclusion, if anything strengthened it, and will be corrected in the paper as soon as possible (version published as WMT contains corrected numbers).

## Citation Information
If you use this dataset, please cite it as follows:
```
@inproceedings{karpinska-iyyer-2023-large,
    title = "Large Language Models Effectively Leverage Document-level Context for Literary Translation, but Critical Errors Persist",
    author = "Karpinska, Marzena  and
      Iyyer, Mohit",
    editor = "Koehn, Philipp  and
      Haddow, Barry  and
      Kocmi, Tom  and
      Monz, Christof",
    booktitle = "Proceedings of the Eighth Conference on Machine Translation",
    month = dec,
    year = "2023",
    address = "Singapore",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2023.wmt-1.41",
    doi = "10.18653/v1/2023.wmt-1.41",
    pages = "419--451",
    abstract = "Large language models (LLMs) are competitive with the state of the art on a wide range of sentence-level translation datasets. However, their ability to translate paragraphs and documents remains unexplored because evaluation in these settings is costly and difficult. We show through a rigorous human evaluation that asking the GPT-3.5 (text-davinci-003) LLM to translate an entire literary paragraph (e.g., from a novel) at once results in higher-quality translations than standard sentence-by-sentence translation across 18 linguistically-diverse language pairs (e.g., translating into and out of Japanese, Polish, and English). Our evaluation, which took approximately 350 hours of effort for annotation and analysis, is conducted by hiring translators fluent in both the source and target language and asking them to provide both span-level error annotations as well as preference judgments of which system{'}s translations are better. We observe that discourse-level LLM translators commit fewer mistranslations, grammar errors, and stylistic inconsistencies than sentence-level approaches. With that said, critical errors still abound, including occasional content omissions, and a human translator{'}s intervention remains necessary to ensure that the author{'}s voice remains intact. We publicly release our dataset and error annotations to spur future research on the evaluation of document-level literary translation.",
}
```
