---
layout: post
title: "Creating a Self-Signed Certificate for Identity Provider"
date: 2017-11-18 09:54:16 +0000
comments: true
categories: [HowTo, PowerShell, Identity Provider, Tips]
---

I’d recently had to create a self-signed certificate for use in IdentityProvider4 and was coming up against problems when using the default options with New-SelfSignedCertificate PS module.

Identity Server was throwing "CryptographicException: Invalid provider type specified" and I had ensured the user account had access so it should have been all good. After a little bit of digging it turned out the private keys were not accessible from .NET. David Christiansen’s [blog post](http://blog.davidchristiansen.com/2016/05/521/) helped me track down the issue but with a little more research I ended up with the following PowerShell to create a working certificate avoiding additional steps I didnt understand ;).
<!--more-->

{% codeblock %}
$idSrvCertificate = New-SelfSignedCertificate `
    -Subject "CN=MyIdentityProviderCert" `
    -FriendlyName "Identity Server Token Signing" `
    -CertStoreLocation "cert:LocalMachine\My" `
    -KeyAlgorithm RSA `
    -KeySpec Signature `
    -KeyLength 2048 `
    -KeyUsage DigitalSignature, KeyEncipherment, DataEncipherment, CertSign `
    -NotBefore (Get-Date) `
    -NotAfter (Get-Date).AddYears(5);

$username = [System.Security.Principal.WindowsIdentity]::GetCurrent().Name;

$keyname = (((Get-ChildItem cert:\LocalMachine\my | Where-Object {$_.thumbprint -like $idSrvCertificate.ThumbPrint}).PrivateKey).CspKeyContainerInfo).UniqueKeyContainerName;

$keypath = $env:ProgramData + "\Microsoft\Crypto\RSA\MachineKeys\";
$fullpath = $keypath + $keyname;
icacls $fullpath /grant $username`:RX;
{% endcodeblock %}

 In addition to creating the certificate it will also ensure the current user has read access to the private keys avoiding the need to run VS elevated when developing, this last part could obviously be extracted and reused for your application pool if running Identity Server in IIS.