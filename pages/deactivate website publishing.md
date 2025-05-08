tags:: website, publishing, publish, pages, github
description:: instructions on how to disable the web version of this graph

- Om de publicatie-functie van deze repository weer te deactiveren zijn er de omgekeerde stappen nodig als bij [[guidelines website publishing]]:
	- (1) logseq settings aanpassen: `Set pages to public by default` in de editor-settings van logseq afvinken
	  (2) github actions: de workflow `.github/workflows/publish.yml` verwijderen
	  (3) github pages: op github, onder de tab `pages`, zet je de `build and deployment` -> `branch` op `None`; nadien kan je de branch `gh-pages` [verwijderen](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-and-deleting-branches-within-your-repository#deleting-a-branch).