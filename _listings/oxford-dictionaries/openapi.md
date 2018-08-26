---
swagger: "2.0"
x-collection-name: Oxford Dictionaries
x-complete: 1
info:
  title: Oxford Dictionaries
  description: if-youre-looking-to-enhance-your-app-or-website-with-dictionary-data-dont-compromise-on-quality--the-oxford-dictionaries-api-offers-easy-and-intuitive-access-to-oxfords-dictionary-content-which-is-trusted-around-the-world--here-at-oxford-dictionaries-home-of-the-oed-we-love-words--thats-why-we-have-experienced-lexicographers-tracking-the-living-language-delving-deep-into-our-corpora-and-monitoring-a-wide-range-of-media-in-order-to-understand-how-words-are-being-used-and-how-language-is-evolving--this-research-is-used-by-our-editors-to-write-and-edit-dictionary-entries-and-translations-meaning-were-able-to-offer-uptodate-accurate-and-reliable-lexical-content-in-multiple-languages-
  termsOfService: http://helloreverb.com/terms/
  version: 1.8.0
host: od-api-demo.oxforddictionaries.com:443
basePath: /api/v1
schemes:
- http
produces:
- application/json
consumes:
- application/json
paths:
  /stats/frequency/ngrams/{source_lang}/{corpus}/{ngram-size}/:
    get:
      summary: Retrieve the frequency of ngrams (1-4) derived from a corpus
      description: |-
        This endpoint returns frequencies of ngrams of size 1-4. That is the number of times a word (ngram size = 1) or words (ngram size > 1) appear in the corpus. Ngrams are case sensitive ("I AM" and "I am" will have different frequency) and frequencies are calculated per word (true case) so "the book" and "the books" are two different ngrams. The results can be filtered based on query parameters.   Parameters can be provided in PATH, GET or POST (form or json). The parameters in PATH are overriden by parameters in GET, POST and json (in that order). In PATH, individual options are separated by semicolon and values are separated by commas (where multiple values can be used).   Example for bigrams (ngram of size 2):
        * PATH: /tokens=a word,another word
        * GET: /?tokens=a word&tokens=another word
        * POST (json):

          ```javascript
            {
                "tokens": ["a word", "another word"]
            }
          ```
      operationId: getStatsFrequencyNgramsSourceLangCorpusNgramSize
      x-api-path-slug: statsfrequencyngramssource-langcorpusngramsize-get
      parameters:
      - in: query
        name: contains
        description: Find ngrams containing the given token(s)
      - in: path
        name: corpus
        description: For corpora other than nmc (New Monitor Corpus) please contact
          api@oxforddictionaries
      - in: query
        name: format
        description: Option specifying whether tokens should be returned as a single
          string (option google) or as a list of strings (option oup)
      - in: query
        name: limit
        description: pagination - results limit
      - in: query
        name: maxDocumentFrequency
        description: Restrict the query to entries that appera in at most `maxDocumentFrequency`
          documents
      - in: query
        name: maxFrequency
        description: Restrict the query to entries with frequency of at most `maxFrequency`
      - in: query
        name: minDocumentFrequency
        description: Restrict the query to entries that appear in at least `minDocumentFrequency`
          documents
      - in: query
        name: minFrequency
        description: Restrict the query to entries with frequency of at least `minFrequency`
      - in: path
        name: ngram-size
        description: the size of ngrams requested (1-4)
      - in: query
        name: No Name
      - in: query
        name: offset
        description: pagination - results offset
      - in: query
        name: punctuation
        description: Flag specifying whether to lookup ngrams that include punctuation
          or not (possible values are true and false; default is false)
      - in: path
        name: source_lang
        description: IANA language code
      - in: query
        name: tokens
        description: List of tokens to filter
      responses:
        200:
          description: OK
      tags:
      - Stats
      - Frequency
      - Ngrams
      - Source
      - Lang
      - Corpus
      - Ngram-size
  /stats/frequency/word/{source_lang}/:
    get:
      summary: Retrieve the frequency of a word derived from a corpus.
      description: |-
        This endpoint provides the frequency of a given word. When multiple database records match the query parameters, the returned frequency is the sum of the individual frequencies. For example, if the query parameters are lemma=test, the returned frequency will include the verb "test", the noun "test" and the adjective "test" in all forms (Test, tested, testing, etc.)   If you are interested in the frequency of the word "test" but want to exclude other forms (e.g., tested) use the option trueCase=test. Normally, the word "test" will be spelt with a capital letter at the beginning of a sentence. The option trueCase will ignore this and it will count "Test" and "test" as the same token. If you are interested in frequencies of "Test" and "test", use the option wordform=test or wordform=Test. Note that trueCase is not just a lower case of the word as some words are genuinely spelt with a capital letter such as the word "press" in Oxford University Press.   Parameters can be provided in PATH, GET or POST (form or json). The parameters in PATH are overriden by parameters in GET, POST and json (in that order). In PATH, individual options are separated by semicolon and values are separated by commas (where multiple values can be used). Examples:
        * PATH: /lemma=test;lexicalCategory=noun
        * GET: /?lemma=test&lexicalCategory=noun
        * POST (json):

          ```javascript
            {
              "lemma": "test",
              "lexicalCategory": "noun"
            }
          ```

         One of the options wordform/trueCase/lemma/lexicalCategory has to be provided.
      operationId: getStatsFrequencyWordSourceLang
      x-api-path-slug: statsfrequencywordsource-lang-get
      parameters:
      - in: query
        name: corpus
        description: For corpora other than nmc (New Monitor Corpus) please contact
          api@oxforddictionaries
      - in: query
        name: lemma
        description: The lemma of the word to look up (e
      - in: query
        name: lexicalCategory
        description: The lexical category of the word(s) to look up (e
      - in: query
        name: No Name
      - in: path
        name: source_lang
        description: IANA language code
      - in: query
        name: trueCase
        description: The written form of the word to look up with normalised case
          (Books --> books)
      - in: query
        name: wordform
        description: The written form of the word to look up (preserving case e
      responses:
        200:
          description: OK
      tags:
      - Stats
      - Frequency
      - Word
      - Source
      - Lang
  /stats/frequency/words/{source_lang}/:
    get:
      summary: Retrieve a list of frequencies of a word/words derived from a corpus.
      description: |-
        This endpoint provides a list of frequencies for a given word or words. Unlike the /word/ endpoint, the results are split into the smallest units.   To exclude a specific value, prepend it with the minus sign ('-'). For example, to get frequencies of the lemma 'happy' but exclude superlative forms (i.e., happiest) you could use options 'lemma=happy;grammaticalFeatures=-degreeType:superlative'.   Parameters can be provided in PATH, GET or POST (form or json). The parameters in PATH are overriden by parameters in GET, POST and json (in that order). In PATH, individual options are separated by semicolon and values are separated by commas (where multiple values can be used).   The parameters wordform/trueCase/lemma/lexicalCategory also exist in a plural form, taking a lists of items. Examples:
        * PATH: /wordforms=happy,happier,happiest
        * GET: /?wordforms=happy&wordforms=happier&wordforms=happiest
        * POST (json):
        ```javascript
          {
            "wordforms": ["happy", "happier", "happiest"]
          }
        ```
         Aside from individual frequency requests, users can also post a list of items for which they would like to get frequencies. The list has to be uploaded in json and the required fields are "items" and "collate".   The field "items" is a list of items for which you want the frequencies. The content of the items depends on the option for "collate". The value of "collate" should be a list of "columns" that the items contain. The list is limited to combinations of "wordform", "lemma", "trueCase" and "lexicalCategory". The fields that are listed in the "collate" options have to be present in each item. Here are some examples of queries:
        * ### Get frequencies of provided wordforms:
        ```javascript
          {
              "collate": ["wordform"],
              "items": [{"wordform": "test"}, {"wordform": "Test"}]
          }
        ```
        * ### Get frequencies of provided lemmas:
        ```javascript
          {
              "collate": ["lemma"],
              "items": [{"lemma": "test"}, {"lemma": "Test"}]
          }
        ```
        * ### Get frequencies of provided lemmas per lexical category:
        ```javascript
          {
              "collate": ["lemma", "lexicalCategory"],
              "items": [
                  {"lemma": "test", "lexicalCategory": "verb"},
                  {"lemma": "test", "lexicalCategory": "noun"}
              ]
          }
        ```
      operationId: getStatsFrequencyWordsSourceLang
      x-api-path-slug: statsfrequencywordssource-lang-get
      parameters:
      - in: query
        name: corpus
        description: For corpora other than nmc (New Monitor Corpus) please contact
          api@oxforddictionaries
      - in: query
        name: grammaticalFeatures
        description: The grammatical features of the word(s) to look up entered as
          a list of k:v (e
      - in: query
        name: lemma
        description: The lemma of the word to look up (e
      - in: query
        name: lexicalCategory
        description: The lexical category of the word(s) to look up (e
      - in: query
        name: limit
        description: pagination - results limit
      - in: query
        name: maxFrequency
        description: Restrict the query to entries with frequency of at most `maxFrequency`
      - in: query
        name: maxNormalizedFrequency
        description: Restrict the query to entries with frequency of at most `maxNormalizedFrequency`
      - in: query
        name: minFrequency
        description: Restrict the query to entries with frequency of at least `minFrequency`
      - in: query
        name: minNormalizedFrequency
        description: Restrict the query to entries with frequency of at least `minNormalizedFrequency`
      - in: query
        name: No Name
      - in: query
        name: offset
        description: pagination - results offset
      - in: query
        name: sort
        description: sort the resulting list by wordform, trueCase, lemma, lexicalCategory,
          frequency, normalizedFrequency
      - in: path
        name: source_lang
        description: IANA language code
      - in: query
        name: trueCase
        description: The written form of the word to look up with normalised case
          (Books --> books)
      - in: query
        name: wordform
        description: The written form of the word to look up (preserving case e
      responses:
        200:
          description: OK
      tags:
      - Stats
      - Frequency
      - Words
      - Source
      - Lang
---