# ArtPS - Art Positioning System

## Prototype:

ArtPS is a global registry of publicly accessible art pieces.

Those works can manifest themselves digitally, materially,
or not manifest themselves at all.

By providing artists a platform that connects places with their art,
ArtPS provides a new type of interaction with both art and public spaces.

## Sitemap:
* / => worldmap and small widgets with xx organizations, artists, artworks each.
* /map/ => full screen map no fuzz
* /artists/ => artist registry

* /artist/ => single artist profile entry, no content
* /artist/${name} => single artist profile



## pages:

### index:
* worldmap with markers for each artwork

### Single:
`/artist/${name}/${workslug}`

#### data:
  * id
  * title
  * slug (from title)
  * text
  * images
  * link
  * 3d object
  * video

### Artist profiles

`/artist/${name}/``

#### data:
* title
* text
* image
* link

### Artist Artwork List

`/artist/${name}/art/`

list of artworks of this artist


### Artist Organization / Collaboration List

`/artist/${name}/collab/`

#### data
* list of organizations of this artist
  * title
  * link
  * short text
  * small img

* list of artists that share projects with this artist.
  * title
  * link
  * short text
  * small img

### Organization Profiles:

`/org/${name}/`

#### data:
* title
* text
* image
* link

  * /org/${name}/artists/
    * list of all artists in this org
  * /org/${name}/art/
    * list of all artworks tagged with this org
