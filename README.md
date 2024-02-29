# Discord Webhook for Gitea Actions
## Setup
1. In Gitea secrets, add a `WEBHOOK_URL` variable with the Discord web hook URL
1. In your Gitea actions yml file, add this to reference the variable you just created:
    ```yaml
        - uses: ruby/setup-ruby@v1
          with:
            ruby-version: '3.3'
        - name: Send Webhook Notification
          env:
            JOB_STATUS: ${{ job.status }}
            WEBHOOK_URL: ${{ secrets.WEBHOOK_URL }}
            HOOK_OS_NAME: ${{ runner.os }}
            WORKFLOW_NAME: ${{ github.workflow }}
          run: |
            git clone -b gitea https://github.com/FreedomCraft-Network/github-actions-discord-webhook.git webhook
            bash webhook/send.sh $JOB_STATUS $WEBHOOK_URL
          shell: bash
    ```
1. Enjoy!
