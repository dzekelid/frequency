---
swagger: "2.0"
x-collection-name: Oxford Dictionaries
x-complete: 0
info:
  title: Oxford Dictionaries Retrieve the frequency of ngrams (1-4) derived from a
    corpus
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