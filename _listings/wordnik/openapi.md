---
swagger: "2.0"
x-collection-name: Wordnik
x-complete: 1
info:
  title: Wordnik
  description: wordnik-is-the-worlds-biggest-online-english-dictionary-by-number-of-words
  version: "4.0"
host: api.wordnik.com
basePath: /v4
schemes:
- http
produces:
- application/json
consumes:
- application/json
paths:
  /word.json/{word}/frequency:
    get:
      summary: Returns word usage over time
      description: Returns word usage over time.
      operationId: getWordFrequency
      x-api-path-slug: word-jsonwordfrequency-get
      parameters:
      - in: query
        name: endYear
        description: Ending Year
      - in: query
        name: startYear
        description: Starting Year
      - in: query
        name: useCanonical
        description: If true will try to return the correct word root (cats -> cat)
      - in: path
        name: word
        description: Word to return
      responses:
        200:
          description: OK
      tags:
      - Words
      - Frequency
---