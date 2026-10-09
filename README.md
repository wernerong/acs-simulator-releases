# ACS Simulator

Public downloads and signed automatic updates. The development repository remains
private. No GitHub account or token is needed to install or receive updates.

## Windows x64

1. Install Docker Desktop with its WSL2/Linux-container engine and start it.
2. Download **ACS-Simulator-Windows-x64-<version>.zip** from the
   [latest release](https://github.com/wernerong/acs-simulator-releases/releases/latest).
3. Extract the complete ZIP to a permanent folder and double-click **Start.cmd**.
4. Create a simulator login and enter the backend hostname and onboarding API key
   supplied privately by your administrator. Register this installation's own
   controller serial in your backend. Do not reuse the Pi's identity.

The public package contains no onboarding key, installed data, users/cards or
device certificates. Never post your API key, passwords or private diagnostics here.
Your laptop must be able to reach your backend; use only an authorized test backend.

## Updates

### Version 5.6.1

Controller firmware uploads and saved-version switching no longer require
supporting DLLs to match a bundled-build hash list. Use your authorized controller
firmware ZIP with its own managed dependencies, including different branches.
This fixes the rejection of otherwise compatible builds in 5.6.0 and earlier
managed releases. Both public and private installers share the fix.

Fresh installations use the updated table schema: key tracking includes names
for the person taking/returning a key, and face templates support 4000 characters.
Existing installations receive the same three additive changes before controller
startup, with a retained database backup. No existing records are deleted or
rewritten, and the selected controller firmware stays unchanged.

The .NET 10 and portable identity-adapter compatibility checks, ZIP safety,
settings preservation, database backup and activation checks remain. Firmware
must still be compatible with the portable runtime; this does not guarantee
every future controller build. Signed automatic simulator updates continue to
verify their signatures and hashes. Existing users need no reinstall: after
the simulator updates, upload the previously rejected ZIP again.

### Version 5.6.0

The controller monitor now offers **Transactions** and **Live logs**, with
bottom/right docking, a separate window, and an adjustable bottom-panel height.
Live logs use bounded incremental reads and stop polling when hidden or paused.
Backend connection tests show an outage countdown and retain offline resend
choices. Cabinet accountability transactions have clearer descriptions.

CAU IP card taps now follow the controller's downloaded mode definition and
Access Ledger in Normal, Secure and Supervised modes. Supported flows verify
Card, request PIN only when required, then submit one access intent. The
controller owns PIN attempts and approval; waiting for supervision is not an
access grant. Serial reader behavior is unchanged. Required biometric,
multiple-participant and unsupported fallback flows fail closed; this does not
add biometric recognition, IP IDS or card/PIN tools to MCP.

**Report an issue** captures expected versus actual behavior and recent evidence
for a door/readers or key cabinet. **Record a test** saves a bounded sequence for
later review. Review and download a developer ZIP from **Issue reports**, or
delete unwanted captures after confirmation. Nothing is uploaded automatically;
there is no built-in AI model or control replay. Review notes before sharing.

A recording follows one selected door or cabinet plus shared input/connection
actions across navigation. It is not an all-modules recorder. The dashboard and
cabinet workbench provide these controls; Diagnostics stays inspection-only.
Capture text/buttons match the surrounding UI, and sidebar navigation is grouped
into Test bench, Inspect and Manage without inconsistent arrows.

Firmware builds now appear once in the chooser. Identical uploads reuse stored
files, completed transfer ZIPs are removed and redundant deployment copies are
avoided, while distinct binaries and the latest recovery copy remain protected.

Optional **MCP access** is available in Deployment settings. Confirm
your simulator login to enable, rotate or revoke one 90-day MCP token.
Twelve tools provide inspection, saved issue reads (`list_issue_reports` and
`get_issue_report`), `list_controls`, `prepare_factory_reset` and
`execute_control`. Discover configured controls, effects and parameter schemas,
then choose **Allow physical tests** with your simulator login to enable writes
using the SAME token. Older read-only configurations do not silently gain writes.
**Disable physical tests** revokes writes without removing inspection access.
MCP is disabled by default, uses the existing localhost port at `/mcp`, and
contains no bundled MCP token. Complete onboarding/DNDS before inspection.
Save the newly issued token privately in your local MCP client's secret store.
Your backend key and browser cookie are not MCP credentials. A cloud client
cannot reach this laptop's localhost without a separately configured secure route.

MCP 0.3.0 retains bearer-client discovery and request admission: 600 POSTs plus a
30-request burst per token per rolling minute, separate strict failed-auth limits,
HTTP 429/Retry-After, and exempt discovery/session housekeeping. Simulator
v5.6.0 appears beside Sign out. Refresh the client's catalog if it cached an older tool list.

Physical controls cover door inputs, LSDI/DOR, controller tamper and power, DDM
fire, cabinet inputs and bounded connections, including individual reader outages.
Actions require matching installation/controller scope and configuration revision;
shared scenario/maintenance locks and durable retry protection guard execution.
Factory reset requires a prepared one-use confirmation and human approval.
Callers are responsible for their actions and controller/backend consequences.
Card/PIN workflows, saved-play MCP execution, SQL writes, settings edits and firmware
administration are not exposed. Readback is physical simulator evidence, not an
access grant or proof of backend delivery.

Includes controller log ZIP downloads, a read-only Database explorer, saved
Scenario plays, bidirectional optical turnstiles, lift/IDS corrections and an
installed simulator version beside **Sign out**. Scenarios support DDM EM/HSM
doors, LSDI inputs, controller tamper and bounded connection outages. Connection
lanes run sequentially. Input readback confirms simulator state, not controller
alarm or recovery delivery. Restoring an input does not reset latched alarms.
Use **Delete play** to remove a saved play after named confirmation; other plays
and run history remain. Runs continue when the browser closes, but not while
the host sleeps.

Fresh installations carry only controller build **20261008.6**, commit **8c92e188**.
Existing installations keep their selected firmware; the bundled build can be
selected separately in Controller firmware. Saved user firmware is not deleted.
Simulator version and controller firmware version are separate identifiers.

Keep the extracted folder. While Docker and ACS Simulator are running, the updater
checks this repository every five minutes. It verifies a signed release and the
downloaded hashes, backs up the database, installs the simulator/runtime update and
checks service health. An unsuccessful update restores the previous images.
Expect a brief interruption of simulated devices during a successful update.

Local login, onboarding details, controller identity, selected controller firmware,
database, saved firmware, issue captures and enabled MCP configuration are retained. Firmware changes remain a separate action
in the simulator. Updates wait for controller administration jobs and active
scenario plays to finish. Interrupted scenarios requiring input review also hold updates.
Offline or sleeping laptops keep their installed version and catch up later.
Docker Desktop/Windows upgrades and incompatible database migrations are not
automatic. Version 5.6.1 includes only the reviewed additive schema changes above.

**Start.cmd** runs it. **Stop.cmd** stops it without deleting data.
**Diagnose.cmd** includes the update status. **Uninstall.cmd** asks for confirmation
and deletes this installation's local data. Do not use Uninstall to upgrade.

If you already use the standalone r4 ZIP, stop r4 and run Start from the new
update-enabled package once, on the same Docker Desktop engine. The existing
installation is retained. Use only the new Start/Stop launchers thereafter; old
standalone launchers do not understand automatic updates. Keep a backup first.

This release channel is for Windows x64. Existing Raspberry Pi and Mac installs
are not enrolled or modified. This is a test simulator, not a production access
controller or a safety/alarm system. Public packages are inspectable software.

Source pushes, drafts and prereleases do not update users. Only an approved signed
stable release does. For support, contact the person who supplied your installer.
