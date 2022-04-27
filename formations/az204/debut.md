# Présentation

Dieudonné NTAMACK

AML => Azure machine learning

Developpeur backend, java + .net, projet azure

## Certification AZ204

taper dans google le numéro de la certification

## Niveau d'entrée dans le cloud

- On-Premise : datacenter en entreprise
  - il faut tout savoir gérer
- IaaS : Infrasctructure as a service , y compris réseau et stockage
  - Utilisation du cloud uniquement pour les VM
- PaaS : Platform as a service 
  - Toute l'infrastructure est dans le cloud provider
- SaaS : Sofware as a Service
  - Le cloud provider gère tout sauf les données
    

### Questions

forfait différents pour Iaas/Paas/SaaS ? passage de l'un à l'autre ?

# Fonctionalité clés

- Plusieurs languages et framework
- Interfacage avec de multiples applications
- bases de données locales

- mode serverless => pas de payement quand l'application n'est pas utilisée
  

### Authentification et authorization

- authentification à partir de l'environnement azure, et fédération des identités
- à interfacer avec l'AD local

web app => architecture 2/3
proxy avant de passer par azure, le client n'a pas accès au serveur

premier accès => easyauth.dll pour authentification, replaçable par un module d'authentification

### connexion hybride

pas obligé d'héberger les données dans un cloud par soucis de confidentialité.
installation de l'hybrid connection manager sur l'environnement on premises

### Azure traffic manager

possibilité d'imbrication du traffic manager

- configuration par performance
- configuration par poids 
- configuration par géographie
- redirection par VNet
- configuration multicritères, en cascade


### Azure app service local cache

### App Service environments (ASE)

Environnement dédié 
décider de déployer un env sur des site géo différent

l'api est la base du pilotage env azure mais Azure à développé des outils tels que le portail Azure
automatisation :
- azure cli
- azure powershell

centralisation désirée par microsoft sur le powershell, azure n'échappe pas à la règle
powershell n'est que pour les environnement windows de base

az cli pouvais s'exécuter sur n'importe quelle plateforme, depuis les choses ont évolués.
ARM permet de faire de l'IaC (infrastructure as code), les templates ARM

az group create --location westeurope --nanme myResourceGroup (nom DNS)

Une resource azure est un nom générique pour un service instancié sur Azure

### App service on Linux

Ruby en rails, PHP et Node ... Microsoft recommende du Linux


### hébergement de l'application sur des environnement docker

### APP Service settings

Override settings in Web.config ou appsettings.json

### types d'ip disponibles

- ip entrantes => ip utilisablent pour se connecter à notre webapp
- ip sortantes => 

autorisation des ip sortantes

l'ip entrante peux changer, changemetn de webapp => changement d'ip 
passage sur du Basic/Standard/Premium

reccupérer les ips 

