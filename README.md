# Rational

Sometimes you accidentally deploy to production at 5:01 PM, break things, and go for dinner. Wouldn't it be great if you were warned before you did that (so you could do it with malice)?

# Usage & How it Works

The action takes arguments to determine the "unacceptable time window"; `start_hour_utc` and `end_hour_utc`. In that window, the action will fail, with a message posted in the PR. If you wish to go ahead, you can add the label that `bypass_label` is set to ("bypass-deploy-window-guard" by default).

If you configure your repository to require this check to pass before merging, you can effectively soft-block merging in the sensitive time you've defined.

Two example workflows in this repo show it in practice:

- [pr-checks](.github/workflows/pr-checks.yaml)
- [scheduled-pr-checks](.github/workflows/scheduled-pr-checks.yaml)

The point of the scheduled workflow is to re-evaluate the acceptable time window. Without this, a PR could pass the check during the acceptable time window, and be merged outside of it, or stay stuck as failed even when we're back in the acceptable time window.
