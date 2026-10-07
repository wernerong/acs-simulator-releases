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

### Version 5.4.0

Firmware builds now appear once in the chooser. Identical uploads reuse stored
files, completed transfer ZIPs are removed and redundant deployment copies are
avoided, while distinct binaries and the latest recovery copy remain protected.

Optional **MCP access** is available in Deployment settings. Confirm
your simulator login to enable, rotate or revoke one 90-day MCP token.
Ten tools provide inspection plus `list_controls`, `prepare_factory_reset` and
`execute_control`. Discover configured controls, effects and parameter schemas,
then choose **Allow physical tests** with your simulator login to enable writes
using the SAME token. Older read-only configurations do not silently gain writes.
**Disable physical tests** revokes writes without removing inspection access.
MCP is disabled by default, uses the existing localhost port at `/mcp`, and
contains no bundled MCP token. Complete onboarding/DNDS before inspection.
Save the newly issued token privately in your local MCP client's secret store.
Your backend key and browser cookie are not MCP credentials. A cloud client
cannot reach this laptop's localhost without a separately configured secure route.

MCP 0.2.0 retains bearer-client discovery and request admission: 600 POSTs plus a
30-request burst per token per rolling minute, separate strict failed-auth limits,
HTTP 429/Retry-After, and exempt discovery/session housekeeping. Simulator
v5.4.0 appears beside Sign out. Refresh the client's catalog if it cached seven tools.

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

Fresh installations carry only controller build **20261006.6**, commit **e279419a**.
Existing installations keep their selected firmware; the bundled build can be
selected separately in Controller firmware. Saved user firmware is not deleted.
Simulator version and controller firmware version are separate identifiers.

Keep the extracted folder. While Docker and ACS Simulator are running, the updater
checks this repository every five minutes. It verifies a signed release and the
downloaded hashes, backs up the database, installs the simulator/runtime update and
checks service health. An unsuccessful update restores the previous images.
Expect a brief interruption of simulated devices during a successful update.

Local login, onboarding details, controller identity, selected controller firmware,
database, saved firmware and enabled MCP configuration are retained. Firmware changes remain a separate action
in the simulator. Updates wait for controller administration jobs and active
scenario plays to finish. Interrupted scenarios requiring input review also hold updates.
Offline or sleeping laptops keep their installed version and catch up later.
Docker Desktop/Windows upgrades and database-schema migrations are not automatic.

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
