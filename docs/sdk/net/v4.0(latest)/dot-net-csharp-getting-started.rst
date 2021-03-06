Getting started
===============

The goal of Virgil .NET/C# SDK Documentation is to give a developer the knowledge and understanding required to implement security into his application using Virgil Security system.

Virgil SDK is a communication gateway between your application and :doc:`../../../services/services`. 

Setting up your project
-----------------------

The Virgil SDK is provided as a package named **Virgil.SDK**. The package is distributed via NuGet package management system.

Target frameworks
~~~~~~~~~~~~~~~~~

-  .NET Framework 4.0 and newer.

Prerequisites
~~~~~~~~~~~~~

-  Visual Studio 2013 RTM Update 2 and newer (Windows)
-  Xamarin Studio 5.x and newer (Windows, Mac)
-  MonoDevelop 4.x and newer (Windows, Mac, Linux)

Installing the package
~~~~~~~~~~~~~~~~~~~~~~

1. Use NuGet Package Manager (Tools -> Library Package Manager -> Package Manager Console)
2. Run

::

	PM> Install-Package Virgil.SDK

User and App Credentials
------------------------

When you register an application on Virgil developer's `dashboard <https://developer.virgilsecurity.com/dashboard>`_, we provide you with an ``appID``, ``appKey`` and ``accessToken``.

-  ``appID`` uniquely identifies your application in our services, it is also used to identify the Public key generated in a pair with ``appKey``. Example:
   ``af6799a2f26376731abb9abf32b5f2ac0933013f42628498adb6b12702df1a87``

-  ``appKey`` is a Private key that is used to perform creation and revocation of **Virgil Cards** (Public key) in Virgil services. Also the ``appKey`` can be used for cryptographic operations to take part in application logic. The ``appKey`` is generated at the time of application creation and must be saved in secure place.

-  ``accessToken`` is a unique string value that provides an authenticated secure access to the Virgil services and is passed with each API call. The *accessToken* also allows the API to associate your app’s requests with your Virgil developer’s account.

Connecting to Virgil
--------------------

Before you can make use of any Virgil services features in your app, you must initialize ``VirgilClient`` class. 

You use the ``VirgilClient`` object to get access to create, revoke and search for **Virgil Cards** (Public keys).

Initializing an API Client
~~~~~~~~~~~~~~~~~~~~~~~~~~

To create an instance of ``VirgilClient`` class, just call its constructor with your application **accessToken** you generated on developer's dashboard.

Namespace: ``Virgil.SDK.Client``

.. code-block:: csharp
    :linenos:

    var client = new VirgilClient("[YOUR_ACCESS_TOKEN_HERE]");

you can also customize initialization using your own parameters

.. code-block:: csharp
    :linenos:

    var parameters = new VirgilClientParams("[YOUR_ACCESS_TOKEN_HERE]");

    parameters.SetCardsServiceAddress("https://cards.virgilsecurity.com");
    parameters.SetReadOnlyCardsServiceAddress("https://cards-ro.virgilsecurity.com");
    parameters.SetIdentityServiceAddress("https://identity.virgilsecurity.com");

    var client = new VirgilClient(parameters);

Initializing Crypto
~~~~~~~~~~~~~~~~~~~

``VirgilCrypto`` class provides cryptographic operations in applications, such as hashing, signature generation and verification, and encryption and decryption.

Namespace: ``Virgil.SDK.Cryptography``

.. code-block:: csharp
    :linenos:

    var crypto = new VirgilCrypto();
