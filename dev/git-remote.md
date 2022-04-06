# git refspec explicit way


for a recent git version let's get a remote branch to a local branch with different names :

````bash
git switch -c heimnico/main heimnico/main
Branch 'heimnico/main' set up to track remote branch 'main' from 'heimnico'.
Switched to a new branch 'heimnico/main'
````

for old version you can use the ``checkout`` command

## list refspecs

### locals

````bash
git show-ref
33c47a86e5ddfa044e4957470a6557f8fbe66483 refs/heads/heimnico/main
384bbdefb948a8f728f38eaba6bb078c6efd6613 refs/heads/main
33c47a86e5ddfa044e4957470a6557f8fbe66483 refs/remotes/heimnico/main
384bbdefb948a8f728f38eaba6bb078c6efd6613 refs/remotes/origin/HEAD
a1649e065b0c69ac80f5c8496a11f4114fdb30a7 refs/remotes/origin/dev
7f34e89b856e9e1397c10a779f87e0b90377991e refs/remotes/origin/feature/build
35033b52a5b0efe33a34f0b225bab71a738f095a refs/remotes/origin/features/ajout_endpoint_getAllVacationByIdEmployee
f83b7b9d87213c929ecb6ed345a8b06fcdc1a0ce refs/remotes/origin/features/branchement-collab
048aed9d663892cc253ea9ff34fcdc39e7fbcae4 refs/remotes/origin/features/security_api_keycloak
384bbdefb948a8f728f38eaba6bb078c6efd6613 refs/remotes/origin/main
194016e1f528ea430dafdaecfe5403e02c85bd2c refs/remotes/origin/poc/dapper
b2665ae62dc50b84b83412c7036c87ef2f1bee57 refs/remotes/origin/recette
````

### remotes

````bash
git ls-remote
From git@ssh.dev.azure.com:v3/heimnico/xperience/xperience-onexperience-api
33c47a86e5ddfa044e4957470a6557f8fbe66483        HEAD
33c47a86e5ddfa044e4957470a6557f8fbe66483        refs/heads/main
````

## fetching with full refsspec

````bash
git fetch heimnico refs/heads/main:refs/remotes/heimnico/main
````

## pulling with full refspec

````bash
git pull heimnico refs/heads/main:refs/remotes/heimnico/main
Already up to date.
````

## pushing

````bash
git push heimnico refs/remotes/heimnico/main:refs/heads/main
Everything up-to-date
````