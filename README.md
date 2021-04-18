# quillandcup-stripe

This repo contains static assets that enables a simple Stripe Checkout based
workflow on Google Sites.

### Motivation

We tried embedding the `stripe.redirectToCheckout()` javascript directly in Google Sites
but it doesn't work. An `embed` creates an iframe without permission to redirect the
top-level page, resulting in this error:

```
Unsafe attempt to initiate navigation for frame with origin 'https://sites.google.com'
from frame with URL 'https://926174618-atari-embeds.googleusercontent.com/embeds/16cb204cf3a9d4d223a0a3fd8b0eec5d/inner-frame-minified.html?jsh=m%3B%2F_%2Fscs%2Fapps-static%2F_%2Fjs%2Fk%3Doz.gapi.en.RrjSsKk8Szw.O%2Fam%3DAQ%2Fd%3D1%2Fct%3Dzgms%2Frs%3DAGLTcCPwd_oodKkRT_hYRO1I-9xRcQV4oQ%2Fm%3D__features__'.
The frame attempting navigation of the top-level window is sandboxed, but the flag of
'allow-top-navigation' or 'allow-top-navigation-by-user-activation' is not set.
```

This [StackOverflow article](https://stackoverflow.com/questions/59823605/form-redirecting-in-new-google-sites)
says that New Sites on Google Sites explicitly don't allow this, while Classic Sites did.

> There isn't anything here that can be done as long as you are working with New Sites.

### Usage

This repo is expected to be hosted as a static asset somewhere (e.g., Github Pages).
Then we can use a normal `<button>` linking to this HTML document in the Google Site.
When clicked, this will open a [new tab](#new-tab) with this page (after a brief 
[flash](#white-flash)), which will immediately call `stripe.redirectToCheckout()` to
open Stripe Checkout for you.

### Known Issues

#### White Flash

Unfortunately, the Google Sites links always redirect through Google to detect malware.
This causes a white screen flash which can be somewhat confusing and disorienting to
the user. This is an [intentional](https://support.google.com/sites/thread/3085407?hl=en)
design choice from Google with no workaround.

#### New Tab

Unfortunately, the Google Sites links always open a new tab rather than redirecting the
current page, like most links do. As far as I can tell, there's no way to override this
behavior in New Sites.

1. https://stackoverflow.com/questions/61242432/open-google-sites-html-links-in-same-window
2. https://support.google.com/sites/thread/6878509?hl=en
