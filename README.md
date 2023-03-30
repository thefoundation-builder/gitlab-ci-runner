# gitlab-ci-runner


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
