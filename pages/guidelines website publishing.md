tags:: website, publishing, publish, pages, github
description:: instructions on how to update the web version of this graph

- Deze repo wordt automatisch vertaald naar een website: https://inbo.github.io/guidelines-monitoring-networks
- Normaal gezien zou je de procedure om een web-kopie van die graph te publiceren maar één keer configureren.
	- Maar: op een **forked** kopie van de repo zou het kunnen dat je de publicatie op een github page wilt deactiveren: [[deactivate website publishing]]
	-
- (1) Logseq Settings
	- In `logseq` kan je bepalen welke delen van je grafiek gepubliceerd worden, en welke niet.
	- https://docs.logseq.com/#/page/publishing/block/configuration
	- in een globale setting kan je aangeven dat pages standaard gepubliceerd worden.
	- Een enkele pagina kan je niet-publiek zetten door de pagina-eigenschap `public` bovenaan in de eerste cel te zetten:
	  ```
	  public:: false
	  ```
- (2) Implement (copy) a Github Actions workflow
	- A brief intro to Github Actions: https://docs.github.com/en/actions/writing-workflows/quickstart
	- Detailed instructions are found here: https://github.com/logseq/publish-spa (as of [[Feb 17th, 2025]])
	- Add the file `.github/workflows/publish.yml` to your repository:
	  ``` yaml
	  on: [push]
	  
	  permissions:
	    contents: write
	  jobs:
	    test:
	      runs-on: ubuntu-latest
	      name: Publish Logseq graph
	      steps:
	        - uses: actions/checkout@v4
	        - uses: logseq/publish-spa@v0.3.0
	        - name: Add a nojekyll file # to make sure asset paths are correctly identified
	          run: touch $GITHUB_WORKSPACE/www/.nojekyll
	        - name: Deploy 🚀
	          uses: JamesIves/github-pages-deploy-action@v4
	          with:
	            folder: www
	  ```
- (3) pages
	- Enable github pages on the repository: https://docs.github.com/en/pages/quickstart
	- link it to the `gh-pages` branch, which is created by the action above
	- https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site