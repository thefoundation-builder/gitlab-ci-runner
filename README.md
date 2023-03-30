gitlab-runner-in-github-action
===

This is a GitLab Runner in a GitHub Action , but as opposed to [the original version](https://dev.to/rikurouvila/how-to-trigger-a-github-action-with-an-htt-request-545) , this one uses a fixed TOKEN and uses the job_id as  changing parameter  ( so the gitlab runner runs with the tag "$job_id" )

you could run this thingy with cron as well when changing build.yml


## Usage
Create a `TOKEN` github action Secret

Example invocation in .gitlab-cy.yml ( see the attached .sh file ):

```

requestrunner:
  stage: requestrunner
  image: ghcr.io/thefoundation-builder/alpine-ci-minimal:latest
  script: 
    - echo requesting runner
    - bash _0_request-github-actions-gitlab-runner.sh "${GITHUB_RUNNER_TOKEN}" "${RUNNER_REPO}" "${CI_PIPELINE_ID}" pages

pages:
  when: delayed
  start_in: 42 s
  tags:
      - "${CI_JOB_NAME}"
  only:
  - master
  stage: hugo
  script:
      - hugo
      - /bin/bash -c "bash update.links.sh"

```
