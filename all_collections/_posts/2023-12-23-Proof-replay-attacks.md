---
layout: post
title: (ZK) Proof Reuse/Replay Attacks
date: 2023-12-23
categories: ["cryptography"]
---
> I find it weird that there's no discussion around this. This issue is often overlooked and even plagues a few well-known protocols I know.

# NIZK
We all know how the development of *zk-SNARK* in 2012 led to the rapid adoption of zkp technology in the recent years, especially in the blockchain space. The primary reason for this is that zk-SNARKs, along with *Bulletproofs* and *zk-STARKs* produce non-interactive zero-knowledge (NIZK) proofs. A prover can produce a proof without requiring interaction with a verifier. This also implies that anyone can verify a proof given by a prover, at any point in time after the proof is made public.

### Problem with NIZK
The non-interactive property, while very useful, needs to be kept in mind while developing applications. Consider the following scenario:
 - *A* produces a proof and gives to *B* for verification. This proof doesn't tie to *A*'s identity.
 - *B* verifies and confirms that the proof is indeed correct.
 - *B* reuses *A*'s proof and gives it to *C*.
 - *C* verifies and confirms *B*'s proof.

By reusing *A*'s proof, *B* was able to falsely prove something they shouldn't be capable to do. This violates the soundness property of zkp.

To understand using an example, let there be a bounty by *C* which awards the person who proves that they know the pre-image of a hash. Let *A* know the pre-image. *A* produces the proof but leaks the proof to *B*. *B* can report the proof to *C* before *A* and claim the bounty. It's easy to see that this is an example of front-running on blockchain.

# Solution
The only way to prevent this is to let go of strict non-interaction. 1) Either produce zero-knowledge proof interactively or 2) leverage platform (e.g. blockchain) interaction properties to authenticate proofs. 1 can be achieved by either switching to an interactive zkp or simulate interaction by asking the verifier to produce a new random value (for each prover) which will be included in the proof. This is still not fool-proof; a malicious verifier *B* could be reusing the random value from elsewhere and reusing the proof, acting as the middle-man. 2 can be achieved on blockchain using the fact that each transaction has to be signed by the sender. The public key can be a part of the proof so that the verifier can be sure that the person sending the transaction indeed produced the proof themselves. This can be replaced with some other form of unique identity for use on non-blockchain applications (possibly losing zero-knowledge property) or a mechanism using signatures similar to blockchain could be devised. The reward should be tied to the public key; if the reward goes to the relayer, the exercise is useless. This is easy to do on blockchain. For offchain applications, encrypting response using the public key can be one solution.

I am yet to deep-dive into MPC and interactive ZK proofs. I believe ideas from these can potentially offer more elegant and definitive solutions. Or maybe there's already a standard way of solving this and I'm ignorant about it (quick google search didn't show much). I'd be happy to be informed or given pointers if anyone ever reads this.