---
description: A communication protocol.
---

# What Is Sismo?

Sismo leverages zero-knowledge proofs (ZKPs) and privacy-preserving technologies to enable users to aggregate and selectively disclose personal data to applications. By using Sismo Connect, an easy-to-integrate SSO, applications can request access to personal data without compromising user privacy.&#x20;

[Sismo Connect](welcome-to-sismo/what-is-sismo-connect.md) aims to replace non-sovereign SSOs such as Sign in with Google and limited SSOs such as Sign in with Ethereum (SIWE).&#x20;

## Fragmented Digital Identities

Our digital identities are fragmented on the internet. A clear need for **ownership** and **aggregation** has risen**,** with **privacy** as an essential precondition:

* Web2 platforms, such as Twitter, confine our data within their respective silos, preventing us from leveraging our social capital across multiple platforms.
* On web3, privacy concerns create barriers for users and applications. Users hesitate to link their private and public accounts due to the fear of exposing sensitive information, while developers, fully aware of the privacy implications, avoid the concept of data aggregation entirely.
* Until now, no solution existed for the private aggregation of web2 and web3 data in a single place, such as linking a user’s bank account, social media profiles, and onchain history without exposing sensitive information.

Sismo, a communication protocol, leverages privacy-preserving technology to bridge the gap between personal data and applications. It enables users to get the most out of their data while providing app developers with the means to request and utilize it responsibly.

{% hint style="success" %}
With Sismo, you can:

* Aggregate your web2 and web3 data in a private Data Vault that you truly own.
* Selectively disclose your data to apps via Sismo Connect—the crypto-native SSO.
{% endhint %}

<figure><img src=".gitbook/assets/1. Introduction (1).png" alt=""><figcaption></figcaption></figure>

## Data Vault: Aggregate Your Identity

Users aggregate their identity in their sovereign, local and private [Data Vault](welcome-to-sismo/what-is-the-data-vault.md). By doing so, they can start generating ZK Proofs and leverage their data across multiple platforms.

{% hint style="info" %}
The Data Vault is encrypted storage for a user's personal data from various web2 and web3 accounts, credentials, and attestations.
{% endhint %}

These contents of a Data Vault are collectively referred to as Data Sources. The granular pieces of data within Data Sources are characterized as [Data Gems](how-sismo-works/core-components.md#what-are-data-gems-and-data-groups). A Data Gem is a valuable element of a user’s digital identity. Examples of Data Gems include:

* NFT ownership of a specific collection
* GitHub commit to a specific repository
* Participation in a specific DAO governance

The Data Vault acts as a private, local and secure place where users can have a complete overview of their digital identity, providing ownership and control over personal data.

<figure><img src=".gitbook/assets/Aggregation.png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
You can create your own Data Vault and start aggregating your identity [here](https://vault-beta.sismo.io/).
{% endhint %}

## Prove & Verify: Selective Disclosure

To prove ownership of Data Sources or Data Gems, users participate in [proving schemes](how-sismo-works/core-components.md#what-are-proving-schemes). Proving schemes enable users to prove ownership of a Data Source and prove that a Data Source is a member of a [Data Group](how-sismo-works/technical-concepts/data-gems-and-data-groups.md) (e.g. a group of NFT holders, DAO participants or GitHub contributors). This attestation of group membership is called a Data Gem. Data Groups can be created in the [Sismo Factory](https://factory.sismo.io/). The [Sismo Hub](how-sismo-works/core-components.md#what-is-the-sismo-hub), Sismo's open data infrastructure, periodically publishes Data Groups onchain.

{% hint style="info" %}
A proving scheme is a cryptographic method that allows one party (the prover) to prove to another party (the verifier) that a certain statement is true, without revealing how it is true—ensuring privacy.
{% endhint %}

The Data Vault includes the provers, enabling users to generate zero-knowledge proofs (ZKPs) that attest ownership of Data Gems. A user generates a proof to make a claim about Data Gems that they own—which can be subsequently verified.

Verifiers integrated into applications accept proofs from users and ensure their validity—whether in onchain smart contracts or offchain backends. In this sense, users can selectively disclose Data Gems to applications without revealing the associated Data Source.

<figure><img src=".gitbook/assets/Selective Disclosure.png" alt=""><figcaption></figcaption></figure>

## Sismo Connect: The Crypto-Native SSO

Sismo Connect is a crypto-native single sign-on method (SSO) for onchain and offchain apps. Designed with developers in mind, Sismo Connect makes it easy for application developers to request and verify ZK proofs attesting ownership of personal data (i.e. Data Sources and Data Gems).

{% hint style="success" %}
Discover applications leveraging the power of Sismo Connect on the [Sismo App Store](https://spaces.sismo.io/).
{% endhint %}

Integration is simple with just a few lines of code: import the front-end package or React button for data requests, and verify proofs using Sismo’s Solidity or TypeScript package. Once integrated, applications can **request** private and granular data, while users can **authenticate** and **selectively disclose** their personal data.

{% hint style="info" %}
Learn how to integrate Sismo Connect into applications [here](build-with-sismo-connect/overview.md).
{% endhint %}

Applications may require just a fraction of a user’s data or data from multiple accounts for access control or reputation importation. In the example below, zkDrop airdrops an NFT to users that own two Data Gems—a Gitcoin Passport and a Nouns NFT. With the power of Sismo Connect, users can hold these Data Gems in separate wallets without creating immutable links between them.

<figure><img src=".gitbook/assets/Sismo Connect.png" alt=""><figcaption></figcaption></figure>
