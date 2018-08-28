---
swagger: "2.0"
x-collection-name: Wordnik
x-complete: 0
info:
  title: Wordnik Returns word usage over time
  description: Returns word usage over time.
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