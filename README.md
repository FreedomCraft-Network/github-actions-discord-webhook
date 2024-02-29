# Discord Webhook for Gitea Actions
## Setup
1. In Gitea secrets, add a `WEBHOOK_URL` variable with the Discord web hook URL
1. In your Gitea actions yml file, add this to reference the variable you just created:
    ```yaml
        - name: Send Webhook Notification
          uses: actions/setup-ruby@v1
          if: always()
          env:
            JOB_STATUS: ${{ job.status }}
            WEBHOOK_URL: ${{ secrets.WEBHOOK_URL }}
            HOOK_OS_NAME: ${{ runner.os }}
            WORKFLOW_NAME: ${{ github.workflow }}
          run: |
            git clone https://github.com/FreedomCraft-Network/github-actions-discord-webhook.git gitea
            bash webhook/send.sh $JOB_STATUS $WEBHOOK_URL
          shell: bash
    ```
1. Enjoy!
