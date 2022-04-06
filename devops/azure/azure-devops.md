# Azure devops

## Using an external registry

utilisation d'une task command line :
````
docker login registry.gitlab.com -u"<token>" -p 9XVbzU4rzcz1oNSTerxC
docker image tag myhealth.web registry.gitlab.com/37rtm.nheim/acedigitale-dev
docker push registry.gitlab.com/37rtm.nheim/acedigitale-dev
````


## Conditional pool

````yaml
  pool:
    ${{ if startsWith(variables['Build.SourceBranch'], 'refs/heads/ci-cd/') }}:
      name: CI-CD-NHM
  displayName: Package Onpremise Test
````
