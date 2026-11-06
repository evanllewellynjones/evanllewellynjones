# evanllewellynjones.com — Site Project Notes

Started: October 9, 2026
Owner: Evan Llewellyn Jones

## Purpose

Personal site on a custom domain, built as static HTML pages served from a GitHub repo through GitHub Pages. The first page is the Alaska 2027 trip itinerary. More pages to follow.

---

## 1. Domain

| Item | Detail |
|---|---|
| Domain | `evanllewellynjones.com` |
| Registrar | Namecheap |
| Nameservers | Namecheap BasicDNS |
| Purchased | Oct 9, 2026 |

To do at Namecheap:
- [ ] Turn on auto-renew
- [ ] Confirm WHOIS privacy (free at Namecheap) is on

Registrar notes: Cloudflare and Porkbun are cheaper at renewal. Namecheap is fine. Avoid registering domains through Wix, Squarespace or GoDaddy, which charge more at renewal and tie the domain to their site plans. The domain can be transferred later if needed.

---

## 2. DNS records (Namecheap → Domain List → Manage → Advanced DNS)

Removed the Namecheap defaults:
- URL Redirect Record on `@` (Unmasked, to `www`)
- CNAME `www` → `parkingpage.namecheap.com`

Records added (6 total):

| Type | Host | Value | TTL |
|---|---|---|---|
| A Record | `@` | `185.199.108.153` | Automatic |
| A Record | `@` | `185.199.109.153` | Automatic |
| A Record | `@` | `185.199.110.153` | Automatic |
| A Record | `@` | `185.199.111.153` | Automatic |
| CNAME Record | `www` | `evanllewellynjones.github.io.` | Automatic |
| TXT Record | `_github-pages-challenge-evanllewellynjones` | `8484251967db77b790a870a53b2833` | Automatic |

Optional IPv6 (AAAA records, Host `@`):
`2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153`

What each does:
- **A records (`@`)** point the bare domain at GitHub Pages' four servers. Four for redundancy.
- **CNAME (`www`)** makes `www.evanllewellynjones.com` work. GitHub redirects between `www` and the bare domain automatically.
- **TXT (`_github-pages-challenge-…`)** proves to GitHub that the domain is ours and stops anyone else from claiming it on GitHub Pages.

Namecheap tip: in the Host field, enter only the part before the domain. Namecheap appends `.evanllewellynjones.com` itself.

Check propagation:
- `dig evanllewellynjones.com +short` → should return the four `185.199.x.153` addresses
- Or dnschecker.org (A record for the domain; TXT record for `_github-pages-challenge-evanllewellynjones.evanllewellynjones.com`)

---

## 3. GitHub

| Item | Detail |
|---|---|
| GitHub user | `evanllewellynjones` |
| Hosting | GitHub Pages |
| Pages source | Deploy from a branch → `main` → `/ (root)` |
| Default URL | `https://evanllewellynjones.github.io/<repo-name>/` |

Steps:
1. [ ] Verify the domain: GitHub profile → Settings → Pages → Add a domain → `evanllewellynjones.com` → **Verify** (after the TXT record propagates)
2. [ ] Upload `index.html` to the repo root and commit
3. [ ] Repo → Settings → Pages → Source: `main` / `(root)` → Save
4. [ ] Repo → Settings → Pages → Custom domain: `evanllewellynjones.com` → Save (creates a `CNAME` file in the repo; keep it)
5. [ ] Tick **Enforce HTTPS** once the DNS check passes (certificate can take up to 24 hours)

Notes:
- On the free GitHub plan, the repo must be **public** for Pages to work. Anything in it is readable by anyone.
- Every `.html` file in the repo becomes a page: `alaska.html` → `evanllewellynjones.com/alaska.html`. `index.html` is the home page.
- Reference docs: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site

---

## 4. Repo contents

```
/
├── index.html   # Alaska Rail & Fjords 2027 itinerary, v2 (current home page)
└── CNAME        # contains: evanllewellynjones.com
```

