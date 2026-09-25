## Automatisk workflow med taggar

<img src="screenshots/m6-cd-images/automatic-workflow.png" alt="Automatically triggered workflow" width="600">

Kan se att workflowen triggas automatiskt och att den printar ut de taggar som imagen är taggad med, alltså sha hashen och `latest`

## Manuell workflow med taggar

<img src="screenshots/m6-cd-images/manual-workflow.png" alt="Manually triggered workflow" width="600">

Precis samma workflow bara att den nu är manuellt triggad så vi kan se att `workflow_dispatch:`fungerar

## Public packages

<img src="screenshots/m6-cd-images/public-packages.png" alt="Public packages" width="600">

Mina packages var redan public från tidigare, antaglien från `M3`. Men bilden bevisar att de är det.

## Test av public packages genom ghcr logout

<img src="screenshots/m6-cd-images/ghcr-terminal.png" alt="ghcr terminal output" width="600">

Terminal output på när jag testade ifall det går att pulla ner mina images utan credentials. Som vi ser så fungerar det och endpointen svara.

## Secrets masking

<img src="screenshots/m6-cd-images/secrets-masking.png" alt="GitHub token secret masking test" width="600">

Testade secrets masking på sin egen branch och triggade workflowen manuellt. Enligt resultatet så maskeras GitHuben tokenen på korrekt sätt. Städade upp mina branches efter det och deletade båda lokalt och origin av branchen så den aldrig nådde main.
