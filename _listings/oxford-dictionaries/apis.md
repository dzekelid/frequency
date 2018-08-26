---
name: Oxford Dictionaries
x-slug: oxford-dictionaries
description: If you&rsquo;re looking to enhance your app or website with dictionary
  data, don&rsquo;t compromise on quality. The Oxford Dictionaries API offers easy
  and intuitive access to Oxfords dictionary content, which is trusted around the
  world. Here at Oxford Dictionaries, home of the OED, we love words. That&rsquo;s
  why we have experienced lexicographers tracking the living language, delving deep
  into our corpora and monitoring a wide range of media in order to understand how
  words are being used and how language is evolving. This research is used by our
  editors to write and edit dictionary entries and translations, meaning we&rsquo;re
  able to offer up-to-date, accurate, and reliable lexical content in multiple languages.
image: http://kinlane-productions.s3.amazonaws.com/api-evangelist-site/company/logos/oxford-dictionaries-api.png
x-kinRank: "7"
x-alexaRank: "0"
tags: Frequency
created: "2018-08-25"
modified: "2018-08-25"
url: https://raw.githubusercontent.com/streamdata-gallery-topics/frequency/master/_listings/oxford-dictionaries/apis.md
specificationVersion: "0.14"
apis:
- name: Oxford Dictionaries - Retrieve the frequency of ngrams (1-4) derived from
    a corpus
  x-api-slug: statsfrequencyngramssource-langcorpusngramsize-get
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
  image: http://kinlane-productions.s3.amazonaws.com/api-evangelist-site/company/logos/oxford-dictionaries-api.png
  humanURL: https://developer.oxforddictionaries.com/
  baseURL: https://od-api-demo.oxforddictionaries.com:443//api/v1
  tags: dictionaries, Words, General Data, Service API, Pedestal
  properties:
  - type: x-postman-collection
    url: https://raw.githubusercontent.com/streamdata-gallery-topics/frequency/master/_listings/oxford-dictionaries/statsfrequencyngramssource-langcorpusngramsize-get-postman.md
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-topics/frequency/master/_listings/oxford-dictionaries/statsfrequencyngramssource-langcorpusngramsize-get-openapi.md
- name: Oxford Dictionaries - Retrieve the frequency of a word derived from a corpus.
  x-api-slug: statsfrequencywordsource-lang-get
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
  image: http://kinlane-productions.s3.amazonaws.com/api-evangelist-site/company/logos/oxford-dictionaries-api.png
  humanURL: https://developer.oxforddictionaries.com/
  baseURL: https://od-api-demo.oxforddictionaries.com:443//api/v1
  tags: dictionaries, Words, General Data, Service API, Pedestal
  properties:
  - type: x-postman-collection
    url: https://raw.githubusercontent.com/streamdata-gallery-topics/frequency/master/_listings/oxford-dictionaries/statsfrequencywordsource-lang-get-postman.md
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-topics/frequency/master/_listings/oxford-dictionaries/statsfrequencywordsource-lang-get-openapi.md
- name: Oxford Dictionaries - Retrieve a list of frequencies of a word/words derived
    from a corpus.
  x-api-slug: statsfrequencywordssource-lang-get
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
  image: http://kinlane-productions.s3.amazonaws.com/api-evangelist-site/company/logos/oxford-dictionaries-api.png
  humanURL: https://developer.oxforddictionaries.com/
  baseURL: https://od-api-demo.oxforddictionaries.com:443//api/v1
  tags: dictionaries, Words, General Data, Service API, Pedestal
  properties:
  - type: x-postman-collection
    url: https://raw.githubusercontent.com/streamdata-gallery-topics/frequency/master/_listings/oxford-dictionaries/statsfrequencywordssource-lang-get-postman.md
  - type: x-openapi-spec
    url: https://raw.githubusercontent.com/streamdata-gallery-topics/frequency/master/_listings/oxford-dictionaries/statsfrequencywordssource-lang-get-openapi.md
x-common:
- type: x-api-gallery
  url: http://orghunter.api.gallery.streamdata.io
- type: x-api-stack
  url: http://oxford.dictionaries.stack.network
- type: x-blog
  url: https://api-blog.oxforddictionaries.com/
- type: x-developer
  url: https://developer.oxforddictionaries.com/
- type: x-faq
  url: https://developer.oxforddictionaries.com/faq
- type: x-forum
  url: https://forum.oxforddictionaries.com/api/
- type: x-twitter
  url: https://twitter.com/OxfordWordsAPI
include: []
maintainers:
- FN: Kin Lane
  x-twitter: apievangelist
  email: info@apievangelist.com
---