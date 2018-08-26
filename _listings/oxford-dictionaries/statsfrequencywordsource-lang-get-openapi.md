---
swagger: "2.0"
x-collection-name: Oxford Dictionaries
x-complete: 0
info:
  title: Oxford Dictionaries Retrieve the frequency of a word derived from a corpus.
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
x-streamrank:
  polling_total_time_average: 0
  polling_size_download_average: 0
  streaming_total_time_average: 0
  streaming_size_download_average: 0
  change_yes: 0
  change_no: 0
  time_percentage: 0
  size_percentage: 0
  change_percentage: 0
  last_run: ""
  days_run: 0
  minute_run: 0
---