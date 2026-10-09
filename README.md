# ACS Simulator

**Test access-control firmware from your browser.**

Open a simulated door, tap a reader, take a cabinet key or inject an input fault.
Watch the real controller respond, repeat a test and collect evidence when
something behaves unexpectedly. The simulator models hardware; the controller
retains access decisions, PIN verification, modes, alarms and backend reporting.

[Download for Windows x64](https://github.com/wernerong/acs-simulator-releases/releases/latest)
| [Release notes](https://github.com/wernerong/acs-simulator-releases/releases)
| [Feature tour](#explore-the-simulator)
| [Quick start](#install-and-start)

This repository distributes installers and signed automatic updates. The source
repository stays private. **No GitHub account or GitHub token is needed.**

## Install and start

You need a Windows x64 PC, Docker Desktop running its Linux/WSL2 engine, and
network access to an authorized ACS test backend. Ask your administrator for
the backend hostname and onboarding API key.

1. Download **ACS-Simulator-Windows-x64-<version>.zip** from the latest release.
2. Extract the whole ZIP to a permanent folder and double-click **Start.cmd**.
3. Create your local simulator login and enter your backend onboarding details.
4. Register this installation's generated controller serial in your backend,
   configure its doors/readers/cabinets, then complete configuration synchronization (DNDS).
5. Open the simulator in your browser and choose a configured device to test.

The package runs the controller, simulator and local database together in Docker.
It does not include your backend, onboarding key, device certificates or live
users/cards. A fresh installation has no configured doors until your backend
configuration is synchronized. Do not reuse another controller's identity.

## Explore the simulator

Screenshots show the actual 5.6.1 interface with synthetic demo data, not a live
installation. Names, cards, keys and incident details are examples. Available
devices and controls depend on your controller configuration and firmware.

### Doors and readers

Choose a configured door, select a database card and tap its IN or OUT reader.
Watch the controller's lock output and reader status, then move the simulated
door contact. Test exit requests, key switches, break glass and wiring faults.

![Door controls with IN and OUT readers, key switch, exit request and break glass](https://raw.githubusercontent.com/wernerong/acs-simulator-releases/main/docs/images/door-controls.png)

Serial and IP readers support the implemented card/PIN flows, including Normal,
Secure and Supervised access. Door models include EM locks, HSM120/HSM220,
sliding doors, starter doors, 120-degree turnstiles and optical gates.
The controller decides access and relocking; a button press is not an access grant.
Required biometric recognition and unsupported multi-person IP flows are not simulated.

<details>
<summary>See the dashboard and navigation</summary>

![Dashboard with configured doors, card selection, grouped navigation and simulator version](https://raw.githubusercontent.com/wernerong/acs-simulator-releases/main/docs/images/doors-readers.png)

</details>

### Key cabinets

Choose a cardholder, request an authorized key or group, open the cabinet and
take or return keys. Follow the on-screen visit steps and slot inventory.
Check misplaced keys, exercise wrong-slot returns and observe controller outcomes.

![Key cabinet with sample key slots, cardholder selection and take or return controls](https://raw.githubusercontent.com/wernerong/acs-simulator-releases/main/docs/images/key-cabinet.png)

### Inputs, alarms and connection faults

Select an LSDI input and switch between normal, event, cut wire and short circuit.
Operate DOR relay outputs. Test mains failure, battery state, supply voltage,
controller tamper and configured DDM fire inputs.

![SIO input terminals and relay outputs with event and wiring-fault controls](https://raw.githubusercontent.com/wernerong/acs-simulator-releases/main/docs/images/inputs-relays.png)

Connections supports timed outages for boards, reader buses, individual serial
or IP readers, and the backend. Restore communications and watch recovery.
Resetting a physical input does **not** clear a controller-latched alarm.
Optional browser sound is a test aid, not a safety siren.

<details>
<summary>See power and controller tamper controls</summary>

![Power supply, battery state and independent controller tamper inputs](https://raw.githubusercontent.com/wernerong/acs-simulator-releases/main/docs/images/power-tamper.png)

</details>

### Repeatable scenario plays

Start from a template, add actions and observations, map lanes to configured
targets, then check and run the play. Save scenarios for repeat testing and inspect
the run timeline. Supported targets include DDM EM/HSM doors, LSDI, controller
tamper and timed connections. Door lanes can run together; connection lanes run
sequentially. Plays continue when the browser closes while the host remains awake.

<details>
<summary>See the scenario builder and a two-door test play</summary>

![Scenario builder with a break-in and recovery sequence mapped to two demo doors](https://raw.githubusercontent.com/wernerong/acs-simulator-releases/main/docs/images/scenarios.png)

</details>

### Evidence when something goes wrong

Use **Report an issue** for unexpected behavior, or **Record a test** before
reproducing it. Add the expected and actual result, review the captured steps
and evidence, then download a developer ZIP. Recordings retain the selected door
or cabinet context plus shared input/connection evidence across navigation;
they do not record every other door and cabinet automatically.

![Issue report with expected behavior, observations, recorded steps and developer ZIP download](https://raw.githubusercontent.com/wernerong/acs-simulator-releases/main/docs/images/issue-report.png)

No built-in AI, automatic upload or automatic replay. Review reports and original
logs before sharing: device identifiers and your own notes may still be sensitive.

## More tools in the same installation

| Area | What you can do |
| --- | --- |
| Controller monitor | Search transactions and live logs, pause polling, resize the panel, or dock it at the bottom, side or in a separate window. |
| Diagnostics | Inspect grouped failures and service status; download original controller logs as ZIPs. |
| Database explorer | Browse controller tables read-only to verify downloaded configuration and recorded state. |
| Lift panel | Exercise configured lift-reader and floor-selection behavior. |
| Controller settings | Inspect effective settings, edit supported configuration files and restart the controller when required. |
| Controller firmware | Upload a compatible firmware ZIP, switch versions and delete stale library versions with password confirmation. Different managed DLL hashes are allowed; runtime compatibility checks still apply. |
| MCP integration | Discover inspection tools and configured physical controls from an MCP-compatible client. Optional, disabled by default; owner-enabled writes share one dedicated token. |
| Traceability | See the simulator version beside Sign out and the separate installed controller firmware version. |

<details>
<summary>See Diagnostics and original log downloads</summary>

![Diagnostics log library with file dates, download range and ZIP download](https://raw.githubusercontent.com/wernerong/acs-simulator-releases/main/docs/images/diagnostics.png)

</details>

## Your first test

After onboarding and configuration synchronization:

1. Open **Doors & readers** and choose a configured door and card.
2. Tap the IN reader. Enter a PIN if prompted; let the controller decide access.
3. Move the simulated door contact, then close it and observe the lock and reader.
4. Check **Controller transactions** for the resulting evidence.
5. If the result is unexpected, select **Report an issue**, or record the next attempt.

Use only an authorized test environment. Controls can generate real controller
alarms and backend transactions. An HTTP-accepted transaction is not proof that
the backend displayed it. The simulator is not a production access controller
or safety/alarm system.

## Install once, keep receiving updates

While Docker and ACS Simulator are running, the updater checks for signed stable
releases every five minutes. It waits for active scenario/administration work,
verifies the update, backs up the database and checks health after installation.
Expect a brief service interruption. Failed health checks restore the previous images.

Your local login, onboarding details, controller identity, database, captures,
saved firmware and selected controller version are retained. Simulator updates
and controller firmware selection are separate. Offline or sleeping PCs catch up
when they are running and connected again.

Use **Stop.cmd** to stop without deleting data, and **Diagnose.cmd** to inspect
update status. **Do not uninstall to upgrade**: Uninstall deletes local data after
confirmation. Keep the extracted launcher folder.

## MCP: optional client access

Enable MCP in **Deployment settings**, confirm your simulator login and store
the issued token privately in your client's secret store. Use the client's tool
catalog to discover reads and **list_controls** to discover configured actions.
For physical writes, explicitly enable **Allow physical tests** using the same
token; older read-only configurations do not gain writes automatically.

The local endpoint is **/mcp** with Bearer authentication. A cloud bot cannot reach
localhost without a separately configured secure route. MCP does not add an AI
model to the simulator. It does not expose arbitrary shell/SQL writes or firmware
administration. Factory reset requires prepared, one-use human confirmation.
You remain responsible for test actions and their backend effects.

## Help and release details

Contact the person who supplied your installer. Use **Diagnose.cmd**, Diagnostics
or a reviewed issue-report ZIP to provide evidence. Never post passwords, API
keys, MCP tokens or unreviewed logs publicly.

This download channel is for **Windows x64**. It does not enroll or modify
existing Raspberry Pi or Mac installations. Screenshots illustrate the shared
simulator interface; host-specific setup and administration can differ.

<details>
<summary>Detailed setup, update behavior and 5.6.2 release changes</summary>

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

### Version 5.6.2

Full-height turnstile passages follow the controller-approved direction: entry
enables **Pass IN**, while exit approval or an enabled exit request enables
**Pass OUT**. The buttons sit on their respective sides and rotate oppositely.
Wrong-side attempts do not consume the shared single passage. Unlock modes and
fire release retain repeated bidirectional movement.

Optical fire release now reports the released lock with a closed contact first,
then opens the contact on a subsequent complete controller read. Partial reads
and writes do not consume that first sample.

A short optical remote-unlock pulse on both outputs now retains one passage
after the pulse ends. Choose **Pass IN** or **Pass OUT**; the first passage
consumes the shared permit for both sides. Unused permits still expire, and
continuous held unlock retains free movement while active.

The firmware settings explanation is clearer. On native Pi, **Keep current Pi
settings** now preserves values inherited from current base settings instead of
restoring removed uploaded environment overrides such as RabbitMQ EnableTLS.
The Windows adapter already preserves effective settings and keeps that behavior.
The Windows package does not deploy changes to a separate native Pi.

The version stamp is **Simulator v5.6.2**. Bundled firmware and schema are unchanged
from 5.6.1; automatic updates preserve existing selected firmware and local data.

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
The installed simulator version appears beside Sign out. Refresh the client's catalog if it cached an older tool list.

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

</details>
