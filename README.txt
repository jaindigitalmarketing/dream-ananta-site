DREAM ANANTA LANDING PAGE - HOSTING PACKAGE
============================================

Upload EVERYTHING in this folder (keep the folder structure) to the web root
of the domain or sub-folder where the page should live.

  index.html                      Landing page (responsive: desktop + mobile)
  thank-you/site-visit/index.html Thank-you page after the site-visit form
  thank-you/enquiry/index.html    Thank-you page after the Enquire form
  thank-you/brochure/index.html   Thank-you page after the brochure form
  assets/images/                  All photos, floor plans, map and logo
  assets/js/dc-runtime.js         Page engine (required - do not delete)

All links are relative, so the site works at the domain root or in a sub-folder.
It is plain static files: any server works (Apache, Nginx, IIS, cPanel,
Netlify, S3, etc.). No database or PHP needed.

BEFORE GOING LIVE - edit the settings block near the top of index.html
---------------------------------------------------------------------
  window.DREAM_ANANTA_CONFIG = {
    leadEndpoint: "",        <- REQUIRED. URL that receives leads (JSON POST)
    brochureUrl: "",         <- link to the brochure PDF
    thankYouBase: "thank-you"
  };

1. leadEndpoint
   While this is empty the three forms DO NOT SEND leads anywhere: visitors
   see a "Preview mode" note instead. Set it to your CRM / webhook URL
   (e.g. RealtyBucket, Zapier, Make or your own API). Each lead is sent as a
   JSON POST with: intent, name, mobile (+91...), email, preferred_config,
   consent, consent_text, consent_at, project, page_url, referrer,
   utm (utm_source, utm_medium, utm_campaign, ...), idempotency_key.
   The endpoint must allow CORS from your domain and return HTTP 200.
   After a successful submit the visitor is sent to the matching thank-you
   page (thank-you/site-visit/, thank-you/enquiry/ or thank-you/brochure/).

2. brochureUrl
   Put the brochure PDF on the server (e.g. assets/brochure/dream-ananta.pdf)
   and enter that path. Set the same value in thank-you/brochure/index.html
   so its "Open Brochure" button appears.

TRACKING
--------
The page pushes events to window.dataLayer: generate_lead, site_visit_request,
visit_cta_click, enquire_click, floorplan_view, brochure_download,
directions_click, phone_click, whatsapp_click and (on the thank-you pages)
thank_you_view. Add your
Google Tag Manager / Meta Pixel snippet to the <head> of each index.html and
map these events there.

Fonts load from Google Fonts; everything else is served from this folder.
