## L39 Slack Webhook URL

Slack > Preferences > Connected accounts > "app management page"
Search "Incoming WebHooks" and "Add App"

- Post to Channel : #info-githubactions
  - "Add Incoming WgHooks integration"

- Webhook URL `https://hooks.slack.com/services/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`
-


## L40 CI Workflow

![](pics/package_json.jpg)

- "test:unit"

```npm run test:unit```

![](pics/run_test-unit.jpg)

## L41 Set up GitHub Secrets

GitHub repo > Settings > Secrets > Actions secrets / New sedcret
- Name: AWS_ACCESS_KEY_ID
- Value: ****

- Name: AWS_SECRET_ACCESS_KEY
- Value: ****

## L42 Delete the ECR Image uploaded manually

ECS > Amazon ECR Repositories

- ecs-sample-webapp
- ecs-sample-backend
- ecs-sample-restapi

 "Delete" button


## L43 Implement CD Workflow

