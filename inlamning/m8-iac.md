## Terraform apply

Före jag körde terraform apply så skapade jag terraform.tfvars och conffade den enligt instruktionerna. Sedan körde jag : 
```bash
terraform fmt -check
terraform init -backend=false
terraform validate
```
och fick grönt på validate. Efter det körde jag `terraform init`, `terraform plan` och sedan apply

<img src="screenshots/m8-iac/terraform-apply.png" alt="Terraform apply" width="600">

Körde `curl`på nya med nya ip på `api/health` och det svarade som förväntat

<img src="screenshots/m8-iac/terraform-curl.png" alt="Curl" width="600">

Testade frotenden i browsern med den nya IP-adressen och även det lyckades

<img src="screenshots/m8-iac/terraform-frontend.png" alt="Frontend i webbläsare" width="600">


## Instance removal och Floating IP dissassociation

Tog bort m7 instance vi skapade manuellt.

<img src="screenshots/m8-iac/instances.png" alt="Instance removal" width="600">

Efter det dissasocierade jag även den gamla floating-ip så den frias upp.

<img src="screenshots/m8-iac/floating-ip.png" alt="Floating-ip" width="600">

## Terraform state  + Terraform destroy

<img src="screenshots/m8-iac/terraform-state.png" alt="Terraform state" width="600">

Terraform state visar den nuvarande staten terraform har av våra cloud resurser.

Outputtade floating ip och destroyade vår vm vi just byggde up med terraform

<img src="screenshots/m8-iac/terraform-destroy.png" alt="Terraform apply" width="600">

Efter det körde jag `terraform apply` igen och kollade floating ip. Den är samma som den var före  vi destroyade alltså sparas den som den borde.

<img src="screenshots/m8-iac/terraform-apply-v2.png" alt="Terraform apply efter destroy" width="600">

## BONUS

Testade köra terraform destoy utan en flag för att se ifall terraform stoppar det som den borde. Fick exakt den varning som beskrevs i instruktionerna.

<img src="screenshots/m8-iac/bonus.png" alt="Terraform apply" width="600">