`index.html` is a single self-contained file:
- v2 uses an inline SVG route map (v1 embedded a base64 Google map image)
- Only external dependency is Google Fonts (Big Shoulders Display, IBM Plex Sans, IBM Plex Mono)
- Light and dark mode supported; works at phone width

Version history:
- **v2 (current), Oct 31, 2026:** Fairbanks-in itinerary with a luxury audit. Project doc `index.html`; artifact version `1793457524-9d4b`.
- **v1 (archived), Oct 10, 2026:** Anchorage-in itinerary. Still kept in the artifact's version history as `1791595621-53ef` ("Alaska Rail & Fjords 2027" artifact). The route and open items are preserved in section 6 below.

---

## 5. Page 1: Alaska Rail & Fjords 2027 — v2 (current)

Trip: Aug 19 – 28, 2027 (home Aug 29)
Travelers: Evan & Dylan (from RDU), Morgan (from New York)
Source: itinerary doc "19 Aug 2027" (docx), Oct 31, 2026

Sections on the page:
1. Header with trip facts and traveler origins
2. Schematic route map (SVG) and a nights list
3. Day by day, Aug 19 – 28, with times and flags
4. Luxury audit: each item vs. the top option, with a call
5. Stays (6 cards)
6. Flights
7. Open items
8. Links

Route summary:

| Dates | Where | How |
|---|---|---|
| Aug 19 | Fly RDU → Fairbanks; 1 night | Daytime 1-stop flight; Pike's Waterfront Lodge (proposed, not in source doc) |
| Aug 20 | Fairbanks → Denali | Denali Star GoldStar, 8:20 AM → 12:10 PM; afternoon ATV tour |
| Aug 20 – 22 | Denali (2 nights) | Grande Denali Lodge; Aug 21 heli-hike + 5 PM off-trail hike |
| Aug 22 | Denali → Anchorage | Denali Star GoldStar, 12:30 PM → 8:00 PM; Hotel Captain Cook |
| Aug 23 | Anchorage → Seward | Coastal Classic GoldStar, 6:45 AM → ~11:05 AM; 2 PM Bear Glacier kayak; Harbor 360 Hotel |
| Aug 24 – 26 | Kenai Fjords Glacier Lodge (2 nights) | Lodge boat 10 AM from Seward (4–5 h cruise) |
| Aug 26 | Seward → Anchorage | Lodge boat back ~5–5:30 PM; Coastal Classic 6:00 PM → 10:15 PM; Wildbirch Hotel |
| Aug 27 | Bear-viewing flight | Floatplane to Lake Clark (Crescent Lake); Wildbirch Hotel |
| Aug 28 | Food & history tour, fly home | Late-afternoon or red-eye; day doubles as bear-flight weather backup |

Conflicts found in the source doc:
- No hotel listed for Aug 19 in Fairbanks.
- Salmon fishing on Aug 25 doesn't fit at the Glacier Lodge (about 50 miles by water from Seward; program is kayak, canoe, hike).
- The Aug 26 afternoon Anchorage food/history tour can't happen (back in Anchorage 10:15 PM). Moved to Aug 28 morning.
- The Aug 23 2 PM kayak works: about 2.5–3 hours of slack after the train.

Luxury upgrades recommended:
- First class both ways; daytime routing into FAI.
- Grande Denali cabin or a canyon-view room.
- Captain Cook Crow's Nest Suite; Crow's Nest dinner on Aug 22.
- Harbor 360 Deluxe King Harbor Balcony room.
- Private floatplane charter for bears (e.g., Alaska Bear Adventures, $4,695 for up to 5).
- Optional: heli-kayak at Bear Glacier.
- Consider the Captain Cook instead of Wildbirch for Aug 26–28.
- Not recommended: Sheldon Chalet (~$32k/night exclusive-use; would replace the whole Denali plan).

