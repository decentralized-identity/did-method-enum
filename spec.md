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

Mulitple listed features function as an OR, indicating that DIDs matching any of the included features are supported.

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


## DID Method Feature Definition

DID Methods may define feature names within their documentation. If they do, they can be used to specify features not easiliy expressed via a prefix match.

The only requirement of feature name definition is that it precisely defines how to interpret the feature names supported by the DID Method. There are two common forms for this: a list of defined feature names, or interpretation instructions. Examples of both of these possibilities are shown below.

### Defined List of Feature Names Example

This DID Method defines two feature names, which must be named:

`FeatureA`:
DIDs within this method that do 1, 2, and 3 are included in this feature.

`FeatureB`:
DIDs within this method that do 4, 5, and 6 are included in this feature.


### Interpretation Instructions Example

The features for this DID Method follow one of the following forms: `<part1>:<part2>` or `<part>`. Part 2 is optional, and defaults to 'all' during evaluation. If Part 2 is not present, the delimiting `:` will also not be present.

The value for Part 1 indicates that DIDs must...

The value for Part 2 indicates that DIDs must...

