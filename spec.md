DID Method Enumeration
==================

**Specification Status:** Draft

**Latest Draft:**
  [https://identity.foundation/did-method-enum](https://identity.foundation/did-method-enum)

Editors:
~ [Sam Curren]()

Participate:
~ [GitHub repo](https://github.com/decentralized-identity/did-method-enum)
~ [File a bug](https://github.com/decentralized-identity/did-method-enum/issues)
~ [Commit history](https://github.com/decentralized-identity/did-method-enum/commits/master)

------------------------------------

## Abstract

There are muliple places in the ecosystem that require expression of which DID methods are supported.

This spec describes a micro data format for the expression of did method support.

Each expression is in the form of a struct/object. Typically, these expressions are represented in a list. See the end for a complete example.

## By Method
The simplest way is to express the method supported

```json=
{
  "method": "web"
}
```

## By Method, with Features

If the DID Method defines feature names in their spec, you can specify the method and include a subset of features of the did method that you support. 

Each feature is expressed as a string. The meaning of the feature strings is specified in the DID method.

Omitting the features list indicates that you support all features of the method.


```json=
{
  "method":"indy",
  "features": ["sovrin", "sovrin:test"]
}

```

```json=
{
  "method": "key",
  "features": ["ed25519-pub", "secp256k1-pub"]
}

```


## By Prefix
When a method name is insufficient and the DID method does not define features, you may need to specify a prefix which limits the matching DIDs further

```json=
{
  "prefix": "did:key:zQ3s"
}
```

You can include mutiple prefix entries in the same list for the same DID method.


## Combined Example

The following example shows common use of the DID Method Support statements in a list

```json=
{
  "did_methods": [
    {
      "method": "web"
    },
    {
      "prefix": "did:key:zQ3s"
    },
    {
      "method": "indy",
      "features": ["sovrin", "sovrin:test"]
    },
    {
      "method": "key",
      "features": ["ed25519-pub", "secp256k1-pub"]
    }
  ]
}
```