Open trip items (v2):
- [ ] Book Fairbanks hotel (Aug 19) and a daytime flight landing by early evening
- [ ] Book GoldStar on all four rail legs; confirm 2027 times
- [ ] Decide on salmon fishing: swap Aug 23 kayak for a private Seward charter / ask the lodge about a pickup / drop it
- [ ] Pick a return flight that allows the Aug 28 morning food tour (late PM or red-eye)
- [ ] Book the private Lake Clark charter for Aug 27; hold Aug 28 as weather day
- [ ] Decide Wildbirch vs. Captain Cook for Aug 26–28
- [ ] Ask the Glacier Lodge about luggage limits on the boat
- [ ] Book limited room categories early (Grande Denali cabin, Crow's Nest Suite, Harbor 360 balcony)

---

## 6. Archived: Itinerary v1 (Oct 10, 2026) — Anchorage in

Kept for reference. The full v1 page is in the artifact version history (`1791595621-53ef`).

Trip: Aug 19 – 29, 2027
Travelers: Evan & Dylan (from RDU), Morgan (from New York)

Route summary (v1):

| Dates | Where | How |
|---|---|---|
| Aug 19 | Fly to Anchorage (arrive 12:53 AM Aug 20) | Delta via MSP |
| Aug 19 – 21 | Anchorage | Hotel Captain Cook or Anchorage Marriott Downtown |
| Aug 21 | Anchorage → Denali | Alaska Railroad Denali Star, GoldStar |
| Aug 21 – 24 | Denali (3 nights) | Grande Denali / Denali Princess / Denali Bluffs |
| Aug 24 | Denali → Seward | Air taxi charter |
| Aug 24 – 27 | Kenai Fjords (3 nights) | Kenai Fjords Wilderness Lodge / Seward Windsong / Tutka Bay |
| Aug 27 | Seward → Anchorage | Coastal Classic, GoldStar |
| Aug 28 | Fly home, arrive Aug 29 | Delta First |

v1 flights:
- Evan & Dylan out: RDU 7:15 PM → ANC 12:53 AM (+1), Delta via MSP (32-min connection), MSP–ANC DL1148
- Morgan out: New York ~4:15 PM → MSP → ANC 12:53 AM (+1), same MSP–ANC flight
- Return Aug 28: ANC 1:15 PM, Delta First, arrive RDU 11:09 AM / JFK 11:25 AM Aug 29 (~18 h with overnight connection)

v1 activities: Anchorage Museum day; Denali hike / Nenana River float (Denali Raft Adventures) / flightseeing (Denali Air, TEMSCO, K2 Aviation); Kenai Fjords cruise (Kenai Fjords Tours, Major Marine), Sunny Cove kayaking, Exit Glacier Guides, silver salmon with Miller's Landing.

v1 open items (superseded):
- Book Anchorage hotel from Aug 19 for the 12:53 AM arrival
- Find a longer MSP connection than 32 minutes
- Compare a red-eye for the return
- Denali → Seward charter: Denali Air is flightseeing only; Kantishna Air Taxi status unconfirmed
- Choose Kenai Fjords lodge (Wilderness Lodge 2-night packages; 25% off if booked by Jan 15, 2027; Tutka Bay is near Homer, not Seward)
- Hold a Denali room Aug 21 – 24
- Book GoldStar on both trains
- Book park bus when the 2027 Reserve Denali system opens

---

## 7. Next steps for the site

- [ ] Finish DNS verification and HTTPS
- [ ] Decide site structure: move the itinerary to `alaska.html` (or `/alaska/index.html`) and make `index.html` a home page
- [ ] Decide what else goes on the site (bio, teaching, investing, art and antiques, travel)
- [ ] Decide what should stay private. A public repo exposes everything; consider a private repo with a paid GitHub plan, or Cloudflare Pages with Cloudflare Access for login-protected pages
- [ ] Add a favicon and basic meta tags (title, description, social preview image)
