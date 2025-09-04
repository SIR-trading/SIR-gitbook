---
description: Towards a Secure and Immutable Protocol
---

# 🧪 Beta Period

For the safety of its users, the protocol will launch in beta. The protocol has 4 distinct states:

1. <mark style="background-color:green;">**Unstoppable:**</mark> The ultimate state, marking the end of the beta period. Here, all parameters are fixed, leaving no room for adjustments. Transitioning to this state signifies that the protocol is fully operational and irreversible, with any persisting issues becoming permanent fixtures. This state is achieved exclusively from the Training Wheels state.
2. <mark style="background-color:blue;">**Training Wheels:**</mark> The initial state during beta, where protocol fees can be modified. This flexibility is crucial for optimizing the fee structure based on real-world data and feedback. The protocol can revert to this state from Emergency but aims to advance to Unstoppable.
3. <mark style="background-color:orange;">**Emergency:**</mark> Activated in response to detected bugs or exploits, this state allows for the suspension of new deposits (minting of TEA or APE) while permitting withdrawals (burning of TEA or APE). It's a containment measure designed to mitigate damage, accessible only from Training Wheels.
4. <mark style="background-color:red;">**Shutdown:**</mark> The final measure if issues identified in the Emergency state remain unresolved after 20 days. In Shutdown, the protocol enables the withdrawal of any funds left by the owner of the contract, safeguarding user assets. The 20-day waiting period is a safety net against potential misuse by the owner.

<figure><img src="../.gitbook/assets/pdfresizer.com-pdf-crop (1) (4).svg" alt=""><figcaption><p>SIR protocol state transition diagram</p></figcaption></figure>
