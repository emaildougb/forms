# NCEMS Forms

Write ups, quick notes and SOG drafts for the CG Staff, plus a personnel search. Makes a Word file in the agency's own format and files it on the CG Staff SharePoint site.

**Version 1.1**

## Links

- Live: [https://forms.northcountryems.org/](https://forms.northcountryems.org/)
- Demo (sample data, nothing saves): [https://forms.northcountryems.org/?demo=1](https://forms.northcountryems.org/?demo=1)
- Repo: [https://github.com/emaildougb/forms](https://github.com/emaildougb/forms)
- Upload: [https://github.com/emaildougb/forms/upload/main](https://github.com/emaildougb/forms/upload/main)
- CG Staff site files: [Personnel Files](https://northcountryemsorg.sharepoint.com/sites/BattalionChiefLocal/Shared%20Documents/Personnel%20Files) · [Forms Reference](https://northcountryemsorg.sharepoint.com/sites/BattalionChiefLocal/Shared%20Documents/Forms%20Reference)

## Files (upload ALL of these)

- `index.html`: the app
- `base-memo.docx`: the letterhead template for write ups (NCEMS logo, PO Box 189 Yacolt address). Body is empty; the app fills it in
- `base-sog.docx`: plain page template for SOG drafts (1 inch margins)
- `logo.png`: NCEMS round logo
- `apple-touch-icon.png`, `icon-512.png`: home screen icon
- `manifest.json`: home screen name "Forms"
- `CNAME`: forms.northcountryems.org
- `README.md`: this file

The policy manual and the CBA are NOT in this repo on purpose. GitHub Pages files are public, and the manual is Lexipol's copyrighted text. The app reads them from the CG Staff SharePoint site after you sign in: `Forms Reference/policy-manual.md` and `Forms Reference/cba.md`. To update either one, replace the file in that folder with the same name.

## One time setup

1. GitHub: new **public** repo named `forms` under emaildougb. Upload every file in this folder
2. Repo Settings > Pages: Deploy from a branch, `main`, `/ (root)`, Save
3. GoDaddy DNS for northcountryems.org: Type `CNAME`, Name `forms`, Value `emaildougb.github.io`, TTL 1 hour
4. Back in Settings > Pages, once the DNS check goes green, tick **Enforce HTTPS**
5. **Sign in setup (Entra).** Forms uses the same Microsoft app registration as CG Staff, so it needs one more redirect address:
   - Go to entra.microsoft.com > Applications > App registrations > All applications
   - Open the one with Application (client) ID `254c214f-bfe2-4ebb-9294-99815e167ab0` (the CG Staff / Facilities and Grounds app)
   - Authentication > under **Single-page application**, Add URI: `https://forms.northcountryems.org/`
   - Save
6. **Lock the Personnel Files folder (important).** The app hides personnel search from anyone not on its chiefs list, but the real lock is the SharePoint permission. Anyone who is a member of the CG Staff site can open that folder in SharePoint unless you change it:
   - The folder is made automatically the first time something is filed. To set it up ahead of time, go to the CG Staff site > Documents and make a folder named exactly `Personnel Files`
   - Click the folder's ... > Manage access (or Details > Manage access) > Advanced settings > **Stop Inheriting Permissions**
   - Remove everyone who should not see personnel files. Leave the chiefs (and HR if you want)
7. Open https://forms.northcountryems.org/ and sign in. Try the demo first if you want to see it without filing anything

## How it works

- **Who gets in:** the same 7 people as CG Staff (`CONFIG.staff`). Everyone else sees "CG Staff only" with a link back to the hub
- **Who can search and file personnel records:** `CONFIG.personnel` (Doug, Derek, Dennis, Bryce, Chuck). Kim and Nick can make SOG drafts and use the policy search but do not see personnel files
- **Name and title on the FROM line and signature:** `CONFIG.signers`, filled from whoever is signed in. Editable on each form
- **Forms:**
  - Quick Note: small note, Positive, Concern or FYI. Saved as a short text file in the employee's folder. Not a coaching
  - Documented Coaching: intro, topics, follow up tasks, closing, optional signature lines. Has a Copy as email button
  - Written Verbal Reprimand and Written Reprimand: Policy 1053.4 opening, concerns, pattern, prior steps, standards, violated policies (quoted wording added for you), expectations, notice
  - Corrective Action Plan: Short (plain language, like the Mraz CAP) or Detailed (data, requirements table, actions with measures, like the Komm CAP). Plan end date and check in weeks fill in from the start date. The Fire Chief approval line is always on (Policy 1053.5)
  - SOG Draft: the house SOG format (title, agency line, gray header table, 1.0 Purpose, 2.0 Scope, numbered sections, References, Appendices, Issued by line, Draft vN)
- **Find a policy:** describe the problem in plain words. It searches every section of the policy manual and the CBA, counting EMS words that mean the same thing (charts, PCR, documentation). Tap Add to put it in the form. No AI
- **AI assist / AI review buttons:** placeholders, labeled "Not connected to AI yet". Copy for Claude copies the draft plus a review prompt to paste into your own Claude
- **Review step:** before making the file it flags placeholders left in [brackets], missing dates, no policy cited, expectations without deadlines, and for a CAP the parts Policy 1053.5 requires
- **Make Word file:** downloads the .docx and (if the box is ticked) files it in `Personnel Files/Last, First/` named `YYYY-MM-DD Type - First Last.docx`. SOG drafts can be filed in `SOG Drafts`
- **Nothing is kept in the app or the browser.** Leaving a form throws it away (the app asks first)
- **Search:** by employee name, plus a search inside every filed document (SharePoint search, so brand new files can take a few minutes to show up)
- **Employee page:** everything filed for that person, newest first, quick notes shown in full, Open goes to the Word file in SharePoint. Upload old file adds past write ups and renames them so they sort by date

## Changelog

### v1.1
- Back works one page at a time: the browser back button, the phone back swipe and the Back buttons all go Review > last step > earlier steps > Forms home, and employee page > Search > home. Back no longer drops you out to the Microsoft sign in page. Backing out of a form's first page asks before throwing it away
- New first box on the "what happened" page: Start here, general ideas and questions. Matching policies show up under it as you type (each piece of the notes is searched on its own) with Add and Read buttons. Export to your Claude copies the notes, what is in the form so far, and the full wording of the matching policy and CBA sections, with a prompt to help write the opening
- The Find a policy search stays as is, now with Both / Policy manual / CBA buttons
- Bargaining unit box for Lead Paramedic and Part-Time Lead Paramedic (CBA Article 1.1) on reprimands and CAPs: CBA items to review before issuing discipline (Articles 1.1, 6, 14, 20, 5, 25, 23, 24) with Add and Read, plus the Weingarten reminder. Added items print under "Collective Bargaining Agreement (IAFF Local 452)". The review step reminds about the union rep and the 30 day grievance window
- Positions: Lead Paramedic, Part-Time Lead Paramedic, Crew 2 Paramedic, Full-Time EMT, Part-Time EMT, Volunteer PMA (Paramedic Assistant). Still free typing
- Documented Coaching: Email it button opens your email app addressed to the employee (first initial.last@northcountryems.org, editable), optional CC to the Fire Chief and BCC, subject and text filled in
- Search hint says "Name, like Langdon". Links to the Personnel Files folder and the CG Staff documents in SharePoint on the home and search pages
- Short CAP prints any policies you added under "Applicable policy"

### v1.0
- First version: Quick Note, Documented Coaching, Written Verbal Reprimand, Written Reprimand, Corrective Action Plan (Short and Detailed), SOG Draft
- Policy search over the manual and CBA from SharePoint, AI placeholders, Copy for Claude, review checklist
- Word files in the agency letterhead format, filed per employee; employee search and old file upload
