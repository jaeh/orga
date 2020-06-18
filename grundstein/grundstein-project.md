# grundstein:

for now, all services below run on one pod on digitalocean.

in the saturated production environment, every service below runs on one or multiple pods in one or multiple clouds,
connected by load balancers and tcp/udp.

each of the services will have to assume this to be true right now too.
* no internal networking.
* every service get's it's own share of the disk and does not share it with other services.
* shared/connected storage can be achieved using volumes on digitalocean for now, but those should be replaced by a separate service soon.
* cdn can be achieved using the digitalocean cdn, but should be replaced by a native cdn solution.

### minimal lock in to digitalocean.
whereever necessary and possible, services will be built as if they are disconnected machines located anywhere, cross-cloud.

---------------------------------------------

## servers

the following section describes the various services grundstein needs to function.

some of them are public, some are private and internal, some are both.

---------------------------------------------

#### gps -> gps.grundstein.it

##### grundstein positioning service / grundstein proxy service

https://github.com/grundstein/gps/

this is the central service.

provides a list of all running services.

this list is static for now, but there will be an api providing functionality to add/remove/scale services.

##### done
* exports list of hosts and their hostname/port pairs.
* serves that list of hosts on http requests (catch all)

##### todo:
* ##### load balancer & proxy service.
  route requests to gss, gas, gis, gcs services,
  based on hostname.

----------------------------------------------

#### gcs -> certificate service
cert.grundstein.it

https://github.com/grundstein/gcs/

generate letsencrypt certificates for all services.

generate internal https certificates and distribute them to the various services.

serve the .wellknown/acme-challenge letsencrypt responses

##### done:
none

##### todo:
* ##### startup:
  * generate certificate authority.
  * generate certificates for every host in @grundstein/gps.
  * once done, start @grundstein/gps service using the cert.

---------------------

#### grs -> redirection service

serves .well-known for letsencrypt certificates and all hosts.

redirects all other requests to https.

##### done
none

##### todo:
all.

------------------------------

#### gms -> yourdomain.com

https://github.com/grundstein/gms

serves magic page static files from memory

##### done:
* serves static magic pages from memory.
* immutable store.

##### todo:
* only serve js, css, html, txt, and favicon.ico, other files will get served by gss.

---------------------------------------------

#### gas -> api server -> api.yourdomain.com
https://github.com/grundstein/gas

serves magic apis.

##### done:
* serves apis from dir.
* gets port from gps.

##### todo:
* serve multiple hostnames

-------------------------------------------------

#### gss -> static server -> static.yourdomain.com

serves static files like images, videos etc from cdn store.

separated from html/css/js server for perf reasons.

use digitalocean cdn for now, looks good enough,
use api to write files to cdn.

keep old versions around until they get deprecated.

##### done:
nothing.

##### todo:
all.

-------------------------------------

#### ghs -> health service
pings all hosted pages and all their resources in regular intervals.

logs and notifies on errors.

shows status pages for all hosted properties.

##### done:
none

##### todo:
all

--------------------------------------

#### auth -> login service -> auth.yourdomain.com

central auth provider

gets pgp signed messages, answers with a jwt.

this jwt stays valid for 10 minutes (by default). (can be 1, 2, 6 hours or 1, 5, 10 minutes)

##### done:
none

##### todo:
all

-----------------------------------------

#### gbs -> build.grundstein.it

build service.

gets triggered by file watcher on changes in repositories.

actually clones those repositories, builds them, then pokes gps to get the new versions registered

##### done:
none

##### todo:
all

---------------------------------------

#### gul -> universal logger -> gul.grundstein.it

opens a post url for incoming logs. never answers.

shows a list of log entries for your hostnames

##### done:
none

##### todo:
all

---------------------------------------

#### gvs -> staging and versioning service - staging.grundstein.it

manages magic network internal versioning (staging environment)

watches all repositories

builds staging versions on push to those repositories

make staging versions available at githash.staging.grundstein.it

##### done:
none

##### todo:
all

----------------------------------------------

#### gmgt -> management
admin.grundstein.it

html ui to:
* connect domain
* connect git
* show admin interface for config and pages.
* use staging to show life preview.

##### done:
none

##### todo:
all

-----------------------------------------

#### gfw -> file watcher

watches git repositories for each host and pulls changes if they exist.

then notifies the staging service to build those branches and serve them via staging.yourdomain.com

##### done:
none

##### todo:
all

----------------------------------------------

## clients

#### browser extension

password protected input to add/delete pages and associated public pgp keys.

authenticate the user against auth.grundstein.it,
using those keys.

write the jwt to javascript window.MAGIC_JWT global.

find a way to not need the private key in the browser extension.

##### done:
none

##### todo:
all

----------------------------------

#### authenticator

cli and standalone app that connects to pgp keys locally and signs a message, gets a jwt in return.

this has to be run once per user per key per action/session.

in return,
the homepage will not require any authentication features.

to provide ease of access, email+pass/github/gitlab/facebook/google etc logins should be provided, but those accounts should basically only access the public profile data by default.
admin capability of those accounts has to be opt-in,
pgp key backed admin is the preferred approach.

the homepage should regularily nag people to install the authenticator app and remove the admin capability from their online account.

---------------------------------------------

#### external dependencies:

https://github.com/openpgpjs/openpgpjs
...


#### questions re: digitalocean

* can we set shared volumes on read-only for some of the sharers
* how do we access the shared volumes, which path are they mounted at


-------------------------------------------

init script:

2 versions:

development:
gets triggered if the only host is 127.0.0.1,
setting up the whole chain via a docker container instead of running through digitalocean.

production:
for each ip in hosts array,
ssh to the server and run grundsteinlegung.sh.

bonus: do in parallel and show multiple windows with progress.


grundsteinlegung, run once for each host:

apt install of common dependencies

add grundstein user(s)

install certbot and setup domains


services.sh

install services and run them

