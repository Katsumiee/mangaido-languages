# Mangaido languages

This repository is a collection of files used to translate [Mangaido](https://mangaido.com) website to different languages.

If only you know some other language than English we would be very grateful if you would like to help us build international community by translating here some files. It's super easy! You don't need to know how to program. Try, we'll tell you how! :smile:

---

## Quick tutorial video how to translate:

[![YouTube video](https://img.youtube.com/vi/sFZJUTPr5K8/0.jpg)](https://youtu.be/sFZJUTPr5K8)

---

### Currently supported languages:

We're currently supporting:

- English (en)
- Français (fr)
- 日本語 (ja)
- 简体中文 (zh-CN)
- 中國傳統的 (zh-TW)
- 한국어 (ko)
- Polski (pl)
- Deutsch (de)
- Bahasa Indonesia (id)
- Filipino (tl)
- Español (es)
- Magyar (hu)

if you know any other language and you want to help, let us know via email: contact@mangaido.com and we will add support to your language so that you will be able to start your translation journey here.

## About translation files

All the translation files are the "YAML" files with ".yml" extension. There are some rules that you should know in order to create working translations.

### Structure of files

The structure of such file looks like this:

File: `./views/chapters/form/en.yml`
```yaml
en:
  chapters:
    form:
      title_label: "Title"
      description_label: "Description"
```

Here we are translating **title** and **description** labels into English (en) that are used to generate chapter's form. File that will translate this labels to Polish will look like this:

File: `./views/chapters/form/pl.yml`
```yaml
pl:
  chapters:
    form:
      title_label: "Tytuł"
      description_label: "Opis"
```

As you can see we changed **en** to **pl** to indicate that following code will be about Polish translation (in code and in filename). We also, of course, translated definitions of labels to Polish.

### Indentation

You can see that indentation (*the placement of text farther to the right*) is very important here. Always use two spaces as an indentation (not tabs). Indentation in YAML files are used to indicate that something more to the right is nested more deeply.

### Structure of folders

Files in this repository are organized in a specific way. Usually folders are nested in a way that the path to them reflects content of ".yml" files inside them. So for example such file: `./views/chapters/form/pl.yml` will have translations of chapter's form for Polish language.

### Longer texts

Sometimes the translation of a label is very long and it is more convenient to use ">" operator instead of double quotes:

```yaml
en:
  :static_pages:
    terms_of_service: "This is a very long text. This is a very long text. This is a very long text. This is a very long text. This is a very long text. This is a very long text. This is a very long text. This is a very long text. "
```

In such conditions you can write:

```yaml
en:
  static_pages:
    terms_of_service: >
      This is a very long text. This is a very long text. This is a very long text. This is a very long text. This is a very long text. This is a very long text. This is a very long text. This is a very long text. 
```

### Variables inside labels

Sometimes you can find translation that look like this:

```yaml
en:
  novels:
    edit:
      title: "Editing: %{title} novel"
```

`%{title}` is a variable. In this place title of a novel will be injected. So this might look like this on the website:

*Editing: Example Great Story novel*

### Pluralization

You may find something like this:

```yaml
en:
  layouts:
    user:
      comments_btn:
        one: "%{count} comment"
        other: "%{count} comments"
      likes_btn:
        one: "%{count} like"
        other: "%{count} likes"
```

Here, we're defining text for "comments" and "likes" buttons. But, text will vary depending on the number of comments or likes. In English there are only two forms ->
- singular ("one")
- plural ("other")

So in English we're defining how the text will look like for "1" comment and for any other number "0, 25, 587, etc."
- 1 comment
- 24 comments

For example in Korean, Chinese and Japanese we will use only "other" key, because of language grammar. So we could delete line with "one" key. For example in Japanese it **might** (I don't know Japanese) look like this:

```yaml
ja:
  layouts:
    user:
      comments_btn:
        other: "%{count}つのコメント"
      likes_btn:
        other: "%{count}つのような"
```

But in Polish it's much more complicated. Here we got 4 keys ("one", "few", "many", "other"). It's because based on the number, words needs to be written differently. So in this example it will look like this:

```yaml
pl:
  layouts:
    user:
      comments_btn:
        one: "%{count} komentarz"
        few: "%{count} komentarze"
        many: "%{count} komentrzy"
        other: "%{count} komentarza"
      comments_btn:
        one: "%{count} polubienie"
        few: "%{count} polubienia"
        many: "%{count} polubień"
        other: "%{count} polubienia"
```

### Pluralization rules

**English, German, Spanish:**
- 1 -> "one" key
- any other numbers -> "other" key

**French, Filipino:**
- 0, 1 -> "one" key
- any other numbers -> "other" key

**Japanese, Chinese, Korean, Hungarian, Indonesian:**
- use only "other" key

**Polish:** (hard to explain - write 4 forms based on this simple examples)
- 1 -> "one" key
- 2, 3, 4 -> "few" key
- 0, 5, 6, 7 -> "many" key
- 3.5, 2.7, 0.16 (all the fractions) -> "other" key

**Russian:** (hard to explain - write 4 forms based on this simple examples)
- 1 -> "one" key
- 2, 3, 4 -> "few" key
- 5, 10 -> "many" key
- 3.5, 2.7, 0.16 (all the fractions) -> "other" key

### HTML tags

Sometimes you will find something like this:

```yaml
en:
  static_pages:
    privacy_policy:
      text_html: >
        <h1>
          This is headline, because of "h1" tag (headline 1)
        <h1>

        <p>
          This is a paragraph, because it's inside "p" tag.
          <br />
          This text is in next line because of "br" tag ("break")
        </p>

        <p>
          <b>This text is bold because of "b" tag</b>
          <i>This text is in italics because of "i" tag</i>
        </p>
```

In some cases it's necessary to have HTML tags inside translation texts to format text properly. We use only this tags:

- `<h1>Text goes here</h1>` - Headline. Text inside is bigger and styled as headline. There are also smaller haedlines: h2, h3, h4, h5
- `<p>Text goes here</p>` - Paragraph. Text inside is a paragraph.
- `<b>Text goes here</b>` - Bold text
- `<i>Text goes here</i>` - Italics
- `<br />` - Break line. Text after this tag will start from new line

If this is possible try not to edit HTML tags and leave them as they are, just translate the text.

---

## State of translation

Translation status as of 09 June 2017.

### Words count

*Counting measured for English language version*

All files:
- word count (more than 2 characters): 8814 words
- word count (more than 3 characters): 7517 words

Big texts:
- Privacy Policy:
  - word count (more than 2 characters): 897 words
  - word count (more than 3 characters): 745 words
- Terms of Service:
  - word count (more than 2 characters): 3381 words
  - word count (more than 3 characters): 2780 words
  
**All files without big texts:**
- word count (more than 2 characters): 8814 - 897 - 3381 = 4536 words
- word count (more than 3 characters): 7517 - 745 - 2780 = **3992 words**

Used command:
`I18n::WordCount.word_count(%path_to_translation%, %number_of_chars%)`

### Number of files

*Counted only English files*

171 `en.yml` files

Used command:
`find . -iname en.yml | wc -l`
