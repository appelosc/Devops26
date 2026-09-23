## Ruleset

<img src="screenshots/m5-ci/ruleset.png" alt="ruleset" width="600">

Skapade ruleset och lade till `require status checks to pass` där `lint and test backend`skall köras före en merge.

## Blockad merge

<img src="screenshots/m5-ci/blocked-merge.png" alt="Blocked merge" width="600">

Testade rulesettet genom att skapa en ruff error och skapa en pull request till main.
Bilden bevisar att regeln fungerar. Resolvade errorn och mergade.

## Manually triggered workflow

<img src="screenshots/m5-ci/manually-triggered-workflow.png" alt="Manually triggered workflow" width="600">

Lade till `workflow_dispatch` så man kan köra testerna manuellt. Bilden bevisar att jag kört lint and test backend via github actions på github.