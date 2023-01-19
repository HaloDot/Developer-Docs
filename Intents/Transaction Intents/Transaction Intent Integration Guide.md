# Transaction Intent Integration Guide #

## Contents ##

- [Transaction Intent Integration Guide](#transaction-intent-integration-guide)
  - [Contents](#contents)
  - [1. Intent Integration Methods](#1-intent-integration-methods)
  - [2. Android Intents Mechanism](#2-android-intents-mechanism)


## 1. Intent Integration Methods ##

The Halo Dot Link application currently provides different mechanisms to integrate our payments solution depending on your use-case. Have a look at the image below as a guideline:

![Integration Mechanisms](../assets/Android%20vs%20deeplinking.png)

This guide will walk you through integration for each mechanism. If you are trying to do a TT3 intent integration, refer to the [TT3 Integration Guide](../TT3%20Intents/TT3%20Intent%20Integration%20Guide.md).

## 2. Android Intents Mechanism ##

This section provides guidance on how to integrate your calling application with the Halo Dot Go app through the Android Intent Mechanism. This is an easy three-step process:

1. Retrieve your `Merchant ID` and `API Key` from the Merchant Portal.
2. Retrieve a `Transaction ID` and payment `JWT`from the Halo Backend.
3. Send an Intent Request to the Halo Dot Go application.

**Retrieve details from the Merchant Portal**

