swagger: "2.0"
x-collection-name: GitHub
x-complete: 1
info:
  title: GitHub
  version: 1.0.0
host: api.github.com
basePath: /
schemes:
- http
produces:
- application/json
consumes:
- application/json
paths:
  /repos/{owner}/{repo}/stats/code_frequency:
    get:
      summary: Get Repos Owner Repo Stats Code Frequency
      description: |-
        Get the number of additions and deletions per week.
        Returns a weekly aggregate of the number of additions and deletions pushed
        to a repository.
      operationId: get-the-number-of-additions-and-deletions-per-weekreturns-a-weekly-aggregate-of-the-number-of-additi
      x-api-path-slug: reposownerrepostatscode-frequency-get
      parameters:
      - in: header
        name: Accept
        description: Is used to set specified media type
      - in: query
        name: access_token
        description: Your Github OAuth token
      - in: path
        name: owner
        description: Name of repository owner
      - in: path
        name: repo
        description: Name of repository
      responses:
        200:
          description: OK
      tags:
      - Repos
      - Owner
      - Repo
      - Stats
      - Code
      - Frequency
      - Aggregation