# Individuell reflektion

## Produktens livscykel

Jag har kört kursen solo, så hela kedjan från M1 till M9 ligger i samma repo och
samma historik. I M1 var "livscykeln" i praktiken bara jag, min editor och
`git push`. I M2 lade jag på branch protection och ett ruleset som kräver pull
request — jag testade att pusha en empty commit direkt till main och remote
avvisade den. M3 containeriserade appen, M4 var bugjakten
där delete-endpointen inte uppdaterade globala `_total_characters` och buggen
hade nått main eftersom ingen skrivit ett test för just den funktionaliteten.

M5 och M6 var så ändrade workflowen ganska mycket. Ruff och pytest flyttade in i Actions som required
status check (testade regeln genom att medvetet skapa en ruff-error och se PR:en
blockeras), och imagena började byggas och taggas automatiskt vid push till
main. M7 var att skapa VMen manuellt med keypair, security group, instans och floating point för att sedan använda ssh in för att få upp stacken. I M8 skrev jag
samma VM som Terraform-kod. Att köra `destroy` och sedan `apply` igen och få
tillbaka samma floating IP var ett ganska bra sätt att förstå skillnaden mellan att "jag satte upp allt manuellt och måste komma ihåg hur" och att "det finns som kod som kör upp samma instans varje gång". I M9 ändrade jag en rubrik
i frontenden, mergade PR:en, och ändringen dök upp på nip.io-urlen utan att jag
rörde servern. Hela workflowen fungerade alltså från commit ->pr -> build images -> deploy to  VM

Det som förändrades mest i hur jag jobbade var vad jag litar på. I början
verifierade jag genom att köra saker själv, pytest lokalt, curl i terminalen,
kolla i webbläsaren. Mot slutet litar jag istället på att checkarna säger nej
ifall något är fel, och min uppgift blev mer att se till att checkarna testar
rätt saker.

Alla delmoment var ganska bra beskrivna och instruktionerna var relativt enkla att följa. Ibland kunde de vara ganska "råddiga", kanske skulle ha gått att förtydliga dem ibland. Kursen var överlag ganska bra, men jag personligen saknade lite teori. Jag tycker i skulle ha kunna dykt djupare i teorin kring de olika temorna som t.ex terraform etc. Jag förstår att kursen är väldigt bred och innehåller massvis med olika ämnen, och att det suklle vara omöjligt att dyka djupt i alla ämnen. Men ibland var teorin ganska kort och man resultatet är att man saknade en djupare förståelse för ämnet. Feedback för nästa gång kursen hålls.

## Vad går sönder utan automation?

Punkten jag funderar på är är CD-steget i M9 eftersom vid gjorde det manuellt för hand i M7. I M7 var varje ändring: bygga image, pusha till GHCR,
ssh in på VM:en, `docker compose pull`, `up -d`, och curla för att se ifall det
faktiskt blev den nya versionen. Det är 5-6 steg där inget verifieras av något annat
än att jag själv kommer ihåg ordningen. I M9 sker samma sak automatiskt med en merge.

Det som konkret går sönder är just ordningen. Deploy-workflowen triggas på
`workflow_run` efter publish-images, för att en vanlig push-trigger skulle köra
parallellt och kunna ssh:a in och pulla *innan* den nya imagen ens finns i GHCR.
För hand kan man göra precis samma misstag som detta undviker. Man pullar för tidigt, får
gamla imagen, ser ingen förändring i webbläsaren och börjar leta efter buggen i
koden istället för i ordningen man gjorde sakerna i. Allt lyckades i teorin men resultatet
blev bara fel och det är nog den typen av fel som är svårast att felsöka
manuellt.