az webapp show --resource-group <gruop_name> --name <app_name> --query
outboundIpAddesses --output
(PossibleIpAddresses


### Scaling vertical
- vers le haut => plus de composants etc sur la machine physique
- vers le bas => reduire les ressources machine

- arrêt de service car changement de machine, duplication
- pas d'automatisation fournie par Azure
  
### Scaling horizontal
- clustering, augmenter ou augmenter le nombre de serveurs disponibles

- pas d'interruption de service
- automatisation possible (auto scale)

Ajustement de metric => ex: si trop d'utilisation CPU => augmentation resource

#### Autoscale partern

- metrique par CPU
- dates semaines
- dates congés etc

via Json et les API sur Azure


autoscale => one to many profiles
Profiles => on to many rules

utilisation de trigger possible pour les autoscale
et ou notification

### Bonnes pratiques scaling

valeur minimum et macimum différente
scaling manuel est reset par autoscale
thresolds => intervales

### Environnements

utilisations de plusieurs slots par webapp exemple pourenv Test/Dev/Prod

workflow de deployment moderne

### Autoswap possible

Route traffic
labs => Pa$$w0rd

### Lab =>

az login
az webapp list --resource-group ManagedPlatform-lod17954831
az webapp list --resource-group ManagedPlatform-lod17954831 --query "[?starts_with(name, 'imgweb')]"

az webapp list --resource-group ManagedPlatform-lod17954831 --query "[?starts_with(name, 'imgweb')].{Name:name}" --output tsv

az webapp deployment source config-zip --resource-group ManagedPlatform-lod17954831 --src web.zip --name imgwebheim

msdeploy

### Function App

pas forcement besoin de web plan, il est possible que ça soit du serverless

possibilité d'utiliser azure stack pour utiliser les fonction azure 

pour consommer une fonction en interne  à azure (non publiée)

#### Triggers

depuis Cosmos 
depuis git Hub

#### Bidings

façon déclarative de connecter les doonées au code

bindings optionnels

#### bonnes pratiques

concue pour pouvoir exécuter une seule opératino à la fois, et dans un temps très cours
Si c'est trop long, Azure risque de l'arrêter.
ne pas appeller une fonction qui appelle une autre fonction.
utiliser des files d'attentes.
pas d'état dans les fonctions

code défensif => réentrant

structure de fonction 

FunctionApp => 
    host.json
        FirstFunction
        SecondFunction

### Durable Functions

éviter les fonction durables mais si besoin de garder un état
- Fan-out/Fan-in
- 
- Monitoring

DurableOrchestrationContext
DurableOrchestrationClient

msdeploy.exe -verb:sync -source:apphostconfig="Default Web Site" -dest:package=c:\dws.zip > DWSpackage7.log

### Compte de stockage

Blob => fichiers
partages SMB
Tables => Service NOSQL
Queues => exemole faire communiquer deux fonctions

VM => compte de stockage nécessaire

plusieurs types de blobs

#### Blocks

la taille des blocs permet d'optimiser les transactions, moins de blocs => efficacité
block taille mininum (quantum)

#### Append

optimisation écriture
Logs => 

#### Page

optimisation lecture/ecriture, les VHD sont stoqyés via des blogs

#### types de stockage

minimum 3 replicas

LRS => une region mais 3 replicas

ZRS => 3 repliques sur des zone de stockage différentes
  - lattence car réplication synchrones
  - replication synchrone

GRS (globaly redundant storage)
  - 3 copies dans chaque region
  - 

RA-GRS 
  -  idem mais avec copie en read only

GZRS

### Chaud/Froid/Archive

- 
- les opérations sont plus couteuse sur du stockage archive
des copies sont possibles en automatique (lifecycle policies)

#### Entetes 
manipuler/lire les métadonnées passent par des métadonnées
préfixer par x-ms-meta-*
ex : x-ms-meta-name

- etag
- lastmodified
- public access
- hasimmutability policy
- haslegalhold

### Api

CloudBlobClient client = sorageAccount.CreateCloudBlobClient();

````
dotnet new console --name BlobManager --output .
````

### Cosmos DB

Déployable sur les site du monde entier
Strong :
- Strong intégrité maximium, sur ecriture => synhcro dans toutes les régions
  - petite latence possible avec 15 ms max
- staleness => replication asynchrone
- Session synchronisations continue sur un seul réplicat, les autres réplicats sont synchronisés plus tard
- Utilisation d'un API au choix

structure des données
compte CosmosDB => API
changement d'API => changement de compte

container => collection => (schema bdd?)

RequestUnit/s => 1 ko dans une table => RU
partition à partir de la clef de partition

throughput => RU

héritage possible Base => container

Procédures stoquées en javascript

false => rollback
true => commit

### Transaction continuation

semble être interressant pour les batchs

Udf : user defined functions
ex : 
definition de fonction
udf.tax(t.income)


### IAAS

#### Provisionning

#### nom de VM
- environnement
- localtion instance
- product service
  
prendre en compte 
- Cout de la virtualisation
- cout du staockage
  
disques gérés et non gérés, 
- gérés => azure gère les disques
- non gérés => vous gérer les disques

Availibility set
- fault domains : hyperviseurs différents/serveurs différents => pane hardware
Update domain
- protéger contre les mise à jour logicielle

Microsoft assure qu'il va faire les mise à jour par update domains

#### Galerie d'images

définir les zones ou sont utilisées les VM

#### Groupe de ressource

Template ARM

possibilité de faire un template parent qui inclu les templates
Automation script

### Rappel Virtualisation

VM => 1 noyeau pour l'os, 1 noyeau pour la VM => gachi
Docker => utilise le noyeau de l'hôte

ex : 

docker pull ubuntu
docker pull mysql:5.7
docker pull nginx:lastest
docker pull mcr.microsoft.com/donet/code/samples:dotnetapp
docker run mcr.microsoft.com/donet/code/samples:dotnetapp

docker container ls -a

docker build dans le dossier dans lequel il ya le docker file

### ACR

en mode premium possibilité de dupliquer les images sur plusieurs region

az acr create
az acr login --name <acrName>

l'image doit être retaggée avant le push

déployer une image =>

az container create

pour la persistence => possibilité d'utiliser des files shares

communications entre containers => utiliser un groupe de container


### Authentification

Azure AD

synchronisation
anciennement => bibliothèque ADAL sur du Azure AD uniquement
remplacé par MSAL mais sur des environnements plus nombreux (interconnexion)

string renant = "contoso.onmicrosoft.com"

compte fédéré => passer par MSAL

authentification pour utilisateurs et pour un compte de service possible

Managed acount => identité géré interne à azure (pour les ressources azure uniquement)
- pas besoin d'information d'authentification
- vérification de la ressource
- pas forcement toutes les ressources (mais la plupart quand même)

sur plusieurs tenant

utiliser le tenant "common"

#### authorization grant
deux endpoint

#### implicit grant
un seul endpoint (appli SPA)

- Interactive
  - redirige l'utilisateur vers un formulaire
- On-Behalf-of
  - l'application s'authentifie
  - pas d'interface passer les infos d'authentification p
- Client credentiel
  - l'application est authentifiée, pas l'utilisateur, pas d'interractions
- Device code
  - L'utilisateur s'authentifie à partir d'un autre device, ouverture de l'URL, le Token est délivré à l'appareil seul
  - authorisation du nouvel appareil par un autre appareil déjà authentifié
- authentification par certificat
  - installation du certificat sur la machine avec l'app registration
  

MSAL
- Authorization code pour une seule application
- Device code toutes les applications
- implicit => reprendre les informations précedentes pour authentifié automatiquement (si possible et auth déjà dans le navigateur) 
- 

### Microsoft Graph 

permet d'accéder à la plateforme office 365 avec un seul SDK ou API rest plustôt que un SDK pour chaque

google => graph explorer, tests des API online
test sur un jeu de données fictif

avantage du SDK => simplification de l'utilisation de l'API
package Microsoft.Graph et Microsoft.Graph.Auth

#### Api Fluent

GraphServiceClient = new GraphServiceClient( authProvider );
User me = await graphClient.Me.Request().GetAsync();


### Authorization compte de stockage

policy associée au container

CORS permet le CROSS Origin RessourceSharing pour éviter de partager (sansn consentement) à un autre domaine

Authorizatoin par tokendans chaque requette
possibilité d'utilisation d'une shared key (par date)

Shared Key ou Shared Access Signature
les clef utilisées jusque ici donne un compte admin, ne pas donner aux End Users
SAS Token => sélection de ressource , définir de manière granulaire les authorization du compte de stockage

permission sur les fichiers, combiner SAS et stored access policy

association d'une stored access policy à plusieurs SAS


### Managed identities

user assigned managed identity => securité renforcée
system assigned managed identity => autant de managed identity que d'application

az web app identity assign --name <app-name> --resource-group <resource-group>

az container create --assign-idendity

user assign :

az identity create
az container create --assign-idendity $id


### apps settings
### Feature management

### Api management (APIM)

aide pour publication d'API
throttling => limition des requettes

- API Backend
- API Frontend => proxy pour le front
- Product => moyen de packager une ou plusieurs API

- Revision => pas de changement de l'interface vers l'API
- Version => changement de l'interface vers l'API

Hierarchie possible pour les policies
dans les policies
<base /> permet d'utiliser la policie parente


### Application Gateway

L7 LoadBalancer => travailler sur le protocole HTTP et pas uniquement la couche 4 IP
- custom routing : redirection à partir de l'URL
- Session afinity : plusieurs sessions par utilisateur => reconnecter au même serveur est possible
- SSL Termination : possibilité de passer en http derière la gateway


### Subscriptions

permet de séparer les parties de l'API, d'authentifier un utilisateur et ou Authoriser un utilisateur
il est aussi possible d'utiliser un certificat pour l'authentification

### Event Grid

event-driven architecture

custom topics pour des évenements custom
Generation d'event sources (messages)
chaque message à un schema
data : payload libre
handler authentifié par son abonnement
filtre possible sur un abonnement de topics ex filtrage sur le champ "eventType"
filtrage avancé possible
publier nos propres évenements

az eventgrif topic create
az eventgrid event-subscription create

pour publier dans plusieurs topics possibilité de créer un Event domain endpoint pour publier dans plusieurs topics à partir d'un seul et même endpoint

### Event Hubs

acquisition de données en streaming
agréger plusieurs dizaine de millions de message à la seconde
gestion par partition
groups de consomateurs sur un event hub ou sur une partition d'un event hub

pas de messages de plus de 7 jours, pour les rendres persistents => activer la Capture
une fois consomé le message est perdu, pour refaire un traitement il faut les persister autre part que dans l'event hub
Utilisation de Kafka

accès au hub

### Notifications hub

enregistrement de l'appareil
gérer et automatiser les notifications
identifier les appareil à notifier
créer des templates
Gérer l'accès au notification hub via un SAS security
Gérer les messages à l'aide de templates utilisation d'un pseudolanguage
Utilisation de tags pour regrouper les devices


### 
https://<stor-acount>.queue.core.windows.net/<queue>


### logging/monitoring

Azure monitor n'est pas vraiment un composant mais un dashboard

journaux globaux mais filtrés quand on n'est positionné sur la ressource
il est plus facile de rester sur la partie globale

3 catégorie :

- Unified monitoring
- Data driver insights (métriques)

### Alertes

- surveiller une ressource
- condition d'alerte
- action suite à l'alerte

### Application insights

Monitoring d'applications

utilisation d'un snipet (customisatble) javascript pour activer le monitoring
il existe egalement des API et un SDK 

utilisation d'une clef
var telemetryClient = new TelemetryClient();


utilisation possible d'elasticsearsh 
utilisation datadog

#### Application map

possibilité de définir un nouveau composant
soit de le faire en XML ou en dotNet

requetter les données via le powershell est possible


### Transient errors

temporary faults
ils sont généralement résolues plus tard de façon autonome
prendre en compte ce genre d'erreur, latence etc ...
- Cancel => annulation de l'action tant que ça ne fonctione pas
- Retry / retry after delay

ex d'erreur transient


### Cache Redis

cache distribué => solution de cache accessible par l'enssemble des serveurs
SPOF => single point of failure

utilisation d'outils en ligne decommande

### CDNs (content delivery networks)

fichiers statiques associés aux sites web optimisation
POP => un serveur disponible au près d'un utilisateur, diminuer la distance entre utilisateur et ressource par un pop

regles de cache globales
regles de caches particulieres
possibilité de précharger le cache


