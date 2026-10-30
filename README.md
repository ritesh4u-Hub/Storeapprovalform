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

Source backup updated 30 October 2026. Live Windows application: https://mis-sweetdreams.in/Storeapprovalform/.

Published changes included in this backup:

- 23 October: **Request changes** accepts a blank reason and retains the approver identity/date. Rejection still requires a reason.
- 24 October: Optional five-year **total monthly minimum rent and CAM amounts** support flat increases. Blank years use the existing percentage calculation; zero is allowed. Payable rent remains the higher of minimum rent and revenue share. Year 1 minimum rent and CAM determine deposits. Projections, CSV reports and shared JPG workings use these amounts.
- 27 October: Optional free-text **Store Category**, **Facade Type** and **Notice period** fields are saved with proposals and included in reports and shared workings. Existing proposals remain compatible.

Validation completed for the published changes: Windows frontend builds and TypeScript checks, legacy-form compatibility, manual/automatic lease schedules, zero CAM, deposits, unchanged franchisee calculations, metadata persistence/validation, report-column alignment, C# handler compilation, live bundle checksums and protected API access. Existing accounts, stores and attachments were preserved.

The archive also retains prepared login-default source from the previous backup. Full publication of that earlier login-default change has not been verified; recent publications updated the application handler, frontend bundle and asset cache version only.

The `app` directory retains the original Sites/Cloudflare implementation with corresponding source changes. It uses different authentication and storage and is not the Windows deployment entry point. The older chatgpt.site demo has not received these recent publications.

## Repository contents

This repository contains application source and runtime templates only. Server passwords, certificate private keys, actual accounts, store records, uploaded media/documents and local publishing tools are excluded. This repository is not a backup of production business data.
