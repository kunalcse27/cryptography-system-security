# Types of Attacks

Understanding different types of attacks is crucial in designing secure systems. Attacks are generally classified into two primary categories:

---

## 1. Passive Attacks

Passive attacks involve monitoring or eavesdropping on transmissions to gather information without altering the data.

### 1.1 Eavesdropping (Intercept)
- **Description:** The attacker secretly listens to private communication, such as network traffic or emails, to obtain sensitive information.
- **Example:** Wiretapping a phone line or sniffing network packets.
- **Impact:** Compromises confidentiality, as information is disclosed.

### 1.2 Traffic Analysis
- **Description:** Analyzing the flow of data (even if encrypted) to infer patterns or sensitive details (like communicating parties, frequency, or timing of messages).
- **Example:** Observing which employees communicate most often, inferring company structure.
- **Impact:** May reveal confidential relationships even when message content stays hidden.

#### Diagram: Data Flow in Passive Attack
```
  Sender        <--Eavesdropper--      Receiver
    |-------------------------------------->|
```

Attacker only observes; there’s no modification of data.

---

## 2. Active Attacks

Active attacks involve modifying, disrupting, or fabricating information during transmission. The attacker tries to alter the system’s resources or affect their operation.

### 2.1 Masquerade (Impersonation)
- **Description:** Attacker pretends to be a legitimate user to gain unauthorized access.
- **Example:** Attacker uses stolen credentials to log in as a user.

### 2.2 Replay Attack
- **Description:** Attacker records a valid transmission and retransmits it later to gain unauthorized advantages.
- **Example:** Reusing an old secure login message to access an account.

### 2.3 Message Modification
- **Description:** Altering a legitimate message in transit to change its meaning or effect.
- **Example:** Changing the amount or recipient in a funds transfer message.

### 2.4 Denial of Service (DoS)
- **Description:** Prevents legitimate users from accessing services/resources by overwhelming the system.
- **Example:** Flooding a website with traffic until it becomes inaccessible.

#### Diagram: Modification in Active Attack

```
  Sender       ---> [Attacker alters data] --->        Receiver
    |-------------------X---------------------->|
```
X = point where attacker modifies the message.

---

## 3. Comparison Table: Passive vs Active Attacks

| Characteristic     | Passive Attack               | Active Attack                     |
|--------------------|-----------------------------|-----------------------------------|
| Action             | Eavesdrops only             | Modifies or disrupts data         |
| Data Manipulation  | No                          | Yes                               |
| Detection          | Difficult                   | Easier (may cause anomalies)      |
| Examples           | Eavesdropping, traffic analysis | Masquerade, replay, DoS      |
| Primary Goal       | Gather information          | Alter, disrupt, or fabricate data |

---

## 4. Conclusion

- **Passive Attacks** focus on information gathering and breach confidentiality.
- **Active Attacks** are more damaging, as they can compromise integrity and availability in addition to confidentiality.
- Security mechanisms are required to detect and defend against both types.

---
