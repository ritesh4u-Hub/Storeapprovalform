# Store Approval Form

Private source backup: download and extract **Storeapprovalform-source.zip** to access the full project source, including the Windows IIS application.

GitHub repository: https://github.com/ritesh4u-Hub/Storeapprovalform


Store profitability projections and independent CGO, HPR, CEO and CFO approvals.

Live application: https://mis-sweetdreams.in/Storeapprovalform/
Login: https://mis-sweetdreams.in/Storeapprovalform/login.html

## Windows production application

The current Windows application source is in `windows-iis/source`, with deployable assets in `windows-iis/public`. The C# backend is `windows-iis/public/Desk.ashx`. Shared financial calculations and exports are in `lib`. See `windows-iis/WINDOWS-HOSTING.md` and `windows-iis/deployment.json`.

Deploy to the existing folder `C:\inetpub\wwwroot\CFOProject\Storeapprovalform`, IIS site `CFO`, application `/Storeapprovalform`, application pool `Storeapprovalform`. Do not create another project directory or an extra `iis` subfolder. Preserve the server's App_Data directory, user accounts and saved stores.

## Features

- Five-year company and franchisee profitability, investment, depreciation and ROI.
- Editable assumptions, sales, operating costs and per-year overrides.
- Draft saving and revisions of submitted proposals with new approvals required.
- Independent head acceptance, rejection and requests for changes, with signed-in identity and timestamps.
- Administrator-managed accounts and role assignments.
- Search, CSV reports, WhatsApp-ready JPG exports and print/PDF output.
- Store photos/videos and later LOI/agreement PDFs from authorized members.
- Recoverable deletion and restoration.

## Build the Windows frontend

Install dependencies with `npm ci`, then run:

```sh
npx esbuild windows-iis/source/main.tsx --bundle --minify --platform=browser --format=iife --outfile=windows-iis/public/app.js --define:process.env.NODE_ENV='"production"' --tsconfig=tsconfig.json
npx tsc --noEmit --incremental false
```

The deployable HTML, CSS and backend remain alongside the generated JavaScript. Only App_Data/defaults.json and its protection web.config are templates; never replace live account, store or attachment data from this repository.

## Deployment status

Updated 23 October 2026. The blank return reason change is published to the existing Windows IIS application: **Request changes** accepts an empty decision reason and retains the approver's identity and timestamp. Rejection still requires a reason. Role checks, version checks and the 4,000-character comment limit remain enforced. Existing accounts, store records and attachments were not modified.

Validation: TypeScript check and Windows frontend build passed; request handler tests covered blank/whitespace/commented returns, audit identity/date, role restrictions, stale versions, comment length and rejection validation. The server compiled the updated C# handler and verified published file contents. The live JavaScript checksum matches the built bundle; anonymous API access returns JSON 401.

The archive also includes prepared login-default source from the previous backup. Its full server deployment has not been verified; the 23 October publication updated the approval handler, frontend bundle and frontend cache version only.

CAM zero-value calculations were checked across all five years: CAM and CAM deposits remain zero. CAM escalation intervals must remain at least one year under the current validation rule.

The `app` directory retains the original Sites/Cloudflare implementation. It uses different authentication and storage and is not the Windows deployment entry point. The blank return reason source update is included there too; it has not been published to the older chatgpt.site demo.

## Repository contents

This repository contains application source and runtime templates only. Server passwords, certificate private keys, actual accounts, store records, uploaded media/documents and local publishing tools are excluded. This repository is not a backup of production business data.
