# KinetixSphere — v1.2.4

One desktop app for recruitment **and** HR. It combines **PeopleDesk 4.2** (Clients & Vendors, Employees, Leave,
Attendance, roles, backups) with **TalentSync Simplify Cloud** (Windows one-click installer, local SQLite, host/client LAN sync
with device approval, team chat, AI resume parsing with Ollama offline mode, encrypted sensitive fields, contractor
timesheets, follow-up reminders, photos, Excel mirror, auto-update hook).

> v1.2.1 is a rebrand of PeopleDesk HR 1.1.1 (new name, logo and colours). Installing it on a PC that had 1.1.1 copies that data across automatically (1.1.1 stays installed until you remove it).

## Install (Windows 10/11, 64-bit)
Run **KinetixSphere-Setup-1.2.4.exe**. It installs per-user with no admin prompt and adds Start-menu + desktop shortcuts.
Windows SmartScreen may say "unknown publisher" because the installer is not code-signed — choose *More info → Run anyway*.

Sign in with the owner email and password. Colleagues get their own accounts from Team & Roles (name@kinetixsphere.com).
If PeopleDesk 4.x data is on the PC, a banner offers to import it (candidates, jobs, clients/vendors, employees, leave, attendance,
resumes and user accounts with their existing passwords). Safe to run again; also under Settings → *Import from PeopleDesk 4.x*.
Uninstall PeopleDesk 4.2 (the old Inno Setup version) first if you have it — it is a different product; its data is left untouched.

## Roles (enforced in the app's main process, not only the UI)
| Role | Can do |
|---|---|
| Super Admin | everything, plus Team & Roles, backups, sync host, branding |
| HR | all recruitment + Employees, leave approvals, everyone's attendance, delete records |
| Recruiter | own candidates/positions, clients & vendors, own leave/attendance (cannot delete) |
| Viewer | read-only |

## What's new in the merge
* Clients & Vendors, Employees, Leave, Attendance, Team & Roles — all synced between PCs by the existing LAN sync.
* Resume reader upgraded with PeopleDesk's rule-based parser: location, current company/designation, total experience from date
  ranges, skills, education, LinkedIn, CTC/notice period. Uncertain fields are orange; imported profiles get a "needs a quick check" flag.
* Spreadsheet import understands PeopleDesk's wide header vocabulary; unmatched columns are kept on the profile; duplicates (same phone/email) skipped.
* Many resumes at once; CSV export; bulk stage/recruiter/delete actions; stages New → … → On Hold.
* Manual backup/restore (zip) and automatic daily backup (last 7). AI keys are never put in a backup.
* Tray icon; closing the window keeps hosting running while this PC is the sync host.

## Licensing
Licensing: the owner account never needs a licence. Every other user gets a 7-day trial from their first sign-in on a PC, then needs a
key made for that PC's Device ID (Settings > Licence manager, owner only). Keys are signed with the owner's private key; the app contains only the public key.

## Where data lives
`%APPDATA%\KinetixSphere\data\peopledesk-hr.db` · resumes `…\resumes` · backups `…\backups` · Excel mirror `Documents\KinetixSphere\Exports`.

## Build
Windows: `npm install` then `BUILD_EXE.bat` (or `npm run build`). CI: `.github/workflows/build-windows.yml`.
Linux cross-build notes are in `scripts/build-windows-on-linux.sh`.
