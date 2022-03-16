Short overview
=======

We are cardanonymous. The aim of our opensource projects is to create the possibility to anonymize yourself on the Cardano network. We will build a P2P mixer using mixing nets (which are used in E-voting) and El Gamal encryption. The software stack will be build with Haskell and should run alongside a full node for complete anonymity (using a trusted vpn for the node is advisable).

E-voting
========
Without going too much in detail a mixing net is a group of parties that shuffles and decrypts set of ciphers. A common use case for this is in e-voting. Here the mixer nodes use an asymmetric homomorfic encryption scheme and publish their public key to everyone. A voter then combines all these public keys and encrypts their vote with this public key. Note that since the vote is encrypted with the combined key it can only be decrypted piece wise by the mixer nodes. The first mixer nodes gather the encrypted voted and re-randomize the ciphers. Then it decrypts his part of the message and sends it to the next node. This is repeated until the last node upon the ciphers will be fully shuffled multiple times and decrypted. The votes can now be publicly counted while preserving the anonymity of the voter. Only if one knows all the private keys of the mixers they can revert a vote to the associated voter.

Note that in this setup the mixer nodes are predetermined trusted parties. In the case of adversarial behavior this protocol would halt or even can be manipulated. By leveraging the blockchain we can take this a step further and create a strong trust less instance of the mixing nets protocol. The main addition the blockchain gives us is a censorship resistance and penalties when adversarial behavior is in play.

El Gamal and non-interactive zero knowledge proofs (NIZK)
========
The chosen encryption scheme for this project is El Gamal. This is a widely used asymmetric encryption method based on the Diffie-Hellman assumption. The main reason this scheme is chosen is because the main verification of these shuffles is done on-chain where calculation need to be performed. These calculations need to be relatively cheap. Also, this scheme naturally extends to non interactive zero knowledge proofs. More precisely, it can provide proof that one has a private key associated to a public key. It also can provide a proof of correct decryption given a public key and an encrypted message. Lastly and most importantly, it can provide a proof that a shuffle, as mentioned above, is performed correctly.

The Mixer
========
Now the idea of the mixer is to use this e-voting scheme in combination with the El Gamal encryption scheme and its NIZK to mix a same amount of Ada and a set of destination addresses that can claim those funds. A simplified way of viewing the protocol; votes are replaced with a destination addresses and mixer nodes are all parties that are involved in the current shuffle of funds. Each party has the opportunity to shuffle the set of ciphers at least once. In case of a timeout a party may lose its right of shuffle. Note that if each party shuffles at least once it is certain that know one can tie the results of the decryptes ciphers to the initial set of ciphers. So even if all parties except you are adversarial, the shuffle is still guaranteed to be untraceable.

Contact
========

You can reach us via the following email address: cardanonymous-git@protonmail.com. Want to anonymously donate to this project, see our git repo on that.

