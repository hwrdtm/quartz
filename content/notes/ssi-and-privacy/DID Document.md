---
title: DID Document
---
A DID Document is a user's extended profile that's connected to their DID. A DID Document is a mini-profile for its DID subject. They are JSON files that serve as a self-contained representation of the DID and provides metadata and cryptographic material associated with the DID.

**DID Documents describe how to interact with the DID subject and contains information that allows others to verify the authenticity and integrity of the DID's information. The document includes things like the DID subject's public keys, authentication and verification methods, as well as service endpoints, such as [DWNs](https://developer.tbd.website/docs/web5/learn/decentralized-web-nodes), that reference the locations of the subject’s data.**

# Fields

The only required field is the `id` field which corresponds to the DID. There may be other fields such as authentication material, encryption key material, and pointers to your DWN.

# Retrieval

Retrieving a DID document is sometimes referred to as "resolving a DID" to their mini-profile (DID Document).

There are many ways to resolve DIDs to their DID documents. For example, you can use Web5's DID SDK to resolve via Web5's own implementation of a resolver, or you can make network requests to [DIF's Universal Resolver](https://dev.uniresolver.io/) outside of Web5.

# Management

Managing a DID Document is essential to maintain its integrity, relevance, and security. In Web5, a DID subject can indicate to their authorized [user agent](https://developer.tbd.website/docs/web5/learn/agents) (e.g., wallet) a change they'd like to make, and that agent will determine if the DID Document needs to be modified, and if so, will do so on the subject's behalf.

# Example

```json
{
  "id": "did:ion:EiBMIz-Hhom0_8EUaWLuscD08Riy0Fo5vp8mCXxszy5Gfg:eyJkZWx0YSI6eyJwYXRjaGVzIjpbeyJhY3Rpb24iOiJyZXBsYWNlIiwiZG9jdW1lbnQiOnsicHVibGljS2V5cyI6W3siaWQiOiJhdXRoeiIsInB1YmxpY0tleUp3ayI6eyJjcnYiOiJzZWNwMjU2azEiLCJrdHkiOiJFQyIsIngiOiJ3endxSEY3cEtzS3dkR3NBNkhpS0dyUGRaQ0FoYW9oeGxJS1JraDhGWjZNIiwieSI6ImVsY0tHbnpMTjNsVnpYWHV6YUk3WWFrWVI3MXBxNnBMbzNUNFRVaERJYXMifSwicHVycG9zZXMiOlsiYXV0aGVudGljYXRpb24iXSwidHlwZSI6Ikpzb25XZWJLZXkyMDIwIn0seyJpZCI6ImVuYyIsInB1YmxpY0tleUp3ayI6eyJjcnYiOiJzZWNwMjU2azEiLCJrdHkiOiJFQyIsIngiOiJuOVRDSEtNZS04Z1J6cl9YMC1XZVF1VzlyM1VGNlhZd1pscEtZTnVVdzhBIiwieSI6Im5UTEgxUS1OR05OMy0ySkxyWW9PMnNDSEdUcndpMXVqR0dNSEdKV3ZSNVkifSwicHVycG9zZXMiOlsia2V5QWdyZWVtZW50Il0sInR5cGUiOiJKc29uV2ViS2V5MjAyMCJ9XSwic2VydmljZXMiOlt7ImlkIjoiZHduIiwic2VydmljZUVuZHBvaW50Ijp7Im1lc3NhZ2VBdXRob3JpemF0aW9uS2V5cyI6WyIjYXV0aHoiXSwibm9kZXMiOlsiaHR0cHM6Ly9kd24udGJkZGV2Lm9yZy9kd24xIiwiaHR0cHM6Ly9kd24udGJkZGV2Lm9yZy9kd24yIl0sInJlY29yZEVuY3J5cHRpb25LZXlzIjpbIiNlbmMiXX0sInR5cGUiOiJEZWNlbnRyYWxpemVkV2ViTm9kZSJ9XX19XSwidXBkYXRlQ29tbWl0bWVudCI6IkVpRDJYTV9mRzQ2eFI4NDJVTjRzMTFOTU80LTEzbkwxdXdUVko1cGVVWFFicmcifSwic3VmZml4RGF0YSI6eyJkZWx0YUhhc2giOiJFaUJWLVQyU1dwWGI2bldwVlpyQXUwYTF3Q2hQdS1tRXJMaWtORWpSZ3VQa2hBIiwicmVjb3ZlcnlDb21taXRtZW50IjoiRWlBcGRSR1U4X2JkQ3oyZFpfR1R3QnZGOWw1ZXNRUWFqbXRjN3REdzcxTUUyQSJ9fQ",
  "@context": [
    "https://www.w3.org/ns/did/v1",
    {
      "@base": "did:ion:EiBMIz-Hhom0_8EUaWLuscD08Riy0Fo5vp8mCXxszy5Gfg:eyJkZWx0YSI6eyJwYXRjaGVzIjpbeyJhY3Rpb24iOiJyZXBsYWNlIiwiZG9jdW1lbnQiOnsicHVibGljS2V5cyI6W3siaWQiOiJhdXRoeiIsInB1YmxpY0tleUp3ayI6eyJjcnYiOiJzZWNwMjU2azEiLCJrdHkiOiJFQyIsIngiOiJ3endxSEY3cEtzS3dkR3NBNkhpS0dyUGRaQ0FoYW9oeGxJS1JraDhGWjZNIiwieSI6ImVsY0tHbnpMTjNsVnpYWHV6YUk3WWFrWVI3MXBxNnBMbzNUNFRVaERJYXMifSwicHVycG9zZXMiOlsiYXV0aGVudGljYXRpb24iXSwidHlwZSI6Ikpzb25XZWJLZXkyMDIwIn0seyJpZCI6ImVuYyIsInB1YmxpY0tleUp3ayI6eyJjcnYiOiJzZWNwMjU2azEiLCJrdHkiOiJFQyIsIngiOiJuOVRDSEtNZS04Z1J6cl9YMC1XZVF1VzlyM1VGNlhZd1pscEtZTnVVdzhBIiwieSI6Im5UTEgxUS1OR05OMy0ySkxyWW9PMnNDSEdUcndpMXVqR0dNSEdKV3ZSNVkifSwicHVycG9zZXMiOlsia2V5QWdyZWVtZW50Il0sInR5cGUiOiJKc29uV2ViS2V5MjAyMCJ9XSwic2VydmljZXMiOlt7ImlkIjoiZHduIiwic2VydmljZUVuZHBvaW50Ijp7Im1lc3NhZ2VBdXRob3JpemF0aW9uS2V5cyI6WyIjYXV0aHoiXSwibm9kZXMiOlsiaHR0cHM6Ly9kd24udGJkZGV2Lm9yZy9kd24xIiwiaHR0cHM6Ly9kd24udGJkZGV2Lm9yZy9kd24yIl0sInJlY29yZEVuY3J5cHRpb25LZXlzIjpbIiNlbmMiXX0sInR5cGUiOiJEZWNlbnRyYWxpemVkV2ViTm9kZSJ9XX19XSwidXBkYXRlQ29tbWl0bWVudCI6IkVpRDJYTV9mRzQ2eFI4NDJVTjRzMTFOTU80LTEzbkwxdXdUVko1cGVVWFFicmcifSwic3VmZml4RGF0YSI6eyJkZWx0YUhhc2giOiJFaUJWLVQyU1dwWGI2bldwVlpyQXUwYTF3Q2hQdS1tRXJMaWtORWpSZ3VQa2hBIiwicmVjb3ZlcnlDb21taXRtZW50IjoiRWlBcGRSR1U4X2JkQ3oyZFpfR1R3QnZGOWw1ZXNRUWFqbXRjN3REdzcxTUUyQSJ9fQ"
    }
  ],
  "service": [
    {
      "id": "#dwn",
      "type": "DecentralizedWebNode",
      "serviceEndpoint": {
        "messageAuthorizationKeys": ["#authz"],
        "nodes": ["https://dwn.tbddev.org/dwn1", "https://dwn.tbddev.org/dwn2"],
        "recordEncryptionKeys": ["#enc"]
      }
    }
  ],
  "verificationMethod": [
    {
      "id": "#authz",
      "controller": "did:ion:EiBMIz-Hhom0_8EUaWLuscD08Riy0Fo5vp8mCXxszy5Gfg:eyJkZWx0YSI6eyJwYXRjaGVzIjpbeyJhY3Rpb24iOiJyZXBsYWNlIiwiZG9jdW1lbnQiOnsicHVibGljS2V5cyI6W3siaWQiOiJhdXRoeiIsInB1YmxpY0tleUp3ayI6eyJjcnYiOiJzZWNwMjU2azEiLCJrdHkiOiJFQyIsIngiOiJ3endxSEY3cEtzS3dkR3NBNkhpS0dyUGRaQ0FoYW9oeGxJS1JraDhGWjZNIiwieSI6ImVsY0tHbnpMTjNsVnpYWHV6YUk3WWFrWVI3MXBxNnBMbzNUNFRVaERJYXMifSwicHVycG9zZXMiOlsiYXV0aGVudGljYXRpb24iXSwidHlwZSI6Ikpzb25XZWJLZXkyMDIwIn0seyJpZCI6ImVuYyIsInB1YmxpY0tleUp3ayI6eyJjcnYiOiJzZWNwMjU2azEiLCJrdHkiOiJFQyIsIngiOiJuOVRDSEtNZS04Z1J6cl9YMC1XZVF1VzlyM1VGNlhZd1pscEtZTnVVdzhBIiwieSI6Im5UTEgxUS1OR05OMy0ySkxyWW9PMnNDSEdUcndpMXVqR0dNSEdKV3ZSNVkifSwicHVycG9zZXMiOlsia2V5QWdyZWVtZW50Il0sInR5cGUiOiJKc29uV2ViS2V5MjAyMCJ9XSwic2VydmljZXMiOlt7ImlkIjoiZHduIiwic2VydmljZUVuZHBvaW50Ijp7Im1lc3NhZ2VBdXRob3JpemF0aW9uS2V5cyI6WyIjYXV0aHoiXSwibm9kZXMiOlsiaHR0cHM6Ly9kd24udGJkZGV2Lm9yZy9kd24xIiwiaHR0cHM6Ly9kd24udGJkZGV2Lm9yZy9kd24yIl0sInJlY29yZEVuY3J5cHRpb25LZXlzIjpbIiNlbmMiXX0sInR5cGUiOiJEZWNlbnRyYWxpemVkV2ViTm9kZSJ9XX19XSwidXBkYXRlQ29tbWl0bWVudCI6IkVpRDJYTV9mRzQ2eFI4NDJVTjRzMTFOTU80LTEzbkwxdXdUVko1cGVVWFFicmcifSwic3VmZml4RGF0YSI6eyJkZWx0YUhhc2giOiJFaUJWLVQyU1dwWGI2bldwVlpyQXUwYTF3Q2hQdS1tRXJMaWtORWpSZ3VQa2hBIiwicmVjb3ZlcnlDb21taXRtZW50IjoiRWlBcGRSR1U4X2JkQ3oyZFpfR1R3QnZGOWw1ZXNRUWFqbXRjN3REdzcxTUUyQSJ9fQ",
      "type": "JsonWebKey2020",
      "publicKeyJwk": {
            "crv": "secp256k1",
            "kty": "EC",
            "x": "wzwqHF7pKsKwdGsA6HiKGrPdZCAhaohxlIKRkh8FZ6M",
            "y": "elcKGnzLN3lVzXXuzaI7YakYR71pq6pLo3T4TUhDIas"
        }
    },
    {
      "id": "#enc",
      "controller": "did:ion:EiBMIz-Hhom0_8EUaWLuscD08Riy0Fo5vp8mCXxszy5Gfg:eyJkZWx0YSI6eyJwYXRjaGVzIjpbeyJhY3Rpb24iOiJyZXBsYWNlIiwiZG9jdW1lbnQiOnsicHVibGljS2V5cyI6W3siaWQiOiJhdXRoeiIsInB1YmxpY0tleUp3ayI6eyJjcnYiOiJzZWNwMjU2azEiLCJrdHkiOiJFQyIsIngiOiJ3endxSEY3cEtzS3dkR3NBNkhpS0dyUGRaQ0FoYW9oeGxJS1JraDhGWjZNIiwieSI6ImVsY0tHbnpMTjNsVnpYWHV6YUk3WWFrWVI3MXBxNnBMbzNUNFRVaERJYXMifSwicHVycG9zZXMiOlsiYXV0aGVudGljYXRpb24iXSwidHlwZSI6Ikpzb25XZWJLZXkyMDIwIn0seyJpZCI6ImVuYyIsInB1YmxpY0tleUp3ayI6eyJjcnYiOiJzZWNwMjU2azEiLCJrdHkiOiJFQyIsIngiOiJuOVRDSEtNZS04Z1J6cl9YMC1XZVF1VzlyM1VGNlhZd1pscEtZTnVVdzhBIiwieSI6Im5UTEgxUS1OR05OMy0ySkxyWW9PMnNDSEdUcndpMXVqR0dNSEdKV3ZSNVkifSwicHVycG9zZXMiOlsia2V5QWdyZWVtZW50Il0sInR5cGUiOiJKc29uV2ViS2V5MjAyMCJ9XSwic2VydmljZXMiOlt7ImlkIjoiZHduIiwic2VydmljZUVuZHBvaW50Ijp7Im1lc3NhZ2VBdXRob3JpemF0aW9uS2V5cyI6WyIjYXV0aHoiXSwibm9kZXMiOlsiaHR0cHM6Ly9kd24udGJkZGV2Lm9yZy9kd24xIiwiaHR0cHM6Ly9kd24udGJkZGV2Lm9yZy9kd24yIl0sInJlY29yZEVuY3J5cHRpb25LZXlzIjpbIiNlbmMiXX0sInR5cGUiOiJEZWNlbnRyYWxpemVkV2ViTm9kZSJ9XX19XSwidXBkYXRlQ29tbWl0bWVudCI6IkVpRDJYTV9mRzQ2eFI4NDJVTjRzMTFOTU80LTEzbkwxdXdUVko1cGVVWFFicmcifSwic3VmZml4RGF0YSI6eyJkZWx0YUhhc2giOiJFaUJWLVQyU1dwWGI2bldwVlpyQXUwYTF3Q2hQdS1tRXJMaWtORWpSZ3VQa2hBIiwicmVjb3ZlcnlDb21taXRtZW50IjoiRWlBcGRSR1U4X2JkQ3oyZFpfR1R3QnZGOWw1ZXNRUWFqbXRjN3REdzcxTUUyQSJ9fQ",
      "type": "JsonWebKey2020",
      "publicKeyJwk": {
            "crv": "secp256k1",
            "kty": "EC",
            "x": "n9TCHKMe-8gRzr_X0-WeQuW9r3UF6XYwZlpKYNuUw8A",
            "y": "nTLH1Q-NGNN3-2JLrYoO2sCHGTrwi1ujGGMHGJWvR5Y"
        }
    }
  ]
}
```

# Resources

https://developer.tbd.website/docs/web5/learn/did_document/
