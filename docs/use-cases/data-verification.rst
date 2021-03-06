#############
Verify data
#############

.. note:: **Version 3** of SDK is used in the following code samples.

Recipient wants to make sure that received data has been sent from a secure source and hasn’t been changed during transport.

.. image:: ../images/VerifyUseCase.png
  :width: 50 %

**Sender and recipient create Virgil accounts with a pair of asymmetric keys**:

- public key on Virgil cloud in Keys service;

.. code:: 

  byte[] publicKey;
  byte[] privateKey;
  
  using (var keyPair new VirgilKeyPair())
  {
      publicKey = keyPair.PublicKey();
      privateKey = keyPair.PrivateKey();
  }


- private key on Virgil cloud in Private Keys service;

.. code:: 

  var password = Encoding.UTF8.GetBytes("my_password-:)")
  
  using (var keyPair = new VirgilKeyPair(password))
  {
      ...
  }

- or private key locally.

**Sender signs the data with his private key in Virgil crypto library.**

.. code:: 

  byte[] sign;
  using (var signer = new VirgilSigner())
  {
      sign = signer.Sign(dataToSign, privateKey);
  }

**Sender transfers the data, his digital signature and UDID to a recipient.**

**Recipient (or any person) verifies data integrity using the digital signature and sender’s public key in Virgil crypto library.**

.. code:: 

  bool isValid;
  using (var signer = new VirgilSigner())
  {
      isValid = signer.Verify(dataToSign, sign, publicKey);
  }
