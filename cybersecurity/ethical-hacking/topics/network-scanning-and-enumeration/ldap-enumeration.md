# LDAP: directory structure and query interpretation

**Lightweight Directory Access Protocol** provides read/search and modification operations against a hierarchical directory. It commonly uses TCP/389 (plain or StartTLS) or TCP/636 (LDAPS). The Global Catalog in Microsoft environments commonly uses 3268/3269. A directory record has a distinguished name (DN), object classes and attributes. A base DN defines where to search; `dc=example,dc=test` is a fictional demonstration, not a real enterprise directory.

## Query mechanics

```bash
ldapsearch -x -H ldap://<AUTHORIZED_HOST> -s base namingContexts
ldapsearch -x -H ldap://<AUTHORIZED_HOST> -b "dc=example,dc=test" "(objectClass=inetOrgPerson)" cn sn uid mail -LLL
ldapsearch -x -H ldap://<AUTHORIZED_HOST> -b "dc=example,dc=test" "(objectClass=posixGroup)" cn gidNumber memberUid -LLL
```

The first request searches the server's root DSE, where `namingContexts` may identify the available naming base. Some server/client combinations need `-b "" -s base` explicitly; otherwise default base behavior may differ. `-x` requests simple authentication rather than SASL; simple bind does **not** mean encrypted or anonymous by definition. `-H` selects URI, `-b` base DN, `-s base` searches a single object, and `-LLL` reduces LDIF comments. Parentheses enclose filters. Quote filters to prevent shell interpretation.

## Key fields and response semantics

| Attribute | Meaning |
|---|---|
| `dn` | Full unique directory path for an entry |
| `objectClass` | Schema type(s) governing allowed attributes |
| `cn` | Common name |
| `sn` | Surname |
| `uid` | Account identifier, depending on directory schema |
| `mail` | Email address value |
| `gidNumber` | Numeric Unix group ID for `posixGroup` |
| `memberUid` | Username membership string for relevant Unix-style group schema |

An `inetOrgPerson` entry with a `uid` demonstrates that the server returns an account object. It does not prove the account can log in, has admin privileges, or that a password has been revealed. An LDIF ending in `result: 0 Success` means the search request succeeded. `numEntries: 0` means no matching accessible entries, which can result from filters, permissions or a wrong search base. Referral and `insufficientAccessRights` responses require different handling.

## Common troubleshooting

- Root query returns no naming context: use documented directory configuration or an authorized credential; avoid guessing organizational structure.
- Empty group results: confirm schema (`posixGroup` vs directory-specific classes), case-insensitive matching, correct base and access controls.
- Connection succeeds but no results: inspect bind identity and access privileges; do not infer there are no accounts.
- TLS/StartTLS problems: verify certificate trust and correct service/port rather than suppressing certificate validation.
- Large directories: request a small attribute set, use approved limits/paging and minimize exposure of sensitive personal data.

## Security implications and mitigation

Anonymous or over-permissive queries can disclose user identifiers, contact data, membership and privilege relationships. Apply LDAP access-control lists by role and attribute, require appropriate authentication, encrypt data in transit, limit enumeration rates and monitor query patterns. Documentation must use fictitious entries and redact personal accounts. Tools discussed in the source include `ldapsearch`, Metasploit's LDAP collection modules, Nessus and graphical directory browsers; tool output is only an observation of the privileges used.