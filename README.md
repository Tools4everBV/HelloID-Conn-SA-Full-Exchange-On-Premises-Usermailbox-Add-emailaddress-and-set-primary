# HelloID-Conn-SA-Full-Exchange-On-Premises-Usermailbox-Add-emailaddress-and-set-primary

| :information_source: Information                                                                                                                                                                                                                                                                                                                                                          |
| :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| This repository contains the connector and configuration code only. The implementer is responsible for acquiring the connection details such as username, password, certificate, etc. You might even need to sign a contract or agreement with the supplier before implementing this connector. Please contact the client's application manager to coordinate the connector requirements. |

## Description

_HelloID-Conn-SA-Full-Exchange-On-Premises-Usermailbox-Add-emailaddress-and-set-primary_ is a template designed for use with HelloID Service Automation (SA) Delegated Forms. It can be imported into HelloID and customized according to your requirements.

By using this delegated form, you can add email addresses to Exchange On-Premises user mailboxes and optionally set them as the primary email address. The following options are available:

1.  Search and select the target user mailbox
2.  View current email addresses assigned to the mailbox
3.  Enter a new email prefix and select the mail domain
4.  Validate that the email address is unique across all recipients
5.  Optionally set the new email address as the primary SMTP address
6.  The mailbox is updated with the new email address while preserving existing proxy addresses

## Getting started

### Requirements

- **Exchange On-Premises Environment**:<br>
  A functional Exchange On-Premises environment with PowerShell remoting enabled. The Exchange server must be accessible via the configured connection URI.
- **PowerShell Remoting**:<br>
  PowerShell remoting must be enabled on the Exchange server to allow remote connections. The Microsoft.Exchange configuration must be accessible.
- **Administrative Credentials**:<br>
  Service account credentials with sufficient permissions to query mailboxes, accepted domains, and modify user mailbox email addresses. The account must have rights to execute Get-Mailbox, Get-Recipient, Get-AcceptedDomain, and Set-Mailbox cmdlets.
- **TLS 1.2**:<br>
  TLS 1.2 must be enabled for secure communication with the Exchange server.
- **HelloID Agent**:<br>
  A HelloID agent is required to execute PowerShell commands against the on-premises Exchange environment.

### Connection settings

The following user-defined variables are used by the connector.

| Setting               | Description                                            | Mandatory |
| --------------------- | ------------------------------------------------------ | --------- |
| ExchangeConnectionUri | The PowerShell connection URI for Exchange On-Premises | Yes       |
| ExchangeAdminUsername | The username for authentication with Exchange          | Yes       |
| ExchangeAdminPassword | The password for authentication with Exchange          | Yes       |

## Remarks

### Email Address Validation Logic

- The connector validates email address uniqueness across all Exchange recipients, including user mailboxes, shared mailboxes, room mailboxes, and equipment mailboxes.
- Validation checks the alias (mailNickname), primary SMTP address, and all proxy addresses.
- If the email address already exists on the selected mailbox, the validation passes with a warning indicating the address is already assigned to that mailbox.

### Proxy Address Management

- The connector preserves all existing proxy addresses when adding a new email address.
- If the new address is set as primary, any existing primary SMTP address (uppercase prefix) is automatically converted to a secondary address (lowercase prefix).
- Duplicate addresses are removed to prevent conflicts.
- The EmailAddressPolicyEnabled flag is set to $false to prevent automatic email address policy overrides.

### Session Management

- The connector establishes a new PowerShell session to Exchange for each datasource and task execution.
- Session options include SkipCACheck, SkipCNCheck, and SkipRevocationCheck set to $false for secure connections.
- Sessions are properly disposed of in the finally block to prevent resource leaks.

### Mail Domain Selection

- The connector retrieves only verified (IsValid = true) accepted domains from Exchange.
- When displaying mail domains, the current mailbox's domain is returned first to ensure HelloID auto-selects the existing domain as the default.

## Development resources

### PowerShell Cmdlets

The following Exchange PowerShell cmdlets are used by the connector:

| Cmdlet             | Description                                               |
| ------------------ | --------------------------------------------------------- |
| Get-Mailbox        | Retrieve user mailbox information and email addresses     |
| Get-Recipient      | Query all recipients to validate email address uniqueness |
| Get-AcceptedDomain | Retrieve verified mail domains for the organization       |
| Set-Mailbox        | Update user mailbox with new email addresses              |

### API documentation

Exchange PowerShell documentation:

- [Connect to Exchange servers using remote PowerShell](https://learn.microsoft.com/en-us/powershell/exchange/connect-to-exchange-servers-using-remote-powershell)
- [Get-Mailbox](https://learn.microsoft.com/en-us/powershell/module/exchange/get-mailbox)
- [Set-Mailbox](https://learn.microsoft.com/en-us/powershell/module/exchange/set-mailbox)
- [Get-Recipient](https://learn.microsoft.com/en-us/powershell/module/exchange/get-recipient)
- [Get-AcceptedDomain](https://learn.microsoft.com/en-us/powershell/module/exchange/get-accepteddomain)

## Getting help

> :bulb: **Tip:**  
> _For more information on Delegated Forms, please refer to our [documentation](https://docs.helloid.com/en/service-automation/delegated-forms.html) pages_.

## HelloID docs

The official HelloID documentation can be found at: https://docs.helloid.com/
