## 📊 Message Fields

The goal is to reproduce the maximum number of fields from the official content pack, in particular those strictly required to rebuild the dashboard widgets included in the official content pack (Global, SSH, Sudo, Users & Groups overviews).

> ⚠️ Not all fields from the official content pack are currently implemented. The tables below reflect only the fields that have been successfully reproduced so far.

---

### General Parsing

| Field Name | Example Value | Description |
|---|---|---|
| `event_created` | `2025-06-28T05:39:00.000Z` | Timestamp extracted from the syslog header |
| `event_source` | `srvjosh` | Hostname extracted from the syslog header |
| `application_name` | `sshd` | Application or service name extracted from the syslog header |
| `process_id` | `2806` | PID extracted from the syslog header |
| `source` | `srvjosh` | Hostname or IP address of the system that generated the event |

---

### SSH

| Field Name | Example Value | Description |
|---|---|---|
| `event_outcome` | `success` | Whether the SSH event succeeded or failed |
| `source_ip` | `192.168.1.66` | IP address of the connecting client |
| `source_hostname` | `laptop-josh.home.local` | Hostname of the connecting client |
| `source_port` | `51234` | Port used by the client to initiate the connection |
| `user_name` | `josh` | Username used during authentication or associated with the session |
| `vendor_credential_type` | `publickey` | Authentication method used (password, publickey) |
| `vendor_event_description` | `Accepted publickey` | Description of what happened during the SSH event |
| `vendor_event_outcome` | `not allowed` | Outcome as reported by the SSH daemon |
| `vendor_event_outcome_reason` | `not listed in AllowUsers` | Reason provided by the SSH daemon to explain the outcome |
| `vendor_ssh_signature` | `ED25519 SHA256:abc123xyz...` | Fingerprint of the key or certificate used during authentication |

---

### Sudo

| Field Name | Example Value | Description |
|---|---|---|
| `event_outcome` | `success` | Whether the sudo attempt succeeded or failed |
| `process_command_line` | `/usr/bin/apt upgrade` | Full command line that was run with elevated privileges |
| `process_working_directory` | `/home/josh` | Working directory from which the sudo command was invoked |
| `source_user_name` | `josh` | User who requested elevated privileges |
| `user_name` | `root` | User account under which the command was executed |
| `vendor_sudo_error` | `user NOT in sudoers` | Error message returned when the sudo attempt was denied |
| `vendor_tty` | `pts/0` | Terminal from which the sudo command was run |

---

### PAM

| Field Name | Example Value | Description |
|---|---|---|
| `event_outcome` | `failure` | Whether the PAM authentication or session event succeeded or failed |
| `source_ip` | `192.168.1.66` | IP address of the remote host that initiated the authentication attempt |
| `source_user_name` | `josh` | Remote user or user who initiated the session on behalf of another |
| `user_name` | `joshadmin` | Account being authenticated or for which a session was opened or closed |
| `vendor_pam_euid` | `0` | Effective user ID under which the process is running |
| `vendor_pam_function` | `auth` | PAM function called during the event (auth, session, account) |
| `vendor_pam_logname` | `josh` | Login name associated with the PAM event |
| `vendor_pam_module` | `pam_unix` | PAM module that handled the authentication |
| `vendor_pam_service_name` | `sshd` | Application or service that invoked PAM |
| `vendor_pam_uid` | `1000` | User ID of the account being authenticated |
| `vendor_tty` | `/dev/pts/1` | Terminal on which the authentication attempt took place |

---

### User and Group Activity

| Field Name | Example Value | Description |
|---|---|---|
| `source_user_id` | `1001` | ID of the user performing the action, or the user ID before a change |
| `user_id` | `1002` | ID of the user account being affected |
| `user_name` | `joshdev` | Name of the user account being affected |
| `vendor_event_description` | `User ID changed` | Description of the action that took place |
| `vendor_group_id` | `1010` | ID of the group being affected |
| `vendor_group_name` | `joshgroup` | Name of the group being affected |
| `vendor_tty` | `/dev/pts/1` | Terminal from which the action was performed |
| `vendor_user_home` | `/home/joshdev` | Home directory assigned to the user account |
| `vendor_user_shell` | `/bin/bash` | Login shell assigned to the user account |
