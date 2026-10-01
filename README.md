# Registry

Windows registry packs for security, privacy, performance, networking, and shell UX.

**Author:** Gorstak  
**Import:** right-click -> *Merge*, or `reg import <file.reg>` (elevated for HKLM)

> Review before applying. Many keys harden or lock down the system.  
> Large dumps (`Immunity`, `Firewall`, `Certificates`, `AdBlock-Routes-Full`) can take time to import.

---

## Layout

| File | Purpose |
|------|---------|
| **Policies.reg** | Machine policy templates, Software Restriction Policy, device-install denials, SmartScreen / RDP / WinRM policy |
| **Performance.reg** | Desktop snappiness, explorer UX, Game Mode, GPU/app power profiles |
| **Privacy.reg** | Telemetry & history cleanup, consent store, advertising ID, recycle-bin policy |
| **Security.reg** | LSA/SAM, ASR rules, TLS, worm surface reduction, single-user hardening, UAC COM approval |
| **Network.reg** | SCHANNEL/cipher hardening, DNS-over-HTTPS (DoH) policy |
| **Browsers.reg** | Chrome / Edge / Brave / Firefox / Arc enterprise policies |
| **UI.reg** | Shell cosmetics, context menus, desktop presentation |
| **Services.reg** | Service host / service configuration dump |
| **Cleanup.reg** | Remove noisy app-event schemes and leftover shell classes |
| **Firewall.reg** | Windows Firewall policy + Base Filtering Engine (BFE) dump |
| **IPSec.reg** | IPSec filters and local policy objects |
| **Certificates.reg** | Disallowed / untrusted certificate store entries |
| **AdBlock-PAC.reg** | PAC `AutoConfigURL` for ad blocking |
| **AdBlock-Routes.reg** | Lite persistent blackhole routes for ad/tracker IPs |
| **AdBlock-Routes-Full.reg** | Full route blocklist (large) |
| **GeoBlock-PAC.reg** | Optional PAC for geo restriction bypass |
| **Immunity.reg** | Bulk Zone.Identifier / MOTW immunity entries (very large) |

---

## Suggested apply order

1. `Policies.reg` -> `Security.reg` -> `Privacy.reg`
2. `Network.reg` -> `Firewall.reg` -> `IPSec.reg` (optional)
3. `Browsers.reg`
4. `Performance.reg` -> `UI.reg` -> `Services.reg` -> `Cleanup.reg`
5. Optional: `Certificates.reg`, ad-block packs, `Immunity.reg`

### Conflicts to note

- **AdBlock-PAC.reg** and **GeoBlock-PAC.reg** both set `AutoConfigURL` - use one, not both.
- **Security.reg** merges several former hardening packs; later sections override earlier ones for the same value.

---

## What was merged

| Category file | Former files |
|---------------|--------------|
| Policies | `MachinePolicy`, `Restrictions`, `DevB`, `Tweaks` |
| Performance | `Perf`, `Games` |
| Privacy | `Privacy`, `DisableTrash`, `UserPolicy` |
| Security | `GEDR_Hardening_Registry`, `GShield`, `GSecurityLite`, `GSecurity`, `single_user_hardening`, `Worms`, `Worms Doors Cleaner`, `COM Auto Approval`, `COMList` |
| Network | `Network`, `DoT` |
| Browsers | `Browsers`, `Brave` |
| UI | `Sminkica` |
| Services | `Services` |
| Cleanup | `JetCleanup` |
| Firewall | `Firewall`, `BFE` |
| IPSec | `IPSec`, `IPSecPolicy` |
| Certificates | `Certs` |
| AdBlock-PAC | `BlockAds` |
| AdBlock-Routes | `PiholeLite` |
| AdBlock-Routes-Full | `Pihole` |
| GeoBlock-PAC | `GeoBlockBypass` |
| Immunity | *(unchanged)* |

Each merged file keeps section comments with the original source name for traceability.
