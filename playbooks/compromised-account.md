# Compromised Account Response Playbook

## Objective

Provide a repeatable procedure for responding to a suspected compromised account.

## 1. Detection

Review suspicious authentication alerts.

## 2. Triage

Identify:

- Username
- Source IP
- Destination host
- Login time
- Login type
- Authentication failures

## 3. Investigation

Review:

- Successful logins
- Failed logins
- Account activity
- Process execution
- Network activity
- Other affected systems

## 4. Containment

- Disable or lock the account when appropriate
- Revoke active sessions
- Reset credentials
- Isolate affected endpoint if required

## 5. Eradication

Determine how credentials were compromised and remove the underlying cause.

## 6. Recovery

- Restore account access
- Apply new credentials
- Monitor subsequent authentication activity

## 7. Lessons Learned

Document detection and security improvements.
