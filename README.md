# Job Listing RPA
A basic automation that goes to RemoteOK.com, scrapes remote job listings, saves them to an Excel file, and sends the file by email.

## Description
An RPA/automation that visits RemoteOK, extracts remote job listings, saves them to a dated Excel file, and emails the file.

## Overview
1. Automates going to the site RemoteOK.com
2. Perform Data scraping (table extraction) from the site. Extracts the jobs table.
3. Stores the following: `Job Name`, `Company` and `Job Posted` in a data table
4. Added these information to an Excel file that has the following name `Listed_Jobs_<current_date>.xlsx`. Saves to Listed_Jobs_<YYYY-MM-DD>.xlsx.
5. Sends the an email with the file as an attachment
Title: Job Listing RPA — RemoteOK → Excel → Email


## Features

- Navigates to RemoteOK and extracts the job table
- Captures Job Title, Company, Date Posted
- Normalizes dates and removes duplicates
- Saves as Listed_Jobs_<YYYY-MM-DD>.xlsx
- Emails the spreadsheet as an attachment

## Tech Stack (update as appropriate)
- RPA: UiPath (REFramework) or Automation: Python + Playwright/Requests + pandas + openpyxl
- Email: SMTP / Outlook / Gmail API

## How it works
1. Open RemoteOK.
2. Extract the job table (handles pagination & dynamic loads).
3. Normalize “Date Posted” to ISO date.
4. De-duplicate by hash(company|title|date).
5. Export to Excel with headers and autofilter.
6. Send email with the Excel attached; include a summary in the body.

## Configuration
- RECIPIENT_EMAIL — where to send the results
- SMTP_HOST, SMTP_PORT, SMTP_USER, SMTP_PASS (or use secure credentials/Assets)
- USER_AGENT — identify the bot politely
- RATE_LIMIT_MS — delay between requests (e.g., 1500–2500ms jitter)

## Run


python run.py



## Ethics & Compliance
- Respects site robots/TOS, light touch scraping, and identifies itself with a User-Agent.
- For sites offering an API, the bot will prefer it.

## Output
- Excel: Listed_Jobs_2025-08-27.xlsx (sample in /samples)
- Email: includes counts (total/new/duplicate/failed)

## Known limitations

- Markup changes to the site may require selector updates.

## Roadmap

- Add CSV export, Slack/Telegram notifications, containerized run (Docker), and CI.

## Structure
job-listing-rpa/
├── README.md
├── LICENSE
├── .gitignore
├── samples/
│   └── Listed_Jobs_2025-08-27.xlsx
├── config/
│   └── .env.example
├── src/
│   ├── main.xaml                 # UiPath (if RPA) 
│   ├── run.py                    # or Python entrypoint
│   ├── scraper.py                # table extraction
│   ├── normalize.py              # date parsing/cleanup
│   ├── export_excel.py
│   ├── mailer.py
│   └── utils.py                  # logging, dedupe, backoff
├── tests/
│   ├── test_normalize.py
│   └── fixtures/
│       └── remoteok_sample.html
└── .github/
    └── workflows/ci.yml          # lint + tests
