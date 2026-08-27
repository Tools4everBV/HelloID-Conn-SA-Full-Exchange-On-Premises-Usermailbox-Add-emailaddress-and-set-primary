# Changelog

All notable changes to this project will be documented in this file. The format is based on [Keep a Changelog](https://keepachangelog.com/), and this project adheres to [Semantic Versioning](https://semver.org/).

## [1.0.0] - 2026-08-27

Initial release of HelloID-Conn-SA-Full-Exchange-On-Premises-Usermailbox-Add-emailaddress-and-set-primary.

### Added

- Initial release for adding email addresses to Exchange On-Premises user mailboxes with optional primary setting.
- Datasource to search and select user mailboxes by name, alias, or email address using wildcard filtering.
- Datasource to retrieve current email addresses for the selected mailbox, displaying prefix and address separately.
- Datasource to get all verified accepted mail domains from Exchange On-Premises.
- Datasource to validate email address uniqueness across all Exchange recipients including user, shared, room, and equipment mailboxes.
- Task to add new email address to user mailbox while preserving existing proxy addresses.
- Support for setting new email address as primary SMTP address, automatically converting existing primary to secondary.
- Form validation to ensure email prefix follows valid format pattern and email address is unique.
- Comprehensive error handling with detailed audit logging for all operations.
- Secure PowerShell remoting connection to Exchange On-Premises with TLS 1.2 support.

### Changed

### Deprecated

### Removed

### Fixed
