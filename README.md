Keygraph
========

What it's all about
-------------------

Keygraph is a project to expand GPG, making keys more useful and easier to verify. Our aim is to add three things to GPG. Two of them are all about keys.

* * * * *

[**Attestations**](https://github.com/keygraph/project/wiki/Attestation) are verifiable statements that the same person controls both a this key and that other account. Think of posting a signed statement in a Github gist, and adding a special UID to your GPG key. Someone who looks at the key can check the gist, and someone who looks at the gist, can check the signature.

With attestations, you might not need to do the whole key-signing party web-of-trust game. If you only need to be fairly confident about who owns a key, check the attestations. Does the person who controls this key also control the Twitter, Github, and Facebook accounts you know your friend uses? This might just be their key.

* * * * *

[**Claims**](https://github.com/keygraph/project/wiki/Claim) are more sorts of things to put in GPG UIDs. GPG only knows about names, email addresses and a few other things. That's so nineties. What about IM, or phone numbers, or a location, or anything else you might want to put on your Facebook page or your Twitter profile? That's what claims are for.

Claims take GPG from an email encryption system to a general identity-proof and contact-info system. If you trust someone's key, you might be able to send them an IM and validate your OTR session with their GPG key. Maybe you don't need crypto, you just want to know where to mail them a package: good thing they added a mailing address to their key.

* * * * *

The last thing we want to improve is **keyservers**. If GPG UIDs are from the nineties, then keyservers are prehistoric. We want to improve the web interface for keyservers so that they're usable by humans. The keyserver page for a key should show the owner's name, photo, and other claims they've attached to their key. It should show which attestations the keyserver was able to verify, and the names and photos for anyone who's certified their key.

If you've ever looked at a keyserver dump, you know that they're full of badly-formed keys, things that are revoked, or broken, or otherwise unusable. Keyservers should ignore things that don't parse. When you browse the keys on a server — whether on the web or in the terminal — you should only see valid, working keys. If you ask for updates on a recently-expired or revoked key, you should learn about the changes, but only if you ask.


How to do it
------------

We're building Keygraph in three parts:

At the core of all these changes are some [specifications](https://github.com/keygraph/social-attributes). We need to be very careful when specifying how attestations work, to make sure that the really are proofs, and really do prove the thing they claim. We need to write different specifications for different services. Compressing an attestation into a Tweet is very different from putting something in the DNS.

There's a desktop [client](https://github.com/keygraph/keygraph-client), a wrapper for GPG. It'll generate attestations and claims, post public statements, and verify the attestations of others.

There's a modified [keyserver](https://github.com/keygraph/keygraph-server), which'll federate with the rest of the keyserver network. It'll provide an improved web UI, and ignore broken and malformed keys.
